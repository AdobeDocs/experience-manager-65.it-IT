---
title: Progetti
description: I progetti consentono di raggruppare le risorse in un’unica entità il cui ambiente comune e condiviso semplifica la gestione dei progetti.
exl-id: 632c0608-2ab8-4a5b-8251-cd747535449b
source-git-commit: 9d497413d0ca72f22712581cf7eda1413eb8d643
workflow-type: tm+mt
source-wordcount: '1360'
ht-degree: 26%

---


# Progetti {#projects}

La funzione Progetti consente di raggruppare le risorse in una singola entità. Si ottiene così un ambiente comune e condiviso che semplifica la gestione dei progetti. I tipi di risorse che puoi associare a un progetto in AEM vengono definiti porzioni. I riquadri possono includere informazioni sul progetto e sul team, risorse, flussi di lavoro e altro, come descritto in dettaglio in [Riquadri di progetto.](#project-tiles)

In qualità di utente, puoi:

* Creare ed eliminare progetti
* Associare contenuto e cartelle di risorse a un progetto
* Rimuovere i collegamenti contenuto dal progetto

## Requisiti di accesso {#access-requirements}

Progetta una funzione AEM standard e non richiede alcuna configurazione aggiuntiva.

Tuttavia, affinché gli utenti dei progetti possano vedere altri utenti/gruppi mentre utilizzano i progetti, ad esempio durante la creazione di progetti, la creazione di attività/flussi di lavoro o la visualizzazione e la gestione del team, è necessario che tali utenti abbiano accesso in lettura a `/home/users` e `/home/groups`.

Il modo più semplice per eseguire questa operazione è quello di **projects-users** accesso in lettura gruppo a `/home/users` e `/home/groups`.

## Console Progetti {#projects-console}

Dalla console Progetti è possibile accedere e gestire i tuoi progetti in AEM.

![Console Progetti](assets/screen-shot_2019-03-05at125110.png)

La console Progetti è simile ad altre console dell’AEM e consente di eseguire diverse azioni sui singoli progetti e di regolare la tua visione dei progetti.

### Attiva/disattiva modalità {#modes}

Puoi utilizzare il selettore della barra per passare da una modalità all’altra della console.

![Selettore della barra](assets/projects-rail.png)

#### Solo contenuto {#content-only}

Solo contenuto è la modalità predefinita all’apertura della console. Mostrerà tutti i tuoi progetti.

#### Timeline {#timeline}

La vista timeline consente di selezionare un singolo progetto e di visualizzarne le attività. Utilizza il selettore della barra o il tasto di scelta rapida `alt+1` per passare a questa visualizzazione.

![Modalità Timeline](assets/project-timeline.png)

### Attiva/Disattiva visualizzazione {#views}

È possibile utilizzare il selettore di visualizzazione per passare dalla visualizzazione dei progetti come riquadri di grandi dimensioni (impostazione predefinita) alla visualizzazione come elenco e viceversa.

![Viste](assets/projects-views.png)

### Filtra la vista {#filter}

Puoi utilizzare il filtro per alternare tra tutti i progetti e solo quelli attivi.

![Filtro](assets/projects-filter.png)

### Selezione e visualizzazione dei progetti {#selecting}

Per selezionare un progetto, passa il mouse sulla sezione del progetto e fai clic sul segno di spunta.

Visualizzare i dettagli di un progetto facendo clic su di esso per analizzarne i dettagli.

### Creazione di nuovi progetti {#creating}

Clic **Crea** per aggiungere un nuovo progetto.

## Riquadri progetto {#project-tiles}

I progetti sono costituiti da diversi tipi di informazioni che si desidera gestire insieme. Queste informazioni sono rappresentate da diversi **Riquadri**.

Al progetto possono essere associate le seguenti tessere.

* [Risorse](#assets)
* [Raccolte di risorse](#asset-collections)
* [Esperienze](#experiences)
* [Collegamenti](#links)
* [Informazioni sul progetto](#project-info)
* [Team](#team)
* [Pagine di destinazione](#landing-pages)
* [E-mail](#emails)
* [Flussi di lavoro](#workflows)
* [Lanci](#launches)
* [Attività](#tasks)

Fai clic sul menu a discesa in alto a destra di qualsiasi sezione per aggiungere altri dati alla sezione.

Fai clic sul pulsante con i puntini di sospensione in basso a destra di qualsiasi sezione per aprire i dati della sezione nella console associata.

### Assets {#assets}

Nel riquadro **Risorse**, puoi raccogliere tutte le risorse utilizzate per un particolare progetto.

![Riquadro risorse](assets/project-tile-assets.png)

Le risorse vengono caricate direttamente nel riquadro.

### Raccolte di risorse {#asset-collections}

Come per le risorse, puoi aggiungere [raccolte di risorse](/help/assets/manage-collections.md) direttamente al progetto. Puoi definire le raccolte in Risorse.

![Riquadro raccolta risorse](assets/project-tile-asset-collection.png)

Per aggiungere una raccolta, fai clic su **Aggiungi raccolta** e seleziona la raccolta appropriata dall’elenco.

### Esperienze {#experiences}

Il **Esperienze** sezione consente di aggiungere al progetto un’app mobile, un sito web o una pubblicazione.

![Riquadro Esperienze](assets/project-tile-experiences.png)

Le icone indicano quale tipo di esperienza è rappresentata.

* Sito Web
* Applicazione mobile

### Collegamenti {#links}

Il **Collegamenti** sezione consente di associare collegamenti esterni al progetto.

![Riquadro Collegamenti](assets/project-tile-links.png)

Puoi denominare il collegamento con un nome facile da riconoscere e modificare la miniatura.

### Informazioni sul progetto {#project-info}

Il **Informazioni progetto** sezione fornisce informazioni generali sul progetto, tra cui una descrizione, lo stato del progetto (inattivo o attivo), una data di scadenza e i membri. Inoltre, è possibile aggiungere una miniatura del progetto, che viene visualizzata nella pagina principale Progetti.

![Riquadro informazioni progetto](assets/project-tile-info.png)

### Processo di traduzione {#translation-job}

Il **Lavoro di traduzione** sezione è il punto in cui si avvia una traduzione e anche il punto in cui viene visualizzato lo stato delle traduzioni.

![Riquadro del processo di traduzione](assets/project-tile-translation.png)

Per impostare la traduzione, consulta il documento [Creazione di progetti di traduzione.](/help/assets/translation-projects.md)

### Team {#team}

In questo riquadro è possibile specificare i membri del team del progetto. Durante la modifica, è possibile immettere il nome del membro del team e assegnare il ruolo utente.

![Riquadro team](assets/project-tile-team.png)

Puoi aggiungere ed eliminare membri dal team. Inoltre, puoi modificare il [ruolo utente](#userroles) assegnato al membro del team.

### Pagine di destinazione {#landing-pages}

Il **Pagine di destinazione** riquadro consente di richiedere una nuova pagina di destinazione.

![Riquadro della pagina di destinazione](assets/project-tile-landing.png)

Questo flusso di lavoro è descritto nel documento[Creare un flusso di lavoro per la pagina di destinazione.](/help/sites-authoring/projects-with-workflows.md#request-landing-page-workflow)

### E-mail {#emails}

Il **E-mail** Questo riquadro consente di gestire le richieste di e-mail. Avvia il **Richiesta e-mail** flusso di lavoro.

![Riquadro e-mail](assets/project-tile-email.png)

Ulteriori informazioni sono descritte nella [Richiedi flusso di lavoro e-mail.](/help/sites-authoring/projects-with-workflows.md#request-email-workflow)

### Flussi di lavoro {#workflows}

Puoi avviare i flussi di lavoro per il progetto. Se sono in esecuzione flussi di lavoro, il loro stato viene visualizzato nel **Flussi di lavoro** affiancare.

![Riquadro Flussi di lavoro](assets/project-tile-workflows.png)

A seconda del progetto creato, sono disponibili diversi flussi di lavoro.

Questi sono descritti in [Utilizzo dei flussi di lavoro per i progetti.](/help/sites-authoring/projects-with-workflows.md)

### Lanci {#launches}

Il **Lanci** mostra tutti i lanci richiesti con un [Richiedi flusso di lavoro di Launch.](/help/sites-authoring/projects-with-workflows.md)

![Riquadro Lanci](assets/project-tile-launches.png)

### Attività {#tasks}

Le attività consentono di monitorare lo stato di tutte le attività correlate al progetto, inclusi i flussi di lavoro. Le attività sono trattate in dettaglio in [Lavorare con le attività](/help/sites-authoring/task-content.md).

![Riquadro Attività](assets/project-tile-tasks.png)

## Modelli di progetto {#project-templates}

I modelli fungono da base per avviare il progetto. L’AEM fornisce questi modelli di progetto standard.

* **Progetto multimediale** - Questo è un progetto di riferimento per le attività relative ai media. Include diversi ruoli di progetto relativi ai file multimediali e flussi di lavoro relativi ai contenuti multimediali.
* **[Progetto servizio fotografico per prodotto](/help/sites-authoring/managing-product-information.md)** - Questo è un esempio di riferimento per la gestione della fotografia di prodotti relativa a eCommerce.
* **[Progetto di traduzione](/help/sites-administering/translation.md)** - Questo è un esempio di riferimento per la gestione delle attività di traduzione. Include ruoli di base e flussi di lavoro per la gestione della traduzione.
* **Progetto semplice** - Questo è un esempio di riferimento per tutti i progetti che non rientrano in altre categorie. Include tre ruoli di base e quattro flussi di lavoro generali per l’AEM.

In base al modello selezionato, all’interno del progetto sono disponibili diverse opzioni, ad esempio i ruoli utente e i flussi di lavoro forniti.

## Ruoli utente in un progetto {#user-roles-in-a-project}

I diversi ruoli utente sono definiti nel modello di progetto e vengono utilizzati per due motivi principali:

1. Autorizzazioni: i ruoli utente rientrano in una delle tre categorie elencate: osservatore, editor, proprietario. Ad esempio, un fotografo o un copywriter avrà gli stessi privilegi di un editor. Le autorizzazioni determinano cosa può fare un utente in relazione al contenuto di un progetto.
1. Flussi di lavoro: i flussi di lavoro determinano chi sono le attività assegnate in un progetto. Le attività possono essere associate a un ruolo del progetto. Ad esempio, è possibile assegnare un&#39;attività ai fotografi in modo che tutti i membri del gruppo che hanno il ruolo di fotografo ottengano l&#39;attività.

Tutti i progetti supportano i seguenti ruoli predefiniti per consentire l’amministrazione delle autorizzazioni di sicurezza e controllo.

| Ruolo | Descrizione | Autorizzazioni | Iscrizione al gruppo |
|---|---|---|---|
| Osservatore | Un utente con questo ruolo può visualizzare i dettagli del progetto, compreso lo stato. | Autorizzazioni di sola lettura per un progetto | `workflow-users` gruppo |
| Editor | Un utente con questo ruolo può caricare e modificare il contenuto di un progetto. | Accesso in lettura e scrittura a un progetto, ai metadati associati e alle risorse correlate<br>Privilegi per caricare un elenco di foto, servizi fotografici, rivedere e approvare le risorse<br>Autorizzazioni di scrittura su `/etc/commerce`<br>Autorizzazioni di modifica per un progetto specifico | `workflow-users` gruppo |
| Proprietario | Un utente con questo ruolo può creare un progetto, avviare il lavoro in un progetto e spostare le risorse approvate nella cartella di produzione. Il proprietario può visualizzare ed eseguire anche tutte le altre attività del progetto. | Autorizzazioni di scrittura su `/etc/commerce` | `dam-users` per poter creare un progetto<br>`projects-administrators` per creare un progetto e spostare le risorse |

Per i progetti creativi, vengono forniti anche ruoli aggiuntivi come fotografi. Puoi utilizzare questi ruoli per derivare ruoli personalizzati per un progetto specifico.

### Creazione automatica gruppo {#auto-group-creation}

Quando crei il progetto e aggiungi utenti ai vari ruoli, i gruppi associati al progetto vengono creati automaticamente per gestire le autorizzazioni associate.

Ad esempio, un progetto denominato Mioprogetto avrebbe tre gruppi **Proprietari mioprogetto**, **Editor Mioprogetto**, **Osservatori mioprogetto**.

Se il progetto viene eliminato, tali gruppi vengono eliminati solo se si seleziona l&#39;opzione appropriata [durante l’eliminazione del progetto.](/help/sites-authoring/touch-ui-managing-projects.md#deleting-a-project) Un amministratore può anche eliminare manualmente i gruppi in **Strumenti** > **Sicurezza** > **Gruppi**.

## Risorse aggiuntive {#additional-resources}

Per ulteriori dettagli sull’utilizzo dei progetti, consulta i seguenti documenti aggiuntivi:

* [Gestione dei progetti](/help/sites-authoring/touch-ui-managing-projects.md)
* [Utilizzo delle attività](/help/sites-authoring/task-content.md)
* [Utilizzo dei flussi di lavoro per i progetti](/help/sites-authoring/projects-with-workflows.md)
* [Progetto creativo e integrazione PIM](/help/sites-authoring/managing-product-information.md)
