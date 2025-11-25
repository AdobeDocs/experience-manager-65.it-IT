---
title: Funzioni obsolete e rimosse in Adobe Experience Manager versione 6.5.
description: Note sulla versione specifiche per le funzioni obsolete e rimosse in Adobe Experience Manager 6.5.
exl-id: d9b6140a-c37d-4b90-a60c-01f471d65621
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
source-git-commit: 07289e891399a78568dcac957bc089cc08c7898c
workflow-type: tm+mt
source-wordcount: '1765'
ht-degree: 13%

---

# Funzioni obsolete e rimosse {#deprecated-and-removed-features}

<!-- Search&Promote is end-of-life September 1, 2022 | Assets | If a user does not have sufficient (read and write) permissions on `/content/dam/collections`, the user cannot create a Collection. | Honor the access control setup of user and ensure appropriate permissions. ||
|Adobe Search & Promote|The integration with Adobe Search & Promote is deprecated. Adobe does not plan to make further enhancements to the Search & Promote integration. Adobe Search & Promote integration remains fully supported while being deprecated.||| -->

Adobe valuta costantemente le funzionalità dei prodotti per reinventare o sostituire nel tempo le funzioni meno recenti con alternative più moderne al fine di migliorare il valore complessivo per il cliente, tenendo comunque in considerazione la compatibilità con le versioni precedenti.

Per comunicare l’imminente rimozione o sostituzione delle funzionalità di Adobe Experience Manager (AEM), si applicano le seguenti regole:

1. Innanzitutto viene annunciato che una specifica funzione diventerà obsoleta. Anche se obsolete, le funzionalità sono ancora disponibili ma non vengono migliorate ulteriormente.
1. La rimozione delle funzionalità obsolete avviene non prima della versione principale successiva. La data effettiva di rimozione verrà annunciata in seguito.

Questo processo offre alla clientela almeno un ciclo di rilascio per adattare la loro implementazione a una nuova versione o alla funzionalità che prenderà il posto di quella dichiarata obsoleta, prima che venga definitivamente rimossa.

## Funzioni obsolete {#deprecated-features}

In questa sezione sono elencate le funzionalità contrassegnate come obsolete con AEM 6.5. In genere, le funzioni pianificate per la rimozione in una versione futura vengono inizialmente impostate come obsolete e ne viene indicata un’alternativa.

Consigliamo alla clientela di verificare se utilizzano la funzione/funzionalità nella loro implementazione corrente e di pianificarne la modifica adottando l’alternativa fornita.

