---
title: ' app AEM Forms'
seo-title: ' app AEM Forms'
description: '''app AEM Forms consente ai dipendenti sul campo di utilizzare moduli adattivi sui propri dispositivi mobili.'
seo-description: '''app AEM Forms consente ai dipendenti sul campo di utilizzare moduli adattivi sui propri dispositivi mobili.'
uuid: fac976c8-b713-4492-b153-f567e7a11ceb
contentOwner: sashanka
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: e18aa345-034c-473b-b4c2-01678bb10616
translation-type: tm+mt
source-git-commit: af326f2d2b278fe36df05afc8c172f74c99a064c
workflow-type: tm+mt
source-wordcount: '2470'
ht-degree: 0%

---


# Introduction to AEM Forms app {#aem-forms-app}

## Panoramica {#overview}

&#39;app AEM Forms consente la sincronizzazione di moduli adattivi, moduli mobili e set di moduli su dispositivi mobili, in base al server. Puoi definire flussi di lavoro incentrati su [Forms nei flussi di lavoro OSGi](/help/forms/using/aem-forms-workflow.md) o Forms in JEE. Ad esempio, si esegue un&#39;azienda bancaria e si utilizza  AEM Forms per gestire le applicazioni e le comunicazioni dei clienti. I clienti compilano un modulo e lo inviano per la verifica. Se il modulo è abilitato su dispositivi mobili, i clienti possono compilarlo nell&#39;app AEM Forms . È inoltre possibile gestire il flusso di lavoro di verifica abilitando il modulo di verifica sui dispositivi mobili. Il lavoratore sul campo può trasportare un dispositivo mobile al cliente, verificare i dettagli e inviare il modulo. L&#39;app  AEM Forms si sincronizza con  server AEM Forms e recupera i moduli abilitati per i dispositivi mobili. Se l&#39;app è offline, memorizza i dati localmente.

