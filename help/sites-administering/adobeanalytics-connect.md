---
title: Connessione ad Adobe  Analytics e creazione di framework
seo-title: Connessione ad Adobe  Analytics e creazione di framework
description: Scoprite come collegare AEM a SiteCatalyst e creare i framework.
seo-description: Scoprite come collegare AEM a SiteCatalyst e creare i framework.
uuid: 3820dd24-4193-42ea-aef2-4669ebfeaa9d
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 6b545a51-3677-4ea1-ac7e-2d01ba19283e
docset: aem65
translation-type: tm+mt
source-git-commit: 8279cd590244a7f2d20cfaf1c7505a3ef57fae4a
workflow-type: tm+mt
source-wordcount: '1550'
ht-degree: 8%

---


# Connessione ad Adobe  Analytics e creazione di framework {#connecting-to-adobe-analytics-and-creating-frameworks}

Per tenere traccia dei dati Web dalle pagine AEM in Adobe  Analytics, crea una configurazione Adobe  Analytics Cloud Services e un framework Analytics  Adobe:

* **Configurazione Adobe  Analytics:** Informazioni sul vostro account Adobe  Analytics. La configurazione Adobe  Analytics consente ad AEM di connettersi ad Adobe  Analytics. Create una configurazione Adobe  Analytics per ciascun account utilizzato.
* **Adobe  Analytics Framework:** Un insieme di mappature tra le proprietà della suite di rapporti di Adobe  Analytics e le variabili CQ. Utilizzate un framework per configurare il modo in cui i dati del sito Web compaiano nei rapporti Adobe  Analytics. I framework sono associati a una configurazione Adobe  Analytics. Potete creare più framework per ciascuna configurazione.

Quando associate una pagina Web a un framework, il framework esegue il tracciamento di tale pagina e dei relativi discendenti. Le visualizzazioni di pagina possono quindi essere recuperate da Adobe  Analytics e visualizzate nella console Siti.

## Prerequisiti {#prerequisites}

### Adobe Analytics Account {#adobe-analytics-account}

Per tenere traccia dei dati AEM in Adobe  Analytics, è necessario disporre di un account Adobe  Analytics valido per  Adobe Marketing Cloud.

L&#39;account Adobe  Analytics deve:

* Disporre di privilegi di **amministratore**
* Da assegnare al gruppo di utenti Accesso **ai servizi** Web.

>[!CAUTION]
>
>Fornire privilegi di **amministratore** (in Adobe  Analytics) non è sufficiente per consentire agli utenti di connettersi da AEM ad Adobe  Analytics. L&#39;account deve inoltre disporre dei privilegi **Web Service Access** .

![chlimage_1-67](assets/chlimage_1-67.png)

Prima di continuare, accertatevi che le credenziali vi consentano di accedere ad Adobe  Analytics. Tramite:

* [Accesso Adobe Experience Cloud](https://login.experiencecloud.adobe.com/exc-content/login.html)

* [Adobe  Analytics Sign](https://sc.omniture.com/login/)

### Configurazione di AEM per l’utilizzo di Adobe  Analytics Data Center {#configuring-aem-to-use-your-adobe-analytics-data-centers}

I centri [](https://developer.omniture.com/en_US/content_page/concepts-terminology/c-how-is-data-stored) dati Adobe  Analytics raccolgono, elaborano e memorizzano i dati associati alla suite di rapporti Adobe  Analytics. Devi configurare AEM per utilizzare il centro dati che ospita la suite di rapporti Adobe  Analytics. Nella tabella seguente sono elencati i centri dati disponibili e il relativo URL.

| Datacenter | URL |
|---|---|
| San Jose | https://api.omniture.com/admin/1.4/rest/ |
| Dallas | https://api2.omniture.com/admin/1.4/rest/ |
| Londra | https://api3.omniture.com/admin/1.4/rest/ |
| Singapore | https://api4.omniture.com/admin/1.4/rest/ |
| Oregon | https://api5.omniture.com/admin/1.4/rest/ |

Per impostazione predefinita, AEM utilizza il centro dati di San Jose (https://api.omniture.com/admin/1.4/rest/).

Utilizzate la console [Web per configurare il bundle](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) OSGi di **Adobe AEM  Analytics HTTP Client**. Aggiungi l’URL **del centro** dati per il centro dati che ospita una suite di rapporti per la quale le pagine AEM raccolgono i dati.

![a-07](assets/aa-07.png)

1. Aprite la console Web nel browser Web. ([https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr))
1. Immettete le credenziali per accedere alla console.

   >[!NOTE]
   >
   >Contattate l’amministratore del sito per verificare se avete accesso a questa console.

1. Selezionate l’elemento Configuration denominato **Adobe AEM  Analytics HTTP Client**.
1. Per aggiungere l&#39;URL di un centro dati, premere il pulsante + accanto all&#39;elenco URL del centro **dati** e digitare l&#39;URL nella casella.

1. Per rimuovere un URL dall’elenco, fate clic sul pulsante - accanto all’URL.
1. Fate clic su Salva.

## Configuring the Connection to Adobe Analytics {#configuring-the-connection-to-adobe-analytics}

>[!CAUTION]
>
>In seguito a modifiche di sicurezza in Adobe Analytics API, non è più possibile utilizzare la versione di Activity Map inclusa in AEM.
>
>The [ActivityMap plugin provided by Adobe Analytics](https://docs.adobe.com/content/help/it/IT/analytics/analyze/activity-map/getting-started/get-started-users/activitymap-install.html) should now be used.

## Configuring for the Activity Map {#configuring-for-the-activity-map}

>[!CAUTION]
>
>In seguito a modifiche di sicurezza in Adobe Analytics API, non è più possibile utilizzare la versione di Activity Map inclusa in AEM.
>
>The [ActivityMap plugin provided by Adobe Analytics](https://docs.adobe.com/content/help/it/IT/analytics/analyze/activity-map/getting-started/get-started-users/activitymap-install.html) should now be used.

## Creazione di un Adobe  Analytics Framework {#creating-a-adobe-analytics-framework}

Per l’ID Suite di rapporti (RSID) in uso, potete controllare quali istanze del server (autore, pubblicazione o entrambe) contribuiscono ai dati della suite di rapporti:

* **Tutti**: Le informazioni provenienti sia dall’istanza di creazione che dall’istanza di pubblicazione popolano la Suite di rapporti.
* **Autore**: Solo le informazioni dell&#39;istanza di creazione popolano la suite di rapporti.
* **Pubblica**: Solo le informazioni dell&#39;istanza di pubblicazione popolano la suite di rapporti.

>[!NOTE]
>
>Selezionando il tipo di istanza del server non si limitano le chiamate ad Adobe  Analytics, si limita a controllare quali chiamate includere il RSID.
>
>Ad esempio, un framework è configurato per utilizzare la suite di rapporti *remota* e l&#39;autore è l&#39;istanza server selezionata. Quando le pagine vengono pubblicate insieme al framework, vengono effettuate chiamate ad Adobe  Analytics, ma queste chiamate non contengono il RSID. Solo le chiamate dall’istanza di creazione includono l’RSID.

1. Utilizzando **Navigazione**, seleziona **Strumenti**, Servizi **** cloud, quindi Servizi **cloud** legacy.
1. Scorrete fino ad **Adobe  Analytics** e selezionate **Mostra configurazioni**.
1. Fate clic sul collegamento **[+]** accanto alla configurazione di Adobe  Analytics.

1. Nella finestra di dialogo **Crea framework** :

   * Specificate un **titolo**.
   * Facoltativamente, potete specificare il **Nome** per il nodo che memorizza i dettagli del framework nell&#39;archivio.
   * Selezionare **Adobe  Analytics Framework**

   Fate clic su **Crea**.

   Il framework viene aperto per la modifica.

1. Nella sezione **Suite** di rapporti del contenitore laterale (lato destro del pannello principale), fate clic su **Aggiungi elemento**. Quindi utilizzate il menu a discesa per selezionare l&#39;ID della suite di rapporti (ad esempio, `geometrixxauth`) con cui interagisce il framework.

   >[!NOTE]
   >
   >Content Finder a sinistra viene popolato con variabili Adobe  Analytics (variabili SiteCatalyst) quando selezionate un ID suite di rapporti.

1. Quindi utilizzate il menu a discesa **Modalità** esecuzione (accanto all&#39;ID della suite di rapporti) per selezionare le istanze del server che desiderate inviare informazioni alla suite di rapporti.

   ![aa-framework-01](assets/aa-framework-01.png)

1. Per rendere il framework disponibile nell’istanza di pubblicazione del sito, nella scheda **Pagina** della barra laterale fate clic su **Attiva framework.**

### Configurazione delle impostazioni server per Adobe  Analytics {#configuring-server-settings-for-adobe-analytics}

Il sistema framework consente di modificare le impostazioni del server all&#39;interno di ogni framework Adobe  Analytics.

>[!CAUTION]
>
>Queste impostazioni determinano dove vengono inviati i dati e come, pertanto è fondamentale che *non vengano alterate tali impostazioni* e che il rappresentante Adobe  Analytics possa configurarle.

Per iniziare, aprite il pannello. Premere la freccia rivolta verso il basso accanto a **Server**:

![server_001](assets/server_001.png)

* **Server per tracking**

   * contiene l’URL utilizzato per inviare chiamate Adobe  Analytics

      * cname - impostazione predefinita per il nome *società dell&#39;account Adobe  Analytics*
      * d1 - corrisponde al centro dati a cui verranno inviate le informazioni (può essere d1, d2 o d3)
      * sc.omtrdc.net - nome di dominio

* **Server di tracciamento protetto**

   * Ha gli stessi segmenti del server di tracciamento
   * Viene utilizzato per l&#39;invio di dati da pagine protette (https://)

* **Namespace visitatore**

   * Lo spazio nomi determina la prima parte dell’URL di tracciamento.
   * Ad esempio, modificando lo spazio dei nomi in **CNAME** , le chiamate effettuate ad Adobe  Analytics avranno l’aspetto **CNAME.d1.omtrdc.net** invece che predefinito.

## Associazione di una pagina a un Adobe  Analytics Framework {#associating-a-page-with-a-adobe-analytics-framework}

Quando una pagina è associata a un framework Analytics  Adobe, la pagina invia dati ad Adobe  Analytics quando la pagina viene caricata. Le variabili compilate dalla pagina vengono mappate e recuperate dalle variabili Adobe  Analytics nel framework. Ad esempio, le visualizzazioni di pagina vengono recuperate da Adobe  Analytics.

I discendenti della pagina ereditano l&#39;associazione con il framework. Ad esempio, quando associate la pagina principale del sito a una struttura, tutte le pagine del sito sono associate alla struttura.

1. Dalla console **Siti** , selezionate la pagina da impostare con il tracciamento.
1. Aprite le Proprietà **[](/help/sites-authoring/editing-page-properties.md)**pagina, direttamente dalla console o dall’editor pagina.
1. Aprite la scheda** Cloud Services*.

1. Utilizzate il menu a discesa **Aggiungi configurazione** per selezionare **Adobe  Analytics** dalle opzioni disponibili. Se l&#39;ereditarietà è collocata, è necessario disattivarla prima che il selettore diventi disponibile.

1. Il selettore a discesa per **Adobe  Analytics** verrà aggiunto alle opzioni disponibili. Utilizzate questa opzione per selezionare la configurazione del framework richiesta.

1. Select **Save &amp; Close**.
1. **[Pubblicate](/help/sites-authoring/publishing-pages.md)**la pagina per attivare la pagina ed eventuali configurazioni/file connessi.
1. Il passo finale consiste nel visitare la pagina nell’istanza di pubblicazione e cercare una parola chiave (ad esempio melanzana) utilizzando il componente **Ricerca** .
1. Potete quindi controllare le chiamate effettuate ad Adobe  Analytics utilizzando uno strumento appropriato; ad esempio, [Adobe Experience Cloud Debugger](https://docs.adobe.com/content/help/en/debugger/using/experience-cloud-debugger.html).
1. Utilizzando l’esempio fornito, la chiamata deve contenere il valore immesso (ad es. melanzana) in eVar7 e l’elenco degli eventi deve contenere event3.

### Visualizzazioni pagina {#page-views}

Quando una pagina è associata a un framework Analytics  Adobe, il numero di visualizzazioni di pagina può essere visualizzato nella vista Elenco della console Siti.

Per ulteriori informazioni, consulta [Vedere pagina  dati](/help/sites-authoring/page-analytics-using.md) Analytics.

### Configurazione dell’intervallo di importazione {#configuring-the-import-interval}

Configurate l’istanza appropriata del servizio Configurazione **polling gestito di** Adobe AEM:

* **Intervallo**sondaggio:
L&#39;intervallo, in secondi, in base al quale il servizio recupera i dati di visualizzazione della pagina da Adobe  Analytics.
L’intervallo predefinito è 43200000 ms (12 ore).

* **Abilita**:
Abilitare o disabilitare il servizio. Per impostazione predefinita, il servizio è abilitato.

Per configurare questo servizio OSGi, potete utilizzare la console [](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) Web o un nodo [osgiConfig nell’archivio](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository) (il servizio PID è `com.day.cq.polling.importer.impl.ManagedPollConfigImpl`).

## Modifica di configurazioni e/o framework Adobe  Analytics {#editing-adobe-analytics-configurations-and-or-frameworks}

Come per la creazione di una configurazione o di un framework Analytics , andate alla schermata (precedente) Servizi **** cloud. Selezionate **Mostra configurazioni**, quindi fate clic sul collegamento alla configurazione specifica da aggiornare.

Quando modificate una configurazione Adobe  Analytics, per aprire la finestra di dialogo **Modifica componente** dovete anche premere il pulsante **Modifica** nella pagina di configurazione stessa.

## Eliminazione di Adobe  Analytics Framework {#deleting-adobe-analytics-frameworks}

Per eliminare un framework Adobe  Analytics, [apritelo per la modifica](#editing-adobe-analytics-configurations-and-or-frameworks).

Quindi selezionate **Elimina framework** dalla scheda **Pagina** della barra laterale.

