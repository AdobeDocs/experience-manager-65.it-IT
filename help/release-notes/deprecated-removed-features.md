---
title: Funzioni obsolete e rimosse in Adobe Experience Manager 6.5.
description: Note specifiche per le funzioni obsolete e rimosse in Adobe Experience Manager 6.5.
translation-type: tm+mt
source-git-commit: 0560eb8e3c127964920827609a9982acf07b515f
workflow-type: tm+mt
source-wordcount: '1719'
ht-degree: 43%

---


# Funzioni obsolete e rimosse {#deprecated-and-removed-features}

Adobe valuta costantemente le funzionalità dei prodotti per reinventare o sostituire nel tempo le funzioni meno recenti con alternative più moderne al fine di migliorare il valore complessivo per il cliente, tenendo comunque in considerazione la compatibilità con le versioni precedenti.

Per comunicare l&#39;imminente rimozione o sostituzione delle capacità AEM, si applicano le regole seguenti:

1. Innanzitutto viene annunciato che una data funzione diventa obsoleta. Anche se è obsoleta, le funzionalità sono ancora disponibili, ma non sono ulteriormente migliorate.
1. L&#39;eliminazione di funzionalità obsolete si verifica non prima nella versione principale successiva. La data di riferimento effettiva per la rimozione verrà annunciata.

Questo processo offre ai clienti almeno un ciclo di rilascio per adattare la loro implementazione a una nuova versione o alla funzionalità che prenderà il posto di quella dichiarata obsoleta, prima che venga definitivamente rimossa.

## Funzioni obsolete {#deprecated-features}

In questa sezione sono elencate le funzioni e le funzionalità contrassegnate come obsolete per AEM 6.5. In genere, le funzioni che si prevede di rimuovere in una versione futura vengono inizialmente rese obsolete e viene fornita un’alternativa.

Consigliamo ai clienti di verificare se utilizzano la funzione o funzionalità nella loro implementazione corrente e di pianificarne la modifica adottando l’alternativa fornita.

