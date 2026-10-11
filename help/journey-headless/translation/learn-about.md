---
title: Scoprire i contenuti headless e come tradurli in AEM
description: Imparare i concetti headless, come si mappano su AEM e la teoria della traduzione in AEM.
exl-id: cb2e2d89-e2d2-462f-8fff-b201847d0641
solution: Experience Manager, Experience Manager Sites
feature: Headless,Content Fragments,Language Copy
role: Admin, Developer, User, Leader
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: bfd4bc52-c397-5127-8f86-8953ba9fc0a3
    internal-label: Headless
  - id: a642c50e-80eb-4fc1-a5d2-f3762d1f841d
    internal-label: Administration
  - id: d9d38edd-df1b-480c-8f5e-72b62576f390
    internal-label: Site and page features
subfeature_v2:
  - id: e9db7c79-8f65-4281-a439-c9049296d903
    internal-label: Content Fragments
  - id: e15a4109-ae5d-497d-b301-31149e35aed4
    internal-label: Language Copy Wizard
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
    internal-label: Leader
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '775'
ht-degree: 98%
---
# Scoprire i contenuti headless e come tradurli in AEM {#learn-about}

Imparare i concetti headless, come si mappano su AEM e la teoria della traduzione in AEM.

## Obiettivo {#objective}

Questo documento ti aiuta a comprendere la distribuzione headless dei contenuti, come AEM supporta i contenuti headless e come tali contenuti possono essere tradotti. Dopo la lettura dovresti:

* Comprendere i concetti di base sulla distribuzione headless dei contenuti.
* Sapere come AEM supporta i contenuti headless e la traduzione.

## Distribuzione contenuti full-stack {#full-stack}

Sin dall’introduzione dei sistemi di gestione dei contenuti (CMS), facili da usare e su larga scala, le aziende li hanno utilizzati come punto centrale per gestire messaggistica, branding e comunicazioni. Utilizzando il CMS come punto centrale per l’amministrazione delle esperienze, è possibile migliorare l’efficienza eliminando la necessità di duplicare attività in sistemi diversi.

![Il classico CMS full-stack](/help/journey-headless/developer/assets/full-stack.png)

In un CMS full stack, tutte le funzionalità per la manipolazione dei contenuti sono disponibili in CMS. Le funzionalità del sistema sono articolate nei diversi componenti dello stack CMS. La soluzione full-stack offre molti vantaggi.

* Occorre gestire un solo sistema.
* I contenuti vengono gestiti a livello centrale.
* Tutti i servizi del sistema sono integrati.
* L’authoring dei contenuti è semplice.

Quindi, se è necessario aggiungere un nuovo canale o supportare nuovi tipi di esperienze, è possibile inserire un nuovo componente (o più di uno) nello stack ed esiste una sola posizione per apportare modifiche.

![Aggiungere un nuovo canale allo stack](/help/journey-headless/developer/assets/adding-channel.png)

Tuttavia, la complessità delle dipendenze all’interno dello stack diventa subito evidente, poiché altri elementi nello stack devono essere regolati per adattarli alle modifiche.

## La “testa” in headless {#the-head}

La “testa” di qualsiasi sistema è generalmente il renderer di output di quel sistema, tipicamente un&#39;interfaccia utente grafica o un altro tipo di output grafico.

Quando parliamo di un CMS headless, il CMS gestisce i contenuti e continua a consegnarli ai consumatori. Tuttavia, consegnando solo il **contenuto** in modo standardizzato, un CMS headless omette il rendering finale dell’output, lasciando la **presentazione** del contenuto al servizio utilizzato.

![CMS headless](/help/journey-headless/developer/assets/headless-cms.png)

I servizi utilizzati, siano essi esperienze AR, un web shop, esperienze mobile, app web progressive (PWA), ecc., prendono i contenuti dal CMS headless e forniscono il loro rendering. Si occupano di fornire le teste per i tuoi contenuti.

Omettendo la “testa” si semplifica il CMS rimuovendo la complessità. In questo modo si sposta anche la responsabilità di eseguire il rendering dei contenuti ai servizi che ne hanno effettivamente bisogno e che sono spesso più adatti a tale rendering.

## Traduzione del contenuto headless in AEM {#translating-in-aem}

Oltre a offrire strumenti affidabili per la creazione, la gestione e la distribuzione di pagine web tradizionali in modalità full-stack, AEM offre anche la possibilità di creare selezioni indipendenti di contenuti e di distribuirle in modo headless.

Grazie alle sue potenzialità, AEM consente di distribuire contenuti headless, full-stack o, contemporaneamente, in entrambe le modalità. Per lo specialista della traduzione, lo stesso set di strumenti di traduzione può essere utilizzato per entrambi i tipi di contenuti, offrendo un approccio unificato per la traduzione dei contenuti.

Più avanti nel percorso imparerai i dettagli su come AEM traduce i contenuti, ma a livello generale, il concetto è semplice:

1. Definire una connessione a un servizio di traduzione configurando il Translation Integration Framework.
1. Definire il contenuto da tradurre utilizzando le regole di traduzione.
1. Creare un progetto di traduzione per raccogliere il contenuto, inviarlo al servizio di traduzione e ricevere il lavoro svolto.
1. Rivedere e pubblicare il contenuto tradotto.

## Passaggio successivo {#what-is-next}

Grazie per aver iniziato il tuo percorso di traduzione headless in AEM! Dopo aver letto questo documento, dovresti:

* Comprendere i concetti di base sulla distribuzione headless dei contenuti.
* Sapere come AEM supporta i contenuti headless e la traduzione.

Acquisite queste conoscenze, continua il tuo percorso di traduzione headless in AEM passando alla consultazione del documento [Introduzione alla traduzione headless in AEM](getting-started.md) che ti fornirà una panoramica sulla gestione dei contenuti headless da parte di AEM e potrai conoscere i relativi strumenti di traduzione.

## Risorse aggiuntive {#additional-resources}

Sebbene sia consigliabile passare alla parte successiva del percorso di traduzione headless consultando il documento [Introduzione alla traduzione headless in AEM,](getting-started.md) di seguito troverai alcune risorse aggiuntive e opzionali che approfondiscono alcuni concetti menzionati in questo documento, ma non sono necessarie per continuare il percorso headless.

* [MSM e traduzione](/help/sites-administering/msm-and-translation.md): dettagli del gestore multisito di AEM e come funzionano i suoi strumenti di traduzione
* [Introduzione ad AEM come CMS headless](/help/sites-developing/headless/introduction.md)
* Il [Portale per sviluppatori AEM](https://experienceleague.adobe.com/landing/experience-manager/headless/developer.html?lang=it)
* [Tutorial per contenuti headless in AEM](https://experienceleague.adobe.com/it/docs/experience-manager-learn/getting-started-with-aem-headless/overview)
