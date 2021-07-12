---
title: Funzioni per community
seo-title: Funzioni per community
description: Scopri come accedere alla console Funzioni della community
seo-description: Scopri come accedere alla console Funzioni della community
uuid: d3d70134-f318-4709-a673-b01a3467d980
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 91833914-b811-4355-a97d-e1a9cb7441f1
docset: aem65
role: Admin
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '2458'
ht-degree: 6%

---


# Funzioni per community{#community-functions}

Il tipo di funzionalità previsto da un’esperienza community è noto. Le funzioni della community sono disponibili come funzioni della community. In sostanza, si tratta di una o più pagine precablate per implementare una funzione community che richiede più che semplicemente l’aggiunta di un componente a una pagina in modalità di authoring. Si tratta dei blocchi costitutivi utilizzati per definire la struttura di un [modello di sito community](/help/communities/sites.md) da cui vengono [creati i siti community](/help/communities/sites-console.md).

Una volta creato un sito community, il contenuto può essere aggiunto alle pagine risultanti utilizzando la modalità di authoring standard [AEM](/help/sites-authoring/editing-content.md). Sono disponibili varie funzioni della community, come mostrato nella console delle funzioni della community.

>[!NOTE]
>
>Le console per la creazione di [siti della community](/help/communities/sites-console.md), [modelli di sito della community](/help/communities/sites.md), [modelli di gruppo della community](/help/communities/tools-groups.md) e [funzioni della community](/help/communities/functions.md) sono utilizzabili solo nell’ambiente di authoring.

## Console Funzioni community {#community-functions-console}

Per accedere alla console funzioni della community nell’ambiente di authoring:

* Passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Community]** > **[!UICONTROL Funzioni community]**.

![funzioni di comunità](assets/community-functions.png)

## Funzioni predefinite {#pre-built-functions}

Di seguito è riportata una breve descrizione delle funzioni fornite con AEM Communities. Ogni funzione include una o più pagine AEM contenenti i componenti Community collegati tra loro in una funzione facilmente incorporata in un [modello di sito community](/help/communities/sites.md).

Un modello di sito community fornisce la struttura di un sito community con login, profili utente, notifiche, messaggi, menu del sito, ricerca, temi e funzioni di branding.

### Impostazioni titolo e URL {#title-and-url-settings}

**** Titleand  **** URLsono proprietà comuni a tutte le funzioni della community.