| Area | Funzione obsoleta | Sostituzione |
|---|---|---|
| Integrazione  Creative Cloud | AEM a Creative Cloud condivisione cartelle è stato introdotto in AEM 6.2 come modo per consentire agli utenti creativi di accedere alle risorse da AEM, in modo che possano aprirle nelle applicazioni CC e caricare nuovi file o salvare le modifiche in AEM. Una nuova funzionalità introdotta nell’applicazione Creative Cloud, Adobe Asset Link, offre un’esperienza utente migliore e un accesso più efficace alle risorse da AEM direttamente da Photoshop, InDesign e Illustrator. Adobe non prevede di apportare ulteriori miglioramenti all’integrazione mediante condivisione delle cartelle Creative Cloud. Sebbene la funzione sia inclusa in AEM, consigliamo ai clienti di utilizzare soluzioni sostitutive. | Ai clienti viene consigliato di passare alle nuove funzionalità di integrazione delle Creative Cloud, tra cui  collegamento delle risorse di Adobe o AEM app desktop. Per ulteriori informazioni, consulta Tecniche consigliate per l&#39;integrazione di AEM e Creative Cloud. |
| Assets | `AssetDownloadServlet`Per la pubblicazione di istanze,  è disattivato per impostazione predefinita. Per ulteriori informazioni, vedi [Elenco di controllo per la sicurezza AEM](/help/sites-administering/security-checklist.md). | Configurazione descritta nell’[Elenco di controllo per la sicurezza AEM](/help/sites-administering/security-checklist.md). |
| Risorse | Se un utente non dispone di autorizzazioni sufficienti (lettura e scrittura) per `/content/dam/collections`, non può creare una raccolta. | Rispetta le impostazioni di controllo dell’accesso dell’utente e verifica le autorizzazioni appropriate. |
| Adobe Search&amp;Promote | L&#39;integrazione con  Adobe Search&amp;Promote è obsoleta. Adobe non prevede di apportare ulteriori miglioramenti all’integrazione con Search&amp;Promote. Nota: l’integrazione con Search&amp;Promote rimane completamente supportata anche se obsoleta. |  |
| Gestione tag DTM | L’integrazione con DTM (Dynamic Tag Manager) è obsoleta. | Inizia a utilizzare Adobe Experience Platform Launch come gestore di tag. |
| Adobe Target | Con l&#39;aggiunta della capacità di AEM di connettersi  servizio Adobe Target utilizzando l&#39;API Adobe Target Standard (API Rest) basata su [!DNL Adobe I/O] in AEM 6.5, la modalità API di Target Classic (XML) è obsoleta. | Riconfigurare l&#39;integrazione in [utilizzare la nuova API](https://helpx.adobe.com/experience-manager/kt/sites/using/aem-sites-target-standard-technical-video-understand.html). |
|  Adobe Target | L&#39;utilizzo dell&#39;integrazione basata su `mbox.js` con  Adobe Target in AEM è obsoleto. | Passare a `at.js` 1.x. |
| Commerce | [CIF ](https://github.com/adobe/commerce-cif-api) REST è stato fornito nel 2018 come set di microservizi per consentire l&#39;integrazione tra i motori AEM e commerciali. Dopo che  Adobe ha acquisito il Magento a metà del 2018,  Adobe ha deciso di modificare il suo approccio per due motivi. Il Magento dispone di un proprio set di API Commerce (REST e GraphQL) e non è buona norma mantenere due set di API. Le tendenze del mercato hanno indicato che i clienti si stavano spostando verso GraphQL, perché è un modo più efficiente di interrogare i dati. Nel 2019,  Adobe ha rilasciato il nuovo Commerce Integration Framework utilizzando le API GraphQL di Magento  come fonte di verità.  Adobe non prevede ulteriori investimenti in CIF REST. Ai clienti viene consigliato di utilizzare la soluzione sostitutiva. | Per le integrazioni AEM-Magento, passate a [AEM CIF Archetype](https://github.com/adobe/aem-cif-project-archetype) e [AEM CIF Core Components](https://github.com/adobe/aem-core-cif-components). Vedere Integrazione AEM e Magento [utilizzando Commerce Integration Framework](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/integrations.html#!AdobeDocs/commerce-cif-documentation/master/integrations/02-AEM-Magento.md). Il sostegno alle integrazioni di terze parti (diverse da quelle dei Magenti) con il nuovo approccio è nella nostra tabella di marcia. |
| Componenti (AEM Sites) | Adobe non prevede di apportare ulteriori miglioramenti alla maggior parte dei componenti di base in `/libs/foundation/components`. Cercare la proprietà `cq:deprecated` e `cq:deprecatedReason` nella cartella del componente. AEM 6.5 include i componenti di base e i clienti che effettuano l&#39;aggiornamento da versioni precedenti possono continuare a utilizzarli così com&#39;è. Inoltre, Foundation Components è completamente supportato anche se obsoleto. |  Adobe consiglia di utilizzare i componenti core per progetti futuri. I siti esistenti possono rimanere invariati o utilizzare la [AEM Modernizza Tools Suite](https://github.com/adobe/aem-modernize-tools) per riorientare il sito in modo che utilizzi i componenti core. |
| Componenti (AEM Sites) | I componenti di Importazione progettazione `/libs/wcm/designimporter/components` sono stati contrassegnati come obsoleti a partire dalla versione 6.5.  Adobe non prevede di apportare ulteriori miglioramenti a tale implementazione di Importazione progettazione. |  Adobe prevede di fornire un&#39;attuazione alternativa del caso d&#39;uso nelle release future. |
| Foundation | Granite Offloading Framework.  Adobe non prevede di apportare ulteriori miglioramenti al framework di scarico introdotto in CQ 5.6.1 per esternalizzare l&#39;elaborazione delle risorse. | Adobe sta lavorando a un framework di offload cloud nativo di nuova generazione. |
| Sviluppatori | `Hobbes.js`.  Adobe non prevede di apportare ulteriori miglioramenti al framework di test dell&#39;interfaccia utente `hobbes.js`. |  Adobe consiglia ai clienti di utilizzare l&#39;automazione selenio. |
| Sviluppatori | Libreria client per interfaccia utente jQuery. Adobe non prevede di mantenere e aggiornare ulteriormente la libreria client per interfaccia utente jQuery fornita come parte della distribuzione (Quickstart) |  Adobe consiglia ai clienti che necessitano ancora di un’interfaccia utente jQuery per il codice, di aggiungerla al codice di base del progetto. |
| Sviluppatori | Libreria client jQuery Animation (`granite.jquery.animation`). Adobe non prevede di mantenere e aggiornare ulteriormente la libreria client per animazione jQuery fornita come parte della distribuzione (Quickstart) |  Adobe consiglia ai clienti che necessitano ancora di animazioni jQuery per il codice di aggiungerlo alla propria base di codice di progetto. |
| Sviluppatori | Libreria client handlebar. Adobe non prevede di mantenere e aggiornare ulteriormente la libreria client per Handlebar fornita come parte della distribuzione (Quickstart) |  Adobe consiglia ai clienti che necessitano ancora di Handlebars per il codice di aggiungere il codice alla propria base di codice del progetto. |
| Sviluppatori | Libreria client Lawnchair. Adobe non prevede di mantenere e aggiornare ulteriormente la libreria client per Lawnchair fornita come parte della distribuzione (Quickstart) |  Adobe consiglia ai clienti che ancora richiedono Lawnsedia per il loro codice di aggiungerlo nella loro base di codice del progetto. |
| Sviluppatori | `Granite.Sling.js` libreria client. Adobe non prevede di migliorare ulteriormente la libreria client Granite.Sling.js fornita come parte della distribuzione (Quickstart) |  Adobe consiglia ai clienti che si affidano alla funzionalità della libreria di rigenerare il codice per non utilizzarlo più. |
| Sviluppatori | Utilizzo di YUI per comprimere/minimizzare le librerie client JavaScript. Adobe non prevede di aggiornare ulteriormente la libreria YUI. Fino AEM 6.4, per impostazione predefinita, YUI ha ridotto a icona JavaScript con l&#39;opzione per passare a Google Closure Compiler (GCC). A partire da AEM 6.5, GCC è l’impostazione predefinita. |  Adobe consiglia ai clienti di effettuare l&#39;aggiornamento a AEM 6.5 per passare al CCG per la loro implementazione |
| Sviluppatori | Editor finestra di dialogo dell’interfaccia utente classica in CRXDE lite. Adobe non prevede di migliorare ulteriormente l’Editor finestra di dialogo dell’interfaccia utente classica fornito come parte della distribuzione (Quickstart) | Nessuna sostituzione disponibile. |
| Forms | &#39;integrazione AEM Forms con  AEM Mobile è obsoleta. | Nessuna sostituzione disponibile. |  | Sviluppatori | Editor finestra di dialogo dell’interfaccia utente classica in CRXDE lite. Adobe non prevede di migliorare ulteriormente l’Editor finestra di dialogo dell’interfaccia utente classica fornito come parte della distribuzione (Quickstart) | Nessuna sostituzione disponibile. |
| Sviluppatori | Libreria client Lodash/underscore.  Adobe non prevede di mantenere e aggiornare ulteriormente la libreria client Lodash/underscore fornita come parte della distribuzione (Quickstart) |  Adobe consiglia ai clienti che necessitano ancora di Lodash/underscore per il codice di aggiungerlo alla base di codice del progetto. |

## Funzioni rimosse {#removed-features}

In questa sezione sono elencate le funzionalità rimosse dalla AEM 6.5. Le versioni precedenti presentavano queste funzionalità contrassegnate come obsolete.

| Area | Funzione obsoleta | Sostituzione |
|--- |--- |--- |
| Activity Map di Analytics | Versione di Activity Map inclusa in AEM. | In seguito a modifiche di sicurezza in Adobe Analytics API, non è più possibile utilizzare la versione di Activity Map inclusa in AEM. Utilizzate il plug-in [ActivityMap fornito da  Adobe Analytics](https://docs.adobe.com/content/help/it/IT/analytics/analyze/activity-map/getting-started/get-started-users/activitymap-install.html). |
| Integrations (Integrazioni) | L&#39;integrazione ExactTarget è stata rimossa dalla distribuzione predefinita (Quickstart) e non è più disponibile. | Nessuna sostituzione. |
| Integrations (Integrazioni) | L&#39;integrazione API Salesforce Force è stata rimossa dalla distribuzione predefinita (Quickstart) ed è ora un pacchetto aggiuntivo da installare da [Distribuzione software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html). | La funzione è ancora disponibile. |
| Forms | Il supporto per il servizio Adobe Central Migration Bridge è stato rimosso in quanto il prodotto Adobe Central non è più supportato. | Nessuna sostituzione. |
| Forms | `com.adobe.fd.df.fdinternal.model.ConfigurationInstance` | Nessuna sostituzione. |
| Forms | `com.adobe.fd.ccm.channels.print.fdinternal.api.service.PrintDataTransformer` | Nessuna sostituzione |
| Forms | L&#39;aggiornamento single-hop dal LiveCycle ES4 SP1 a AEM Forms 6.5 su JEE non è disponibile | Consultate [percorsi di aggiornamento disponibili](../forms/using/upgrade.md) nella documentazione  aggiornamento di AEM Forms. |
| Forms | È stato rimosso il supporto del clustering basato su UPD da  AEM Forms su JEE | È possibile utilizzare solo il clustering basato su TCP in  AEM Forms su JEE. Se si aggiorna un server multicast UDP da una versione precedente a AEM 5.5 Forms su JEE, si eseguono configurazioni manuali per passare al clustering gemFire basato su TCP. Per istruzioni dettagliate, vedere [Aggiornamento ai moduli AEM 6.5 su JEE](../forms/using/upgrade-forms-jee.md) |
| Sviluppatori | Firebug Lite è stato rimosso dalla distribuzione predefinita (Quickstart) | Utilizza le console di sviluppo integrate nel browser |
| Sviluppatori | Rimuovere il supporto `customJavaScriptPath` in HTML Client Library Manager. | Nessuna sostituzione |
| [!DNL Assets] | La funzione di scaricamento delle risorse viene rimossa in [!DNL Adobe Experience Manager] 6.5. | Nessuna sostituzione disponibile. |
| Cache | `system/console/slingjsp` is remove non è più disponibile in AEM 6.5. | Le classi e la cache di Luminosità vengono memorizzate nel pacchetto Apache Sling Commons FileSystem ClassLoader. È possibile controllare il numero del bundle nella console Web AEM e rimuovere la cartella della cache direttamente dal file system (`crx-quickstart/launchpad/felix/bundle<ID>`). |

## Annuncio preliminare per la prossima release {#pre-announcement-for-next-release}

Questa sezione viene utilizzata per annunciare le prossime modifiche nelle release future. Le modifiche annunciate non sono ancora efficaci, ma avranno un impatto sui clienti. Ad esempio, le funzioni non sono ancora obsolete ma influiscono sugli utenti dopo la rimozione di tale valore. Questi aggiornamenti sono forniti a scopo di pianificazione.

| Area | Funzione obsoleta | Annuncio |
|--- |--- |--- |
| Foundation | Framework interfaccia utente | Adobe prevede di rendere obsoleti i componenti Coral UI 2 nel 2019. L’interfaccia Coral UI 3 è stata introdotta con AEM 6.2 e AEM 6.5 è completamente basato su Coral 3. Adobe consiglia ai clienti e ai partner che hanno creato delle interfacce utente personalizzate con Coral 2 di eseguire il refactoring per Coral 3. Adobe fornisce uno strumento per convertire le finestre di dialogo Coral 2 in Coral 3. [Ulteriori informazioni](/help/sites-developing/dialog-conversion.md). |
