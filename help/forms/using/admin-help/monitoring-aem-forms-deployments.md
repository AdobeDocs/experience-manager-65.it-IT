---
title: Monitoraggio delle distribuzioni di moduli AEM
seo-title: Monitoring AEM forms deployments
description: È possibile monitorare AEM distribuzioni dei moduli sia a livello di sistema che a livello interno. Ulteriori informazioni sul monitoraggio delle distribuzioni di moduli AEM da questo documento.
seo-description: You can monitor AEM forms deployments from both a system level and an internal level. Learn more about monitoring AEM forms deployments from this document.
uuid: 032b7a93-3069-4ad5-a8c6-4c160f290669
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: b3e7bca0-5aaf-4f28-bddb-fd7e8ed72ee8
exl-id: 931e8095-5c7c-4c1f-b95b-75ac2827d4f3
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '605'
ht-degree: 0%

---

# Monitoraggio delle distribuzioni di moduli AEM {#monitoring-aem-forms-deployments}

È possibile monitorare AEM distribuzioni dei moduli sia a livello di sistema che a livello interno. È possibile utilizzare strumenti di gestione specializzati come HP OpenView, IBM Tivoli e CA UniCenter e un monitor JMX di terze parti denominato *JConsole* per monitorare in modo specifico l’attività Java. L’implementazione di una strategia di monitoraggio migliora la disponibilità, l’affidabilità e le prestazioni delle distribuzioni di moduli AEM.

