---
title: Amministrazione delle istanze dei flussi di lavoro
seo-title: Administering Workflow Instances
description: Scopri come amministrare le istanze dei flussi di lavoro.
seo-description: Lear how to administer Workflow Instances.
uuid: 81e53ef5-fe62-4ed4-b2d4-132aa986d5aa
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: d9c96e7f-9416-48e1-a6af-47384f7bee92
exl-id: 90923d39-3ac5-4028-976c-d011f0404476
source-git-commit: 8b4459c69b73159ce5afd819dfb772df5c51cd16
workflow-type: tm+mt
source-wordcount: '1136'
ht-degree: 0%

---

# Amministrazione delle istanze dei flussi di lavoro{#administering-workflow-instances}

La console del flusso di lavoro fornisce diversi strumenti per l’amministrazione delle istanze del flusso di lavoro, in modo che vengano eseguite come previsto.

>[!NOTE]
>
>La [Console JMX](/help/sites-administering/jmx-console.md#workflow-maintenance) fornisce ulteriori operazioni di manutenzione del flusso di lavoro.

Sono disponibili diverse console per l’amministrazione dei flussi di lavoro. Utilizza la [navigazione globale](/help/sites-authoring/basic-handling.md#global-navigation) per aprire **Strumenti** riquadro, quindi selezionare **Flusso di lavoro**:

* **Modelli**: Gestire le definizioni dei flussi di lavoro
* **Istanze**: Visualizzare e gestire le istanze del flusso di lavoro in esecuzione
* **Lanci**: Gestire il modo in cui avviare i flussi di lavoro
* **Archivia**: Visualizzare la cronologia dei flussi di lavoro completati correttamente
* **Errori**: Visualizzare la cronologia dei flussi di lavoro completati con errori
* **Assegnazione automatica**: Configurare l’assegnazione automatica dei flussi di lavoro ai modelli

## Monitoraggio dello stato delle istanze del flusso di lavoro {#monitoring-the-status-of-workflow-instances}

1. Selezione tramite navigazione **Strumenti**, quindi **Flusso di lavoro**.
1. Seleziona **Istanze** per visualizzare l’elenco delle istanze del flusso di lavoro attualmente in corso.

   ![wf-96](assets/wf-96.png)


## Cerca istanze del flusso di lavoro {#search-workflow-instances}

1. Selezione tramite navigazione **Strumenti**, quindi **Flusso di lavoro**.
1. Seleziona **Istanze** per visualizzare l’elenco delle istanze del flusso di lavoro attualmente in corso. Nella barra superiore, nell’angolo sinistro, seleziona **Filtri**. In alternativa, è possibile utilizzare i tasti alt+1. Viene visualizzata la seguente finestra di dialogo:

   ![wf-99-1](assets/wf-99-1.png)

1. Nella finestra di dialogo Filtro , seleziona i criteri di ricerca del flusso di lavoro. Puoi eseguire ricerche in base ai seguenti input:

   * Percorso payload: Selezionare un percorso specifico
   * Modello di flusso di lavoro: Selezionare un modello di flusso di lavoro
   * Assegnatario: Selezionare un assegnatario del flusso di lavoro
   * Tipo: Attività, elemento del flusso di lavoro o errore del flusso di lavoro
   * Stato attività: Attivo, Completo o Terminato
   * Dove Sono: Proprietario e assegnatario, solo proprietario, solo assegnatario
   * Data di inizio: Data di inizio prima o dopo una data specificata
   * Data di fine: Data di fine prima o dopo una data specificata
   * Data di scadenza: Data di scadenza prima o dopo una data specificata
   * Data aggiornamento: Data aggiornata prima o dopo una data specificata

## Sospensione, ripresa e chiusura di un’istanza di flusso di lavoro {#suspending-resuming-and-terminating-a-workflow-instance}

1. Selezione tramite navigazione **Strumenti**, quindi **Flusso di lavoro**.
1. Seleziona **Istanze** per visualizzare l’elenco delle istanze del flusso di lavoro attualmente in corso.

   ![wf-96-1](assets/wf-96-1.png)

1. Seleziona un elemento specifico, quindi utilizza **Termina**, **Sospendi** oppure **Riprendi**, se del caso; conferma e/o ulteriori dettagli sono richiesti:

   ![wf-97-1](assets/wf-97-1.png)

## Visualizzazione dei flussi di lavoro archiviati {#viewing-archived-workflows}

1. Selezione tramite navigazione **Strumenti**, quindi **Flusso di lavoro**.
1. Seleziona **Archivia** per visualizzare l’elenco delle istanze del flusso di lavoro completate correttamente.

   ![wf-98](assets/wf-98.png)

   >[!NOTE]
   >
   >Lo stato di interruzione viene considerato come una terminazione corretta in quanto si verifica in seguito a un&#39;azione dell&#39;utente; ad esempio:
   >
   >* utilizzo **Termina** action
   >* quando una pagina, soggetta a un flusso di lavoro, viene (forzata) eliminata, il flusso di lavoro viene terminato


1. Seleziona un elemento specifico, quindi **Cronologia aperta** per ulteriori dettagli:

   ![wf-99](assets/wf-99.png)

## Correzione degli errori di un&#39;istanza del flusso di lavoro {#fixing-workflow-instance-failures}

Quando un flusso di lavoro non riesce, AEM fornisce la **Errori** console per indagare e intraprendere azioni appropriate una volta gestita la causa originale:

* **Dettagli errore**
Apre una finestra per visualizzare 
**Messaggio di errore**, **Passaggio** e **Stack errori**.

* **Cronologia aperta**
Mostra i dettagli della cronologia del flusso di lavoro.

* **Passaggio del nuovo tentativo** Esegue nuovamente l&#39;istanza del componente Passaggio script. Utilizzare il comando Riprova passaggio dopo aver risolto la causa dell&#39;errore originale. Ad esempio, prova a ripetere il passaggio dopo aver corretto un bug nello script eseguito dal passaggio del processo.
* **Termina** Termina il flusso di lavoro se l’errore ha causato una situazione irreprensibile per il flusso di lavoro. Ad esempio, il flusso di lavoro può basarsi su condizioni ambientali quali le informazioni nell’archivio che non sono più valide per l’istanza del flusso di lavoro.
* **Termina e riprova** Simile a **Termina** tranne per il fatto che una nuova istanza di flusso di lavoro viene avviata utilizzando il payload, il titolo e la descrizione originali.

Per indagare gli errori, quindi riprendere o terminare il flusso di lavoro in seguito, utilizza i seguenti passaggi:

1. Selezione tramite navigazione **Strumenti**, quindi **Flusso di lavoro**.
1. Seleziona **Errori** per visualizzare l’elenco delle istanze del flusso di lavoro che non sono state completate correttamente.
1. Seleziona un elemento specifico, quindi l’azione appropriata:

   ![wf-47](assets/wf-47.png)

## Rimozione regolare delle istanze del flusso di lavoro {#regular-purging-of-workflow-instances}

Minimizzare il numero di istanze del flusso di lavoro aumenta le prestazioni del motore del flusso di lavoro, in modo da poter eliminare regolarmente dall’archivio le istanze del flusso di lavoro completate o in esecuzione.

Configura **Configurazione di eliminazione del flusso di lavoro di Adobe Granite** per eliminare le istanze del flusso di lavoro in base alla loro età e al loro stato. È inoltre possibile eliminare le istanze del flusso di lavoro di tutti i modelli o di un modello specifico.

Puoi anche creare più configurazioni del servizio per eliminare le istanze del flusso di lavoro che soddisfano criteri diversi. Ad esempio, crea una configurazione che elimina le istanze di un particolare modello di flusso di lavoro quando sono in esecuzione per molto più tempo del tempo previsto. Crea un’altra configurazione che elimina tutti i flussi di lavoro completati dopo un certo numero di giorni per ridurre al minimo le dimensioni dell’archivio.

Per configurare il servizio, puoi utilizzare la funzione [Console web](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) o [aggiungi una configurazione OSGi all’archivio](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository). Nella tabella seguente sono descritte le proprietà necessarie per entrambi i metodi.

>[!NOTE]
>
>Per aggiungere la configurazione all’archivio, il PID del servizio è:
>
>`com.adobe.granite.workflow.purge.Scheduler`
>
>Poiché il servizio è un servizio di fabbrica, il nome `sling:OsgiConfig` Il nodo richiede un suffisso di identificatore, ad esempio:
>
>`com.adobe.granite.workflow.purge.Scheduler-myidentifier`

<table>
 <tbody>
  <tr>
   <th>Nome proprietà (console Web)</th>
   <th>Nome proprietà OSGi</th>
   <th>Descrizione</th>
  </tr>
  <tr>
   <td>Nome processo</td>
   <td>scheduledpurge.name</td>
   <td>Un nome descrittivo per l'eliminazione pianificata.</td>
  </tr>
  <tr>
   <td>Stato flusso di lavoro</td>
   <td>scheduledpurge.workflowStatus</td>
   <td><p>Lo stato delle istanze del flusso di lavoro da eliminare. I seguenti valori sono validi:</p>
    <ul>
     <li>COMPLETATO: Le istanze del flusso di lavoro completate vengono eliminate.</li>
     <li>IN ESECUZIONE: Le istanze del flusso di lavoro in esecuzione vengono eliminate.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Modelli da eliminare</td>
   <td>scheduledpurge.modelIds</td>
   <td><p>ID dei modelli di flusso di lavoro da eliminare. L'ID è il percorso del nodo del modello, ad esempio:<br /> /conf/global/settings/workflow/models/dam/update_asset/jcr:content/model<br /> Non specificare alcun valore per eliminare le istanze di tutti i modelli di flusso di lavoro.</p> <p>Per specificare più modelli, fare clic sul pulsante + nella console Web. </p> </td>
  </tr>
  <tr>
   <td>Età del flusso di lavoro</td>
   <td>scheduledpurge.daysold</td>
   <td>L’età in giorni delle istanze del flusso di lavoro da eliminare.</td>
  </tr>
 </tbody>
</table>

## Impostazione della dimensione massima della casella in entrata {#setting-the-maximum-size-of-the-inbox}

Puoi impostare la dimensione massima della casella in entrata configurando la **Servizio flusso di lavoro di Adobe Granite**, utilizzando [Console web](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) o [aggiungi una configurazione OSGi all’archivio](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository). Nella tabella seguente viene descritta la proprietà configurata per entrambi i metodi.

>[!NOTE]
>
>Per aggiungere la configurazione all’archivio, il PID del servizio è:
>
>`com.adobe.granite.workflow.core.WorkflowSessionFactory`.

| Nome proprietà (console Web) | Nome proprietà OSGi |
|---|---|
| Dimensione massima query casella in entrata | granite.workflow.inboxQuerySize |

## Utilizzo delle variabili del flusso di lavoro per i datastore di proprietà del cliente {#using-workflow-variables-customer-datastore}

I dati elaborati dai flussi di lavoro vengono memorizzati nell’Adobe fornito di storage (JCR). Questi dati possono essere sensibili in natura. È possibile salvare tutti i metadati/dati definiti dall&#39;utente nell&#39;archivio gestito anziché nell&#39;archiviazione fornita dall&#39;Adobe. In queste sezioni viene descritto come impostare queste variabili per lo storage esterno.

### Impostare il modello per l&#39;utilizzo dello storage esterno dei metadati {#set-model-for-external-storage}

A livello di modello di flusso di lavoro, viene fornito un flag per indicare che il modello (e le sue istanze di runtime) dispone di archiviazione esterna dei metadati. Le variabili del flusso di lavoro non verranno mantenute in JCR per le istanze del flusso di lavoro dei modelli contrassegnati per lo storage esterno.

La proprietà *userMetadataPersistenceEnabled* verranno memorizzati nel *jcr:content node* del modello di flusso di lavoro. Questo flag viene mantenuto nei metadati del flusso di lavoro come *cq:userMetaDataCustomPersistenceEnabled*.

L’illustrazione seguente mostra come impostare il flag su un flusso di lavoro.

![workflow-externalize-config](assets/workflow-externalize-config.png)

### API per metadati nello storage esterno {#apis-for-metadata-external-storage}

Per memorizzare le variabili esternamente, devi implementare le API che il flusso di lavoro espone.

UserMetaDataPersistenceContext

Gli esempi seguenti mostrano come utilizzare l’API .

```
@ProviderType
public interface UserMetaDataPersistenceContext {
 
    /**
     * Gets the workflow for persistence
     * @return workflow
     */
    Workflow getWorkflow();
 
    /**
     * Gets the workflow id for persistence
     * @return workflowId
     */
    String getWorkflowId();
 
    /**
     * Gets the user metadata persistence id
     * @return userDataId
     */
    String getUserDataId();
}
```

UserMetaDataPersistenceProvider

```
/**
 * This provider can be implemented to store the user defined workflow-data metadata in a custom storage location
 */
@ConsumerType
public interface UserMetaDataPersistenceProvider {
 
   /**
    * Retrieves the metadata using a unique identifier
    * @param userMetaDataPersistenceContext
    * @param metaDataMap of user defined workflow data metaData
    * @throws WorkflowException
    */
   void get(UserMetaDataPersistenceContext userMetaDataPersistenceContext, MetaDataMap metaDataMap) throws WorkflowException;
 
   /**
    * Stores the given metadata to the custom storage location
    * @param userMetaDataPersistenceContext
    * @param metaDataMap metadata map
    * @return the unique identifier that can be used to retrieve metadata. If null is returned, then workflowId is used.
    * @throws WorkflowException
    */
   String put(UserMetaDataPersistenceContext userMetaDataPersistenceContext, MetaDataMap metaDataMap) throws WorkflowException;
} 
```
