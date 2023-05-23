---
title: app AEM Forms
seo-title: AEM Forms app
description: L’app AEM Forms consente ai lavoratori sul campo di utilizzare moduli adattivi sui loro dispositivi mobili.
seo-description: AEM Forms app enables your field workers to use adaptive forms on their mobile devices.
uuid: fac976c8-b713-4492-b153-f567e7a11ceb
contentOwner: sashanka
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: e18aa345-034c-473b-b4c2-01678bb10616
exl-id: 171754a2-1ba5-42dc-b6d2-3d730807cc31
source-git-commit: 63f066013c34a5994e2c6a534d88db0c464cc905
workflow-type: tm+mt
source-wordcount: '2450'
ht-degree: 2%

---

# Introduzione all’app AEM Forms {#aem-forms-app}

## Panoramica {#overview}

L’app AEM Forms consente la sincronizzazione di moduli adattivi, moduli mobili e set di moduli su dispositivi mobili, in base al server. Puoi definire flussi di lavoro che sono [Flussi di lavoro incentrati su Forms su OSGi](/help/forms/using/aem-forms-workflow.md) o Forms in JEE. Ad esempio, puoi gestire una società bancaria e utilizzare AEM Forms per gestire le applicazioni e le comunicazioni dei clienti. I clienti compilano un modulo e lo inviano per la verifica. Se abiliti il modulo su dispositivi mobili, i clienti possono compilarlo nell’app AEM Forms. Puoi anche gestire il flusso di lavoro di verifica abilitando il modulo di verifica su dispositivi mobili. Il tuo operatore sul campo può portare un dispositivo mobile al cliente, verificare i dettagli e inviare il modulo. L’app AEM Forms si sincronizza con il server AEM Forms e recupera i moduli abilitati per i dispositivi mobili. Se l’app è offline, memorizza i dati localmente.

Il codice sorgente dell’app AEM Forms è disponibile per i clienti tramite Software Distribution. Il pacchetto del codice sorgente in Distribuzione di software è disponibile come: `adobe-aemfd-forms-app-src-pkg-<version>.zip`.

