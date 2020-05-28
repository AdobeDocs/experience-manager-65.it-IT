---
title: Funzioni obsolete e rimosse
description: Note specifiche per le funzioni obsolete e rimosse in Adobe Experience Manager 6.5.
uuid: 81d9a064-e712-4eff-bd3b-6e15513a5435
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5
discoiquuid: e8e2e01b-0117-48c3-86d8-609d29a147be
docset: aem65
translation-type: tm+mt
source-git-commit: 49209cb64c829fde396e87ca4b2e326ecf1dd941
workflow-type: tm+mt
source-wordcount: '1634'
ht-degree: 58%

---


# Funzioni obsolete e rimosse {#deprecated-and-removed-features}

Adobe valuta costantemente le funzionalità dei prodotti, per reinventare o sostituire nel tempo le funzioni meno recenti con alternative più moderne al fine di migliorare il valore complessivo per il cliente, tenendo comunque in considerazione la compatibilità con le versioni precedenti.

Per comunicare l’imminente rimozione/sostituzione delle funzionalità AEM, si applicano le seguenti regole:

1. Innanzitutto viene annunciato che una data funzione diventa obsoleta. Anche se è obsoleta, le funzionalità sono ancora disponibili, ma non saranno ulteriormente migliorate.
1. La rimozione delle funzionalità obsolete verrà attuata a partire dalla versione principale successiva. La data di riferimento effettiva per la rimozione verrà annunciata.

Questo processo offre ai clienti almeno un ciclo di rilascio per adattare la loro implementazione a una nuova versione o alla funzionalità che prenderà il posto di quella dichiarata obsoleta, prima che venga definitivamente rimossa.

## Funzioni obsolete {#deprecated-features}

In questa sezione sono elencate le funzioni e le funzionalità contrassegnate come obsolete per AEM 6.5. In genere, le funzioni che si prevede di rimuovere in una versione futura vengono inizialmente rese obsolete e viene fornita un’alternativa.

Consigliamo ai clienti di verificare se utilizzano la funzione o funzionalità nella loro implementazione corrente e di pianificarne la modifica adottando l’alternativa fornita.

