---
title: Funzioni community
description: Scopri come accedere alla console Funzioni community
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
docset: aem65
role: Admin
exl-id: 2395c895-c611-43ac-abb6-c2bc4b4a41f4
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '2215'
ht-degree: 2%

---

# Funzioni community{#community-functions}

Il tipo di funzioni previste da un’esperienza della community sono ben note. Le funzioni della community sono disponibili come funzioni della community. In sostanza, si tratta di una o più pagine collegate per implementare una funzione per la community che richiede molto di più della semplice aggiunta di un componente a una pagina in modalità di authoring. Si tratta dei blocchi predefiniti utilizzati per definire la struttura di un [modello di sito community](/help/communities/sites.md) da cui vengono creati [siti community](/help/communities/sites-console.md).

Una volta creato il sito della community, il contenuto può essere aggiunto alle pagine risultanti utilizzando la [modalità di creazione AEM standard](/help/sites-authoring/editing-content.md). Sono disponibili diverse funzioni per la community, come illustrato nella console delle funzioni per la community.

>[!NOTE]
>
>Le console per la creazione di [siti community](/help/communities/sites-console.md), [modelli di siti community](/help/communities/sites.md), [modelli di gruppi community](/help/communities/tools-groups.md) e [funzioni community](/help/communities/functions.md) sono utilizzabili solo nell&#39;ambiente di authoring.

## Console funzioni community {#community-functions-console}

Per raggiungere la console delle funzioni community nell’ambiente di authoring:

* Passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Community]** > **[!UICONTROL Funzioni community]**.

![funzioni-community](assets/community-functions.png)

## Funzioni predefinite {#pre-built-functions}

Segue una breve descrizione delle funzioni fornite con AEM Communities. Ogni funzione include una o più pagine AEM contenenti componenti Communities collegati tra loro in una funzione che viene facilmente incorporata in un [modello di sito community](/help/communities/sites.md).

Un modello di sito community fornisce la struttura di un sito community, incluse le funzioni di accesso, profili utente, notifiche, messaggistica, menu del sito, ricerca, temi e branding.

### Impostazioni titolo e URL {#title-and-url-settings}

**Title** e **URL** sono proprietà comuni a tutte le funzioni community.

