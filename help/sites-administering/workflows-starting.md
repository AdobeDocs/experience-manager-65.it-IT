---
title: Avvio dei flussi di lavoro
seo-title: Starting Workflows
description: Scopri come avviare Flussi di lavoro in AEM.
seo-description: Learn how to start Workflows in AEM.
uuid: 0648d335-ecce-459d-95fd-3d4d76181b32
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: e9ab4796-a050-40de-b073-af7d33cff009
exl-id: 84a1964c-4121-4763-b946-9eee6093747d
source-git-commit: 2bae11eafb875f01602c39c0dba00a888e11391a
workflow-type: tm+mt
source-wordcount: '794'
ht-degree: 6%

---

# Avvio dei flussi di lavoro{#starting-workflows}

Quando amministri flussi di lavoro puoi avviarli utilizzando diversi metodi:

* Manualmente:

   * Da un [modello di flusso di lavoro](#workflow-models).
   * Utilizzo di un pacchetto di flusso di lavoro per [elaborazione batch](#workflow-packages-for-batch-processing).

* Automaticamente:

   * In risposta alle modifiche ai nodi; [utilizzando un Launcher](#workflows-launchers).

>[!NOTE]
>
>Sono disponibili anche altri metodi per gli autori; per maggiori dettagli consultare:
>
>* [Applicazione dei flussi di lavoro alle pagine](/help/sites-authoring/workflows-applying.md)
>* [Come applicare i flussi di lavoro alle risorse DAM](/help/assets/assets-workflow.md)
>* [AEM Forms](https://helpx.adobe.com/aem-forms/6-2/aem-workflows-submit-process-form.html)
>* [Progetti traduzione](/help/sites-administering/tc-manage.md)

>


## Modelli flusso di lavoro {#workflow-models}

Puoi avviare un flusso di lavoro [basato su uno dei modelli](/help/sites-administering/workflows.md#workflow-models-and-instances) elencati nella console Modelli di flusso di lavoro . L’unica informazione obbligatoria è il payload, anche se è possibile aggiungere un titolo e/o un commento.

## Moduli di avvio dei flussi di lavoro {#workflows-launchers}

Workflow Launcher monitora le modifiche nell’archivio dei contenuti per avviare flussi di lavoro in base alla posizione e al tipo di risorsa del nodo modificato.

Utilizzando **Launcher** puoi:

* Vedi i flussi di lavoro già avviati per nodi specifici.
* Seleziona un flusso di lavoro da avviare quando è stato creato/modificato/rimosso un determinato tipo di nodo/nodo.
* Rimuovi una relazione esistente tra workflow e nodo.

Puoi creare un modulo di avvio per qualsiasi nodo. Tuttavia, le modifiche a determinati nodi non avviano flussi di lavoro. Le modifiche ai nodi sotto i percorsi seguenti non causano l&#39;avvio dei flussi di lavoro:

* `/var/workflow/instances`
* Qualsiasi nodo della casella in entrata del flusso di lavoro in un punto qualsiasi del ramo `/home/users`
* `/tmp`
* `/var/audit`
* `/var/classes`
* `/var/eventing`
* `/var/linkchecker`
* `/var/mobile`
* `/var/statistics`

   * Eccezione: Le modifiche ai nodi sotto `/var/statistics/tracking` *do* causano l&#39;avvio dei flussi di lavoro.

L’installazione standard include diverse definizioni. Vengono utilizzati per le attività di gestione delle risorse digitali e di collaborazione sociale:

![wf-100](assets/wf-100.png)

## Pacchetti di flussi di lavoro per l&#39;elaborazione in batch {#workflow-packages-for-batch-processing}

I pacchetti di flussi di lavoro sono pacchetti che possono essere passati a un flusso di lavoro come payload per l’elaborazione, consentendo l’elaborazione di più risorse.

Un pacchetto di flusso di lavoro:

* contiene collegamenti a un set di risorse (ad esempio pagine, risorse).
* contiene informazioni sul pacchetto come la data di creazione, l&#39;utente che ha creato il pacchetto e una breve descrizione.
* è definito utilizzando un modello di pagina specializzato; tali pagine consentono all’utente di specificare le risorse nel pacchetto.
* può essere utilizzato più volte.
* può essere modificato dall’utente (aggiungi o rimuovi risorse) mentre l’istanza del flusso di lavoro è in esecuzione.

## Avvio di un flusso di lavoro dalla console Modelli {#starting-a-workflow-from-the-models-console}

1. Passa alla console **Modelli** utilizzando **Strumenti**, **Flusso di lavoro**, quindi **Modelli**.
1. Seleziona il flusso di lavoro (in base alla vista della console); puoi anche utilizzare Ricerca (in alto a sinistra) se necessario:

   ![wf-103](assets/wf-103.png)

   >[!NOTE]
   >
   >L&#39;indicatore **[Transient](/help/sites-developing/workflows.md#transient-workflows)** mostra i flussi di lavoro per i quali la cronologia del flusso di lavoro non verrà mantenuta.

1. Seleziona **Avvia flusso di lavoro** dalla barra degli strumenti.
1. Viene visualizzata la finestra di dialogo Esegui flusso di lavoro , che consente di specificare:

   * **Payload**

      Può essere una pagina, un nodo, una risorsa, un pacchetto, tra le altre risorse.

   * **Titolo**

      Un titolo facoltativo per identificare l’istanza.

   * **Commento**

      Un commento facoltativo per indicare i dettagli di questa istanza.
   ![wf-104](assets/wf-104.png)

## Creazione di una configurazione Launcher {#creating-a-launcher-configuration}

1. Passa alla console **Workflow Launcher** utilizzando **Strumenti**, **Flusso di lavoro**, quindi **Moduli di avvio**.
1. Seleziona **Crea**, quindi **Aggiungi Launcher** per aprire la finestra di dialogo:

   ![wf-105](assets/wf-105.png)

   * **Tipo evento**

      Il tipo di evento che avvierà il flusso di lavoro:

      * Creato
      * Modificato
      * Rimosso
   * **Tipo di nodo**

      Il tipo di nodo a cui si applica il modulo di avvio del flusso di lavoro.

   * **Percorso**

      Percorso a cui si applica il modulo di avvio del flusso di lavoro.

   * **Modalità di esecuzione**

      Il tipo di server a cui si applica il modulo di avvio del flusso di lavoro. Seleziona **Autore**, **Pubblica** o **Autore e pubblicazione**.

   * **Condizioni**

      Elenco di condizioni per i valori dei nodi che, una volta valutati, determinano se il flusso di lavoro viene avviato. Ad esempio, la seguente condizione causa l’avvio del flusso di lavoro quando il nodo ha un nome di proprietà con il valore Utente:

      name==Utente

   * **Funzioni**

      Elenco di funzioni da abilitare. Seleziona le feature desiderate utilizzando il selettore a discesa.

   * **Funzioni disabilitate**

   Elenco delle funzioni da disattivare. Seleziona le feature desiderate utilizzando il selettore a discesa.

   * **Modello flusso di lavoro**

      Il flusso di lavoro da avviare quando il tipo di evento si verifica sul tipo di nodo e/o sul percorso sotto la condizione definita.

   * **Descrizione**

      Testo personalizzato per descrivere e identificare la configurazione del modulo di avvio.

   * **Attiva**

      Controlla se il modulo di avvio del flusso di lavoro è attivato:

      * Seleziona **Abilita** per avviare i flussi di lavoro quando le proprietà di configurazione sono soddisfatte.
      * Seleziona **Disabilita** quando il flusso di lavoro non deve essere eseguito (anche quando le proprietà di configurazione sono soddisfatte).
   * **Escludi elenco**

      Questo specifica eventuali eventi JCR da escludere (cioè ignorare) quando si determina se un flusso di lavoro deve essere attivato.

      Questa proprietà di avvio è un elenco separato da virgole di elementi: &quot;

      * `property-name` ignora qualsiasi  `jcr` evento attivato sul nome della proprietà specificato. &quot;
      * `event-user-data:<*someValue*>` ignora qualsiasi evento che contiene il  `*<someValue*`>  `user-data` impostato tramite l&#39; [ `ObservationManager` API] (https://www.adobe.io/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/observation/ObservationManager.html#setUserData(java.lang.String).

      Esempio:

      `jcr:lastModified,dc:modified,dc:format,jcr:lastModifiedBy,imageMap,event-user-data:changedByWorkflowProcess`

      Questa funzione può essere utilizzata per ignorare eventuali modifiche attivate da un altro processo di flusso di lavoro aggiungendo l’elemento di esclusione:

      `event-user-data:changedByWorkflowProcess`





1. Seleziona **Crea** per creare il modulo di avvio e tornare alla console.

   Quando si verifica l’evento appropriato, viene attivato il modulo di avvio e viene avviato il flusso di lavoro.

## Gestione di una configurazione del modulo di avvio {#managing-a-launcher-configuration}

Dopo aver creato la configurazione del modulo di avvio, puoi utilizzare la stessa console per selezionare l’istanza, quindi **Visualizza proprietà** (e modificarle) o **Elimina**.
