---
title: ' AEM Mobile On-Demand'
seo-title: ' AEM Mobile On-Demand'
description: L'avvio di una nuova esperienza  app AEM Mobile richiede una coesione di ruoli prima che sia pronta per la modifica del contenuto. Seguite questa pagina per iniziare a usare AEM servizi on-demand mobili.
seo-description: L'avvio di una nuova esperienza  app AEM Mobile richiede una coesione di ruoli prima che sia pronta per la modifica del contenuto. Seguite questa pagina per iniziare a usare AEM servizi on-demand mobili.
uuid: 175c609d-3cb8-4a1b-bfea-278df272e500
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: introduction
content-type: reference
discoiquuid: dc6891cd-19cc-4dff-8bda-a41ed8af8bfb
translation-type: tm+mt
source-git-commit: a876a1a8d4aeb9e9a94c93a16742a4058307b0a8
workflow-type: tm+mt
source-wordcount: '804'
ht-degree: 1%

---


#  AEM Mobile On-Demand{#aem-mobile-on-demand}

>[!NOTE]
>
> Adobe consiglia di utilizzare l&#39;editor SPA per i progetti che richiedono il rendering lato client basato sul framework dell&#39;applicazione a pagina singola (ad es. React). [Per saperne di più](/help/sites-developing/spa-overview.md).

