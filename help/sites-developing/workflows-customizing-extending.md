---
title: Estensione della funzionalità del flusso di lavoro
seo-title: Estensione della funzionalità del flusso di lavoro
description: 'null'
seo-description: 'null'
uuid: 9f4ea2a8-8b21-4e7c-ac73-dd37d9ada111
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: f23408c3-6b37-4047-9cce-0cab97bb6c5c
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379

---


# Estensione della funzionalità del flusso di lavoro{#extending-workflow-functionality}

In questo argomento viene descritto come sviluppare componenti passo personalizzati per i flussi di lavoro e come interagire in modo programmatico con i flussi di lavoro.

La creazione di un passaggio di workflow personalizzato include le attività seguenti:

* Sviluppare il componente fase del flusso di lavoro.
* Implementate la funzionalità step come servizio OSGi o script ECMA.

È inoltre possibile [interagire con i flussi di lavoro da programmi e script](/help/sites-developing/workflows-program-interaction.md).

## Componenti per passaggi di workflow - Nozioni di base {#workflow-step-components-the-basics}

Un componente passo del flusso di lavoro definisce l’aspetto e il comportamento del passaggio durante la creazione di modelli di workflow:

* La categoria e il nome del passaggio nella barra laterale del flusso di lavoro.
* Aspetto del passaggio nei modelli di workflow.
* Finestra di dialogo di modifica per la configurazione delle proprietà del componente.
* Il servizio o lo script eseguito in fase di esecuzione.

Come per [tutti i componenti](/help/sites-developing/components.md), i componenti dei passaggi del flusso di lavoro ereditano dal componente specificato per la `sling:resourceSuperType` proprietà. Il diagramma seguente mostra la gerarchia di `cq:component` nodi che costituiscono la base di tutti i componenti dei passaggi del flusso di lavoro. Il diagramma include anche i componenti Passo **** processo, Passaggio **** partecipante e Passaggio **partecipante** dinamico, in quanto questi sono i punti di partenza più comuni (e di base) per lo sviluppo di componenti passo personalizzati.

![aem_wf_componentsinherit](assets/aem_wf_componentinherit.png)

>[!CAUTION]
>
>Non ***devi*** cambiare nulla nel `/libs` percorso.
>
>Questo perché il contenuto di `/libs` viene sovrascritto al successivo aggiornamento dell’istanza (e potrebbe essere sovrascritto quando si applica un hotfix o un feature pack).
>
>Il metodo consigliato per la configurazione e altre modifiche è:
>
>1. Ricreare l&#39;elemento richiesto (ovvero come esiste in `/libs``/apps`
>2. Apportare modifiche all&#39;interno `/apps`


Il `/libs/cq/workflow/components/model/step` componente è l’antenato comune più vicino del passo **del** processo, del passo **** partecipante e del passo **partecipante** dinamico, che ereditano tutti i seguenti elementi:

* `step.jsp`

   Lo `step.jsp` script esegue il rendering del titolo del componente passo quando viene aggiunto a un modello.

   ![wf-22-1](assets/wf-22-1.png)

