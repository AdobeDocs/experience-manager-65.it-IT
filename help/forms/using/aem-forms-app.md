---
title: app AEM Forms
seo-title: AEM Forms app
description: L’app AEM Forms consente ai collaboratori sul campo di utilizzare moduli adattivi sui propri dispositivi mobili.
seo-description: AEM Forms app enables your field workers to use adaptive forms on their mobile devices.
uuid: fac976c8-b713-4492-b153-f567e7a11ceb
contentOwner: sashanka
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: e18aa345-034c-473b-b4c2-01678bb10616
exl-id: 171754a2-1ba5-42dc-b6d2-3d730807cc31
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2452'
ht-degree: 2%

---

# Introduzione all’app AEM Forms {#aem-forms-app}

## Panoramica {#overview}

L’app AEM Forms consente la sincronizzazione di moduli adattivi, moduli mobili e set di moduli su dispositivi mobili, in base al server. Puoi definire i flussi di lavoro [Flussi di lavoro Forms incentrati su OSGi](/help/forms/using/aem-forms-workflow.md) o flussi di lavoro Forms su JEE. Ad esempio, esegui una società bancaria e utilizza AEM Forms per gestire le applicazioni e le comunicazioni dei clienti. I clienti compilano un modulo e lo inviano per la verifica. Se si abilita il modulo su dispositivi mobili, i clienti possono compilarlo nell’app AEM Forms. Puoi anche gestire il flusso di lavoro di verifica abilitando il modulo di verifica su dispositivi mobili. Il lavoratore sul campo può trasportare al cliente un dispositivo mobile, verificare i dettagli e inviare il modulo. L’app AEM Forms si sincronizza con il server AEM Forms e recupera i moduli abilitati per i dispositivi mobili. Se l’app è offline, i dati vengono memorizzati localmente.

Il codice sorgente dell’app AEM Forms è disponibile per i clienti tramite Distribuzione di software. Il pacchetto del codice sorgente in Distribuzione di software è disponibile come segue: `adobe-aemfd-forms-app-src-pkg-<version>.zip`.