Quando una funzione di community viene aggiunta a un modello di sito di community o [modifica](/help/communities/sites-console.md#modifying-site-properties) la struttura di un sito di community, viene visualizzata la finestra di dialogo della funzione in cui è possibile configurare Titolo e URL.

#### Dettagli funzione di configurazione {#configuration-function-details}

![title-url-details](assets/title-url-details.png)

* **Titolo**

  (*Obbligatorio*) Testo visualizzato nel menu delle funzionalità del sito

* **URL**

  (*Obbligatorio*) Nome utilizzato per generare l&#39;URI. Il nome deve essere conforme alle [convenzioni di denominazione](/help/sites-developing/naming-conventions.md) imposte da AEM e JCR.

Ad esempio, utilizzando il sito creato seguendo l&#39;esercitazione [Guida introduttiva](/help/communities/getting-started.md), se

* Title = Pagina Web
* URL = pagina

L’URL della pagina è https://localhost:4503/content/sites/engage/en/page.html

e il collegamento del menu per la pagina viene visualizzato come:

![pagina-coinvolgimento](assets/engage-page.png)

### Funzione Flusso attività {#activity-stream-function}

La funzione di flusso attività è una pagina con un [componente Flussi attività](/help/communities/activities.md) in cui sono selezionate tutte le visualizzazioni (tutte le attività, le attività utente e seguenti). Consulta anche [Activity Stream Essentials](/help/communities/essentials-activities.md) per sviluppatori.

Quando si aggiunge un modello, viene visualizzata la seguente finestra di dialogo:

#### Dettagli funzione di configurazione {#configuration-function-details-1}

![dettagli-funzione](assets/function-details.png)

* [Impostazioni titolo e URL](#title-and-url-settings)

* **Mostra la vista &quot;Le mie attività&quot;**

  Se selezionata, la pagina Attività include una scheda che filtra le attività in base a quelle generate all&#39;interno della community dal membro corrente. L&#39;opzione Predefinita è selezionata.

* **Mostra visualizzazione &quot;Tutte le attività&quot;**

  Se selezionata, la pagina Attività include una scheda che include tutte le attività generate all&#39;interno della comunità a cui il membro corrente ha accesso. L&#39;opzione Predefinita è selezionata.

* **Mostra visualizzazione &quot;Feed notizie&quot;**

  Se selezionata, le pagine Attività includono una scheda che filtra le attività in base a quelle che il membro corrente sta seguendo. L&#39;opzione Predefinita è selezionata.

### Funzione Blog {#blog-function}

La funzione blog è una pagina con un [componente Blog](/help/communities/blog-feature.md) configurato per l&#39;assegnazione di tag, il caricamento di file e i seguenti membri per la modifica automatica, il voto e la moderazione. Consulta anche [Blog Essentials](/help/communities/blog-developer-basics.md) per sviluppatori.

Quando si aggiunge un modello, viene visualizzata la seguente finestra di dialogo:

![componente-blog](assets/blog-component.png)

* [Impostazioni titolo e URL](#title-and-url-settings)

* **Consenti membri privilegiati**

  Se selezionato, il blog consente solo ai membri con privilegi di creare articoli consentendo la selezione di un [gruppo di membri con privilegi](/help/communities/users.md#privileged-members-group). Se non viene selezionata, tutti i membri della community possono creare. Il valore predefinito è deselezionato.

* **Consenti caricamenti file**

  Se viene selezionato, il blog consente ai membri di caricare i file. L&#39;opzione Predefinita è selezionata.

* **Consenti risposte concatenate**

  Se non è selezionato, il blog consente di rispondere (commenti) a un articolo, ma non di rispondere ai commenti. L&#39;opzione Predefinita è selezionata.

* **Consenti contenuto in primo piano**

  Se selezionato, il blog viene identificato come [contenuto in primo piano](/help/communities/featured.md). L&#39;opzione Predefinita è selezionata.

### Funzione Calendario {#calendar-function}

La funzione calendario è una pagina con un [componente Calendario](/help/communities/calendar.md) configurato per consentire l&#39;assegnazione di tag. Consulta anche [Calendar Essentials](/help/communities/calendar-basics-for-developers.md) per sviluppatori.

Quando si aggiunge un modello, viene visualizzata la seguente finestra di dialogo:

![dettagli-calendario](assets/calendar-details.png)

* [Impostazioni titolo e URL](#title-and-url-settings)

* **Consenti blocco**

  Se viene selezionato, il forum consente di fissare le risposte all&#39;argomento all&#39;inizio dell&#39;elenco dei commenti. L&#39;opzione Predefinita è selezionata.

* **Consenti membri privilegiati**

  Se selezionato, il blog consente solo ai membri con privilegi di creare articoli consentendo la selezione di un [gruppo di membri con privilegi](/help/communities/users.md#privileged-members-group). Se non viene selezionata, tutti i membri della community possono creare. Il valore predefinito è deselezionato.

* **Consenti caricamenti file**

  Se viene selezionato, il blog consente ai membri di caricare i file. L&#39;opzione Predefinita è selezionata.

* **Consenti risposte concatenate**

  Se non è selezionato, il blog consente di rispondere (commenti) a un articolo, ma non di rispondere ai commenti. L&#39;opzione Predefinita è selezionata.

* **Consenti contenuto in primo piano**

  Se viene selezionato, il contenuto verrà identificato come [contenuto in primo piano](/help/communities/featured.md). L&#39;opzione Predefinita è selezionata.

### Funzione contenuto in primo piano {#featured-content-function}

La funzione di contenuto in primo piano è una pagina con un [componente di contenuto in primo piano](/help/communities/featured.md) configurato per consentire l&#39;aggiunta e l&#39;eliminazione di commenti.

È possibile che la funzionalità del contenuto sia consentita o meno per ogni componente (vedere [Funzione blog](#blog-function), [Funzione calendario](#calendar-function), [Funzione forum](#forum-function), [Funzione ideazione](#ideation-function) e [Funzione QnA](#qna-function)).

Quando viene aggiunta a un modello, l&#39;unica configurazione è per [Impostazioni titolo e URL](#title-and-url-settings).

### Funzione Libreria file {#file-library-function}

La funzione libreria file è una pagina con un [componente Libreria file](/help/communities/file-library.md) configurato per consentire l&#39;aggiunta e l&#39;eliminazione di commenti.

Quando viene aggiunta a un modello, l&#39;unica configurazione è per [Impostazioni titolo e URL](#title-and-url-settings).

### Funzione Forum {#forum-function}

La funzione forum è una pagina con un [componente forum](/help/communities/forum.md) configurato per l&#39;assegnazione di tag, il caricamento di file e di seguito i membri per la modifica automatica, il voto e la moderazione.

Quando si aggiunge un modello, viene visualizzata la seguente finestra di dialogo:

#### Dettagli funzione di configurazione {#configuration-function-details-2}

![componente forum1](assets/forum-component1.png)

* [Impostazioni titolo e URL](#title-and-url-settings)

* **Consenti blocco**

  Se viene selezionato, il forum consente di fissare le risposte all&#39;argomento all&#39;inizio dell&#39;elenco dei commenti. L&#39;opzione Predefinita è selezionata.

* **Consenti membri privilegiati**

  Se viene selezionato, il forum consente solo ai membri con privilegi di pubblicare argomenti consentendo la selezione di un [gruppo di membri con privilegi](/help/communities/users.md#privileged-members-group). Se non è selezionata, tutti i membri della community possono pubblicare post. Il valore predefinito è deselezionato.

* **Consenti caricamenti file**

  Se viene selezionato, il forum consente ai membri di caricare i file. L&#39;opzione Predefinita è selezionata.

* **Consenti risposte concatenate**

  Se non viene selezionato, il forum consente di inserire commenti su un argomento, ma non è consentito rispondere a tali commenti. L&#39;opzione Predefinita è selezionata.

* **Consenti contenuto in primo piano**

  Se viene selezionato, il contenuto del componente viene identificato come [contenuto in primo piano](/help/communities/featured.md). L&#39;opzione Predefinita è selezionata.

### Funzione Gruppi {#groups-function}

>[!CAUTION]
>
>La funzione dei gruppi deve *non* essere la *prima o l&#39;unica* funzione nella struttura di un sito o in un modello di sito community.
>
>Qualsiasi altra funzione, ad esempio la funzione [page](#page-function), deve essere inclusa ed elencata per prima.

La funzione gruppi consente ai membri della community di creare sottocomunità all’interno del sito community nell’ambiente di pubblicazione.

A seconda delle [impostazioni](/help/communities/sites-console.md#groupmanagement) quando la funzione Gruppi è inclusa in un [modello di sito community](/help/communities/sites.md), i gruppi possono essere pubblici o privati e uno o più modelli di gruppo community possono essere configurati per fornire una scelta di modelli quando il gruppo community viene effettivamente creato (ad esempio dall&#39;ambiente di pubblicazione). Un [modello per gruppi community](/help/communities/tools-groups.md) specifica le funzionalità delle community create per le pagine dei gruppi, ad esempio forum e calendari.

Quando si crea un gruppo community, viene creato in modo dinamico un gruppo di membri per il nuovo gruppo, al quale è possibile assegnare o unire membri. Per ulteriori informazioni, vedere [Gestione di utenti e gruppi di utenti](/help/communities/users.md).

A partire da Communities [feature pack 1](/help/communities/deploy-communities.md#latestfeaturepack), i gruppi community vengono creati nell&#39;ambiente di authoring utilizzando la console [Communities Sites&#39; Groups](/help/communities/groups.md) e possono essere creati nell&#39;ambiente di pubblicazione se abilitati.

Quando si aggiunge un modello, viene visualizzata la seguente finestra di dialogo:

![group-template-config](assets/group-template-config.png)

* [Impostazioni titolo e URL](#title-and-url-settings)

* **Seleziona modelli di gruppo**

  Un elenco a discesa che consente di selezionare uno o più modelli di gruppo abilitati tra cui può scegliere il futuro creatore di un nuovo gruppo community (nell’ambiente di pubblicazione).

* **Consenti membri privilegiati**

  Se viene selezionato, il forum consente solo ai membri con privilegi di pubblicare argomenti consentendo la selezione di un [gruppo di sicurezza dei membri con privilegi](/help/communities/users.md#privileged-members-group). Se non è selezionata, tutti i membri della community possono pubblicare post. Il valore predefinito è deselezionato.

* **Consenti creazione Publish**

  Se questa opzione è selezionata, i membri autorizzati della community possono creare un gruppo nell’ambiente di pubblicazione. Se questa opzione è deselezionata, è possibile creare nuovi gruppi (sottocomunità) nell’ambiente di authoring solo dalla console Gruppi di siti community.
L&#39;opzione Predefinita è selezionata.

### Funzione ideazione {#ideation-function}

La funzione di ideazione è una pagina con un [componente ideazione](/help/communities/ideation-feature.md).

Quando viene aggiunto a un modello, viene visualizzata la seguente finestra di dialogo che specifica i nomi di titolo e URL predefiniti e le impostazioni di visualizzazione predefinite per il modello:

![funzione-ideazione](assets/ideation-function.png)

* [Impostazioni titolo e URL](#title-and-url-settings)

* **Consenti membri privilegiati**

  Se viene selezionato, il forum consente solo ai membri con privilegi di pubblicare argomenti consentendo la selezione di un [gruppo di sicurezza dei membri con privilegi](/help/communities/users.md#privileged-members-group). Se non è selezionata, tutti i membri della community possono pubblicare post. Il valore predefinito è deselezionato.

* **Consenti caricamenti file**

  Se selezionata, l&#39;idea include la possibilità per i membri di caricare i file. L&#39;opzione Predefinita è selezionata.

* **Consenti risposte concatenate**

  Se non viene selezionata, l&#39;idea consente di rispondere (commenti) a un argomento, ma non di rispondere ai commenti. L&#39;opzione Predefinita è selezionata.

* **Consenti contenuto in primo piano**

  Se viene selezionato, il contenuto verrà identificato come [contenuto in primo piano](/help/communities/featured.md). L&#39;opzione Predefinita è selezionata.

### Funzione Classifica {#leaderboard-function}

La funzione classifica è una pagina con un [componente classifica](/help/communities/enabling-leaderboard.md).

**NOTA**: il componente Classifica richiede un&#39;ulteriore configurazione *dopo* la creazione di un sito community da un modello di community che include la funzione Classifica. Specifica le [regole](/help/communities/enabling-leaderboard.md#rules-tab) del componente Classifica, che dipendono dalla configurazione di [punteggi e distintivi](/help/communities/implementing-scoring.md) per il sito community.

Quando viene aggiunto a un modello, viene visualizzata la seguente finestra di dialogo che specifica i nomi di titolo e URL predefiniti e le impostazioni di visualizzazione predefinite per il modello:

![finestra di dialogo della classifica](assets/leaderboard-dialog.png)

* [Impostazioni titolo e URL](#title-and-url-settings)

* **Distintivo visualizzato**

  Se questa opzione è selezionata, nella classifica verrà inclusa una colonna per le icone dei badge.
Il valore predefinito è deselezionato.

* **Nome badge visualizzato**

  Se questa opzione è selezionata, nella classifica viene inclusa una colonna per il nome del badge.
Il valore predefinito è deselezionato.

* **Visualizza avatar**

  Se l&#39;opzione è selezionata, l&#39;immagine avatar del membro viene inclusa nella classifica, accanto al collegamento del nome al suo profilo membro.
Il valore predefinito è deselezionato.

### Funzione Pagina {#page-function}

La funzione di pagina aggiunge una pagina vuota al sito community da collegare alle funzioni del sito community: accesso, menu, notifiche, messaggi, temi e branding. Il contenuto viene aggiunto alla pagina utilizzando la [modalità di creazione AEM standard](/help/sites-authoring/editing-content.md).

Quando viene aggiunta a un modello, l&#39;unica configurazione è per [Impostazioni titolo e URL](#title-and-url-settings).

### Funzione D/R {#qna-function}

La funzione QnA è una pagina con un componente [QnA](/help/communities/working-with-qna.md) configurato per l&#39;assegnazione di tag, il caricamento di file e i seguenti membri per la modifica automatica, il voto e la moderazione.

Quando viene aggiunta a un modello, la configurazione consente di limitare i membri con privilegi:

![qna-dialog](assets/qna-dialog.png)

* [Impostazioni titolo e URL](#title-and-url-settings)

* **Consenti blocco**

  Se viene selezionato, il forum consente di fissare le risposte all&#39;argomento all&#39;inizio dell&#39;elenco dei commenti. L&#39;opzione Predefinita è selezionata.

* **Consenti membri privilegiati**

  Se viene selezionato, il forum QnA consente solo ai membri con privilegi di pubblicare domande consentendo la selezione di un [gruppo di membri con privilegi](/help/communities/users.md#privileged-members-group). Se non è selezionata, tutti i membri della community possono pubblicare post. Il valore predefinito è deselezionato.

* **Consenti caricamenti file**

  Se viene selezionato, il forum QnA consente ai membri di caricare i file. L&#39;opzione Predefinita è selezionata.

* **Consenti risposte concatenate**

  Se non viene selezionato, il forum di QnA consente di inserire commenti (risposte) a una domanda pubblicata, ma non sono consentite risposte alle risposte. L&#39;opzione Predefinita è selezionata.

* **Consenti contenuto in primo piano**

  Se viene selezionato, il contenuto verrà identificato come [contenuto in primo piano](/help/communities/featured.md). L&#39;opzione Predefinita è selezionata.

## Crea funzione community {#create-community-function}

È possibile creare una funzione community selezionando l&#39;icona `Create Community Function` nella parte superiore della console Funzioni community. È possibile creare più funzioni basate sulla stessa blueprint AEM e personalizzarle in modo univoco aprendo la modalità di modifica dell’autore.

![create-community-function](assets/create-community-function.png)

### Nome funzione community {#community-function-name}

![nome-funzione](assets/function-name.png)

Nel pannello Nome funzione community, vengono configurati un nome, una descrizione e l’abilitazione o meno della funzione:

* **Nome funzione community**

  Nome della funzione utilizzato per la visualizzazione e l&#39;archiviazione.

* **Descrizione funzione community**

  Descrizione della funzione per la visualizzazione.

* **Disabilitato/Abilitato**

  Un interruttore che controlla se la funzione è referenziabile.

### Blueprint AEM {#aem-blueprint}

![aem-blueprint](assets/aem-blueprint.png)

Nel pannello `AEM Blueprint` è possibile selezionare il blueprint che è l&#39;implementazione sottostante della funzione community.

La funzione community è un mini sito che include una o più pagine, precollegate per l’inserimento in un sito community e include le funzioni di accesso, profili utente, notifiche, messaggistica, menu del sito, ricerca, temi e branding. Una volta creata la funzione, è possibile [aprirla](#open-community-function) in modalità di modifica dell&#39;autore e personalizzare le impostazioni della pagina o del componente.

Poiché la funzione community è implementata come [Live Copy](/help/sites-administering/msm.md#live-copies) di un [blueprint](/help/sites-administering/msm-livecopy.md#creatingablueprint), è possibile eseguire il rollout delle modifiche apportate a una funzione che influisce su tutte le pagine del sito community create dal [modello di sito community](/help/communities/sites.md) o dal [modello di gruppo community](/help/communities/tools-groups.md) che include la funzione. È inoltre possibile dissociare una pagina dalla blueprint principale per apportare modifiche a livello di pagina.

Vedere anche [Gestione multisito](/help/sites-administering/msm.md).

### Miniatura  {#thumbnail}

![funzione-miniatura](assets/funtion-thumbnail.png)

Nel pannello Miniature è possibile caricare un&#39;immagine da visualizzare nella [console Funzioni community](#community-functions-console).

## Apri funzione community {#open-community-function}

![open-function](assets/open-function.png)

Seleziona l’icona `Open Community Function` per accedere alla modalità di modifica dell’autore per creare il contenuto della pagina e modificare la configurazione dei componenti della funzione.

### Configurazione dei componenti {#configuring-components}

Una funzione community viene implementata come Live Copy di un blueprint AEM, i cui dettagli sono documentati in [Multi Site Manager](/help/sites-administering/msm.md).

È possibile non solo creare il contenuto della pagina, ma anche configurare i componenti.

Se si configura un componente in una pagina di un sito community creato, potrebbe essere necessario annullare [ereditarietà](/help/sites-administering/msm-livecopy.md#changing-live-copy-content) per configurare il componente. Al termine della configurazione, l’ereditarietà deve essere ristabilita.

Per informazioni sulla configurazione, visitare [Componenti community](/help/communities/author-communities.md) per gli autori.

## Funzione modifica per community {#edit-community-function}

![modifica-funzione](assets/edit-function.png)

Selezionare l&#39;icona `Edit Community Function` per modificare le proprietà della funzione utilizzando gli stessi pannelli di [creazione di una funzione community](#create-community-function), inclusa l&#39;attivazione o la disattivazione della funzione.
