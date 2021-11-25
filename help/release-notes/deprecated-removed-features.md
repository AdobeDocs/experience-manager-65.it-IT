---
title: Funzioni obsolete e rimosse in Adobe Experience Manager 6.5.
description: Note specifiche per le funzioni obsolete e rimosse in Adobe Experience Manager 6.5.
exl-id: d9b6140a-c37d-4b90-a60c-01f471d65621
source-git-commit: c9db5a1764d98bb049c08a0e6962b7ed5e1bfe5c
workflow-type: tm+mt
source-wordcount: '1753'
ht-degree: 43%

---

# Funzioni obsolete e rimosse {#deprecated-and-removed-features}

Adobe valuta costantemente le funzionalità dei prodotti per reinventare o sostituire nel tempo le funzioni meno recenti con alternative più moderne al fine di migliorare il valore complessivo per il cliente, tenendo comunque in considerazione la compatibilità con le versioni precedenti.

Per comunicare l’imminente rimozione o sostituzione delle funzionalità di AEM, si applicano le seguenti regole:

1. Innanzitutto viene annunciato che una data funzione diventa obsoleta. Anche se è obsoleta, le funzionalità sono ancora disponibili ma non vengono ulteriormente migliorate.
1. La rimozione delle funzionalità obsolete si verifica non prima nella versione principale successiva. La data di riferimento effettiva per la rimozione verrà annunciata.

Questo processo offre ai clienti almeno un ciclo di rilascio per adattare la loro implementazione a una nuova versione o alla funzionalità che prenderà il posto di quella dichiarata obsoleta, prima che venga definitivamente rimossa.

## Funzioni obsolete {#deprecated-features}

In questa sezione sono elencate le funzioni e le funzionalità contrassegnate come obsolete per AEM 6.5. In genere, le funzioni che si prevede di rimuovere in una versione futura vengono inizialmente rese obsolete e viene fornita un’alternativa.

Consigliamo ai clienti di verificare se utilizzano la funzione o funzionalità nella loro implementazione corrente e di pianificarne la modifica adottando l’alternativa fornita.

