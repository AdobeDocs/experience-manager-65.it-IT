---
title: Come utilizzare il servizio di script eseguito in AEM Forms su JEE Workbench per generare dati XML?
description: Utilizzo del servizio di script execute in AEM Forms su JEE Workbench per creare dati XML
exl-id: 2ec57cd4-f41b-4e5c-849d-88ca3d2cfe19
source-git-commit: 37d2c70bff770d13b8094c5959e488f5531aef55
workflow-type: tm+mt
source-wordcount: '1003'
ht-degree: 0%

---

# Utilizzo del servizio di script execute in AEM Forms su JEE Workbench per creare dati XML {#using-execute-script-service-forms-jee-workbench}

C&#39;è molto XML coinvolto con AEM Forms sui flussi di lavoro JEE Process Management, ad esempio: Le informazioni XML possono essere create in un processo e inviate a un’applicazione Flex in AEM Forms su JEE Workspace, utilizzate per le impostazioni di sistema o per passare informazioni da e verso i moduli. Ci sono molte istanze in cui uno sviluppatore AEM Forms su JEE deve gestire XML e molte volte questo richiede che il XML sia gestito tramite un processo AEM Forms su JEE.

Quando si utilizzano impostazioni XML semplici, è possibile utilizzare il `Set Value` , che è un servizio AEM Forms predefinito su JEE. Questo servizio imposta il valore di uno o più elementi dati nel modello dati del processo. Per una logica condizionale molto semplice &quot;se questo, allora quello&quot; scenari, questo servizio può soddisfare lo scopo.

Tuttavia, in situazioni più complesse, il servizio Imposta valore non è altrettanto efficace. In queste situazioni, è necessario affidarsi a un set più solido di comandi di programmazione, come quelli forniti da un linguaggio di programmazione come Java. L&#39;utilizzo di Java per creare XML complessi può essere molto più semplice e chiaro rispetto alla creazione di un documento XML da testo semplice all&#39;interno del servizio Imposta valore. Inoltre, è più facile includere la programmazione condizionale in Java che all’interno di un servizio Set Value.

## Utilizzo del servizio Esegui script in un processo {#using-execute-script-service-in-process}

All’interno dell’insieme dei servizi AEM Forms standard su JEE disponibili in AEM Forms su JEE Workbench, è la variabile `Execute Script` servizio. Questo servizio consente di eseguire script nei processi e fornisce `executeScript` per farlo.

### Creare un&#39;applicazione e un processo con il servizio &quot;Esegui script&quot; definito come attività {#create-an-application}

La creazione complessiva di applicazioni e processi non rientra nell’ambito di applicazione di questa esercitazione, ma per questo motivo è stata creata un’applicazione denominata &quot;DemoApplication02&quot;. Presupponendo che un&#39;applicazione sia già stata creata, è necessario creare un processo in questa applicazione per chiamare il servizio executeScript. Per aggiungere all&#39;applicazione un processo che include `Execute Script` servizio:

1. Fai clic con il pulsante destro del mouse sull&#39;applicazione e seleziona [!UICONTROL Nuovo]. In [!UICONTROL Nuovo] menu a tendina, selezionare [!UICONTROL Processo]. Assegna un nome al processo di conseguenza, aggiungi una descrizione se necessario e seleziona l&#39;icona che desideri rappresentare il processo. Ai fini di questa esercitazione, è stato creato un processo e denominato tale processo come  `executeScriptDemoProcess`.
1. Definisci i punti di inizio o la scelta semplice per aggiungere i punti di inizio in un secondo momento.
1. Il processo viene ora creato e deve essere aperto automaticamente nel [!UICONTROL Progettazione dei processi] finestra. In questa finestra, fai clic sull’icona Selettore attività nella parte superiore della finestra Progettazione processi e trascina la nuova attività sulla corsia a nuoto. A questo punto, il [!UICONTROL Finestra Definisci attività] (vedere la figura seguente).
   ![Definisci attività](assets/define-activity.jpg)
1. Il servizio executeScript si trova in `Foundation` insieme di servizi. Il nome Servizi elenca l’oggetto come `Execute Script – 1.0` con il nome dell&#39;operazione `executeScript`. Fare clic per selezionare l&#39;elemento.
1. Questo processo deve essere creato e, per impostazione predefinita, il [!UICONTROL Proprietà processo] nel riquadro a sinistra.

#### Aggiungi uno script al processo con il servizio &quot;Esegui script&quot; {#add-script-to-process-with-execute-script}