Per ulteriori informazioni sul monitoraggio delle distribuzioni di moduli AEM, vedere [Guida tecnica per il monitoraggio delle distribuzioni di moduli AEM](https://www.adobe.com/devnet/livecycle/pdfs/lc_monitoring_wp_ue.pdf).

## Monitoraggio tramite MBeans {#monitoring-using-mbeans}

AEM forms fornisce due MBeans registrati che forniscono informazioni statistiche e di navigazione. Sono gli unici MBeans supportati per l’integrazione e l’ispezione:

* **ServiceStatistic:** Questo MBean fornisce informazioni sul nome del servizio e la relativa versione.
* **OperationStatistic:** Questo MBean fornisce le statistiche di ogni servizio del server dei moduli. Qui gli amministratori possono ottenere informazioni su un particolare servizio come il tempo di chiamata, il numero di errori e così via.

### Interfacce pubbliche ServiceStatisticMbean {#servicestatisticmbean-public-interfaces}

È possibile accedere alle seguenti interfacce pubbliche di ServiceStatistic MBean a scopo di test:

```java
 public String getServiceId();
 public int getMajorVersion();
 public int getMinorVersion();
```

### Interfacce pubbliche OperationStatisticMbean {#operationstatisticmbean-public-interfaces}

È possibile accedere alle seguenti interfacce pubbliche di OperationStatistic MBean a scopo di test:

```java
 // InvocationCount: The number of times the method is invoked.
 public long getInvocationCount();
 // InvocationStartTime: The time at which the method started to execute.
 public long getInvocationStartTime();
 // InvocationEndTime: The time at which the method finished execution.
 public long getInvocationEndTime();
 // InvocationTime: The time taken for the execution of the method.
 public long getInvocationTime();
 // LastSamplingDateTime: Convert InvocationStartTime to a formatted string
 public String getLastSamplingDateTime();
 // MaxInvocationTime: The maximum time taken for the execution of the method.
 public long getMaxInvocationTime();
 // MinInvocationTime: The minimum time taken for the execution of the method.
 public long getMinInvocationTime();
 // AverageInvocationTime: the averege execution time taken for the execution of the method.
 public double getAverageInvocationTime();
 // ExceptionCount: The number of times the method has thrown an Exception.
 public long getExceptionCount();
 // ExceptionMessage: The message of the last exception occurred.
 public String getExeptionMessage();
 public void setExceptionMessage(String errorMessage);
```

### MBean Tree &amp; Operation Statistics {#mbean-tree-operation-statistics}

Utilizzando una console JMX (JConsole), sono disponibili le statistiche di OperationStatistic MBean. Queste statistiche sono attributi di MBean e possono essere spostate nella seguente struttura gerarchica:

**MBean tree**

**Nome di dominio Adobe:** Dipende da Application Server. Se l&#39;Application Server non definisce il dominio, l&#39;impostazione predefinita è adobe.com.

**Tipo di servizio:** AdobeService è il nome utilizzato per elencare tutti i servizi.

**NomeServizioAdobe:** Nome servizio o ID servizio.

**Versione:** Versione del servizio.

**Statistiche operative**

**Ora dell&#39;intervento:** Tempo impiegato per l&#39;esecuzione del metodo. Ciò non include il momento in cui la richiesta viene serializzata, trasferita dal client al server e deserializzata.

**Conteggio delle vocazioni:** Il numero di volte in cui viene richiamato il servizio.

**Tempo medio di chiamata:** Tempo medio di tutte le chiamate eseguite dall&#39;avvio del server.

**Tempo massimo di chiamata:** La durata della chiamata più lunga eseguita dall&#39;avvio del server.

**Tempo minimo di chiamata:** Durata della chiamata più breve eseguita dall&#39;avvio del server.

**Conteggio eccezioni:** Numero di chiamate che hanno generato errori.

**Messaggio di eccezione:** Messaggio di errore dell&#39;ultima eccezione che si è verificata.

**Data ultimo campionamento:** Data dell&#39;ultima chiamata.

**Unità di tempo:** Il valore predefinito è millisecondi.

Per abilitare il monitoraggio JMX, i server applicativi in genere necessitano di alcune configurazioni. Per informazioni specifiche, consulta la documentazione del server applicazioni .

### Esempi di come configurare l&#39;accesso JMX aperto {#examples-of-how-to-set-up-open-jmx-access}

**JBoss 4.0.3/4.2.0 - configurare l&#39;avvio JVM**

Per visualizzare MBeans da JConsole, configura i parametri di avvio JVM dell&#39;application server JBoss. Assicurati che JBoss sia avviato dal file run.bat/sh.

1. Modifica il file run.bat che si trova in InstallJBoss/bin.
1. Trova la riga JAVA_OPTS e aggiungi quanto segue:

   ```shell
    -Dcom.sun.management.jmxremote -Dcom.sun.management.jmxremote.port=9088 -Dcom.sun.management.jmxremote.authenticate=false -Dcom.sun.management.jmxremote.ssl=false
   ```

**WebLogic 9.2/10 - configurare l&#39;avvio JVM**

1. Modifica il file startWebLogic.bat che si trova in `[WebLogic home]/user_projects/domains/Adobe_Live_Cycle/bin`.
1. Trova la riga JAVA_OPTS e aggiungi quanto segue:

   ```shell
    -Dcom.sun.management.jmxremote -Dcom.sun.management.jmxremote.port=9088 -Dcom.sun.management.jmxremote.authenticate=false -Dcom.sun.management.jmxremote.ssl=false
   ```

1. Riavvia WebLogic.

>[!NOTE]
>
>Per WebLogic, è possibile accedere alla MBean utilizzando il telecomando o IIOP.

**Accesso remoto a MBean**

1. Avvia JConsole per la nuova connessione e fai clic sulla scheda remota.
1. Immetti il nome host e la porta (9088, il numero specificato durante le opzioni di avvio di JVM).

**Websphere 6.1: configurare l&#39;avvio JVM**

1. In Admin Console (Application server > server1 > Process Definition > JVM), aggiungi la seguente riga nel campo Generic JVM Argument:

   ```shell
    -Djavax.management.builder.initial= -Dcom.sun.management.jmxremote
   ```

1. Aggiungi o rimuovi il commento alle tre righe seguenti nel file /opt/IBM/WebSphere/AppServer/java/jre/lib/management/management.properties (o &lt;your websphere=&quot;&quot; jre=&quot;&quot;>lib/management/management.properties):

   ```shell
    com.sun.management.jmxremote.port=9999 //any port you like, but make sure you use this port when you connect
    com.sun.management.jmxremote.authenticate=false
    com.sun.management.jmxremote.ssl=false
   ```

1. Riavvia WebSphere.
