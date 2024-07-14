---
title: Verifica delle app mobili
description: Scopri come automatizzare o testare manualmente le app mobili utilizzando vari strumenti.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing
content-type: reference
exl-id: e10e1904-7016-4eb0-9408-36297285f378
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '975'
ht-degree: 0%

---

# Verifica delle app mobili{#testing-mobile-apps}

>[!NOTE]
>
>L’Adobe consiglia di utilizzare l’Editor SPA per i progetti che richiedono il rendering lato client basato su framework di applicazione a pagina singola (ad esempio, React). [Ulteriori informazioni](/help/sites-developing/spa-overview.md).

Data l’ampia gamma di dispositivi sul mercato e di dispositivi in fase di rilascio, il test delle app è diventato imperativo. Si tratta di un’area in cui funzionalità e usabilità possono ottenere recensioni negative su un app store, ma un singolo difetto può causare la disinstallazione dell’app. Presta particolare attenzione ai piani di test e al controllo qualità. Il seguente collegamento tratta molti degli argomenti che devono essere trattati in generale, ad esempio l’identificazione dell’ambiente, la definizione dei casi di test, i tipi di test, i presupposti e il coinvolgimento dei clienti. Vengono inoltre descritti gli strumenti utili per l’attività di test. Gli strumenti interni, come [Hobbes](/help/sites-developing/hobbes.md), possono essere utili per i test dell&#39;interfaccia utente basati sul Web. [Giorno difficile](/help/sites-developing/tough-day.md) può stressare le tue istanze con un carico simulato. Se l’ambiente di test ha già esperienza con strumenti di terze parti, come Selenium, puoi utilizzare anche questi.

Quando si sviluppa un’app mobile, vi sono molti nuovi problemi specifici per i dispositivi che devono essere affrontati insieme a quelli dei test tradizionali.

* Funzionale: l’app soddisfa tutti i requisiti?
* Usabilità - L’app è facile da usare e da comprendere per il cliente?
* Prestazioni: cosa accade durante un picco nell’utilizzo? Gli elementi dell’app, come swipes e caroselli, sono rapidi e non distolgono l’esperienza?
* Errore o interruzioni: cosa succede quando si verifica una chiamata o una notifica in arrivo mentre l’app è in esecuzione? Cosa succede in caso di interruzione o spegnimento della rete?
* Installazione e aggiornamenti: qual è l’esperienza di installazione? Come vengono inviati gli aggiornamenti?
* Tecnico: l’app consuma troppo energia da un dispositivo?
* Localizzazione - Tutte le aree dell’app sono tradotte?
* Certificazione - L’app è stata certificata? I clienti possono credere che rispetti tutti i requisiti legali sulla privacy dei dati?

È necessario rispondere a queste domande durante il test automatico e manuale.

## Test automatizzati {#automated-testing}

È necessario eseguire un certo grado di test automatizzati per coprire la varietà di dimensioni dello schermo, vincoli di memoria, metodi di input e sistemi operativi. Non solo copre molti dei casi di prova, ma può accelerare il test di regressione quando vengono introdotte nuove funzioni o nuovi dispositivi. Idealmente, gli strumenti di automazione dovrebbero ridurre o limitare la duplicazione degli sforzi. Utilizza strumenti o framework per applicare il tuo impegno di test a tutte le piattaforme. Il grafico seguente mostra una struttura semplificata di un ambiente di test per i test dell’interfaccia utente basati su web e per i test delle app mobili. Il lato sinistro del grafico mostra una serie di nodi Selenium con browser. SeleniumGrid può eseguire il farm out dei test comuni dell’interfaccia utente basati sul web in uno qualsiasi di questi nodi. L’hub Selenium può anche connettersi ad Appium per il test di app multipiattaforma. Sono mostrati solo i simulatori, ma puoi incorporare le utility adb, per Android™ e Xcode per i dispositivi iOS. Più avanti in questo documento vengono forniti collegamenti che consentono di trovare dettagli specifici per gli strumenti menzionati.

![chlimage_1](assets/chlimage_1.jpeg)

## Test manuale {#manual-testing}

