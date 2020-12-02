---
title: Connessione a  Adobe Analytics e creazione di framework
seo-title: Connessione a  Adobe Analytics e creazione di framework
description: Scopri come collegare AEM al SiteCatalyst e creare framework.
seo-description: Scopri come collegare AEM al SiteCatalyst e creare framework.
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


# Connessione a  Adobe Analytics e creazione di framework {#connecting-to-adobe-analytics-and-creating-frameworks}

Per tenere traccia dei dati Web dalle pagine AEM in  Adobe Analytics, crea una configurazione Adobe Analytics Cloud Services e un framework Adobe Analytics :

* **Configurazione Adobe Analytics:** le informazioni sul vostro account  Adobe Analytics. La  configurazione Adobe Analytics consente AEM connettersi  Adobe Analytics. Create una configurazione Adobe Analytics  per ciascun account utilizzato.
* **Adobe Analytics Framework:** un insieme di mappature tra  proprietà della suite di rapporti Adobe Analytics e le variabili CQ. Utilizzate un framework per configurare il modo in cui i dati del sito Web popolano i rapporti Adobe Analytics . I framework sono associati a una configurazione Adobe Analytics . Potete creare più framework per ciascuna configurazione.

Quando associate una pagina Web a un framework, il framework esegue il tracciamento di tale pagina e dei relativi discendenti. Le visualizzazioni di pagina possono quindi essere recuperate da  Adobe Analytics e visualizzate nella console Siti.

## Prerequisiti {#prerequisites}

###  account Adobe Analytics {#adobe-analytics-account}

Per tenere traccia AEM dati in  Adobe Analytics, è necessario disporre di un account Adobe Marketing Cloud  Adobe Analytics valido.

L&#39;account Adobe Analytics  deve:

* Disponete dei privilegi di **Amministratore**
* Da assegnare al gruppo di utenti **Accesso ai servizi Web**.

