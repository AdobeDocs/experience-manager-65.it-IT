---
title: AEM Adobe PhoneGap
seo-title: AEM Adobe PhoneGap
description: AEM si integra con PhoneGap in modo da poter creare facilmente app utilizzando le pagine AEM. Segui questa pagina per iniziare a utilizzare Adobe PhoneGap Enterprise.
seo-description: AEM integrates with PhoneGap so that you can easily create apps using AEM pages. Follow this page to get started with Adobe PhoneGap Enterprise.
uuid: bdd90cda-2489-4763-a90a-9c409d6e68ae
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: introduction
content-type: reference
discoiquuid: fbcdea8a-72e9-431b-9c32-dc02d4cdb9c8
exl-id: d989e235-5993-4738-8523-5b9a5f6bf712
source-git-commit: 5bdf42d1ce7b2126bfb2670049deec4b6eaedba2
workflow-type: tm+mt
source-wordcount: '487'
ht-degree: 1%

---

# AEM Adobe PhoneGap{#aem-adobe-phonegap}

>[!NOTE]
>
>L’Adobe consiglia di utilizzare l’Editor SPA per i progetti che richiedono il rendering lato client basato su framework di applicazione a pagina singola (ad esempio, React). [Ulteriori informazioni](/help/sites-developing/spa-overview.md).

AEM si integra con PhoneGap in modo da poter creare facilmente app utilizzando le pagine AEM. PhoneGap permette all’utente di creare app che consentono agli utenti di lavorare con i contenuti. Sincronizzazione contenuti consente di creare archivi con versioni delle pagine da includere nel bundle con le app.

In genere, un’ ***Amministratore AEM*** è responsabile dell’aggiunta di una nuova applicazione al catalogo AEM Mobile, sia tramite la creazione guidata di una nuova app, sia tramite l’importazione di un’applicazione esistente.

Da qui un ***Autore AEM*** (o *Addetto marketing*) ora può utilizzare i modelli e i componenti predefiniti per aggiungere e modificare pagine, trascinare e rilasciare componenti e aggiungere contenuti multimediali di tutti i tipi da DAM, incluse immagini, video e frammenti di testo (frammenti di contenuto).

La vera potenza di AEM Mobile è che un *sapiente* ***Sviluppatore AEM*** può estendere e creare modelli web e componenti personalizzati per abilitare *Autore AEM* per creare esperienze mobili belle e coinvolgenti. Questi modelli e componenti non sono ottimizzati solo per il mondo delle app mobili, ma comunicano sia con il dispositivo che con il server AEM (qualsiasi server remoto) agli endpoint del servizio omni-channel.

>[!NOTE]
>
>Quando *Autore AEM* ritiene che l&#39;app sia pronta, possono prima far scaricare l&#39;app alle parti interessate tramite **[Verifica Adobe](/help/mobile/phonegap-mobile-quickstart.md)** (disponibile sia in AppStore che in PlayStore) per la revisione e l’approvazione. Una volta ricevuta la luce verde, può rilasciare questo contenuto nuovo o aggiornato direttamente ai suoi utenti tramite la dashboard di gestione del rilascio dei contenuti di AEM Mobile ContentSync. Una persona può assumere qualsiasi numero di ruoli, questo dipende da te e dai tuoi criteri di governance.

## Prerequisiti {#prerequisites}

AEM Mobile è solo uno dei pilastri che compongono l&#39;intera piattaforma AEM.

Prima di lavorare con AEM Mobile e seguire i passaggi descritti in questa guida introduttiva, gli utenti devono avere familiarità con AEM e AEM Mobile Control Center. Consulta:

[Guida introduttiva ad AEM](/help/sites-deploying/deploy.md)

[Panoramica di AEM Mobile Control Center](/help/mobile/phonegap-authoring-apps.md)

## Collegamenti rapidi per autori {#quicklinks-for-authors}

Consulta [Authoring per Adobe PhoneGap Enterprise nell’AEM](/help/mobile/phonegap.md) per scoprire i ruoli e le responsabilità di un autore.

## Collegamenti rapidi per sviluppatori {#quicklinks-for-developers}

Esistono applicazioni di esempio che si integreranno con AEM Mobile e possono essere personalizzate dallo sviluppatore. Fai clic su [Sviluppo di Adobe PhoneGap Enterprise con AEM](/help/mobile/developing-in-phonegap.md).

Nei capitoli successivi scoprirai concetti avanzati come l’etichettatura bianca per l’applicazione, la localizzazione, l’internazionalizzazione, la sincronizzazione dei contenuti, il targeting, Analytics e altro ancora.

## Collegamenti rapidi per gli amministratori {#quicklinks-for-administrators}

Consulta [Amministrazione di contenuti per Adobe PhoneGap Enterprise con AEM](/help/mobile/administer-phonegap.md) per configurare e gestire l’app mobile.

>[!NOTE]
>
>Utilizzando le tecnologie ibride per dispositivi mobili, puoi creare applicazioni mobili avanzate che *esecuzione offline e online* con AEM Mobile infatti, molti clienti scelgono di creare app che verificano quando sono online o offline e si comportano di conseguenza.
