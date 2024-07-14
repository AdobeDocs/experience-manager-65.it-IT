---
title: Best practice per la traduzione
description: Trova le best practice compilate dai team tecnici e di consulenza Adobi per aiutarti a iniziare a lavorare su progetti di traduzione.
feature: Language Copy
exl-id: 01a81c4b-cb30-4f7e-b281-7194ebb5fc70
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: eae057caed533ef16bb541b4ad41b8edd7aaa1c7
workflow-type: tm+mt
source-wordcount: '837'
ht-degree: 93%

---

# Best practice per la traduzione{#translation-best-practices}

## Generale {#general}

La creazione o l’espansione di una presenza web globale può essere un processo complesso, ma con una buona previsione e una buona pianificazione AEM può semplificare gli sforzi e supportare gli obiettivi aziendali globali.

* **Pianifica l’espansione globale** prima di implementare il primo sito. Adattare un sito esistente a una copertura globale quando il sito è stato implementato con breve preavviso è tipicamente più difficile del pianificare l’espansione globale all’inizio:

   * Valuta lo stato attuale della maturità di localizzazione della tua organizzazione. Determina se disponi di **strumenti**, **processi** e **risorse** per supportare l’espansione globale.
   * Presta attenzione a **regolamenti globali** e **preferenze linguistiche regionali**. Progetta strutture e processi di contenuto flessibili in grado di adattarsi a un ambiente aziendale globale in continua evoluzione.

* Determina un modello di **governance** che supporta il tuo business globale e utilizza i meccanismi AEM come MSM e autorizzazioni utente per applicare il modello scelto. Ad esempio, puoi determinare se il contenuto verrà creato a livello centrale e “inviato” o “trascinato” alle aree geografiche o ai Paesi. Determina i contenuti che possono essere sbloccati e modificati nelle aree geografiche. Determina chi è responsabile dell’avvio e della gestione delle traduzioni.
* Se le risorse lo consentono, è meglio gestire l’attività di traduzione con un team centrale che può sviluppare competenze negli strumenti, nei processi e nelle relazioni con i fornitori necessari.
* **Pianifica**, **crea un prototipo** e **testa** la struttura e i processi globali per assicurarti che supportino l’attività e che tu disponga del supporto richiesto dalle parti interessate nelle aree geografiche.

## Struttura sito  {#site-structure}

* Durante la progettazione della struttura del sito, esamina innanzitutto il contenuto e determina dove e in quale lingua viene creato il contenuto. Questa posizione deve essere il livello principale del sito.
* La best practice consiste in una **struttura basata sul linguaggio** con un massimo di 3 livelli tra l’authoring di livello superiore e i siti del Paese.
* Utilizza una convenzione di denominazione di un sito in una lingua o in un Paese che segue gli **standard W3C**.
* Determina in che modo i contenuti vengono distribuiti da aree geografiche e Paesi. Considera quali Paesi condividono le lingue. Si consiglia di creare master di lingua, un livello di pagine non attivate, in cui il contenuto tradotto può essere rivisto e modificato e quindi inviato o trascinato a un sito del Paese che condivide tale lingua.
* Sono disponibili due approcci per la creazione di master di lingua: tramite copie per lingua e tramite copie MSM/live.

   * L’approccio basato sulla copia per lingua è quello utilizzato dall’AEM per  un framework di integrazione della traduzione pronto all’uso, e quindi è il modo più semplice per iniziare. Il framework fornisce un’interfaccia utente che semplifica inizialmente la propagazione e la traduzione delle modifiche apportate al contenuto dalla lingua principale (ad esempio inglese) al contenuto principale di un’altra lingua. Tuttavia, man mano che il progetto cresce, l’automazione del flusso di lavoro diventa sempre più necessaria per gestire la traduzione di un maggior numero di pagine e/o lingue.
   * L’approccio MSM/Live Copy può essere un’alternativa per i casi di utilizzo avanzati, in cui i siti sono più grandi e complessi. Una governance forte e l’automazione del flusso di lavoro sono necessarie fin dall’inizio per gestire le complesse relazioni di ereditarietà tra i master in inglese e in lingua e per ridurre il rischio di sovrascrittura delle traduzioni esistenti. Questa gestione può essere effettuata con l’aiuto di alcuni connettori di traduzione. Vedi [MSM e siti multilingue](/help/sites-administering/msm-best-practices.md#msm-and-multilingual-websites) per ulteriori informazioni.

* Se la lingua master dispone di varianti globali, è possibile utilizzare MSM per creare una Live Copy dal master globale da utilizzare per la traduzione. Ad esempio, se l’authoring globale viene eseguito in un master inglese americano, crea un master inglese internazionale come Live Copy e base per la traduzione in altre lingue.
* Utilizza MSM per creare siti nazionali dai master in lingua tradotta e per distribuire contenuti a siti che condividono la stessa lingua. Ad esempio, il master in lingua francese può essere esteso ai siti di Francia, Belgio e Svizzera.
* Pianifica, crea un prototipo e testa prima di avviare l’implementazione.

## Processi e metodi di traduzione {#translation-processes-and-methods}

* Coinvolgi un **fornitore di servizi di localizzazione (LSP)** con competenze in traduzione e relative attività di localizzazione. Tali fornitori possono contribuire a dimensionare la tua attività globale fornendo un’ampia gamma di risorse e tecnologie per migliorare l’efficienza e risparmiare sui costi di traduzione:

   * Alcuni LSP sono sia fornitori di servizi che di tecnologie. Ci sono anche fornitori di tecnologie indipendenti che permettono a molti LSP di condividere le piattaforme di traduzione.
   * Il **framework di traduzione AEM** supporta l’integrazione con diversi fornitori di tecnologie di traduzione sia per la traduzione automatica che per quella umana.
   * Scopri come [integrare i connettori LSP nel sistema AEM](/help/sites-administering/translation.md) per automatizzare la traduzione dei contenuti o come creare, esportare e importare manualmente i progetti di traduzione da testare e nei casi in cui non vi sia alcun fornitore di servizi linguistici o di tecnologia di traduzione.

* Scegli un **metodo di traduzione** più adatto al contenuto.

   * **Traduzione umana** è ideale per i contenuti in cui la messaggistica e le aspettative di qualità sono elevate e il contenuto resterà per un certo periodo di tempo sul sito, come le pagine di marketing.
   * **Traduzione automatica** può essere una buona scelta per grandi volumi di traduzione quando il tempo di pubblicazione è critico, le aspettative di qualità sono informali o i costi di traduzione umana sono proibitivi. I contenuti di supporto della knowledge base e quelli generati dagli utenti sono comunemente tradotti in modalità automatica.

* Utilizza le competenze dei fornitori di servizi di localizzazione, Adobe Consulting e System Integrator per pianificare, creare un prototipo e testare la struttura multilingue del sito.
