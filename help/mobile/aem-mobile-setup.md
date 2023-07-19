---
title: Configurazione AEM Mobile
seo-title: AEM Mobile SetUp
description: Segui questa pagina per configurare AEM Mobile e consentire quindi all’utente di creare e gestire il contenuto all’interno dell’AEM. Questa pagina fornisce informazioni sull’integrazione dell’istanza AEM con l’account AEM Mobile On-demand Services basato su cloud e i progetti.
seo-description: Follow this page for setting up AEM Mobile and thus allowing the user to create and manage the content within AEM. This page provides information on integrating the AEM instance with the cloud-based AEM Mobile On-Demand Services account and project(s).
uuid: 03bf5b56-7750-4f76-b079-43761367655a
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-on-demand-services-app
discoiquuid: 393cf504-917e-4bf6-9a8b-b7a5bd862c65
exl-id: 0ead982d-2315-4947-b762-596aa2aa42a1
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '929'
ht-degree: 2%

---

# Configurazione AEM Mobile{#aem-mobile-setup}

>[!NOTE]
>
>L’Adobe consiglia di utilizzare l’Editor SPA per i progetti che richiedono il rendering lato client basato su framework di applicazione a pagina singola (ad esempio, React). [Ulteriori informazioni](/help/sites-developing/spa-overview.md).

>[!CAUTION]
>
>I clienti delle app AEM Mobile esistenti che eseguono la migrazione da AEM 6.2 o 6.3 a AEM 6.5 possono continuare a utilizzare le app AEM Mobile scaricando un pacchetto da PackageShare. Tuttavia, le nuove installazioni di AEM 6.5 non supporteranno la funzionalità delle app AEM Mobile.

Per utilizzare l’AEM per produrre contenuti per le app AEM Mobile, è necessario integrare l’istanza AEM con l’account e i progetti AEM Mobile On-demand Services basati su cloud.

Segui questi passaggi per configurare AEM Mobile e consentire quindi all’utente di creare e gestire i contenuti all’interno dell’AEM.

## Provisioning di AEM Mobile {#aem-mobile-provisioning}

Per iniziare a configurare AEM Mobile, devi:

* **Richiedi una chiave API**: per accedere all’API On-Demand Services, devi richiedere una chiave API. Per richiedere la chiave API, completa la sezione [Modulo PDF](https://helpx.adobe.com/digital-publishing-solution/help/aem-mobile-end-of-life-faq.html). Invia il modulo completato al supporto Adobe Developer: [wwds@adobe.com](mailto:wwds@adobe.com)

* **Generare l&#39;ID dispositivo e il token dispositivo**: dopo aver ricevuto la chiave API, puoi generare l’ID dispositivo e il token dispositivo. Vai a `https://aex.aemmobile.adobe.com` ed effettuare le seguenti operazioni:

   * Fornisci la chiave API
   * Accedi con un Adobe ID aggiunto a un progetto AEM Mobile con le seguenti autorizzazioni (vedi i passaggi seguenti per creare un progetto)

      * Amministrazione > Gestisci progetti e utenti
      * Contenuto > Aggiungi e modifica contenuto, Elimina contenuto, Visualizza contenuto, Pubblica contenuto

Se tutte le condizioni sono soddisfatte, verranno generati un ID dispositivo e un token dispositivo.

>[!NOTE]
>
>L’Adobe ID necessario deve poter accedere a un progetto AEM Mobile. Consulta [Amministrazione account per AEM Mobile](https://helpx.adobe.com/digital-publishing-solution/help/aem-mobile-end-of-life-faq.html) nella Guida in linea.

## Creazione di progetti per AEM Mobile {#creating-projects-for-aem-mobile}

Quando si crea un progetto, si specificano le impostazioni per qualsiasi piattaforma di destinazione: iOS, Android, Windows e Visualizzatore Web per desktop. Molte delle impostazioni di progetto specificate influiscono sul comportamento dell’app.

La creazione di un progetto richiede l’accesso al portale dei servizi on-demand utilizzando un Adobe ID con il ruolo Amministratore principale. La modifica di un progetto richiede un ruolo Amministratore principale o un ruolo utente con un **Gestione di progetti e utenti** autorizzazione.

>[!NOTE]
>
>Per ulteriori informazioni sulla creazione di progetti in AEM Mobile, fai clic su [qui](https://helpx.adobe.com/digital-publishing-solution/help/creating-projects.html).

## Configurazione di un connettore AEM Mobile {#configuring-an-aem-mobile-connector}

La configurazione dell’AEM prevede i seguenti passaggi per la configurazione del connettore. Una volta completata la configurazione del connettore AEM Mobile, l’utente può impostare gruppi di utenti e autorizzazioni.

Il connettore AEM Mobile On-Demand viene utilizzato per associare il contenuto gestito di AEM Mobile ai servizi Adobe Experience Manager Mobili On-Demand. Questo consente agli autori di contenuti di creare e gestire il materiale per le applicazioni mobili utilizzando gli strumenti AEM, mentre utilizzano i servizi AEM Mobile On-Demand per una facile distribuzione dei contenuti mobili.

>[!NOTE]
>
>Questo è un passaggio unico per configurare l’istanza dell’AEM.

### Configurazione del client AEM Mobile On-demand Services {#configuring-aem-mobile-on-demand-services-client}

Per il corretto funzionamento delle integrazioni AEM Mobile, devi completare i passaggi di configurazione.

1. Vai alla configurazione del servizio OSGI

   1. AEM > Strumenti > Operazioni > Console web
   1. Scorri o cerca ***Client Experience Manager Mobile On-demand Services (era client Adobe Digital Publishing Solution)***

1. Modifica ***Client Experience Manager Mobile On-demand Services***

   1. **(Obbligatorio)** Immettere i campi obbligatori:

      1. ID client.
      1. Segreto client.

   1. **(Facoltativo)** Modifica i valori esistenti.

1. Salva le modifiche.
1. Di seguito è riportata una configurazione di esempio:

![chlimage_1-53](assets/chlimage_1-53.png)

### Configurazione di AEM Mobile On-demand Services Cloud Service {#configuring-aem-mobile-on-demand-services-cloudservice}

1. Vai a Cloud Services

   1. AEM > Strumenti > Implementazione > [CloudServices](http://localhost:4502/libs/cq/core/content/tools/cloudservices.html). Scorri o cerca ***Servizi on-demand Adobe Experience Manager Mobili***

1. Seleziona ***Configura ora*** o ***Mostra configurazioni*** e seleziona l’icona aggiungi nuova configurazione

1. Crea una nuova configurazione

   1. Inserisci un titolo e un nome
   1. Immetti ID dispositivo
   1. Immetti token dispositivo
   1. Seleziona ***Prova configurazione dispositivo*** per convalidare i valori immessi
   1. Seleziona Ok

## Aggiunta di ruoli utente e assegnazione di autorizzazioni di AEM Mobile {#adding-aem-mobile-user-roles-and-assigning-permissions}

Dopo aver creato un progetto è necessario creare ruoli e concedere l’accesso agli utenti. Solo gli amministratori principali possono creare e modificare i ruoli. Quando si crea un ruolo, si abilitano le funzionalità o le autorizzazioni per gli utenti a cui sono assegnate tali autorizzazioni. Ad esempio, puoi creare un ruolo che include le autorizzazioni per la creazione di app e un altro ruolo che include le autorizzazioni per la creazione e la pubblicazione di contenuti.

Nello sviluppo di app AEM Mobile, esistono tre ruoli diversi:

* Amministratore
* Sviluppatore
* Autore

Per ulteriori informazioni sulla creazione di ruoli con autorizzazioni diverse, ad esempio per la creazione di app o per la creazione e pubblicazione di contenuti, fai clic su [Creazione di ruoli utente e concessione dell&#39;accesso](https://helpx.adobe.com/digital-publishing-solution/help/account-admin-dps.html) nella Guida di AEM Mobile.

>[!NOTE]
>
>La gestione dei contenuti delle app richiede uno sforzo collettivo da parte di sviluppatori, autori e amministratori di contenuti. Gli autori manipolano le pagine, che a loro volta si basano su modelli e componenti generati dagli sviluppatori di app. Infine, gli amministratori pubblicano in modo strategico il contenuto aggiornato dell’app. La configurazione di gruppi e autorizzazioni AEM definisce i loro ruoli nel dashboard o nel centro di controllo dell’app.
>
>Per ulteriori informazioni su AEM Mobile Dashboard, fai clic su [qui](/help/mobile/mobile-apps-ondemand-application-dashboard.md).

Dopo aver creato i ruoli con autorizzazioni diverse, ad esempio per la creazione di app o per la creazione e la pubblicazione di contenuti, consulta [**Configurare utenti e gruppi di utenti**](/help/mobile/aem-mobile-configure-users.md) per configurare utenti e gruppi in modo da supportare l’authoring e la gestione delle app mobili.

### Risorse aggiuntive {#additional-resources}

Per ulteriori informazioni sugli altri due ruoli e responsabilità per la creazione di un’app AEM Mobile On-demand Services, consulta le risorse seguenti:

* [Sviluppo di contenuti AEM per AEM Mobile On-demand Services](/help/mobile/aem-mobile-on-demand.md)
* [Creazione di contenuti AEM per l’app AEM Mobile On-demand Services](/help/mobile/mobile-apps-ondemand.md)

>[!NOTE]
>
>Per visualizzare in anteprima il contenuto dell’app, incluse le pagine e gli articoli, consulta [Anteprima con verifica preliminare](/help/mobile/aem-mobile-manage-ondemand-services.md).
