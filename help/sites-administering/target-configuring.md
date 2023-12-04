---
title: Configurazione manuale dell’integrazione con Adobe Target
seo-title: Manually Configuring the Integration with Adobe Target
description: Scopri come configurare manualmente l’integrazione con Adobe Target.
seo-description: Learn how to manually configure the integration with Adobe Target.
uuid: 0bb76a65-f981-4cc5-bee8-5feb3297137c
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 20c8eb1d-5847-4902-b7d3-4c3286423b46
exl-id: 0f710685-dc4f-4333-9847-d002b2637d08
source-git-commit: 10b370fd8f855f71c6d7d791c272137bb5e04d97
workflow-type: tm+mt
source-wordcount: '2122'
ht-degree: 28%

---

# Configurazione manuale dell’integrazione con Adobe Target {#manually-configuring-the-integration-with-adobe-target}

Puoi modificare le configurazioni della procedura guidata di consenso effettuate durante l’utilizzo della procedura guidata, oppure integrarle manualmente con Adobe Target senza utilizzare la procedura guidata.

## Modifica delle configurazioni della procedura guidata Opt-in {#modifying-the-opt-in-wizard-configurations}

Il [Procedura guidata Opt-in](/help/sites-administering/opt-in.md) che [integra AEM con Adobe Target](/help/sites-administering/target.md) crea automaticamente una configurazione cloud di Target denominata Configurazione di Target con provisioning. La procedura guidata crea anche un framework Target per la configurazione cloud denominato Provisioned Target Framework. Se necessario, puoi modificare le proprietà della configurazione e del framework cloud.

Puoi anche configurare Adobe Target per utilizzare Adobe Target come origine per la generazione di rapporti quando esegui il targeting del contenuto configurando la configurazione di A4T Analytics Cloud.

