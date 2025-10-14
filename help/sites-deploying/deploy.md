---
title: Distribuzione e manutenzione
description: Scopri come iniziare a installare AEM.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
docset: aem65
exl-id: 3df0662a-0768-4b56-8b94-c517657b4bd9
solution: Experience Manager, Experience Manager Sites
feature: Deploying
role: Admin
source-git-commit: f96b178ae84b4b930b59e36d4994970682c53dbd
workflow-type: tm+mt
source-wordcount: '1779'
ht-degree: 3%

---

# Distribuzione e manutenzione{#deploying-and-maintaining}

In questa pagina trovi:

* [Concetti di base](#basic-concepts)

   * [Cos’è AEM?](#what-is-aem)
   * [Distribuzioni tipiche](#typical-deployment-scenarios)

      * [On-premise](#on-premise)
      * [Managed Services con Cloud Manager](#managed-services-using-cloud-manager)

* [Guida introduttiva](#getting-started)

   * [Prerequisiti](#prerequisites)
   * [Recupero del software](#getting-the-software)
   * [Installazione locale predefinita](#default-local-install)
   * [Installazioni di authoring e pubblicazione](#author-and-publish-installs)
   * [Directory di installazione decompressa](#unpacked-install-directory)
   * [Avvio e arresto](#starting-and-stopping)

Dopo aver acquisito familiarità con queste nozioni di base, puoi trovare informazioni più avanzate e dettagliate nelle seguenti sottopagine:

* [Requisiti tecnici](/help/sites-deploying/technical-requirements.md)
* [Distribuzioni consigliate](/help/sites-deploying/recommended-deploys.md)
* [Installazione autonoma personalizzata](/help/sites-deploying/custom-standalone-install.md)
* [Installazione server applicazioni](/help/sites-deploying/application-server-install.md)
* [Risoluzione dei problemi](/help/sites-deploying/troubleshooting.md)
* [Avvio e arresto riga di comando](/help/sites-deploying/command-line-start-and-stop.md)
* [Configurazione](/help/sites-deploying/configuring.md)
* [Aggiornamento ad AEM 6.5](/help/sites-deploying/upgrade.md)
* [eCommerce](/help/commerce/cif-classic/deploying/ecommerce.md)
* [Articoli pratici sulla configurazione](/help/sites-deploying/ht-deploy.md)
* [Console Web](/help/sites-deploying/web-console.md)
* [Risoluzione dei problemi di replica](/help/sites-deploying/troubleshoot-rep.md)
* [Best practice](/help/sites-deploying/best-practices.md)
* [Distribuzione delle community](/help/communities/deploy-communities.md)
* [Introduzione alla piattaforma AEM](/help/sites-deploying/platform.md)
* [Linee guida sulle prestazioni](/help/sites-deploying/performance-guidelines.md)
* [Guida introduttiva ad AEM Mobile](/help/mobile/getting-started-aem-mobile.md)
* [Cos&#39;è AEM Screens?](https://experienceleague.adobe.com/docs/experience-manager-screens/user-guide/aem-screens-introduction.html?lang=it)

## Concetti di base {#basic-concepts}

### Cos’è AEM? {#what-is-aem}

Adobe Experience Manager è un sistema client-server basato su Web per la creazione, la gestione e la distribuzione di siti Web commerciali e servizi correlati. Combina diverse funzioni a livello di infrastruttura e di applicazione in un unico pacchetto integrato.

A livello di infrastruttura, AEM fornisce quanto segue:

* **Server applicazioni Web**: AEM può essere distribuito in modalità standalone (include un server Web Jetty integrato) o come applicazione Web in un server applicazioni di terze parti.
* **Web Application Framework**: AEM incorpora Sling Web Application Framework che semplifica la scrittura di applicazioni Web RESTful orientate ai contenuti.
* **Archivio dei contenuti**: AEM include un Java™ Content Repository (JCR), un tipo di database gerarchico progettato appositamente per i dati non strutturati e semistrutturati. L’archivio memorizza non solo il contenuto rivolto all’utente, ma anche tutto il codice, i modelli e i dati interni utilizzati dall’applicazione.

Su questa base, AEM offre anche diverse funzioni a livello di applicazione per la gestione di:

* **Siti Web**
* **Applicazioni mobili**
* **Pubblicazioni digitali**
* **Forms e documenti**
* **Assets digitale**
* **Community**
* **Commerce in linea**

Infine, i clienti possono utilizzare questi elementi di base a livello di infrastruttura e applicazione per creare soluzioni personalizzate creando applicazioni proprie.

Il server AEM è **basato su Java** ed è in esecuzione sulla maggior parte dei sistemi operativi che supportano tale piattaforma. Tutte le interazioni client con AEM vengono eseguite tramite un **browser Web**.

>[!NOTE]
>
>La funzione Adaptive Forms, disponibile in AEM 6.5 QuickStart, è progettata esclusivamente a scopo di esplorazione e valutazione. Per l’utilizzo in produzione, è essenziale ottenere una licenza valida per AEM Forms, in quanto la funzionalità Adaptive Forms richiede una licenza appropriata.

### Scenari di implementazione tipici {#typical-deployment-scenarios}

Nella terminologia di AEM, per &quot;istanza&quot; si intende una copia di AEM in esecuzione su un server. Le installazioni di AEM in genere richiedono almeno due istanze, in genere eseguite in computer separati:

* **Autore**: istanza di AEM utilizzata per creare, caricare e modificare contenuti e amministrare il sito Web. Quando il contenuto è pronto per essere pubblicato, viene replicato nell’istanza di pubblicazione.
* **Pubblicazione**: istanza di AEM che fornisce al pubblico il contenuto pubblicato.

Queste istanze sono identiche in termini di software installato. Si differenziano solo per configurazione. Inoltre, la maggior parte delle installazioni utilizza un Dispatcher:

* **Dispatcher**: un server web statico (Apache httpd, Microsoft® IIS e così via) è stato potenziato con il modulo Dispatcher di AEM. Memorizza nella cache le pagine web prodotte dall’istanza di pubblicazione per migliorare le prestazioni.

Esistono molte opzioni ed elaborazioni avanzate per questa configurazione, ma il modello di base di authoring, pubblicazione e Dispatcher è al centro della maggior parte delle implementazioni. Iniziamo concentrandoci su una configurazione semplice. Di seguito vengono illustrate le opzioni di distribuzione avanzate.

Le sezioni seguenti descrivono entrambi gli scenari:

* **On-Premise**: AEM implementato e gestito nell&#39;ambiente aziendale.

* **Managed Services - Cloud Manager per Adobe Experience Manager**: AEM distribuito e gestito da Adobe Managed Services.

### On-premise {#on-premise}

Puoi installare AEM sui server dell’ambiente aziendale. Le istanze di installazione tipiche includono: ambienti di sviluppo, test e pubblicazione. Consulta [Guida introduttiva](/help/sites-deploying/deploy.md#getting%20started) per informazioni di base su come ottenere il software AEM per installarlo localmente.

Per ulteriori informazioni sulle tipiche distribuzioni locali, vedere [Distribuzioni consigliate](/help/sites-deploying/recommended-deploys.md).

### Managed Services con Cloud Manager {#managed-services-using-cloud-manager}

AEM Managed Services è una soluzione completa per la gestione delle esperienze digitali. Offre i vantaggi della soluzione di distribuzione delle esperienze nel cloud, pur mantenendo tutti i vantaggi di controllo, sicurezza e personalizzazione di un’implementazione on-premise. AEM Managed Services consente ai clienti di avviarsi più rapidamente tramite l’implementazione sul cloud e l’utilizzo delle best practice e del supporto di Adobe. Le organizzazioni e gli utenti aziendali possono coinvolgere i clienti in tempi minimi, aumentare la quota di mercato e concentrarsi sulla creazione di campagne di marketing innovative riducendo al contempo il carico sull&#39;IT.

Con AEM Managed Services i clienti possono trarre i seguenti vantaggi:

**Time to Market più veloce:** Grazie all&#39;infrastruttura cloud flessibile di Adobe Managed Services, le organizzazioni possono pianificare, avviare e ottimizzare rapidamente le esperienze digitali di successo. Adobe gestisce l’architettura cloud senza richiedere capitale aggiuntivo, hardware o software; i Customer Solutions Engineer di Adobe si occupano dell’architettura, del provisioning e della personalizzazione di AEM per la connessione alle app back-end e delle best practice per la pubblicazione.

**Prestazioni più elevate:** fornisce esperienze digitali affidabili per la tua azienda con quattro opzioni di disponibilità dei servizi: 99,5%, 99,9%, 99,95% e 99,99%. Inoltre, consente il backup automatico e modelli di disaster recovery multimodali per garantire affidabilità e gestione di emergenza.

**Costi IT ottimizzati:** le organizzazioni che forniscono assistenza proattiva e supporto tecnico possono utilizzare sempre l&#39;ultima versione di AEM. La manutenzione e il supporto Platinum di Adobe vengono inclusi automaticamente nelle nuove implementazioni di AMS Enterprise/Basic, offrendo competenze tecniche ed esperienza operativa per aiutare le organizzazioni a mantenere le proprie applicazioni mission-critical. Le funzionalità di base gratuite di Analytics o Target offrono ulteriore valore, soprattutto per le organizzazioni di fascia media con esigenze limitate di analisi e personalizzazione.

**Massima sicurezza:** garantisce la sicurezza fisica, di rete e dei dati di livello enterprise ospitando le applicazioni dei clienti in una struttura ad accesso limitato, dietro i sistemi firewall o all&#39;interno di un cloud privato virtuale. Include macchine virtuali a tenant singolo con crittografia di storage dei dati affidabile, antivirali e isolamento dei dati.

**Cloud Manager**: Cloud Manager, parte dell&#39;offerta Adobe Experience Manager Managed Services, è un portale self-service che consente alle organizzazioni di gestire autonomamente Adobe Experience Manager nel cloud. Include una pipeline CI/CD (Continuous Integration and Continuous Delivery) all’avanguardia che consente ai team IT e ai partner di implementazione di velocizzare la distribuzione di personalizzazioni o aggiornamenti senza compromettere le prestazioni o la sicurezza. Cloud Manager è disponibile solo per i clienti di Adobe Managed Service.

Per ulteriori informazioni su Cloud Manager e sulle relative risorse, consulta la [**Guida utente di Cloud Manager**](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/introduction.html?lang=it).

## Guida introduttiva {#getting-started}

### Prerequisiti {#prerequisites}

Mentre le istanze di produzione vengono eseguite su computer dedicati che eseguono un sistema operativo ufficialmente supportato (vedi [Requisiti tecnici](/help/sites-deploying/technical-requirements.md)), il server Experience Manager verrà eseguito su qualsiasi sistema che supporta [**Java™ Standard Edition 8**](https://www.oracle.com/java/technologies/downloads/#java8).

A scopo di familiarizzazione e per lo sviluppo su AEM, è comune utilizzare un’istanza installata sul computer locale con Apple OS X o versioni desktop di Microsoft® Windows o Linux®.

Sul lato client, AEM funziona con tutti i browser moderni (**Microsoft® Edge**, **Internet Explorer** 11, **Chrome &#x200B;** 51+**&#x200B; &#x200B;**, **Firefox &#x200B;** 47+, **Safari** 8+) sia sui sistemi operativi desktop che su quelli tablet. Per informazioni dettagliate, consulta [Piattaforme client supportate](/help/sites-deploying/technical-requirements.md#supported-client-platforms).

### Recupero del software {#getting-the-software}

I clienti con un contratto di manutenzione e supporto valido devono aver ricevuto una notifica tramite posta elettronica con un codice e poter scaricare AEM dal [**sito Web Adobe Licensing**](https://licensing.adobe.com/). I partner commerciali possono richiedere l&#39;accesso al download da [**spphelp@adobe.com**](mailto:spphelp@adobe.com).

Il pacchetto software AEM è disponibile in due forme:

* **cq-quickstart-6.5.0.jar:** File eseguibile autonomo *jar* che include tutto ciò che è necessario eseguire.

* **cq-quickstart-6.5.0.war:** Un file *war* per la distribuzione in un server applicazioni di terze parti.

Nella sezione seguente viene descritta l&#39;**installazione autonoma**. Per informazioni dettagliate sull&#39;installazione di AEM in un server applicazioni, vedere [Installazione server applicazioni](/help/sites-deploying/application-server-install.md).

### Installazione locale predefinita {#default-local-install}

1. Creare una directory di installazione nel computer locale. Ad esempio:

   Percorso di installazione UNIX®: **/opt/aem**

   Percorso di installazione di Windows: **`C:\Program Files\aem`**

   Allo stesso modo, è comune installare istanze di esempio in una cartella direttamente sul desktop. In ogni caso, Adobe si riferisce genericamente a questa posizione come:

   `<aem-install>`

   *Il percorso della directory dei file deve essere costituito solo da caratteri ASCII USA.*

1. Posiziona i file **jar** e **license** in questa directory:

   ```shell
   <aem-install>/
       cq-quickstart-6.5.0.jar
       license.properties
   ```

   Se non si fornisce un file `license.properties`, AEM reindirizzerà il browser a una schermata di **Benvenuto** all&#39;avvio, in cui è possibile immettere una chiave di licenza. Se non disponi ancora di un codice di licenza valido, devi richiederlo ad Adobe.

1. Per avviare l&#39;istanza in un ambiente GUI, fare doppio clic sul file **`cq-quickstart-6.5.0.jar`**.

   In alternativa, puoi avviare AEM dalla riga di comando:

   ```shell
       java -Xmx1024M -jar cq-quickstart-6.5.0.jar
   ```

AEM impiega qualche minuto per decomprimere il file jar, installarsi e avviare. La procedura sopra descritta comporta:

* un&#39;istanza di **AEM author**
* in esecuzione su **localhost**
* sulla porta **4502**

Per accedere all’istanza, seleziona:

**`https://localhost:4502`**

Il risultato nell&#39;istanza di authoring verrà configurato automaticamente per la connessione a un&#39;istanza di pubblicazione **&#x200B;**&#x200B;in **`localhost:4503`**.

### Installazioni di authoring e pubblicazione {#author-and-publish-installs}

L&#39;installazione predefinita (un&#39;istanza **author** su **`localhost:4502`**) può essere modificata semplicemente rinominando il file `jar` prima di avviarlo per la prima volta. Il pattern di denominazione è:

**`cq-<instance-type>-p<port-number>.jar`**

Ad esempio, rinominando il file in

**`cq-author-p4502.jar`**

E il suo avvio comporta l&#39;esecuzione di un&#39;istanza di authoring su **`localhost:4502`**.

Analogamente, rinominare e avviare il file

**`cq-publish-p4503.jar`**

Determina un&#39;istanza di pubblicazione in esecuzione su **`localhost:4503`**.

Ad esempio, installa queste due istanze in

`<aem-install>/author` e

**`<aem-install>/publish`**

Per ulteriori informazioni sulla personalizzazione dell&#39;installazione, vedere:

* [Installazione autonoma personalizzata](/help/sites-deploying/custom-standalone-install.md)
* [Modalità di esecuzione](/help/sites-deploying/configure-runmodes.md)

### Directory di installazione decompressa {#unpacked-install-directory}

Quando il file jar quickstart viene avviato per la prima volta, si disinserisce nella stessa directory in una nuova sottodirectory denominata `crx-quickstart`. Dovresti avere quanto segue:

```xml
<aem-install>/
    license.properties
    cq-quickstart-6.5.0.jar
    crx-quickstart/
        app/
        bin/
        conf/
        launchpad/
        logs/
        metrics/
        monitoring/
        opt/
        repository/
        threaddumps/
        eula-de_DE.html
        eula-en_US.html
        eula-fr_FR.html
        eula-ja_JP.html
        readme.txt
```

Se l’istanza è stata installata dall’interfaccia utente, si apre automaticamente una finestra del browser e si apre anche una finestra dell’applicazione desktop che mostra l’host e la porta dell’istanza e un interruttore di accensione/spegnimento:

![schermata di avvio](assets/screen_shot_.png)

### Avvio e arresto {#starting-and-stopping}

Una volta che AEM si è disinstallato e si è avviato per la prima volta, facendo doppio clic sul file jar nella directory di installazione, l’istanza viene avviata senza essere reinstallata.

Per arrestare l&#39;istanza dall&#39;interfaccia utente grafica, fare clic sull&#39;opzione **on/off** nella finestra dell&#39;applicazione desktop.

Puoi anche arrestare e avviare AEM dalla riga di comando. Se l&#39;istanza è già stata installata per la prima volta, gli **script della riga di comando** sono disponibili qui:

**`<aem-install>/crx-quickstart/bin/`**

Questa cartella contiene i seguenti script di shell UNIX® bash:

* **`start`**: avvia l&#39;istanza
* `stop`: arresta l&#39;istanza
* **`status`**: segnala lo stato dell&#39;istanza
* **`quickstart`**: utilizzato per configurare le informazioni di avvio, se necessario.

Esistono anche **`bat`** file equivalenti per Windows. Per informazioni più dettagliate, consulta:

* [Avvio e arresto riga di comando](/help/sites-deploying/command-line-start-and-stop.md)

AEM avvia e reindirizza automaticamente il browser web alla pagina appropriata, in genere la pagina di accesso; ad esempio:

`https://localhost:4502/`

![schermata di accesso](assets/screen_shot_2019-04-08at83533am.png)

Dopo aver effettuato l’accesso, puoi accedere ad AEM. Per ulteriori informazioni, a seconda del ruolo, consulta:

* [Authoring](/help/sites-authoring/first-steps.md)
* [Amministrazione](/help/sites-administering/home.md)
* [Sviluppo](/help/sites-developing/getting-started.md)
* [Gestione](/help/managing/best-practices.md)

## Implementazione avanzata {#advanced-deployment}

La sezione precedente consente di comprendere le nozioni di base sull’installazione di AEM. Tuttavia, l’installazione di un sistema di produzione completo di AEM può comportare una complessità notevolmente maggiore. Per una copertura completa dell’installazione avanzata, consulta le seguenti pagine secondarie:

* [Requisiti tecnici](/help/sites-deploying/technical-requirements.md)
* [Distribuzioni consigliate](/help/sites-deploying/recommended-deploys.md)
* [Installazione autonoma personalizzata](/help/sites-deploying/custom-standalone-install.md)
* [Installazione server applicazioni](/help/sites-deploying/application-server-install.md)
* [Risoluzione dei problemi](/help/sites-deploying/troubleshooting.md)
* [Avvio e arresto riga di comando](/help/sites-deploying/command-line-start-and-stop.md)
* [Configurazione](/help/sites-deploying/configuring.md)
* [Aggiornamento ad AEM 6.5](/help/sites-deploying/upgrade.md)
* [eCommerce](/help/commerce/cif-classic/deploying/ecommerce.md)
* [Articoli pratici sulla configurazione](/help/sites-deploying/ht-deploy.md)
* [Console Web](/help/sites-deploying/web-console.md)
* [Risoluzione dei problemi di replica](/help/sites-deploying/troubleshoot-rep.md)
* [Best practice](/help/sites-deploying/best-practices.md)
* [Distribuzione delle community](/help/communities/deploy-communities.md)
* [Introduzione alla piattaforma AEM](/help/sites-deploying/platform.md)
* [Linee guida sulle prestazioni](/help/sites-deploying/performance-guidelines.md)
* [Guida introduttiva ad AEM Mobile](/help/mobile/getting-started-aem-mobile.md)
* [Cos&#39;è AEM Screens?](https://experienceleague.adobe.com/docs/experience-manager-screens/user-guide/aem-screens-introduction.html?lang=it)