>[!CAUTION]
>
>Fornire privilegi **Amministratore** (all&#39;interno  Adobe Analytics) non è sufficiente per consentire all&#39;utente di connettersi da AEM a  Adobe Analytics. L&#39;account deve inoltre disporre dei privilegi **Accesso al servizio Web**.

![chlimage_1-67](assets/chlimage_1-67.png)

Prima di procedere, accertatevi che le credenziali vi consentano di accedere a  Adobe Analytics. Tramite:

* [Accesso Adobe Experience Cloud](https://login.experiencecloud.adobe.com/exc-content/login.html)

* [ accesso Adobe Analytics](https://sc.omniture.com/login/)

### Configurazione di AEM per utilizzare i centri dati Adobe Analytics  {#configuring-aem-to-use-your-adobe-analytics-data-centers}

 Adobe Analytics [data center](https://developer.omniture.com/en_US/content_page/concepts-terminology/c-how-is-data-stored) raccogliere, elaborare e archiviare i dati associati alla suite di rapporti Adobe Analytics . Devi configurare AEM per utilizzare il centro dati che ospita la tua suite di rapporti Adobe Analytics . Nella tabella seguente sono elencati i centri dati disponibili e il relativo URL.

| Datacenter | URL |
|---|---|
| San Jose | https://api.omniture.com/admin/1.4/rest/ |
| Dallas | https://api2.omniture.com/admin/1.4/rest/ |
| Londra | https://api3.omniture.com/admin/1.4/rest/ |
| Singapore | https://api4.omniture.com/admin/1.4/rest/ |
| Oregon | https://api5.omniture.com/admin/1.4/rest/ |

AEM utilizza il centro dati San Jose (https://api.omniture.com/admin/1.4/rest/) per impostazione predefinita.

Utilizzate la [console Web per configurare il bundle OSGi](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) **Adobe AEM client HTTP Analytics**. Aggiungete l&#39; **URL del centro dati** per il centro dati che ospita una suite di rapporti per la quale le pagine AEM raccolgono i dati.

![a-07](assets/aa-07.png)

1. Aprite la console Web nel browser Web. ([https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr))
1. Immettete le credenziali per accedere alla console.

   >[!NOTE]
   >
   >Contattate l’amministratore del sito per verificare se avete accesso a questa console.

1. Selezionare l&#39;elemento Configuration denominato **Adobe AEM client HTTP Analytics**.
1. Per aggiungere l&#39;URL di un centro dati, premere il pulsante + accanto all&#39;elenco **URL del centro dati** e digitare l&#39;URL nella casella.

1. Per rimuovere un URL dall’elenco, fate clic sul pulsante - accanto all’URL.
1. Fate clic su Salva.

## Configurazione della connessione per  Adobe Analytics {#configuring-the-connection-to-adobe-analytics}

>[!CAUTION]
>
>In seguito a modifiche di sicurezza in Adobe Analytics API, non è più possibile utilizzare la versione di Activity Map inclusa in AEM.
>
>È ora necessario utilizzare il plug-in [ActivityMap fornito da  Adobe Analytics](https://docs.adobe.com/content/help/it/IT/analytics/analyze/activity-map/getting-started/get-started-users/activitymap-install.html).

## Configurazione per il Activity Map  {#configuring-for-the-activity-map}

>[!CAUTION]
>
>In seguito a modifiche di sicurezza in Adobe Analytics API, non è più possibile utilizzare la versione di Activity Map inclusa in AEM.
>
>È ora necessario utilizzare il plug-in [ActivityMap fornito da  Adobe Analytics](https://docs.adobe.com/content/help/en/analytics/analyze/activity-map/getting-started/get-started-users/activitymap-install.html).

## Creazione di un  Adobe Analytics Framework {#creating-a-adobe-analytics-framework}

Per l’ID Suite di rapporti (RSID) in uso, potete controllare quali istanze del server (autore, pubblicazione o entrambe) contribuiscono ai dati della suite di rapporti:

* **Tutti**: Le informazioni provenienti sia dall’istanza di creazione che dall’istanza di pubblicazione popolano la Suite di rapporti.
* **Autore**: Solo le informazioni dell&#39;istanza di creazione popolano la suite di rapporti.
* **Pubblica**: Solo le informazioni dell&#39;istanza di pubblicazione popolano la suite di rapporti.

>[!NOTE]
>
>Selezionando il tipo di istanza del server non si limitano le chiamate a  Adobe Analytics, si limita a controllare quali chiamate includere il RSID.
>
>Ad esempio, un framework è configurato per utilizzare la suite di rapporti *diiweretail* e l&#39;autore è l&#39;istanza del server selezionata. Quando le pagine vengono pubblicate insieme al framework, vengono effettuate chiamate ad Adobe Analytics , ma queste chiamate non contengono il RSID. Solo le chiamate dall’istanza di creazione includono l’RSID.

1. Utilizzando **Navigazione**, selezionare **Strumenti**, **Cloud Services**, quindi **Cloud Services precedenti**.
1. Scorrete fino a **Adobe Analytics** e selezionate **Mostra configurazioni**.
1. Fate clic sul collegamento **[+]** accanto alla configurazione Adobe Analytics .

1. Nella finestra di dialogo **Crea framework**:

   * Specificare un **Titolo**.
   * Facoltativamente è possibile specificare il **Nome** per il nodo che memorizza i dettagli del framework nella directory archivio.
   * Selezionare **Adobe Analytics Framework**

   Fare clic su **Crea**.

   Il framework viene aperto per la modifica.

1. Nella sezione **Suite di rapporti** del contenitore laterale (lato destro del pannello principale), fate clic su **Aggiungi elemento**. Quindi utilizzate il menu a discesa per selezionare l&#39;ID della suite di rapporti (ad esempio, `geometrixxauth`) con cui interagisce il framework.

   >[!NOTE]
   >
   >Content Finder a sinistra viene popolato con  variabili Adobe Analytics (variabili di SiteCatalyst) quando selezionate un ID suite di rapporti.

1. Quindi utilizzate il menu a discesa **Modalità di esecuzione** (accanto all&#39;ID della suite di rapporti) per selezionare le istanze del server che desiderate inviare informazioni alla suite di rapporti.

   ![aa-framework-01](assets/aa-framework-01.png)

1. Per rendere il framework disponibile nell&#39;istanza di pubblicazione del sito, nella scheda **Pagina** della barra laterale fate clic su **Attiva framework.**

### Configurazione delle impostazioni del server per  Adobe Analytics {#configuring-server-settings-for-adobe-analytics}

Il sistema framework consente di modificare le impostazioni del server all&#39;interno di ogni  framework Adobe Analytics.

>[!CAUTION]
>
>Queste impostazioni determinano dove vengono inviati i dati e come, pertanto è fondamentale che *non si interferisca con queste impostazioni* e lasciare che il rappresentante Adobe Analytics  configuri il messaggio.

Per iniziare, aprite il pannello. Premere la freccia rivolta verso il basso accanto a **Server**:

![server_001](assets/server_001.png)

* **Server per tracking**

   * contiene l&#39;URL utilizzato per inviare  chiamate Adobe Analytics

      * cname - per impostazione predefinita viene utilizzato l&#39;account Adobe Analytics  *Nome società*
      * d1 - corrisponde al centro dati a cui verranno inviate le informazioni (può essere d1, d2 o d3)
      * sc.omtrdc.net - nome di dominio

* **Server di tracciamento protetto**

   * Ha gli stessi segmenti del server di tracciamento
   * Viene utilizzato per l&#39;invio di dati da pagine protette (https://)

* **Namespace visitatore**

   * Lo spazio nomi determina la prima parte dell’URL di tracciamento.
   * Ad esempio, se si modifica lo spazio dei nomi in **CNAME**, le chiamate effettuate a  Adobe Analytics saranno simili a **CNAME.d1.omtrdc.net** anziché a quelle predefinite.

## Associazione di una pagina a un Adobe Analytics Framework  {#associating-a-page-with-a-adobe-analytics-framework}

Quando una pagina è associata a un framework Adobe Analytics , la pagina invia i dati ad  Adobe Analytics quando la pagina viene caricata. Le variabili compilate dalla pagina vengono mappate e recuperate da  variabili Adobe Analytics nel framework. Ad esempio, le visualizzazioni di pagina vengono recuperate da  Adobe Analytics.

I discendenti della pagina ereditano l&#39;associazione con il framework. Ad esempio, quando associate la pagina principale del sito a una struttura, tutte le pagine del sito sono associate alla struttura.

1. Dalla console **Siti**, selezionate la pagina da impostare con il tracciamento.
1. Aprire la **[Proprietà pagina](/help/sites-authoring/editing-page-properties.md)**, direttamente dalla console o dall&#39;editor pagina.
1. Aprite la scheda** Cloud Services**.

1. Utilizzate il menu a discesa **Aggiungi configurazione** per selezionare **Adobe Analytics** dalle opzioni disponibili. Se l&#39;ereditarietà è collocata, è necessario disattivarla prima che il selettore diventi disponibile.

1. Il selettore a discesa per **Adobe Analytics** verrà aggiunto alle opzioni disponibili. Utilizzate questa opzione per selezionare la configurazione del framework richiesta.

1. Selezionare **Save &amp; Close**.
1. **[Pubblicate](/help/sites-authoring/publishing-pages.md)** la pagina per attivare la pagina ed eventuali configurazioni/file connessi.
1. Il passo finale consiste nel visitare la pagina nell’istanza di pubblicazione e cercare una parola chiave (ad esempio melanzana) utilizzando il componente **Search**.
1. È quindi possibile controllare le chiamate effettuate a  Adobe Analytics utilizzando uno strumento appropriato; ad esempio, [Adobe Experience Cloud Debugger](https://docs.adobe.com/content/help/en/debugger/using/experience-cloud-debugger.html).
1. Utilizzando l&#39;esempio fornito, la chiamata deve contenere il valore immesso (ad es. melanzana) in  eVar 7 e l&#39;elenco degli eventi deve contenere event3.

### Visualizzazioni pagina {#page-views}

Quando una pagina è associata a un framework Adobe Analytics , il numero di visualizzazioni di pagina può essere visualizzato nella vista Elenco della console Siti.

Per ulteriori informazioni, vedere [Seeing Page Analytics Data](/help/sites-authoring/page-analytics-using.md).

### Configurazione dell&#39;intervallo di importazione {#configuring-the-import-interval}

Configurare l&#39;istanza appropriata del servizio **Adobe AEM configurazione del polling gestito**:

* **Intervallo** sondaggio: L&#39;intervallo, in secondi, in base al quale il servizio recupera i dati di visualizzazione della pagina da  Adobe Analytics.
L’intervallo predefinito è 43200000 ms (12 ore).

* **Abilita**: Abilitare o disabilitare il servizio. Per impostazione predefinita, il servizio è abilitato.

Per configurare questo servizio OSGi, è possibile utilizzare la [console Web](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) o un nodo [osgiConfig nell&#39;archivio](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository) (il servizio PID è `com.day.cq.polling.importer.impl.ManagedPollConfigImpl`).

## Modifica  configurazioni e/o framework Adobe Analytics {#editing-adobe-analytics-configurations-and-or-frameworks}

Come per la creazione di una configurazione o un framework Adobe Analytics , andate alla schermata (precedente) **Cloud Services**. Selezionare **Mostra configurazioni**, quindi fare clic sul collegamento alla configurazione specifica da aggiornare.

Durante la modifica di una configurazione Adobe Analytics , è necessario premere il pulsante **Modifica** nella pagina di configurazione stessa per aprire la finestra di dialogo **Modifica componente**.

## Eliminazione  framework Adobe Analytics {#deleting-adobe-analytics-frameworks}

Per eliminare un framework Adobe Analytics , prima [aprirlo per la modifica](#editing-adobe-analytics-configurations-and-or-frameworks).

Selezionare quindi **Elimina framework** dalla scheda **Pagina** della barra laterale.

