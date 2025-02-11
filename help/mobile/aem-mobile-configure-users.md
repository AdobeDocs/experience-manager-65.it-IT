---
title: Configurare utenti e gruppi di utenti
description: Segui questa pagina per comprendere i ruoli utente e come configurare utenti e gruppi per supportare l’authoring e la gestione dell’app Mobile On-Demand Services.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-on-demand-services-app
exl-id: 58b7d1b9-a851-442a-9d02-212cad8abbed
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 1%

---

# Configurare utenti e gruppi di utenti {#configure-your-users-and-user-groups}

{{ue-over-mobile}}

Questo capitolo descrive i ruoli utente e le modalità di configurazione di utenti e gruppi per supportare l’authoring e la gestione delle app mobili.

## Utenti dell’applicazione AEM Mobile e amministrazione dei gruppi {#aem-mobile-application-users-and-group-administration}

### Autori di contenuti di applicazioni AEM Mobile (gruppo app-author) {#aem-mobile-application-content-authors-app-author-group}

I membri del gruppo di authoring delle app sono responsabili dell’authoring dei contenuti delle app mobili AEM, inclusi pagine, testo, immagini e video.

#### Configurazione del gruppo - autori-app {#group-configuration-app-authors}

1. Crea un gruppo di utenti denominato, &quot;app-authors&quot;:

   Passa all&#39;Admin Console utente: [http://localhost:4502/libs/granite/security/content/groupadmin.html](http://localhost:4502/libs/granite/security/content/groupadmin.html)

   Dalla console del gruppo di utenti, seleziona il pulsante &quot;+&quot; per creare un gruppo.

   Imposta l’ID di questo gruppo su &quot;app-authors&quot; per indicare che si tratta di un tipo specifico di gruppo di utenti Author specifico per l’authoring di applicazioni mobili all’interno dell’AEM.

1. Aggiungi membro al gruppo: Autori

   ![chlimage_1-167](assets/chlimage_1-167.png)

1. Dopo aver creato il gruppo utenti autori app, puoi aggiungere singoli membri del gruppo a questo nuovo gruppo tramite l&#39;[Admin Console utente](http://localhost:4502/libs/granite/security/content/useradmin.md).

   ![chlimage_1-168](assets/chlimage_1-168.png)

1. Di seguito è riportata l’aggiunta al gruppo di autori di contenuti dell’AEM:

   (Lettura) il

   * /app
   * /etc/clientlibs
   * /etc/designs
   * /etc/cloudservices/dps2015

### AEM Mobile Application Administrators Group (gruppo app-admins) {#aem-mobile-application-administrators-group-app-admins-group}

I membri del gruppo app-admins possono creare contenuti dell&#39;applicazione con le stesse autorizzazioni incluse con gli autori dell&#39;app **AND**, inoltre, sono responsabili di:

* Gestione temporanea, pubblicazione e cancellazione dell&#39;applicazione ContentSync OTA updates

>[!NOTE]
>
>Le autorizzazioni determinano la disponibilità di alcune azioni dell’utente nel Centro comandi app AEM.
>
>Tieni presente che alcune opzioni non sono disponibili per gli autori di app che sono disponibili per gli amministratori di app.

### Configurazione del gruppo - app-admins {#group-configuration-app-admins}

1. Crea un gruppo denominato app-admins.
1. Aggiungi i seguenti gruppi al nuovo gruppo app-admins:

   * content-authors
   * workflow-users

   ![chlimage_1-169](assets/chlimage_1-169.png)

   >[!NOTE]
   >
   >gli utenti del flusso di lavoro devono creare in remoto con il servizio PhoneGap Build

1. Passa alla [console Autorizzazioni](http://localhost:4502/useradmin) e aggiungi le autorizzazioni per amministrare i servizi cloud

   * (Lettura, modifica, creazione, eliminazione, replica) in /etc/cloudservices/mobileservices

1. Nella stessa console Autorizzazioni, aggiungi le autorizzazioni per staging, pubblicazione e cancellazione degli aggiornamenti dei contenuti dell’app;

   * (Lettura, modifica, creazione, eliminazione, replica) in /etc/packages/mobileapp
   * (Lettura) su /var/contentsync

   >[!NOTE]
   >
   >La replica dei pacchetti viene utilizzata per pubblicare gli aggiornamenti dell’app dall’istanza di authoring a quella di pubblicazione

   >[!CAUTION]
   >
   >L’accesso /var/contentsync è negato come standard.
   >
   >Se si omette l’autorizzazione READ, è possibile che vengano generati e replicati pacchetti di aggiornamento vuoti.

1. Aggiungi membri al gruppo in base alle esigenze
1. Per esportare contenuto o caricare

   * (Lettura) su /etc/contentsync per accedere ai modelli di esportazione
   * (Lettura) su /var per l’attraversamento del percorso su letture
   * (Lettura, scrittura, modifica, eliminazione) su /var/contentsync per scrivere, leggere e ripulire il contenuto di esportazione memorizzato nella cache di ContentSync

### Risorse aggiuntive {#additional-resources}

Per ulteriori informazioni sugli altri due ruoli e responsabilità per la creazione di un’app AEM Mobile On-demand Services, consulta le risorse seguenti:

* [Sviluppo di contenuti AEM per AEM Mobile On-demand Services](/help/mobile/aem-mobile-on-demand.md)
* [Creazione di contenuti AEM per l’app AEM Mobile On-demand Services](/help/mobile/mobile-apps-ondemand.md)
