---
title: Integrazione con Adobe Marketing Cloud
seo-title: Integrazione con Adobe Marketing Cloud
description: Scopri come integrare AEM con Adobe Marketing Cloud.
seo-description: Scopri come integrare AEM con Adobe Marketing Cloud.
uuid: 36d71dd3-7fb0-4237-99d3-4fbb2e162e7b
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: ba496f6a-c9aa-49b5-8207-8633748d2c17
translation-type: tm+mt
source-git-commit: 471b57a52efc849eb57201e6397221fa4f88c746

---


# Integrazione con Adobe Marketing Cloud{#integrating-with-the-adobe-marketing-cloud}

Adobe [Marketing Cloud](https://www.adobe.com/solutions/digital-marketing.html)include potenti prodotti di analisi Web e ottimizzazione per siti Web che forniscono dati e informazioni fruibili e in tempo reale per promuovere iniziative online di successo. Offre una piattaforma integrata e aperta per l&#39;ottimizzazione del business online. Il Cloud è costituito da applicazioni integrate per raccogliere e sfruttare al meglio le informazioni fornite dai clienti al fine di ottimizzare le attività di acquisizione, conversione e conservazione dei clienti, nonché la creazione e distribuzione di contenuti.

Con Adobe Experience Manager (AEM), potete effettuare l&#39;integrazione diretta con i seguenti prodotti Adobe Marketing Cloud:

* Adobe Analytics offre agli esperti di marketing informazioni fruibili e in tempo reale sulle strategie online e le iniziative di marketing.
* Adobe Target offre agli esperti di marketing la possibilità di rendere i contenuti online sempre più rilevanti per i clienti — ottenere una maggiore conversione.
* Adobe Scene7 automatizza la gestione dei contenuti multimediali, ottimizza la pubblicazione Web e ottimizza le esperienze Web in un ambiente ospitato.
* Adobe Dynamic Tag Management offre agli esperti di marketing strumenti intuitivi per gestire in modo rapido e semplice un numero illimitato di tag Adobe e di terze parti.
* Adobe Search&amp;Promote offre agli addetti al marketing la possibilità di controllare e ottimizzare i risultati della ricerca sui propri siti.
* Adobe Campaign consente di gestire i contenuti di distribuzione delle e-mail direttamente in Adobe Experience Manager.

Inoltre, potete [integrare AEM con Creative Cloud](/help/assets/aem-cc-folder-sharing-best-practices.md) e con servizi [di](/help/sites-administering/third-party-services.md)terze parti.

## Integrazione con Adobe Analytics {#integrating-with-adobe-analytics}

[Adobe Analytics](https://www.omniture.com/en/products/analytics/sitecatalyst) è la soluzione leader di settore che offre agli esperti di marketing digitale un&#39;unica soluzione per misurare, analizzare e ottimizzare i dati integrati da tutte le iniziative online attraverso più canali di marketing. Fornisce ai professionisti del marketing informazioni analitiche Web fruibili e in tempo reale sulle strategie digitali e sulle iniziative di marketing. Adobe Analytics aiuta gli esperti di marketing a identificare rapidamente i percorsi più redditizi attraverso un sito Web, segmentare il traffico per individuare i visitatori Web di alto valore, determinare dove i visitatori si stanno allontanando dal sito e identificare metriche di successo importanti per le campagne di marketing online.

Puoi utilizzare Adobe Analytics per analizzare i dati dai tuoi siti.

L’integrazione con Adobe Analytics consente di effettuare le seguenti operazioni:

* Abilita il tracciamento utente di Analytics.
* Mappatura delle modalità di esecuzione (ad esempio creazione e pubblicazione) su suite di rapporti diverse.
* Invia le variabili ClientContext come variabili di conversione o proprietà di traffico.
* Utilizzare mappature variabili predefinite.
* Configurare le sezioni complete del sito contemporaneamente.
* Tracciamento degli eventi personalizzati.

Per informazioni sull&#39;integrazione di AEM con Analytics, consultate [Integrazione con Adobe Analytics](/help/sites-administering/adobeanalytics.md).

Potete inoltre utilizzare la procedura guidata di [consenso](/help/sites-administering/opt-in.md) per eseguire facilmente l&#39;integrazione.

## Integrazione con Adobe Target {#integrating-with-adobe-target}

[Adobe Target](https://www.omniture.com/en/products/conversion/test-and-target) è utilizzato dagli esperti di marketing per progettare ed eseguire test online, creare segmenti di pubblico on-the-fly (basati sul comportamento) e automatizzare il targeting dei contenuti e delle esperienze online.

Oggi i consumatori online hanno esigenze in continua evoluzione e si aspettano contenuti pertinenti, anche personalizzati, dall&#39;ampia varietà di siti e fonti di contenuti tra cui possono scegliere. Per coinvolgere un pubblico online, è fondamentale che gli esperti di marketing online identifichino rapidamente quali offerte e quali contenuti sono rilevanti e coinvolgenti per il pubblico. Grazie a queste conoscenze, gli esperti di marketing devono poter sviluppare continuamente i propri siti e indirizzare i contenuti appropriati a diversi tipi di pubblico.

[L&#39;integrazione con Adobe Target](/help/sites-administering/target.md) spiega come integrare il sito con Target.

Potete inoltre utilizzare la procedura guidata di [consenso](/help/sites-administering/opt-in.md) per eseguire facilmente l&#39;integrazione.

## Accesso ad Analytics e Target {#opting-in-to-analytics-and-target}

AEM fornisce una semplice procedura di consenso per l&#39;integrazione con Adobe Analytics e Adobe Target. Quando effettuate l’accesso come amministratore e visitate la console Progetti, viene visualizzata una procedura guidata di consenso.

![chlimage_1-107](assets/chlimage_1-107a.png)

Scegli l&#39;integrazione con Analytics e/o Target per consentire l&#39;utilizzo delle funzionalità di tracciamento e analisi delle pagine e di personalizzazione. Quando si sceglie di effettuare l&#39;accesso, è necessario fornire le informazioni sull&#39;account utente e specificare le pagine che vengono tracciate.

Per ulteriori informazioni, consulta [Scelta in Adobe Analytics e Adobe Target.](/help/sites-administering/opt-in.md)

## Integrazione con Scene7 {#integrating-with-scene}

[Adobe Scene7](https://www.adobe.com/products/scene7.html) è una soluzione in hosting per la pubblicazione, la gestione, il miglioramento e la distribuzione di risorse di marketing dinamiche e merchandising visivo avanzati per il Web, il mobile, l’e-mail, i social media, i display e la stampa collegati a Internet.

In AEM, potete pubblicare risorse digitali direttamente da AEM a Scene7 e pubblicare risorse digitali da Scene7 ad AEM.

Inoltre, potete visualizzare le risorse AEM pubblicate in Scene7 in diversi visualizzatori:

* Zoom di base
* Zoom a comparsa DHTML
* Zoom a comparsa Flash
* Video
* Flash Modello
* Modello immagini

Per ulteriori informazioni sulla modalità di integrazione di AEM con Scene7, consultate la documentazione [](/help/sites-administering/scene7.md)Integrazione con Scene7.

## Integrazione con Adobe Dynamic Tag Management {#integrating-with-adobe-dynamic-tag-management}

[Adobe Dynamic Tag Management](https://www.adobe.com/solutions/digital-marketing/dynamic-tag-management.html) offre agli esperti di marketing strumenti intuitivi per gestire in modo rapido e semplice un numero illimitato di tag Adobe e di terze parti. Potrai avere maggiore controllo e flessibilità per ottimizzare praticamente tutto online, riducendo al contempo la dipendenza dalle risorse IT.

[Integra Adobe Dynamic Tag Management](/help/sites-administering/dtm.md) con AEM per poter utilizzare le proprietà Web di Gestione tag dinamica per tenere traccia dei siti AEM.

## Integrazione con Adobe Audience Manager {#integrating-with-adobe-audience-manager}

L’integrazione di Audience Manager è stata rimossa in AEM 6.3.

## Integrazione con Search&amp;Promote {#integrating-with-search-promote}

[Adobe Search&amp;Promote](https://www.omniture.com/en/products/conversion/search-and-promote) consente agli esperti di marketing di ottimizzare il modo in cui i visitatori consultano, trovano, confrontano e selezionano prodotti e contenuti pertinenti sul Web e sui siti mobili. Le aziende possono promuovere facilmente gli elementi prioritari in base agli obiettivi aziendali e alle intenzioni dei visitatori, nonché automatizzare le attività di merchandising e promozioni tramite attivatori o metriche basate su KPI.

Adobe Search&amp;Promote è un&#39;applicazione affidabile e scalabile per la ricerca di siti in hosting, in grado di scalare fino a milioni di pagine o prodotti, per aziende online molto visitate che vanno dalla vendita al dettaglio ai siti di notizie. Offre livelli senza precedenti di controllo degli esperti di marketing e rilevanza basata sulle metriche.

Per informazioni sull’integrazione di AEM e Search&amp;Promote, consultate [Integrazione con Adobe Search&amp;Promote](/help/sites-administering/search-and-promote.md).

## Integrazione con Adobe Campaign {#integrating-with-adobe-campaign}

[Adobe Campaign](https://www.adobe.com/solutions/campaign-management.html) consente di gestire i contenuti di distribuzione delle e-mail direttamente in Adobe Experience Manager.

Per informazioni sul modo in cui AEM si integra con Adobe Campaign, consulta [Integrazione con Adobe Campaign](/help/sites-administering/campaignstandard.md).

## Integrazione con Livefyre {#integrating-with-livefyre}

Informazioni su AEM e Livefyre:

* [Guida introduttiva di Livefyre](https://answers.livefyre.com/developers/getting-started)

* [Livefyre e AEM](https://answers.livefyre.com/product/livefyre-for-adobe-experience-manager-aem/livefyre-for-adobe-experience-manager/)

