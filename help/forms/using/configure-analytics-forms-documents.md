---
title: Configurazione di analisi e rapporti
seo-title: Configurazione di analisi e rapporti
description: Scoprite come configurare Adobe Analytics per individuare i pattern di interazione e i problemi che gli utenti devono affrontare quando utilizzano moduli adattivi, documenti adattivi e moduli HTML5.
seo-description: Scoprite come configurare Adobe Analytics per individuare i pattern di interazione e i problemi che gli utenti devono affrontare quando utilizzano moduli adattivi, documenti adattivi e moduli HTML5.
uuid: ac5d1300-f303-40e8-a33e-4859a54ac10d
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: integrations
discoiquuid: 96a77980-4213-4779-a540-00905ea8f7e3
docset: aem65
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# Configurazione di analisi e rapporti{#configuring-analytics-and-reports}

AEM Forms si integra con Adobe Analytics per acquisire e tenere traccia delle metriche delle prestazioni per i moduli e i documenti pubblicati. L&#39;obiettivo dell&#39;analisi di queste metriche è di rendere più utilizzabili moduli o documenti con decisioni informate basate sui dati richiesti.

>[!NOTE]
>
>La funzione di analisi in AEM Forms è disponibile come parte del pacchetto del componente aggiuntivo AEM Forms. Per informazioni sull&#39;installazione del pacchetto del componente aggiuntivo, consultate [Installazione e configurazione di AEM Forms](../../forms/using/installing-configuring-aem-forms-osgi.md).
>
>Oltre al pacchetto del componente aggiuntivo, è necessario disporre di un account Adobe Analytics e di privilegi di amministratore per l&#39;istanza di AEM. Per informazioni sulla soluzione, consulta [Adobe Analytics](https://www.adobe.com/solutions/digital-analytics.html).

## Panoramica {#overview}

È possibile utilizzare Adobe Analytics per scoprire i pattern di interazione e i problemi che gli utenti devono affrontare durante l&#39;uso di moduli adattivi, moduli HTML5 e comunicazioni interattive. Adobe Analytics tiene traccia e memorizza automaticamente le informazioni relative ai seguenti parametri:

* **Tempo** medio di riempimento: Tempo medio impiegato per compilare il modulo.
* **Rappresentazioni**: Numero di volte che un modulo viene aperto.
* **Bozze**: Numero di volte in cui un modulo viene salvato nello stato bozza.
* **Invii**: Numero di volte in cui il modulo viene inviato.
* **Interrompi**: Numero di volte in cui gli utenti si allontanano senza compilare il modulo.

Puoi personalizzare Adobe Analytics per aggiungere o rimuovere altri parametri. Oltre alle informazioni di cui sopra, il rapporto contiene le seguenti informazioni su ogni pannello del modulo HTML5 e adattivo:

* **Ora**: Tempo trascorso sul pannello e sui campi del pannello.
* **Errore**: Numero di errori riscontrati nel pannello e nei campi del pannello.
* **Aiuto**: Numero di volte che un utente apre la guida di un pannello e dei campi del pannello.

## Creazione di una suite di rapporti {#creating-report-suite}

I dati di Analytics vengono memorizzati in repository specifici del cliente denominati suite di rapporti. Per creare una suite di rapporti e utilizzare Adobe Analytics, devi disporre di un account Adobe Marketing Cloud valido. Prima di eseguire i seguenti passaggi, accertatevi di disporre di un account Adobe Marketing Cloud valido.

Per creare una suite di rapporti, effettuate le seguenti operazioni.

