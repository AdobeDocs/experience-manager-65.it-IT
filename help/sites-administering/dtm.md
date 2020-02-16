---
title: Integrazione con Adobe Dynamic Tag Management
seo-title: Integrazione con Adobe Dynamic Tag Management
description: Scopri l’integrazione con Adobe Dynamic Tag Management.
seo-description: Scopri l’integrazione con Adobe Dynamic Tag Management.
uuid: cbb9f942-44e3-4cd5-b07d-4298a7a08376
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: b8c7a20a-7694-4a49-b66a-060720f17dad
translation-type: tm+mt
source-git-commit: 58fa0f05bae7ab5ba51491be3171b5c6ffbe870d

---


# Integrazione con Adobe Dynamic Tag Management {#integrating-with-adobe-dynamic-tag-management}

Integra [Adobe Dynamic Tag Management](https://www.adobe.com/solutions/digital-marketing/dynamic-tag-management.html) con AEM per poter utilizzare le proprietà Web di Gestione tag dinamica per tenere traccia dei siti AEM. Gestione tag dinamica consente ai professionisti del marketing di gestire i tag per la raccolta dei dati e la distribuzione dei dati tra i sistemi di marketing digitale. Ad esempio, utilizzate Gestione tag dinamica per raccogliere i dati di utilizzo per il sito Web AEM e distribuire i dati per l&#39;analisi in Adobe Analytics o Adobe Target.

Prima di effettuare l’integrazione, è necessario creare la proprietà [](https://microsite.omniture.com/t2/help/en_US/dtm/#Web_Properties) Web Gestione tag dinamica per tenere traccia del dominio del sito AEM. Le opzioni [di](https://microsite.omniture.com/t2/help/en_US/dtm/#Hosting__Embed_Tab) hosting della proprietà Web devono essere configurate in modo da poter configurare AEM per l&#39;accesso alle librerie Gestione tag dinamica.

Dopo aver configurato l’integrazione, le modifiche apportate agli strumenti e alle regole di distribuzione Gestione tag dinamica non richiedono la modifica della configurazione Gestione tag dinamica in AEM. Le modifiche sono automaticamente disponibili per AEM.

>[!NOTE]
>
>Se utilizzate Gestione dinamica dei tag con una configurazione proxy personalizzata, dovete configurare sia le configurazioni proxy del client HTTP che alcune funzionalità di AEM utilizzano le API 3.x, sia quelle delle API 4.x:
>
>* 3.x è configurato con [http://localhost:4502/system/console/configMgr/com.day.commons.httpclient](http://localhost:4502/system/console/configMgr/com.day.commons.httpclient)
>* 4.x è configurato con [http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)
>



## Opzioni di distribuzione {#deployment-options}

Le seguenti opzioni di distribuzione influiscono sulla configurazione dell&#39;integrazione con Gestione tag dinamica.

### Gestione tag dinamica hosting {#dynamic-tag-management-hosting}

AEM supporta la gestione tag dinamica ospitata nel cloud o ospitata su AEM.

* In hosting sul cloud: Le librerie JavaScript per la gestione tag dinamica sono memorizzate nel cloud e le pagine AEM vi fanno riferimento direttamente.
* ospitato da AEM: Gestione tag dinamica genera librerie JavaScript. AEM utilizza un modello di flusso di lavoro per ottenere e installare le librerie.

Il tipo di hosting utilizzato dall&#39;implementazione determina alcune delle attività di configurazione e implementazione che esegui. Per informazioni sulle opzioni di hosting, consultate [Hosting - Embed Tab](https://microsite.omniture.com/t2/help/en_US/dtm/#Hosting__Embed_Tab) (Hosting - Embed Tab) nella guida di Gestione tag dinamica.

### Libreria produzione e gestione temporanea {#staging-and-production-library}

Decidete se l’istanza di creazione di AEM utilizza il codice di staging o di produzione Gestione tag dinamica.

In genere l’istanza di creazione utilizza le librerie di staging Gestione tag dinamica e l’istanza di produzione utilizza le librerie di produzione. Questo scenario consente di utilizzare l’istanza di creazione per testare configurazioni di Gestione tag dinamica non approvate.

Se necessario, l’istanza di creazione può usare le librerie di produzione. Sono disponibili plug-in per browser Web che consentono di passare dall&#39;utilizzo di librerie di staging a scopo di test quando le librerie sono ospitate nel cloud.

### Utilizzo del gruppo di distribuzione Gestione tag dinamica {#using-the-dynamic-tag-management-deployment-hook}

Quando AEM ospita le librerie Gestione tag dinamica, puoi utilizzare il servizio gancio di distribuzione Gestione tag dinamica per inviare automaticamente in push gli aggiornamenti della libreria ad AEM. Gli aggiornamenti della libreria vengono inviati in push quando vengono apportate modifiche alle librerie, ad esempio quando vengono modificate le proprietà Web di Gestione tag dinamica.

Per utilizzare il gancio di distribuzione, Gestione tag dinamica deve essere in grado di connettersi all’istanza AEM che ospita le librerie. Devi [abilitare l&#39;accesso ad AEM](/help/sites-administering/dtm.md#enabling-access-for-the-deployment-hook-service) per i server Gestione tag dinamica.

In alcune circostanze AEM potrebbe non essere raggiungibile, ad esempio quando AEM si trova dietro un firewall. In questi casi, potete utilizzare l&#39;opzione Importazione polling AEM per recuperare periodicamente le librerie. Un&#39;espressione di processo cron imposta la pianificazione per i download della libreria.

## Abilitazione dell&#39;accesso al servizio del gruppo di distribuzione {#enabling-access-for-the-deployment-hook-service}

Abilita il servizio gancio di distribuzione Gestione tag dinamica per accedere ad AEM in modo che il servizio possa aggiornare le librerie ospitate da AEM. Specificate l&#39;indirizzo IP dei server Gestione tag dinamica che aggiornano le librerie di staging e produzione come richiesto:

* Staging: `107.21.99.31`
* Produzione: `23.23.225.112` e `204.236.240.48`

Perform the configuration using either the [Web Console](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) or a [`sling:OsgiConfig`](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository) node:

* Nella console Web, utilizza l’elemento di configurazione Adobe DTM Deploy Hook nella pagina Configurazione.
* Per una configurazione OSGi, il servizio PID è `com.adobe.cq.dtm.impl.servlets.DTMDeployHookServlet`.

Nella tabella seguente sono descritte le proprietà da configurare.

| Console Web, proprietà | OSGi, proprietà | Descrizione |
|---|---|---|
| Gestione dinamica dei tag - Elenco bianco IP | `dtm.staging.ip.whitelist` | Indirizzo IP del server Gestione tag dinamica che aggiorna le librerie di staging. |
| Elenco bianco IP DTM produzione | `dtm.production.ip.whitelist` | Indirizzo IP del server Gestione tag dinamica che aggiorna le librerie di produzione. |

## Creazione della configurazione Gestione tag dinamica {#creating-the-dynamic-tag-management-configuration}

Crea una configurazione cloud in modo che l’istanza AEM possa autenticarsi con Gestione tag dinamica e interagire con la tua proprietà Web.

>[!NOTE]
>
>Evitate di includere nelle pagine due codici di monitoraggio di Adobe Analytics quando la vostra proprietà Web DTM include lo strumento Adobe Analytics e utilizzate anche [Content Insight](/help/sites-authoring/content-insights.md). Nella configurazione [cloud di](/help/sites-administering/adobeanalytics-connect.md#configuring-the-connection-to-adobe-analytics)Adobe Analytics, seleziona l’opzione Non includere il codice di tracciamento.

### Impostazioni generali {#general-settings}

<table>
 <tbody>
  <tr>
   <th>Proprietà</th>
   <th>Descrizione</th>
  </tr>
  <tr>
   <td>Token API</td>
   <td>Il valore della proprietà Token API dell'account utente Gestione tag dinamica. AEM utilizza questa proprietà per l’autenticazione con Gestione tag dinamica.</td>
  </tr>
  <tr>
   <td>Azienda</td>
   <td>Società a cui è associato l’ID di accesso.</td>
  </tr>
  <tr>
   <td>Proprietà</td>
   <td>Nome della proprietà Web creata per la gestione dei tag per il sito AEM.</td>
  </tr>
  <tr>
   <td>Includi codice di produzione per Autore</td>
   <td><p>Selezionate questa opzione per fare in modo che le istanze di creazione e pubblicazione di AEM utilizzino la versione di produzione delle librerie Gestione tag dinamica. </p> <p>Se questa opzione non è selezionata, le impostazioni di gestione temporanea vengono applicate all’istanza di creazione e le impostazioni di produzione vengono applicate all’istanza di pubblicazione.</p> </td>
  </tr>
 </tbody>
</table>

### Proprietà di hosting autonomo - Produzione e allestimento {#self-hosting-properties-staging-and-production}

Le seguenti proprietà della configurazione Gestione tag dinamica consentono ad AEM di ospitare le librerie Gestione tag dinamica. Le proprietà consentono ad AEM di scaricare e installare le librerie. Facoltativamente, puoi aggiornare automaticamente le librerie per assicurarti che riflettano eventuali modifiche apportate nell’applicazione Gestione tag dinamica.

Alcune proprietà utilizzano i valori ottenuti dalla sezione Download libreria della scheda Incorpora per la proprietà Web Gestione tag dinamica. Per ulteriori informazioni, consulta Download [della](https://microsite.omniture.com/t2/help/en_US/dtm/#Library_Download) libreria nella guida di Gestione tag dinamica.

>[!NOTE]
>
>Quando ospitate il bundle Gestione tag dinamica in AEM, prima di creare la configurazione è necessario abilitare il download della libreria in Gestione tag dinamica. Inoltre, Akamai deve essere abilitato perché Akamai fornisce le librerie per il download.

Quando ospita le librerie Gestione tag dinamica in AEM, AEM configura automaticamente alcune proprietà della proprietà Web in base alla configurazione in uso. Vedere le descrizioni nella tabella seguente.

<table>
 <tbody>
  <tr>
   <th>Proprietà</th>
   <th>Descrizione</th>
  </tr>
  <tr>
   <td>Usa hosting autonomo</td>
   <td>Selezionate quando ospitate il file libreria Gestione tag dinamica in AEM. Selezionando questa opzione vengono visualizzate le altre proprietà della tabella.</td>
  </tr>
  <tr>
   <td>URL bundle DTM</td>
   <td>URL da utilizzare per scaricare la libreria Gestione tag dinamica. Ottenete questo valore dalla sezione Download URL della pagina Download libreria di Gestione tag dinamica. Per motivi di sicurezza, questo valore deve essere configurato manualmente.</td>
  </tr>
  <tr>
   <td>Flusso di lavoro per download</td>
   <td><p>Modello di flusso di lavoro da utilizzare per scaricare e installare la libreria Gestione tag dinamica. Il modello predefinito è Download DTM Bundle predefinito. Utilizzare questo modello a meno che non sia stato creato un modello personalizzato.</p> <p>Il flusso di lavoro predefinito per il download attiva automaticamente le librerie al momento del download.</p> </td>
  </tr>
  <tr>
   <td>Suggerimento dominio</td>
   <td><p>(Facoltativo) Il dominio del server AEM che ospita la libreria Gestione tag dinamica. Specificate un valore per ignorare il dominio predefinito configurato per il servizio <a href="/help/sites-developing/externalizer.md">Esternalizzatore collegamento CQ</a>Day.</p> <p>Quando è connesso a Gestione tag dinamica, AEM utilizza questo valore per configurare il Percorso HTTP temporaneo o il Percorso HTTP di produzione delle proprietà Download della libreria per la proprietà Web Gestione tag dinamica.</p> </td>
  </tr>
  <tr>
   <td>Suggerimento dominio sicuro</td>
   <td><p>(Facoltativo) Il dominio del server AEM che ospita la libreria Gestione tag dinamica tramite HTTPS. Specificate un valore per ignorare il dominio predefinito configurato per il servizio <a href="/help/sites-developing/externalizer.md">Esternalizzatore collegamento CQ</a>Day.</p> <p>Quando è connesso a Gestione tag dinamica, AEM utilizza questo valore per configurare il percorso HTTPS di gestione dei tag dinamici o il percorso HTTPS di produzione delle proprietà Download della libreria per la proprietà Web Gestione tag dinamica.</p> </td>
  </tr>
  <tr>
   <td>Segreto condiviso</td>
   <td><p>(Facoltativo) Il segreto condiviso da utilizzare per decrittografare il download. Ottenete questo valore dal campo Segreto condiviso della pagina Download della libreria di Gestione tag dinamica.</p> <p><strong></strong> Nota: Nel computer in cui è installato AEM devono essere installate le librerie <a href="https://www.openssl.org/docs/apps/openssl.html">OpenSSL</a> , in modo che AEM possa decrittografare le librerie scaricate.</p> </td>
  </tr>
  <tr>
   <td>Abilita importazione polling</td>
   <td><p>(Facoltativo) Selezionare questa opzione per scaricare e installare periodicamente la libreria Gestione tag dinamica per verificare di utilizzare una versione aggiornata. Se selezionata, Gestione tag dinamica non invia richieste HTTP POST all’URL del gruppo di distribuzione.</p> <p>AEM configura automaticamente la proprietà Deploy Hook URL delle proprietà Library Download per la proprietà Web Gestione tag dinamica. Quando è selezionata, la proprietà è configurata senza alcun valore. Se non è selezionata, la proprietà viene configurata con l'URL della configurazione Gestione tag dinamica.</p> <p>Abilita Polling Importer quando l’hook di distribuzione Gestione tag dinamica non è in grado di connettersi ad AEM, ad esempio quando AEM si trova dietro un firewall.</p> </td>
  </tr>
  <tr>
   <td>Espressione di pianificazione</td>
   <td>(Viene visualizzato ed è richiesto se è selezionata l’opzione Abilita Importazione polling). Espressione cron che controlla quando vengono scaricate le librerie di gestione tag dinamica.</td>
  </tr>
 </tbody>
</table>

![chlimage_1-352](assets/chlimage_1-352.png)

### Proprietà hosting cloud - Produzione e gestione temporanea {#cloud-hosting-properties-staging-and-production}

Quando la configurazione della gestione tag dinamica è in hosting sul cloud, puoi configurare le seguenti proprietà.

<table>
 <tbody>
  <tr>
   <th>Proprietà</th>
   <th>Descrizione</th>
  </tr>
  <tr>
   <td>Usa hosting autonomo</td>
   <td>Deselezionate questa opzione quando il file di libreria Gestione tag dinamica è in hosting nel cloud.</td>
  </tr>
  <tr>
   <td>Codice intestazione</td>
   <td><p>Il codice dell'intestazione per l'area di gestione dei tag dinamici ottenuto da Gestione tag dinamica per l'host. Questo valore viene popolato automaticamente quando ci si connette a Gestione tag dinamica.</p> <p> Per visualizzare il codice in Gestione tag dinamica, fai clic sulla scheda Incorpora, quindi sul nome host. Espandete la sezione del codice di intestazione e fate clic su Copia codice da incorporare del codice di incorporamento temporaneo o, se necessario, sull'area del codice da incorporare produzione.</p> </td>
  </tr>
  <tr>
   <td>Codice piè di pagina</td>
   <td><p>Il codice piè di pagina per l'area di gestione dei tag dinamici ottenuto da Gestione tag dinamica per l'host. Questo valore viene popolato automaticamente quando ci si connette a Gestione tag dinamica.</p> <p>Per visualizzare il codice in Gestione tag dinamica, fai clic sulla scheda Incorpora, quindi sul nome host. Espandete la sezione Codici piè di pagina e fate clic su Copia codice da incorporare del codice di incorporamento temporaneo o sull’area Codice da incorporare produzione, a seconda delle necessità.</p> </td>
  </tr>
 </tbody>
</table>

![chlimage_1-353](assets/chlimage_1-353.png)

La procedura seguente utilizza l’interfaccia touch per configurare l’integrazione con Gestione tag dinamica.

1. Nella barra laterale fate clic su Strumenti > Operazioni > Cloud > Servizi cloud.
1. Nell’area Gestione tag dinamica viene visualizzato uno dei seguenti collegamenti per aggiungere una configurazione:

   * Fate clic su Configura ora se si tratta della prima configurazione che state aggiungendo.
   * Fate clic su Show Configurations (Mostra configurazioni), quindi fate clic sul collegamento + accanto a Available Configurations (Configurazioni disponibili) se sono state create una o più configurazioni.
   ![chlimage_1-354](assets/chlimage_1-354.png)

1. Digitate un titolo per la configurazione e fate clic su Crea.
1. Nel campo Token API, immettete il valore della proprietà Token API dell&#39;account utente Gestione tag dinamica.

   Per ottenere il valore del token API, contatta l&#39;assistenza clienti DTM.

   >[!NOTE]
   >
   >Il token API scade solo se l&#39;utente di Gestione tag dinamica lo richiede esplicitamente.

   ![chlimage_1-355](assets/chlimage_1-355.png)

1. Fate clic su Connetti a Gestione dinamica dei tag. AEM esegue l’autenticazione con Gestione tag dinamica e recupera l’elenco delle società a cui è associato l’account.
1. Selezionate la Società, quindi selezionate la Proprietà che state utilizzando per tenere traccia del sito AEM.
1. Se utilizzate il codice di staging nell’istanza di creazione, deselezionate Includi codice produzione sull’autore.
1. Immettete i valori per le proprietà nelle schede Impostazioni di gestione temporanea e Impostazioni produzione, se necessario, quindi fate clic su OK.

## Download manuale della libreria Gestione tag dinamica {#manually-downloading-the-dynamic-tag-management-library}

Scarica manualmente le librerie Gestione tag dinamica per aggiornarle immediatamente su AEM. Ad esempio, scaricate manualmente quando desiderate testare una libreria aggiornata prima che venga pianificato il download automatico della libreria da parte di Importazione polling.

1. Nella barra laterale fate clic su Strumenti > Operazioni > Cloud > Servizi cloud.
1. Nell&#39;area Gestione tag dinamica, fai clic su Mostra configurazioni, quindi fai clic sulla configurazione.
1. Nell&#39;area Impostazioni di gestione temporanea o Impostazioni di produzione, fate clic sul pulsante Attiva flusso di lavoro per scaricare e distribuire il bundle della libreria.

   ![chlimage_1-356](assets/chlimage_1-356.png)

>[!NOTE]
>
>I file scaricati sono memorizzati in `/etc/clientlibs/dtm/my config/companyID/propertyID/servertype`.
>
>I seguenti elementi sono tratti direttamente dalla configurazione [](#creating-the-dynamic-tag-management-configuration)DTM.
>
>* `myconfig`
>* `companyID`
>* `propertyID`
>* `servertype`
>



## Associazione di una configurazione Gestione tag dinamica al sito {#associating-a-dynamic-tag-management-configuration-with-your-site}

Associate la configurazione Gestione tag dinamica alle pagine del sito Web in modo che AEM aggiunga lo script richiesto alle pagine. Associate la pagina principale del sito alla configurazione. Tutti i discendenti di tale pagina ereditano l&#39;associazione. Se necessario, è possibile ignorare l&#39;associazione in una pagina discendente.

Utilizzate la procedura seguente per associare una pagina e i discendenti a una configurazione Gestione tag dinamica.

1. Aprite la pagina principale del sito nell’interfaccia classica.
1. Utilizzare la barra laterale per aprire le proprietà della pagina.
1. Nella scheda Servizi cloud, fai clic su Aggiungi servizio, seleziona Gestione tag dinamica, quindi fai clic su OK.

   ![chlimage_1-357](assets/chlimage_1-357.png)

1. Utilizzate il menu a discesa Gestione tag dinamica per selezionare la configurazione, quindi fate clic su OK.

Per ignorare l’associazione di configurazione ereditata per una pagina, attenersi alla procedura descritta di seguito. L’override influisce sulla pagina e su tutti i discendenti della pagina.

1. Aprite la pagina nell’interfaccia classica.
1. Utilizzare la barra laterale per aprire le proprietà della pagina.
1. Nella scheda Servizi cloud, fai clic sull&#39;icona a forma di lucchetto accanto alla proprietà Ereditato da, quindi fai clic su Sì nella finestra di dialogo di conferma.

   ![chlimage_1-358](assets/chlimage_1-358.png)

1. Rimuovere o selezionare una configurazione di gestione tag dinamica diversa, quindi fare clic su OK.

