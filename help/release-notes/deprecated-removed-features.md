---
title: Funzioni obsolete e rimosse in Adobe Experience Manager versione 6.5.
description: Note sulla versione specifiche per le funzioni obsolete e rimosse in Adobe Experience Manager 6.5.
exl-id: d9b6140a-c37d-4b90-a60c-01f471d65621
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
source-git-commit: 191c4b02274ca7e3e9d4622b72cd585870581f47
workflow-type: tm+mt
source-wordcount: '1747'
ht-degree: 10%

---

# Funzioni obsolete e rimosse {#deprecated-and-removed-features}

<!-- Search&Promote is end-of-life September 1, 2022 | Assets | If a user does not have sufficient (read and write) permissions on `/content/dam/collections`, the user cannot create a Collection. | Honor the access control setup of user and ensure appropriate permissions. ||
|Adobe Search & Promote|The integration with Adobe Search & Promote is deprecated. Adobe does not plan to make further enhancements to the Search & Promote integration. Adobe Search & Promote integration remains fully supported while being deprecated.||| -->

Adobe valuta costantemente le funzionalità dei prodotti per reinventare o sostituire nel tempo le funzioni meno recenti con alternative più moderne al fine di migliorare il valore complessivo per il cliente, tenendo comunque in considerazione la compatibilità con le versioni precedenti.

Per comunicare l’imminente rimozione o sostituzione delle funzionalità Adobe Experience Manager (AEM), si applicano le seguenti regole:

1. Innanzitutto viene annunciato che una data funzione diventa obsoleta. Anche se obsolete, le funzionalità sono ancora disponibili ma non vengono ulteriormente migliorate.
1. La rimozione delle funzionalità obsolete avviene non prima della versione principale successiva. La data effettiva di rimozione verrà annunciata in seguito.

Questo processo offre ai clienti almeno un ciclo di rilascio per adattare la loro implementazione a una nuova versione o alla funzionalità che prenderà il posto di quella dichiarata obsoleta, prima che venga definitivamente rimossa.

## Funzioni obsolete {#deprecated-features}

In questa sezione sono elencate le funzionalità contrassegnate come obsolete con AEM 6.5. In genere, le funzioni pianificate per la rimozione in una versione futura vengono inizialmente impostate come obsolete e ne viene indicata un’alternativa.

Consigliamo ai clienti di verificare se utilizzano la funzione/funzionalità nella loro implementazione corrente e di pianificarne la modifica adottando l’alternativa fornita.

