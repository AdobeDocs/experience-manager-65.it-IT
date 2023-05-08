---
title: Configurazione AEM Mobile
seo-title: AEM Mobile SetUp
description: Segui questa pagina per configurare AEM Mobile e consentire all’utente di creare e gestire il contenuto all’interno di AEM. Questa pagina fornisce informazioni sull’integrazione dell’istanza AEM con l’account AEM Mobile On-demand Services basato su cloud e i progetti.
seo-description: Follow this page for setting up AEM Mobile and thus allowing the user to create and manage the content within AEM. This page provides information on integrating the AEM instance with the cloud-based AEM Mobile On-Demand Services account and project(s).
uuid: 03bf5b56-7750-4f76-b079-43761367655a
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-on-demand-services-app
discoiquuid: 393cf504-917e-4bf6-9a8b-b7a5bd862c65
exl-id: 0ead982d-2315-4947-b762-596aa2aa42a1
source-git-commit: 85d39e59b82fdfdcd310be61787a315668aebe38
workflow-type: tm+mt
source-wordcount: '928'
ht-degree: 2%

---

# Configurazione AEM Mobile{#aem-mobile-setup}

>[!NOTE]
>
>Adobe consiglia di utilizzare l’editor di SPA per i progetti che richiedono il rendering lato client basato sul framework di un’applicazione a pagina singola (ad esempio, React). [Ulteriori informazioni](/help/sites-developing/spa-overview.md).

>[!CAUTION]
>
>I clienti esistenti delle app AEM Mobile che eseguono la migrazione da AEM 6.2 o 6.3 a AEM 6.5 possono continuare a utilizzare le app AEM Mobile scaricando un pacchetto da PackageShare. Tuttavia, le nuove installazioni di AEM 6.5 non supporteranno la funzionalità delle app AEM Mobile.

Per utilizzare AEM per produrre contenuti per le app AEM Mobile, è necessario integrare l’istanza AEM con l’account AEM Mobile On-demand Services basato su cloud e i progetti.

Segui questi passaggi per configurare AEM Mobile e consentire all’utente di creare e gestire il contenuto all’interno di AEM.

## Provisioning AEM Mobile {#aem-mobile-provisioning}

Per iniziare a utilizzare la configurazione di AEM Mobile, devi:

* **Richiedere una chiave API**: Per accedere all’API dei servizi on-demand, devi richiedere una chiave API. Per richiedere la chiave API, completa il [modulo PDF](https://helpx.adobe.com/digital-publishing-solution/help/aem-mobile-end-of-life-faq.html). Invia il modulo completato all’Assistenza Adobe Developer: [wwds@adobe.com](mailto:wwds@adobe.com)

* **Generare l’ID dispositivo e il token dispositivo**: Dopo aver ricevuto la chiave API, puoi generare l’ID dispositivo e il token dispositivo. Vai a `https://aex.aemmobile.adobe.com` e procedi come segue:

   * Fornisci la chiave API
   * Accedi con un Adobe ID aggiunto a un progetto AEM Mobile con le seguenti autorizzazioni (vedi i passaggi seguenti per creare un progetto)

      * Amministrazione > Gestione progetti e utenti
      * Contenuto > Aggiungi e modifica contenuto, Elimina contenuto, Visualizza contenuto, Pubblica contenuto

Se tutte le condizioni sono soddisfatte, verranno generati un ID dispositivo e un token dispositivo.

>[!NOTE]
>
>È necessario concedere l’accesso ad Adobe ID in un progetto AEM Mobile. Vedi [Amministrazione account per AEM Mobile](https://helpx.adobe.com/digital-publishing-solution/help/aem-mobile-end-of-life-faq.html) nella Guida in linea.

## Creazione di progetti per AEM Mobile {#creating-projects-for-aem-mobile}

Quando crei un progetto, specifica le impostazioni per qualsiasi piattaforma di destinazione: Visualizzatore Web iOS, Android, Windows e Desktop. Molte delle impostazioni di progetto specificate influiscono sul comportamento dell’app.

La creazione di un progetto richiede l’accesso al portale dei servizi on-demand utilizzando un Adobe ID con un ruolo Amministratore principale. La modifica di un progetto richiede un ruolo Amministratore principale o un ruolo utente con un **Gestione di progetti e utenti** autorizzazione.

>[!NOTE]
>
>Per ulteriori informazioni sulla creazione di progetti in AEM Mobile, fai clic su [qui](https://helpx.adobe.com/digital-publishing-solution/help/creating-projects.html).

## Configurazione di un connettore AEM Mobile {#configuring-an-aem-mobile-connector}

AEM configurazione prevede i seguenti passaggi per la configurazione del connettore. Una volta completata la configurazione del connettore AEM Mobile, l’utente può impostare gruppi di utenti e autorizzazioni.

Il connettore AEM Mobile On-Demand viene utilizzato per associare il contenuto gestito da AEM Mobile ai servizi on-demand di Adobe Experience Manager Mobile. Questo consente agli autori dei contenuti di creare e gestire il materiale per le applicazioni mobili utilizzando strumenti AEM e i servizi on-demand di AEM Mobile per una facile distribuzione dei contenuti mobili.

>[!NOTE]
>
>Questo è un unico passaggio per configurare l&#39;istanza AEM.

### Configurazione del client AEM Mobile On-demand Services {#configuring-aem-mobile-on-demand-services-client}

Devi completare i passaggi di configurazione affinché le integrazioni AEM Mobile funzionino correttamente.

1. Vai alla configurazione del servizio OSGI

   1. AEM > Strumenti > Operazioni > Console web
   1. Scorrere o cercare ***Client Experience Manager Mobile On-demand Services (era Adobe Digital Publishing Solution Client)***

1. Modifica ***Client Experience Manager Mobile On-demand Services***

   1. **(Obbligatorio)** Immetti i campi obbligatori:

      1. ID client.
      1. Segreto client.
   1. **(Facoltativo)** Modifica i valori esistenti.


1. Salva le modifiche.
1. Ecco un esempio di configurazione:

![chlimage_1-53](assets/chlimage_1-53.png)

### Configurazione di AEM Mobile On-demand Services Cloud Service {#configuring-aem-mobile-on-demand-services-cloudservice}

1. Vai a Cloud Services

   1. AEM > Strumenti > Implementazione> [CloudServices](http://localhost:4502/libs/cq/core/content/tools/cloudservices.html). Scorrere o cercare ***Servizi on-demand Adobe Experience Manager Mobile***

1. Seleziona ***Configura ora*** o ***Mostra configurazioni*** e seleziona l’icona aggiungi nuova configurazione

1. Crea una nuova configurazione

   1. Immetti un titolo e un nome
   1. Immetti ID dispositivo
   1. Immettere il token del dispositivo
   1. Seleziona ***Verificare la configurazione del dispositivo*** per convalidare i valori immessi
   1. Seleziona Ok

## Aggiunta di ruoli utente di AEM Mobile e assegnazione di autorizzazioni {#adding-aem-mobile-user-roles-and-assigning-permissions}

Dopo aver creato un progetto, devi creare ruoli e concedere l’accesso agli utenti. Solo gli amministratori principali possono creare e modificare ruoli. Quando crei un ruolo, abiliti le funzionalità (o le autorizzazioni) per tutti gli utenti a cui sono assegnate tali autorizzazioni. Ad esempio, puoi creare un ruolo che include le autorizzazioni per la creazione di app e un altro ruolo che include le autorizzazioni per la creazione e la pubblicazione di contenuti.

Nello sviluppo dell’app AEM Mobile esistono tre ruoli diversi:

* Amministratore
* Sviluppatore
* Autore

Per ulteriori informazioni sulla creazione di ruoli con autorizzazioni diverse, ad esempio per la creazione di app o per la creazione e la pubblicazione di contenuti, fai clic su [Creazione di ruoli utente e concessione dell&#39;accesso](https://helpx.adobe.com/digital-publishing-solution/help/account-admin-dps.html) nell’Aiuto di AEM Mobile.

>[!NOTE]
>
>La gestione dei contenuti delle app richiede uno sforzo collettivo da parte di sviluppatori, autori e amministratori di contenuti. Gli autori manipolano le pagine, che a loro volta si basano su modelli e componenti generati dagli sviluppatori di app. Infine, gli amministratori pubblicano in modo strategico il contenuto aggiornato dell’app. L&#39;impostazione AEM gruppi e autorizzazioni definisce i loro ruoli nel dashboard o nel centro di controllo dell&#39;app.
>
>Per ulteriori informazioni sul dashboard di AEM Mobile, fai clic su [qui](/help/mobile/mobile-apps-ondemand-application-dashboard.md).

Dopo aver creato ruoli con autorizzazioni diverse, ad esempio per la creazione dell’app o per la creazione e la pubblicazione di contenuti, consulta [**Configurare utenti e gruppi di utenti**](/help/mobile/aem-mobile-configure-users.md) per configurare i tuoi utenti e gruppi per supportare la creazione e la gestione delle tue app mobili.

### Risorse aggiuntive {#additional-resources}

Per ulteriori informazioni sugli altri due ruoli e responsabilità per la creazione di un’app AEM Mobile On-demand Services, consulta le risorse seguenti:

* [Sviluppo di contenuti AEM per AEM Mobile On-demand Services](/help/mobile/aem-mobile-on-demand.md)
* [Creazione di contenuti AEM per l’app AEM Mobile On-demand Services](/help/mobile/mobile-apps-ondemand.md)

>[!NOTE]
>
>Per visualizzare in anteprima il contenuto dell&#39;app, comprese le pagine di ricerca e gli articoli, vedi [Anteprima con Preflight](/help/mobile/aem-mobile-manage-ondemand-services.md).