<table>
 <tbody>
  <tr>
   <td><b>Area</b></td>
   <td><b>Funzione obsoleta</b></td>
   <td><b>Sostituzione</b></td>
  </tr>
  <tr>
   <td>Integrazione  Creative Cloud</td>
   <td><p><a href="/help/assets/aem-cc-folder-sharing-best-practices.md">AEM to Creative Cloud Folder Sharing</a> è stato introdotto in AEM 6.2 per consentire agli utenti creativi di accedere alle risorse da AEM, in modo che possano aprirle nelle applicazioni CC e caricare nuovi file o salvare le modifiche in AEM. Una nuova funzionalità introdotta nell’applicazione Creative Cloud, Adobe Asset Link, offre un’esperienza utente migliore e un accesso più efficace alle risorse da AEM direttamente da Photoshop, InDesign e Illustrator.</p> <p>Adobe non prevede di apportare ulteriori miglioramenti all’integrazione mediante condivisione delle cartelle Creative Cloud. Sebbene la funzione sia inclusa in AEM, consigliamo ai clienti di utilizzare soluzioni sostitutive.</p> </td>
   <td>Ai clienti viene consigliato di passare alle nuove funzionalità di integrazione di Creative Cloud, tra cui Adobe Asset Link o l'app desktop AEM. Review <a href="/help/assets/aem-cc-integration-best-practices.md">AEM and Creative Cloud Integration Best Practices</a> for more details.</td>
  </tr>
  <tr>
   <td>Assets</td>
   <td>
    <ol>
     <li>Per la pubblicazione di istanze, AssetDownloadServlet è disattivato per impostazione predefinita. Per ulteriori informazioni, vedi <a href="/help/sites-administering/security-checklist.md">Elenco di controllo per la sicurezza AEM</a>.</li>
     <li>Se un utente non ha autorizzazioni sufficienti (lettura e scrittura) su /content/dam/collections, non è in grado di creare una raccolta.</li>
    </ol> </td>
   <td>
    <ol>
     <li>Configurazione descritta nell’<a href="/help/sites-administering/security-checklist.md">Elenco di controllo per la sicurezza AEM</a>.</li>
     <li>Rispetta le impostazioni di controllo dell’accesso dell’utente e verifica le autorizzazioni appropriate.<br /> </li>
    </ol> </td>
  </tr>
  <tr>
   <td>Adobe Search&amp;Promote</td>
   <td><p>L'integrazione con Adobe Search &amp; Promote è obsoleta.</p> <p>Adobe non prevede di apportare ulteriori miglioramenti all’integrazione con Search&amp;Promote. Nota: l’integrazione con Search&amp;Promote rimane completamente supportata anche se obsoleta.</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Gestione tag DTM</td>
   <td>L’integrazione con DTM (Dynamic Tag Manager) è obsoleta.</td>
   <td>Inizia a utilizzare Adobe Experience Platform Launch come gestore di tag</td>
  </tr>
  <tr>
   <td>Adobe Target</td>
   <td>Poiché in AEM 6.5 è possibile connettere AEM al servizio Adobe Target tramite le API per Adobe Target Standard basate su I/O (API REST), il metodo API per Target Classic (XML) è stato dichiarato obsoleto.</td>
   <td><a href="https://helpx.adobe.com/experience-manager/kt/sites/using/aem-sites-target-standard-technical-video-understand.html">Riconfigura l’integrazione in modo da utilizzare le nuove API</a></td>
  </tr>
  <tr>
   <td>Adobe Target</td>
   <td>L’utilizzo dell’integrazione basata su mbox.js con Adobe Target in AEM è stata dichiarata obsoleta.</td>
   <td>Passa ad at.js 1.x</td>
  </tr>
  <tr>
   <td>Commerce</td>
   <td><p><a href="https://github.com/adobe/commerce-cif-api" target="_blank">CIF REST</a> è stato fornito nel 2018 come set di microservizi per consentire l’integrazione tra AEM e i motori di commercio.</p> <p>Dopo l'acquisizione di Magento da parte di Adobe a metà del 2018, Adobe ha deciso di cambiare approccio per due motivi: </p> <p><strong>1.</strong> Magento dispone di un proprio set di API Commerce (REST e GraphQL) e non è buona norma mantenere due set di API </p> <p><strong>2.</strong> Le tendenze del mercato hanno indicato che i clienti si stavano spostando verso GraphQL, perché è un modo più efficiente di interrogare i dati. Nel 2019, Adobe ha rilasciato il nuovo Commerce Integration Framework utilizzando le API GraphQL di Magento come fonte di verità.</p> <p>Adobe non intende effettuare ulteriori investimenti in CIF REST. Ai clienti viene consigliato di utilizzare la soluzione sostitutiva.</p> </td>
   <td><p>Per le integrazioni AEM-Magento, passa ai componenti core <a href="https://github.com/adobe/aem-cif-project-archetype" target="_blank">AEM CIF Archetype</a>e <a href="https://github.com/adobe/aem-core-cif-components" target="_blank">AEM CIF</a></p> <p>Per ulteriori informazioni, consulta <a href="https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/integrations.html#!AdobeDocs/commerce-cif-documentation/master/integrations/02-AEM-Magento.md" target="_blank">AEM e Integrazione Magento con Commerce Integration Framework</a> .</p> <p>Il sostegno alle integrazioni di terze parti (diverse da Magento) con il nuovo approccio è nella nostra tabella di marcia.</p> </td>
  </tr>
  <tr>
   <td>Componenti (AEM Sites)</td>
   <td><p>Adobe non prevede di apportare ulteriori miglioramenti alla maggior parte dei componenti di base in /libs/foundation/components.</p> <p>Cerca le proprietà <strong>cq:deprecated</strong> e <strong>cq:deprecatedReason</strong> nella cartella dei componenti.</p> <p>In AEM 6.5 sono inclusi i componenti di base e i clienti che effettuano l’aggiornamento da versioni precedenti possono continuare a utilizzarli così com’è. Inoltre, i componenti di base rimangono completamente supportati mentre vengono dichiarati obsoleti. </p> </td>
   <td>Consigliamo ai clienti di utilizzare i componenti core per i progetti futuri. Existing sites can remain as is or use the <a href="https://github.com/adobe/aem-modernize-tools">AEM Modernize Tools Suite</a> to refactor the site to use Core Components.</td>
  </tr>
  <tr>
   <td>Componenti (AEM Sites)</td>
   <td>I componenti Importazione progettazione /libs/wcm/designimporter/components sono stati contrassegnati come obsoleti a partire dalla versione 6.5. Adobe non intende apportare ulteriori miglioramenti a tale implementazione di Importazione progettazione.</td>
   <td>Adobe intende introdurre in versioni future un’implementazione alternativa per questo caso d’uso.</td>
  </tr>
  <tr>
   <td>Foundation</td>
   <td><p>Granite Offloading Framework</p> <p>Adobe non prevede di apportare ulteriori miglioramenti al framework di offload introdotto nella versione 5.6.1 per esternalizzare l’elaborazione delle risorse. </p> </td>
   <td>Adobe sta lavorando a un framework di offload cloud nativo di nuova generazione.</td>
  </tr>
  <tr>
   <td>Sviluppatori</td>
   <td><p>Hobbes.js</p> <p>Adobe non intende apportare ulteriori miglioramenti al framework di test dell'interfaccia utente di hobbes.js.</p> </td>
   <td>Adobe consiglia ai clienti di utilizzare l'automazione selenio.</td>
  </tr>
  <tr>
   <td>Sviluppatori</td>
   <td><p>Libreria client per interfaccia utente jQuery</p> <p>Adobe non prevede di mantenere e aggiornare ulteriormente la libreria client per interfaccia utente jQuery fornita come parte della distribuzione (Quickstart)</p> </td>
   <td>Adobe consiglia ai clienti che necessitano ancora di un’interfaccia utente jQuery per il codice, di aggiungerlo alla base di codice del progetto.</td>
  </tr>
  <tr>
   <td>Sviluppatori</td>
   <td><p>Libreria client jQuery Animation (granite.jquery.animation)</p> <p>Adobe non prevede di mantenere e aggiornare ulteriormente la libreria client per animazione jQuery fornita come parte della distribuzione (Quickstart)</p> </td>
   <td>Adobe consiglia ai clienti che necessitano ancora di animazioni jQuery per il proprio codice di aggiungerlo alla propria base di codice di progetto.</td>
  </tr>
  <tr>
   <td>Sviluppatori</td>
   <td><p>Libreria client handlebar</p> <p>Adobe non prevede di mantenere e aggiornare ulteriormente la libreria client per Handlebar fornita come parte della distribuzione (Quickstart)</p> </td>
   <td>Adobe consiglia ai clienti che necessitano ancora di Handlebars per il codice, di aggiungerlo alla propria base di codici di progetto.</td>
  </tr>
  <tr>
   <td>Sviluppatori</td>
   <td><p>Libreria client Lawnchair</p> <p>Adobe non prevede di mantenere e aggiornare ulteriormente la libreria client per Lawnchair fornita come parte della distribuzione (Quickstart)</p> </td>
   <td>Adobe consiglia ai clienti che necessitano ancora di una poltrona per il proprio codice di aggiungerlo alla propria base di codici di progetto.</td>
  </tr>
  <tr>
   <td>Sviluppatori</td>
   <td><p>Libreria client Granite.Sling.js</p> <p>Adobe non prevede di migliorare ulteriormente la libreria client Granite.Sling.js fornita come parte della distribuzione (Quickstart)</p> </td>
   <td>Adobe consiglia ai clienti che si affidano alla funzionalità della libreria di rigenerare il codice per non utilizzarlo più.</td>
  </tr>
  <tr>
   <td>Sviluppatori</td>
   <td>Utilizzo di YUI per comprimere/minimizzare le librerie client JavaScript. Adobe non prevede di aggiornare ulteriormente la libreria YUI. Fino a AEM 6.4, per impostazione predefinita, YUI ha ridotto a icona JavaScript con l'opzione per passare a Google Closure Compiler (GCC). A partire da AEM 6.5, GCC è l’impostazione predefinita.</td>
   <td>Adobe consiglia ai clienti di effettuare l’aggiornamento ad AEM 6.5 per passare al CC per la loro implementazione</td>
  </tr>
  <tr>
   <td>Sviluppatori</td>
   <td><p>Editor finestra di dialogo dell’interfaccia utente classica in CRXDE lite</p> <p>Adobe non prevede di migliorare ulteriormente l’Editor finestra di dialogo dell’interfaccia utente classica fornito come parte della distribuzione (Quickstart)</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Forms</td>
   <td><p>L'integrazione di AEM Forms con AEM Mobile&lt; è obsoleta </p> </td>
   <td>Nessuna sostituzione </td>
  </tr>
 </tbody>