| Area | Funzione | Sostituzione | Versione (SP) |
|---|---|---|---|
| Sites | [Editor SPA](/help/sites-developing/spa-editor-deprecation.md) | Per i casi d&#39;uso headless, utilizza [Universal Editor](/help/sites-developing/universal-editor/introduction.md) per la modifica visiva o [Content Fragment Editor](/help/sites-developing/universal-editor/introduction.md) per la modifica basata su modulo. | 6.5.23 |
| Sites | Servizio **Configurazione polling gestito di Adobe AEM**: `com.day.cq.polling.importer.impl.ManagedPollConfigImpl` | Il servizio **Importazione Sling per report di Adobe AEM Analytics**. Consulta Connessione ad Adobe Analytics e creazione di framework - [Configurazione dell&#39;intervallo di importazione](/help/sites-administering/adobeanalytics-connect.md#configuring-the-import-interval) | 6.5.19.0 |
| Screens | ActiveMQ in Adobe Experience Manager (AEM). ActiveMQ è stato utilizzato per la comunicazione tra due istanze AEM Publish. | Adobe consiglia ai clienti di utilizzare ora un load balancer. | 6.5.18.0 |
| Proprietà di Frammenti di esperienza per **Stato social media**. | |  | 6.5.11.0 |
| [!DNL Sites] | Modelli per frammenti di contenuto, per creare frammenti di contenuto semplici. | [Frammenti di contenuti strutturati basati su modelli](/help/assets/content-fragments/content-fragments-models.md) ora. | 6.5.11.0 |
| Integrazione di Creative Cloud | La condivisione cartelle da AEM a Creative Cloud è stata introdotta in AEM 6.2. Consente agli utenti creativi di accedere alle risorse da AEM in modo che possano aprirle nelle applicazioni [!DNL Creative Cloud] e caricare nuovi file o salvare le modifiche in AEM. Una nuova funzionalità introdotta nell’applicazione Creative Cloud, Adobe Asset Link, offre una migliore esperienza utente e un accesso più efficace alle risorse da AEM direttamente da Photoshop, InDesign e Illustrator. Adobe non prevede di apportare ulteriori miglioramenti all’integrazione tra AEM e Condivisione cartelle di Creative Cloud. Sebbene la funzione sia inclusa in AEM, si consiglia ai clienti di utilizzare soluzioni sostitutive. | Si consiglia ai clienti di passare alle nuove funzionalità di integrazione di Creative Cloud, incluso Adobe Asset Link o l’app desktop AEM. |  |
| Risorse | `AssetDownloadServlet` è disabilitato per impostazione predefinita per le istanze di pubblicazione. Per ulteriori dettagli, vedere [Elenco di controllo della sicurezza di AEM](/help/sites-administering/security-checklist.md). | Configurazione descritta in [Elenco di controllo della sicurezza di AEM](/help/sites-administering/security-checklist.md). |  |
| Integrazioni | La schermata **[!UICONTROL Opt-in di Experience Manager Cloud Services]** è obsoleta poiché l&#39;integrazione di [!DNL Experience Manager] e [!DNL Adobe Target] è stata aggiornata in [!DNL Experience Manager] 6.5. L’integrazione supporta l’API di Adobe Target Standard. L&#39;API utilizza l&#39;autenticazione tramite Adobe IMS e [!DNL Adobe I/O Runtime]. Supporta il ruolo crescente di Adobe Launch per lo strumento di [!DNL Experience Manager] pagine per analisi e personalizzazione. La procedura guidata di consenso è funzionalmente irrilevante. | Configurare le connessioni di sistema, l&#39;autenticazione Adobe IMS e le integrazioni [!DNL Adobe I/O Runtime] tramite i rispettivi servizi cloud [!DNL Experience Manager]. | 6.5.7.0 |
| Connettori | Il connettore Adobe JCR per Microsoft® SharePoint 2010 e Microsoft® SharePoint 2013 è obsoleto per [!DNL Experience Manager] 6.5. | N/D |  |
| Dynamic Tag Manager (DTM) | L’integrazione con DTM è stata dichiarata obsoleta. | Passa a utilizzare Adobe Experience Platform Launch come gestore di tag. |   |
| Adobe Target | Aggiungendo la possibilità per AEM di connettersi al servizio Adobe Target utilizzando l&#39;API Adobe Target Standard basata su [!DNL Adobe I/O] (Rest API) in AEM 6.5, il metodo API di Target Classic (XML) è diventato obsoleto. | Riconfigura l&#39;integrazione in [utilizza la nuova API](/help/sites-administering/target.md). |  |
| Adobe Target | L&#39;utilizzo dell&#39;integrazione basata su `mbox.js` con Adobe Target in AEM è obsoleto. | Passa a utilizzare `at.js` 1.x. |  |
| Commerce | [CIF REST](https://github.com/adobe/commerce-cif-api) è stato fornito nel 2018 come set di microservizi per abilitare le integrazioni tra AEM e i motori commerce. Dopo che Adobe ha acquisito Adobe Commerce (precedentemente Magento) a metà del 2018, Adobe ha deciso di cambiare il suo approccio per due motivi. Commerce dispone di un proprio set di API Commerce (REST e GraphQL) e non è buona prassi mantenere due set di API. Le tendenze del mercato indicano che i clienti si stavano muovendo verso GraphQL, perché è un modo più efficiente di interrogare i dati. Nel 2019, Adobe ha rilasciato la nuova Commerce integration framework utilizzando le API GraphQL di Commerce come fonte di verità. Adobe non prevede di effettuare ulteriori investimenti in CIF REST. Si consiglia ai clienti di utilizzare la soluzione sostitutiva. | Per le integrazioni AEM-Commerce, passa a [AEM CIF Archetype](https://github.com/adobe/aem-cif-project-archetype) e [AEM CIF Core Components](https://github.com/adobe/aem-core-cif-components). Consulta Integrazione di AEM e Adobe Commerce [con Commerce integration framework](/help/commerce/cif/integrating/magento.md). Il supporto per le integrazioni di terze parti (diverse da Commerce) con il nuovo approccio è nella roadmap di Adobe. |  |
| Componenti (AEM Sites) | Adobe non prevede di apportare ulteriori miglioramenti alla maggior parte dei componenti di base memorizzati in `/libs/foundation/components`. Cercare le proprietà `cq:deprecated` e `cq:deprecatedReason` nella cartella dei componenti. In AEM 6.5 sono inclusi i Componenti di base e i clienti che eseguono l’aggiornamento da versioni precedenti possono continuare a utilizzarli nello stato corrente. Inoltre, i Componenti di base sono supportati anche se obsoleti. | Adobe consiglia di utilizzare i Componenti core per i progetti futuri. I siti esistenti possono rimanere invariati oppure utilizzare la [suite di strumenti di modernizzazione AEM](https://github.com/adobe/aem-modernize-tools) per eseguire il refactoring del sito in modo da utilizzare i Componenti core. |  |
| Componenti (AEM Sites) | I componenti Importazione progettazione `/libs/wcm/designimporter/components` sono stati contrassegnati come obsoleti a partire dalla versione 6.5. Adobe non prevede di apportare ulteriori miglioramenti a tale implementazione dell’importazione progettazione. | Adobe prevede di fornire un’implementazione alternativa del caso d’uso nelle versioni future. |  |
| Foundation | Framework di offload Granite. Adobe non prevede di apportare ulteriori miglioramenti al framework di offload introdotto in CQ 5.6.1 per esternalizzare l’elaborazione delle risorse. | Adobe sta lavorando a un framework di offload nativo per il cloud di nuova generazione. |  |
| Sviluppatori | `Hobbes.js`. Adobe non prevede ulteriori miglioramenti al framework di test dell&#39;interfaccia utente `hobbes.js`. | Adobe consiglia ai clienti di utilizzare l’automazione Selenium. |  |
| Sviluppatori | Libreria client dell’interfaccia utente jQuery. Adobe non prevede di gestire e aggiornare ulteriormente la libreria client dell’interfaccia utente jQuery fornita come parte della distribuzione (Quickstart). | Adobe consiglia ai clienti che richiedono ancora l’interfaccia utente jQuery per il codice di aggiungerla alla base di codice del progetto. |  |
| Sviluppatori | Libreria client di animazione jQuery (`granite.jquery.animation`). Adobe non prevede di mantenere e aggiornare ulteriormente la libreria client jQuery Animation fornita come parte della distribuzione (Quickstart). | Adobe consiglia ai clienti che ancora richiedono jQuery Animations per il codice di aggiungerlo alla base di codice del progetto. |  |
| Sviluppatori | Libreria client Handlebars. Adobe non prevede di gestire e aggiornare ulteriormente la libreria client Handlebar fornita come parte della distribuzione (Quickstart). | Adobe consiglia ai clienti che richiedono ancora `Handlebars` per il codice di aggiungerlo alla base di codice del progetto. |  |
| Sviluppatori | Libreria client Lawnchair. Adobe non prevede di mantenere e aggiornare ulteriormente la libreria client Lawnchair fornita come parte della distribuzione (Quickstart). | Adobe consiglia ai clienti che richiedono ancora Lawnchair per il codice di aggiungerlo alla base di codice del progetto. |  |
| Sviluppatori | Libreria client `Granite.Sling.js`. Adobe non prevede di migliorare ulteriormente la libreria client Granite.Sling.js fornita come parte della distribuzione (Quickstart). | Adobe consiglia ai clienti che si affidano alla funzionalità della libreria di eseguire il refactoring del codice per non utilizzarlo più. |  |
| Sviluppatori | Utilizzo di YUI per comprimere/minimizzare le librerie client di JavaScript. Adobe non prevede di aggiornare ulteriormente la libreria YUI. Fino alla versione 6.4 di AEM, per impostazione predefinita YUI minimizzava JavaScript con l’opzione di passare a Google Closure Compiler (GCC). A partire da AEM 6.5, GCC è l’impostazione predefinita. | Adobe consiglia ai clienti di eseguire l’aggiornamento a AEM 6.5 per passare a GCC per l’implementazione |  |
| Sviluppatori | Editor di finestre di dialogo dell’interfaccia classica in CRXDE Lite. Adobe non prevede di migliorare ulteriormente l’Editor di finestre di dialogo per l’interfaccia classica fornito come parte della distribuzione (Quickstart) | Nessuna sostituzione disponibile. |  |
| Forms | L’integrazione di AEM Forms con AEM Mobile è stata rimossa. | Nessuna sostituzione disponibile. |  |
| Sviluppatori | Editor di finestre di dialogo dell’interfaccia classica in CRXDE Lite. Adobe non prevede di migliorare ulteriormente l’Editor di finestre di dialogo per l’interfaccia classica fornito come parte della distribuzione (Quickstart) | Nessuna sostituzione disponibile. |  |
| Sviluppatori | Libreria client lodash/underscore. Adobe non prevede di mantenere e aggiornare ulteriormente la libreria client Lodash/underscore fornita come parte della distribuzione (Quickstart). | Adobe consiglia ai clienti che richiedono ancora Lodash/underscore per il codice di aggiungerlo alla base di codice del progetto. |  |

## Funzioni rimosse {#removed-features}

In questa sezione sono elencate le funzionalità rimosse da AEM 6.5. Le versioni precedenti presentavano queste funzionalità contrassegnate come obsolete.

| Area | Funzione | Sostituzione | Versione (SP) |
|--- |--- |--- |--- |
| Commerce | AEM CIF Classic è stato rimosso. | Eseguire la migrazione a [AEM CIF](/help/commerce/cif/migration.md). Se hai ancora bisogno di CIF Classic, è stato creato un pacchetto di compatibilità, [contatta l&#39;Assistenza clienti Adobe](https://experienceleague.adobe.com/it?support-solution=General#support). | 6.5.22.0 |
| Integrazione con [!DNL Experience Cloud] | È possibile sincronizzare le risorse con [!DNL Experience Cloud] utilizzando una configurazione tramite [!DNL Adobe I/O]. [!DNL Adobe Experience Cloud] era precedentemente denominato [!DNL Adobe Experience Cloud]. | In caso di domande, [contatta l&#39;Assistenza clienti Adobe](https://experienceleague.adobe.com/it?support-solution=General#support). |  |
| Activity Map di Analytics | Versione di Activity Map inclusa in AEM. | In seguito a modifiche di sicurezza nell’API di Adobe Analytics, non è più possibile utilizzare la versione di Activity Map inclusa in AEM. Utilizza il plug-in [ActivityMap fornito da Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/analyze/activity-map/getting-started/get-started-users/activitymap-install.html?lang=it). |  |
| Integrazioni | L’integrazione ExactTarget è stata rimossa dalla distribuzione predefinita (Quickstart) e non è più disponibile. | Nessun sostituto. |  |
| Integrazioni | L&#39;integrazione API di Salesforce Force è stata rimossa dalla distribuzione predefinita (Quickstart) ed è ora un pacchetto aggiuntivo da installare da [Distribuzione software](https://experience.adobe.com/#/downloads/content/software-distribution/it/aem.html). | La funzione è ancora disponibile. |  |
| Forms | Il supporto per il servizio Adobe Central Migration Bridge è stato rimosso in quanto il prodotto Adobe Central non è più supportato. | Nessun sostituto. |  |
| Forms | `com.adobe.fd.df.fdinternal.model.ConfigurationInstance` | Nessun sostituto. |  |
| Forms | `com.adobe.fd.ccm.channels.print.fdinternal.api.service.PrintDataTransformer` | Nessuna sostituzione |  |
| Forms | L’aggiornamento single-hop da LiveCycle ES4 SP1 ad AEM 6.5 Forms su JEE non è disponibile | Consulta [percorsi di aggiornamento disponibili](../forms/using/upgrade.md) nella documentazione dell&#39;aggiornamento di AEM Forms. |  |
| Forms | Supporto del clustering basato su UPD rimosso da AEM Forms su JEE | In AEM Forms su JEE è possibile utilizzare solo il clustering basato su TCP. Se si aggiorna un server multicast UDP da una versione precedente a AEM 5.5 Forms su JEE, eseguire le configurazioni manuali per passare al clustering gemfire basato su TCP. Per istruzioni dettagliate, consulta [Aggiornamento a AEM 6.5 Forms su JEE](../forms/using/upgrade-forms-jee.md) |  |
| Sviluppatori | Firebug Lite è stato rimosso dalla distribuzione predefinita (Quickstart) | Utilizzare le console per sviluppatori integrate nel browser |  |
| Sviluppatori | Rimuovere il supporto per `customJavaScriptPath` in Gestione librerie client HTML. | Nessuna sostituzione |  |
| [!DNL Assets] | La funzionalità di offload delle risorse è stata rimossa in [!DNL Adobe Experience Manager] 6.5. | Nessuna sostituzione disponibile. |  |
| Cache | `system/console/slingjsp` è stato rimosso e non è più disponibile in AEM 6.5. | La cache di classi e Slightly è memorizzata nel bundle Apache Sling Commons FileSystem ClassLoader. È possibile controllare il numero del bundle nella Console Web AEM e rimuovere la cartella della cache direttamente dal file system (`crx-quickstart/launchpad/felix/bundle<ID>`). |  |
| Screens | Rimozione del supporto del bundle activemq e delle relative configurazioni. |  |  |

<!-- ## Pre-announcement for next release {#pre-announcement-for-next-release}

This section is used to pre-announce the upcoming changes in the future releases. The announced changes are not yet effective but will impact customers. For example, the features are not yet deprecated but impacts the users after deprecation. These updates are provided for planning purpose.

|Area|Feature|Announcement|
|--- |--- |--- |
|Foundation|UI Framework|Adobe is planning to deprecate the Coral UI 2 components in 2019. Coral UI 3 was introduced with AEM 6.2, and AEM 6.5 is fully based on Coral 3. Adobe recommends customers and partners that have build custom UIs with Coral 2 to refactored them to Coral 3. Adobe is providing a tool to convert Coral 2 dialogs to Coral 3 - [Read more](/help/sites-developing/modernization-tools.md).|
-->
