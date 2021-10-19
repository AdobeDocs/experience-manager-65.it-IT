---
title: Console Gruppi per community
seo-title: Community Groups Console
description: La console Gruppi consente di creare gruppi community
seo-description: Groups console lets you create Community groups
uuid: 21e2bde3-7354-4193-bcb3-c672c6342252
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: d381ea40-fe49-4d32-bfad-1379c7a02aba
docset: aem65
pagetitle: Community Groups Console
role: Admin
exl-id: ef371ff8-6b4f-4e5a-98fb-d7c274927c46
source-git-commit: 1074843a0105df39382b64defe66fc262986b9c9
workflow-type: tm+mt
source-wordcount: '1678'
ht-degree: 2%

---

# Console Gruppi per community {#community-groups-console}

La console Gruppi consente di accedere alla creazione di gruppi di community quando un sito di una community è [struttura del modello](/help/communities/sites-console.md#step1) include [funzione gruppi](/help/communities/functions.md#groups-function).

* Supporto AEM Communities per la nidificazione dei gruppi all’interno di altri gruppi. La nidificazione del gruppo è possibile quando [Struttura del nuovo gruppo](/help/communities/tools-groups.md) contiene la funzione gruppi .
* Solo per l’ambiente di authoring, esiste una procedura guidata per la creazione di gruppi simile alla procedura guidata per la creazione di siti.
* Il fatto che i membri possano o meno creare gruppi in ambiente di pubblicazione è configurabile quando si aggiunge una funzione Groups a una struttura del sito community o a una struttura di gruppo community.

Dei tre modelli di gruppo inclusi, solo il `Reference Group` il modello include una funzione di gruppi nella relativa struttura.

I diversi aspetti dei gruppi comunitari sono i seguenti:

* **Creazione**: è possibile creare un nuovo gruppo sull’istanza di authoring ed eventualmente di pubblicazione.
* **Controllo**: Il gruppo può essere aperto o segreto.
* **Nidificazione**: Il gruppo può contenere zero o più gruppi.

<!-- This is a 404 on helpx. Please update or remove.
>[!NOTE]
>
>Community groups, created in the publish environment before the [existence of the Community Groups console](/help/communities/version-history.md#featurepack1fp1), will not be listed in the Community Groups console, and thus, are not modifiable using the console.
-->

>[!NOTE]
>
>Questa console Gruppi, accessibile solo dalla console Sites di Communities, non deve essere confusa con il membro [Console Gruppi](/help/communities/members.md) per la gestione dei gruppi di membri.
>
>I gruppi di membri sono gruppi di utenti registrati nell’ambiente di pubblicazione e a cui si accede dall’ambiente di authoring utilizzando [servizio tunnel](/help/communities/deploy-communities.md#tunnel-service-on-author).

## Creazione gruppo {#group-creation}

Per accedere alla console Gruppi :

* All&#39;autore, accedi con privilegi di amministratore.
* Dalla navigazione globale: **[!UICONTROL Community]** > **[!UICONTROL Sites]**.
* Seleziona una cartella del sito community esistente per aprirla.
* Seleziona un&#39;istanza di un sito community all&#39;interno della cartella.

   * La struttura del sito comunitario deve comprendere una funzione di gruppo.
   * Queste schermate vengono visualizzate nell&#39;esercitazione Guida introduttiva dopo [creazione di gruppi in pubblicazione](/help/communities/published-site.md).

   ![create-group](assets/create-group.png)

* Seleziona la **Cartella Gruppi** per aprirlo.

   Quando vengono aperti, vengono visualizzati tutti i gruppi esistenti, creati in fase di creazione o di pubblicazione.

   Da questa console Gruppi è possibile creare nuovi gruppi.

   ![create-new-group](assets/create-new-group.png)

* Seleziona la **Crea gruppo** pulsante .

### Passaggio 1: Modello Gruppo community {#step-community-group-template}

![Gruppi di community multilingue](assets/multi-lingual-group.png)

* **Titolo gruppo community**

   Titolo da visualizzare per il gruppo.
Il titolo viene visualizzato sul sito pubblicato per il gruppo.

* **Descrizione gruppo community**

   Descrizione del gruppo.

* **Directory principale gruppo community**

   Percorso principale del gruppo.
La radice predefinita è il sito padre, ma può essere spostata in qualsiasi posizione all’interno del sito web. Non è consigliabile modificarlo.

* **Lingue disponibili supplementari per i gruppi della community** menu

   Utilizza il menu a discesa per selezionare le lingue disponibili per i gruppi di community. Nel menu vengono visualizzate tutte le lingue in cui viene creato il sito della community principale. In questo singolo passaggio gli utenti possono selezionare una di queste lingue per creare gruppi in più impostazioni internazionali. Lo stesso gruppo viene creato in più lingue specificate nella console Gruppi dei rispettivi siti della community.

* **Nome gruppo community**

   Nome della pagina principale del gruppo che viene visualizzata nell&#39;URL. Evita di usare caratteri di sottolineatura (_) e parole chiave come le risorse e la configurazione nel nome del gruppo.

   * Ricontrolla il nome in quanto non viene facilmente modificato dopo la creazione del gruppo.
   * L’URL di base verrà visualizzato sotto la `Community Group Name`.
   * Per un URL valido, aggiungi &quot;.html&quot;
      *per esempio*, `https://localhost:4502/content/sites/mysight/en/mygroup.html`.

* **Modello Gruppo community** menu

   Utilizza il menu a discesa per scegliere una [modello di gruppo community](/help/communities/tools.md).

### Passaggio 2: Progettazione {#step-design}

### TEMA DEL GRUPPO COMUNITARIO {#community-group-theme}

![communitygrouptheme](assets/communitygrouptheme.png)

Il framework utilizza `Twitter Bootstrap` per fornire al sito un design dinamico e flessibile. È possibile selezionare uno dei molti temi di Bootstrap precaricati per personalizzare lo stile del modello di gruppo community selezionato oppure caricare un tema di Bootstrap.

Se selezionato, il tema verrà sovrapposto con un segno di spunta blu opaco.

È possibile selezionare un tema diverso dal tema del sito padre.

Dopo la pubblicazione del sito, è possibile [modificare le proprietà](#modifyinggroupproperties) e selezionare un tema diverso.

### MARCHIO DEL GRUPPO COMUNITARIO {#community-group-branding}

![marchio di gruppo](assets/community-group-branding.png)

Il branding del sito community è un’immagine visualizzata come intestazione nella parte superiore di ogni pagina. È possibile visualizzare un banner per il gruppo che differisce dalle altre pagine del sito.

Le dimensioni dell’immagine devono essere pari alla visualizzazione prevista della pagina nel browser e a 120 pixel in altezza.

Quando crei o selezioni un’immagine, tieni presente quanto segue:

* L&#39;altezza dell&#39;immagine viene ritagliata a 120 pixel misurati dal bordo superiore dell&#39;immagine
* L&#39;immagine viene fissata al bordo sinistro della finestra del browser
* L&#39;immagine non viene ridimensionata, in modo tale che quando la larghezza dell&#39;immagine è:

   * Inferiore alla larghezza del browser, l&#39;immagine si ripeterà in orizzontale.
   * Maggiore della larghezza del browser, l&#39;immagine apparirà ritagliata.

### Passaggio 3: Impostazioni {#step-settings}

**MODERAZIONE**

![selezionare i ruoli dei membri del gruppo community](assets/group-admin.png)

**Moderatori gruppo community**

Per impostazione predefinita, viene ereditato l&#39;elenco dei moderatori del sito della comunità padre.

È possibile aggiungere moderatori specifici al gruppo. Cerca membri (da ambiente di pubblicazione) per aggiungerli come moderatori

**Amministratori gruppo**

Per impostazione predefinita, l&#39;amministratore del sito della community padre è l&#39;amministratore per i gruppi.

Tuttavia, è possibile assegnare amministratori di gruppo indipendenti. Gli amministratori del gruppo possono gestire il proprio gruppo (ad esempio G1) e creare un sottogruppo nidificato sotto G1. Possono inoltre assegnare amministratori diversi al sottogruppo.

Un utente U1, quindi, può essere un amministratore in un gruppo G1 e un utente regolare nel suo gruppo nidificato G2.

**ISCRIZIONE**

L&#39;impostazione di appartenenza consente di selezionare uno dei tre modi per garantire un gruppo di comunità.

![appartenenza a un gruppo](assets/community-group-membership.png)

* **Iscrizione opzionale**

   Se selezionato, il gruppo community è un gruppo pubblico. I membri del sito possono partecipare al gruppo e pubblicare senza entrare esplicitamente nel gruppo. Il valore predefinito è selezionato.

* **Iscrizione obbligatoria**

   Se selezionato, il gruppo community è un gruppo aperto. I membri del sito della community possono visualizzare i contenuti del gruppo, ma devono unirsi al gruppo per pubblicare contenuti. I membri si uniscono selezionando `Join` nell’ambiente di pubblicazione. Il valore predefinito non è selezionato.

* **Iscrizione limitata**

   Se selezionato, il gruppo della community è un gruppo segreto. I membri della comunità devono essere invitati esplicitamente. I membri invitati vengono inseriti nella casella di ricerca. I membri possono essere aggiunti successivamente utilizzando [Console Membri e gruppi](/help/communities/members.md) l’ambiente di authoring. Il valore predefinito non è selezionato.

**MINIATURA**

![community-group-thumbnail](assets/community-group-thumbnail.png)

La miniatura è un’immagine da visualizzare per il gruppo all’atto dell’authoring e della pubblicazione.

Le dimensioni ottimali per un&#39;immagine di gruppo sono 170 x 90 pixel in un formato immagine supportato (ad esempio JPG o PNG).

Se non viene aggiunta alcuna immagine, viene visualizzata un’immagine predefinita.

![immagine thumbnail](assets/thumbnail-image.png)

### Passaggio 4: Crea gruppo {#step-create-group}

![community-create-group](assets/community-create-group.png)

Se sono necessarie delle regolazioni, utilizza **Indietro** per farli.

Una volta **Crea** viene selezionato e avviato, il processo di creazione del gruppo non può essere interrotto.

Al termine del processo, la scheda per il nuovo sito della sottocomunità (gruppo) viene visualizzata nella console Gruppi di siti di Communities, da cui gli autori possono aggiungere contenuti di pagina o gli amministratori possono modificare le proprietà del sito.

![crea gruppo community](assets/create-community-groups.png)

>[!NOTE]
>
>Il gruppo viene creato in tutte le lingue, come specificato in [Passaggio 1: Modello Gruppo community](/help/communities/groups.md#step-community-group-template) in Lingue supplementari disponibili per i gruppi della community, nella console Gruppi della community dei rispettivi siti della community.

## Contenuto gruppo autore {#author-group-content}

![open-site](assets/open-site.png)

Il contenuto della pagina di un gruppo può essere creato con gli stessi strumenti di qualsiasi altra pagina AEM. Per aprire il gruppo per l’authoring, selezionate l’icona Apri sito che viene visualizzata quando passate il puntatore del mouse sulla scheda del gruppo.

## Modifica proprietà gruppo {#modify-group-properties}

È possibile modificare le proprietà di un sito della sottocomunità esistente, specificate durante il processo di creazione del gruppo community, selezionando l’icona Modifica sito che viene visualizzata quando si passa il mouse sulla scheda del gruppo:

![sito di modifica](assets/edit-site.png)

I dettagli delle seguenti proprietà corrispondono alle descrizioni fornite nella [Creazione di gruppi](#group-creation) sezione . È possibile modificare qualsiasi gruppo nidificato, creato nell’ambiente di pubblicazione o di authoring.

![community-group-basic](assets/community-group-basic.png)

### Modifica base {#modify-basic}

Il pannello BASIC consente di modificare

* Titolo gruppo community
* Descrizione gruppo community

Impossibile modificare il nome del gruppo comunitario.

La scelta di un diverso modello di gruppo community non avrebbe alcun impatto su un sito di gruppo community esistente, in quanto non rimane alcuna connessione tra modelli e siti.

Invece, [STRUTTURA](#modify-structure) della sottocomunità può essere modificata.

### Modifica struttura {#modify-structure}

Il pannello STRUTTURA consente di modificare la struttura inizialmente creata dal modello di gruppo community selezionato durante la creazione del sito sub-community dall’ambiente di authoring o di pubblicazione. Dal pannello è possibile:

* Trascina e rilascia altri [funzioni della community](/help/communities/functions.md) nella struttura del sito.
* In un&#39;istanza di una funzione comunitaria nella struttura del sito:

   * **`Gear icon`**
Modifica le impostazioni, inclusi il titolo della visualizzazione, l’URL e [gruppi di membri privilegiati](/help/communities/users.md#privilegedmembersgroups).

   * **`Trashcan icon`**
Rimuovere (eliminare) le funzioni dalla struttura del sito.

   * **`Grid icon`**
Modifica l&#39;ordine delle funzioni come visualizzato nella barra di navigazione di livello superiore del sito.

>[!CAUTION]
>
>Anche se il titolo visualizzato può essere modificato senza effetti collaterali, si sconsiglia di modificare il nome URL di una funzione community appartenente a un sito community.
>
>Ad esempio, la ridenominazione dell’URL non comporterà lo spostamento dell’UGC esistente, con l’effetto di perdere l’UGC.

>[!CAUTION]
>
>La funzione gruppi deve *not* essere *primo né unico* nella struttura del sito.
>
>Qualsiasi altra funzione, ad esempio [funzione pagina](/help/communities/functions.md#page-function), deve essere incluso ed elencato per primo.

**Esempio: Aggiunta di una funzione di calendario a una struttura della sottocomunità (gruppo)**

![add-calendar per gruppo community](assets/community-group-add-calendar.png)

### Modifica progettazione {#modify-design}

Il pannello PROGETTAZIONE consente di modificare il tema:

* [Tema gruppo community](#community-group-theme)
* [Marchio gruppo community](#community-group-branding)

   * Scorri fino alla parte inferiore del pannello per modificare l’immagine del marchio.

### Modifica impostazioni {#modify-settings}

Il pannello IMPOSTAZIONI consente di aggiungere community [moderatori](#moderation).

### Modifica appartenenza {#modify-membership}

La [ISCRIZIONE](#membership) pannello è solo informativo. Non è possibile modificare il tipo di appartenenza al gruppo stabilito, sia esso facoltativo, obbligatorio o limitato.

### Modifica miniatura {#modify-thumbnail}

La [MINIATURA](#thumbnail) Il pannello consente di caricare un’immagine per rappresentare il gruppo community ai visitatori del sito nell’ambiente di pubblicazione e nella console Gruppi del sito di Communities nell’ambiente di authoring.

## Pubblicare il gruppo {#publish-the-group}

![sito di pubblicazione](assets/publish-site.png)

Una volta creato o modificato un gruppo di community, è possibile pubblicare (attivare) il gruppo selezionando la `Publish Site` icona.

Dopo la corretta pubblicazione del gruppo, viene visualizzato un messaggio:

![pubblicato in gruppo](assets/group-published.png)

>[!CAUTION]
>
>Il sito della comunità padre e i gruppi padre dovrebbero essere già stati pubblicati.
>
>Il sito community e i gruppi nidificati devono essere pubblicati in modo dall’alto verso il basso.

## Elimina il gruppo {#delete-the-group}

![icona Elimina](assets/deleteicon.png)

Per eliminare un gruppo dalla console Gruppi della community, seleziona l’icona Elimina gruppo , visualizzata quando si passa il mouse sul gruppo.

Questo rimuove tutti gli elementi associati al gruppo, ad esempio tutti i contenuti del gruppo vengono eliminati in modo permanente e le appartenenze utente vengono rimosse dal sistema.
