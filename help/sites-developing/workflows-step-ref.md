---
title: Guida di riferimento per i passaggi dei flussi di lavoro
seo-title: Guida di riferimento per i passaggi dei flussi di lavoro
description: Guida di riferimento per i passaggi dei flussi di lavoro
seo-description: 'null'
uuid: 88bf6997-73a1-4639-82aa-5dff08d3ef86
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: e3afffd0-d90c-4bd0-b814-f7aeac6ceb6d
docset: aem65
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '3288'
ht-degree: 2%

---


# Guida di riferimento per i passaggi dei flussi di lavoro {#workflow-step-reference}

I modelli di flusso di lavoro sono composti da una serie di passaggi di vari tipi. A seconda del tipo, questi passaggi possono essere configurati ed estesi con parametri e script per fornire la funzionalità e il controllo necessari.

>[!NOTE]
>
>Questa sezione descrive i passaggi standard del flusso di lavoro.
>
>Per i passaggi specifici del modulo consulta anche:
>
>* [Riferimento dettagliato sui flussi di lavoro per AEM Forms](/help/forms/using/aem-forms-workflow-step-reference.md)
>* [Elaborazione delle risorse tramite gestori di contenuti multimediali e flussi di lavoro](/help/assets/media-handlers.md)

>



## Proprietà passaggio {#step-properties}

Ogni componente del passaggio dispone di una finestra di dialogo **Proprietà passaggio** che consente di definire e modificare le proprietà richieste.

### Proprietà del passaggio - Scheda comune {#step-properties-common-tab}

Per la maggior parte dei componenti dei passaggi del flusso di lavoro è disponibile una combinazione delle seguenti proprietà, nella scheda **Comune** della finestra di dialogo delle proprietà:

* ****
TitoloTitolo del passaggio.

* ****
DescrizioneUna descrizione del passaggio.

