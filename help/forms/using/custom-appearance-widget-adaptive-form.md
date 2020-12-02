---
title: Creare un aspetto personalizzato per i campi modulo adattivi
seo-title: Creare un aspetto personalizzato per i campi modulo adattivi
description: Personalizzare l'aspetto dei componenti forniti con i prodotti forniti con i prodotti Forms adattivi.
seo-description: Personalizzare l'aspetto dei componenti forniti con i prodotti forniti con i prodotti Forms adattivi.
uuid: 1aa36443-774a-49fb-b3d1-d5a2d5ff849a
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: d388acef-7313-4e68-9395-270aef6ef2c6
docset: aem65
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '1728'
ht-degree: 0%

---


# Creare un aspetto personalizzato per i campi modulo adattivi{#create-custom-appearances-for-adaptive-form-fields}

## Introduzione {#introduction}

I moduli adattivi si basano sul [framework di aspetto](/help/forms/using/introduction-widgets.md) per consentire all&#39;utente di creare un aspetto personalizzato per i campi modulo adattivi e offrire un&#39;esperienza utente diversa. Ad esempio, sostituire pulsanti di scelta e caselle di controllo con pulsanti di attivazione/disattivazione oppure utilizzare i plug-in jQuery personalizzati per limitare gli input degli utenti in campi quali numeri di telefono o ID e-mail.

Questo documento spiega come utilizzare un plug-in jQuery per creare queste esperienze alternative per i campi modulo adattivi. Inoltre, mostra un esempio per creare un aspetto personalizzato per il componente Campo numerico affinché venga visualizzato come un passo o un cursore numerico.

Analizziamo innanzitutto i termini e i concetti chiave utilizzati in questo articolo.

**Aspetto:** si riferisce allo stile, all&#39;aspetto e all&#39;organizzazione di vari elementi di un campo modulo adattivo. In genere include un&#39;etichetta, un&#39;area interattiva per fornire gli input, un&#39;icona della guida e descrizioni brevi e lunghe del campo. La personalizzazione dell&#39;aspetto descritta in questo articolo è applicabile all&#39;aspetto dell&#39;area di input del campo.

**jQuery** pluginFornisce un meccanismo standard, basato sul framework di widget jQuery, per implementare un aspetto alternativo.

**Sistema di librerie lato client** ClientLibUn sistema di librerie lato client AEM elaborazione lato client basato su codice JavaScript e CSS complessi. Per ulteriori informazioni, consultate Utilizzo delle librerie lato client.

**** ArchetypeUn progetto Maven che modella toolkit definito come modello o modello originale per i progetti Maven. Per ulteriori informazioni, vedere Introduzione ai tipi di archivio.

**User** ControlIndica l&#39;elemento principale di un widget che contiene il valore del campo e viene utilizzato dal framework di aspetto per il binding dell&#39;interfaccia utente dei widget personalizzata con il modello di modulo adattivo.

## Passaggi per creare un aspetto personalizzato {#steps-to-create-a-custom-appearance}

Per creare un aspetto personalizzato, ad alto livello effettuate le seguenti operazioni:

1. **Crea un progetto**: Create un progetto Maven che genera un pacchetto di contenuti da distribuire in AEM.
1. **Estendi una classe** widget esistente: Estendete una classe di widget esistente e ignorate le classi richieste.
1. **Creare una libreria** client: Create una  `clientLib: af.customwidget` libreria e aggiungete i file JavaScript e CSS richiesti.

1. **Create e installate il progetto**: Create il progetto Maven e installate il pacchetto di contenuti generato su AEM.
1. **Aggiornare il modulo** adattivo: Aggiornare le proprietà dei campi modulo adattivi per utilizzare l&#39;aspetto personalizzato.

### Creare un progetto {#create-a-project}

Un archetipo di cielo è un punto di partenza per la creazione di un aspetto personalizzato. I dettagli dell&#39;archetipo da utilizzare sono i seguenti:

* **Repository**: https://repo.adobe.com/nexus/content/groups/public/
* **Id** Artifact: custom-appearance-archetype
* **ID** gruppo: com.adobe.aemforms
* **Versione**: 1.0.4

Esegui il comando seguente per creare un progetto locale basato su archetype:

