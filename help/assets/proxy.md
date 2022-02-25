---
title: '"[!DNL Assets] sviluppo proxy"'
description: Un proxy è un [!DNL Experience Manager] istanza che utilizza i processi proxy worker per l'elaborazione dei processi. Scopri come configurare un [!DNL Experience Manager] proxy, operazioni supportate, componenti proxy e come sviluppare un proxy worker personalizzato.
contentOwner: AG
role: Admin, Architect
exl-id: 42fff236-b4e1-4f42-922c-97da32a933cf
source-git-commit: e24316cb9495a552960ae0620e4198f10a08b691
workflow-type: tm+mt
source-wordcount: '844'
ht-degree: 0%

---

# [!DNL Assets] sviluppo proxy {#assets-proxy-development}

[!DNL Adobe Experience Manager Assets] utilizza un proxy per distribuire l&#39;elaborazione per determinate attività.

Un proxy è un&#39;istanza di Experience Manager specifica (e talvolta separata) che utilizza i proxy worker come processori responsabili della gestione di un lavoro e della creazione di un risultato. Un proxy worker può essere utilizzato per un&#39;ampia varietà di attività. Nel caso di un [!DNL Assets] proxy che può essere utilizzato per caricare le risorse per il rendering all’interno di Assets. Ad esempio, il [proxy worker IDS](indesign.md) utilizza un [!DNL Adobe InDesign] Server per elaborare i file da utilizzare in Assets.

Quando il proxy è separato [!DNL Experience Manager] in questo modo si riduce il carico sul [!DNL Experience Manager] istanze di authoring. Per impostazione predefinita, [!DNL Assets] esegue le attività di elaborazione delle risorse nella stessa JVM (esternalizzata tramite Proxy) per ridurre il carico sul [!DNL Experience Manager] istanza di authoring.

## Proxy (accesso HTTP) {#proxy-http-access}

Un proxy è disponibile tramite il servlet HTTP quando è configurato per accettare processi di elaborazione in: `/libs/dam/cloud/proxy`. Questo servlet crea un lavoro sling dai parametri inviati. Questo viene quindi aggiunto alla coda del processo proxy e collegato al processo di lavoro proxy appropriato.

### Operazioni supportate {#supported-operations}

* `job`

   **Requisiti**: il parametro `jobevent` deve essere impostato come mappa del valore serializzato. Viene utilizzato per creare un `Event` per un processore di lavoro.

   **Risultato**: Aggiunge un nuovo processo. In caso di esito positivo, viene restituito un ID processo univoco.

```shell
curl -u admin:admin -F":operation=job" -F"someproperty=xxxxxxxxxxxx"
    -F"jobevent=serialized value map" http://localhost:4502/libs/dam/cloud/proxy
```

* `result`

   **Requisiti**: il parametro `jobid` deve essere impostato.

   **Risultato**: Restituisce una rappresentazione JSON del Nodo risultato creato dal processore del processo.

```shell
curl -u admin:admin -F":operation=result" -F"jobid=xxxxxxxxxxxx"
    http://localhost:4502   /libs/dam/cloud/proxy
```

* `resource`

   **Requisiti**: il parametro jobid deve essere impostato.

   **Risultato**: Restituisce una risorsa associata al processo specificato.

```shell
curl -u admin:admin -F":operation=resource" -F"jobid=xxxxxxxxxxxx"
    -F"resourcePath=something.pdf" http://localhost:4502/libs/dam/cloud/proxy
```

* `remove`

   **Requisiti**: il parametro jobid deve essere impostato.

   **Risultati**: Rimuove un processo se trovato.

```shell
curl -u admin:admin -F":operation=remove" -F"jobid=xxxxxxxxxxxx"
    http://localhost:4502/libs/dam/cloud/proxy
```

### Proxy Worker {#proxy-worker}

Un proxy worker è un processore responsabile della gestione di un processo e della creazione di un risultato. I lavoratori risiedono nell&#39;istanza proxy e devono implementare [sling JobProcessor](https://sling.apache.org/site/eventing-and-jobs.html) da riconoscere come proxy worker.

