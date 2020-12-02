---
title: Configurazione di utenti e gruppi di utenti
seo-title: Configurazione di utenti e gruppi di utenti
description: Seguite questa pagina per comprendere i ruoli utente e come configurare utenti e gruppi per supportare l'authoring e la gestione dell'app dei servizi on-demand per dispositivi mobili.
seo-description: Seguite questa pagina per comprendere i ruoli utente e come configurare utenti e gruppi per supportare l'authoring e la gestione dell'app dei servizi on-demand per dispositivi mobili.
uuid: 461e1725-41dd-4883-92b9-a7e175660401
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-on-demand-services-app
discoiquuid: c3c73e67-7f85-4308-b4cd-1b42d4f3f2d9
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 1%

---


# Configurare utenti e gruppi di utenti {#configure-your-users-and-user-groups}

>[!NOTE]
>
> Adobe consiglia di utilizzare l&#39;editor SPA per i progetti che richiedono il rendering lato client basato sul framework dell&#39;applicazione a pagina singola (ad es. React). [Per saperne di più](/help/sites-developing/spa-overview.md).

Questo capitolo descrive i ruoli utente e come configurare utenti e gruppi per l’authoring e la gestione delle app mobili.

##  AEM Mobile Application Users and Group Administration {#aem-mobile-application-users-and-group-administration}

###  AEM Mobile Application Content Authors (gruppo di autori app) {#aem-mobile-application-content-authors-app-author-group}

I membri del gruppo di autori dell&#39;app sono responsabili della creazione AEM contenuto dell&#39;applicazione mobile, inclusi pagine, testo, immagini e video.

#### Configurazione del gruppo - app-authors {#group-configuration-app-authors}

1. Create un nuovo gruppo di utenti denominato &#39;app-authors&#39;:

   Andate al Admin Console  utenti: [http://localhost:4502/libs/granite/security/content/groupadmin.html](http://localhost:4502/libs/granite/security/content/groupadmin.html)

   Dall’interno della console del gruppo di utenti, fate clic sul pulsante &quot;+&quot; per creare un gruppo.

   Impostate l&#39;ID di questo gruppo su &#39;app-authors&#39; per indicare che si tratta di un tipo specifico di gruppo di utenti autori specifico per la creazione di applicazioni mobili all&#39;interno di AEM.

1. Aggiungi membro al gruppo: Autori

   ![chlimage_1-167](assets/chlimage_1-167.png)

1. Dopo aver creato il gruppo di utenti autori dell&#39;app, puoi aggiungere singoli membri del team a questo nuovo gruppo tramite la [console di amministrazione utente](http://localhost:4502/libs/granite/security/content/useradmin.md).

   ![chlimage_1-168](assets/chlimage_1-168.png)

1. Di seguito è possibile aggiungere AEM gruppo di autori di contenuti:

   (Leggi su

   * /app
   * /etc/clientlibs
   * /etc/designs
   * /etc/cloudservices/dps2015

###  AEM Mobile Application Administrators Group (gruppo app-admins) {#aem-mobile-application-administrators-group-app-admins-group}

I membri del gruppo di amministratori dell&#39;app possono creare contenuto dell&#39;applicazione con le stesse autorizzazioni incluse con gli autori dell&#39;app **AND** inoltre sono responsabili per:

* Gestione temporanea, pubblicazione e cancellazione degli aggiornamenti dell&#39;applicazione ContentSync OTA

>[!NOTE]
>
>Le autorizzazioni determinano la disponibilità di alcune azioni utente in AEM App Command Center.
>
>Noterete che alcune opzioni non sono disponibili per gli autori di app disponibili per gli amministratori di app.

### Configurazione del gruppo - app-admins {#group-configuration-app-admins}

1. Create un nuovo gruppo denominato app-admins.
1. Aggiungi i seguenti gruppi al nuovo gruppo di amministratori delle app:

   * content-authors
   * workflow-users

   ![chlimage_1-169](assets/chlimage_1-169.png)

   >[!NOTE]
   >
   >gli utenti del flusso di lavoro devono creare da remoto con il servizio PhoneGap Build

1. Andate alla [console Autorizzazioni](http://localhost:4502/useradmin) e aggiungete le autorizzazioni per amministrare i servizi cloud

   * (Lettura, Modifica, Creazione, Eliminazione, Replica) su /etc/cloud/services/mobileservizi

1. Nella stessa console Autorizzazioni, aggiungete le autorizzazioni per organizzare, pubblicare e cancellare gli aggiornamenti dei contenuti delle app;

   * (Lettura, Modifica, Creazione, Eliminazione, Replica) su /etc/packages/mobileapp
   * (Leggi) su /var/contentsync

   >[!NOTE]
   >
   >La replica del pacchetto viene utilizzata per pubblicare gli aggiornamenti dell&#39;app dall&#39;istanza di creazione all&#39;istanza di pubblicazione

   >[!CAUTION]
   >
   >/var/contentsync accesso negato OOTB.
   >
   >Se si omette l&#39;autorizzazione READ è possibile creare e replicare pacchetti di aggiornamento vuoti.

1. Aggiungi membri a questo gruppo in base alle esigenze
1. Per esportare contenuto o caricare

   * (Leggi) su /etc/contentsync per accedere ai modelli di esportazione
   * (Leggi su /var to per l&#39;attraversamento del percorso durante la lettura)
   * (Lettura, scrittura, modifica, eliminazione) su /var/contentsync per scrivere, leggere e pulire il contenuto dell&#39;esportazione nella cache di ContentSync

### Risorse aggiuntive {#additional-resources}

Per ulteriori informazioni sugli altri due ruoli e responsabilità per la creazione di un&#39;app AEM Mobile On-demand Services , consulta le risorse seguenti:

* [Sviluppo AEM contenuto per  AEM Mobile On-demand Services](/help/mobile/aem-mobile-on-demand.md)
* [Creazione AEM contenuto per  app AEM Mobile On-demand Services](/help/mobile/mobile-apps-ondemand.md)
