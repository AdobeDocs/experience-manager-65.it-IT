---
title: Progetti
seo-title: Projects
description: I progetti consentono di raggruppare le risorse in un'entità con un ambiente comune e condiviso, semplificando la gestione dei progetti.
seo-description: Projects let you group resources into one entity whose common, shared environment makes it easy to manage your projects
uuid: 4b5b9d78-d515-46af-abe2-882da0a1c8ae
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: projects
content-type: reference
discoiquuid: dee7ac7c-ca86-48e9-8d95-7826fa926c68
docset: aem65
exl-id: 632c0608-2ab8-4a5b-8251-cd747535449b
source-git-commit: 85e993000c016240c0fbf398ec8192990e60eee6
workflow-type: tm+mt
source-wordcount: '1366'
ht-degree: 37%

---


# Progetti {#projects}

La funzione Progetti consente di raggruppare le risorse in una singola entità. Si ottiene così un ambiente comune e condiviso che semplifica la gestione dei progetti. I tipi di risorse che puoi associare a un progetto in AEM vengono definiti porzioni. I riquadri possono includere informazioni sul progetto e sul team, risorse, flussi di lavoro e altro, come descritto in dettaglio in [Riquadri di progetto.](#project-tiles)

In qualità di utente, puoi:

* Creare ed eliminare progetti
* Assegnare contenuti e cartelle di attività a un progetto
* Rimuovere i collegamenti a contenuti dal progetto

## Requisiti di accesso {#access-requirements}

Progetta una funzione di AEM standard e non richiede alcuna configurazione aggiuntiva.

Tuttavia, affinché gli utenti dei progetti possano vedere altri utenti/gruppi utilizzando Progetti quali la creazione di progetti, la creazione di attività/flussi di lavoro o la visualizzazione e la gestione del team, questi utenti devono avere accesso in lettura a `/home/users` e `/home/groups`.

Il modo più semplice per farlo è quello di dare **utenti dei progetti** accesso in lettura di gruppo a `/home/users` e `/home/groups`.

## Console Progetti {#projects-console}

Dalla console dei progetti è possibile accedere ai tuoi progetti e gestirli in AEM.

![Console Progetti](assets/screen-shot_2019-03-05at125110.png)

La console Progetti è simile alle altre console presenti in AEM, consente di eseguire varie azioni su singoli progetti e di modificare la visualizzazione dei progetti.

### Attiva/disattiva la modalità {#modes}

Puoi usare il selettore della barra per cambiare modalità console.

![Selettore della barra](assets/projects-rail.png)

#### Solo contenuto {#content-only}

Solo contenuto è la modalità predefinita all’apertura della console. Mostrerà tutti i tuoi progetti.

#### Timeline  {#timeline}

La visualizzazione timeline consente di selezionare un singolo progetto e visualizzarne l’attività. Utilizza il selettore della barra o il tasto di scelta rapida `alt+1` per passare a questa visualizzazione.

![Modalità Timeline](assets/project-timeline.png)

### Attiva/disattiva la visualizzazione {#views}

È possibile utilizzare il selettore di visualizzazione per passare dalla visualizzazione dei progetti come riquadri di grandi dimensioni (impostazione predefinita) alla visualizzazione come elenco o come calendario.

![Viste](assets/projects-views.png)

### Filtrare la visualizzazione {#filter}

Puoi utilizzare il filtro per alternare tra tutti i progetti e solo quelli attivi.

![Filtro](assets/projects-filter.png)

### Selezione e visualizzazione di progetti {#selecting}

Seleziona un progetto passando il mouse sulla porzione del progetto e facendo clic sul segno di spunta.

Per visualizzare i dettagli di un progetto, fai clic su di esso per approfondirne i dettagli.

### Creazione di nuovi progetti {#creating}

Fai clic su **Crea** per aggiungere un nuovo progetto.

## Porzioni del progetto {#project-tiles}

I progetti sono composti da diversi tipi di informazioni che desideri gestire insieme. Queste informazioni sono rappresentate da diverse **Porzioni**.

È possibile associare le seguenti porzioni al progetto.

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

Fai clic sul menu a discesa in alto a destra di qualsiasi riquadro per aggiungere più dati al riquadro.

Fai clic sul pulsante dei puntini di sospensione in basso a destra di qualsiasi riquadro per aprire i dati della tessera nella console associata.

### Assets {#assets}

Nella sezione **Risorse**, puoi raccogliere tutte le risorse usate per un particolare progetto.

![Riquadro risorse](assets/project-tile-assets.png)

Puoi caricare le risorse direttamente nella porzione.

### Raccolte di risorse {#asset-collections}

Come per le risorse, puoi aggiungere [raccolte di risorse](/help/assets/manage-collections.md) direttamente al tuo progetto. Puoi definire le raccolte in Risorse.

![Riquadro di raccolta risorse](assets/project-tile-asset-collection.png)

Per aggiungere una raccolta, fai clic su **Aggiungi raccolta** e seleziona la raccolta appropriata dall’elenco.

### Esperienze {#experiences}

La **Esperienze** consente di aggiungere al progetto un’app mobile, un sito web o una pubblicazione.

![Riquadro esperienze](assets/project-tile-experiences.png)

Le icone indicano quale tipo di esperienza è rappresentata.

* Sito Web
* App mobile

### Collegamenti {#links}

La **Collegamenti** consente di associare collegamenti esterni al progetto.

![Riquadro collegamenti](assets/project-tile-links.png)

Puoi denominare il collegamento con un nome facile da riconoscere, nonché modificare la miniatura.

### Informazioni progetto {#project-info}

La **Informazioni sul progetto** La sezione fornisce informazioni generali sul progetto, tra cui una descrizione, lo stato del progetto (inattivo o attivo), una data di scadenza e i membri. Inoltre, puoi aggiungere una miniatura del progetto, che viene visualizzata nella pagina principale Progetti.

![Riquadro informazioni progetto](assets/project-tile-info.png)

### Processo di traduzione {#translation-job}

La **Processo di traduzione** riquadro è dove si inizia una traduzione e anche dove si vede lo stato delle traduzioni.

![Riquadro del processo di traduzione](assets/project-tile-translation.png)

Per impostare la traduzione, vedere il documento [Creazione di progetti di traduzione.](/help/assets/translation-projects.md)

### Team {#team}

In questa porzione, è possibile specificare i membri del team del progetto. Durante la modifica, è possibile immettere il nome del membro del team e assegnare un ruolo all’utente.

![Riquadro team](assets/project-tile-team.png)

Puoi aggiungere ed eliminare membri dal team. Inoltre, puoi modificare il [ruolo utente](#userroles) assegnato al membro del team.

### Pagine di destinazione {#landing-pages}

La porzione **** Pagine di destinazione consente di richiedere una nuova pagina di destinazione.

![Riquadro pagina di destinazione](assets/project-tile-landing.png)

Questo flusso di lavoro è descritto nel documento[Crea un flusso di lavoro Pagina di destinazione.](/help/sites-authoring/projects-with-workflows.md#request-landing-page-workflow)

### E-mail {#emails}

La porzione **E-mail** consente di gestire le richieste per e-mail. Inizia la **Richiesta e-mail** workflow.

![Riquadro e-mail](assets/project-tile-email.png)

Per ulteriori informazioni, consulta [Flusso di lavoro richiedi e-mail](/help/sites-authoring/projects-with-workflows.md#request-email-workflow)

### Flussi di lavoro {#workflows}

Puoi avviare i flussi di lavoro per il progetto. Se sono in esecuzione flussi di lavoro, il loro stato viene visualizzato nella sezione **Flussi di lavoro** piastrelle.

![Riquadro dei flussi di lavoro](assets/project-tile-workflows.png)

A seconda del progetto creato sono disponibili diversi flussi di lavoro.

I diversi flussi di lavoro sono descritti in [Utilizzo dei flussi di lavoro del progetto.](/help/sites-authoring/projects-with-workflows.md)

### Lanci {#launches}

La **Lanci** mostra tutti i lanci richiesti con un [Richiedi flusso di lavoro Launch.](/help/sites-authoring/projects-with-workflows.md)

![Lanci riquadro](assets/project-tile-launches.png)

### Attività {#tasks}

Le attività consentono di controllare lo stato di tutte le attività relative al progetto, tra cui i flussi di lavoro. Le attività sono trattate in dettaglio in [Lavorare con le attività](/help/sites-authoring/task-content.md).

![Riquadro attività](assets/project-tile-tasks.png)

## Modelli di progetto {#project-templates}

I modelli fungono da base per avviare il progetto. AEM fornisce questi modelli di progetto standard.

* **Progetto multimediale** - Questo è un progetto di esempio di riferimento per le attività relative ai contenuti multimediali. Include diversi ruoli di progetto relativi ai file multimediali e anche flussi di lavoro relativi ai contenuti multimediali.
* **[Progetto servizio fotografico per prodotto](/help/sites-authoring/managing-product-information.md)** - Questo è un esempio di riferimento per la gestione della fotografia di prodotti correlati all’e-commerce.
* **[Progetto di traduzione](/help/sites-administering/translation.md)** - Questo è un esempio di riferimento per la gestione delle attività relative alla traduzione. Include ruoli di base e flussi di lavoro per la gestione della traduzione.
* **Progetto semplice** - Questo è un esempio di riferimento per tutti i progetti che non rientrano in altre categorie. Include tre ruoli di base e quattro flussi di lavoro AEM generali.

In base al modello selezionato, all’interno del progetto sono disponibili diverse opzioni, ad esempio i ruoli utente e i flussi di lavoro forniti.

## Ruoli utente in un progetto {#user-roles-in-a-project}

I diversi ruoli utente vengono definiti nel modello di progetto e utilizzati per due motivi principali:

1. Autorizzazioni: I ruoli utente rientrano in una delle tre categorie elencate: osservatore, editor, proprietario. Ad esempio, un fotografo o un copywriter avrà gli stessi privilegi di un editor. Le autorizzazioni determinano le azioni di un utente in relazione ai contenuti di un progetto.
1. Flussi di lavoro: I flussi di lavoro determinano le attività assegnate a un progetto. Le attività possono essere associate a un ruolo del progetto. Ad esempio, è possibile assegnare un’attività ai fotografi in modo che tutti i membri del team che hanno il ruolo di fotografo ottengano l’attività.

Tutti i progetti supportano i seguenti ruoli predefiniti per consentire all’utente di amministrare le autorizzazioni di controllo e protezione.

| Ruolo | Descrizione | Autorizzazioni | Iscrizione al gruppo |
|---|---|---|---|
| Osservatore | Un utente con questo ruolo può visualizzare le informazioni di progetto, tra cui lo stato del progetto. | Autorizzazioni di sola lettura per un progetto | `workflow-users` gruppo |
| Editor | Un utente con questo ruolo può caricare e modificare il contenuto di un progetto. | Accesso in lettura e scrittura a un progetto, ai metadati associati e alle risorse correlate<br>Privilegi per caricare un elenco di foto, un servizio fotografico e per rivedere e approvare le risorse<br>Autorizzazioni di scrittura su `/etc/commerce`<br>Modificare le autorizzazioni per un progetto specifico | `workflow-users` gruppo |
| Proprietario | Un utente con questo ruolo può creare un progetto, avviare il lavoro in un progetto e spostare le risorse approvate nella cartella di produzione. Il proprietario può visualizzare ed eseguire tutte le altre attività del progetto. | Autorizzazioni di scrittura su `/etc/commerce` | `dam-users` per creare un progetto<br>`project-administrators` per creare un progetto e spostare le risorse |

Per i progetti creativi vengono forniti anche altri ruoli, come i fotografi. Puoi usare questi ruoli per creare ruoli personalizzati per un progetto specifico.

### Creazione automatica dei gruppi {#auto-group-creation}

Quando crei il progetto e aggiungi utenti ai vari ruoli, i gruppi associati al progetto vengono creati automaticamente per gestire le autorizzazioni associate.

Ad esempio, un progetto denominato Mioprogetto avrebbe tre gruppi: **Proprietari mioprogetto**, **Editor mioprogetto**, **Osservatori mioprogetto**.

Se il progetto viene eliminato, questi gruppi vengono eliminati solo se selezioni l’opzione appropriata [durante l’eliminazione del progetto.](/help/sites-authoring/touch-ui-managing-projects.md#deleting-a-project) Un amministratore può inoltre eliminare manualmente i gruppi in **Strumenti** > **Sicurezza** > **Gruppi**.

## Risorse aggiuntive {#additional-resources}

Per ulteriori dettagli sull’utilizzo dei progetti, consulta i seguenti documenti aggiuntivi:

* [Gestione dei progetti](/help/sites-authoring/touch-ui-managing-projects.md)
* [Utilizzo delle attività](/help/sites-authoring/task-content.md)
* [Utilizzo dei flussi di lavoro per i progetti](/help/sites-authoring/projects-with-workflows.md)
* [Integrazione Progetto creativo e PIM](/help/sites-authoring/managing-product-information.md)
