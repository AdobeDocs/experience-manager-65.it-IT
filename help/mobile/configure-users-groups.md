---
title: Configurazione di utenti e gruppi di utenti
description: Segui questa pagina per scoprire i ruoli utente e come configurare utenti e gruppi per supportare la creazione e la gestione delle tue app mobili.
uuid: 55cea2b3-d7e6-4174-92b3-ee97e46b59c4
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-adobe-phonegap-enterprise
discoiquuid: 167f3bd9-7dbc-4e6b-9868-3ee53935641b
exl-id: 9f814204-8cd4-4ba9-9e25-3ff1b25c1955
source-git-commit: f4b6eb2ded17ec641f23a1fc3b977ce77169c8a1
workflow-type: tm+mt
source-wordcount: '633'
ht-degree: 0%

---

# Configurare utenti e gruppi di utenti {#configure-your-users-and-user-groups}

>[!NOTE]
>
>Adobe consiglia di utilizzare l’editor di SPA per i progetti che richiedono il rendering lato client basato sul framework di un’applicazione a pagina singola (ad esempio, React). [Ulteriori informazioni](/help/sites-developing/spa-overview.md).

Questo capitolo descrive i ruoli utente e come configurare utenti e gruppi per supportare la creazione e la gestione delle app mobili.

## Utenti di applicazioni e amministrazione di gruppi AEM Mobile {#aem-mobile-application-users-and-group-administration}

Per organizzare e gestire il modello di autorizzazioni per le app AEM sono disponibili i due gruppi seguenti:

* amministratori di app per amministratori di app
* autori di app per autori di app

### Autori del contenuto dell&#39;applicazione AEM Mobile (gruppo autore dell&#39;app) {#aem-mobile-application-content-authors-app-author-group}

I membri del gruppo di autori dell’app sono responsabili della creazione AEM contenuto dell’app mobile, compresi pagine, testo, immagini e video.

#### Configurazione del gruppo - app-authors {#group-configuration-app-authors}

1. Crea un nuovo gruppo di utenti denominato &quot;app-authors&quot;:

   Passa all’Admin Console utente: [http://localhost:4502/libs/granite/security/content/groupadmin.html](http://localhost:4502/libs/granite/security/content/groupadmin.html)

   Dall’interno della console dei gruppi di utenti, seleziona il pulsante &quot;+&quot; per creare un gruppo.

   Imposta l&#39;ID di questo gruppo su &#39;app-authors&#39; per indicare che si tratta di un tipo specifico di gruppo di utenti autore specifico per la creazione di applicazioni mobili all&#39;interno di AEM.

1. Aggiungi membro al gruppo: Autori

   ![chlimage_1-18](assets/chlimage_1-18.png)

   Aggiungere autori di app al gruppo Autori

1. Ora che hai creato il gruppo di utenti app-authors, puoi aggiungere singoli membri del team a questo nuovo gruppo tramite [Admin Console utente](http://localhost:4502/libs/granite/security/content/useradmin.md).

   ![chlimage_1-19](assets/chlimage_1-19.png)

   Modificare i gruppi di utenti

1. Passa a [Console Autorizzazioni](http://localhost:4502/useradmin) e aggiungi le autorizzazioni per amministrare cloudservices

   * (Leggi) su /etc/cloudservices
   >[!NOTE]
   >
   >Gli autori di app estendono il gruppo predefinito di autori di contenuti (autori) AEM ereditando così la possibilità di creare contenuti in /content/phonegap

### Gruppo Amministratori applicazioni AEM Mobile (gruppo Amministratori app) {#aem-mobile-application-administrators-group-app-admins-group}

I membri del gruppo di amministratori dell&#39;app possono creare contenuti dell&#39;applicazione con le stesse autorizzazioni incluse con gli autori dell&#39;app **E** inoltre sono responsabili:

* Configurazione di PhoneGap Build ed Adobe Mobile Services Cloud Services in AEM
* Staging, pubblicazione e cancellazione degli aggiornamenti OTA di sincronizzazione dei contenuti dell’applicazione

>[!NOTE]
>
>Le autorizzazioni determinano la disponibilità di alcune azioni dell&#39;utente nel Centro comandi AEM app.
>
>Noterai che alcune opzioni non sono disponibili per gli autori delle app disponibili per gli amministratori delle app.

#### Configurazione del gruppo - amministratori delle app {#group-configuration-app-admins}

1. Crea un nuovo gruppo denominato app-admins.
1. Aggiungi i seguenti gruppi al nuovo gruppo di amministratori dell&#39;app:

   * content-authors
   * utenti del flusso di lavoro

   ![chlimage_1-20](assets/chlimage_1-20.png)

1. Passa a [Console Autorizzazioni](http://localhost:4502/useradmin) e aggiungi le autorizzazioni per amministrare cloudservices

   * (Lettura, modifica, creazione, eliminazione, replica) su /etc/cloudservices/mobileservizi
   * (Lettura, modifica, creazione, eliminazione, replica) su /etc/cloudservices/phonegap-build

1. Nella stessa console Autorizzazioni, aggiungi le autorizzazioni per eseguire l’area di visualizzazione, pubblicare e cancellare gli aggiornamenti del contenuto dell’app

   * (Leggi, Modifica, Crea, Elimina, Replica) su /etc/packages/mobileapp
   * (Leggi) su /var/contentsync

   >[!NOTE]
   >
   >La replica del pacchetto viene utilizzata per pubblicare gli aggiornamenti dell’app dall’istanza dell’autore all’istanza di pubblicazione

   >[!CAUTION]
   >
   >L&#39;accesso a /var/contentsync è negato a OOTB.
   >
   >Se si omette l&#39;autorizzazione READ, i pacchetti di aggiornamento vuoti vengono generati e replicati.

1. Aggiungi i membri del gruppo in base alle esigenze

## Autorizzazioni sezione dashboard {#dashboard-tile-permissions}

I riquadri del dashboard possono esporre diverse azioni in base alle autorizzazioni di cui dispone l’utente. Di seguito sono descritte le azioni disponibili per ogni riquadro.

Oltre a queste autorizzazioni, puoi anche mostrare/nascondere un’azione in base alla configurazione dell’app corrente. Ad esempio, non ha senso esporre l’azione &quot;Build remota&quot;, se all’app non è stata assegnata una configurazione cloud PhoneGap. Questi saranno elencati di seguito in &quot;**Condizione di configurazione**&quot; sezioni.

### Gestisci porzione app {#manage-app-tile}

Al momento la tessera non dispone di azioni che richiedono autorizzazioni, tuttavia la pagina dei dettagli per l’applicazione dispone delle seguenti azioni:

* *Modifica* per app-author e app-admin (trigger interfaccia utente - jcr:write - on /content/phonegap/{suffix})
* *Scarica* per app-author e app-admin (trigger interfaccia utente - su /content/phonegap/{suffix})

L’immagine seguente mostra le opzioni Scarica e Modifica per un’app:

![chlimage_1-21](assets/chlimage_1-21.png)