* **Stadio flusso di lavoro**

   Un selettore a discesa per applicare un elemento [Stage](/help/sites-developing/workflows.md#workflow-stages) al passaggio.

* **Timeout**

   Il periodo dopo il quale il passaggio verrà &quot;interrotto&quot;.
Puoi scegliere tra: **Off**, **Immediato**, **1h**, **6h**, **12h**, **24h**.

* **Gestore timeout**

   Il gestore che controllerà il flusso di lavoro quando il passaggio scade; ad esempio:
   `Auto Advancer`

* **Avanzamento gestore**

   Seleziona questa opzione per avanzare automaticamente il flusso di lavoro al passaggio successivo dopo l’esecuzione. Se non è selezionato, lo script di implementazione deve gestire l’avanzamento del flusso di lavoro.

### Proprietà passaggio: scheda Utente/gruppo {#step-properties-user-group-tab}

Le seguenti proprietà sono disponibili per molti componenti dei passaggi del flusso di lavoro, nella scheda **Utente/Gruppo** della finestra di dialogo delle proprietà:

* **Notifica all&#39;utente via e-mail**

   * Puoi inviare una notifica ai partecipanti inviando loro un messaggio e-mail quando il flusso di lavoro raggiunge il passaggio .
   * Se attivato, un messaggio e-mail verrà inviato all&#39;utente definito dalla proprietà **Utente/Gruppo** o a ciascun membro del gruppo, se è definito un gruppo.

* **Utente/Gruppo**

   * Una casella di selezione a discesa consente di navigare e selezionare un utente o un gruppo.
   * Se assegni il passaggio a un utente specifico, solo questo utente può intervenire sul passaggio.
   * Se assegni il passaggio a un intero gruppo, quando il flusso di lavoro raggiunge questo passaggio tutti gli utenti del gruppo avranno l’azione nella **Casella in entrata flusso di lavoro**.
   * Per ulteriori informazioni, consulta [Partecipazione ai flussi di lavoro](/help/sites-authoring/workflows-participating.md) .

## Suddivisione E {#and-split}

Il **AND Split** crea una suddivisione nel flusso di lavoro, dopodiché entrambi i rami saranno attivi. Puoi aggiungere i passaggi del flusso di lavoro a ogni ramo in base alle tue esigenze. Questo passaggio ti consente di introdurre più percorsi di elaborazione nel flusso di lavoro. Ad esempio, puoi consentire che determinati passaggi di revisione si verifichino in parallelo, risparmiando tempo.

![wf-26](assets/wf-26.png)

### AND Split - Configurazione {#and-split-configuration}

Per configurare la suddivisione:

* Modifica le **proprietà di divisione AND**:

   * **Nome** diviso: assegnare un nome a fini esplicativi
   * Selezionare il numero di rami richiesti; 2, 3, 4 o 5.

* Aggiungi i passaggi del flusso di lavoro ai rami come necessario.

   ![wf-27](assets/wf-27.png)

## Passaggio contenitore {#container-step}

Un passaggio contenitore avvia un altro modello di flusso di lavoro che viene eseguito come flusso di lavoro secondario.

Questo contenitore consente di riutilizzare i modelli di flusso di lavoro per implementare sequenze di passaggi comuni. Ad esempio, un modello di flusso di lavoro di traduzione può essere utilizzato in più flussi di lavoro di modifica.

![wf-28](assets/wf-28.png)

### Passaggio contenitore - Configurazione {#container-step-configuration}

Per configurare il passaggio , modifica e utilizza le seguenti schede:

* [Comune](#step-properties-common-tab)
* **Contenitore**

   * **Flusso di lavoro secondario**: Seleziona il flusso di lavoro da avviare.

## Passaggio GoTo {#goto-step}

Il **Passaggio** consente di specificare il passaggio successivo da eseguire nel modello di flusso di lavoro. È possibile specificare una definizione di regola, uno script esterno o uno script ECMA come espressione di indirizzamento per valutare il passaggio successivo per il modello di flusso di lavoro.

* Se la condizione specificata mantiene true, il **Passaggio di destinazione** viene completato e il motore del flusso di lavoro esegue il passaggio specificato.
* Se la condizione specificata non è vera, il **Passaggio di visita** viene completato e la logica di indirizzamento normale determina il passaggio successivo da eseguire.

Il **Passaggio** consente di implementare strutture di indirizzamento avanzate nei modelli di flusso di lavoro. Ad esempio, per implementare un ciclo, è possibile definire il **Passaggio di destinazione** per eseguire un passaggio precedente nel flusso di lavoro, con l&#39;espressione di indirizzamento che valuta una condizione di ciclo.

### Passaggio a : configurazione {#goto-step-configuration}

Per configurare il passaggio , modifica e utilizza le seguenti schede:

* [Comune](#step-properties-common-tab)
* **Processo**

   * **Passaggio** di destinazione: Selezionare il passaggio da eseguire dopo aver valutato la condizione per l&#39;espressione di indirizzamento.
   * **Espressione** di routing: Selezionare Definizione regola, Script esterno o script ECMA che determina se eseguire o meno il passaggio  **di Target**.

      * **Definizione regola:** utilizza l’editor di  [espressioni ](/help/forms/using/variable-in-aem-workflows.md#use-expression-editor) per definire la regola.
      * **Script esterno:** il percorso dello script esterno.
      * **Script** ECMA: Lo script che determina se eseguire il  **passaggio Passaggio**.

#### Simulazione di un loop per {#simulating-a-for-loop}

Per simulare un ciclo for è necessario mantenere un conteggio del numero di iterazioni del ciclo che si sono verificate:

* In genere, il conteggio rappresenta un indice degli elementi su cui viene eseguito il processo nel flusso di lavoro.
* Il conteggio viene valutato come criterio di uscita del ciclo.

Ad esempio, per implementare un flusso di lavoro che esegue un&#39;azione su più nodi JCR, puoi utilizzare un contatore di loop come indice per i nodi. Per mantenere il conteggio, memorizza un valore `integer` nella mappa dati dell’istanza del flusso di lavoro. Utilizza lo script del **Passaggio** per incrementare il conteggio e confrontare il conteggio con i criteri di uscita.

```
function check(){
   var count=0;
   var keyname="loopcount"
   try{
      if (workflowData.getMetaDataMap().containsKey(keyname)){
        log.info("goto script: found loopcount key");
        count= parseInt(workflowData.getMetaDataMap().get(keyname))+1;
      }

     workflowData.getMetaDataMap().put(keyname,count);

     }catch(err) {
         log.info(err.message);
         return false;
    }
   if (parseInt(count) <7){
       return true;
   } else {
      return false;
   }
}
```

### Simulazione di un ciclo for utilizzando la definizione della regola {#simulateforloop}

È inoltre possibile simulare un ciclo for utilizzando Definizione regola come espressione di indirizzamento. [Creare una variabile  **** ](/help/forms/using/variable-in-aem-workflows.md#create-a-variable) numerosa di tipo dati Long. Utilizza **Espressione** come modalità di mappatura nel passaggio **[Imposta variabile](/help/sites-developing/using-variables-in-aem-workflows.md#set-a-variable)** per impostare il valore della variabile **count** su **count + 1** per ogni esecuzione del passaggio **Imposta variabile**.

![Simulazione di un ciclo for](assets/variable_use_case_count_new.png)

In **Passaggio**, utilizza **Imposta variabile** come **Passaggio di destinazione** e **conteggia &lt; 5** come espressione di indirizzamento.

![Condizione per la simulazione di un loop for](assets/variable_use_case_count1_new.png)

Il passaggio **Imposta variabile** esegue ripetutamente l&#39;incremento del valore di **count** di 1 su ogni esecuzione fino a raggiungere il valore 5.

## Suddivisione O {#or-split}

Il **Split** crea una suddivisione nel flusso di lavoro, dopodiché sarà attivo un solo ramo. Questo passaggio ti consente di introdurre i percorsi di elaborazione condizionale nel flusso di lavoro. Puoi aggiungere i passaggi del flusso di lavoro a ogni ramo in base alle tue esigenze.

>[!NOTE]
>
>Per ulteriori informazioni sulla creazione di una divisione OR, consulta: [https://helpx.adobe.com/experience-manager/using/aem64_workflow_servlet.html](https://helpx.adobe.com/experience-manager/using/aem64_workflow_servlet.html)

![Ramo con divisione OR](assets/variables_orsplit_new.png)

### Divisione OR - Configurazione {#or-split-configuration}

Per configurare la suddivisione:

* Modifica le **proprietà di divisione OR**:

   * **Comune**

      * Specifica il nome della suddivisione.
   * **Filiali (*x)***

      * **Aggiungi ramo:** aggiungi altri rami al passaggio.
      * **Seleziona espressione** di routing: Selezionare l&#39;espressione di routing per valutare il ramo attivo. I valori possibili sono: Definizione regola, script esterno e script ECMA.
      * **Fare clic per aggiungere un&#39;espressione**: Aggiungi espressione per valutare il ramo attivo se selezioni  **Definizione** regola come espressione di indirizzamento.
      * **Percorso** script: Percorso di un file contenente lo script per valutare il ramo attivo se si seleziona  **External** Scriptas come espressione di indirizzamento.
      * **Script**: Aggiungi lo script nella casella per valutare il ramo attivo se selezioni  **ECMA** Scriptas come espressione di indirizzamento.
      * **Percorso** predefinito: Il ramo predefinito viene seguito nel caso di più rami. Per impostazione predefinita, è possibile specificare un solo ramo.

   >[!NOTE]
   >
   >    * Un ramo viene valutato alla volta in base all&#39;espressione di indirizzamento.
   >    * I rami vengono valutati dall&#39;alto verso il basso.
   >    * Viene eseguito il primo script che restituisce true.
   >    * Se nessun ramo restituisce true, il flusso di lavoro non procede.


   >[!NOTE]
   >
   >Consulta [Definizione di una regola per una divisione OR](/help/sites-developing/workflows-models.md#defineruleecmascript).

* Aggiungi i passaggi del flusso di lavoro ai rami come necessario.

## Passaggi e scelte dei partecipanti {#participant-steps-and-choosers}

### Passaggio partecipante {#participant-step}

Un **Passaggio partecipante** consente di assegnare la proprietà per una particolare azione. Il flusso di lavoro procederà solo quando l’utente ha riconosciuto manualmente il passaggio. Viene utilizzato quando desideri che un utente esegua un’azione sul flusso di lavoro; ad esempio, un passaggio di revisione.

Sebbene non sia direttamente correlata, l’autorizzazione utente deve essere presa in considerazione al momento dell’assegnazione di un’azione; l’utente deve avere accesso alla pagina che è il payload del flusso di lavoro.

#### Passaggio partecipante: configurazione {#participant-step-configuration}

Per configurare il passaggio , modifica e utilizza le seguenti schede:

* [Comune](#step-properties-common-tab)
* [Utente/Gruppo](#step-properties-user-group-tab)

>[!NOTE]
>
>L’iniziatore del flusso di lavoro viene sempre informato quando:
>
>* Il flusso di lavoro viene completato (completato).
>* Il flusso di lavoro viene interrotto (terminato).

>



>[!NOTE]
>
>Per abilitare le notifiche e-mail, è necessario configurare alcune proprietà. Puoi anche personalizzare il modello e-mail o aggiungere un modello e-mail per una nuova lingua. Consulta [Configurazione notifica e-mail](/help/sites-administering/notification.md#configuringemailnotification) per configurare le notifiche e-mail in AEM.

### Passaggio partecipante finestra di dialogo {#dialog-participant-step}

Utilizza un **Passaggio partecipante finestra di dialogo** per raccogliere informazioni dall&#39;utente a cui è assegnato l&#39;elemento di lavoro. Questo passaggio è utile per raccogliere piccole quantità di dati utilizzate più avanti nel flusso di lavoro.

Al termine del passaggio, la finestra di dialogo **Completa elemento di lavoro** contiene i campi definiti nella finestra di dialogo. I dati raccolti nei campi vengono memorizzati nei nodi del payload del flusso di lavoro. I passaggi successivi del flusso di lavoro possono quindi leggere il valore dal repository.

Per configurare il passaggio, specificare il gruppo o l’utente a cui assegnare l’elemento di lavoro e il percorso della finestra di dialogo.

#### Passaggio partecipante finestra di dialogo - Configurazione {#dialog-participant-step-configuration}

Per configurare il passaggio , modifica e utilizza le seguenti schede:

* [Comune](#step-properties-common-tab)
* [Utente/Gruppo](#step-properties-user-group-tab)
* **Finestra di dialogo**

   * **Percorso** finestra di dialogo: Percorso del nodo di dialogo della  [finestra di dialogo creata](#dialog-participant-step-creating-a-dialog).

#### Passaggio partecipante finestra di dialogo - Creazione di una finestra di dialogo {#dialog-participant-step-creating-a-dialog}

Per creare una finestra di dialogo è necessario creare la finestra di dialogo:

* Decidi dove saranno memorizzati i dati risultanti [nel payload](#dialog-participant-step-storing-data-in-the-payload).
* [Definire la finestra di dialogo; ciò include la definizione dei campi utilizzati per raccogliere (e salvare) i dati](#dialog-participant-step-dialog-definition).

#### Passaggio partecipante finestra di dialogo - Memorizzazione dei dati nel payload {#dialog-participant-step-storing-data-in-the-payload}

Puoi memorizzare i dati dei widget nel payload del flusso di lavoro o nei metadati dell’elemento di lavoro. Il formato della proprietà `name` del nodo del widget determina la posizione di memorizzazione dei dati.

* **Archiviare i dati con il payload**

   * Per memorizzare i dati dei widget come proprietà del payload del flusso di lavoro, utilizza il formato seguente per il valore della proprietà name del nodo del widget:
      `./jcr:content/nodename`

   * I dati vengono memorizzati nella proprietà `nodename` del nodo di payload. Se il nodo non contiene tale proprietà, viene creata la proprietà .
   * Quando viene memorizzato con il payload, gli usi successivi della finestra di dialogo con lo stesso payload sovrascrivono il valore della proprietà.

* **Archiviare i dati con l’elemento di lavoro**

   * Per memorizzare i dati dei widget come proprietà dei metadati dell&#39;elemento di lavoro, utilizza il formato seguente per il valore della proprietà name:
      `nodename`

   * I dati vengono memorizzati nella proprietà `nodename` dell&#39;elemento di lavoro `metadata`. I dati vengono conservati se la finestra di dialogo viene successivamente utilizzata con lo stesso payload.

#### Passaggio partecipante finestra di dialogo - Definizione finestra di dialogo {#dialog-participant-step-dialog-definition}

1. **Struttura finestra di dialogo**

   Le finestre di dialogo per i passaggi partecipanti alla finestra di dialogo sono simili alle finestre di dialogo create per creare i componenti. Sono memorizzati in:

   `/apps/myapp/workflow/dialogs`

   Le finestre di dialogo per l’interfaccia touch standard hanno la seguente struttura di nodi:

   ```xml
   newComponent (cq:Component)
     |- cq:dialog (nt:unstructured)
       |- content
         |- layout
           |- items
             |- column
               |- items
                 |- component0
                 |- component1
                 |- ...
   ```

   >[!NOTE]
   >
   >Per ulteriori informazioni, consulta [Creazione e configurazione di una finestra di dialogo](/help/sites-developing/developing-components.md#creating-and-configuring-a-dialog).

1. **Proprietà Percorso finestra di dialogo**

   La proprietà **Dialog Participant Step** include la proprietà **Dialog Path** (insieme alle proprietà di un [Participant Step](#participant-step)). Il valore della proprietà **Percorso finestra di dialogo** rappresenta il percorso del nodo `dialog` della finestra di dialogo.

   Ad esempio, la finestra di dialogo è contenuta in un componente denominato `EmailWatch` memorizzato nel nodo :

   `/apps/myapp/workflows/dialogs`

   Per l’interfaccia touch viene utilizzato il seguente valore per la proprietà **Percorso finestra di dialogo** :

   `/apps/myapp/workflow/dialogs/EmailWatch/cq:dialog`

   ![wf-30](assets/wf-30.png)

1. **Definizione finestra di dialogo di esempio**

   Il seguente frammento di codice XML rappresenta una finestra di dialogo che memorizza un valore `String` nel nodo `watchEmail` del contenuto del payload. Il nodo titolo rappresenta il componente [TextField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/coral/foundation/form/textfield/index.html) :

   ```xml
   jcr:primaryType="nt:unstructured"
       jcr:title="Watcher Email Address Dialog"
       sling:resourceType="cq/gui/components/authoring/dialog">
       <content jcr:primaryType="nt:unstructured"
           sling:resourceType="granite/ui/components/foundation/container">
           <layout jcr:primaryType="nt:unstructured"
               margin="false"
               sling:resourceType="granite/ui/components/foundation/layouts/fixedcolumns"
           />
           <items jcr:primaryType="nt:unstructured">
               <column jcr:primaryType="nt:unstructured"
                   sling:resourceType="granite/ui/components/foundation/container">
                   <items jcr:primaryType="nt:unstructured">
                       <title jcr:primaryType="nt:unstructured"
                           fieldLabel="Notification Email Address"
                           name="./jcr:content/watchEmails"
                           sling:resourceType="granite/ui/components/foundation/form/textfield"
                       />
                   </items>
               </column>
           </items>
       </content>
   </cq:dialog>
   ```

   Questo esempio, nel caso dell’interfaccia touch, darà luogo a una finestra di dialogo come:

   ![chlimage_1-70](assets/chlimage_1-70.png)

### Passaggio partecipante dinamico {#dynamic-participant-step}

Il componente **Passaggio partecipante dinamico** è simile a **[Passaggio partecipante](#participant-step)** con la differenza che il partecipante viene selezionato automaticamente in fase di esecuzione.

Per configurare il passaggio, è necessario selezionare un **Selettore partecipante** che identifichi il partecipante a cui assegnare l&#39;elemento di lavoro, insieme a una finestra di dialogo.

#### Passaggio partecipante dinamico - Configurazione {#dynamic-participant-step-configuration}

Per configurare il passaggio , modifica e utilizza le seguenti schede:

* [Comune](#step-properties-common-tab)
* **Selettore partecipanti**

   * **Selettore** partecipante: Nome del selettore  [partecipante creato](#developingtheparticipantchooser).
   * **Argomenti**: Eventuali argomenti richiesti.
   * **E-mail**: Se inviare una notifica e-mail all’utente.

* **Finestra di dialogo**

   * **Percorso** finestra di dialogo: Percorso del nodo di dialogo della  [finestra di dialogo creata (come con il  **Passaggio partecipante finestra di dialogo**)](#dialog-participant-step-creating-a-dialog).

#### Passaggio partecipante dinamico - Sviluppo del selettore partecipante {#dynamic-participant-step-developing-the-participant-chooser}

Si crea il selettore dei partecipanti. Pertanto, puoi utilizzare qualsiasi logica o criterio di selezione. Ad esempio, il selettore dei partecipanti può selezionare l&#39;utente (all&#39;interno di un gruppo) con il minor numero di elementi di lavoro. È possibile creare un numero qualsiasi di partecipanti che scelgono di utilizzare con istanze diverse del componente **Passaggio partecipante dinamico** nei modelli di flusso di lavoro.

Creare un servizio OSGi o un codice ECMAScript che seleziona un utente a cui assegnare l&#39;elemento di lavoro.

* **ECMAscript**

   Gli script devono includere una funzione denominata getParticipant che restituisce un ID utente come valore `String`. Archivia gli script personalizzati, ad esempio nella cartella `/apps/myapp/workflow/scripts` o in una sottocartella.

   Uno script di esempio è incluso in un&#39;istanza AEM standard:

   `/libs/workflow/scripts/initiator-participant-chooser.ecma`

   >[!CAUTION]
   >
   >***Non è necessario*** modificare nulla nel percorso `/libs`.
   >
   >
   >Questo perché il contenuto di `/libs` viene sovrascritto la prossima volta che aggiorni l&#39;istanza (e può essere sovrascritto quando applichi un hotfix o un feature pack).

   Questo script seleziona l’iniziatore del flusso di lavoro come partecipante:

   ```
   function getParticipant() {
       return workItem.getWorkflow().getInitiator();
   }
   ```

   >[!NOTE]
   >
   >Il componente **Selettore partecipante iniziatore flusso di lavoro** estende il **Passaggio partecipante dinamico** e utilizza questo script come implementazione del passaggio.

* **Servizio OSGi**

   I servizi devono implementare l&#39;interfaccia [com.day.cq.workflow.exec.ParticipantStepChooser](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/workflow/exec/ParticipantStepChooser.html) . L’interfaccia definisce i seguenti membri:

   * `SERVICE_PROPERTY_LABEL` campo: Utilizzare questo campo per specificare il nome del selettore dei partecipanti. Il nome viene visualizzato in un elenco dei selettori dei partecipanti disponibili nelle proprietà **Passaggio partecipante dinamico** .

   * `getParticipant` metodo: Restituisce l&#39;ID principale risolto dinamicamente come  `String` valore.
   >[!CAUTION]
   >
   >Il metodo `getParticipant` restituisce l&#39;ID principale risolto dinamicamente. Può trattarsi di un ID gruppo o di un ID utente.
   >
   >
   >Tuttavia, un id gruppo può essere utilizzato solo per un **Passaggio partecipante**, quando viene restituito un elenco di partecipanti. Per un **Passaggio partecipante dinamico** viene restituito un elenco vuoto che non può essere utilizzato per la delega.

   Per rendere la tua implementazione disponibile ai componenti **Passaggio partecipante dinamico** , aggiungi la tua classe Java a un bundle OSGi che esporta il servizio e distribuisci il bundle sul server AEM.

   >[!NOTE]
   >
   >**Random Participant** Choosers è un servizio di esempio che seleziona un utente casuale (  `com.day.cq.workflow.impl.process.RandomParticipantChooser`). L&#39;esempio di componente **Random Participant Choose** r step estende il **Dynamic Participant Step** e utilizza questo servizio come implementazione passo.

#### Passaggio partecipante dinamico - Esempio di servizio di selezione partecipanti {#dynamic-participant-step-example-participant-chooser-service}

La seguente classe Java implementa l&#39;interfaccia `ParticipantStepChooser` . La classe restituisce il nome del partecipante che ha avviato il flusso di lavoro. Il codice utilizza la stessa logica utilizzata dallo script di esempio (`initiator-participant-chooser.ecma`).

L’annotazione `@Property` imposta il valore del campo `SERVICE_PROPERTY_LABEL` su `Workflow Initiator Participant Chooser`.

```java
package com.adobe.example;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Properties;
import org.apache.felix.scr.annotations.Property;
import org.apache.felix.scr.annotations.Service;
import org.osgi.framework.Constants;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import com.adobe.granite.workflow.WorkflowException;
import com.adobe.granite.workflow.WorkflowSession;
import com.adobe.granite.workflow.exec.ParticipantStepChooser;
import com.adobe.granite.workflow.exec.WorkItem;
import com.adobe.granite.workflow.metadata.MetaDataMap;

@Component
@Service
@Properties({
        @Property(name = Constants.SERVICE_DESCRIPTION, value = "An example implementation of a dynamic participant chooser."),
        @Property(name = ParticipantStepChooser.SERVICE_PROPERTY_LABEL, value = "Workflow Initiator Participant Chooser (service)") })
public class InitiatorParticipantChooser implements ParticipantStepChooser {

 private Logger logger = LoggerFactory.getLogger(this.getClass());

 public String getParticipant(WorkItem arg0, WorkflowSession arg1,
   MetaDataMap arg2) throws WorkflowException {

  String initiator = arg0.getWorkflow().getInitiator();
  logger.info("Assigning Dynamic Participant Step work item to {}",initiator);

  return initiator;
 }
}
```

Nella finestra di dialogo delle proprietà **Passaggio partecipante dinamico** , l&#39;elenco **Selettore partecipante** include l&#39;elemento `Workflow Initiator Participant Chooser (script)` che rappresenta questo servizio.

All’avvio del modello di flusso di lavoro, il registro indica l’ID dell’utente che ha avviato il flusso di lavoro e a chi è assegnato l’elemento di lavoro. In questo esempio, l’utente `admin` ha avviato il flusso di lavoro.

`13.09.2015 15:48:53.037 *INFO* [10.176.129.223 [1347565733037] POST /etc/workflow/instances HTTP/1.1] com.adobe.example.InitiatorParticipantChooser Assigning Dynamic Participant Step work item to admin`

### Passaggio partecipante modulo {#form-participant-step}

Il **Passaggio partecipante al modulo** presenta un modulo quando l’elemento di lavoro viene aperto. Quando l’utente compila e invia il modulo, i dati del campo vengono memorizzati nei nodi del payload del flusso di lavoro.

Per configurare il passaggio, specificare il gruppo o l’utente a cui assegnare l’elemento di lavoro e il percorso del modulo.

>[!CAUTION]
>
>Questa sezione tratta la sezione [Forms dei componenti di base per l&#39;authoring delle pagine](/help/sites-authoring/default-components-foundation.md#form).

#### Passaggio partecipante modulo - Configurazione {#form-participant-step-configuration}

Per configurare il passaggio , modifica e utilizza le seguenti schede:

* [Comune](#step-properties-common-tab)
* [Utente/Gruppo](#step-properties-user-group-tab)
* **Modulo**

   * **Percorso** modulo: Percorso del  [modulo creato](#form-participant-step-creating-the-form).

#### Passaggio partecipante modulo - Creazione del modulo {#form-participant-step-creating-the-form}

Creare un modulo da utilizzare normalmente con un **Passaggio partecipante al modulo**. Tuttavia, i moduli per un Passaggio partecipante a un modulo devono avere le seguenti configurazioni:

* Per il componente **Inizio modulo** deve essere impostata la proprietà **Tipo azione** su `Edit Workflow Controlled Resource(s)`.
* Il componente **Inizio modulo** deve avere un valore per la proprietà `Form Identifier` .
* Ai componenti modulo deve essere impostata la proprietà **Nome elemento** sul percorso del nodo in cui sono memorizzati i dati del campo. Il percorso deve individuare un nodo nel contenuto del payload del flusso di lavoro. Il valore utilizza il formato seguente:

   `./jcr:content/path_to_node`

* Il modulo deve includere un componente **Pulsante di invio flusso di lavoro**. Non configuri proprietà del componente.

I requisiti del flusso di lavoro determinano dove memorizzare i dati dei campi. Ad esempio, i dati dei campi possono essere utilizzati per configurare le proprietà del contenuto della pagina. Il seguente valore di una proprietà **Nome elemento** memorizza i dati del campo come valore della proprietà `redirectTarget` del nodo `jcr:content`:

`./jcr:content/redirectTarget`

Nell’esempio seguente, i dati dei campi vengono utilizzati come contenuto di un componente **Testo** nella pagina del payload:

`./jcr:content/par/text_3/text`

Il primo esempio può essere utilizzato per qualsiasi pagina sottoposta a rendering dal componente `cq:Page` . Il secondo esempio può essere utilizzato solo quando la pagina di payload include un componente **Testo** con un ID di `text_3`.

Il modulo può trovarsi in qualsiasi punto dell’archivio, tuttavia gli utenti del flusso di lavoro devono essere autorizzati a leggere il modulo.

### Selettore casuale partecipanti {#random-participant-chooser}

Il passaggio **Selettore casuale partecipante** è un selettore partecipante che assegna l’elemento di lavoro generato a un utente selezionato in modo casuale da un elenco.

![wf-31](assets/wf-31.png)

#### Selettore casuale partecipanti - Configurazione {#random-participant-chooser-configuration}

Per configurare il passaggio , modifica e utilizza le seguenti schede:

* [Comune](#step-properties-common-tab)
* **Argomenti**

   * **Partecipanti**: Specifica l&#39;elenco di utenti disponibili per la selezione. Per aggiungere un utente all&#39;elenco, fare clic su **Aggiungi elemento** e digitare il percorso principale del nodo utente o l&#39;ID utente. L&#39;ordine degli utenti non influisce sulla probabilità di assegnazione di un elemento di lavoro.

### Selettore partecipante iniziatore flusso di lavoro {#workflow-initiator-participant-chooser}

Il passaggio **Selettore partecipante iniziatore flusso di lavoro** è un selettore dei partecipanti che assegna l’elemento di lavoro generato all’utente che ha avviato il flusso di lavoro. Non sono disponibili proprietà da configurare diverse dalle proprietà **Common** .

#### Selettore partecipante iniziatore flusso di lavoro - Configurazione {#workflow-initiator-participant-chooser-configuration}

Per configurare il passaggio , modifica utilizzando le seguenti schede:

* [Comune](#step-properties-common-tab)

## Passaggio processo {#process-step}

Un **Passaggio processo** esegue un ECMAScript o chiama un servizio OSGi per eseguire l&#39;elaborazione automatica.

![wf-32](assets/wf-32.png)

### Passaggio del processo: configurazione {#process-step-configuration}

Per configurare il passaggio , modifica e utilizza le seguenti schede:

* [Comune](#step-properties-common-tab)
* **Processo**

   * **Processo**: Implementazione del processo da eseguire. Utilizzare il menu a discesa per selezionare il servizio ECMAScript o OSGi. Per informazioni su:

      * I servizi standard ECMAScripts e OSGi, vedi [Processi incorporati per i passaggi del processo](/help/sites-developing/workflows-process-ref.md).
      * Creazione di script ECMAS per un passaggio del processo, vedere [Implementazione di un passaggio del processo con ECMAScript](/help/sites-developing/workflows-customizing-extending.md#using-ecmascript).
      * Creazione di servizi OSGi per un passaggio del processo, consulta [Implementazione di un passaggio del processo con una classe Java](/help/sites-developing/workflows-customizing-extending.md#implementing-a-process-step-with-a-java-class).
   * **Avanzamento** gestore: Seleziona questa opzione per avanzare automaticamente il flusso di lavoro al passaggio successivo dopo l’esecuzione. Se non è selezionato, lo script di implementazione deve gestire l’avanzamento del flusso di lavoro.
   * **Argomenti**: Argomenti da passare al processo.


## Imposta variabile {#set-variable}

Il passaggio Imposta variabile consente di impostare il valore di una variabile e di definire l’ordine in cui i valori vengono impostati. La variabile viene impostata nell’ordine in cui le mappature delle variabili sono elencate nel passaggio Imposta variabile .

![Aggiungi mappatura per impostare una variabile](assets/set_variable_addmappingnew.png)

### Imposta variabile - Configurazione {#setvariable}

Per configurare il passaggio , modifica e utilizza le seguenti schede:

* [Comune](/help/sites-developing/workflows-step-ref.md#step-properties-common-tab)
* **Mappatura**

   * **Seleziona variabile:** utilizza questa opzione per selezionare una variabile per impostarne il valore.
   * **Seleziona Modalità di mappatura:**  seleziona una modalità di mappatura per impostare il valore della variabile. A seconda del tipo di dati della variabile, è possibile utilizzare le seguenti opzioni per impostare il valore di una variabile:

      * **Letterale:** utilizza l’opzione se conosci il valore esatto da specificare.
      * **Espressione:** utilizza l’opzione quando il valore da utilizzare viene calcolato in base a un’espressione. L’espressione viene creata nell’editor di espressioni fornito.
      * **Notazione del punto JSON:** utilizza l’opzione per recuperare un valore da una variabile di tipo JSON o FDM.
      * **XPATH:** utilizza l&#39;opzione per recuperare un valore da una variabile di tipo XML.
      * **Relativo al payload:** utilizza l’opzione quando il valore da salvare nella variabile è disponibile in un percorso relativo al payload.
      * **Percorso assoluto:** utilizza l’opzione quando il valore da salvare nella variabile è disponibile in un percorso assoluto.
   * **Specifica valore:** specifica un valore da mappare alla variabile. Il valore specificato in questo campo dipende dalla modalità di mappatura.
   * **Aggiungi mappatura:** utilizza questa opzione per aggiungere altre mappature per impostare un valore per la variabile.