>[!NOTE]
>
>Se non utilizzate AEM come origine di gestione dei contenuti, consultate la sezione [ Guida di AEM Mobile On-demand Services](https://helpx.adobe.com/digital-publishing-solution/topics.html).

AEM offre diversi strumenti che consentono di integrare i contenuti nelle applicazioni mobili.

Il diagramma seguente illustra come i vari componenti di  AEM Mobile e dei servizi on-demand si integrano per distribuire contenuti alle app mobili.

AEM&#39;app Preflight può essere considerata un ambiente di verifica per visualizzare l&#39;anteprima dell&#39;app e del contenuto prima della pubblicazione; mentre l&#39;app AEM Mobile  è l&#39;app finale creata per la distribuzione.

>[!NOTE]
>
>Per informazioni dettagliate sull&#39;app Preflight, consultate [Utilizzo dell&#39;app AEM Preflight](https://helpx.adobe.com/digital-publishing-solution/help/preflight-app.html) nella Guida  AEM Mobile On-demand Services.

![chlimage_1-171](assets/chlimage_1-171.png)

>[!NOTE]
>
>Nel diagramma precedente, l&#39;istanza AEM Publish non è necessaria per uno scenario di distribuzione tipico per  AEM Mobile On-demand Services.

## Avvio di una nuova app mobile {#starting-a-new-mobile-app}

 AEM Mobile è solo uno dei pilastri che compongono la piattaforma AEM completa.

L&#39;avvio di una nuova esperienza  app AEM Mobile richiede una coesione di ruoli prima che sia pronta per la modifica del contenuto. I seguenti ruoli forniscono un punto di partenza per la creazione di una nuova applicazione AEM Mobile :

* **Administrator**
* **Developer (Sviluppatore)**
* **Authoring**

>[!NOTE]
>
>Prima di lavorare con  AEM Mobile e di seguire i passaggi descritti in questa guida introduttiva, gli utenti devono avere familiarità con AEM. Scopri le basi di AEM [qui](/help/sites-deploying/deploy.md).

### Informazioni sul  AEM Mobile Application Dashboard {#understanding-the-aem-mobile-application-dashboard}

Prima di comprendere i ruoli e le responsabilità, l&#39;utente deve essere a conoscenza di **AEM Mobile Control Center** o del **Pannello applicazioni**. Fate clic [qui](/help/mobile/mobile-apps-ondemand-application-dashboard.md) per una conoscenza approfondita.

### Amministratore AEM {#aem-administrator}

Un ***AEM amministratore*** è responsabile dell&#39;aggiunta di una nuova applicazione al  catalogo AEM Mobile, sia mediante la creazione di una nuova app tramite la procedura guidata di creazione, sia mediante l&#39;importazione di un&#39;applicazione esistente. AEM amministratori che creano una nuova app utilizzando  procedura guidata di creazione di AEM Mobile ** in genere selezionano uno dei modelli di app desiderati dagli esempi di riferimento forniti dall&#39;utente oppure (nella maggior parte dei casi) da un modello di app personalizzato creato dagli sviluppatori *AEM.*

Durante la creazione di un&#39;app tramite  AEM Mobile On-demand Services, un amministratore AEM è responsabile delle seguenti attività:

* [Configurazione  AEM Mobile](/help/mobile/aem-mobile-setup.md)
* [Configurazione di gruppi di utenti e utenti](/help/mobile/aem-mobile-configure-users.md)
* [Anteprima con verifica preliminare](/help/mobile/aem-mobile-manage-ondemand-services.md)
* [Amministrazione di Content Services](/help/mobile/developing-content-services.md)

Per iniziare a utilizzare i ruoli e le responsabilità di un amministratore, vedere [Amministrazione dei contenuti da utilizzare  AEM Mobile On-demand Services](/help/mobile/aem-mobile.md).

## Sviluppatore AEM {#aem-developer}

Uno sviluppatore **AEM** estende e crea modelli Web e componenti personalizzati per consentire a *AEM Author *di creare esperienze mobili attraenti e coinvolgenti. Questi modelli e componenti non sono ottimizzati solo per il mondo delle app mobili; ma comunicare sia al dispositivo che al server AEM (qualsiasi server remoto) ai punti finali del servizio omnicanale. AEM editor di contenuti integrato viene utilizzato da *AEM Authors* per creare esperienze avanzate e pertinenti all&#39;interno dell&#39;app, inclusa l&#39;integrazione con il resto dell&#39;Adobe Marketing Cloud.

Durante la creazione di un&#39;app tramite  AEM Mobile On-demand Services, uno sviluppatore AEM è responsabile delle seguenti attività:

* [Modelli e componenti per app](/help/mobile/app-templates-and-components1.md)
* [Mobile con sincronizzazione dei contenuti](/help/mobile/mobile-ondemand-contentsync.md)
* [Proprietà contenuto ed esportazione di contenuto](/help/mobile/on-demand-content-properties-exporting.md)
* [Sviluppo  AEM Mobile Content Services](/help/mobile/developing-content-services.md)

Per iniziare a utilizzare i ruoli e le responsabilità degli sviluppatori, vedere [Sviluppo AEM contenuto per  AEM Mobile On-demand Services](/help/mobile/aem-mobile-on-demand.md).

>[!NOTE]
>
>Il ruolo *AEM sviluppatore* non inizia e non termina con lo sviluppo di modelli e componenti. Uno sviluppatore *AEM* può creare un&#39;app completamente nuova anziché semplicemente estendere l&#39;esempio di implementazione dei riferimenti out-of-the-box.

## AEM Author {#aem-author}

Un ***AEM Author* (o *Marketer*)**utilizza i modelli e i componenti sviluppati o forniti appositamente per aggiungere e modificare pagine, trascinare componenti e aggiungere supporti di tutti i tipi da DAM, incluse immagini, video e frammenti di testo (frammenti di contenuto). AEM editor di contenuti incorporato viene quindi utilizzato da *AEM Authors* per creare esperienze avanzate e pertinenti all&#39;interno dell&#39;app, inclusa l&#39;integrazione con il resto dell&#39;Adobe Marketing Cloud.

Durante la creazione di un&#39;app tramite  AEM Mobile On-demand Services, un autore deve comprendere i seguenti argomenti:

* [ AEM Mobile Application Dashboard](/help/mobile/mobile-apps-ondemand-application-dashboard.md)
* [Azioni di creazione e configurazione delle applicazioni](/help/mobile/mobile-apps-ondemand-application-create-configure-action.md)
* [Configurazione cloud](/help/mobile/mobile-on-demand-associating-an-on-demand-app-to-cloud-configuration.md)
* [Gestione dei contenuti](/help/mobile/mobile-apps-ondemand-manage-content-ondemand.md)
* [Panoramica di Content Services](/help/mobile/develop-content-as-a-service.md)

Per iniziare con i ruoli e le responsabilità di un autore, consulta [Creazione AEM contenuto per  AEM Mobile On-demand Services App](/help/mobile/mobile-apps-ondemand.md).

>[!NOTE]
>
>AEM Author è anche responsabile per la configurazione dell&#39;adesione, la creazione di schede e layout e l&#39;invio di notifiche push. Inoltre, per ulteriori informazioni sui metodi di authoring dei contenuti; gestione di articoli e raccolte; creazione di banner, schede e layout in  AEM Mobile, consultate [ AEM Mobile On-Demand Portal](https://helpx.adobe.com/digital-publishing-solution/topics.html#dynamicpod_reference_2).

