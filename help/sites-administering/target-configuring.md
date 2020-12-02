---
title: Configurazione manuale dell'integrazione con  Adobe Target
seo-title: Configurazione manuale dell'integrazione con  Adobe Target
description: Scoprite come configurare manualmente l'integrazione con  Adobe Target.
seo-description: Scoprite come configurare manualmente l'integrazione con  Adobe Target.
uuid: 0bb76a65-f981-4cc5-bee8-5feb3297137c
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 20c8eb1d-5847-4902-b7d3-4c3286423b46
translation-type: tm+mt
source-git-commit: a8ba56849f6bb9f0cf6571fc51f4b5cae71620e0
workflow-type: tm+mt
source-wordcount: '2202'
ht-degree: 5%

---


# Configurazione manuale dell&#39;integrazione con  Adobe Target {#manually-configuring-the-integration-with-adobe-target}

È possibile modificare le configurazioni della procedura guidata di consenso o integrare manualmente  Adobe Target senza ricorrere alla procedura guidata.

## Modifica delle configurazioni della procedura guidata di consenso {#modifying-the-opt-in-wizard-configurations}

La [procedura guidata di consenso](/help/sites-administering/opt-in.md) che [integra AEM con  Adobe Target](/help/sites-administering/target.md) crea automaticamente una configurazione cloud di Target denominata Configurazione di destinazione con provisioning. La procedura guidata crea inoltre un framework Target per la configurazione cloud denominato Provisioning Target Framework. Se necessario, potete modificare le proprietà della configurazione e della struttura del cloud.

Potete anche configurare  Adobe Target per utilizzare  Adobe Target come origine di reporting per il targeting del contenuto configurando la configurazione A4T  Analytics Cloud Configuration.

