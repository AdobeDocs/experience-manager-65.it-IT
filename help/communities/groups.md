---
title: Console Gruppi per community
description: Scopri la console Gruppi community, che consente di creare gruppi community quando la struttura di modelli di un sito community include la funzione gruppi.
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
docset: aem65
pagetitle: Community Groups Console
role: Admin
exl-id: ef371ff8-6b4f-4e5a-98fb-d7c274927c46
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1698'
ht-degree: 1%

---

# Console Gruppi per community {#community-groups-console}

La console Gruppi consente di creare gruppi community quando la [struttura modello](/help/communities/sites-console.md#step1) di un sito community include la funzione [gruppi](/help/communities/functions.md#groups-function).

* AEM Communities supporta la nidificazione di gruppi all’interno di altri gruppi. La nidificazione dei gruppi è possibile quando la struttura [ del nuovo gruppo](/help/communities/tools-groups.md) contiene la funzione dei gruppi.
* Solo per l’ambiente di authoring, è disponibile una procedura guidata per la creazione di gruppi simile alla procedura guidata per la creazione di siti.
* Se i membri possono o meno creare gruppi nell&#39;ambiente di pubblicazione, è possibile configurarlo quando si aggiunge una funzione Gruppi a una struttura del sito o del gruppo di community.

Dei tre modelli di gruppo inclusi, solo il modello `Reference Group` include una funzione di gruppo nella struttura.

I diversi aspetti dei gruppi comunitari sono:

* **Creazione**: è possibile creare un nuovo gruppo nell&#39;istanza di authoring e, facoltativamente, nell&#39;istanza di pubblicazione.
* **Controllo**: il gruppo può essere aperto o segreto.
* **Nidificazione**: il gruppo può contenere zero o più gruppi.

<!-- This is a 404 on helpx. Update or remove.
>[!NOTE]
>
>Community groups, created in the publish environment before the [existence of the Community Groups console](/help/communities/version-history.md#featurepack1fp1), is not listed in the Community Groups console, and thus, are not modifiable using the console.
-->

>[!NOTE]
>
>Questa console Gruppi, accessibile solo dalla console dei siti di Communities, non deve essere confusa con il membro [Console Gruppi](/help/communities/members.md) per la gestione dei gruppi di membri.
>
>I gruppi di membri sono gruppi di utenti registrati nell&#39;ambiente di pubblicazione e a cui si accede dall&#39;ambiente di authoring utilizzando il [servizio tunnel](/help/communities/deploy-communities.md#tunnel-service-on-author).

## Creazione gruppo {#group-creation}

Per accedere alla console Gruppi:

* In modalità Autore, accedi con privilegi di amministratore.
* Dalla navigazione globale: **[!UICONTROL Communities]** > **[!UICONTROL Sites]**.
* Selezionare una cartella del sito community esistente per aprirla.
* Selezionare un&#39;istanza di un sito community all&#39;interno della cartella.

   * La struttura del sito community deve includere una funzione di gruppo.
   * Queste schermate provengono dall&#39;esercitazione introduttiva dopo [la creazione di gruppi durante la pubblicazione](/help/communities/published-site.md).

  ![crea-gruppo](assets/create-group.png)

* Seleziona la cartella **Groups** per aprirla.

  All’apertura, vengono visualizzati tutti i gruppi esistenti, siano essi creati in Author o Publish.

  Da questa console Gruppi è possibile creare nuovi gruppi.

  ![create-new-group](assets/create-new-group.png)

* Selezionare il pulsante **Crea gruppo**.

### Passaggio 1: modello per gruppo community {#step-community-group-template}

![Gruppi community multilingue](assets/multi-lingual-group.png)

* **Titolo gruppo community**

  Titolo da visualizzare per il gruppo.
Il titolo del gruppo viene visualizzato nel sito pubblicato.

* **Descrizione gruppo community**

  Descrizione del gruppo.

* **Directory principale gruppo community**

  Percorso della directory principale del gruppo.
La directory principale predefinita è il sito padre, ma la directory principale può essere spostata in qualsiasi posizione all’interno del sito web. Non è consigliabile modificarlo.

* **Menu Lingue aggiuntive gruppo community disponibili**

  Utilizzare il menu a discesa per selezionare le lingue disponibili per i gruppi community. Il menu visualizza tutte le lingue in cui viene creato il sito community principale. Gli utenti possono scegliere tra queste lingue per creare gruppi in più lingue in questo singolo passaggio. Lo stesso gruppo viene creato in più lingue specificate nella console Gruppi dei rispettivi siti community.

* **Nome gruppo community**

  Il nome della pagina principale del gruppo che viene visualizzata nell&#39;URL. Evita di usare caratteri di sottolineatura (_) e parole chiave come risorse e configurazione nel nome del gruppo.

   * Ricontrollare il nome in quanto non può essere modificato facilmente dopo la creazione del gruppo.
   * L&#39;URL di base viene visualizzato sotto `Community Group Name`.
   * Per un URL valido, aggiungi &quot;.html&quot;
     *ad esempio*, `https://localhost:4502/content/sites/mysight/en/mygroup.html`.

* Menu **Modello per gruppo community**

  Utilizzare l&#39;elenco a discesa per scegliere un [modello di gruppo community](/help/communities/tools.md) disponibile.

### Passaggio 2: Progettazione {#step-design}

### TEMA GRUPPO COMMUNITY {#community-group-theme}

![communitygrouptheme](assets/communitygrouptheme.png)

Il framework utilizza `Twitter Bootstrap` per portare una progettazione reattiva e flessibile al sito. È possibile selezionare uno dei numerosi temi di Bootstrap precaricati per assegnare uno stile al modello di gruppo community selezionato oppure caricare un tema di Bootstrap.

Se questa opzione è selezionata, il tema viene sovrapposto con un segno di spunta blu opaco.

È possibile selezionare un tema diverso da quello del sito principale.

Dopo la pubblicazione del sito community, è possibile [modificare le proprietà](#modifyinggroupproperties) e selezionare un tema diverso.

### MARCHIO PER GRUPPO COMMUNITY {#community-group-branding}

![community-group-branding](assets/community-group-branding.png)

Il branding del sito community è un’immagine visualizzata come intestazione nella parte superiore di ogni pagina. È possibile visualizzare un banner per il gruppo diverso da altre pagine del sito.

L’immagine deve essere ridimensionata in modo da avere la larghezza prevista per la pagina nel browser e un’altezza di 120 pixel.

Quando crei o selezioni un’immagine, tieni presente quanto segue:

* L&#39;altezza dell&#39;immagine viene ritagliata a 120 pixel misurati dal bordo superiore dell&#39;immagine
* L&#39;immagine è bloccata sul bordo sinistro della finestra del browser
* Non esiste alcun ridimensionamento dell’immagine, tale che quando la larghezza dell’immagine è:

   * Inferiore alla larghezza del browser, l’immagine viene ripetuta orizzontalmente.
   * Maggiore della larghezza del browser, l&#39;immagine appare ritagliata.

### Passaggio 3: Impostazioni {#step-settings}

**MODERAZIONE**

![seleziona ruoli membri del gruppo community](assets/group-admin.png)

**Moderatori gruppo community**

Per impostazione predefinita, viene ereditato l&#39;elenco di moderatori del sito della community principale.

È possibile aggiungere moderatori specifici al gruppo. Cerca membri (dall’ambiente di pubblicazione) per aggiungerli come moderatori

**Amministratori di gruppi**

Per impostazione predefinita, l&#39;amministratore del sito della community padre è anche l&#39;amministratore dei gruppi.

Tuttavia, è possibile assegnare amministratori di gruppi indipendenti. Gli amministratori di gruppi possono gestire il proprio gruppo (ad esempio, G1) e creare un sottogruppo nidificato in G1. Possono inoltre assegnare amministratori diversi per il sottogruppo.

Un utente U1 può quindi essere un amministratore in un gruppo G1 e un utente normale nel suo gruppo nidificato G2.

**APPARTENENZA**

L&#39;impostazione di appartenenza consente di selezionare uno dei tre modi per proteggere un gruppo community.

![appartenenza a gruppi community](assets/community-group-membership.png)

* **Iscrizione facoltativa**

  Se viene selezionato, il gruppo community è un gruppo pubblico. I membri del sito possono partecipare al gruppo e pubblicare i post senza partecipare esplicitamente al gruppo. L&#39;opzione Predefinita è selezionata.

* **Iscrizione richiesta**

  Se viene selezionato, il gruppo community è un gruppo aperto. I membri del sito della community possono visualizzare il contenuto del gruppo, ma devono unirsi al gruppo per pubblicare il contenuto. I membri partecipano selezionando il pulsante `Join` nell&#39;ambiente di pubblicazione. Impostazione predefinita non selezionata.

* **Iscrizione limitata**

  Se viene selezionato, il gruppo community è un gruppo segreto. I membri della community devono essere invitati esplicitamente. I membri invitati vengono inseriti nella casella di ricerca. I membri possono essere aggiunti in un secondo momento utilizzando le [console Membri e Gruppi](/help/communities/members.md) dell&#39;ambiente di authoring. Impostazione predefinita non selezionata.

**MINIATURA**

![miniatura-gruppo-community](assets/community-group-thumbnail.png)

La miniatura è un’immagine da visualizzare per il gruppo durante l’authoring e la pubblicazione.

Le dimensioni ottimali di un&#39;immagine di gruppo sono 170 x 90 pixel in un formato di immagine supportato (come JPG-o PNG).

Se non viene aggiunta alcuna immagine, viene visualizzata un&#39;immagine predefinita.

![immagine-miniatura](assets/thumbnail-image.png)

### Passaggio 4: creare un gruppo {#step-create-group}

![community-create-group](assets/community-create-group.png)

Se sono necessarie modifiche, usare il pulsante **Indietro** per apportare le modifiche.

Dopo aver selezionato e avviato **Crea**, il processo di creazione del gruppo non può essere interrotto.

Al termine del processo, la scheda per il nuovo sito (gruppo) della sottocommunity viene visualizzata nella console Gruppi di siti community, da cui gli autori possono aggiungere il contenuto della pagina oppure gli amministratori possono modificare le proprietà del sito.

![crea gruppo community](assets/create-community-groups.png)

>[!NOTE]
>
>Il gruppo viene creato in tutte le lingue, come specificato in [Passaggio 1: modello gruppo community](/help/communities/groups.md#step-community-group-template) in lingue aggiuntive gruppo community disponibili, nella console Gruppi community dei rispettivi siti community.

## Contenuto gruppo di authoring {#author-group-content}

![sito aperto](assets/open-site.png)

Il contenuto della pagina di un gruppo può essere creato con gli stessi strumenti di qualsiasi altra pagina dell’AEM. Per aprire il gruppo per la creazione, seleziona l’icona Apri sito che viene visualizzata quando passi il puntatore sulla scheda del gruppo.

## Modifica proprietà gruppo {#modify-group-properties}

Le proprietà di un sito di una comunità secondaria esistente, specificate durante il processo di creazione del gruppo di comunità, possono essere modificate selezionando l&#39;icona Modifica sito che viene visualizzata quando si passa il puntatore sulla scheda del gruppo:

![modifica-sito](assets/edit-site.png)

I dettagli delle seguenti proprietà corrispondono alle descrizioni fornite nella sezione [Creazione gruppo](#group-creation). Qualsiasi gruppo nidificato può essere modificato, sia che venga creato nell’ambiente di pubblicazione che in quello di authoring.

![community-group-basic](assets/community-group-basic.png)

### Modifica di base {#modify-basic}

Il pannello BASIC consente di modificare

* Titolo gruppo community
* Descrizione gruppo community

Il nome del gruppo community non può essere modificato.

La scelta di un modello di gruppo community diverso non avrà alcun effetto su un sito di gruppo community esistente, poiché non rimane alcuna connessione tra modelli e siti.

È invece possibile modificare la [STRUTTURA](#modify-structure) della sottocommunity.

### Modifica struttura {#modify-structure}

Il pannello STRUTTURA consente di modificare la struttura inizialmente creata dal modello di gruppo community selezionato durante la creazione del sito della sottocommunity dall’ambiente di authoring o di pubblicazione. Dal pannello, è possibile:

* Trascinare altre [funzioni community](/help/communities/functions.md) nella struttura del sito.
* In un’istanza di una funzione community nella struttura del sito:

   * **`Gear icon`**
Modificare le impostazioni, inclusi il titolo di visualizzazione, l&#39;URL e [i gruppi di membri con privilegi](/help/communities/users.md#privilegedmembersgroups).

   * **`Trashcan icon`**
Rimuovere (eliminare) le funzioni dalla struttura del sito.

   * **`Grid icon`**
Consente di modificare l&#39;ordine delle funzioni visualizzato nella barra di spostamento di primo livello del sito.

>[!CAUTION]
>
>Anche se il titolo visualizzato può essere modificato senza effetti collaterali, si sconsiglia di modificare il nome URL di una funzione community appartenente a un sito community.
>
>Ad esempio, la ridenominazione dell’URL non sposta l’UGC esistente, pertanto ha l’effetto di &quot;perdere&quot; l’UGC.

>[!CAUTION]
>
>La funzione dei gruppi deve *non* essere la *prima o l&#39;unica* funzione nella struttura del sito.
>
>Qualsiasi altra funzione, ad esempio la funzione [page](/help/communities/functions.md#page-function), deve essere inclusa ed elencata per prima.

**Esempio: aggiunta di una funzione di calendario a una struttura di sottocomunità (gruppo)**

![community-group-add-calendar](assets/community-group-add-calendar.png)

### Modifica progettazione {#modify-design}

Il pannello DESIGN consente di modificare il tema:

* [Tema gruppo community](#community-group-theme)
* [Marchio gruppo community](#community-group-branding)

   * Scorri fino alla parte inferiore del pannello per modificare l’immagine del brand.

### Modifica impostazioni {#modify-settings}

Il pannello IMPOSTAZIONI consente di aggiungere [moderatori](#moderation) della community.

### Modifica appartenenza {#modify-membership}

Il pannello [APPARTENENZA](#membership) è puramente informativo. Non è possibile modificare il tipo di appartenenza al gruppo stabilito, sia esso facoltativo, obbligatorio o limitato.

### Modifica miniatura {#modify-thumbnail}

Il pannello [THUMBNAIL](#thumbnail) consente di caricare un&#39;immagine per rappresentare il gruppo community nei visitatori del sito nell&#39;ambiente Publish e nella console Gruppi del sito community nell&#39;ambiente di authoring.

## Publish il gruppo {#publish-the-group}

![sito di pubblicazione](assets/publish-site.png)

Dopo aver creato o modificato un gruppo community, è possibile pubblicarlo (attivarlo) selezionando l&#39;icona `Publish Site`.

Dopo la pubblicazione del gruppo, viene visualizzato il seguente messaggio:

![gruppo-pubblicato](assets/group-published.png)

>[!CAUTION]
>
>Il sito della community padre e i gruppi padre avrebbero dovuto essere già stati pubblicati.
>
>Il sito community e i gruppi nidificati devono essere pubblicati in modalità top-down.

## Elimina il gruppo {#delete-the-group}

![icona Elimina](assets/deleteicon.png)

Per eliminare un gruppo dalla console Gruppi della community, fai clic sull’icona Elimina gruppo, visualizzata quando si passa il puntatore del mouse sul gruppo.

In questo modo vengono rimossi tutti gli elementi associati al gruppo, ad esempio tutto il contenuto del gruppo viene eliminato in modo permanente e le appartenenze utente vengono rimosse dal sistema.
