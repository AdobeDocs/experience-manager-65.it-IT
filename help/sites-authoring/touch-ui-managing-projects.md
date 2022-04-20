---
title: Gestione dei progetti
seo-title: Managing Projects
description: Progetti consente di organizzare il progetto raggruppando le risorse in un’unica entità accessibile e gestibile nella console Progetti
seo-description: Projects lets you organize your project by grouping resources into one entity which can be acessed and managed intheProjects console
uuid: ac937582-181f-429b-9404-3c71d1241495
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: projects
content-type: reference
discoiquuid: fb354c72-debb-4fb6-9ccf-56ff5785c3ae
exl-id: 62586c8e-dab4-4be9-a44a-2c072effe3c0
source-git-commit: 200b47070b7ead54ee54eea504bd960d4e0731d9
workflow-type: tm+mt
source-wordcount: '987'
ht-degree: 20%

---


# Gestione dei progetti {#managing-projects}

In **Progetti** Puoi accedere ai tuoi progetti e gestirli.

![Console Progetti](assets/projects-console.png)

Puoi creare un progetto, associare le risorse al progetto ed eliminare un progetto o collegamenti alle risorse mediante la console.

## Requisiti di accesso {#access-requirements}

Progetta una funzione di AEM standard e non richiede alcuna configurazione aggiuntiva.

Tuttavia, affinché gli utenti dei progetti possano vedere altri utenti/gruppi utilizzando Progetti quali la creazione di progetti, la creazione di attività/flussi di lavoro o la visualizzazione e la gestione del team, questi utenti devono avere accesso in lettura a `/home/users` e `/home/groups`.

Il modo più semplice per farlo è quello di dare **utenti dei progetti** accesso in lettura di gruppo a `/home/users` e `/home/groups`.

## Creazione di un progetto {#creating-a-project}

Per creare un nuovo progetto, effettua le seguenti operazioni.

