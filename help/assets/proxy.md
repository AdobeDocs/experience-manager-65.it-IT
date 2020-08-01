---
title: Sviluppo proxy di [!DNL Assets]
description: Un proxy è [!DNL Experience Manager] instance that uses proxy workers to process jobs. Learn how to configure an [!DNL Experience Manager] un proxy, operazioni supportate, componenti proxy e come sviluppare un proxy lavoratore personalizzato.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 9fc1201db83ae0d3bb902d4dc3ab6d78cc1dc251
workflow-type: tm+mt
source-wordcount: '861'
ht-degree: 0%

---


# [!DNL Assets] sviluppo proxy {#assets-proxy-development}

[!DNL Adobe Experience Manager Assets] utilizza un proxy per distribuire l&#39;elaborazione per determinate attività.

Un proxy è un&#39;istanza di Experience Manager  specifica (e a volte separata) che utilizza i proxy worker come processori responsabili della gestione di un processo e della creazione di un risultato. Un lavoratore proxy può essere utilizzato per un&#39;ampia gamma di attività. Nel caso di un [!DNL Assets] proxy, questo può essere utilizzato per caricare le risorse per il rendering all’interno delle risorse. Ad esempio, il lavoratore [proxy](indesign.md) IDS utilizza un [!DNL Adobe InDesign] server per elaborare i file da utilizzare in Assets.

Se il proxy è un&#39; [!DNL Experience Manager] istanza separata, questo consente di ridurre il carico sulle istanze di authoring dei Experienci Manager . Per impostazione predefinita, [!DNL Assets] esegue le attività di elaborazione delle risorse nella stessa JVM (esternalizzata tramite proxy) per ridurre il carico sull’istanza di creazione del Experience Manager .

## Proxy (accesso HTTP) {#proxy-http-access}

Un proxy è disponibile tramite il servlet HTTP quando è configurato per accettare processi di elaborazione in: `/libs/dam/cloud/proxy`. Questo servlet crea un processo di sling dai parametri inseriti. Questo viene aggiunto alla coda di processo del proxy e collegato al lavoratore proxy appropriato.

### Operazioni supportate {#supported-operations}

* `job`

   **Requisiti**: il parametro `jobevent` deve essere impostato come mappa di valore serializzato. Viene utilizzato per creare un processore `Event` per un processo.

   **Risultato**: Aggiunge un nuovo processo. In caso di esito positivo, viene restituito un ID di processo univoco.

```shell
curl -u admin:admin -F":operation=job" -F"someproperty=xxxxxxxxxxxx"
    -F"jobevent=serialized value map" http://localhost:4502/libs/dam/cloud/proxy
```

* `result`

   **Requisiti**: il parametro `jobid` deve essere impostato.

   **Risultato**: Restituisce una rappresentazione JSON del nodo risultato creato dal processore del processo.

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

   **Risultati**: Rimuove un processo se viene trovato.

```shell
curl -u admin:admin -F":operation=remove" -F"jobid=xxxxxxxxxxxx"
    http://localhost:4502/libs/dam/cloud/proxy
```

### Proxy Worker {#proxy-worker}

Un lavoratore proxy è un processore responsabile della gestione di un processo e della creazione di un risultato. I lavoratori risiedono nell&#39;istanza proxy e devono implementare [sling JobProcessor](https://sling.apache.org/site/eventing-and-jobs.html) per essere riconosciuti come un lavoratore proxy.