1. Accedete a [https://sc.omniture.com/login/](https://sc.omniture.com/login/)
1. In Marketing Cloud, seleziona **Admin** > **Admin Console** > **Suite** di rapporti.
1. Selezionate **Crea nuovo** > Suite **di** rapporti in Report Suite Manager.

   ![Crea nuova suite di rapporti](assets/newreportsuite_new.png)

   Crea nuova suite di rapporti

1. Accertatevi che il primo elenco a discesa sia impostato su **Crea da un modello** , quindi selezionate **Commerce**.
1. Individuate il campo ID **suite di** rapporti e aggiungete un nuovo ID suite di rapporti. Ad esempio, JJEsquire. Sotto il campo ID suite di rapporti viene visualizzato un ID suite di rapporti. Include un prefisso automatico, che è spesso il nome della società.
1. Aggiungete un nuovo titolo **** del sito. Ad esempio, JJEsquire Getting Started Suite. Questo titolo viene usato nell’interfaccia utente di Analytics. Usa l&#39;ID suite di rapporti nel tuo codice.
1. Selezionate un **fuso** orario dal menu a discesa. Tutti i dati inclusi in questa suite di rapporti vengono registrati in base al fuso orario definito.
1. Lasciate vuoti i campi URL **di** base e Pagina **** predefinita. Questi due valori vengono utilizzati solo dall&#39;interfaccia di Adobe Marketing Cloud per il collegamento al sito Web.
1. Lascia l&#39;opzione Data **** live impostata su Oggi. Go Live Date determina il giorno in cui viene attivata la suite di rapporti.
1. Nel campo Visualizzazioni **stimate di pagina per giorno** , digitare 100. Utilizzate questo campo per stimare il numero di visualizzazioni di pagina previste per il sito Web al giorno. Questa stima consente ad Adobe di disporre della quantità appropriata di hardware necessaria per elaborare i dati che verranno raccolti.
1. Selezionare una divisa **di** base dal menu a discesa. Tutti i dati di valuta inclusi in questa suite di rapporti vengono convertiti e memorizzati in questo formato di valuta.
1. Fate clic su **Crea suite di rapporti** . Dovresti visualizzare l&#39;aggiornamento della pagina con un messaggio che informa che la tua suite di rapporti è stata creata correttamente.
1. Seleziona la suite di rapporti appena creata. Andate a **Modifica impostazioni** > **Generale** > Impostazioni account **generali**.

   ![Impostazioni account generali](assets/geographic_settings.png)

   Impostazioni account generali

1. Nella schermata Impostazioni account generali, abilita **Reporting** geografia e fai clic su **Salva.**
1. Andate a **Modifica impostazioni** > **Traffico** > Variabili **** traffico.
1. Nella suite di rapporti, configura e abilita le seguenti variabili di traffico.

   * **formName**: Identificatore per un modulo adattivo.
   * **formInstance**: Identificatore di un’istanza di modulo adattivo. Abilita i rapporti Percorso per questa variabile.
   * **fieldName**: Identificatore di un campo modulo adattivo. Abilita i rapporti Percorso per questa variabile.
   * **panelName**: Identificatore di un pannello di moduli adattivi. Abilita i rapporti Percorso per questa variabile.
   * **formTitle**: Titolo del modulo.
   * **fieldTitle**: Titolo del campo modulo.
   * **panelTitle**: Titolo del pannello del modulo.
   * **analyticsVersion**: Versione dell&#39;analisi dei moduli.

1. Andate a **Modifica impostazioni** > **Conversione** > Eventi **di** successo. Definire e attivare i seguenti eventi di successo:

   | Evento Success | Tipo |
   |---|---|
   | abbandono | Contatore |
   | rendering | Contatore |
   | panelVisit | Contatore |
   | fieldVisit | Contatore |
   | save | Contatore |
   | errore | Contatore |
   | aiuto | Contatore |
   | submit | Contatore |
   | timeSpent | Numerico |

   >[!NOTE]
   >
   >Un numero di evento e di proprietà utilizzato per configurare l&#39;analisi di AEM Forms deve essere diverso dal numero di evento e dal numero di proprietà utilizzati nella configurazione dell&#39;analisi [di](/help/sites-administering/adobeanalytics.md) AEM.

1. Disconnettetevi dall&#39;account Adobe Marketing Cloud.

## Creazione della configurazione del servizio Cloud {#creating-cloud-service-configuration}

La configurazione del servizio cloud è un&#39;informazione sull&#39;account Adobe Analytics. La configurazione consente ad Adobe Experience Manager (AEM) di connettersi ad Adobe Analytics. Create una configurazione separata per ciascun account Analytics che utilizzate.

1. Accedete all’istanza di creazione di AEM come amministratore.
1. Nell&#39;angolo in alto a sinistra, fai clic su **Adobe Experience Manager** > **Strumenti** ![](/help/forms/using/assets/tools.png) > **Distribuzione** > Servizi **** Cloud.
1. Individua l’icona **Adobe Analytics** . Fate clic su **Mostra configurazioni** , quindi fate clic su **[+]** per aggiungere una nuova configurazione.

   Se siete un utente principiante, fate clic su **Configura ora**.

1. Aggiungete un Titolo alla nuova configurazione (la compilazione del campo Nome è facoltativa). Ad esempio, Configurazione della mia analisi. Fai clic su **Crea**.

1. Quando il pannello Modifica si apre nella pagina di configurazione, compila i campi:

   * **Società**: Il nome della società come descritto in Adobe Analytics.
   * **Nome utente**: Nome utilizzato per accedere ad Adobe Analytics.
   * **Password**: La password di Adobe Analytics per l&#39;account indicato sopra.
   * **Centro** dati: Centro dati del tuo account Adobe Analytics.

1. Fate clic su **Connetti ad Analytics**. Viene visualizzata una finestra di dialogo con il messaggio che indica che la connessione è stata eseguita correttamente. Fai clic su **OK**. 

## Creazione di un framework di servizi cloud {#creating-cloud-service-framework}

Un framework di Adobe Analytics è un set di mappature tra le variabili Adobe Analytics e AEM. Utilizzare un framework per configurare il modo in cui i moduli compilano i dati nei rapporti di Adobe Analytics. I framework sono associati a una configurazione di Adobe Analytics. Potete creare più framework per ciascuna configurazione.

1. Nella console Servizi cloud AEM, fai clic su **Mostra configurazioni** in Adobe Analytics.
1. Fai clic sul collegamento **[+]** accanto a accanto alla configurazione di Analytics.

   ![Configurazione di Adobe Analytics](assets/adobe-analytics-cloud-services.png)

   Configurazione di Adobe Analytics

1. Digitate un **titolo** e un **nome** per il framework, selezionate **Adobe Analytics** Framework e fate clic su **Crea**. Il framework viene aperto per la modifica.
1. Nella sezione Suite di rapporti del contenitore laterale, fate clic su **Aggiungi elemento**, quindi utilizzate il menu a discesa per selezionare l&#39;ID suite di rapporti (ad esempio, JJEsquire) con cui interagisce il framework.
1. Accanto all&#39;ID della suite di rapporti, seleziona le istanze del server che desideri inviare informazioni alla suite di rapporti.

   ![information_to_send_to_report_suite](assets/information_to_send_to_report_suite.png)

1. Trascinare un componente **Analisi** modulo dall’ **altra** categoria da SideKick al framework.
1. Per mappare le variabili di Analytics con le variabili definite nel componente, trascinate una variabile da AEM Content Finder su un campo del componente di tracciamento.

   ![Mappatura di variabili AEM con variabili Adobe Analytics](assets/analytics_new.png)

1. Attivate il framework utilizzando la scheda **della** pagina nella barra laterale, fate clic su **Attiva framework**.

## Configurazione del servizio di configurazione di AEM Forms Analytics {#configuring-aem-forms-analytics-configuration-service}

1. Nell’istanza di creazione, aprite Gestione configurazione console Web AEM in `https://<server>:<port>;/system/console/configMgr`.
1. Individuazione e apertura della configurazione di AEM Forms Analytics

   ![Servizio di configurazione di AEM Forms Analytics](assets/analytics_configuration.png)

   Servizio di configurazione di AEM Forms Analytics

1. Specificate i valori appropriati per i campi seguenti e fate clic su **Salva**.

   * **SiteCatalyst Framework**: Selezionate la struttura/configurazione definita nella sezione Impostare una struttura per il tracciamento.
   * **Linea di base** tracciamento ora campo: Specificate la durata, in secondi, dopo la quale la visita sul campo deve essere tracciata. Il valore predefinito è 0. Quando il valore è maggiore di 0 (zero), due eventi di tracciamento separati vengono inviati al server Adobe Analytics. Il primo evento indica al server di analisi di interrompere il tracciamento del campo uscito. Il secondo evento viene inviato dopo la scadenza della durata specificata. Il secondo evento indica al server di analisi di avviare il tracciamento del campo visitato. L&#39;utilizzo di due eventi separati consente di misurare con precisione il tempo trascorso su un campo. Quando il valore è 0 (zero), un singolo evento di tracciamento viene inviato al server Adobe Analytics.

   * **Cron** di sincronizzazione dei report di analisi: Specifica l&#39;espressione cron per il recupero dei report da Adobe Analytics. Il valore predefinito è 0 0 2 ? * *.

   * **Timeout report recupero:** Specificate la durata, in secondi, dell&#39;attesa che il server risponda al report di analisi. Il tempo predefinito è 120 secondi.
   >[!NOTE]
   >
   >L&#39;operazione di recupero del rapporto di timeout può richiedere fino a 10 secondi in più, quindi il numero specificato di secondi.

1. Ripetete i passaggi da 1 a 3 nell’istanza di pubblicazione per configurare l’analisi.

Ora è possibile abilitare l&#39;analisi per i moduli e generare un rapporto di analisi.

## Abilitazione dell&#39;analisi per un modulo o un documento {#enabling-analytics-for-a-form-or-document}

1. Effettuate l&#39;accesso al portale AEM all&#39;indirizzo `https://[hostname]:'port'`.
1. Fare clic su **Moduli > Moduli e documenti**, selezionare un modulo o un documento, quindi fare clic su **Abilita analisi**. L&#39;analisi è abilitata.

   ![Abilitazione dell&#39;analisi per un modulo o un documento](assets/enable-analytics-1.png)

   Abilitazione dell&#39;analisi per un modulo

   **A.** Pulsante Abilita Analytics **B.** Modulo selezionato

   Per informazioni dettagliate sulla visualizzazione dei rapporti di analisi dei moduli, consultate [Visualizzazione e comprensione dei rapporti di analisi di AEM Forms](../../forms/using/view-understand-aem-forms-analytics-reports.md)

