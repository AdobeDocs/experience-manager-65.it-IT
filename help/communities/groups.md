---
title: Console Gruppi community
seo-title: Console Gruppi community
description: La console Gruppi consente di creare gruppi community
seo-description: La console Gruppi consente di creare gruppi community
uuid: 21e2bde3-7354-4193-bcb3-c672c6342252
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: d381ea40-fe49-4d32-bfad-1379c7a02aba
docset: aem65
pagetitle: Community Groups Console
translation-type: tm+mt
source-git-commit: 807a81045fca19ab83b9d7872684a5f8a9ed70f1
workflow-type: tm+mt
source-wordcount: '1678'
ht-degree: 2%

---


# Console Gruppi community {#community-groups-console}

La console Gruppi consente di creare gruppi di community quando la struttura [di](/help/communities/sites-console.md#step1) modelli di un sito community include la funzione [](/help/communities/functions.md#groups-function)Gruppi.

*  AEM Communities supporta la nidificazione dei gruppi all&#39;interno di altri gruppi. La nidificazione dei gruppi è possibile quando la [struttura del nuovo gruppo](/help/communities/tools-groups.md) contiene la funzione dei gruppi.
* Solo per l’ambiente di authoring, è disponibile una procedura guidata per la creazione di gruppi simile a quella per la creazione di siti.
* Se i membri possono o meno creare gruppi nell&#39;ambiente di pubblicazione, è possibile configurarli quando si aggiunge una funzione Gruppi a una struttura del sito community o di un gruppo community.

Dei tre modelli di gruppo inclusi, solo il `Reference Group` modello include una funzione di gruppo nella sua struttura.

I diversi aspetti dei gruppi comunitari sono:

* **Creazione**: è possibile creare un nuovo gruppo all’istanza di creazione e, facoltativamente, all’istanza di pubblicazione.
* **Controllo**: può essere aperto o segreto.
* **Nidificazione**: può contenere zero o più gruppi.

<!-- This is a 404 on helpx. Please update or remove.
>[!NOTE]
>
>Community groups, created in the publish environment before the [existence of the Community Groups console](/help/communities/version-history.md#featurepack1fp1), will not be listed in the Community Groups console, and thus, are not modifiable using the console.
-->

>[!NOTE]
>
>Questa console Gruppi, accessibile solo dalla console Siti community, non deve essere confusa con la console [](/help/communities/members.md) Gruppi membri per la gestione dei gruppi di membri.
>
>I gruppi di membri sono gruppi di utenti registrati nell’ambiente di pubblicazione a cui si accede dall’ambiente di authoring mediante il servizio [](/help/communities/deploy-communities.md#tunnel-service-on-author)tunnel.

## Creazione gruppo {#group-creation}

Per accedere alla console Gruppi:

* Per l’authoring, effettuate l’accesso con privilegi di amministratore.
* Dalla navigazione globale: **[!UICONTROL Community]** > **[!UICONTROL Siti]**.
* Selezionate una cartella del sito community esistente per aprirla.
* Selezionate un&#39;istanza di un sito community all&#39;interno della cartella.

   * La struttura del sito community deve includere una funzione di gruppo.
   * Queste schermate sono estratte dall’esercitazione Guida introduttiva dopo la [creazione di gruppi al momento della pubblicazione](/help/communities/published-site.md).

   ![create-group](assets/create-group.png)

* Selezionate la cartella **** Gruppi per aprirla.

   Quando vengono aperti, vengono visualizzati tutti i gruppi esistenti, sia quelli creati al momento dell’authoring che quelli creati al momento della pubblicazione.

   Da questa console Gruppi è possibile creare nuovi gruppi.

   ![create-new-group](assets/create-new-group.png)

* Fate clic sul pulsante **Crea gruppo** .

### Passaggio 1: Modello gruppo community {#step-community-group-template}

![Gruppi di community multilingue](assets/multi-lingual-group.png)

* **Titolo gruppo community**

   Titolo visualizzato per il gruppo.
Il titolo viene visualizzato sul sito pubblicato per il gruppo.

* **Descrizione gruppo community**

   Descrizione del gruppo.

* **Directory principale gruppo community**

   Il percorso principale del gruppo.
La radice predefinita è il sito principale principale, ma può essere spostata in qualsiasi posizione all&#39;interno del sito Web. Non è consigliato modificarlo.

* **Menu Lingue aggiuntive per gruppi community** disponibili

   Utilizzate il menu a discesa per selezionare le lingue del gruppo di community disponibili. Nel menu vengono visualizzate tutte le lingue in cui viene creato il sito community principale. Gli utenti possono selezionare una di queste lingue per creare gruppi in più lingue in questo singolo passaggio. Lo stesso gruppo viene creato in più lingue specificate nella console Gruppi dei rispettivi siti della community.

* **Nome gruppo community**

   Nome della pagina principale del gruppo che viene visualizzata nell’URL.

   * Controllate il nome perché non può essere facilmente modificato dopo la creazione del gruppo.
   * L&#39;URL di base verrà visualizzato sotto il `Community Group Name`.
   * Per un URL valido, aggiungi &quot;.html&quot;
      *ad esempio*, `https://localhost:4502/content/sites/mysight/en/mygroup.html`.

* **Menu Modello** gruppo community

   Utilizzate il menu a discesa per scegliere un modello [di gruppo di](/help/communities/tools.md)community disponibile.

### Passaggio 2: Progettazione {#step-design}

### COMMUNITY GROUP THEME {#community-group-theme}

![communityGroup](assets/communitygrouptheme.png)

Il framework utilizza l’Bootstrap [](https://twitterbootstrap.org/) Twitter per fornire al sito un design reattivo e flessibile. È possibile selezionare uno dei numerosi temi di Bootstrap precaricati per definire lo stile del modello di gruppo di community selezionato oppure caricare un tema di Bootstrap.

Quando è selezionato, il tema sarà sovrapposto con un segno di spunta blu opaco.

È possibile selezionare un tema diverso dal tema del sito padre.

Dopo la pubblicazione del sito community, è possibile [modificare le proprietà](#modifyinggroupproperties) e selezionare un tema diverso.

### COMMUNITY GROUP BRANDING {#community-group-branding}

![marchio di gruppo](assets/community-group-branding.png)

Il marchio Community del sito è un&#39;immagine visualizzata come intestazione nella parte superiore di ogni pagina. È possibile visualizzare un banner per il gruppo che differisce dalle altre pagine del sito.

Le dimensioni dell’immagine devono corrispondere alla larghezza prevista per la visualizzazione della pagina nel browser e a 120 pixel in altezza.

Quando create o selezionate un’immagine, tenete presente:

* L’altezza dell’immagine viene ritagliata a 120 pixel, misurati dal bordo superiore dell’immagine
* L&#39;immagine viene bloccata sul bordo sinistro della finestra del browser
* L’immagine non viene ridimensionata, pertanto quando la larghezza dell’immagine è:

   * Con una larghezza inferiore a quella del browser, l&#39;immagine viene ripetuta in orizzontale.
   * Maggiore della larghezza del browser, l&#39;immagine apparentemente verrà ritagliata.

### Passaggio 3: Impostazioni {#step-settings}

**MODERAZIONE**

![selezionare i ruoli dei membri del gruppo community](assets/group-admin.png)

**Moderatori gruppo community**

Per impostazione predefinita, l&#39;elenco di moderatori del sito community principale è ereditato.

È possibile aggiungere moderatori specifici al gruppo. Cercare membri (dall’ambiente di pubblicazione) per aggiungerli come moderatori

**Amministratori gruppo**

Per impostazione predefinita, anche l&#39;amministratore del sito community principale è l&#39;amministratore per i gruppi.

Tuttavia, è possibile assegnare amministratori di gruppi indipendenti. Gli amministratori del gruppo possono gestire il proprio gruppo (ad esempio G1) e creare un sottogruppo nidificato sotto G1. Possono inoltre assegnare diversi amministratori per il sottogruppo.

Un utente U1 può quindi essere un amministratore in un gruppo G1 e un utente regolare nel suo gruppo nidificato G2.

**APPARTENENZA**

L&#39;impostazione di appartenenza consente di selezionare uno dei tre modi per proteggere un gruppo community.

![appartenenza a un gruppo](assets/community-group-membership.png)

* **Iscrizione opzionale**

   Se selezionato, il gruppo community è un gruppo pubblico. I membri del sito possono partecipare al gruppo e pubblicare post senza entrare esplicitamente nel gruppo. Il valore predefinito è selezionato.

* **Iscrizione obbligatoria**

   Se selezionato, il gruppo community è un gruppo aperto. I membri del sito della community possono visualizzare il contenuto del gruppo, ma devono unirsi al gruppo per pubblicare contenuti. I membri si uniscono selezionando il `Join` pulsante nell’ambiente di pubblicazione. Il valore predefinito non è selezionato.

* **Iscrizione limitata**

   Se selezionato, il gruppo community è un gruppo segreto. I membri della community devono essere invitati esplicitamente. I membri invitati vengono inseriti nella casella di ricerca. I membri possono essere aggiunti in seguito utilizzando le console [Membri e Gruppi](/help/communities/members.md) nell’ambiente di authoring. Il valore predefinito non è selezionato.

**MINIATURA**

![community-group-thumbnail](assets/community-group-thumbnail.png)

La miniatura è un’immagine da visualizzare per il gruppo al momento dell’authoring e della pubblicazione.

Le dimensioni ottimali per un’immagine di gruppo sono 170 x 90 pixel in un formato immagine supportato (ad esempio, JPG o PNG).

Se non viene aggiunta alcuna immagine, viene visualizzata un&#39;immagine predefinita.

![miniatura](assets/thumbnail-image.png)

### Passaggio 4: Crea gruppo {#step-create-group}

![community-create-group](assets/community-create-group.png)

Se sono necessarie delle regolazioni, fate clic sul pulsante **Indietro** .

Dopo aver selezionato e avviato **Crea** , il processo di creazione del gruppo non può essere interrotto.

Al termine del processo, la scheda per il nuovo sito della community secondaria (gruppo) viene visualizzata nella console Gruppi siti community, da cui gli autori possono aggiungere contenuti di pagina o gli amministratori possono modificare le proprietà del sito.

![crea gruppo community](assets/create-community-groups.png)

>[!NOTE]
>
>Il gruppo viene creato in tutte le lingue, come specificato nel [Passaggio 1: Modello](/help/communities/groups.md#step-community-group-template) Gruppo community in ulteriori lingue del gruppo community disponibili, nella console Gruppi community dei rispettivi siti community.

## Contenuto gruppo autore {#author-group-content}

![open-site](assets/open-site.png)

Il contenuto della pagina di un gruppo può essere creato con gli stessi strumenti di qualsiasi altra pagina AEM. Per aprire il gruppo per la creazione, selezionate l&#39;icona Apri sito che viene visualizzata quando passate il puntatore del mouse sulla scheda del gruppo.

## Modifica proprietà gruppo {#modify-group-properties}

Le proprietà di un sito sub-community esistente, specificate durante il processo di creazione del gruppo community, possono essere modificate selezionando l&#39;icona Modifica sito che viene visualizzata quando si passa il puntatore sulla scheda del gruppo:

![edit-site](assets/edit-site.png)

I dettagli delle seguenti proprietà corrispondono alle descrizioni fornite nella sezione Creazione [](#group-creation) gruppo. È possibile modificare qualsiasi gruppo nidificato, creato nell’ambiente di pubblicazione o di creazione.

![community-group-basic](assets/community-group-basic.png)

### Modifica base {#modify-basic}

Il pannello BASIC consente di modificare

* Titolo gruppo community
* Descrizione gruppo community

Impossibile modificare il nome del gruppo community.

La scelta di un diverso modello di gruppo community non avrebbe alcun effetto su un sito di gruppo community esistente, in quanto non rimane alcuna connessione tra i modelli e i siti.

Al contrario, la [STRUTTURA](#modify-structure) della sub-comunità può essere modificata.

### Modifica struttura {#modify-structure}

Il pannello STRUTTURA consente di modificare la struttura creata inizialmente dal modello di gruppo community selezionato al momento della creazione del sito della sottocomunità dall’ambiente di creazione o pubblicazione. Dal pannello è possibile:

* Trascinare ulteriori funzioni [della](/help/communities/functions.md) community nella struttura del sito.
* In un&#39;istanza di una funzione community nella struttura del sito:

   * **`Gear icon`**
Modificate le impostazioni, inclusi il titolo di visualizzazione, l&#39;URL e i gruppi [di membri](/help/communities/users.md#privilegedmembersgroups)privilegiati.

   * **`Trashcan icon`**
Rimuovere (eliminare) le funzioni dalla struttura del sito.

   * **`Grid icon`**
Modificate l&#39;ordine delle funzioni come visualizzate nella barra di navigazione di livello superiore del sito.

>[!CAUTION]
>
>Anche se il titolo visualizzato può essere modificato senza effetti collaterali, si consiglia di non modificare il nome URL di una funzione community appartenente a un sito community.
>
>Ad esempio, la ridenominazione dell’URL non comporterà lo spostamento dell’UGC esistente, con l’effetto di perdere l’UGC.

>[!CAUTION]
>
>La funzione group *non* deve essere la *prima né l&#39;unica* funzione nella struttura del sito.
>
>Qualsiasi altra funzione, come la funzione [](/help/communities/functions.md#page-function)page, deve essere inclusa ed elencata per prima.

**Esempio: Aggiunta di una funzione di calendario a una struttura di sottocomunità (gruppo)**

![community-group-add-Calendar](assets/community-group-add-calendar.png)

### Modifica struttura {#modify-design}

Il pannello PROGETTAZIONE consente di modificare il tema:

* [Tema gruppo community](#community-group-theme)
* [Marchio gruppo community](#community-group-branding)

   * Scorrete fino in fondo al pannello per cambiare l’immagine del marchio.

### Modifica impostazioni {#modify-settings}

Il pannello IMPOSTAZIONI consente di aggiungere [moderatori](#moderation)della community.

### Modifica appartenenza {#modify-membership}

Il pannello [MEMBERSHIP](#membership) è solo informativo. Non è possibile modificare il tipo di appartenenza al gruppo stabilito, sia essa facoltativa, obbligatoria o limitata.

### Modifica miniatura {#modify-thumbnail}

Il pannello [THUMBNAIL](#thumbnail) consente di caricare un’immagine per rappresentare il gruppo community ai visitatori del sito nell’ambiente di pubblicazione e nella console Gruppi del sito delle community nell’ambiente di authoring.

## Pubblicare il gruppo {#publish-the-group}

![sito di pubblicazione](assets/publish-site.png)

Dopo che un gruppo di community è stato creato o modificato di recente, è possibile pubblicare (attivare) il gruppo selezionando l’ `Publish Site` icona .

Dopo che il gruppo è stato pubblicato correttamente, viene visualizzato un messaggio:

![pubblicato in gruppo](assets/group-published.png)

>[!CAUTION]
>
>Il sito della comunità padre e i gruppi padre dovrebbero essere già stati pubblicati.
>
>Il sito della community e i gruppi nidificati devono essere pubblicati in modo top-down.

## Eliminare il gruppo {#delete-the-group}

![icona delete](assets/deleteicon.png)

Per eliminare un gruppo dalla console Gruppi della community, fate clic sull’icona Elimina gruppo, visualizzata quando si passa il mouse sul gruppo.

Questo rimuove tutti gli elementi associati al gruppo, ad esempio tutto il contenuto del gruppo viene eliminato definitivamente e le appartenenze utente vengono rimosse dal sistema.
