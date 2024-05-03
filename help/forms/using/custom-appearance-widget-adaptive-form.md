---
title: Creare aspetti personalizzati per i campi del modulo adattivo
description: Personalizza l’aspetto dei componenti pronti all’uso in Adaptive Forms.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
docset: aem65
exl-id: 770e257a-9ffd-46a4-9703-ff017ce9caed
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '1702'
ht-degree: 0%

---

# Creare aspetti personalizzati per i campi del modulo adattivo{#create-custom-appearances-for-adaptive-form-fields}

## Introduzione {#introduction}

I moduli adattivi utilizzano [framework aspetto](/help/forms/using/introduction-widgets.md) per aiutarti a creare aspetti personalizzati per i campi del modulo adattivo e fornire un’esperienza utente diversa. Ad esempio, sostituisci i pulsanti di scelta e le caselle di controllo con pulsanti di attivazione o utilizza plug-in jQuery personalizzati per limitare gli input degli utenti in campi come numeri di telefono o ID e-mail.

Questo documento spiega come utilizzare un plug-in jQuery per creare queste esperienze alternative per i campi del modulo adattivo. Inoltre, mostra un esempio per creare un aspetto personalizzato affinché il componente campo numerico venga visualizzato come un indicatore numerico o un cursore.

Esaminiamo innanzitutto i termini e i concetti chiave utilizzati in questo articolo.

**Aspetto** Si riferisce allo stile, all’aspetto e all’organizzazione dei vari elementi di un campo modulo adattivo. Di solito include un’etichetta, un’area interattiva per fornire input, un’icona di aiuto e descrizioni brevi e lunghe del campo. La personalizzazione dell’aspetto illustrata in questo articolo è applicabile all’aspetto dell’area di input del campo.

**Plug-in jQuery** Fornisce un meccanismo standard, basato sul framework del widget jQuery, per implementare un aspetto alternativo.

**ClientLib** Sistema di librerie lato client nell’elaborazione lato client dell’AEM gestito da codice JavaScript e CSS complesso. Per ulteriori informazioni, consulta Utilizzo delle librerie lato client.

**Archetipo** Toolkit per modelli di progetto Maven definito come modello o modello originale per i progetti Maven. Per ulteriori informazioni, consulta Introduzione agli archetipi.

**Controllo utente** Fa riferimento all’elemento principale in un widget che contiene il valore del campo e viene utilizzato dal framework dell’aspetto per associare l’interfaccia utente del widget personalizzato al modello di modulo adattivo.

## Passaggi per creare un aspetto personalizzato {#steps-to-create-a-custom-appearance}

Per creare un aspetto personalizzato, effettua le seguenti operazioni:

1. **Creare un progetto**: crea un progetto Maven che genera un pacchetto di contenuti da distribuire su AEM.
1. **Estendere una classe widget esistente**: estendere una classe widget esistente ed eseguire l&#39;override delle classi richieste.
1. **Creare una libreria client**: crea un `clientLib: af.customwidget` e aggiungi i file JavaScript e CSS richiesti.

1. **Creare e installare il progetto**: crea il progetto Maven e installa il pacchetto di contenuti generato su AEM.
1. **Aggiornare il modulo adattivo**: aggiorna le proprietà del campo modulo adattivo per utilizzare l’aspetto personalizzato.

### Creare un progetto {#create-a-project}

Un archetipo Maven è un punto di partenza per la creazione di un aspetto personalizzato. I dettagli dell’archetipo da utilizzare sono i seguenti:

* **Archivio**: https://repo1.maven.org/maven2/com/adobe/
* **ID artefatto**: custom-APPEARance-archetype
* **ID gruppo**: com.adobe.aemforms
* **Versione**: 1.0.4

Esegui il comando seguente per creare un progetto locale basato sull’archetipo:

`mvn archetype:generate -DarchetypeRepository=https://repo1.maven.org/maven2/com/adobe/ -DarchetypeGroupId=com.adobe.aemforms -DarchetypeArtifactId=custom-appearance-archetype -DarchetypeVersion=1.0.4`

Il comando scarica i plug-in Maven e le informazioni di archetipo dall’archivio e genera un progetto basato sulle seguenti informazioni:

* **groupId**: ID gruppo utilizzato dal progetto Maven generato
* **artifactId**: ID artefatto utilizzato dal progetto Maven generato.
* **version**: versione per il progetto Maven generato.
* **pacchetto**: pacchetto utilizzato per la struttura del file.
* **artifactName**: nome dell’artefatto del pacchetto AEM generato.
* **packageGroup**: gruppo di pacchetti del pacchetto AEM generato.
* **widgetName**: nome dell&#39;aspetto utilizzato come riferimento.

