---
title: Console di gestione membri e gruppi
description: Come accedere alle console di gestione dei membri e dei gruppi
uuid: 2e93e861-a066-4189-91db-f8b784bc5aea
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: ccabf301-b417-48aa-8501-8360fd9f3e36
role: Admin
exl-id: b64e24d2-8407-484c-8216-8d328ef5fa4f
source-git-commit: 201c87da1316944e594ade6d95800326b1e6667c
workflow-type: tm+mt
source-wordcount: '961'
ht-degree: 4%

---


# Console di gestione membri e gruppi {#members-groups-management-consoles}

## Panoramica {#overview}

Le funzioni di AEM Communities spesso richiedono la registrazione e l’accesso dei visitatori del sito prima di poter partecipare a una community nell’ambiente di pubblicazione. La registrazione degli utenti è necessaria solo nell’ambiente di pubblicazione e viene comunemente definita *membri* per distinguerli *utenti* registrati nell’ambiente di authoring.

### Membri (utenti) alla pubblicazione {#members-users-on-publish}

Utilizzo delle console Membri e Gruppi di Communities, membri e gruppi di membri registrati in *pubblicare* l’ambiente può essere creato e gestito dal *autore* ambiente. Ciò è possibile solo quando [servizio tunnel](deploy-communities.md#tunnel-service-on-author) è abilitato.

### Utenti su Autore {#users-on-author}

Per la gestione di utenti e gruppi registrati in *autore* è necessario per utilizzare la console di sicurezza della piattaforma:

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
>Non sarà possibile utilizzare la console Membri se [servizio tunnel](deploy-communities.md#tunnel-service-on-author) non è abilitato.

![La console membro](assets/member-console1.png)

### Ricerca {#search-features}

Seleziona l’icona del pannello laterale a sinistra del `Members` per aprire o disattivare il pannello laterale di ricerca.

![Icona del pannello laterale di ricerca.](assets/leftpanel-icon.png)


![Opzioni filtro per la console membri](assets/member-console2.png)

Selezionare l&#39;icona di ricerca sul lato sinistro del `Members` per far chiudere il pannello laterale di ricerca.

### Statistiche membri {#member-statistics}

Colonne visualizzate `Views`, `Posts`, `Follows` e `Likes` vengono aggiornati quando l’utente è membro di uno o più siti della community con Adobe Analytics [abilitato](sites-console.md#analytics).

### Esporta CSV {#export-csv}

Selezione del `Export CSV` Il collegamento consente di scaricare tutti i membri come elenco di valori separati da virgola, adatti per l&#39;importazione in un foglio di calcolo.

Le intestazioni di colonna sono

`| Screen Name |Last Name |First Name |Status |Views |Posts |Follows |Likes |`

## Crea nuovo membro {#create-new-member}

Seleziona `Create Member` per creare un utente nell’ambiente di pubblicazione.

![Finestra Crea nuovo membro](assets/create-member1.png)

### GENERALE - Dettagli membro {#general-member-details}

La maggior parte dei campi sono campi facoltativi che il membro può compilare in un secondo momento sul proprio profilo.

* **[!UICONTROL ID]**

(*Obbligatorio*) L&#39;ID autorizzabile è l&#39;ID di accesso del membro.
Per impostazione predefinita, l’ID viene impostato sul valore dell’indirizzo e-mail richiesto.
*Una volta creato, l’ID non può essere modificato*.

* **[!UICONTROL Indirizzo e-mail]**

(*Obbligatorio*) Indirizzo e-mail del membro.
L&#39;utente può cambiare il proprio indirizzo e-mail quando aggiorna il profilo.I Se l&#39;ID è quello predefinito, l&#39;ID *non* cambia quando l’indirizzo e-mail viene modificato.

* **[!UICONTROL Password]**

  (*Obbligatorio*) La password di accesso.

* **[!UICONTROL Ripeti password]**

  (*Obbligatorio*) Immettere nuovamente la password per la verifica.

* **[!UICONTROL Aggiungi membro ai siti]**

  (*Facoltativo*) Selezionare un membro dai siti community esistenti per aggiungerlo al gruppo membri del sito community.

* **[!UICONTROL Aggiungi membro a gruppi]**

  (*Facoltativo*) Selezionare un gruppo di membri esistente per aggiungere il membro a tale gruppo.

* Seleziona **[!UICONTROL Salva]**

### GENERALE - Impostazioni account {#general-account-settings}

In Impostazioni account un amministratore della community può effettuare le seguenti operazioni:

* **[!UICONTROL Stato]**
   * Vietato Un membro non è in grado di accedere, impedendogli di visualizzare pagine o partecipare ad attività che richiedono l&#39;accesso. Possono ancora visitare in forma anonima un sito della community aperto.

   * Non vietato Un membro ha pieno accesso al sito della community.

  Il valore predefinito è `Not Banned`.

* **[!UICONTROL Limiti per contributi]**

  Se questa opzione è selezionata, la capacità del membro di pubblicare contenuti è limitata.
Il valore predefinito dipende dalla configurazione dei limiti dei contributi.
Consulta [Limiti contributi membri](limits.md).

* **[!UICONTROL Modifica password]**

  Collegamento presente quando si modifica un membro esistente. Consente a un amministratore di comunità di reimpostare una password per un membro.

### GENERALE - Foto {#general-photo}

Per fornire un avatar al membro, inizia selezionando **[!UICONTROL Carica immagine]** e scegli un&#39;immagine di tipo .jpg, .png, .tif o .gif. Le dimensioni preferite per un&#39;immagine sono 240 x 240 pixel a 72 dpi.

### GENERALE - Aggiungi membro ai siti {#general-add-member-to-sites}

Il membro può essere aggiunto a uno o più gruppi di membri dei siti community. Iniziare immettendo il testo nella casella di testo.

### GENERALE - Aggiungi membro a gruppi {#general-add-member-to-groups}

Il membro può essere aggiunto a uno o più gruppi di membri. Iniziare immettendo il testo nella casella di testo.

### Scheda DISTINTIVI {#badges-tab}

Il `BADGES` Il pannello consente di assegnare manualmente i badge e di revocarli. I distintivi possono essere per i ruoli assegnati e i distintivi generalmente ottenuti.

Vedi anche [Punteggio e distintivi](implementing-scoring.md).

![Finestra Modifica impostazioni appartenenza](assets/create-member2.png)

* **[!UICONTROL Aggiungi badge]**
   * Inizia a digitare per selezionare [badge disponibili](badges.md). Una volta selezionato un badge, scegli ogni sito, o tutti i siti, in cui il badge deve essere visualizzato insieme all’avatar del membro.
   * È possibile scegliere più badge e siti.
* **[!UICONTROL Rimuovere i badge]**
   * Seleziona l’icona cestino accanto a un badge per rimuoverlo.

## Console Gruppi {#groups-console}

La console Gruppi, disponibile nell’ambiente di authoring, consente di creare e gestire i gruppi di membri registrati nell’ambiente di pubblicazione. È particolarmente utile per [Gruppi membri privilegiati](users.md#privilegedmembersgroups).

Per accedere alla console Gruppi:
* Dalla navigazione globale, seleziona **[!UICONTROL Navigazione]** > **[!UICONTROL Community]** > **[!UICONTROL Gruppi]**.

>[!CAUTION]
>
>Non sarà possibile utilizzare la console Gruppi se [servizio tunnel](deploy-communities.md#tunnel-service-on-author) non è abilitato.

### Crea nuovo gruppo {#create-new-group}

Seleziona `Add Group` per creare un gruppo nell’ambiente di pubblicazione.

![Finestra Crea nuovo gruppo](assets/group-console1.png)

I campi obbligatori per la creazione di un nuovo gruppo di membri lato pubblicazione sono:

* **[!UICONTROL ID]**

  (*Obbligatorio*) ID univoco del gruppo.

  *Una volta creato, l’ID non può essere modificato.*

* **[!UICONTROL Nome]**

  (*Facoltativo*) Il nome visualizzato del gruppo.

  Il valore predefinito è l’ID.

* **[!UICONTROL Descrizione]**

  (*Facoltativo*) Descrizione dello scopo e delle autorizzazioni del gruppo.

* **[!UICONTROL Aggiungi membri al gruppo]**

  (*Facoltativo*) Selezionare i membri lato pubblicazione da includere come membri iniziali del gruppo.

* Seleziona **[!UICONTROL Salva]**

## Amministratori autorizzati {#authorized-administrators}

Quando si lavora con i membri nella console dei membri delle community, è necessario accedere come utente con le autorizzazioni appropriate e per l’agente di replica utilizzato da [servizio tunnel](deploy-communities.md#tunnel-service-on-author) per essere configurato correttamente.

Se non è stato eseguito l&#39;accesso come `admin`, quindi l&#39;utente connesso deve essere un membro di `administrators` gruppo di utenti.

Vedi anche [Agenti di replica per l’autore](deploy-communities.md#replication-agents-on-author).
