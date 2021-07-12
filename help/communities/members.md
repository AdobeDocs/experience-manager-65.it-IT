---
title: Console di gestione membri e gruppi
seo-title: Console di gestione membri e gruppi
description: Accesso alle console Gestione membri e gruppi
seo-description: Accesso alle console Gestione membri e gruppi
uuid: 2e93e861-a066-4189-91db-f8b784bc5aea
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: ccabf301-b417-48aa-8501-8360fd9f3e36
role: Admin
exl-id: b64e24d2-8407-484c-8216-8d328ef5fa4f
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '963'
ht-degree: 4%

---

# Console di gestione membri e gruppi {#members-groups-management-consoles}

## Panoramica {#overview}

Le funzioni di AEM Communities richiedono spesso la registrazione e l’accesso dei visitatori del sito prima di partecipare a una community nell’ambiente di pubblicazione. La registrazione utente deve esistere solo nell&#39;ambiente di pubblicazione e viene comunemente definita *membri* per distinguerli dagli *utenti* registrati nell&#39;ambiente di authoring.

### Membri (utenti) in Pubblica {#members-users-on-publish}

Utilizzando le console Membri e Gruppi della community, i membri e i gruppi di membri registrati nell&#39;ambiente *pubblica* possono essere creati e gestiti dall&#39;ambiente *author* . Questo è possibile solo quando il [servizio tunnel](deploy-communities.md#tunnel-service-on-author) è abilitato.

### Utenti sull’autore {#users-on-author}

Per gestire gli utenti e i gruppi registrati nell&#39;ambiente *author* , è necessario utilizzare la console di sicurezza della piattaforma:

* Dalla navigazione globale, seleziona **[!UICONTROL Strumenti]** > **[!UICONTROL Sicurezza]** > **[!UICONTROL Utenti]**.
* Dalla navigazione globale, seleziona **[!UICONTROL Strumenti]** > **[!UICONTROL Sicurezza]** > **[!UICONTROL Gruppi]**.

>[!NOTE]
>
>Con il contenuto di esempio distribuito e abilitato, molti utenti di esempio esistono sia nell’ambiente di authoring che in quello di pubblicazione. Questi utenti non saranno presenti quando si esegue [nosamplecontent runmode](../../help/sites-administering/production-ready.md).

## Console dei membri {#members-console}

Nell’ambiente di authoring, per accedere alla console Membri per la gestione dei membri registrati nell’ambiente di pubblicazione:

* Dalla navigazione globale, seleziona **[!UICONTROL Navigazione]** > **[!UICONTROL Comunità]** > **[!UICONTROL Membri]**

