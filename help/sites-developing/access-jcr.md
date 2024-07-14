---
title: Come accedere a livello di programmazione al JCR per AEM
description: Puoi modificare in modo programmatico nodi e proprietà che si trovano all’interno dell’archivio AEM, che fa parte di Adobe Experience Cloud
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
exl-id: fe946b9a-b29e-4aa5-b973-e2a652417a55
solution: Experience Manager, Experience Manager Sites
feature: Developing,JCR
role: Developer
source-git-commit: 305227eff3c0d6414a5ae74bcf3a74309dccdd13
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 0%

---

# Come accedere a livello di programmazione al JCR per AEM{#how-to-programmatically-access-the-aem-jcr}

Puoi modificare in modo programmatico i nodi e le proprietà che si trovano all’interno dell’archivio Adobe CQ, che fa parte di Adobe Experience Cloud. Per accedere all’archivio CQ, utilizza l’API Java™ Content Repository (JCR). Puoi utilizzare l’API Java™ JCR per creare, sostituire, aggiornare ed eliminare (CRUD) contenuti che si trovano all’interno dell’archivio Adobe CQ. Per ulteriori informazioni sull&#39;API Java™ JCR, vedi [https://jackrabbit.apache.org/jcr/jcr-api.html](https://jackrabbit.apache.org/jcr/jcr-api.html).

