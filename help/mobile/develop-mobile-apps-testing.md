---
title: Verifica delle app mobili
seo-title: Verifica delle app mobili
description: 'null'
seo-description: 'null'
uuid: 3b402d34-5cab-4280-b8b9-88ad9f8fc5e4
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing
content-type: reference
discoiquuid: 5a98e1bd-f5c1-4f2f-ac02-dbd005dc1de7
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '1027'
ht-degree: 0%

---


# Verifica delle app mobili{#testing-mobile-apps}

>[!NOTE]
>
> Adobe consiglia di utilizzare l&#39;editor SPA per i progetti che richiedono il rendering lato client basato sul framework dell&#39;applicazione a pagina singola (ad es. React). [Per saperne di più](/help/sites-developing/spa-overview.md).

Data l&#39;ampia gamma di dispositivi sul mercato e dispositivi in fase di rilascio, il test delle app è diventato estremamente importante. Si tratta di un&#39;area in cui funzionalità e facilità d&#39;uso possono generare recensioni ridotte su un app store, ma un singolo difetto può causare la disinstallazione dell&#39;app. Occorre prestare attenzione ai piani di test e alla garanzia della qualità. Il collegamento seguente illustra molti degli argomenti che devono essere affrontati in generale, ad esempio, identificare l&#39;ambiente, definire casi di test, tipi di test, ipotesi, coinvolgimento del cliente, ecc. Sono stati inoltre discussi gli strumenti per facilitare il lavoro di test. Gli strumenti interni, come [Hobbes](/help/sites-developing/hobbes.md), possono essere utili per i test dell&#39;interfaccia utente basati sul Web. [Dura ](/help/sites-developing/tough-day.md) Daycan sottolineare le vostre istanze con un carico simulato. Se l&#39;ambiente di test dispone già di esperienza con strumenti 3rd-party, come Selenium, anche questi possono essere utilizzati.

Quando si sviluppa un&#39;app mobile, esistono molti nuovi problemi specifici per i dispositivi che devono essere affrontati insieme a quelli dei test tradizionali.

* Funzionalità: Tutti i requisiti sono soddisfatti dall&#39;app?
* Usabilità: l&#39;app è facile da usare e comprendere per il cliente?
* Prestazioni - Cosa succede durante un picco di utilizzo? Gli elementi dell&#39;app, come lo scorrimento e il cursore del mouse, sono rapidi e non distogliono l&#39;esperienza?
* Errore o Interruzioni: cosa accade in caso di chiamata o notifica in arrivo durante l&#39;esecuzione dell&#39;app? Cosa succede in caso di interruzione o spegnimento della rete?
* Installazione e aggiornamenti - Com&#39;è l&#39;esperienza di installazione? In che modo gli aggiornamenti vengono rifiutati?
* Tecnico - L&#39;app sta consumando troppa energia da un dispositivo?
* Localizzazione: tutte le aree dell&#39;app sono tradotte?
* Certificazione - L&#39;app è stata certificata? I clienti possono essere certi che rispetta tutti i requisiti legali sulla privacy dei dati?

Queste domande devono essere risolte durante il test automatico e manuale.

## Test automatico {#automated-testing}

È opportuno eseguire un certo grado di test automatizzato per coprire la varietà di dimensioni dello schermo, vincoli di memoria, metodi di input e sistemi operativi. Non solo copre gran parte dei casi di test, ma può accelerare il test di regressione quando vengono introdotte nuove funzioni o dispositivi. Idealmente, gli strumenti di automazione dovrebbero ridurre o limitare la duplicazione degli sforzi. Utilizzate strumenti o framework in modo che il vostro sforzo di test sia applicabile a tutte le piattaforme. Il grafico seguente mostra una struttura semplificata di un ambiente di test sia per i test dell&#39;interfaccia utente basati sul Web che per i test delle app mobili. Il lato sinistro del grafico mostra una serie di nodi Selenium con i browser. SeleniumGrid consente di sottoporre a farm test dell’interfaccia utente comuni basati sul Web per uno qualsiasi di questi nodi. L&#39;hub di Selenium può anche connettersi ad Appium per il test delle app su più piattaforme. Vengono visualizzati solo i simulatori, ma potete incorporare adb, per le utility Android e Xcode per i dispositivi iOS. I collegamenti sono disponibili più avanti in questo documento, dove è possibile trovare dettagli specifici per gli strumenti indicati.

![chlimage_1](assets/chlimage_1.jpeg)

## Test manuale {#manual-testing}

