---
title: Variabili nei flussi di lavoro  AEM Forms
seo-title: Variabili nei flussi di lavoro  AEM Forms
description: Create una variabile, impostate un valore per la variabile e utilizzatela  passaggi del flusso di lavoro AEM Forms.
seo-description: Create una variabile, impostate un valore per la variabile e utilizzatela  passaggi del flusso di lavoro AEM Forms.
uuid: 634a75c4-4899-478f-9e5d-a870f5efa583
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: cbf4e35a-7905-44ab-ab68-fb443443f02d
docset: aem65
translation-type: tm+mt
source-git-commit: 252dac988c8256cf99ee8487feb937d5345ed797
workflow-type: tm+mt
source-wordcount: '2113'
ht-degree: 1%

---


# Variabili nei flussi di lavoro  AEM Forms{#variables-in-aem-forms-workflows}

Una variabile in un modello di workflow consente di memorizzare un valore in base al tipo di dati. Potete quindi utilizzare il nome della variabile in qualsiasi passaggio del flusso di lavoro per recuperare il valore memorizzato nella variabile. È inoltre possibile utilizzare nomi di variabili per definire le espressioni per l&#39;adozione di decisioni di routing.

AEM modelli di flusso di lavoro potete:

* [Creare una ](../../forms/using/variable-in-aem-workflows.md#create-a-variable) variabile di un tipo di dati in base al tipo di informazioni che si desidera memorizzare al suo interno.
* [Impostate un valore per la ](../../forms/using/variable-in-aem-workflows.md#set-a-variable) variabile utilizzando il passaggio del flusso di lavoro Imposta variabile.
* [Utilizzare la ](../../forms/using/variable-in-aem-workflows.md#use-a-variable) variabile in tutti  passaggi del flusso di lavoro di AEM Forms per recuperare il valore memorizzato e nei passaggi di divisione e visita OR per definire un&#39;espressione di routing.

Il seguente video illustra come creare, impostare e utilizzare le variabili in AEM modelli di flusso di lavoro:

>[!VIDEO](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/using/variables_introduction_1_1.mp4)

Le variabili sono un&#39;estensione dell&#39;interfaccia [MetaDataMap](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/metadata/MetaDataMap.html) esistente. È possibile utilizzare [MetaDataMap](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/metadata/MetaDataMap.html) in ECMAScript per accedere ai metadati salvati utilizzando le variabili.

## Creare una variabile {#create-a-variable}

Per creare le variabili, utilizzate la sezione Variabili disponibile nella barra laterale del modello di workflow. AEM variabili di flusso di lavoro supportano i seguenti tipi di dati:

* **Tipi** di dati di base: Long, Double, Boolean, Date e String
* **Tipi** di dati complessi:  [istanza Document](https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/aemfd/docmanager/Document.html),  [XML](https://docs.oracle.com/javase/8/docs/api/org/w3c/dom/Document.html),  [JSON](https://static.javadoc.io/com.google.code.gson/gson/2.3/com/google/gson/JsonObject.html) e Form Data Model.

>[!NOTE]
>
>I flussi di lavoro supportano solo il formato ISO8601 per le variabili di tipo Data.

È necessario [ pacchetto aggiuntivo AEM Forms](https://helpx.adobe.com/it/aem-forms/kb/aem-forms-releases.html) per i tipi di dati Document e Form Data Model.  Utilizzate il tipo di dati ArrayList per creare raccolte di variabili. È possibile creare una variabile ArrayList per tutti i tipi di dati primitivi e complessi. Ad esempio, creare una variabile ArrayList e selezionare String come sottotipo per memorizzare più valori stringa utilizzando la variabile.

Per creare una variabile, eseguite i seguenti passaggi:

1. In un&#39;istanza AEM, passare a Strumenti ![](/help/forms/using/assets/hammer.png) > Flusso di lavoro > Modelli.
1. Toccate **[!UICONTROL Crea]** e specificate il titolo e un nome opzionale per il modello di workflow. Selezionare il modello e toccare **[!UICONTROL Modifica]**.
1. Toccate l&#39;icona delle variabili disponibile nella barra laterale del modello di workflow e toccate **[!UICONTROL Aggiungi variabile]**.

   ![Aggiungi variabile](assets/variables_add_variable_new.png)

1. Nella finestra di dialogo Aggiungi variabile, specificate il nome e selezionate il tipo di variabile.
1. Selezionare il tipo di dati dall&#39;elenco a discesa **[!UICONTROL Tipo]** e specificare i valori seguenti:

   * Tipo di dati di base - Specificate un valore predefinito facoltativo per la variabile.
   * JSON o XML - Specificate un percorso di schema JSON o XML facoltativo. Il sistema convalida il percorso dello schema durante la mappatura e la memorizzazione delle proprietà disponibili in questo schema a un&#39;altra variabile.
   * Modello dati modulo - Specifica un percorso del modello dati del modulo.
   * ArrayList - Specifica un sottotipo per la raccolta.

1. Specificate una descrizione facoltativa per la variabile e toccate ![done_icon](assets/done_icon.png) per salvare le modifiche. La variabile viene visualizzata nell’elenco disponibile nel riquadro a sinistra.

Quando create delle variabili, tenete presenti le seguenti procedure:

* Crea tutte le variabili necessarie per un flusso di lavoro. Tuttavia, per conservare le risorse del database, utilizzate il numero minimo di variabili richieste e riutilizzate le variabili quando possibile.
* Le variabili seguono la distinzione tra maiuscole e minuscole. Assicurati di fare riferimento alle variabili con lo stesso caso nel flusso di lavoro.
* Evitare di utilizzare caratteri speciali nel nome della variabile

## Impostare una variabile {#set-a-variable}

È possibile utilizzare il passaggio Imposta variabile per impostare il valore di una variabile e definire l&#39;ordine in cui i valori vengono impostati. La variabile viene impostata nell&#39;ordine in cui le mappature delle variabili sono elencate nel passaggio della variabile set.

Le modifiche ai valori delle variabili interessano solo l’istanza del processo in cui avviene la modifica. Ad esempio, quando un flusso di lavoro viene avviato e i dati variabili cambiano, le modifiche interessano solo l&#39;istanza del flusso di lavoro. Le modifiche non hanno effetto su altre istanze del flusso di lavoro avviate in precedenza o avviate successivamente.

A seconda del tipo di dati della variabile, è possibile utilizzare le seguenti opzioni per impostare il valore di una variabile:

* **Letterale:** utilizzare l&#39;opzione quando si conosce il valore esatto da specificare.

* **Espressione:** utilizzare l&#39;opzione quando il valore da utilizzare viene calcolato in base a un&#39;espressione. L&#39;espressione viene creata nell&#39;editor di espressioni fornito.

* **Notazione punto JSON:** utilizzate l&#39;opzione per recuperare un valore da una variabile di tipo JSON o FDM.
* **XPATH:** utilizzare l&#39;opzione per recuperare un valore da una variabile di tipo XML.

* **Relativa al payload:** utilizzare l&#39;opzione quando il valore da salvare in variabile è disponibile in un percorso relativo al payload.

* **Percorso assoluto:** utilizzate l&#39;opzione quando il valore da salvare in variabile è disponibile in un percorso assoluto.

Potete anche aggiornare elementi specifici di una variabile di tipo JSON o XML utilizzando la notazione JSON DOT o XPATH.

### Aggiungi mappatura tra variabili {#add-mapping-between-variables}

Per aggiungere la mappatura tra le variabili, effettua i seguenti passaggi:

1. Nella pagina di modifica del flusso di lavoro, toccate l’icona Passaggi disponibile nella barra laterale del modello di workflow.
1. Trascinare il passaggio **Imposta variabile** nell&#39;editor del flusso di lavoro, toccare il passaggio e selezionare ![Configura_icona](assets/configure_icon.png) (Configura).
1. Nella finestra di dialogo Imposta variabile, selezionare **[!UICONTROL Mapping]** > **[!UICONTROL Aggiungi mappatura]**.
1. Nella sezione **Mappa variabile**, selezionare la variabile da memorizzare i dati, selezionare la modalità di mappatura e specificare un valore da memorizzare nella variabile. Le modalità di mappatura variano in base al tipo di variabile.
1. Mappare più variabili per creare un&#39;espressione significativa. Toccate ![done_icon](assets/done_icon.png) per salvare le modifiche.

### Esempio 1: Eseguire una query su una variabile XML per impostare il valore di una variabile stringa {#example-query-an-xml-variable-to-set-value-for-a-string-variable}

Selezionare una variabile di tipo XML per memorizzare un file XML. Eseguire una query sulla variabile XML per impostare il valore di una variabile stringa per la proprietà disponibile nel file XML. Utilizzare **Specificare XPATH per il campo della variabile XML** per definire la proprietà da memorizzare nella variabile stringa.

In questo esempio, selezionare una variabile **formdata** XML per memorizzare il file **cc-app.xml**. Eseguire una query sulla variabile **formdata** per impostare il valore per la variabile di stringa **email** in modo da memorizzare il valore per la proprietà **emailAddress** disponibile nel file **cc-app.xml**.

>[!VIDEO](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/using/set_variable_example1.mp4 "Imposta il valore di una variabile")

### Esempio 2: Utilizzare un&#39;espressione per memorizzare il valore in base ad altre variabili {#example2}

Utilizzare un&#39;espressione per calcolare la somma delle variabili e memorizzare il risultato in una variabile.

In questo esempio, utilizzate l&#39;editor di espressioni per definire un&#39;espressione per calcolare la somma delle variabili **assetscost** e **balanceamount** e memorizzare il risultato nella variabile **totalvalue**.

>[!VIDEO](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/using/variables_expression.mp4)

## Utilizza editor di espressioni {#use-expression-editor}

È inoltre possibile utilizzare le espressioni per calcolare il valore di una variabile in fase di esecuzione. Le variabili forniscono un editor di espressioni per definire le espressioni.

Utilizzate l&#39;editor di espressioni per:

* Impostate il valore delle variabili utilizzando altre variabili di flusso di lavoro, numeri o espressioni matematiche.
* Utilizzare variabili di flusso di lavoro, stringa, numero o espressione all&#39;interno di un&#39;espressione matematica
* Aggiungere condizioni per impostare i valori delle variabili.
* Aggiungere operatori tra le condizioni.

![Editor espressioni](assets/variables_expression_editor_new.png)

Si basa sull&#39;editor di regole per moduli adattivi con le seguenti modifiche. Editor di regole nelle variabili:

* Non supporta le funzioni.
* Non fornisce un&#39;interfaccia utente per visualizzare il riepilogo delle regole
* Non ha un editor di codice.
* Non supporta l&#39;abilitazione e la disattivazione del valore di un oggetto.
* Non supporta l&#39;impostazione della proprietà di un oggetto.
* Non supporta la chiamata a un servizio Web.

Per ulteriori informazioni, vedere [editor di regole per moduli adattivi](../../forms/using/rule-editor.md).

## Utilizzare una variabile {#use-a-variable}

È possibile utilizzare le variabili per recuperare input e output o salvare il risultato di un passaggio. L’editor del flusso di lavoro fornisce due tipi di passaggi per il flusso di lavoro:

* Passaggi del flusso di lavoro con supporto per le variabili
* Passaggi del flusso di lavoro senza supporto delle variabili

### Passaggi del flusso di lavoro con supporto per le variabili {#workflow-steps-with-support-for-variables}

Il passaggio Vai a, O Dividi e tutti  passaggi del flusso di lavoro AEM Forms supportano le variabili.

#### O Passaggio di divisione {#or-split-step}

La divisione OR crea una divisione nel flusso di lavoro, dopo di che è attivo un solo ramo. Questo passaggio consente di introdurre i percorsi di elaborazione condizionale nel flusso di lavoro. Potete aggiungere i passaggi del flusso di lavoro a ogni ramo, a seconda delle necessità.

È possibile definire l&#39;espressione di routing per un ramo utilizzando una definizione di regola, uno script ECMA o uno script esterno.

È possibile utilizzare le variabili per definire l&#39;espressione di routing utilizzando l&#39;editor di espressioni. Per ulteriori informazioni sull&#39;utilizzo delle espressioni di routing per il passaggio di divisione OR, vedere [OR Split step](/help/sites-developing/workflows-step-ref.md#or-split).

In questo esempio, prima di definire l&#39;espressione di routing, utilizzare [esempio 2](../../forms/using/variable-in-aem-workflows.md#example2) per impostare il valore per la variabile **totalvalue**. La diramazione 1 è attiva se il valore della variabile **totalvalue** è maggiore di 50000. Allo stesso modo, è possibile definire una regola per rendere attivo il ramo 2 se il valore della variabile **totalvalue** è inferiore a 50000.

>[!VIDEO](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/using/variables_orsplit_example.mp4)

Analogamente, selezionare un percorso di script esterno o specificare lo script ECMA per le espressioni di routing per valutare il ramo attivo. Toccate **[!UICONTROL Rinomina ramo]** per specificare un nome alternativo per il ramo.

Per ulteriori esempi, vedere [Creare un modello di workflow](../../forms/using/aem-forms-workflow.md#create-a-workflow-model).

#### Vai al passaggio {#go-to-step}

Il **Passaggio di Go** consente di specificare il passaggio successivo nel modello di workflow da eseguire, a seconda del risultato di un&#39;espressione di routing.

Analogamente al passaggio di divisione OR, è possibile definire l&#39;espressione di routing per il passaggio Goto utilizzando una definizione di regola, uno script ECMA o uno script esterno.

È possibile utilizzare le variabili per definire l&#39;espressione di routing utilizzando l&#39;editor di espressioni. Per ulteriori informazioni sull&#39;utilizzo delle espressioni di routing per il passaggio Goto, vedere [Passaggio di Go](/help/sites-developing/workflows-step-ref.md#goto-step).

![Vai a regola](assets/variables_goto_rule1_new.png)

In questo esempio, il passaggio Goto specifica l&#39;applicazione di revisione della carta di credito come passaggio successivo se il valore per la variabile **actionTaka1/> è uguale a** Necessità di ulteriori informazioni **.**

Per ulteriori esempi sull&#39;utilizzo della definizione della regola nel passaggio Goto, vedere [Simulazione di un ciclo For](/help/sites-developing/workflows-step-ref.md#simulateforloop).

#### Passaggi del flusso di lavoro Forms incentrati sul flusso di lavoro {#forms-workflow-centric-workflow-steps}

Tutti  passaggi del flusso di lavoro AEM Forms supportano le variabili. Per ulteriori informazioni, consultate [Flusso di lavoro Forms-centric su OSGi](../../forms/using/aem-forms-workflow-step-reference.md).

### Procedura del flusso di lavoro senza supporto per le variabili {#workflow-steps-without-support-for-variables}

È possibile utilizzare l&#39;interfaccia [MetaDataMap](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/metadata/MetaDataMap.html) per accedere alle variabili nei passaggi del flusso di lavoro che non supportano le variabili.

#### Recuperare il valore della variabile {#retrieve-the-variable-value}

Utilizzate le seguenti API nello script ECMA per recuperare i valori per le variabili esistenti in base al tipo di dati:

| Tipo di dati variabile | API |
|---|---|
| Primitive (Long, Double, Boolean, Date e String) | workItem.getWorkflowData().getMetaDataMap().get(variableName, type) |
| Documento | Packages.com.adobe.aemfd.docmanager.Document doc = workItem.getWorkflowData().getMetaDataMap().get(&quot;docVar&quot;, Packages.com.adobe.aemfd.docmanager.Document.class); |
| XML | Packages.org.w3c.dom.Document xmlObject = workItem.getWorkflowData().getMetaDataMap().get(variableName, Packages.org.w3c.dom.Document.class); |
| Modello dati modulo | Packages.com.adobe.aem.dermis.api.FormDataModelInstance fdmObject = workItem.getWorkflowData().getMetaDataMap().get(variableName, Packages.com.adobe.aem.dermis.api.FormDataModelInstance.class); |
| JSON | Packages.com.google.gson.JsonObject jsonObject = workItem.getWorkflowData().getMetaDataMap().get(variableName, Packages.com.google.gson.JsonObject.class); |

È necessario [ pacchetto aggiuntivo AEM Forms](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) per i tipi di dati variabili Document e Form Data Model.

**Esempio**

Recuperare il valore del tipo di dati stringa utilizzando la seguente API:

```javascript
workItem.getWorkflowData().getMetaDataMap().get(accname, Packages.java.lang.String)
```

#### Aggiornare il valore della variabile {#update-the-variable-value}

Utilizzate la seguente API nello script ECMA per aggiornare il valore di una variabile:

```javascript
workItem.getWorkflowData().getMetaDataMap().put(variableName, value)
```

**Esempio**

```javascript
workItem.getWorkflowData().getMetaDataMap().put(salary, 50000)
```

aggiorna il valore della variabile **pay** a 50000.

### Impostare le variabili per richiamare i flussi di lavoro {#apiinvokeworkflow}

Potete utilizzare un&#39;API per impostare le variabili e passarle alle istanze del flusso di lavoro richiamate.

[workflowSession.](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/WorkflowSession.html#startWorkflow-com.adobe.granite.workflow.model.WorkflowModel-com.adobe.granite.workflow.exec.WorkflowData-java.util.Map-) startWorkflows modello, wfData e metaData come argomenti. Utilizzate MetaDataMap per impostare il valore della variabile.

In questa API, la variabile **variableName** è impostata su **value** utilizzando metaData.put(variableName, value);

```javascript
import com.adobe.granite.workflow.model.WorkflowModel;
import com.adobe.granite.workflow.metadata.MetaDataMap;
import com.adobe.aemfd.docmanager.Document;

/*Assume that you already have a workflowSession and modelId along with the payloadType and payload*/
WorkflowData wfData = workflowSession.newWorkflowData(payloadType, payload);
MetaDataMap metaData = wfData.getMetaDataMap();
metaData.put(variableName, value); //Create a variable "variableName" in your workflow model
WorkflowModel model = workflowSession.getModel(modelId);
workflowSession.startWorkflow(model, wfData, metaData);
```

**Esempio**

Inizializzare l&#39;oggetto documento **doc** su un percorso (&quot;a/b/c&quot;) e impostare il valore della variabile **docVar** sul percorso memorizzato nell&#39;oggetto documento.

```javascript
import com.adobe.granite.workflow.WorkflowSession;
import com.adobe.granite.workflow.exec.WorkflowData;
import com.adobe.granite.workflow.model.WorkflowModel;
import com.adobe.granite.workflow.metadata.MetaDataMap;
import com.adobe.aemfd.docmanager.Document;

/*This example assumes that you already have a workflowSession and modelId along with the payloadType and payload */
WorkflowData wfData = workflowSession.newWorkflowData(payloadType, payload);
MetaDataMap metaData = wfData.getMetaDataMap();
Document doc = new Document("/a/b/c");// initialize a document object
metaData.put("docVar",doc); //Assuming that you have created a variable "docVar" of type Document in your workflow model
WorkflowModel model = workflowSession.getModel(modelId);
workflowSession.startWorkflow(model, wfData, metaData);
```

## Modificare una variabile {#edit-a-variable}

1. Nella pagina del flusso di lavoro di modifica, toccate l&#39;icona Variabili disponibile nella barra laterale del modello di workflow. Nella sezione Variabili del riquadro a sinistra sono visualizzate tutte le variabili esistenti.
1. Toccate l&#39;icona ![edit](assets/edit.png) (Edit) accanto al nome della variabile da modificare.
1. Modificate le informazioni della variabile e toccate ![done_icon](assets/done_icon.png) per salvare le modifiche. Non è possibile modificare i campi **[!UICONTROL Name]** e **[!UICONTROL Type]** per una variabile.

## Eliminare una variabile {#delete-a-variable}

Prima di eliminare la variabile, rimuovete dal flusso di lavoro tutti i riferimenti della variabile. Assicurarsi che la variabile non sia utilizzata nel flusso di lavoro.

Per eliminare una variabile, eseguite i seguenti passaggi:

1. Nella pagina del flusso di lavoro di modifica, toccate l&#39;icona Variabili disponibile nella barra laterale del modello di workflow. Nella sezione Variabili del riquadro a sinistra sono visualizzate tutte le variabili esistenti.
1. Toccate l’icona Elimina accanto al nome della variabile da eliminare.
1. Toccate ![done_icon](assets/done_icon.png) per confermare ed eliminare la variabile.

## Riferimenti {#references}

Per ulteriori esempi sull&#39;uso delle variabili  passaggi del flusso di lavoro AEM Forms, vedere [Variabili nei flussi di lavoro AEM](https://helpx.adobe.com/experience-manager/kt/forms/using/authoring_variables_in_aem_forms-workflow1.html).