>[!NOTE]
>
>Il lavoratore deve implementare [sling JobProcessor](https://sling.apache.org/site/eventing-and-jobs.html) per essere riconosciuto come lavoratore proxy.

### API client {#client-api}

[`JobService`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html) è disponibile come servizio OSGi che fornisce metodi per creare processi, rimuovere processi e ottenere risultati da tali processi. L&#39;implementazione predefinita di questo servizio (`JobServiceImpl`) utilizza il client HTTP per comunicare con il servlet proxy remoto.

Esempio di utilizzo delle API:

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

>[!NOTE]
>
>La documentazione di riferimento per l&#39;API proxy è disponibile in [`com.day.cq.dam.api.proxy`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/dam/api/proxy/package-summary.html).

Sia le configurazioni di proxy che quelle di proxy worker sono disponibili tramite configurazioni di servizi cloud accessibili dalla console [!DNL Assets] Strumenti **o in** `/etc/cloudservices/proxy`. Ogni lavoratore proxy deve aggiungere un nodo in `/etc/cloudservices/proxy` per i dettagli di configurazione specifici del lavoratore (ad esempio, `/etc/cloudservices/proxy/workername`).

>[!NOTE]
>
>Per ulteriori informazioni, consulta [configurazione](indesign.md#configuring-the-proxy-worker-for-indesign-server) InDesign Server Proxy Worker e configurazione [](../sites-developing/extending-cloud-config.md) Cloud Services.

Esempio di utilizzo delle API:

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

### Sviluppo di un Proxy Worker personalizzato {#developing-a-customized-proxy-worker}

Il lavoratore [proxy](indesign.md) IDS è un esempio di un lavoratore [!DNL Assets] proxy già fornito out-of-the-box per esternalizzare l&#39;elaborazione delle risorse  InDesign.

È inoltre possibile sviluppare e configurare il proprio [!DNL Assets] proxy worker per creare un lavoratore specializzato per l&#39;invio e l&#39;outsourcing delle attività di [!DNL Assets] elaborazione.

Per impostare un lavoratore proxy personalizzato è necessario:

* Configurare e implementare (utilizzando Sling eventing):

   * un argomento del processo personalizzato
   * un gestore eventi di processo personalizzato

* Quindi utilizzate l&#39;API JobService per:

   * invio del processo personalizzato al proxy
   * gestire il lavoro

* Se desiderate utilizzare il proxy da un flusso di lavoro, dovete implementare un passaggio esterno personalizzato utilizzando l&#39;API WorkflowExternalProcess e l&#39;API JobService.

Nel diagramma seguente e nei passaggi viene descritto come procedere:

![chlimage_1-249](assets/chlimage_1-249.png)

>[!NOTE]
>
>Nei passaggi seguenti, gli equivalenti  InDesign sono indicati come esempi di riferimento.

1. Viene utilizzato un processo [](https://sling.apache.org/site/eventing-and-jobs.html) Sling, per cui è necessario definire un argomento di processo per il caso d’uso.

   Ad esempio, vedere `IDSJob.IDS_EXTENDSCRIPT_JOB` per il proxy worker IDS.

1. Il passaggio esterno viene utilizzato per attivare l’evento e quindi attendere che sia terminato; questo viene fatto tramite un sondaggio sull&#39;ID. Per implementare le nuove funzionalità è necessario sviluppare un proprio passaggio.

   Implementate un `WorkflowExternalProcess`, quindi utilizzate l’API JobService e l’argomento del processo per preparare un evento di processo e inviarlo a JobService (un servizio OSGi).

   Ad esempio, vedere `INDDMediaExtractProcess`.java per il lavoratore proxy IDS.

1. Implementare un gestore di processi per l’argomento. Questo gestore richiede lo sviluppo in modo che esegua l&#39;azione specifica e sia considerato come implementazione del lavoratore.

   Ad esempio, vedere `IDSJobProcessor.java` per il proxy worker IDS.

1. Fate uso di `ProxyUtil.java` in dam-commons. Questo consente di inviare i processi ai lavoratori utilizzando il proxy DAM.

>[!NOTE]
>
>Ciò che il framework [!DNL Assets] proxy non fornisce è il meccanismo del pool.
>
>L&#39; [!DNL InDesign] integrazione consente l&#39;accesso a un pool di [!DNL InDesign] server (IDSPool). Questo pool è specifico dell&#39; [!DNL InDesign] integrazione e non fa parte del framework [!DNL Assets] proxy.

>[!NOTE]
>
>Sincronizzazione dei risultati:
>
>In caso di n istanze che utilizzano lo stesso proxy, il risultato dell&#39;elaborazione rimane con il proxy. È compito del client ( Autore Experience Manager) richiedere il risultato utilizzando lo stesso ID processo univoco fornito al client al momento della creazione del processo. Il proxy ottiene semplicemente il lavoro e mantiene il risultato pronto per essere richiesto.