Oltre al test automatizzato, l&#39;app deve seguire un ciclo di test manuali. I clienti che eseguono l&#39;app su un dispositivo reale non possono essere duplicati da uno script. Anche qui, avete molte opzioni. Potete utilizzare una piattaforma, come HockeyApp, per definire chi ha accesso e raccogliere i commenti. Oppure potete affidare l’intero processo a un servizio come UTest, ElusiveStars o Testin. Se disponete di un gruppo di tester interni, ma senza differenze tra i dispositivi, vi sono servizi cloud in cui potete eseguire test manuali sui loro pool di dispositivi. Uno di questi servizi che fornisce questo è SauceLabs. Potete anche creare app in remoto su PhoneGap Enterprise e installarle sui dispositivi locali come livello di test di accettazione o demo. Per informazioni sulle funzioni e la documentazione più recenti, visitare il sito Web [PhoneGap](https://phonegap.com/). Qualunque sia l&#39;approccio, le prove manuali devono essere effettuate;

* colpire un grande bersaglio di tester,
* eseguire il test su un ampio pool di dispositivi (dispositivi ideali reali, ma simulatori/emulatori se non sono disponibili dispositivi reali),
* fornire feedback informativi:

   * segnalazioni di arresto anomalo,
   * analytics/tracking,
   * usabilità,
   * aree di attenzione,
   * prestazioni,
   * consumo di dati/energia, ecc.

## Strumenti {#tools}

È disponibile un&#39;ampia gamma di strumenti per testare le app mobili. La scelta di quelli da utilizzare dipende dalla vostra situazione specifica: caratteristiche, prezzo, supporto, copertura, ecc. Segue una breve descrizione di alcuni strumenti e servizi disponibili.

**Selenio**

* Framework che include un&#39;API per il test degli script per il feed WebDriver e il controllo di vari browser.
* Potete utilizzarlo insieme ad Appium per eseguire test sui dispositivi reali.
* SeleniumGrid indirizza i test su nodi per test paralleli.
* L&#39;IDE selenio aiuta a ridurre la scrittura di test case.

Per ulteriori informazioni, vedere [https://www.seleniumhq.org/](https://www.seleniumhq.org/).

**Testdroid**

* Un servizio di test basato su cloud con ganci di integrazione continui e test dei dispositivi reali.
* Include un App Crawler che verifica la compatibilità del dispositivo, analizza i registri, attraversa le viste, prende le schermate e monitora le prestazioni.

Per ulteriori informazioni, vedere [https://testdroid.com/](https://testdroid.com/).

**Appio**

* Appium è un framework multipiattaforma popolare per l&#39;automazione di test mobili.
* Inoltre, un ispettore è dotato delle capacità di registrazione per aiutare i casi di test del codice.

Per ulteriori informazioni, vedere [https://appium.io/](https://appium.io/).

**SauceLabs**

* SauceLabs fornisce test basati su cloud e si integra con l&#39;integrazione continua.
* I test vengono eseguiti automaticamente nel loro ambiente cloud oppure è possibile avviare un dispositivo o una piattaforma particolare ed eseguire test manuali per facilitare il debug dei problemi.

Per ulteriori informazioni, vedere [https://saucelabs.com/](https://saucelabs.com/).

**AppTestNow**

* Un servizio di outsourcing per il test delle app mobili.
* Include un ampio pool di dispositivi e offre un&#39;ampia gamma di tipi di test: prestazioni, qualità, funzionalità, certificazione, localizzazione, consumo di dati, ecc.

Per ulteriori informazioni, vedere [https://www.apptestnow.com](https://www.apptestnow.com/).

**HockeyApp**

* HockeyApp rientra nel test manuale in cui l&#39;app mobile viene spinta in un app store personale dove i tester possono scaricarla e provarla.

Per ulteriori informazioni, vedere [https://hockeyapp.net/features/](https://hockeyapp.net/features/).

**Jenkins**

* Sebbene non sia uno strumento di test, Jenkins è un framework di integrazione continua che fornisce la spina dorsale per i test automatizzati. Numerosi plug-in di terze parti sono disponibili per estendere le funzionalità. Ad esempio, il plug-in SeleniumGrid fornisce un&#39;interfaccia utente per gestire il nodo e i nodi Selenium.

Per ulteriori informazioni, vedere [https://jenkins-ci.org/](https://jenkins-ci.org/) e [https://wiki.jenkins-ci.org/display/JENKINS/Plugins](https://wiki.jenkins-ci.org/display/JENKINS/Plugins).