Il progetto generato ha la seguente struttura:

```java
─<artifactId>

 └───src

     └───main

         └───content

             └───jcr_root

                 └───etc

                     └───clientlibs

                         └───custom

                             └───<widgetName>

                                 ├───common [client library - af.customwidgets which encapsulates below clientLibs]

                                 ├───integration [client library - af.customwidgets.<widgetName>_widget which contains template files for integrating a third-party plugin with Adaptive Forms]

                                 │   ├───css

                                 │   └───javascript

                                 └───jqueryplugin [client library - af.customwidgets.<widgetName>_plugin which holds the third-party plugins and related dependencies]

                                     ├───css

                                     └───javascript
```

### Estendere una classe widget esistente {#extend-an-existing-widget-class}

Una volta creato il modello di progetto, effettua le seguenti modifiche, in base alle esigenze:

1. Includi la dipendenza del plug-in di terze parti dal progetto.

   1. Inserire i plug-in jQuery di terze parti o personalizzati nella `jqueryplugin/javascript` cartella e i file CSS correlati in `jqueryplugin/css` cartella. Per ulteriori dettagli, vedi i file JS e CSS in `jqueryplugin/javascript and jqueryplugin/css` cartella.

   1. Modifica il `js.txt` e `css.txt` file per includere eventuali file JavaScript e CSS aggiuntivi del plug-in jQuery.

1. Integra il plug-in di terze parti con il framework per abilitare l’interazione tra il framework di aspetto personalizzato e il plug-in jQuery. Il nuovo widget funzionerà solo dopo aver esteso o ignorato le seguenti funzioni.

<table>
 <tbody>
  <tr>
   <td><strong>Funzione</strong></td>
   <td><strong>Descrizione</strong></td>
  </tr>
  <tr>
   <td><code>render</code></td>
   <td>La funzione render restituisce l’oggetto jQuery per l’elemento HTML predefinito del widget. L’elemento HTML predefinito deve essere di tipo attivabile. Ad esempio: <code>&lt;a&gt;</code>, <code>&lt;input&gt;</code>, e <code>&lt;li&gt;</code>. L’elemento restituito viene utilizzato come <code>$userControl</code>. Se il <code>$userControl</code> specifica il vincolo di cui sopra, le funzioni del <code>AbstractWidget</code> La classe funziona come previsto, altrimenti alcune delle API comuni (attivazione, clic) richiedono modifiche. </td>
  </tr>
  <tr>
   <td><code>getEventMap</code></td>
   <td>Restituisce una mappa per convertire gli eventi HTML in eventi XFA. <br /> <code class="code">{
      blur: XFA_EXIT_EVENT,
      }</code><br /> Questo esempio mostra che <code>blur</code> è un evento HTML e <code>XFA_EXIT_EVENT</code> è l’evento XFA corrispondente. </td>
  </tr>
  <tr>
   <td><code>getOptionsMap</code></td>
   <td>Restituisce una mappa che fornisce dettagli sull’azione da eseguire in seguito alla modifica di un’opzione. Le chiavi sono le opzioni fornite al widget e i valori sono funzioni che vengono richiamate ogni volta che viene rilevata una modifica nell’opzione. Il widget fornisce gestori per tutte le opzioni comuni (eccetto <code>value</code> e <code>displayValue</code>).</td>
  </tr>
  <tr>
   <td><code>getCommitValue</code></td>
   <td>Il framework del widget jQuery carica la funzione ogni volta che il valore del widget jQuery viene salvato nel modello XFA (ad esempio, all’evento di uscita di un campo di testo). L’implementazione deve restituire il valore salvato nel widget. Al gestore viene fornito il nuovo valore per l’opzione.</td>
  </tr>
  <tr>
   <td><code>showValue</code></td>
   <td>Per impostazione predefinita, in XFA al momento dell’immissione dell’evento, il <code>rawValue</code> del campo. Questa funzione viene chiamata per mostrare <code>rawValue</code> all'utente. </td>
  </tr>
  <tr>
   <td><code>showDisplayValue</code></td>
   <td>Per impostazione predefinita, in XFA all’evento di uscita, il <code>formattedValue</code> del campo. Questa funzione viene chiamata per mostrare <code>formattedValue</code> all'utente. </td>
  </tr>
 </tbody>
</table>

