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
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# Console Gruppi community{#community-groups-console}

La console Gruppi consente di creare gruppi di community quando la struttura [di](/help/communities/sites-console.md#step1) modelli di un sito community include la funzione [](/help/communities/functions.md#groups-function)Gruppi.

* AEM Communities supporta la nidificazione di gruppi all&#39;interno di altri gruppi. La nidificazione dei gruppi è possibile quando la [struttura del nuovo gruppo](/help/communities/tools-groups.md) contiene la funzione dei gruppi.
* Solo per l’ambiente di authoring, esiste una procedura guidata per la creazione di gruppi simile a quella per la creazione di siti.
* Se i membri possono o meno creare gruppi nell&#39;ambiente di pubblicazione, è possibile configurarli quando si aggiunge una funzione Gruppi a una struttura del sito community o di un gruppo community.

Dei tre modelli di gruppo inclusi, solo il `Reference Group` modello include una funzione di gruppo nella sua struttura.

I diversi aspetti dei gruppi comunitari sono:

* **Creazione**: è possibile creare un nuovo gruppo all’autore ed eventualmente alla pubblicazione
* **Controllo**: il gruppo può essere aperto o segreto
* **Nidificazione**: un gruppo può contenere zero o più gruppi

<!-- This is a 404 on helpx. Please update or remove.
>[!NOTE]
>
>Community groups, created in the publish environment before the [existence of the Community Groups console](/help/communities/version-history.md#featurepack1fp1), will not be listed in the Community Groups console, and thus, are not modifiable using the console.-->

>[!NOTE]
>
>Questa console Gruppi, accessibile solo dalla console Siti community, non deve essere confusa con la console [](/help/communities/members.md) Gruppi membri per la gestione dei gruppi di membri.
>
>I gruppi di membri sono gruppi di utenti registrati nell’ambiente di pubblicazione a cui si accede dall’ambiente di authoring mediante il servizio [](/help/communities/deploy-communities.md#tunnel-service-on-author)tunnel.

## Creazione gruppo {#group-creation}

Per accedere alla console Gruppi:

* Al momento dell&#39;authoring, effettuate l&#39;accesso con privilegi di amministratore
* Dalla navigazione globale: **Community, Siti**
* Selezionate una cartella del sito community esistente per aprirla
* Selezionare un&#39;istanza di un sito community all&#39;interno della cartella

   * la struttura del sito comunitario deve comprendere una funzione di gruppo
   * queste schermate sono estratte dall’esercitazione Guida introduttiva dopo la [creazione di gruppi al momento della pubblicazione](/help/communities/published-site.md)

Selezionate la cartella **** Gruppi per aprirla.

Quando vengono aperti, vengono visualizzati tutti i gruppi esistenti, sia quelli creati al momento dell’authoring che quelli creati al momento della pubblicazione.

Da questa console Gruppi è possibile creare nuovi gruppi.

![chlimage_1-200](assets/chlimage_1-200.png)

* Fate clic sul pulsante **Crea gruppo** .

### Passaggio 1: Modello gruppo community {#step-community-group-template}

![Gruppi di community multilingue](assets/multi-lingual-group.png)

* **Titolo**gruppo community: un titolo di visualizzazione per il gruppo.
Il titolo viene visualizzato sul sito pubblicato per il gruppo.

* **Descrizione** gruppo community: una descrizione del gruppo.
* **Radice**gruppo community: il percorso principale del gruppo.
La radice predefinita è il sito principale principale, ma può essere spostata in qualsiasi posizione all&#39;interno del sito Web. Non è consigliato modificarlo.

* ****Lingue aggiuntive disponibili per il gruppo community** menu: **utilizzare il menu a discesa per selezionare le lingue del gruppo community disponibili. Nel menu vengono visualizzate tutte le lingue in cui viene creato il sito community principale. Gli utenti possono selezionare una di queste lingue per creare gruppi in più lingue in questo singolo passaggio. Lo stesso gruppo viene creato in più lingue specificate nella console Gruppi dei rispettivi siti della community.

* **Nome** gruppo community: il nome della pagina principale del gruppo che viene visualizzata nell’URL

   * controllate il nome perché non viene facilmente modificato dopo la creazione del gruppo
   * l&#39;URL di base verrà visualizzato sotto la `Community Group Name`
   * per un URL valido, aggiungi &quot;.html&quot;
      *ad esempio*, `https://localhost:4502/content/sites/mysight/en/mygroup.html`

* **Menu Modello** gruppo community: utilizzate il menu a discesa per scegliere un modello [di gruppo di](/help/communities/tools.md)community disponibile.

### Passaggio 2: Progettazione {#step-design}

#### COMMUNITY GROUP THEME {#community-group-theme}

Il framework utilizza [Twitter Bootstrap](https://twitterbootstrap.org/) per fornire al sito un design reattivo e flessibile. È possibile selezionare uno dei numerosi temi Bootstrap precaricati per definire lo stile del modello di gruppo di community selezionato oppure caricare un tema Bootstrap.

Quando è selezionato, il tema sarà sovrapposto con un segno di spunta blu opaco.

È possibile selezionare un tema diverso dal tema del sito padre.

Dopo la pubblicazione del sito community, è possibile [modificare le proprietà](#modifyinggroupproperties) e selezionare un tema diverso.

#### COMMUNITY GROUP BRANDING {#community-group-branding}

![chlimage_1-201](assets/chlimage_1-201.png)

Il marchio Community del sito è un&#39;immagine visualizzata come intestazione nella parte superiore di ogni pagina. È possibile visualizzare un banner per il gruppo che differisce dalle altre pagine del sito.

Le dimensioni dell’immagine devono corrispondere alla larghezza prevista per la visualizzazione della pagina nel browser e a 120 pixel in altezza.

Quando create o selezionate un’immagine, tenete presente:

* L’altezza dell’immagine viene ritagliata a 120 pixel, misurati dal bordo superiore dell’immagine
* L&#39;immagine viene bloccata sul bordo sinistro della finestra del browser
* L’immagine non viene ridimensionata, pertanto quando la larghezza dell’immagine è:

   * con una larghezza inferiore a quella del browser, l&#39;immagine viene ripetuta in orizzontale
   * maggiore della larghezza del browser, l&#39;immagine apparirà ritagliata

### Passaggio 3:Impostazioni {#step-settings}

#### MODERATION {#moderation}

![selezionare i ruoli dei membri del gruppo community](assets/group-admin.png)

**Moderatori gruppo community**

Per impostazione predefinita, l&#39;elenco di moderatori del sito community principale è ereditato.

È possibile aggiungere moderatori specifici al gruppo. Cercare membri (dall’ambiente di pubblicazione) per aggiungerli come moderatori

**Amministratori gruppo**

Per impostazione predefinita, anche l&#39;amministratore del sito community principale è l&#39;amministratore per i gruppi.

Tuttavia, è possibile assegnare amministratori di gruppi indipendenti. Gli amministratori del gruppo possono gestire il proprio gruppo (ad esempio G1) e creare un sottogruppo nidificato sotto G1. Possono inoltre assegnare diversi amministratori per il sottogruppo.

Un utente U1 può quindi essere un amministratore in un gruppo G1 e un utente regolare nel suo gruppo nidificato G2.

#### MEMBERSHIP {#membership}

L&#39;impostazione di appartenenza consente di selezionare uno dei tre modi per proteggere un gruppo community.

![chlimage_1-202](assets/chlimage_1-202.png)

* **Iscrizione** opzionale Se selezionata, il gruppo community è un gruppo pubblico. I membri del sito possono partecipare al gruppo e pubblicare post senza entrare esplicitamente nel gruppo. Il valore predefinito è selezionato.

* **Iscrizione** obbligatoria Se selezionata, il gruppo di community è un gruppo aperto. I membri della community possono visualizzare il contenuto del gruppo, ma devono unirsi al gruppo per pubblicare contenuti. I membri si uniscono selezionando il `Join` pulsante nell’ambiente di pubblicazione. Il valore predefinito non è selezionato.

* **Appartenenza** limitata Se selezionata, il gruppo community è un gruppo segreto. I membri della community devono essere invitati esplicitamente. I membri invitati vengono inseriti nella casella di ricerca. I membri possono essere aggiunti in seguito utilizzando le console [Membri e Gruppi](/help/communities/members.md) nell’ambiente di authoring. Il valore predefinito non è selezionato.

#### MINIATURA {#thumbnail}

![chlimage_1-203](assets/chlimage_1-203.png)

La miniatura è un’immagine da visualizzare per il gruppo al momento dell’authoring e della pubblicazione.

Le dimensioni ottimali per un’immagine di gruppo sono 170 x 90 pixel in un formato immagine supportato (ad esempio, JPG o PNG).

Se non viene aggiunta alcuna immagine, viene visualizzata un&#39;immagine predefinita.

![chlimage_1-204](assets/chlimage_1-204.png)

### Passaggio 4: Crea gruppo {#step-create-group}

![chlimage_1-206](assets/chlimage_1-205.png)

Se sono necessarie delle regolazioni, utilizzare il tasto **Back **per eseguire tali regolazioni.

Dopo aver selezionato e avviato **Crea** , il processo di creazione del gruppo non può essere interrotto.

Al termine del processo, la scheda per il nuovo sito della community secondaria (gruppo) viene visualizzata nella console Gruppi siti community, da cui gli autori possono aggiungere contenuti di pagina o gli amministratori possono modificare le proprietà del sito.

![crea gruppo community](assets/create-community-groups.png)

>[!NOTE]
>
>Il gruppo viene creato in tutte le lingue, come specificato nel [Passaggio 1: Modello](/help/communities/groups.md#step-community-group-template) Gruppo community in ulteriori lingue del gruppo community disponibili, nella console Gruppi community dei rispettivi siti community.

## Contenuto gruppo autore {#author-group-content}

![chlimage_1-206](assets/chlimage_1-206.png)

Il contenuto di una pagina di un gruppo può essere creato con gli stessi strumenti di qualsiasi altra pagina AEM. Per aprire il gruppo per la creazione, selezionate l&#39;icona Apri sito che viene visualizzata quando passate il puntatore del mouse sulla scheda del gruppo.

## Modifica proprietà gruppo {#modify-group-properties}

Le proprietà di un sito sub-community esistente, specificate durante il processo di creazione del gruppo community, possono essere modificate selezionando l&#39;icona Modifica sito che viene visualizzata quando si passa il puntatore sulla scheda del gruppo:

![chlimage_1-207](assets/chlimage_1-207.png)

I dettagli delle seguenti proprietà corrispondono alle descrizioni fornite nella sezione Creazione [](#group-creation) gruppo. È possibile modificare qualsiasi gruppo nidificato, creato nell’ambiente di pubblicazione o di creazione.

![chlimage_1-208](assets/chlimage_1-208.png)

### Modifica base {#modify-basic}

Il pannello BASIC consente di modificare

* Titolo gruppo community
* Descrizione gruppo community

Impossibile modificare il nome del gruppo community.

La scelta di un diverso modello di gruppo community non avrebbe alcun effetto su un sito di gruppo community esistente, in quanto non rimane alcuna connessione tra i modelli e i siti.

Al contrario, la [STRUTTURA](#modify-structure) della sub-comunità può essere modificata.

### Modifica struttura {#modify-structure}

Il pannello STRUTTURA consente di modificare la struttura creata inizialmente dal modello di gruppo community selezionato al momento della creazione del sito della sottocomunità dall’ambiente di creazione o pubblicazione. Dal pannello è possibile

* Trascinare ulteriori funzioni [della](/help/communities/functions.md) community nella struttura del sito
* In un&#39;istanza di una funzione community nella struttura del sito:

   * **`Gear icon`**
Modificate le impostazioni, inclusi il titolo di visualizzazione e il nome dell&#39;URL*e i gruppi [di membri](/help/communities/users.md#privilegedmembersgroups)privilegiati.

   * **`Trashcan icon`**
Rimuovere (eliminare) funzioni dalla struttura del sito.

   * **`Grid icon`**
Modificate l&#39;ordine delle funzioni come visualizzate nella barra di navigazione di livello superiore del sito.

>[!CAUTION]
>
>* Anche se il titolo del display può essere modificato senza effetti collaterali, non è consigliabile modificare il nome URL di una funzione community appartenente a un sito community.
Ad esempio, la ridenominazione dell’URL non comporterà lo spostamento dell’UGC esistente, con l’effetto di perdere l’UGC.

>[!CAUTION]
La funzione dei gruppi non deve *essere la *prima e l&#39;unica* funzione nella struttura del sito.
Qualsiasi altra funzione, come la funzione [](/help/communities/functions.md#page-function)page, deve essere inclusa ed elencata per prima.

#### Esempio: Aggiunta di una funzione di calendario a una struttura di sottocomunità (gruppo) {#example-adding-a-calendar-function-to-a-sub-community-group-structure}

![chlimage_1-209](assets/chlimage_1-209.png)

### Modifica struttura {#modify-design}

Il pannello PROGETTAZIONE consente di modificare il tema:

* [Tema gruppo community](#community-group-theme)
* [Marchio gruppo community](#community-group-branding)

   * scorrete fino alla parte inferiore del pannello per cambiare l’immagine del marchio

### Modifica impostazioni {#modify-settings}

Il pannello IMPOSTAZIONI consente di aggiungere [moderatori](#moderation)della community.

### Modifica appartenenza {#modify-membership}

Il pannello [MEMBERSHIP](#membership) è solo informativo. Non è possibile modificare il tipo di appartenenza al gruppo stabilito, sia essa facoltativa, obbligatoria o limitata.

### Modifica miniatura {#modify-thumbnail}

Il pannello [THUMBNAIL](#thumbnail) consente di caricare un’immagine per rappresentare il gruppo community ai visitatori del sito nell’ambiente di pubblicazione e nella console Gruppi del sito delle community nell’ambiente di authoring.

## Pubblicare il gruppo {#publish-the-group}

![chlimage_1-210](assets/chlimage_1-210.png)

Dopo che un gruppo di community è stato creato o modificato di recente, è possibile pubblicare (attivare) il gruppo selezionando l’ `Publish Site` icona .

Dopo che il gruppo è stato pubblicato correttamente, viene visualizzato un messaggio:

![chlimage_1-211](assets/chlimage_1-211.png)

>[!CAUTION]
Il sito della comunità padre e i gruppi padre dovrebbero essere già stati pubblicati.
Il sito della community e i gruppi nidificati devono essere pubblicati in modo top-down.

## Eliminare il gruppo {#delete-the-group}

![icona delete]()

Per eliminare un gruppo dalla console Gruppi della community, fate clic sull’icona Elimina gruppo, visualizzata quando si passa il mouse sul gruppo.

Questo rimuove tutti gli elementi associati al gruppo, ad esempio tutto il contenuto del gruppo viene eliminato definitivamente e le appartenenze utente vengono rimosse dal sistema.