Una volta creato il processo con l’attività &quot;Esegui script&quot; definita, è possibile aggiungere uno script a questo processo. Per aggiungere uno script a questo processo:

1. Passa a [!UICONTROL Proprietà processo] tavolozza. All’interno di questa palette, espandi la [!UICONTROL Ingresso] e fai clic sull&#39;icona &quot;...&quot;.

1. Nella casella di testo che appare scrivere lo script. Quando lo script è stato scritto, premere OK (vedi Figura qui sotto).
   ![Esegui script](assets/execute-script.jpg)

## Creazione di XML tramite il servizio Esegui script {#create-xml-execute-script-service}

Una volta creato un processo con il servizio Esegui script incluso, è possibile utilizzare questo script per creare XML. Uno scriverebbe gli script descritti di seguito nella casella di testo descritta in Aggiungi uno script al processo con il `Execute Script` Sezione servizio precedente.

**Informazioni sulla tecnologia di Execute Script Service**

Per sapere quali sono le capacità e i limiti del servizio Execute Script, è necessario conoscere i fondamenti tecnologici del servizio. AEM Forms su JEE utilizza il parser DOM (Document Object Model) di Apache Xerces per creare e memorizzare variabili XML all&#39;interno dei processi. Xerces è un’implementazione Java delle specifiche del modello di oggetto documento di W3C; definizione [qui](https://dom.spec.whatwg.org/). La specifica DOM è un modo standard di manipolare XML esistente dal 1998. L&#39;implementazione Java di Xerces, Xerces-J, supporta la versione 1.0 di DOM Level 2.

Le classi Java utilizzate per memorizzare le variabili XML sono le seguenti:

* org.apache.xerces.dom.NodeImpl e

* org.apache.xerces.dom.DocumentImpl

DocumentImpl è una sottoclasse di NodeImpl, quindi si può supporre che qualsiasi variabile di processo XML sia una derivazione NodeImpl. È possibile trovare la documentazione per NodeImpl [qui](https://xerces.apache.org/xerces-j/apiDocs/org/apache/xerces/dom/NodeImpl.html).

**Creazione XML di esempio utilizzando il servizio Esegui script**

Esempio di creazione di XML all&#39;interno di un servizio Execute Script. Il processo ha una variabile, un nodo, di tipo XML. Il risultato finale di questa attività sarà un documento XML. L&#39;attività di quel documento o il modo in cui viene applicato al processo generale non rientrano nell&#39;ambito di questa esercitazione; alla fine, si riduce a ciò che il codice XML deve fare nell&#39;applicazione complessiva. Come accennato nell’introduzione, XML può essere utilizzato per molti scopi in AEM Forms su moduli e processi JEE, si tratta semplicemente di una spiegazione di come codificare l’attività Esegui script per generare un semplice documento XML.

Un semplice script Java per l&#39;output di un file XML ha un aspetto simile al seguente:

```xml
import org.apache.xerces.dom.DocumentImpl;

import org.w3c.dom.Document;

import org.w3c.dom.Element;



Document document = new DocumentImpl();

Element topLevelResources = document.createElement("resources");

Element resource = document.createElement("resource");

resource.setAttribute("id", "first item id");

resource.setAttribute("value", "first item value");

topLevelResources.appendChild(resource);

document.appendChild(topLevelResources);

patExecContext.setProcessDataValue("/process_data/node", document);
```

>[!NOTE]
>
>che gli oggetti DOM di cui sopra devono essere importati nello script.

Il risultato di questo semplice script è un nuovo documento XML con un nodo variabile impostato su:

```xml
<resources>

<resource id="first item id" value="first item value"/>

</resources>
```

**Utilizzo di un ciclo iterativo per aggiungere nodi al codice XML**

I nodi possono essere aggiunti anche a una variabile XML esistente all&#39;interno del processo. La variabile, node, contiene l’oggetto XML appena creato.

```xml
Document document = patExecContext.getProcessDataValue("/process_data/node");

NodeList childNodes = document.getChildNodes();

int numChildren = childNodes.getLength();

for (int i = 0; i < numChildren; i++)

{

Node currentChild = childNodes.item(i);

if (currentChild.getNodeType() == Node.ELEMENT_NODE)

{

// found the top level node

Element newResource = document.createElement("resource");

newResource.setAttribute("id", "second item id");

newResource.setAttribute("value", "second item value");

currentChild.appendChild(newResource);

break;

}

}

patExecContext.setProcessDataValue("/process_data/node", document);
The variable node in the XML is now set to:

<resources> 

<resource id="first item id" value="first item value"/> 

<resource id="second item id" value="second item value"/> 

</resources>
```
