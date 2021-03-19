---
title: Configurazione di OSGi
seo-title: Configurazione di OSGi
description: OSGi è un elemento fondamentale nello stack tecnologico di Adobe Experience Manager (AEM). Viene utilizzato per controllare i bundle compositi di AEM e la loro configurazione. Questo articolo descrive come gestire le impostazioni di configurazione per tali bundle.
seo-description: OSGi è un elemento fondamentale nello stack tecnologico di Adobe Experience Manager (AEM). Viene utilizzato per controllare i bundle compositi di AEM e la loro configurazione. Questo articolo descrive come gestire le impostazioni di configurazione per tali bundle.
uuid: b39059a5-dd61-486a-869a-0d7a732c3a47
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: d701e4ba-417f-4b57-b103-27fd25290736
feature: Configurazione
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '2014'
ht-degree: 0%

---


# Configurazione di OSGi{#configuring-osgi}

[](https://www.osgi.org/) OSGiè un elemento fondamentale nello stack tecnologico di Adobe Experience Manager (AEM). Viene utilizzato per controllare i bundle compositi di AEM e la loro configurazione.

OSGi &quot;*fornisce le primitive standardizzate che consentono di costruire applicazioni da componenti piccoli, riutilizzabili e collaborativi. Questi componenti possono essere composti in un&#39;applicazione e distribuiti*&quot;.

Questo consente una facile gestione dei bundle in quanto possono essere arrestati, installati, avviati individualmente. Le interdipendenze vengono gestite automaticamente. Ogni componente OSGi (vedi la [specifica OSGi](https://www.osgi.org/Specifications/HomePage)) è contenuto in uno dei vari bundle.

Puoi gestire le impostazioni di configurazione per tali bundle:

* utilizzando la [console Web Adobe CQ](#osgi-configuration-with-the-web-console)
* utilizzo di [file di configurazione](#osgi-configuration-with-configuration-files)
* configurazione di [nodi-contenuto ( `sling:OsgiConfig`) nell&#39;archivio](#osgi-configuration-in-the-repository)

Entrambi i metodi possono essere utilizzati anche se esistono differenze sottili, principalmente in relazione a [Modalità di esecuzione](/help/sites-deploying/configure-runmodes.md):

* [Console web Adobe CQ](#osgi-configuration-with-the-web-console)

   * La Web Console è l’interfaccia standard per la configurazione OSGi. Offre un’interfaccia utente per la modifica delle varie proprietà, dove è possibile selezionare valori da elenchi predefiniti.

      Pertanto è il metodo più semplice da utilizzare.

   * Tutte le configurazioni effettuate con la console Web vengono applicate immediatamente e applicabili all&#39;istanza corrente, indipendentemente dalla modalità di esecuzione corrente o da eventuali modifiche successive alla modalità di esecuzione.

* [file di configurazione](#osgi-configuration-with-configuration-files)

   * Contiene le impostazioni definite nella console Web.
   * Può essere incluso nei pacchetti di contenuti da utilizzare su altre istanze.

* [content-nodes (sling:osgiConfig) nell&#39;archivio](#osgi-configuration-in-the-repository)

   * È necessaria una configurazione manuale tramite CRXDE Lite.
   * A causa delle convenzioni di denominazione dei nodi `sling:OsgiConfig`, puoi collegare la configurazione a una specifica [modalità di esecuzione](/help/sites-deploying/configure-runmodes.md). Puoi anche salvare le configurazioni per più di una modalità di esecuzione nello stesso archivio.
   * Tutte le configurazioni appropriate vengono applicate immediatamente (a seconda della modalità di esecuzione).

A prescindere dal metodo utilizzato, tutti i seguenti metodi di configurazione:

* Assicurati che la copia o la replica del contenuto del repository ricrea configurazioni identiche.
* Consentire il check-out delle configurazioni su FileVault o Subversion; per la sicurezza o per ulteriori aggiornamenti.
* Può essere salvato in pacchetti da utilizzare durante la configurazione di altre istanze.
* Consente di eseguire rollout di configurazione utilizzando gli script per proporre i dettagli di configurazione.

>[!NOTE]
>
>I dettagli di alcune impostazioni importanti sono elencati in [Impostazioni di configurazione OSGi.](/help/sites-deploying/osgi-configuration-settings.md)

## Configurazione OSGi con la console Web {#osgi-configuration-with-the-web-console}

La [console Web](/help/sites-deploying/web-console.md) in AEM fornisce un&#39;interfaccia standardizzata per la configurazione dei bundle. La scheda **Configurazione** viene utilizzata per configurare i bundle OSGi ed è quindi il meccanismo sottostante per la configurazione AEM parametri di sistema.

Tutte le modifiche apportate vengono immediatamente applicate alla configurazione OSGi pertinente, non è necessario riavviare il sistema.

>[!NOTE]
>
>Le modifiche apportate nella console Web vengono salvate nell&#39;archivio come [file di configurazione](#osgi-configuration-with-configuration-files). Questi possono essere inclusi nei pacchetti di contenuti da riutilizzare in altre installazioni.

>[!NOTE]
>
>Nella console Web tutte le descrizioni che fanno riferimento alle impostazioni predefinite si riferiscono ai valori predefiniti di Sling.
>
>Adobe Experience Manager dispone di valori predefiniti propri e pertanto i valori predefiniti impostati potrebbero essere diversi da quelli documentati nella console.

Per aggiornare una configurazione con la console Web:

1. Accedi alla scheda **Configurazione** della console Web tramite:

   * Aprite la console Web dal collegamento nel menu **Strumento -> Operazioni**. Dopo aver effettuato l’accesso alla console è possibile utilizzare il menu a discesa di:

      **OSGi >**

   * URL diretto; ad esempio:

      `http://localhost:4502/system/console/configMgr`
   Verrà visualizzato un elenco.

1. Seleziona il bundle da configurare tramite:

   * facendo clic sull&#39;icona **Modifica** per quel bundle
   * cliccando sul **Nome** del bundle

1. Viene aperta una finestra di dialogo. Consente di modificare le impostazioni desiderate. ad esempio, impostare **Log Level** su `INFO`:

   ![chlimage_1-140](assets/chlimage_1-140.png)

   >[!NOTE]
   >
   >Gli aggiornamenti vengono salvati nell&#39;archivio come [file di configurazione](#osgi-configuration-with-configuration-files). Per individuarli successivamente (ad esempio per includere in un pacchetto di contenuti da utilizzare su un’altra istanza) è necessario annotare l’identità persistente ( `PID`).

1. Fai clic su **Salva**.

   Le modifiche vengono applicate immediatamente alla configurazione OSGi pertinente del sistema in esecuzione. Non è necessario riavviare il sistema.

   >[!NOTE]
   >
   >È ora possibile individuare i file di configurazione [correlati](#osgi-configuration-with-configuration-files); ad esempio, da includere in un pacchetto di contenuti da utilizzare su un’altra istanza.

## Configurazione OSGi con file di configurazione {#osgi-configuration-with-configuration-files}

Le modifiche di configurazione effettuate tramite la Console web vengono mantenute nell’archivio come file di configurazione ( `.config`) in:

`/apps`

Questi possono essere inclusi nei pacchetti di contenuti e riutilizzati in altre istanze.

>[!NOTE]
>
>Il formato dei file di configurazione è molto specifico. Per informazioni dettagliate, consulta la [documentazione Sling Apache](https://sling.apache.org/documentation/development/slingstart.html#default-configuration-format) .
>
>Per questo motivo è consigliabile creare e gestire il file di configurazione apportando modifiche effettive nella console Web.

La console Web non mostra alcuna indicazione di dove nell’archivio sono state salvate le modifiche, ma queste possono essere facilmente posizionate:

1. Crea il file di configurazione effettuando una modifica iniziale nella console Web](#osgi-configuration-with-the-web-console).[
1. Apri CRXDE Lite.
1. Nel menu **Strumenti** seleziona **Query ...** .
1. Invia una query di **Tipo** `SQL` per cercare il PID della configurazione che hai aggiornato.

   Ad esempio, **Apache Felix OSGi Management Console** ha l&#39;identità persistente (PID) di:

   `org.apache.felix.webconsole.internal.servlet.OsgiManager`

   La query SQL potrebbe quindi essere:

   ```shell
   select * from nt:base where jcr:path like '/apps/%' and contains(*, 'org.apache.felix.webconsole.internal.servlet.OsgiManager')
   ```

1. Verrà visualizzato il nodo del file di configurazione.

   Per l&#39;esempio precedente:

   `/apps/system/config/org.apache.felix.webconsole.internal.servlet.OsgiManager.config`

   >[!CAUTION]
   >
   >Puoi aprire questo file per visualizzare le modifiche, ma per evitare errori di digitazione è consigliabile apportare modifiche effettive con la console.

1. Ora puoi creare un pacchetto di contenuti, contenente questo nodo, e utilizzarlo come necessario sulle altre istanze.

## Configurazione OSGi nell&#39;archivio {#osgi-configuration-in-the-repository}

Oltre a utilizzare la console web, puoi anche definire i dettagli di configurazione nell’archivio. Questo consente di configurare facilmente le diverse modalità di esecuzione.

Queste configurazioni vengono effettuate creando nodi `sling:OsgiConfig` nell&#39;archivio a cui fare riferimento per il sistema. Questi nodi riflettono le configurazioni OSGi e formano un’interfaccia utente per tali configurazioni. Per aggiornare i dati di configurazione si aggiornano le proprietà del nodo.

Se modifichi i dati di configurazione nell’archivio, le modifiche vengono immediatamente applicate alla configurazione OSGi pertinente, come se le modifiche fossero state apportate utilizzando la console Web, con i controlli di convalida e coerenza appropriati. Questo vale anche per l’azione di copia di una configurazione da `/libs/` a `/apps/`.

Poiché lo stesso parametro di configurazione può essere individuato in diverse posizioni, il sistema:

* cerca tutti i nodi di tipo `sling:OsgiConfig`
* filtra in base al nome del servizio
* filtra in base alla modalità di esecuzione

>[!NOTE]
>
>Leggi anche [come definire un confinamento basato su archivio per una specifica istanza solo](https://helpx.adobe.com/experience-manager/kb/RunModeDependentConfigAndInstall.html).

### Aggiunta di una nuova configurazione al repository {#adding-a-new-configuration-to-the-repository}

#### Cosa devi sapere {#what-you-need-to-know}

Per aggiungere una nuova configurazione all’archivio è necessario conoscere quanto segue:

1. L’ **Identità persistente** (PID) del servizio.

   Fai riferimento al campo **Configurazioni** nella console Web. Il nome viene visualizzato tra parentesi dopo il nome del bundle (o in **Informazioni di configurazione** verso il fondo della pagina).

   Ad esempio, crea un nodo `com.day.cq.wcm.core.impl.VersionManagerImpl.` per configurare **AEM WCM Version Manager**.

   ![chlimage_1-141](assets/chlimage_1-141.png)

1. Se è richiesta una specifica [modalità di esecuzione](/help/sites-deploying/configure-runmodes.md). Crea la cartella:

   * `config` - per tutte le modalità di esecuzione
   * `config.author` - per l’ambiente di authoring
   * `config.publish` - per l’ambiente di pubblicazione
   * `config.<run-mode>` - se del caso

1. Se è necessario un **Configurazione** o **Configurazione di fabbrica**.
1. i singoli parametri da configurare; incluse le definizioni di parametri esistenti che dovranno essere ricreati.

   Fai riferimento al singolo campo del parametro nella console Web. Il nome viene visualizzato tra parentesi per ciascun parametro.

   Ad esempio, creare una proprietà
   `versionmanager.createVersionOnActivation` per configurare  **Crea versione su Activation**.

   ![chlimage_1-142](assets/chlimage_1-142.png)

1. Esiste già una configurazione in `/libs`? Per elencare tutte le configurazioni nell&#39;istanza, utilizza lo strumento **Query** in CRXDE Lite per inviare la seguente query SQL:

   `select * from sling:OsgiConfig`

   In tal caso, questa configurazione può essere copiata in ` /apps/<yourProject>/`, quindi personalizzata nella nuova posizione.

#### Creazione della configurazione nell&#39;archivio {#creating-the-configuration-in-the-repository}

Per aggiungere effettivamente la nuova configurazione all’archivio:

1. Utilizza CRXDE Lite per passare a:

   ` /apps/<yourProject>`

1. Se non esiste già, crea la cartella `config` ( `sling:Folder`):

   * `config` - applicabile a tutte le modalità di esecuzione
   * `config.<run-mode>` - specifica di una particolare modalità di esecuzione

1. Sotto questa cartella crea un nodo:

   * Tipo: `sling:OsgiConfig`
   * Nome: l&#39;identità persistente (PID);

      ad esempio per AEM WCM Version Manager utilizzare `com.day.cq.wcm.core.impl.VersionManagerImpl`
   >[!NOTE]
   >
   >Quando si crea una configurazione di fabbrica, aggiungere `-<identifier>` al nome.
   >
   >Come in: `org.apache.sling.commons.log.LogManager.factory.config-<identifier>`
   >
   >Dove `<identifier>` viene sostituito da testo libero che è necessario immettere per identificare l&#39;istanza (non è possibile omettere tali informazioni); ad esempio:
   >
   >`org.apache.sling.commons.log.LogManager.factory.config-MINE`

1. Per ogni parametro da configurare, crea una proprietà su questo nodo:

   * Nome: il nome del parametro come mostrato nella console Web; il nome viene visualizzato tra parentesi alla fine della descrizione del campo. Ad esempio, per `Create Version on Activation` utilizza `versionmanager.createVersionOnActivation`
   * Tipo: se del caso.
   * Valore: se necessario.

   È sufficiente creare le proprietà per i parametri che si desidera configurare. Gli altri avranno comunque i valori predefiniti impostati da AEM.

1. Salva tutte le modifiche.

   Le modifiche vengono applicate non appena il nodo viene aggiornato riavviando il servizio (come con le modifiche apportate nella console Web).

>[!CAUTION]
>
>Non è necessario modificare nulla nel percorso `/libs`.

>[!CAUTION]
>
>Il percorso completo di una configurazione deve essere corretto per essere letto all&#39;avvio.

## Dettagli di configurazione {#configuration-details}

### Ordine di risoluzione all&#39;avvio {#resolution-order-at-startup}

Viene utilizzato il seguente ordine di precedenza:

1. Nodi archivio sotto `/apps/*/config...`.o con file di tipo `sling:OsgiConfig` o proprietà.

1. Nodi archivio con tipo `sling:OsgiConfig` in `/libs/*/config...`. (definizioni predefinite).

1. Qualsiasi file `.config` di `<*cq-installation-dir*>/crx-quickstart/launchpad/config/...`. sul file system locale.

Ciò significa che una configurazione generica in `/libs` può essere mascherata da una configurazione specifica del progetto in `/apps`.

### Ordine di risoluzione in runtime {#resolution-order-at-runtime}

Le modifiche apportate alla configurazione durante l&#39;esecuzione del sistema attivano un ricaricamento con la configurazione modificata.

Si applica quindi il seguente ordine di precedenza:

1. La modifica di una configurazione nella console Web avrà effetto immediato in quanto ha la precedenza in fase di esecuzione.
1. La modifica di una configurazione in `/apps` avrà effetto immediato.
1. La modifica di una configurazione in `/libs` avrà effetto immediato, a meno che non sia mascherata da una configurazione in `/apps`.

### Risoluzione di più modalità di esecuzione {#resolution-of-multiple-run-modes}

Per configurazioni specifiche della modalità di esecuzione, è possibile combinare più modalità di esecuzione. Ad esempio, puoi creare cartelle di configurazione nel seguente stile:

`/apps/*/config.<runmode1>.<runmode2>/`

Le configurazioni in tali cartelle verranno applicate se tutte le modalità di esecuzione corrispondono a una modalità di esecuzione definita all&#39;avvio.

Ad esempio, se un&#39;istanza è stata avviata con le modalità di esecuzione `author,dev,emea`, verranno applicati i nodi di configurazione in `/apps/*/config.emea`, `/apps/*/config.author.dev/` e `/apps/*/config.author.emea.dev/`, mentre i nodi di configurazione in `/apps/*/config.author.asean/` e `/config/author.dev.emea.noldap/` non verranno applicati.

Se sono applicabili più configurazioni per lo stesso PID, viene applicata la configurazione con il numero più alto di modalità di esecuzione corrispondenti.

Ad esempio, se un&#39;istanza è stata avviata con le modalità di esecuzione `author,dev,emea` e sia `/apps/*/config.author/` che `/apps/*/config.emea.author/` definiscono una configurazione per
`com.day.cq.wcm.core.impl.VersionManagerImpl`, viene applicata la configurazione in `/apps/*/config.emea.author/`.

La granularità di questa regola è a livello di PID.
Non è possibile definire alcune proprietà per lo stesso PID in `/apps/*/config.author/` e altre specifiche in `/apps/*/config.emea.author/` per lo stesso PID.
La configurazione con il maggior numero di modalità di esecuzione corrispondenti sarà efficace per l&#39;intero PID.

### Configurazioni standard {#standard-configurations}

L’elenco seguente mostra una piccola selezione delle configurazioni disponibili (in un’installazione standard) nell’archivio:

* Autore - AEM filtro WCM:

   `libs/wcm/core/config.author/com.day.cq.wcm.core.WCMRequestFilter`

* Pubblica - AEM filtro WCM:

   `libs/wcm/core/config.publish/com.day.cq.wcm.core.WCMRequestFilter`

* Pubblica - AEM statistiche pagina WCM:

   `libs/wcm/core/config.publish/com.day.cq.wcm.core.stats.PageViewStatistics`

>[!NOTE]
>
>Poiché queste configurazioni risiedono in `/libs`, non devono essere modificate direttamente, ma copiate nell&#39;area dell&#39;applicazione ( `/apps`) prima della personalizzazione.

Per elencare tutti i nodi di configurazione nell&#39;istanza, utilizza la funzionalità **Query** in CRXDE Lite per inviare la seguente query SQL:

`select * from sling:OsgiConfig`

### Persistenza di configurazione {#configuration-persistence}

* Se modifichi una configurazione tramite la console Web, in genere viene scritta nell’archivio all’indirizzo:

   `/apps/{somewhere}`

   * Per impostazione predefinita `{somewhere}` è `system/config` in modo che la configurazione venga scritta in

      `/apps/system/config`

   * Tuttavia, se modifichi una configurazione che proviene inizialmente da un’altra posizione nell’archivio: ad esempio:

      /libs/foo/config/someconfig

      Quindi la configurazione aggiornata viene scritta nella posizione originale; ad esempio:

      `/apps/foo/config/someconfig`

* Le impostazioni modificate da `admin` vengono salvate nei file `*.config` in:

   ```
      /crx-quickstart/launchpad/config
   ```

   * Si tratta dell’area dati privata dell’amministratore di configurazione OSGi e contiene tutti i dettagli di configurazione specificati da `admin`, indipendentemente da come sono entrati nel sistema.
   * Si tratta di un dettaglio dell’implementazione e non devi mai modificare direttamente questa directory.
   * Tuttavia, è utile conoscere la posizione di questi file di configurazione in modo che le copie possano essere prese per il backup e/o installazione multipla:

      * Console di gestione Apache Felix OSGi

         `../crx/org/apache/felix/webconsole/internal/servlet/OsgiManager.config`

      * Archivio client CRX Sling

         `../com/day/crx/sling/client/impl/CRXSlingClientRepository/<pid-nr>.config`

>[!CAUTION]
>
>Devi ***mai*** modificare le cartelle o i file in:
>
>`/crx-quickstart/launchpad/config`

