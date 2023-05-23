---
title: Estensione [!DNL Adobe Experience Manager] 6.5 utilizzando Adobe Developer App Builder.
description: Estensione [!DNL Adobe Experience Manager] 6.5 utilizzando Adobe Developer App Builder.
exl-id: 8221c2db-82d4-43df-ad38-e8e7831541ac
source-git-commit: cc1b86a15eb7ef45616bc9ea4f8aab4a28e74add
workflow-type: tm+mt
source-wordcount: '550'
ht-degree: 0%

---

# Estensione [!DNL Adobe Experience Manager] utilizzo di Adobe Developer App Builder {#extend-using-app-builder}

## Cos’è App Builder per AEM {#project-appbuilder}

Il nuovo Adobe Developer App Builder fornisce un framework di estensibilità per uno sviluppatore per estendere facilmente le funzionalità AEM.

App Builder fornisce un framework unificato di estensibilità di terze parti per l’integrazione e la creazione di esperienze personalizzate che estendono Adobe Experience Manager. Con questo framework di estensibilità completo, basato sull’infrastruttura Adobe, gli sviluppatori possono creare microservizi personalizzati, estendere e integrare Adobe Experience Manager tra le soluzioni Adobe e il resto dello stack IT.

App Builder consente ai clienti di estendere facilmente Adobe Experience Manager in vari casi d’uso:

* Estensibilità middleware: possibilità di collegare i sistemi esterni con applicazioni Adobe per la creazione di connettori personalizzati o per l&#39;utilizzo di una suite di integrazioni predefinite.
* Estensibilità dei servizi di base: estende le funzionalità delle applicazioni di base estendendo il comportamento predefinito con funzioni personalizzate e logica di business.
* Estensibilità dell’esperienza utente: estendere l’esperienza di base per supportare i requisiti aziendali o creare proprietà digitali, vetrine e app di back-office specifiche per il cliente.

App Builder è disponibile per i clienti e i partner aziendali tramite la nostra anteprima per sviluppatori dall’estate 2020. La disponibilità generale (GA) di App Builder è pianificata per dicembre 2021. Accogliamo con favore gli sviluppatori per provare App Builder attraverso il nostro [Programma di prova](https://adobe.ly/appbuilder-trial).

>[!NOTE]
>
>Per i clienti AEM as a Cloud Service che desiderano sfruttare App Builder, visita [Estensione di Adobe Experience Manager as a Cloud Service tramite Adobe Developer App Builder](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/configuring-and-extending/app-builder.html).

## Architettura {#architecture}

Invece di una soluzione preconfigurata, Adobe Developer App Builder fornisce una piattaforma di sviluppo comune, coerente e standardizzata per estendere le soluzioni Adobe Cloud come AEM, tra cui:

* Console Adobe Developer: per lo sviluppo di estensioni e microservizi personalizzati, consente agli sviluppatori di creare e gestire progetti e al contempo di accedere a tutti gli strumenti e le API necessari per creare plug-in e integrazioni.
* Strumenti per sviluppatori: strumenti open-source, SDK e librerie per consentire agli sviluppatori di creare facilmente estensioni e integrazioni personalizzate. Utilizza React Spectrum (il toolkit dell’interfaccia utente di Adobe) per avere un’unica interfaccia utente comune per tutte le app di Adobe.
* Servizi: I/O Runtime per l&#39;hosting dell&#39;infrastruttura sulla nostra piattaforma senza server ed Eventi di I/O per le integrazioni basate su eventi. Dell fornisce inoltre il supporto predefinito per l&#39;archiviazione di dati e file.
* Adobe Experience Cloud: gli sviluppatori possono inviare estensioni e integrazioni da pubblicare nella propria organizzazione Experience Cloud. Gli amministratori di sistema possono quindi rivedere, gestire e approvare tali estensioni. Dopo la pubblicazione, le estensioni e gli strumenti personalizzati di App Builder sono disponibili insieme ad altre app Adobe Experience Cloud.

Il diagramma seguente illustra come un’applicazione standard basata su App Builder sfrutta queste funzionalità:

![Architettura](assets/appbuilder-architecture.jpg)

Per ulteriori dettagli sull’architettura di App Builder, consulta [Panoramica dell’architettura](https://www.adobe.io/app-builder/docs/guides/).

## Introduzione ad App Builder {#additional-resources}

Per aiutarti a iniziare a utilizzare App Builder, abbiamo creato una serie di documenti per aiutarti a iniziare:

* [Guida introduttiva di App Builder](https://www.adobe.io/app-builder/docs/getting_started/)

## Continua l’apprendimento con la documentazione {#appbuilder-documentation}

App Builder fornisce video e documentazione per gli sviluppatori, incluse guide e documentazione di riferimento per aiutarti a iniziare a sviluppare applicazioni personalizzate:

* [Documentazione di App Builder](https://www.adobe.io/app-builder/docs/overview/)
* [Video di App Builder](https://www.youtube.com/playlist?list=PLcVEYUqU7VRfDij-Jbjyw8S8EzW073F_o)

## Prova una delle applicazioni di esempio {#appbuilder-codesamples}

Sei pronto a iniziare a sviluppare? Abbiamo un sacco di applicazioni di esempio per aiutarti a passare rapidamente:

* [Laboratori di codice di App Builder sul sito web di Adobe Developer](https://www.adobe.io/app-builder/docs/resources/)

