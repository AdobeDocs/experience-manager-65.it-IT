---
title: Monitoraggio delle distribuzioni di moduli AEM
seo-title: Monitoraggio delle distribuzioni di moduli AEM
description: È possibile monitorare le distribuzioni dei moduli AEM sia a livello di sistema che a livello interno. Ulteriori informazioni sul monitoraggio delle distribuzioni di moduli AEM da questo documento.
seo-description: È possibile monitorare le distribuzioni dei moduli AEM sia a livello di sistema che a livello interno. Ulteriori informazioni sul monitoraggio delle distribuzioni di moduli AEM da questo documento.
uuid: 032b7a93-3069-4ad5-a8c6-4c160f290669
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: b3e7bca0-5aaf-4f28-bddb-fd7e8ed72ee8
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '634'
ht-degree: 0%

---


# Monitoraggio delle distribuzioni di moduli AEM {#monitoring-aem-forms-deployments}

È possibile monitorare le distribuzioni dei moduli AEM sia a livello di sistema che a livello interno. Potete utilizzare strumenti di gestione specializzati come HP OpenView, IBM Tivoli e CA UniCenter e un monitor JMX di terze parti denominato *JConsole* per monitorare specificamente l&#39;attività Java. L&#39;implementazione di una strategia di monitoraggio migliora la disponibilità, l&#39;affidabilità e le prestazioni delle installazioni dei moduli AEM.

Per ulteriori informazioni sul monitoraggio delle distribuzioni di moduli AEM, consulta [Una guida tecnica per il monitoraggio delle distribuzioni](https://www.adobe.com/devnet/livecycle/pdfs/lc_monitoring_wp_ue.pdf)di moduli AEM.

## Monitoraggio con MBeans {#monitoring-using-mbeans}

I moduli AEM forniscono due MBeans registrati che forniscono informazioni di navigazione e statistiche. Sono gli unici MBeans supportati per l&#39;integrazione e l&#39;ispezione:

* **ServiceStatistic:** Questo MBean fornisce informazioni sul nome del servizio e sulla sua versione.
* **OperationStatistic:** Questo MBean fornisce le statistiche di ogni servizio del server dei moduli. È qui che gli amministratori possono ottenere informazioni su un particolare servizio, ad esempio ora di chiamata, numero di errori e così via.

### Interfacce pubbliche ServiceStatisticMava {#servicestatisticmbean-public-interfaces}

È possibile accedere alle seguenti interfacce pubbliche di ServiceStatistic MBean a scopo di test:

```java
 public String getServiceId();
 public int getMajorVersion();
 public int getMinorVersion();
```

### Interfacce pubbliche OperationStatisticMfava {#operationstatisticmbean-public-interfaces}

È possibile accedere a queste interfacce pubbliche di OperationStatistic MBean a scopo di test:

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

Utilizzando una console JConsole (JMX console), sono disponibili le statistiche di OperationStatistic MBean. Queste statistiche sono attributi di MBean e possono essere spostate nella seguente struttura gerarchica:

**MBean tree**

**Nome dominio Adobe:** Dipende da Application Server. Se Application Server non definisce il dominio, il valore predefinito è adobe.com.

**ServiceType:** AdobeService è il nome utilizzato per elencare tutti i servizi.

**AdobeServiceName:** Nome servizio o ID servizio.

**Versione:** Versione del servizio.

**Statistiche operazione**

**Tempo di richiamo:** Tempo necessario per l&#39;esecuzione del metodo. Ciò non include l&#39;ora in cui la richiesta viene serializzata, trasferita dal client al server e deserializzata.

**Numero di vocazioni:** Il numero di volte in cui il servizio viene richiamato.

**Tempo medio di chiamata:** Tempo medio di tutte le chiamate eseguite dall&#39;avvio del server.

**Tempo massimo di chiamata:** Durata della chiamata più lunga eseguita dall&#39;avvio del server.

**Tempo minimo di chiamata:** Durata della chiamata più breve eseguita dall&#39;avvio del server.

**Conteggio eccezioni:** Numero di chiamate che hanno generato errori.

**Messaggio eccezione:** Messaggio di errore dell&#39;ultima eccezione che si è verificata.

**Data ultima campionamento:** Data dell’ultima chiamata.

**Unità di tempo:** Il valore predefinito è millisecondi.

Per abilitare il monitoraggio JMX, i server applicazione in genere necessitano di una certa configurazione. Per informazioni specifiche, consultate la documentazione del server applicazione.

### Esempi di come impostare l&#39;accesso JMX aperto {#examples-of-how-to-set-up-open-jmx-access}

**JBoss 4.0.3/4.2.0 - configurare l&#39;avvio della JVM**

Per visualizzare gli MBeans da JConsole, configurare i parametri di avvio JVM del server applicazioni JBoss. Assicurarsi che JBoss sia avviato dal file run.bat/sh.

1. Modificate il file run.bat che si trova in InstallJBoss/bin.
1. Trovate la riga JAVA_OPTS e aggiungete quanto segue:

   ```shell
    -Dcom.sun.management.jmxremote -Dcom.sun.management.jmxremote.port=9088 -Dcom.sun.management.jmxremote.authenticate=false -Dcom.sun.management.jmxremote.ssl=false
   ```

**WebLogic 9.2 /10 - configurare l&#39;avvio JVM**

1. Modificate il file startWebLogic.bat che si trova in `[WebLogic home]/user_projects/domains/Adobe_Live_Cycle/bin`.
1. Trovate la riga JAVA_OPTS e aggiungete quanto segue:

   ```shell
    -Dcom.sun.management.jmxremote -Dcom.sun.management.jmxremote.port=9088 -Dcom.sun.management.jmxremote.authenticate=false -Dcom.sun.management.jmxremote.ssl=false
   ```

1. Riavviare WebLogic.

>[!NOTE]
>
>Per WebLogic, è possibile accedere a MBean utilizzando il telecomando o IIOP.

**Accesso remoto a MBean**

1. Avviare JConsole per una nuova connessione e fare clic sulla scheda remota.
1. Immettere il nome host e la porta (9088, il numero specificato durante le opzioni di avvio di JVM).

**Webfera 6.1 - configurare l&#39;avvio JVM**

1. Nella console di amministrazione (server applicazioni > server1 > Definizione processo > JVM), aggiungere la seguente riga al campo relativo all&#39;argomento JVM generico:

   ```shell
    -Djavax.management.builder.initial= -Dcom.sun.management.jmxremote
   ```

1. Aggiungete o rimuovete il commento dalle seguenti tre righe nel file /opt/IBM/WebSphere/AppServer/java/jre/lib/management/management.properties (o &lt;JRE_Siti Web>/ lib/management/management.properties):

   ```shell
    com.sun.management.jmxremote.port=9999 //any port you like, but make sure you use this port when you connect
    com.sun.management.jmxremote.authenticate=false
    com.sun.management.jmxremote.ssl=false
   ```

1. Riavviate WebSphere.