>[!CAUTION]
>
>Non sarà possibile utilizzare la console Membri se il servizio [tunnel](deploy-communities.md#tunnel-service-on-author) non è abilitato.

![membro-console1](assets/member-console1.png)

### Ricerca {#search-features}

Seleziona l’icona del pannello laterale sul lato sinistro dell’ intestazione `Members` per aprire il pannello laterale di ricerca.

![](assets/leftpanel-icon.png)


![membro-console2](assets/member-console2.png)

Seleziona l’icona di ricerca sul lato sinistro dell’intestazione `Members` per chiudere il pannello laterale di ricerca.

### Statistiche membri {#member-statistics}

Le colonne contenenti `Views`, `Posts`, `Follows` e `Likes` vengono aggiornate quando l&#39;utente è membro di uno o più siti della community con Adobe Analytics [enabled](sites-console.md#analytics).

### Esporta CSV {#export-csv}

Selezionando il collegamento `Export CSV` si scaricano tutti i membri come un elenco di valori separati da virgole, idonei all’importazione in un foglio di calcolo.

Le intestazioni di colonna sono

`| Screen Name |Last Name |First Name |Status |Views |Posts |Follows |Likes |`

## Crea nuovo membro {#create-new-member}

Seleziona `Create Member` per creare un utente nell’ambiente di pubblicazione.

![create-membro1](assets/create-member1.png)

### GENERALE - Dettagli dei membri {#general-member-details}

La maggior parte dei campi sono campi facoltativi che il membro può successivamente compilare sul proprio profilo.

* **[!UICONTROL ID]**

(*Obbligatorio*) L&#39;ID autorizzabile è l&#39;ID di accesso del membro.
Per impostazione predefinita, l’ID è impostato sul valore dell’indirizzo e-mail richiesto.
*Una volta creato, l&#39;ID potrebbe non essere modificato*.

* **[!UICONTROL Indirizzo e-mail]**

(*Obbligatorio*) L&#39;indirizzo e-mail del membro.
Il membro può cambiare il proprio indirizzo e-mail quando aggiorna il proprio profilo.I
Se l’ID è stato impostato per impostazione predefinita sull’indirizzo e-mail, quando l’indirizzo e-mail viene modificato l’ID *non* viene modificato.

* **[!UICONTROL Password]**

   (*Obbligatorio*) La password di accesso.

* **[!UICONTROL Ripeti password]**

   (*Obbligatorio*) Immetti nuovamente la password per la verifica.

* **[!UICONTROL Aggiungi membro ai siti]**

   (*Facoltativo*) Per aggiungere il membro al gruppo di membri del sito community, seleziona uno dei siti community esistenti.

* **[!UICONTROL Aggiungi membro a gruppi]**

   (*Facoltativo*) Selezionare uno dei gruppi di membri esistenti per aggiungere il membro a tale gruppo.

* Seleziona **[!UICONTROL Salva]**

### GENERALE - Impostazioni account {#general-account-settings}

In Impostazioni account è possibile per un amministratore della community:

* **[!UICONTROL Stato]**
   * Vietato
Un membro non è in grado di accedere, impedendo loro di visualizzare pagine o partecipare ad attività che richiedono l’accesso. Possono ancora visitare in forma anonima un sito aperto della comunità.

   * Non bloccato
Un membro ha pieno accesso al sito della community.

   Il valore predefinito è `Not Banned`.

* **[!UICONTROL Limiti per contributi]**

   Se questa opzione è selezionata, la capacità del membro di pubblicare contenuto è limitata.
L’impostazione predefinita dipende dalla configurazione dei limiti dei contributi.
Consulta [Limiti dei contributi dei membri](limits.md).

* **[!UICONTROL Modifica password]**

   Collegamento presente durante la modifica di un membro esistente. Consente a un amministratore della community di reimpostare una password per un membro.

### GENERALE - Foto {#general-photo}

Per fornire un avatar al membro, inizia selezionando **[!UICONTROL Carica immagine]** e scegli un&#39;immagine di tipo .jpg, .png, .tif o .gif. La dimensione preferita di un’immagine è 240 x 240 pixel a 72 dpi.

### GENERALE - Aggiungi membro a siti {#general-add-member-to-sites}

Il membro può essere aggiunto a uno o più gruppi di membri della community. Iniziare inserendo testo nella casella di testo.

### GENERALE - Aggiungi membro ai gruppi {#general-add-member-to-groups}

Il membro può essere aggiunto a uno o più gruppi di membri. Iniziare inserendo testo nella casella di testo.

### Scheda BADGES {#badges-tab}

Il pannello `BADGES` consente di assegnare e revocare manualmente i badge. I badge possono essere assegnati a ruoli e badge tipicamente acquisiti.

Vedi anche [Punteggio e badge](implementing-scoring.md).

![create-membro2](assets/create-member2.png)

* **[!UICONTROL Aggiungi badge]**
   * Inizia a digitare per selezionare i [badge disponibili](badges.md). Dopo aver selezionato un badge, scegli ogni sito o tutti i siti in cui deve essere visualizzato il badge insieme all’avatar del membro.
   * È possibile scegliere più badge e siti.
* **[!UICONTROL Rimuovere i badge]**
   * Seleziona l’icona del cestino accanto a un badge per rimuoverlo.

## Console Gruppi {#groups-console}

La console Gruppi, disponibile nell’ambiente di authoring, consente di creare e gestire i gruppi di membri registrati nell’ambiente di pubblicazione. È particolarmente utile per:
* [Gruppi di membri privilegiati](users.md#privilegedmembersgroups)
* Assegnazione basata su gruppi di [risorse di abilitazione](resources.md)

Per accedere alla console Gruppi :
* Dalla navigazione globale, seleziona **[!UICONTROL Navigazione]** > **[!UICONTROL Comunità]** > **[!UICONTROL Gruppi]**.

>[!CAUTION]
>
>Non sarà possibile utilizzare la console Gruppi se il [servizio tunnel](deploy-communities.md#tunnel-service-on-author) non è abilitato.

### Crea nuovo gruppo {#create-new-group}

Seleziona `Add Group` per creare un gruppo nell’ambiente di pubblicazione.

![group-console1](assets/group-console1.png)

I campi richiesti per la creazione di un nuovo gruppo di membri lato pubblicazione sono:

* **[!UICONTROL ID]**

   (*Obbligatorio*) L&#39;ID univoco del gruppo.

   *Una volta creato, l&#39;ID potrebbe non essere modificato.*

* **[!UICONTROL Nome]**

   (*Facoltativo*) Il nome visualizzato del gruppo.

   Il valore predefinito è ID.

* **[!UICONTROL Descrizione]**

   (*Facoltativo*) Una descrizione dello scopo e delle autorizzazioni del gruppo.

* **[!UICONTROL Aggiungi membri al gruppo]**

   (*Facoltativo*) Seleziona i membri lato pubblicazione da includere come membri iniziali del gruppo.

* Seleziona **[!UICONTROL Salva]**

## Amministratori autorizzati {#authorized-administrators}

Quando si lavora con i membri nella console dei membri di Communities, è necessario effettuare l&#39;accesso come utente con le autorizzazioni appropriate e configurare correttamente l&#39;agente di replica utilizzato dal [servizio tunnel](deploy-communities.md#tunnel-service-on-author).

Se l&#39;accesso non è eseguito come `admin`, l&#39;utente connesso deve essere membro del gruppo di utenti `administrators`.

Vedere anche [Agenti di replica su Author](deploy-communities.md#replication-agents-on-author).
