---
title: Modalità di esecuzione
seo-title: Run Modes
description: Scopri come ottimizzare l’istanza AEM per scopi specifici utilizzando le modalità di esecuzione.
seo-description: Learn how to tune your AEM instance for specific purposes by using run modes.
uuid: 8a0c6e5c-4fae-43e2-b745-eee58f346ceb
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: 12329e26-40bc-4c94-bc60-6d9cbd01345f
feature: Configuring
exl-id: 6d03cb1d-500e-4a23-80e5-347a43dff30e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '747'
ht-degree: 1%

---

# Modalità di esecuzione{#run-modes}

Le modalità di esecuzione ti consentono di regolare la tua istanza AEM per uno scopo specifico; ad esempio autore o pubblicazione, test, sviluppo, intranet o altri.

Operazioni disponibili:

* [Definire raccolte di parametri di configurazione per ogni modalità di esecuzione](#defining-configuration-properties-for-a-run-mode).

   Viene applicato un set di parametri di configurazione di base per tutte le modalità di esecuzione, quindi è possibile regolare set aggiuntivi in base allo scopo del proprio ambiente specifico. Vengono applicate come necessario.

* [Definire i bundle aggiuntivi da installare per una particolare modalità](#defining-additional-bundles-to-be-installed-for-a-run-mode).

Tutte le impostazioni e le definizioni vengono archiviate nell&#39;unico archivio e attivate impostando il **Modalità di esecuzione**.

## Modalità di esecuzione dell&#39;installazione {#installation-run-modes}

Le modalità di esecuzione dell&#39;installazione (o fisse) vengono utilizzate al momento dell&#39;installazione e poi fissate per l&#39;intera durata dell&#39;istanza, non possono essere modificate.

Le modalità di esecuzione dell&#39;installazione sono pronte all&#39;uso:

* `author`
* `publish`
* `samplecontent`
* `nosamplecontent`

Si tratta di due coppie di modalità di esecuzione reciprocamente esclusive; ad esempio, puoi:

* o `author` o `publish`, non contemporaneamente

* combinare `author` con `samplecontent` o `nosamplecontent` (ma non entrambi)

>[!CAUTION]
>
>Quando si utilizza una delle modalità di esecuzione di cui sopra (authoring, publish, samplecontent, nosamplecontent), il valore utilizzato al momento dell&#39;installazione definisce la modalità di esecuzione per *intera vita* dell&#39;impianto.
>
>Per queste modalità di esecuzione, *impossibile* cambiali dopo l&#39;installazione.

## Modalità di esecuzione personalizzate {#customized-run-modes}

Puoi anche creare modalità di esecuzione personalizzate. Questi possono essere combinati in modo da coprire scenari quali:

* `author` + `development`

* `publish` + `test`

* `publish` + `test` + `golive`

* `publish` + `intranet`

* come richiesto . . .

È inoltre possibile selezionare modalità di esecuzione personalizzate a ogni avvio.

## Utilizzo di samplecontent e nosamplecontent {#using-samplecontent-and-nosamplecontent}

Queste modalità consentono di controllare l’uso del contenuto campione. Il contenuto di esempio viene definito prima della creazione dell’avvio rapido e può includere pacchetti, configurazioni e così via:

* La `samplecontent` la modalità di esecuzione installerà il contenuto (modalità predefinita).

* La `nosamplecontent` la modalità non installerà il contenuto di esempio.

La modalità di esecuzione nosamplecontent è progettata per le installazioni di produzione.

## Definizione delle proprietà di configurazione per una modalità di esecuzione {#defining-configuration-properties-for-a-run-mode}

È possibile salvare nell&#39;archivio una raccolta di valori per le proprietà di configurazione, utilizzate per una particolare modalità di esecuzione.

La modalità di esecuzione è indicata da un suffisso sul nome della cartella. Questo consente di memorizzare tutte le configurazioni in un unico archivio come. Esempio:

* `config`

   Applicabile per tutte le modalità di esecuzione

* `config.author`

   Utilizzato per la modalità di esecuzione dell’autore

* `config.publish`

   Utilizzato per la modalità di esecuzione di pubblicazione

* `config.<run-mode>`

   Utilizzato per la modalità di esecuzione applicabile; ad esempio, config

Vedi [Configurazione OSGi nell’archivio](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository) per ulteriori dettagli sulla definizione dei singoli nodi di configurazione all&#39;interno di queste cartelle e sulla creazione di configurazioni per combinazioni di più modalità di esecuzione.

>[!NOTE]
>
>Per [Modalità di esecuzione dell&#39;installazione](#installation-run-modes) (ad esempio, autore) la modalità di esecuzione non può essere modificata dopo l’installazione. Tuttavia, le modifiche alle singole proprietà di configurazione avranno effetto al riavvio.

## Definizione dei bundle aggiuntivi da installare per una modalità di esecuzione {#defining-additional-bundles-to-be-installed-for-a-run-mode}

È inoltre possibile specificare bundle aggiuntivi da installare per una particolare modalità di esecuzione. Per queste definizioni, le cartelle di installazione vengono utilizzate per contenere i bundle. Anche in questo caso la modalità di esecuzione è indicata da un prefisso :

* `install.author`
* `install.publish`

Queste cartelle sono di tipo `nt:folder` e deve contenere il pacchetto appropriato.

## Avvio di CQ con una modalità di esecuzione specifica {#starting-cq-with-a-specific-run-mode}

Se hai definito configurazioni per più modalità di esecuzione, devi definire quale deve essere utilizzato all&#39;avvio. Esistono diversi metodi per specificare quale modalità di esecuzione utilizzare; l&#39;ordine di risoluzione è il seguente:

1. [ ](#using-the-sling-properties-file)
1. [ ](#using-the-r-option)
1. [proprietà del sistema (](#using-a-system-property-in-the-start-script)

1. [Rilevamento nome file](#filename-detection-renaming-the-jar-file)

Quando utilizzi un server applicazioni puoi anche [definire la modalità di esecuzione in web.xml](#defining-the-run-mode-in-web-xml-with-application-server).

### Utilizzo del file sling.properties {#using-the-sling-properties-file}

La `sling.properties` può essere utilizzato per definire la modalità di esecuzione richiesta:

1. Modifica il file di configurazione:

   `<cq-installation-dir>/crx-quickstart/conf/sling.properties`

1. Aggiungi le seguenti proprietà: l’esempio seguente è per autore:

   `sling.run.modes=author`

### Utilizzo dell’opzione -r {#using-the-r-option}

Una modalità di esecuzione personalizzata può essere attivata utilizzando la variabile `-r` quando si avvia l&#39;avvio rapido. Ad esempio, utilizzare il comando seguente per avviare un&#39;istanza AEM con la modalità di esecuzione impostata su dev. &quot;

```shell
java -jar cq-56-p4545.jar -r dev
```

### Utilizzo di una proprietà di sistema nello script iniziale {#using-a-system-property-in-the-start-script}

È possibile utilizzare una proprietà di sistema nello script iniziale per specificare la modalità di esecuzione.

* Ad esempio, utilizza quanto segue per avviare un&#39;istanza come istanza di pubblicazione di produzione situata negli Stati Uniti:

   `-Dsling.run.modes=publish,prod,us`

### Rilevamento nome file - ridenominazione del file jar {#filename-detection-renaming-the-jar-file}

È possibile attivare le due seguenti modalità di esecuzione dell&#39;installazione rinominando il file jar dell&#39;installazione prima dell&#39;installazione:

* pubblicazione
* author

Il file jar deve utilizzare la convenzione di denominazione:

`cq5-<run-mode>-p<port-number>`

Ad esempio, imposta la `publish` modalità di esecuzione denominando il file jar:

`cq5-publish-p4503`

### Definizione della modalità di esecuzione in web.xml (con Application Server) {#defining-the-run-mode-in-web-xml-with-application-server}

Quando utilizzi un server applicazioni puoi anche configurare la proprietà :

`sling.run.modes`

nel file :

`WEB-INF/web.xml`

Questo è nel AEM `war` e deve essere aggiornato prima della distribuzione.

Vedi [Installazione di AEM con un server applicazioni](/help/sites-deploying/application-server-install.md) per ulteriori dettagli.
