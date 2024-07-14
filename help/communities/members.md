---
title: Console di gestione membri e gruppi
description: Come accedere alle console di gestione dei membri e dei gruppi
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: b64e24d2-8407-484c-8216-8d328ef5fa4f
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '959'
ht-degree: 1%

---


# Console di gestione membri e gruppi {#members-groups-management-consoles}

## Panoramica {#overview}

Le funzioni di AEM Communities spesso richiedono la registrazione e l’accesso dei visitatori del sito prima di poter partecipare a una community nell’ambiente di pubblicazione. La registrazione degli utenti è necessaria solo nell&#39;ambiente di pubblicazione e viene comunemente indicata come *membri* per distinguerli dagli *utenti* registrati nell&#39;ambiente di authoring.

### Membri (utenti) su Publish {#members-users-on-publish}

Utilizzando le console Membri e Gruppi di Communities, è possibile creare e gestire membri e gruppi di membri registrati nell&#39;ambiente *publish* dall&#39;ambiente *author*. Ciò è possibile solo quando il servizio [tunnel](deploy-communities.md#tunnel-service-on-author) è abilitato.

### Utenti su Autore {#users-on-author}

Per la gestione di utenti e gruppi registrati nell&#39;ambiente *author*, è necessario utilizzare la console di sicurezza della piattaforma:

* Dalla navigazione globale, seleziona **[!UICONTROL Strumenti]** > **[!UICONTROL Sicurezza]** > **[!UICONTROL Utenti]**.
* Dalla navigazione globale, seleziona **[!UICONTROL Strumenti]** > **[!UICONTROL Sicurezza]** > **[!UICONTROL Gruppi]**.

>[!NOTE]
>
>Con il contenuto di esempio distribuito e abilitato, molti utenti di esempio esistono sia nell’ambiente di authoring che in quello di pubblicazione. Questi utenti non saranno presenti quando si esegue con [nosamplecontent runmode](../../help/sites-administering/production-ready.md).

## Console Membri {#members-console}

Nell’ambiente di authoring, per raggiungere la console Membri per la gestione dei membri registrati nell’ambiente di pubblicazione:

* Dalla navigazione globale, seleziona **[!UICONTROL Navigazione]** > **[!UICONTROL Community]** > **[!UICONTROL Membri]**

