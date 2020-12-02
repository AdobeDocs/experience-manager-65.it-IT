---
title: ' configurazione AEM Mobile'
seo-title: ' configurazione AEM Mobile'
description: Seguite questa pagina per configurare  AEM Mobile e consentire all'utente di creare e gestire il contenuto all'interno di AEM. Questa pagina fornisce informazioni sull’integrazione dell’istanza AEM con l’account AEM Mobile On-demand Services  basato su cloud e i progetti.
seo-description: Seguite questa pagina per configurare  AEM Mobile e consentire all'utente di creare e gestire il contenuto all'interno di AEM. Questa pagina fornisce informazioni sull’integrazione dell’istanza AEM con l’account AEM Mobile On-demand Services  basato su cloud e i progetti.
uuid: 03bf5b56-7750-4f76-b079-43761367655a
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-on-demand-services-app
discoiquuid: 393cf504-917e-4bf6-9a8b-b7a5bd862c65
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '990'
ht-degree: 1%

---


#  AEM Mobile SetUp{#aem-mobile-setup}

>[!NOTE]
>
> Adobe consiglia di utilizzare l&#39;editor SPA per i progetti che richiedono il rendering lato client basato sul framework dell&#39;applicazione a pagina singola (ad es. React). [Per saperne di più](/help/sites-developing/spa-overview.md).

>[!CAUTION]
>
>I clienti esistenti  app AEM Mobile che eseguono la migrazione da AEM 6.2 o 6.3 a AEM 6.5 possono continuare a utilizzare  app AEM Mobile scaricando un [pacchetto da PackageShare](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq640/compatpack/aem-mobile-package). Tuttavia, le nuove installazioni di AEM 6.5 non supporteranno  funzionalità delle app AEM Mobile.

Per utilizzare AEM per produrre contenuto per  app AEM Mobile, è necessario integrare l&#39;istanza AEM con l&#39;account AEM Mobile On-demand Services  basato su cloud e i progetti.

Attenetevi a questa procedura per configurare  AEM Mobile e consentire quindi all&#39;utente di creare e gestire il contenuto all&#39;interno di AEM.

##  AEM Mobile Provisioning {#aem-mobile-provisioning}

Per iniziare  configurazione di AEM Mobile, è necessario:

* **Richiedete una chiave** API: Per accedere a On-Demand Services API, è necessario richiedere una chiave API. Per richiedere la chiave API, completare il modulo [PDF](https://helpx.adobe.com/digital-publishing-solution/help/integrating-dps.html). Inviate il modulo compilato all&#39;Assistenza sviluppatori  Adobe: [wwds@adobe.com](mailto:wwds@adobe.com)

* **Generate l&#39;ID dispositivo e il token** dispositivo: Dopo aver ricevuto la chiave API, potete generare l&#39;ID dispositivo e il token dispositivo. Andate a https://aex.aemmobile.adobe.com[](https://aex.aemmobile.adobe.com/) ed effettuate le seguenti operazioni:

   * Fornite la chiave API
   * Effettua l’accesso con un Adobe ID  che hai aggiunto a un progetto AEM Mobile  con le seguenti autorizzazioni (vedi i passaggi sottostanti per creare un progetto)

      * Amministrazione > Gestisci progetti e utenti
      * Contenuto > Aggiungi e modifica contenuto, Elimina contenuto, Visualizza contenuto, Pubblica contenuto

Se tutte le condizioni sono soddisfatte, verranno generati un ID dispositivo e un Token dispositivo.

>[!NOTE]
>
>È necessario concedere all&#39;Adobe ID  l&#39;accesso su un progetto AEM Mobile . Consulta [Amministrazione account per  AEM Mobile](https://helpx.adobe.com/digital-publishing-solution/help/account-admin-dps.html) nella Guida in linea.

## Creazione di progetti per  AEM Mobile {#creating-projects-for-aem-mobile}

Quando create un progetto, specificate le impostazioni per qualsiasi piattaforma di destinazione: iOS, Android, Windows e Desktop Web Viewer. Molte delle impostazioni di progetto specificate influiscono sul comportamento dell&#39;app.

La creazione di un progetto richiede l&#39;accesso al portale dei servizi on-demand utilizzando un Adobe ID  con un ruolo Amministratore principale. La modifica di un progetto richiede un ruolo Amministratore principale o un ruolo utente con un&#39;autorizzazione **Gestisci progetti e utenti**.

>[!NOTE]
>
>Per ulteriori informazioni sulla creazione di progetti in  AEM Mobile, fare clic su [qui](https://helpx.adobe.com/digital-publishing-solution/help/creating-projects.html).

## Configurazione di un connettore AEM Mobile  {#configuring-an-aem-mobile-connector}

AEM configurazione prevede i seguenti passaggi per la configurazione del connettore. Una volta completata la configurazione del connettore AEM Mobile , l&#39;utente può impostare gruppi di utenti e autorizzazioni.

Il connettore AEM Mobile On-Demand  viene utilizzato per collegare  contenuto gestito da AEM Mobile ai servizi on-demand di Adobe Experience Manager Mobile. In questo modo gli autori dei contenuti possono creare e gestire il materiale per le applicazioni mobili utilizzando gli strumenti di AEM e utilizzando  servizi on-demand di AEM Mobile per una facile distribuzione dei contenuti mobili.

>[!NOTE]
>
>Si tratta di un unico passaggio per impostare l&#39;istanza AEM.

### Configurazione  client AEM Mobile On-demand Services {#configuring-aem-mobile-on-demand-services-client}

Per consentire il corretto funzionamento delle integrazioni AEM Mobile , è necessario completare i passaggi di configurazione.

1. Vai alla configurazione del servizio OSGI

   1. AEM > Strumenti > Operazioni > Console Web
   1. Scorrere o cercare ***Experience Manager Mobile On-demand Services Client (era  Adobe Digital Publishing Solution Client)***

1. Modifica ***Experience Manager Mobile On-demand Services Client***

   1. **(Obbligatorio)** Immettere i campi obbligatori:

      1. ID client.
      1. Segreto client.
   1. **(Facoltativo)** Modificate i valori esistenti.


1. Salva le modifiche.
1. Esempio di configurazione:

![chlimage_1-53](assets/chlimage_1-53.png)

### Configurazione  AEM Mobile On-demand Services Cloud Service {#configuring-aem-mobile-on-demand-services-cloudservice}

1. Vai ai Cloud Services

   1. AEM > Strumenti > Distribuzione> [CloudServices](http://localhost:4502/libs/cq/core/content/tools/cloudservices.html). Scorrere o cercare ***Adobe Experience Manager Mobile On-demand Services***

1. Selezionare ***Configura ora*** o ***Mostra configurazioni*** e selezionare l&#39;icona Aggiungi nuova configurazione

1. Creare una nuova configurazione

   1. Immettere un titolo e un nome
   1. Immetti ID dispositivo
   1. Immetti token dispositivo
   1. Selezionare ***Verifica configurazione dispositivo*** per convalidare i valori immessi
   1. Seleziona OK

## Aggiunta  ruoli utente AEM Mobile e assegnazione delle autorizzazioni {#adding-aem-mobile-user-roles-and-assigning-permissions}

Dopo aver creato un progetto è necessario creare ruoli e concedere l&#39;accesso agli utenti. Solo gli Amministratori principali possono creare e modificare i ruoli. Quando create un ruolo, abilitate le capacità (o autorizzazioni) per tutti gli utenti a cui sono assegnate tali autorizzazioni. Ad esempio, potete creare un ruolo che include le autorizzazioni per la creazione di app e un altro ruolo che include le autorizzazioni per la creazione e la pubblicazione di contenuto.

Nello sviluppo  app AEM Mobile, esistono tre ruoli diversi:

* Administrator
* Developer (Sviluppatore)
* Autore

Per ulteriori informazioni sulla creazione di ruoli con autorizzazioni diverse, ad esempio per la creazione di app o per la creazione e la pubblicazione di contenuto, fate clic su [Creazione di ruoli utente e concessione di accesso](https://helpx.adobe.com/digital-publishing-solution/help/account-admin-dps.html) nella  Guida di AEM Mobile.

>[!NOTE]
>
>La gestione dei contenuti delle app richiede un impegno collettivo da parte di sviluppatori, autori di contenuti e amministratori. Gli autori modificano le pagine, che a loro volta si basano su modelli e componenti generati dagli sviluppatori di app. Infine, gli amministratori pubblicano strategicamente il contenuto dell&#39;app aggiornata. L&#39;impostazione AEM gruppi e autorizzazioni definisce i loro ruoli nel dashboard dell&#39;app o nel Centro di controllo.
>
>Per ulteriori informazioni su  AEM Mobile Dashboard, fare clic su [qui](/help/mobile/mobile-apps-ondemand-application-dashboard.md).

Dopo aver creato ruoli con autorizzazioni diverse, ad esempio per la creazione di app o per la creazione e la pubblicazione di contenuto, consultate [**Configurare i gruppi utenti e utenti**](/help/mobile/aem-mobile-configure-users.md) per configurare utenti e gruppi in modo da supportare la creazione e la gestione delle app mobili.

### Risorse aggiuntive {#additional-resources}

Per ulteriori informazioni sugli altri due ruoli e responsabilità per la creazione di un&#39;app AEM Mobile On-demand Services , consulta le risorse seguenti:

* [Sviluppo AEM contenuto per  AEM Mobile On-demand Services](/help/mobile/aem-mobile-on-demand.md)
* [Creazione AEM contenuto per  app AEM Mobile On-demand Services](/help/mobile/mobile-apps-ondemand.md)

>[!NOTE]
>
>Per un&#39;anteprima dei contenuti dell&#39;app, comprese le pagine di ricerca e gli articoli, vedete [Anteprima con Preflight](/help/mobile/aem-mobile-manage-ondemand-services.md).
