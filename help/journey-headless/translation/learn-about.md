---
title: Scopri i contenuti headless e come tradurli in AEM
description: Impara concetti headless, come si mappano a AEM e la teoria della traduzione AEM.
source-git-commit: 38525b6cc14e9f6025564c060b8cfb4f9e0ea473
workflow-type: tm+mt
source-wordcount: '727'
ht-degree: 0%

---

# Scopri i contenuti headless e come tradurli in AEM {#learn-about}

Impara concetti headless, come si mappano a AEM e la teoria della traduzione AEM.

## Obiettivo {#objective}

Questo documento ti aiuta a comprendere la distribuzione headless dei contenuti, come AEM supporta la conversione headless e come tali contenuti possono essere tradotti. Dopo la lettura è necessario:

* Comprendi i concetti di base sulla distribuzione di contenuti headless.
* Sii familiare con come AEM supporta headless e la traduzione.

## Distribuzione completa dei contenuti {#full-stack}

Sin dall&#39;introduzione dei sistemi di gestione dei contenuti (CMS), facili da usare e su larga scala, le aziende li hanno sfruttati come posizione centrale per gestire messaggi, branding e comunicazioni. Utilizzando il CMS come punto centrale per l&#39;amministrazione delle esperienze, è possibile migliorare l&#39;efficienza eliminando la necessità di duplicare attività in sistemi diversi.

![Il classico CMS full-stack](/help/journey-headless/developer/assets/full-stack.png)

In un CMS completo, tutte le funzionalità per la manipolazione dei contenuti si trovano nel CMS. Le caratteristiche del sistema compongono diversi componenti dello stack CMS. La soluzione completa offre molti vantaggi.

* C&#39;è un sistema da mantenere.
* I contenuti vengono gestiti a livello centrale.
* Tutti i servizi del sistema sono integrati.
* L’authoring dei contenuti è semplice.

Quindi, se è necessario aggiungere un nuovo canale o supportare nuovi tipi di esperienze, è possibile inserire uno (o più) nuovi componenti nello stack e c&#39;è una sola posizione per apportare modifiche.

![Aggiunta di un nuovo canale alla pila](/help/journey-headless/developer/assets/adding-channel.png)

Tuttavia, la complessità delle dipendenze all’interno dello stack diventa rapidamente evidente, poiché altri elementi nello stack devono essere regolati per adattarsi alle modifiche.

## Testa senza testa {#the-head}

La testa di qualsiasi sistema è generalmente il renderer di output di quel sistema, tipicamente sotto forma di un&#39;interfaccia grafica o di un&#39;altra uscita grafica.

Quando parliamo di un CMS headless, il CMS gestisce i contenuti e continua a consegnarli ai consumatori. Tuttavia, consegnando solo il **content** in modo standardizzato, un CMS headless omette il rendering finale dell&#39;output, lasciando **presentazione** del contenuto al servizio che consuma.

![CMS headless](/help/journey-headless/developer/assets/headless-cms.png)

I servizi che consumano, siano essi esperienze AR, un negozio web, esperienze mobili, app web progressive (PWA), ecc, prendere in contenuti dal CMS headless e fornire il loro rendering. Si prendono cura di fornire le proprie teste per i contenuti.

Omettendo la testa si semplifica il CMS rimuovendo la complessità. In questo modo si sposta anche la responsabilità di rendere i contenuti ai servizi che ne hanno effettivamente bisogno e che sono spesso più adatti a tale rendering.

## Traduzione di contenuti headless in AEM {#translating-in-aem}

Oltre ad offrire strumenti affidabili per la creazione, la gestione e la distribuzione di pagine web tradizionali in modalità impilata, AEM offre anche la possibilità di creare selezioni di contenuti indipendenti e di distribuirle senza testa.

La potenza di AEM consente di distribuire contenuti headless, full-stack o contemporaneamente in entrambi i modelli. Per lo specialista della traduzione, lo stesso set di strumenti di traduzione può essere applicato a entrambi i tipi di contenuti, offrendo un approccio unificato per la traduzione dei contenuti.

Più avanti nel percorso imparerai i dettagli su come AEM tradurre i contenuti, ma ad alto livello, il concetto è semplice:

1. Definire una connessione a un servizio di traduzione configurando il framework di integrazione della traduzione.
1. Definisci il contenuto da tradurre utilizzando le regole di traduzione.
1. Crea un progetto di traduzione per raccogliere il contenuto, inviarlo al servizio di traduzione e ricevere i risultati.
1. Rivedi e pubblica il contenuto tradotto.

## Novità {#what-is-next}

Grazie per aver iniziato sul tuo percorso di traduzione senza testa AEM! Dopo aver letto questo documento, è necessario:

* Comprendi i concetti di base sulla distribuzione di contenuti headless.
* Sii familiare con come AEM supporta headless e la traduzione.

Sviluppa questa conoscenza e continua il tuo percorso di traduzione senza testa AEM prossimo revisione del documento [Guida introduttiva alla traduzione senza testa AEM](getting-started.md) dove avrai una panoramica di come AEM gestire i contenuti headless e conoscere i suoi strumenti di traduzione.

## Risorse aggiuntive {#additional-resources}

Mentre si consiglia di passare alla parte successiva del percorso di traduzione headless rivedendo il documento [Inizia con AEM traduzione senza testa,](getting-started.md) di seguito sono riportate alcune risorse aggiuntive facoltative che approfondiscono alcuni concetti menzionati in questo documento, ma non è necessario che continuino sul percorso headless.

* [MSM e traduzione](/help/sites-administering/msm-and-translation.md) - Dettagli di AEM Multi-Site Manager e come funziona con i suoi strumenti di traduzione
