---
title: Funzioni obsolete e rimosse in Adobe Experience Manager versione 6.5.
description: Note sulla versione specifiche per le funzioni obsolete e rimosse in Adobe Experience Manager 6.5.
exl-id: d9b6140a-c37d-4b90-a60c-01f471d65621
source-git-commit: 5c10c5d20338b696fdab2291c714a7d6313cca8a
workflow-type: tm+mt
source-wordcount: '1689'
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
| Sites | Il **Adobe Configurazione polling gestito AEM** servizio: `com.day.cq.polling.importer.impl.ManagedPollConfigImpl` | Il **Adobe Importazione Sling del rapporto di AEM Analytics** servizio. Consulta Collegamento ad Adobe Analytics e creazione di framework - [Configurazione dell&#39;intervallo di importazione](/help/sites-administering/adobeanalytics-connect.md#configuring-the-import-interval) | 6.5.19.0 |
| [!DNL Sites] | Proprietà di Frammenti di esperienza per **Stato social media**. |   | 6.5.11.0 |
| [!DNL Sites] | Modelli per frammenti di contenuto, per creare frammenti di contenuto semplici. | [Frammenti di contenuto strutturati basati su modelli](/help/assets/content-fragments/content-fragments-models.md) ora. | 6.5.11.0 |
| Integrazione Creative Cloud | L’AEM per la condivisione delle cartelle di Creative Cloud è stato introdotto nell’AEM 6.2. Consente agli utenti creativi di accedere alle risorse dell’AEM in modo da poterle aprire in [!DNL Creative Cloud] e caricare nuovi file o salvare le modifiche apportate all&#39;AEM. Una nuova funzionalità rilasciata nell’applicazione Creative Cloud, Adobe Asset Link, offre una migliore esperienza utente e un accesso più efficace alle risorse dall’AEM direttamente da Photoshop, InDesign e Illustrator. Adobe non prevede di apportare ulteriori miglioramenti all’integrazione di Condivisione Creative Cloud cartelle con l’AEM. Sebbene la funzione sia inclusa nell’AEM, si consiglia ai clienti di utilizzare soluzioni sostitutive. | Si consiglia ai clienti di passare alle nuove funzionalità di integrazione Creative Cloud, incluso Adobe Asset Link o l’app desktop AEM. |  |
| Risorse | `AssetDownloadServlet` è disattivato per impostazione predefinita per le istanze di pubblicazione. Per ulteriori dettagli, consulta [Lista di controllo per la sicurezza AEM](/help/sites-administering/security-checklist.md). | Configurazione descritta in [Lista di controllo per la sicurezza dell’AEM](/help/sites-administering/security-checklist.md). |  |
| Integrazioni | Schermata **[!UICONTROL Consenso Experienci Manager Cloud Service]** è obsoleto perché [!DNL Experience Manager] e [!DNL Adobe Target] L’integrazione di è stata aggiornata in [!DNL Experience Manager] 6.5. L’integrazione supporta l’API di Adobe Target Standard. L’API utilizza l’autenticazione tramite Adobe IMS e [!DNL Adobe I/O Runtime]. Sostiene il ruolo crescente del lancio Adobe nello strumento [!DNL Experience Manager] per le pagine di analytics e personalizzazione, la procedura guidata di consenso è funzionalmente irrilevante. | Configurare connessioni di sistema, autenticazione Adobe IMS e [!DNL Adobe I/O Runtime] integrazioni tramite il rispettivo [!DNL Experience Manager] servizi cloud. | 6.5.7.0 |
| Connettori | Il connettore Adobe JCR per Microsoft® SharePoint 2010 e Microsoft® SharePoint 2013 è obsoleto per [!DNL Experience Manager] 6.5 | N/D |  |
| Dynamic Tag Manager (DTM) | L’integrazione con DTM è stata dichiarata obsoleta. | Passa a utilizzare Adobe Experience Platform Launch come gestore di tag. |   |
| Adobe Target | Con l’aggiunta della possibilità per l’AEM di connettersi al servizio Adobe Target utilizzando [!DNL Adobe I/O] basato sull’API Adobe Target Standard (Rest API) nell’AEM 6.5, il metodo API di Target Classic (XML) è obsoleto. | Riconfigura l’integrazione in [utilizza la nuova API](/help/sites-administering/target.md). |  |
| Adobe Target | Utilizzo di `mbox.js` L’integrazione basata su con Adobe Target nell’AEM è stata dichiarata obsoleta. | Passa all&#39;uso `at.js` 1.x. |  |
| Commerce | [RIPOSO CIF](https://github.com/adobe/commerce-cif-api) è stato fornito nel 2018 come un insieme di microservizi per consentire integrazioni tra AEM e motori commerce. Dopo che Adobe ha acquisito Adobe Commerce (precedentemente Magento) a metà del 2018, Adobe ha deciso di cambiare il suo approccio per due motivi. Commerce dispone di un proprio set di API Commerce (REST e GraphQL) e non è buona prassi mantenere due set di API. Le tendenze del mercato indicano che i clienti si stavano muovendo verso GraphQL, perché è un modo più efficiente di interrogare i dati. Nel 2019, Adobe ha rilasciato la nuova Commerce integration framework utilizzando le API GraphQL di Commerce come fonte di verità. Adobe non prevede di effettuare ulteriori investimenti nell&#39;CIF REST. Si consiglia ai clienti di utilizzare la soluzione sostitutiva. | Per le integrazioni AEM-Commerce, passa a [Archetipo CIF AEM](https://github.com/adobe/aem-cif-project-archetype) e [Componenti core dell’CIF dell’AEM](https://github.com/adobe/aem-core-cif-components). Consulta Integrazione di AEM e Adobe Commerce [utilizzo della Commerce integration framework](/help/commerce/cif/integrating/magento.md). Il supporto per le integrazioni di terze parti (diverse da Commerce) con il nuovo approccio è nella roadmap di Adobe. |  |
| Componenti (AEM Sites) | Adobe non prevede di apportare ulteriori miglioramenti alla maggior parte dei Componenti di base memorizzati in `/libs/foundation/components`. Cerca `cq:deprecated` e `cq:deprecatedReason` nella cartella dei componenti. AEM 6.5 include i Componenti di base e i clienti che eseguono l’aggiornamento da versioni precedenti possono continuare a utilizzarli così come sono. Inoltre, i Componenti di base sono supportati anche se obsoleti. | L’Adobe consiglia di utilizzare i Componenti core per i progetti futuri. I siti esistenti possono rimanere invariati o utilizzare [Suite di strumenti di modernizzazione AEM](https://github.com/adobe/aem-modernize-tools) per eseguire il refactoring del sito in modo da utilizzare i Componenti core. |  |
| Componenti (AEM Sites) | Componenti importazione progettazione `/libs/wcm/designimporter/components` sono state contrassegnate come obsolete a partire dalla versione 6.5. Adobe non prevede di apportare ulteriori miglioramenti a tale implementazione dell&#39;importazione di progettazione. | Adobe prevede di fornire un’implementazione alternativa del caso d’uso nelle versioni future. |  |
| Foundation | Framework di offload Granite. Adobe non prevede di apportare ulteriori miglioramenti al framework di offload introdotto in CQ 5.6.1 per esternalizzare l’elaborazione delle risorse. | Adobe sta lavorando su un framework di offload nativo per il cloud di nuova generazione. |  |
| Sviluppatori | `Hobbes.js`. Adobe non prevede di apportare ulteriori miglioramenti alla `hobbes.js` framework di test dell’interfaccia utente. | L’Adobe consiglia ai clienti di utilizzare l’automazione Selenium. |  |
| Sviluppatori | Libreria client dell’interfaccia utente jQuery. Adobe non prevede di gestire e aggiornare ulteriormente la libreria client dell’interfaccia utente jQuery fornita come parte della distribuzione (Quickstart). | L’Adobe consiglia ai clienti che richiedono ancora l’interfaccia utente jQuery per il codice di aggiungerla alla base di codice del progetto. |  |
| Sviluppatori | Libreria client di animazione jQuery (`granite.jquery.animation`). Adobe non prevede di gestire e aggiornare ulteriormente la libreria client di animazione jQuery fornita come parte della distribuzione (Quickstart). | L’Adobe consiglia ai clienti che ancora richiedono jQuery Animations per il codice di aggiungerlo alla base di codice del progetto. |  |
| Sviluppatori | Libreria client Handlebars. Adobe non prevede di gestire e aggiornare ulteriormente la libreria client Handlebar fornita come parte della distribuzione (Quickstart). | L’Adobe consiglia ai clienti che richiedono ancora `Handlebars` affinché il codice possa aggiungerlo alla base di codice del progetto. |  |
| Sviluppatori | Libreria client Lawnchair. Adobe non prevede di mantenere e aggiornare ulteriormente la libreria client Lawnchair fornita come parte della distribuzione (Quickstart). | L’Adobe consiglia ai clienti che richiedono ancora Lawnchair per il codice di aggiungerlo alla base di codice del progetto. |  |
| Sviluppatori | `Granite.Sling.js` libreria client. Adobe non prevede di migliorare ulteriormente la libreria client Granite.Sling.js fornita come parte della distribuzione (Quickstart). | L’Adobe consiglia ai clienti che si affidano alla capacità della libreria di eseguire il refactoring del codice per non utilizzarlo più. |  |
| Sviluppatori | Utilizzo di YUI per comprimere/minimizzare le librerie client JavaScript. L’Adobe non prevede di aggiornare ulteriormente la libreria YUI. Fino a AEM 6.4, per impostazione predefinita YUI minimizzava JavaScript con l’opzione di passare a Google Closure Compiler (GCC). A partire da AEM 6.5, GCC è il valore predefinito. | L’Adobe consiglia ai clienti che eseguono l’aggiornamento a AEM 6.5 di passare a GCC per l’implementazione |  |
| Sviluppatori | Editor di finestre di dialogo dell’interfaccia classica in CRXDE Liti. L’Adobe non prevede di migliorare ulteriormente l’Editor di finestre di dialogo dell’interfaccia classica fornito come parte della distribuzione (Quickstart) | Nessuna sostituzione disponibile. |  |
| Forms | L’integrazione di AEM Forms con AEM Mobile è stata rimossa. | Nessuna sostituzione disponibile. |  | Sviluppatori | Editor di finestre di dialogo dell’interfaccia classica in CRXDE Liti. L’Adobe non prevede di migliorare ulteriormente l’Editor di finestre di dialogo dell’interfaccia classica fornito come parte della distribuzione (Quickstart) | Nessuna sostituzione disponibile. |  |
| Sviluppatori | Libreria client lodash/underscore. Adobe non prevede di mantenere e aggiornare ulteriormente la libreria client Lodash/underscore fornita come parte della distribuzione (Quickstart). | L’Adobe consiglia ai clienti che richiedono ancora Lodash/underscore per il codice di aggiungerlo alla base di codice del progetto. |  |

## Funzioni rimosse {#removed-features}

In questa sezione sono elencate le funzioni e le funzionalità rimosse da AEM 6.5. Le versioni precedenti presentavano queste funzionalità contrassegnate come obsolete.

| Area | Funzione obsoleta | Sostituzione | Versione (SP) |
|--- |--- |--- |--- |
| Integrazione con [!DNL Experience Cloud] | Puoi sincronizzare le risorse con [!DNL Experience Cloud] utilizzo di una configurazione tramite [!DNL Adobe I/O]. [!DNL Adobe Experience Cloud] precedentemente denominato [!DNL Adobe Experience Cloud]. | In caso di domande, [contatta l’Assistenza clienti Adobe](https://experienceleague.adobe.com/?support-solution=General&amp;lang=it#support). |  |
| Activity Map di Analytics | Versione dell’Activity Map inclusa nell’AEM. | In seguito a modifiche di sicurezza nell’API di Adobe Analytics, non è più possibile utilizzare la versione di Activity Map inclusa in AEM. Utilizza il [Plug-in ActivityMap fornito da Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/analyze/activity-map/getting-started/get-started-users/activitymap-install.html?lang=it). |  |
| Integrazioni | L’integrazione ExactTarget è stata rimossa dalla distribuzione predefinita (Quickstart) e non è più disponibile. | Nessun sostituto. |  |
| Integrazioni | L’integrazione API di Salesforce Force è stata rimossa dalla distribuzione predefinita (Quickstart) ed è ora un pacchetto aggiuntivo da installare da [Distribuzione di software](https://experience.adobe.com/#/downloads/content/software-distribution/it/aem.html). | La funzione è ancora disponibile. |
| Forms | Il supporto per il servizio Central Migration Bridge di Adobe è stato rimosso in quanto Adobe Central non è più supportato. | Nessun sostituto. |  |
| Forms | `com.adobe.fd.df.fdinternal.model.ConfigurationInstance` | Nessun sostituto. |  |
| Forms | `com.adobe.fd.ccm.channels.print.fdinternal.api.service.PrintDataTransformer` | Nessuna sostituzione |  |
| Forms | L’aggiornamento single-hop da LiveCycle ES4 SP1 a AEM 6.5 Forms su JEE non è disponibile | Consulta [percorsi di aggiornamento disponibili](../forms/using/upgrade.md) nella documentazione sull’aggiornamento di AEM Forms. |  |
| Forms | Supporto del clustering basato su UPD rimosso da AEM Forms su JEE | In AEM Forms su JEE è possibile utilizzare solo il clustering basato su TCP. Se si aggiorna un server multicast UDP da una versione precedente a Forms AEM 5.5 su JEE, eseguire le configurazioni manuali per passare al cluster gemfire basato su TCP. Per istruzioni dettagliate, consulta [Aggiornamento a moduli AEM 6.5 su JEE](../forms/using/upgrade-forms-jee.md) |  |
| Sviluppatori | Firebug Lite è stato rimosso dalla distribuzione predefinita (Quickstart) | Utilizzare le console per sviluppatori integrate nel browser |
| Sviluppatori | Rimuovi `customJavaScriptPath` supporto in HTML Client Library Manager. | Nessuna sostituzione |  |
| [!DNL Assets] | La funzione di offload delle risorse viene rimossa in [!DNL Adobe Experience Manager] 6.5 | Nessuna sostituzione disponibile. |  |
| Cache | `system/console/slingjsp` è stato rimosso e non è più disponibile in AEM 6.5. | La cache di classi e Slightly è memorizzata nel bundle Apache Sling Commons FileSystem ClassLoader. Puoi controllare il numero del bundle nella console web AEM e rimuovere la cartella della cache direttamente dal file system (`crx-quickstart/launchpad/felix/bundle<ID>`). |  |
| Screens | Rimozione del supporto del bundle activemq e delle relative configurazioni. |  |  |

<!-- ## Pre-announcement for next release {#pre-announcement-for-next-release}

This section is used to pre-announce the upcoming changes in the future releases. The announced changes are not yet effective but will impact customers. For example, the features are not yet deprecated but impacts the users after deprecation. These updates are provided for planning purpose.

|Area|Feature|Announcement|
|--- |--- |--- |
|Foundation|UI Framework|Adobe is planning to deprecate the Coral UI 2 components in 2019. Coral UI 3 was introduced with AEM 6.2, and AEM 6.5 is fully based on Coral 3. Adobe recommends customers and partners that have build custom UIs with Coral 2 to refactored them to Coral 3. Adobe is providing a tool to convert Coral 2 dialogs to Coral 3 - [Read more](/help/sites-developing/modernization-tools.md).|
-->