| Area | Funzione obsoleta | Sostituzione | Versione (SP) |
|---|---|---|---|
|   |   |   |   |
| Sites | Il servizio **Configurazione polling gestito AEM** di Adobe: `com.day.cq.polling.importer.impl.ManagedPollConfigImpl` | Il servizio **Importazione Sling del report di Adobe AEM Analytics**. Consulta Connessione ad Adobe Analytics e creazione di framework - [Configurazione dell&#39;intervallo di importazione](/help/sites-administering/adobeanalytics-connect.md#configuring-the-import-interval) | 6.5.19.0 |
| Screens | ActiveMQ in Adobe Experience Manager (AEM). ActiveMQ è stato utilizzato per la comunicazione tra due istanze di AEM Publish. | Adobe consiglia ai clienti di utilizzare ora un load balancer. | 6.5.18.0 |
| Proprietà di Frammenti di esperienza per **Stato social media**. |   | 6.5.11.0 |
| [!DNL Sites] | Modelli per frammenti di contenuto, per creare frammenti di contenuto semplici. | [Frammenti di contenuto strutturati basati su modelli](/help/assets/content-fragments/content-fragments-models.md) ora. | 6.5.11.0 |
| Integrazione Creative Cloud | L’AEM per la condivisione delle cartelle di Creative Cloud è stato introdotto nell’AEM 6.2. Consente agli utenti creativi di accedere alle risorse dell&#39;AEM in modo che possano aprirle nelle applicazioni [!DNL Creative Cloud] e caricare nuovi file o salvare le modifiche all&#39;AEM. Una nuova funzionalità rilasciata nell’applicazione Creative Cloud, Adobe Asset Link, offre una migliore esperienza utente e un accesso più efficace alle risorse dall’AEM direttamente da Photoshop, InDesign e Illustrator. Adobe non prevede di apportare ulteriori miglioramenti all’integrazione di Condivisione Creative Cloud cartelle con l’AEM. Sebbene la funzione sia inclusa nell’AEM, si consiglia ai clienti di utilizzare soluzioni sostitutive. | Si consiglia ai clienti di passare alle nuove funzionalità di integrazione Creative Cloud, incluso Adobe Asset Link o l’app desktop AEM. |  |
| Risorse | `AssetDownloadServlet` è disabilitato per impostazione predefinita per le istanze di pubblicazione. Per ulteriori dettagli, vedere [Elenco di controllo della sicurezza AEM](/help/sites-administering/security-checklist.md). | Configurazione descritta in [Elenco di controllo della sicurezza AEM](/help/sites-administering/security-checklist.md). |  |
| Integrazioni | Opt-in **degli Experienci Manager Cloud Service della schermata** è obsoleto poiché l&#39;integrazione di [!DNL Experience Manager] e [!DNL Adobe Target] è stata aggiornata in [!DNL Experience Manager] 6.5. L’integrazione supporta l’API di Adobe Target Standard. L&#39;API utilizza l&#39;autenticazione tramite Adobe IMS e [!DNL Adobe I/O Runtime]. Supporta il ruolo crescente di Adobe Launch per lo strumento di [!DNL Experience Manager] pagine per analisi e personalizzazione. La procedura guidata di consenso è funzionalmente irrilevante. | Configurare le connessioni di sistema, l&#39;autenticazione Adobe IMS e le integrazioni [!DNL Adobe I/O Runtime] tramite i rispettivi servizi cloud [!DNL Experience Manager]. | 6.5.7.0 |
| Connettori | Il connettore Adobe JCR per Microsoft® SharePoint 2010 e Microsoft® SharePoint 2013 è obsoleto per [!DNL Experience Manager] 6.5. | N/D |  |
| Dynamic Tag Manager (DTM) | L’integrazione con DTM è stata dichiarata obsoleta. | Passa a utilizzare Adobe Experience Platform Launch come gestore di tag. |   |
| Adobe Target | Aggiungendo la possibilità per l&#39;AEM di connettersi al servizio Adobe Target utilizzando l&#39;API Adobe Target Standard basata su [!DNL Adobe I/O] (Rest API) in AEM 6.5, il metodo API di Target Classic (XML) è diventato obsoleto. | Riconfigura l&#39;integrazione in [utilizza la nuova API](/help/sites-administering/target.md). |  |
| Adobe Target | L&#39;utilizzo dell&#39;integrazione basata su `mbox.js` con Adobe Target nell&#39;AEM è obsoleto. | Passa a utilizzare `at.js` 1.x. |  |
| Commerce | [CIF REST](https://github.com/adobe/commerce-cif-api) è stato fornito nel 2018 come set di microservizi per abilitare le integrazioni tra AEM e motori commerce. Dopo che Adobe ha acquisito Adobe Commerce (precedentemente Magento) a metà del 2018, Adobe ha deciso di cambiare il suo approccio per due motivi. Commerce dispone di un proprio set di API Commerce (REST e GraphQL) e non è buona prassi mantenere due set di API. Le tendenze del mercato indicano che i clienti si stavano muovendo verso GraphQL, perché è un modo più efficiente di interrogare i dati. Nel 2019, Adobe ha rilasciato la nuova Commerce integration framework utilizzando le API GraphQL di Commerce come fonte di verità. Adobe non prevede di effettuare ulteriori investimenti nell&#39;CIF REST. Si consiglia ai clienti di utilizzare la soluzione sostitutiva. | Per le integrazioni AEM-Commerce, passare a [AEM CIF Archetipo](https://github.com/adobe/aem-cif-project-archetype) e [AEM CIF Componenti core](https://github.com/adobe/aem-core-cif-components). Consulta Integrazione di AEM e Adobe Commerce [con Commerce integration framework](/help/commerce/cif/integrating/magento.md). Il supporto per le integrazioni di terze parti (diverse da Commerce) con il nuovo approccio è nella roadmap di Adobe. |  |
| Componenti (AEM Sites) | Adobe non prevede di apportare ulteriori miglioramenti alla maggior parte dei componenti di base archiviati in `/libs/foundation/components`. Cercare le proprietà `cq:deprecated` e `cq:deprecatedReason` nella cartella dei componenti. AEM 6.5 include i Componenti di base e i clienti che eseguono l’aggiornamento da versioni precedenti possono continuare a utilizzarli così come sono. Inoltre, i Componenti di base sono supportati anche se obsoleti. | Adobe consiglia di utilizzare i Componenti core per i progetti futuri. I siti esistenti possono rimanere invariati oppure utilizzare la [Suite di strumenti di modernizzazione AEM](https://github.com/adobe/aem-modernize-tools) per eseguire il refactoring del sito in modo da utilizzare i Componenti core. |  |
| Componenti (AEM Sites) | I componenti Importazione progettazione `/libs/wcm/designimporter/components` sono stati contrassegnati come obsoleti a partire dalla versione 6.5. Adobe non intende apportare ulteriori miglioramenti a tale implementazione dell’importazione di progetti. | Adobe prevede di fornire un’implementazione alternativa del caso d’uso nelle versioni future. |  |
| Foundation | Framework di offload Granite. Adobe non prevede di apportare ulteriori miglioramenti al framework di offload introdotto in CQ 5.6.1 per esternalizzare l’elaborazione delle risorse. | Adobe sta lavorando a un framework di offload nativo per il cloud di nuova generazione. |  |
| Sviluppatori | `Hobbes.js`. Adobe non prevede di apportare ulteriori miglioramenti al framework di test dell&#39;interfaccia utente `hobbes.js`. | Adobe consiglia ai clienti di utilizzare l’automazione Selenium. |  |
| Sviluppatori | Libreria client dell’interfaccia utente jQuery. Adobe non prevede di gestire e aggiornare ulteriormente la libreria client dell’interfaccia utente jQuery fornita come parte della distribuzione (Quickstart). | Adobe consiglia ai clienti che richiedono ancora l’interfaccia utente jQuery per il codice di aggiungerla alla base di codice del progetto. |  |
| Sviluppatori | Libreria client di animazione jQuery (`granite.jquery.animation`). Adobe non prevede di gestire e aggiornare ulteriormente la libreria client di animazione jQuery fornita come parte della distribuzione (Quickstart). | Adobe consiglia ai clienti che richiedono ancora jQuery Animations per il codice di aggiungerlo alla base di codice del progetto. |  |
| Sviluppatori | Libreria client Handlebars. Adobe non prevede di gestire e aggiornare ulteriormente la libreria client Handlebar fornita come parte della distribuzione (Quickstart). | Adobe consiglia ai clienti che richiedono ancora `Handlebars` per il codice di aggiungerlo alla base di codice del progetto. |  |
| Sviluppatori | Libreria client Lawnchair. Adobe non prevede di mantenere e aggiornare ulteriormente la libreria client Lawnchair fornita come parte della distribuzione (Quickstart). | Adobe consiglia ai clienti che richiedono ancora Lawnchair per il codice di aggiungerlo alla base di codice del progetto. |  |
| Sviluppatori | Libreria client `Granite.Sling.js`. Adobe non prevede di migliorare ulteriormente la libreria client Granite.Sling.js fornita come parte della distribuzione (Quickstart). | Adobe consiglia ai clienti che si affidano alla funzionalità della libreria di eseguire il refactoring del codice per non utilizzarlo più. |  |
| Sviluppatori | Utilizzo dell’interfaccia utente per comprimere/minimizzare le librerie client di JavaScript. Adobe non prevede di aggiornare ulteriormente la libreria YUI. Fino a AEM 6.4, per impostazione predefinita YUI minimizzava JavaScript con l&#39;opzione di passare a Google Closure Compiler (GCC). A partire da AEM 6.5, GCC è il valore predefinito. | Adobe consiglia ai clienti che eseguono l’aggiornamento a AEM 6.5 di passare a GCC per l’implementazione |  |
| Sviluppatori | Editor di finestre di dialogo dell’interfaccia classica in CRXDE Lite. Adobe non prevede di migliorare ulteriormente l’Editor di finestre di dialogo per l’interfaccia classica fornito come parte della distribuzione (Quickstart) | Nessuna sostituzione disponibile. |  |
| Moduli | L’integrazione di AEM Forms con AEM Mobile è stata rimossa. | Nessuna sostituzione disponibile. |
| Sviluppatori | Editor di finestre di dialogo dell’interfaccia classica in CRXDE Lite. Adobe non prevede di migliorare ulteriormente l’Editor di finestre di dialogo per l’interfaccia classica fornito come parte della distribuzione (Quickstart) | Nessuna sostituzione disponibile. |  |
| Sviluppatori | Libreria client lodash/underscore. Adobe non prevede di mantenere e aggiornare ulteriormente la libreria client Lodash/underscore fornita come parte della distribuzione (Quickstart). | Adobe consiglia ai clienti che richiedono ancora Lodash/underscore per il codice di aggiungerlo alla base di codice del progetto. |  |

## Funzioni rimosse {#removed-features}

In questa sezione sono elencate le funzioni e le funzionalità rimosse da AEM 6.5. Le versioni precedenti presentavano queste funzionalità contrassegnate come obsolete.

| Area | Funzione obsoleta | Sostituzione | Versione (SP) |
|--- |--- |--- |--- |
| Commerce | AEM CIF Classic è stato rimosso. | Eseguire la migrazione a [CIF AEM](/help/commerce/cif/migration.md). Se hai ancora bisogno di CIF Classic, è stato creato un pacchetto di compatibilità, [contatta l&#39;Assistenza clienti Adobe](https://experienceleague.adobe.com/it?support-solution=General#support). | 6.5.22.0 |
| Integrazione con [!DNL Experience Cloud] | È possibile sincronizzare le risorse con [!DNL Experience Cloud] utilizzando una configurazione tramite [!DNL Adobe I/O]. [!DNL Adobe Experience Cloud] era precedentemente denominato [!DNL Adobe Experience Cloud]. | In caso di domande, [contatta l&#39;Assistenza clienti Adobe](https://experienceleague.adobe.com/it?support-solution=General#support). |  |
| Activity Map di Analytics | Versione dell’Activity Map inclusa nell’AEM. | In seguito a modifiche di sicurezza nell’API di Adobe Analytics, non è più possibile utilizzare la versione di Activity Map inclusa in AEM. Utilizza il plug-in [ActivityMap fornito da Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/analyze/activity-map/getting-started/get-started-users/activitymap-install.html?lang=it). |  |
| Integrazioni | L’integrazione ExactTarget è stata rimossa dalla distribuzione predefinita (Quickstart) e non è più disponibile. | Nessun sostituto. |  |
| Integrazioni | L&#39;integrazione API di Salesforce Force è stata rimossa dalla distribuzione predefinita (Quickstart) ed è ora un pacchetto aggiuntivo da installare da [Distribuzione software](https://experience.adobe.com/#/downloads/content/software-distribution/it/aem.html). | La funzione è ancora disponibile. |
| Moduli | Adobe Il supporto per il servizio Bridge di migrazione centrale è stato rimosso in quanto il prodotto Adobe Central non è più supportato. | Nessun sostituto. |  |
| Moduli | `com.adobe.fd.df.fdinternal.model.ConfigurationInstance` | Nessun sostituto. |  |
| Moduli | `com.adobe.fd.ccm.channels.print.fdinternal.api.service.PrintDataTransformer` | Nessuna sostituzione |  |
| Moduli | L’aggiornamento single-hop da LiveCycle ES4 SP1 a AEM 6.5 Forms su JEE non è disponibile | Consulta [percorsi di aggiornamento disponibili](../forms/using/upgrade.md) nella documentazione dell&#39;aggiornamento di AEM Forms. |  |
| Moduli | Supporto del clustering basato su UPD rimosso da AEM Forms su JEE | In AEM Forms su JEE è possibile utilizzare solo il clustering basato su TCP. Se si aggiorna un server multicast UDP da una versione precedente a Forms AEM 5.5 su JEE, eseguire le configurazioni manuali per passare al cluster gemfire basato su TCP. Per istruzioni dettagliate, consulta [Aggiornamento ai moduli AEM 6.5 in JEE](../forms/using/upgrade-forms-jee.md) |  |
| Sviluppatori | Firebug Lite è stato rimosso dalla distribuzione predefinita (Quickstart) | Utilizzare le console per sviluppatori integrate nel browser |
| Sviluppatori | Rimuovere il supporto per `customJavaScriptPath` in Gestione librerie client HTML. | Nessuna sostituzione |  |
| [!DNL Assets] | La funzionalità di offload delle risorse è stata rimossa in [!DNL Adobe Experience Manager] 6.5. | Nessuna sostituzione disponibile. |  |
| Cache | `system/console/slingjsp` è stato rimosso e non è più disponibile in AEM 6.5. | La cache di classi e Slightly è memorizzata nel bundle Apache Sling Commons FileSystem ClassLoader. È possibile controllare il numero del bundle nella console Web AEM e rimuovere la cartella della cache direttamente dal file system (`crx-quickstart/launchpad/felix/bundle<ID>`). |  |
| Screens | Rimozione del supporto del bundle activemq e delle relative configurazioni. |  |  |

<!-- ## Pre-announcement for next release {#pre-announcement-for-next-release}

This section is used to pre-announce the upcoming changes in the future releases. The announced changes are not yet effective but will impact customers. For example, the features are not yet deprecated but impacts the users after deprecation. These updates are provided for planning purpose.

|Area|Feature|Announcement|
|--- |--- |--- |
|Foundation|UI Framework|Adobe is planning to deprecate the Coral UI 2 components in 2019. Coral UI 3 was introduced with AEM 6.2, and AEM 6.5 is fully based on Coral 3. Adobe recommends customers and partners that have build custom UIs with Coral 2 to refactored them to Coral 3. Adobe is providing a tool to convert Coral 2 dialogs to Coral 3 - [Read more](/help/sites-developing/modernization-tools.md).|
-->