L’app AEM Forms è supportata su dispositivi iOS, Android, Windows. Puoi installare l’app AEM Forms per Android da Google Play, iOS da App Store e Windows da Windows Store.

    [ ![google_play](assets/google_play.png)](https://play.google.com/store/apps/details?id=com.adobe.aem.forms)
    
    [ ![app_store](assets/app_store.png)](https://itunes.apple.com/us/app/adobe-experience-manager-forms/id1129625976?ls=1&amp;mt=8)
    
    [ ![microsoft-badge-icon](assets/microsoft-badge-icon.png)](https://www.microsoft.com/en-us/store/p/adobe-experience-manager-forms/9nd12rlxtgtt)

Per installare, personalizzare e distribuire l’app su dispositivi iOS, Android o Windows, vedi [Personalizzare, generare e distribuire l’app AEM Forms](#customize-build-distribute).

## Prerequisiti {#prerequisites}

L&#39;app AEM Forms richiede un server AEM Forms. Gli utenti possono eseguire il rendering dei moduli creati nel server AEM Forms, compilarli, salvarli come bozze e inviarli. L’app si connette al server e recupera i moduli abilitati da esso. L’app AEM Forms viene sincronizzata con il server e, non appena i moduli vengono caricati nell’app, gli utenti possono lavorare offline. Se l’app è offline, i dati vengono salvati sul dispositivo e sincronizzati con il server quando l’app è online.

### App AEM Forms con server che utilizzano il flusso di lavoro AEM Forms {#aem-forms-app-with-servers-using-aem-forms-workflow}

Se disponi di un server AEM Forms Workflow, puoi eseguire il rendering dei moduli come attività nell’app AEM Forms. Ad esempio, si esegue un&#39;azienda bancaria e il cliente compila un&#39;applicazione per utilizzare i propri servizi. L’applicazione è un modulo adattivo che accetta le informazioni dei clienti e le memorizza come invio per la revisione. L&#39;amministratore rivede un&#39;applicazione e inoltra una richiesta di verifica al lavoratore sul campo. L&#39;applicazione inoltrata abilita come attività un modulo di verifica nell&#39;app del lavoratore sul campo. Il lavoratore sul campo trasporta il dispositivo mobile al cliente e verifica i dettagli.

### App AEM Forms con server che utilizzano un flusso di lavoro incentrato su Forms su OSGi {#aem-forms-app-with-servers-using-forms-centric-workflow-on-osgi}

Se disponi di un server AEM Forms, puoi eseguire il rendering dei moduli adattivi come applicazione AEM casella in entrata e come attività nell’app AEM Forms. Ad esempio, si esegue un&#39;azienda bancaria e il cliente compila un&#39;applicazione per utilizzare i propri servizi. L’applicazione è associata a un modulo adattivo che accetta le informazioni dei clienti e le memorizza come invio per la revisione. L&#39;amministratore rivede l&#39;attività e approva la richiesta di verifica al lavoratore sul campo. Il lavoratore sul campo trasporta il dispositivo mobile al cliente e verifica i dettagli.

### Moduli autonomi o app AEM Forms con server senza flusso di lavoro AEM Forms {#standalone-forms-or-aem-forms-app-with-servers-without-aem-forms-workflow}

Un server AEM Forms che non utilizza AEM Forms Workflow è AEM Forms su OSGi o un modulo mobile o adattivo autonomo. L’app AEM Forms funziona con l’implementazione AEM Forms in [OSGi](/help/sites-deploying/configuring-osgi.md). Forms abilitato e pubblicato per l’app AEM Forms sono disponibili nell’app.

I moduli vengono scaricati nell’app e sono disponibili offline. Ad esempio, si esegue un&#39;azienda bancaria e un cliente compila un&#39;applicazione sul sito. L’applicazione è un modulo adattivo che accetta le informazioni dei clienti e le memorizza per la revisione. L’amministratore rivede il modulo e crea un modulo di verifica nell’istanza AEM autore. L’amministratore abilita la sincronizzazione del modulo con l’app AEM Forms e lo pubblica. Se il modulo di verifica è disponibile nell’app AEM Forms, l’agente di campo può utilizzare un dispositivo mobile per verificare i dettagli del cliente. Il dispositivo mobile si sincronizza con il server e il modulo di verifica viene caricato nell’app. L’agente del campo può visitare il cliente, verificare i dettagli, salvare i dati come bozza o inviare il modulo di verifica. Il modulo viene sincronizzato con il server ogni volta che l’app è online.

Per sincronizzare il modulo nell’app AEM Forms:

1. Nell’istanza di authoring, seleziona un modulo e fai clic su **[!UICONTROL Visualizza proprietà]**.

1. Nella pagina delle proprietà, fai clic su **[!UICONTROL Avanzate]**.
1. In Avanzate, abilita l&#39;opzione: **[!UICONTROL Sincronizzazione con l’app AEM Forms]** e toccare **[!UICONTROL Salva]**.

Quando il modulo viene pubblicato, l’app si sincronizza con il server e recupera il modulo. Per sincronizzare più moduli, nell’istanza di authoring, seleziona più moduli in Forms Manager e tocca **[!UICONTROL Sincronizzazione con l’app AEM Forms]**.

## Supporto per dispositivi mobili {#mobile-device-support}

Vedi [App AEM Forms (precedentemente nota come Mobile Workspace)](/help/forms/using/aem-forms-jee-supported-platforms.md#aem-forms-workspace-app)

## Funzioni principali dell’app AEM Forms {#key-features-of-aem-forms-app}

### App AEM Forms con server AEM Forms {#aem-forms-app-with-aem-forms-servers}

Puoi sincronizzare l’app con il server AEM Forms e lavorare con i moduli sul tuo dispositivo mobile.

Con il server AEM Forms Workflow è possibile associare un modulo a un punto di partenza in un processo di workbench e AEM applicazione Inbox. A un&#39;applicazione Casella in entrata AEM può essere associato un modulo adattivo. Un punto iniziale può avere un modulo adattivo, un modulo HTML5 o un set di moduli ad esso associato. È possibile inviare un punto iniziale come attività oppure salvarlo come bozza. Per ulteriori informazioni sulle differenze tra un&#39;applicazione Casella in entrata AEM e un punto iniziale, vedere [Azioni e funzionalità dei flussi di lavoro AEM incentrati sui moduli sui flussi di lavoro OSGi e JEE per AEM Forms](capabilities-osgi-jee-workflows.md).

Con il server AEM Forms senza flusso di lavoro AEM Forms, nell’app AEM Forms viene eseguito il rendering di un modulo abilitato per la sincronizzazione nell’app. Forms è disponibile nella scheda Forms dell’app e può essere inviato o salvato come bozza. I moduli adattivi e i moduli per dispositivi mobili sono supportati nell’app.

1. **Salvataggio di un&#39;attività o di un modulo come bozza**

   L’opzione Salva come bozza consente di salvare un’istantanea di un’attività o di un modulo insieme ai dati compilati e ai file allegati al modulo associato. Le bozze vengono salvate sul dispositivo mobile e sincronizzate con il server AEM Forms per un successivo recupero.

   Vedi [Salvataggio di un&#39;attività o di un modulo come bozza](/help/forms/using/save-as-draft.md).

1. **Salva modulo come modello**

   A volte, quando gli utenti compilano un modulo, gli input per alcuni campi rimangono gli stessi. Per tali istanze, è possibile compilare i campi che richiedono valori identici in ogni istanza e salvare il modulo o la bozza come modello. Ora, ogni volta che crei un’istanza del modello, i campi specificati vengono già compilati con i valori specificati nel modello. Consente di risparmiare tempo e fatica per compilare il modulo.

   Vedi [Salvare i moduli come modelli](/help/forms/using/save-forms-and-start-points-as-templates.md).

### Uso delle attività e dei moduli {#working-with-tasks-and-forms}

Puoi sincronizzare l’app con il server AEM Forms Workflow e lavorare su attività e moduli sul tuo dispositivo mobile.

Un’attività sul dispositivo mobile contiene un modulo adattivo, un modulo HTML5 o un set di moduli e può anche contenere allegati e [URL di riepilogo](/help/forms/using/getting-task-variables-summary-url.md). Per impostazione predefinita, le attività assegnate all&#39;utente vengono posizionate nel **[!UICONTROL Attività]** cartella. Quando si lavora su un&#39;attività, è possibile modificare l&#39;attività e salvare una bozza di copia dell&#39;attività sul server AEM Forms.

Un modulo sul dispositivo mobile può essere un modulo adattivo o mobile. Forms abilitato per la sincronizzazione nell’app dei moduli è disponibile nella cartella Forms. È possibile sincronizzare i moduli abilitati nel server AEM Forms senza flusso di lavoro AEM Forms (AEM Forms su OSGi).

Consulta:

* [Apertura di un’attività](/help/forms/using/open-task.md)
* [Uso di un modulo](/help/forms/using/working-with-form.md)

### Utilizzo offline {#working-offline}

Puoi lavorare sul tuo dispositivo mobile in modalità offline. È possibile accedere all&#39;applicazione anche se non è presente alcuna connettività di rete e può funzionare su tutti i moduli sincronizzati con il dispositivo al momento dell&#39;ultima connessione online. Per informazioni dettagliate sulla sincronizzazione dei moduli, vedere [Sincronizzazione dell’app](/help/forms/using/sync-app.md). Se si sceglie di sincronizzare gli allegati associati a un modulo, è possibile aprire gli allegati anche in modalità offline. È possibile modificare il modulo, aggiungere annotazioni e inviare o salvare un modulo in modalità offline. Al successivo accesso online, il modulo viene sincronizzato con il server AEM Forms.

Per maggiori dettagli, vedi [Utilizzo della modalità offline](/help/forms/using/work-offline-mode.md).

### Aggiunta di annotazioni {#adding-annotations}

È possibile aggiungere i seguenti allegati a un modulo sul dispositivo mobile

* **Note**- È possibile utilizzare la funzione Note per aggiungere uno script a mano libera o una nota di testo nel modulo. Per maggiori dettagli, vedi [Aggiunta di una nota](/help/forms/using/add-attachments.md#adding-a-note).

* **Immagine**- L’app AEM Forms include una funzione che utilizza le funzionalità della fotocamera o la galleria del tuo dispositivo mobile. Utilizzando l’allegato fotografico, è possibile aggiungere una fotografia con il modulo associato. Per maggiori dettagli, vedi [Aggiunta di una fotografia](/help/forms/using/add-attachments.md#adding-a-photograph).

### Salvataggio automatico {#autosave}

Quando un utente immette dei dati nell’app AEM Forms, la funzione di salvataggio automatico li salva a intervalli regolari. La funzione di salvataggio automatico nell’app AEM Forms ti aiuta a evitare la perdita di dati se l’app si chiude a causa di condizioni come la batteria scarica.

Vedi [Utilizzo del salvataggio automatico nell’app AEM Forms](/help/forms/using/autosave-data-app.md).

## Differenze tra AEM casella in entrata e funzioni dell’app AEM Forms {#differences-between-aem-inbox-and-aem-forms-app-features}

Due dei principali modi per avviare un flusso di lavoro incentrato su Forms sono quelli utilizzati [Casella in entrata AEM](/help/forms/using/manage-applications-inbox.md) e l&#39;app AEM Forms. Le funzionalità della casella in entrata AEM e dell’app AEM Forms, tuttavia, differiscono. AEM casella in entrata funziona solo con [Flussi di lavoro incentrati su Forms](/help/forms/using/aem-forms-workflow.md) mentre l’app AEM Forms funziona sia con flussi di lavoro incentrati su Forms che con la gestione dei processi. Per ulteriori informazioni sulle differenze tra le funzionalità della casella in entrata AEM e dell’app AEM Forms, vedi [Azioni e funzionalità dei flussi di lavoro AEM incentrati sui moduli sui flussi di lavoro OSGi e JEE per AEM Forms](capabilities-osgi-jee-workflows.md).

## Moduli supportati {#supported-forms}

Tipi di moduli supportati nell’app AEM Forms:

### Modulo adattivo {#adaptive-form}

Un modulo adattivo che si adatta dinamicamente agli input degli utenti è supportato nell’app AEM Forms. Sono supportati anche i moduli adattivi caricati a priori.

### Modulo mobile {#mobile-form}

È possibile creare moduli per dispositivi mobili in AEM Forms. I moduli per dispositivi mobili sono rappresentati come moduli HTML nei dispositivi mobili che si adattano in base ai dispositivi di visualizzazione.

### Set di moduli {#formset}

Con i set di moduli, è possibile raggruppare più moduli relativi a un servizio o a un processo per automatizzare un processo aziendale e presentarli agli utenti finali. In questo caso, gli utenti possono compilare l’intero set come un unico set e non è necessario archiviare, inviare e tenere traccia dei singoli moduli o processi.

>[!NOTE]
>
>Richiede flusso di lavoro AEM Forms (AEM Forms su JEE).

## Funzionamento dell’app AEM Forms {#how-aem-forms-app-works}

L’app AEM Forms fornisce una soluzione mobile per consentire ai lavoratori sul campo di lavorare sui moduli ad essi assegnati. L&#39;applicazione memorizza in cache i dati completi dal server e fornisce un&#39;esperienza utente efficiente salvando tutto il lavoro localmente. I dati dal disco vengono inviati al server tramite aggiornamenti di sincronizzazione puntuali.

L’app AEM Forms è un’applicazione basata su PhoneGap 5.0 in cui il modello Backbone viene utilizzato in modo efficiente per presentare i dati memorizzati nei modelli attraverso le visualizzazioni. Tutte le operazioni native vengono eseguite tramite plug-in PhoneGap.

## Personalizzare, generare e distribuire l’app AEM Forms {#customize-build-distribute}

>[!NOTE]
>
>Applicabile solo se utilizzi il codice sorgente dell’app AEM Forms per creare l’app.

L’app AEM Forms è facile da personalizzare in base alle esigenze specifiche dell’organizzazione. Il codice sorgente dell’applicazione viene fornito insieme ad AEM Forms. Puoi modificare il codice sorgente e creare la tua soluzione per la forza lavoro mobile. Puoi anche firmare l’app con la tua chiave Enterprise.

### Personalizzazione {#customize}

Puoi personalizzare la tua app per:

**Branding**: Modifica l’icona dell’app, il nome dell’app, le immagini di avvio e le pagine nell’app AEM Forms. Puoi anche modificare il testo per localizzare l’app per una regione specifica. Per ulteriori informazioni sul branding dell’app AEM Forms, vedi [Personalizzazione del branding](/help/forms/using/branding-customization.md).

**Tema**: Modifica stili quali colori, font e spaziatura nell’interfaccia utente dell’app AEM Forms. Per ulteriori informazioni, consulta [Personalizzazione del tema](/help/forms/using/theme-customization.md).

**Gesto**: Modifica i gesti come scorrere a destra e scorrere a sinistra nell&#39;interfaccia utente dell&#39;app AEM Forms. Per ulteriori informazioni, consulta [Personalizzazione dei movimenti](/help/forms/using/gesture-customization.md).

Per ulteriori informazioni sulla configurazione di un progetto di app AEM Forms per la personalizzazione, consulta:

* [Configurare l’ambiente per l’app AEM Forms](/help/forms/using/setup-environment-mobile-workspace.md)
* [Configurazione del progetto Visual Studio e creazione dell&#39;app Windows](/help/forms/using/setup-visual-studio-project-build-installer.md)
* [Configurare il progetto Xcode e creare l’app iOS](/help/forms/using/setup-xcode-project-build-installer.md)
* [Configurare il progetto Eclipse e creare l’app Android](/help/forms/using/setup-eclipse-project-build-installer.md)

### Creare e distribuire {#build-and-distribute}

Il codice sorgente per l’app AEM Forms può essere estratto dal `adobe-lc-mobileworkspace-src.zip` disponibile come parte del pacchetto sorgente dell’app AEM Forms su Distribuzione software.

Per ottenere la sorgente dell’app AEM Forms, esegui i seguenti passaggi:

1. Apri [Software Distribution](https://experience.adobe.com/downloads). Per accedere a Software Distribution è necessario disporre di un Adobe ID.
1. Tocca **[!UICONTROL Adobe Experience Manager]** che si trova nel menu di intestazione.
1. In **[!UICONTROL Filtri]** sezione:
   1. Seleziona **[!UICONTROL Forms]** dal **[!UICONTROL Soluzione]** elenco a discesa.
   2. Seleziona la versione e digita il pacchetto. È inoltre possibile utilizzare **[!UICONTROL Download di ricerca]** per filtrare i risultati.
1. Toccare il nome del pacchetto applicabile al sistema operativo in uso, selezionare **[!UICONTROL Accettare i termini dell&#39;EULA]**, e tocca **[!UICONTROL Scarica]**.
1. Apri [Gestione pacchetti](https://docs.adobe.com/content/help/it/experience-manager-65/administering/contentmanagement/package-manager.html) e fai clic su **[!UICONTROL Carica pacchetto]** per caricarlo.
1. Seleziona il pacchetto e fai clic su **[!UICONTROL Installa]**.

**Per iOS**:

Per informazioni dettagliate su come creare un’app iOS (.ipa), consulta [Configurare il progetto Xcode e creare l&#39;app iOS](/help/forms/using/setup-xcode-project-build-installer.md).

Per informazioni dettagliate su come firmare l’app AEM Forms con il profilo di provisioning, consulta [Configurazione, elaborazione e risoluzione dei problemi della firma del codice iOS](https://developer.apple.com/support/code-signing/).

**Per Android**:

Per informazioni dettagliate su come creare un’app Android (.apk), consulta [Configurare il progetto Eclipse e creare l’app Android](/help/forms/using/setup-eclipse-project-build-installer.md).

Per informazioni dettagliate su come firmare l’app AEM Forms, vedi [Firma delle applicazioni](https://developer.android.com/tools/publishing/app-signing.html).

**Per Windows**:

Per informazioni dettagliate su come creare un’app Windows (.appx), consulta [Configurare il progetto Visual Studio e creare l&#39;app Windows](/help/forms/using/setup-visual-studio-project-build-installer.md).

Per informazioni dettagliate su come distribuire l’app tramite MDM, consulta [Distribuire l’app AEM Forms](/help/forms/using/distribute-mobile-workspace-app.md). La distribuzione dell’app tramite MDM è applicabile solo per iOS e Android.

## Recommendations per aggiornare Mobile Workspace all’app AEM Forms {#recommendations-to-upgrade-mobile-workspace-to-aem-forms-app}

Se effettui l’aggiornamento alla versione più recente dell’app AEM Forms, accertati di leggere i seguenti punti:

* **Se hai installato una versione precedente dell’app dal Play Store su Android**
Puoi aggiornare l’app direttamente dal Play Store.

* **Se la versione precedente dell’app è generata e installata utilizzando il codice sorgente (applicabile per iOS e Android)**:

   Prima di installare la nuova app, sincronizza tutti i dati con il server AEM Forms. Dopo la sincronizzazione dei dati, disinstalla la versione precedente dell&#39;app e installa la nuova app.