>[!NOTE]
>
>Il lavoratore deve implementare [sling JobProcessor](https://sling.apache.org/site/eventing-and-jobs.html) da riconoscere come proxy worker.

### API client {#client-api}

[`JobService`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html) è disponibile come servizio OSGi che fornisce metodi per creare lavori, rimuovere lavori e ottenere risultati da tali processi. Implementazione predefinita di questo servizio (`JobServiceImpl`) utilizza il client HTTP per comunicare con il servlet proxy remoto.

Di seguito è riportato un esempio di utilizzo API:

```java
@Reference
 JobService proxyJobService;

 // to create a new job
 final Hashtable props = new Hashtable();
 props.put("someproperty", "some value");
 props.put(JobUtil.PROPERTY_JOB_TOPIC, "myworker/job"); // this is an identifier of the worker
 final String jobId = proxyJobService.addJob(props, new Asset[]{asset});

 // to check status (returns JobService.STATUS_FINISHED or JobService.STATUS_INPROGRESS)
 int status = proxyJobService.getStatus(jobId)

 // to get the result
 final String jsonString = proxyJobService.getResult(jobId);

 // to remove job and cleanup
 proxyJobService.removeJob(jobId);
```

### Configurazioni Cloud Service {#cloud-service-configurations}

<!-- TBD: Cannot find com.day.cq.dam.api.proxy at https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html which were generated in May 2020. Hiding this broken link for now.
>[!NOTE]
>
>Reference documentation for the proxy API is available under [`com.day.cq.dam.api.proxy`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/dam/api/proxy/package-summary.html).
-->

Le configurazioni proxy e proxy worker sono disponibili tramite configurazioni cloud services accessibili dal [!DNL Assets] **Strumenti** console o sotto `/etc/cloudservices/proxy`. Ogni proxy worker deve aggiungere un nodo in `/etc/cloudservices/proxy` per i dettagli di configurazione specifici del lavoratore (ad esempio, `/etc/cloudservices/proxy/workername`).

>[!NOTE]
>
>Vedi [Configurazione di InDesign Server Proxy Worker](indesign.md#configuring-the-proxy-worker-for-indesign-server) e [Configurazione dei Cloud Services](../sites-developing/extending-cloud-config.md) per ulteriori informazioni.

Di seguito è riportato un esempio di utilizzo API:

```java
@Reference(policy = ReferencePolicy.STATIC)
 ProxyConfig proxyConfig;

 // to get proxy config
 Configuration cloudConfig = proxyConfig.getConfiguration();
 final String value = cloudConfig.get("someProperty", "defaultValue");

 // to get worker config
 Configuration cloudConfig = proxyConfig.getConfiguration("workername");
 final String value = cloudConfig.get("someProperty", "defaultValue");
```

### Sviluppo di un proxy worker personalizzato {#developing-a-customized-proxy-worker}

La [proxy worker IDS](indesign.md) è un esempio di [!DNL Assets] proxy worker già fornito per l’outsourcing dell’elaborazione delle risorse di InDesign.

Puoi anche sviluppare e configurare [!DNL Assets] proxy worker per creare un lavoratore specializzato per l&#39;invio e l&#39;outsourcing del tuo [!DNL Assets] attività di elaborazione.

Per configurare un processo di lavoro proxy personalizzato è necessario:

* Configurazione e implementazione (utilizzando l’evento Sling):

   * un argomento di lavoro personalizzato
   * un gestore di eventi di lavoro personalizzato

* Quindi utilizza l’API JobService per:

   * invia il processo personalizzato al proxy
   * gestire il proprio lavoro

* Se desideri utilizzare il proxy da un flusso di lavoro, devi implementare un passaggio esterno personalizzato utilizzando l’API WorkflowExternalProcess e l’API JobService.

Il diagramma seguente e i passaggi descrivono come procedere:

![chlimage_1-249](assets/chlimage_1-249.png)

>[!NOTE]
>
>Nei passaggi seguenti, gli equivalenti di InDesign sono indicati come esempi di riferimento.

1. A [Processo Sling](https://sling.apache.org/site/eventing-and-jobs.html) viene utilizzato, quindi devi definire un argomento di lavoro per il tuo caso d’uso.

   Ad esempio, vedi `IDSJob.IDS_EXTENDSCRIPT_JOB` per il proxy worker IDS.

1. Il passaggio esterno viene utilizzato per attivare l’evento e quindi attendere fino al termine; questo viene fatto tramite sondaggi sull&#39;id. Devi sviluppare un tuo passaggio per implementare nuove funzionalità.

   Implementare un `WorkflowExternalProcess`, quindi utilizza l’API JobService e l’argomento del tuo lavoro per preparare un evento di lavoro e inviarlo al JobService (un servizio OSGi).

   Ad esempio, vedi `INDDMediaExtractProcess`.java per il proxy worker IDS.

1. Implementa un gestore di processi per l’argomento. Questo gestore richiede lo sviluppo in modo che esegua l&#39;azione specifica ed è considerato l&#39;implementazione del processo di lavoro.

   Ad esempio, vedi `IDSJobProcessor.java` per il proxy worker IDS.

1. Utilizzare `ProxyUtil.java` in dam-commons. Questo consente di inviare i lavori ai lavoratori utilizzando il proxy dam.

>[!NOTE]
>
>Cosa [!DNL Assets] il framework proxy non fornisce il meccanismo di pool preconfigurato.
>
>La [!DNL InDesign] l&#39;integrazione consente l&#39;accesso a un pool di [!DNL InDesign] server (IDSPool). Questo pool è specifico per [!DNL InDesign] integrazione e non parte del [!DNL Assets] struttura proxy.

>[!NOTE]
>
>Sincronizzazione dei risultati:
>
>Con n istanze che utilizzano lo stesso proxy, il risultato dell&#39;elaborazione rimane con il proxy. È compito del client (ad Experience Manager Autore) richiedere il risultato utilizzando lo stesso ID di processo univoco assegnato al client al momento della creazione del processo. Il proxy ottiene semplicemente il lavoro svolto e mantiene il risultato pronto per essere richiesto.
