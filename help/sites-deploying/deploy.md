---
title: Implementazione e manutenzione
seo-title: Deploying and Maintaining
description: Scopri come iniziare a installare l’AEM.
seo-description: Learn how to get started with the AEM installation.
uuid: 4429ac4d-abd7-47d8-b19d-773accb7cc7a
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: e48cc0ed-688c-44c8-b6d6-5f3c8593a295
docset: aem65
exl-id: 3df0662a-0768-4b56-8b94-c517657b4bd9
source-git-commit: 9052ed3e89fdc67d94fc60bbff64d42255565767
workflow-type: tm+mt
source-wordcount: '1802'
ht-degree: 8%

---

# Implementazione e manutenzione{#deploying-and-maintaining}

In questa pagina trovi:

* [Concetti di base](#basic-concepts)

   * [Che cos’è AEM?](#what-is-aem)
   * [Implementazioni tipiche](#typical-deployment-scenarios)

      * [On-premise](#on-premise)
      * [Managed Services con Cloud Manager](#managed-services-using-cloud-manager)

* [Guida introduttiva](#getting-started)

   * [Prerequisiti](#prerequisites)
   * [Recupero del software](#getting-the-software)
   * [Installazione locale predefinita](#default-local-install)
   * [Installazioni di authoring e pubblicazione](#author-and-publish-installs)
   * [Directory di installazione decompressa](#unpacked-install-directory)
   * [Avvio e arresto](#starting-and-stopping)

Una volta acquisite familiarità con queste nozioni di base, le informazioni più avanzate e dettagliate sono disponibili nelle seguenti sottopagine:

* [Requisiti tecnici](/help/sites-deploying/technical-requirements.md)
* [Distribuzioni consigliate](/help/sites-deploying/recommended-deploys.md)
* [Installazione personalizzata indipendente](/help/sites-deploying/custom-standalone-install.md)
* [Installazione dell’applicazione da server](/help/sites-deploying/application-server-install.md)
* [Risoluzione dei problemi](/help/sites-deploying/troubleshooting.md)
* [Avvio e interruzione da riga di comando](/help/sites-deploying/command-line-start-and-stop.md)
* [Configurazione](/help/sites-deploying/configuring.md)
* [Aggiornamento a AEM 6.5](/help/sites-deploying/upgrade.md)
* [eCommerce](/help/commerce/cif-classic/deploying/ecommerce.md)
* [Articoli pratici sulla configurazione](/help/sites-deploying/ht-deploy.md)
* [Console Web](/help/sites-deploying/web-console.md)
* [Risoluzione dei problemi di replica](/help/sites-deploying/troubleshoot-rep.md)
* [Best practice  ](/help/sites-deploying/best-practices.md)
* [Distribuzione delle community](/help/communities/deploy-communities.md)
* [Introduzione alla piattaforma AEM](/help/sites-deploying/platform.md)
* [Linee guida sulle prestazioni](/help/sites-deploying/performance-guidelines.md)
* [Guida introduttiva di AEM Mobile](/help/mobile/getting-started-aem-mobile.md)
* [Cos’è AEM Screens?](https://experienceleague.adobe.com/docs/experience-manager-screens/user-guide/aem-screens-introduction.html?lang=it)

## Concetti di base {#basic-concepts}

### Che cos’è AEM? {#what-is-aem}

Adobe Experience Manager è un sistema client-server basato sul Web per la creazione, gestione e distribuzione di siti Web commerciali e di servizi correlati, che combina varie funzioni a livello di infrastruttura e di applicazione in un unico pacchetto integrato.

A livello di infrastruttura, l’AEM fornisce quanto segue:

* **Server applicazioni Web**: AEM può essere distribuito in modalità indipendente (include un server web Jetty integrato) o come applicazione web all’interno di un server applicazioni di terze parti.
* **Framework applicazione Web**: AEM incorpora Sling Web Application Framework che semplifica la scrittura di applicazioni web RESTful orientate ai contenuti.
* **Archivio dei contenuti**: AEM include Java Content Repository (JCR), un tipo di database gerarchico progettato specificamente per i dati non strutturati e semistrutturati. L’archivio memorizza non solo il contenuto rivolto all’utente, ma anche tutto il codice, i modelli e i dati interni utilizzati dall’applicazione.

Su questa base, l&#39;AEM offre anche una serie di funzionalità a livello di applicazione per la gestione di:

* **Siti Web**
* **Applicazioni mobili**
* **Pubblicazioni digitali**
* **Forms**
* **Risorse digitali**
* **Communities**
* **Commercio online**

Infine, i clienti possono utilizzare questi elementi di base a livello di infrastruttura e applicazione per creare soluzioni personalizzate creando applicazioni proprie.

Il server AEM è **Basato su Java** e viene eseguito sulla maggior parte dei sistemi operativi che supportano tale piattaforma. Tutte le interazioni dei clienti con l’AEM avvengono attraverso **browser web**.

### Scenari di implementazione tipici {#typical-deployment-scenarios}

Nella terminologia AEM, per &quot;istanza&quot; si intende una copia dell’AEM in esecuzione su un server. Le installazioni dell’AEM in genere coinvolgono almeno due istanze, in genere eseguite su macchine separate:

* **Autore**: istanza AEM utilizzata per creare, caricare e modificare i contenuti e amministrare il sito web. Quando il contenuto è pronto per essere pubblicato, viene replicato nell’istanza di pubblicazione.
* **Pubblica**: istanza dell’AEM che rende pubblici i contenuti pubblicati.

Queste istanze sono identiche in termini di software installato. Si differenziano solo per configurazione. Inoltre, la maggior parte delle installazioni utilizza un dispatcher:

* **Dispatcher**: server web statico (Apache httpd, Microsoft IIS, ecc.) potenziato con il modulo dispatcher per AEM. Memorizza nella cache le pagine web prodotte dall’istanza Publish per migliorarne le prestazioni.

Sono disponibili molte opzioni ed elaborazioni avanzate per questa configurazione, ma il pattern di base di authoring, pubblicazione e dispatcher è al centro della maggior parte delle distribuzioni. Inizieremo concentrandoci su una configurazione relativamente semplice. Seguirà la discussione sulle opzioni di distribuzione avanzate.

Le sezioni seguenti descrivono entrambi gli scenari:

* **On-premise**: AEM implementato e gestito nell’ambiente aziendale.

* **Managed Services - Cloud Manager per Adobe Experience Manager**: AEM implementato e gestito da Adobe Managed Services.

### On-premise {#on-premise}

È possibile installare AEM sui server dell&#39;ambiente aziendale. Le istanze di installazione tipiche includono: ambienti di sviluppo, test e pubblicazione. Consulta la sezione [Guida introduttiva](/help/sites-deploying/deploy.md#getting%20started) per informazioni di base su come ottenere il software AEM per installarlo localmente.

Per ulteriori informazioni sulle tipiche implementazioni on-premise, consulta [Distribuzioni consigliate](/help/sites-deploying/recommended-deploys.md).

### Managed Services con Cloud Manager {#managed-services-using-cloud-manager}

AEM Managed Services è una soluzione completa per la gestione delle esperienze digitali. Offre i vantaggi della soluzione di distribuzione delle esperienze nel cloud, pur mantenendo tutti i vantaggi di controllo, sicurezza e personalizzazione di un’implementazione on-premise. AEM Managed Services consente ai clienti di avviarsi più rapidamente implementando sul cloud e utilizzando le best practice e il supporto di Adobe. Le organizzazioni e gli utenti aziendali possono coinvolgere i clienti in tempi minimi, aumentare la quota di mercato e concentrarsi sulla creazione di campagne di marketing innovative riducendo al contempo il carico sull&#39;IT.

Con AEM Managed Services i clienti possono realizzare i seguenti vantaggi:

**Time-to-Market più rapido:** Grazie all’infrastruttura cloud flessibile di Adobe Managed Services, le organizzazioni possono pianificare, avviare e ottimizzare rapidamente le esperienze digitali di successo. Adobe gestisce l’architettura cloud senza richiedere capitale, hardware o software aggiuntivo e i Customer Solutions Engineer di Adobe, aiutano con l’architettura AEM, il provisioning, la personalizzazione per la connessione alle app back-end e le best practice per la pubblicazione.

**Prestazioni più elevate:** Offre esperienze digitali affidabili per la tua azienda con quattro opzioni di disponibilità dei servizi: 99,5%, 99,9%, 99,95% e 99,99%. Consente inoltre il backup automatico e modelli di disaster recovery multimodali per garantire affidabilità e gestione di emergenza.

**Costi IT ottimizzati:** La guida proattiva e la competenza tecnica aiutano le organizzazioni a mantenere aggiornata la versione più recente dell’AEM. Adobe Platinum Maintenance and Support viene incluso automaticamente nelle nuove implementazioni di AMS Enterprise/Basic, offrendo competenze tecniche ed esperienza operativa per aiutare le organizzazioni a mantenere le applicazioni mission-critical. Le funzionalità di base gratuite di Analytics o Target offrono ulteriore valore, soprattutto per le organizzazioni di fascia media con esigenze limitate di analisi e personalizzazione.

**Massima sicurezza:** Garantisce la sicurezza fisica, di rete e dei dati di livello enterprise, ospitando le applicazioni dei clienti in una struttura ad accesso limitato, dietro i sistemi firewall o all&#39;interno di un cloud privato virtuale. Include macchine virtuali a tenant singolo con crittografia di storage dei dati affidabile, antivirali e isolamento dei dati.

**Cloud Manager**: Cloud Manager fa parte dell’offerta Managed Services di Adobe Experience Manager ed è un portale self-service che consente alle organizzazioni di gestire autonomamente Adobe Experience Manager nel cloud. Include una pipeline CI/CD (Continuous Integration and Continuous Delivery) all’avanguardia che consente ai team IT e ai partner di implementazione di velocizzare la distribuzione di personalizzazioni o aggiornamenti senza compromettere le prestazioni o la sicurezza. Cloud Manager è disponibile solo per gli Adobi di clienti Managed Service.

Per ulteriori informazioni su Cloud Manager e sulle relative risorse, consulta [**Guida utente di Cloud Manager**](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/introduction.html).

## Guida introduttiva {#getting-started}

### Prerequisiti {#prerequisites}

Mentre le istanze di produzione vengono in genere eseguite su computer dedicati che eseguono un sistema operativo ufficialmente supportato (vedi [Requisiti tecnici](/help/sites-deploying/technical-requirements.md)), il server di Experience Manager verrà eseguito su qualsiasi sistema che supporta [**Java Standard Edition 8**](https://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).

A scopo di familiarizzazione e per lo sviluppo su AEM è abbastanza comune utilizzare un&#39;istanza installata sul computer locale che esegue Apple OS X o versioni desktop di Microsoft Windows o Linux.

Sul lato client, AEM funziona con tutti i browser moderni (**Microsoft Edge**, **Internet Explorer** 11, **Chrome **51+** **, **Firefox **47+, **Safari** 8+) su sistemi operativi desktop e tablet. Consulta [Piattaforme client supportate](/help/sites-deploying/technical-requirements.md#supported-client-platforms) per i dettagli.

### Recupero del software {#getting-the-software}

I clienti con un contratto di manutenzione e supporto valido devono aver ricevuto una notifica e-mail con un codice ed essere in grado di scaricare l’AEM dal [**Sito Web Adobe Licensing**](https://licensing.adobe.com/). I partner commerciali possono richiedere l’accesso al download da [**spphelp@adobe.com**](mailto:spphelp@adobe.com).

Il pacchetto software AEM è disponibile in due formati:

* **cq-quickstart-6.5.0.jar:** Un eseguibile autonomo *barattolo* che include tutto il necessario per iniziare a utilizzare.

* **cq-quickstart-6.5.0.war:** A *guerra* per la distribuzione in un server applicazioni di terze parti.

Nella sezione seguente vengono descritte le **installazione autonoma**. Per ulteriori informazioni sull&#39;installazione di AEM in un server applicazioni, vedere [Installazione server applicazioni](/help/sites-deploying/application-server-install.md).

### Installazione locale predefinita {#default-local-install}

1. Creare una directory di installazione nel computer locale. Esempio:

   Percorso di installazione UNIX: **/opt/aem**

   Percorso di installazione di Windows: **`C:\Program Files\aem`**

   Allo stesso modo, è comune installare istanze di esempio in una cartella direttamente sul desktop. In ogni caso, ci riferiremo genericamente a questa posizione come:

   `<aem-install>`

   *Si noti che il percorso della directory dei file deve essere costituito solo da caratteri ASCII US.*

1. Posiziona **barattolo** e **licenza** file in questa directory:

   ```shell
   <aem-install>/
       cq-quickstart-6.5.0.jar
       license.properties
   ```

   Se non fornisci un’ `license.properties` , AEM reindirizzerà il browser a un **Benvenuti** all&#39;avvio, dove è possibile immettere un codice di licenza. Se non si dispone ancora di un codice di licenza, è necessario richiedere un codice di licenza valido all&#39;Adobe.

1. Per avviare l&#39;istanza in un ambiente GUI, fare doppio clic sul pulsante **`cq-quickstart-6.5.0.jar`** file.

   In alternativa, puoi avviare AEM dalla riga di comando:

   ```shell
       java -Xmx1024M -jar cq-quickstart-6.5.0.jar
   ```

L’AEM impiegherà alcuni minuti per decomprimere il file jar, installarsi e avviare. La procedura sopra descritta comporta:

* un **Autore AEM** istanza
* in esecuzione **localhost**
* sulla porta **4502**

Per accedere all’istanza, fai clic sul browser per:

**`https://localhost:4502`**

Il risultato nell’istanza di authoring verrà configurato automaticamente per la connessione a **istanza di pubblicazione** il **`localhost:4503`**.

### Installazioni di authoring e pubblicazione {#author-and-publish-installs}

L&#39;installazione predefinita (un **autore** istanza su **`localhost:4502`**) può essere modificata semplicemente rinominando il `jar` prima di avviarlo per la prima volta. Il pattern di denominazione è:

**`cq-<instance-type>-p<port-number>.jar`**

Ad esempio, rinominando il file in

**`cq-author-p4502.jar`**

e il suo avvio darà luogo a un’istanza di authoring in esecuzione su **`localhost:4502`**.

Analogamente, rinominare e avviare il file

**`cq-publish-p4503.jar`**

si tradurrà in un’istanza Publish in esecuzione su **`localhost:4503`**.

Ad esempio, installa queste due istanze in

`<aem-install>/author`e

**`<aem-install>/publish`**

Per ulteriori informazioni sulla personalizzazione dell&#39;installazione, vedere:

* [Installazione personalizzata indipendente](/help/sites-deploying/custom-standalone-install.md)
* [Modalità di esecuzione](/help/sites-deploying/configure-runmodes.md)

### Directory di installazione decompressa {#unpacked-install-directory}

Quando il file jar quickstart viene avviato per la prima volta, si decomprime nella stessa directory in una nuova sottodirectory denominata `crx-quickstart`. Dovresti finire con quanto segue:

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

>[!NOTE]
>
>Se si utilizzano i symlink, vedere [problemi relativi a symlink](https://helpx.adobe.com/experience-manager/kb/changing-symlink.html).

### Avvio e arresto {#starting-and-stopping}

Una volta che l’AEM si è disimballato e si è avviato per la prima volta, facendo doppio clic sul file jar nella directory di installazione si avvia semplicemente l’istanza, non la reinstalla.

Per arrestare l&#39;istanza dall&#39;interfaccia utente grafica, fare clic sul pulsante **on/off** accendere la finestra dell&#39;applicazione desktop.

È inoltre possibile arrestare e avviare AEM dalla riga di comando. Se hai già installato l’istanza per la prima volta, il **script della riga di comando** si trovano qui:

**`<aem-install>/crx-quickstart/bin/`**

Questa cartella contiene i seguenti script di shell base Unix:

* **`start`**: avvia l’istanza
* `stop`: arresta l’istanza
* **`status`**: segnala lo stato dell’istanza
* **`quickstart`**: utilizzato per configurare le informazioni di avvio, se necessario.

Ci sono anche equivalenti **`bat`** file per Windows. Per informazioni più dettagliate, consulta:

* [Avvio e interruzione da riga di comando](/help/sites-deploying/command-line-start-and-stop.md)

L’AEM avvia e reindirizza automaticamente il browser web alla pagina appropriata, solitamente la pagina di accesso; ad esempio:

`https://localhost:4502/`

![schermata di accesso](assets/screen_shot_2019-04-08at83533am.png)

Una volta effettuato l’accesso, puoi accedere all’AEM. Per ulteriori informazioni, a seconda del ruolo, consulta:

* [Authoring  ](/help/sites-authoring/home.md)
* [Amministrazione](/help/sites-administering/home.md)
* [Sviluppo](/help/sites-developing/home.md)
* [Gestione](/help/managing/best-practices.md)

## Implementazione avanzata {#advanced-deployment}

La sezione precedente consente di comprendere le nozioni di base dell&#39;installazione dell&#39;AEM. Tuttavia, l&#39;installazione di un sistema completo di produzione di AEM può comportare una complessità notevolmente maggiore. Per una copertura completa dell’installazione avanzata, consulta le seguenti pagine secondarie:

* [Requisiti tecnici](/help/sites-deploying/technical-requirements.md)
* [Distribuzioni consigliate](/help/sites-deploying/recommended-deploys.md)
* [Installazione personalizzata indipendente](/help/sites-deploying/custom-standalone-install.md)
* [Installazione dell’applicazione da server](/help/sites-deploying/application-server-install.md)
* [Risoluzione dei problemi](/help/sites-deploying/troubleshooting.md)
* [Avvio e interruzione da riga di comando](/help/sites-deploying/command-line-start-and-stop.md)
* [Configurazione](/help/sites-deploying/configuring.md)
* [Aggiornamento a AEM 6.5](/help/sites-deploying/upgrade.md)
* [eCommerce](/help/commerce/cif-classic/deploying/ecommerce.md)
* [Articoli pratici sulla configurazione](/help/sites-deploying/ht-deploy.md)
* [Console Web](/help/sites-deploying/web-console.md)
* [Risoluzione dei problemi di replica](/help/sites-deploying/troubleshoot-rep.md)
* [Best practice  ](/help/sites-deploying/best-practices.md)
* [Distribuzione delle community](/help/communities/deploy-communities.md)
* [Introduzione alla piattaforma AEM](/help/sites-deploying/platform.md)
* [Linee guida sulle prestazioni](/help/sites-deploying/performance-guidelines.md)
* [Guida introduttiva di AEM Mobile](/help/mobile/getting-started-aem-mobile.md)
* [Cos’è AEM Screens?](https://experienceleague.adobe.com/docs/experience-manager-screens/user-guide/aem-screens-introduction.html?lang=it)