`mvn archetype:generate -DarchetypeRepository=https://repo.adobe.com/nexus/content/groups/public/ -DarchetypeGroupId=com.adobe.aemforms -DarchetypeArtifactId=custom-appearance-archetype -DarchetypeVersion=1.0.4`

Il comando scarica i plug-in Maven e le informazioni archetype dall&#39;archivio e genera un progetto in base alle seguenti informazioni:

* **groupId**: ID gruppo utilizzato dal progetto Maven generato
* **artifactId**: ID artefatto utilizzato dal progetto Maven generato.
* **versione**: Versione per il progetto Maven generato.
* **pacchetto**: Pacchetto utilizzato per la struttura del file.
* **artifactName**: Nome dell&#39;artefatto del pacchetto AEM generato.
* **packageGroup**: Gruppo di pacchetti del pacchetto AEM generato.
* **widgetName**: Nome dell&#39;aspetto usato come riferimento.

Il progetto generato ha la struttura seguente:

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

### Estendi una classe di widget esistente {#extend-an-existing-widget-class}

Dopo aver creato il modello di progetto, effettuate le seguenti modifiche, come necessario:

1. Includete la dipendenza del plug-in di terze parti nel progetto.

   1. Inserite i plug-in jQuery di terze parti o personalizzati nella cartella `jqueryplugin/javascript` e i file CSS correlati nella cartella `jqueryplugin/css`. Per ulteriori dettagli, consultate i file JS e CSS nella cartella `jqueryplugin/javascript and jqueryplugin/css`.

   1. Modificate i file `js.txt` e `css.txt` in modo da includere eventuali file JavaScript e CSS aggiuntivi del plug-in jQuery.

1. Integrate il plug-in di terze parti con il framework per consentire l&#39;interazione tra il framework di aspetto personalizzato e il plug-in jQuery. Il nuovo widget funzionerà solo dopo l’estensione o l’esclusione delle seguenti funzioni.