>[!CAUTION]
>
>Se il servizio [tunnel](deploy-communities.md#tunnel-service-on-author) non è abilitato, non sarà possibile utilizzare la console Membri.

![Console membri](assets/member-console1.png)

### Ricerca {#search-features}

Selezionare l&#39;icona del pannello laterale sul lato sinistro dell&#39;intestazione `Members` per aprire alternativamente il pannello laterale di ricerca.

![Icona pannello laterale di ricerca.](assets/leftpanel-icon.png)


![Opzioni filtro per la console membri](assets/member-console2.png)

Selezionare l&#39;icona di ricerca sul lato sinistro dell&#39;intestazione `Members` per chiudere il pannello laterale di ricerca.

### Statistiche membri {#member-statistics}

Le colonne che visualizzano `Views`, `Posts`, `Follows` e `Likes` vengono aggiornate quando l&#39;utente è membro di uno o più siti della community con Adobe Analytics [abilitato](sites-console.md#analytics).

### Esporta CSV {#export-csv}

La selezione del collegamento `Export CSV` comporta il download di tutti i membri come elenco di valori separati da virgola, adatti per l&#39;importazione in un foglio di calcolo.

Le intestazioni di colonna sono

`| Screen Name |Last Name |First Name |Status |Views |Posts |Follows |Likes |`

## Crea nuovo membro {#create-new-member}

Selezionare `Create Member` per creare un utente nell&#39;ambiente di pubblicazione.

![Finestra Crea nuovo membro](assets/create-member1.png)

### GENERALE - Dettagli membro {#general-member-details}

La maggior parte dei campi sono campi facoltativi che il membro può compilare in un secondo momento sul proprio profilo.

* **[!UICONTROL ID]**

(*Obbligatorio*) L&#39;ID autorizzabile è l&#39;ID di accesso del membro.
Per impostazione predefinita, l’ID viene impostato sul valore dell’indirizzo e-mail richiesto.
*Una volta creato, l&#39;ID non può essere modificato*.

* **[!UICONTROL Indirizzo e-mail]**

(*Obbligatorio*) Indirizzo e-mail del membro.
L&#39;utente può cambiare il proprio indirizzo email durante l&#39;aggiornamento del profilo.I
Se l&#39;ID viene impostato automaticamente sull&#39;indirizzo e-mail, l&#39;ID *non* verrà modificato quando l&#39;indirizzo e-mail verrà modificato.

* **[!UICONTROL Password]**

  (*Obbligatorio*) La password di accesso.

* **[!UICONTROL Password Retype]**

  (*Obbligatorio*) Reimmettere la password per la verifica.

* **[!UICONTROL Aggiungi membro a Sites]**

  (*Facoltativo*) Selezionare uno dei siti community esistenti per aggiungere il membro al gruppo di membri del sito community.

* **[!UICONTROL Aggiungi membro a gruppi]**

  (*Facoltativo*) Selezionare uno dei gruppi di membri esistenti per aggiungere il membro a tale gruppo.

* Seleziona **[!UICONTROL Salva]**

### GENERALE - Impostazioni account {#general-account-settings}

In Impostazioni account un amministratore della community può effettuare le seguenti operazioni:

* **[!UICONTROL Stato]**
   * Vietato
Un membro non è in grado di accedere, impedendo loro di visualizzare le pagine o di partecipare ad attività che richiedono l&#39;accesso. Possono ancora visitare in forma anonima un sito della community aperto.

   * Non vietato
Un membro ha accesso completo al sito community.

  Il valore predefinito è `Not Banned`.

* **[!UICONTROL Limiti contributi]**

  Se questa opzione è selezionata, la capacità del membro di pubblicare contenuti è limitata.
Il valore predefinito dipende dalla configurazione dei limiti dei contributi.
Vedere [Limiti contributi membri](limits.md).

* **[!UICONTROL Cambia password]**

  Collegamento presente quando si modifica un membro esistente. Consente a un amministratore di comunità di reimpostare una password per un membro.

### GENERALE - Foto {#general-photo}

Per fornire un avatar al membro, selezionare **[!UICONTROL Carica immagine]** e scegliere un&#39;immagine di tipo jpg, png, tif o gif. Le dimensioni preferite per un&#39;immagine sono 240 x 240 pixel a 72 dpi.

### GENERALE - Aggiungi membro ai siti {#general-add-member-to-sites}

Il membro può essere aggiunto a uno o più gruppi di membri dei siti community. Iniziare immettendo il testo nella casella di testo.

### GENERALE - Aggiungi membro a gruppi {#general-add-member-to-groups}

Il membro può essere aggiunto a uno o più gruppi di membri. Iniziare immettendo il testo nella casella di testo.

### Scheda DISTINTIVI {#badges-tab}

Il pannello `BADGES` consente di assegnare manualmente i badge e revocarli. I distintivi possono essere per i ruoli assegnati e distintivi generalmente ottenuti.

Vedi anche [Punteggio e distintivi](implementing-scoring.md).

![Finestra Modifica impostazioni appartenenza](assets/create-member2.png)

* **[!UICONTROL Aggiungi badge]**
   * Inizia a digitare per selezionare tra [distintivi disponibili](badges.md). Una volta selezionato un badge, scegli ogni sito, o tutti i siti, in cui il badge deve essere visualizzato insieme all’avatar del membro.
   * È possibile scegliere più badge e siti.
* **[!UICONTROL Rimuovi distintivi]**
   * Seleziona l’icona cestino accanto a un badge per rimuoverlo.

## Console Gruppi {#groups-console}

La console Gruppi, disponibile nell’ambiente di authoring, consente di creare e gestire i gruppi di membri registrati nell’ambiente di pubblicazione. È particolarmente utile per [Gruppi membri con privilegi](users.md#privilegedmembersgroups).

Per accedere alla console Gruppi:
* Dalla navigazione globale, seleziona **[!UICONTROL Navigazione]** > **[!UICONTROL Community]** > **[!UICONTROL Gruppi]**.

>[!CAUTION]
>
>Se il servizio [tunnel](deploy-communities.md#tunnel-service-on-author) non è abilitato, non sarà possibile utilizzare la console Gruppi.

### Crea nuovo gruppo {#create-new-group}

Selezionare `Add Group` per creare un gruppo nell&#39;ambiente di pubblicazione.

![Finestra Crea nuovo gruppo](assets/group-console1.png)

I campi obbligatori per la creazione di un gruppo di membri lato pubblicazione sono:

* **[!UICONTROL ID]**

  (*Obbligatorio*) ID univoco del gruppo.

  *Una volta creato, l&#39;ID non può essere modificato.*

* **[!UICONTROL Nome]**

  (*Facoltativo*) Il nome visualizzato del gruppo.

  Il valore predefinito è l’ID.

* **[!UICONTROL Descrizione]**

  (*Facoltativo*) Descrizione dello scopo e delle autorizzazioni del gruppo.

* **[!UICONTROL Aggiungi Membri Al Gruppo]**

  (*Facoltativo*) Selezionare i membri lato pubblicazione da includere come membri iniziali del gruppo.

* Seleziona **[!UICONTROL Salva]**

## Amministratori autorizzati {#authorized-administrators}

Quando si lavora con i membri nella console dei membri delle community, è necessario accedere come utente con le autorizzazioni appropriate e configurare correttamente l&#39;agente di replica utilizzato dal servizio [tunnel](deploy-communities.md#tunnel-service-on-author).

Se non è stato eseguito l&#39;accesso come `admin`, l&#39;utente connesso deve essere un membro del gruppo di utenti `administrators`.

Vedi anche [Agenti di replica sull&#39;autore](deploy-communities.md#replication-agents-on-author).
