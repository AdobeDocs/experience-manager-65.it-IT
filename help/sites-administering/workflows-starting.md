---
title: Avvio dei flussi di lavoro
seo-title: Avvio dei flussi di lavoro
description: Scopri come avviare flussi di lavoro in AEM.
seo-description: Scopri come avviare flussi di lavoro in AEM.
uuid: 0648d335-ecce-459d-95fd-3d4d76181b32
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: e9ab4796-a050-40de-b073-af7d33cff009
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '804'
ht-degree: 5%

---


# Avvio dei flussi di lavoro{#starting-workflows}

Quando amministri flussi di lavoro puoi avviarli utilizzando diversi metodi:

* Manualmente:

   * Da un [modello di flusso di lavoro](#workflow-models).
   * Utilizzo di un pacchetto di workflow per l&#39; [elaborazione batch](#workflow-packages-for-batch-processing).

* Automaticamente:

   * In risposta alle modifiche ai nodi; [utilizzando un Launcher](#workflows-launchers).

>[!NOTE]
>
>Altri metodi sono disponibili anche per gli autori; per maggiori dettagli, consulta:
>
>* [Applicazione dei flussi di lavoro alle pagine](/help/sites-authoring/workflows-applying.md)
>* [Come applicare i flussi di lavoro alle risorse DAM](/help/assets/assets-workflow.md)
>* [AEM Forms](https://helpx.adobe.com/aem-forms/6-2/aem-workflows-submit-process-form.html)
>* [Progetti traduzione](/help/sites-administering/tc-manage.md)

>



## Modelli flusso di lavoro {#workflow-models}

È possibile avviare un flusso di lavoro [in base a uno dei modelli](/help/sites-administering/workflows.md#workflow-models-and-instances) elencati nella console Modelli di workflow. L’unica informazione obbligatoria è il payload, anche se è possibile aggiungere un titolo e/o un commento.

## Lanci flussi di lavoro {#workflows-launchers}

Workflow Launcher monitora le modifiche nell&#39;archivio dei contenuti per avviare flussi di lavoro in base alla posizione e al tipo di risorsa del nodo modificato.

Utilizzando **Launcher** è possibile:

* Vedere i flussi di lavoro già avviati per nodi specifici.
* Selezionare un flusso di lavoro da avviare quando un determinato nodo/tipo di nodo è stato creato/modificato/rimosso.
* Rimuovere una relazione esistente tra workflow e nodo.

È possibile creare un avvio per qualsiasi nodo. Tuttavia, le modifiche apportate a determinati nodi non avviano flussi di lavoro. Le modifiche apportate ai nodi sotto i seguenti percorsi non causano l&#39;avvio di flussi di lavoro:

* `/var/workflow/instances`
* Qualsiasi nodo Workflow-inbox ubicato in un punto qualsiasi del ramo `/home/users`
* `/tmp`
* `/var/audit`
* `/var/classes`
* `/var/eventing`
* `/var/linkchecker`
* `/var/mobile`
* `/var/statistics`

   * Eccezione: Le modifiche apportate ai nodi sotto `/var/statistics/tracking` *do* causano l&#39;avvio dei flussi di lavoro.

Diverse definizioni sono incluse nell&#39;installazione standard. Sono utilizzati per le attività di gestione delle risorse digitali e di collaborazione social:

![wf-100](assets/wf-100.png)

## Pacchetti di flussi di lavoro per l&#39;elaborazione batch {#workflow-packages-for-batch-processing}

I pacchetti di workflow sono pacchetti che possono essere passati a un flusso di lavoro come payload per l&#39;elaborazione, consentendo l&#39;elaborazione di più risorse.

Un pacchetto di workflow:

* contiene collegamenti a un set di risorse (come pagine, risorse).
* contiene informazioni sul pacchetto, ad esempio la data di creazione, l&#39;utente che ha creato il pacchetto e una breve descrizione.
* è definito utilizzando un modello di pagina specializzato; tali pagine consentono all&#39;utente di specificare le risorse nel pacchetto.
* può essere utilizzato più volte.
* può essere modificato dall&#39;utente (aggiungi o rimuovi risorse) mentre l&#39;istanza del flusso di lavoro è in esecuzione.

## Avvio di un flusso di lavoro dalla console Modelli {#starting-a-workflow-from-the-models-console}

1. Andate alla console **Modelli** utilizzando **Strumenti**, **Flusso di lavoro**, quindi **Modelli**.
1. Selezionate il flusso di lavoro (in base alla vista della console); potete anche utilizzare Cerca (in alto a sinistra) se necessario:

   ![wf-103](assets/wf-103.png)

   >[!NOTE]
   >
   >L&#39;indicatore **[Transient](/help/sites-developing/workflows.md#transient-workflows)** mostra i flussi di lavoro per i quali la cronologia del flusso di lavoro non sarà persistente.

1. Selezionare **Avvia flusso di lavoro** dalla barra degli strumenti.
1. Viene visualizzata la finestra di dialogo Esegui flusso di lavoro, che consente di specificare:

   * **Payload**

      Può trattarsi di una pagina, un nodo, una risorsa, un pacchetto, tra le altre risorse.

   * **Titolo**

      Titolo facoltativo per identificare l’istanza.

   * **Commento**

      Un commento facoltativo per aiutare a indicare i dettagli di questa istanza.
   ![wf-104](assets/wf-104.png)

## Creazione di una configurazione di avvio {#creating-a-launcher-configuration}

1. Andate alla console **Workflow Launchers** utilizzando **Tools**, **Workflow**, quindi **Launchers**.
1. Selezionare **Crea**, quindi **Aggiungi avvio** per aprire la finestra di dialogo:

   ![wf-105](assets/wf-105.png)

   * **Tipo evento**

      Il tipo di evento che avvia il flusso di lavoro:

      * Creato
      * Modificato
      * Rimosso
   * **Notetype**

      Il tipo di nodo a cui si applica l&#39;avvio del flusso di lavoro.

   * **Percorso**

      Percorso a cui si applica l&#39;avvio del flusso di lavoro.

   * **Modalità di esecuzione**

      Il tipo di server a cui si applica l&#39;avvio del flusso di lavoro. Selezionare **Autore**, **Pubblica** o **Autore e pubblicazione**.

   * **Condizioni**

      Un elenco di condizioni per i valori dei nodi che, se valutati, determinano se il flusso di lavoro viene avviato. Ad esempio, la condizione seguente determina l&#39;avvio del flusso di lavoro quando il nodo ha un nome di proprietà con il valore Utente:

      name==Utente

   * **Funzioni**

      Elenco delle funzioni da abilitare. Selezionate le feature desiderate utilizzando il selettore a discesa.

   * **Funzioni disabilitate**

   Elenco delle funzioni da disattivare. Selezionate le feature desiderate utilizzando il selettore a discesa.

   * **Modello flusso di lavoro**

      Il flusso di lavoro da avviare quando il tipo di evento si verifica sul tipo di nodo e/o sul percorso in base alla condizione definita.

   * **Descrizione**

      Testo personale per descrivere e identificare la configurazione del modulo di avvio.

   * **Attiva**

      Controlla se l’avvio del flusso di lavoro è attivato:

      * Selezionare **Abilita** per avviare flussi di lavoro quando le proprietà di configurazione sono soddisfatte.
      * Selezionare **Disattiva** quando il flusso di lavoro non deve essere eseguito (non anche quando le proprietà di configurazione sono soddisfatte).
   * **Escludi elenco**

      Specifica tutti gli eventi JCR da escludere (ovvero da ignorare) quando si determina se un flusso di lavoro deve essere attivato.

      Questa proprietà di avvio è un elenco separato da virgole di elementi: &quot;

      * `property-name` ignora qualsiasi  `jcr` evento attivato sul nome della proprietà specificata. &quot;
      * `event-user-data:<*someValue*>` ignora qualsiasi evento che contiene il  `*<someValue*`>  `user-data` impostato tramite l&#39; [ `ObservationManager` API] (https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/observation/ObservationManager.html#setUserData(java.lang.String).

      Esempio:

      `jcr:lastModified,dc:modified,dc:format,jcr:lastModifiedBy,imageMap,event-user-data:changedByWorkflowProcess`

      Questa funzione può essere utilizzata per ignorare le modifiche avviate da un altro processo di workflow aggiungendo l’elemento exclude:

      `event-user-data:changedByWorkflowProcess`





1. Selezionare **Crea** per creare il modulo di avvio e tornare alla console.

   Una volta che si verifica l&#39;evento appropriato, viene avviato il programma di avvio e il flusso di lavoro viene avviato.

## Gestione di una configurazione di avvio {#managing-a-launcher-configuration}

Dopo aver creato la configurazione di avvio, è possibile utilizzare la stessa console per selezionare l&#39;istanza, quindi **Visualizza proprietà** (e modificarle) o **Elimina**.
