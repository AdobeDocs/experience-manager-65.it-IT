---
title: Modalità di esecuzione
description: Scopri come ottimizzare l’istanza AEM per scopi specifici utilizzando le modalità di esecuzione.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
feature: Configuring
exl-id: 6d03cb1d-500e-4a23-80e5-347a43dff30e
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '746'
ht-degree: 1%

---

# Modalità di esecuzione{#run-modes}

Le modalità di esecuzione consentono di regolare l’istanza AEM per uno scopo specifico, ad esempio authoring o pubblicazione, test, sviluppo, Intranet o altri.

Operazioni disponibili:

* [Definire insiemi di parametri di configurazione per ogni modalità di esecuzione](#defining-configuration-properties-for-a-run-mode).

  Un set di base di parametri di configurazione viene applicato a tutte le modalità di esecuzione e puoi quindi regolare altri set in base allo scopo dell’ambiente specifico. Questi vengono applicati in base alle esigenze.

* [Definisci i bundle aggiuntivi da installare per una particolare modalità](#defining-additional-bundles-to-be-installed-for-a-run-mode).

Tutte le impostazioni e le definizioni vengono memorizzate in un unico repository e attivate impostando **Modalità di esecuzione**.

## Modalità di esecuzione dell’installazione {#installation-run-modes}

Le modalità di esecuzione dell’installazione (o fisse) vengono utilizzate al momento dell’installazione e quindi corrette per l’intera durata dell’istanza, e non possono essere modificate.

Sono disponibili modalità di esecuzione dell’installazione pronte all’uso:

* `author`
* `publish`
* `samplecontent`
* `nosamplecontent`

Si tratta di due coppie di modalità di esecuzione che si escludono a vicenda; ad esempio, è possibile:

* definisci `author` o `publish`, non entrambi contemporaneamente

* combinare `author` con `samplecontent` o `nosamplecontent` (ma non entrambi)

>[!CAUTION]
>
>Quando si utilizza una delle modalità di esecuzione di cui sopra (author, publish, samplecontent, nosamplecontent), il valore utilizzato al momento dell’installazione definisce la modalità di esecuzione per *intera durata* di tale impianto.
>
>Per queste modalità di esecuzione è possibile: *non può* modificarli dopo l&#39;installazione.

## Modalità di esecuzione personalizzate {#customized-run-modes}

Puoi anche creare modalità di esecuzione personalizzate. Queste possono essere combinate per coprire scenari quali:

* `author` + `development`

* `publish` + `test`

* `publish` + `test` + `golive`

* `publish` + `intranet`

* come richiesto . . .

Ad ogni avvio è possibile selezionare anche modalità di esecuzione personalizzate.

## Utilizzo di samplecontent e nosamplecontent {#using-samplecontent-and-nosamplecontent}

Queste modalità ti consentono di controllare l’utilizzo di contenuti di esempio. Il contenuto di esempio viene definito prima che venga generato l’avvio rapido e può includere pacchetti, configurazioni e così via:

* Il `samplecontent` modalità di esecuzione installa questo contenuto (modalità predefinita).

* Il `nosamplecontent` La modalità non installa il contenuto di esempio.

La modalità di esecuzione nosamplecontent è progettata per le installazioni di produzione.

## Definizione delle proprietà di configurazione per una modalità di esecuzione {#defining-configuration-properties-for-a-run-mode}

Un insieme di valori per le proprietà di configurazione, utilizzati per una particolare modalità di esecuzione, può essere salvato nel repository.

La modalità di esecuzione è indicata da un suffisso nel nome della cartella. Questo consente di memorizzare tutte le configurazioni in un archivio come. Ad esempio:

* `config`

  Applicabile a tutte le modalità di esecuzione

* `config.author`

  Utilizzato per la modalità di esecuzione dell’autore

* `config.publish`

  Utilizzato per la modalità di esecuzione pubblicazione

* `config.<run-mode>`

  Utilizzato per la modalità di esecuzione applicabile; ad esempio, config

Consulta [Configurazione OSGi nell’archivio](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository) per ulteriori dettagli sulla definizione dei singoli nodi di configurazione all&#39;interno di queste cartelle e sulla creazione di configurazioni per combinazioni di più modalità di esecuzione.

>[!NOTE]
>
>Per [Modalità di esecuzione dell’installazione](#installation-run-modes) (ad esempio, autore) la modalità di esecuzione non può essere modificata dopo l’installazione. Tuttavia, le modifiche alle singole proprietà di configurazione avranno effetto al riavvio.

## Definizione di bundle aggiuntivi da installare per una modalità di esecuzione {#defining-additional-bundles-to-be-installed-for-a-run-mode}

È inoltre possibile specificare bundle aggiuntivi da installare per una particolare modalità di esecuzione. Per queste definizioni, le cartelle di installazione vengono utilizzate per contenere i bundle. Anche in questo caso la modalità di esecuzione è indicata da un prefisso:

* `install.author`
* `install.publish`

Queste cartelle sono di tipo `nt:folder` e devono contenere il pacchetto appropriato.

## Avvio di CQ con una modalità di esecuzione specifica {#starting-cq-with-a-specific-run-mode}

Se sono state definite configurazioni per più modalità di esecuzione, è necessario definire quale deve essere utilizzata all&#39;avvio. Esistono diversi metodi per specificare quale modalità di esecuzione utilizzare; l’ordine di risoluzione è:

1. [proprietà di sistema (](#using-a-system-property-in-the-start-script)
1. [](#using-the-sling-properties-file)
1. [](#using-the-r-option)
1. [Rilevamento del nome file](#filename-detection-renaming-the-jar-file)

Quando si utilizza un server applicazioni è inoltre possibile [definire la modalità di esecuzione in web.xml](#defining-the-run-mode-in-web-xml-with-application-server).

### Utilizzo del file sling.properties {#using-the-sling-properties-file}

Il `sling.properties` Il file può essere utilizzato per definire la modalità di esecuzione richiesta:

1. Modifica il file di configurazione:

   `<cq-installation-dir>/crx-quickstart/conf/sling.properties`

1. Aggiungi le seguenti proprietà; l’esempio seguente è per autore:

   `sling.run.modes=author`

### Utilizzo dell&#39;opzione -r {#using-the-r-option}

È possibile attivare una modalità di esecuzione personalizzata utilizzando `-r` quando si avvia quickstart. Ad esempio, utilizza il seguente comando per avviare un’istanza AEM con la modalità di esecuzione impostata su dev. &quot;

```shell
java -jar cq-56-p4545.jar -r dev
```

### Utilizzo di una proprietà di sistema nello script iniziale {#using-a-system-property-in-the-start-script}

È possibile utilizzare una proprietà di sistema nello script di avvio per specificare la modalità di esecuzione.

* Ad esempio, utilizza quanto segue per avviare un’istanza come istanza di pubblicazione di produzione negli Stati Uniti:

  `-Dsling.run.modes=publish,prod,us`

### Rilevamento del nome file - Ridenominazione del file jar {#filename-detection-renaming-the-jar-file}

Le due modalità di esecuzione dell’installazione seguenti possono essere attivate rinominando il file jar dell’installazione prima dell’installazione:

* pubblicazione
* author

Il file jar deve utilizzare la convenzione di denominazione:

`cq5-<run-mode>-p<port-number>`

Ad esempio, imposta `publish` modalità di esecuzione denominando il file jar:

`cq5-publish-p4503`

### Definizione della modalità di esecuzione in web.xml (con Application Server) {#defining-the-run-mode-in-web-xml-with-application-server}

Quando utilizzi un server applicazioni puoi anche configurare la proprietà:

`sling.run.modes`

nel file:

`WEB-INF/web.xml`

Questo è nel AEM `war` e devono essere aggiornati prima della distribuzione.

Consulta [Installazione di AEM con un server applicazioni](/help/sites-deploying/application-server-install.md) per ulteriori dettagli.
