---
title: Come si utilizza il servizio di esecuzione script in AEM Forms su JEE Workbench per generare dati XML?
description: Utilizzo del servizio Execute Script in AEM Forms su JEE Workbench per generare dati XML
exl-id: 2ec57cd4-f41b-4e5c-849d-88ca3d2cfe19
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: ee990092f3174a8c29443eb451d7188c1e27fa7d
workflow-type: tm+mt
source-wordcount: '1043'
ht-degree: 0%

---

# Utilizzo del servizio Execute Script in AEM Forms su JEE Workbench per generare dati XML {#using-execute-script-service-forms-jee-workbench}

I flussi di lavoro di AEM Forms per la gestione dei processi JEE contengono molti XML, ad esempio: le informazioni XML possono essere create in un processo e inviate a un&#39;applicazione Flex in AEM Forms su JEE Workspace, utilizzate per le impostazioni di sistema o per la trasmissione di informazioni da e verso i moduli. Esistono molte istanze in cui uno sviluppatore AEM Forms su JEE deve gestire XML e molte volte questo richiede che l’XML sia gestito tramite un processo AEM Forms su JEE.

Quando si utilizzano impostazioni XML semplici, è possibile utilizzare il servizio `Set Value`, che è un servizio AEM Forms su JEE predefinito. Questo servizio imposta il valore di uno o più elementi dati nel modello dati del processo. Per semplici scenari condizionali &quot;se questo, allora quello&quot;, questo servizio può soddisfare lo scopo.

Tuttavia, in situazioni più complesse, il servizio Imposta valore non è altrettanto efficace. In queste situazioni, ci si deve basare su un set più robusto di comandi di programmazione, come quelli forniti da un linguaggio di programmazione come Java™. L&#39;utilizzo di Java™ per generare XML complessi può essere molto più semplice e chiaro rispetto alla creazione di un documento XML da testo semplice all&#39;interno del servizio Set Value. Inoltre, è più facile includere la programmazione condizionale in Java™ che all’interno di un servizio Set Value.

## Utilizzo del servizio Execute Script in un processo {#using-execute-script-service-in-process}

Nel set dei servizi standard di AEM Forms su JEE disponibili in AEM Forms su JEE Workbench, è incluso il servizio `Execute Script`. Questo servizio consente di eseguire script nei processi e fornisce l&#39;operazione `executeScript` per eseguire tale operazione.

### Creare un’applicazione e un processo con il servizio &quot;Esegui script&quot; definito come attività {#create-an-application}

La creazione complessiva di applicazioni e processi non rientra nell&#39;ambito di questa esercitazione, ma ai fini di questa istruzione è stata creata un&#39;applicazione denominata &quot;DemoApplication02&quot;. Se un&#39;applicazione è già stata creata, è necessario creare un processo in questa applicazione per chiamare il servizio executeScript. Per aggiungere un processo all&#39;applicazione che include il servizio `Execute Script`:

1. Fare clic con il pulsante destro del mouse sull&#39;applicazione e selezionare **[!UICONTROL Nuovo]**. Nel menu a tendina **[!UICONTROL New]**, selezionare **[!UICONTROL Processo]**. Assegna un nome al processo, aggiungi una descrizione, se necessario, e seleziona l’icona che desideri rappresenti il processo. Ai fini di questa esercitazione, è stato creato un processo denominato `executeScriptDemoProcess`.
1. Definisci i punti iniziali o scegli di aggiungere i punti iniziali in un secondo momento.
1. Il processo è stato creato e dovrebbe essere aperto automaticamente nella finestra [!UICONTROL Progettazione processo]. In questa finestra, fare clic sull&#39;icona del selettore attività nella parte superiore della finestra Progettazione processo e trascinare la nuova attività sulla corsia di nuoto. A questo punto, dovrebbe essere visualizzata la [!UICONTROL finestra Definisci attività] (vedere la figura seguente).
   ![Definisci attività](assets/define-activity.jpg)
1. Il servizio executeScript si trova nel set di servizi `Foundation`. Il nome dei servizi elenca l&#39;oggetto come `Execute Script – 1.0` con il nome dell&#39;operazione `executeScript`. Fai clic su per selezionare questo elemento.
1. È ora necessario creare il processo e per impostazione predefinita nel riquadro a sinistra viene visualizzata la finestra [!UICONTROL Proprietà processo].

