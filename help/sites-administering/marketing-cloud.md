---
title: Integrazione con Adobe Marketing Cloud
description: Scopri come integrare Adobe Experience Manager con Adobe Marketing Cloud.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
exl-id: ba518290-dd82-44dc-ae7c-c8152df89179
source-git-commit: d19b203ffe75a5628f350113d4d74a2916beffc8
workflow-type: tm+mt
source-wordcount: '998'
ht-degree: 1%

---

# Integrazione con Adobe Marketing Cloud{#integrating-with-the-adobe-marketing-cloud}

Il [Adobe Marketing Cloud](https://www.adobe.com/solutions/digital-marketing.html) include potenti prodotti di analisi web e ottimizzazione di siti web che forniscono dati e informazioni fruibili e in tempo reale per promuovere iniziative online di successo. Offre una piattaforma integrata e aperta per l&#39;ottimizzazione aziendale online. Cloud è costituito da applicazioni integrate per raccogliere e sfruttare la potenza delle informazioni sui clienti al fine di ottimizzare le attività di acquisizione, conversione e fidelizzazione dei clienti, nonché la creazione e la distribuzione di contenuti.

Con Adobe Experience Manager (AEM) puoi integrarti perfettamente con i seguenti prodotti di Adobe Marketing Cloud:

* Adobe Analytics fornisce agli esperti di marketing informazioni fruibili e in tempo reale sulle strategie online e le iniziative di marketing.
* Adobe Target offre agli esperti di marketing la possibilità di rendere i contenuti online sempre più rilevanti per i clienti, ottenendo una maggiore conversione.
* Adobe Dynamic Media Classic automatizza la gestione dei contenuti multimediali, semplifica la pubblicazione web e migliora le esperienze web, il tutto in un ambiente in hosting.
* Adobe Dynamic Tag Management offre agli addetti al marketing strumenti intuitivi per gestire in modo rapido e semplice un numero illimitato di tag di Adobe e di terze parti.
* Adobe Search&amp;Promote offre agli addetti al marketing la possibilità di controllare e ottimizzare i risultati della ricerca sui loro siti.
* Adobe Campaign ti consente di gestire il contenuto delle e-mail di consegna direttamente in Adobe Experience Manager.

Inoltre, è possibile [integrare AEM con Creative Cloud](/help/assets/aem-cc-integration-best-practices.md) e con [servizi di terze parti](/help/sites-administering/third-party-services.md).

## Integrazione con Adobe Analytics {#integrating-with-adobe-analytics}

[Adobe ](https://www.omniture.com/en/products/analytics/sitecatalyst) Analytics è la soluzione leader di settore che offre agli esperti di marketing digitale un’unica posizione per misurare, analizzare e ottimizzare i dati integrati da tutte le iniziative online su più canali di marketing. Fornisce agli esperti di marketing informazioni analitiche web fruibili e in tempo reale sulle strategie digitali e sulle iniziative di marketing. Adobe Analytics aiuta gli esperti di marketing a identificare rapidamente i percorsi più redditizi attraverso un sito web, segmentare il traffico per individuare i visitatori web di alto valore, determinare dove i visitatori si spostano fuori dal sito e identificare metriche di successo critiche per le campagne di marketing online.

Puoi utilizzare Adobe Analytics per analizzare i dati dai tuoi siti.

L’integrazione con Adobe Analytics consente di effettuare le seguenti operazioni:

* Abilita il tracciamento degli utenti di Analytics.
* Mappa le modalità di esecuzione (ad esempio autore e pubblicazione) su suite di rapporti diverse.
* Invia variabili di contesto client come variabili di conversione o proprietà del traffico.
* Utilizza mappature variabili predefinite.
* Configura le sezioni complete del sito contemporaneamente.
* Tracciare eventi personalizzati.

Per informazioni sull&#39;integrazione di AEM con Analytics, consulta [Integrazione con Adobe Analytics](/help/sites-administering/adobeanalytics.md).

Puoi inoltre utilizzare la [procedura guidata di consenso](/help/sites-administering/opt-in.md) per eseguire facilmente l&#39;integrazione.

## Integrazione con Adobe Target {#integrating-with-adobe-target}

[Gli esperti di marketing utilizzano ](https://www.omniture.com/en/products/conversion/test-and-target) Target per progettare ed eseguire test online, creare al volo segmenti di pubblico on-the-fly (in base al comportamento) e automatizzare il targeting di contenuti ed esperienze online.

Oggi i consumatori online hanno esigenze in continua evoluzione e si aspettano contenuti pertinenti, anche personalizzati, dall&#39;ampia varietà di siti e fonti di contenuto tra cui possono scegliere. Per coinvolgere un pubblico online, è fondamentale che gli esperti di marketing online identifichino rapidamente quali offerte e contenuti sono rilevanti e convincenti per il pubblico. Grazie a queste conoscenze, gli esperti di marketing devono poter sviluppare continuamente i propri siti e indirizzare i contenuti appropriati a diversi tipi di pubblico.

[L’integrazione con Adobe ](/help/sites-administering/target.md) Target spiega come integrare il sito con Target.

Puoi inoltre utilizzare la [procedura guidata di consenso](/help/sites-administering/opt-in.md) per eseguire facilmente l&#39;integrazione.

## Consenso ad Analytics e Target {#opting-in-to-analytics-and-target}

AEM fornisce una semplice procedura di consenso da integrare con Adobe Analytics e Adobe Target. Quando accedi come amministratore e visita la console Progetti , viene visualizzata una procedura guidata di consenso.

![chlimage_1-107](assets/chlimage_1-107a.png)

Effettua l’integrazione con Analytics e/o Target per abilitare l’utilizzo delle funzionalità di tracciamento e analisi delle pagine e delle funzionalità di personalizzazione. Quando si sceglie il consenso, è necessario fornire le informazioni sul proprio account utente e specificare le pagine che vengono tracciate.

Per ulteriori informazioni, consulta [Scelta di Adobe Analytics e Adobe Target.](/help/sites-administering/opt-in.md)

## Integrazione con Adobe Dynamic Media Classic {#integrating-with-scene}

Adobe Dynamic Media Classic è una soluzione in hosting per la pubblicazione, la gestione, l’ottimizzazione e la distribuzione di risorse di marketing dinamiche e di materiale video di merchandising su web, dispositivi mobili, e-mail, social media, display collegati a Internet e stampa.

In Adobe Experience Manager puoi pubblicare risorse digitali direttamente da Adobe Experience Manager a Dynamic Media Classic e da Dynamic Media Classic ad Adobe Experience Manager.

Inoltre, puoi visualizzare le risorse Adobe Experience Manager pubblicate in Dynamic Media Classic in vari visualizzatori, come Zoom di base e Video.

Per ulteriori informazioni sulle modalità di integrazione di Adobe Experience Manager con Dynamic Media Classic, consulta la documentazione [Integrazione con Dynamic Media Classic](/help/sites-administering/scene7.md) .

## Integrazione con Adobe Dynamic Tag Management {#integrating-with-adobe-dynamic-tag-management}

[Adobe Dynamic Tag ](https://www.adobe.com/solutions/digital-marketing/dynamic-tag-management.html) Management offre agli addetti al marketing strumenti intuitivi per gestire in modo rapido e semplice un numero illimitato di tag di Adobe e di terze parti. Potrai avere più controllo e flessibilità per ottimizzare praticamente tutto online, riducendo al contempo la dipendenza dalle risorse IT.

[Integra la Dynamic Tag ](/help/sites-administering/dtm.md) Management di Adobe con AEM in modo da poter utilizzare le proprietà web di Dynamic Tag Management per tenere traccia AEM siti.

## Integrazione con Adobe Audience Manager {#integrating-with-adobe-audience-manager}

L’integrazione di Audience Manager è stata rimossa in AEM 6.3.

## Integrazione con Search&amp;Promote {#integrating-with-search-promote}

Un Search&amp;Promote di Adobe consente agli esperti di marketing di ottimizzare il modo in cui i visitatori navigano, trovano, confrontano e selezionano prodotti e contenuti rilevanti sui siti web e mobili. Le aziende possono promuovere facilmente gli elementi prioritari in base agli obiettivi aziendali e alle finalità dei visitatori, nonché automatizzare le attività di merchandising e promozioni tramite trigger o metriche basate su KPI.

Adobe Search&amp;Promote è un&#39;applicazione affidabile e scalabile per la ricerca di siti in hosting, in grado di scalare fino a milioni di pagine o prodotti, per aziende online molto visitate che vanno dal retail ai siti di notizie. Offre livelli senza precedenti di controllo degli addetti al marketing e rilevanza basata sulle metriche.

Per informazioni sull&#39;integrazione di AEM e Search&amp;Promote, vedere [Integrazione con Adobe Search&amp;Promote](/help/sites-administering/search-and-promote.md).

## Integrazione con Adobe Campaign {#integrating-with-adobe-campaign}

[Adobe ](https://www.adobe.com/solutions/campaign-management.html) Campaign consente di gestire i contenuti delle e-mail inviate direttamente in Adobe Experience Manager.

Per informazioni su come AEM si integra con Adobe Campaign, consulta [Integrazione con Adobe Campaign](/help/sites-administering/campaignstandard.md).

## Integrazione con Livefyre {#integrating-with-livefyre}

Scopri AEM e Livefyre:

* [Guida introduttiva di Livefyre](https://answers.livefyre.com/developers/getting-started)

* [Livefyre e AEM](https://answers.livefyre.com/product/livefyre-for-adobe-experience-manager-aem/livefyre-for-adobe-experience-manager/)