Per individuare la configurazione cloud e il framework, vai a **Cloud Service** tramite **Strumenti** > **Distribuzione** > **Cloud**. ([http://localhost:4502/libs/cq/core/content/tools/cloudservices.html](http://localhost:4502/libs/cq/core/content/tools/cloudservices.html)) Sotto Adobe Target, fai clic su **Mostra configurazioni**.

### Proprietà configurazione destinazione predisposta {#provisioned-target-configuration-properties}

I seguenti valori delle proprietà vengono utilizzati nella configurazione cloud Provisioned Target Configuration creata dalla procedura guidata Opt-in:

* **Codice client:** Come immesso nella procedura guidata Opt-in.
* **E-mail:** Come immesso nella procedura guidata Opt-in.
* **Password:** Come immesso nella procedura guidata Opt-in.
* **Tipo API:** REST
* **Sincronizzare I Segmenti Da Adobe Target:** Selezionato.

* **Libreria client:** mbox.js.
* **Utilizza DTM per distribuire la libreria client:** Non selezionato. Seleziona questa opzione se [utilizzare DTM](/help/sites-administering/dtm.md) o un altro sistema di gestione dei tag per ospitare il file mbox.js o AT.js. L’Adobe consiglia di utilizzare DTM anziché AEM per distribuire la libreria.

* **Mbox.js personalizzato:** Nessuno specificato per utilizzare il file mbox.js predefinito. Specifica un file mbox.js personalizzato da utilizzare, se necessario. Viene visualizzato solo se hai selezionato mbox.js.
* **AT.js personalizzato:** Nessuno è stato specificato in modo che venga utilizzato il file AT.js predefinito. Specifica un file AT.js personalizzato da utilizzare, in base alle esigenze. Viene visualizzato solo se avete selezionato AT.js.

>[!NOTE]
>
>In AEM 6.3, puoi selezionare il file della libreria di Target, [AT.JS](https://developer.adobe.com/target/implement/client-side/atjs/atjs-functions/mboxcreate-atjs/): nuova libreria di implementazione di Adobe Target, progettata sia per le tipiche implementazioni web che per le applicazioni a pagina singola.
>
>AT.js offre diversi miglioramenti rispetto alla libreria mbox.js:
>
>* Tempi di caricamento delle pagine migliorati per le implementazioni web
>* Maggiore sicurezza
>* Migliori opzioni di implementazione per le applicazioni a pagina singola
>* AT.js contiene i componenti inclusi in target.js, quindi cessano le chiamate a target.

<!-- OLD URL WHICH IS 404 https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/mbox-implement/mbox-download.html -->

### Proprietà framework destinazione con provisioning {#provisioned-target-framework-properties}

Il framework di destinazione predisposto creato dalla procedura guidata Opt-in è configurato per l&#39;invio di dati contestuali dall&#39;archivio dati profilo. Per impostazione predefinita, l’età e il genere dei dati dell’archivio vengono inviati a Target. È probabile che la soluzione richieda l’invio di parametri aggiuntivi.

![Framework di destinazione con provisioning](assets/chlimage_1-158.png)

È possibile configurare il framework per inviare informazioni di contesto aggiuntive a Target come descritto in [Aggiunta di un framework Target](/help/sites-administering/target-configuring.md#adding-a-target-framework).

### Configurazione della configurazione di A4T Analytics Cloud {#configuring-a-t-analytics-cloud-configuration}

Puoi configurare Adobe Target per l’utilizzo di Adobe Analytics come origine per la generazione di rapporti durante il targeting del contenuto.

>[!NOTE]
>
>L’autenticazione credenziali utente (legacy) non funziona con A4T (sia per Target che per Analytics). Pertanto, i clienti devono utilizzare l’autenticazione IMS invece dell’autenticazione con credenziali utente.

A questo scopo, specifica la configurazione cloud A4T con cui collegare la configurazione cloud di Adobe Target:

1. Accedi a **Cloud Service** tramite **Logo AEM** > **Strumenti** > **Distribuzione** > **Cloud Service**.
1. Nella sezione **Adobe Target**, fai clic su **Configura ora**.
1. Riconnetti alla configurazione di Adobe Target.
1. In **Configurazione di A4T Analytics Cloud** dal menu a discesa, seleziona il framework.

   >[!NOTE]
   >
   >Sono disponibili solo le configurazioni di Analytics abilitate per A4T.
   >
   >Durante la configurazione di A4T con AEM, è possibile che in un riferimento alla configurazione manchi una voce. Per selezionare il framework di analisi, effettua le seguenti operazioni:
   >
   >1. Accedi a **Strumenti** > **Generale** > **CRXDE Liti**.
   1. Accedi a [Finestra di dialogo Configurazione di A4T Analytics](#a4t-analytics-config-dialog) (vedi sotto)
   1. Impostare la proprietà **disable** a **false**.
   1. Clic **Salva tutto**.

#### Finestra di dialogo Configurazione di A4T Analytics {#a4t-analytics-config-dialog}

```xml
/libs/cq/analytics/components/testandtargetpage/dialog/items/tabs/items/tab1_general/items/a4tAnalyticsConfig
```

![AdobeTargetSettings](assets/adobe-target-settings.jpg)

Clic **OK**. Quando esegui il targeting dei contenuti con Adobe Target, puoi [seleziona l’origine del rapporto](/help/sites-authoring/content-targeting-touch.md).

## Integrazione manuale con Adobe Target {#manually-integrating-with-adobe-target}

Integrazione manuale con Adobe Target invece di utilizzare la procedura guidata di consenso.

>[!NOTE]
>
Il file della libreria di Target, [AT.JS](https://developer.adobe.com/target/implement/client-side/atjs/atjs-functions/mboxcreate-atjs/), è una nuova libreria di implementazione per Adobe Target progettata sia per le tipiche implementazioni web che per le applicazioni a pagina singola. Adobe consiglia di utilizzare AT.js invece di mbox.js come libreria client.
>
AT.js offre diversi miglioramenti rispetto alla libreria mbox.js:
>
* Tempi di caricamento delle pagine migliorati per le implementazioni web
* Maggiore sicurezza
* Migliori opzioni di implementazione per le applicazioni a pagina singola
* AT.js contiene i componenti inclusi in target.js, quindi non effettua più chiamate a target.js
>
Puoi selezionare AT.js o mbox.js nel menu a discesa **Libreria client**.

<!-- OLD URL from above was 404 https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/mbox-implement/mbox-download.html -->

### Creazione di una configurazione cloud di Target {#creating-a-target-cloud-configuration}

Per consentire ad AEM di interagire con Adobe Target, crea una configurazione cloud di Target. Per creare la configurazione, fornisci il codice client Adobe Target e le credenziali utente.

Puoi creare la configurazione cloud di Target una sola volta perché tale configurazione può essere associata a più campagne AEM. Se disponi di diversi codici client Adobe Target, crea una configurazione per ogni codice client.

Puoi impostare la configurazione cloud in modo da sincronizzare i segmenti da Adobe Target. Se abiliti la sincronizzazione, i segmenti vengono importati da Target in background al momento del salvataggio della configurazione cloud.

Segui la procedura seguente per creare una configurazione cloud di Target in AEM:

1. Accedi a **Cloud Service** tramite **Logo AEM** > **Strumenti** > **Cloud Service** > **Cloud Service legacy**. ([http://localhost:4502/libs/cq/core/content/tools/cloudservices.html](http://localhost:4502/libs/cq/core/content/tools/cloudservices.html))

   Il **Cloud Service** viene visualizzata la pagina della panoramica.

1. Nella sezione **Adobe Target**, fai clic su **Configura ora**.
1. Nella finestra di dialogo **Crea configurazione**:

   1. Assegna alla configurazione un **Titolo**.
   1. Seleziona il modello **Configurazione Adobe Target**.
   1. Fai clic su **Crea**.

   Viene visualizzata la finestra di dialogo di modifica.

   ![AdobeTargetSettings](assets/adobe-target-settings.jpg)

   >[!NOTE]
   >
   Durante la configurazione di A4T con AEM, è possibile che in un riferimento alla configurazione manchi una voce. Per selezionare il framework di analisi, effettua le seguenti operazioni:
   >
   1. Accedi a **Strumenti** > **Generale** > **CRXDE Liti**.
   1. Accedi a **/libs/cq/analytics/components/testandtargetpage/dialog/items/tabs/items/tab1_general/items/a4tAnalyticsConfig**
   1. Impostare la proprietà **disable** a **false**.
   1. Clic **Salva tutto**.

1. Nella finestra di dialogo, specifica i valori per queste proprietà.

   * **Codice client**: il codice client dell’account di Target
   * **E-mail**: l’e-mail dell’account Target.
   * **Password**: password dell’account Target.
   * **Tipo di API**: REST o XML
   * **Configurazione di A4T Analytics Cloud**: seleziona la configurazione di Analytics Cloud utilizzata per gli obiettivi e le metriche delle attività di destinazione. È necessaria questa configurazione se utilizzi Adobe Analytics come origine per la generazione di rapporti durante il targeting del contenuto. Se non vedi la configurazione cloud, vedi la nota in [Configurazione della configurazione di A4T Analytics Cloud](#configuring-a-t-analytics-cloud-configuration).

   * **Utilizza targeting accurato:** per impostazione predefinita questa casella di controllo è selezionata. Se viene selezionata, la configurazione del servizio cloud attende il caricamento del contesto prima di caricare il contenuto. Vedi la nota che segue.
   * **Sincronizzare i segmenti da Adobe Target:** Seleziona questa opzione per scaricare i segmenti definiti in Target e utilizzarli in AEM. Seleziona questa opzione quando la proprietà Tipo API è REST, perché i segmenti in linea non sono supportati e devi utilizzare i segmenti da Target. Il termine AEM &quot;segmento&quot; equivale al termine Target &quot;pubblico&quot;.
   * **Libreria client:** Seleziona se desideri la libreria client mbox.js o AT.js.
   * **Utilizza DTM per distribuire la libreria client** : seleziona questa opzione per utilizzare AT.js o mbox.js da DTM o un altro sistema di gestione dei tag. Configura [l’integrazione di DTM](/help/sites-administering/dtm.md) per utilizzare questa opzione. L’Adobe consiglia di utilizzare DTM anziché AEM per distribuire la libreria.
   * **mbox.js personalizzato**: lascia vuoto se hai selezionato la casella DTM o per utilizzare il valore predefinito mbox.js. In alternativa, puoi caricare il file mbox.js personalizzato. Viene visualizzato solo se hai selezionato mbox.js.
   * **AT.js personalizzato**: lascia vuoto se hai selezionato la casella DTM o per utilizzare il valore predefinito di AT.js. In alternativa, carica il tuo file AT.js personalizzato. Viene visualizzato solo se avete selezionato AT.js.

   >[!NOTE]
   >
   Per impostazione predefinita, quando scegli di accedere alla procedura guidata di configurazione di Adobe Target, il targeting accurato è abilitato.
   >
   Il targeting accurato significa che la configurazione del servizio cloud attende il caricamento del contesto prima di caricare il contenuto. Di conseguenza, in termini di prestazioni, un targeting accurato può creare un ritardo di alcuni millisecondi prima del caricamento del contenuto.
   >
   Il targeting accurato è sempre abilitato nell’istanza di authoring. Tuttavia, nell’istanza di pubblicazione puoi scegliere di disattivare il targeting accurato a livello globale cancellando il segno di spunta accanto a Targeting accurato nella configurazione del servizio cloud (**http://localhost:4502/etc/cloudservices.html**). Puoi inoltre attivare e disattivare il targeting accurato per i singoli componenti indipendentemente dall’impostazione nella configurazione del servizio cloud.
   >
   Se hai ***già*** creato i componenti di destinazione e modificato questa impostazione, le modifiche non influiscono su tali componenti. Modifica direttamente tali componenti.

1. Clic **Connetti a Target** per inizializzare la connessione con Target. Se la connessione ha esito positivo, viene visualizzato il messaggio **Connessione riuscita**. Fai clic su **OK** sul messaggio e quindi **OK** nella finestra di dialogo.

   Se non riesci a connetterti a Target, consulta la sezione [risoluzione problemi](/help/sites-administering/target-configuring.md#troubleshooting-target-connection-problems).

### Aggiunta di un framework Target {#adding-a-target-framework}

Dopo aver impostato la configurazione cloud di Target, aggiungi un framework di Target. Il framework identifica i parametri predefiniti inviati ad Adobe Target dal [ClientContext](/help/sites-administering/client-context.md) o [ContextHub](/help/sites-developing/ch-configuring.md) componenti. Target utilizza i parametri per determinare i segmenti che si applicano al contesto corrente.

Puoi creare più framework per una singola configurazione di Target. I framework multipli sono utili quando devi inviare un diverso set di parametri a Target per diverse sezioni del sito web. Crea un framework per ogni set di parametri inviato. Associa ogni sezione del sito Web al framework appropriato. Una pagina web può utilizzare un solo framework alla volta.

1. Nella pagina di configurazione di Target, fai clic su **+** (segno più) accanto a Framework disponibili.
1. Nella finestra di dialogo Crea framework, specifica un **Titolo**, seleziona **Framework Adobe Target** e fai clic su **Crea**.

   ![Finestra di dialogo Crea framework](assets/chlimage_1-161.png)

   Viene visualizzata la pagina framework. Il Sidekick fornisce componenti che rappresentano informazioni provenienti [ClientContext](/help/sites-administering/client-context.md) o [ContextHub](/help/sites-developing/ch-configuring.md) che puoi mappare.

   ![Componenti per framework](assets/chlimage_1-162.png)

1. Trascina il componente ClientContext che rappresenta i dati da utilizzare per la mappatura sulla destinazione di rilascio. In alternativa, trascina **Store ContextHub** componente del framework.

   >[!NOTE]
   >
   Durante la mappatura, i parametri vengono passati a una mbox tramite stringhe semplici. Non è possibile mappare array da ContextHub.

   Ad esempio, per utilizzare **Dati profilo** sui visitatori del tuo sito per controllare la campagna di Target, trascina **Dati profilo** alla pagina. Vengono visualizzate le variabili dei dati di profilo disponibili per la mappatura per i parametri di Adobe Target.

   ![Dati profilo](assets/chlimage_1-163.png)

1. Seleziona le variabili da rendere visibili al sistema Adobe Target selezionando la casella di selezione **Condividi** nelle colonne appropriate.

   ![Condividi](assets/chlimage_1-164.png)

   >[!NOTE]
   >
   La sincronizzazione dei parametri è solo unidirezionale, cioè da AEM ad Adobe Target.

Il framework viene creato. Per replicare il framework nell’istanza di pubblicazione, utilizza l’opzione **Attiva framework** dalla barra laterale.

### Associazione di attività alla configurazione cloud di Target  {#associating-activities-with-the-target-cloud-configuration}

Associa [Attività dell’AEM](/help/sites-authoring/activitylib.md) con la configurazione cloud di Target in modo da poter eseguire il mirroring delle attività in [Adobe Target](https://experienceleague.adobe.com/docs/target/using/experiences/offers/manage-content.html).

>[!NOTE]
>
Il tipo di attività disponibile viene stabilito in base ai seguenti elementi:
>
>
* Se il **xt_only** L’opzione è abilitata sul tenant di Adobe Target (clientcode) utilizzato sul lato AEM per connettersi ad Adobe Target, quindi puoi creare **solo** Attività XT nel AEM.
>
* Se il **xt_only** l&#39;opzione è **non** sul tenant di Adobe Target (clientcode), è possibile creare **entrambi** Attività XT e A/B nell’AEM.
>
**Nota aggiuntiva:** **xt_only** L’opzione è un’impostazione applicata a un determinato tenant Target (clientcode) e può essere modificata solo direttamente in Adobe Target. Non puoi attivare o disattivare questa opzione da AEM.

### Associazione del framework di Target al sito {#associating-the-target-framework-with-your-site}

Dopo aver creato un framework di Target in AEM, associa le pagine web al framework. I componenti di destinazione nelle pagine inviano i dati definiti dal framework ad Adobe Target per il tracciamento. (vedere [Targeting dei contenuti](/help/sites-authoring/content-targeting-touch.md).)

Quando si associa una pagina al framework, le pagine figlie ereditano l&#39;associazione.

1. In **Sites** , passare al sito da configurare.
1. Utilizzando [azioni rapide](/help/sites-authoring/basic-handling.md#quick-actions) o [modalità di selezione](/help/sites-authoring/basic-handling.md), seleziona **Visualizza proprietà.**
1. Seleziona la scheda **Servizi cloud**.
1. Clic **Modifica**.
1. Clic **Aggiungi configurazione** in **Configurazioni Cloud Service** e seleziona **Adobe Target**.

   ![Aggiungi configurazione](assets/chlimage_1-165.png)

1. Selezionare il framework desiderato in **Riferimento configurazione**.

   >[!NOTE]
   >
   Accertati di selezionare il **framework** che hai creato e non la configurazione cloud di Target in cui è stato creato.

1. Clic **Fine**.
1. Attiva la pagina root del sito web in modo da replicarlo sul server di pubblicazione. (vedere [Come Pubblicare Le Pagine](/help/sites-authoring/publishing-pages.md).)

   >[!NOTE]
   >
   Se il framework allegato alla pagina non è ancora stato attivato, viene visualizzata una procedura guidata che consente di pubblicarlo.

## Risoluzione dei problemi di connessione a Target {#troubleshooting-target-connection-problems}

Per risolvere i problemi che si verificano durante la connessione a Target, puoi eseguire le seguenti attività:

* Verifica che le credenziali utente fornite siano corrette.
* Assicurati che l’istanza AEM possa connettersi al server Target. Ad esempio, assicurati che le regole del firewall non blocchino le connessioni AEM in uscita o che l’AEM sia configurato per l’utilizzo dei proxy necessari.
* Cerca messaggi utili nel registro degli errori AEM. Il file error.log si trova in **crx-quickstart/logs** directory in cui è installato AEM.
* Quando modifichi l’attività in Adobe Target, l’URL punta a localhost. Per ovviare a questo problema, imposta AEM Externalizer sull’URL corretto.
