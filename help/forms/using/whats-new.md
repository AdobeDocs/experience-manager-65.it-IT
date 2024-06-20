---
title: Riepilogo delle nuove funzionalità | AEM 6.5 Forms
description: Funzioni e miglioramenti più recenti ai moduli e ai documenti AEM, la soluzione di gestione delle esperienze digitali più avanzata al mondo.
topic-tags: introduction
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
exl-id: 47b9de1f-b16a-424c-b8b4-e9d7b3dcca86
solution: Experience Manager, Experience Manager Forms
feature: Release Information
role: Admin, User, Developer
source-git-commit: 872e2de411f51b5f0b26a2ff47cb49f01313d39f
workflow-type: tm+mt
source-wordcount: '637'
ht-degree: 1%

---

# Riepilogo delle nuove funzionalità | AEM 6.5 Forms{#new-features-summary-aem-forms}

| Prodotto | Adobe Experience Manager 6.5 |
| -------- | ---------------------------- |
| Versione | 6.5.19.0 |
| Tipo | Versione Service Pack |
| Data | sabato 8 dicembre 2023 |

## Cosa è incluso in Adobe Experience Manager 6.5 Forms Service Pack 19 (6.5.19.0)

L&#39;Experience Manager 6.5.19.0 include nuove funzionalità, miglioramenti chiave richiesti dai clienti, correzioni di bug e miglioramenti a livello di prestazioni, stabilità e sicurezza, rilasciati dopo la disponibilità iniziale della versione 6.5 di aprile 2019. [Installa il service pack](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/aem-forms-current-service-pack-installation-instructions.html) sull&#39;Experience Manager 6.5.

### Nuove funzioni

#### Nuovi componenti core modulo adattivo

Per migliorare la scalabilità dei moduli, vengono aggiunte schede verticali, Termini e Condizioni e Casella di controllo.

* **[Componente casella di controllo](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/checkbox.html)**: il Forms adattivo basato sui Componenti core ora può includere un componente casella di controllo. Consente agli utenti di effettuare scelte binarie, selezionando o deselezionando una particolare opzione. In genere viene visualizzata come una piccola casella su cui è possibile fare clic o toccare per alternare due stati: selezionato e deselezionato. La casella di controllo è un elemento modulo comune utilizzato per presentare una scelta sì/no o vero/falso.

* **[Componente termini e condizioni](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/terms-and-conditions.html)**: Forms adattivo basato su componenti core ora può includere un componente Termini e condizioni. Consente agli autori dei moduli di introdurre una sezione specifica all’interno del modulo in cui vengono presentati agli utenti i termini, le condizioni o gli accordi legali associati all’utilizzo di un servizio, un prodotto o una piattaforma. Questo componente è progettato per informare gli utenti sulle regole, le normative e gli obblighi che si impegnano a rispettare inviando il modulo.

  ![Schede verticali, termini e condizioni e componenti casella di controllo](/help/forms/using/assets/forms-components.png)

* **[Componente Schede verticali](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/vertical-tabs.html)**: Forms adattivo basato su Componenti core ora può organizzare il contenuto del modulo in un elenco verticale di schede, fornendo un layout strutturato e navigabile. L’utilizzo di schede verticali in un modulo può migliorare l’esperienza utente complessiva semplificando la navigazione e migliorando l’organizzazione del contenuto del modulo, soprattutto nelle situazioni in cui un modulo contiene più sezioni o informazioni complesse.

#### Versione a 64 bit di AEM Forms Designer

Il [Versione a 64 bit di AEM Forms Designer](/help/forms/using/installing-configuring-designer.md) offre prestazioni, scalabilità e gestione della memoria migliorate per migliorare l’esperienza di creazione dei moduli. Grazie all&#39;architettura a 64 bit, è possibile gestire con facilità progetti ancora più grandi e complessi, garantendo flussi di lavoro di progettazione ottimizzati ed efficienza. Migliora le funzionalità di progettazione dei moduli e abbraccia il futuro di AEM Forms Designer con questa versione all’avanguardia.

#### Collegare un Forms adattivo all’elenco di Microsoft® SharePoint

