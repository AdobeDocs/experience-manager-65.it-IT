---
title: Glossario di AEM Forms
description: Il glossario di AEM Forms fornisce un elenco completo dei termini chiave, delle definizioni e dei concetti utilizzati in Adobe Experience Manager Forms (AEM Forms), per aiutare gli utenti a comprendere e utilizzare i moduli adattivi e le funzioni correlate.
feature: Adaptive Forms
role: Admin, User, Developer
hidefromtoc: true
hide: true
source-git-commit: 37f471e09c13b7ab036ab1043d11dfed98da1d97
workflow-type: tm+mt
source-wordcount: '1773'
ht-degree: 1%

---

# Glossario di AEM Forms

## [Moduli adattivi](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/create-an-adaptive-form-on-forms-cs/creating-adaptive-form)

Moduli dinamici e reattivi che ne modificano layout e presentazione in base al dispositivo e all’input dell’utente, migliorando l’esperienza utente su varie piattaforme. Include logica condizionale, associazione dati dinamica e comportamento basato su regole.

## [Controllo delle versioni dei moduli adattivi](https://experienceleague.adobe.com/it/docs/experience-manager-65/content/forms/adaptive-forms-core-components/add-versioning-reviews-comments)

Capacità di gestire più versioni di un modulo nell’archivio utilizzando il controllo delle versioni dei nodi JCR. Assicura audit trail e un facile rollback per i moduli adattivi.

## [Integrazione Adobe Analytics Forms](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/forms/integrate/services/enable-adobe-analytics-adaptive-form-using-experience-cloud-setup-automation)

Fornisce informazioni dettagliate sulle interazioni degli utenti (ad esempio, abbandono dei campi, tempo trascorso per sezione) con Adobe Analytics, consentendo un’ottimizzazione della progettazione dei moduli basata sui dati.

## [Pacchetto Del Componente Aggiuntivo AEM Forms](https://experienceleague.adobe.com/it/docs/experience-manager-65/content/forms/install-aem-forms/osgi-installation/installing-configuring-aem-forms-osgi)

Applicazione distribuita in Adobe Experience Manager (AEM) come pacchetto, contenente servizi (provider API) e servlet o JSP gestiti dal framework Sling dell’AEM.

## [AEM Forms su JEE](https://experienceleague.adobe.com/it/docs/experience-manager-65/content/forms/install-aem-forms/jee-installation/aem-forms-jee-supported-platforms)

Un’opzione di implementazione di AEM Forms che sfrutta i server Java Enterprise Edition (JEE), fornendo scalabilità a livello aziendale, gestione delle transazioni e supporto per flussi di lavoro aziendali complessi.

## [AEM Forms su OSGi](https://experienceleague.adobe.com/it/docs/experience-manager-65/content/implementing/deploying/introduction/technical-requirements)

AEM Forms nell’ambiente OSGi è il pacchetto standard AEM Author o AEM Publish con AEM Forms implementato. Puoi eseguire AEM Forms su OSGi in un ambiente server singolo, in una farm e in configurazioni cluster. La configurazione del cluster è disponibile solo per le istanze di creazione AEM.

## [Adobe Sign in AEM Forms](https://experienceleague.adobe.com/it/docs/experience-manager-65/content/forms/adaptive-forms-advanced-authoring/adobe-sign-integration-adaptive-forms)

Un servizio RESTful per flussi di lavoro di firma digitale sicuri e fluidi. Si integra con AEM Forms utilizzando l’autenticazione basata su OAuth, consentendo la raccolta automatizzata delle firme e il tracciamento in tempo reale.

## [Servizi documentali AEM Forms 6.5](https://experienceleague.adobe.com/it/docs/experience-manager-65/content/forms/use-document-services/overview-aem-document-services)

API fornite dal livello web di AEM Forms per l’utilizzo remoto da parte di client basati su HTTP, come i moduli per dispositivi mobili SDK.Funzionalità all’interno di AEM Forms che consentono la creazione, l’assemblaggio, la distribuzione e l’archiviazione di documenti PDF, l’aggiunta di firme digitali e la decodifica di Forms in codice a barre.

