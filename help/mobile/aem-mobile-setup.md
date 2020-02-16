---
title: Impostazione AEM Mobile
seo-title: Impostazione AEM Mobile
description: Seguite questa pagina per configurare AEM Mobile e consentire quindi all'utente di creare e gestire il contenuto in AEM. Questa pagina fornisce informazioni sull'integrazione dell'istanza AEM con l'account AEM Mobile On-Demand Services basato su cloud e i progetti.
seo-description: Seguite questa pagina per configurare AEM Mobile e consentire quindi all'utente di creare e gestire il contenuto in AEM. Questa pagina fornisce informazioni sull'integrazione dell'istanza AEM con l'account AEM Mobile On-Demand Services basato su cloud e i progetti.
uuid: 03bf5b56-7750-4f76-b079-43761367655a
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-on-demand-services-app
discoiquuid: 393cf504-917e-4bf6-9a8b-b7a5bd862c65
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Impostazione AEM Mobile{#aem-mobile-setup}

>[!NOTE]
>
>Adobe consiglia di utilizzare SPA Editor per i progetti che richiedono il rendering lato client basato sul framework dell&#39;applicazione a pagina singola (ad es. React). [Per saperne di più](/help/sites-developing/spa-overview.md).

>[!CAUTION]
>
>I clienti delle app AEM Mobile esistenti che eseguono la migrazione da AEM 6.2 o 6.3 a AEM 6.5 possono continuare a utilizzare le app AEM Mobile scaricando un [pacchetto da PackageShare](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq640/compatpack/aem-mobile-package). Tuttavia, le nuove installazioni di AEM 6.5 non supporteranno la funzionalità delle app AEM Mobile.

Per utilizzare AEM per produrre contenuto per le app AEM Mobile, dovete integrare l&#39;istanza AEM con l&#39;account AEM Mobile On-Demand Services basato su cloud e con i progetti.

Seguite questi passaggi per configurare AEM Mobile e consentire quindi all&#39;utente di creare e gestire il contenuto in AEM.

## Provisioning di AEM Mobile {#aem-mobile-provisioning}

Per iniziare a utilizzare la configurazione di AEM Mobile, dovete:

* **Richiedete una chiave** API: Per accedere a On-Demand Services API, è necessario richiedere una chiave API. Per richiedere la chiave API, completare il modulo [](https://helpx.adobe.com/digital-publishing-solution/help/integrating-dps.html)PDF. Inviate il modulo compilato all&#39;Assistenza sviluppatori di Adobe: [wwds@adobe.com](mailto:wwds@adobe.com)

* **Generate l&#39;ID dispositivo e il token** dispositivo: Dopo aver ricevuto la chiave API, potete generare l&#39;ID dispositivo e il token dispositivo. Andate a [https://aex.aemmobile.adobe.com](https://aex.aemmobile.adobe.com/) ed effettuate le seguenti operazioni:

   * Fornite la chiave API
   * Effettuate l&#39;accesso con un Adobe ID aggiunto a un progetto AEM Mobile con le seguenti autorizzazioni (consultate i passaggi sottostanti per creare un progetto)

      * Amministrazione > Gestisci progetti e utenti
      * Contenuto > Aggiungi e modifica contenuto, Elimina contenuto, Visualizza contenuto, Pubblica contenuto

Se tutte le condizioni sono soddisfatte, verranno generati un ID dispositivo e un Token dispositivo.

>[!NOTE]
>
>L&#39;Adobe ID necessario deve avere accesso a un progetto AEM Mobile. Consultate Amministrazione [account per AEM Mobile](https://helpx.adobe.com/digital-publishing-solution/help/account-admin-dps.html) nell&#39;Aiuto online.

## Creazione di progetti per AEM Mobile {#creating-projects-for-aem-mobile}

Quando create un progetto, specificate le impostazioni per qualsiasi piattaforma di destinazione: iOS, Android, Windows e Desktop Web Viewer. Molte delle impostazioni di progetto specificate influiscono sul comportamento dell&#39;app.

Per creare un progetto è necessario accedere al portale dei servizi on-demand utilizzando un Adobe ID che disponga di un ruolo Amministratore principale. La modifica di un progetto richiede un ruolo Amministratore principale o un ruolo utente con un&#39;autorizzazione **Gestisci progetti e utenti** .

>[!NOTE]
>
>Per ulteriori informazioni sulla creazione di progetti in AEM Mobile, fate clic [qui](https://helpx.adobe.com/digital-publishing-solution/help/creating-projects.html).

## Configurazione di un connettore AEM Mobile {#configuring-an-aem-mobile-connector}

La configurazione di AEM prevede i seguenti passaggi per la configurazione del connettore. Una volta completata la configurazione del connettore AEM Mobile, l&#39;utente può impostare gruppi di utenti e autorizzazioni.

Il connettore AEM Mobile On-Demand viene utilizzato per associare il contenuto gestito AEM Mobile ai servizi on-demand di Adobe Experience Manager Mobile. In questo modo gli autori dei contenuti possono creare e gestire il materiale per le applicazioni mobili utilizzando gli strumenti di AEM e i servizi on-demand di AEM Mobile per una facile distribuzione dei contenuti mobili.

>[!NOTE]
>
>Si tratta di un unico passaggio per configurare l’istanza di AEM.

### Configurazione del client AEM Mobile On-Demand Services {#configuring-aem-mobile-on-demand-services-client}

Affinché le integrazioni AEM Mobile funzionino correttamente, dovete completare i passaggi di configurazione.

1. Vai alla configurazione del servizio OSGI

   1. AEM > Strumenti > Operazioni > Console Web
   1. Scorrere o cercare il client ***Experience Manager Mobile On-demand Services (era il client Adobe Digital Publishing Solution)***

1. Modifica del client ***Experience Manager Mobile On-demand Services***

   1. **(Obbligatorio)** Immettete i campi obbligatori:

      1. ID client.
      1. Segreto client.
   1. **(Facoltativo)** Modificate i valori esistenti.


1. Salva le modifiche.
1. Esempio di configurazione:

![chlimage_1-53](assets/chlimage_1-53.png)

### Configurazione di AEM Mobile On-Demand Services CloudService {#configuring-aem-mobile-on-demand-services-cloudservice}

1. Vai a Servizi cloud

   1. AEM > Strumenti > Distribuzione > [CloudServices](http://localhost:4502/libs/cq/core/content/tools/cloudservices.html). Scorrere o cercare ***Adobe Experience Manager Mobile On-demand Services***

1. Selezionate ***Configura ora*** o ***Mostra configurazioni*** e selezionate l&#39;icona Aggiungi nuova configurazione

1. Creare una nuova configurazione

   1. Immettere un titolo e un nome
   1. Immetti ID dispositivo
   1. Immetti token dispositivo
   1. Seleziona ***Verifica configurazione*** dispositivo per convalidare i valori immessi
   1. Seleziona OK

## Aggiunta di ruoli utente di AEM Mobile e assegnazione di autorizzazioni {#adding-aem-mobile-user-roles-and-assigning-permissions}

Dopo aver creato un progetto è necessario creare ruoli e concedere l&#39;accesso agli utenti. Solo gli Amministratori principali possono creare e modificare i ruoli. Quando create un ruolo, abilitate le capacità (o autorizzazioni) per tutti gli utenti a cui sono assegnate tali autorizzazioni. Ad esempio, potete creare un ruolo che include le autorizzazioni per la creazione di app e un altro ruolo che include le autorizzazioni per la creazione e la pubblicazione di contenuto.

Nello sviluppo di app AEM Mobile, esistono tre ruoli diversi:

* Administrator
* Sviluppatore
* Authoring

Per ulteriori informazioni sulla creazione di ruoli con autorizzazioni diverse, ad esempio per la creazione di app o per la creazione e la pubblicazione di contenuto, fate clic su [Creazione di ruoli utente e concessione dell&#39;accesso](https://helpx.adobe.com/digital-publishing-solution/help/account-admin-dps.html) nell&#39;Aiuto di AEM Mobile.

>[!NOTE]
>
>La gestione dei contenuti delle app richiede un impegno collettivo da parte di sviluppatori, autori di contenuti e amministratori. Gli autori modificano le pagine, che a loro volta si basano su modelli e componenti generati dagli sviluppatori di app. Infine, gli amministratori pubblicano strategicamente il contenuto dell&#39;app aggiornata. L’impostazione di gruppi AEM e autorizzazioni definisce i loro ruoli nel dashboard dell’app o nel Centro di controllo.
>
>Per ulteriori informazioni su AEM Mobile Dashboard, fate clic [qui](/help/mobile/mobile-apps-ondemand-application-dashboard.md).

Dopo aver creato ruoli con autorizzazioni diverse, ad esempio per la creazione di app o per la creazione e la pubblicazione di contenuto, consultate [**Configurare i gruppi **](/help/mobile/aem-mobile-configure-users.md)utenti e utenti per configurare utenti e gruppi in modo da supportare la creazione e la gestione delle app mobili.

### Additional Resources {#additional-resources}

Per ulteriori informazioni sugli altri due ruoli e responsabilità per la creazione di un&#39;app AEM Mobile On-Demand Services, consultate le risorse seguenti:

* [Sviluppo di contenuto AEM per i servizi on-demand AEM Mobile](/help/mobile/aem-mobile-on-demand.md)
* [Creazione di contenuti AEM per AEM Mobile On-Demand Services App](/help/mobile/mobile-apps-ondemand.md)

>[!NOTE]
>
>Per un&#39;anteprima del contenuto dell&#39;app, comprese le pagine di ricerca e gli articoli, consultate [Anteprima con verifica preliminare](/help/mobile/aem-mobile-manage-ondemand-services.md).
