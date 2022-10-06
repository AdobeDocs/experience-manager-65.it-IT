---
title: Verifica delle app mobili
seo-title: Testing Mobile Apps
description: Verifica delle app mobili
seo-description: null
uuid: 3b402d34-5cab-4280-b8b9-88ad9f8fc5e4
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing
content-type: reference
discoiquuid: 5a98e1bd-f5c1-4f2f-ac02-dbd005dc1de7
exl-id: e10e1904-7016-4eb0-9408-36297285f378
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1025'
ht-degree: 0%

---

# Verifica delle app mobili{#testing-mobile-apps}

>[!NOTE]
>
>Adobe consiglia di utilizzare l’editor di SPA per i progetti che richiedono il rendering lato client basato sul framework di un’applicazione a pagina singola (ad esempio, React). [Per saperne di più](/help/sites-developing/spa-overview.md).

Data l&#39;ampia gamma di dispositivi sul mercato e i dispositivi in fase di rilascio, testare le tue app è diventato estremamente importante. Si tratta di un&#39;area in cui funzionalità e usabilità possono ottenere recensioni basse su un app store, ma un singolo difetto può causare la disinstallazione dell&#39;app. Occorre prestare attenzione ai piani di test e alla garanzia della qualità. Il collegamento seguente tratta molti degli argomenti che devono essere affrontati in generale, ad esempio, identificare l’ambiente, definire casi di test, tipi di test, presupposti, coinvolgimento del cliente, ecc. Sono inoltre trattati gli strumenti per contribuire al lavoro di test. Strumenti interni, come [Hobbes](/help/sites-developing/hobbes.md)può essere utile con i test dell’interfaccia utente basati sul Web. [Giorno difficile](/help/sites-developing/tough-day.md) può sollecitare le istanze con un carico simulato. Se l’ambiente di test dispone già di esperienza con strumenti di terze parti, come Selenium, anche questi possono essere utilizzati.

Quando si sviluppa un’app mobile, sono presenti molti nuovi problemi specifici per i dispositivi che devono essere affrontati insieme a quelli dei test tradizionali.

* Funzionalità : tutti i requisiti sono soddisfatti dall’app?
* Usabilità: l’app è facile da usare e comprendere per il cliente?
* Prestazioni: cosa succede durante un picco di utilizzo? Gli elementi dell’app, come i tasti di scorrimento e i caroselli, sono rapidi e non distogliono l’esperienza?
* Errori o arresti anomali: cosa succede quando si verifica una chiamata o una notifica in entrata mentre l&#39;app è in esecuzione? Cosa succede in caso di interruzione o spegnimento della rete?
* Installazione e aggiornamenti: com&#39;è l&#39;esperienza di installazione? Come vengono inviati gli aggiornamenti?
* Tecnico: la tua app sta consumando troppa energia da un dispositivo?
* Localizzazione : tutte le aree dell’app sono tradotte?
* Certificazione: la tua app è stata certificata? I clienti possono essere certi che soddisfi tutti i requisiti legali sulla privacy dei dati?

Queste domande devono essere risolte durante il test automatico e manuale.

## Test automatizzato {#automated-testing}

È necessario eseguire un certo grado di test automatizzati per coprire la varietà di dimensioni dello schermo, vincoli di memoria, metodi di input e sistemi operativi. Non solo copre gran parte dei casi di test, ma può accelerare il test di regressione quando vengono introdotte nuove funzioni o dispositivi. Idealmente, gli strumenti di automazione dovrebbero ridurre o limitare la duplicazione degli sforzi. Utilizza strumenti o framework in modo che il tuo sforzo di test sia applicabile a tutte le piattaforme. Il grafico seguente mostra una struttura semplificata di un ambiente di test sia per i test dell’interfaccia utente basati su web che per i test delle app mobili. Il lato sinistro del grafico mostra una serie di nodi Selenium con browser. SeleniumGrid può sottoporre a farm test comuni dell’interfaccia utente basati sul web a uno qualsiasi di questi nodi. L&#39;hub Selenium può anche connettersi ad Appium per il test di app multipiattaforma. Vengono visualizzati solo i simulatori, ma è possibile incorporare adb, per Android e le utility Xcode per i dispositivi iOS. I collegamenti sono forniti più avanti in questo documento dove è possibile trovare dettagli specifici per gli strumenti menzionati.

![chlimage_1](assets/chlimage_1.jpeg)

## Test manuale {#manual-testing}

