---
title: Come accedere programmaticamente a AEM JCR
seo-title: How to programmatically access the AEM JCR
description: Puoi modificare programmaticamente nodi e proprietà situati all’interno dell’archivio AEM, che fa parte di Adobe Marketing Cloud
seo-description: You can programmatically modify nodes and properties located within the AEM repository, which is part of the Adobe Marketing Cloud
uuid: 2051d03f-430a-4cae-8f6d-e5bc727d733f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 69f62a38-7991-4009-8db7-ee8fd35dc535
exl-id: fe946b9a-b29e-4aa5-b973-e2a652417a55
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '591'
ht-degree: 0%

---

# Come accedere programmaticamente a AEM JCR{#how-to-programmatically-access-the-aem-jcr}

Puoi modificare programmaticamente nodi e proprietà che si trovano all’interno dell’archivio Adobe CQ, che fa parte di Adobe Marketing Cloud. Per accedere all’archivio CQ, utilizza l’API Java Content Repository (JCR). Puoi utilizzare l’API Java JCR per eseguire operazioni di creazione, sostituzione, aggiornamento ed eliminazione (CRUD) su contenuti che si trovano all’interno dell’archivio Adobe CQ. Per ulteriori informazioni sull&#39;API Java JCR, vedi [https://jackrabbit.apache.org/jcr/jcr-api.html](https://jackrabbit.apache.org/jcr/jcr-api.html).

>[!NOTE]
>
>Questo articolo di sviluppo modifica Adobe CQ JCR da un&#39;applicazione Java esterna. Al contrario, puoi modificare il JCR dall&#39;interno di un bundle OSGi utilizzando l&#39;API JCR. Per maggiori dettagli, vedi [Persistenza dei dati CQ nel Java Content Repository](https://helpx.adobe.com/experience-manager/using/persisting-cq-data-java-content1.html).

>[!NOTE]
>
>Per utilizzare l’API JCR, aggiungi la `jackrabbit-standalone-2.4.0.jar` nel percorso della classe dell&#39;applicazione Java. Puoi ottenere questo file JAR dalla pagina web API Java JCR all&#39;indirizzo [https://jackrabbit.apache.org/jcr/jcr-api.html](https://jackrabbit.apache.org/jcr/jcr-api.html).

>[!NOTE]
>
>Per scoprire come eseguire una query su Adobe CQ JCR utilizzando l’API JCR Query, vedi [Query dei dati di Adobe Experience Manager tramite l’API JCR](https://helpx.adobe.com/experience-manager/using/querying-experience-manager-data-using1.html).

## Creare un’istanza di archivio {#create-a-repository-instance}

Sebbene esistano diversi modi per connettersi a un archivio e stabilire una connessione, questo articolo di sviluppo utilizza un metodo statico appartenente al `org.apache.jackrabbit.commons.JcrUtils` classe. Il nome del metodo è `getRepository`. Questo metodo prende un parametro di stringa che rappresenta l&#39;URL del server Adobe CQ. Esempio `http://localhost:4503/crx/server`.

La `getRepository`restituisce un `Repository`, come illustrato nell’esempio di codice seguente.

```java
//Create a connection to the AEM JCR repository running on local host
Repository repository = JcrUtils.getRepository("http://localhost:4503/crx/server");
```

## Creare un’istanza di sessione {#create-a-session-instance}

La `Repository`L&#39;istanza rappresenta l&#39;archivio CRX. Utilizzi le `Repository`istanza per stabilire una sessione con l&#39;archivio. Per creare una sessione, richiama il `Repository`dell’istanza `login`e passare un `javax.jcr.SimpleCredentials` oggetto. La `login`restituisce un `javax.jcr.Session` istanza.

Crea un `SimpleCredentials`utilizzando il relativo costruttore e passando i seguenti valori stringa:

* Nome utente;
* Password corrispondente

Quando trasmetti il secondo parametro, chiama l&#39;oggetto String `toCharArray`metodo . Il codice seguente mostra come chiamare il `login`metodo che restituisce un `javax.jcr.Sessioninstance`.

```java
//Create a Session instance
javax.jcr.Session session = repository.login( new SimpleCredentials("admin", "admin".toCharArray()));
```

## Creare un’istanza di nodo {#create-a-node-instance}

Utilizza un `Session`istanza per creare un `javax.jcr.Node` istanza. A `Node`instance ti consente di eseguire le operazioni sui nodi. Ad esempio, puoi creare un nuovo nodo. Per creare un nodo che rappresenta il nodo principale, richiama il `Session`dell&#39;istanza `getRootNode` , come illustrato nella seguente riga di codice.

```java
//Create a Node
Node root = session.getRootNode();
```

Una volta creata una `Node`Ad esempio, puoi eseguire attività quali la creazione di un altro nodo e l’aggiunta di un valore ad esso. Ad esempio, il codice seguente crea due nodi e aggiunge un valore al secondo nodo.

```java
// Store content
Node day = adobe.addNode("day");
day.setProperty("message", "Adobe CQ is part of the Adobe Digital Marketing Suite!");
```

## Recupera valori nodo {#retrieve-node-values}

Per recuperare un nodo e il relativo valore, richiama il `Node`dell’istanza `getNode`e passare un valore stringa che rappresenta il percorso completo del nodo. Considera la struttura del nodo creata nell’esempio di codice precedente. Per recuperare il nodo giorno, specifica adobe/day, come mostrato nel codice seguente:

```java
// Retrieve content
Node node = root.getNode("adobe/day");
System.out.println(node.getPath());
System.out.println(node.getProperty("message").getString());
```

## Creare nodi nell’archivio di Adobe CQ {#create-nodes-in-the-adobe-cq-repository}

Il seguente esempio di codice Java rappresenta una classe Java che si connette ad Adobe CQ e crea un `Session`e aggiunge nuovi nodi. A un nodo viene assegnato un valore di dati, quindi il valore del nodo e il relativo percorso viene scritto sulla console. Al termine della sessione, assicurati di disconnettersi.

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

Dopo aver eseguito l&#39;esempio di codice completo e creato i nodi, puoi visualizzare i nuovi nodi nel **[!UICONTROL CRXDE Lite]**, come illustrato nella figura seguente.

![chlimage_1-68](assets/chlimage_1-68a.png)
