---
title: Registrazione
description: Scopri come configurare i parametri globali per il servizio di registrazione centrale, le impostazioni specifiche per i singoli servizi o come richiedere la registrazione dei dati.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
feature: Configuring
exl-id: b32001a1-0078-43f6-89d6-781d6d2e9c94
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: f96b178ae84b4b930b59e36d4994970682c53dbd
workflow-type: tm+mt
source-wordcount: '636'
ht-degree: 0%

---

# Registrazione{#logging}

AEM offre la possibilità di configurare:

* parametri globali per il servizio di registrazione centrale
* richiedere la registrazione dei dati; una configurazione di registrazione specializzata per le informazioni sulla richiesta
* impostazioni specifiche per i singoli servizi; ad esempio, un singolo file di registro e un formato per i messaggi di registro

Sono tutte [configurazioni OSGi](/help/sites-deploying/configuring-osgi.md).

>[!NOTE]
>
>La registrazione in AEM si basa sui principi Sling. Per ulteriori informazioni, vedere [Registrazione Sling](https://sling.apache.org/site/logging.html).

## Registrazione globale {#global-logging}

[Configurazione registrazione Sling Apache](/help/sites-deploying/osgi-configuration-settings.md) utilizzata per configurare il logger radice. Questo definisce le impostazioni globali per l’accesso ad AEM:

* livello di registrazione
* posizione del file di registro centrale
* il numero di versioni da conservare
* rotazione delle versioni; dimensione massima o intervallo di tempo
* formato da utilizzare per la scrittura dei messaggi di registro

## Logger e writer per singoli servizi {#loggers-and-writers-for-individual-services}

Oltre alle impostazioni di registrazione globali, AEM consente di configurare impostazioni specifiche per un singolo servizio:

* il livello di registrazione specifico
* posizione del singolo file di registro
* il numero di versioni da conservare
* rotazione delle versioni; dimensione massima o intervallo di tempo
* formato da utilizzare per la scrittura dei messaggi di registro
* il logger (il servizio OSGi che fornisce i messaggi di registro)

In questo modo è possibile canalizzare i messaggi di registro per un singolo servizio in un file separato. Ciò può essere particolarmente utile durante lo sviluppo o il test; ad esempio, quando è necessario un livello di registro aumentato per un servizio specifico.

AEM utilizza quanto segue per scrivere i messaggi di registro su un file:

1. Un servizio **OSGi** (logger) scrive un messaggio di registro.
1. Un **Logger** accetta questo messaggio e lo formatta in base alle tue specifiche.
1. Un **Logging Writer** scrive tutti questi messaggi nel file fisico definito.

Questi elementi sono collegati dai seguenti parametri per gli elementi appropriati:

* **Logger (Logger)**

  Definisci i servizi che generano i messaggi.

* **File di registro (Logger di registrazione)**

  Definisci il file fisico per l’archiviazione dei messaggi di registro.

  Viene utilizzato per collegare un Logger con un Logger. Il valore deve essere identico allo stesso parametro nella configurazione di Logging Writer per la connessione da effettuare.

* **File di log (Logging Writer)**

  Definisci il file fisico in cui verranno scritti i messaggi del registro.

  Questo deve essere identico allo stesso parametro nella configurazione di Logging Writer, altrimenti la corrispondenza non verrà effettuata. Se non viene trovata alcuna corrispondenza, verrà creato un writer implicito con la configurazione predefinita (rotazione giornaliera del registro).

### Logger e writer standard {#standard-loggers-and-writers}

Alcuni logger e writer sono inclusi in un’installazione standard di AEM.

Il primo è un caso speciale in quanto controlla sia i file `request.log` che `access.log`:

* Logger:

   * Registratore dati di richieste personalizzabili Apache Sling

     (org.apache.sling.engine.impl.log.RequestLoggerService)

   * Scrivere messaggi sul contenuto della richiesta a `request.log`.

* Collegamenti a:

   * Logger richieste Apache Sling

     (org.apache.sling.engine.impl.log.RequestLogger)

   * Scrive i messaggi in `request.log` o `access.log`.

Questi possono essere personalizzati se necessario, anche se la configurazione standard è adatta per la maggior parte delle installazioni.

Le altre coppie seguono la configurazione standard:

* Logger:

   * Configurazione logger registrazione Sling Apache

     (org.apache.sling.commons.log.LogManager.factory.config)

   * Scrive `Information` messaggi in `logs/error.log`.

* Collegamenti a Writer:

   * Configurazione di Apache Sling Logging Writer

     (org.apache.sling.commons.log.LogManager.factory.writer)

* Logger:

   * Configurazione logger registrazione Sling Apache
(org.apache.sling.commons.log.LogManager.factory.config.649d51b7-6425-45c9-81e6-2697a03d6be7)

   * Scrive `Warning` messaggi in `../logs/error.log` per il servizio `org.apache.pdfbox`.

* Non è collegato a un processo di scrittura specifico, pertanto creerà e utilizzerà un processo di scrittura implicito con configurazione predefinita (rotazione giornaliera del registro).

### Creazione di logger e autori personalizzati {#creating-your-own-loggers-and-writers}

Puoi definire una tua coppia Logger/Writer:

1. Creare un&#39;istanza della configurazione di fabbrica [configurazione del logger di registrazione Sling Apache](/help/sites-deploying/osgi-configuration-settings.md).

   1. Specificare il file di registro.
   1. Specifica il logger.
   1. Configura gli altri parametri come richiesto.

1. Creare un&#39;istanza della configurazione di fabbrica [configurazione del writer di registrazione Sling di Apache](/help/sites-deploying/osgi-configuration-settings.md).

   1. Specifica il file di registro, che deve corrispondere a quello specificato per il logger.
   1. Configura gli altri parametri come richiesto.

>[!NOTE]
>
>In determinate circostanze è possibile creare un [file di registro personalizzato](/help/sites-deploying/monitoring-and-maintaining.md#create-a-custom-log-file).
