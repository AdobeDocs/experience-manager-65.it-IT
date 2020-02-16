---
title: Variabili nei flussi di lavoro AEM
seo-title: Variabili nei flussi di lavoro AEM
description: Create una variabile, impostate un valore per la variabile e utilizzatela nei passaggi del flusso di lavoro di OPPURE Split e Goto AEM.
seo-description: Create una variabile, impostate un valore per la variabile e utilizzatela nei passaggi del flusso di lavoro di OPPURE Split e Goto AEM.
uuid: cc62ff11-51d4-4db4-9c6d-5dc2caa1da52
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: bbb9936e-ecd2-44b3-b4ae-dd62a3160641
docset: aem65
translation-type: tm+mt
source-git-commit: bc042696506bf1691c2eeffc6ab941be85fa274c

---


# Variabili nei flussi di lavoro AEM{#variables-in-aem-workflows}

Una variabile in un modello di workflow consente di memorizzare un valore in base al tipo di dati. Potete quindi utilizzare il nome della variabile in qualsiasi passaggio del flusso di lavoro per recuperare il valore memorizzato nella variabile. È inoltre possibile utilizzare nomi di variabili per definire le espressioni per l&#39;adozione di decisioni di routing.

Nei modelli di flusso di lavoro AEM è possibile:

* [Creare una variabile](/help/sites-developing/using-variables-in-aem-workflows.md#create-a-variable) di un tipo di dati in base al tipo di informazioni che si desidera memorizzare al suo interno.
* [Impostate un valore per la variabile](/help/sites-developing/using-variables-in-aem-workflows.md#set-a-variable) utilizzando il passaggio del flusso di lavoro Imposta variabile.
* [Utilizzate la variabile](/help/sites-developing/using-variables-in-aem-workflows.md#use-a-variable) nei passaggi del flusso di lavoro di OPPURE Split e Goto AEM per definire un&#39;espressione per prendere decisioni di routing. È inoltre possibile utilizzare le variabili in tutti i passaggi del flusso di lavoro di AEM Forms.

Il seguente video illustra come creare, impostare e utilizzare le variabili nei modelli di flusso di lavoro AEM:

>[!VIDEO](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/using/usevariables_example.mp4)

Le variabili sono un&#39;estensione dell&#39;interfaccia [MetaDataMap](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/metadata/MetaDataMap.html) . È possibile utilizzare [MetaDataMap](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/metadata/MetaDataMap.html) in ECMAScript per accedere ai metadati salvati utilizzando le variabili.

## Creare una variabile {#create-a-variable}

Per creare le variabili, utilizzate la sezione Variabili disponibile nella barra laterale del modello di workflow. Le variabili del flusso di lavoro AEM supportano i seguenti tipi di dati:

* **Tipi** di dati di base: Long, Double, Boolean, Date e String
* **Tipi** di dati complessi: [XML](https://docs.oracle.com/javase/8/docs/api/org/w3c/dom/Document.html) e [JSON](https://static.javadoc.io/com.google.code.gson/gson/2.3/com/google/gson/JsonObject.html)

>[!NOTE]
>
>I flussi di lavoro supportano solo il formato ISO8601 per le variabili di tipo Data.

Per ulteriori tipi di dati complessi disponibili nei flussi di lavoro AEM Forms, consulta [Variabili nei flussi di lavoro](/help/forms/using/variable-in-aem-workflows.md)AEM Forms.  Utilizzate il tipo di dati ArrayList per creare raccolte di variabili. È possibile creare una variabile ArrayList per tutti i tipi di dati primitivi e complessi. Ad esempio, creare una variabile ArrayList e selezionare String come sottotipo per memorizzare più valori stringa utilizzando la variabile.

Per creare una variabile, eseguite i seguenti passaggi:

1. In un’istanza di AEM, andate a Strumenti > Flusso di lavoro > Modelli.
1. Toccate **[!UICONTROL Crea]** e specificate il titolo e un nome facoltativo per il modello di workflow. Selezionate il modello e toccate **[!UICONTROL Modifica]**.
1. Toccate l&#39;icona delle variabili disponibile nella barra laterale del modello di workflow e toccate **[!UICONTROL Aggiungi variabile]**.

   ![Aggiungi variabile](assets/variables_add_variable_new.png)

1. Nella finestra di dialogo Aggiungi variabile, specificate il nome e selezionate il tipo di variabile.
1. Selezionare il tipo di dati dall&#39;elenco a discesa **[!UICONTROL Tipo]** e specificare i valori seguenti:

   * Tipo di dati di base - Specificate un valore predefinito facoltativo per la variabile.
   * JSON o XML - Specificate un percorso di schema JSON o XML facoltativo. Il sistema convalida il percorso dello schema durante la mappatura e la memorizzazione delle proprietà disponibili in questo schema a un&#39;altra variabile.
   * Modello dati modulo - Specifica un percorso del modello dati modulo.
   * ArrayList - Specifica un sottotipo per la raccolta.

1. Specificate una descrizione facoltativa per la variabile e toccate ![](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-4/forms/using/chart-component/Done_Icon.png) per salvare le modifiche. La variabile viene visualizzata nell’elenco disponibile nel riquadro a sinistra.

Quando create delle variabili, tenete presenti le seguenti procedure:

* Crea tutte le variabili necessarie per un flusso di lavoro. Tuttavia, per conservare le risorse del database, utilizzate il numero minimo di variabili richieste e riutilizzate le variabili quando possibile.
* Le variabili seguono la distinzione tra maiuscole e minuscole. Assicurati di fare riferimento alle variabili con lo stesso caso nel flusso di lavoro.
* Evitare di utilizzare caratteri speciali nel nome della variabile

## Impostare una variabile {#set-a-variable}

È possibile utilizzare il passaggio Imposta variabile per impostare il valore di una variabile e definire l&#39;ordine in cui i valori vengono impostati. La variabile viene impostata nell&#39;ordine in cui le mappature delle variabili sono elencate nel passaggio della variabile set.

Le modifiche ai valori delle variabili interessano solo l’istanza del processo in cui avviene la modifica. Ad esempio, quando un flusso di lavoro viene avviato e i dati variabili cambiano, le modifiche interessano solo l&#39;istanza del flusso di lavoro. Le modifiche non hanno effetto su altre istanze del flusso di lavoro avviate in precedenza o avviate successivamente.

A seconda del tipo di dati della variabile, è possibile utilizzare le seguenti opzioni per impostare il valore di una variabile:

* **** Letterale: Utilizzate l&#39;opzione quando conoscete il valore esatto da specificare.
* **** Espressione: Utilizzare l&#39;opzione quando il valore da utilizzare viene calcolato in base a un&#39;espressione. L&#39;espressione viene creata nell&#39;editor di espressioni fornito.
* **** Notazione punto JSON: Utilizzate l&#39;opzione per recuperare un valore da una variabile di tipo JSON o FDM.
* **** XPATH: Utilizzare l&#39;opzione per recuperare un valore da una variabile di tipo XML.
* **** Relativo al payload: Utilizzare l&#39;opzione quando il valore da salvare in variabile è disponibile in un percorso relativo al payload.
* **** Percorso assoluto: Utilizzare l&#39;opzione quando il valore da salvare nella variabile è disponibile in un percorso assoluto.

Potete anche aggiornare elementi specifici di una variabile di tipo JSON o XML utilizzando la notazione JSON DOT o XPATH.

### Aggiungi mappatura tra variabili {#add-mapping-between-variables}

Per aggiungere la mappatura tra le variabili, effettua i seguenti passaggi:

1. Nella pagina di modifica del flusso di lavoro, toccate l’icona Passaggi disponibile nella barra laterale del modello di workflow.
1. Trascinate il passaggio **Imposta variabile** nell’editor del flusso di lavoro, toccate il passaggio e selezionate ![](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-4/forms/using/configure_icon.png) (Configura).
1. Nella finestra di dialogo Imposta variabile, selezionare **[!UICONTROL Mapping]** > **[!UICONTROL Aggiungi mapping]**.
1. Nella sezione Variabile **** mappa, selezionate la variabile da memorizzare i dati, selezionate la modalità di mappatura e specificate un valore da memorizzare nella variabile. Le modalità di mappatura variano in base al tipo di variabile.
1. Mappare più variabili per creare un&#39;espressione significativa. Toccate ![](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-4/forms/using/chart-component/Done_Icon.png) per salvare le modifiche.

### Esempio 1: Eseguire una query su una variabile XML per impostare il valore di una variabile stringa {#example-query-an-xml-variable-to-set-value-for-a-string-variable}

Selezionare una variabile di tipo XML per memorizzare un file XML. Eseguire una query sulla variabile XML per impostare il valore di una variabile stringa per la proprietà disponibile nel file XML. Utilizzare **Specifica XPATH per il campo della variabile** XML per definire la proprietà da memorizzare nella variabile stringa.

In questo esempio, selezionate una variabile XML **formdata** per memorizzare il file **cc-app.xml** . Eseguite una query sulla variabile **formdata** per impostare il valore per la variabile della stringa **emailaddress** in modo da memorizzare il valore per la proprietà **emailAddress** disponibile nel file **cc-app.xml** .

>[!VIDEO](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/using/set_variable_example1.mp4 "Imposta il valore di una variabile")

### Esempio 2: Utilizzare un&#39;espressione per memorizzare un valore basato su altre variabili {#example2}

Utilizzare un&#39;espressione per calcolare la somma delle variabili e memorizzare il risultato in una variabile.

In questo esempio, utilizzate l&#39;editor di espressioni per definire un&#39;espressione per calcolare la somma delle variabili **assetscost** e **Balanceamount** e memorizzare il risultato nella variabile **totalvalue** .

>[!VIDEO](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/using/variables_expression.mp4)

## Usa editor espressioni {#use-expression-editor}

È inoltre possibile utilizzare le espressioni per calcolare il valore di una variabile nel runtime. Le variabili forniscono un editor di espressioni per definire le espressioni.

Utilizzate l&#39;editor di espressioni per:

* Impostare il valore delle variabili utilizzando altre variabili di flusso di lavoro, numeri o espressioni matematiche.
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

Per ulteriori informazioni, vedere Editor [di regole per moduli](/help/forms/using/rule-editor.md)adattivi.

## Utilizzare una variabile {#use-a-variable}

È possibile utilizzare le variabili per recuperare input e output o salvare il risultato di un passaggio. L’editor del flusso di lavoro fornisce due tipi di passaggi per il flusso di lavoro:

* Passaggi del flusso di lavoro con supporto per le variabili
* Passaggi del flusso di lavoro senza supporto delle variabili

### Passaggi del flusso di lavoro con supporto per le variabili {#workflow-steps-with-support-for-variables}

Il passaggio Vai a, O Dividi e tutti i passaggi del flusso di lavoro di AEM Forms supportano le variabili.

#### Passaggio divisione OR {#or-split-step}

La divisione OR crea una divisione nel flusso di lavoro, dopo di che è attivo un solo ramo. Questo passaggio consente di introdurre i percorsi di elaborazione condizionale nel flusso di lavoro. Potete aggiungere i passaggi del flusso di lavoro a ogni ramo, a seconda delle necessità.

È possibile definire l&#39;espressione di routing per un ramo utilizzando una definizione di regola, uno script ECMA o uno script esterno.

È possibile utilizzare le variabili per definire l&#39;espressione di routing utilizzando l&#39;editor di espressioni. Per ulteriori informazioni sull&#39;uso delle espressioni di routing per il passaggio di divisione OR, vedere Passaggio [di divisione](/help/sites-developing/workflows-step-ref.md#or-split)OR.

In questo esempio, prima di definire l&#39;espressione di routing, utilizzare [l&#39;esempio 2](/help/sites-developing/using-variables-in-aem-workflows.md#example2) per impostare il valore per la variabile **totalvalue** . Il ramo 1 è attivo se il valore della variabile **total value** è maggiore di 50000. Allo stesso modo, è possibile definire una regola per rendere attivo il ramo 2 se il valore della variabile **total value** è inferiore a 50000.

>[!VIDEO](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/using/variables_orsplit_example.mp4)

Analogamente, selezionare un percorso di script esterno o specificare lo script ECMA per le espressioni di routing per valutare il ramo attivo. Toccate **[!UICONTROL Rinomina ramo]** per specificare un nome alternativo per il ramo.

Per ulteriori esempi, consultate [Creare un modello](/help/forms/using/aem-forms-workflow.md#create-a-workflow-model)di workflow.

#### Vai al passaggio {#go-to-step}

Il passo **Vai** consente di specificare il passaggio successivo nel modello di workflow da eseguire, a seconda del risultato di un&#39;espressione di routing.

Analogamente al passaggio di divisione OR, è possibile definire l&#39;espressione di routing per il passaggio Goto utilizzando una definizione di regola, uno script ECMA o uno script esterno.

È possibile utilizzare le variabili per definire l&#39;espressione di routing utilizzando l&#39;editor di espressioni. Per ulteriori informazioni sull&#39;uso delle espressioni di routing per il passaggio Goto, vedere Passaggio [](/help/sites-developing/workflows-step-ref.md#goto-step)Goto.

![Vai a regola](assets/variables_goto_rule1_new.png)

In questo esempio, il passaggio Goto specifica l&#39;Applicazione carta di credito Rivedi come passaggio successivo se il valore per la variabile **action** è uguale a **Necessità di ulteriori informazioni**.

Per ulteriori esempi sull&#39;utilizzo della definizione della regola nel passaggio Goto, vedere [Simulazione di un ciclo](/help/sites-developing/workflows-step-ref.md#simulateforloop)For.

#### Passaggi del flusso di lavoro incentrati sui moduli {#forms-workflow-centric-workflow-steps}

Tutti i passaggi del flusso di lavoro di AEM Forms supportano le variabili. Per ulteriori informazioni, vedere Flusso di lavoro incentrato sui [moduli in OSGi](/help/forms/using/aem-forms-workflow-step-reference.md).

### Passaggi del flusso di lavoro senza supporto delle variabili {#workflow-steps-without-support-for-variables}

Puoi utilizzare l’interfaccia [MetaDataMap](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/metadata/MetaDataMap.html) per accedere alle variabili nei passaggi del flusso di lavoro che non supportano le variabili.

#### Recuperare il valore della variabile {#retrieve-the-variable-value}

Utilizzate le seguenti API nello script ECMA per recuperare i valori per le variabili esistenti in base al tipo di dati:

| Tipo di dati variabile | API |
|---|---|
| Primitive (Long, Double, Boolean, Date e String) | workItem.getWorkflowData().getMetaDataMap().get(variableName, type) |
| XML | Packages.org.w3c.dom.Document xmlObject = workItem.getWorkflowData().getMetaDataMap().get(variableName, Packages.org.w3c.dom.Document.class); |
| JSON | Packages.com.google.gson.JsonObject jsonObject = workItem.getWorkflowData().getMetaDataMap().get(variableName, Packages.com.google.gson.JsonObject.class); |

Per informazioni sulle API per ulteriori tipi di dati variabili complesse disponibili nei flussi di lavoro AEM Forms, consultate [Variabili nei flussi di lavoro](/help/forms/using/variable-in-aem-workflows.md)AEM Forms.

**Esempio**

Recuperare il valore del tipo di dati stringa utilizzando la seguente API:

```
workItem.getWorkflowData().getMetaDataMap().get(accname, Packages.java.lang.String)
```

#### Aggiornare il valore della variabile {#update-the-variable-value}

Utilizzate la seguente API nello script ECMA per aggiornare il valore di una variabile:

```
workItem.getWorkflowData().getMetaDataMap().put(variableName, value)
```

**Esempio**

```
workItem.getWorkflowData().getMetaDataMap().put(salary, 50000)
```

aggiorna il valore della variabile **stipendio** a 50000.

### Impostazione delle variabili per richiamare i flussi di lavoro {#apiinvokeworkflow}

Potete utilizzare un&#39;API per impostare le variabili e passarle alle istanze del flusso di lavoro richiamate.

[workflowSession.startWorkflow](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/WorkflowSession.html#startWorkflow-com.adobe.granite.workflow.model.WorkflowModel-com.adobe.granite.workflow.exec.WorkflowData-java.util.Map-) utilizza model, wfData e metaData come argomenti. Utilizzate MetaDataMap per impostare il valore della variabile.

In questa API, la variabile **variableName** è impostata su **value **utilizzando metaData.put(variableName, value);

```java
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

## Modificare una variabile {#edit-a-variable}

1. Nella pagina del flusso di lavoro di modifica, toccate l&#39;icona Variabili disponibile nella barra laterale del modello di workflow. Nella sezione Variabili del riquadro a sinistra sono visualizzate tutte le variabili esistenti.
1. Toccate l’icona ![](https://helpx.adobe.com/content/dam/help/images/en/edit.png) (Modifica) accanto al nome della variabile da modificare.
1. Modificate le informazioni sulla variabile e toccate ![](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-4/forms/using/chart-component/Done_Icon.png) per salvare le modifiche. Non è possibile modificare i campi **[!UICONTROL Nome]** e **[!UICONTROL Tipo]** per una variabile.

## Eliminare una variabile {#delete-a-variable}

Prima di eliminare la variabile, rimuovete dal flusso di lavoro tutti i riferimenti della variabile. Assicurarsi che la variabile non sia utilizzata nel flusso di lavoro.

Per eliminare una variabile, eseguite i seguenti passaggi:

1. Nella pagina del flusso di lavoro di modifica, toccate l&#39;icona Variabili disponibile nella barra laterale del modello di workflow. Nella sezione Variabili del riquadro a sinistra sono visualizzate tutte le variabili esistenti.
1. Toccate l’icona Elimina accanto al nome della variabile da eliminare.
1. Toccate ![](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-4/forms/using/chart-component/Done_Icon.png) per confermare ed eliminare la variabile.