Quando una funzione community viene aggiunta a un modello di sito community o quando [modifica](/help/communities/sites-console.md#modifying-site-properties) la struttura di un sito community, viene visualizzata la finestra di dialogo della funzione in modo che sia possibile configurare il Titolo e l’URL.

#### Dettagli funzione di configurazione {#configuration-function-details}

![title-url-details](assets/title-url-details.png)

* **Titolo**

   (*Richiesto*) Testo visualizzato nel menu delle funzioni del sito

* **URL**

   (*Obbligatorio*) Il nome utilizzato per generare l’URI. Il nome deve essere conforme alle [convenzioni di denominazione](/help/sites-developing/naming-conventions.md) imposte da AEM e JCR.

Ad esempio, utilizzando il sito creato seguendo l&#39;esercitazione [Guida introduttiva](/help/communities/getting-started.md), se

* Titolo = Pagina Web
* URL = page

Quindi, l&#39;URL della pagina è https://localhost:4503/content/sites/engage/en/page.html

e il collegamento del menu per la pagina viene visualizzato come:

![interpage](assets/engage-page.png)

### Funzione Flusso attività {#activity-stream-function}

La funzione flusso di attività è una pagina con un [componente Flussi di attività](/help/communities/activities.md) con tutte le visualizzazioni selezionate (tutte le attività, le attività dell&#39;utente e seguenti). Per gli sviluppatori, consulta anche [Activity Stream Essentials](/help/communities/essentials-activities.md) .

Quando viene aggiunto a un modello, si apre la seguente finestra di dialogo:

#### Dettagli funzione di configurazione {#configuration-function-details-1}

![dettagli della funzione](assets/function-details.png)

* [Impostazioni titolo e URL](#title-and-url-settings)

* **Mostra vista Le mie attività**

   Se selezionata, la pagina Attività include una scheda che filtra le attività in base a quelle generate all’interno della community dal membro corrente. Il valore predefinito è selezionato.

* **Mostra la vista Tutte le attività**

   Se selezionata, la pagina Attività include una scheda che include tutte le attività generate all’interno della community a cui il membro corrente ha accesso. Il valore predefinito è selezionato.

* **Mostra vista Feed notizie**

   Se selezionata, le pagine Attività includono una scheda che filtra le attività in base a quelle che il membro corrente sta seguendo. Il valore predefinito è selezionato.

### Funzione Assegnazioni {#assignments-function}

La funzione assegnazioni è la funzione di base che definisce un [sito community per l&#39;abilitazione](/help/communities/overview.md#enablement-community). Consente l&#39;assegnazione di risorse di abilitazione ai membri della community. Per gli sviluppatori, consulta anche [Assegnazioni Essentials](/help/communities/essentials-assignments.md) .

Questa funzione è disponibile come funzione del componente aggiuntivo [enablement](/help/communities/enablement.md). Il componente aggiuntivo per l’abilitazione richiede licenze aggiuntive per l’utilizzo in un ambiente di produzione.

Quando viene aggiunta a un modello, l’unica configurazione è per [Impostazioni titolo e URL](#title-and-url-settings).

### Funzione Blog {#blog-function}

La funzione blog è una pagina con un [componente Blog](/help/communities/blog-feature.md) configurato per l&#39;assegnazione di tag, il caricamento di file, il seguito, i membri per la modifica automatica, il voto e la moderazione. Per gli sviluppatori, consulta anche [Blog Essentials](/help/communities/blog-developer-basics.md) .

Quando viene aggiunto a un modello, si apre la seguente finestra di dialogo:

![componente blog](assets/blog-component.png)

* [Impostazioni titolo e URL](#title-and-url-settings)

* **Consenti membri privilegiati**

   Se selezionato, il blog consente solo ai membri privilegiati di creare articoli consentendo la selezione di un [gruppo di membri privilegiati](/help/communities/users.md#privileged-members-group). Se non è selezionato, tutti i membri della community possono creare. Il valore predefinito è deselezionato.

* **Consenti caricamenti file**

   Se selezionato, il blog include la possibilità per i membri di caricare i file. Il valore predefinito è selezionato.

* **Consenti risposte concatenate**

   Se non è selezionato, il blog consente le risposte (commenti) a un articolo, ma le risposte ai commenti non sono consentite. Il valore predefinito è selezionato.

* **Consenti contenuto in primo piano**

   Se selezionato, il blog è identificato come [contenuto in primo piano](/help/communities/featured.md). Il valore predefinito è selezionato.

### Funzione Calendario {#calendar-function}

La funzione Calendario è una pagina con un [componente Calendario](/help/communities/calendar.md) configurato per consentire l’assegnazione di tag. Per gli sviluppatori, consulta anche [Calendar Essentials](/help/communities/calendar-basics-for-developers.md) .

Quando viene aggiunto a un modello, si apre la seguente finestra di dialogo:

![dettagli calendario](assets/calendar-details.png)

* [Impostazioni titolo e URL](#title-and-url-settings)

* **Consenti blocco**

   Se selezionato, il forum consente di fissare le risposte dell’argomento all’inizio dell’elenco dei commenti. Il valore predefinito è selezionato.

* **Consenti membri privilegiati**

   Se selezionato, il blog consente solo ai membri privilegiati di creare articoli consentendo la selezione di un [gruppo di membri privilegiati](/help/communities/users.md#privileged-members-group). Se non è selezionato, tutti i membri della community possono creare. Il valore predefinito è deselezionato.

* **Consenti caricamenti file**

   Se selezionato, il blog include la possibilità per i membri di caricare i file. Il valore predefinito è selezionato.

* **Consenti risposte concatenate**

   Se non è selezionato, il blog consente le risposte (commenti) a un articolo, ma le risposte ai commenti non sono consentite. Il valore predefinito è selezionato.

* **Consenti contenuto in primo piano**

   Se selezionato, il relativo contenuto è identificato come [contenuto in primo piano](/help/communities/featured.md). Il valore predefinito è selezionato.

### Funzione Catalogo {#catalog-function}

La funzione di catalogo consente ai membri della [community di abilitazione](/help/communities/overview.md#enablement-community) di sfogliare le risorse di abilitazione che non sono loro assegnate. Per gli sviluppatori, consulta [Assegnazione tag alle risorse di abilitazione](/help/communities/tag-resources.md) e [Nozioni di base sul catalogo](/help/communities/catalog-developer-essentials.md) .

Tutte le risorse di abilitazione e i percorsi di apprendimento per il sito community vengono visualizzati in tutti i cataloghi se la relativa proprietà, ` [Show in Catalog](/help/communities/resources.md)`, è impostata su true. Per includere in modo esplicito le risorse e i percorsi di apprendimento, è necessario applicare un [pre-filtro](/help/communities/catalog-developer-essentials.md#pre-filters) al catalogo.

Quando viene aggiunta a un modello, la configurazione consente di specificare i namespace dei tag utilizzati per configurare il filtro tag presentato ai visitatori del sito:

![Funzione di catalogo](assets/catalog-function.png)

* [Impostazioni titolo e URL](#title-and-url-settings)

* **Seleziona tutti i namespace**

   Gli spazi dei nomi dei tag selezionati definiscono quali tag possono essere selezionati dai visitatori per filtrare l’elenco delle risorse di abilitazione elencate nel catalogo.
Se selezionato, sono disponibili tutti i namespace dei tag consentiti per il sito community.
Se deselezionato, è possibile selezionare uno o più namespace consentiti per il sito community.
Il valore predefinito è selezionato.

### Funzione di contenuto {#featured-content-function}

La funzione di contenuto in primo piano è una pagina con un [componente Contenuto in primo piano](/help/communities/featured.md) configurato per consentire l’aggiunta e l’eliminazione di commenti.

La possibilità di utilizzare il contenuto può essere consentita o disabilitata per componente (consulta [Funzione blog](#blog-function), [Funzione calendario](#calendar-function), [Funzione forum](#forum-function), [Funzione ideazione](#ideation-function) e [Funzione QnA](#qna-function)).

Quando viene aggiunta a un modello, l’unica configurazione è per [Impostazioni titolo e URL](#title-and-url-settings).

### Funzione Libreria file {#file-library-function}

La funzione libreria file è una pagina con un [componente Libreria file](/help/communities/file-library.md) configurato per consentire l&#39;aggiunta e l&#39;eliminazione di commenti.

Quando viene aggiunta a un modello, l’unica configurazione è per [Impostazioni titolo e URL](#title-and-url-settings).

### Funzione Forum {#forum-function}

La funzione forum è una pagina con un [componente Forum](/help/communities/forum.md) configurato per l’assegnazione di tag, il caricamento di file, i seguenti membri per la modifica automatica, il voto e la moderazione.

Quando viene aggiunto a un modello, si apre la seguente finestra di dialogo:

#### Dettagli funzione di configurazione {#configuration-function-details-2}

![forum-component1](assets/forum-component1.png)

* [Impostazioni titolo e URL](#title-and-url-settings)

* **Consenti blocco**

   Se selezionato, il forum consente di fissare le risposte dell’argomento all’inizio dell’elenco dei commenti. Il valore predefinito è selezionato.

* **Consenti membri privilegiati**

   Se selezionato, il forum consente solo ai membri privilegiati di pubblicare argomenti consentendo la selezione di un [gruppo di membri privilegiati](/help/communities/users.md#privileged-members-group). Se non è selezionata, tutti i membri della community possono effettuare la pubblicazione. Il valore predefinito è deselezionato.

* **Consenti caricamenti file**

   Se selezionato, il forum include la possibilità per i membri di caricare i file. Il valore predefinito è selezionato.

* **Consenti risposte concatenate**

   Se non è selezionato, il forum consente l’inserimento di commenti su un argomento, ma le risposte a tali commenti non sono consentite. Il valore predefinito è selezionato.

* **Consenti contenuto in primo piano**

   Se selezionato, il contenuto del componente viene identificato come [contenuto in primo piano](/help/communities/featured.md). Il valore predefinito è selezionato.

### Funzione Groups {#groups-function}

>[!CAUTION]
>
>La funzione dei gruppi deve essere *not* la funzione *prima o la funzione unica* nella struttura di un sito o in un modello di sito community.
>
>Qualsiasi altra funzione, come la [funzione pagina](#page-function), deve essere inclusa ed elencata per prima.

La funzione gruppi consente ai membri della community di creare sottocommunity all’interno del sito della community nell’ambiente di pubblicazione.

A seconda delle [impostazioni](/help/communities/sites-console.md#groupmanagement) quando la funzione Groups è inclusa in un [modello di sito community](/help/communities/sites.md), i gruppi possono essere pubblici o privati e uno o più modelli di gruppo community possono essere configurati per fornire una scelta di modelli quando il gruppo community viene effettivamente creato (ad esempio dall&#39;ambiente di pubblicazione). Un [modello di gruppo community](/help/communities/tools-groups.md) specifica quali funzioni di Communities vengono create per le pagine del gruppo, ad esempio forum e calendari.

Quando viene creato un gruppo di community, viene creato in modo dinamico un gruppo di membri per il nuovo gruppo, a cui è possibile assegnare o unire i membri. Per ulteriori informazioni, consulta [Gestione di utenti e gruppi di utenti](/help/communities/users.md).

A partire dal [feature pack 1](/help/communities/deploy-communities.md#latestfeaturepack) di Communities, i gruppi di community vengono creati nell&#39;ambiente di authoring utilizzando la [console Gruppi di siti di Communities](/help/communities/groups.md) e possono essere creati nell&#39;ambiente di pubblicazione quando abilitato.

Quando viene aggiunto a un modello, si apre la seguente finestra di dialogo:

![group-template-config](assets/group-template-config.png)

* [Impostazioni titolo e URL](#title-and-url-settings)

* **Seleziona modelli per gruppi**

   Un elenco a discesa che consente di selezionare uno o più modelli di gruppo abilitati da cui scegliere il futuro creatore di un nuovo gruppo community (nell’ambiente di pubblicazione).

* **Consenti membri privilegiati**

   Se selezionato, il forum consente solo ai membri privilegiati di pubblicare argomenti consentendo la selezione di un [gruppo di sicurezza dei membri privilegiati](/help/communities/users.md#privileged-members-group). Se non è selezionata, tutti i membri della community possono effettuare la pubblicazione. Il valore predefinito è deselezionato.

* **Consenti creazione pubblicazione**

   Se selezionato, i membri della community autorizzati possono creare un gruppo nell’ambiente di pubblicazione. Se deselezionato, i nuovi gruppi (sub-community) possono essere creati solo nell’ambiente di authoring dalla console Gruppi di Communities Sites .
Il valore predefinito è selezionato.

### Funzione ideazione {#ideation-function}

La funzione di ideazione è una pagina con un [componente Ideazione](/help/communities/ideation-feature.md).

Quando viene aggiunta a un modello, viene visualizzata la finestra di dialogo seguente, che specifica il Titolo e i nomi URL predefiniti, nonché le impostazioni di visualizzazione predefinite per il modello:

![funzione d&#39;ideazione](assets/ideation-function.png)

* [Impostazioni titolo e URL](#title-and-url-settings)

* **Consenti membri privilegiati**

   Se selezionato, il forum consente solo ai membri privilegiati di pubblicare argomenti consentendo la selezione di un [gruppo di sicurezza dei membri privilegiati](/help/communities/users.md#privileged-members-group). Se non è selezionata, tutti i membri della community possono effettuare la pubblicazione. Il valore predefinito è deselezionato.

* **Consenti caricamenti file**

   Se selezionata, l’idea include la possibilità per i membri di caricare i file. Il valore predefinito è selezionato.

* **Consenti risposte concatenate**

   Se non è selezionata, l’idea consente di rispondere (commenti) a un argomento, ma non di rispondere ai commenti. Il valore predefinito è selezionato.

* **Consenti contenuto in primo piano**

   Se selezionato, il relativo contenuto è identificato come [contenuto in primo piano](/help/communities/featured.md). Il valore predefinito è selezionato.

### Funzione Classifica {#leaderboard-function}

La funzione della classifica è una pagina con un [componente della classifica](/help/communities/enabling-leaderboard.md).

**NOTA**: Il componente Leaderboard deve essere ulteriormente configurato  ** dopo la creazione di un sito community da un modello community che include la funzione Leaderboard. Specifica le [regole](/help/communities/enabling-leaderboard.md#rules-tab) del componente Leaderboard, che dipendono dalla configurazione di [punteggio e badge](/help/communities/implementing-scoring.md) per il sito della community.

Quando viene aggiunta a un modello, viene visualizzata la finestra di dialogo seguente, che specifica il Titolo e i nomi URL predefiniti, nonché le impostazioni di visualizzazione predefinite per il modello:

![classifica-dialogo](assets/leaderboard-dialog.png)

* [Impostazioni titolo e URL](#title-and-url-settings)

* **Visualizza badge**

   Se selezionata, nella classifica è inclusa una colonna per le icone di badge.
Il valore predefinito è deselezionato.

* **Nome badge visualizzato**

   Se questa opzione è selezionata, nella classifica è inclusa una colonna per il nome del badge.
Il valore predefinito è deselezionato.

* **Visualizza avatar**

   Se selezionata, l&#39;immagine avatar del membro viene inclusa nella classifica, accanto al suo collegamento nome al suo profilo membro.
Il valore predefinito è deselezionato.

### Funzione Pagina {#page-function}

La funzione page aggiunge al sito community una pagina vuota che è collegata alle funzioni del sito community: accesso, menu, notifiche, messaggistica, temi e branding. Il contenuto viene aggiunto alla pagina utilizzando la [modalità di creazione AEM standard](/help/sites-authoring/editing-content.md).

Quando viene aggiunta a un modello, l’unica configurazione è per [Impostazioni titolo e URL](#title-and-url-settings).

### Funzione D/R {#qna-function}

La funzione QnA è una pagina con un componente [QnA](/help/communities/working-with-qna.md) configurato per l&#39;assegnazione di tag, il caricamento di file, i seguenti elementi, i membri per la modifica automatica, il voto e la moderazione.

Quando viene aggiunta a un modello, la configurazione consente restrizioni ai membri con privilegi:

![qna-dialog](assets/qna-dialog.png)

* [Impostazioni titolo e URL](#title-and-url-settings)

* **Consenti blocco**

   Se selezionato, il forum consente di fissare le risposte dell’argomento all’inizio dell’elenco dei commenti. Il valore predefinito è selezionato.

* **Consenti membri privilegiati**

   Se selezionato, il forum QnA consente solo ai membri privilegiati di inviare domande consentendo la selezione di un [gruppo di membri privilegiati](/help/communities/users.md#privileged-members-group). Se non è selezionata, tutti i membri della community possono effettuare la pubblicazione. Il valore predefinito è deselezionato.

* **Consenti caricamenti file**

   Se selezionato, il forum QnA include la possibilità per i membri di caricare i file. Il valore predefinito è selezionato.

* **Consenti risposte concatenate**

   Se non è selezionato, il forum QnA consente di inserire commenti (risposte) a una domanda pubblicata, ma non è consentito rispondere alle risposte. Il valore predefinito è selezionato.

* **Consenti contenuto in primo piano**

   Se selezionato, il relativo contenuto è identificato come [contenuto in primo piano](/help/communities/featured.md). Il valore predefinito è selezionato.

## Crea funzione community {#create-community-function}

Per creare una funzione community, seleziona l’icona `Create Community Function` situata nella parte superiore della console Funzioni community . È possibile creare più funzioni basate sullo stesso Blueprint AEM e quindi personalizzate in modo univoco aprendo in modalità di modifica dell’autore.

![funzione create-community](assets/create-community-function.png)

### Nome funzione community {#community-function-name}

![nome funzione](assets/function-name.png)

Nel pannello Nome funzione community sono configurati un nome, una descrizione e se la funzione è abilitata o disabilitata:

* **Nome funzione community**

   Nome della funzione utilizzata per la visualizzazione e l&#39;archiviazione.

* **Descrizione della funzione community**

   Descrizione della funzione per la visualizzazione.

* **Disabilitato/Abilitato**

   Interruttore che controlla se la funzione è referenziabile.

### Blueprint AEM {#aem-blueprint}

![blueprint aem](assets/aem-blueprint.png)

Nel pannello `AEM Blueprint` è possibile selezionare il modello che è l&#39;implementazione sottostante della funzione community.

La funzione community è un mini sito che include una o più pagine, preconnesso per l’inclusione in un sito community con login, profili utente, notifiche, messaggistica, menu del sito, ricerca, temi e funzioni di branding. Una volta creata la funzione, è possibile [aprire la funzione](#open-community-function) in modalità di modifica dell&#39;autore e personalizzare le impostazioni della pagina o del componente.

Poiché la funzione community è implementata come [Live Copy](/help/sites-administering/msm.md#live-copies) di un [blueprint](/help/sites-administering/msm-livecopy.md#creatingablueprint), è possibile eseguire il rollout delle modifiche apportate a una funzione che interessa tutte le pagine del sito community create dal [modello di sito community](/help/communities/sites.md) o dal [modello di gruppo community](/help/communities/tools-groups.md) che include la funzione. È inoltre possibile dissociare una pagina dalla blueprint principale per apportare modifiche a livello di pagina.

Vedere anche [Multi Site Manager](/help/sites-administering/msm.md).

### Miniatura  {#thumbnail}

![miniatura funzione](assets/funtion-thumbnail.png)

Nel pannello Miniatura, è possibile caricare un&#39;immagine da visualizzare nella [console Funzioni della community](#community-functions-console).

## Apri funzione community {#open-community-function}

![a funzionamento aperto](assets/open-function.png)

Seleziona l’ icona `Open Community Function` per accedere alla modalità di modifica dell’autore per creare il contenuto della pagina e modificare la configurazione dei componenti della funzione.

### Configurazione dei componenti {#configuring-components}

Una funzione community viene implementata come Live Copy di una blueprint AEM, i cui dettagli sono documentati in [Multi Site Manager](/help/sites-administering/msm.md).

È possibile non solo creare il contenuto della pagina, ma anche configurare i componenti.

Se si configura un componente in una pagina di un sito community creato, potrebbe essere necessario annullare [ereditarietà](/help/sites-administering/msm-livecopy.md#changing-live-copy-content) per configurare il componente. L’ereditarietà deve essere ristabilita al termine della configurazione.

Per informazioni sulla configurazione, visita [Componenti di Communities](/help/communities/author-communities.md) per gli autori.

## Funzione modifica per community {#edit-community-function}

![funzione di modifica](assets/edit-function.png)

Seleziona l&#39;icona `Edit Community Function` per modificare le proprietà della funzione utilizzando gli stessi pannelli di [creazione di una funzione community](#create-community-function), inclusa l&#39;abilitazione o la disattivazione della funzione.