Oltre ai test automatizzati, l&#39;app deve seguire un ciclo di test manuali. I clienti che eseguono l&#39;app su un dispositivo reale non possono essere duplicati da uno script. Anche qui, hai molte opzioni. Puoi utilizzare una piattaforma, ad esempio HockeyApp, per definire chi ha accesso e raccogliere feedback. Oppure, puoi affidare l&#39;intero processo a un servizio come UTest, ElusiveStars o Testin. Se disponi di un gruppo di tester interni, ma non sono presenti differenze tra i dispositivi, sono disponibili servizi cloud in cui è possibile eseguire test manuali sul pool di dispositivi. Uno di questi servizi che fornisce questo è SauceLabs. Puoi anche creare app in remoto su PhoneGap Enterprise e installarle su dispositivi locali come livello di test di accettazione o demo. Consulta la sezione [PhoneGap](https://phonegap.com/) sito web per le funzioni e la documentazione più recenti. Qualunque sia l&#39;approccio, le prove manuali devono essere effettuate;

* colpire un grande bersaglio di tester,
* test su un ampio pool di dispositivi (dispositivi idealmente reali, ma simulatori/emulatori se non sono disponibili dispositivi reali),
* fornire feedback informativi:

   * segnalazioni di arresti anomali,
   * analisi/tracciamento,
   * usabilità,
   * settori di attenzione,
   * prestazioni,
   * consumo di dati/energia, ecc.

## Strumenti {#tools}

È disponibile un&#39;ampia gamma di strumenti per testare le app mobili. La scelta di quelli da utilizzare sarà basata sulla tua situazione specifica: caratteristiche, prezzo, supporto, copertura, ecc. Ecco una breve descrizione di alcuni degli strumenti e dei servizi disponibili.

**Selenio**

* Framework che include un&#39;API per gli script di test per alimentare WebDriver e controllare vari browser.
* Puoi utilizzarlo insieme ad Appium per eseguire test su dispositivi reali.
* SeleniumGrid indirizza i test tra nodi per il test parallelo.
* L&#39;IDE al selenio aiuta a ridurre la scrittura di case di prova.

Per ulteriori informazioni consulta [https://www.seleniumhq.org/](https://www.seleniumhq.org/).

**Testdroid**

* Un servizio di test basato su cloud con hook di integrazione continui e test di dispositivi reali.
* Include un crawler per app che controlla la compatibilità del dispositivo, analizza i registri, analizza le visualizzazioni, effettua le schermate e monitora le prestazioni.

Per ulteriori informazioni consulta [https://testdroid.com/](https://testdroid.com/).

**Appio**

* Appium è un framework popolare tra piattaforme per automatizzare i test mobili.
* Inoltre, un ispettore è incluso con capacità di record per aiutare i casi di test del codice.

Per ulteriori informazioni consulta [https://appium.io/](https://appium.io/).

**SauceLabs**

* SauceLabs fornisce test basati su cloud e si integra con un&#39;integrazione continua.
* I test vengono eseguiti automaticamente nel loro ambiente cloud oppure è possibile avviare un dispositivo o una piattaforma particolare ed eseguire test manuali per facilitare il debug dei problemi.

Per ulteriori informazioni consulta [https://saucelabs.com/](https://saucelabs.com/).

**AppTestNow**

* Un servizio di outsourcing che testerà le tue app mobili.
* Include un ampio pool di dispositivi e offre una vasta gamma di tipi di test: prestazioni, qualità, funzionalità, certificazione, localizzazione, consumo di dati, ecc.

Per ulteriori informazioni consulta [https://www.apptestnow.com](https://www.apptestnow.com/).

**HockeyApp**

* HockeyApp rientra nel test manuale dove l&#39;app mobile viene spinta in un app store personale dove i tester possono scaricare e provare.

Per ulteriori informazioni consulta [https://hockeyapp.net/features/](https://hockeyapp.net/features/).

**Jenkins**

* Sebbene non sia uno strumento di test, Jenkins è un framework di integrazione continua che fornisce la spina dorsale per i test automatizzati. Sono disponibili numerosi plug-in di terze parti per estendere le funzionalità. Ad esempio, il plugin SeleniumGrid fornisce un&#39;interfaccia utente per aiutare a gestire l&#39;hub e i nodi Selenium.

Per ulteriori informazioni consulta [https://jenkins-ci.org/](https://jenkins-ci.org/) e [https://wiki.jenkins-ci.org/display/JENKINS/Plugins](https://wiki.jenkins-ci.org/display/JENKINS/Plugins).