Per individuare la configurazione cloud e il framework, passare a **Cloud Services** tramite **Strumenti** > **Distribuzione** > **Cloud**. ([http://localhost:4502/libs/cq/core/content/tools/cloudservices.html](http://localhost:4502/libs/cq/core/content/tools/cloudservices.html))
Sotto  Adobe Target, fare clic o toccare **Mostra configurazioni**.

### Proprietà di configurazione di Target con provisioning {#provisioned-target-configuration-properties}

I seguenti valori di proprietà vengono utilizzati nella configurazione cloud di configurazione di Target con provisioning creata dalla procedura guidata di consenso:

* **Codice client:** come specificato nella procedura guidata di consenso.
* **E-mail:** come specificato nella procedura guidata di consenso.
* **Password:** come specificato nella procedura guidata di consenso.
* **Tipo API:** REST
* **Sincronizza Segmenti Da  Adobe Target:** Selezionati.

* **Libreria client:** mbox.js.
* **Utilizza DTM per distribuire la libreria client:** non selezionato. Selezionate questa opzione se [utilizzate DTM](/help/sites-administering/dtm.md) o un altro sistema di gestione tag per ospitare il file mbox.js o AT.js.  Adobe consiglia di utilizzare Gestione dinamica dei tag anziché AEM per distribuire la libreria.

* **Custom mbox.js:** None specificato in modo che venga utilizzato il file mbox.js predefinito. Specificate un file mbox.js personalizzato da utilizzare come necessario. Viene visualizzato solo se avete selezionato mbox.js.
* **AT.js personalizzato:** Nessuno specificato in modo che venga utilizzato il file AT.js predefinito. Specificate un file AT.js personalizzato da utilizzare come necessario. Viene visualizzato solo se avete selezionato AT.js.

>[!NOTE]
>
>In AEM 6.3, è possibile selezionare il file della libreria Target, [AT.JS](https://docs.adobe.com/content/help/en/target/using/implement-target/client-side/mbox-implement/mbox-download.html), una nuova libreria di implementazione per  Adobe Target progettata sia per le implementazioni Web tipiche che per le applicazioni a pagina singola.
>
>AT.js offre diversi miglioramenti rispetto alla libreria mbox.js:
>
>* Tempi di caricamento delle pagine migliorati per le implementazioni Web
>* Maggiore sicurezza
>* Migliori opzioni di implementazione per le applicazioni a pagina singola
>* AT.js contiene i componenti che erano inclusi in target.js, pertanto non esiste più una chiamata a target.js


### Proprietà del framework di Target con provisioning {#provisioned-target-framework-properties}

Il framework di destinazione con provisioning creato dalla procedura guidata di consenso è configurato per l&#39;invio di dati contestuali dall&#39;archivio dati profilo. Per impostazione predefinita, gli elementi relativi a età e genere dello store vengono inviati a Target. Probabilmente la soluzione richiede l&#39;invio di parametri aggiuntivi.

![chlimage_1-158](assets/chlimage_1-158.png)

Potete configurare il framework per inviare informazioni di contesto aggiuntive a Target come descritto in [Aggiunta di un framework di Target](/help/sites-administering/target-configuring.md#adding-a-target-framework).

### Configurazione di A4T  Analytics Cloud {#configuring-a-t-analytics-cloud-configuration}

Potete configurare  Adobe Target per utilizzare  Adobe Analytics come origine di reporting per il targeting del contenuto.

A tal fine, dovete specificare quale configurazione cloud A4T collegare la configurazione cloud Adobe Target  con:

1. Andate a **Cloud Services** tramite il **logo AEM** > **Strumenti** > **Distribuzione** > **Cloud Services**.
1. Nella sezione **Adobe Target**, fare clic su **Configura ora**.
1. Riconnettersi alla configurazione Adobe Target .
1. Nel menu a discesa **A4T  Analytics Cloud Configuration**, selezionate il framework.

   >[!NOTE]
   >
   >Sono disponibili solo le configurazioni di analisi abilitate per A4T.
   >
   >Durante la configurazione di A4T con AEM, potrebbe essere presente una voce di riferimento alla configurazione mancante. Per poter selezionare il framework di analisi, effettuate le seguenti operazioni:
   >
   >1. Passare a **Strumenti** > **Generale** > **CRXDE Lite**.
   1. Andate a **/libs/cq/analytics/components/testandtargetpage/dialog/items/tab/items/tab1_general/items/a4tAnalyticsConfig**
   1. Impostare la proprietà **disable** su **false**.
   1. Toccate o fate clic su **Salva tutto**.


   ![chlimage_1-159](assets/chlimage_1-159.png)

   Fai clic su **OK**. Quando eseguite il targeting del contenuto con  Adobe Target, potete [selezionare l&#39;origine del report](/help/sites-authoring/content-targeting-touch.md).

## Integrazione manuale con  Adobe Target {#manually-integrating-with-adobe-target}

Effettuate l&#39;integrazione manuale con  Adobe Target invece di utilizzare la procedura guidata di consenso.

>[!NOTE]
Il file della libreria Target, [AT.JS](https://docs.adobe.com/content/help/en/target/using/implement-target/client-side/mbox-implement/mbox-download.html), è una nuova libreria di implementazione per  Adobe Target, progettata sia per le implementazioni Web tipiche che per le applicazioni a pagina singola.  Adobe consiglia di utilizzare AT.js invece di mbox.js come libreria client.
AT.js offre diversi miglioramenti rispetto alla libreria mbox.js:
* Tempi di caricamento delle pagine migliorati per le implementazioni Web
* Maggiore sicurezza
* Migliori opzioni di implementazione per le applicazioni a pagina singola
* AT.js contiene i componenti che erano inclusi in target.js, pertanto non esiste più una chiamata a target.js

È possibile selezionare AT.js o mbox.js nel menu a discesa **Libreria client**.

### Creazione di una configurazione di Target Cloud {#creating-a-target-cloud-configuration}

Per abilitare AEM a interagire con  Adobe Target, crea una configurazione cloud di Target. Per creare la configurazione, dovete fornire il codice client Adobe Target  e le credenziali utente.

Potete creare la configurazione cloud di Target solo una volta, perché potete associare la configurazione a più campagne AEM. Se avete diversi codici client Adobe Target , create una configurazione per ciascun codice client.

Puoi configurare la configurazione cloud per sincronizzare i segmenti da  Adobe Target. Se abilitate la sincronizzazione, i segmenti vengono importati in background da Target non appena viene salvata la configurazione cloud.

Utilizzate la procedura seguente per creare una configurazione cloud di Target in AEM:

1. Andate a **Cloud Services** tramite il **logo AEM** > **Strumenti** > **Distribuzione** > **Cloud Services**. ([http://localhost:4502/libs/cq/core/content/tools/cloudservices.html](http://localhost:4502/libs/cq/core/content/tools/cloudservices.html))

   Viene visualizzata la pagina di panoramica **Adobe Marketing Cloud**.

1. Nella sezione **Adobe Target**, fare clic su **Configura ora**.
1. Nella finestra di dialogo **Crea configurazione**:

   1. Assegnare alla configurazione un **Titolo**.
   1. Selezionare il modello **Adobe Target Configuration**.
   1. Fai clic su **Crea**.

   Viene visualizzata la finestra di dialogo di modifica.

   ![chlimage_1-160](assets/chlimage_1-160.png)

   >[!NOTE]
   Durante la configurazione di A4T con AEM, potrebbe essere presente una voce di riferimento alla configurazione mancante. Per poter selezionare il framework di analisi, effettuate le seguenti operazioni:
   1. Passare a **Strumenti** > **Generale** > **CRXDE Lite**.
   1. Andate a **/libs/cq/analytics/components/testandtargetpage/dialog/items/tab/items/tab1_general/items/a4tAnalyticsConfig**
   1. Impostare la proprietà **disable** su **false**.
   1. Toccate o fate clic su **Salva tutto**.


1. Nella finestra di dialogo, inserite i valori per queste proprietà.

   * **Codice** client: il codice client dell&#39;account di destinazione
   * **E-mail**: l&#39;e-mail dell&#39;account Target.
   * **Password**: la password dell&#39;account Target.
   * **Tipo** API: REST o XML
   * **Configurazione** A4T  Analytics Cloud: Seleziona la configurazione cloud di Analytics utilizzata per gli obiettivi e le metriche dell&#39;attività di destinazione. Questo è necessario se utilizzate  Adobe Analytics come origine di reporting quando eseguite il targeting del contenuto. Se non visualizzate la configurazione cloud, consultate la nota in [Configurazione A4T  configurazione Analytics Cloud](#configuring-a-t-analytics-cloud-configuration).

   * **Usa targeting preciso:** per impostazione predefinita questa casella di controllo è selezionata. Se selezionata, la configurazione del servizio cloud attende il caricamento del contesto prima di caricare il contenuto. Vedere la nota che segue.
   * **Sincronizza segmenti da  Adobe Target:** selezionare questa opzione per scaricare i segmenti definiti in Target per utilizzarli in AEM. Devi selezionare questa opzione quando la proprietà Tipo API è REST, perché i segmenti in linea non sono supportati e devi sempre utilizzare i segmenti da Target. Il termine AEM &quot;segmento&quot; è equivalente al termine &quot;audience&quot; di Target.
   * **Libreria client:** selezionate se desiderate la libreria client mbox.js o AT.js.
   * **Utilizza DTM per distribuire la libreria**  client: seleziona questa opzione per utilizzare AT.js o mbox.js da DTM o un altro sistema di gestione tag. Per utilizzare questa opzione è necessario [configurare l&#39;integrazione DTM](/help/sites-administering/dtm.md).  Adobe consiglia di utilizzare Gestione dinamica dei tag anziché AEM per distribuire la libreria.
   * **Custom mbox.js**: Lasciate vuoto se avete selezionato la casella Gestione dinamica dei tag o per utilizzare il file mbox.js predefinito. In alternativa, caricate il mbox.js personalizzato. Viene visualizzato solo se avete selezionato mbox.js.
   * **AT.js** personalizzato: Lasciate vuoto se avete selezionato la casella Gestione dinamica dei tag o per utilizzare il file AT.js predefinito. In alternativa, caricate il vostro AT.js personalizzato. Viene visualizzato solo se avete selezionato AT.js.

   >[!NOTE]
   Per impostazione predefinita, quando si sceglie di accedere alla  procedura guidata di configurazione di Adobe Target, viene attivato il targeting accurato.
   Con targeting accurato, la configurazione del servizio cloud attende che il contesto venga caricato prima di caricare il contenuto. Di conseguenza, in termini di prestazioni, un targeting accurato potrebbe creare un ritardo di alcuni millisecondi prima del caricamento del contenuto.
   Il targeting accurato è sempre abilitato nell&#39;istanza di creazione. Tuttavia, nell&#39;istanza di pubblicazione potete scegliere di disattivare il targeting accurato a livello globale deselezionando il segno di spunta accanto a Accurata Targeting nella configurazione del servizio cloud (**http://localhost:4502/etc/cloudservices.html**). Potete inoltre attivare e disattivare il targeting accurato per i singoli componenti, indipendentemente dall&#39;impostazione nella configurazione del servizio cloud.
   Se ***già*** sono stati creati componenti di destinazione e modificate questa impostazione, le modifiche apportate non influiscono su tali componenti. È necessario apportare direttamente modifiche a tali componenti.

1. Fate clic su **Connetti a Target** per inizializzare la connessione con Target. Se la connessione ha esito positivo, viene visualizzato il messaggio **Connessione riuscita**. Fare clic su **OK** sul messaggio, quindi su **OK** nella finestra di dialogo.

   Se non riuscite a connettervi a Target, consultate la sezione [risoluzione dei problemi](/help/sites-administering/target-configuring.md#troubleshooting-target-connection-problems).

### Aggiunta di un framework di destinazione {#adding-a-target-framework}

Dopo aver configurato la configurazione cloud di Target, aggiungi un framework Target. Il framework identifica i parametri predefiniti inviati a  Adobe Target dai componenti [Client Context](/help/sites-administering/client-context.md) o [ContextHub](/help/sites-developing/ch-configuring.md) disponibili. Target utilizza i parametri per determinare i segmenti che si applicano al contesto corrente.

Potete creare più framework per una singola configurazione di Target. Più framework sono utili quando è necessario inviare a Target un set diverso di parametri per diverse sezioni del sito Web. Create un framework per ciascun set di parametri da inviare. Associate ogni sezione del sito Web al framework appropriato. Una pagina Web può utilizzare un solo framework per volta.

1. Nella pagina di configurazione di Target, fate clic sul **+** (segno più) accanto a Framework disponibili.
1. Nella finestra di dialogo Crea framework, specificate un **Titolo**, selezionate il **Adobe Target Framework** e fate clic su **Crea**.

   ![chlimage_1-161](assets/chlimage_1-161.png)

   Viene visualizzata la pagina del framework. La barra laterale fornisce componenti che rappresentano le informazioni provenienti dal [Client Context](/help/sites-administering/client-context.md) o da [ContextHub](/help/sites-developing/ch-configuring.md) mappabili dall&#39;utente.

   ![chlimage_1-162](assets/chlimage_1-162.png)

1. Trascinare il componente ClientContext che rappresenta i dati da utilizzare per la mappatura sulla destinazione di rilascio. In alternativa, trascinate il componente **ContextHub Store** nel framework.

   >[!NOTE]
   Durante la mappatura, i parametri vengono passati a una mbox tramite semplici stringhe. Non è possibile mappare array da ContextHub.

   Ad esempio, per utilizzare **Dati profilo** sui visitatori del sito per controllare la campagna Target, trascinate il componente **Dati profilo** sulla pagina. Vengono visualizzate le variabili di dati del profilo disponibili per la mappatura ai parametri di Target.

   ![chlimage_1-163](assets/chlimage_1-163.png)

1. Selezionate le variabili che desiderate rendere visibili al sistema Adobe Target  selezionando la casella di controllo **Condividi** nelle colonne appropriate.

   ![chlimage_1-164](assets/chlimage_1-164.png)

   >[!NOTE]
   La sincronizzazione dei parametri è solo unidirezionale, da AEM a  Adobe Target.

Il framework viene creato. Per replicare il framework nell&#39;istanza di pubblicazione, utilizzate l&#39;opzione **Attiva framework** dalla barra laterale.

### Associazione delle attività con la configurazione di Target Cloud {#associating-activities-with-the-target-cloud-configuration}

Associate le attività di [AEM](/help/sites-authoring/activitylib.md) alla configurazione cloud di Target in modo da poter eseguire il mirroring delle attività in [ Adobe Target](https://docs.adobe.com/content/help/en/target/using/experiences/offers/manage-content.html).

>[!NOTE]
Il tipo di attività disponibile viene stabilito in base ai seguenti elementi:
* Se l&#39;opzione **xt_only** è abilitata sul tenant di Adobe Target (clientcode) utilizzato sul lato AEM per connettersi ad Adobe Target, puoi creare **solo** attività XT in AEM.

* Se le opzioni **xt_only** **non** sono abilitate sul tenant di Adobe Target (clientcode), puoi creare **sia** le attività XT che A/B in AEM.

**Nota aggiuntiva:** le opzioni **xt_only** sono un&#39;impostazione applicata a un determinato tenant Target (clientcode) e possono essere modificate solo direttamente in Adobe Target. Non puoi attivare o disattivare questa opzione da AEM.

### Associazione del framework di Target al sito {#associating-the-target-framework-with-your-site}

Dopo aver creato un framework Target in AEM, associate le pagine Web al framework. I componenti di destinazione nelle pagine inviano i dati definiti dal framework a  Adobe Target per il tracciamento. (Vedere [Targeting dei contenuti](/help/sites-authoring/content-targeting-touch.md).)

Quando associate una pagina al framework, le pagine figlie ereditano l&#39;associazione.

1. Nella console **Siti**, andate al sito che desiderate configurare.
1. Utilizzando la [azioni rapide](/help/sites-authoring/basic-handling.md#quick-actions) o la [modalità di selezione](/help/sites-authoring/basic-handling.md), selezionare **Visualizza proprietà.**
1. Selezionare la scheda **Cloud Services**.
1. Toccate/fate clic su **Modifica**.
1. Toccate/fate clic su **Aggiungi configurazione** in **Configurazioni Cloud Service** e selezionate **Adobe Target**.

   ![chlimage_1-165](assets/chlimage_1-165.png)

1. Selezionare il framework desiderato in **Riferimento configurazione**.

   >[!NOTE]
   Accertatevi di selezionare il **framework** specifico creato e non la configurazione cloud di Target in cui è stato creato.

1. Toccate/fate clic su **Fine**.
1. Attivate la pagina principale del sito Web per replicarla sul server di pubblicazione. (Vedere [Come pubblicare le pagine](/help/sites-authoring/publishing-pages.md).)

   >[!NOTE]
   Se il framework allegato alla pagina non è stato ancora attivato, si apre una procedura guidata che consente di pubblicarlo.

## Risoluzione dei problemi di connessione a Target {#troubleshooting-target-connection-problems}

Per risolvere i problemi che si verificano durante la connessione a Target, effettuate le seguenti operazioni:

* Verificate che le credenziali utente fornite siano corrette.
* Assicuratevi che l&#39;istanza AEM possa connettersi al server di Target. Ad esempio, accertatevi che le regole del firewall non blocchino le connessioni AEM in uscita o che AEM configurato per utilizzare i proxy necessari.
* Cercare messaggi utili nel registro errori AEM. Il file error.log si trova nella directory **crx-quickstart/logs** in cui è installato AEM.
* Quando modificate l&#39;attività in  Adobe Target, l&#39;URL punta a localhost. Per ovviare a questo problema, impostate l&#39;esternalizzatore AEM sull&#39;URL corretto.