1. In **Progetti** console, tocca o fai clic **Crea** per aprire **Crea progetto** procedura guidata.
1. Seleziona un modello e fai clic su **Successivo**. Ulteriori informazioni sui modelli di progetto standard [qui.](/help/sites-authoring/projects.md#project-templates)

   ![Creazione guidata progetto](assets/create-project-wizard.png)

1. Definisci la **Titolo** e **Descrizione** e aggiungi un **Miniatura** se necessario. Puoi anche aggiungere o eliminare gli utenti e il gruppo a cui appartengono,

   ![Passaggio delle proprietà della procedura guidata](assets/create-project-wizard-properties.png)

1. Tocca o fai clic su **Crea**. Ti viene richiesto se desideri aprire il nuovo progetto o tornare alla console.

La procedura per la creazione di un progetto è la stessa per tutti i modelli di progetto. La differenza tra i tipi di progetti si riferisce alle risorse disponibili [ruoli utente](/help/sites-authoring/projects.md) e [flussi di lavoro.](/help/sites-authoring/projects-with-workflows.md)

### Associazione delle risorse al progetto {#associating-resources-with-your-project}

I progetti consentono di raggruppare le risorse in un’unica entità per gestirle nel loro insieme. Pertanto devi associare le risorse al progetto. Queste risorse sono raggruppate all’interno del progetto come **Porzioni**. I tipi di risorse che è possibile aggiungere sono descritti nella sezione [Porzioni di progetto](/help/sites-authoring/projects.md#project-tiles).

Per associare risorse a un progetto:

1. Apri il progetto dalla console **Progetti**.
1. Tocca o fai clic su **Aggiungi sezione**, quindi seleziona la porzione che desideri collegare al progetto. È possibile selezionare tra più tipi di porzioni.

   ![Aggiungi riquadro](assets/project-add-tile.png)

1. Tocca o fai clic su **Crea**. La risorsa è ora collegata al progetto e accessibile da questo.

### Aggiungere elementi a una porzione {#adding-items-to-a-tile}

Per alcune porzioni è possibile aggiungere più di un oggetto. Ad esempio, è possibile avere più flussi di lavoro o esperienze in esecuzione allo stesso tempo.

Per aggiungere elementi a una tessera:

1. In **Progetti**, individua il progetto e fai clic sull’icona freccia rivolta verso il basso in alto a destra della porzione a cui desideri aggiungere un elemento e seleziona l’opzione appropriata.

   * L’opzione dipende dal tipo di riquadro. Ad esempio **Crea attività** per **Attività** piastrelle o **Avvia flusso di lavoro** per **Flussi di lavoro** piastrelle.

   ![Chevron](assets/project-tile-create-task.png)

1. Aggiungi l’elemento alla tessera come faresti quando crei una nuova tessera. Sono descritte le porzioni di progetto [qui.](/help/sites-authoring/projects.md#project-tiles)

## Visualizzazione delle informazioni sul progetto {#viewing-project-info}

Lo scopo principale dei progetti è quello di raggruppare le informazioni associate in un unico luogo per renderle più accessibili e fruibili. Sono disponibili diversi modi per accedere a queste informazioni.

### Aprire una porzione {#opening-a-tile}

È possibile visualizzare gli elementi inclusi nella porzione selezionata, modificarli o eliminarli.

Per aprire una porzione e visualizzare o modificare gli elementi:

1. Tocca o fai clic sull’icona dei puntini di sospensione in basso a destra della tessera.

   ![Riquadro attività](assets/project-tile-tasks.png)

1. AEM apre la console per i tipi di elementi associati alla tessera e per i filtri in base al progetto selezionato.

   ![Attività del progetto](assets/project-tasks.png)

### Visualizzazione della cronologia di un progetto {#viewing-a-project-timeline}

La cronologia di un progetto fornisce informazioni sull’ultimo utilizzo delle risorse associate. Per visualizzare la timeline del progetto, effettua le seguenti operazioni.

1. In **Progetti** console, fai clic o tocca **Timeline** nel selettore della barra in alto a sinistra nella console.
   ![Selezione della modalità timeline](assets/projects-timeline-rail.png)
2. Nella console selezionate il progetto per il quale desiderate visualizzare la timeline.
   ![Vista timeline del progetto](assets/project-timeline-view.png)

Le risorse vengono visualizzate nella barra laterale. Al termine, utilizza il selettore della barra per tornare alla visualizzazione normale.

### Visualizzazione di progetti inattivi {#viewing-active-inactive-projects}

Per alternare tra le opzioni attive e [progetti inattivi,](#making-projects-inactive-or-active) in **Progetti** nella console, fai clic su **Attiva/Disattiva progetti** nella barra degli strumenti.

![Icona Attiva/Disattiva progetti](assets/projects-toggle-active.png)

Per impostazione predefinita, la console mostra i progetti attivi. Fai clic sul pulsante **Attiva/Disattiva progetti** per passare alla visualizzazione di progetti inattivi. Fai di nuovo clic su di esso per tornare ai progetti attivi.

## Organizzazione dei progetti {#organizing-projects}

Sono disponibili diverse opzioni per organizzare i progetti in modo da mantenere **Progetti** da console gestibile.

### Cartelle di progetto {#project-folders}

È possibile creare cartelle in **Progetti** per raggruppare e organizzare progetti simili.

1. In **Progetti** tocca o fai clic sulla console **Crea** e poi **Crea cartella**.

   ![Crea cartella](assets/project-create-folder.png)

1. Assegna un titolo alla cartella e fai clic su **Crea**.

1. La cartella viene aggiunta alla console.

Ora puoi creare progetti all’interno della cartella . È possibile creare più cartelle e nidificare anche le cartelle.

### Attivazione di progetti {#making-projects-inactive-or-active}

È possibile contrassegnare un progetto come inattivo se è stato completato ma si desidera comunque mantenere le informazioni relative al progetto. [I progetti inattivi ora vengono visualizzati](#viewing-active-inactive-projects) per impostazione predefinita in **Progetti** console.

Per rendere un progetto inattivo, effettua le seguenti operazioni.

1. Apri **Proprietà progetto** finestra del progetto.
   * Per eseguire questa operazione dalla console, seleziona il progetto o dall’interno del progetto tramite la **Informazioni progetto** piastrelle.
1. In **Proprietà progetto** finestra, modificare **Stato del progetto** cursore da **Attivo** a **Inattivo**.

   ![Selettore dello stato del progetto nella finestra delle proprietà](assets/project-status.png)

1. Tocca o fai clic su **Salva e chiudi** per salvare le modifiche.

### Eliminazione di progetti {#deleting-a-project}

Per eliminare un progetto, effettua le seguenti operazioni.

1. Passa al livello superiore della **Progetti** console.
1. Seleziona il progetto nella console.
1. Tocca o fai clic su **Elimina** nella barra degli strumenti.
1. AEM rimuovere o modificare i dati di progetto associati al momento dell’eliminazione del progetto. Seleziona le opzioni necessarie nel **Elimina progetto** finestra di dialogo.
   * Rimuovi gruppi e ruoli del progetto
   * Elimina cartella risorse di progetto
   * Termina flussi di lavoro per progetto

   ![Opzioni di eliminazione del progetto](assets/project-delete-options.png)
1. Tocca o fai clic su **Elimina** per eliminare il progetto con le opzioni selezionate.

Per ulteriori informazioni sui gruppi creati automaticamente dai progetti, consulta [Creazione automatica dei gruppi](/help/sites-authoring/projects.md#auto-group-creation) per i dettagli.