| Area | Funzione obsoleta | Sostituzione | Versione (SP) |
|---|---|---|---|
| [!DNL Sites] | Modelli per frammenti di contenuto, per la creazione di frammenti di contenuto semplici. | [Frammenti di contenuto strutturati basati su modelli](/help/assets/content-fragments/content-fragments-models.md) ora. | 6.5.11.0 |
| Integrazione  Creative Cloud | AEM a Creative Cloud condivisione cartelle è stato introdotto in AEM 6.2 come modo per consentire agli utenti creativi di accedere alle risorse da AEM, in modo che possano aprirle in [!DNL Creative Cloud] e carica nuovi file o salva le modifiche in AEM. Una nuova funzionalità introdotta nell’applicazione Creative Cloud, Adobe Asset Link, offre un’esperienza utente migliore e un accesso più efficace alle risorse da AEM direttamente da Photoshop, InDesign e Illustrator. Adobe non prevede di apportare ulteriori miglioramenti all’integrazione mediante condivisione delle cartelle Creative Cloud. Sebbene la funzione sia inclusa in AEM, consigliamo ai clienti di utilizzare soluzioni sostitutive. | Consigliamo ai clienti di passare a nuove funzionalità di integrazione Creative Cloud, tra cui Adobe Asset Link o AEM’app desktop. |  |
| Assets | `AssetDownloadServlet`Per la pubblicazione di istanze,  è disattivato per impostazione predefinita. Per ulteriori informazioni, vedi [Elenco di controllo per la sicurezza AEM](/help/sites-administering/security-checklist.md). | Configurazione descritta nell’[Elenco di controllo per la sicurezza AEM](/help/sites-administering/security-checklist.md). |  |
| Risorse | Se un utente non dispone di autorizzazioni sufficienti (lettura e scrittura) su `/content/dam/collections`, l&#39;utente non può creare una raccolta. | Rispetta le impostazioni di controllo dell’accesso dell’utente e verifica le autorizzazioni appropriate. |  |
| Adobe Search&amp;Promote | L’integrazione con Adobe Search&amp;Promote è obsoleta. Adobe non prevede di apportare ulteriori miglioramenti all’integrazione con Search&amp;Promote. Nota: l’integrazione con Search&amp;Promote rimane completamente supportata anche se obsoleta. |  |  |
| Gestione tag DTM | L’integrazione con DTM (Dynamic Tag Manager) è obsoleta. | Inizia a utilizzare Adobe Experience Platform Launch come gestore di tag. |  |
| Adobe Target | Con l’aggiunta della possibilità di AEM di connettersi al servizio Adobe Target tramite la funzione [!DNL Adobe I/O] basato sull’API Adobe Target Standard (Rest API) in AEM 6.5, il metodo API di Target Classic (XML) è obsoleto. | Riconfigura l’integrazione in [utilizzare la nuova API](https://helpx.adobe.com/experience-manager/kt/sites/using/aem-sites-target-standard-technical-video-understand.html). |  |
| Adobe Target | Utilizzo della `mbox.js` l’integrazione basata su Adobe Target in AEM è obsoleta. | Passa all&#39;utilizzo `at.js` 1.x. |  |
| Commerce | [CIF REST](https://github.com/adobe/commerce-cif-api) è stato fornito nel 2018 come set di microservizi per consentire integrazioni tra motori AEM e commerce. Dopo l’acquisizione del Magento da parte dell’Adobe a metà del 2018, l’Adobe ha deciso di modificare il proprio approccio per due motivi. Il Magento dispone di un proprio set di API Commerce (REST e GraphQL) e non è buona prassi mantenere due set di API. Le tendenze del mercato indicano che i clienti si stavano spostando verso GraphQL, perché è un modo più efficiente di eseguire query sui dati. Nel 2019, Adobe ha rilasciato il nuovo Commerce Integration Framework utilizzando le API GraphQL di Magento come fonte di verità. L’Adobe non prevede di effettuare ulteriori investimenti in REST CIF. Si consiglia vivamente ai clienti di utilizzare la soluzione sostitutiva. | Per le integrazioni AEM Magento, passa a [Archetipo CIF AEM](https://github.com/adobe/aem-cif-project-archetype) e [Componenti core CIF di AEM](https://github.com/adobe/aem-core-cif-components). Vedi Integrazione AEM e Magento [utilizzo di Commerce Integration Framework](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/integrations.html#!AdobeDocs/commerce-cif-documentation/master/integrations/02-AEM-Magento.md). Il supporto per le integrazioni di terze parti (diverse dal Magento) con il nuovo approccio è nella nostra tabella di marcia. |  |
| Componenti (AEM Sites) | Adobe non prevede di apportare ulteriori miglioramenti alla maggior parte dei componenti di base in `/libs/foundation/components`. Cerca la `cq:deprecated` e `cq:deprecatedReason` nella cartella dei componenti. AEM 6.5 include i componenti di base e i clienti che eseguono l’aggiornamento da versioni precedenti possono continuare a utilizzarli normalmente. Inoltre, i componenti di base sono completamente supportati anche se obsoleti. | Adobe consiglia di utilizzare i componenti core per i progetti futuri. I siti esistenti possono rimanere come sono o utilizzare il [AEM suite di strumenti di modernizzazione](https://github.com/adobe/aem-modernize-tools) per eseguire il refactoring del sito per utilizzare i componenti core. |  |
| Componenti (AEM Sites) | Componenti per Importazione progettazione `/libs/wcm/designimporter/components` sono stati contrassegnati come obsoleti a partire dalla versione 6.5. Adobe non prevede di apportare ulteriori miglioramenti a tale implementazione di Importazione progettazione. | L’Adobe prevede di fornire un’implementazione alternativa del caso d’uso nelle versioni future. |  |
| Foundation | Granite Offloading Framework. Adobe non prevede di apportare ulteriori miglioramenti al framework di offload introdotto in CQ 5.6.1 per esternalizzare l’elaborazione delle risorse. | Adobe sta lavorando a un framework di offload cloud nativo di nuova generazione. |  |
| Sviluppatori | `Hobbes.js`. Adobe non prevede di apportare ulteriori miglioramenti al `hobbes.js` framework di test dell&#39;interfaccia utente. | L’Adobe consiglia ai clienti di utilizzare l’automazione Selenium. |  |
| Sviluppatori | Libreria client per interfaccia utente jQuery. Adobe non prevede di mantenere e aggiornare ulteriormente la libreria client per interfaccia utente jQuery fornita come parte della distribuzione (Quickstart) | Adobe consiglia ai clienti che richiedono ancora l’interfaccia utente jQuery per il loro codice di aggiungerla alla codebase del progetto. |  |
| Sviluppatori | Libreria client per animazione jQuery (`granite.jquery.animation`). Adobe non prevede di mantenere e aggiornare ulteriormente la libreria client per animazione jQuery fornita come parte della distribuzione (Quickstart) | Adobe consiglia ai clienti che richiedono ancora animazioni jQuery per il loro codice di aggiungerlo alla codebase del progetto. |  |
| Sviluppatori | Libreria client handlebar. Adobe non prevede di mantenere e aggiornare ulteriormente la libreria client per Handlebar fornita come parte della distribuzione (Quickstart) | Adobe consiglia ai clienti che richiedono ancora Handlebar per il loro codice di aggiungerlo alla codebase del progetto. |  |
| Sviluppatori | Libreria client Lawnchair. Adobe non prevede di mantenere e aggiornare ulteriormente la libreria client per Lawnchair fornita come parte della distribuzione (Quickstart) | Adobe consiglia ai clienti che richiedono ancora Lawnchair per il loro codice di aggiungerlo alla codebase del progetto. |  |
| Sviluppatori | `Granite.Sling.js` libreria client. Adobe non prevede di migliorare ulteriormente la libreria client Granite.Sling.js fornita come parte della distribuzione (Quickstart) | Adobe consiglia ai clienti che si affidano alla funzionalità della libreria di eseguire il refactoring del codice per non utilizzarla più. |  |
| Sviluppatori | Utilizzo di YUI per comprimere/minimizzare le librerie client JavaScript. Adobe non prevede di aggiornare ulteriormente la libreria YUI. Fino a AEM 6.4, YUI era il formato predefinito per minimizzare JavaScript con l&#39;opzione per passare a Google Closure Compiler (GCC). A partire da AEM 6.5, GCC è l’impostazione predefinita. | Adobe consiglia ai clienti che eseguono l’aggiornamento a AEM 6.5 di passare a GCC per la loro implementazione |  |
| Sviluppatori | Editor finestra di dialogo dell’interfaccia utente classica in CRXDE lite. Adobe non prevede di migliorare ulteriormente l’Editor finestra di dialogo dell’interfaccia utente classica fornito come parte della distribuzione (Quickstart) | Nessuna sostituzione disponibile. |  |
| Forms | L’integrazione di AEM Forms con AEM Mobile è obsoleta. | Non è disponibile alcuna sostituzione. |  | Sviluppatori | Editor finestra di dialogo dell’interfaccia utente classica in CRXDE lite. Adobe non prevede di migliorare ulteriormente l’Editor finestra di dialogo dell’interfaccia utente classica fornito come parte della distribuzione (Quickstart) | Nessuna sostituzione disponibile. |  |
| Sviluppatori | Libreria client Lodash/underscore. Adobe non prevede di mantenere e aggiornare ulteriormente la libreria client Lodash/underscore fornita come parte della distribuzione (Quickstart) | Adobe consiglia ai clienti che richiedono ancora il Lodash/underscore per il loro codice di aggiungerlo alla codebase del progetto. |  |

## Funzioni rimosse {#removed-features}

In questa sezione sono elencate le funzionalità rimosse da AEM 6.5. Nelle versioni precedenti queste funzionalità erano indicate come obsolete.

| Area | Funzione obsoleta | Sostituzione | Versione (SP) |
|--- |--- |--- |--- |
| Integrazione con [!DNL Experience Cloud] | Puoi sincronizzare le tue risorse con [!DNL Experience Cloud] utilizzo di una configurazione tramite [!DNL Adobe I/O]. [!DNL Adobe Experience Cloud] è stato precedentemente chiamato [!DNL Adobe Marketing Cloud]. | Se hai delle domande, [contattare l&#39;assistenza clienti Adobe](https://www.adobe.com/account/sign-in.supportportal.html). |  |
| Activity Map di Analytics | Versione di Activity Map inclusa in AEM. | In seguito a modifiche di sicurezza nell’API di Adobe Analytics, non è più possibile utilizzare la versione di Activity Map inclusa in AEM. Utilizza la [Plug-in ActivityMap fornito da Adobe Analytics](https://docs.adobe.com/content/help/it/analytics/analyze/activity-map/getting-started/get-started-users/activitymap-install.html). |  |
| Integrazioni | L’integrazione ExactTarget è stata rimossa dalla distribuzione predefinita (Quickstart) e non è più disponibile. | Nessuna sostituzione. |  |
| Integrazioni | L’integrazione dell’API Salesforce Force è stata rimossa dalla distribuzione predefinita (Quickstart) ed è ora un pacchetto aggiuntivo da cui installare [Distribuzione di software](https://experience.adobe.com/#/downloads/content/software-distribution/it/aem.html). | La funzione è ancora disponibile. |
| Forms | Il supporto per il servizio Adobe Central Migration Bridge è stato rimosso in quanto il prodotto Adobe Central non è più supportato. | Nessuna sostituzione. |  |
| Forms | `com.adobe.fd.df.fdinternal.model.ConfigurationInstance` | Nessuna sostituzione. |  |
| Forms | `com.adobe.fd.ccm.channels.print.fdinternal.api.service.PrintDataTransformer` | Nessuna sostituzione |  |
| Forms | Aggiornamento single-hop da LiveCycle ES4 SP1 a AEM 6.5 Forms su JEE non disponibile | Vedi [percorsi di aggiornamento disponibili](../forms/using/upgrade.md) nella documentazione relativa all’aggiornamento di AEM Forms. |  |
| Forms | Supporto del clustering basato su UPD rimosso da AEM Forms su JEE | È possibile utilizzare solo il clustering basato su TCP in AEM Forms su JEE. Se si aggiorna un server multicast UDP da una versione precedente a AEM 5.5 Forms su JEE, si eseguono configurazioni manuali per passare al clustering gemfire basato su TCP. Per istruzioni dettagliate, vedi [Aggiornamento a AEM moduli 6.5 su JEE](../forms/using/upgrade-forms-jee.md) |  |
| Sviluppatori | Firebug Lite è stato rimosso dalla distribuzione predefinita (Quickstart) | Utilizza le console di sviluppo integrate nel browser |
| Sviluppatori | Rimuovi `customJavaScriptPath` supporto in HTML Client Library Manager. | Nessuna sostituzione |  |
| [!DNL Assets] | La funzione di scaricamento delle risorse viene rimossa in [!DNL Adobe Experience Manager] 6.5. | Nessuna sostituzione disponibile. |  |
| Cache | `system/console/slingjsp` La rimozione di non è più disponibile in AEM 6.5. | Le classi e la cache Slightly sono memorizzate nel bundle Apache Sling Commons FileSystem ClassLoader . Puoi controllare il numero del bundle nella Console Web AEM e rimuovere la cartella della cache direttamente dal file system (`crx-quickstart/launchpad/felix/bundle<ID>`). |  |

## Pre-annuncio per la prossima versione {#pre-announcement-for-next-release}

Questa sezione viene utilizzata per preannunciare le modifiche imminenti nelle versioni future. Le modifiche annunciate non sono ancora efficaci, ma avranno un impatto sui clienti. Ad esempio, le funzioni non sono ancora obsolete ma hanno un impatto sugli utenti dopo la rimozione. Questi aggiornamenti vengono forniti a scopo di pianificazione.

| Area | Funzione obsoleta | Annuncio |
|--- |--- |--- |
| Foundation | Framework interfaccia utente | Adobe prevede di rendere obsoleti i componenti Coral UI 2 nel 2019. L’interfaccia Coral UI 3 è stata introdotta con AEM 6.2 e AEM 6.5 è completamente basato su Coral 3. Adobe consiglia ai clienti e ai partner che hanno creato delle interfacce utente personalizzate con Coral 2 di eseguire il refactoring per Coral 3. Adobe fornisce uno strumento per convertire le finestre di dialogo Coral 2 in Coral 3. [Ulteriori informazioni](/help/sites-developing/modernization-tools.md). |