</table>

## Funzioni rimosse {#removed-features}

In questa sezione sono elencate le funzionalità rimosse da AEM 6.5. Le versioni precedenti presentavano queste funzionalità contrassegnate come obsolete.

| Area | Funzione obsoleta | Sostituzione |
|--- |--- |--- |
| Activity Map di Analytics | Versione di Activity Map inclusa in AEM. | In seguito a modifiche di sicurezza in Adobe Analytics API, non è più possibile utilizzare la versione di Activity Map inclusa in AEM. Utilizzate il plug-in [ActivityMap fornito da Adobe Analytics](https://docs.adobe.complugin /content/help/en/analytics/analyze/activity-map/getting-started/get-started-users/activitymap-install.html). |
| Integrations (Integrazioni) | L&#39;integrazione ExactTarget è stata rimossa dalla distribuzione predefinita (Quickstart) e non è più disponibile. | Nessuna sostituzione |
| Integrations (Integrazioni) | L’integrazione delle API Force di Salesforce è stata rimossa dalla distribuzione predefinita (Quickstart) ed è ora un pacchetto aggiuntivo da installare da PackageShare. | La funzione è ancora disponibile. |
| Forms | Il supporto per il servizio Adobe Central Migration Bridge è stato rimosso in quanto il prodotto Adobe Central non è più supportato. | Nessuna sostituzione |
| Forms | `com.adobe.fd.df.fdinternal.model.ConfigurationInstance` | Nessuna sostituzione |
| Forms | `com.adobe.fd.ccm.channels.print.fdinternal.api.service.PrintDataTransformer` | Nessuna sostituzione |
| Forms | L&#39;aggiornamento single-hop da LiveCycle ES4 SP1 a AEM 6.5 Forms su JEE non è disponibile | Consulta i percorsi [di aggiornamento](../forms/using/upgrade.md) disponibili nella documentazione di aggiornamento di AEM Forms. |
| Forms | È stato rimosso il supporto del clustering basato su UPD da AEM Forms su JEE | In AEM Forms su JEE è possibile utilizzare solo il clustering basato su TCP. Se si aggiorna un server multicast UDP da una versione precedente a AEM 5.5 Forms su JEE, vengono eseguite configurazioni manuali per passare al clustering gemFire basato su TCP. Per istruzioni dettagliate, consultate [Aggiornamento ai moduli AEM 6.5 su JEE](../forms/using/upgrade-forms-jee.md) |
| Sviluppatori | Firebug Lite è stato rimosso dalla distribuzione predefinita (Quickstart) | Utilizza le console di sviluppo integrate nel browser |
| Sviluppatori | Remove `customJavaScriptPath` support in HTML Client Library Manager. | Nessuna sostituzione |
| Assets | La funzione di scaricamento delle risorse è stata rimossa in AEM 6.5 | Nessuna sostituzione |
| Cache | `system/console/slingjsp` is remove non è più disponibile in AEM 6.5. | Le classi e la cache di Luminosità vengono memorizzate nel pacchetto Apache Sling Commons FileSystem ClassLoader. Potete controllare il numero del bundle nella console Web di AEM e rimuovere la cartella della cache direttamente dal file system (`crx-quickstart/launchpad/felix/bundle<ID>`). |

## Pre-annuncio per rilascio successivo {#pre-announcement-for-next-release}

In questa sezione vengono pre-annunciate le modifiche future che non riguardano funzioni dichiarate obsolete, ma che hanno un impatto sui clienti. Queste informazioni vengono fornite a scopo di pianificazione.

| Area | Funzione obsoleta | Annuncio |
|--- |--- |--- |
| Foundation | Framework interfaccia utente | Adobe prevede di rendere obsoleti i componenti Coral UI 2 nel 2019. L’interfaccia Coral UI 3 è stata introdotta con AEM 6.2 e AEM 6.5 è completamente basato su Coral 3. Adobe consiglia ai clienti e ai partner che hanno creato delle interfacce utente personalizzate con Coral 2 di eseguire il refactoring per Coral 3. Adobe fornisce uno strumento per convertire le finestre di dialogo Coral 2 in Coral 3. [Ulteriori informazioni](/help/sites-developing/dialog-conversion.md). |