Il codice sorgente dell&#39;app AEM Forms  è disponibile per i clienti tramite Distribuzione software. Il pacchetto del codice sorgente in Distribuzione software è disponibile come segue: `adobe-aemfd-forms-app-src-pkg-<version>.zip`.

 app AEM Forms è supportata sui dispositivi iOS, Android e Windows. Puoi installare  app AEM Forms per Android da Google Play, iOS da App Store e Windows da Windows Store.

    [ ![google_play](assets/google_play.png)](https://play.google.com/store/apps/details?id=com.adobe.aem.forms)
    
    [ ![app_store](assets/app_store.png)](https://itunes.apple.com/us/app/adobe-experience-manager-forms/id1129625976?ls=1&amp;mt=8)
    
    [ ![microsoft-badge-icon](assets/microsoft-badge-icon.png)](https://www.microsoft.com/en-us/store/p/adobe-experience-manager-forms/9nd12rlxtgtt)

Per installare, personalizzare e distribuire l&#39;app sui dispositivi iOS, Android o Windows, consultate [Personalizzare, creare e distribuire l&#39;app](#customize-build-distribute)AEM Forms .

## Prerequisiti {#prerequisites}

 app AEM Forms richiede un server AEM Forms . Gli utenti possono eseguire il rendering dei moduli creati nel AEM server di moduli, compilarli, salvarli come bozze e inviarli. L&#39;app si connette al server e recupera i moduli abilitati da esso. &#39;app AEM Forms si sincronizza con il server e non appena i moduli vengono caricati nell&#39;app, gli utenti possono lavorare offline. Se l&#39;app è offline, i dati vengono salvati sul dispositivo e i dati vengono sincronizzati con il server quando l&#39;app è online.

###  app AEM Forms con server tramite  flusso di lavoro AEM Forms {#aem-forms-app-with-servers-using-aem-forms-workflow}

Se si dispone di un server AEM Forms Workflow , è possibile eseguire il rendering dei moduli come attività &#39;app AEM Forms. Ad esempio, si esegue un&#39;azienda bancaria e il cliente compila un&#39;applicazione per utilizzare i propri servizi. L’applicazione è un modulo adattivo che accetta le informazioni dei clienti e le memorizza come invio per la revisione. L&#39;amministratore rivede un&#39;applicazione e inoltra una richiesta di verifica al lavoratore sul campo. L&#39;applicazione inoltrata abilita un modulo di verifica nell&#39;app del lavoratore sul campo come attività. Il lavoratore sul campo trasporta il dispositivo mobile al cliente e verifica i dettagli.

###  app AEM Forms con server che utilizzano un flusso di lavoro basato su Forms su OSGi {#aem-forms-app-with-servers-using-forms-centric-workflow-on-osgi}

Se si dispone di un server AEM Forms , è possibile eseguire il rendering dei moduli adattivi come applicazione AEM Posta in arrivo e le operazioni &#39;app AEM Forms. Ad esempio, si esegue un&#39;azienda bancaria e il cliente compila un&#39;applicazione per utilizzare i propri servizi. L&#39;applicazione è associata a un modulo adattivo che accetta le informazioni dei clienti e le memorizza come invio per la revisione. L&#39;amministratore rivede l&#39;attività e approva la richiesta di verifica al lavoratore del campo. Il lavoratore sul campo trasporta il dispositivo mobile al cliente e verifica i dettagli.

### Moduli standalone o app AEM Forms  con server senza  flusso di lavoro AEM Forms {#standalone-forms-or-aem-forms-app-with-servers-without-aem-forms-workflow}

Un server AEM Forms  che non utilizza  flusso di lavoro AEM Forms è  AEM Forms su OSGi o un modulo mobile o adattivo indipendente. &#39;app AEM Forms funziona con l&#39;implementazione AEM Forms  su [OSGi](/help/sites-deploying/configuring-osgi.md). L&#39;Forms che abilitate e pubblicate per &#39;app AEM Forms è disponibile nell&#39;app.

I moduli vengono scaricati nell&#39;app e sono disponibili offline. Ad esempio, si esegue un&#39;azienda bancaria e un cliente compila un&#39;applicazione sul sito. L&#39;applicazione è un modulo adattivo che accetta le informazioni dei clienti e le memorizza per la revisione. L&#39;amministratore rivede il modulo e crea un modulo di verifica nell&#39;istanza AEM autore. L&#39;amministratore abilita la sincronizzazione del modulo con &#39;app AEM Forms e lo pubblica. Se il modulo di verifica è disponibile &#39;app AEM Forms, l&#39;agente del campo può utilizzare un dispositivo mobile per verificare i dettagli del cliente. Il dispositivo mobile si sincronizza con il server e il modulo di verifica viene caricato nell&#39;app. L&#39;agente del campo può visitare il cliente, verificare i dettagli, salvare i dati come bozza o inviare il modulo di verifica. Il modulo viene sincronizzato con il server ogni volta che l&#39;app è online.

Per sincronizzare il modulo &#39;app AEM Forms:

1. Nell’istanza di creazione, selezionare un modulo e fare clic su **[!UICONTROL Visualizza proprietà]**.

1. Nella pagina delle proprietà fare clic su **[!UICONTROL Avanzate]**.
1. In Avanzate, abilita opzione: **[!UICONTROL Sincronizza con  app]** AEM Forms e tocca **[!UICONTROL Salva]**.

Quando il modulo viene pubblicato, l&#39;app si sincronizza con il server e recupera il modulo. Per sincronizzare più moduli, nell&#39;istanza di creazione selezionare più moduli in Forms Manager e toccare **[!UICONTROL Sincronizza con  app]** AEM Forms.

## Supporto per dispositivi mobili {#mobile-device-support}

Consultate [app AEM Forms (precedentemente nota come Mobile Workspace)](/help/forms/using/aem-forms-jee-supported-platforms.md#aem-forms-workspace-app)

## Funzioni chiave dell&#39;app  AEM Forms {#key-features-of-aem-forms-app}

###  app AEM Forms con  server AEM Forms {#aem-forms-app-with-aem-forms-servers}

È possibile sincronizzare l&#39;app con il server AEM Forms  e lavorare con i moduli sul dispositivo mobile.

Con  server AEM Forms Workflow, è possibile associare un modulo a un punto di partenza in un processo Workbench e AEM applicazione Inbox. A un&#39;applicazione Casella in entrata AEM può essere associato un modulo adattivo. Un punto di avvio può avere un modulo adattivo, un modulo HTML5 o un set di moduli ad esso associato. Un punto di inizio può essere inviato come attività oppure l&#39;attività può essere salvata come bozza. Per ulteriori informazioni sulle differenze tra un&#39;applicazione AEM Inbox e un punto di partenza, vedere [Azioni e funzionalità dei flussi di lavoro AEM basati su moduli su OSGi e  flussi di lavoro](capabilities-osgi-jee-workflows.md)AEM Forms JEE.

Con  server AEM Forms senza  flusso di lavoro AEM Forms, viene eseguito il rendering di un modulo abilitato per la sincronizzazione nell&#39;app  AEM Forms. Forms è disponibile nella scheda Forms dell&#39;app, può essere inviato o salvato come bozza. Nell&#39;app sono supportati moduli adattivi e moduli per dispositivi mobili.

1. **Salvataggio di un&#39;attività o di un modulo come bozza**

   L&#39;opzione Salva come bozza consente di salvare un&#39;istantanea di un&#39;attività o di un modulo insieme ai dati compilati e ai file allegati nel modulo associato. Le bozze vengono salvate sul dispositivo mobile e sincronizzate con  server AEM Forms per un successivo recupero.

   Vedere [Salvataggio di un&#39;attività o di un modulo come bozza](/help/forms/using/save-as-draft.md).

1. **Salva il modulo come modello**

   A volte, quando gli utenti compilano un modulo, gli input di alcuni campi rimangono gli stessi. Per tali istanze, è possibile compilare i campi che richiedono valori identici in ogni istanza e salvare il modulo o la bozza come modello. Ora, ogni volta che create un’istanza del modello, i campi specificati sono già compilati con i valori specificati nel modello. Consente di risparmiare tempo e sforzi per compilare il modulo.

   Vedere [Salvare i moduli come modelli](/help/forms/using/save-forms-and-start-points-as-templates.md).

### Operazioni con le attività e i moduli {#working-with-tasks-and-forms}

Puoi sincronizzare l&#39;app con il server  AEM Forms Workflow e lavorare su attività e moduli sul dispositivo mobile.

Un&#39;attività sul dispositivo mobile contiene un modulo adattivo, un modulo HTML5 o un set di moduli e può contenere allegati e URL [di](/help/forms/using/getting-task-variables-summary-url.md)riepilogo. Per impostazione predefinita, le attività assegnate all’utente vengono inserite nella cartella **[!UICONTROL Attività]** . Quando lavorate su un&#39;attività, potete modificare l&#39;attività e salvare una bozza di copia dell&#39;attività sul server AEM Forms .

Un modulo sul dispositivo mobile può essere un modulo adattivo o un modulo mobile. Forms abilitato per la sincronizzazione nell&#39;app dei moduli è disponibile nella cartella Forms. È possibile sincronizzare i moduli abilitati  server AEM Forms senza  flusso di lavoro AEM Forms ( AEM Forms su OSGi).

Consulta:

* [Apertura di un&#39;attività](/help/forms/using/open-task.md)
* [Uso di un modulo](/help/forms/using/working-with-form.md)

### Utilizzo offline {#working-offline}

Potete utilizzare il dispositivo mobile in modalità offline. È possibile accedere all&#39;applicazione anche in assenza di connettività di rete e lavorare su tutti i moduli sincronizzati con il dispositivo al momento dell&#39;ultima connessione. Per informazioni dettagliate sulla sincronizzazione dei moduli, vedere [Sincronizzazione dell&#39;app](/help/forms/using/sync-app.md). Se si sceglie di sincronizzare gli allegati associati a un modulo, è possibile aprire gli allegati anche in modalità offline. È possibile modificare il modulo, aggiungere annotazioni e inviare o salvare un modulo in modalità offline. Al successivo accesso online, il modulo viene sincronizzato con il server AEM Forms .

Per informazioni dettagliate, consultate [Utilizzo della modalità](/help/forms/using/work-offline-mode.md)offline.

### Adding annotations {#adding-annotations}

È possibile aggiungere i seguenti allegati a un modulo sul dispositivo mobile

* **Note**: è possibile utilizzare la funzione Note per aggiungere uno script a mano libera o una nota di testo nel modulo. Per informazioni dettagliate, consultate [Aggiunta di una nota](/help/forms/using/add-attachments.md#adding-a-note).

* **Immagine**- L&#39;app  AEM Forms include una funzione che utilizza la funzionalità della fotocamera o la galleria del dispositivo mobile. Utilizzando l&#39;allegato fotografico, è possibile aggiungere una fotografia con il modulo associato. Per informazioni dettagliate, consultate [Aggiunta di una fotografia](/help/forms/using/add-attachments.md#adding-a-photograph).

### Autosavaluta {#autosave}

Quando un utente immette dei dati nell&#39;app AEM Forms , la funzione di salvataggio automatico li salva a intervalli regolari. La funzione di salvataggio automatico nell&#39;app AEM Forms  consente di evitare la perdita di dati se l&#39;app si chiude a causa di condizioni come la batteria scarica.

Consultate [Utilizzo del salvataggio automatico in &#39;app](/help/forms/using/autosave-data-app.md)AEM Forms.

## Differenze tra AEM Posta in arrivo e  funzionalità dell&#39;app AEM Forms {#differences-between-aem-inbox-and-aem-forms-app-features}

Due dei modi principali per avviare un flusso di lavoro incentrato su Forms sono utilizzare [AEM Posta in arrivo](/help/forms/using/manage-applications-inbox.md) e  app AEM Forms. Le funzionalità dell&#39;app AEM Posta in arrivo e  AEM Forms, tuttavia, differiscono. AEM Inbox funziona solo con flussi di lavoro [basati su](/help/forms/using/aem-forms-workflow.md) Forms, mentre l&#39;app AEM Forms  funziona sia con flussi di lavoro incentrati su Forms che con la gestione dei processi. Per ulteriori informazioni sulle differenze tra AEM funzionalità delle app in entrata e , vedi [Azioni e funzionalità dei flussi di lavoro AEM incentrati sui moduli nei flussi di lavoro](capabilities-osgi-jee-workflows.md)OSGi e  AEM Forms JEE.

## Moduli supportati {#supported-forms}

Tipi di modulo supportati nell&#39;app AEM Forms :

### Modulo adattivo {#adaptive-form}

Un modulo adattivo che si adatta dinamicamente agli input dell&#39;utente è supportato &#39;app AEM Forms. Sono supportati anche i moduli adattivi caricati in modo persistente.

### Modulo mobile {#mobile-form}

È possibile creare moduli per dispositivi mobili in  AEM Forms. I moduli mobili vengono rappresentati come moduli HTML nei dispositivi mobili che si adattano in base ai dispositivi di visualizzazione.

### Set di moduli {#formset}

Con i formati, è possibile raggruppare più moduli relativi a un servizio o a un processo per automatizzare un processo aziendale e presentarli agli utenti finali. In questo caso, gli utenti possono compilare l&#39;intero set come un unico set e non è necessario archiviare, inviare e tenere traccia dei singoli moduli o processi.

>[!NOTE]
>
>Richiede  flusso di lavoro AEM Forms ( AEM Forms su JEE).

##  funzionamento dell&#39;app AEM Forms {#how-aem-forms-app-works}

&#39;app AEM Forms offre una soluzione mobile che consente ai lavoratori sul campo di lavorare sui moduli ad essi assegnati. L&#39;applicazione memorizza nella cache i dati completi dal server e fornisce un&#39;esperienza utente efficiente salvando tutto il lavoro localmente. I dati del disco vengono inviati al server tramite aggiornamenti tempestivi della sincronizzazione.

 app AEM Forms è un&#39;applicazione basata su PhoneGap 5.0 in cui il modello Backbone viene utilizzato in modo efficiente per presentare i dati memorizzati nei modelli attraverso le viste. Tutte le operazioni native vengono eseguite tramite i plug-in PhoneGap.

## Personalizzare, creare e distribuire l&#39;app  AEM Forms {#customize-build-distribute}

>[!NOTE]
>
>Applicabile solo se utilizzate  codice sorgente dell&#39;app AEM Forms per creare l&#39;app.

&#39;app AEM Forms è facile da personalizzare in base alle esigenze specifiche dell&#39;organizzazione. Il codice sorgente per l’applicazione viene fornito insieme  AEM Forms. Puoi cambiare il codice sorgente e creare una tua soluzione per la forza lavoro mobile. Potete inoltre firmare l&#39;app con la vostra chiave enterprise.

### Personalizzazione {#customize}

Potete personalizzare l&#39;app per:

**Branding**: Modifica l&#39;icona dell&#39;app, il nome dell&#39;app, le immagini di avvio e le pagine in &#39;app AEM Forms. Potete anche modificare il testo per localizzare l&#39;app per un&#39;area specifica. Per ulteriori informazioni sul marchio dell&#39;app AEM Forms , consultate Personalizzazione del [marchio](/help/forms/using/branding-customization.md).

**Tema**: Modifica di stili quali colori, font e spaziatura nell&#39;interfaccia utente  app AEM Forms. Per ulteriori informazioni, consultate Personalizzazione dei [temi](/help/forms/using/theme-customization.md).

**Gesti**: Modifica gesti quali il passaggio del dito verso destra e il passaggio del dito verso sinistra nell&#39;interfaccia utente dell&#39;app AEM Forms . Per ulteriori informazioni, consultate Personalizzazione dei [gesti](/help/forms/using/gesture-customization.md).

Per ulteriori informazioni sulla configurazione di un progetto  app AEM Forms per la personalizzazione, vedi:

* [Configurare l&#39;ambiente per &#39;app AEM Forms](/help/forms/using/setup-environment-mobile-workspace.md)
* [Configurare il progetto Visual Studio e creare l&#39;app Windows](/help/forms/using/setup-visual-studio-project-build-installer.md)
* [Configurare il progetto Xcode e creare l&#39;app iOS](/help/forms/using/setup-xcode-project-build-installer.md)
* [Configurare il progetto Eclipse e creare l&#39;app Android](/help/forms/using/setup-eclipse-project-build-installer.md)

### Creazione e distribuzione {#build-and-distribute}

Il codice sorgente per l&#39;app AEM Forms  può essere estratto dal `adobe-lc-mobileworkspace-src.zip` che è disponibile come parte del pacchetto di origine dell&#39;app AEM Forms  sulla distribuzione del software.

Per ottenere l&#39;origine dell&#39;app AEM Forms , effettuate le seguenti operazioni:

1. Apri distribuzione [](https://experience.adobe.com/downloads)software. È necessario un Adobe ID  per accedere a Distribuzione software.
1. Toccate **[!UICONTROL Adobe Experience Manager]** disponibile nel menu di intestazione.
1. Nella sezione **[!UICONTROL Filtri]** :
   1. Selezionate **[!UICONTROL Forms]** dall&#39;elenco a discesa **[!UICONTROL Soluzione]** .
   2. Selezionate la versione e digitate il tipo di pacchetto. Potete anche utilizzare l&#39;opzione Download **[!UICONTROL di]** ricerca per filtrare i risultati.
1. Toccate il nome del pacchetto applicabile al sistema operativo in uso, selezionate **[!UICONTROL Accetta termini]** EULA e toccate **[!UICONTROL Scarica]**.
1. Aprite [Package Manager](https://docs.adobe.com/content/help/en/experience-manager-65/administering/contentmanagement/package-manager.html) e fate clic su **[!UICONTROL Carica pacchetto]** per caricare il pacchetto.
1. Select the package and click **[!UICONTROL Install]**.

**Per iOS**:

Per informazioni dettagliate su come creare un&#39;app iOS (.ipa), consultate [Configurare il progetto Xcode e creare l&#39;app](/help/forms/using/setup-xcode-project-build-installer.md)iOS.

Per informazioni dettagliate su come firmare l&#39;app AEM Forms  con il profilo di provisioning, consultate Configurazione, elaborazione e risoluzione dei problemi per la firma dei codici [iOS](https://developer.apple.com/support/code-signing/).

**Per Android**:

Per informazioni dettagliate su come creare un&#39;app Android (.apk), consultate [Configurare il progetto Eclipse e creare l&#39;app](/help/forms/using/setup-eclipse-project-build-installer.md)Android.

Per informazioni dettagliate su come firmare l&#39;app AEM Forms , consultate [Firma delle applicazioni](https://developer.android.com/tools/publishing/app-signing.html).

**Per Windows**:

Per informazioni dettagliate su come creare un&#39;app Windows (.appx), consultate [Configurare il progetto Visual Studio e creare l&#39;app](/help/forms/using/setup-visual-studio-project-build-installer.md)Windows.

Per informazioni dettagliate su come distribuire l&#39;app tramite MDM, consultate [Distribuire  app](/help/forms/using/distribute-mobile-workspace-app.md)AEM Forms. La distribuzione delle app tramite MDM è applicabile solo per iOS e Android.

## Recommendations per aggiornare Mobile Workspace all&#39;app AEM Forms  {#recommendations-to-upgrade-mobile-workspace-to-aem-forms-app}

Se state effettuando l&#39;aggiornamento alla versione più recente &#39;app AEM Forms, accertatevi di leggere i punti seguenti:

* **Se avete installato una versione precedente dell&#39;app dallo store Play su Android** Potete aggiornare l&#39;app direttamente dallo store Play.

* **Se la versione precedente dell&#39;app è creata e installata utilizzando il codice sorgente (applicabile per iOS e Android)**:

   Prima di installare la nuova app, sincronizzate tutti i dati con il server AEM Forms . Una volta sincronizzati i dati, disinstallate la versione precedente dell&#39;app e installate la nuova app.

