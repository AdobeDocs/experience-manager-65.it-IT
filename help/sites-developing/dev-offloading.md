---
title: Creazione e utilizzo di processi per l'offload
description: La funzione di individuazione Sling di Apache fornisce un’API Java che consente di creare processi JobManager e servizi JobConsumer che li utilizzano
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
exl-id: 4e6f452d-0251-46f3-ba29-1bd85cda73a6
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '393'
ht-degree: 0%

---

# Creazione e utilizzo di processi per l&#39;offload{#creating-and-consuming-jobs-for-offloading}

La funzione di individuazione Sling di Apache fornisce un’API Java che consente di creare processi JobManager e servizi JobConsumer che li utilizzano.

Per informazioni sulla creazione di topologie di offload e sulla configurazione del consumo di argomenti, vedere [Offload dei processi](/help/sites-deploying/offloading.md).

## Gestione dei payload dei processi {#handling-job-payloads}

Il framework di offload definisce due proprietà di processo utilizzate per identificare il payload del processo. Gli agenti di replica di offload utilizzano queste proprietà per identificare le risorse da replicare nelle istanze nella topologia:

* `offloading.job.input.payload`: elenco di percorsi di contenuto separato da virgole. Il contenuto viene replicato nell’istanza che esegue il processo.
* `offloading.job.output.payload`: elenco di percorsi di contenuto separato da virgole. Al termine dell’esecuzione del processo, il payload del processo viene replicato in questi percorsi nell’istanza che ha creato il processo.

Utilizza il `OffloadingJobProperties` enum per fare riferimento ai nomi delle proprietà:

* `OffloadingJobProperties.INPUT_PAYLOAD.propertyName()`
* `OffloadingJobProperties.OUTPUT_PAYLOAD.propetyName()`

I processi non richiedono payload. Tuttavia, il payload è necessario se il processo richiede la manipolazione di una risorsa e viene scaricato su un computer che non lo ha creato.

## Creazione di processi per l&#39;offload {#creating-jobs-for-offloading}

Creare un client che chiama il metodo JobManager.addJob per creare un processo eseguito da un JobConsumer selezionato automaticamente. Fornisci le seguenti informazioni per creare il processo:

* Argomento: Argomento del processo.
* Nome: (facoltativo)
* Mappa proprietà: A `Map<String, Object>` oggetto che contiene un numero qualsiasi di proprietà, ad esempio i percorsi del payload di input e di output. Questo oggetto Map è disponibile per l&#39;oggetto JobConsumer che esegue il processo.

Il servizio di esempio seguente crea un processo per un argomento e un percorso di payload di input specifici.

```java
package com.adobe.example.offloading;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Service;
import org.apache.felix.scr.annotations.Reference;

import java.util.HashMap;

import org.apache.sling.event.jobs.Job;
import org.apache.sling.event.jobs.JobManager;

import org.apache.sling.api.resource.ResourceResolverFactory;
import org.apache.sling.api.resource.ResourceResolver;

import com.adobe.granite.offloading.api.OffloadingJobProperties;

@Component
@Service
public class JobGeneratorImpl implements JobGenerator  {

 @Reference
 private JobManager jobManager;
 @Reference ResourceResolverFactory resolverFactory;

 public String createJob(String topic, String payload) throws Exception {
  Job offloadingJob;

  ResourceResolver resolver = resolverFactory.getResourceResolver(null);
  if(resolver.getResource(payload)!=null){

   HashMap<String, Object> jobprops = new HashMap<String, Object>();
   jobprops.put(OffloadingJobProperties.INPUT_PAYLOAD.propertyName(), payload);

   offloadingJob = jobManager.addJob(topic, null, jobprops);
  } else {
   throw new Exception("Payload for job cannot be found");
  }
  if (offloadingJob == null){
   throw new Exception ("Offloading job could not be created");
  }
  return offloadingJob.getId();
 }
}
```

Il registro contiene il seguente messaggio quando viene chiamato JobGeneratorImpl.createJob per `com/adobe/example/offloading` argomento e `/content/geometrixx/de/services` payload:

```shell
10.06.2013 15:43:33.868 *INFO* [JobHandler: /etc/workflow/instances/2013-06-10/model_1554418768647484:/content/geometrixx/en/company] com.adobe.example.offloading.JobGeneratorImpl Received request to make job for topic com/adobe/example/offloading and payload /content/geometrixx/de/services
```

## Sviluppare un consumatore di lavoro {#developing-a-job-consumer}

