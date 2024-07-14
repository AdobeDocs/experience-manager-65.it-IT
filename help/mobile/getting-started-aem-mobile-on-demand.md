---
title: Adobe Experience Manager Mobili On-Demand
description: L’avvio di una nuova esperienza di app mobile Adobe Experience Manager (AEM) richiede una coerenza di ruoli prima di essere pronta per la modifica dei contenuti. Segui questa pagina per iniziare a utilizzare i servizi mobili on-demand dell’AEM.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: introduction
content-type: reference
exl-id: 4be199d8-963d-4807-b9bb-e23fa577c5f2
solution: Experience Manager
feature: Mobile
role: User
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '761'
ht-degree: 1%

---

# AEM Mobile On-Demand{#aem-mobile-on-demand}

>[!NOTE]
>
>L’Adobe consiglia di utilizzare l’Editor SPA per i progetti che richiedono il rendering lato client basato su framework di applicazione a pagina singola (ad esempio, React). [Ulteriori informazioni](/help/sites-developing/spa-overview.md).

>[!NOTE]
>
>Se non utilizzi Adobe Experience Manager (AEM) come origine per la gestione dei contenuti, consulta la [Guida di AEM Mobile On-demand Services](https://helpx.adobe.com/digital-publishing-solution/topics.html).

AEM fornisce diversi strumenti che consentono di integrare i contenuti nelle applicazioni mobili.

Il diagramma seguente illustra come i vari componenti di AEM Mobile e On-Demand Services si integrano per distribuire contenuti alle app mobili.

L’app Verifica preliminare AEM può essere considerata un ambiente di test per visualizzare in anteprima l’app e il contenuto prima della pubblicazione; mentre l’app AEM Mobile è l’app finale creata per la distribuzione.

>[!NOTE]
>
>Per informazioni approfondite sull&#39;app Verifica preliminare, vedere [Utilizzo dell&#39;app Verifica preliminare AEM](https://helpx.adobe.com/digital-publishing-solution/help/preflight-app.html) nella Guida di AEM Mobile On-demand Services.

![chlimage_1-171](assets/chlimage_1-171.png)

>[!NOTE]
>
>Nel diagramma precedente, l’istanza Publish dell’AEM non è necessaria per uno scenario di distribuzione tipico in AEM Mobile On-demand Services.

## Avvio di una nuova app mobile {#starting-a-new-mobile-app}

AEM Mobile è solo uno dei pilastri che compongono l&#39;intera piattaforma AEM.

L’avvio di una nuova esperienza di app AEM Mobile richiede una coerenza di ruoli prima di essere pronta per la modifica dei contenuti. I seguenti ruoli forniscono un punto di partenza per la creazione di un’applicazione AEM Mobile:

* **Amministratore**
* **Sviluppatore**
* **Autore**

>[!NOTE]
>
>Prima di lavorare con AEM Mobile e seguire i passaggi descritti in questa guida introduttiva, gli utenti devono avere familiarità con l’AEM. Scopri le nozioni di base dell&#39;AEM [qui](/help/sites-deploying/deploy.md).

### Informazioni sul dashboard dell’applicazione AEM Mobile {#understanding-the-aem-mobile-application-dashboard}

Prima di comprendere i ruoli e le responsabilità, l&#39;utente deve avere una conoscenza approfondita di **AEM Mobile Control Center** o del **dashboard applicazioni**. Fai clic [qui](/help/mobile/mobile-apps-ondemand-application-dashboard.md) per una comprensione approfondita.

### Amministratore AEM {#aem-administrator}

Un ***amministratore AEM*** è responsabile dell&#39;aggiunta di un&#39;applicazione al catalogo AEM Mobile, sia tramite la creazione guidata di un&#39;app, sia tramite l&#39;importazione di un&#39;applicazione esistente. Gli amministratori AEM che creano un&#39;app utilizzando la *procedura guidata per la creazione* di AEM Mobile in genere selezionano uno dei modelli di app desiderati dagli esempi di riferimento predefiniti di Adobe o (in genere) da un modello di app personalizzato creato da *sviluppatori AEM.*

Un amministratore AEM è responsabile delle seguenti attività durante la creazione di un’app tramite AEM Mobile On-demand Services:

* [Configurazione di AEM Mobile](/help/mobile/aem-mobile-setup.md)
* [Configurazione degli utenti e dei gruppi di utenti](/help/mobile/aem-mobile-configure-users.md)
* [Anteprima con verifica preliminare](/help/mobile/aem-mobile-manage-ondemand-services.md)
* [Amministrazione di Content Services](/help/mobile/developing-content-services.md)

Per iniziare a utilizzare i ruoli e le responsabilità di un amministratore, consulta [Amministrazione del contenuto per l&#39;utilizzo di AEM Mobile On-demand Services](/help/mobile/aem-mobile.md).

## Sviluppatore AEM {#aem-developer}

Uno sviluppatore **AEM** estende e crea modelli web e componenti personalizzati per consentire all&#39; *Autore AEM *di creare esperienze mobili belle e coinvolgenti. Questi modelli e componenti non sono ottimizzati solo per il mondo delle app mobili, ma comunicano sia con il dispositivo che con il server AEM (qualsiasi server remoto) agli endpoint del servizio omni-channel. L&#39;editor di contenuti integrato dell&#39;AEM viene utilizzato da *autori AEM* per creare esperienze avanzate e rilevanti all&#39;interno dell&#39;app, inclusa l&#39;integrazione con il resto del Adobe Experience Cloud.

Uno sviluppatore AEM è responsabile delle seguenti attività durante la creazione di un’app tramite AEM Mobile On-demand Services:

* [Modelli di app e componenti](/help/mobile/app-templates-and-components1.md)
* [Dispositivi mobili con sincronizzazione contenuti](/help/mobile/mobile-ondemand-contentsync.md)
* [Proprietà del contenuto ed esportazione del contenuto](/help/mobile/on-demand-content-properties-exporting.md)
* [Sviluppo di AEM Mobile Content Services](/help/mobile/developing-content-services.md)

Per iniziare a usare i ruoli e le responsabilità degli sviluppatori, consulta [Sviluppo di contenuti AEM per AEM Mobile On-demand Services](/help/mobile/aem-mobile-on-demand.md).

>[!NOTE]
>
>Il ruolo *Sviluppatore AEM* non inizia e non termina con lo sviluppo di modelli e componenti. Uno sviluppatore *AEM* può creare un&#39;app completamente nuova anziché semplicemente estendere l&#39;esempio di implementazione di riferimento preconfigurato.

## Autore AEM {#aem-author}

Un ***Autore AEM* (o *Addetto marketing*)**utilizza modelli e componenti sviluppati o predefiniti per aggiungere e modificare pagine, trascinare e rilasciare componenti e aggiungere supporti di tutti i tipi da DAM, inclusi immagini, video e frammenti di testo (frammenti di contenuto). L&#39;editor di contenuti integrato dell&#39;AEM viene quindi utilizzato da *autori AEM* per creare esperienze avanzate e rilevanti all&#39;interno dell&#39;app, inclusa l&#39;integrazione con il resto del Adobe Experience Cloud.

Un autore AEM deve comprendere i seguenti argomenti durante la creazione di un’app tramite AEM Mobile On-demand Services:

* [Dashboard dell’applicazione AEM Mobile](/help/mobile/mobile-apps-ondemand-application-dashboard.md)
* [Azioni di creazione e configurazione delle applicazioni](/help/mobile/mobile-apps-ondemand-application-create-configure-action.md)
* [Configurazione cloud](/help/mobile/mobile-on-demand-associating-an-on-demand-app-to-cloud-configuration.md)
* [Gestione del contenuto](/help/mobile/mobile-apps-ondemand-manage-content-ondemand.md)
* [Panoramica di Content Services](/help/mobile/develop-content-as-a-service.md)

Per iniziare a utilizzare i ruoli e le responsabilità di un autore, consulta [Creazione di contenuti AEM per l&#39;app AEM Mobile On-demand Services](/help/mobile/mobile-apps-ondemand.md).

>[!NOTE]
>
>Un autore AEM è anche responsabile della configurazione dei diritti, della creazione di schede e layout e dell’invio di notifiche push. Per ulteriori informazioni sui metodi di creazione dei contenuti, gestione di articoli e raccolte, creazione di banner, schede e layout in AEM Mobile, vedere [AEM Mobile On-Demand Portal](https://helpx.adobe.com/digital-publishing-solution/topics.html#dynamicpod_reference_2).
