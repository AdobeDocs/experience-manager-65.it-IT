---
title: Configurazione di OSGi
description: OSGi è un elemento fondamentale nello stack tecnologico di Adobe Experience Manager (AEM). Viene utilizzato per controllare i bundle compositi dell'AEM e la loro configurazione. Questo articolo descrive come gestire le impostazioni di configurazione per tali bundle.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
feature: Configuring
exl-id: 5ecd09a3-c4be-4361-9816-03106435346f
source-git-commit: f349c8fd9c370ba589d217cd3b1d0521ae5c5597
workflow-type: tm+mt
source-wordcount: '1954'
ht-degree: 0%

---

# Configurazione di OSGi{#configuring-osgi}

[OSGi](https://www.osgi.org/) è un elemento fondamentale nello stack tecnologico di Adobe Experience Manager (AEM). Viene utilizzato per controllare i bundle compositi dell&#39;AEM e la loro configurazione.

OSGi &quot;*fornisce le primitive standardizzate che consentono di creare applicazioni a partire da componenti di piccole dimensioni, riutilizzabili e collaborativi. Questi componenti possono essere composti in un’applicazione e distribuiti*&quot;.

In questo modo è possibile gestire facilmente i bundle che possono essere arrestati, installati e avviati singolarmente. Le interdipendenze vengono gestite automaticamente. Ogni componente OSGi (vedi [Specifiche OSGi](https://docs.osgi.org/specification/)) è contenuto in uno dei vari bundle.

Puoi gestire le impostazioni di configurazione per tali bundle:

* utilizzando [Console web di Adobe CQ](#osgi-configuration-with-the-web-console)
* utilizzo [file di configurazione](#osgi-configuration-with-configuration-files)
* configurazione [content-nodes ( `sling:OsgiConfig`) nel repository](#osgi-configuration-in-the-repository)

Entrambi i metodi possono essere utilizzati anche se ci sono sottili differenze, principalmente in relazione a [Modalità di esecuzione](/help/sites-deploying/configure-runmodes.md):

* [Console web di Adobe CQ](#osgi-configuration-with-the-web-console)

   * La console web è l’interfaccia standard per la configurazione OSGi. Fornisce un’interfaccia utente per la modifica delle varie proprietà, dove è possibile selezionare i valori possibili dagli elenchi predefiniti.

     In quanto tale, è il metodo più semplice da utilizzare.

   * Tutte le configurazioni effettuate con la console web vengono applicate immediatamente e sono applicabili all’istanza corrente, indipendentemente dalla modalità di esecuzione corrente o da eventuali modifiche successive.

* [file di configurazione](#osgi-configuration-with-configuration-files)

   * Contengono le impostazioni definite nella console web.
   * Può essere incluso nei pacchetti di contenuti per l’utilizzo in altre istanze.

* [content-nodes (sling:osgiConfig) nell’archivio](#osgi-configuration-in-the-repository)

   * Richiede la configurazione manuale con CRXDE Liti.
   * A causa delle convenzioni di denominazione `sling:OsgiConfig` è possibile collegare la configurazione a uno specifico [modalità di esecuzione](/help/sites-deploying/configure-runmodes.md). Puoi anche salvare le configurazioni per più di una modalità di esecuzione nello stesso archivio.
   * Tutte le configurazioni appropriate vengono applicate immediatamente (a seconda della modalità di esecuzione).

Indipendentemente dal metodo utilizzato, tutti i metodi di configurazione seguenti:

* Assicurarsi che la copia o la replica del contenuto dell&#39;archivio ricrei configurazioni identiche.
* Consente di estrarre le configurazioni in FileVault o Subversion per motivi di sicurezza o per ulteriori aggiornamenti.
* Possono essere salvate in pacchetti da utilizzare per la configurazione di altre istanze.
* Consente di eseguire i rollout di configurazione utilizzando script per propagare i dettagli di configurazione.

>[!NOTE]
>
>I dettagli di alcune impostazioni importanti sono elencati in [Impostazioni configurazione OSGi.](/help/sites-deploying/osgi-configuration-settings.md)

## Configurazione OSGi con la console web {#osgi-configuration-with-the-web-console}

Il [Console web](/help/sites-deploying/web-console.md) in AEM fornisce un’interfaccia standardizzata per la configurazione dei bundle. Il **Configurazione** La scheda viene utilizzata per configurare i bundle OSGi ed è quindi il meccanismo sottostante per configurare i parametri del sistema AEM.

Tutte le modifiche apportate vengono immediatamente applicate alla configurazione OSGi pertinente, non è necessario riavviare il sistema.

>[!NOTE]
>
>Le modifiche apportate nella console web vengono salvate nell’archivio come [file di configurazione](#osgi-configuration-with-configuration-files). Questi file possono essere inclusi nei pacchetti di contenuti per essere riutilizzati in ulteriori installazioni.

>[!NOTE]
>
>Nella console Web, tutte le descrizioni che menzionano le impostazioni predefinite si riferiscono alle impostazioni predefinite di Sling.
>
>Adobe Experience Manager dispone di proprie impostazioni predefinite; pertanto, le impostazioni predefinite impostate potrebbero essere diverse da quelle documentate nella console.

Per aggiornare una configurazione con la console web:

1. Accedere a **Configurazione** della console Web:

   * Apertura della console web dal collegamento **Strumento > Operazioni** menu. Dopo l’accesso alla console, puoi utilizzare il menu a discesa di:

     **OSGi >**

   * L’URL diretto; ad esempio:

     `http://localhost:4502/system/console/configMgr`

   Viene visualizzato un elenco.

1. Seleziona il bundle da configurare effettuando una delle seguenti operazioni:

   * clic su **Modifica** icona per il bundle
   * clic su **Nome** del bundle

1. Viene visualizzata una finestra di dialogo. Qui puoi modificare in base alle esigenze. Ad esempio, imposta **Livello registro** a `INFO`:

   ![chlimage_1-140](assets/chlimage_1-140.png)

   >[!NOTE]
   >
   >Gli aggiornamenti vengono salvati nell’archivio come [file di configurazione](#osgi-configuration-with-configuration-files). Per individuare questi file in un secondo momento e includerli in un pacchetto di contenuti da utilizzare in un’altra istanza, ad esempio, annota l’identità persistente ( `PID`).

1. Fai clic su **Salva**.

   Le modifiche vengono immediatamente applicate alla configurazione OSGi pertinente del sistema in esecuzione, non è necessario riavviare il sistema.

   >[!NOTE]
   >
   >Ora puoi individuare i relativi [file di configurazione](#osgi-configuration-with-configuration-files). Ad esempio, per includere in un pacchetto di contenuti per l’utilizzo in un’altra istanza.

## Configurazione OSGi con file di configurazione {#osgi-configuration-with-configuration-files}

Le modifiche apportate alla configurazione utilizzando la console Web vengono mantenute nell&#39;archivio come file di configurazione ( `.config`) in:

`/apps`

Questi file possono essere inclusi nei pacchetti di contenuti e riutilizzati in altre istanze.

>[!NOTE]
>
>Il formato dei file di configurazione è specifico. Consulta la documentazione di Sling Apache per:
>* dettagli completi di [Apache Sling Provisioning Model e Apache SlingStart](https://sling.apache.org/documentation/development/slingstart.html#default-configuration-format).
>* esercitazioni ed esempi di [Recupero risorse e proprietà in Sling](https://sling.apache.org/documentation/tutorials-how-tos/getting-resources-and-properties-in-sling.html).
>
>Per questo motivo, si consiglia di creare e gestire il file di configurazione apportando modifiche effettive nella console web.

La console Web non mostra alcuna indicazione sulla posizione in cui sono state salvate le modifiche nell’archivio, ma è possibile individuarle facilmente:

1. Creare il file di configurazione [modifica iniziale nella console web](#osgi-configuration-with-the-web-console).
1. Apri CRXDE Liti.
1. In **Strumenti** menu, seleziona **Query...** .
1. Per cercare il PID della configurazione aggiornata, invia una query di **Tipo** `SQL`.

   Ad esempio: **Console di gestione Apache Felix OSGi** presenta l’identità persistente (PID) di:

   `org.apache.felix.webconsole.internal.servlet.OsgiManager`

   Pertanto, la query SQL potrebbe essere:

   ```shell
   select * from nt:base where jcr:path like '/apps/%' and contains(*, 'org.apache.felix.webconsole.internal.servlet.OsgiManager')
   ```

1. Viene visualizzato il nodo del file di configurazione.

   Per l’esempio precedente:

   `/apps/system/config/org.apache.felix.webconsole.internal.servlet.OsgiManager.config`

   >[!CAUTION]
   >
   >Puoi aprire questo file per visualizzare le modifiche, ma per evitare errori di digitazione si consiglia di apportare modifiche effettive con la console.

1. Ora puoi creare un pacchetto di contenuti contenente questo nodo e utilizzarlo come richiesto sulle altre istanze.

## Configurazione OSGi nell’archivio {#osgi-configuration-in-the-repository}

Oltre a utilizzare la console web, puoi anche definire i dettagli di configurazione nell’archivio. In questo modo è possibile configurare facilmente le diverse modalità di esecuzione.

Queste configurazioni vengono effettuate creando `sling:OsgiConfig` nodi nell’archivio a cui il sistema deve fare riferimento. Questi nodi rispecchiano le configurazioni OSGi e a essi viene creata un’interfaccia utente. Per aggiornare i dati di configurazione, devi aggiornare le proprietà del nodo.

Se modifichi i dati di configurazione nell’archivio, le modifiche vengono immediatamente applicate alla configurazione OSGi pertinente. È come se le modifiche fossero state apportate utilizzando la console Web, con i controlli di convalida e coerenza appropriati. Questo flusso di lavoro si applica anche all’azione di copia di una configurazione da `/libs/` a `/apps/`.

Poiché lo stesso parametro di configurazione si trova in più posizioni, il sistema:

* cerca tutti i nodi di tipo `sling:OsgiConfig`
* filtri in base al nome del servizio
* filtri in base alla modalità di esecuzione

>[!NOTE]
>
>Leggi anche [come definire una configurazione basata su archivio solo per una specifica istanza](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17500.html).

### Aggiunta di una nuova configurazione all’archivio {#adding-a-new-configuration-to-the-repository}

#### Cosa è necessario sapere {#what-you-need-to-know}

Per aggiungere una configurazione all’archivio, è necessario conoscere quanto segue:

1. Il **Identità persistente** (PID) del servizio.

   Fai riferimento a **Configurazioni** nella console Web. Il nome viene visualizzato tra parentesi dopo il nome del bundle (o nella **Informazioni di configurazione** verso il fondo della pagina).

   Ad esempio, crea un nodo `com.day.cq.wcm.core.impl.VersionManagerImpl.` da configurare **Gestione versioni WCM AEM**.

   ![chlimage_1-141](assets/chlimage_1-141.png)

1. È un valore specifico [modalità di esecuzione](/help/sites-deploying/configure-runmodes.md) richiesto? Crea la cartella:

   * `config` - per tutte le modalità di esecuzione
   * `config.author` - per l’ambiente di authoring
   * `config.publish` - per l’ambiente di pubblicazione
   * `config.<run-mode>` - se del caso

1. È un **Configurazione** o **Configurazione factory** necessario?
1. I singoli parametri da configurare, comprese le definizioni di parametri esistenti che devono essere ricreati.

   Fai riferimento al singolo campo dei parametri nella console Web. Il nome viene visualizzato tra parentesi per ciascun parametro.

   Ad esempio, crea una proprietà
   `versionmanager.createVersionOnActivation` da configurare **Crea versione all&#39;attivazione**.

   ![chlimage_1-142](assets/chlimage_1-142.png)

1. Esiste una configurazione in `/libs`? Per elencare tutte le configurazioni nell’istanza, utilizza **Query** in CRXDE Liti per inviare la seguente query SQL:

   `select * from sling:OsgiConfig`

   In tal caso, questa configurazione può essere copiata in ` /apps/<yourProject>/`, quindi personalizzato nella nuova posizione.

#### Creazione della configurazione nel repository {#creating-the-configuration-in-the-repository}

Per aggiungere effettivamente la nuova configurazione all’archivio:

1. Utilizza CRXDE Liti per passare a:

   ` /apps/<yourProject>`

1. Se non esiste, crea `config` cartella ( `sling:Folder`):

   * `config` - applicabile a tutte le modalità di funzionamento
   * `config.<run-mode>` - specifico per una particolare modalità di esecuzione

1. In questa cartella, crea un nodo:

   * Tipo: `sling:OsgiConfig`
   * Nome: identità persistente (PID);

     ad esempio, per l’utilizzo di Gestione versioni WCM AEM `com.day.cq.wcm.core.impl.VersionManagerImpl`

   >[!NOTE]
   >
   >Quando si aggiunge una configurazione di fabbrica `-<identifier>` al nome.
   >
   >Come in: `org.apache.sling.commons.log.LogManager.factory.config-<identifier>`
   >
   >Dove `<identifier>` viene sostituito da testo libero che è necessario immettere per identificare l&#39;istanza (non è possibile omettere queste informazioni); ad esempio:
   >
   >`org.apache.sling.commons.log.LogManager.factory.config-MINE`

1. Per ogni parametro da configurare, crea una proprietà su questo nodo:

   * Nome: il nome del parametro come mostrato nella console Web; il nome viene visualizzato tra parentesi alla fine della descrizione del campo. Ad esempio, per `Create Version on Activation` utilizzare `versionmanager.createVersionOnActivation`
   * Tipo: a seconda dei casi.
   * Valore: come richiesto.

   È necessario creare solo le proprietà per i parametri che si desidera configurare, mentre per gli altri parametri vengono comunque utilizzati i valori predefiniti impostati dall&#39;AEM.

1. Salva tutte le modifiche.

   Le modifiche vengono applicate quando il nodo viene aggiornato riavviando il servizio (come con le modifiche apportate nella console Web).

>[!CAUTION]
>
>Non modificare nulla nella `/libs` percorso.

>[!CAUTION]
>
>Il percorso completo di una configurazione deve essere corretto per essere letto all&#39;avvio.

## Dettagli configurazione {#configuration-details}

### Ordine di risoluzione all&#39;avvio {#resolution-order-at-startup}

Viene utilizzato il seguente ordine di precedenza:

1. Nodi dell’archivio in `/apps/*/config...`.con tipo `sling:OsgiConfig` o di proprietà.

1. Nodi archivio con tipo `sling:OsgiConfig` in `/libs/*/config...`. (definizioni predefinite).

1. Qualsiasi `.config` file da `<*cq-installation-dir*>/crx-quickstart/launchpad/config/...`. sul file system locale.

Una configurazione generica in `/libs` possono essere nascosti da una configurazione specifica del progetto in `/apps`.

### Ordine di risoluzione in fase di esecuzione {#resolution-order-at-runtime}

Le modifiche apportate alla configurazione durante l&#39;esecuzione del sistema attivano un ricaricamento con la configurazione modificata.

Si applica quindi il seguente ordine di precedenza:

1. La modifica di una configurazione nella console web ha effetto immediato in quanto ha la precedenza in fase di esecuzione.
1. Modifica di una configurazione in `/apps` ha effetto immediato.
1. Modifica di una configurazione in `/libs` ha effetto immediato, a meno che non venga nascosto da una configurazione in `/apps`.

### Risoluzione di più modalità di esecuzione {#resolution-of-multiple-run-modes}

Per le configurazioni specifiche della modalità di esecuzione, è possibile combinare più modalità di esecuzione. Ad esempio, puoi creare cartelle di configurazione con lo stile seguente:

`/apps/*/config.<runmode1>.<runmode2>/`

Le configurazioni in tali cartelle vengono applicate se tutte le modalità di esecuzione corrispondono a una modalità di esecuzione definita all&#39;avvio.

Ad esempio, se un’istanza è stata avviata con le modalità di esecuzione `author,dev,emea`, nodi di configurazione in `/apps/*/config.emea`, `/apps/*/config.author.dev/`, e `/apps/*/config.author.emea.dev/` viene applicato, mentre i nodi di configurazione in `/apps/*/config.author.asean/` e `/config/author.dev.emea.noldap/` non vengono applicati.

Se sono applicabili più configurazioni per lo stesso PID, viene applicata la configurazione con il maggior numero di modalità di esecuzione corrispondenti.

Ad esempio, se un’istanza è stata avviata con le modalità di esecuzione `author,dev,emea`, ed entrambi `/apps/*/config.author/` e `/apps/*/config.emea.author/` definire una configurazione per
`com.day.cq.wcm.core.impl.VersionManagerImpl`, la configurazione in `/apps/*/config.emea.author/` viene applicata.

La granularità di questa regola è a livello PID.
Impossibile definire alcune proprietà per lo stesso PID in `/apps/*/config.author/` e più specifici in `/apps/*/config.emea.author/` per lo stesso PID.
La configurazione con il maggior numero di modalità di esecuzione corrispondenti è valida per l’intero PID.

### Configurazioni standard {#standard-configurations}

L’elenco seguente mostra una piccola selezione delle configurazioni disponibili (in un’installazione standard) nell’archivio:

* Autore - Filtro WCM AEM:

  `libs/wcm/core/config.author/com.day.cq.wcm.core.WCMRequestFilter`

* Pubblicazione - Filtro WCM AEM:

  `libs/wcm/core/config.publish/com.day.cq.wcm.core.WCMRequestFilter`

* Pubblicazione - Statistiche pagina WCM AEM:

  `libs/wcm/core/config.publish/com.day.cq.wcm.core.stats.PageViewStatistics`

>[!NOTE]
>
>Poiché queste configurazioni risiedono in `/libs` non devono essere modificati direttamente, ma copiati nell&#39;area dell&#39;applicazione ( `/apps`) prima della personalizzazione.

Per elencare tutti i nodi di configurazione nell’istanza, utilizza **Query** funzionalità di CRXDE Liti per inviare la seguente query SQL:

`select * from sling:OsgiConfig`

### Persistenza della configurazione {#configuration-persistence}

* Se modifichi una configurazione tramite la console web, questa viene (in genere) scritta nell’archivio in:

  `/apps/{somewhere}`

   * Per impostazione predefinita `{somewhere}` è `system/config` in modo che la configurazione venga scritta in

     `/apps/system/config`

   * Tuttavia, se stai modificando una configurazione che proviene inizialmente da un’altra posizione nell’archivio, ad esempio:

     /libs/foo/config/someconfig

     La configurazione aggiornata viene quindi scritta nella posizione originale; ad esempio:

     `/apps/foo/config/someconfig`

* Impostazioni modificate da `admin` sono salvati in `*.config` file in:

  ```
     /crx-quickstart/launchpad/config
  ```

   * Questa area contiene i dati privati dell’amministratore della configurazione OSGi e tutti i dettagli di configurazione specificati da `admin`, indipendentemente da come sono entrati nel sistema.
   * Quest’area è un dettaglio di implementazione e non devi mai modificare direttamente questa directory.
   * Tuttavia, è utile conoscere la posizione di questi file di configurazione in modo che possano essere eseguite copie per il backup, più installazioni o entrambe:

      * Console di gestione Apache Felix OSGi

        `../crx/org/apache/felix/webconsole/internal/servlet/OsgiManager.config`

      * Archivio client CRX Sling

        `../com/day/crx/sling/client/impl/CRXSlingClientRepository/<pid-nr>.config`

>[!CAUTION]
>
>Non modificare mai le cartelle o i file in:
>
>`/crx-quickstart/launchpad/config`
