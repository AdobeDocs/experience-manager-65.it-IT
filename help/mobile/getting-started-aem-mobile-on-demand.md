---
title: AEM Mobile on-demand
seo-title: AEM Mobile On-Demand
description: L’avvio di una nuova esperienza con le app AEM Mobile richiede una combinazione di ruoli prima di essere pronto per la modifica dei contenuti. Segui questa pagina per iniziare a utilizzare AEM servizi on-demand mobili.
seo-description: Starting a new AEM Mobile app experience requires a cohesion of roles before it is ready for content editing. Follow this page to get started with AEM mobile On-Demand services.
uuid: 175c609d-3cb8-4a1b-bfea-278df272e500
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: introduction
content-type: reference
discoiquuid: dc6891cd-19cc-4dff-8bda-a41ed8af8bfb
exl-id: 4be199d8-963d-4807-b9bb-e23fa577c5f2
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '771'
ht-degree: 1%

---

# AEM Mobile on-demand{#aem-mobile-on-demand}

>[!NOTE]
>
>Adobe consiglia di utilizzare l’editor di SPA per i progetti che richiedono il rendering lato client basato sul framework di un’applicazione a pagina singola (ad esempio, React). [Per saperne di più](/help/sites-developing/spa-overview.md).

>[!NOTE]
>
>Se non utilizzi AEM come origine per la gestione dei contenuti, consulta [Guida di AEM Mobile On-demand Services](https://helpx.adobe.com/digital-publishing-solution/topics.html).

AEM fornisce diversi strumenti che consentono di integrare i contenuti nelle applicazioni mobili.

Il diagramma seguente illustra il modo in cui i vari componenti di AEM Mobile e On-Demand Services si integrano per distribuire contenuti alle app mobili.

AEM’app Preflight può essere considerata un ambiente di test per visualizzare in anteprima l’app e il contenuto prima della pubblicazione; mentre l’app AEM Mobile è l’app finale creata per la distribuzione.

>[!NOTE]
>
>Per informazioni approfondite sull’app Preflight, vedi [Utilizzo dell’app AEM Preflight](https://helpx.adobe.com/digital-publishing-solution/help/preflight-app.html) nell’Aiuto di AEM Mobile On-demand Services.

![chlimage_1-171](assets/chlimage_1-171.png)

>[!NOTE]
>
>Nel diagramma precedente, l’istanza AEM Publish non è necessaria per uno scenario di implementazione tipico per AEM Mobile On-demand Services.

## Avvio di una nuova app mobile {#starting-a-new-mobile-app}

AEM Mobile è solo uno dei pilastri che costituisce la piattaforma AEM completa.

L’avvio di una nuova esperienza con le app AEM Mobile richiede una combinazione di ruoli prima di essere pronto per la modifica dei contenuti. I seguenti ruoli forniscono un punto di partenza per la creazione di una nuova applicazione AEM Mobile:

* **Amministratore**
* **Sviluppatore**
* **Autore**

>[!NOTE]
>
>Prima di lavorare con AEM Mobile e di seguire i passaggi descritti in questa guida introduttiva, gli utenti devono avere familiarità con AEM. Scopri le basi di AEM [qui](/help/sites-deploying/deploy.md).

### Informazioni sul dashboard dell’applicazione AEM Mobile {#understanding-the-aem-mobile-application-dashboard}

Prima di comprendere i ruoli e le responsabilità, l’utente deve avere una conoscenza approfondita dei **Centro di controllo AEM Mobile** o **Dashboard dell&#39;applicazione**. Fai clic su [qui](/help/mobile/mobile-apps-ondemand-application-dashboard.md) per una comprensione approfondita.

### Amministratore AEM {#aem-administrator}

Un ***Amministratore AEM*** è responsabile dell’aggiunta di una nuova applicazione al catalogo AEM Mobile, tramite la creazione di una nuova app tramite la procedura guidata di creazione o l’importazione di un’applicazione esistente. Amministratori AEM che creano una nuova app utilizzando AEM Mobile *creazione guidata* in genere seleziona uno dei modelli di app desiderati dai nostri esempi di riferimento predefiniti o (nella maggior parte dei casi) un modello di app personalizzato creato da *Sviluppatori AEM.*

Durante la creazione di un’app tramite AEM Mobile On-demand Services, un amministratore AEM è responsabile delle seguenti attività:

* [Configurazione di AEM Mobile](/help/mobile/aem-mobile-setup.md)
* [Configurazione di utenti e gruppi di utenti](/help/mobile/aem-mobile-configure-users.md)
* [Anteprima con Preflight](/help/mobile/aem-mobile-manage-ondemand-services.md)
* [Amministrazione dei servizi di contenuti](/help/mobile/developing-content-services.md)

Per iniziare a utilizzare i ruoli e le responsabilità di un amministratore, consulta [Amministrazione di contenuti per l’utilizzo di AEM Mobile On-demand Services](/help/mobile/aem-mobile.md).

## Sviluppatore AEM {#aem-developer}

Un **sviluppatore AEM** estende e crea modelli web e componenti personalizzati per consentire a *AEM Author *di creare esperienze mobili belle e coinvolgenti. Questi modelli e componenti non sono ottimizzati solo per il mondo delle app mobili; ma comunicare sia al dispositivo che al server AEM (qualsiasi server remoto) agli endpoint del servizio omni-channel. AEM editor di contenuti incorporati viene utilizzato da *Autori AEM* per creare esperienze avanzate e rilevanti all’interno dell’app, inclusa l’integrazione con il resto di Adobe Marketing Cloud.

Durante la creazione di un’app tramite AEM Mobile On-demand Services, uno sviluppatore AEM è responsabile delle seguenti attività:

* [Modelli e componenti per app](/help/mobile/app-templates-and-components1.md)
* [Mobile con sincronizzazione dei contenuti](/help/mobile/mobile-ondemand-contentsync.md)
* [Proprietà del contenuto ed esportazione del contenuto](/help/mobile/on-demand-content-properties-exporting.md)
* [Sviluppo di servizi per contenuti AEM Mobile](/help/mobile/developing-content-services.md)

Per iniziare a utilizzare i ruoli e le responsabilità degli sviluppatori, consulta [Sviluppo di contenuti AEM per AEM Mobile On-demand Services](/help/mobile/aem-mobile-on-demand.md).

>[!NOTE]
>
>Un *AEM* Il ruolo non inizia e termina con lo sviluppo di modelli e componenti. Un *sviluppatore AEM* può creare un’app completamente nuova, anziché estendere semplicemente l’esempio di implementazione di riferimento predefinito.

## Autore AEM {#aem-author}

Un ***AEM Author* o *Addetto marketing*)**utilizza modelli e componenti personalizzati sviluppati o predefiniti per aggiungere e modificare pagine, trascinare componenti e aggiungere file multimediali di tutti i tipi dal DAM, incluse immagini, video e frammenti di testo (frammenti di contenuto). AEM editor di contenuti incorporati viene quindi utilizzato da *Autori AEM* per creare esperienze avanzate e rilevanti all’interno dell’app, inclusa l’integrazione con il resto di Adobe Marketing Cloud.

Un autore AEM deve comprendere i seguenti argomenti durante la creazione di un’app tramite AEM Mobile On-demand Services:

* [Dashboard dell&#39;applicazione AEM Mobile](/help/mobile/mobile-apps-ondemand-application-dashboard.md)
* [Azioni di creazione e configurazione delle applicazioni](/help/mobile/mobile-apps-ondemand-application-create-configure-action.md)
* [Configurazione cloud](/help/mobile/mobile-on-demand-associating-an-on-demand-app-to-cloud-configuration.md)
* [Gestione dei contenuti](/help/mobile/mobile-apps-ondemand-manage-content-ondemand.md)
* [Panoramica dei servizi di contenuto](/help/mobile/develop-content-as-a-service.md)

Per iniziare a utilizzare i ruoli e le responsabilità di un autore, consulta [Creazione di contenuti AEM per l’app AEM Mobile On-demand Services](/help/mobile/mobile-apps-ondemand.md).

>[!NOTE]
>
>Un autore di AEM è anche responsabile della configurazione dell’adesione, della creazione di schede e layout e dell’invio di notifiche push. Inoltre, per ulteriori informazioni sui metodi di authoring dei contenuti, la gestione degli articoli e delle collezioni; creazione di banner, schede e layout in AEM Mobile, vedi [AEM Mobile On-Demand Portal](https://helpx.adobe.com/digital-publishing-solution/topics.html#dynamicpod_reference_2).
