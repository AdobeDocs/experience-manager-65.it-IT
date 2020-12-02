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
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '2013'
ht-degree: 0%

---


# Configurazione di OSGi{#configuring-osgi}

[](https://www.osgi.org/) OSGiè un elemento fondamentale nello stack tecnologico di Adobe Experience Manager (AEM). Viene utilizzato per controllare i bundle compositi di AEM e la loro configurazione.

OSGi &quot;*fornisce le primitive standardizzate che consentono di creare applicazioni da componenti piccoli, riutilizzabili e collaborativi. Questi componenti possono essere composti in un&#39;applicazione e distribuiti*&quot;.

In questo modo è possibile gestire facilmente i bundle in quanto possono essere arrestati, installati e avviati individualmente. Le interdipendenze vengono gestite automaticamente. Ciascun componente OSGi (vedere la [specifica OSGi](https://www.osgi.org/Specifications/HomePage)) è contenuto in uno dei vari bundle.

Potete gestire le impostazioni di configurazione per tali bundle tramite:

* utilizzo della [ console Web Adobe CQ](#osgi-configuration-with-the-web-console)
* utilizzo di [file di configurazione](#osgi-configuration-with-configuration-files)
* configurazione di [nodi di contenuto ( `sling:OsgiConfig`) nell&#39;archivio](#osgi-configuration-in-the-repository)

Entrambi i metodi possono essere utilizzati anche se esistono sottili differenze, principalmente in relazione a [Modalità di esecuzione](/help/sites-deploying/configure-runmodes.md):

* [ della console Web di Adobe CQ](#osgi-configuration-with-the-web-console)

   * La console Web è l’interfaccia standard per la configurazione OSGi. Offre un’interfaccia utente per la modifica delle varie proprietà, dove è possibile selezionare i possibili valori da elenchi predefiniti.

      Di conseguenza, è il metodo più semplice da usare.

   * Tutte le configurazioni effettuate con la console Web vengono applicate immediatamente e si applicano all&#39;istanza corrente, indipendentemente dalla modalità di esecuzione corrente, o da eventuali modifiche successive alla modalità di esecuzione.

* [file di configurazione](#osgi-configuration-with-configuration-files)

   * Contiene le impostazioni definite nella console Web.
   * Può essere incluso nei pacchetti di contenuto per l&#39;utilizzo in altre istanze.

* [nodi di contenuto (sling:osgiConfig) nella directory archivio](#osgi-configuration-in-the-repository)

   * Questo richiede la configurazione manuale tramite CRXDE Lite.
   * A causa delle convenzioni di denominazione dei nodi `sling:OsgiConfig`, è possibile collegare la configurazione a una specifica [modalità di esecuzione](/help/sites-deploying/configure-runmodes.md). È anche possibile salvare le configurazioni per più modalità di esecuzione nello stesso repository.
   * Tutte le configurazioni appropriate vengono applicate immediatamente (a seconda della modalità di esecuzione).

A prescindere dal metodo utilizzato, tutti i seguenti metodi di configurazione:

* Verificare che la copia o la replica del contenuto del repository ricrei configurazioni identiche.
* Consentire il check-out delle configurazioni su FileVault o Subversion; per la sicurezza o per ulteriori aggiornamenti.
* Può essere salvato in pacchetti per l’utilizzo durante la configurazione di altre istanze.
* Consentono di eseguire i rollout di configurazione utilizzando gli script per fornire i dettagli di configurazione.

>[!NOTE]
>
>I dettagli di alcune impostazioni importanti sono elencati in [Impostazioni di configurazione OSGi.](/help/sites-deploying/osgi-configuration-settings.md)

## Configurazione OSGi con la console Web {#osgi-configuration-with-the-web-console}

La [console Web](/help/sites-deploying/web-console.md) in AEM fornisce un&#39;interfaccia standard per la configurazione dei bundle. La scheda **Configuration** viene utilizzata per configurare i bundle OSGi ed è quindi il meccanismo sottostante per configurare AEM parametri di sistema.

Eventuali modifiche apportate vengono applicate immediatamente alla configurazione OSGi interessata, senza necessità di riavvio.

>[!NOTE]
>
>Le modifiche apportate nella console Web vengono salvate nella directory archivio come [file di configurazione](#osgi-configuration-with-configuration-files). Questi possono essere inclusi in pacchetti di contenuti da riutilizzare in altre installazioni.

>[!NOTE]
>
>Nella console Web tutte le descrizioni che fanno riferimento alle impostazioni predefinite si riferiscono alle impostazioni predefinite di Sling.
>
>Adobe Experience Manager ha le proprie impostazioni predefinite, pertanto le impostazioni predefinite potrebbero essere diverse da quelle documentate nella console.

Per aggiornare una configurazione con la console Web:

1. Per accedere alla scheda **Configurazione** della console Web, effettuare le seguenti operazioni:

   * Aprite la console Web dal collegamento nel menu **Strumento -> Operazioni**. Dopo aver effettuato l’accesso alla console è possibile utilizzare il menu a discesa di:

      **OSGi >**

   * URL diretto; ad esempio:

      `http://localhost:4502/system/console/configMgr`
   Verrà visualizzato un elenco.

1. Selezionate il bundle da configurare tramite:

   * facendo clic sull&#39;icona **Edit** per il bundle
   * facendo clic sul **Nome** del bundle

1. Viene aperta una finestra di dialogo. Qui è possibile apportare le modifiche necessarie; ad esempio, impostare **Livello di registro** su `INFO`:

   ![chlimage_1-140](assets/chlimage_1-140.png)

   >[!NOTE]
   >
   >Gli aggiornamenti vengono salvati nella directory archivio come [file di configurazione](#osgi-configuration-with-configuration-files). Per individuarli successivamente, (ad esempio per includere in un pacchetto di contenuti da utilizzare in un&#39;altra istanza) è necessario prendere nota dell&#39;identità persistente ( `PID`).

1. Fai clic su **Salva**.

   Le modifiche vengono applicate immediatamente alla configurazione OSGi del sistema in esecuzione. Non è necessario riavviare il sistema.

   >[!NOTE]
   >
   >È ora possibile individuare i file di configurazione [correlati](#osgi-configuration-with-configuration-files); ad esempio, da includere in un pacchetto di contenuto da utilizzare in un&#39;altra istanza.

## Configurazione OSGi con file di configurazione {#osgi-configuration-with-configuration-files}

Le modifiche di configurazione effettuate tramite la console Web vengono memorizzate nella directory archivio come file di configurazione ( `.config`) in:

`/apps`

Questi possono essere inclusi nei pacchetti di contenuto e riutilizzati in altre istanze.

>[!NOTE]
>
>Il formato dei file di configurazione è molto specifico. Per maggiori informazioni, consultare la [documentazione Sling Apache](https://sling.apache.org/documentation/development/slingstart.html#default-configuration-format).
>
>Per questo motivo si consiglia di creare e mantenere il file di configurazione apportando modifiche effettive nella console Web.

La console Web non mostra alcuna indicazione della posizione in cui sono state salvate le modifiche, ma può essere facilmente individuata:

1. Creare il file di configurazione [effettuando una modifica iniziale nella console Web](#osgi-configuration-with-the-web-console).
1. Apri CRXDE Lite.
1. Nel menu **Strumenti** selezionare **Query ...** .
1. Inviare una query di **Tipo** `SQL` per cercare il PID della configurazione aggiornata.

   Ad esempio, **Apache Felix OSGi Management Console** ha l&#39;identità persistente (PID) di:

   `org.apache.felix.webconsole.internal.servlet.OsgiManager`

   Pertanto, la query SQL potrebbe essere:

   ```shell
   select * from nt:base where jcr:path like '/apps/%' and contains(*, 'org.apache.felix.webconsole.internal.servlet.OsgiManager')
   ```

1. Verrà visualizzato il nodo del file di configurazione.

   Per l&#39;esempio precedente:

   `/apps/system/config/org.apache.felix.webconsole.internal.servlet.OsgiManager.config`

   >[!CAUTION]
   >
   >Potete aprire questo file per visualizzare le modifiche, ma per evitare errori di digitazione è consigliabile apportare modifiche effettive con la console.

1. Ora potete creare un pacchetto di contenuto contenente questo nodo e utilizzarlo come necessario per le altre istanze.

## Configurazione OSGi nell&#39;archivio {#osgi-configuration-in-the-repository}

Oltre a utilizzare la console Web, potete anche definire i dettagli di configurazione nella directory archivio. Questo consente di configurare facilmente le diverse modalità di esecuzione.

Queste configurazioni vengono eseguite creando nodi `sling:OsgiConfig` nella directory archivio a cui fare riferimento il sistema. Questi nodi riflettono le configurazioni OSGi e formano un&#39;interfaccia utente per tali configurazioni. Per aggiornare i dati di configurazione, aggiornare le proprietà del nodo.

Se modificate i dati di configurazione nel repository, le modifiche vengono applicate immediatamente alla configurazione OSGi interessata, come se le modifiche fossero state apportate utilizzando la console Web, con i controlli di convalida e coerenza appropriati. Ciò vale anche per l&#39;azione di copia di una configurazione da `/libs/` a `/apps/`.

Poiché lo stesso parametro di configurazione può essere individuato in più punti, il sistema:

* cerca tutti i nodi di tipo `sling:OsgiConfig`
* filtri in base al nome del servizio
* filtri in base alla modalità di esecuzione

>[!NOTE]
>
>Leggere anche [come definire un confinamento basato su repository per una specifica istanza solo](https://helpx.adobe.com/experience-manager/kb/RunModeDependentConfigAndInstall.html).

### Aggiunta di una nuova configurazione all&#39;archivio {#adding-a-new-configuration-to-the-repository}

#### Cosa devi sapere {#what-you-need-to-know}

Per aggiungere una nuova configurazione al repository è necessario conoscere quanto segue:

1. **Identità persistente** (PID) del servizio.

   Fare riferimento al campo **Configurazioni** nella console Web. Il nome viene visualizzato tra parentesi dopo il nome del bundle (o in **Informazioni di configurazione** nella parte inferiore della pagina).

   Ad esempio, creare un nodo `com.day.cq.wcm.core.impl.VersionManagerImpl.` per configurare **AEM WCM Version Manager**.

   ![chlimage_1-141](assets/chlimage_1-141.png)

1. Indica se è necessaria una [modalità di esecuzione](/help/sites-deploying/configure-runmodes.md) specifica. Create la cartella:

   * `config` - per tutte le modalità di esecuzione
   * `config.author` - per l&#39;ambiente di authoring
   * `config.publish` - per l’ambiente di pubblicazione
   * `config.<run-mode>` - se del caso

1. Se è necessaria una **configurazione** o **configurazione di fabbrica**.
1. I singoli parametri da configurare; incluse eventuali definizioni di parametri esistenti che dovranno essere ricreate.

   Fate riferimento al singolo campo dei parametri nella console Web. Il nome viene visualizzato tra parentesi per ciascun parametro.

   Ad esempio, creare una proprietà
   `versionmanager.createVersionOnActivation` per configurare  **Crea versione all&#39;attivazione**.

   ![chlimage_1-142](assets/chlimage_1-142.png)

1. Esiste già una configurazione in `/libs`? Per elencare tutte le configurazioni nell&#39;istanza, utilizzare lo strumento **Query** in CRXDE Lite per inviare la seguente query SQL:

   `select * from sling:OsgiConfig`

   In tal caso, questa configurazione può essere copiata in ` /apps/<yourProject>/`, quindi personalizzata nella nuova posizione.

#### Creazione della configurazione nell&#39;archivio {#creating-the-configuration-in-the-repository}

Per aggiungere la nuova configurazione alla directory archivio:

1. Utilizzate il CRXDE Lite per passare a:

   ` /apps/<yourProject>`

1. Se non già esistente, create la cartella `config` ( `sling:Folder`):

   * `config` - applicabile a tutte le modalità di esecuzione
   * `config.<run-mode>` - specifica di una particolare modalità di esecuzione

1. In questa cartella create un nodo:

   * Tipo: `sling:OsgiConfig`
   * Nome: l’identità persistente (PID);

      ad esempio, AEM WCM Version Manager utilizza `com.day.cq.wcm.core.impl.VersionManagerImpl`
   >[!NOTE]
   >
   >Quando si crea una configurazione di fabbrica, aggiungere `-<identifier>` al nome.
   >
   >Come in: `org.apache.sling.commons.log.LogManager.factory.config-<identifier>`
   >
   >Dove `<identifier>` viene sostituito da testo libero che è necessario immettere per identificare l&#39;istanza (non è possibile omettere tali informazioni); ad esempio:
   >
   >`org.apache.sling.commons.log.LogManager.factory.config-MINE`

1. Per ogni parametro da configurare, create una proprietà su questo nodo:

   * Nome: il nome del parametro come mostrato nella console Web; il nome viene visualizzato tra parentesi alla fine della descrizione del campo. Ad esempio, per `Create Version on Activation` utilizzare `versionmanager.createVersionOnActivation`
   * Tipo: se del caso.
   * Valore: come necessario.

   È necessario creare solo proprietà per i parametri che si desidera configurare, mentre altri continueranno a utilizzare i valori predefiniti come impostato da AEM.

1. Salvate tutte le modifiche.

   Le modifiche vengono applicate non appena il nodo viene aggiornato riavviando il servizio (come con le modifiche apportate nella console Web).

>[!CAUTION]
>
>Non è necessario modificare nulla nel percorso `/libs`.

>[!CAUTION]
>
>Il percorso completo di una configurazione deve essere corretto affinché possa essere letto all&#39;avvio.

## Dettagli configurazione {#configuration-details}

### Ordine di risoluzione all&#39;avvio {#resolution-order-at-startup}

Viene utilizzato il seguente ordine di precedenza:

1. I nodi del repository in `/apps/*/config...`.con il tipo `sling:OsgiConfig` o i file di proprietà.

1. nodi repository con tipo `sling:OsgiConfig` in `/libs/*/config...`. (definizioni predefinite).

1. Qualsiasi `.config` file da `<*cq-installation-dir*>/crx-quickstart/launchpad/config/...`. nel file system locale.

Ciò significa che una configurazione generica in `/libs` può essere mascherata da una configurazione specifica di progetto in `/apps`.

### Ordine di risoluzione in fase di esecuzione {#resolution-order-at-runtime}

Le modifiche alla configurazione apportate durante l&#39;esecuzione del sistema attivano un ricaricamento con la configurazione modificata.

Viene quindi applicato il seguente ordine di precedenza:

1. La modifica di una configurazione nella console Web avrà effetto immediato in quanto ha precedenza in fase di esecuzione.
1. La modifica di una configurazione in `/apps` avrà effetto immediato.
1. La modifica di una configurazione in `/libs` avrà effetto immediato, a meno che non venga mascherata da una configurazione in `/apps`.

### Risoluzione di più modalità di esecuzione {#resolution-of-multiple-run-modes}

Per configurazioni specifiche della modalità di esecuzione, è possibile combinare più modalità di esecuzione. Ad esempio, potete creare le cartelle di configurazione nel seguente stile:

`/apps/*/config.<runmode1>.<runmode2>/`

Le configurazioni in tali cartelle verranno applicate se tutte le modalità di esecuzione corrispondono a una modalità di esecuzione definita all&#39;avvio.

Ad esempio, se un&#39;istanza è stata avviata con le modalità di esecuzione `author,dev,emea`, i nodi di configurazione in `/apps/*/config.emea`, `/apps/*/config.author.dev/` e `/apps/*/config.author.emea.dev/` saranno applicati, mentre i nodi di configurazione in `/apps/*/config.author.asean/` e `/config/author.dev.emea.noldap/` non saranno applicati.

Se si applicano più configurazioni per lo stesso PID, viene applicata la configurazione con il numero più elevato di modalità di esecuzione corrispondenti.

Ad esempio, se un&#39;istanza è stata avviata con le modalità di esecuzione `author,dev,emea` e sia `/apps/*/config.author/` che `/apps/*/config.emea.author/` definire una configurazione per
`com.day.cq.wcm.core.impl.VersionManagerImpl`, verrà applicata la configurazione in `/apps/*/config.emea.author/`.

La granularità di questa regola è a livello PID.
Non è possibile definire alcune proprietà per lo stesso PID in `/apps/*/config.author/` e più specifiche in `/apps/*/config.emea.author/` per lo stesso PID.
La configurazione con il maggior numero di modalità di esecuzione corrispondenti sarà efficace per l&#39;intero PID.

### Configurazioni standard {#standard-configurations}

L&#39;elenco seguente mostra una piccola selezione delle configurazioni disponibili (in un&#39;installazione standard) nell&#39;archivio:

* Autore - AEM filtro WCM:

   `libs/wcm/core/config.author/com.day.cq.wcm.core.WCMRequestFilter`

* Pubblica - AEM filtro WCM:

   `libs/wcm/core/config.publish/com.day.cq.wcm.core.WCMRequestFilter`

* Pubblica - AEM statistiche pagina WCM:

   `libs/wcm/core/config.publish/com.day.cq.wcm.core.stats.PageViewStatistics`

>[!NOTE]
>
>Poiché queste configurazioni risiedono in `/libs`, non devono essere modificate direttamente, ma copiate nell&#39;area dell&#39;applicazione ( `/apps`) prima della personalizzazione.

Per elencare tutti i nodi di configurazione dell&#39;istanza, utilizzare la funzionalità **Query** in CRXDE Lite per inviare la seguente query SQL:

`select * from sling:OsgiConfig`

### Persistenza della configurazione {#configuration-persistence}

* Se modificate una configurazione tramite la console Web, in genere viene scritta nella directory archivio all’indirizzo:

   `/apps/{somewhere}`

   * Per impostazione predefinita, `{somewhere}` è `system/config` in modo che la configurazione sia scritta in

      `/apps/system/config`

   * Tuttavia, se state modificando una configurazione che inizialmente proveniva da un’altra posizione della directory archivio: ad esempio:

      /libs/foo/config/someconfig

      La configurazione aggiornata viene quindi scritta nella posizione originale; ad esempio:

      `/apps/foo/config/someconfig`

* Le impostazioni modificate da `admin` vengono salvate nei file `*.config` in:

   ```
      /crx-quickstart/launchpad/config
   ```

   * Si tratta dell&#39;area dati privata dell&#39;amministratore di configurazione OSGi e contiene tutti i dettagli di configurazione specificati da `admin`, indipendentemente da come sono entrati nel sistema.
   * Si tratta di un dettaglio di implementazione e non devi mai modificare direttamente questa directory.
   * Tuttavia, è utile conoscere la posizione di questi file di configurazione in modo che le copie possano essere effettuate per il backup e/o l&#39;installazione multipla:

      * Apache Felix OSGi Management Console

         `../crx/org/apache/felix/webconsole/internal/servlet/OsgiManager.config`

      * Repository client CRX Sling

         `../com/day/crx/sling/client/impl/CRXSlingClientRepository/<pid-nr>.config`

>[!CAUTION]
>
>È necessario ***never*** modificare le cartelle o i file in:
>
>`/crx-quickstart/launchpad/config`

