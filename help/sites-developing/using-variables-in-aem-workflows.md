---
title: Variabili nei flussi di lavoro AEM
seo-title: Variables in AEM Workflows
description: Crea una variabile, imposta un valore per la variabile e utilizzala nei passaggi del flusso di lavoro di divisione OR e Vai AEM.
seo-description: Create a variable, set a value for the variable, and use it in OR Split and  Goto AEM workflow steps.
uuid: cc62ff11-51d4-4db4-9c6d-5dc2caa1da52
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: bbb9936e-ecd2-44b3-b4ae-dd62a3160641
docset: aem65
exl-id: c8aeceec-860c-49ee-b681-d7107e52020d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2057'
ht-degree: 0%

---

# Variabili nei flussi di lavoro AEM{#variables-in-aem-workflows}

Una variabile in un modello di flusso di lavoro è un modo per memorizzare un valore in base al suo tipo di dati. Puoi quindi utilizzare il nome della variabile in qualsiasi passaggio del flusso di lavoro per recuperare il valore memorizzato nella variabile . È inoltre possibile utilizzare i nomi delle variabili per definire le espressioni per prendere decisioni di indirizzamento.

Nei modelli AEM flusso di lavoro puoi:

* [Creare una variabile](/help/sites-developing/using-variables-in-aem-workflows.md#create-a-variable) di un tipo di dati in base al tipo di informazioni che si desidera memorizzare in esso.
* [Imposta un valore per la variabile](/help/sites-developing/using-variables-in-aem-workflows.md#set-a-variable) mediante il passaggio del flusso di lavoro Imposta variabile .
* [Utilizza la variabile](/help/sites-developing/using-variables-in-aem-workflows.md#use-a-variable) nei passaggi del flusso di lavoro Dividi e Vai in OR per definire un’espressione per prendere decisioni di indirizzamento. Puoi anche utilizzare le variabili in tutti i passaggi del flusso di lavoro di AEM Forms.

Il video seguente illustra come creare, impostare e utilizzare le variabili nei modelli di flusso di lavoro AEM:

>[!VIDEO](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/using/usevariables_example.mp4)

Le variabili sono un&#39;estensione del [MetaDataMap](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/metadata/MetaDataMap.html) interfaccia. È possibile utilizzare [MetaDataMap](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/metadata/MetaDataMap.html) in ECMAScript per accedere ai metadati salvati utilizzando le variabili.

## Creare una variabile {#create-a-variable}

Puoi creare le variabili utilizzando la sezione Variabili disponibile nella barra laterale del modello di flusso di lavoro. AEM variabili del flusso di lavoro supportano i seguenti tipi di dati:

* **Tipi di dati principali**: Long, Double, Boolean, Date e String
* **Tipi di dati complessi**: [XML](https://docs.oracle.com/javase/8/docs/api/org/w3c/dom/Document.html) e [JSON](https://static.javadoc.io/com.google.code.gson/gson/2.3/com/google/gson/JsonObject.html)

>[!NOTE]
>
>I flussi di lavoro supportano solo il formato ISO8601 per le variabili di tipo Data.

Per ulteriori tipi di dati complessi disponibili nei flussi di lavoro AEM Forms, consulta [Variabili nei flussi di lavoro AEM Forms](/help/forms/using/variable-in-aem-workflows.md).  Utilizzare il tipo di dati ArrayList per creare raccolte di variabili. È possibile creare una variabile ArrayList per tutti i tipi di dati primitivi e complessi. Ad esempio, creare una variabile ArrayList e selezionare Stringa come sottotipo per memorizzare più valori stringa utilizzando la variabile .

Esegui i seguenti passaggi per creare una variabile:

1. In un&#39;istanza AEM, passa a Strumenti > Flusso di lavoro > Modelli.
1. Tocca **[!UICONTROL Crea]** e specifica il titolo e un nome facoltativo per il modello di flusso di lavoro. Seleziona il modello e tocca **[!UICONTROL Modifica]**.
1. Tocca l’icona delle variabili disponibile nella barra laterale del modello di flusso di lavoro e tocca **[!UICONTROL Aggiungi variabile]**.

   ![Aggiungi variabile](assets/variables_add_variable_new.png)

1. Nella finestra di dialogo Aggiungi variabile , specifica il nome e seleziona il tipo di variabile.
1. Seleziona il tipo di dati dal **[!UICONTROL Tipo]** elenco a discesa e specifica i seguenti valori:

   * Tipo di dati primitivo - Specifica un valore predefinito facoltativo per la variabile.
   * JSON o XML - Specifica un percorso di schema JSON o XML facoltativo. Il sistema convalida il percorso dello schema durante la mappatura e la memorizzazione delle proprietà disponibili in questo schema in un&#39;altra variabile.
   * Modello dati modulo : consente di specificare un percorso del modello dati del modulo.
   * ArrayList - Specifica un sottotipo per la raccolta.

1. Specifica una descrizione facoltativa per la variabile e tocca ![](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-4/forms/using/chart-component/Done_Icon.png) per salvare le modifiche. La variabile viene visualizzata nell’elenco disponibile nel riquadro a sinistra.

Quando crei delle variabili, prendi in considerazione le seguenti pratiche:

* Crea tutte le variabili necessarie per un flusso di lavoro. Tuttavia, per conservare le risorse del database, utilizza il numero minimo di variabili richieste e riutilizza le variabili quando possibile.
* Le variabili sono sensibili all’uso di maiuscole e minuscole. Assicurati di fare riferimento alle variabili utilizzando lo stesso caso nel flusso di lavoro.
* Evita di usare caratteri speciali nel nome della variabile

## Imposta una variabile {#set-a-variable}

È possibile utilizzare il passaggio Imposta variabile per impostare il valore di una variabile e definire l&#39;ordine in cui i valori vengono impostati. La variabile è impostata nell’ordine in cui le mappature delle variabili sono elencate nel passaggio set variable .

Le modifiche ai valori delle variabili influiscono solo sull&#39;istanza del processo in cui avviene la modifica. Ad esempio, quando un flusso di lavoro viene avviato e i dati delle variabili cambiano, le modifiche influiscono solo sull’istanza del flusso di lavoro. Le modifiche non influiscono su altre istanze del flusso di lavoro che sono state avviate in precedenza o che sono state avviate successivamente.

A seconda del tipo di dati della variabile, è possibile utilizzare le seguenti opzioni per impostare il valore di una variabile:

* **Letterale:** Utilizza l’opzione quando conosci il valore esatto da specificare.
* **Espressione:** Utilizza l’opzione quando il valore da utilizzare viene calcolato in base a un’espressione. L’espressione viene creata nell’editor di espressioni fornito.
* **Notazione punto JSON:** Utilizza l’opzione per recuperare un valore da una variabile di tipo JSON o FDM.
* **XPATH:** Utilizzare l&#39;opzione per recuperare un valore da una variabile di tipo XML.
* **Relativo al payload:** Utilizza l’opzione quando il valore da salvare nella variabile è disponibile in un percorso relativo al payload.
* **Percorso assoluto:** Utilizza l’opzione quando il valore da salvare nella variabile è disponibile in un percorso assoluto.

È inoltre possibile aggiornare elementi specifici di una variabile di tipo JSON o XML utilizzando la notazione DOT JSON o XPATH.

### Aggiungi mappatura tra variabili {#add-mapping-between-variables}

Esegui i seguenti passaggi per aggiungere la mappatura tra le variabili:

1. Nella pagina di modifica del flusso di lavoro, tocca l’icona Passaggi disponibile nella barra laterale del modello di flusso di lavoro.
1. Trascina e rilascia la **Imposta variabile** passa all’editor del flusso di lavoro, tocca il passaggio e seleziona ![](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-4/forms/using/configure_icon.png) (Configura).
1. Nella finestra di dialogo Imposta variabile, seleziona **[!UICONTROL Mappatura]** > **[!UICONTROL Aggiungi mappatura]**.
1. In **Variabile mappa** , seleziona la variabile da memorizzare i dati, seleziona la modalità di mappatura e specifica un valore da memorizzare nella variabile . Le modalità di mappatura variano in base al tipo di variabile.
1. Mappa più variabili per creare un’espressione significativa. Tocca ![](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-4/forms/using/chart-component/Done_Icon.png) per salvare le modifiche.

### Esempio 1: Eseguire una query su una variabile XML per impostare il valore di una variabile stringa {#example-query-an-xml-variable-to-set-value-for-a-string-variable}

Selezionare una variabile di tipo XML per memorizzare un file XML. Eseguire una query sulla variabile XML per impostare il valore di una variabile stringa per la proprietà disponibile nel file XML. Utilizzo **Specifica XPATH per la variabile XML** per definire la proprietà da memorizzare nella variabile stringa.

In questo esempio, seleziona una **formdata** Variabile XML in cui memorizzare **cc-app.xml** file. Eseguire una query **formdata** per impostare il valore per **indirizzo email** variabile stringa per memorizzare il valore per **emailAddress** disponibile nella **cc-app.xml** file.

>[!VIDEO](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/using/set_variable_example1.mp4 "Imposta il valore di una variabile")

### Esempio 2: Utilizza un’espressione per memorizzare un valore basato su altre variabili {#example2}

Utilizza un&#39;espressione per calcolare la somma delle variabili e memorizzare il risultato in una variabile.

In questo esempio, utilizza l’editor di espressioni per definire un’espressione per calcolare la somma di **assetscost** e **saldo** e memorizza il risultato in **total value** variabile.

>[!VIDEO](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/using/variables_expression.mp4)

## Utilizza editor di espressioni {#use-expression-editor}

Puoi inoltre utilizzare le espressioni per calcolare il valore di una variabile in fase di runtime. Le variabili forniscono un editor di espressioni per definire le espressioni.

Utilizza l’editor di espressioni per:

* Imposta il valore delle variabili utilizzando altre variabili del flusso di lavoro, numeri o espressioni matematiche.
* Utilizzare variabili di flusso di lavoro, stringa, numero o espressione all’interno di un’espressione matematica
* Aggiungi condizioni per impostare valori di variabili.
* Aggiungi operatori tra condizioni.

![Editor espressioni](assets/variables_expression_editor_new.png)

Si basa sull’editor di regole dei moduli adattivi con le seguenti modifiche. Editor di regole nelle variabili:

* Non supporta le funzioni.
* Non fornisce un&#39;interfaccia utente per visualizzare il riepilogo delle regole
* Non dispone di editor di codice.
* Non supporta l&#39;abilitazione e la disattivazione del valore di un oggetto.
* Non supporta l&#39;impostazione della proprietà di un oggetto.
* Non supporta la chiamata di un servizio Web.

Per ulteriori informazioni, consulta [editor di regole per moduli adattivi](/help/forms/using/rule-editor.md).

## Utilizzare una variabile {#use-a-variable}

È possibile utilizzare le variabili per recuperare gli input e l’output o salvare il risultato di un passaggio. L’editor del flusso di lavoro fornisce due tipi di passaggi del flusso di lavoro:

* Passaggi del flusso di lavoro con supporto per le variabili
* Passaggi del flusso di lavoro senza supporto per le variabili

### Passaggi del flusso di lavoro con supporto per le variabili {#workflow-steps-with-support-for-variables}

Il passaggio Vai a, O Dividi e tutti i passaggi del flusso di lavoro AEM Forms supportano le variabili.

#### Passaggio a divisione OR {#or-split-step}

La divisione OR crea una suddivisione nel flusso di lavoro, dopodiché è attivo un solo ramo. Questo passaggio ti consente di introdurre i percorsi di elaborazione condizionale nel flusso di lavoro. Puoi aggiungere i passaggi del flusso di lavoro a ogni ramo in base alle tue esigenze.

È possibile definire l&#39;espressione di indirizzamento per un ramo utilizzando una definizione di regola, uno script ECMA o uno script esterno.

Puoi utilizzare le variabili per definire l’espressione di indirizzamento utilizzando l’editor di espressioni. Per ulteriori informazioni sull&#39;utilizzo delle espressioni di indirizzamento per il passaggio Divisione OR, vedere [Passaggio a divisione OR](/help/sites-developing/workflows-step-ref.md#or-split).

In questo esempio, prima di definire l&#39;espressione di indirizzamento, utilizza [esempio 2](/help/sites-developing/using-variables-in-aem-workflows.md#example2) per impostare il valore per **total value** variabile. La diramazione 1 è attiva se il valore della **total value** è maggiore di 50000. Allo stesso modo, è possibile definire una regola per rendere attivo il ramo 2 se il valore del **total value** è inferiore a 50000.

>[!VIDEO](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/using/variables_orsplit_example.mp4)

Analogamente, selezionare un percorso di script esterno o specificare lo script ECMA per le espressioni di routing per valutare il ramo attivo. Tocca **[!UICONTROL Rinomina ramo]** per specificare un nome alternativo per il ramo.

Per ulteriori esempi, consulta [Creare un modello di flusso di lavoro](/help/forms/using/aem-forms-workflow.md#create-a-workflow-model).

#### Vai al passaggio {#go-to-step}

La **Passaggio Vai a** consente di specificare il passaggio successivo nel modello di flusso di lavoro da eseguire, in base al risultato di un&#39;espressione di indirizzamento.

Simile al passaggio di divisione OR, è possibile definire l&#39;espressione di indirizzamento per il passaggio Goto utilizzando una definizione di regola, uno script ECMA o uno script esterno.

Puoi utilizzare le variabili per definire l’espressione di indirizzamento utilizzando l’editor di espressioni. Per ulteriori informazioni sull&#39;utilizzo delle espressioni di indirizzamento per il passaggio Passaggio , vedi [Passaggio Vai a](/help/sites-developing/workflows-step-ref.md#goto-step).

![Regola Vai a](assets/variables_goto_rule1_new.png)

In questo esempio, il passaggio Passaggio specifica l&#39;applicazione con carta di credito di revisione come passaggio successivo se il valore per **azioni intraprese** è uguale a **Ulteriori informazioni**.

Per ulteriori esempi sull’utilizzo della definizione della regola nel passaggio Passaggio , vedi [Simulazione di un ciclo For](/help/sites-developing/workflows-step-ref.md#simulateforloop).

#### Passaggi del flusso di lavoro incentrati sul flusso di lavoro Forms {#forms-workflow-centric-workflow-steps}

Tutti i passaggi del flusso di lavoro di AEM Forms supportano le variabili. Per ulteriori informazioni, consulta [Flusso di lavoro incentrato su Forms su OSGi](/help/forms/using/aem-forms-workflow-step-reference.md).

### Passaggi del flusso di lavoro senza supporto per le variabili {#workflow-steps-without-support-for-variables}

È possibile utilizzare [MetaDataMap](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/metadata/MetaDataMap.html) per accedere alle variabili nei passaggi del flusso di lavoro che non supportano le variabili.

#### Recupera il valore della variabile {#retrieve-the-variable-value}

Utilizza le seguenti API nello script ECMA per recuperare i valori per le variabili esistenti in base al tipo di dati:

| Tipo di dati variabile | API |
|---|---|
| Primitivo (Long, Double, Boolean, Date e String) | workItem.getWorkflowData().getMetaDataMap().get(variableName, type) |
| XML | Packages.org.w3c.dom.Document xmlObject = workItem.getWorkflowData().getMetaDataMap().get(variableName, Packages.org.w3c.dom.Document.class); |
| JSON | Packages.com.google.gson.JsonObject jsonObject = workItem.getWorkflowData().getMetaDataMap().get(variableName, Packages.com.google.gson.JsonObject.class); |

Per informazioni sulle API per ulteriori tipi di dati variabili complesse disponibili nei flussi di lavoro AEM Forms, consulta [Variabili nei flussi di lavoro AEM Forms](/help/forms/using/variable-in-aem-workflows.md).

**Esempio**

Recupera il valore del tipo di dati stringa utilizzando la seguente API:

```
workItem.getWorkflowData().getMetaDataMap().get(accname, Packages.java.lang.String)
```

#### Aggiorna il valore della variabile {#update-the-variable-value}

Utilizza la seguente API nello script ECMA per aggiornare il valore di una variabile:

```
workItem.getWorkflowData().getMetaDataMap().put(variableName, value)
```

**Esempio**

```
workItem.getWorkflowData().getMetaDataMap().put(salary, 50000)
```

aggiorna il valore per **stipendio** a 50000.

### Impostare le variabili per richiamare i flussi di lavoro {#apiinvokeworkflow}

Puoi utilizzare un’API per impostare le variabili e trasmetterle alle istanze del flusso di lavoro.

[workflowSession.startWorkflow](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/WorkflowSession.html#startWorkflow-com.adobe.granite.workflow.model.WorkflowModel-com.adobe.granite.workflow.exec.WorkflowData-java.util.Map-) utilizza model, wfData e metaData come argomenti. Utilizza MetaDataMap per impostare il valore della variabile.

In questa API, la **variableName** è impostata su **value** utilizzando metaData.put(variableName, value);

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

1. Nella pagina modifica flusso di lavoro , tocca l’icona Variabili disponibile nella barra laterale del modello di flusso di lavoro. Nella sezione Variabili del riquadro a sinistra vengono visualizzate tutte le variabili esistenti.
1. Tocca ![](https://helpx.adobe.com/content/dam/help/images/en/edit.png) (Modifica) accanto al nome della variabile da modificare.
1. Modifica le informazioni sulla variabile e tocca ![](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-4/forms/using/chart-component/Done_Icon.png) per salvare le modifiche. Non è possibile modificare il **[!UICONTROL Nome]** e **[!UICONTROL Tipo]** campi per una variabile.

## Eliminare una variabile {#delete-a-variable}

Prima di eliminare la variabile, rimuovi tutti i riferimenti della variabile dal flusso di lavoro. Assicurati che la variabile non sia utilizzata nel flusso di lavoro.

Esegui i seguenti passaggi per eliminare una variabile:

1. Nella pagina modifica flusso di lavoro , tocca l’icona Variabili disponibile nella barra laterale del modello di flusso di lavoro. Nella sezione Variabili del riquadro a sinistra vengono visualizzate tutte le variabili esistenti.
1. Tocca l’icona Elimina accanto al nome della variabile da eliminare.
1. Tocca ![](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-4/forms/using/chart-component/Done_Icon.png) per confermare ed eliminare la variabile.
