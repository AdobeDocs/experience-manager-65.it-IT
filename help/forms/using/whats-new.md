---
title: Riepilogo delle nuove funzioni | AEM 6.5 Forms
seo-title: New features summary | AEM 6.5 Forms
description: Funzioni e miglioramenti più recenti per moduli e documenti della soluzione di gestione dell’esperienza digitale più avanzata al mondo.
seo-description: Latest features and improvements to forms and documents of world’s most advanced digital experience management solution.
uuid: 179d372d-b7f6-4771-8349-fc6b7854efac
topic-tags: introduction
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 0e949429-cd5f-4301-aa72-14803cdfab00
docset: aem65
exl-id: 47b9de1f-b16a-424c-b8b4-e9d7b3dcca86
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1224'
ht-degree: 1%

---

# Riepilogo delle nuove funzioni | AEM 6.5 Forms{#new-features-summary-aem-forms}

## Rapporti sulle transazioni {#transaction-reports}

I rapporti sulle transazioni consentono di acquisire e tenere traccia del numero di moduli inviati, documenti elaborati e documenti sottoposti a rendering. L&#39;obiettivo del monitoraggio di queste transazioni è quello di prendere una decisione informata sull&#39;utilizzo del prodotto e sul ribilanciamento degli investimenti in hardware e software. Alcuni esempi di transazioni includono:

* Invio di un modulo adattivo, di un modulo HTML5 o di un set di moduli
* Rendering di una stampa o di una versione web di una comunicazione interattiva
* Conversione di un documento da un formato di file a un altro

Per informazioni sulla configurazione e l’utilizzo dei rapporti sulle transazioni, consulta [Panoramica dei rapporti sulle transazioni](../../forms/using/transaction-reports-overview.md).

![Report di transazione di esempio](assets/surface_transaction_reporting.png)

## Comunicazioni interattive {#interactive-communications}

**Definire i pattern di visualizzazione dei dati**

