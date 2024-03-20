---
title: Avvio dei flussi di lavoro
description: Scopri come amministrare i flussi di lavoro in Adobe Experience Manager in modo da poterli avviare utilizzando vari metodi, manualmente o automaticamente.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
exl-id: 84a1964c-4121-4763-b946-9eee6093747d
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '790'
ht-degree: 2%

---

# Avvio dei flussi di lavoro{#starting-workflows}

Durante l’amministrazione dei flussi di lavoro puoi avviarli utilizzando vari metodi:

* Manualmente:

   * Da un [Modello flusso di lavoro](#workflow-models).
   * Utilizzo di un pacchetto di flusso di lavoro per [elaborazione batch](#workflow-packages-for-batch-processing).

* Automaticamente:

   * In risposta alle modifiche apportate ai nodi; [utilizzo di un modulo di avvio](#workflows-launchers).

>[!NOTE]
>
>Altri metodi sono disponibili anche per gli autori; per informazioni complete vedi:
>
>* [Applicazione dei flussi di lavoro alle pagine](/help/sites-authoring/workflows-applying.md)
>* [Applicare i flussi di lavoro alle risorse DAM](/help/assets/assets-workflow.md)
>* [AEM Forms](https://helpx.adobe.com/aem-forms/6-2/aem-workflows-submit-process-form.html)
>* [Progetti di traduzione](/help/sites-administering/tc-manage.md)
>

## Modelli flusso di lavoro {#workflow-models}

Puoi avviare un flusso di lavoro [basato su uno dei modelli](/help/sites-administering/workflows.md#workflow-models-and-instances) elencati nella console Modelli di flusso di lavoro. Le uniche informazioni obbligatorie sono il payload, anche se è possibile aggiungere un titolo e/o un commento.

## Moduli di avvio dei flussi di lavoro {#workflows-launchers}

Il modulo di avvio dei flussi di lavoro monitora le modifiche nell’archivio dei contenuti per avviare i flussi di lavoro in base alla posizione e al tipo di risorsa del nodo modificato.

Utilizzo di **Modulo di avvio** è possibile:

* Consulta i flussi di lavoro già avviati per nodi specifici.
* Seleziona un flusso di lavoro da avviare quando un determinato tipo di nodo/nodo è stato creato/modificato/rimosso.
* Rimuovi una relazione esistente tra flusso di lavoro e nodo.

È possibile creare un modulo di avvio per qualsiasi nodo. Tuttavia, le modifiche apportate ad alcuni nodi non avviano i flussi di lavoro. Le modifiche apportate ai nodi al di sotto dei percorsi seguenti non determinano l’avvio dei flussi di lavoro:

* `/var/workflow/instances`
* Qualsiasi nodo della casella in entrata del flusso di lavoro che si trova in un punto qualsiasi della `/home/users` filiale
* `/tmp`
* `/var/audit`
* `/var/classes`
* `/var/eventing`
* `/var/linkchecker`
* `/var/mobile`
* `/var/statistics`

   * Eccezione: modifiche ai nodi sottostanti `/var/statistics/tracking` *fare* avvia i flussi di lavoro.

Varie definizioni sono incluse nell&#39;installazione standard. Questi vengono utilizzati per attività di gestione delle risorse digitali e collaborazione social:

![wf-100](assets/wf-100.png)

## Pacchetti flusso di lavoro per elaborazione batch {#workflow-packages-for-batch-processing}

I pacchetti del flusso di lavoro sono pacchetti che possono essere passati a un flusso di lavoro come payload per l’elaborazione, consentendo l’elaborazione di più risorse.

Un pacchetto di flusso di lavoro:

* contiene collegamenti a un set di risorse (ad esempio pagine, risorse).
* contiene informazioni sul pacchetto, ad esempio la data di creazione, l&#39;utente che lo ha creato e una breve descrizione.
* viene definito utilizzando un modello di pagina specializzato; tali pagine consentono all’utente di specificare le risorse nel pacchetto.
* può essere utilizzato più volte.
* possono essere modificate dall’utente (aggiungi o rimuovi risorse) mentre l’istanza di flusso di lavoro è effettivamente in esecuzione.

## Avvio di un flusso di lavoro dalla console Modelli {#starting-a-workflow-from-the-models-console}

1. Accedi a **Modelli** console utilizzando **Strumenti**, **Flusso di lavoro**, quindi **Modelli**.
1. Seleziona il flusso di lavoro (in base alla vista della console); se necessario, puoi anche utilizzare la funzione di ricerca (in alto a sinistra):

   ![wf-103](assets/wf-103.png)

   >[!NOTE]
   >
   >Il **[Transitorio](/help/sites-developing/workflows.md#transient-workflows)** Questo indicatore mostra i flussi di lavoro per i quali la cronologia del flusso di lavoro non viene mantenuta.

1. Seleziona **Avvia flusso di lavoro** dalla barra degli strumenti.
1. Viene visualizzata la finestra di dialogo Esegui flusso di lavoro, che consente di specificare:

   * **Payload**

     Può trattarsi di una pagina, un nodo, una risorsa, un pacchetto, ecc.

   * **Titolo**

     Titolo facoltativo per identificare questa istanza.

   * **Commento**

     Un commento facoltativo per indicare i dettagli di questa istanza.

   ![wf-104](assets/wf-104.png)

## Creazione di una configurazione del modulo di avvio {#creating-a-launcher-configuration}

1. Accedi a **Moduli di avvio dei flussi di lavoro** console utilizzando **Strumenti**, **Flusso di lavoro**, quindi **Moduli di avvio**.
1. Seleziona **Crea**, quindi **Aggiungi modulo di avvio** per aprire la finestra di dialogo:

   ![wf-105](assets/wf-105.png)

   * **Tipo di evento**

     Tipo di evento che avvia il flusso di lavoro:

      * Creato
      * Modificato
      * Rimosso

   * **Nodetype**

     Tipo di nodo a cui si applica il modulo di avvio del flusso di lavoro.

   * **Percorso**

     Percorso a cui si applica il modulo di avvio dei flussi di lavoro.

   * **Modalità di esecuzione**

     Tipo di server a cui si applica il modulo di avvio del flusso di lavoro. Seleziona **Autore**, **Pubblica**, o **Creazione e pubblicazione**.

   * **Condizioni**

     Un elenco di condizioni per i valori dei nodi che, una volta valutati, determinano se il flusso di lavoro viene avviato. Ad esempio, la seguente condizione causa l’avvio del flusso di lavoro quando il nodo ha un nome di proprietà con il valore Utente:

     name==User

   * **Funzioni**

     Elenco di funzionalità da attivare. Seleziona le funzioni richieste utilizzando il selettore a discesa.

   * **Funzioni disattivate**

   Elenco di funzionalità da disattivare. Seleziona le funzioni richieste utilizzando il selettore a discesa.

   * **Modello flusso di lavoro**

     Il flusso di lavoro da avviare quando il Tipo di evento si verifica sul Tipo di nodo e/o Percorso nella Condizione definita.

   * **Descrizione**

     Testo personalizzato per descrivere e identificare la configurazione del modulo di avvio.

   * **Attiva**

     Controlla se il modulo di avvio del flusso di lavoro è attivato:

      * Seleziona **Abilita** per avviare i flussi di lavoro quando le proprietà di configurazione sono soddisfatte.
      * Seleziona **Disattiva** quando il flusso di lavoro non deve essere eseguito (nemmeno quando le proprietà di configurazione sono soddisfatte).

   * **Escludi elenco**

     Questo specifica eventuali eventi JCR da escludere (ovvero da ignorare) quando si determina se un flusso di lavoro deve essere attivato.

     Questa proprietà di avvio è un elenco di elementi separato da virgole: &quot;

      * `property-name` ignora qualsiasi `jcr` evento che si è attivato sul nome della proprietà specificato. &quot;
      * `event-user-data:<*someValue*>` ignora qualsiasi evento che contiene `*<someValue*`> `user-data` impostato tramite [`ObservationManager` API](https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/observation/ObservationManager.html#setUserData(java.lang.String).

     Ad esempio:

     `jcr:lastModified,dc:modified,dc:format,jcr:lastModifiedBy,imageMap,event-user-data:changedByWorkflowProcess`

     Questa funzione può essere utilizzata per ignorare eventuali modifiche attivate da un altro processo di flusso di lavoro aggiungendo l’elemento da escludere:

     `event-user-data:changedByWorkflowProcess`

1. Seleziona **Crea**, per creare il modulo di avvio e tornare alla console.

   Quando si verifica l’evento appropriato, viene attivato il modulo di avvio e avviato il flusso di lavoro.

## Gestione di una configurazione del modulo di avvio {#managing-a-launcher-configuration}

Dopo aver creato la configurazione di avvio, puoi utilizzare la stessa console per selezionare l’istanza, quindi **Visualizza proprietà** (e modificarli) oppure **Elimina**.