| **Nome servizio** | **Descrizione** | **Collegamento alla documentazione** |
|------------------------------|---------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------|
| **Servizio Forms** | Esegui il rendering dei PDF forms utilizzando modelli e XML, integra i dati del modulo per l’importazione o l’esportazione e supporta il rendering basato su frammenti. | [Documentazione del servizio Forms](https://experienceleague.adobe.com/it/docs/experience-manager-65/content/forms/use-document-services/output-service) |
| **Servizio di output** | Genera documenti unendo dati con modelli in formati come PDF, PCL o PostScript. | [Documentazione del servizio di output](https://experienceleague.adobe.com/it/docs/experience-manager-65/content/forms/use-document-services/output-service) |
| **Servizio assemblatore** | Combina, riorganizza, convalida e migliora i documenti PDF e XDP. | [Documentazione del servizio Assembler](https://experienceleague.adobe.com/it/docs/experience-manager-65/content/forms/use-document-services/assembler-service) |
| **Converti servizio PDF** | Converte i documenti PDF in PostScript o in formati immagine come PNG, JPEG o TIFF. | [Documentazione del servizio ConvertPDF](https://experienceleague.adobe.com/it/docs/experience-manager-65/content/forms/use-document-services/using-convertpdf-service) |
| **Servizio Forms in codice a barre** | Estrae dati dai codici a barre nei file TIFF e PDF per automatizzare i processi di acquisizione dei dati. | [Documentazione del servizio Forms in codice a barre](https://experienceleague.adobe.com/it/docs/experience-manager-65/content/forms/use-document-services/using-barcoded-forms-service) |
| **Servizio DocAssurance** | Crittografia, decrittografia, firma digitale e applicazione dei criteri di protezione dei documenti ai PDF. | [Documentazione del servizio DocAssurance](https://experienceleague.adobe.com/it/docs/experience-manager-65/content/forms/use-document-services/overview-aem-document-services#doc-assurance-service) |
| **Servizio PDF Generator** | Converte i formati di file nativi (ad esempio: Microsoft Word, Excel) in documenti PDF. | [Documentazione del servizio PDF Generator](https://experienceleague.adobe.com/it/docs/experience-manager-65/content/forms/use-document-services/aem-document-services-programmatically#pdfgeneratorservice) |

## [API di comunicazione as a Cloud Service di Forms](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction)

AEM Forms as a Cloud Service fornisce strumenti avanzati per la gestione di moduli e flussi di lavoro di comunicazione, con supporto per la creazione di moduli digitali, l’acquisizione di dati e le comunicazioni personalizzate. Le API di comunicazione cloud forniscono generazione, manipolazione, convalida e integrazione sicura dei documenti on-demand e batch con sistemi esterni tramite HTTP, garantendo operazioni semplificate e sicure.

| **Nome servizio** | **Descrizione** | **Collegamento alla documentazione** |
|-------------------------------|------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------|
| **Generazione documento** | Combinare un modello (XFA o PDF) con dati XML per generare documenti in formati PDF e di stampa come PS, PCL, DPL, IPL e ZPL. | [Documentazione sulla generazione di documenti](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction.html?lang=it#document-generation) |
| **Manipolazione documento** | Combinare e ridisporre i documenti di PDF. | [Documentazione sulla manipolazione dei documenti](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction#document-manipulation) |
| **Conversione documento** | Converti un PDF in PDF/A e verifica la conformità di PDF/A. | [Documentazione sulla conversione dei documenti](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction#document-conversion) |
| **Documento Assurance** | Aggiungere o rimuovere campi di firma, firmare, certificare, crittografare, decrittografare e applicare diritti di utilizzo ai documenti PDF. | [Documentazione di Document Assurance](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction#doc-assurance) |
| **Firme digitali** | Integra Adobe Sign per la firma elettronica sicura di moduli e documenti. | [Documentazione sulle firme digitali](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction.html?lang=it#digital-signatures) |


## [AEM Forms Workbench](https://experienceleague.adobe.com/it/docs/experience-manager-65/content/forms/install-aem-forms/jee-installation/install-workbench)

Applicazione desktop per la creazione, la modifica e la distribuzione di flussi di lavoro, nonché per la gestione di processi aziendali incentrati sui moduli. Offre integrazione con i servizi e i sistemi back-end.

## [Archetipo](https://experienceleague.adobe.com/it/docs/experience-manager-core-components/using/developing/archetype/overview)

Modello o modello in AEM utilizzato per generare un nuovo progetto con una struttura predefinita, che facilita la standardizzazione, la configurazione rapida e l’adesione alle best practice per lo sviluppo dell’AEM.

## [Istanza Autore](https://experienceleague.adobe.com/it/docs/experience-manager-65/content/forms/publish-process-aem-forms/publishing-unpublishing-forms)

L’ambiente in cui i creatori e gli amministratori di contenuti progettano, creano e gestiscono i contenuti prima di pubblicarli. Supporta il controllo delle versioni, l&#39;anteprima e il test.

## [Creazione front-end](https://experienceleague.adobe.com/it/docs/experience-manager-65/content/forms/install-aem-forms/aem-forms-architecture-deployment#architecture)

Interfaccia utente per la creazione e la gestione dei moduli in AEM Forms.

## [Blocco modulo adattivo](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/edge-delivery/build-forms/forms-references/form-components)

Unità di incapsulamento che raggruppa in modo logico componenti e metadati correlati, consentendo la gestione dinamica dei dati e una facile scalabilità in moduli in più fasi.

## [Componenti di base](https://experienceleague.adobe.com/it/docs/experience-manager-core-components/using/adaptive-forms/introduction)

Blocchi predefiniti riutilizzabili per la creazione di moduli, inclusi campi modulo, contenitori di layout, pulsanti e altri elementi interattivi.

## [Gestione della corrispondenza](https://experienceleague.adobe.com/it/docs/experience-manager-65/content/forms/letters-correspondences/cm-overview)

Modulo che consente alle aziende di creare, gestire e distribuire corrispondenza personalizzata utilizzando modelli, regole e origini dati predefiniti. Include modelli di lettere, comunicazioni con i clienti e generazione batch.

## [CRX (Content repository extreme)](https://experienceleague.adobe.com/it/docs/experience-manager-65/content/forms/use-aem-forms-workspace/html-workspace-architecture)

Java Content Repository (JCR) integrato in AEM che memorizza dati strutturati e non strutturati, consentendo l’archiviazione gerarchica di contenuti, modelli e configurazioni.

## [Componente personalizzato](https://experienceleague.adobe.com/it/docs/experience-manager-core-components/using/adaptive-forms/customize-adaptive-forms-core-components)

Un componente personalizzato che estende la funzionalità di AEM Forms, sviluppato utilizzando modelli Sling, Sightly (HTL) e Java. Generalmente utilizzato per una logica di business univoca o per l’interattività lato client avanzata.

## [XCI personalizzato (informazioni configurazione XML)](https://experienceleague.adobe.com/it/docs/experience-manager-65/content/forms/administrator-help/configure-forms/specifying-xci-configuration-options)

In Adobe Experience Manager (AEM) Forms, un file XCI (XML Configuration Information) personalizzato consente agli amministratori di definire proprietà di rendering specifiche per moduli e documenti. Configurando le impostazioni XCI nella console di amministrazione, puoi sostituire le impostazioni predefinite di sistema con opzioni personalizzate, garantendo un’elaborazione e una presentazione personalizzate dei moduli.

## [Integrazione dei dati](https://experienceleague.adobe.com/it/docs/experience-manager-65/content/forms/form-data-model/data-integration)

Integrazione perfetta di origini dati esterne, come database, servizi web o API REST, in moduli e flussi di lavoro per abilitare esperienze utente dinamiche e personalizzate.

## [Origini dati](https://experienceleague.adobe.com/it/docs/experience-manager-65/content/forms/form-data-model/configure-data-sources)

Interfacce per l&#39;integrazione di dati esterni nei moduli, tra cui JDBC per database relazionali, endpoint REST per servizi Web e OData per sistemi SAP. Gestito tramite AEM Forms Data Integration Framework.

## [Frammenti di documenti](https://experienceleague.adobe.com/it/docs/experience-manager-65/content/forms/letters-correspondences/lists)

Componenti riutilizzabili di documenti, quali intestazioni, piè di pagina, clausole di esclusione di responsabilità o clausole, che possono essere inclusi in modo dinamico nei moduli o nella corrispondenza per garantire la coerenza.

## [Documento record (DoR)](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/generate-document-of-record-for-non-xfa-based-adaptive-forms)

Funzione di AEM Forms che genera una versione di archiviazione non modificabile di un modulo inviato, in genere in formato PDF, mantenendo il contenuto e il layout esatti come record della transazione.

## [Edge Delivery Services](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/edge-delivery/overview)

Distribuzione ottimizzata dei contenuti per AEM Forms, con latenza ridotta per risorse quali moduli, temi e librerie client, dove gli autori possono aggiornare e pubblicare rapidamente i contenuti.

## [Integrazione Forms](https://experienceleague.adobe.com/it/docs/experience-manager-65/content/forms/form-data-model/data-integration)

Comporta la connessione di AEM Forms ai sistemi aziendali (ad esempio, SAP, Salesforce) utilizzando bundle e connettori OSGi, supportando flussi di dati bidirezionali e aggiornamenti in tempo reale.

## [Revisione modulo](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/create-reviews-forms)

Funzione basata su flusso di lavoro che consente alle parti interessate di rivedere i moduli adattivi, aggiungere annotazioni e approvare modifiche prima della pubblicazione. Utilizza la casella in entrata AEM e la gestione delle attività.

## [Modello dati modulo (FDM)](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/using-form-data-model)

Un livello di rappresentazione che collega i moduli adattivi alle origini dati back-end, consentendo l’integrazione con i servizi web RESTful, i servizi SOAP e OData. FDM consente agli autori dei moduli di mappare i campi modulo direttamente alle strutture di dati back-end, garantendo una sincronizzazione perfetta dell’input dell’utente con i sistemi esterni.

## [Localizzazione modulo](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/supporting-new-language-localization)

Il processo dei moduli adattivi per supportare più lingue e impostazioni internazionali, garantendo che i moduli siano accessibili e di facile utilizzo per un pubblico diverso.

## [Portale moduli](https://experienceleague.adobe.com/it/docs/experience-manager-65/content/forms/use-forms-portal/creating-form-portal-page)

I componenti di Forms Portal consentono agli sviluppatori Web di creare e personalizzare un portale Forms nei siti Web creati con Adobe Experience Manager (AEM). Consente agli utenti di individuare, accedere e inviare moduli in modo efficiente su piattaforme web e mobili.

## [Rendering modulo e invio front-end](https://experienceleague.adobe.com/it/docs/experience-manager-65/content/forms/install-aem-forms/aem-forms-architecture-deployment#architecture)

Interfaccia utente in AEM Forms che consente agli utenti di visualizzare e inviare moduli tramite un browser Web.

## [Set di moduli](https://experienceleague.adobe.com/it/docs/experience-manager-65/content/forms/html5-forms/formset-in-aem-forms)

Una raccolta di moduli correlati raggruppati insieme per essere presentati come un’unica entità agli utenti, consentendo di suddividere in sezioni gestibili i processi complessi di raccolta dati.

## [Forms Designer](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/forms/using-communications/installing-configuring-designer)

Applicazione autonoma utilizzata per progettare modelli di moduli in moduli XDP e utilizzarla nell’AEM Forms per generare documenti di record.

## [Flusso di lavoro incentrato su Forms](https://experienceleague.adobe.com/it/docs/experience-manager-65/content/forms/workflows/aem-forms-workflow)

Un set di passaggi automatizzati o manuali in AEM Forms che gestiscono i processi aziendali, ad esempio l’approvazione di documenti, la pubblicazione di contenuti o le notifiche degli utenti.

## [Comunicazione interattiva](https://experienceleague.adobe.com/it/docs/experience-manager-65/content/forms/getting-started/interactive-communications-overview)

Implementazione personalizzata per la gestione di comunicazioni multicanale altamente personalizzate. Combina dati provenienti da varie fonti, come sistemi CRM o ERP, per fornire comunicazioni in formati quali web, dispositivi mobili, e-mail e stampa.

## [JCR (Java Content Repository)](https://experienceleague.adobe.com/it/docs/experience-manager-learn/cloud-service/underlying-technology/introduction-jcr)

Repository gerarchico basato su standard per l&#39;archiviazione di contenuti, configurazioni e metadati in AEM, che supporta l&#39;archiviazione di dati strutturati e non strutturati.

## [Lettere](https://experienceleague.adobe.com/it/docs/experience-manager-65/content/forms/letters-correspondences/create-letter#create-a-letter-template)

Comunicazioni con i clienti generate utilizzando AEM Forms Document Services. Le lettere vengono create utilizzando una combinazione di modelli XDP, modelli di dati e frammenti riutilizzabili, garantendo scalabilità in scenari con volumi elevati.

## [Metadati in AEM Forms](https://experienceleague.adobe.com/it/docs/experience-manager-65/content/forms/manage-administer-aem-forms/manage-form-metadata)

I metadati consentono di categorizzare e recuperare in modo efficiente le risorse. AEM Forms include metadati predefiniti per ogni tipo di risorsa e ne consente la personalizzazione. Fornisce inoltre strumenti per creare, gestire e scambiare metadati in modo semplice.

## [PDF Generator](https://experienceleague.adobe.com/it/docs/experience-manager-learn/forms/document-services/using-pdfg-in-aem-forms)

Strumento di AEM Forms che converte vari formati di file (ad esempio Word, Excel e PowerPoint) in documenti PDF e fornisce funzionalità quali crittografia, filigrana e unione.

## [Istanza Publish](https://experienceleague.adobe.com/it/docs/experience-manager-65/content/forms/publish-process-aem-forms/publishing-unpublishing-forms)

L’ambiente in AEM che fornisce contenuti live agli utenti finali. Fornisce moduli, pagine e altre esperienze digitali con prestazioni ottimizzate.

## [Editor regole](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/rule-editor-core-components/rule-editor-core-components)

Strumento visivo in Adaptive Forms che consente agli autori di definire regole e logiche personalizzate per i campi modulo, ad esempio visibilità, convalida e precompilazione dei dati, senza richiedere competenze di codifica.

## [Firme scarabocchio](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/add-components-to-an-adaptive-form/signing-forms-using-scribble)

Funzione di AEM Forms che consente agli utenti di firmare elettronicamente i moduli disegnando la propria firma direttamente sul modulo utilizzando un mouse o un dispositivo touch.

## [Azione di invio in AEM Forms](https://experienceleague.adobe.com/it/docs/experience-manager-65/content/forms/adaptive-forms-basic-authoring/configuring-submit-actions)

Azioni lato server o lato client eseguite all’invio del modulo. Alcuni esempi includono chiamate REST API, il richiamo di un flusso di lavoro o la scrittura di dati in un JCR (Java Content Repository).

## [Temi](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/using-themes-in-core-components)

Framework di stile basati su CSS applicati ai moduli adattivi, utilizzando LESS/SASS per i preprocessori. I temi garantiscono la conformità con le linee guida di branding e gli standard di accessibilità, consentono di personalizzare un tema, modificarne gli elementi di progettazione, il layout, i colori, la composizione tipografica e, a volte, il codice sottostante.

## [Modello](https://experienceleague.adobe.com/it/docs/experience-manager-core-components/using/adaptive-forms/sample-themes-templates-form-data-models-core-components)

Blueprint per moduli adattivi, contenenti elementi strutturali (campi, layout) e script preconfigurati, puoi creare e personalizzare nuovi modelli o utilizzare modelli preconfigurati esistenti.

## [Livello Web](https://experienceleague.adobe.com/it/docs/experience-manager-65/content/forms/install-aem-forms/aem-forms-architecture-deployment#architecture)

Comprende JSP o servlet costruiti su servizi comuni e forms, che forniscono funzionalità quali authoring front-end, rendering e invio di moduli front-end e API REST.

## [XDP (pacchetto dati XML)](https://experienceleague.adobe.com/it/docs/experience-manager-65/content/forms/manage-administer-aem-forms/get-xdp-pdf-documents-aem)

Formato di file utilizzato in AEM Forms per la progettazione e la strutturazione dei moduli, che consente il rendering come PDF o HTML, supportando al contempo il contenuto dinamico e l’interattività.

## [XFA (XML Forms Architecture)](https://experienceleague.adobe.com/it/docs/experience-manager-65/content/forms/adaptive-forms-basic-authoring/creating-adaptive-form#create-an-adaptive-form-based-on-an-xfa-form-template)

Una tecnologia legacy per la creazione di PDF forms interattivi e dinamici. I moduli XFA offrono funzionalità avanzate, come regolazioni del layout dinamico, scripting e integrazione perfetta con i sistemi back-end.

## [Schema XML o JSON](https://experienceleague.adobe.com/it/docs/experience-manager-65/content/forms/adaptive-forms-basic-authoring/creating-adaptive-form#create-an-adaptive-form-based-on-xml-or-json-schema)

Struttura standardizzata utilizzata per definire il formato e l’organizzazione dei dati XML o JSON nei moduli e nei flussi di lavoro. Questi schemi garantiscono una gestione coerente dei dati e consentono l’interoperabilità con i sistemi esterni.

<!--

## **Custom Properties**  

Developer-defined metadata attributes added to components or forms for advanced behaviors, accessed via Sling APIs or Groovy scripts for dynamic processing.

## **Embedding** 

Integrating adaptive forms into AEM Sites or external web pages using `<iframe>` or SPA (Single Page Application) models. Embedding supports seamless session handling and cross-origin resource sharing (CORS).

## **CDN (Content Delivery Network)**  

Distributed networks (e.g., Akamai) used for caching and delivering forms-related resources, ensuring high availability and faster load times for geographically distributed users.


## **Dispatcher**  

An AEM caching and load balancing tool configured to optimize delivery of adaptive forms. Its filter rules ensure secure access control while caching frequently accessed forms and assets.

## **Editors**  

Tools like the Adaptive Forms Editor, Theme Editor, and Rule Editor, enabling developers and content authors to customize forms and their behavior without extensive coding.

## **Responsive UI**  

An implementation of media queries and flexible grids, ensuring adaptive forms render seamlessly across various screen sizes and devices.

## **Custom Functions**  

JavaScript-based utilities or REST microservices that provide additional logic (e.g., complex field validation or data pre-population), extending the out-of-the-box capabilities of AEM Forms.

## **Package Manager**  

AEM's CRX Package Manager facilitates importing/exporting adaptive forms, data schemas, or configurations as .zip files, enabling modular deployment in distributed environments.

## **UE (User Experience)**  

Design principles and optimizations applied in AEM Forms to enhance usability, including accessibility features (ARIA roles, tab navigation) and intuitive layouts.

## **Forms Submission Services**

Back-end services for handling form submissions, integrating with the AEM Workflow engine, third-party APIs, or direct JCR persistence.


Foundation components
e-signing
adobe sign
letters
submit action
data sources
adaptive form block
edge delivery services
forms integration
custom component 
themes
template 
custom properties
embedding
CDN
Dispatcher
editors
responsive UI
custom functions
package manager
communication APIs
UE
Forms submission services
Form review
Forms Versioning
Adobe analytics forms integration specific

## **AEM Forms Foundation Components**  
Core reusable elements within AEM Forms, built on Granite UI, enabling developers to create complex forms. They provide robust features like data bindings, field validations, and support for multilingual content.


## **e-Signing**  
An implementation of digital signature standards (e.g., PKCS #7) within AEM Forms, integrated with Adobe Sign APIs to ensure secure and legally binding electronic signatures.

## Workspace

A browser-based interface for users to interact with AEM Forms workflows, tasks, and approvals.

## Sling

A REST-based web framework used in AEM to map request URLs to content resources, enabling efficient content rendering and delivery.

-->