AEM Forms fornisce un’integrazione standard per [inviare i dati dei moduli direttamente a SharePoint List](/help/forms/using/configuring-submit-actions.md#submit-to-microsoft&reg;-sharepoint-list)), che consente di utilizzare le funzionalità degli elenchi di SharePoint. È possibile configurare Microsoft® SharePoint List come origine dati per un modello dati modulo e utilizzare l’azione Invia utilizzando il modello dati modulo per inviare un modulo adattivo a SharePoint List.

#### Supporto per la configurazione delle proprietà del documento record per i frammenti di moduli adattivi

Ora puoi facilmente [personalizzare i frammenti di moduli adattivi e i relativi campi nell’editor di moduli adattivi](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md).

#### Include la versione a 64 bit di XMLFM

L&#39;iterazione a 64 bit di XMLFM offre prestazioni, scalabilità e gestione della memoria migliorate. È il primo servizio nativo a 64 bit implementato sul lato server. Sfruttando la capacità intrinseca di accedere a risorse di memoria notevolmente più grandi rispetto alla sua controparte a 32 bit, XMLFM a 64 bit consente la gestione senza problemi di carichi di lavoro di rendering più grandi. Questa tappa rappresenta non solo un salto nelle prestazioni, ma introduce anche miglioramenti fondamentali al framework di servizio nativo all’interno del server AEM Forms. Questo aggiornamento consente al server AEM Forms di supportare facilmente qualsiasi servizio nativo a 64 bit.



## Correzioni di bug

La versione include anche correzioni per oltre 20 problemi segnalati dai clienti. Per un elenco dettagliato delle correzioni incluse nel service pack, consulta [note sulla versione](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/release-notes.html?lang=it#forms-6519)


## Installazione del service pack

Il service pack include nuove funzioni e correzioni di bug sia per AEM Forms su JEE che per AEM Forms su OSGi. Le istruzioni di installazione presentano modifiche rispetto ai service pack precedenti. Per le istruzioni di installazione, vedere [Istruzioni di installazione di AEM Forms service pack](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/aem-forms-current-service-pack-installation-instructions.html?lang=en).






<!-- 
## Transaction Reports {#transaction-reports}



Transaction reports lets you capture and track the number of submitted forms, processed documents, and rendered documents. The objective behind tracking these transactions is to make an informed decision about the product usage and rebalancing investments in hardware and software. Some examples of transactions include:

* Submission of an Adaptive Form, an HTML5 Form, or a Form Set
* Rendition of a print or a web version of an interactive communication
* Conversion of a document from one file format to another

For information about configuring and using transaction reports, see [Transaction Reports Overview](../../forms/using/transaction-reports-overview.md).

![A sample transaction report](assets/surface_transaction_reporting.png)

## Interactive Communications {#interactive-communications}

**Define data display patterns**

Interactive Communication authors can now define [data display patterns](create-interactive-communication.md#datadisplaypatterns) for fields, variables, and form data model elements. For example, date, currency, or phone formats.

**Use new types of charts**

You can now add [Quadrant charts and charts with multiple series](../../forms/using/chart-component-interactive-communications.md) to Interactive Communications.

**Sort columns in a table**

You can now [sort columns of a table](../../forms/using/create-interactive-communication.md#sortcolumns) in the Interactive Communication. You can bind and sort table columns with static text or data model objects.

**Use new components in a web channel**

You can now add Button and Separator components to the web channel. For more information, see [Add Button component to the web channel](../../forms/using/create-interactive-communication.md#add-button-component-to-the-web-channel) and [Separator component in web channel](../../forms/using/create-interactive-communication.md#separatorcomponent).

**Layout mode to resize components**

You can now switch to [Layout mode](../../forms/using/resize-using-layout-mode.md) to resize components in the Web channel using a WYSIWYG interface.

**Usability improvements**

Interactive Communication authors can now utilize various easy-to-use operations while creating correspondences. The list of operations includes:

* [Perform undo-redo actions in print and web channels](../../forms/using/create-interactive-communication.md#undoredoactions)
* [Add variables in a document fragment using @ symbol](../../forms/using/texts-interactive-communications.md#searchvariables)
* [Add data model elements in a document fragment using @ symbol](../../forms/using/texts-interactive-communications.md#searchdatamodelproperties)
* [Delete or add a web channel to an existing Interactive Communication](../../forms/using/create-interactive-communication.md#edit-interactive-communication-properties)
* [Bind data source elements with fields and variables using drag-and-drop actions](../../forms/using/create-interactive-communication.md#binddatasourceelements)
* [Highlight unbound fields and variables while authoring Interactive Communication](../../forms/using/create-interactive-communication.md#distinguishunboundfields)
* [Perform additional actions such as copy, group, or more on inherited components in a web channel](../../forms/using/create-interactive-communication.md#componenttoolbar)

**Improvements in sync process**

There are several improvements in the Web channel layout auto-generated using the Print channel.

![Interactive Communications Charts](assets/interactive-communication-charts.png)

## Adaptive Forms {#adaptive-forms}

### Use Adobe Sign's cloud-based digital signatures in Adaptive Forms {#use-adobe-sign-s-cloud-based-digital-signatures-in-adaptive-forms}

[Cloud-based digital signatures](https://helpx.adobe.com/sign/kb/digital-certificate-providers.html) or remote signatures are a new generation of digital signatures that work across desktop, mobile, and the web — and meet the highest levels of compliance and assurance for signer authentication. You can now [sign an Adaptive Form](../../forms/using/working-with-adobe-sign.md) with Cloud-based digital signatures.

#### Embed an Adaptive Form or Interactive Communication in AEM Sites Single Page Applications {#embed-an-adaptive-form-or-interactive-communcation-in-aem-sites-single-page-applications}

AEM Forms lets you [seamlessly embed an Adaptive Form](../../forms/using/embed-adaptive-form-aem-sites-spa.md) or Interactive Communication in an AEM Sites single page application (SPA). The embedded Adaptive Form and Interactive Communication is fully functional and users can fill and submit the form without leaving the page. It helps user remain in context of other elements on the web page and simultaneously interact with the adaptive form or Interactive Communication.

#### Sort columns of Adaptive Form tables {#sort-columns-of-adaptive-form-tables}

You can [sort any column of an Adaptive Form table](../../forms/using/adaptive-forms-tables.md#sortcolumnstable) in an ascending or descending order. You can apply sorting to table columns with static text, data model object properties, or a combination of static text and data model object properties.

#### Restrict the availability of Adaptive Forms templates to specific paths {#restrict-the-availability-of-adaptive-forms-templates-to-specific-paths}

Adaptive forms has added support for the cq:allowedPaths property. The property [restricts availability of Adaptive Forms templates to specific paths](creating-adaptive-form.md#adaptive-form-templates).

#### Add check boxes to the Adaptive Form dynamically {#add-check-boxes-to-the-adaptive-form-dynamically}

You can now define rules to [add checkboxes to the Adaptive Form dynamically](../../forms/using/rule-editor.md#setpropertyrule) based on custom function, a form object, or an object property.

## AEM Workflows {#aem-workflows}

### Use variables in AEM Workflows {#use-variables-in-aem-workflows}

Variables enable workflow steps to hold and pass metadata across workflow steps at runtime. You can create different types of variables for storing different types of data. For example, integers, strings, documents, or form data model instances. Typically, you use a variable or a collection of variables when you need to make a decision based on the value that it holds or to store information that you need later in a process.

Variables are an extension of [MetaDataMap](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/metadata/MetaDataMap.html) interface available in the previous version. It helps save time spent in developing custom ECMAScript code used to retrieve and update metadata values. You continue using MetaDataMap interface and ECMAScript code to manipulate metadata. Some benefits of using variables over MetaDataMap and ECMAScript are:

* Dynamically store, update, and use values stored in a variable across the workflow without relying on custom code
* Retrieve and update values directly to a form data model and data file (XML/JSON ) of a submitted form
* Store complete documents in a variable to perform document processing

The Go To step, OR Split step, and all AEM Forms workflow steps support variables. You can use MetaDataMap interface to access variables in workflow steps that do not have a native support for variables. For more information, see [Variables in AEM Workflows](../../forms/using/variable-in-aem-workflows.md).

![Setting a variable for in a workflow](assets/variable.png)

#### Use a workflow with different Adaptive Forms  {#use-a-workflow-with-different-adaptive-forms}

You can [specify an Adaptive Form for the assign task](../../forms/using/aem-forms-workflow-step-reference.md#assign-task-step) and document of record step of form-centric workflows on the runtime. It allows a workflow to work with different Adaptive Forms. You can decide the method to select an Adaptive Form while designing the workflow. The Adaptive Form can be located at an absolute path, submitted as payload to the workflow, or available at a path calculated using a variable.

#### Use enhanced logging capabilities of forms-centric workflow steps {#use-enhanced-logging-capabilities-of-forms-centric-workflow-steps}

Logging capabilities of forms-centric workflow steps are standardized. Now, all form-centric workflow steps produce similarly standardized logs. It helps improve debugging speed.

## Data Integration {#data-integration}

You can now:

* [Validate input data](../../forms/using/work-with-form-data-model.md#automated-validation-of-input-data) based on a list of constraints. It helps ensure that only valid data is submitted to data source.
* [Override default endpoint](../../forms/using/configure-data-sources.md#configure-soap-web-services) defined in a WSDL (Web Services Description Language) file.

* [Override default](../../forms/using/configure-data-sources.md#configure-restful-web-services) [scheme, host, and base path](../../forms/using/configure-data-sources.md#configure-restful-web-services) defined in Swagger definition file.

## Platform and Security updates {#platform-and-security-updates}

### Major platform updates {#major-platform-updates}

AEM Forms can be set up using any combination of supported operating systems, application servers, databases, database drivers, JDK, LDAP servers, and email servers. The following are the major changes in [supported platforms](../../forms/using/aem-forms-jee-supported-platforms.md):

<table>
 <tbody>
  <tr>
   <td>Component</td>
   <td>Support Removed</td>
  </tr>
  <tr>
   <td>Operating systems</td>
   <td>
    <ul>
     <li>Microsoft Windows Server 2012 R2</li>
     <li>IBM AIX*</li>
     <li>Sun Solaris*</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Application servers<br /> </td>
   <td>
    <ul>
    <li>WebSphere Liberty profile</li>
    <li>Oracle WebLogic</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Databases</td>
   <td>
    <ul>
     <li>IBM DB2 <br /> </li>
     <li>Oracle RAC</li>
    </ul> </td>
  </tr>
  <tr>
   <td>LDAP servers</td>
   <td>
    <ul>
     <li>Microsoft Active Directory 2012</li>
     <li>Novell eDirectory 8.8.7 </li>
     <li>IBM Lotus Domino 8.5.0 </li>
    </ul> </td>
  </tr>
  <tr>
   <td>Email servers</td>
   <td>
    <ul>
     <li>IBM Lotus Domino 8.5.0 </li>
    </ul> </td>
  </tr>
  <tr>
   <td>Connectors</td>
   <td>
    <ul>
     <li>Connector for Microsoft Sharepoint 2013</li>
     <li>Connector for EMC Documentum 7.0</li>
    </ul> </td>
  </tr>
  <tr>
   <td>AEM Forms app<br /> </td>
   <td>
    <ul>
     <li>Windows 8.1 support</li>
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

&#42; Contact Adobe Support for information on migrating to a different platform

#### New HTML5-based UIs {#new-html-based-uis}

In line with planned EOL of Adobe Flash Player and overall direction of migrating Flash-based content to open standards, AEM 6.5 Forms has replaced Flash-based UI of Health Monitor, Process Management, Reader Extension, and Category Management UI of AEM Forms on JEE Administration Console with HTML5-based UI.

#### Security improvements {#security-improvements}

* AEM 6.5 Forms on JEE administration console UI is now based on Apache Struts 2.5.
* AEM 6.5 Forms now uses jQuery to 3.2.1 and jQuery UI 1.12.1. See, [upgrade documentation](/help/forms/using/introduction-aem-forms.md) for the impact of the change.

#### Accessibility improvements {#accessibility-improvements}

AEM 6.5 Forms has improved accessibility of AEM Forms Workspace. 
!-->