Gli autori di comunicazioni interattive possono ora definire [pattern di visualizzazione dei dati](create-interactive-communication.md#datadisplaypatterns) per campi, variabili ed elementi del modello dati del modulo. Ad esempio, formati data, valuta o telefono.

**Utilizzare nuovi tipi di grafici**

È ora possibile aggiungere [Grafici quadranti e grafici con più serie](../../forms/using/chart-component-interactive-communications.md) alle comunicazioni interattive.

**Ordinare le colonne in una tabella**

Ora puoi [ordinare le colonne di una tabella](../../forms/using/create-interactive-communication.md#sortcolumns) nella comunicazione interattiva. È possibile eseguire il binding e l’ordinamento delle colonne di una tabella con oggetti di testo statici o modelli di dati.

**Utilizzare nuovi componenti in un canale web**

È ora possibile aggiungere i componenti Pulsante e Separatore al canale Web. Per ulteriori informazioni, consulta [Aggiungi componente Pulsante al canale web](../../forms/using/create-interactive-communication.md#add-button-component-to-the-web-channel) e [Componente separatore nel canale web](../../forms/using/create-interactive-communication.md#separatorcomponent).

**Modalità Layout per ridimensionare i componenti**

Ora puoi passare a [Modalità Layout](../../forms/using/resize-using-layout-mode.md) per ridimensionare i componenti nel canale web utilizzando un’interfaccia WYSIWYG.

**Miglioramenti a livello di usabilità**

Gli autori di comunicazioni interattive possono ora utilizzare varie operazioni di facile utilizzo durante la creazione di corrispondenze. L&#39;elenco delle operazioni comprende:

* [Eseguire azioni Annulla-Ripristina nei canali web e di stampa](../../forms/using/create-interactive-communication.md#undoredoactions)
* [Aggiungere variabili in un frammento di documento utilizzando il simbolo @](../../forms/using/texts-interactive-communications.md#searchvariables)
* [Aggiungere elementi del modello dati in un frammento di documento utilizzando il simbolo @](../../forms/using/texts-interactive-communications.md#searchdatamodelproperties)
* [Eliminare o aggiungere un canale Web a una comunicazione interattiva esistente](../../forms/using/create-interactive-communication.md#edit-interactive-communication-properties)
* [Binding degli elementi dell’origine dati con campi e variabili mediante azioni di trascinamento della selezione](../../forms/using/create-interactive-communication.md#binddatasourceelements)
* [Evidenziazione di campi e variabili non associati durante la creazione di comunicazioni interattive](../../forms/using/create-interactive-communication.md#distinguishunboundfields)
* [Esegui azioni aggiuntive come copia, gruppo o altro sui componenti ereditati in un canale web](../../forms/using/create-interactive-communication.md#componenttoolbar)

**Miglioramenti nel processo di sincronizzazione**

Sono stati apportati diversi miglioramenti al layout del canale Web generato automaticamente utilizzando il canale Stampa.

![Grafici di comunicazione interattiva](assets/interactive-communication-charts.png)

## Moduli adattivi {#adaptive-forms}

### Utilizzare firme digitali basate su cloud Adobe Sign in Adaptive Forms {#use-adobe-sign-s-cloud-based-digital-signatures-in-adaptive-forms}

[Firme digitali basate su cloud](https://helpx.adobe.com/sign/kb/digital-certificate-providers.html) Le firme remote o remote rappresentano una nuova generazione di firme digitali utilizzabili tra desktop, dispositivi mobili e web e soddisfano i più elevati livelli di conformità e garanzia per l’autenticazione dei firmatari. Ora puoi [firmare un modulo adattivo](../../forms/using/working-with-adobe-sign.md) con firme digitali basate su cloud.

#### Incorporare un modulo adattivo o una comunicazione interattiva nelle applicazioni a pagina singola di AEM Sites {#embed-an-adaptive-form-or-interactive-communcation-in-aem-sites-single-page-applications}

AEM Forms consente di: [incorporare facilmente un modulo adattivo](../../forms/using/embed-adaptive-form-aem-sites-spa.md) Comunicazione interattiva in un’applicazione a pagina singola AEM Sites (SPA). Il modulo adattivo e la comunicazione interattiva incorporati sono completamente funzionanti e gli utenti possono compilare e inviare il modulo senza uscire dalla pagina. Consente all’utente di rimanere nel contesto di altri elementi della pagina web e di interagire contemporaneamente con il modulo adattivo o la comunicazione interattiva.

#### Ordinare le colonne delle tabelle dei moduli adattivi {#sort-columns-of-adaptive-form-tables}

È possibile [ordinare qualsiasi colonna di una tabella Modulo adattivo](../../forms/using/adaptive-forms-tables.md#sortcolumnstable) in ordine crescente o decrescente. È possibile applicare l’ordinamento alle colonne di tabella con testo statico, proprietà dell’oggetto modello dati o una combinazione di proprietà statiche di testo e oggetti modello dati.

#### Limitare la disponibilità di modelli di Forms adattivi a percorsi specifici {#restrict-the-availability-of-adaptive-forms-templates-to-specific-paths}

Moduli adattivi ha aggiunto il supporto per la proprietà cq:allowedPaths . La proprietà [limita la disponibilità di modelli di Forms adattivi a percorsi specifici](creating-adaptive-form.md#adaptive-form-templates).

#### Aggiungi dinamicamente le caselle di controllo al modulo adattivo {#add-check-boxes-to-the-adaptive-form-dynamically}

È ora possibile definire regole per [aggiunta dinamica di caselle di controllo al modulo adattivo](../../forms/using/rule-editor.md#setpropertyrule) basato su una funzione personalizzata, un oggetto modulo o una proprietà oggetto.

## Flussi di lavoro AEM {#aem-workflows}

### Utilizzare le variabili nei flussi di lavoro AEM {#use-variables-in-aem-workflows}

Le variabili consentono ai passaggi del flusso di lavoro di conservare e trasmettere i metadati tra i passaggi del flusso di lavoro in fase di runtime. Puoi creare diversi tipi di variabili per memorizzare diversi tipi di dati. Ad esempio, numeri interi, stringhe, documenti o istanze del modello dati del modulo. In genere, si utilizza una variabile o una raccolta di variabili quando è necessario prendere una decisione in base al valore che contiene o per memorizzare le informazioni necessarie in un secondo momento in un processo.

Le variabili sono un&#39;estensione di [MetaDataMap](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/metadata/MetaDataMap.html) Interfaccia disponibile nella versione precedente. Consente di risparmiare tempo nello sviluppo di codice ECMAScript personalizzato utilizzato per recuperare e aggiornare i valori dei metadati. Si continua a utilizzare l&#39;interfaccia MetaDataMap e il codice ECMAScript per manipolare i metadati. Alcuni vantaggi dell&#39;utilizzo di variabili su MetaDataMap ed ECMAScript sono:

* Memorizza, aggiorna e utilizza in modo dinamico i valori memorizzati in una variabile all’interno del flusso di lavoro senza ricorrere al codice personalizzato
* Recuperare e aggiornare i valori direttamente in un modello dati del modulo e in un file di dati (XML/JSON ) di un modulo inviato
* Archiviare documenti completi in una variabile per eseguire l&#39;elaborazione dei documenti

Il passaggio Vai a, O Dividi e tutti i passaggi del flusso di lavoro AEM Forms supportano le variabili. Puoi utilizzare l’interfaccia MetaDataMap per accedere alle variabili nei passaggi del flusso di lavoro che non dispongono di un supporto nativo per le variabili. Per ulteriori informazioni, consulta [Variabili nei flussi di lavoro AEM](../../forms/using/variable-in-aem-workflows.md).

![Impostazione di una variabile per in un flusso di lavoro](assets/variable.png)

#### Utilizzare un flusso di lavoro con Forms adattivo diverso  {#use-a-workflow-with-different-adaptive-forms}

È possibile [specifica un modulo adattivo per l’attività di assegnazione](../../forms/using/aem-forms-workflow-step-reference.md#assign-task-step) e il documento della fase record dei flussi di lavoro incentrati sui moduli sul runtime. Consente a un flusso di lavoro di funzionare con diversi Adaptive Forms. È possibile scegliere il metodo per selezionare un modulo adattivo durante la progettazione del flusso di lavoro. Il modulo adattivo può trovarsi in un percorso assoluto, essere inviato come payload al flusso di lavoro o essere disponibile in un percorso calcolato utilizzando una variabile.

#### Utilizzare funzionalità di registrazione avanzate per i passaggi del flusso di lavoro incentrati sui moduli {#use-enhanced-logging-capabilities-of-forms-centric-workflow-steps}

Le funzionalità di registrazione dei passaggi del flusso di lavoro incentrati sui moduli sono standardizzate. Ora, tutti i passaggi del flusso di lavoro incentrati sui moduli producono registri standardizzati simili. Consente di migliorare la velocità di debug.

## Integrazione dei dati {#data-integration}

Ora puoi:

* [Convalida dei dati di input](../../forms/using/work-with-form-data-model.md#automated-validation-of-input-data) in base a un elenco di vincoli. Ciò consente di garantire che all’origine dati vengano inviati solo dati validi.
* [Ignora endpoint predefinito](../../forms/using/configure-data-sources.md#configure-soap-web-services) definito in un file WSDL (Web Services Description Language).

* [Ignora impostazione predefinita](../../forms/using/configure-data-sources.md#configure-restful-web-services) [schema, host e percorso di base](../../forms/using/configure-data-sources.md#configure-restful-web-services) definito nel file di definizione Swagger.

## Aggiornamenti a piattaforma e sicurezza {#platform-and-security-updates}

### Aggiornamenti principali delle piattaforme {#major-platform-updates}

AEM Forms può essere configurato utilizzando qualsiasi combinazione di sistemi operativi, server di applicazioni, database, driver di database, JDK, server LDAP e server di posta elettronica supportati. Di seguito sono riportate le principali modifiche apportate a [piattaforme supportate](../../forms/using/aem-forms-jee-supported-platforms.md):

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
    <li>Profilo WebSphere Liberty</li>
    <li>Oracle WebLogic</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Database</td>
   <td>
    <ul>
     <li>IBM DB2 <br /> </li>
     <li>RAC Oracle</li>
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
     <li>Connettore per Microsoft Sharepoint 2013</li>
     <li>Connettore per EMC Documentum 7.0</li>
    </ul> </td>
  </tr>
  <tr>
   <td>app AEM Forms<br /> </td>
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

&#42; Contatta il supporto Adobe per informazioni sulla migrazione a una piattaforma diversa

#### Nuove interfacce basate su HTML5 {#new-html-based-uis}

In linea con le EOL pianificate del Flash Player di Adobe e con la direzione generale della migrazione dei contenuti basati su Flash agli standard aperti, AEM 6.5 Forms ha sostituito l’interfaccia utente basata su Flash di Health Monitor, Process Management, Extension Reader e Gestione categorie di AEM Forms nella console di amministrazione JEE con l’interfaccia utente basata su HTML5.

#### Miglioramenti della sicurezza {#security-improvements}

* AEM 6.5 Forms sull’interfaccia utente della console di amministrazione JEE è ora basato su Apache Struts 2.5.
* AEM 6.5 Forms ora utilizza jQuery a 3.2.1 e jQuery UI 1.12.1. Vedi, [documentazione di aggiornamento](/help/forms/home.md) per l&#39;impatto del cambiamento.

#### Miglioramenti all’accessibilità {#accessibility-improvements}

AEM 6.5 Forms ha migliorato l’accessibilità di AEM Forms Workspace.
