---
title: Best practice per la traduzione
seo-title: Best practice per la traduzione
description: Trova le best practice compilate dai team di ingegneria e consulenza di Adobe per aiutarti a iniziare a usare i progetti di traduzione.
seo-description: Trova le best practice compilate dai team di ingegneria e consulenza di Adobe per aiutarti a iniziare a usare i progetti di traduzione.
uuid: 3bac1d73-9696-4c9b-8bdd-6f00fac40cf7
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features, best-practices
content-type: reference
discoiquuid: 1554010e-a1d1-4edf-b28f-9eead8f83b4a
feature: Language Copy
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '861'
ht-degree: 0%

---


# Best practice per la traduzione{#translation-best-practices}

## Generale {#general}

La creazione o l&#39;espansione di una presenza web globale può essere un processo complesso, ma con una buona previsione e una buona pianificazione AEM può semplificare i vostri sforzi e supportare i vostri obiettivi aziendali globali.

* **Pianifica l&#39;** espansione globale prima di implementare il tuo primo sito. L&#39;adattamento di un sito esistente per la copertura globale quando il sito è stato implementato con breve preavviso è tipicamente più difficile della pianificazione dell&#39;espansione globale all&#39;inizio:

   * Valutare lo stato attuale della maturità di localizzazione della tua organizzazione. Stabilisci se disponi degli **strumenti**, **processi** e **risorse** per supportare l&#39;espansione globale.
   * Presta attenzione alle **normative globali** e alle **preferenze per le lingue regionali**. Progettazione di strutture e processi di contenuto flessibili in grado di adattarsi a un ambiente aziendale globale in continua evoluzione.

* Determina un modello **governance** che supporta la tua attività globale e utilizza meccanismi AEM come MSM e le autorizzazioni utente per applicare il modello scelto. Ad esempio, puoi determinare se il contenuto verrà creato a livello centrale e inviato o &quot;trascinato&quot; alle aree geografiche o ai paesi. Determina i contenuti che possono essere sbloccati e modificati nelle aree geografiche. Determinare chi è responsabile dell&#39;avvio e della gestione delle traduzioni.
* Se le risorse lo consentono, è meglio gestire l&#39;attività di traduzione da un team centrale che può sviluppare competenze negli strumenti, nei processi e nelle relazioni con i fornitori necessari.
* **Pianificare**,  **** prototipare e  **** testare la tua struttura e i tuoi processi globali per assicurarti che supportino l&#39;attività e che tu disponga del supporto richiesto dalle parti interessate nelle aree geografiche.

## Struttura sito  {#site-structure}

* Durante la progettazione della struttura del sito, esamina innanzitutto il contenuto e determina dove e in quale lingua viene creato il contenuto. Questa posizione deve essere il livello superiore del sito.
* La best practice è una **struttura basata su lingua** con non più di 3 livelli tra l’authoring di livello principale e i siti di paese.
* Utilizza una convenzione per la denominazione di un sito in lingua/paese che segue **W3C standards**.
* Determinare in che modo i contenuti vengono distribuiti da aree geografiche e paesi. Considerate quali paesi condividono le lingue. Si consiglia di creare master per la lingua, un livello di pagine non attivate, in cui il contenuto tradotto può essere rivisto e modificato e quindi inviato o estratto a un sito del paese che condivide tale lingua.
* Sono disponibili due approcci per la creazione di master lingua: utilizzo di copie per lingua e di copie MSM/live.

   * L’approccio per la copia della lingua è quello utilizzato AEM framework di integrazione della traduzione standard, e quindi è il modo più semplice per iniziare. Il framework fornisce un’interfaccia utente che semplifica inizialmente la propagazione e la traduzione delle modifiche al contenuto dal master in lingua principale (ad esempio inglese) ai master in lingua. Tuttavia, man mano che il progetto cresce, l&#39;automazione del flusso di lavoro diventa sempre più necessaria per gestire la traduzione dell&#39;aumento del numero di pagine e/o lingue.
   * L’approccio MSM/Live Copy può essere un’alternativa per i casi di utilizzo avanzati, in cui i siti sono più grandi e complessi. Una governance forte e l&#39;automazione del flusso di lavoro sono necessarie fin dall&#39;inizio per gestire le complesse relazioni di ereditarietà tra i master in inglese e in lingua e per ridurre il rischio di sovrascrittura delle traduzioni esistenti. Questa gestione può essere effettuata con l’aiuto di alcuni connettori di traduzione. Per ulteriori informazioni, consulta [MSM e siti multilingue](/help/sites-administering/msm-best-practices.md#msm-and-multilingual-websites) .

* Se la lingua master dispone di varianti globali, è possibile utilizzare MSM per creare una Live Copy dal master globale da utilizzare per la traduzione. Ad esempio, se l’authoring globale viene eseguito in un master inglese americano, crea un master inglese internazionale come Live Copy e base per la traduzione in altre lingue.
* Utilizza MSM per creare siti di paesi dai master in lingua tradotta e per distribuire contenuti a siti che condividono la stessa lingua. Ad esempio, il master in lingua francese può essere esteso ai siti di Francia, Belgio e Svizzera.
* Pianifica, prototipo e testa prima, prima di avviare l&#39;implementazione.

## Processi e metodi di traduzione {#translation-processes-and-methods}

* Coinvolgi un **provider di servizi di localizzazione (LSP)** con esperienza nelle attività di traduzione e localizzazione correlate. I LSP possono contribuire a scalare la tua attività globale fornendo un&#39;ampia gamma di risorse e tecnologie per migliorare l&#39;efficienza e risparmiare sui costi di traduzione:

   * Alcuni LSP sono sia fornitori di servizi che di tecnologie. Ci sono anche fornitori di tecnologie indipendenti che permettono a molti LSP di partecipare alle loro piattaforme di traduzione.
   * Il **AEM Framework di traduzione** supporta l&#39;integrazione con diversi fornitori di tecnologie di traduzione sia per la traduzione automatica che per quella umana.
   * Scopri come [integrare i connettori LSP nel sistema di AEM](/help/sites-administering/translation.md) per automatizzare la traduzione dei contenuti o come creare, esportare e importare manualmente progetti di traduzione per i test e nei casi in cui non vi sia alcun provider di tecnologia LSP o di traduzione.

* Scegli un **metodo di traduzione** più adatto al contenuto.

   * **La** traduzione umana è ideale per i contenuti in cui la messaggistica e le aspettative di qualità sono elevate e il contenuto sarà live per un certo periodo di tempo sul sito, come le pagine di marketing.
   * **La** traduzione automatica può essere una buona scelta per i volumi di traduzione di massa quando il tempo di pubblicazione è critico, le aspettative di qualità sono rilassate o i costi di traduzione umana sono proibitivi. Supporto della knowledge base e dei contenuti generati dagli utenti sono comunemente tradotti da macchine.

* Utilizza le competenze dei fornitori di servizi di localizzazione, Adobe Consulting e System Integrator per pianificare, prototipare e testare la tua struttura multilingue del sito.

