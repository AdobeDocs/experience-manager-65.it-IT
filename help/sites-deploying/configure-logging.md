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
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '664'
ht-degree: 0%

---

# Registrazione{#logging}

AEM offre la possibilità di configurare:

* parametri globali per il servizio di registrazione centrale
* richiedere la registrazione dei dati; una configurazione di registrazione specializzata per le informazioni di richiesta
* impostazioni specifiche per i singoli servizi; ad esempio, un singolo file di log e un formato per i messaggi di log

Questi sono tutti [Configurazioni OSGi](/help/sites-deploying/configuring-osgi.md).

>[!NOTE]
>
>L&#39;accesso AEM è basato sui principi Sling. Vedi [Registrazione Sling](https://sling.apache.org/site/logging.html) per ulteriori informazioni.

## Registrazione globale {#global-logging}

[Configurazione della registrazione Apache Sling](/help/sites-deploying/osgi-configuration-settings.md) viene utilizzato per configurare il logger principale. Definisce le impostazioni globali per l’accesso AEM:

* livello di registrazione
* la posizione del file di log centrale
* il numero di versioni da conservare
* rotazione della versione; dimensione massima o intervallo di tempo
* il formato da utilizzare per la scrittura dei messaggi di log

>[!NOTE]
>
>Questo [Articolo della Knowledge Base](https://helpx.adobe.com/experience-manager/kb/HowToRotateRequestAndAccessLog.html) spiega come ruotare i file request.log e access.log.

## Loggers e Scrittori per servizi individuali {#loggers-and-writers-for-individual-services}

Oltre alle impostazioni di registrazione globale, AEM consente di configurare impostazioni specifiche per un singolo servizio:

* livello di registrazione specifico
* la posizione del singolo file di log
* il numero di versioni da conservare
* rotazione della versione; dimensione massima o intervallo di tempo
* il formato da utilizzare per la scrittura dei messaggi di log
* il logger (il servizio OSGi che fornisce i messaggi di log)

Questo ti consente di incanalare i messaggi di log per un singolo servizio in un file separato. Ciò può essere particolarmente utile durante lo sviluppo o i test; ad esempio, quando hai bisogno di un livello di registro maggiore per un servizio specifico.

AEM utilizza quanto segue per scrivere messaggi di log nel file:

1. Un **Servizio OSGi** (logger) scrive un messaggio di log.
1. A **Logger di registrazione** prende questo messaggio e lo formatta in base alle tue specifiche.
1. A **Registratore** scrive tutti questi messaggi nel file fisico definito.

Questi elementi sono collegati dai seguenti parametri per gli elementi appropriati:

* **Logger (logger di registrazione)**

   Definisci i servizi che generano i messaggi.

* **File di registro (logger di registrazione)**

   Definire il file fisico per la memorizzazione dei messaggi di log.

   Viene utilizzato per collegare un logger di registrazione a un Registratore di registrazione. Il valore deve essere identico allo stesso parametro nella configurazione di Logging Writer per la connessione da effettuare.

* **File di log (Registratore)**

   Definire il file fisico in cui verranno scritti i messaggi di log.

   Deve essere identico allo stesso parametro nella configurazione di Logging Writer, altrimenti la corrispondenza non verrà effettuata. Se non vi è alcuna corrispondenza, verrà creato un writer implicito con la configurazione predefinita (rotazione giornaliera del registro).

### Registratori e scrittori standard {#standard-loggers-and-writers}

Alcuni Loggers e Scrittori sono inclusi in un’installazione AEM standard.

Il primo è un caso speciale in quanto controlla sia la `request.log` e `access.log` file:

* Il logger:

   * Apache Sling Registratore dati di richiesta personalizzabile

      (org.apache.sling.engine.impl.log.RequestLoggerService)

   * Scrivi messaggi sul contenuto della richiesta in `request.log`.

* Collegamenti a:

   * Registratore di richieste Apache Sling

      (org.apache.sling.engine.impl.log.RequestLogger)

   * Scrive i messaggi in `request.log` o `access.log`.

Questi possono essere personalizzati se necessario, anche se la configurazione standard è adatta per la maggior parte delle installazioni.

Le altre coppie seguono la configurazione standard:

* Il logger:

   * Configurazione del logger di registrazione Sling di Apache

      (org.apache.sling.commons.log.LogManager.factory.config)

   * Scritture `Information` messaggi a `logs/error.log`.

* Collegamenti allo scrittore:

   * Configurazione di Apache Sling Logging Writer

      (org.apache.sling.commons.log.LogManager.factory.writer)

* Il logger:

   * Configurazione del logger di registrazione Apache Sling (org.apache.sling.commons.log.LogManager.factory.config.649d51b7-6425-45c9-81e6-2697a03d6be7)

   * Scritture `Warning` messaggi a `../logs/error.log` per il servizio `org.apache.pdfbox`.

* Non si collega a uno specifico Writer in modo da creare e utilizzare un writer implicito con configurazione predefinita (rotazione giornaliera del registro).

### Creazione di propri logger e scrittori {#creating-your-own-loggers-and-writers}

Puoi definire una coppia Logger / Writer personalizzata:

1. Crea una nuova istanza della configurazione di fabbrica [Configurazione del logger di registrazione Sling di Apache](/help/sites-deploying/osgi-configuration-settings.md).

   1. Specificare il file di registro.
   1. Specifica il logger.
   1. Configura gli altri parametri come richiesto.

1. Crea una nuova istanza della configurazione di fabbrica [Configurazione di Apache Sling Logging Writer](/help/sites-deploying/osgi-configuration-settings.md).

   1. Specifica il file di registro, che deve corrispondere a quello specificato per il logger.
   1. Configura gli altri parametri come richiesto.

>[!NOTE]
>
>In alcune circostanze è possibile creare un [file di registro personalizzato](/help/sites-deploying/monitoring-and-maintaining.md#create-a-custom-log-file).
