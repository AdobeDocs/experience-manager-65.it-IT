---
title: Domande frequenti sulla fine del ciclo di vita del visualizzatore DHTML
seo-title: Domande frequenti sulla fine del ciclo di vita del visualizzatore DHTML
description: A partire dal 31 gennaio 2014, la piattaforma di visualizzatore DHTML di Scene7 terminerà ufficialmente. Questa notifica fornisce le risposte alle domande frequenti in modo da poter preparare la transizione alla nuova piattaforma di visualizzatori HTML5.
seo-description: A partire dal 31 gennaio 2014, la piattaforma di visualizzatore DHTML di Scene7 terminerà ufficialmente. Questa notifica fornisce le risposte alle domande frequenti in modo da poter preparare la transizione alla nuova piattaforma di visualizzatori HTML5.
uuid: a78c03b3-6513-42e1-881f-6a9551659769
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: d94244ac-a5f6-4c95-ab8c-26b41d25863f
translation-type: tm+mt
source-git-commit: 283802809d665cd979e2f1a4fa969b6ddc491ed6
workflow-type: tm+mt
source-wordcount: '1665'
ht-degree: 0%

---


# Domande frequenti sulla fine del ciclo di vita del visualizzatore DHTML{#dhtml-viewer-end-of-life-faqs}

A partire dal 31 gennaio 2014, la piattaforma di visualizzatore DHTML di Scene7 terminerà ufficialmente. Questa notifica fornisce le risposte alle domande frequenti in modo da poter preparare la transizione alla nuova piattaforma di visualizzatori HTML5.

**Qual è il cambiamento?**

A partire dal 31 gennaio 2014, Scene7 cesserà ufficialmente di supportare la piattaforma di visualizzatori DHTML.

**Cosa significa fine vita?**

Fine del ciclo di vita significa che Scene7 (1) non aggiungerà più miglioramenti di funzionalità alla piattaforma di visualizzatore DHTML (2) non risolve più né rilascerà correzioni di bug sulla piattaforma di visualizzatore DHTML e (3) l’assistenza clienti non risolverà più problemi o non fornirà più supporto per problemi o domande relativi al visualizzatore DHTML.

**Perché Scene7 sta apportando questa modifica?**

Gli standard Web sono in costante evoluzione e DHTML è una vecchia tecnologia di sviluppo Web che viene rapidamente sostituita da HTML5. Il limite più grande per DHTML come piattaforma è che non è in grado di creare la ricchezza di esperienza che HTML5 ora può supportare in modo coerente e più semplice su più browser. Ad esempio, tali limitazioni includono la mancanza di supporto tra browser per:

* Cursori personalizzati
* Angoli arrotondati
* Animazioni (come capovolgimento della pagina, riduzione dello zoom)
* Effetti (ad esempio ombre, bagliori)
* Supporto completo dei font
* Riproduzione video senza plug-in

Specifico per la piattaforma visualizzatore Scene7 DHTML, sia la soluzione basata su JSP che le API Javascript non sono state ottimizzate per i dispositivi mobili per sfruttare le funzionalità multi-touch e gestuale. E anche se i visualizzatori DHTML rilasciati nel 2011/inizio 2012 sono ottimizzati per dispositivi mobili, erano difficili da personalizzare e mantenere a causa della mancanza di un framework di sviluppo flessibile basato su componenti SDK.

Basato su queste limitazioni su DHTML e sulla trazione rapida del settore con HTML5 come standard emergente sia per desktop che per dispositivi mobili, Scene7 ha deciso di investire in una piattaforma visualizzatore basata su HTML5. Questo investimento offrirà ai nostri clienti una piattaforma affidabile grazie alla quale possono creare visualizzatori interattivi più ricchi e coinvolgenti in grado di raggiungere gli utenti su schermi diversi, inclusi i dispositivi desktop, iOS e Android.

**Come posso sapere se il mio visualizzatore utilizza la piattaforma DHTML?**

Per determinare se il visualizzatore utilizzato dalla società è DHTML e quindi interessato da questa modifica, controllate se:

1. La società utilizza un visualizzatore Scene7 fornito in dotazione elencato in questa tabella in cui &quot;Viewer Technology&quot; è designato come &quot;DHTML&quot;:

   [https://help.adobe.com/en_US/scene7/using/WS6E593DEA-7D81-4cd6-84B0-85E8BB274176.html#WS1c46793299cf21d77e926d1613177f0a020-8000](https://help.adobe.com/en_US/scene7/using/WS6E593DEA-7D81-4cd6-84B0-85E8BB274176.html#WS1c46793299cf21d77e926d1613177f0a020-8000)

1. La società sta utilizzando un visualizzatore creato come nuovo predefinito basato su un visualizzatore Scene7 fornito con voi in questa tabella in cui &quot;Viewer Technology&quot; è designato come &quot;DHTML&quot;:

   [https://help.adobe.com/en_US/scene7/using/WS6E593DEA-7D81-4cd6-84B0-85E8BB274176.html#WS1c46793299cf21d77e926d1613177f0a020-8000](https://help.adobe.com/en_US/scene7/using/WS6E593DEA-7D81-4cd6-84B0-85E8BB274176.html#WS1c46793299cf21d77e926d1613177f0a020-8000)

1. La società utilizza un visualizzatore personalizzato creato dalla soluzione DHTML basata su JSP:

   [https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#JSP_Reference](https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#JSP_Reference)

1. La società utilizza un visualizzatore personalizzato creato dall&#39;API JavaScript:

   [https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#API_Reference](https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#API_Reference)

1. La società utilizza un visualizzatore personalizzato creato con l’API a comparsa multischermo DHTML:

   [https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#Multi-screen_Flyout_Viewer](https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#Multi-screen_Flyout_Viewer)

1. La società utilizza un visualizzatore personalizzato creato con l’API a comparsa per desktop DHTML:

   [https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#Desktop_Flyout_Viewer](https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#Desktop_Flyout_Viewer)

1. La società utilizza una libreria di rilevamento dispositivi che fa parte del pacchetto visualizzatori DHTML:

   Cerca JS include nel codice &quot;sj_deviceDetect.js&quot;.

   Questo è stato sostituito dal nuovo codice di rilevamento dispositivo JS qui: [https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#Detecting_devices_and_browsers](https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#Detecting_devices_and_browsers) .

**Che cos’è la piattaforma di visualizzatore sostitutiva?**

La sostituzione per DHTML è la piattaforma visualizzatore Scene7 HTML5, composta da:

* Visualizzatori HTML5 out-of-box con interazioni ottimizzate per dispositivi mobili su numerosi tipi di visualizzatori, tra cui zoom di base, zoom a comparsa, set di immagini, set di campioni, set 360 gradi multidimensionali e file multimediali diversi. Per esempi aggiornati di questi visualizzatori, consultate: [https://microsite.omniture.com/t2/help/en_US/s7/vlist/vlist.html](https://microsite.omniture.com/t2/help/en_US/s7/vlist/vlist.html)
* SDK per visualizzatori HTML5 che consente di personalizzare  visualizzatori Adobe Scene7 per i siti e i dispositivi supportati da HTML5 (come iOS e Android), fornendo la massima flessibilità e creatività per conferire al visualizzatore aspetto e interattività il massimo marchio. I vantaggi dei componenti riutilizzabili ottimizzati per le prestazioni riducono i costi complessivi di sviluppo del visualizzatore e accelerano lo sviluppo personalizzato.

**Per quando la piattaforma visualizzatore HTML5 avrà le funzioni necessarie per la transizione dalla piattaforma visualizzatore DHTML?**

Scene7 ha rilasciato il primo SDK per visualizzatori HTML5 nell’autunno 2011 con l’avvio della versione 5.5. Da allora, abbiamo aggiunto numerose funzionalità alla piattaforma e supporto esteso per un numero sempre maggiore di tipi di visualizzatori. Per la maggior parte dei requisiti comuni per i visualizzatori, è probabile che la piattaforma per visualizzatori HTML5 disponga già delle funzioni necessarie per effettuare la migrazione. E continuiamo a investire in modo aggressivo in questa piattaforma di visualizzatori con rilasci ogni trimestre.

Per determinare se i requisiti del visualizzatore possono essere soddisfatti oggi con la piattaforma per visualizzatori HTML5, consultate la seguente documentazione:

[https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#About_HTML5_Viewers](https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#About_HTML5_Viewers) (per visualizzatori out-of-box e funzionalità di personalizzazione)

[https://help.adobe.com/en_US/scene7/using/WSd4272150f67705c11b002eec12fcba4dee6-8000.html](https://help.adobe.com/en_US/scene7/using/WSd4272150f67705c11b002eec12fcba4dee6-8000.html) (per accedere alla documentazione dell&#39;SDK API)

Se non siete ancora certi se l’SDK per visualizzatori HTML5 può soddisfare i vostri requisiti, rivolgetevi al nostro team di servizi professionali.

**Come si trasferiscono i visualizzatori sulla piattaforma HTML5?**

Per trasferire i visualizzatori alla piattaforma HTML5, Scene7 offre le seguenti opzioni:

1. Utilizzate uno dei visualizzatori HTML5 forniti da Scene7, di cui potete trovare alcuni esempi: [https://microsite.omniture.com/t2/help/en_US/s7/vlist/vlist.html](https://microsite.omniture.com/t2/help/en_US/s7/vlist/vlist.html)
1. Configurate uno dei visualizzatori HTML5 integrati in Scene7 nella configurazione dell’applicazione SPS. Questo consente di personalizzare determinati comportamenti quali le dimensioni del visualizzatore, le transizioni, il comportamento di zoom, ecc.: [https://help.adobe.com/en_US/scene7/using/WS6E593DEA-7D81-4cd6-84B0-85E8BB274176.html](https://help.adobe.com/en_US/scene7/using/WS6E593DEA-7D81-4cd6-84B0-85E8BB274176.html)
1. Personalizzate l’aspetto dei visualizzatori HTML5 integrati in Scene7 modificando i CSS per modificare la progettazione visiva, ad esempio l’immagine di un pulsante, la posizione, la trasparenza, i colori di sfondo e così via: [https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#Customizing_HTML5_Viewers](https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#Customizing_HTML5_Viewers)
1. Create un visualizzatore HTML5 personalizzato da zero utilizzando l’SDK che può essere scaricato qui: [https://help.adobe.com/en_US/scene7/using/WSd4272150f67705c11b002eec12fcba4dee6-8000.html](https://help.adobe.com/en_US/scene7/using/WSd4272150f67705c11b002eec12fcba4dee6-8000.html). Potete interagire con i servizi professionali per creare il visualizzatore personalizzato o farlo costruire dal vostro team di sviluppo Web.

**E per i browser che non supportano HTML5?**

HTML5 è supportato su molti dispositivi mobili e browser Web e continua a conquistare la trazione. Attualmente, anche se HTML5 non è supportato su Internet Explorer 8 o versioni successive, Scene7 ha innovato la nostra piattaforma di visualizzatori HTML5 per estendere il supporto anche a IE 7 e IE 8. Con la piattaforma per visualizzatori Scene7 HTML5 , potete raggiungere la stragrande maggioranza degli utenti desktop e mobili con un’unica piattaforma di sviluppo.

Gli attuali requisiti di sistema a partire dalla versione SDK HTML5 2.2.1 sono:

* Microsoft® Windows® XP o versione successiva, Macintosh® OS X 10.6 o versione successiva
* Firefox 17, Safari 5.1, Chrome 23, Internet Explorer 7 o versione successiva
* iOS 3.2.2 o successivo
* Certificato su iPhone3 o versione successiva e iPad1 o versione successiva (browser nativi)
* Android OS 2.2 o successivo

Per verificare se il browser è compatibile con la piattaforma di visualizzatori HTML5, avviate il seguente visualizzatore di esempio:

[https://s7d1.scene7.com/s7viewers/html5/flyout.html?asset=Scene7SharedAssets/Sample%20Image](https://s7d1.scene7.com/s7viewers/html5/flyout.html?asset=Scene7SharedAssets/Sample%20Image)

Se l’immagine ingrandita viene visualizzata passando il mouse o trascinando il dito sull’immagine principale, è un browser/dispositivo supportato.

**Quali opzioni sono disponibili se si desidera restare in produzione con il visualizzatore DHTML esistente?**

Anche se potete ancora essere live in produzione con visualizzatori basati su DHTML, è importante notare che dopo il 31 gennaio 2014 non vi saranno miglioramenti, correzioni di bug né assistenza clienti. Di conseguenza, consigliamo a tutti i clienti di migrare alla piattaforma di visualizzatori HTML5 più affidabile. . Tuttavia, se la vostra situazione aziendale impedisce tale migrazione entro la data EOL, avete la possibilità di stipulare contratti con i servizi professionali per estendere il periodo di manutenzione supportato. Per maggiori informazioni, contatta il tuo account manager.

**Chi posso contattare per maggiori informazioni?**

Se questa domanda frequente non risponde a tutte le tue domande, [utilizza il Admin Console  per creare un caso](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html) di assistenza o contatta il tuo account manager  Adobe.
