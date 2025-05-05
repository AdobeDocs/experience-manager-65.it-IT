---
title: Connessione ad Adobe Analytics e creazione di framework
description: Scopri come collegare l’AEM al SiteCatalyst e creare framework.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
docset: aem65
exl-id: 8262bbf9-a982-479b-a2b5-f8782dd4182d
solution: Experience Manager, Experience Manager Sites
feature: Integration
role: Admin
source-git-commit: eae057caed533ef16bb541b4ad41b8edd7aaa1c7
workflow-type: tm+mt
source-wordcount: '1484'
ht-degree: 1%

---

# Connessione ad Adobe Analytics e creazione di framework {#connecting-to-adobe-analytics-and-creating-frameworks}

Per tenere traccia dei dati web dalle pagine dell’AEM in Adobe Analytics, crea una configurazione dei servizi Adobe Analytics Cloud e un framework Adobe Analytics:

* **Configurazione Adobe Analytics:** le informazioni sul tuo account Adobe Analytics. La configurazione di Adobe Analytics consente all’AEM di connettersi ad Adobe Analytics. Crea una configurazione di Adobe Analytics per ogni account utilizzato.
* **Adobe Analytics Framework:** un set di mappature tra le proprietà della suite di rapporti di Adobe Analytics e le variabili CQ. Utilizza un framework per configurare il modo in cui i dati del tuo sito web compilano i rapporti di Adobe Analytics. I framework sono associati a una configurazione Adobe Analytics. Puoi creare più framework per ogni configurazione.

Quando si associa una pagina Web a un framework, il framework esegue il tracciamento della pagina e dei relativi discendenti. Le visualizzazioni di pagina possono quindi essere recuperate da Adobe Analytics e visualizzate nella console Sites.

## Prerequisiti {#prerequisites}

### Account Adobe Analytics {#adobe-analytics-account}

Per tenere traccia dei dati AEM in Adobe Analytics, devi disporre di un account Adobe Experience Cloud Adobe Analytics valido.

L’account Adobe Analytics deve:

* Disponi di **privilegi di amministratore**
* Essere assegnato al gruppo di utenti **Accesso al servizio Web**.

>[!CAUTION]
>
>Non è sufficiente fornire privilegi di **amministratore** (in Adobe Analytics) per consentire a un utente di connettersi da AEM ad Adobe Analytics. L&#39;account deve inoltre disporre dei privilegi di **Accesso al servizio Web**.

![chlimage_1-67](assets/chlimage_1-67.png)

Prima di procedere, accertati di disporre delle credenziali per accedere ad Adobe Analytics. In uno dei modi seguenti:

* [Accesso a Adobe Experience Cloud](https://experience.adobe.com/#/@login/home)

* [Accesso ad Adobe Analytics](https://sc.omniture.com/login/)

### Configurazione dell’AEM per l’utilizzo dei centri dati di Adobe Analytics {#configuring-aem-to-use-your-adobe-analytics-data-centers}

I [data center](https://experienceleague.adobe.com/docs/analytics/analyze/reports-analytics/reporting-interface/overview-data-collection.html?lang=it) di Adobe Analytics raccolgono, elaborano e memorizzano i dati associati alla suite di rapporti di Adobe Analytics. Configura AEM per utilizzare il data center che ospita la tua suite di rapporti Adobe Analytics. Il centro dati è menzionato nel contratto. Per queste informazioni, contatta un amministratore della tua organizzazione.

Se necessario, utilizzare quanto segue per essere instradato al data center corretto: `https://api.omniture.com/`.

Se l’organizzazione richiede la raccolta o il recupero di dati da un centro dati specifico, utilizza quanto segue:

| Datacenter | URL |
|---|---|
| Londra | `https://api3.omniture.com/` |
| Singapore | `https://api4.omniture.com/` |
| Oregon | `https://api5.omniture.com/` |

Utilizza la [console Web per configurare il bundle OSGi](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) **Adobe del client HTTP AEM Analytics**. Aggiungi **URL del centro dati** per il centro dati che ospita una suite di rapporti per la quale le pagine AEM raccolgono i dati.

![aa-07](assets/aa-07.png)

1. Apri la console Web nel browser. ([https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr))
1. Per accedere alla console, immetti le tue credenziali.

   >[!NOTE]
   >
   >Per verificare se è possibile accedere a questa console, contattare l&#39;amministratore del sito.

1. Selezionare l&#39;elemento di configurazione denominato **Adobe AEM Analytics HTTP Client**.
1. Per aggiungere l&#39;URL di un data center, premere il pulsante + accanto all&#39;elenco **URL del data center** e digitare l&#39;URL nella casella.

1. Per rimuovere un URL dall’elenco, fai clic sul pulsante - accanto all’URL.
1. Fai clic su Salva.

## Configurazione della connessione ad Adobe Analytics {#configuring-the-connection-to-adobe-analytics}

>[!CAUTION]
>
>A causa di modifiche di sicurezza nell’API di Adobe Analytics, non è più possibile utilizzare la versione di Activity Map inclusa nell’AEM.
>
>È ora necessario utilizzare il plug-in [ActivityMap fornito da Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/analyze/activity-map/getting-started/get-started-users/activitymap-install.html?lang=it).

## Configurazione per l’Activity Map {#configuring-for-the-activity-map}

>[!CAUTION]
>
>A causa di modifiche di sicurezza nell’API di Adobe Analytics, non è più possibile utilizzare la versione di Activity Map inclusa nell’AEM.
>
>È ora necessario utilizzare il plug-in [ActivityMap fornito da Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/analyze/activity-map/getting-started/get-started-users/activitymap-install.html?lang=it).

## Creazione di un framework Adobe Analytics {#creating-a-adobe-analytics-framework}

Per l’ID suite di rapporti (RSID) in uso, puoi controllare quali istanze del server (authoring, pubblicazione o entrambe) contribuiscono ai dati della suite di rapporti:

* **Tutti**: le informazioni dell&#39;istanza di authoring e di pubblicazione popolano la suite di rapporti.
* **Autore**: solo le informazioni dell&#39;istanza di authoring popolano la suite di rapporti.
* **Publish**: solo le informazioni dell&#39;istanza Publish popolano la suite di rapporti.

>[!NOTE]
>
>La selezione del tipo di istanza del server non limita le chiamate ad Adobe Analytics, ma controlla semplicemente le chiamate che includono l’RSID.
>
>Ad esempio, un framework è configurato per utilizzare la suite di rapporti *diiweretail* e l&#39;istanza del server selezionata è Author. Quando si pubblicano le pagine insieme al framework, vengono comunque effettuate chiamate ad Adobe Analytics, tuttavia queste chiamate non contengono l’RSID. Solo le chiamate dall&#39;istanza di authoring includono l&#39;RSID.

1. Utilizzando **Navigazione**, seleziona **Strumenti**, **Cloud Service**, quindi **Cloud Service precedenti**.
1. Scorri fino a **Adobe Analytics** e seleziona **Mostra configurazioni**.
1. Fai clic sul collegamento **[+]** accanto alla configurazione di Adobe Analytics.

1. Nella finestra di dialogo **Crea framework**:

   * Specificare un **Titolo**.
   * Facoltativamente, è possibile specificare **Name** per il nodo che memorizza i dettagli del framework nell&#39;archivio.
   * Seleziona **Adobe Analytics Framework**

   E fai clic su **Crea**.

   Il framework si apre per la modifica.

1. Nella sezione **Suite per report** del pod laterale (lato destro del pannello principale), fai clic su **Aggiungi elemento**. Quindi utilizzare il menu a discesa per selezionare l&#39;ID suite di rapporti (ad esempio, `geometrixxauth`) con cui il framework interagisce.

   >[!NOTE]
   >
   >Quando selezioni un ID suite di rapporti, il Finder dei contenuti a sinistra viene compilato con le variabili di Adobe Analytics (Variabili di SiteCatalyst).

1. Per selezionare le istanze del server a cui si desidera inviare informazioni, utilizzare l&#39;elenco a discesa **Modalità di esecuzione** accanto all&#39;ID suite di rapporti.

   ![aa-framework-01](assets/aa-framework-01.png)

1. Per rendere disponibile il framework nell&#39;istanza di pubblicazione del sito, nella scheda **Pagina** della barra laterale, fare clic su **Attiva framework.**

### Configurazione delle impostazioni del server per Adobe Analytics {#configuring-server-settings-for-adobe-analytics}

Il framework system consente di modificare le impostazioni del server all’interno di ogni framework Adobe Analytics.

>[!CAUTION]
>
>Queste impostazioni determinano dove vengono inviati i dati e come, pertanto è fondamentale che *non manomettere queste impostazioni* e consentire al rappresentante Adobe Analytics di configurarle.

Per iniziare, apri il pannello. Premere la freccia verso il basso accanto a **Server**:

![server_001](assets/server_001.png)

* **Server di tracciamento**

   * contiene l’URL utilizzato per inviare chiamate Adobe Analytics

      * `cname` - impostazione predefinita *Nome società* dell&#39;account Adobe Analytics
      * `d1` - corrisponde al data center a cui vengono inviate le informazioni (`d1`, `d2` o `d3`)
      * `sc.omtrdc.net` - nome dominio

* **Server di tracciamento protetto**

   * Ha gli stessi segmenti del server di tracciamento
   * Utilizzato per l&#39;invio di dati da pagine protette (`https://`)

* **Spazio dei nomi visitatore**

   * Lo spazio dei nomi determina la prima parte dell’URL di tracciamento.
   * Se ad esempio si modifica lo spazio dei nomi in **CNAME**, le chiamate effettuate ad Adobe Analytics avranno l&#39;aspetto di **CNAME.d1.omtrdc.net** anziché quello predefinito.

## Associazione di una pagina a un framework Adobe Analytics {#associating-a-page-with-a-adobe-analytics-framework}

Quando una pagina è associata a un framework Adobe Analytics, invia dati ad Adobe Analytics al caricamento della pagina. Le variabili che la pagina compila vengono mappate e recuperate dalle variabili di Adobe Analytics nel framework. Ad esempio, le visualizzazioni di pagina vengono recuperate da Adobe Analytics.

I discendenti della pagina ereditano l’associazione con il framework. Ad esempio, quando si associa la pagina principale del sito a un framework, tutte le pagine del sito vengono associate al framework.

1. Dalla console **Sites**, seleziona la pagina che desideri impostare con il tracciamento.
1. Apri **[Proprietà pagina](/help/sites-authoring/editing-page-properties.md)** direttamente dalla console o dall&#39;editor pagina.
1. Apri la scheda **&#x200B; Cloud Service &#x200B;**.

1. Utilizza il menu a discesa **Aggiungi configurazione** per selezionare **Adobe Analytics** dalle opzioni disponibili. Se è presente l’ereditarietà, disattivala prima che il selettore diventi disponibile.

1. Il selettore a discesa per **Adobe Analytics** è aggiunto alle opzioni disponibili. Seleziona la configurazione del framework richiesta.

1. Seleziona **Salva e chiudi**.
1. Per attivare la pagina e le configurazioni/i file collegati, **[Publish](/help/sites-authoring/publishing-pages.md)** la pagina.
1. Il passaggio finale consiste nel visitare la pagina nell&#39;istanza di pubblicazione e cercare una parola chiave (ad esempio, melanzana) utilizzando il componente **Ricerca**.
1. Puoi quindi controllare le chiamate effettuate ad Adobe Analytics utilizzando uno strumento appropriato, ad esempio [Adobe Experience Cloud Debugger](https://experienceleague.adobe.com/docs/experience-platform/debugger/home.html?lang=it).
1. Utilizzando l’esempio fornito, la chiamata deve contenere il valore inserito (ossia melanzana) in eVar7 e l’elenco degli eventi deve contenere event3.

### Visualizzazioni pagina {#page-views}

Quando una pagina è associata a un framework Adobe Analytics, il numero di visualizzazioni di pagina può essere visualizzato nella vista a elenco della console Sites.

Per ulteriori dettagli, vedi [Visualizzazione dei dati di analisi delle pagine](/help/sites-authoring/page-analytics-using.md).

### Configurazione dell&#39;intervallo di importazione {#configuring-the-import-interval}

Configura l&#39;istanza appropriata del servizio **Adobe AEM Analytics Report Sling Importer**:

* **Tentativi di recupero**:
Numero di tentativi di recupero di un rapporto in coda.
Il valore predefinito è `6`.

* **Ritardo recupero**:
Il numero di millisecondi tra i tentativi di recuperare un rapporto in coda.
Il valore predefinito è `10000`. Dato che è in millisecondi corrisponde a 10 secondi.

* **Frequenza di recupero**:
Espressione `cron` per determinare la frequenza di recupero del report di Analytics.
Il valore predefinito è `0 0 0/12 * * ?`. Corrisponde a 12 recuperi ogni ora.

Per configurare questo servizio OSGi, è possibile utilizzare la [console Web](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) o un nodo [osgiConfig nell&#39;archivio](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository) (il PID del servizio è `com.day.cq.analytics.sitecatalyst.impl.importer.ReportImporterScheduler`).

## Modifica delle configurazioni e/o dei framework di Adobe Analytics {#editing-adobe-analytics-configurations-and-or-frameworks}

Come per la creazione di una configurazione o di un framework Adobe Analytics, passa alla schermata **Cloud Service** (legacy). Seleziona **Mostra configurazioni**, quindi fai clic sul collegamento alla configurazione specifica da aggiornare.

Durante la modifica di una configurazione di Adobe Analytics, premi **Modifica** nella pagina di configurazione per aprire la finestra di dialogo **Modifica componente**.

## Eliminazione dei framework di Adobe Analytics {#deleting-adobe-analytics-frameworks}

Per eliminare un framework Adobe Analytics, aprirlo prima [per modificarlo](#editing-adobe-analytics-configurations-and-or-frameworks).

Quindi seleziona **Elimina framework** dalla scheda **Pagina** della barra laterale.
