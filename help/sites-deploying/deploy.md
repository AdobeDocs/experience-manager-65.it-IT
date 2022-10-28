---
title: Implementazione e manutenzione
seo-title: Deploying and Maintaining
description: Scopri come iniziare a utilizzare l’installazione di AEM.
seo-description: Learn how to get started with the AEM installation.
uuid: 4429ac4d-abd7-47d8-b19d-773accb7cc7a
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: e48cc0ed-688c-44c8-b6d6-5f3c8593a295
docset: aem65
exl-id: 3df0662a-0768-4b56-8b94-c517657b4bd9
source-git-commit: bb8dbb9069c4575af62a4d0b21195cee75944fea
workflow-type: tm+mt
source-wordcount: '1808'
ht-degree: 8%

---

# Implementazione e manutenzione{#deploying-and-maintaining}

In questa pagina trovi:

* [Concetti di base](#basic-concepts)

   * [Che cos’è AEM?](#what-is-aem)
   * [Implementazioni tipiche](#typical-deployment-scenarios)

      * [On-Premise](#on-premise)
      * [Managed Services con Cloud Manager](#managed-services-using-cloud-manager)

* [Guida introduttiva](#getting-started)

   * [Prerequisiti](#prerequisites)
   * [Recupero del software](#getting-the-software)
   * [Installazione locale predefinita](#default-local-install)
   * [Installazione di authoring e pubblicazione](#author-and-publish-installs)
   * [Directory di installazione non imballata](#unpacked-install-directory)
   * [Avvio e arresto](#starting-and-stopping)

Una volta acquisita familiarità con queste nozioni di base, troverai informazioni più avanzate e dettagliate nelle seguenti sottopagine:

* [Requisiti tecnici](/help/sites-deploying/technical-requirements.md)
* [Implementazioni consigliate](/help/sites-deploying/recommended-deploys.md)
* [Installazione personalizzata indipendente](/help/sites-deploying/custom-standalone-install.md)
* [Installazione dell’applicazione da server](/help/sites-deploying/application-server-install.md)
* [Risoluzione dei problemi](/help/sites-deploying/troubleshooting.md)
* [Avvio e interruzione da riga di comando](/help/sites-deploying/command-line-start-and-stop.md)
* [Configurazione](/help/sites-deploying/configuring.md)
* [Aggiornamento a AEM 6.5](/help/sites-deploying/upgrade.md)
* [eCommerce](/help/commerce/cif-classic/deploying/ecommerce.md)
* [Articoli dimostrativi sulla configurazione](/help/sites-deploying/ht-deploy.md)
* [Console Web](/help/sites-deploying/web-console.md)
* [Risoluzione dei problemi di replica](/help/sites-deploying/troubleshoot-rep.md)
* [Best practice  ](/help/sites-deploying/best-practices.md)
* [Distribuzione di Communities](/help/communities/deploy-communities.md)
* [Introduzione alla piattaforma AEM](/help/sites-deploying/platform.md)
* [Linee guida sulle prestazioni](/help/sites-deploying/performance-guidelines.md)
* [Guida introduttiva di AEM Mobile](/help/mobile/getting-started-aem-mobile.md)
* [Cos’è AEM Screens?](https://docs.adobe.com/content/help/it/experience-manager-screens/user-guide/aem-screens-introduction.html)

## Concetti di base {#basic-concepts}

### Che cos’è AEM? {#what-is-aem}

Adobe Experience Manager è un sistema client-server basato sul Web per la creazione, gestione e distribuzione di siti Web commerciali e di servizi correlati, che combina varie funzioni a livello di infrastruttura e di applicazione in un unico pacchetto integrato.

A livello di infrastruttura AEM fornisce quanto segue:

* **Server applicazioni Web**: AEM può essere implementato in modalità autonoma (include un server web Jetty integrato) o come applicazione web all’interno di un server applicativo di terze parti.
* **Framework applicazione Web**: AEM incorpora Sling Web Application Framework che semplifica la scrittura di applicazioni web RESTful orientate ai contenuti.
* **Archivio dei contenuti**: AEM include un Java Content Repository (JCR), un tipo di database gerarchico progettato specificatamente per dati non strutturati e semi-strutturati. Il repository memorizza non solo il contenuto rivolto all&#39;utente, ma anche tutto il codice, i modelli e i dati interni utilizzati dall&#39;applicazione.

Sulla base di questa base, AEM offre anche una serie di funzioni a livello di applicazione per la gestione di:

* **Siti Web**
* **Applicazioni mobili**
* **Pubblicazioni digitali**
* **Forms**
* **Risorse digitali**
* **Communities**
* **Commercio online**

Infine, i clienti possono utilizzare questi blocchi di base a livello di infrastruttura e applicazione per creare soluzioni personalizzate creando applicazioni personalizzate.

Il server AEM è **Basato su Java** e viene eseguito sulla maggior parte dei sistemi operativi che supportano tale piattaforma. L’interazione con AEM da parte del client viene eseguita tramite un **browser web**.

### Scenari di implementazione tipici {#typical-deployment-scenarios}

Nella terminologia AEM &quot;istanza&quot; è una copia di AEM in esecuzione su un server. Le installazioni AEM di solito coinvolgono almeno due istanze, in genere in esecuzione su macchine separate:

* **Autore**: Un’istanza AEM utilizzata per creare, caricare e modificare i contenuti e per amministrare il sito web. Quando il contenuto è pronto per essere live, viene replicato nell’istanza di pubblicazione.
* **Pubblica**: Un&#39;istanza AEM che trasmette il contenuto pubblicato al pubblico.

Queste istanze sono identiche in termini di software installato. Sono differenziati solo dalla configurazione. Inoltre, la maggior parte delle installazioni utilizza un dispatcher:

* **Dispatcher**: Un server web statico (Apache httpd, Microsoft IIS, ecc.) è stato migliorato con il modulo dispatcher AEM. Memorizza in cache le pagine web prodotte dall’istanza di pubblicazione per migliorare le prestazioni.

Questa configurazione offre molte opzioni avanzate ed elaborazioni, ma il modello di base di authoring, pubblicazione e dispatcher è al centro della maggior parte delle distribuzioni. Inizieremo concentrandoci su un assetto relativamente semplice. Seguirà la discussione sulle opzioni di distribuzione avanzate.

Le sezioni seguenti descrivono entrambi gli scenari:

* **On-Premise**: AEM implementato e gestito nel tuo ambiente aziendale.

* **Managed Services - Cloud Manager per Adobe Experience Manager**: AEM implementato e gestito da Adobe Managed Services.

### On-Premise {#on-premise}

È possibile installare AEM sui server nel proprio ambiente aziendale. Le istanze di installazione tipiche includono: Ambienti di sviluppo, test e pubblicazione. Fai riferimento alla [Introduzione](/help/sites-deploying/deploy.md#getting%20started) sezione per informazioni di base su come ottenere il software AEM per installarlo localmente.

Per ulteriori informazioni sulle tipiche distribuzioni locali, consulta [Implementazioni consigliate](/help/sites-deploying/recommended-deploys.md).

### Managed Services con Cloud Manager {#managed-services-using-cloud-manager}

AEM Managed Services è una soluzione completa per la gestione delle esperienze digitali. Offre vantaggi della soluzione di distribuzione dell’esperienza nel cloud, mantenendo al tempo stesso tutti i vantaggi di controllo, sicurezza e personalizzazione derivanti da un’implementazione on-premise. AEM Managed Services consente ai clienti di avviare più rapidamente implementando sul cloud e anche basandosi sulle best practice e il supporto di Adobe. Le organizzazioni e gli utenti aziendali possono coinvolgere i clienti in tempi minimi, promuovere la quota di mercato e concentrarsi sulla creazione di campagne di marketing innovative riducendo al contempo il carico sull&#39;IT.

Con AEM i clienti Managed Services possono realizzare i seguenti vantaggi:

**Time to Market più rapido:** Grazie all’infrastruttura cloud flessibile di Adobe Managed Services, le organizzazioni possono pianificare, avviare e ottimizzare rapidamente le esperienze digitali di successo. Adobe gestisce l’architettura cloud senza bisogno di capitale aggiuntivo, hardware o software e gli ingegneri di successo dei clienti di Adobe, aiutano con l’architettura AEM, il provisioning, la personalizzazione per la connessione alle app back-end e le best practice per il go-live.

**Prestazioni più elevate:** Offre esperienze digitali affidabili per la tua azienda con quattro opzioni di disponibilità dei servizi: 99,5%, 99,9%, 99,95% e 99,99%. Inoltre, consente il backup automatico e modelli di disaster recovery multimodali per garantire affidabilità e gestione delle situazioni di emergenza.

**Costi IT ottimizzati:** Assistenza e competenza proattiva aiutano le organizzazioni a rimanere aggiornate sull&#39;ultima versione di AEM. Adobe Platinum Maintenance and Support è incluso automaticamente nelle nuove implementazioni di AMS Enterprise/Basic, offrendo competenze tecniche ed esperienza operativa per aiutare le organizzazioni a mantenere le applicazioni mission critical. Le funzionalità di base gratuite di Analytics o Target offrono un valore aggiuntivo, in particolare per le organizzazioni di mercato medio con esigenze limitate di analisi e personalizzazione.

**Massima sicurezza:** Garantisce la sicurezza fisica, di rete e dei dati di livello enterprise ospitando le applicazioni dei clienti in una struttura ad accesso limitato, dietro i sistemi firewall o all&#39;interno di un cloud privato virtuale. Include macchine virtuali a tenant singolo con crittografia di archiviazione dati affidabile, antivirali e isolamento dei dati.

**Cloud Manager**: Cloud Manager, parte dell’offerta Adobe Experience Manager Managed Services, è un portale self-service che consente alle organizzazioni di gestire autonomamente Adobe Experience Manager nel cloud. Include una pipeline CI/CD (Continuous Integration/Continuous Delivery) all’avanguardia che consente ai team IT e ai partner di implementazione di velocizzare la distribuzione di personalizzazioni o aggiornamenti senza compromettere prestazioni o sicurezza. Cloud Manager è disponibile solo per i clienti di Adobe Managed Service.

Per ulteriori informazioni su Cloud Manager e le relative risorse, consulta [**Guida utente di Cloud Manager**](https://docs.adobe.com/content/help/it/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html).

## Guida introduttiva {#getting-started}

### Prerequisiti {#prerequisites}

Mentre le istanze di produzione vengono solitamente eseguite su macchine dedicate che eseguono un sistema operativo ufficialmente supportato (vedi [Requisiti tecnici](/help/sites-deploying/technical-requirements.md)), il server di Experience Manager verrà eseguito su qualsiasi sistema che supporti [**Java Standard Edition 8**](https://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).

Per scopi di familiarizzazione e per lo sviluppo su AEM è abbastanza comune utilizzare un&#39;istanza installata sul tuo computer locale che esegue Apple OS X o versioni desktop di Microsoft Windows o Linux.

Sul lato client, AEM funziona con tutti i browser moderni (**Microsoft Edge**, **Internet Explorer** 11, **Chrome **51+** **, **Firefox **47+, **Safari** 8+) sia sui sistemi operativi desktop che tablet. Vedi [Piattaforme client supportate](/help/sites-deploying/technical-requirements.md#supported-client-platforms) per i dettagli.

### Recupero del software {#getting-the-software}

I clienti con un contratto di manutenzione e assistenza valido devono aver ricevuto una notifica via e-mail con un codice ed essere in grado di scaricare AEM dal [**Sito Web Adobe Licensing**](https://licensing.adobe.com/). I partner commerciali possono richiedere l&#39;accesso al download da [**spphelp@adobe.com**](mailto:spphelp@adobe.com).

Il pacchetto software AEM è disponibile in due moduli:

* **cq-quickstart-6.5.0.jar:** Un eseguibile autonomo *barattolo* file che include tutto ciò che è necessario per iniziare a funzionare.

* **cq-quickstart-6.5.0.war:** A *guerra* file per la distribuzione in un server applicazioni di terze parti.

Nella sezione seguente descriviamo il **installazione indipendente**. Per informazioni dettagliate sull&#39;installazione di AEM in un server applicazioni, vedi [Installazione del server applicazioni](/help/sites-deploying/application-server-install.md).

### Installazione locale predefinita {#default-local-install}

1. Crea una directory di installazione sul computer locale. Esempio:

   Percorso di installazione UNIX: **/opt/aem**

   Percorso di installazione di Windows: **`C:\Program Files\aem`**

   Allo stesso modo, è comune installare istanze di esempio in una cartella direttamente sul desktop. In ogni caso, riferiremo genericamente a questa posizione come:

   `<aem-install>`

   *Tenere presente che il percorso della directory dei file deve essere costituito solo da caratteri ASCII statunitensi.*

1. Posiziona il **barattolo** e **license **files in this directory:

   ```shell
   <aem-install>/
       cq-quickstart-6.5.0.jar
       license.properties
   ```

   Se non fornisci un `license.properties` AEM reindirizzerà il browser a un **Benvenuto** all&#39;avvio, dove è possibile immettere una chiave di licenza. Se non ne hai ancora uno, dovrai richiedere una chiave di licenza valida da Adobe.

1. Per avviare l&#39;istanza in un ambiente GUI, fai doppio clic sul pulsante **`cq-quickstart-6.5.0.jar`** file.

   In alternativa, puoi avviare AEM dalla riga di comando:

   ```shell
       java -Xmx1024M -jar cq-quickstart-6.5.0.jar
   ```

AEM ci vorranno alcuni minuti per rimuovere il file jar, installarsi e avviare. La procedura di cui sopra si traduce in:

* un **autore AEM** istanza
* in esecuzione **localhost**
* sulla porta **4502**

Per accedere all’istanza, posiziona il browser in base a:

**`https://localhost:4502`**

Il risultato nell’istanza di authoring verrà configurato automaticamente per connettersi a un **pubblica istanza** su **`localhost:4503`**.

### Installazione di authoring e pubblicazione {#author-and-publish-installs}

L&#39;installazione predefinita (un **autore** istanza su **`localhost:4502`**) può essere modificata semplicemente rinominando il `jar` prima di avviarlo per la prima volta. Il pattern di denominazione è:

**`cq-<instance-type>-p<port-number>.jar`**

Ad esempio, rinominare il file in

**`cq-author-p4502.jar`**

e il suo avvio darà luogo a un&#39;istanza di authoring in esecuzione su **`localhost:4502`**.

Analogamente, rinominare e avviare il file

**`cq-publish-p4503.jar`**

comporterà l&#39;esecuzione di un&#39;istanza di pubblicazione su **`localhost:4503`**.

Installa queste due istanze in, ad esempio

`<aem-install>/author`e

**`<aem-install>/publish`**

Per ulteriori dettagli sulla personalizzazione dell&#39;installazione, consulta:

* [Installazione personalizzata indipendente](/help/sites-deploying/custom-standalone-install.md)
* [Modalità di esecuzione](/help/sites-deploying/configure-runmodes.md)

### Directory di installazione non imballata {#unpacked-install-directory}

Quando il jar quickstart viene avviato per la prima volta, si estrae nella stessa directory sotto una nuova sottodirectory denominata `crx-quickstart`. Dovresti finire con quanto segue:

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

Se l’istanza è stata installata dall’interfaccia utente, viene visualizzata automaticamente una finestra del browser e viene visualizzata anche una finestra dell’applicazione desktop che visualizza l’host e la porta dell’istanza e un interruttore on/off:

![schermata di avvio](assets/screen_shot_.png)

>[!NOTE]
>
>Se utilizzi collegamenti simbolici, consulta [problemi con symlink](https://helpx.adobe.com/experience-manager/kb/changing-symlink.html).

### Avvio e arresto {#starting-and-stopping}

Una volta che AEM ha disimballato se stesso e avviato per la prima volta, facendo doppio clic sul file jar nella directory di installazione si avvia semplicemente l&#39;istanza, non la reinstalla.

Per interrompere l&#39;istanza dall&#39;interfaccia grafica, fai clic sul pulsante **on/off** attivare la finestra dell&#39;applicazione desktop.

È inoltre possibile arrestare e avviare AEM dalla riga di comando. Presupponendo che l’istanza sia già stata installata per la prima volta, l’ **script della riga di comando** si trovano qui:

**`<aem-install>/crx-quickstart/bin/`**

Questa cartella contiene i seguenti script di shell base Unix:

* **`start`**: Avvia l&#39;istanza
* `stop`: Interrompe l&#39;istanza
* **`status`**: Segnala lo stato dell’istanza
* **`quickstart`**: Utilizzato per configurare le informazioni di avvio, se necessario.

Ci sono anche equivalenti **`bat`** file per Windows. Per informazioni più dettagliate, consulta:

* [Avvio e interruzione da riga di comando](/help/sites-deploying/command-line-start-and-stop.md)

AEM avvia e reindirizza automaticamente il browser Web alla pagina appropriata, in genere la pagina di accesso; ad esempio:

`https://localhost:4502/`

![schermata di accesso](assets/screen_shot_2019-04-08at83533am.png)

Una volta effettuato l&#39;accesso, potrai accedere a AEM. Per ulteriori informazioni, a seconda del ruolo, consulta quanto segue:

* [Authoring  ](/help/sites-authoring/home.md)
* [Amministrazione](/help/sites-administering/home.md)
* [Sviluppo](/help/sites-developing/home.md)
* [Gestione](/help/managing/best-practices.md)

## Implementazione avanzata {#advanced-deployment}

La sezione precedente dovrebbe fornire una buona comprensione delle basi dell&#39;installazione AEM. Tuttavia, l&#39;installazione di un sistema di produzione completo di AEM può comportare una notevole complessità. Per una copertura completa dell’installazione avanzata, consulta le seguenti sottopagine:

* [Requisiti tecnici](/help/sites-deploying/technical-requirements.md)
* [Implementazioni consigliate](/help/sites-deploying/recommended-deploys.md)
* [Installazione personalizzata indipendente](/help/sites-deploying/custom-standalone-install.md)
* [Installazione dell’applicazione da server](/help/sites-deploying/application-server-install.md)
* [Risoluzione dei problemi](/help/sites-deploying/troubleshooting.md)
* [Avvio e interruzione da riga di comando](/help/sites-deploying/command-line-start-and-stop.md)
* [Configurazione](/help/sites-deploying/configuring.md)
* [Aggiornamento a AEM 6.5](/help/sites-deploying/upgrade.md)
* [eCommerce](/help/commerce/cif-classic/deploying/ecommerce.md)
* [Articoli dimostrativi sulla configurazione](/help/sites-deploying/ht-deploy.md)
* [Console Web](/help/sites-deploying/web-console.md)
* [Risoluzione dei problemi di replica](/help/sites-deploying/troubleshoot-rep.md)
* [Best practice  ](/help/sites-deploying/best-practices.md)
* [Distribuzione di Communities](/help/communities/deploy-communities.md)
* [Introduzione alla piattaforma AEM](/help/sites-deploying/platform.md)
* [Linee guida sulle prestazioni](/help/sites-deploying/performance-guidelines.md)
* [Guida introduttiva di AEM Mobile](/help/mobile/getting-started-aem-mobile.md)
* [Cos’è AEM Screens?](https://docs.adobe.com/content/help/en/experience-manager-screens/user-guide/aem-screens-introduction.html)
