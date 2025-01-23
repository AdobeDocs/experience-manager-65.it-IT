---
title: Variabili nei flussi di lavoro AEM
description: Crea una variabile, imposta un valore per la variabile e utilizzala nei passaggi del flusso di lavoro Divisione OR e Vai a AEM.
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
docset: aem65
exl-id: c8aeceec-860c-49ee-b681-d7107e52020d
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 8305f77e895ad383a398cf8d4effa2b64cd45677
workflow-type: tm+mt
source-wordcount: '1935'
ht-degree: 0%

---

# Variabili nei flussi di lavoro AEM{#variables-in-aem-workflows}

Una variabile in un modello di flusso di lavoro è un modo per memorizzare un valore in base al relativo tipo di dati. Puoi quindi utilizzare il nome della variabile in qualsiasi passaggio del flusso di lavoro per recuperare il valore memorizzato nella variabile. È inoltre possibile utilizzare i nomi delle variabili per definire le espressioni per l&#39;adozione delle decisioni di instradamento.

Nei modelli di flusso di lavoro dell’AEM puoi effettuare le seguenti operazioni:

* [Creare una variabile](/help/sites-developing/using-variables-in-aem-workflows.md#create-a-variable) di un tipo di dati in base al tipo di informazioni che si desidera memorizzare.
* [Impostare un valore per la variabile](/help/sites-developing/using-variables-in-aem-workflows.md#set-a-variable) utilizzando il passaggio del flusso di lavoro Imposta variabile.
* [Utilizzare la variabile](/help/sites-developing/using-variables-in-aem-workflows.md#use-a-variable) nei passaggi del flusso di lavoro OR Split e Goto AEM in modo da poter definire un&#39;espressione per prendere decisioni di indirizzamento. Puoi anche utilizzare le variabili in tutti i passaggi del flusso di lavoro di AEM Forms.

Il video seguente illustra come creare, impostare e utilizzare le variabili nei modelli di flusso di lavoro AEM:

<!-- FUTURE ERROR: YouTube and mp4 videos are not supported -->

>[!VIDEO](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/using/usevariables_example.mp4)

Le variabili sono un&#39;estensione dell&#39;interfaccia [MetaDataMap](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/granite/workflow/metadata/MetaDataMap.html). È possibile utilizzare [MetaDataMap](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/granite/workflow/metadata/MetaDataMap.html) in ECMAScript per accedere ai metadati salvati utilizzando le variabili.

## Creare una variabile {#create-a-variable}

Puoi creare le variabili utilizzando la sezione Variabili disponibile nella barra laterale del modello di flusso di lavoro. Le variabili del flusso di lavoro AEM supportano i seguenti tipi di dati:

* **Tipi di dati di base**: Long, Double, Boolean, Date e String
* **Tipi di dati complessi**: [XML](https://docs.oracle.com/javase/8/docs/api/org/w3c/dom/Document.html) e [JSON](https://www.javadoc.io/doc/com.google.code.gson/gson/2.3/com/google/gson/JsonObject.html)

>[!NOTE]
>
>I flussi di lavoro supportano solo il formato ISO8601 per le variabili di tipo Data.

Per ulteriori tipi di dati complessi disponibili nei flussi di lavoro AEM Forms, vedi [Variabili nei flussi di lavoro AEM Forms](/help/forms/using/variable-in-aem-workflows.md). Utilizzare il tipo di dati ArrayList per creare raccolte di variabili. È possibile creare una variabile ArrayList per tutti i tipi di dati primitivi e complessi. Ad esempio, creare una variabile ArrayList e selezionare Stringa come sottotipo per memorizzare più valori stringa utilizzando la variabile.

Per creare una variabile:

1. In un’istanza AEM, passa a Strumenti > Flusso di lavoro > Modelli.
1. Seleziona **[!UICONTROL Crea]** e specifica il titolo e un nome facoltativo per il modello di flusso di lavoro. Selezionare il modello e selezionare **[!UICONTROL Modifica]**.
1. Seleziona l&#39;icona delle variabili disponibile nella barra laterale del modello di flusso di lavoro e seleziona **[!UICONTROL Aggiungi variabile]**.

   ![Aggiungi variabile](assets/variables_add_variable_new.png)

1. Nella finestra di dialogo Aggiungi variabile, specifica il nome e seleziona il tipo di variabile.
1. Selezionare il tipo di dati dall&#39;elenco a discesa **[!UICONTROL Tipo]** e specificare i valori seguenti:

   * Tipo di dati primitivo: specifica un valore predefinito facoltativo per la variabile.
   * JSON o XML: specifica un percorso JSON o schema XML facoltativo. Il sistema convalida il percorso dello schema durante la mappatura e l&#39;archiviazione delle proprietà disponibili in questo schema in un&#39;altra variabile.
   * Modello dati modulo: specifica un percorso per il modello dati modulo.
   * ArrayList - Specificare un sottotipo per la raccolta.

1. Specificare una descrizione facoltativa per la variabile e selezionare ![Icona Salva indicata da un segno di spunta all&#39;interno di una casella.](assets/Done_Icon.png) per salvare le modifiche. La variabile viene visualizzata nell’elenco disponibile nel riquadro a sinistra.

Quando crei delle variabili, prendi in considerazione le seguenti procedure:

* Crea tutte le variabili necessarie per un flusso di lavoro. Tuttavia, per conservare le risorse del database, utilizza il numero minimo di variabili richieste e, se possibile, riutilizza le variabili.
* Per le variabili viene fatta distinzione tra maiuscole e minuscole. Assicurati di fare riferimento alle variabili utilizzando la stessa maiuscola/minuscola nel flusso di lavoro.
* Evita di usare caratteri speciali nel nome della variabile

## Imposta una variabile {#set-a-variable}

È possibile utilizzare il passo Imposta variabile per impostare il valore di una variabile e definire l&#39;ordine in cui i valori vengono impostati. La variabile viene impostata nell’ordine in cui le mappature delle variabili sono elencate nel passaggio Imposta variabile.

Le modifiche ai valori delle variabili influiscono solo sull&#39;istanza del processo in cui si verifica la modifica. Ad esempio, quando viene avviato un flusso di lavoro e i dati delle variabili cambiano, le modifiche influiscono solo su tale istanza del flusso di lavoro. Le modifiche non influiscono su altre istanze del flusso di lavoro avviate in precedenza o in un secondo momento.

A seconda del tipo di dati della variabile, puoi utilizzare le seguenti opzioni per impostare il valore di una variabile:

* **Valore letterale:** Utilizzare l&#39;opzione quando si conosce il valore esatto da specificare.
* **Espressione:** Utilizzare l&#39;opzione quando il valore da utilizzare viene calcolato in base a un&#39;espressione. L’espressione viene creata nell’editor di espressioni fornito.
* **Notazione punti JSON:** Utilizzare l&#39;opzione per recuperare un valore da una variabile di tipo JSON o FDM.
* **XPATH:** Utilizzare l&#39;opzione per recuperare un valore da una variabile di tipo XML.
* **Relativo al payload:** Utilizzare l&#39;opzione quando il valore da salvare nella variabile è disponibile in un percorso relativo al payload.
* **Percorso assoluto:** Utilizzare l&#39;opzione quando il valore da salvare nella variabile è disponibile in un percorso assoluto.

È inoltre possibile aggiornare elementi specifici di una variabile di tipo JSON o XML utilizzando la notazione JSON DOT o XPATH.

### Aggiungi mappatura tra variabili {#add-mapping-between-variables}

Per aggiungere la mappatura tra variabili, eseguire le operazioni seguenti:

1. Nella pagina di modifica del flusso di lavoro, seleziona l’icona Passaggi disponibile nella barra laterale del modello di flusso di lavoro.
1. Trascinare e rilasciare il passaggio **Imposta variabile** nell&#39;editor del flusso di lavoro, selezionare il passaggio e selezionare ![Icona Configura indicata da una chiave inglese.](assets/configure_icon.png) (Configura).
1. Nella finestra di dialogo Imposta variabile, seleziona **[!UICONTROL Mapping]** > **[!UICONTROL Aggiungi mapping]**.
1. Nella sezione **Variabile mappa** selezionare la variabile per la memorizzazione dei dati, selezionare la modalità di mappatura e specificare un valore da memorizzare nella variabile. Le modalità di mappatura variano in base al tipo di variabile.
1. Mappa più variabili in modo da poter creare un’espressione significativa. Selezionare l&#39;icona di salvataggio ![contrassegnata da un segno di spunta all&#39;interno di una casella.](assets/Done_Icon.png) per salvare le modifiche.

### Esempio 1: eseguire una query su una variabile XML per impostare il valore per una variabile stringa {#example-query-an-xml-variable-to-set-value-for-a-string-variable}

Selezionare una variabile di tipo XML in cui memorizzare un file XML. Eseguire una query sulla variabile XML per impostare il valore di una variabile stringa per la proprietà disponibile nel file XML. Utilizzare **Specificare XPATH per il campo della variabile XML** per definire la proprietà da memorizzare nella variabile stringa.

In questo esempio, selezionare una variabile XML **formdata** per archiviare il file **cc-app.xml**. Eseguire una query sulla variabile **formdata** in modo da impostare il valore per la variabile di stringa **emailaddress** per archiviare il valore per la proprietà **emailAddress** disponibile nel file **cc-app.xml**.

>[!VIDEO](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/using/set_variable_example1.mp4 "Imposta il valore di una variabile")

### Esempio 2: utilizzare un’espressione per memorizzare un valore basato su altre variabili {#example2}

Utilizza un’espressione per calcolare la somma delle variabili e memorizzare il risultato in una variabile.

In questo esempio, utilizza l&#39;editor espressioni per definire un&#39;espressione per calcolare la somma di **variabili assetscost** e **balanceamount** e archiviare il risultato in **variabile totalvalue**.

<!-- FUTURE ERROR: YouTube and mp4 videos are not supported -->

>[!VIDEO](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/using/variables_expression.mp4)

## Utilizza editor di espressioni {#use-expression-editor}

Puoi anche utilizzare le espressioni per calcolare il valore di una variabile in fase di esecuzione. Le variabili forniscono un editor di espressioni per definire le espressioni.

Utilizza l’editor di espressioni per:

* Imposta il valore delle variabili utilizzando altre variabili del flusso di lavoro, numeri o espressioni matematiche.
* Utilizzare variabili del flusso di lavoro, stringhe, numeri o espressioni all’interno di un’espressione matematica
* Aggiungi condizioni per poter impostare i valori delle variabili.
* Aggiungi operatori tra condizioni.

![Editor espressioni](assets/variables_expression_editor_new.png)

Si basa sull’editor di regole per moduli adattivi con le seguenti modifiche. Editor regole nelle variabili:

* Non supporta funzioni.
* Non fornisce un’interfaccia utente per visualizzare il riepilogo delle regole
* Non dispone di editor di codice.
* Non supporta l&#39;abilitazione e la disabilitazione del valore di un oggetto.
* Non supporta l&#39;impostazione della proprietà di un oggetto.
* Non supporta la chiamata di un servizio web.

Per ulteriori informazioni, consulta [editor di regole per moduli adattivi](/help/forms/using/rule-editor.md).

## Utilizza una variabile {#use-a-variable}

È possibile utilizzare le variabili per recuperare input e output o salvare il risultato di un passaggio. L’editor del flusso di lavoro fornisce due tipi di passaggi del flusso di lavoro:

* Passaggi del flusso di lavoro con supporto per le variabili
* Passaggi del flusso di lavoro senza supporto per le variabili

### Passaggi del flusso di lavoro con supporto per le variabili {#workflow-steps-with-support-for-variables}

Il passaggio Vai a, il passaggio di suddivisione OR e tutti i passaggi del flusso di lavoro di AEM Forms supportano le variabili.

#### O Dividi passaggio {#or-split-step}

La suddivisione OR crea una suddivisione nel flusso di lavoro, dopo la quale è attivo un solo ramo. Questo passaggio ti consente di introdurre nel flusso di lavoro i percorsi di elaborazione condizionale. Puoi aggiungere i passaggi del flusso di lavoro a ogni ramo in base alle esigenze.

È possibile definire un&#39;espressione di indirizzamento per un ramo utilizzando una definizione di regola, uno script ECMA o uno script esterno.

È possibile utilizzare le variabili per definire l’espressione di indirizzamento utilizzando l’editor di espressioni. Per ulteriori informazioni sull&#39;utilizzo delle espressioni di routing per il passaggio Divisione OR, vedere [Passaggio Divisione OR](/help/sites-developing/workflows-step-ref.md#or-split).

In questo esempio, prima di definire l&#39;espressione di routing, utilizzare [esempio 2](/help/sites-developing/using-variables-in-aem-workflows.md#example2) per impostare il valore per la variabile **totalvalue**. Il ramo 1 è attivo se il valore della variabile **totalvalue** è maggiore di 50000. Allo stesso modo, puoi definire una regola per rendere attivo il Ramo 2 se il valore della variabile **totalvalue** è minore di 50000.

<!-- FUTURE ERROR: YouTube and mp4 videos are not supported -->

>[!VIDEO](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/using/variables_orsplit_example.mp4)

Analogamente, selezionate un percorso di script esterno o specificate lo script ECMA per instradare le espressioni per valutare il ramo attivo. Selezionare **[!UICONTROL Rinomina branch]** per specificare un nome alternativo per il branch.

Per ulteriori esempi, vedere [Creare un modello di flusso di lavoro](/help/forms/using/aem-forms-workflow.md#create-a-workflow-model).

#### Vai al passaggio {#go-to-step}

Il **passaggio Vai a** consente di specificare il passaggio successivo da eseguire nel modello di flusso di lavoro, a seconda del risultato di un&#39;espressione di routing.

Analogamente alla fase di suddivisione OR, potete definire l&#39;espressione di indirizzamento per la fase Vai a (Goto) utilizzando una definizione di regola, uno script ECMA o uno script esterno.

È possibile utilizzare le variabili per definire l’espressione di indirizzamento utilizzando l’editor di espressioni. Per ulteriori informazioni sull&#39;utilizzo delle espressioni di routing per il passaggio Goto, vedere [Passaggio Goto](/help/sites-developing/workflows-step-ref.md#goto-step).

![Vai a regola](assets/variables_goto_rule1_new.png)

In questo esempio, il passaggio Vai a specifica il passaggio successivo Verifica richiesta carta di credito se il valore per la variabile **actiontaked** è uguale a **Ulteriori informazioni necessarie**.

Per ulteriori esempi sull&#39;utilizzo della definizione della regola nel passaggio Vai a, vedere [Simulazione di un ciclo For](/help/sites-developing/workflows-step-ref.md#simulateforloop).

#### Passaggi del flusso di lavoro incentrati sul flusso di lavoro Forms {#forms-workflow-centric-workflow-steps}

Tutti i passaggi di AEM Forms Workflow supportano le variabili. Per ulteriori informazioni, consulta [Flusso di lavoro incentrato su Forms in OSGi](/help/forms/using/aem-forms-workflow-step-reference.md).

### Passaggi del flusso di lavoro senza supporto per le variabili {#workflow-steps-without-support-for-variables}

È possibile utilizzare l&#39;interfaccia [MetaDataMap](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/granite/workflow/metadata/MetaDataMap.html) per accedere alle variabili nei passaggi del flusso di lavoro che non supportano le variabili.

#### Recupera il valore della variabile {#retrieve-the-variable-value}

Per recuperare i valori per le variabili esistenti in base al tipo di dati, utilizza le seguenti API nello script ECMA.

| Tipo di dati variabile | API |
|---|---|
| Primitiva (Long, Double, Boolean, Date e String) | workItem.getWorkflowData().getMetaDataMap().get(variableName, type) |
| XML | Packages.org.w3c.dom.Document xmlObject = workItem.getWorkflowData().getMetaDataMap().get(variableName, Packages.org.w3c.dom.Document.class); |
| JSON | Packages.com.google.gson.JsonObject jsonObject = workItem.getWorkflowData().getMetaDataMap().get(variableName, Packages.com.google.gson.JsonObject.class); |

Per informazioni sulle API per ulteriori tipi di dati per variabili complesse disponibili nei flussi di lavoro di AEM Forms, vedi [Variabili nei flussi di lavoro di AEM Forms](/help/forms/using/variable-in-aem-workflows.md).

**Esempio**

Recupera il valore del tipo di dati stringa utilizzando la seguente API:

```
workItem.getWorkflowData().getMetaDataMap().get(accname, Packages.java.lang.String)
```

#### Aggiornare il valore della variabile {#update-the-variable-value}

Per aggiornare il valore di una variabile, utilizzare la seguente API nello script ECMA.

```
workItem.getWorkflowData().getMetaDataMap().put(variableName, value)
```

**Esempio**

```
workItem.getWorkflowData().getMetaDataMap().put(salary, 50000)
```

Aggiorna il valore della variabile **stipendio** in 50000.

### Impostare le variabili per richiamare i flussi di lavoro {#apiinvokeworkflow}

Puoi utilizzare un’API per impostare le variabili e trasmetterle alle istanze del flusso di lavoro.

[workflowSession.startWorkflow](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/granite/workflow/WorkflowSession.html#startWorkflow-com.adobe.granite.workflow.model.WorkflowModel-com.adobe.granite.workflow.exec.WorkflowData-java.util.Map-) utilizza model, wfData e metaData come argomenti. Utilizza MetaDataMap per impostare il valore della variabile.

In questa API, la variabile **variableName** è impostata su **value** utilizzando metaData.put(variableName, value);

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

1. Nella pagina Modifica flusso di lavoro, seleziona l’icona Variabili disponibile nella barra laterale del modello di flusso di lavoro. La sezione Variabili nel riquadro a sinistra visualizza tutte le variabili esistenti.
1. Selezionare l&#39;icona di modifica ![contrassegnata da un simbolo a forma di matita.Icona ](assets/edit.png) (Modifica) accanto al nome della variabile da modificare.
1. Modificare le informazioni sulla variabile e selezionare ![Icona Salva contrassegnata da un segno di spunta.](assets/Done_Icon.png) per salvare le modifiche. Impossibile modificare i campi **[!UICONTROL Nome]** e **[!UICONTROL Tipo]** per una variabile.

## Eliminare una variabile {#delete-a-variable}

Prima di eliminare la variabile, rimuovi tutti i riferimenti della variabile dal flusso di lavoro. Assicurati che la variabile non venga utilizzata nel flusso di lavoro.

Per eliminare una variabile:

1. Nella pagina Modifica flusso di lavoro, seleziona l’icona Variabili disponibile nella barra laterale del modello di flusso di lavoro. La sezione Variabili nel riquadro a sinistra visualizza tutte le variabili esistenti.
1. Seleziona l’icona Elimina accanto al nome della variabile da eliminare.
1. Selezionare l&#39;icona ![Fine indicata da un segno di spunta.](assets/Done_Icon.png) per confermare ed eliminare la variabile.
