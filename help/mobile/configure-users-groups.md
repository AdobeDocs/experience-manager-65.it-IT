---
title: Configurazione di utenti e gruppi di utenti
seo-title: Configurazione di utenti e gruppi di utenti
description: Seguite questa pagina per comprendere i ruoli utente e come configurare utenti e gruppi per supportare l'authoring e la gestione delle app mobili.
seo-description: Seguite questa pagina per comprendere i ruoli utente e come configurare utenti e gruppi per supportare l'authoring e la gestione delle app mobili.
uuid: 55cea2b3-d7e6-4174-92b3-ee97e46b59c4
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-adobe-phonegap-enterprise
discoiquuid: 167f3bd9-7dbc-4e6b-9868-3ee53935641b
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '666'
ht-degree: 0%

---


# Configurare utenti e gruppi di utenti {#configure-your-users-and-user-groups}

>[!NOTE]
>
> Adobe consiglia di utilizzare l&#39;editor SPA per i progetti che richiedono il rendering lato client basato sul framework dell&#39;applicazione a pagina singola (ad es. React). [Per saperne di più](/help/sites-developing/spa-overview.md).

Questo capitolo descrive i ruoli utente e come configurare utenti e gruppi per l’authoring e la gestione delle app mobili.

##  AEM Mobile Application Users and Group Administration {#aem-mobile-application-users-and-group-administration}

Per organizzare e gestire il modello di autorizzazioni per AEM app, sono disponibili i due gruppi seguenti:

* amministratori di app per amministratori di app
* autori di app per autori di app

###  AEM Mobile Application Content Authors (gruppo di autori app) {#aem-mobile-application-content-authors-app-author-group}

I membri del gruppo di autori dell&#39;app sono responsabili della creazione AEM contenuto dell&#39;applicazione mobile, inclusi pagine, testo, immagini e video.

#### Configurazione del gruppo - app-authors {#group-configuration-app-authors}

1. Create un nuovo gruppo di utenti denominato &#39;app-authors&#39;:

   Andate al Admin Console  utenti: [http://localhost:4502/libs/granite/security/content/groupadmin.html](http://localhost:4502/libs/granite/security/content/groupadmin.html)

   Dall’interno della console del gruppo di utenti, fate clic sul pulsante &quot;+&quot; per creare un gruppo.

   Impostate l&#39;ID di questo gruppo su &#39;app-authors&#39; per indicare che si tratta di un tipo specifico di gruppo di utenti autori specifico per la creazione di applicazioni mobili all&#39;interno di AEM.

1. Aggiungi membro al gruppo: Autori

   ![chlimage_1-18](assets/chlimage_1-18.png)

   Aggiunta di autori di app al gruppo Autori

1. Dopo aver creato il gruppo di utenti autori dell&#39;app, puoi aggiungere singoli membri del team a questo nuovo gruppo tramite la [console di amministrazione utente](http://localhost:4502/libs/granite/security/content/useradmin.md).

   ![chlimage_1-19](assets/chlimage_1-19.png)

   Modifica dei gruppi di utenti

1. Andate alla [console Autorizzazioni](http://localhost:4502/useradmin) e aggiungete le autorizzazioni per amministrare i servizi cloud

   * (Leggi) su /etc/cloudservices
   >[!NOTE]
   >
   >Gli autori delle app estendono il gruppo predefinito di autori di contenuti (autori) da AEM, ereditando così la possibilità di creare contenuti in /content/phonegap

###  AEM Mobile Application Administrators Group (gruppo app-admins) {#aem-mobile-application-administrators-group-app-admins-group}

I membri del gruppo di amministratori dell&#39;app possono creare contenuto dell&#39;applicazione con le stesse autorizzazioni incluse con gli autori dell&#39;app **AND** inoltre sono responsabili per:

* Configurazione di PhoneGap Build e  servizi cloud di Mobile Services in AEM
* Gestione temporanea, pubblicazione e cancellazione degli aggiornamenti dell&#39;applicazione Content Sync OTA

>[!NOTE]
>
>Le autorizzazioni determinano la disponibilità di alcune azioni utente in AEM App Command Center.
>
>Noterete che alcune opzioni non sono disponibili per gli autori di app disponibili per gli amministratori di app.

#### Configurazione del gruppo - app-admins {#group-configuration-app-admins}

1. Create un nuovo gruppo denominato app-admins.
1. Aggiungi i seguenti gruppi al nuovo gruppo di amministratori delle app:

   * content-authors
   * workflow-users

   ![chlimage_1-20](assets/chlimage_1-20.png)

1. Andate alla [console Autorizzazioni](http://localhost:4502/useradmin) e aggiungete le autorizzazioni per amministrare i servizi cloud

   * (Lettura, Modifica, Creazione, Eliminazione, Replica) su /etc/cloud/services/mobileservizi
   * (Leggi, Modifica, Crea, Elimina, Replica) su /etc/cloudservices/phonegap-build

1. Nella stessa console Autorizzazioni, aggiungi le autorizzazioni per organizzare, pubblicare e cancellare gli aggiornamenti dei contenuti delle app

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

## Autorizzazioni sezione dashboard {#dashboard-tile-permissions}

Le sezioni del dashboard possono esporre azioni diverse in base alle autorizzazioni di cui dispone l&#39;utente. Di seguito sono descritte le azioni disponibili per ogni sezione.

Oltre a queste autorizzazioni, un&#39;azione può anche essere visualizzata o nascosta in base alla configurazione dell&#39;app corrente. Ad esempio, non ha senso esporre l&#39;azione &quot;Remote Build&quot;, se all&#39;app non è stata assegnata una configurazione cloud PhoneGap. Questi saranno elencati di seguito nelle sezioni &quot;**Condizione di configurazione**&quot;.

### Gestisci sezione app {#manage-app-tile}

Al momento la sezione non dispone di azioni che richiedono autorizzazioni, tuttavia la pagina dei dettagli dell&#39;applicazione include le azioni seguenti:

* *Editor* per app-author e app-admin (attivatore interfaccia utente - jcr:write - on /content/phonegap/{suffix})
* *Download* per app-author e app-admin (attivatore interfaccia utente - su /content/phonegap/{suffix})

L&#39;immagine seguente mostra le opzioni di download e modifica per un&#39;app:

![chlimage_1-21](assets/chlimage_1-21.png)