L&#39;app AEM Forms è supportata su dispositivi iOS, Android e Windows. Puoi installare l’app AEM Forms per Android da Google Play, iOS da App Store e Windows da Windows Store.

    [ ![google_play](assets/google_play.png)](https://play.google.com/store/apps/details?id=com.adobe.aem.forms)
    
    [![app_store](assets/app_store.png)](https://itunes.apple.com/us/app/adobe-experience-manager-forms/id1129625976?ls=1&amp;mt=8)
    
    [![microsoft-badge-icon](assets/microsoft-badge-icon.png)](https://www.microsoft.com/en-us/store/p/adobe-experience-manager-forms/9nd12rlxtgtt)

Per installare, personalizzare e distribuire l&#39;app su dispositivi iOS, Android o Windows, vedi [Personalizzare, generare e distribuire l’app AEM Forms](#customize-build-distribute).

## Prerequisiti {#prerequisites}

L&#39;app AEM Forms richiede un server AEM Forms. Gli utenti possono eseguire il rendering dei moduli creati nel server AEM Forms, compilarli, salvarli come bozze e inviarli. L’app si connette al server e recupera i moduli abilitati da esso. L’app AEM Forms si sincronizza con il server e non appena i moduli vengono caricati nell’app, gli utenti possono lavorare offline. Se l&#39;app è offline, i dati vengono salvati sul dispositivo e sincronizzati con il server quando l&#39;app è online.

### App AEM Forms con server tramite Flusso di lavoro AEM Forms {#aem-forms-app-with-servers-using-aem-forms-workflow}

Se disponi di un server flusso di lavoro AEM Forms, puoi eseguire il rendering dei moduli come attività nell’app AEM Forms. Ad esempio, si esegue una società bancaria e il cliente compila un&#39;applicazione per utilizzare i servizi. L’applicazione è un modulo adattivo che accetta informazioni dai clienti e le memorizza come inoltro per la revisione. L&#39;amministratore esamina un&#39;applicazione e inoltra una richiesta di verifica al processo di lavoro sul campo. L’applicazione inoltrata abilita un modulo di verifica nell’app del lavoratore sul campo come attività. Il lavoratore sul campo invia il dispositivo mobile al cliente e verifica i dettagli.

### App AEM Forms con server che utilizzano un flusso di lavoro incentrato su Forms su OSGi {#aem-forms-app-with-servers-using-forms-centric-workflow-on-osgi}

Se disponi di un server AEM Forms, puoi eseguire il rendering dei moduli adattivi come applicazione Casella in entrata AEM e come attività nell’app AEM Forms. Ad esempio, si esegue una società bancaria e il cliente compila un&#39;applicazione per utilizzare i servizi. L’applicazione è associata a un modulo adattivo che accetta informazioni dai clienti e le memorizza come inoltro per la revisione. L&#39;amministratore rivede l&#39;attività e approva la richiesta di verifica al processo di lavoro sul campo. Il lavoratore sul campo invia il dispositivo mobile al cliente e verifica i dettagli.

### Moduli autonomi o app AEM Forms con server senza flusso di lavoro AEM Forms {#standalone-forms-or-aem-forms-app-with-servers-without-aem-forms-workflow}

Un server AEM Forms che non utilizza AEM Forms Workflow è AEM Forms su OSGi, un modulo mobile standalone o un modulo adattivo. L’app AEM Forms funziona con l’implementazione di AEM Forms su [OSGi](/help/sites-deploying/configuring-osgi.md). I Forms che abiliti e pubblichi per l’app AEM Forms sono disponibili nella tua app.

I moduli vengono scaricati nell’app e sono disponibili offline. Si supponga ad esempio di gestire una società bancaria e che un cliente riempia un&#39;applicazione sul sito. L’applicazione è un modulo adattivo che accetta informazioni dai clienti e le memorizza per la revisione. L’amministratore rivede il modulo e crea un modulo di verifica nell’istanza di authoring AEM. L’amministratore abilita la sincronizzazione del modulo con l’app AEM Forms e lo pubblica. Se il modulo di verifica è disponibile nell’app AEM Forms, l’agente sul campo può utilizzare un dispositivo mobile per verificare i dettagli del cliente. Il dispositivo mobile si sincronizza con il server e il modulo di verifica viene caricato nell’app. L’agente sul campo può visitare il cliente, verificare i dettagli, salvare i dati come bozza o inviare il modulo di verifica. Il modulo viene sincronizzato con il server ogni volta che l&#39;app è online.

Per sincronizzare il modulo nell’app AEM Forms:

1. Nell’istanza di authoring, seleziona un modulo e fai clic su **[!UICONTROL Visualizza proprietà]**.

1. Nella pagina delle proprietà, fai clic su **[!UICONTROL Avanzate]**.
1. In Avanzate, abilita opzione: **[!UICONTROL Sincronizza con l’app AEM Forms]** e tocca **[!UICONTROL Salva]**.

Quando il modulo viene pubblicato, l’app si sincronizza con il server e recupera il modulo. Per sincronizzare più moduli, nell’istanza di authoring seleziona più moduli in Forms Manager e tocca **[!UICONTROL Sincronizza con l’app AEM Forms]**.

## Supporto per dispositivi mobili {#mobile-device-support}

Consulta [App AEM Forms (precedentemente nota come Mobile Workspace)](/help/forms/using/aem-forms-jee-supported-platforms.md#aem-forms-workspace-app)

## Funzioni chiave dell’app AEM Forms {#key-features-of-aem-forms-app}

### App AEM Forms con server AEM Forms {#aem-forms-app-with-aem-forms-servers}

Puoi sincronizzare la tua app con il server AEM Forms e lavorare con i moduli sul tuo dispositivo mobile.

Con il server di AEM Forms Workflow, un modulo può essere associato a un punto d’inizio in un processo di Workbench e a un’applicazione Casella in entrata AEM. A un’applicazione Casella in entrata AEM può essere associato un modulo adattivo. A un punto iniziale può essere associato un modulo adattivo, un modulo HTML5 o un set di moduli. È possibile inviare un punto d&#39;inizio come attività oppure salvare l&#39;attività come bozza. Per ulteriori informazioni sulle differenze tra un’applicazione Casella in entrata AEM e un punto d’inizio, consulta [Azioni e funzionalità dei flussi di lavoro AEM basati su moduli sui flussi di lavoro OSGi e AEM Forms JEE](capabilities-osgi-jee-workflows.md).

Con il server di AEM Forms senza il flusso di lavoro di AEM Forms, nell’app di AEM Forms viene eseguito il rendering di un modulo abilitato per la sincronizzazione nell’app. I Forms sono disponibili nella scheda Forms dell’app, possono essere inviati o salvati come bozza. I moduli adattivi e i moduli mobili sono supportati nell’app.

1. **Salvataggio di un&#39;attività o di un modulo come bozza**

   L’opzione Salva come bozza consente di salvare un’istantanea di un’attività o di un modulo insieme ai dati compilati e ai file allegati al modulo associato. Le bozze vengono salvate sul dispositivo mobile e sincronizzate con il server AEM Forms per un recupero successivo.

   Consulta [Salvataggio di un&#39;attività o di un modulo come bozza](/help/forms/using/save-as-draft.md).

1. **Salva modulo come modello**

   A volte, quando gli utenti compilano un modulo, gli input per alcuni campi rimangono gli stessi. Per tali istanze, è possibile compilare i campi che richiedono valori identici in ogni istanza e salvare il modulo o la bozza come modello. Ora, ogni volta che crei un’istanza del modello, i campi specificati sono già compilati con i valori specificati nel modello. Consente di risparmiare tempo e fatica per compilare il modulo.

   Consulta [Salva moduli come modelli](/help/forms/using/save-forms-and-start-points-as-templates.md).

### Utilizzo di attività e moduli {#working-with-tasks-and-forms}

Puoi sincronizzare l’app con il server Flusso di lavoro di AEM Forms e lavorare su attività e moduli sul tuo dispositivo mobile.

Un’attività sul dispositivo mobile contiene un modulo adattivo, un modulo HTML5 o un set di moduli e può anche contenere allegati e [URL di riepilogo](/help/forms/using/getting-task-variables-summary-url.md). Per impostazione predefinita, le attività a te assegnate vengono inserite in **[!UICONTROL Attività]** cartella. Quando si lavora su un’attività, è possibile modificarla e salvare una bozza di copia dell’attività sul server AEM Forms.

Un modulo sul dispositivo mobile può essere un modulo adattivo o mobile. I Forms abilitati per la sincronizzazione nell’app forms sono disponibili nella cartella Forms. Puoi sincronizzare i moduli abilitati nel server AEM Forms senza il flusso di lavoro di AEM Forms (AEM Forms su OSGi).

Consulta:

* [Apertura di un’attività](/help/forms/using/open-task.md)
* [Utilizzo di un modulo](/help/forms/using/working-with-form.md)

### Utilizzo non in linea {#working-offline}

Puoi lavorare sul tuo dispositivo mobile in modalità offline. È possibile accedere all&#39;applicazione anche in assenza di connettività di rete e utilizzare tutti i moduli sincronizzati con il dispositivo quando si è connessi l&#39;ultima volta. Per informazioni dettagliate su come sincronizzare i moduli, vedi [Sincronizzazione dell’app](/help/forms/using/sync-app.md). Se si sceglie di sincronizzare gli allegati associati a un modulo, è possibile aprire gli allegati anche in modalità non in linea. È possibile modificare il modulo, aggiungere annotazioni e inviare o salvare un modulo in modalità offline. Il modulo viene sincronizzato con il server AEM Forms alla successiva connessione.

Per ulteriori informazioni, consulta [Utilizzo della modalità offline](/help/forms/using/work-offline-mode.md).

### Aggiunta di annotazioni {#adding-annotations}

È possibile aggiungere i seguenti allegati a un modulo sul dispositivo mobile

* **Note**- È possibile utilizzare la funzione Note per aggiungere uno scarabocchio a mano libera o una nota di testo nel modulo. Per ulteriori informazioni, consulta [Aggiunta di una nota](/help/forms/using/add-attachments.md#adding-a-note).

* **Immagine**- L’app AEM Forms include una funzione che utilizza le funzionalità della fotocamera o la galleria del tuo dispositivo mobile. Utilizzando l&#39;allegato della fotografia, è possibile aggiungere una fotografia con il modulo associato. Per ulteriori informazioni, consulta [Aggiunta di una fotografia](/help/forms/using/add-attachments.md#adding-a-photograph).

### Salvataggio automatico {#autosave}

Quando un utente immette dati nell’app AEM Forms, la funzione di salvataggio automatico li salva a intervalli regolari. La funzione di salvataggio automatico nell’app AEM Forms ti aiuta a evitare la perdita di dati se l’app si chiude a causa di condizioni come la batteria scarica.

Consulta [Utilizzo del salvataggio automatico nell’app AEM Forms](/help/forms/using/autosave-data-app.md).

## Differenze tra la casella in entrata dell’AEM e le funzioni dell’app AEM Forms {#differences-between-aem-inbox-and-aem-forms-app-features}

Due dei modi principali per avviare un flusso di lavoro incentrato su Forms sono [Casella in entrata AEM](/help/forms/using/manage-applications-inbox.md) e l&#39;app AEM Forms. Tuttavia, le funzionalità della casella in entrata dell’AEM e dell’app AEM Forms sono diverse. La casella in entrata AEM funziona solo con [Flussi di lavoro incentrati su Forms](/help/forms/using/aem-forms-workflow.md) l’app AEM Forms funziona sia con flussi di lavoro incentrati su Forms che con la gestione dei processi. Per ulteriori informazioni sulle differenze tra la casella in entrata dell’AEM e le funzionalità delle app AEM Forms, consulta [Azioni e funzionalità dei flussi di lavoro AEM basati su moduli sui flussi di lavoro OSGi e AEM Forms JEE](capabilities-osgi-jee-workflows.md).

## Moduli supportati {#supported-forms}

Tipi di moduli supportati nell’app AEM Forms:

### Modulo adattivo {#adaptive-form}

Nell’app AEM Forms è supportato un modulo adattivo che si adatta dinamicamente agli input dell’utente. Sono supportati anche i moduli adattivi con caricamento lazy.

### Modulo mobile {#mobile-form}

Puoi creare moduli per dispositivi mobili in AEM Forms. I moduli mobili vengono riprodotti come moduli HTML nei dispositivi mobili che si adattano in base ai dispositivi di visualizzazione.

### Set di moduli {#formset}

Con i set di moduli, è possibile raggruppare più moduli relativi a un servizio o a un processo per automatizzare un processo aziendale e presentarli agli utenti finali. In questo caso, gli utenti possono compilare l’intero set in un’unica soluzione e non è necessario archiviare, inviare e tenere traccia di singoli moduli o processi.

>[!NOTE]
>
>Richiede AEM Forms Workflow (AEM Forms su JEE).

## Come funziona l’app AEM Forms {#how-aem-forms-app-works}

L’app AEM Forms fornisce una soluzione mobile che consente ai lavoratori sul campo di lavorare sui moduli loro assegnati. L’applicazione memorizza nella cache i dati completi dal server e offre un’esperienza utente efficiente salvando tutto il lavoro localmente. I dati del disco vengono inviati al server tramite aggiornamenti di sincronizzazione tempestivi.

L’app AEM Forms è un’applicazione basata su PhoneGap 5.0 in cui il modello Backbone viene utilizzato in modo efficiente per presentare i dati memorizzati nei modelli tramite le viste. Tutte le operazioni native vengono eseguite tramite i plug-in PhoneGap.

## Personalizzare, generare e distribuire l’app AEM Forms {#customize-build-distribute}

>[!NOTE]
>
>Applicabile solo se per generare l’app utilizzi il codice sorgente dell’app AEM Forms.

L’app AEM Forms è facile da personalizzare in base alle esigenze specifiche dell’organizzazione. Il codice sorgente dell’applicazione viene fornito insieme ad AEM Forms. Puoi modificare il codice sorgente e creare una soluzione personalizzata per la forza lavoro mobile. Puoi anche firmare l’app con la tua chiave Enterprise.

### Personalizzazione {#customize}

Puoi personalizzare l’app per:

**Marchio**: modifica l’icona dell’app, il nome dell’app, le immagini e le pagine di avvio nell’app AEM Forms. Puoi anche modificare il testo per localizzare l’app per un’area specifica. Per ulteriori informazioni sul branding dell’app AEM Forms, consulta [Personalizzazione del branding](/help/forms/using/branding-customization.md).

**Tema**: modifica gli stili, ad esempio colori, font e spaziatura, nell’interfaccia utente dell’app AEM Forms. Per ulteriori informazioni, consulta [Personalizzazione del tema](/help/forms/using/theme-customization.md).

**Gesto**: modifica i movimenti come scorri verso destra e scorri verso sinistra nell’interfaccia utente dell’app AEM Forms. Per ulteriori informazioni, consulta [Personalizzazione del gesto](/help/forms/using/gesture-customization.md).

Per ulteriori informazioni sulla configurazione di un progetto di app AEM Forms per la personalizzazione, consulta:

* [Configurare l’ambiente per l’app AEM Forms](/help/forms/using/setup-environment-mobile-workspace.md)
* [Configurare il progetto Visual Studio e creare l&#39;app Windows](/help/forms/using/setup-visual-studio-project-build-installer.md)
* [Configurare il progetto Xcode e creare l’app iOS](/help/forms/using/setup-xcode-project-build-installer.md)
* [Configurare il progetto Eclipse e creare l’app Android](/help/forms/using/setup-eclipse-project-build-installer.md)

### Creare e distribuire {#build-and-distribute}

Il codice sorgente dell’app AEM Forms può essere estratto dal file `adobe-lc-mobileworkspace-src.zip` che è disponibile come parte del pacchetto sorgente dell’app AEM Forms sulla Distribuzione di software.

Per ottenere l’origine dell’app AEM Forms, effettua le seguenti operazioni:

1. Apri [Software Distribution](https://experience.adobe.com/downloads). Per accedere a Software Distribution è necessario disporre di un Adobe ID.
1. Tocca **[!UICONTROL Adobe Experience Manager]** che si trova nel menu di intestazione.
1. In **[!UICONTROL Filtri]** sezione:
   1. Seleziona **[!UICONTROL Forms]** dal **[!UICONTROL Soluzione]** elenco a discesa.
   2. Seleziona la versione e digita per il pacchetto. È inoltre possibile utilizzare **[!UICONTROL Cerca download]** per filtrare i risultati.
1. Tocca il nome del pacchetto applicabile al sistema operativo in uso, quindi seleziona **[!UICONTROL Accetta termini EULA]**, e tocca **[!UICONTROL Scarica]**.
1. Apri [Gestione pacchetti](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=it) e fai clic su **[!UICONTROL Carica pacchetto]** per caricarlo.
1. Seleziona il pacchetto e fai clic su **[!UICONTROL Installa]**.

**Per iOS**:

Per informazioni dettagliate su come creare un’app iOS (.ipa), consulta [Configurare il progetto Xcode e creare l’app iOS](/help/forms/using/setup-xcode-project-build-installer.md).

Per informazioni dettagliate su come firmare l’app AEM Forms con il tuo profilo di provisioning, consulta [Configurazione, processo e risoluzione dei problemi di iOS Code Signing](https://developer.apple.com/support/code-signing/).

**Per Android**:

Per informazioni dettagliate su come creare un’app Android (con estensione apk), consulta [Configurare il progetto Eclipse e creare l’app Android](/help/forms/using/setup-eclipse-project-build-installer.md).

Per informazioni dettagliate su come firmare l’app AEM Forms, consulta [Firma delle applicazioni](https://developer.android.com/tools/publishing/app-signing.html).

**Per Windows**:

Per informazioni dettagliate su come creare un&#39;app Windows (.appx), fare riferimento a [Configurare il progetto Visual Studio e creare l&#39;app Windows](/help/forms/using/setup-visual-studio-project-build-installer.md).

Per informazioni dettagliate su come distribuire l’app tramite MDM, consulta [Distribuire l’app AEM Forms](/help/forms/using/distribute-mobile-workspace-app.md). La distribuzione delle app tramite MDM è applicabile solo per iOS e Android.

## Recommendations per aggiornare Mobile Workspace all’app AEM Forms {#recommendations-to-upgrade-mobile-workspace-to-aem-forms-app}

Se stai effettuando l’aggiornamento alla versione più recente dell’app AEM Forms, assicurati di aver letto i seguenti punti:

* **Se hai installato una versione precedente dell’app da Play Store su Android**
Puoi aggiornare l’app direttamente dal play store.

* **Se la versione precedente dell’app viene generata e installata utilizzando il codice sorgente (applicabile per iOS e Android)**:

   Prima di installare la nuova app, sincronizza tutti i dati con il server AEM Forms. Dopo aver sincronizzato i dati, disinstalla la versione precedente dell’app e installa la nuova app.