1. Aggiornare il file JavaScript in `integration/javascript` cartella, come richiesto.

   * Sostituisci il testo `__widgetName__` con il nome effettivo del widget.
   * Estendere il widget da una classe di widget predefinita adatta. Nella maggior parte dei casi, è la classe di widget corrispondente al widget esistente che viene sostituito. Il nome della classe padre viene utilizzato in più posizioni, pertanto si consiglia di cercare tutte le istanze della stringa `xfaWidget.textField` nel file e sostituirli con la classe padre effettiva utilizzata.
   * Estendi il `render` per fornire un&#39;interfaccia utente alternativa. È la posizione da cui verrà richiamato il plug-in jQuery per aggiornare l’interfaccia utente o il comportamento di interazione. Il `render` Il metodo deve restituire un elemento user-control.

   * Estendi il `getOptionsMap` metodo per ignorare qualsiasi impostazione di opzione interessata a causa di una modifica nel widget. La funzione restituisce una mappatura che fornisce i dettagli dell’azione da eseguire in caso di modifica di un’opzione. Le chiavi sono le opzioni fornite al widget e i valori sono le funzioni chiamate ogni volta che viene rilevata una modifica nell’opzione.
   * Il `getEventMap` il metodo mappa gli eventi attivati dal widget, con gli eventi richiesti dal modello di modulo adattivo. Il valore predefinito mappa gli eventi HTML standard per il widget predefinito e deve essere aggiornato se viene attivato un evento alternativo.
   * Il `showDisplayValue` e `showValue` applica la clausola display and edit picture e può essere sostituita per avere un comportamento alternativo.

   * Il `getCommitValue` viene richiamato dal framework dei moduli adattivi quando `commit`si verifica. In genere, si tratta dell’evento di uscita, ad eccezione degli elementi a discesa, pulsante di scelta e casella di controllo in cui si verifica in caso di modifica). Per ulteriori informazioni, consulta [Espressioni Forms adattive](../../forms/using/adaptive-form-expressions.md#p-value-commit-script-p).

   * Il file modello fornisce un’implementazione di esempio per vari metodi. Rimuovere i metodi da non estendere.

### Creare una libreria client {#create-a-client-library}

Il progetto di esempio generato dall’archetipo Maven crea automaticamente le librerie client richieste e le racchiude in una libreria client con una categoria `af.customwidgets`. I file JavaScript e CSS disponibili nel `af.customwidgets` sono inclusi automaticamente in fase di runtime.

### Generare e installare {#build-and-install}

Per generare il progetto, esegui il seguente comando sulla shell per generare un pacchetto CRX da installare sul server AEM.

`mvn clean install`

>[!NOTE]
>
>Il progetto Maven fa riferimento a un archivio remoto all’interno del file POM. Questo è solo a scopo di riferimento e, in base agli standard Maven, le informazioni dell’archivio vengono acquisite in `settings.xml` file.

### Aggiornare il modulo adattivo {#update-the-adaptive-form}

Per applicare l’aspetto personalizzato a un campo modulo adattivo:

1. Apri il modulo adattivo in modalità di modifica.
1. Apri **Proprietà** per il campo in cui si desidera applicare l&#39;aspetto personalizzato.
1. In **Stile** , aggiorna il `CSS class` per aggiungere il nome dell&#39;aspetto nel `widget_<widgetName>` formato. Ad esempio: **widget_numericstepper**

## Esempio: creare un aspetto personalizzato   {#sample-create-a-custom-appearance-nbsp}

Esaminiamo ora un esempio per creare un aspetto personalizzato in modo che un campo numerico venga visualizzato come un indicatore numerico o un dispositivo di scorrimento. Effettua le seguenti operazioni:

1. Esegui il seguente comando per creare un progetto locale basato su Archetipo Maven:

   `mvn archetype:generate -DarchetypeRepository=https://repo1.maven.org/maven2/com/adobe/ -DarchetypeGroupId=com.adobe.aemforms -DarchetypeArtifactId=custom-appearance-archetype -DarchetypeVersion=1.0.4`

   Viene richiesto di specificare i valori per i seguenti parametri.
   *I valori utilizzati in questo esempio sono evidenziati in grassetto*.

   `Define value for property 'groupId': com.adobe.afwidgets`

   `Define value for property 'artifactId': customWidgets`

   `Define value for property 'version': 1.0.1-SNAPSHOT`

   `Define value for property 'package': com.adobe.afwidgets`

   `Define value for property 'artifactName': customWidgets`

   `Define value for property 'packageGroup': adobe/customWidgets`

   `Define value for property 'widgetName': numericStepper`

1. Accedi a `customWidgets` (valore specificato per `artifactID` directory) ed eseguire il comando seguente per generare un progetto Eclipse:

   `mvn eclipse:eclipse`

1. Apri lo strumento Eclipse ed effettua le seguenti operazioni per importare il progetto Eclipse:

   1. Seleziona **[!UICONTROL File > Importa > Progetti esistenti in Workspace]**.

   1. Sfoglia e seleziona la cartella in cui hai eseguito `archetype:generate` comando.

   1. Clic **[!UICONTROL Fine]**.

      ![eclipse-screenshot](assets/eclipse-screenshot.png)

1. Selezionate il widget da utilizzare per l&#39;aspetto personalizzato. In questo esempio viene utilizzato il seguente widget stepper numerico:

   [https://www.jqueryscript.net/form/User-Friendly-Number-Input-Spinner-with-jQuery-Bootstrap.html](https://www.jqueryscript.net/form/User-Friendly-Number-Input-Spinner-with-jQuery-Bootstrap.html)

   Nel progetto Eclipse, controlla il codice del plug-in in. `plugin.js` per assicurarsi che corrisponda ai requisiti per l&#39;aspetto. In questo esempio, l&#39;aspetto soddisfa i seguenti requisiti:

   * Il stepper numerico deve estendersi da `- $.xfaWidget.numericInput`.
   * Il `set value` metodo del widget imposta il valore dopo che lo stato attivo si trova sul campo. È un requisito obbligatorio per un widget per moduli adattivi.
   * Il `render` il metodo deve essere sostituito per richiamare `bootstrapNumber` metodo.

   * Non esiste alcuna dipendenza aggiuntiva per il plug-in diversa dal codice sorgente principale del plug-in.
   * L’esempio non esegue alcuno stile sul stepper, pertanto non è necessario alcun CSS aggiuntivo.
   * Il `$userControl` l&#39;oggetto deve essere disponibile per `render` metodo. È un campo del `text` tipo clonato con il codice del plug-in.

   * Il **+** e **-** I pulsanti devono essere disattivati quando il campo è disattivato.

1. Sostituisci il contenuto del `bootstrap-number-input.js` (jPlug-in Query) con il contenuto del `numericStepper-plugin.js` file.
1. In `numericStepper-widget.js` , aggiungi il seguente codice per ignorare il metodo di rendering per richiamare il plug-in e restituire `$userControl` oggetto:

   ```javascript
   render : function() {
        var control = $.xfaWidget.numericInput.prototype.render.apply(this, arguments);
        var $control = $(control);
        var controlObject;
        try{
            if($control){
            $control.bootstrapNumber();
            var id = $control.attr("id");
            controlObject = $("#"+id);
            }
        }catch (exc){
             console.log(exc);
        }
        return controlObject;
   }
   ```

1. In `numericStepper-widget.js` file, sostituisci il `getOptionsMap` per ignorare l&#39;opzione access e nascondere i pulsanti + e - in modalità disabilitata.

   ```javascript
   getOptionsMap: function(){
       var parentOptionsMap = $.xfaWidget.numericInput.prototype.getOptionsMap.apply(this,arguments),
   
       newMap = $.extend({},parentOptionsMap,
   
        {
   
              "access": function(val) {
              switch(val) {
                 case "open" :
                   this.$userControl.removeAttr("readOnly");
                   this.$userControl.removeAttr("aria-readonly");
                   this.$userControl.removeAttr("disabled");
                   this.$userControl.removeAttr("aria-disabled");
                   this.$userControl.parent().find(".input-group-btn button").prop('disabled',false);
                   break;
                 case "nonInteractive" :
                 case "protected" :
                   this.$userControl.attr("disabled", "disabled");
                   this.$userControl.attr("aria-disabled", "true");
                   this.$userControl.parent().find(".input-group-btn button").prop('disabled',true);
                   break;
                case "readOnly" :
                   this.$userControl.attr("readOnly", "readOnly");
                   this.$userControl.attr("aria-readonly", "true");
                   this.$userControl.parent().find(".input-group-btn button").prop('disabled',true);
                   break;
               default :
                   this.$userControl.removeAttr("disabled");
                   this.$userControl.removeAttr("aria-disabled");
                   this.$userControl.parent().find(".input-group-btn button").prop('disabled',false);
                   break;
             }
          },
      });
      return newMap;
    }
   ```

1. Salva le modifiche, passa alla cartella contenente `pom.xml` ed esegui il seguente comando Maven per generare il progetto:

   `mvn clean install`

1. Installa il pacchetto utilizzando Gestione pacchetti AEM.

1. Apri il modulo adattivo in modalità di modifica in cui desideri applicare l’aspetto personalizzato ed effettua le seguenti operazioni:

   1. Fare clic con il pulsante destro del mouse sul campo a cui si desidera applicare l&#39;aspetto e fare clic su **[!UICONTROL Modifica]** per aprire la finestra di dialogo Modifica componente.

   1. Nella scheda Stile, aggiorna il **[!UICONTROL Classe CSS]** proprietà da aggiungere `widget_numericStepper`.

Il nuovo aspetto creato è ora disponibile.
