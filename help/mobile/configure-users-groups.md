---
title: Configurare utenti e gruppi di utenti
description: Segui questa pagina per comprendere i ruoli utente e come configurare utenti e gruppi per supportare l’authoring e la gestione delle app mobili.
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
>L’Adobe consiglia di utilizzare l’Editor SPA per i progetti che richiedono il rendering lato client basato su framework di applicazione a pagina singola (ad esempio, React). [Ulteriori informazioni](/help/sites-developing/spa-overview.md).

Questo capitolo descrive i ruoli utente e le modalità di configurazione di utenti e gruppi per supportare l’authoring e la gestione delle app mobili.

## Utenti dell’applicazione AEM Mobile e amministrazione dei gruppi {#aem-mobile-application-users-and-group-administration}

Per organizzare e gestire il modello di autorizzazione per le app AEM, sono disponibili i due gruppi seguenti:

* app-admins per amministratori di app
* autori di app per autori di app

### Autori di contenuti di applicazioni AEM Mobile (gruppo app-author) {#aem-mobile-application-content-authors-app-author-group}

I membri del gruppo di authoring delle app sono responsabili dell’authoring dei contenuti delle app mobili AEM, inclusi pagine, testo, immagini e video.

#### Configurazione del gruppo - autori-app {#group-configuration-app-authors}

1. Crea un nuovo gruppo di utenti denominato, &quot;app-authors&quot;:

   Passa all’Admin Console utente: [http://localhost:4502/libs/granite/security/content/groupadmin.html](http://localhost:4502/libs/granite/security/content/groupadmin.html)

   Dall’interno della console del gruppo di utenti, seleziona il pulsante &quot;+&quot; per creare il gruppo.

   Imposta l’ID di questo gruppo su &quot;app-authors&quot; per indicare che si tratta di un tipo specifico di gruppo di utenti Author specifico per l’authoring di applicazioni mobili all’interno dell’AEM.

1. Aggiungi membro al gruppo: Autori

   ![chlimage_1-18](assets/chlimage_1-18.png)

   Aggiungere autori delle app al gruppo Autori

1. Dopo aver creato il gruppo utenti autori app, puoi aggiungere singoli membri del gruppo a questo nuovo gruppo tramite [User Admin Console](http://localhost:4502/libs/granite/security/content/useradmin.md).

   ![chlimage_1-19](assets/chlimage_1-19.png)

   Modifica gruppi di utenti

1. Accedi a [Console Autorizzazioni](http://localhost:4502/useradmin) e aggiungere le autorizzazioni per amministrare cloudservices

   * (Leggi) su /etc/cloudservices
   >[!NOTE]
   >
   >Gli autori delle app estendono il gruppo predefinito di autori di contenuti (Autori) dall’AEM, ereditando in tal modo la possibilità di creare contenuti in /content/phonegap

### AEM Mobile Application Administrators Group (gruppo app-admins) {#aem-mobile-application-administrators-group-app-admins-group}

I membri del gruppo app-admins possono creare contenuti dell’applicazione con le stesse autorizzazioni fornite agli autori delle app **E** sono inoltre responsabili di:

* Configurazione di PhoneGap Build e Adobe Mobile Services Cloud Services nell’AEM
* Staging, pubblicazione e cancellazione dell&#39;applicazione Content Sync OTA updates

>[!NOTE]
>
>Le autorizzazioni determinano la disponibilità di alcune azioni dell’utente nel Centro comandi app AEM.
>
>Noterai che alcune opzioni non sono disponibili per gli autori di app che sono disponibili per gli amministratori di app.

#### Configurazione del gruppo - app-admins {#group-configuration-app-admins}

1. Crea un nuovo gruppo denominato app-admins.
1. Aggiungi i seguenti gruppi al nuovo gruppo app-admins:

   * content-authors
   * workflow-users

   ![chlimage_1-20](assets/chlimage_1-20.png)

1. Accedi a [Console Autorizzazioni](http://localhost:4502/useradmin) e aggiungere le autorizzazioni per amministrare cloudservices

   * (Lettura, modifica, creazione, eliminazione, replica) in /etc/cloudservices/mobileservices
   * (Lettura, modifica, creazione, eliminazione, replica) in /etc/cloudservices/phonegap-build

1. Nella stessa console Autorizzazioni, aggiungi le autorizzazioni per staging, pubblicazione e cancellazione degli aggiornamenti dei contenuti dell’app

   * (Lettura, modifica, creazione, eliminazione, replica) in /etc/packages/mobileapp
   * (Lettura) su /var/contentsync

   >[!NOTE]
   >
   >La replica dei pacchetti viene utilizzata per pubblicare gli aggiornamenti dell’app dall’istanza di authoring a quella di pubblicazione

   >[!CAUTION]
   >
   >Accesso negato a /var/contentsync OOTB.
   >
   >Se si omette l’autorizzazione READ, è possibile che vengano generati e replicati pacchetti di aggiornamento vuoti.

1. Aggiungi membri al gruppo in base alle esigenze

## Autorizzazioni delle sezioni del dashboard {#dashboard-tile-permissions}

I riquadri del dashboard possono esporre azioni diverse in base alle autorizzazioni di cui dispone l’utente. Di seguito sono descritte le azioni disponibili per ogni sezione.

Oltre a queste autorizzazioni, un’azione può anche essere visualizzata/nascosta in base alla configurazione dell’app corrente. Ad esempio, se all’app non è stata assegnata alcuna configurazione cloud PhoneGap, l’azione &quot;Remote Build&quot; non verrà esposta in alcun modo. Questi saranno elencati di seguito in &quot;**Condizione di configurazione**&#39; sezioni.

### Gestisci sezione app {#manage-app-tile}

Al momento il riquadro non presenta azioni che richiedono autorizzazioni, tuttavia la pagina dei dettagli dell’applicazione presenta le azioni seguenti:

* *Modifica* per app-author e app-admin (Trigger interfaccia utente - jcr:write - su /content/phonegap/{suffix})
* *Scarica* per app-author e app-admin (Trigger interfaccia utente: su /content/phonegap/{suffix})

L’immagine seguente mostra le opzioni Scarica e Modifica per un’app:

![chlimage_1-21](assets/chlimage_1-21.png)
