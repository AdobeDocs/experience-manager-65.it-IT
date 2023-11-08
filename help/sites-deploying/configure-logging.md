---
title: Registrazione
seo-title: Logging
description: Scopri come configurare i parametri globali per il servizio di registrazione centrale, le impostazioni specifiche per i singoli servizi o come richiedere la registrazione dei dati.
seo-description: Learn how to configure global parameters for the central logging service, specific settings for the individual services or how to request data logging.
uuid: 8c9e3628-2f2c-445d-9706-5c7725b85fe2
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: 5aa69b10-2cd0-4d34-8104-8c3b88405926
feature: Configuring
exl-id: b32001a1-0078-43f6-89d6-781d6d2e9c94
source-git-commit: 941e5d7574d31622f50e50e717c21cd2eba2e602
workflow-type: tm+mt
source-wordcount: '660'
ht-degree: 0%

---

# Registrazione{#logging}

L’AEM ti offre la possibilità di configurare:

* parametri globali per il servizio di registrazione centrale
* richiedere la registrazione dei dati; una configurazione di registrazione specializzata per le informazioni sulla richiesta
* impostazioni specifiche per i singoli servizi; ad esempio, un singolo file di registro e un formato per i messaggi di registro

Questi sono tutti [Configurazioni OSGi](/help/sites-deploying/configuring-osgi.md).

>[!NOTE]
>
>La registrazione in AEM si basa sui principi Sling. Consulta [Sling Logging](https://sling.apache.org/site/logging.html) per ulteriori informazioni.

## Registrazione globale {#global-logging}

[Configurazione registrazione Apache Sling](/help/sites-deploying/osgi-configuration-settings.md) viene utilizzato per configurare il logger radice. Questo definisce le impostazioni globali per l’accesso all’AEM:

* livello di registrazione
* posizione del file di registro centrale
* il numero di versioni da conservare
* rotazione delle versioni; dimensione massima o intervallo di tempo
* formato da utilizzare per la scrittura dei messaggi di registro

>[!NOTE]
>
>Questo [Articolo della Knowledge Base](https://helpx.adobe.com/experience-manager/kb/HowToRotateRequestAndAccessLog.html) spiega come ruotare i file request.log e access.log.

## Logger e writer per singoli servizi {#loggers-and-writers-for-individual-services}

Oltre alle impostazioni di registrazione globali, AEM consente di configurare impostazioni specifiche per un singolo servizio:

* il livello di registrazione specifico
* posizione del singolo file di registro
* il numero di versioni da conservare
* rotazione delle versioni; dimensione massima o intervallo di tempo
* formato da utilizzare per la scrittura dei messaggi di registro
* il logger (il servizio OSGi che fornisce i messaggi di registro)

In questo modo è possibile canalizzare i messaggi di registro per un singolo servizio in un file separato. Ciò può essere particolarmente utile durante lo sviluppo o il test; ad esempio, quando è necessario un livello di registro aumentato per un servizio specifico.

AEM utilizza quanto segue per scrivere i messaggi di registro nel file:

1. Un **Servizio OSGi** (logger) scrive un messaggio di registro.
1. A **Logger di registrazione** prende questo messaggio e lo formatta in base alle tue specifiche.
1. A **Registratore** scrive tutti questi messaggi nel file fisico definito.

Questi elementi sono collegati dai seguenti parametri per gli elementi appropriati:

* **Logger (Logger)**

  Definisci i servizi che generano i messaggi.

* **File di registro (Logger)**

  Definisci il file fisico per l’archiviazione dei messaggi di registro.

  Viene utilizzato per collegare un Logger con un Logger. Il valore deve essere identico allo stesso parametro nella configurazione di Logging Writer per la connessione da effettuare.

* **File di registro (Logging Writer)**

  Definisci il file fisico in cui verranno scritti i messaggi del registro.

  Questo deve essere identico allo stesso parametro nella configurazione di Logging Writer, altrimenti la corrispondenza non verrà effettuata. Se non viene trovata alcuna corrispondenza, verrà creato un writer implicito con la configurazione predefinita (rotazione giornaliera del registro).

### Logger e writer standard {#standard-loggers-and-writers}

Alcuni Logger e Writer sono inclusi in un&#39;installazione AEM standard.

Il primo è un caso speciale in quanto controlla sia `request.log` e `access.log` file:

* Logger:

   * Registratore dati di richieste personalizzabili Apache Sling

     (org.apache.sling.engine.impl.log.RequestLoggerService)

   * Scrivi messaggi sul contenuto della richiesta a `request.log`.

* Collegamenti a:

   * Logger richieste Apache Sling

     (org.apache.sling.engine.impl.log.RequestLogger)

   * Scrive i messaggi in uno dei due modi `request.log` o `access.log`.

Questi possono essere personalizzati se necessario, anche se la configurazione standard è adatta per la maggior parte delle installazioni.

Le altre coppie seguono la configurazione standard:

* Logger:

   * Configurazione logger registrazione Sling Apache

     (org.apache.sling.commons.log.LogManager.factory.config)

   * Scritture `Information` messaggi a `logs/error.log`.

* Collegamenti a Writer:

   * Configurazione di Apache Sling Logging Writer

     (org.apache.sling.commons.log.LogManager.factory.writer)

* Logger:

   * Configurazione del logger di registrazione Apache Sling (org.apache.sling.commons.log.LogManager.factory.config.649d51b7-6425-45c9-81e6-2697a03d6be7)

   * Scritture `Warning` messaggi a `../logs/error.log` per il servizio `org.apache.pdfbox`.

* Non è collegato a un processo di scrittura specifico, pertanto creerà e utilizzerà un processo di scrittura implicito con configurazione predefinita (rotazione giornaliera del registro).

### Creazione di logger e autori personalizzati {#creating-your-own-loggers-and-writers}

Puoi definire una tua coppia Logger/Writer:

1. Creare un&#39;istanza della configurazione di fabbrica [Configurazione logger registrazione Sling Apache](/help/sites-deploying/osgi-configuration-settings.md).

   1. Specificare il file di registro.
   1. Specifica il logger.
   1. Configura gli altri parametri come richiesto.

1. Creare un&#39;istanza della configurazione di fabbrica [Configurazione di Apache Sling Logging Writer](/help/sites-deploying/osgi-configuration-settings.md).

   1. Specifica il file di registro, che deve corrispondere a quello specificato per il logger.
   1. Configura gli altri parametri come richiesto.

>[!NOTE]
>
>In alcune circostanze potrebbe essere utile creare un’ [file di registro personalizzato](/help/sites-deploying/monitoring-and-maintaining.md#create-a-custom-log-file).
