---
title: Estensione di  [!DNL Adobe Experience Manager] 6.5 tramite Adobe Developer App Builder.
description: Estensione di  [!DNL Adobe Experience Manager] 6.5 tramite Adobe Developer App Builder.
exl-id: 8221c2db-82d4-43df-ad38-e8e7831541ac
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: f96b178ae84b4b930b59e36d4994970682c53dbd
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 0%

---

# Estensione di [!DNL Adobe Experience Manager] tramite Adobe Developer App Builder {#extend-using-app-builder}

## Cos’è App Builder per AEM {#project-appbuilder}

Il nuovo Adobe Developer App Builder fornisce un framework di estensibilità per uno sviluppatore per estendere facilmente le funzionalità di AEM.

App Builder fornisce un framework unificato di estensibilità di terze parti per l’integrazione e la creazione di esperienze personalizzate che estendono Adobe Experience Manager. Con questo framework di estensibilità completo, basato sull’infrastruttura di Adobe, gli sviluppatori possono creare microservizi personalizzati, estendere e integrare Adobe Experience Manager tra le soluzioni Adobe e il resto dello stack IT.

App Builder offre ai clienti un modo per estendere facilmente Adobe Experience Manager in vari casi d’uso:

* Estensibilità middleware: collega i sistemi esterni con le applicazioni Adobe creando connettori personalizzati o utilizzando una suite di integrazioni predefinite.
* Estensibilità dei servizi di base: estende le funzionalità delle applicazioni di base estendendo il comportamento predefinito con funzioni personalizzate e logica di business.
* Estensibilità dell’esperienza utente: estendere l’esperienza di base per supportare i requisiti aziendali o creare proprietà digitali, vetrine e app di back-office specifiche per il cliente.

>[!NOTE]
>
>Per i clienti di AEM as a Cloud Service che desiderano utilizzare App Builder, consulta [Estensione di Adobe Experience Manager as a Cloud Service con Adobe Developer App Builder](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/app-builder.html?lang=it).

## Architettura {#architecture}

Invece di una soluzione preconfigurata, Adobe Developer App Builder fornisce una piattaforma di sviluppo comune, coerente e standardizzata per estendere le soluzioni Adobe Cloud come AEM, tra cui:

* Adobe Developer Console: per lo sviluppo di estensioni e microservizi personalizzati, consente agli sviluppatori di creare e gestire progetti e al tempo stesso di accedere a tutti gli strumenti e le API necessari per creare plug-in e integrazioni.
* Strumenti per sviluppatori: strumenti open-source, SDK e librerie per consentire agli sviluppatori di creare facilmente estensioni e integrazioni personalizzate. Usa React Spectrum (toolkit dell’interfaccia utente di Adobe) per avere un’unica interfaccia utente comune per tutte le app Adobe.
* Servizi: I/O Runtime per l&#39;hosting dell&#39;infrastruttura sulla piattaforma senza server di Adobe ed Eventi di I/O per integrazioni basate su eventi. Adobe fornisce inoltre supporto predefinito per l’archiviazione di dati e file.
* Adobe Experience Cloud: gli sviluppatori possono inviare estensioni e integrazioni da pubblicare nella propria organizzazione Experience Cloud. Gli amministratori di sistema possono quindi rivedere, gestire e approvare tali estensioni. Dopo la pubblicazione, le estensioni e gli strumenti personalizzati di App Builder sono disponibili insieme ad altre app Adobe Experience Cloud.

Il diagramma seguente illustra come un’applicazione standard basata su App Builder utilizza queste funzionalità:

![Architettura](assets/appbuilder-architecture.jpg)

Per ulteriori dettagli sull&#39;architettura di App Builder, consulta [Panoramica dell&#39;architettura](https://developer.adobe.com/app-builder/docs/guides/app_builder_guides/architecture_overview/architecture-overview).

## Introduzione ad App Builder {#additional-resources}

Per aiutarti a iniziare a utilizzare App Builder, è stata creata una serie di documenti per aiutarti a iniziare:

* [Guida introduttiva di App Builder](https://developer.adobe.com/app-builder/docs/get_started/)

## Continua l’apprendimento con la documentazione {#appbuilder-documentation}

App Builder fornisce video e documentazione per gli sviluppatori, incluse guide e documentazione di riferimento per aiutarti a iniziare a sviluppare applicazioni personalizzate:

* [Documentazione di App Builder](https://developer.adobe.com/app-builder/docs/overview/)
* [Video su App Builder](https://www.youtube.com/playlist?list=PLcVEYUqU7VRfDij-Jbjyw8S8EzW073F_o)

## Prova una delle applicazioni di esempio {#appbuilder-codesamples}

Sei pronto a iniziare a sviluppare? Sono disponibili numerose applicazioni di esempio per aiutarti a passare rapidamente all’azione:

* [Laboratori di codice App Builder sul sito Web Adobe Developer](https://developer.adobe.com/app-builder/docs/resources/)

