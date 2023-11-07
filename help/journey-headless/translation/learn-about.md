---
title: Scoprire i contenuti headless e come tradurli in AEM
description: Imparare i concetti headless, come si mappano su AEM e la teoria della traduzione in AEM.
exl-id: cb2e2d89-e2d2-462f-8fff-b201847d0641
source-git-commit: fc2f26a69c208947c14e8c6036825bb217901481
workflow-type: tm+mt
source-wordcount: '757'
ht-degree: 91%

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

In un CMS full stack, tutte le funzionalità per la manipolazione dei contenuti sono disponibili nel CMS. Le funzionalità del sistema sono articolate nei diversi componenti dello stack CMS. La soluzione full-stack offre molti vantaggi.

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

I servizi che consumano, siano essi esperienze AR, un web shop, esperienze mobili, app web progressive (PWA) e così via, accettano contenuti dal CMS headless e forniscono il proprio rendering. Si occupano di fornire le teste per i tuoi contenuti.

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
* Un [Introduzione all’AEM come CMS headless](/help/sites-developing/headless/introduction.md)
* Il [Portale per sviluppatori AEM](https://experienceleague.adobe.com/landing/experience-manager/headless/developer.html?lang=it)
* [Tutorials per headless nell&#39;AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html?lang=it)
