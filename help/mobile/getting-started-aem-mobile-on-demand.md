---
title: AEM Mobile On-Demand
seo-title: AEM Mobile On-Demand
description: L'avvio di una nuova esperienza di app AEM Mobile richiede una coesione di ruoli prima che sia pronta per la modifica del contenuto. Seguite questa pagina per iniziare a usare i servizi on-demand AEM Mobile.
seo-description: L'avvio di una nuova esperienza di app AEM Mobile richiede una coesione di ruoli prima che sia pronta per la modifica del contenuto. Seguite questa pagina per iniziare a usare i servizi on-demand AEM Mobile.
uuid: 175c609d-3cb8-4a1b-bfea-278df272e500
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: introduction
content-type: reference
discoiquuid: dc6891cd-19cc-4dff-8bda-a41ed8af8bfb
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# AEM Mobile On-Demand{#aem-mobile-on-demand}

>[!NOTE]
>
>Adobe consiglia di utilizzare SPA Editor per i progetti che richiedono il rendering lato client basato sul framework dell&#39;applicazione a pagina singola (ad es. React). [Per saperne di più](/help/sites-developing/spa-overview.md).

>[!NOTE]
>
>Se non utilizzate AEM come origine di gestione del contenuto, consultate la guida [dei servizi on-demand di](https://helpx.adobe.com/digital-publishing-solution/topics.html)AEM Mobile.

AEM offre diversi strumenti che consentono di integrare i contenuti nelle applicazioni mobili.

Il diagramma seguente illustra come i vari componenti di AEM Mobile e dei servizi on-demand si integrano per distribuire contenuti alle app mobili.

L&#39;app AEM Preflight può essere considerata un ambiente di verifica per visualizzare l&#39;anteprima dell&#39;app e del contenuto prima della pubblicazione; mentre l&#39;app AEM Mobile è l&#39;app finale creata per la distribuzione.

>[!NOTE]
>
>Per informazioni dettagliate sull&#39;app Preflight, consultate [Utilizzo dell&#39;app](https://helpx.adobe.com/digital-publishing-solution/help/preflight-app.html) AEM Preflight nell&#39;Aiuto dei servizi on-demand di AEM Mobile.

![chlimage_1-171](assets/chlimage_1-171.png)

>[!NOTE]
>
>Nel diagramma precedente, l&#39;istanza AEM Publish non è necessaria per uno scenario di distribuzione tipico per i servizi on-demand AEM Mobile.

## Avvio di una nuova app mobile {#starting-a-new-mobile-app}

AEM Mobile è solo uno dei pilastri che compongono la piattaforma AEM completa.

L&#39;avvio di una nuova esperienza di app AEM Mobile richiede una coesione di ruoli prima che sia pronta per la modifica del contenuto. I seguenti ruoli forniscono un punto di partenza per la creazione di una nuova applicazione AEM Mobile:

* **Administrator**
* **Sviluppatore**
* **Authoring**

>[!NOTE]
>
>Prima di lavorare con AEM Mobile e di seguire i passaggi descritti in questa guida introduttiva, gli utenti devono avere familiarità con AEM. Learn the basics of AEM [here](/help/sites-deploying/deploy.md).

### Nozioni di base sul dashboard dell&#39;applicazione AEM Mobile {#understanding-the-aem-mobile-application-dashboard}

Prima di comprendere i ruoli e le responsabilità, l&#39;utente deve essere a conoscenza di **AEM Mobile Control Center** o di **Application Dashboard**. Fai clic [qui](/help/mobile/mobile-apps-ondemand-application-dashboard.md) per una conoscenza approfondita.

### Amministratore AEM {#aem-administrator}

Un amministratore ***di*** AEM è responsabile dell&#39;aggiunta di una nuova applicazione al catalogo AEM Mobile, tramite la creazione di una nuova app tramite la procedura guidata di creazione o l&#39;importazione di un&#39;applicazione esistente. Gli amministratori di AEM che creano una nuova app tramite la procedura guidata *di* creazione di AEM Mobile in genere selezionano uno dei modelli di app desiderati dagli esempi di riferimento forniti dall&#39;utente oppure (nella maggior parte dei casi) da un modello di app personalizzato creato dagli sviluppatori di *AEM.*

Un amministratore AEM è responsabile delle seguenti attività durante la creazione di un&#39;app tramite i servizi on-demand AEM Mobile:

* [Configurazione di AEM Mobile](/help/mobile/aem-mobile-setup.md)
* [Configurazione di gruppi di utenti e utenti](/help/mobile/aem-mobile-configure-users.md)
* [Anteprima con verifica preliminare](/help/mobile/aem-mobile-manage-ondemand-services.md)
* [Amministrazione di Content Services](/help/mobile/developing-content-services.md)

Per iniziare a utilizzare i ruoli e le responsabilità di un amministratore, consultate [Amministrazione dei contenuti per utilizzare i servizi](/help/mobile/aem-mobile.md)on-demand AEM Mobile.

## AEM Developer {#aem-developer}

Uno sviluppatore **** AEM estende e crea modelli Web e componenti personalizzati per consentire a *AEM Author *di creare esperienze mobili attraenti e coinvolgenti. Questi modelli e componenti non sono ottimizzati solo per il mondo delle app mobili; comunica sia al dispositivo che al server AEM (qualsiasi server remoto) ai punti finali del servizio omnicanale. L’editor di contenuti incorporato di AEM viene utilizzato dagli autori *di* AEM per creare esperienze avanzate e rilevanti all’interno dell’app, inclusa l’integrazione con il resto di Adobe Marketing Cloud.

Durante la creazione di un&#39;app tramite AEM Mobile On-Demand Services, uno sviluppatore AEM è responsabile delle seguenti attività:

* [Modelli e componenti app](/help/mobile/app-templates-and-components1.md)
* [Mobile con sincronizzazione dei contenuti](/help/mobile/mobile-ondemand-contentsync.md)
* [Proprietà contenuto ed esportazione di contenuto](/help/mobile/on-demand-content-properties-exporting.md)
* [Sviluppo di AEM Mobile Content Services](//help/mobile/developing-content-services.md)

Per iniziare a utilizzare i ruoli e le responsabilità degli sviluppatori, consultate [Sviluppo di contenuto AEM per i servizi](/help/mobile/aem-mobile-on-demand.md)on-demand AEM Mobile.

>[!NOTE]
>
>Il ruolo dello ** sviluppatore AEM non inizia e non termina con lo sviluppo di modelli e componenti. Uno sviluppatore *di* AEM può creare un&#39;app completamente nuova anziché estendere semplicemente l&#39;esempio di implementazione dei riferimenti out-of-the-box.

## AEM Author {#aem-author}

Un ***AEM Author *(o*Marketer *)**utilizza i modelli e i componenti sviluppati o forniti appositamente per aggiungere e modificare pagine, trascinare componenti e aggiungere supporti di tutti i tipi dal DAM, incluse immagini, video e frammenti di testo (frammenti di contenuto). L’editor di contenuti incorporato di AEM viene quindi utilizzato dagli autori*di *AEM per creare esperienze complete e pertinenti all’interno dell’app, inclusa l’integrazione con il resto di Adobe Marketing Cloud.

Un autore di AEM deve comprendere i seguenti argomenti, durante la creazione di un&#39;app tramite i servizi on-demand AEM Mobile:

* [Pannello applicazione AEM Mobile](/help/mobile/mobile-apps-ondemand-application-dashboard.md)
* [Azioni di creazione e configurazione delle applicazioni](/help/mobile/mobile-apps-ondemand-application-create-configure-action.md)
* [Configurazione cloud](/help/mobile/mobile-on-demand-associating-an-on-demand-app-to-cloud-configuration.md)
* [Gestione dei contenuti](/help/mobile/mobile-apps-ondemand-manage-content-ondemand.md)
* [Panoramica di Content Services](/help/mobile/develop-content-as-a-service.md)

Per iniziare con i ruoli e le responsabilità di un autore, consultate [Creazione di contenuti AEM per AEM Mobile On-Demand Services App](/help/mobile/mobile-apps-ondemand.md).

>[!NOTE]
>
>AEM Author è anche responsabile per la configurazione dell&#39;adesione, la creazione di schede e layout e l&#39;invio di notifiche push. Inoltre, per ulteriori informazioni sui metodi di creazione dei contenuti; gestione di articoli e raccolte; creazione di banner, schede e layout in AEM Mobile, consultate [AEM Mobile On-Demand Portal](https://helpx.adobe.com/digital-publishing-solution/topics.html#dynamicpod_reference_2).

