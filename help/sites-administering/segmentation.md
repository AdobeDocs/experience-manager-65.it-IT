---
title: Configurazione della segmentazione con ContextHub
seo-title: Configurazione della segmentazione con ContextHub
description: Scopri come configurare la segmentazione con Context Hub.
seo-description: Scopri come configurare la segmentazione con Context Hub.
uuid: 196cfb18-317c-443d-b6f1-f559e4221baa
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: 6cade87c-9ed5-47d7-9b39-c942268afdad
translation-type: tm+mt
source-git-commit: e5e00cc181c2dc3a28e25beb52f9a4c459ee313a
workflow-type: tm+mt
source-wordcount: '1779'
ht-degree: 2%

---


# Configurazione della segmentazione con ContextHub{#configuring-segmentation-with-contexthub}

>[!NOTE]
>
>Questa sezione descrive la configurazione della segmentazione quando si utilizza ContextHub. Se utilizzi la funzionalità ClientContext, consulta la documentazione relativa alla [configurazione della segmentazione per ClientContext](/help/sites-administering/campaign-segmentation.md).


La segmentazione è un concetto chiave per la creazione di una campagna. Per informazioni sul funzionamento della segmentazione e sui termini chiave, consultate [Gestione dell&#39;audience](/help/sites-authoring/managing-audiences.md).

A seconda delle informazioni già raccolte sui visitatori del sito e degli obiettivi da raggiungere, dovrete definire i segmenti e le strategie necessari per il contenuto di destinazione.

Questi segmenti vengono quindi utilizzati per fornire a un visitatore contenuto con targeting specifico. Questo contenuto viene mantenuto nella sezione [Personalizzazione](/help/sites-authoring/personalization.md) del sito Web. [Le ](/help/sites-authoring/activitylib.md) attività qui definite possono essere incluse in qualsiasi pagina e definire per quale segmento di visitatori si applica il contenuto specializzato.

AEM consente di personalizzare facilmente l&#39;esperienza degli utenti. Consente inoltre di verificare i risultati delle definizioni dei segmenti.

## Accesso ai segmenti {#accessing-segments}

La console [Audiences](/help/sites-authoring/managing-audiences.md) viene utilizzata per gestire i segmenti per ContextHub o ClientContext, nonché i tipi di pubblico per l&#39;account Adobe Target . Questa documentazione descrive la gestione dei segmenti per ContextHub. Per [Segmenti ClientContext](/help/sites-administering/campaign-segmentation.md) e  segmenti Adobe Target, consulta la documentazione pertinente.

Per accedere ai tuoi segmenti, nella navigazione globale seleziona **Navigazione > Personalizzazione > Audiences**.

![chlimage_1-310](assets/chlimage_1-310.png)

## Editor segmento {#segment-editor}

L&#39; **Editor segmento** consente di modificare facilmente un segmento. Per modificare un segmento, selezionare un segmento nell&#39;elenco [dei segmenti](/help/sites-administering/segmentation.md#accessing-segments) e fare clic sul pulsante **Modifica**.

![segmenteditor](assets/segmenteditor.png)

Utilizzando il browser Componenti è possibile aggiungere contenitori **AND** e **OR** per definire la logica del segmento, quindi aggiungere componenti aggiuntivi per confrontare proprietà e valori o script di riferimento e altri segmenti per definire i criteri di selezione (vedere [Creazione di un nuovo segmento](#creating-a-new-segment)) per definire lo scenario esatto per la selezione del segmento.

Quando l&#39;intera istruzione restituisce true, il segmento ha risolto. Se sono applicabili più segmenti, viene utilizzato anche il fattore **Incrementa**. Per informazioni dettagliate sul fattore di incremento, vedere [Creazione di un nuovo segmento](#creating-a-new-segment).](/help/sites-administering/campaign-segmentation.md#boost-factor)[

>[!CAUTION]
>
>L&#39;editor segmenti non verifica la presenza di riferimenti circolari. Ad esempio, il segmento A fa riferimento a un altro segmento B, che a sua volta fa riferimento al segmento A. Devi accertarti che i tuoi segmenti non contengano riferimenti circolari.

### Contenitori {#containers}

I seguenti contenitori sono disponibili out-of-the-box e consentono di raggruppare confronti e riferimenti per la valutazione booleana. È possibile trascinarli dal Browser componenti all’editor. Per ulteriori informazioni, vedere la sezione [Utilizzo di AND e OR Containers](/help/sites-administering/segmentation.md#using-and-and-or-containers).

<table>
 <tbody>
  <tr>
   <td>Contenitore E<br /> </td>
   <td>Operatore AND booleano<br /> </td>
  </tr>
  <tr>
   <td>Contenitore O<br /> </td>
   <td>Operatore OR booleano</td>
  </tr>
 </tbody>
</table>

### Confronti {#comparisons}

Per valutare le proprietà del segmento sono disponibili i seguenti confronti out-of-the-box. È possibile trascinarli dal Browser componenti all’editor.

<table>
 <tbody>
  <tr>
   <td>Property-Value<br /> </td>
   <td>Confronta una proprietà di un archivio con un valore definito<br /> </td>
  </tr>
  <tr>
   <td>Property-Property</td>
   <td>Confronta una proprietà di uno store con un'altra proprietà<br /> </td>
  </tr>
  <tr>
   <td>Riferimento segmento proprietà</td>
   <td>Confronta una proprietà di uno store con un altro segmento di riferimento<br /> </td>
  </tr>
  <tr>
   <td>Riferimento script di proprietà</td>
   <td>Confronta una proprietà di uno store con i risultati di uno script<br /> </td>
  </tr>
  <tr>
   <td>Riferimento segmento-Riferimento script</td>
   <td>Confronta un segmento di riferimento con i risultati di uno script<br /> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Quando si confrontano i valori, se il tipo di dati del confronto non è impostato (ovvero impostato su auto detection), il motore di segmentazione di ContextHub confronterà semplicemente i valori come farebbe javascript. Non riporta i valori ai tipi previsti, il che può portare a risultati fuorvianti. Esempio:
>
>`null < 30 // will return true`
>
>Pertanto, durante la creazione di un segmento [è necessario selezionare un **tipo di dati** ogni volta che i tipi di valori confrontati sono noti. ](/help/sites-administering/segmentation.md#creating-a-new-segment) Esempio:
>
>Quando si confronta la proprietà `profile/age`, è già noto che il tipo confrontato sarà **number**, quindi anche se `profile/age` non è impostato, un confronto `profile/age` inferiore a 30 restituirà **false**, come previsto.

### Riferimenti {#references}

I seguenti riferimenti sono disponibili out-of-the-box per il collegamento diretto a uno script o a un altro segmento. È possibile trascinarli dal Browser componenti all’editor.

<table>
 <tbody>
  <tr>
   <td>Riferimento segmento<br /> </td>
   <td>Valutazione del segmento a cui si fa riferimento</td>
  </tr>
  <tr>
   <td>Riferimento script</td>
   <td>Valutare lo script di riferimento. Per ulteriori informazioni, vedere la sezione <a href="/help/sites-administering/segmentation.md#using-script-references">Utilizzo di riferimenti di script</a>.</td>
  </tr>
 </tbody>
</table>

## Creazione di un nuovo segmento {#creating-a-new-segment}

Per definire il nuovo segmento:

1. Dopo [l&#39;accesso ai segmenti](/help/sites-administering/segmentation.md#accessing-segments), [passare alla cartella](#organizing-segments) in cui si desidera creare il segmento o lasciarlo nella directory principale.

1. tocca o fai clic sul pulsante Crea e seleziona **Crea segmento ContextHub**.

   ![chlimage_1-311](assets/chlimage_1-311.png)

1. In **Nuovo segmento ContextHub**, immettete un titolo per il segmento e un valore di incremento, se necessario, quindi toccate o fate clic su **Crea**.

   ![chlimage_1-312](assets/chlimage_1-312.png)

   Ogni segmento ha un parametro di incremento che viene utilizzato come fattore di ponderazione. Un numero più alto indica che il segmento sarà selezionato in preferenza rispetto a un segmento con un numero inferiore nelle istanze in cui più segmenti sono validi.

   * Valore minimo: `0`
   * Valore massimo: `1000000`

1. Trascina un confronto o un riferimento all’editor segmenti che verrà visualizzato nel contenitore AND predefinito.
1. Tocca o fai doppio clic sull&#39;opzione di configurazione del nuovo riferimento o segmento per modificare i parametri specifici. In questo esempio, stiamo provando le persone di San Jose.

   ![screen_shot_2012-02-02at103135am](assets/screen_shot_2012-02-02at103135ama.png)

   Impostate sempre un **Tipo di dati**, se possibile, per garantire che i confronti vengano valutati correttamente. Per ulteriori informazioni, vedere [Confronti](/help/sites-administering/segmentation.md#comparisons).

1. Fare clic su **OK** per salvare la definizione:
1. Aggiungi altri componenti in base alle esigenze. È possibile formulare espressioni booleane utilizzando i componenti contenitore per confronti AND e OR (vedere [Utilizzo di AND e OR Containers](/help/sites-administering/segmentation.md#using-and-and-or-containers) di seguito). Con l&#39;editor segmenti è possibile eliminare i componenti non più necessari o trascinarli in nuove posizioni all&#39;interno dell&#39;istruzione.

### Utilizzo di AND e OR Containers {#using-and-and-or-containers}

I componenti AND e OR del contenitore consentono di creare segmenti complessi in AEM. A tal fine, è importante essere consapevoli di alcuni punti fondamentali:

* Il livello principale della definizione è sempre il contenitore AND creato inizialmente. Questo non può essere modificato, ma non ha un effetto sul resto della definizione del segmento.
* Verificare che la nidificazione del contenitore abbia senso. I contenitori possono essere visualizzati come parentesi dell&#39;espressione booleana.

L&#39;esempio seguente viene utilizzato per selezionare i visitatori che sono considerati nel nostro gruppo di fascia alta:

Maschio e tra i 30 e i 59 anni

OPPURE

Femmina e tra i 30 e i 59 anni

Per iniziare, posizionate un componente contenitore OR all’interno del contenitore AND predefinito. All&#39;interno del contenitore OR, potete aggiungere due contenitori AND e all&#39;interno di entrambi è possibile aggiungere la proprietà o i componenti di riferimento.

![screen_shot_2012-02-02at105145am](assets/screen_shot_2012-02-02at105145ama.png)

### Utilizzo dei riferimenti di script {#using-script-references}

Utilizzando il componente Riferimento script, la valutazione di una proprietà del segmento può essere delegata a uno script esterno. Una volta configurato correttamente, lo script può essere utilizzato come qualsiasi altro componente di una condizione di segmento.

#### Definizione di uno script come riferimento {#defining-a-script-to-reference}

1. Aggiungi file a `contexthub.segment-engine.scripts` clientlib.
1. Implementare una funzione che restituisce un valore. Esempio:

   ```
   ContextHub.console.log(ContextHub.Shared.timestamp(), '[loading] contexthub.segment-engine.scripts - script.profile-info.js');
   
   (function() {
       'use strict';
   
       /**
        * Sample script returning profile information. Returns user info if data is available, false otherwise.
        *
        * @returns {Boolean}
        */
       var getProfileInfo = function() {
           /* let the SegmentEngine know when script should be re-run */
           this.dependOn(ContextHub.SegmentEngine.Property('profile/age'));
           this.dependOn(ContextHub.SegmentEngine.Property('profile/givenName'));
   
           /* variables */
           var name = ContextHub.get('profile/givenName');
           var age = ContextHub.get('profile/age');
   
           return name === 'Joe' && age === 123;
       };
   
       /* register function */
       ContextHub.SegmentEngine.ScriptManager.register('getProfileInfo', getProfileInfo);
   
   })();
   ```

1. Registra lo script con `ContextHub.SegmentEngine.ScriptManager.register`.

Se lo script dipende da proprietà aggiuntive, lo script deve chiamare `this.dependOn()`. Ad esempio, se lo script dipende da `profile/age`:

```
this.dependOn(ContextHub.SegmentEngine.Property('profile/age'));
```

#### Riferimento a uno script {#referencing-a-script}

1. Crea segmento ContextHub.
1. Aggiungete il componente **Riferimento script** nella posizione desiderata del segmento.
1. Aprire la finestra di dialogo di modifica del componente **Riferimento script**. Se [è configurato correttamente](/help/sites-administering/segmentation.md#defining-a-script-to-reference), lo script deve essere disponibile nel menu a discesa **Nome script**.

## Organizzazione dei segmenti {#organizing-segments}

Se hai molti segmenti, possono diventare difficili da gestire come elenco semplice. In questi casi, può essere utile creare cartelle per gestire i segmenti.

### Creare una nuova cartella {#create-folder}

1. Dopo [l&#39;accesso ai segmenti](#accessing-segments), fare clic o toccare il pulsante **Crea** e selezionare **Cartella**.

   ![Aggiungi cartella](assets/contexthub-create-segment.png)

1. Specificare un **Titolo** e un **Nome** per la cartella.
   * Il **Titolo** deve essere descrittivo.
   * Il **Nome** diventerà il nome del nodo nella directory archivio.
      * Verrà generato automaticamente in base al titolo e verrà modificato in base alle convenzioni di denominazione [AEM.](/help/sites-developing/naming-conventions.md)
      * Può essere regolato se necessario.

   ![Crea cartella](assets/contexthub-create-folder.png)

1. Tocca o fai clic su **Crea**.

   ![Conferma cartella](assets/contexthub-confirm-folder.png)

1. La cartella verrà visualizzata nell&#39;elenco dei segmenti.
   * La modalità di ordinamento delle colonne influisce sulla posizione nell’elenco della nuova cartella.
   * Potete toccare o fare clic sulle intestazioni di colonna per regolare l’ordinamento.
      ![La nuova cartella](assets/contexthub-folder.png)

### Modifica cartelle esistenti {#modify-folders}

1. Dopo [l&#39;accesso ai segmenti](#accessing-segments), tocca o fai clic sulla cartella che desideri modificare per selezionarla.

   ![Selezione cartella](assets/contexthub-select-folder.png)

1. Toccate o fate clic su **Rinomina** nella barra degli strumenti per rinominare la cartella.

1. Immetti un nuovo **Titolo cartella** e tocca o fai clic su **Salva**.

   ![Rinomina cartella](assets/contexthub-rename-folder.png)

>[!NOTE]
>
>Quando si rinominano le cartelle, è possibile modificare solo il titolo. Impossibile modificare il nome.

### Eliminare una cartella

1. Dopo [l&#39;accesso ai segmenti](#accessing-segments), tocca o fai clic sulla cartella che desideri modificare per selezionarla.

   ![Selezione cartella](assets/contexthub-select-folder.png)

1. Toccate o fate clic su **Elimina** nella barra degli strumenti per eliminare la cartella.

1. Viene visualizzata una finestra di dialogo con un elenco di cartelle selezionate per l’eliminazione.

   ![Conferma eliminazione](assets/contexthub-confirm-segment-delete.png)

   * Toccate o fate clic su **Elimina** per confermare.
   * Toccate o fate clic su **Annulla** per interrompere.

1. Se una delle cartelle selezionate contiene sottocartelle o segmenti, l’eliminazione deve essere confermata.

   ![Conferma eliminazione di elementi figlio](assets/contexthub-confirm-segment-child-delete.png)

   * Toccate o fate clic su **Forza eliminazione** per confermare.
   * Toccate o fate clic su **Annulla** per interrompere.

>[!NOTE]
>
> Non è possibile spostare un segmento da una cartella all’altra.

## Verifica dell&#39;applicazione di un segmento {#testing-the-application-of-a-segment}

Una volta definito il segmento, è possibile testare i potenziali risultati con l&#39;aiuto di **[ContextHub](/help/sites-authoring/ch-previewing.md).**

1. Anteprima di una pagina
1. Fate clic sull’icona ContextHub per visualizzare la barra degli strumenti ContextHub
1. Selezionare una persona che corrisponda al segmento creato
1. ContextHub risolverà i segmenti applicabili alla persona selezionata

Ad esempio, la nostra definizione di segmento semplice per identificare gli utenti nel nostro gruppo di fascia alta è una definizione di segmento semplice basata sull&#39;età e sul genere dell&#39;utente. Quando si carica una persona specifica che soddisfa tali criteri, viene visualizzato se il segmento è stato risolto correttamente:

![screen_shot_2012-02-02at105926am](assets/screen_shot_2012-02-02at105926am.png)

Oppure, se non è stato risolto:

![screen_shot_2012-02-02at110019am](assets/screen_shot_2012-02-02at110019am.png)

>[!NOTE]
>
>Tutte le caratteristiche vengono risolte immediatamente, anche se la maggior parte delle modifiche apportate al ricaricamento della pagina.

Tali test possono essere eseguiti anche sulle pagine di contenuto e in combinazione con contenuti mirati e relative **Attività** e **Esperienze**.

Se avete impostato un&#39;attività e un&#39;esperienza utilizzando l&#39;esempio di segmento del gruppo di fascia alta riportato sopra, potete facilmente testare il segmento con l&#39;attività. Per informazioni dettagliate sulla configurazione di un&#39;attività, consultate la relativa [documentazione sull&#39;authoring di contenuto di destinazione](/help/sites-authoring/content-targeting-touch.md).

1. In modalità di modifica di una pagina in cui sono stati impostati contenuti mirati, potete vedere che il contenuto è indirizzato tramite l&#39;icona a forma di freccia sul contenuto.

   ![chlimage_1-313](assets/chlimage_1-313.png)

1. Passate alla modalità di anteprima e utilizzate il context hub, passate a una persona che non corrisponde alla segmentazione configurata per l&#39;esperienza.

   ![chlimage_1-314](assets/chlimage_1-314.png)

1. Passate a una persona che non corrisponde alla segmentazione configurata per l&#39;esperienza e controllate che l&#39;esperienza cambi di conseguenza.

   ![chlimage_1-315](assets/chlimage_1-315.png)

## Utilizzo del segmento {#using-your-segment}

I segmenti vengono utilizzati per indirizzare il contenuto effettivo visto da audience target specifiche. Per ulteriori informazioni sui tipi di pubblico e i segmenti e sull&#39;[Creazione di contenuti mirati](/help/sites-authoring/content-targeting-touch.md) sull&#39;utilizzo di tipi di pubblico e segmenti per il targeting dei contenuti, vedere [Gestione dell&#39;audience](/help/sites-authoring/managing-audiences.md).