* [cq:dialog](/help/sites-developing/developing-components.md#creating-and-configuring-a-dialog)

   Una finestra di dialogo con le seguenti schede:

   * **Comune**: per modificare il titolo e la descrizione.
   * **Avanzate**: per modificare le proprietà delle notifiche e-mail.
   ![wf-44](assets/wf-44.png) ![wf-45](assets/wf-45.png)

   >[!NOTE]
   >
   >Quando le schede della finestra di dialogo di modifica di un componente passo non corrispondono a questo aspetto predefinito, il componente passo dispone di script definiti, proprietà del nodo o schede di dialogo che ignorano queste schede ereditate.

### Script ECMA {#ecma-scripts}

I seguenti oggetti sono disponibili (a seconda del tipo di passaggio) negli script ECMA:

* [WorkItem](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/workflow/exec/WorkItem.html) workItem
* [WorkflowSession](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/workflow/WorkflowSession.html) WorkflowSession
* [WorkflowData](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/workflow/exec/WorkflowData.html) WorkflowData
* `args`: con gli argomenti di processo.

* `sling`: per accedere ad altri servizi OSGI.
* `jcrSession`

### MetaDataMaps {#metadatamaps}

Potete utilizzare i metadati del flusso di lavoro per mantenere le informazioni necessarie per tutta la durata del flusso di lavoro. Un requisito comune dei passaggi del flusso di lavoro consiste nel mantenere i dati per un utilizzo futuro nel flusso di lavoro o nel recuperare i dati persistenti.

Esistono tre tipi di oggetti MetaDataMap: `Workflow`, `WorkflowData` e `WorkItem` oggetti. Hanno tutti lo stesso scopo, ovvero memorizzare i metadati.

Un oggetto WorkItem ha una propria MetaDataMap che può essere utilizzata solo mentre l&#39;elemento di lavoro (ad es. step) è in esecuzione.

Sia `Workflow` che `WorkflowData` i metadati vengono condivisi nell’intero flusso di lavoro. In questi casi, si consiglia di usare solo la mappa di `WorkflowData` metadati.

## Creazione di componenti personalizzati per i passaggi del flusso di lavoro {#creating-custom-workflow-step-components}

I componenti della fase del flusso di lavoro possono essere [creati allo stesso modo di qualsiasi altro componente](/help/sites-developing/components.md).

Per ereditare da uno dei componenti del passo di base (esistenti), aggiungere al `cq:Component` nodo la seguente proprietà:

* Nome: `sling:resourceSuperType`
* Tipo: `String`
* Valore: Uno dei seguenti percorsi che si risolve in un componente base:

   * `cq/workflow/components/model/process`
   * `cq/workflow/components/model/participant`
   * `cq/workflow/components/model/dynamic_participant`

### Specifica del titolo e della descrizione predefiniti per le istanze dei passaggi {#specifying-the-default-title-and-description-for-step-instances}

Utilizzare la procedura seguente per specificare i valori predefiniti per i campi **Titolo** e **Descrizione** della scheda **Comune** .

>[!NOTE]
>
>I valori dei campi vengono visualizzati nell&#39;istanza del passaggio quando sono soddisfatti entrambi i seguenti requisiti:
>
>* La finestra di dialogo di modifica del passaggio memorizza il titolo e la descrizione nelle seguenti posizioni: >
>* `./jcr:title`
>* `./jcr:description` location
>
>  
Questo requisito è soddisfatto quando la finestra di dialogo di modifica utilizza la scheda Comune implementata dal `/libs/cq/flow/components/step/step` componente.
>
>* Il componente step o un predecessore del componente non ignora lo `step.jsp` script implementato dal `/libs/cq/flow/components/step/step` componente.


1. Sotto il `cq:Component` nodo, aggiungi il seguente nodo:

   * Nome: `cq:editConfig`
   * Tipo: `cq:EditConfig`
   >[!NOTE]
   >
   >Per ulteriori informazioni sul nodo cq:editConfig, vedere [Configurazione del comportamento di modifica di un componente](/help/sites-developing/developing-components.md#configuring-the-edit-behavior).

1. Sotto il `cq:EditConfig` nodo, aggiungi il seguente nodo:

   * Nome: `cq:formParameters`
   * Tipo: `nt:unstructured`

1. Aggiungi `String` proprietà dei seguenti nomi al `cq:formParameters` nodo:

   * `jcr:title`: Il valore riempie il campo **Titolo** della scheda **Comune** .
   * `jcr:description`: Il valore riempie il campo **Descrizione** della scheda **Comune** .

### Salvataggio dei valori delle proprietà nei metadati del flusso di lavoro {#saving-property-values-in-workflow-metadata}

>[!NOTE]
>
>Vedere [Persistenza e accesso ai dati](#persisting-and-accessing-data). In particolare, per informazioni sull&#39;accesso al valore della proprietà in fase di esecuzione, vedere [Accesso ai valori delle proprietà finestra di dialogo in fase di esecuzione](#accessing-dialog-property-values-at-runtime).

La proprietà name di `cq:Widget` items specifica il nodo JCR che memorizza il valore del widget. Quando i widget nella finestra di dialogo dei componenti del passaggio del flusso di lavoro memorizzano i valori sotto il `./metaData` nodo, il valore viene aggiunto al flusso di lavoro `MetaDataMap`.

Ad esempio, un campo di testo in una finestra di dialogo è un `cq:Widget` nodo con le seguenti proprietà:

| Nome | Tipo | Valore |
|---|---|---|
| `xtype` | `String` | `textarea` |
| `name` | `String` | `./metaData/subject` |
| `fieldLabel` | `String` | `Email Subject` |

Il valore specificato in questo campo di testo viene aggiunto all&#39; ` [MetaDataMap](#metadatamaps)` oggetto dell&#39;istanza del flusso di lavoro ed è associato alla `subject` chiave.

>[!NOTE]
>
>Quando la chiave è `PROCESS_ARGS`, il valore è prontamente disponibile nelle implementazioni di script ECMA tramite la `args` variabile. In questo caso, il valore della proprietà name è `./metaData/PROCESS_ARGS.`

### Sostituzione dell’implementazione passo {#overriding-the-step-implementation}

Ciascun componente passo di base consente agli sviluppatori di modelli di flusso di lavoro di configurare le seguenti funzionalità principali in fase di progettazione:

* Passaggio processo: Il servizio o lo script ECMA da eseguire in fase di esecuzione.
* Passaggio partecipante: ID dell’utente a cui è assegnato l’elemento di lavoro generato.
* Passaggio partecipante dinamico: Il servizio o lo script ECMA che seleziona l&#39;ID dell&#39;utente a cui è assegnato l&#39;elemento di lavoro.

Per attivare il componente per l’utilizzo in uno scenario di flusso di lavoro specifico, configurate la funzione chiave nella progettazione e rimuovete la possibilità per gli sviluppatori di modelli di modificarla.

1. Sotto il nodo cq:component, aggiungi il seguente nodo:

   * Nome: `cq:editConfig`
   * Tipo: `cq:EditConfig`
   Per ulteriori informazioni sul nodo cq:editConfig, vedere [Configurazione del comportamento di modifica di un componente](/help/sites-developing/developing-components.md#configuring-the-edit-behavior).

1. Sotto il nodo cq:EditConfig, aggiungi il seguente nodo:

   * Nome: `cq:formParameters`
   * Tipo: `nt:unstructured`

1. Aggiungere una `String` proprietà al `cq:formParameters` nodo. Il super type del componente determina il nome della proprietà:

   * Passaggio processo: `PROCESS`
   * Passaggio partecipante: `PARTICIPANT`
   * Passaggio partecipante dinamico: `DYNAMIC_PARTICIPANT`

1. Specificare il valore della proprietà:

   * `PROCESS`: Percorso dello script ECMA o del PID del servizio che implementa il comportamento del passaggio.
   * `PARTICIPANT`: ID dell’utente a cui è assegnato l’elemento di lavoro.
   * `DYNAMIC_PARTICIPANT`: Percorso dello script ECMA o del PID del servizio che seleziona l&#39;utente per assegnare l&#39;elemento di lavoro.

1. Per rimuovere la capacità degli sviluppatori di modelli di modificare i valori delle proprietà, ignorare la finestra di dialogo del super type del componente.

### Aggiunta di moduli e finestre di dialogo ai passi dei partecipanti {#adding-forms-and-dialogs-to-participant-steps}

Personalizzate il componente passo partecipante per fornire le funzioni disponibili nei componenti Passo [partecipante](/help/sites-developing/workflows-step-ref.md#form-participant-step) modulo e Passaggio [partecipante](/help/sites-developing/workflows-step-ref.md#dialog-participant-step) finestra di dialogo:

* Presentare un modulo all&#39;utente quando apre l&#39;elemento di lavoro generato.
* Presentare all&#39;utente una finestra di dialogo personalizzata al completamento dell&#39;elemento di lavoro generato.

Per informazioni sul nuovo componente, effettuate le seguenti operazioni (consultate [Creazione di componenti](#creating-custom-workflow-step-components)personalizzati per i passaggi del flusso di lavoro):

1. Sotto il `cq:Component` nodo, aggiungi il seguente nodo:

   * Nome: `cq:editConfig`
   * Tipo: `cq:EditConfig`
   Per ulteriori informazioni sul nodo cq:editConfig, vedere [Configurazione del comportamento di modifica di un componente](/help/sites-developing/components-basics.md#edit-behavior).

1. Sotto il nodo cq:EditConfig, aggiungi il seguente nodo:

   * Nome: `cq:formParameters`
   * Tipo: `nt:unstructured`

1. Per presentare un modulo quando l&#39;utente apre l&#39;elemento di lavoro, aggiungere al `cq:formParameters` nodo la seguente proprietà:

   * Nome: `FORM_PATH`
   * Tipo: `String`
   * Valore: Percorso che risolve al modulo

1. Per visualizzare una finestra di dialogo personalizzata quando l&#39;utente completa l&#39;elemento di lavoro, aggiungere la seguente proprietà al `cq:formParameters` nodo

   * Nome: `DIALOG_PATH`
   * Tipo: `String`
   * Valore: Percorso che risolve la finestra di dialogo

### Configurazione del comportamento di Workflow Step Runtime {#configuring-the-workflow-step-runtime-behavior}

Sotto il `cq:Component` nodo, aggiungere un `cq:EditConfig` nodo. Sotto a cui si aggiunge un `nt:unstructured` `cq:formParameters`nodo (da assegnare al nodo) e a tale nodo si aggiungono le seguenti proprietà:

* Nome: `PROCESS_AUTO_ADVANCE`

   * Tipo: `Boolean`
   * Valore:

      * se impostato sul flusso di lavoro, `true` il passaggio viene eseguito e continua. Questa operazione è predefinita e consigliata
      * quando `false`il flusso di lavoro viene eseguito e interrotto; questo richiede una maggiore manutenzione, quindi `true` è consigliato

* Nome: `DO_NOTIFY`

   * Tipo: `Boolean`
   * Valore: indica se le notifiche e-mail devono essere inviate per i passaggi di partecipazione degli utenti (e presuppone che il server di posta elettronica sia configurato correttamente)

## Persistenza e accesso ai dati {#persisting-and-accessing-data}

### Dati persistenti per i passaggi successivi del flusso di lavoro {#persisting-data-for-subsequent-workflow-steps}

Potete utilizzare i metadati del flusso di lavoro per mantenere le informazioni necessarie per tutta la durata del flusso di lavoro, nonché per passare da un passaggio all’altro. Un requisito comune dei passaggi del flusso di lavoro consiste nel mantenere i dati per un utilizzo futuro o nel recuperare i dati persistenti dai passaggi precedenti.

I metadati del flusso di lavoro vengono memorizzati in un [`MetaDataMap`](#metadatamaps) oggetto. L&#39;API Java fornisce il [`Workflow.getWorkflowData`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/exec/Workflow.html) metodo per restituire un [`WorkflowData`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/exec/WorkflowData.html) oggetto che fornisce l&#39; `MetaDataMap` oggetto appropriato. Questo `WorkflowData` `MetaDataMap` oggetto è disponibile per il servizio OSGi o lo script ECMA di un componente step.

#### Java {#java}

Il metodo execute dell&#39; `WorkflowProcess` implementazione viene passato all&#39; `WorkItem` oggetto. Utilizzare questo oggetto per ottenere l&#39; `WorkflowData` oggetto per l&#39;istanza del flusso di lavoro corrente. Nell&#39;esempio seguente viene aggiunto un elemento all&#39; `MetaDataMap` oggetto workflow, quindi ogni elemento viene registrato. L’elemento (&quot;mykey&quot;, &quot;My Step Value&quot;) è disponibile per i passaggi successivi del flusso di lavoro.

```java
public void execute(WorkItem item, WorkflowSession session, MetaDataMap args) throws WorkflowException {

    MetaDataMap wfd = item.getWorkflow().getWorkflowData().getMetaDataMap();

    wfd.put("mykey", "My Step Value");

    Set<String> keyset = wfd.keySet();
    Iterator<String> i = keyset.iterator();
    while (i.hasNext()){
     Object key = i.next();
     log.info("The workflow medata includes key {} and value {}",key.toString(),wfd.get(key).toString());
    }
}
```

#### Script ECMA {#ecma-script}

La `graniteWorkItem` variabile è la rappresentazione script ECMA dell&#39;oggetto `WorkItem` Java corrente. Pertanto, potete utilizzare la `graniteWorkItem` variabile per ottenere i metadati del flusso di lavoro. Il seguente script ECMA può essere utilizzato per implementare un passo **** processo per aggiungere un elemento all&#39; `MetaDataMap` oggetto del flusso di lavoro e quindi registrare ogni elemento. Questi elementi sono quindi disponibili per i passaggi successivi del flusso di lavoro.

>[!NOTE]
>
>La `metaData` variabile immediatamente disponibile per lo script step è costituita dai metadati del passaggio. I metadati del passaggio sono diversi dai metadati del flusso di lavoro.

```
var currentDateInMillis = new Date().getTime();

graniteWorkItem.getWorkflowData().getMetaDataMap().put("hardcodedKey","theKey");

graniteWorkItem.getWorkflowData().getMetaDataMap().put("currentDateInMillisKey",currentDateInMillis);

var iterator = graniteWorkItem.getWorkflowData().getMetaDataMap().keySet().iterator();
while (iterator.hasNext()){
    var key = iterator.next();
    log.info("Workflow metadata key, value = " + key.toString() + ", " + graniteWorkItem.getWorkflowData().getMetaDataMap().get(key));
}
```

### Accesso ai valori delle proprietà finestra di dialogo in fase di esecuzione {#accessing-dialog-property-values-at-runtime}

L&#39; `MetaDataMap` oggetto delle istanze del flusso di lavoro è utile per memorizzare e recuperare i dati per tutta la durata del flusso di lavoro. Per le implementazioni dei componenti del passaggio del flusso di lavoro, l’icona `MetaDataMap` è particolarmente utile per recuperare i valori delle proprietà dei componenti in fase di esecuzione.

>[!NOTE]
>
>Per informazioni sulla configurazione della finestra di dialogo del componente per memorizzare le proprietà come metadati del flusso di lavoro, consultate [Salvataggio dei valori delle proprietà nei metadati](#saving-property-values-in-workflow-metadata)del flusso di lavoro.

Il flusso di lavoro `MetaDataMap` è disponibile per le implementazioni di processi script Java ed ECMA:

* Nelle implementazioni Java dell&#39;interfaccia WorkflowProcess, il `args` parametro è l&#39; `MetaDataMap` oggetto del flusso di lavoro.

* Nelle implementazioni di script ECMA, il valore è disponibile utilizzando le `args` variabili e `metadata` .

### Esempio: Recupero degli argomenti del componente Passo processo {#example-retrieving-the-arguments-of-the-process-step-component}

La finestra di dialogo di modifica del componente Passo **** processo include la proprietà **Argomenti** . Il valore della proprietà **Arguments** viene memorizzato nei metadati del flusso di lavoro ed è associato alla `PROCESS_ARGS` chiave.

Nel diagramma seguente, il valore della proprietà **Arguments** è `argument1, argument2`:

![wf-24](assets/wf-24.png)

#### Java {#java-1}

Il seguente codice Java è il `execute` metodo per un&#39; `WorkflowProcess` implementazione. Il metodo registra il valore nel `args` file `MetaDataMap` associato alla `PROCESS_ARGS` chiave.

```java
public void execute(WorkItem item, WorkflowSession session, MetaDataMap args) throws WorkflowException {
     if (args.containsKey("PROCESS_ARGS")){
      log.info("workflow metadata for key PROCESS_ARGS and value {}",args.get("PROCESS_ARGS","string").toString());
     }
    }
```

Quando viene eseguita una fase di processo che utilizza questa implementazione Java, il registro contiene la voce seguente:

```xml
16.02.2018 12:07:39.566 *INFO* [JobHandler: /var/workflow/instances/server0/2018-02-16/model_855140139900189:/content/we-retail/de] com.adobe.example.workflow.impl.process.LogArguments workflow metadata for key PROCESS_ARGS and value argument1, argument2
```

#### Script ECMA {#ecma-script-1}

Il seguente script ECMA viene utilizzato come processo per il passo **di** processo. Vengono registrati il numero di argomenti e i valori degli argomenti:

```
var iterator = graniteWorkItem.getWorkflowData().getMetaDataMap().keySet().iterator();
while (iterator.hasNext()){
    var key = iterator.next();
    log.info("Workflow metadata key, value = " + key.toString() + ", " + graniteWorkItem.getWorkflowData().getMetaDataMap().get(key));
}
log.info("hardcodedKey "+ graniteWorkItem.getWorkflowData().getMetaDataMap().get("hardcodedKey"));
log.info("currentDateInMillisKey "+ graniteWorkItem.getWorkflowData().getMetaDataMap().get("currentDateInMillisKey"));
```

>[!NOTE]
>
>Questa sezione descrive come utilizzare gli argomenti per i passaggi del processo. Le informazioni si applicano anche ai selettori dei partecipanti dinamici.

>[!NOTE]
>Per un altro esempio di memorizzazione delle proprietà dei componenti nei metadati del flusso di lavoro, consultate Esempio: Crea un passaggio del flusso di lavoro del logger. In questo esempio è disponibile una finestra di dialogo che consente di associare il valore dei metadati a una chiave diversa da PROCESS_ARGS.

### Script e argomenti di processo {#scripts-and-process-arguments}

All&#39;interno di uno script per un componente Passo **** processo, gli argomenti sono disponibili tramite l&#39; `args` oggetto.

Quando si crea un componente passo personalizzato, l&#39;oggetto `metaData` è disponibile in uno script. Questo oggetto è limitato a un singolo argomento stringa.

## Sviluppo di implementazioni delle fasi del processo {#developing-process-step-implementations}

Quando i passaggi del processo vengono avviati durante il processo di un flusso di lavoro, i passaggi inviano una richiesta a un servizio OSGi o eseguono uno script ECMA. Sviluppare il servizio o lo script ECMA che esegue le azioni necessarie per il flusso di lavoro.

>[!NOTE]
>
>Per informazioni sull&#39;associazione del componente Passaggio processo al servizio o allo script, vedere Passaggio [](/help/sites-developing/workflows-step-ref.md#process-step) processo o [Sostituzione dell&#39;implementazione](#overriding-the-step-implementation)passo.

### Implementazione di un passaggio di processo con una classe Java {#implementing-a-process-step-with-a-java-class}

Per definire un processo come componente di servizio OSGI (bundle Java):

1. Create il bundle e distribuitelo nel contenitore OSGI. Consultate la documentazione sulla creazione di un bundle con [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md) o [Eclipse](/help/sites-developing/howto-projects-eclipse.md).

   >[!NOTE]
   >
   >Il componente OSGI deve implementare l’ `WorkflowProcess` interfaccia con il suo `execute()` metodo. Vedere l&#39;esempio di codice riportato di seguito.

   >[!NOTE]
   >
   >Il nome del pacchetto deve essere aggiunto alla `<*Private-Package*>` sezione della `maven-bundle-plugin` configurazione.

1. Aggiungere la proprietà SCR `process.label` e impostare il valore come desiderato. Questo sarà il nome con cui il passaggio del processo viene elencato quando si utilizza il componente **Processo** generico. Vedere l&#39;esempio seguente.
1. Nell’editor **Modelli** , aggiungete il passaggio del processo al flusso di lavoro utilizzando il componente Passo **** processo generico.
1. Nella finestra di dialogo di modifica (del passaggio **** Processo), andate alla scheda **Processo** e selezionate l&#39;implementazione del processo.
1. Se utilizzate gli argomenti nel codice, impostate gli argomenti relativi al **processo**. Ad esempio: false.
1. Salvate le modifiche, sia per il passaggio che per il modello di workflow (angolo in alto a sinistra dell&#39;editor modelli).

I metodi java, rispettivamente, le classi che implementano il metodo Java eseguibile sono registrate come servizi OSGI, consentendo di aggiungere metodi in qualsiasi momento durante il runtime.

Il seguente componente OSGI aggiunge la proprietà `approved` al nodo del contenuto della pagina quando il payload è una pagina:

```java
package com.adobe.example.workflow.impl.process;

import com.adobe.granite.workflow.WorkflowException;
import com.adobe.granite.workflow.WorkflowSession;
import com.adobe.granite.workflow.exec.WorkItem;
import com.adobe.granite.workflow.exec.WorkflowData;
import com.adobe.granite.workflow.exec.WorkflowProcess;
import com.adobe.granite.workflow.metadata.MetaDataMap;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Property;
import org.apache.felix.scr.annotations.Service;

import org.osgi.framework.Constants;

import javax.jcr.Node;
import javax.jcr.RepositoryException;
import javax.jcr.Session;

/**
 * Sample workflow process that sets an <code>approve</code> property to the payload based on the process argument value.
 */
@Component
@Service
public class MyProcess implements WorkflowProcess {

 @Property(value = "An example workflow process implementation.")
 static final String DESCRIPTION = Constants.SERVICE_DESCRIPTION;
 @Property(value = "Adobe")
 static final String VENDOR = Constants.SERVICE_VENDOR;
 @Property(value = "My Sample Workflow Process")
 static final String LABEL="process.label";

 private static final String TYPE_JCR_PATH = "JCR_PATH";

 public void execute(WorkItem item, WorkflowSession session, MetaDataMap args) throws WorkflowException {
  WorkflowData workflowData = item.getWorkflowData();
  if (workflowData.getPayloadType().equals(TYPE_JCR_PATH)) {
   String path = workflowData.getPayload().toString() + "/jcr:content";
   try {
    Session jcrSession = session.adaptTo(Session.class);
    Node node = (Node) jcrSession.getItem(path);
    if (node != null) {
     node.setProperty("approved", readArgument(args));
     jcrSession.save();
    }
   } catch (RepositoryException e) {
    throw new WorkflowException(e.getMessage(), e);
   }
  }
 }

 private boolean readArgument(MetaDataMap args) {
  String argument = args.get("PROCESS_ARGS", "false");
  return argument.equalsIgnoreCase("true");
 }
}
```

>[!NOTE]
>
>Se il processo ha esito negativo tre volte nella riga, un elemento viene inserito nella casella in entrata dell’amministratore del flusso di lavoro.

### Utilizzo di ECMAScript {#using-ecmascript}

Gli script ECMA consentono agli sviluppatori di script di implementare i passaggi del processo. Gli script si trovano nell&#39;archivio JCR ed sono eseguiti da tale archivio.

Nella tabella seguente sono elencate le variabili immediatamente disponibili per l&#39;elaborazione degli script, che forniscono l&#39;accesso agli oggetti dell&#39;API Java del flusso di lavoro.

| Classe Java | Nome variabile script | Descrizione |
|---|---|---|
| `com.adobe.granite.workflow.exec.WorkItem` | `graniteWorkItem` | L’istanza del passaggio corrente. |
| `com.adobe.granite.workflow.WorkflowSession` | `graniteWorkflowSession` | La sessione del flusso di lavoro dell’istanza del passaggio corrente. |
| `String[]` (contiene argomenti di processo) | `args` | Gli argomenti step. |
| `com.adobe.granite.workflow.metadata.MetaDataMap` | `metaData` | I metadati dell&#39;istanza del passaggio corrente. |
| `org.apache.sling.scripting.core.impl.InternalScriptHelper` | `sling` | Fornisce l&#39;accesso all&#39;ambiente di runtime Sling. |

Lo script di esempio seguente illustra come accedere al nodo JCR che rappresenta il payload del flusso di lavoro. La `graniteWorkflowSession` variabile viene adattata a una variabile di sessione JCR, utilizzata per ottenere il nodo dal percorso di payload.

```
var workflowData = graniteWorkItem.getWorkflowData();
if (workflowData.getPayloadType() == "JCR_PATH") {
    var path = workflowData.getPayload().toString();
    var jcrsession = graniteWorkflowSession.adaptTo(Packages.javax.jcr.Session);
    var node = jcrsession.getNode(path);
    if (node.hasProperty("approved")){
     node.setProperty("approved", args[0] == "true" ? true : false);
     node.save();
 }
}
```

Lo script seguente verifica se il payload è un&#39;immagine ( `.png` file), ne crea un&#39;immagine in bianco e nero e la salva come nodo di pari livello.

```
var workflowData = graniteWorkItem.getWorkflowData();
if (workflowData.getPayloadType() == "JCR_PATH") {
    var path = workflowData.getPayload().toString();
    var jcrsession = graniteWorkflowSession.adaptTo(Packages.javax.jcr.Session);
    var node = jcrsession.getRootNode().getNode(path.substring(1));
     if (node.isNodeType("nt:file") && node.getProperty("jcr:content/jcr:mimeType").getString().indexOf("image/") == 0) {
        var is = node.getProperty("jcr:content/jcr:data").getStream();
        var layer = new Packages.com.day.image.Layer(is);
        layer.grayscale();
                var parent = node.getParent();
                var gn = parent.addNode("grey" + node.getName(), "nt:file");
        var content = gn.addNode("jcr:content", "nt:resource");
                content.setProperty("jcr:mimeType","image/png");
                var cal = Packages.java.util.Calendar.getInstance();
                content.setProperty("jcr:lastModified",cal);
                var f = Packages.java.io.File.createTempFile("test",".png");
        var tout = new Packages.java.io.FileOutputStream(f);
        layer.write("image/png", 1.0, tout);
        var fis = new Packages.java.io.FileInputStream(f);
                content.setProperty("jcr:data", fis);
                parent.save();
        tout.close();
        fis.close();
        is.close();
        f.deleteOnExit();
    }
}
```

Per utilizzare lo script:

1. Creare lo script (ad esempio con CRXDE Lite) e salvarlo nell&#39;archivio sottostante `/apps/myapp/workflow/scripts`
1. Per specificare un titolo che identifichi lo script nella finestra di dialogo di modifica del passo **di** processo, aggiungere le seguenti proprietà al `jcr:content` nodo dello script:

   | Nome | Tipo | Valore |
   |---|---|---|
   | `jcr:mixinTypes` | `Name[]` | `mix:title` |
   | `jcr:title` | `String` | Nome da visualizzare nella finestra di dialogo di modifica. |

1. Modificare l&#39;istanza **Passo** processo e specificare lo script da utilizzare.

## Sviluppo dei partecipanti {#developing-participant-choosers}

Potete sviluppare i selettori dei partecipanti per i componenti Passo **partecipante** dinamico.

Quando un componente Passo **partecipante** dinamico viene avviato durante un flusso di lavoro, il passaggio deve determinare il partecipante al quale può essere assegnato l’elemento di lavoro generato. A questo scopo, effettuare una delle seguenti operazioni:

* invia una richiesta a un servizio OSGi
* esegue uno script ECMA per selezionare il partecipante

Potete sviluppare un servizio o uno script ECMA che selezioni il partecipante in base ai requisiti del flusso di lavoro.

>[!NOTE]
>
>Per informazioni sull’associazione del componente Passo **partecipante** dinamico al servizio o allo script, consultate Passaggio [partecipante](/help/sites-developing/workflows-step-ref.md#dynamic-participant-step) dinamico o [Sostituzione dell’implementazione](#persisting-and-accessing-data)passo.

### Sviluppo di un selettore partecipanti mediante una classe Java {#developing-a-participant-chooser-using-a-java-class}

Per definire un passaggio partecipante come componente di servizio OSGI (classe Java):

1. Il componente OSGI deve implementare l’ `ParticipantStepChooser` interfaccia con il suo `getParticipant()` metodo. Vedere l&#39;esempio di codice riportato di seguito.

   Create il bundle e distribuitelo nel contenitore OSGI.

1. Aggiungete la proprietà SCR `chooser.label` e impostate il valore come richiesto. Questo sarà il nome in cui è elencato il selettore partecipanti, utilizzando il componente Passaggio **partecipante** dinamico. Vedere l&#39;esempio:

   ```java
   package com.adobe.example.workflow.impl.process;
   
   import com.adobe.granite.workflow.WorkflowException;
   import com.adobe.granite.workflow.WorkflowSession;
   import com.adobe.granite.workflow.exec.ParticipantStepChooser;
   import com.adobe.granite.workflow.exec.WorkItem;
   import com.adobe.granite.workflow.exec.WorkflowData;
   import com.adobe.granite.workflow.metadata.MetaDataMap;
   
   import org.apache.felix.scr.annotations.Component;
   import org.apache.felix.scr.annotations.Property;
   import org.apache.felix.scr.annotations.Service;
   
   import org.osgi.framework.Constants;
   
   /**
    * Sample dynamic participant step that determines the participant based on a path given as argument.
    */
   @Component
   @Service
   
   public class MyDynamicParticipant implements ParticipantStepChooser {
   
    @Property(value = "An example implementation of a dynamic participant chooser.")
    static final String DESCRIPTION = Constants.SERVICE_DESCRIPTION;
       @Property(value = "Adobe")
       static final String VENDOR = Constants.SERVICE_VENDOR;
       @Property(value = "Dynamic Participant Chooser Process")
       static final String LABEL=ParticipantStepChooser.SERVICE_PROPERTY_LABEL;
   
       private static final String TYPE_JCR_PATH = "JCR_PATH";
   
       public String getParticipant(WorkItem workItem, WorkflowSession workflowSession, MetaDataMap args) throws WorkflowException {
           WorkflowData workflowData = workItem.getWorkflowData();
           if (workflowData.getPayloadType().equals(TYPE_JCR_PATH)) {
               String path = workflowData.getPayload().toString();
               String pathFromArgument = args.get("PROCESS_ARGS", String.class);
               if (pathFromArgument != null && path.startsWith(pathFromArgument)) {
                   return "admin";
               }
           }
           return "administrators";
       }
   }
   ```

1. Nell’editor **Modelli** , aggiungete il passaggio partecipante dinamico al flusso di lavoro utilizzando il componente Passo **partecipante** dinamico generico.
1. Nella finestra di dialogo di modifica, selezionate la scheda Selezione **partecipanti** e selezionate l’implementazione del selettore.
1. Se utilizzate gli argomenti nel codice, impostate gli argomenti relativi al **processo**. Per questo esempio: `/content/we-retail/de`.
1. Salvare le modifiche, sia per il passaggio che per il modello di workflow.

### Sviluppo di un selettore partecipanti mediante uno script ECMA {#developing-a-participant-chooser-using-an-ecma-script}

È possibile creare uno script ECMA che selezioni l&#39;utente a cui viene assegnato l&#39;elemento di lavoro generato dal Passaggio **** partecipante. Lo script deve includere una funzione denominata `getParticipant` che non richiede argomenti e restituisce `String` l&#39;ID di un utente o di un gruppo.

Gli script si trovano nell&#39;archivio JCR ed vengono eseguiti da tale archivio.

Nella tabella seguente sono elencate le variabili che forniscono accesso immediato agli oggetti Java del flusso di lavoro negli script.

| Classe Java | Nome variabile script |
|---|---|
| `com.adobe.granite.workflow.exec.WorkItem` | `graniteWorkItem` |
| `com.adobe.granite.workflow.WorkflowSession` | `graniteWorkflowSession` |
| `String[]` (contiene argomenti di processo) | `args` |
| `com.adobe.granite.workflow.metadata.MetaDataMap` | `metaData` |
| `org.apache.sling.scripting.core.impl.InternalScriptHelper` | `sling` |

```
function getParticipant() {
    var workflowData = graniteWorkItem.getWorkflowData();
    if (workflowData.getPayloadType() == "JCR_PATH") {
        var path = workflowData.getPayload().toString();
        if (path.indexOf("/content/we-retail/de") == 0) {
            return "admin";
        } else {
            return "administrators";
        }
    }
}
```

1. Creare lo script (ad esempio con CRXDE Lite) e salvarlo nell&#39;archivio sottostante `/apps/myapp/workflow/scripts`
1. Per specificare un titolo che identifichi lo script nella finestra di dialogo di modifica del passo **di** processo, aggiungere le seguenti proprietà al `jcr:content` nodo dello script:

   | Nome | Tipo | Valore |
   |---|---|---|
   | `jcr:mixinTypes` | `Name[]` | `mix:title` |
   | `jcr:title` | `String` | Nome da visualizzare nella finestra di dialogo di modifica. |

1. Modificate l&#39;istanza Passaggio [partecipante](/help/sites-developing/workflows-step-ref.md#dynamic-participant-step) dinamico e specificate lo script da utilizzare.

## Gestione dei pacchetti di flussi di lavoro {#handling-workflow-packages}

[I pacchetti](/help/sites-authoring/workflows-applying.md#specifying-workflow-details-in-the-create-workflow-wizard) di workflow possono essere passati a un flusso di lavoro per l&#39;elaborazione. I pacchetti di flussi di lavoro contengono riferimenti a risorse quali pagine e risorse.

>[!NOTE]
>
>I seguenti passaggi del processo di flusso di lavoro accettano pacchetti di flussi di lavoro per l’attivazione in massa di pagine:
>
>* [`com.day.cq.wcm.workflow.process.ActivatePageProcess`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/workflow/process/ActivatePageProcess.html)
>* [`com.day.cq.wcm.workflow.process.DeactivatePageProcess`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/workflow/process/DeactivatePageProcess.html)
>



Potete sviluppare dei passaggi per ottenere le risorse del pacchetto ed elaborarle. I seguenti membri del `com.day.cq.workflow.collection` pacchetto forniscono l&#39;accesso ai pacchetti di workflow:

* `ResourceCollection`: Classe pacchetto flusso di lavoro.
* `ResourceCollectionUtil`: Utilizzare per recuperare gli oggetti ResourceCollection.
* `ResourceCollectionManager`: Crea e recupera le raccolte. Un&#39;implementazione viene distribuita come servizio OSGi.

La seguente classe Java di esempio illustra come ottenere le risorse del pacchetto:

```java
package com.adobe.example;

import java.util.ArrayList;
import java.util.List;

import com.day.cq.workflow.WorkflowException;
import com.day.cq.workflow.WorkflowSession;
import com.day.cq.workflow.collection.ResourceCollection;
import com.day.cq.workflow.collection.ResourceCollectionManager;
import com.day.cq.workflow.collection.ResourceCollectionUtil;
import com.day.cq.workflow.exec.WorkItem;
import com.day.cq.workflow.exec.WorkflowData;
import com.day.cq.workflow.exec.WorkflowProcess;
import com.day.cq.workflow.metadata.MetaDataMap;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Property;
import org.apache.felix.scr.annotations.Service;
import org.apache.felix.scr.annotations.Reference;
import org.osgi.framework.Constants;

import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import javax.jcr.Node;
import javax.jcr.PathNotFoundException;
import javax.jcr.RepositoryException;
import javax.jcr.Session;

@Component
@Service
public class LaunchBulkActivate implements WorkflowProcess {

 private static final Logger log = LoggerFactory.getLogger(LaunchBulkActivate.class);

 @Property(value="Bulk Activate for Launches")
  static final String PROCESS_NAME ="process.label";
 @Property(value="A sample workflow process step to support Launches bulk activation of pages")
 static final String SERVICE_DESCRIPTION = Constants.SERVICE_DESCRIPTION;

 @Reference
 private ResourceCollectionManager rcManager;
public void execute(WorkItem workItem, WorkflowSession workflowSession) throws Exception {
    Session session = workflowSession.getSession();
    WorkflowData data = workItem.getWorkflowData();
    String path = null;
    String type = data.getPayloadType();
    if (type.equals(TYPE_JCR_PATH) && data.getPayload() != null) {
        String payloadData = (String) data.getPayload();
        if (session.itemExists(payloadData)) {
            path = payloadData;
        }
    } else if (data.getPayload() != null && type.equals(TYPE_JCR_UUID)) {
        Node node = session.getNodeByUUID((String) data.getPayload());
        path = node.getPath();
    }

    // CUSTOMIZED CODE IF REQUIRED....

    if (path != null) {
        // check for resource collection
        ResourceCollection rcCollection = ResourceCollectionUtil.getResourceCollection((Node)session.getItem(path), rcManager);
        // get list of paths to replicate (no resource collection: size == 1
        // otherwise size >= 1
        List<String> paths = getPaths(path, rcCollection);
        for (String aPath: paths) {

            // CUSTOMIZED CODE....

        }
    } else {
        log.warn("Cannot process because path is null for this " + "workitem: " + workItem.toString());
    }
}

/**
 * helper
 */
private List<String> getPaths(String path, ResourceCollection rcCollection) {
    List<String> paths = new ArrayList<String>();
    if (rcCollection == null) {
        paths.add(path);
    } else {
        log.debug("ResourceCollection detected " + rcCollection.getPath());
        // this is a resource collection. the collection itself is not
        // replicated. only its members
        try {
            List<Node> members = rcCollection.list(new String[]{"cq:Page", "dam:Asset"});
            for (Node member: members) {
                String mPath = member.getPath();
                paths.add(mPath);
            }
        } catch(RepositoryException re) {
            log.error("Cannot build path list out of the resource collection " + rcCollection.getPath());
        }
    }
    return paths;
}
}
```

## Esempio: Creazione di un passaggio personalizzato {#example-creating-a-custom-step}

Un modo semplice per iniziare a creare un passaggio personalizzato è quello di copiare un passaggio esistente da:

`/libs/cq/workflow/components/model`

### Creazione del passaggio di base {#creating-the-basic-step}

1. Ricreare il percorso in /apps; ad esempio:

   `/apps/cq/workflow/components/model`

   Le nuove cartelle sono di tipo `nt:folder`:

   ```xml
   - apps
     - cq
       - workflow (nt:folder)
         - components (nt:folder)
           - model (nt:folder)
   ```

   >[!NOTE]
   >
   >Questo passaggio non si applica all’editor classico per modelli di interfaccia utente.

1. Quindi inserite il passaggio copiato nella cartella /apps; ad esempio:

   `/apps/cq/workflow/components/model/myCustomStep`

   Ecco il risultato del nostro esempio personalizzato passo:

   ![wf-34](assets/wf-34.png)

   >[!CAUTION]
   >
   >Poiché nell&#39;interfaccia standard non sono visualizzati sulla scheda solo il titolo e non i dettagli, non `details.jsp` è necessario come per l&#39;editor dell&#39;interfaccia classica.

1. Applicare le seguenti proprietà al nodo:

   `/apps/cq/workflow/components/model/myCustomStep`

   **Proprietà di interesse:**

   * `sling:resourceSuperType`

      Deve ereditare da un passaggio esistente.

      In questo esempio ereditiamo dal passaggio di base in `cq/workflow/components/model/step`, ma potete utilizzare altri super tipi come `participant`, `process`, ecc.

   * `jcr:title`

      Titolo visualizzato quando il componente è elencato nel browser dei passaggi (pannello a sinistra dell’editor del modello di workflow).

   * `cq:icon`

      Utilizzato per specificare un&#39;icona [Corallo](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/coral-ui/coralui3/Coral.Icon.html) per il passaggio.

   * `componentGroup`

      Deve essere uno dei seguenti:

      * Flusso di lavoro collaborazione
      * Flusso di lavoro DAM
      * Flusso di lavoro per moduli
      * Progetti
      * Flusso di lavoro WCM
      * Flusso di lavoro
   ![wf-35](assets/wf-35.png)

1. Ora potete aprire un modello di workflow per la modifica. Nel browser dei passaggi è possibile filtrare per visualizzare il **mio passo** personalizzato:

   ![wf-36](assets/wf-36.png)

   Trascinate **il passaggio** personalizzato sul modello per visualizzare la scheda:

   ![wf-37](assets/wf-37.png)

   Se non `cq:icon` è stato definito alcun passaggio, viene visualizzata un&#39;icona predefinita utilizzando le prime due lettere del titolo. Esempio:

   ![wf-38](assets/wf-38.png)

#### Definizione della finestra di dialogo Configurazione passo {#defining-the-step-configure-dialog}

Dopo aver [creato il passaggio](#creating-the-basic-step)di base, definite la finestra di dialogo **Configura** come segue:

1. Configura le proprietà sul nodo `cq:editConfig` come segue:

   **Proprietà di interesse:**

   * `cq:inherit`

      Quando è impostato su `true`, il componente passo eredita le proprietà dal passaggio specificato in `sling:resourceSuperType`.

   * `cq:disableTargeting`

      Impostate come richiesto.
   ![wf-39](assets/wf-39.png)

1. Configura le proprietà sul nodo `cq:formsParameter` come segue:

   **Proprietà di interesse:**

   * `jcr:title`

      Imposta il titolo predefinito sulla scheda passo nella mappa del modello e nel campo **Titolo** della finestra di dialogo di configurazione **Personalizzato - Proprietà** passo.

   * È inoltre possibile definire proprietà personalizzate.
   ![wf-40](assets/wf-40.png)

1. Configurare le proprietà sul nodo `cq:listeners`.

   Il `cq:listener` nodo e le relative proprietà consentono di impostare i gestori eventi che reagiscono agli eventi nell&#39;editor modelli dell&#39;interfaccia touch; ad esempio, trascinare un passaggio su una pagina modello o modificare le proprietà di un passaggio.

   **Proprietà degli interessi:**

   * `afterMove: REFRESH_PAGE`
   * `afterdelete: CQ.workflow.flow.Step.afterDelete`
   * `afteredit: CQ.workflow.flow.Step.afterEdit`
   * `afterinsert: CQ.workflow.flow.Step.afterInsert`
   Questa configurazione è essenziale per il corretto funzionamento dell&#39;editor. Nella maggior parte dei casi questa configurazione non deve essere modificata.

   Tuttavia, l&#39;impostazione `cq:inherit` su true (sul `cq:editConfig` nodo, vedi sopra) consente di ereditare questa configurazione, senza dover includerla esplicitamente nella definizione del passaggio. Se non è presente alcuna ereditarietà, è necessario aggiungere il nodo con le proprietà e i valori seguenti.

   In questo esempio, l&#39;ereditarietà è stata attivata in modo da poter rimuovere il `cq:listeners` nodo e il passaggio continuerà a funzionare correttamente.

   ![wf-41](assets/wf-41.png)

1. Ora puoi aggiungere un&#39;istanza del passaggio a un modello di workflow. Quando si **configura** il passaggio viene visualizzata la finestra di dialogo:

   ![wf-42](assets/wf-42.png) ![wf-43](assets/wf-43.png)

#### Markup di esempio utilizzati in questo esempio {#sample-markup-used-in-this-example}

La marcatura per un passaggio personalizzato è rappresentata nel nodo principale `.content.xml` del componente. Esempio `.content.xml` utilizzato per questo esempio:

`/apps/cq/workflow/components/model/myCustomStep/.content.xml`

```xml
<?xml version="1.0" encoding="UTF-8"?>
<jcr:root xmlns:sling="https://sling.apache.org/jcr/sling/1.0" xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0"
    cq:icon="bell"
    jcr:primaryType="cq:Component"
    jcr:title="My Custom Step"
    sling:resourceSuperType="cq/workflow/components/model/process"
    allowedParents="[*/parsys]"
    componentGroup="Workflow"/>
```

L&#39; `_cq_editConfig.xml` esempio utilizzato in questo esempio:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<jcr:root xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0" xmlns:nt="https://www.jcp.org/jcr/nt/1.0"
    cq:disableTargeting="{Boolean}true"
    cq:inherit="{Boolean}true"
    jcr:primaryType="cq:EditConfig">
    <cq:formParameters
        jcr:primaryType="nt:unstructured"
        jcr:title="My Custom Step Card"
        SAMPLE_PROPERY="sample value"/>
    <cq:listeners
        jcr:primaryType="cq:EditListenersConfig"
        afterdelete="CQ.workflow.flow.Step.afterDelete"
        afteredit="CQ.workflow.flow.Step.afterEdit"
        afterinsert="CQ.workflow.flow.Step.afterInsert"
        afterMove="REFRESH_PAGE"/>
</jcr:root>
```

L&#39; `_cq_dialog/.content.xml` esempio utilizzato in questo esempio:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<jcr:root xmlns:sling="https://sling.apache.org/jcr/sling/1.0" xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0" xmlns:nt="https://www.jcp.org/jcr/nt/1.0"
    jcr:primaryType="nt:unstructured"
    jcr:title="My Custom - Step Properties"
    sling:resourceType="cq/gui/components/authoring/dialog">
    <content
        jcr:primaryType="nt:unstructured"
        sling:resourceType="granite/ui/components/coral/foundation/tabs">
        <items jcr:primaryType="nt:unstructured">
            <common
                cq:hideOnEdit="true"
                jcr:primaryType="nt:unstructured"
                jcr:title="Common"
                sling:resourceType="granite/ui/components/coral/foundation/fixedcolumns"/>
            <process
                cq:hideOnEdit="true"
                jcr:primaryType="nt:unstructured"
                jcr:title="Process"
                sling:resourceType="granite/ui/components/coral/foundation/fixedcolumns"/>
            <mycommon
                jcr:primaryType="nt:unstructured"
                jcr:title="Common"
                sling:resourceType="granite/ui/components/coral/foundation/fixedcolumns">
                <items jcr:primaryType="nt:unstructured">
                    <columns
                        jcr:primaryType="nt:unstructured"
                        sling:resourceType="granite/ui/components/coral/foundation/container">
                        <items jcr:primaryType="nt:unstructured">
                            <title
                                jcr:primaryType="nt:unstructured"
                                sling:resourceType="granite/ui/components/coral/foundation/form/textfield"
                                fieldLabel="Title"
                                name="./jcr:title"/>
                            <description
                                jcr:primaryType="nt:unstructured"
                                sling:resourceType="granite/ui/components/coral/foundation/form/textarea"
                                fieldLabel="Description"
                                name="./jcr:description"/>
                        </items>
                    </columns>
                </items>
            </mycommon>
            <advanced
                jcr:primaryType="nt:unstructured"
                jcr:title="Advanced"
                sling:resourceType="granite/ui/components/coral/foundation/fixedcolumns">
                <items jcr:primaryType="nt:unstructured">
                    <columns
                        jcr:primaryType="nt:unstructured"
                        sling:resourceType="granite/ui/components/coral/foundation/container">
                        <items jcr:primaryType="nt:unstructured">
                            <email
                                jcr:primaryType="nt:unstructured"
                                sling:resourceType="granite/ui/components/coral/foundation/form/checkbox"
                                fieldDescription="Notify user via email."
                                fieldLabel="Email"
                                name="./metaData/PROCESS_AUTO_ADVANCE"
                                text="Notify user via email."
                                value="true"/>
                        </items>
                    </columns>
                </items>
            </advanced>
        </items>
    </content>
</jcr:root>
```

>[!NOTE]
>
>Osservate i nodi comuni e di processo nella definizione della finestra di dialogo. Questi sono ereditati dalla fase di processo che abbiamo utilizzato come supertipo per il nostro passaggio personalizzato:
>
>`sling:resourceSuperType : cq/workflow/components/model/process`

>[!NOTE]
>
>Le finestre di dialogo dell’editor modelli dell’interfaccia classica continueranno a funzionare con l’editor dell’interfaccia touch standard.
>
>Anche se AEM dispone di uno strumento di conversione [della](/help/sites-developing/dialog-conversion.md) finestra di dialogo se desideri aggiornare le finestre di dialogo classiche dei passaggi dell’interfaccia utente alle finestre di dialogo standard dell’interfaccia utente. Dopo la conversione, per alcuni casi potrebbero essere apportati miglioramenti manuali al dialogo.
>
>* Nei casi in cui una finestra di dialogo aggiornata è vuota, è possibile esaminare le finestre di dialogo con funzionalità simili, come esempi di come fornire una soluzione. `/libs` Esempio:
   >
   >
* `/libs/cq/workflow/components/model`
>* `/libs/cq/workflow/components/workflow`
>* `/libs/dam/components`
>* `/libs/wcm/workflow/components/autoassign`
>* `/libs/cq/projects`
>
>  
Non è necessario modificare nulla in `/libs`, è sufficiente utilizzarli come esempi. Per sfruttare uno dei passaggi esistenti, copiateli `/apps` e modificateli.
