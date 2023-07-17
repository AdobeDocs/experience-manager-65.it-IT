---
title: Adobe Experience Manager Mobili On-Demand
description: L’avvio di una nuova esperienza di app mobile Adobe Experience Manager (AEM) richiede una coerenza di ruoli prima di essere pronta per la modifica dei contenuti. Segui questa pagina per iniziare a utilizzare i servizi mobili on-demand dell’AEM.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: introduction
content-type: reference
exl-id: 4be199d8-963d-4807-b9bb-e23fa577c5f2
source-git-commit: 96e2e945012046e6eac878389b7332985221204e
workflow-type: tm+mt
source-wordcount: '772'
ht-degree: 1%

---

# AEM Mobile On-Demand{#aem-mobile-on-demand}

>[!NOTE]
>
>L’Adobe consiglia di utilizzare l’Editor SPA per i progetti che richiedono il rendering lato client basato su framework di applicazione a pagina singola (ad esempio, React). [Ulteriori informazioni](/help/sites-developing/spa-overview.md).

>[!NOTE]
>
>Se non utilizzi Adobe Experience Manager (AEM) come origine per la gestione dei contenuti, consulta [Guida di AEM Mobile On-demand Services](https://helpx.adobe.com/digital-publishing-solution/topics.html).

AEM fornisce diversi strumenti che consentono di integrare i contenuti nelle applicazioni mobili.

Il diagramma seguente illustra come i vari componenti di AEM Mobile e On-Demand Services si integrano per distribuire contenuti alle app mobili.

L’app Verifica preliminare AEM può essere considerata un ambiente di test per visualizzare in anteprima l’app e il contenuto prima della pubblicazione; mentre l’app AEM Mobile è l’app finale creata per la distribuzione.

>[!NOTE]
>
>Per informazioni approfondite sull’app Verifica preliminare, consulta [Utilizzo dell’app Verifica preliminare AEM](https://helpx.adobe.com/digital-publishing-solution/help/preflight-app.html) nella Guida di AEM Mobile On-demand Services.

![chlimage_1-171](assets/chlimage_1-171.png)

>[!NOTE]
>
>Nel diagramma precedente, l’istanza AEM Publish non è necessaria per uno scenario di distribuzione tipico in AEM Mobile On-demand Services.

## Avvio di una nuova app mobile {#starting-a-new-mobile-app}

AEM Mobile è solo uno dei pilastri che compongono l&#39;intera piattaforma AEM.

L’avvio di una nuova esperienza di app AEM Mobile richiede una coerenza di ruoli prima di essere pronta per la modifica dei contenuti. I seguenti ruoli forniscono un punto di partenza per la creazione di un’applicazione AEM Mobile:

* **Amministratore**
* **Sviluppatore**
* **Autore**

>[!NOTE]
>
>Prima di lavorare con AEM Mobile e seguire i passaggi descritti in questa guida introduttiva, gli utenti devono avere familiarità con l’AEM. Scopri le nozioni di base dell’AEM [qui](/help/sites-deploying/deploy.md).

### Informazioni sul dashboard dell’applicazione AEM Mobile {#understanding-the-aem-mobile-application-dashboard}

Prima di comprendere i ruoli e le responsabilità, l’utente deve conoscere a fondo **Centro controllo AEM Mobile** o **Dashboard applicazione**. Clic [qui](/help/mobile/mobile-apps-ondemand-application-dashboard.md) per una comprensione approfondita.

### Amministratore AEM {#aem-administrator}

Un ***Amministratore AEM*** è responsabile dell’aggiunta di un’applicazione al catalogo AEM Mobile, tramite la creazione guidata di un’app o l’importazione di un’applicazione esistente. Amministratori AEM che creano un’app utilizzando AEM Mobile *creazione guidata* in genere, seleziona uno dei modelli di app desiderati dagli esempi di riferimento predefiniti di Adobe o (in genere) da un modello di app personalizzato creato da *Sviluppatori AEM.*

Un amministratore AEM è responsabile delle seguenti attività durante la creazione di un’app tramite AEM Mobile On-demand Services:

* [Configurazione di AEM Mobile](/help/mobile/aem-mobile-setup.md)
* [Configurazione degli utenti e dei gruppi di utenti](/help/mobile/aem-mobile-configure-users.md)
* [Anteprima con verifica preliminare](/help/mobile/aem-mobile-manage-ondemand-services.md)
* [Amministrazione di Content Services](/help/mobile/developing-content-services.md)

Per iniziare a utilizzare i ruoli e le responsabilità di un amministratore, consulta [Amministrazione di contenuti per l’utilizzo di AEM Mobile On-demand Services](/help/mobile/aem-mobile.md).

## Sviluppatore AEM {#aem-developer}

Un **Sviluppatore AEM** estende e crea modelli web e componenti personalizzati per consentire a *AEM Author *di creare esperienze mobili belle e coinvolgenti. Questi modelli e componenti non sono ottimizzati solo per il mondo delle app mobili, ma comunicano sia con il dispositivo che con il server AEM (qualsiasi server remoto) agli endpoint del servizio omni-channel. L’editor di contenuti integrato AEM viene utilizzato da *Autori AEM* creare esperienze avanzate e pertinenti all’interno dell’app, inclusa l’integrazione con il resto di Adobe Experience Cloud.

Uno sviluppatore AEM è responsabile delle seguenti attività durante la creazione di un’app tramite AEM Mobile On-demand Services:

* [Modelli di app e componenti](/help/mobile/app-templates-and-components1.md)
* [Dispositivi mobili con sincronizzazione contenuti](/help/mobile/mobile-ondemand-contentsync.md)
* [Proprietà del contenuto ed esportazione del contenuto](/help/mobile/on-demand-content-properties-exporting.md)
* [Sviluppo di AEM Mobile Content Services](/help/mobile/developing-content-services.md)

Per iniziare a utilizzare i ruoli e le responsabilità dello sviluppatore, consulta [Sviluppo di contenuti AEM per AEM Mobile On-demand Services](/help/mobile/aem-mobile-on-demand.md).

>[!NOTE]
>
>Un *Sviluppatore AEM* Il ruolo non inizia e termina con lo sviluppo di modelli e componenti. Un *Sviluppatore AEM* può creare un’app completamente nuova anziché semplicemente estendere l’esempio di implementazione di riferimento fornito con la soluzione.

## Autore AEM {#aem-author}

Un ***Autore AEM* (o *Addetto marketing*)**utilizza modelli e componenti personalizzati sviluppati o pronti all’uso per aggiungere e modificare pagine, trascinare e rilasciare componenti e aggiungere contenuti multimediali di tutti i tipi da DAM, incluse immagini, video e frammenti di testo (frammenti di contenuto). L’editor di contenuti integrato AEM viene quindi utilizzato da *Autori AEM* creare esperienze avanzate e pertinenti all’interno dell’app, inclusa l’integrazione con il resto di Adobe Experience Cloud.

Un autore AEM deve comprendere i seguenti argomenti durante la creazione di un’app tramite AEM Mobile On-demand Services:

* [Dashboard dell’applicazione AEM Mobile](/help/mobile/mobile-apps-ondemand-application-dashboard.md)
* [Azioni di creazione e configurazione delle applicazioni](/help/mobile/mobile-apps-ondemand-application-create-configure-action.md)
* [Configurazione cloud](/help/mobile/mobile-on-demand-associating-an-on-demand-app-to-cloud-configuration.md)
* [Gestione del contenuto](/help/mobile/mobile-apps-ondemand-manage-content-ondemand.md)
* [Panoramica di Content Services](/help/mobile/develop-content-as-a-service.md)

Per iniziare a utilizzare i ruoli e le responsabilità di un autore, consulta [Creazione di contenuti AEM per l’app AEM Mobile On-demand Services](/help/mobile/mobile-apps-ondemand.md).

>[!NOTE]
>
>Un autore AEM è anche responsabile della configurazione dell’adesione, della creazione di schede e layout e dell’invio di notifiche push. Inoltre, per ulteriori informazioni sui metodi di creazione dei contenuti, gestione di articoli e raccolte, creazione di banner, schede e layout in AEM Mobile, consulta [Portale AEM Mobile On-Demand](https://helpx.adobe.com/digital-publishing-solution/topics.html#dynamicpod_reference_2).
