---
title: Configurare utenti e gruppi di utenti
seo-title: Configure Your Users and User Groups
description: Segui questa pagina per scoprire i ruoli utente e come configurare utenti e gruppi per supportare la creazione e la gestione dell’app mobile On-Demand Services.
seo-description: Follow this page to understand the user roles and how to configure your users and groups to support the authoring and mangement of your mobile On-Demand services app.
uuid: 461e1725-41dd-4883-92b9-a7e175660401
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-on-demand-services-app
discoiquuid: c3c73e67-7f85-4308-b4cd-1b42d4f3f2d9
exl-id: 58b7d1b9-a851-442a-9d02-212cad8abbed
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 1%

---

# Configurare utenti e gruppi di utenti {#configure-your-users-and-user-groups}

>[!NOTE]
>
>Adobe consiglia di utilizzare l’editor di SPA per i progetti che richiedono il rendering lato client basato sul framework di un’applicazione a pagina singola (ad esempio, React). [Per saperne di più](/help/sites-developing/spa-overview.md).

Questo capitolo descrive i ruoli utente e come configurare utenti e gruppi per supportare la creazione e la gestione delle app mobili.

## Utenti di applicazioni e amministrazione di gruppi AEM Mobile {#aem-mobile-application-users-and-group-administration}

### Autori del contenuto dell&#39;applicazione AEM Mobile (gruppo autore dell&#39;app) {#aem-mobile-application-content-authors-app-author-group}

I membri del gruppo di autori dell’app sono responsabili della creazione AEM contenuto dell’app mobile, compresi pagine, testo, immagini e video.

#### Configurazione del gruppo - app-authors {#group-configuration-app-authors}

1. Crea un nuovo gruppo di utenti denominato &quot;app-authors&quot;:

   Passa all’Admin Console utente: [http://localhost:4502/libs/granite/security/content/groupadmin.html](http://localhost:4502/libs/granite/security/content/groupadmin.html)

   Dall’interno della console dei gruppi di utenti, seleziona il pulsante &quot;+&quot; per creare un gruppo.

   Imposta l&#39;ID di questo gruppo su &#39;app-authors&#39; per indicare che si tratta di un tipo specifico di gruppo di utenti autore specifico per la creazione di applicazioni mobili all&#39;interno di AEM.

1. Aggiungi membro al gruppo: Autori

   ![chlimage_1-167](assets/chlimage_1-167.png)

1. Ora che hai creato il gruppo di utenti app-authors, puoi aggiungere singoli membri del team a questo nuovo gruppo tramite [Admin Console utente](http://localhost:4502/libs/granite/security/content/useradmin.md).

   ![chlimage_1-168](assets/chlimage_1-168.png)

1. Di seguito è possibile aggiungere AEM gruppo di autori di contenuti:

   (Leggi) su

   * /app
   * /etc/clientlibs
   * /etc/designs
   * /etc/cloudservices/dps2015

### Gruppo Amministratori applicazioni AEM Mobile (gruppo Amministratori app) {#aem-mobile-application-administrators-group-app-admins-group}

I membri del gruppo di amministratori dell&#39;app possono creare contenuti dell&#39;applicazione con le stesse autorizzazioni incluse con gli autori dell&#39;app **E** inoltre sono responsabili:

* Staging, pubblicazione e cancellazione degli aggiornamenti OTA di ContentSync dell’applicazione

>[!NOTE]
>
>Le autorizzazioni determinano la disponibilità di alcune azioni dell&#39;utente nel Centro comandi AEM app.
>
>Noterai che alcune opzioni non sono disponibili per gli autori delle app disponibili per gli amministratori delle app.

### Configurazione del gruppo - amministratori delle app {#group-configuration-app-admins}

1. Crea un nuovo gruppo denominato app-admins.
1. Aggiungi i seguenti gruppi al nuovo gruppo di amministratori dell&#39;app:

   * content-authors
   * utenti del flusso di lavoro

   ![chlimage_1-169](assets/chlimage_1-169.png)

   >[!NOTE]
   >
   >gli utenti del flusso di lavoro sono tenuti a creare in remoto con il servizio PhoneGap Build

1. Passa a [Console Autorizzazioni](http://localhost:4502/useradmin) e aggiungi le autorizzazioni per amministrare cloudservices

   * (Lettura, modifica, creazione, eliminazione, replica) su /etc/cloudservices/mobileservizi

1. Nella stessa console Autorizzazioni, aggiungi le autorizzazioni per impostare, pubblicare e cancellare gli aggiornamenti dei contenuti delle app;

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
1. Per esportare contenuto o caricare

   * (Leggi) su /etc/contentsync per accedere ai modelli di esportazione
   * (Leggi) su /var a per l&#39;attraversamento del percorso sulle letture
   * (Leggi, Scrivi, Modifica, Elimina) su /var/contentsync per scrivere, leggere e pulire il contenuto di esportazione in cache di ContentSync

### Risorse aggiuntive {#additional-resources}

Per ulteriori informazioni sugli altri due ruoli e responsabilità per la creazione di un’app AEM Mobile On-demand Services, consulta le risorse seguenti:

* [Sviluppo di contenuti AEM per AEM Mobile On-demand Services](/help/mobile/aem-mobile-on-demand.md)
* [Creazione di contenuti AEM per l’app AEM Mobile On-demand Services](/help/mobile/mobile-apps-ondemand.md)
