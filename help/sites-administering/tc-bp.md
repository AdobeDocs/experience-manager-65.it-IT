---
title: Tecniche consigliate per la traduzione
seo-title: Tecniche consigliate per la traduzione
description: Trovi le best practice compilate dai team di progettazione e consulenza  Adobe per aiutarvi a imparare a usare i progetti di traduzione.
seo-description: Trovi le best practice compilate dai team di progettazione e consulenza  Adobe per aiutarvi a imparare a usare i progetti di traduzione.
uuid: 3bac1d73-9696-4c9b-8bdd-6f00fac40cf7
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features, best-practices
content-type: reference
discoiquuid: 1554010e-a1d1-4edf-b28f-9eead8f83b4a
translation-type: tm+mt
source-git-commit: a929252a13f66da8ac3e52aea0655b12bdd1425f
workflow-type: tm+mt
source-wordcount: '859'
ht-degree: 0%

---


# Translation Best Practices{#translation-best-practices}

## Generale {#general}

La creazione o l&#39;espansione di una presenza Web globale può essere un processo complesso, ma con un buon AEM di pianificazione e di previsione può semplificare i vostri sforzi e supportare i vostri obiettivi aziendali globali.

* **Pianificate l&#39;espansione** globale prima di implementare il primo sito. Adattare un sito esistente per la copertura globale quando il sito è stato implementato con breve preavviso è tipicamente più difficile che pianificare l&#39;espansione globale all&#39;inizio:

   * Valuta lo stato corrente della maturità della localizzazione della tua organizzazione. Determinare se sono **disponibili strumenti**, **processi** e **risorse** per supportare l&#39;espansione globale.
   * Prestate attenzione alle normative **** globali e alle preferenze **linguistiche** regionali. Progettazione di strutture e processi di contenuto flessibili in grado di adattarsi a un ambiente aziendale globale in continua evoluzione.

* Determinare un modello di **governance** che supporti il business globale e utilizzare meccanismi AEM come MSM e autorizzazioni utente per applicare il modello scelto. Ad esempio, potete determinare se il contenuto verrà creato a livello centrale e se verrà inviato o meno alle regioni o ai paesi. Determinare il contenuto che può essere sbloccato e modificato nelle aree geografiche. Determinare chi è responsabile dell&#39;avvio e della gestione delle traduzioni.
* Se le risorse lo consentono, è meglio gestire l&#39;attività di traduzione da un team centrale che può sviluppare competenze negli strumenti, nei processi e nelle relazioni con i fornitori necessari.
* **Pianificate**, **prototipi** e **testate** la struttura e i processi globali per garantire che supportino l&#39;azienda e che possiate contare sul supporto necessario degli azionisti nelle aree geografiche.

## Struttura sito  {#site-structure}

* Durante la progettazione della struttura del sito, è innanzitutto necessario esaminare il contenuto e determinare dove e in quale lingua è stato creato il contenuto. Questa posizione deve essere il livello principale del sito.
* La procedura ottimale è una struttura **basata sulle** lingue con un massimo di 3 livelli tra l’authoring di livello principale e i siti dei paesi.
* Utilizzate una convenzione di denominazione del sito lingua/paese conforme agli standard **** W3C.
* Determinare la modalità di distribuzione dei contenuti per regioni e paesi. Considerate quali paesi condividono le lingue. Si consiglia di creare master di lingua, un livello di pagine non attivate, in cui i contenuti tradotti possono essere rivisti e modificati, quindi inviati o estratti a un sito del paese che condivide tale lingua.
* Esistono due approcci per la creazione di master di lingua: utilizzo di copie in lingua e di copie MSM/live.

   * L&#39;approccio basato sulla copia della lingua è quello utilizzato AEM framework di integrazione della traduzione out-of-the-box, e quindi è il modo più semplice per iniziare. Il framework fornisce un&#39;interfaccia utente che semplifica inizialmente la propagazione e la traduzione delle modifiche apportate ai contenuti dalla lingua principale (ad esempio l&#39;inglese) ai master delle lingue. Tuttavia, con la crescita del progetto, l&#39;automazione del flusso di lavoro diventa sempre più necessaria per gestire la traduzione di un numero maggiore di pagine e/o lingue.
   * L&#39;approccio MSM/Live Copy può essere un&#39;alternativa per i casi di utilizzo avanzati, in cui i siti sono più grandi e complessi. Una governance forte e l&#39;automazione del flusso di lavoro sono necessarie fin dall&#39;inizio per gestire le complesse relazioni di ereditarietà tra i master in inglese e in lingua inglese e per ridurre il rischio di sovrascrittura delle traduzioni esistenti. Questa gestione può essere realizzata con l&#39;aiuto di alcuni connettori di traduzione. Per ulteriori informazioni, consulta [MSM e Siti](/help/sites-administering/msm-best-practices.md#msm-and-multilingual-websites) multilingue.

* Se la lingua master presenta varianti globali, è possibile utilizzare MSM per creare una Live Copy dal master globale da utilizzare per la traduzione. Ad esempio, se l’authoring globale viene eseguito in un master inglese americano, create un master inglese internazionale come copia dal vivo e base per la traduzione in altre lingue.
* Utilizzate MSM per creare siti per i paesi dai master per le lingue tradotte e per distribuire contenuti a siti che condividono la stessa lingua. Ad esempio, il master in lingua francese può essere distribuito in Francia, Belgio e Svizzera.
* Pianificate, prototipi e testate prima l&#39;implementazione.

## Processi e metodi di traduzione {#translation-processes-and-methods}

* Coinvolgere un provider di servizi di **localizzazione (LSP)** con competenze in traduzione e relative attività di localizzazione. I sistemi LSP possono contribuire a scalare l&#39;attività globale fornendo un&#39;ampia gamma di risorse e tecnologie per migliorare l&#39;efficienza e risparmiare sui costi di traduzione:

   * Alcuni LSP sono sia fornitori di servizi che di tecnologie. Ci sono anche fornitori di tecnologie indipendenti che consentono a molti LSP di partecipare alle loro piattaforme di traduzione.
   * Il **AEM Quadro** di traduzione sostiene l&#39;integrazione con diversi fornitori di tecnologie di traduzione sia per la traduzione automatica che per la traduzione umana.
   * Scoprite come [integrare i connettori LSP nel sistema](/help/sites-administering/translation.md) AEM per automatizzare la conversione dei contenuti, o come creare, esportare e importare manualmente i progetti di traduzione per il test e nei casi in cui non vi sia un provider LSP o di tecnologia di traduzione.

* Scegliete un metodo **di** traduzione più adatto al contenuto.

   * **La traduzione** umana è particolarmente adatta ai contenuti in cui messaggi e aspettative di qualità sono elevate e il contenuto vivrà per un certo periodo di tempo sul sito, come le pagine di marketing.
   * **La traduzione** automatica può essere una buona scelta per volumi di traduzione di massa quando il tempo di pubblicazione è critico, le aspettative di qualità sono rilassate, o i costi di traduzione umana sono proibitivi. La knowledge base del supporto e il contenuto generato dagli utenti sono comunemente tradotti da computer.

* Potrai contare sulle competenze dei provider di servizi di localizzazione,  Consulenza di Adobe e Integratori di sistema per progettare, creare prototipi e testare la tua struttura multilingue del sito.