#### Aggiungere uno script al processo con il servizio &quot;Esegui script&quot; {#add-script-to-process-with-execute-script}

Una volta creato il processo con l’attività di servizio &quot;Esegui script&quot; definita, è possibile aggiungere uno script a questo processo. Per aggiungere uno script al processo:

1. Passare alla tavolozza [!UICONTROL Proprietà processo]. In questa palette, espandi la sezione [!UICONTROL Input] e fai clic sull&#39;icona &quot;...&quot;.

1. Scrivere lo script nella casella di testo visualizzata. Una volta scritto lo script, premere OK (vedere la figura seguente).
   ![Esegui script](assets/execute-script.jpg)

## Creazione di XML tramite il servizio Execute Script {#create-xml-execute-script-service}

Una volta creato un processo con il servizio Execute Script incluso, è possibile utilizzare questo script per creare XML. Gli script descritti di seguito vengono scritti nella casella di testo descritta nella sezione precedente Aggiungere uno script al processo con il servizio `Execute Script`.

>[!NOTE]
>
> Se il codice dello script JAVA supera le 10 righe, si consiglia di aggiungerlo ai DSC (Document Service Components) personalizzati anziché scriverlo direttamente nel processo. Le DSC personalizzate migliorano la manutenibilità, la riutilizzabilità e le prestazioni mantenendo leggeri i flussi di lavoro. Il riferimento a questi componenti nei flussi di lavoro garantisce una migliore efficienza di esecuzione e impedisce potenziali rallentamenti dovuti all’elaborazione di blocchi di codice di grandi dimensioni all’interno del flusso di lavoro.

**Informazioni sulla tecnologia del servizio Execute Script**

Per sapere quali sono le capacità e le limitazioni del servizio Execute Script, è necessario conoscere le basi tecnologiche del servizio. AEM Forms su JEE utilizza il parser DOM (Document Object Model) di Apache Xerces per creare e memorizzare variabili XML all’interno dei processi. Xerces è un&#39;implementazione Java™ della specifica [Document Object Model](https://dom.spec.whatwg.org/) di W3C. La specifica DOM è un metodo standard per la manipolazione di XML che esiste dal 1998. L&#39;implementazione Java™ di Xerces, Xerces-J, supporta il livello DOM 2 versione 1.0.

Le classi Java™ utilizzate per memorizzare le variabili XML sono:

* org.apache.xerces.dom.NodeImpl e

* org.apache.xerces.dom.DocumentImpl

DocumentImpl è una sottoclasse di NodeImpl, quindi si può supporre che qualsiasi variabile di processo XML sia una derivazione di NodeImpl. Per ulteriori dettagli, consulta la documentazione di [NodeImpl](https://xerces.apache.org/xerces-j/apiDocs/org/apache/xerces/dom/NodeImpl.html).

**Creazione XML di esempio tramite il servizio Execute Script**

Di seguito è riportato un esempio di creazione di XML all&#39;interno di un servizio Execute Script. Il processo ha un nodo variabile di tipo XML. Il risultato di questa attività è un documento XML. Le funzioni del documento o le modalità di applicazione al processo generale non rientrano nell&#39;ambito di questa esercitazione; in ultima analisi, dipende da cosa è necessario fare il codice XML nell&#39;applicazione generale. Come accennato nell’introduzione, XML può essere utilizzato per molti scopi in AEM Forms su moduli e processi JEE. Si tratta semplicemente di una spiegazione di come codificare l’attività Esegui script per generare un semplice documento XML.

Un JavaScript semplice per l&#39;output XML avrà un aspetto simile al seguente:

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
>Gli oggetti DOM precedentemente menzionati devono essere importati nello script.

Il risultato di questo script semplice è un nuovo documento XML con un nodo variabile impostato su:

```xml
<resources>

<resource id="first item id" value="first item value"/>

</resources>
```

**Utilizzo di un ciclo iterativo per aggiungere nodi all&#39;XML**

I nodi possono essere aggiunti anche a una variabile XML esistente all’interno del processo. La variabile, node, contiene l&#39;oggetto XML creato.

```xml
Document document = patExecContext.getProcessDataValue("/process_data/node");

NodeList childNodes = document.getChildNodes();

int numChildren = childNodes.getLength();

for (int i = 0; i < numChildren; i++)

{

Node currentChild = childNodes.item(i);

if (currentChild.getNodeType() == Node.ELEMENT_NODE)

{

// found the top-level node

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
