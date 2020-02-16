---
title: Come accedere a AEM JCR a livello di programmazione
seo-title: Come accedere a AEM JCR a livello di programmazione
description: Puoi modificare a livello di programmazione nodi e proprietà situati nell’archivio di AEM, che fa parte di Adobe Marketing Cloud
seo-description: Puoi modificare a livello di programmazione nodi e proprietà situati nell’archivio di AEM, che fa parte di Adobe Marketing Cloud
uuid: 2051d03f-430a-4cae-8f6d-e5bc727d733f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 69f62a38-7991-4009-8db7-ee8fd35dc535
translation-type: tm+mt
source-git-commit: 6d216e7521432468a01a29ad2879f8708110d970

---


# Come accedere a AEM JCR a livello di programmazione{#how-to-programmatically-access-the-aem-jcr}

È possibile modificare a livello di programmazione nodi e proprietà situati nell&#39;archivio di Adobe CQ, che fa parte di Adobe Marketing Cloud. Per accedere all&#39;archivio CQ, utilizzate l&#39;API Java Content Repository (JCR). Potete utilizzare l&#39;API Java JCR per eseguire operazioni di creazione, sostituzione, aggiornamento ed eliminazione (CRUD) su contenuti che si trovano all&#39;interno dell&#39;archivio di Adobe CQ. Per ulteriori informazioni sull&#39;API Java JCR, vedete [https://jackrabbit.apache.org/jcr/jcr-api.html](https://jackrabbit.apache.org/jcr/jcr-api.html).

>[!NOTE]
>
>Questo articolo di sviluppo modifica Adobe CQ JCR da un&#39;applicazione Java esterna. Al contrario, potete modificare il JCR dall&#39;interno di un bundle OSGi utilizzando l&#39;API JCR. Per informazioni dettagliate, consultate [Persisting CQ data in Java Content Repository](https://helpx.adobe.com/experience-manager/using/persisting-cq-data-java-content1.html).

>[!NOTE]
>
>Per utilizzare l&#39;API JCR, aggiungete il `jackrabbit-standalone-2.4.0.jar` file al percorso di classe dell&#39;applicazione Java. Potete ottenere questo file JAR dalla pagina Web Java JCR API all&#39;indirizzo [https://jackrabbit.apache.org/jcr/jcr-api.html](https://jackrabbit.apache.org/jcr/jcr-api.html).

>[!NOTE]
>
>Per informazioni su come eseguire una query su Adobe CQ JCR utilizzando l&#39;API JCR Query, consulta [Query dei dati di Adobe Experience Manager tramite l&#39;API](https://helpx.adobe.com/experience-manager/using/querying-experience-manager-data-using1.html)JCR.

## Creare un&#39;istanza Repository {#create-a-repository-instance}

Sebbene esistano diversi modi per connettersi a un repository e stabilire una connessione, questo articolo di sviluppo utilizza un metodo statico che appartiene alla `org.apache.jackrabbit.commons.JcrUtils` classe. Il nome del metodo è `getRepository`. Questo metodo richiede un parametro stringa che rappresenta l’URL del server Adobe CQ. Esempio `http://localhost:4503/crx/server`.

Il `getRepository`metodo restituisce un’ `Repository`istanza, come illustrato nel seguente esempio di codice.

```java
//Create a connection to the AEM JCR repository running on local host
Repository repository = JcrUtils.getRepository("http://localhost:4503/crx/server");
```

## Creare un&#39;istanza di sessione {#create-a-session-instance}

L&#39; `Repository`istanza rappresenta l&#39;archivio CRX. L’ `Repository`istanza viene utilizzata per stabilire una sessione con la directory archivio. Per creare una sessione, richiamate il `Repository`metodo dell’ `login`istanza e passate un `javax.jcr.SimpleCredentials` oggetto. Il `login`metodo restituisce un’ `javax.jcr.Session` istanza.

È possibile creare un `SimpleCredentials`oggetto utilizzando il relativo costruttore e passando i seguenti valori stringa:

* Nome utente;
* La password corrispondente

Quando si passa il secondo parametro, chiamare il `toCharArray`metodo dell&#39;oggetto String. Il codice seguente mostra come chiamare il `login`metodo che restituisce un `javax.jcr.Sessioninstance`.

```java
//Create a Session instance
javax.jcr.Session session = repository.login( new SimpleCredentials("admin", "admin".toCharArray()));
```

## Creare un&#39;istanza Node {#create-a-node-instance}

Usate un’ `Session`istanza per creare un’ `javax.jcr.Node` istanza. Un&#39; `Node`istanza consente di eseguire operazioni sui nodi. Ad esempio, puoi creare un nuovo nodo. Per creare un nodo che rappresenta il nodo principale, invocare il `Session`metodo dell&#39; `getRootNode` istanza, come illustrato nella riga di codice seguente.

```java
//Create a Node
Node root = session.getRootNode();
```

Dopo aver creato un&#39; `Node`istanza, è possibile eseguire attività quali la creazione di un altro nodo e l&#39;aggiunta di un valore. Ad esempio, il codice seguente crea due nodi e aggiunge un valore al secondo nodo.

```java
// Store content
Node day = adobe.addNode("day");
day.setProperty("message", "Adobe CQ is part of the Adobe Digital Marketing Suite!");
```

## Recupera valori nodo {#retrieve-node-values}

Per recuperare un nodo e il relativo valore, richiamare il `Node`metodo dell&#39; `getNode`istanza e passare un valore di stringa che rappresenta il percorso completo del nodo. Considerare la struttura dei nodi creata nell&#39;esempio di codice precedente. Per recuperare il nodo giorno, specificate adobe/day, come illustrato nel seguente codice:

```java
// Retrieve content
Node node = root.getNode("adobe/day");
System.out.println(node.getPath());
System.out.println(node.getProperty("message").getString());
```

## Creare nodi nell’archivio di Adobe CQ {#create-nodes-in-the-adobe-cq-repository}

Il seguente esempio di codice Java rappresenta una classe Java che si connette ad Adobe CQ, crea un’ `Session`istanza e aggiunge nuovi nodi. A un nodo viene assegnato un valore di dati, quindi il valore del nodo e il relativo percorso vengono scritti nella console. Al termine della sessione, disconnettetevi.

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

Dopo aver eseguito l&#39;esempio di codice completo e creato i nodi, è possibile visualizzare i nuovi nodi in **[!UICONTROL CRXDE Lite]**, come illustrato nell&#39;illustrazione seguente.

![chlimage_1-68](assets/chlimage_1-68a.png)