>[!NOTE]
>
>Questo articolo di sviluppo modifica Adobe CQ JCR da un’applicazione Java™ esterna. Al contrario, puoi modificare il JCR dall’interno di un bundle OSGi utilizzando l’API JCR. Per ulteriori dettagli, vedere [Dati CQ persistenti nel repository dei contenuti Java™](https://helpx.adobe.com/experience-manager/using/persisting-cq-data-java-content1.html).

>[!NOTE]
>
>Per utilizzare l&#39;API JCR, aggiungi il file `jackrabbit-standalone-2.4.0.jar` al percorso della classe dell&#39;applicazione Java™. Puoi ottenere questo file JAR dalla pagina Web dell&#39;API Java™ JCR all&#39;indirizzo [https://jackrabbit.apache.org/jcr/jcr-api.html](https://jackrabbit.apache.org/jcr/jcr-api.html).

>[!NOTE]
>
>Per informazioni su come eseguire query su Adobe CQ JCR utilizzando l&#39;API di query JCR, consulta [Query dei dati Adobe Experience Manager tramite l&#39;API JCR](https://helpx.adobe.com/experience-manager/using/querying-experience-manager-data-using1.html).

## Creare un’istanza dell’archivio {#create-a-repository-instance}

Sebbene esistano diversi modi per connettersi a un repository e stabilire una connessione, questo articolo di sviluppo utilizza un metodo statico che appartiene alla classe `org.apache.jackrabbit.commons.JcrUtils`. Il nome del metodo è `getRepository`. Questo metodo accetta un parametro stringa che rappresenta l’URL del server Adobe CQ. Esempio: `http://localhost:4503/crx/server`.

Il metodo `getRepository` restituisce un&#39;istanza `Repository`, come illustrato nell&#39;esempio di codice seguente.

```java
//Create a connection to the AEM JCR repository running on local host
Repository repository = JcrUtils.getRepository("http://localhost:4503/crx/server");
```

## Creare un’istanza Session {#create-a-session-instance}

L&#39;istanza `Repository` rappresenta l&#39;archivio CRX. Utilizzare l&#39;istanza `Repository` per stabilire una sessione con l&#39;archivio. Per creare una sessione, richiamare il metodo `login` dell&#39;istanza `Repository` e passare un oggetto `javax.jcr.SimpleCredentials`. Il metodo `login` restituisce un&#39;istanza `javax.jcr.Session`.

Per creare un oggetto `SimpleCredentials`, utilizzare il relativo costruttore e passare i seguenti valori stringa:

* Il nome utente;
* La password corrispondente

Quando si passa il secondo parametro, chiamare il metodo `toCharArray` dell&#39;oggetto String. Nel codice seguente viene illustrato come chiamare il metodo `login` che restituisce un `javax.jcr.Sessioninstance`.

```java
//Create a Session instance
javax.jcr.Session session = repository.login( new SimpleCredentials("admin", "admin".toCharArray()));
```

## Creare un’istanza del nodo {#create-a-node-instance}

Utilizzare un&#39;istanza `Session` per creare un&#39;istanza `javax.jcr.Node`. Un&#39;istanza `Node` consente di eseguire operazioni sui nodi. Ad esempio, puoi creare un nodo. Per creare un nodo che rappresenta il nodo principale, richiamare il metodo `getRootNode` dell&#39;istanza `Session`, come illustrato nella riga di codice seguente.

```java
//Create a Node
Node root = session.getRootNode();
```

Dopo aver creato un&#39;istanza `Node`, è possibile eseguire attività quali la creazione di un altro nodo e l&#39;aggiunta di un valore. Ad esempio, il codice seguente crea due nodi e aggiunge un valore al secondo nodo.

```java
// Store content
Node day = adobe.addNode("day");
day.setProperty("message", "Adobe CQ is part of the Adobe Digital Marketing Suite!");
```

## Recupera valori nodo {#retrieve-node-values}

Per recuperare un nodo e il relativo valore, richiamare il metodo `getNode` dell&#39;istanza `Node` e passare un valore stringa che rappresenta il percorso completo del nodo. Considera la struttura dei nodi creata nell’esempio di codice precedente. Per recuperare il nodo del giorno, specifica adobe/day, come illustrato nel codice seguente:

```java
// Retrieve content
Node node = root.getNode("adobe/day");
System.out.println(node.getPath());
System.out.println(node.getProperty("message").getString());
```

## Creare nodi nel repository di Adobe CQ {#create-nodes-in-the-adobe-cq-repository}

Il codice Java™ seguente rappresenta una classe Java™ che si connette ad Adobe CQ, crea un&#39;istanza `Session` e aggiunge nuovi nodi. A un nodo viene assegnato un valore di dati, quindi il valore del nodo e il relativo percorso vengono scritti nella console. Al termine della sessione, assicurati di disconnettersi.

```java
/*
 * This Java Quick Start uses the jackrabbit-standalone-2.4.0.jar
 * file. See the previous section for the location of this JAR file
 */

import javax.jcr.Repository;
import javax.jcr.Session;
import javax.jcr.SimpleCredentials;
import javax.jcr.Node;

import org.apache.jackrabbit.commons.JcrUtils;
import org.apache.jackrabbit.core.TransientRepository;

public class GetRepository {

public static void main(String[] args) throws Exception {

try {

    //Create a connection to the CQ repository running on local host
    Repository repository = JcrUtils.getRepository("http://localhost:4503/crx/server");

   //Create a Session
   javax.jcr.Session session = repository.login( new SimpleCredentials("admin", "admin".toCharArray()));

  //Create a node that represents the root node
  Node root = session.getRootNode();

  // Store content
  Node adobe = root.addNode("adobe");
  Node day = adobe.addNode("day");
  day.setProperty("message", "Adobe CQ is part of the Adobe Digital Marketing Suite!");

  // Retrieve content
  Node node = root.getNode("adobe/day");
  System.out.println(node.getPath());
  System.out.println(node.getProperty("message").getString());

  // Save the session changes and log out
  session.save();
  session.logout();
  }
 catch(Exception e){
  e.printStackTrace();
  }
 }
}
```

Dopo aver eseguito l&#39;esempio di codice completo e aver creato i nodi, è possibile visualizzare i nuovi nodi in **[!UICONTROL CRXDE Liti]**, come illustrato nella figura seguente.

![chlimage_1-68](assets/chlimage_1-68a.png)