<table>
 <tbody>
  <tr>
   <td><strong>Funzione</strong></td>
   <td><strong>Descrizione</strong></td>
  </tr>
  <tr>
   <td><code>render</code></td>
   <td>La funzione di rendering restituisce l'oggetto jQuery per l'elemento HTML predefinito del widget. L'elemento HTML predefinito deve essere di tipo attivabile. Ad esempio, <code>&lt;a&gt;</code>, <code>&lt;input&gt;</code> e <code>&lt;li&gt;</code>. L'elemento restituito viene utilizzato come <code>$userControl</code>. Se <code>$userControl</code> specifica il vincolo di cui sopra, le funzioni della classe <code>AbstractWidget</code> funzionano come previsto, altrimenti alcune delle API comuni (focus, click) richiedono delle modifiche. </td>
  </tr>
  <tr>
   <td><code>getEventMap</code></td>
   <td>Restituisce una mappa per convertire gli eventi HTML in eventi XFA. <br /> <code class="code">{
      blur: XFA_EXIT_EVENT,
      }</code><br /> Questo esempio mostra che  <code>blur</code> è un evento HTML ed  <code>XFA_EXIT_EVENT</code> è l'evento XFA corrispondente. </td>
  </tr>
  <tr>
   <td><code>getOptionsMap</code></td>
   <td>Restituisce una mappa che fornisce informazioni dettagliate sull'azione da eseguire al cambio di un'opzione. Le chiavi sono le opzioni fornite al widget e i valori sono funzioni che vengono chiamate ogni volta che viene rilevata una modifica nell'opzione. Il widget fornisce gestori per tutte le opzioni comuni (tranne <code>value</code> e <code>displayValue</code>).</td>
  </tr>
  <tr>
   <td><code>getCommitValue</code></td>
   <td>Il framework di widget jQuery carica la funzione ogni volta che il valore del widget jQuery viene salvato nel modello XFA (ad esempio, in corrispondenza dell'evento exit di un campo di testo). L’implementazione deve restituire il valore salvato nel widget. Al gestore viene fornito il nuovo valore per l'opzione.</td>
  </tr>
  <tr>
   <td><code>showValue</code></td>
   <td>Per impostazione predefinita, in XFA all'evento enter, viene visualizzato il simbolo <code>rawValue</code> del campo. Questa funzione viene chiamata per mostrare l' <code>rawValue</code> all'utente. </td>
  </tr>
  <tr>
   <td><code>showDisplayValue</code></td>
   <td>Per impostazione predefinita, in XFA all'evento exit, viene visualizzato il simbolo <code>formattedValue</code> del campo. Questa funzione viene chiamata per mostrare l' <code>formattedValue</code> all'utente. </td>
  </tr>
 </tbody>
</table>

1. Aggiornate il file JavaScript nella cartella `integration/javascript`, come necessario.

   * Sostituite il testo `__widgetName__` con il nome effettivo del widget.
   * Estendete il widget da una classe di widget out-of-the-box adeguata. Nella maggior parte dei casi, Si tratta della classe widget corrispondente al widget esistente che viene sostituito. Il nome della classe principale viene utilizzato in più posizioni, pertanto si consiglia di cercare tutte le istanze della stringa `xfaWidget.textField` nel file e sostituirle con la classe padre effettiva utilizzata.
   * Estendete il metodo `render` per fornire un&#39;interfaccia utente alternativa. Si tratta del percorso dal quale verrà richiamato il plug-in jQuery per aggiornare l&#39;interfaccia utente o il comportamento dell&#39;interazione. Il metodo `render` deve restituire un elemento controllo utente.

   * Estendete il metodo `getOptionsMap` per escludere qualsiasi impostazione di opzione interessata da una modifica nel widget. La funzione restituisce una mappatura che fornisce i dettagli dell&#39;azione da eseguire in caso di modifica di un&#39;opzione. Le chiavi sono le opzioni fornite al widget e i valori sono le funzioni richiamate ogni volta che viene rilevata una modifica nell&#39;opzione.
   * Il metodo `getEventMap` mappa gli eventi attivati dal widget, con gli eventi richiesti dal modello di modulo adattivo. Il valore predefinito mappa gli eventi HTML standard per il widget predefinito e deve essere aggiornato se viene attivato un evento alternativo.
   * Le `showDisplayValue` e `showValue` applicano la clausola di visualizzazione e modifica dell&#39;immagine e possono essere ignorate per avere un comportamento alternativo.

   * Il metodo `getCommitValue` viene chiamato dal framework di moduli adattivi quando si verifica l&#39;evento `commit`. Generalmente si tratta dell&#39;evento exit, ad eccezione degli elementi a discesa, pulsante di scelta e casella di controllo in cui si verifica al momento della modifica). Per ulteriori informazioni, vedere [Espressioni Forms adattive](../../forms/using/adaptive-form-expressions.md#p-value-commit-script-p).

   * Il file modello fornisce un esempio di implementazione per vari metodi. Rimuovere i metodi che non devono essere estesi.

### Creare una libreria client {#create-a-client-library}

Il progetto di esempio generato dall&#39;archetype Maven crea automaticamente le librerie client necessarie e le racchiude in una libreria client con una categoria `af.customwidgets`. I file JavaScript e CSS disponibili in `af.customwidgets` vengono inclusi automaticamente in fase di esecuzione.

### Creare e installare {#build-and-install}

Per creare il progetto, eseguite il seguente comando sulla shell per generare un pacchetto CRX che deve essere installato sul server AEM.

`mvn clean install`

>[!NOTE]
>
>Il progetto maven si riferisce a un repository remoto all&#39;interno del file POM. Questo è solo a scopo di riferimento, e secondo gli standard di Maven, le informazioni del repository vengono acquisite nel file `settings.xml`.

### Aggiornare il modulo adattivo {#update-the-adaptive-form}

Per applicare l&#39;aspetto personalizzato a un campo modulo adattivo:

1. Aprire il modulo adattivo in modalità di modifica.
1. Aprire la finestra di dialogo **Property** relativa al campo in cui si desidera applicare l&#39;aspetto personalizzato.
1. Nella scheda **Stile**, aggiornare la proprietà `CSS class` per aggiungere il nome dell&#39;aspetto nel formato `widget_<widgetName>`. Ad esempio: **widget_numericstepper**

## Esempio: Creare un aspetto personalizzato   {#sample-create-a-custom-appearance-nbsp}

Esaminiamo ora un esempio per creare un aspetto personalizzato per un campo numerico che verrà visualizzato come uno stepper o un cursore numerico. Effettuate le seguenti operazioni:

1. Esegui il comando seguente per creare un progetto locale basato su Maven archetype:

   `mvn archetype:generate -DarchetypeRepository=https://repo.adobe.com/nexus/content/groups/public/ -DarchetypeGroupId=com.adobe.aemforms -DarchetypeArtifactId=custom-appearance-archetype -DarchetypeVersion=1.0.4`

   Viene richiesto di specificare i valori per i seguenti parametri.
   *I valori utilizzati in questo esempio sono evidenziati in grassetto*.

   `Define value for property 'groupId': com.adobe.afwidgets`

   `Define value for property 'artifactId': customWidgets`

   `Define value for property 'version': 1.0.1-SNAPSHOT`

   `Define value for property 'package': com.adobe.afwidgets`

   `Define value for property 'artifactName': customWidgets`

   `Define value for property 'packageGroup': adobe/customWidgets`

   `Define value for property 'widgetName': numericStepper`

1. Andate alla directory `customWidgets` (valore specificato per la proprietà `artifactID`) ed eseguite il comando seguente per generare un progetto Eclipse:

   `mvn eclipse:eclipse`

1. Aprite lo strumento Eclipse ed effettuate le seguenti operazioni per importare il progetto Eclipse:

   1. Selezionare **[!UICONTROL File > Importa > Progetti esistenti in Workspace]**.

   1. Individuate e selezionate la cartella in cui è stato eseguito il comando `archetype:generate`.

   1. Fare clic su **[!UICONTROL Fine]**.

      ![eclipse-screenshot](assets/eclipse-screenshot.png)

1. Selezionate il widget da usare per l’aspetto personalizzato. Questo esempio utilizza il seguente widget per passo numerico:

   [https://www.jqueryscript.net/form/User-Friendly-Number-Input-Spinner-with-jQuery-Bootstrap.html](https://www.jqueryscript.net/form/User-Friendly-Number-Input-Spinner-with-jQuery-Bootstrap.html)

   Nel progetto Eclipse, controllate il codice plug-in nel file `plugin.js` per verificare che corrisponda ai requisiti per l&#39;aspetto. In questo esempio, l&#39;aspetto soddisfa i seguenti requisiti:

   * Lo stepper numerico deve estendersi da `- $.xfaWidget.numericInput`.
   * Il metodo `set value` del widget imposta il valore dopo che lo stato attivo è sul campo. È un requisito obbligatorio per i widget per moduli adattivi.
   * Per richiamare il metodo `render` è necessario sostituire il metodo `bootstrapNumber`.

   * Non esiste alcuna dipendenza aggiuntiva per il plug-in diversa dal codice sorgente principale del plug-in.
   * L&#39;esempio non esegue alcuno stile sullo stepper, pertanto non è necessario alcun CSS aggiuntivo.
   * L&#39;oggetto `$userControl` deve essere disponibile per il metodo `render`. Si tratta di un campo del tipo `text` che viene clonato con il codice del plug-in.

   * I pulsanti **+** e **-** devono essere disattivati quando il campo è disabilitato.

1. Sostituite il contenuto del `bootstrap-number-input.js` (plugin jQuery) con il contenuto del file `numericStepper-plugin.js`.
1. Nel file `numericStepper-widget.js`, aggiungete il seguente codice per ignorare il metodo di rendering per richiamare il plug-in e restituire l&#39;oggetto `$userControl`:

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

1. Nel file `numericStepper-widget.js`, ignorare la proprietà `getOptionsMap` per ignorare l&#39;opzione di accesso e nascondere i pulsanti + e - in modalità disattivata.

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

1. Salvate le modifiche, individuate la cartella contenente il file `pom.xml` ed eseguite il seguente comando Maven per creare il progetto:

   `mvn clean install`

1. Installate il pacchetto utilizzando AEM Package Manager.

1. Aprite il modulo adattivo in modalità di modifica in cui desiderate applicare l’aspetto personalizzato ed effettuate le seguenti operazioni:

   1. Fare clic con il pulsante destro del mouse sul campo in cui si desidera applicare l&#39;aspetto e fare clic su **[!UICONTROL Modifica]** per aprire la finestra di dialogo Modifica componente.

   1. Nella scheda Attribuzione stile, aggiornare la proprietà **[!UICONTROL Classe CSS]** per aggiungere `widget_numericStepper`.

Il nuovo aspetto appena creato è ora disponibile per l’uso.
