---
title: Riepilogo delle nuove funzioni| Moduli AEM 6.5
seo-title: Riepilogo delle nuove funzioni| Moduli AEM 6.5
description: Ultime funzioni e miglioramenti a moduli e documenti della soluzione di gestione dell'esperienza digitale più avanzata al mondo.
seo-description: Ultime funzioni e miglioramenti a moduli e documenti della soluzione di gestione dell'esperienza digitale più avanzata al mondo.
uuid: 179d372d-b7f6-4771-8349-fc6b7854efac
topic-tags: introduction
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 0e949429-cd5f-4301-aa72-14803cdfab00
docset: aem65
translation-type: tm+mt
source-git-commit: 726163106ddb80600eaa7cc09b1a2e9b035a223e

---


# Riepilogo delle nuove funzioni| Moduli AEM 6.5{#new-features-summary-aem-forms}

## Report transazione {#transaction-reports}

I rapporti sulle transazioni consentono di acquisire e tenere traccia del numero di moduli inviati, documenti elaborati e documenti sottoposti a rendering. L&#39;obiettivo dietro il monitoraggio di queste transazioni è quello di prendere una decisione informata sull&#39;utilizzo del prodotto e sul ribilanciamento degli investimenti in hardware e software. Alcuni esempi di transazioni includono:

* Invio di un modulo adattivo, un modulo HTML5 o un set di moduli
* Rendering di una versione cartacea o Web di una comunicazione interattiva
* Conversione di un documento da un formato di file a un altro

Per informazioni sulla configurazione e l&#39;utilizzo dei rapporti sulle transazioni, vedere Panoramica [dei rapporti sulle](../../forms/using/transaction-reports-overview.md)transazioni.

![Un esempio di rapporto sulle transazioni](assets/surface_transaction_reporting.png)

## Comunicazioni interattive {#interactive-communications}

**Definire i pattern di visualizzazione dei dati**

