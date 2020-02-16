---
title: Console di gestione membri e gruppi
seo-title: Console di gestione membri e gruppi
description: Come accedere alle console di gestione di membri e gruppi
seo-description: Come accedere alle console di gestione di membri e gruppi
uuid: 2e93e861-a066-4189-91db-f8b784bc5aea
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: ccabf301-b417-48aa-8501-8360fd9f3e36
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Console di gestione membri e gruppi {#members-groups-management-consoles}

## Panoramica {#overview}

Le funzioni di AEM Communities spesso richiedono la registrazione e l&#39;accesso dei visitatori del sito prima di partecipare a una community nell&#39;ambiente di pubblicazione. La registrazione degli utenti è necessaria solo nell’ambiente di pubblicazione e sono comunemente denominati *membri* per distinguerli dagli *utenti* registrati nell’ambiente di authoring.

### Membri (utenti) in Pubblica {#members-users-on-publish}

Utilizzando le console Membri e Gruppi della community, i membri e i gruppi di membri registrati nell’ambiente di *pubblicazione* possono essere creati e gestiti dall’ambiente di *authoring* . Questo è possibile solo quando il servizio [](deploy-communities.md#tunnel-service-on-author) tunnel è attivato.

### Utenti su autore {#users-on-author}

Per gestire utenti e gruppi registrati nell’ambiente di *authoring* , è necessario utilizzare la console di protezione della piattaforma:

* Dalla selezione globale per la navigazione `Tools, Security, Users`
* Dalla selezione globale per la navigazione `Tools, Security, Groups`

>[!NOTE]
>
>Con il contenuto di esempio distribuito e attivato, molti utenti di esempio esistono sia nell’ambiente di creazione che nell’ambiente di pubblicazione. Questi utenti non saranno presenti se eseguiti con [nosamplecontent runmode](../../help/sites-administering/production-ready.md).

## Console Membri {#members-console}

Nell’ambiente di authoring, per accedere alla console Membri per la gestione dei membri registrati nell’ambiente di pubblicazione:

* Dalla navigazione globale: **[!UICONTROL Navigazione > Community > Membri]**

>[!CAUTION]
>
>Non sarà possibile utilizzare la console Membri se il servizio [](deploy-communities.md#tunnel-service-on-author) tunnel non è abilitato.

![chlimage_1-119](assets/chlimage_1-119.png)

### Ricerca {#search-features}

Selezionate l’icona del pannello laterale a sinistra dell’ `Members` intestazione per aprire il pannello laterale di ricerca.

![chlimage_1-120](assets/chlimage_1-120.png) ![chlimage_1-121](assets/chlimage_1-121.png)

Selezionate l’icona di ricerca a sinistra dell’ `Members` intestazione per chiudere il pannello di ricerca.

### Statistiche membri {#member-statistics}

Le colonne che vengono visualizzate `Views`, `Posts`e `Follows`vengono aggiornate quando l&#39;utente è membro di uno o più siti della community con Adobe Analytics `Likes` abilitato [](sites-console.md#analytics).

### Esporta CSV {#export-csv}

Selezionando il `Export CSV` collegamento, tutti i membri vengono scaricati come un elenco di valori separati da virgole, da importare in un foglio di calcolo.

Le intestazioni di colonna sono

`| Screen Name |Last Name |First Name |Status |Views |Posts |Follows |Likes |`

## Crea nuovo membro {#create-new-member}

Selezionate questa opzione `Create Member` per creare un utente nell’ambiente di pubblicazione.

![chlimage_1-122](assets/chlimage_1-122.png)

### GENERALE - Dettagli membro {#general-member-details}

La maggior parte dei campi sono campi facoltativi che il membro può successivamente compilare nel proprio profilo.

* **[!UICONTROL ID]**(*obbligatorio*) L’ID autorizzabile è l’ID di accesso del membro.
Per impostazione predefinita, l’ID è impostato sul valore dell’indirizzo e-mail richiesto.
   *Una volta creato, l’ID potrebbe non essere modificato.*

* **[!UICONTROL Indirizzo]** e-mail (*obbligatorio*) L&#39;indirizzo e-mail del membro.
Il membro può cambiare il proprio indirizzo e-mail quando aggiorna il proprio profilo. Se l’ID viene impostato automaticamente sull’indirizzo e-mail, l’ID *non* cambia quando l’indirizzo e-mail viene modificato.

* **[!UICONTROL Password]**(*richiesta*) La password di accesso.

* **[!UICONTROL Digitate nuovamente la password]**(*richiesta*) Immettete nuovamente la password per la verifica.

* **[!UICONTROL Aggiungi membro a siti]**(*facoltativo*) Seleziona uno dei siti community esistenti per aggiungere il membro al gruppo di membri della community.

* **[!UICONTROL Aggiungi membro a gruppi]**(*facoltativo*) Seleziona uno dei gruppi di membri esistenti per aggiungere il membro a tale gruppo.

* Seleziona **[!UICONTROL Salva]**

### GENERALE - Impostazioni account {#general-account-settings}

In Impostazioni account è possibile per un amministratore della community di

* **[!UICONTROL Stato]**
   * VietatoUn membro non è in grado di effettuare l&#39;accesso, né di visualizzarne le pagine o di partecipare ad attività che richiedono l&#39;accesso. Possono ancora visitare in forma anonima un sito di community aperto.

   * Non vietatoUn membro ha accesso completo al sito della community.
   Default is `Not Banned`.

* **[!UICONTROL Limiti]**contributi Se questa opzione è selezionata, la capacità del membro di pubblicare contenuti è limitata.
L’impostazione predefinita dipende dalla configurazione dei limiti dei contributi.
Consulta Limiti [di contributi](limits.md)membri.

* **[!UICONTROL Modifica password]** Collegamento presente durante la modifica di un membro esistente. Consente a un amministratore della community di ripristinare una password per un membro.

### GENERALE - Foto {#general-photo}

Per fornire un avatar al membro, selezionate **[!UICONTROL Carica immagine]** e scegliete un’immagine di tipo .jpg, .png, .tif o .gif. Le dimensioni preferite per un’immagine sono 240 x 240 pixel a 72 dpi.

### GENERAL - Add Member to Sites {#general-add-member-to-sites}

Il membro può essere aggiunto a uno o più gruppi di membri della community. Iniziate immettendo il testo nella casella di testo.

### GENERAL - Add Member to Groups {#general-add-member-to-groups}

Il membro può essere aggiunto a uno o più gruppi di membri. Iniziate immettendo il testo nella casella di testo.

### Scheda BADGES {#badges-tab}

Il `BADGES` pannello consente di assegnare manualmente i simboli e revocarli. I simboli possono essere per i ruoli assegnati e i simboli tipicamente guadagnati.

Vedere anche [Punteggio e Badge](implementing-scoring.md).

![chlimage_1-123](assets/chlimage_1-123.png)

* **[!UICONTROL Aggiungi simboli]**
   * Inizia a digitare per selezionare uno dei simboli [disponibili](badges.md). Dopo aver selezionato un contrassegno, scegliete ogni sito, o tutti i siti, su cui deve essere visualizzato il contrassegno insieme all&#39;avatar del membro.
   * È possibile scegliere più simboli e siti.
* **[!UICONTROL Rimuovi simboli]**
   * Selezionate l&#39;icona del cestino accanto a un contrassegno per rimuoverlo

## Console Gruppi {#groups-console}

La console Gruppi, disponibile nell’ambiente di authoring, consente di creare e gestire i gruppi di membri registrati nell’ambiente di pubblicazione. È particolarmente utile per:
* [Gruppi di membri privilegiati](users.md#privilegedmembersgroups)
* Assegnazione delle risorse di [abilitazione in base al gruppo](resources.md)

Per accedere alla console Gruppi:
* Dalla navigazione globale: **[!UICONTROL Navigazione > Community > Gruppi]**

>[!CAUTION]
>
>Non sarà possibile utilizzare la console Gruppi se il servizio [](deploy-communities.md#tunnel-service-on-author) tunnel non è abilitato.

### Crea nuovo gruppo {#create-new-group}

Selezionate `Add Group` per creare un gruppo nell’ambiente di pubblicazione.

![chlimage_1-124](assets/chlimage_1-124.png)

I campi necessari per creare un nuovo gruppo di membri lato pubblicazione sono:

* **[!UICONTROL ID]**(*obbligatorio*) L’ID univoco del gruppo.
   *Una volta creato, l’ID potrebbe non essere modificato.*

* **[!UICONTROL Nome]**(*facoltativo*) Il nome visualizzato per il gruppo.

   Il valore predefinito è ID.

* **[!UICONTROL Descrizione]**(*facoltativo*) Una descrizione dello scopo e delle autorizzazioni del gruppo.

* **[!UICONTROL Aggiungi membri al gruppo]**(*facoltativo*) Selezionate i membri lato pubblicazione da includere come membri iniziali del gruppo.

* Seleziona **[!UICONTROL Salva]**

## Amministratori autorizzati {#authorized-administrators}

Quando lavorate con i membri nella console dei membri di Communities, è necessario effettuare l&#39;accesso come utente con le autorizzazioni appropriate e configurare correttamente l&#39;agente di replica utilizzato dal servizio [](deploy-communities.md#tunnel-service-on-author) tunnel.

Se non avete effettuato l’accesso come `admin`, l’utente che ha effettuato l’accesso deve essere membro del gruppo di `administrators` utenti.

Vedere anche Agenti [di replica sull&#39;autore](deploy-communities.md#replication-agents-on-author).