Per utilizzare i lavori, sviluppa un servizio OSGi che implementa `org.apache.sling.event.jobs.consumer.JobConsumer` di rete. Identificare con l&#39;argomento da utilizzare utilizzando `JobConsumer.PROPERTY_TOPICS` proprietà.

L’esempio seguente di implementazione di JobConsumer si registra con `com/adobe/example/offloading` argomento. Il consumatore imposta semplicemente la proprietà Consumed del nodo di contenuto del payload su true.

```java
package com.adobe.example.offloading;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Property;
import org.apache.felix.scr.annotations.Reference;
import org.apache.felix.scr.annotations.Service;
import org.apache.sling.api.resource.ResourceResolver;
import org.apache.sling.api.resource.ResourceResolverFactory;
import org.apache.sling.event.jobs.Job;
import org.apache.sling.event.jobs.JobManager;
import org.apache.sling.event.jobs.consumer.JobConsumer;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import javax.jcr.Session;
import javax.jcr.Node;

import com.adobe.granite.offloading.api.OffloadingJobProperties;

@Component
@Service
public class MyJobConsumer implements JobConsumer {

 public static final String TOPIC = "com/adobe/example/offloading";

 @Property(value = TOPIC)
 static final String myTopic = JobConsumer.PROPERTY_TOPICS;

 @Reference
 private ResourceResolverFactory resolverFactory;

 @Reference
 private JobManager jobManager;

 private final Logger log = LoggerFactory.getLogger(getClass());

 public JobResult process(Job job) {
  JobResult result = JobResult.FAILED;
  String topic = job.getTopic();
  log.info("Consuming job of topic: {}", topic);
  String payloadIn =  (String) job.getProperty(OffloadingJobProperties.INPUT_PAYLOAD.propertyName());
  String payloadOut =  (String) job.getProperty(OffloadingJobProperties.OUTPUT_PAYLOAD.propertyName());

  log.info("Job has Input Payload {} and Output Payload {}",payloadIn, payloadOut);

  ResourceResolver resolver = null;
  try {
   resolver = resolverFactory.getAdministrativeResourceResolver(null);
   Session session = resolver.adaptTo(Session.class);
   Node inNode = session.getNode(payloadIn);
   inNode.getNode(Node.JCR_CONTENT).setProperty("consumed",true);
   result = JobResult.OK;
  }catch (Exception e){
   log.info("ERROR -- JOB RESULT IS FAILURE " + e.getMessage());
   result = JobResult.FAILED;
  }
  log.info("Job OK for payload {}",payloadIn);
  return result;
 }
}
```

La classe MyJobConsumer genera i seguenti messaggi di registro per un payload di input di /content/geometrixx/de/services:

```shell
10.06.2013 16:02:40.803 *INFO* [pool-7-thread-17-<main queue>(com/adobe/example/offloading)] com.adobe.example.offloading.MyJobConsumer Consuming job of topic: com/adobe/example/offloading
10.06.2013 16:02:40.803 *INFO* [pool-7-thread-17-<main queue>(com/adobe/example/offloading)] com.adobe.example.offloading.MyJobConsumer Job has Input Payload /content/geometrixx/de/services and Output Payload /content/geometrixx/de/services
10.06.2013 16:02:40.884 *INFO* [pool-7-thread-17-<main queue>(com/adobe/example/offloading)] com.adobe.example.offloading.MyJobConsumer Job OK for payload /content/geometrixx/de/services
```

La proprietà Consumed può essere osservata utilizzando CRXDE Liti:

![chlimage_1-25](assets/chlimage_1-25a.png)

## Dipendenze Maven {#maven-dependencies}

Aggiungi le seguenti definizioni di dipendenza al file pom.xml in modo che Maven possa risolvere le classi relative all’offload.

```xml
<dependency>
   <groupId>org.apache.sling</groupId>
   <artifactId>org.apache.sling.event</artifactId>
   <version>3.1.5-R1485539</version>
   <scope>provided</scope>
</dependency>
<dependency>
   <groupId>com.adobe.granite</groupId>
   <artifactId>com.adobe.granite.offloading.core</artifactId>
   <version>1.0.4</version>
   <scope>provided</scope>
</dependency>
```

Gli esempi precedenti richiedevano anche le seguenti definizioni di dipendenze:

```xml
<dependency>
   <groupId>org.apache.sling</groupId>
   <artifactId>org.apache.sling.api</artifactId>
   <version>2.4.3-R1488084</version>
   <scope>provided</scope>
</dependency>

<dependency>
   <groupId>org.apache.sling</groupId>
   <artifactId>org.apache.sling.jcr.jcr-wrapper</artifactId>
   <version>2.0.0</version>
   <scope>provided</scope>
</dependency>
```