Oltre al test automatico, l’app deve essere sottoposta a un ciclo di test manuale. I clienti che eseguono l’app su un dispositivo reale non possono essere duplicati da uno script. Anche qui, hai molte opzioni. Puoi utilizzare una piattaforma, come HockeyApp, per definire chi ha accesso e raccogliere feedback. In alternativa, è possibile affidare l&#39;intero processo a un servizio come UTest, ElusiveStars o Testin. Se disponi di un gruppo di tester interni, ma non di dispositivi diversi, puoi eseguire test manuali sui loro pool di dispositivi tramite i servizi cloud. Un servizio di questo tipo è SauceLabs. Puoi anche creare app da remoto per PhoneGap Enterprise e installarle su dispositivi locali come livello di test di accettazione o dimostrazione. Per informazioni sulle funzioni e la documentazione più recenti, visitare il sito Web PhoneGap (`https://phonegap.com/`). Indipendentemente dall’approccio adottato, il test manuale deve effettuare le seguenti operazioni:

* ha raggiunto un vasto target di tester,
* effettuare prove su un ampio pool di dispositivi (idealmente dispositivi reali, ma simulatori/emulatori se non sono disponibili dispositivi reali),
* fornire feedback informativo:

   * rapporti sugli arresti anomali,
   * analisi/tracciamento,
   * usabilità,
   * aree di attenzione,
   * prestazioni,
   * dati/consumo energetico e così via.

## Strumenti {#tools}

È disponibile un’ampia gamma di strumenti per testare le app mobili. La scelta di quelli da utilizzare deve essere basata sulla tua situazione specifica: caratteristiche, prezzo, supporto, copertura e così via. Di seguito è riportata solo una breve descrizione di alcuni degli strumenti e dei servizi disponibili.

**Selenio**

* Framework che include un&#39;API per gli script di test per alimentare WebDriver e controllare vari browser.
* Puoi utilizzarlo con Appium per il test su dispositivi reali.
* SeleniumGrid indirizza i test tra nodi per i test paralleli.
* L&#39;IDE di selenio aiuta a ridurre la scrittura di test case.

Per ulteriori informazioni, vedere [https://www.selenium.dev/](https://www.selenium.dev/).

**Testdroid**

* Servizio di test basato su cloud con hook di integrazione continua e test sul dispositivo reale.
* Incluso è un App Crawler che controlla la compatibilità del dispositivo, analizza i registri, analizza le viste, acquisisce le schermate e monitora le prestazioni.

Per ulteriori informazioni, vedere [https://testdroid.com/](https://testdroid.com/).

**Appia**

* Appium è un framework multipiattaforma popolare per l’automazione dei test mobili.
* Inoltre, è incluso un ispettore con capacità di record per aiutare a codificare i casi di test.

Per ulteriori informazioni, vedere [https://appium.io/](https://appium.io/).

**Laboratori di salsa**

* SauceLabs fornisce test basati su cloud e si integra con l’integrazione continua.
* I test vengono eseguiti automaticamente nel relativo ambiente cloud oppure è possibile avviare un dispositivo o una piattaforma particolare ed eseguire test manuali per facilitare il debug dei problemi.

Per ulteriori informazioni, vedere [https://saucelabs.com/](https://saucelabs.com/).

<!-- **AppTestNow**

* An outsourcing service that tests your mobile apps.
* Included is a large pool of devices and offers a wide range of types of testing: performance, quality, functional, certification, localization, data consumption, and so on.

For more information, see [https://apptestnow.com/](https://apptestnow.com/). -->

**HockeyApp**

* HockeyApp rientra nel test manuale in cui l&#39;app mobile viene inviata a un app store personale dove i tester possono scaricarla e provarla.

Per ulteriori informazioni, vedere [https://hockeyapp.net/features/](https://hockeyapp.net/features/).

**Jenkins**

* Anche se non è uno strumento di test, Jenkins è un framework di integrazione continua che fornisce la spina dorsale per i test automatizzati. Sono disponibili numerosi plug-in di terze parti per estendere la funzionalità. Ad esempio, il plugin SeleniumGrid fornisce un’interfaccia utente per aiutare a gestire l’hub e i nodi Selenium.

Per ulteriori informazioni, vedere [https://www.jenkins.io/](https://www.jenkins.io/) e [https://plugins.jenkins.io/](https://plugins.jenkins.io/).
