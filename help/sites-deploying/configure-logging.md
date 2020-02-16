---
title: Registrazione
seo-title: Registrazione
description: Scoprite come configurare i parametri globali per il servizio di registrazione centrale, le impostazioni specifiche per i singoli servizi o come richiedere la registrazione dei dati.
seo-description: Scoprite come configurare i parametri globali per il servizio di registrazione centrale, le impostazioni specifiche per i singoli servizi o come richiedere la registrazione dei dati.
uuid: 8c9e3628-2f2c-445d-9706-5c7725b85fe2
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: 5aa69b10-2cd0-4d34-8104-8c3b88405926
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Registrazione{#logging}

AEM offre la possibilità di configurare:

* parametri globali per il servizio di registrazione centrale
* richiedere la registrazione dei dati; una configurazione di registrazione specializzata per le informazioni di richiesta
* impostazioni specifiche per i singoli servizi; ad esempio, un singolo file di registro e un formato per i messaggi di registro

Sono tutte configurazioni [](/help/sites-deploying/configuring-osgi.md)OSGi.

>[!NOTE]
>
>L’accesso in AEM è basato sui principi Sling. Per ulteriori informazioni, consultate Registrazione [Sling](https://sling.apache.org/site/logging.html) .

## Registrazione globale {#global-logging}

[La configurazione](/help/sites-deploying/osgi-configuration-settings.md) Apache Sling Logging viene utilizzata per configurare il logger radice. Definisce le impostazioni globali per l’accesso in AEM:

* livello di registrazione
* posizione del file di registro centrale
* il numero di versioni da conservare
* rotazione della versione; dimensione massima o intervallo di tempo
* il formato da utilizzare per la scrittura dei messaggi di registro

>[!NOTE]
>
>Questo articolo [della](https://helpx.adobe.com/experience-manager/kb/HowToRotateRequestAndAccessLog.html) Knowledge Base spiega come ruotare i file request.log e access.log.

## Loggers e scrittori per servizi individuali {#loggers-and-writers-for-individual-services}

Oltre alle impostazioni di registrazione globali, AEM consente di configurare impostazioni specifiche per un singolo servizio:

* il livello di registrazione specifico
* il percorso del singolo file di registro
* il numero di versioni da conservare
* rotazione della versione; dimensione massima o intervallo di tempo
* il formato da utilizzare per la scrittura dei messaggi di registro
* logger (il servizio OSGi che fornisce i messaggi di registro)

Questo consente di canalizzare i messaggi di registro per un singolo servizio in un file separato. Ciò può essere particolarmente utile durante lo sviluppo o i test; ad esempio, quando è necessario un livello di registro maggiore per un servizio specifico.

AEM utilizza i seguenti strumenti per scrivere messaggi di registro nel file:

1. Un servizio **** OSGi (logger) scrive un messaggio di registro.
1. Un **Registratore** di registrazione riceve questo messaggio e lo formatta in base alle specifiche dell’utente.
1. Un **utente che esegue la registrazione** scrive tutti questi messaggi nel file fisico definito.

Questi elementi sono collegati dai seguenti parametri per gli elementi appropriati:

* **Logger (Logging)**

   Definire i servizi che generano i messaggi.

* **File di registro (Logging Logger)**

   Definire il file fisico per la memorizzazione dei messaggi di registro.

   Viene utilizzato per collegare un Registratore di registrazione a un Registratore di registrazione. Per stabilire la connessione, il valore deve essere identico allo stesso parametro nella configurazione di Log Writer.

* **File di registro (Writer di registrazione)**

   Definire il file fisico in cui verranno scritti i messaggi di registro.

   Deve essere identico allo stesso parametro nella configurazione di Logging Writer, altrimenti la corrispondenza non verrà effettuata. Se non esiste alcuna corrispondenza, verrà creato un Writer implicito con configurazione predefinita (rotazione del registro giornaliera).

### Registratori e scrittori standard {#standard-loggers-and-writers}

Alcuni logger e autori sono inclusi in un’installazione standard di AEM.

Il primo è un caso speciale in quanto controlla sia i `request.log` file che i `access.log` file:

* Registratore:

   * Apache Sling Custom Request Data Logger

      (org.apache.sling.Engine.impl.log.RequestLoggerService)

   * Scrivete messaggi sul contenuto della richiesta a `request.log`.

* Collegamenti a:

   * Registratore di richieste Apache Sling

      (org.apache.sling.Engine.impl.log.RequestLogger)

   * Scrive i messaggi in `request.log` o `access.log`.

Questi possono essere personalizzati se necessario, anche se la configurazione standard è adatta per la maggior parte delle installazioni.

Le altre coppie seguono la configurazione standard:

* Registratore:

   * Configurazione Del Registratore Di Registrazione Apache Sling

      (org.apache.sling.commons.log.LogManager.factory.config)

   * Scrive `Information` messaggi in `logs/error.log`.

* Collegamenti allo scrittore:

   * Configurazione dello scrittore di registrazione Apache Sling

      (org.apache.sling.commons.log.LogManager.factory.writer)

* Registratore:

   * Configurazione del logger di registrazione Apache Sling(org.apache.sling.commons.log.LogManager.factory.config.649d51b7-6425-45c9-81e6-2697a03d6be7)

   * Scrive `Warning` messaggi in `../logs/error.log` per il servizio `org.apache.pdfbox`.

* Non si collega a uno specifico Writer in modo da creare e utilizzare un Writer implicito con configurazione predefinita (rotazione del registro giornaliera).

### Creazione di registri e scrittori personalizzati {#creating-your-own-loggers-and-writers}

Puoi definire la tua coppia Logger/Writer:

1. Create una nuova istanza della configurazione [Apache Sling Logging Logging Configuration](/help/sites-deploying/osgi-configuration-settings.md).

   1. Specificate il file di registro.
   1. Specificate il logger.
   1. Configurate gli altri parametri come necessario.

1. Create una nuova istanza della configurazione [Apache Sling Logging Writer Configuration](/help/sites-deploying/osgi-configuration-settings.md).

   1. Specificare il file di registro. Deve corrispondere a quello specificato per il logger.
   1. Configurate gli altri parametri come necessario.

>[!NOTE]
>
>In alcune circostanze è possibile creare un file [di registro](/help/sites-deploying/monitoring-and-maintaining.md#create-a-custom-log-file)personalizzato.