Gli autori delle comunicazioni interattive ora possono definire pattern [di visualizzazione dei](create-interactive-communication.md#datadisplaypatterns) dati per campi, variabili ed elementi del modello di dati del modulo. Ad esempio, i formati data, valuta o telefono.

**Utilizzare nuovi tipi di grafici**

È ora possibile aggiungere grafici [quadranti e grafici con più serie](../../forms/using/chart-component-interactive-communications.md) alle comunicazioni interattive.

**Ordinare le colonne in una tabella**

È ora possibile [ordinare le colonne di una tabella](../../forms/using/create-interactive-communication.md#sortcolumns) nella comunicazione interattiva. È possibile eseguire il binding e l&#39;ordinamento delle colonne di tabella con oggetti di testo statici o modelli di dati.

**Utilizzare nuovi componenti in un canale Web**

È ora possibile aggiungere i componenti Pulsante e Separatore al canale Web. Per ulteriori informazioni, vedere [Aggiungi componente Pulsante al canale](../../forms/using/create-interactive-communication.md#add-button-component-to-the-web-channel) Web e Componente [Separatore nel canale](../../forms/using/create-interactive-communication.md#separatorcomponent)Web.

**Modalità Layout per ridimensionare i componenti**

È ora possibile passare alla modalità [](../../forms/using/resize-using-layout-mode.md) Layout per ridimensionare i componenti nel canale Web utilizzando un&#39;interfaccia WYSIWYG.

**Miglioramenti a livello di usabilità**

Gli autori delle comunicazioni interattive possono ora utilizzare varie operazioni di facile utilizzo durante la creazione delle corrispondenze. L&#39;elenco delle operazioni comprende:

* [Esecuzione di azioni Annulla-Ripristina nei canali di stampa e Web](../../forms/using/create-interactive-communication.md#undoredoactions)
* [Aggiunta di variabili in un frammento di documento tramite il simbolo @](../../forms/using/texts-interactive-communications.md#searchvariables)
* [Aggiunta di elementi del modello dati in un frammento di documento tramite il simbolo @](../../forms/using/texts-interactive-communications.md#searchdatamodelproperties)
* [Eliminazione o aggiunta di un canale Web a una comunicazione interattiva esistente](../../forms/using/create-interactive-communication.md#edit-interactive-communication-properties)
* [Binding degli elementi dell&#39;origine dati con campi e variabili mediante azioni di trascinamento](../../forms/using/create-interactive-communication.md#binddatasourceelements)
* [Evidenziazione di campi e variabili non associati durante la creazione di comunicazioni interattive](../../forms/using/create-interactive-communication.md#distinguishunboundfields)
* [Eseguire azioni aggiuntive, ad esempio copiare, raggruppare o altro su componenti ereditati in un canale Web](../../forms/using/create-interactive-communication.md#componenttoolbar)

**Miglioramenti nel processo di sincronizzazione**

Sono stati introdotti diversi miglioramenti nel layout del canale Web generato automaticamente tramite il canale di stampa.

![Grafici per le comunicazioni interattive](assets/interactive-communication-charts.png)

## Moduli adattivi {#adaptive-forms}

### Utilizzare le firme digitali basate sul cloud di Adobe Sign nei moduli adattivi {#use-adobe-sign-s-cloud-based-digital-signatures-in-adaptive-forms}

[Le firme](https://helpx.adobe.com/sign/kb/digital-certificate-providers.html) digitali o le firme remote basate su cloud sono una nuova generazione di firme digitali utilizzabili tra computer desktop, dispositivi mobili e Web. e soddisfare i massimi livelli di conformità e garanzia per l&#39;autenticazione dei firmatari. È ora possibile [firmare un modulo](../../forms/using/working-with-adobe-sign.md) adattivo con firme digitali basate su cloud.

#### Incorporare un modulo adattivo o una comunicazione interattiva nelle applicazioni di pagina singola AEM Sites {#embed-an-adaptive-form-or-interactive-communcation-in-aem-sites-single-page-applications}

AEM Forms consente di incorporare [facilmente un modulo](../../forms/using/embed-adaptive-form-aem-sites-spa.md) adattivo o una comunicazione interattiva in un’applicazione SPA (Single Page Application) AEM Sites. Il modulo adattivo e la comunicazione interattiva incorporati sono completamente funzionanti e gli utenti possono compilare e inviare il modulo senza uscire dalla pagina. Consente agli utenti di restare nel contesto di altri elementi della pagina Web e di interagire contemporaneamente con il modulo adattivo o la comunicazione interattiva.

#### Ordinare le colonne di tabelle Modulo adattivo {#sort-columns-of-adaptive-form-tables}

È possibile [ordinare qualsiasi colonna di una tabella](../../forms/using/adaptive-forms-tables.md#sortcolumnstable) Modulo adattivo in ordine crescente o decrescente. È possibile applicare l&#39;ordinamento alle colonne di tabella con testo statico, proprietà dell&#39;oggetto modello dati o una combinazione di proprietà statiche dell&#39;oggetto testo e modello dati.

#### Limitare la disponibilità di modelli di moduli adattivi per percorsi specifici {#restrict-the-availability-of-adaptive-forms-templates-to-specific-paths}

I moduli adattivi hanno aggiunto il supporto per la proprietà cq:allowPaths. La proprietà [limita la disponibilità dei modelli di moduli adattivi a percorsi](../../forms/using/creating-adaptive-form.md#main-pars-text)specifici.

#### Aggiunta dinamica delle caselle di controllo al modulo adattivo {#add-check-boxes-to-the-adaptive-form-dynamically}

È ora possibile definire regole per [aggiungere al modulo adattivo le caselle di controllo in modo dinamico](../../forms/using/rule-editor.md#setpropertyrule) in base a una funzione personalizzata, a un oggetto modulo o a una proprietà oggetto.

## Flussi di lavoro AEM {#aem-workflows}

### Utilizzare le variabili nei flussi di lavoro AEM {#use-variables-in-aem-workflows}

Le variabili consentono ai passaggi del flusso di lavoro di contenere e trasmettere i metadati tra le fasi del flusso di lavoro in fase di esecuzione. È possibile creare diversi tipi di variabili per memorizzare diversi tipi di dati. Ad esempio, numeri interi, stringhe, documenti o istanze del modello dati del modulo. In genere, si utilizza una variabile o una raccolta di variabili quando è necessario prendere una decisione in base al valore che contiene o per memorizzare le informazioni necessarie in un secondo momento in un processo.

Le variabili sono un&#39;estensione dell&#39;interfaccia [MetaDataMap](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/metadata/MetaDataMap.html) disponibile nella versione precedente. Consente di risparmiare tempo nello sviluppo di codice ECMAScript personalizzato utilizzato per recuperare e aggiornare i valori dei metadati. Continuate a utilizzare l’interfaccia MetaDataMap e il codice ECMAScript per manipolare i metadati. Alcuni vantaggi dell’utilizzo di variabili tramite MetaDataMap ed ECMAScript sono:

* Memorizzare, aggiornare e utilizzare in modo dinamico i valori memorizzati in una variabile all&#39;interno di un flusso di lavoro senza ricorrere al codice personalizzato
* Recuperare e aggiornare i valori direttamente in un modello dati e in un file dati del modulo (XML/JSON) di un modulo inviato
* Archiviare documenti completi in una variabile per eseguire l&#39;elaborazione dei documenti

Il passaggio Vai a, O Dividi e tutti i passaggi del flusso di lavoro di AEM Forms supportano le variabili. Puoi utilizzare l’interfaccia MetaDataMap per accedere alle variabili nei passaggi del flusso di lavoro che non dispongono di un supporto nativo per le variabili. Per ulteriori informazioni, consultate [Variabili nei flussi di lavoro](../../forms/using/variable-in-aem-workflows.md)AEM.

![Impostazione di una variabile per in un flusso di lavoro](assets/variable.png)

#### Utilizzare un flusso di lavoro con diversi moduli adattivi {#use-a-workflow-with-different-adaptive-forms}

È possibile [specificare un modulo adattivo per l&#39;attività](../../forms/using/aem-forms-workflow-step-reference.md#assign-task-step) di assegnazione e il passaggio del documento del record dei flussi di lavoro incentrati sui moduli in fase di esecuzione. Consente di utilizzare un flusso di lavoro con diversi moduli adattivi. È possibile scegliere il metodo per selezionare un modulo adattivo durante la progettazione del flusso di lavoro. Il modulo adattivo può trovarsi in un percorso assoluto, essere inviato come payload al flusso di lavoro o essere disponibile in un percorso calcolato utilizzando una variabile.

#### Utilizzare funzionalità di registrazione avanzate per i passaggi di flusso di lavoro incentrati sui moduli {#use-enhanced-logging-capabilities-of-forms-centric-workflow-steps}

Le funzionalità di registrazione dei passaggi di flusso di lavoro incentrati sui moduli sono standardizzate. Ora, tutti i passaggi del flusso di lavoro incentrati sui moduli producono file di registro standardizzati simili. Consente di migliorare la velocità di debug.

## Integrazione dei dati {#data-integration}

È ora possibile:

* [Convalida dei dati](../../forms/using/work-with-form-data-model.md#automated-validation-of-input-data) di input in base a un elenco di vincoli. In questo modo si garantisce che solo i dati validi vengano inviati all&#39;origine dati.
* [Ignora endpoint](../../forms/using/configure-data-sources.md#configure-soap-web-services) predefinito definito in un file WSDL (Web Services Description Language).

* [Ignora](../../forms/using/configure-data-sources.md#configure-restful-web-services) schema predefinito [, host e percorso](../../forms/using/configure-data-sources.md#configure-restful-web-services) base definiti nel file di definizione Swagger.

## Aggiornamenti per piattaforma e sicurezza {#platform-and-security-updates}

### Aggiornamenti principali delle piattaforme {#major-platform-updates}

I moduli AEM possono essere configurati utilizzando qualsiasi combinazione di sistemi operativi, server applicazione, database, driver di database, JDK, server LDAP e server e-mail supportati. Di seguito sono riportate le principali modifiche apportate alle piattaforme [](../../forms/using/aem-forms-jee-supported-platforms.md)supportate:

<table>
 <tbody>
  <tr>
   <td>Componente</td>
   <td>Supporto rimosso</td>
  </tr>
  <tr>
   <td>Sistemi operativi</td>
   <td>
    <ul>
     <li>Microsoft Windows Server 2012 R2</li>
     <li>IBM AIX*</li>
     <li>Sun Solaris*</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Server applicazioni<br /> </td>
   <td>
    <ul>
     <li>Oracle Weblogic</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Database</td>
   <td>
    <ul>
     <li>IBM DB2 <br /> </li>
     <li>Oracle RAC</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Server LDAP</td>
   <td>
    <ul>
     <li>Microsoft Active Directory 2012</li>
     <li>Novell eDirectory 8.8.7 </li>
     <li>IBM Lotus Domino 8.5.0 </li>
    </ul> </td>
  </tr>
  <tr>
   <td>Server e-mail</td>
   <td>
    <ul>
     <li>IBM Lotus Domino 8.5.0 </li>
    </ul> </td>
  </tr>
  <tr>
   <td>Connettori</td>
   <td>
    <ul>
     <li>Connettore per Microsoft SharePoint 2013</li>
     <li>Connettore per EMC Documentum 7.0</li>
    </ul> </td>
  </tr>
  <tr>
   <td>AEM Forms app<br /> </td>
   <td>
    <ul>
     <li>Supporto di Windows 8.1</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Java </td>
   <td>
    <ul>
     <li>Java 11</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

* Per informazioni sulla migrazione a un&#39;altra piattaforma, contattate il supporto Adobe

#### Nuova interfaccia utente basata su HTML5 {#new-html-based-uis}

In linea con l’EOL pianificato di Adobe Flash Player e con la direzione generale della migrazione dei contenuti basati su Flash agli standard aperti, AEM 6.5 Forms ha sostituito l’interfaccia utente basata su Flash di Health Monitor, Process Management, Reader Extension e Category Management UI di AEM Forms nella console di amministrazione JEE con interfaccia utente basata su HTML5.

#### Miglioramenti della sicurezza {#security-improvements}

* AEM 6.5 Forms nell’interfaccia utente della console di amministrazione JEE ora si basa su Apache Struts 2.5.
* AEM 6.5 Forms utilizza ora jQuery per 3.2.1 e jQuery UI 1.12.1. Consulta la documentazione [di](/help/forms/home.md) aggiornamento per verificare l’impatto della modifica.

#### Miglioramenti all&#39;accessibilità {#accessibility-improvements}

AEM 6.5 Forms offre una migliore accessibilità ad AEM Forms Workspace.
