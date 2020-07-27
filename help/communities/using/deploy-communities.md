---
title: Implementazione di Communities
seo-title: Implementazione di Communities
description: Come distribuire i AEM Communities
seo-description: Come distribuire i AEM Communities
uuid: 18d9b424-004d-43b2-968a-318e27a93759
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
content-type: reference
topic-tags: deploying
discoiquuid: c8d7355f-5a70-40d1-bf22-62fab8002ea0
docset: aem65
translation-type: tm+mt
source-git-commit: d80c6609b5a0ac299b57b1d0c0e8d6210e595b97
workflow-type: tm+mt
source-wordcount: '1894'
ht-degree: 1%

---


# Implementazione di Communities{#deploying-communities}

## Prerequisiti {#prerequisites}

* [AEM 6.5 Platform](/help/sites-deploying/deploy.md)

* AEM Communities, licenza

* Licenze facoltative per :

   * [Funzioni di Adobe  Analytics per Communities](/help/communities/analytics.md)
   * [MongoDB per MSRP](/help/communities/msrp.md)
   * [Adobe Cloud for ASRP](/help/communities/asrp.md)

## Elenco di controllo dell&#39;installazione {#installation-checklist}

**Per la piattaforma[AEM](/help/sites-deploying/deploy.md#what-is-aem)**

* installa gli ultimi aggiornamenti di [AEM 6.5](#aem64updates)

* se non si utilizzano le porte predefinite (4502, 4503), [configurare gli agenti di replica](#replication-agents-on-author)
* [replicare la chiave di crittografia](#replicate-the-crypto-key)
* se supporta la globalizzazione, [imposta la traduzione](/help/sites-administering/translation.md)automatica (è disponibile l&#39;impostazione di esempio per lo sviluppo)

**Per la funzionalità[Community](/help/communities/overview.md)**

* se distribuite una farm [di](/help/sites-deploying/recommended-deploys.md#tarmk-farm)pubblicazione, [identificate l&#39;editore principale](#primary-publisher)

* [abilitare il servizio tunnel](#tunnel-service-on-author)
* [abilita login mediante profilo sociale](/help/communities/social-login.md#adobe-granite-oauth-authentication-handler)
* [configurare Adobe  Analytics](/help/communities/analytics.md)
* impostare un servizio e-mail [predefinito](/help/communities/email.md)
* identificare la scelta per lo storage [UGC](/help/communities/working-with-srp.md) condiviso (**SRP**)

   * se MongoDB SRP [(MSRP)](/help/communities/msrp.md)

      * [installazione e configurazione di MongoDB](/help/communities/msrp.md#mongodb-configuration)
      * [configura Solr](/help/communities/solr.md)
      * [select MSRP](/help/communities/srp-config.md)
   * se database relazionale SRP [(DSRP)](/help/communities/dsrp.md)

      * [installare il driver JDBC per MySQL](#jdbc-driver-for-mysql)
      * [installazione e configurazione di MySQL per DSRP](/help/communities/dsrp-mysql.md)
      * [configura Solr](/help/communities/solr.md)
      * [select DSRP](/help/communities/srp-config.md)
   * se Adobe SRP [(ASRP)](/help/communities/asrp.md)

      * collaborazione con il rappresentante commerciale di riferimento per il provisioning
      * [seleziona ASRP](/help/communities/srp-config.md)
   * se JCR SRP [(JSRP)](/help/communities/jsrp.md)

      * non è un archivio UGC condiviso:

         * UGC non è mai replicato
         * UGC visibile solo nell’istanza o nel cluster AEM in cui è stato immesso
      * il valore predefinito è JSRP

   Per la funzione di **[abilitazione](/help/communities/overview.md#enablement-community)**

   * [installazione e configurazione di FFmpeg](/help/communities/ffmpeg.md)
   * [installare il driver JDBC per MySQL](#jdbc-driver-for-mysql)
   * [installare AEM Communities SCORM-Engine](#scorm-package)
   * [installazione e configurazione di MySQL per l&#39;abilitazione](/help/communities/mysql.md)






## Latest Releases {#latest-releases}

AEM 6.5 Communities GA con il pacchetto Communities. Per informazioni sugli aggiornamenti di AEM 6.5 [Communities](/help/release-notes/release-notes.md#experiencemanagercommunities), consulta le Note [sulla versione di](/help/release-notes/release-notes.md#communities-release-notes.html)AEM 6.5.

### Aggiornamenti di AEM 6.5 {#aem-updates}

A partire da AEM 6.4, gli aggiornamenti alle community vengono forniti come parte dei Service Pack e dei pacchetti AEM Cumulative Fix.

Per gli ultimi aggiornamenti ad AEM 6.5, consulta [Adobe Experience Manager 6.4 Cumulative Fix Pack e Service Pack](https://helpx.adobe.com/it/experience-manager/aem-releases-updates.html).

### Cronologia versioni {#version-history}

Come in AEM 6.4 e versioni successive, le funzioni AEM Communities e gli hotfix fanno parte di pacchetti di correzioni e Service Pack cumulativi di AEM Communities. Non esistono pertanto pacchetti di caratteristiche distinti.

### Driver JDBC per MySQL {#jdbc-driver-for-mysql}

Due funzionalità Community utilizzano un database MySQL:

* per l&#39; [abilitazione](/help/communities/enablement.md) : registrazione delle attività SCORM e degli studenti
* per [DSRP](/help/communities/dsrp.md) : memorizzazione di contenuto generato dall&#39;utente (UGC)

Il connettore MySQL deve essere ottenuto e installato separatamente.

Le misure necessarie sono:

1. scaricate l&#39;archivio ZIP da [https://dev.mysql.com/downloads/connector/j/](https://dev.mysql.com/downloads/connector/j/)

   * la versione deve essere >= 5.1.38

1. estrarre mysql-Connector-java-&lt;versione>-bin.jar (bundle) dall&#39;archivio
1. utilizzate la console Web per installare e avviare il bundle:

   * ad esempio, https://localhost:4502/system/console/bundles
   * select **`Install/Update`**
   * Sfoglia... per selezionare il bundle estratto dall&#39;archivio ZIP scaricato
   * verificare che* Il driver JDBC di Oracle Corporation per MySQLcom.mysql.jdbc* sia attivo e avviarlo in caso contrario (o controllare i registri)

1. se l&#39;installazione avviene su una distribuzione esistente dopo la configurazione di JDBC, eseguire un nuovo riferimento JDBC al nuovo connettore salvando nuovamente la configurazione JDBC dalla console Web:

   * ad esempio, https://localhost:4502/system/console/configMgr
   * individua `Day Commons JDBC Connections Pool` configurazione
   * selezionare per aprire
   * select `Save`

1. Ripetere i passaggi 3 e 4 per tutte le istanze di creazione e pubblicazione

Ulteriori informazioni sull&#39;installazione dei bundle sono disponibili nella pagina Console [](/help/sites-deploying/web-console.md#bundles) Web.

#### Esempio: Bundle del connettore MySQL installato {#example-installed-mysql-connector-bundle}

![](../assets/chlimage_1-125.png)

### Pacchetto SCORM {#scorm-package}

SCORM (Shareable Content Object Reference Model) è una raccolta di standard e specifiche per l&#39;e-learning. SCORM definisce anche come il contenuto può essere incluso in un file ZIP trasferibile.

Il motore SCORM AEM Communities è richiesto per la funzione di [abilitazione](/help/communities/overview.md#enablement-community) . Pacchetti Scorm supportati da AEM 6.5 Communities:

* [cq-social-scorm-package, versione 2.3.7](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/social/scorm/cq-social-scorm-pkg) che include il motore [SCORM 2017.1](https://rusticisoftware.com/blog/scorm-engine-2017-released/) .

**Per installare un pacchetto SCORM**

1. Installa il pacchetto [cq-social-scorm, versione 2.3.7](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/social/scorm/cq-social-scorm-pkg)da Package Share
1. Scaricate `/libs/social/config/scorm/database_scormengine_data.sql` dall&#39;istanza cq ed eseguitela in server mysql per creare uno schema scormEngineDB aggiornato.
1. Aggiungi `/content/communities/scorm/RecordResults` nella proprietà Esclusi percorsi nel filtro CSRF da `https://<hostname>:<port>/system/console/configMgr&#39; sugli editori.

#### Registrazione SCORM {#scorm-logging}

Durante l&#39;installazione, tutte le attività di abilitazione vengono registrate in modo dettagliato nella console del sistema.

Se desiderato, il livello di registro può essere impostato su WARN per il `RusticiSoftware.*` pacchetto.

Per utilizzare i registri, vedere [Uso dei record di controllo e dei file](/help/sites-deploying/monitoring-and-maintaining.md#working-with-audit-records-and-log-files)di registro.

### AEM Advanced MLS {#aem-advanced-mls}

Per la raccolta SRP (MSRP o DSRP) per supportare la ricerca multilingue avanzata (MLS), sono necessari nuovi plug-in Solr oltre a uno schema personalizzato e alla configurazione Solr. Tutti gli elementi richiesti vengono assemblati in un file zip scaricabile.

Il download avanzato di MLS (noto anche come &#39;phasetwo&#39;) è disponibile dall&#39;archivio di Adobe:

* [AEM-SOLR-MLS-phasetwo](https://repo.adobe.com/nexus/content/repositories/releases/com/adobe/tat/AEM-SOLR-MLS-phasetwo/1.2.40/)

   * versione 1.2.40, 6 aprile 2016
   * scarica AEM-SOLR-MLS-phasetwo-1.2.40.zip

Per informazioni dettagliate e sull&#39;installazione, visitare Configurazione [](/help/communities/solr.md) solare per SRP.

### Informazioni sui collegamenti a Package Share {#about-links-to-package-share}

**Pacchetti visibili in Adobe AEM Cloud**

I collegamenti ai pacchetti in questa pagina non richiedono alcuna istanza in esecuzione di AEM in quanto devono creare pacchetti di condivisione su `adobeaemcloud.com`. Mentre i pacchetti sono visualizzabili, il `Install`pulsante consente di installare i pacchetti in un sito ospitato da Adobe. Se si desidera eseguire l&#39;installazione in un&#39;istanza AEM locale, la selezione `Install`darà luogo a un errore.

**Come eseguire l&#39;installazione su un&#39;istanza AEM locale**

Per installare i pacchetti visibili in `adobeaemcloud.com` un’istanza AEM locale, è necessario prima scaricare il pacchetto su un disco locale:

* select the **Assets** tab
* seleziona **download su disco**

Nell&#39;istanza locale di AEM, utilizza il gestore pacchetti (ad esempio [https://localhost:4502/crx/packmgr/](https://localhost:4502/crx/packmgr/)) per caricare nell&#39;archivio pacchetti di AEM locale.

In alternativa, accedendo al pacchetto utilizzando la condivisione di pacchetti dall&#39;istanza locale di AEM (ad esempio, [https://localhost:4502/crx/packageshare/](https://localhost:4502/crx/packageshare/)), il `Download`pulsante viene scaricato nell&#39;archivio pacchetti dell&#39;istanza locale di AEM.

Una volta nell&#39;archivio pacchetti dell&#39;istanza AEM locale, utilizzate il gestore pacchetti per installare il pacchetto.

Per ulteriori informazioni, vedere [Come utilizzare i pacchetti](/help/sites-administering/package-manager.md#package-share).

## Implementazioni consigliate {#recommended-deployments}

In AEM Communities, uno store comune viene utilizzato per memorizzare il contenuto generato dall&#39;utente (UGC, user generated content) ed è spesso denominato provider di risorse di [storage (SRP)](/help/communities/working-with-srp.md). La distribuzione consigliata si basa sulla scelta di un&#39;opzione SRP per lo store comune.

Lo store comune supporta la moderazione e l&#39;analisi di UGC nell&#39;ambiente di pubblicazione, eliminando al contempo la necessità di [replicare](/help/communities/sync.md) UGC.

* [Archivio](/help/communities/working-with-srp.md) contenuti community: illustra le opzioni di storage SRP per le community AEM

* [Topologie](/help/communities/topologies.md) consigliate: illustra la topologia da utilizzare in base al caso di utilizzo e alla scelta SRP

## Aggiornamento {#upgrading}

Quando effettuate l’aggiornamento alla piattaforma AEM 6.5 dalle versioni precedenti di AEM, è importante leggere [Aggiornamento ad AEM 6.5](/help/sites-deploying/upgrade.md).

Oltre ad aggiornare la piattaforma, leggi [Aggiornamento agli AEM Communities 6.5](/help/communities/upgrade.md) per informazioni sulle modifiche apportate a Communities.

## Configurazioni {#configurations}

### Editore principale {#primary-publisher}

Se la distribuzione scelta è una farm [di](/help/communities/topologies.md#tarmk-publish-farm)pubblicazione, un&#39;istanza di pubblicazione AEM deve essere identificata come **`primary publisher`** per le attività che non devono verificarsi in tutte le istanze, ad esempio per le funzioni che si basano su **notifications **o su **Adobe  Analytics**.

Per impostazione predefinita, la configurazione `AEM Communities Publisher Configuration` OSGi è configurata con la **`Primary Publisher`** casella di controllo selezionata, in modo che tutte le istanze di pubblicazione in una farm di pubblicazione si identifichino automaticamente come principali.

Pertanto, è necessario **modificare la configurazione su tutte le istanze** di pubblicazione secondarie per deselezionare la **`Primary Publisher`** casella di controllo.

![](../assets/chlimage_1-126.png)

Per tutte le altre istanze di pubblicazione (secondarie) in una farm di pubblicazione:

* accesso con privilegi di amministratore
* accedere alla console [Web](/help/sites-deploying/configuring-osgi.md)

   * ad esempio, [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr)

* individuare la `AEM Communities Publisher Configuration`
* seleziona l’icona di modifica
* deselezionare la casella Editore **** principale
* select **Save**

### Agenti di replica sull&#39;autore {#replication-agents-on-author}

La replica viene utilizzata per il contenuto del sito creato nell&#39;ambiente di pubblicazione, ad esempio i gruppi di community, nonché per la gestione di membri e gruppi di membri dall&#39;ambiente di authoring tramite il servizio [](#tunnel-service-on-author)tunnel.

Per l&#39;editore principale, accertatevi che [Replication Agent Config](/help/sites-deploying/replication.md) identifichi correttamente il server di pubblicazione e l&#39;utente autorizzato. L&#39;utente autorizzato predefinito `admin,` dispone già delle autorizzazioni appropriate (è membro di `Communities Administrators`).

Affinché un altro utente disponga delle autorizzazioni appropriate, deve essere aggiunto come membro al gruppo di `administrators` utenti (anche membro di `Communities Administrators`).

Nell’ambiente di authoring sono disponibili due agenti di replica che richiedono la corretta configurazione del trasporto.

* accedere alla console Replica all’istanza di creazione

   * dalla navigazione globale : **Strumenti, distribuzione, replica, agenti in fase di creazione**

* seguire la stessa procedura per entrambi gli agenti:

   * **Agente predefinito (pubblicazione)**
   * **Agente replica inversa (pubblicazione invertita)**

      1. selezionare l&#39;agente
      1. select **edit**
      1. select the **Transport** tab
      1. se non la porta `4503`, modificate l&#39; **URI** per specificare la porta corretta

      1. in caso contrario, modificate `admin`l’ **utente** e la **password** per specificare un membro del gruppo di `administrators` utenti

Le immagini seguenti mostrano i risultati della modifica della porta da 4503 a 6103 tramite:

#### Agente predefinito (pubblicazione) {#default-agent-publish}

![configure-limits](../assets/configure-limits.png)

#### Agente replica inversa (pubblicazione invertita) {#reverse-replication-agent-publish-reverse}

![](../assets/chlimage_1-128.png)

### Servizio Tunnel sull&#39;autore {#tunnel-service-on-author}

Quando si utilizza l’ambiente di authoring per [creare siti](/help/communities/sites-console.md), [modificare le proprietà](/help/communities/sites-console.md#modifying-site-properties) del sito o [gestire membri](/help/communities/members.md)della comunità, è necessario accedere ai membri (utenti) registrati nell’ambiente di pubblicazione, non agli utenti registrati nell’autore.

Il servizio tunnel fornisce questo accesso tramite l&#39;agente di replica in fase di creazione.

Per abilitare il servizio tunnel:

* sull’ **autore**
* accesso con privilegi amministrativi
* se l&#39;editore non è localhost:4503 o l&#39;utente del trasporto non lo è, `admin`[configurare l&#39;agente di replica](#replication-agents-on-author)

* accedere alla console [Web](/help/sites-deploying/configuring-osgi.md)

   * ad esempio, [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)

* individuare la `AEM Communities Publish Tunnel Service`
* seleziona l’icona di modifica
* selezionare **enable **box
* select **Save**

![](../assets/chlimage_1-129.png)

### Replicare la chiave Crypto {#replicate-the-crypto-key}

Esistono due funzioni dei AEM Communities che richiedono che tutte le istanze del server AEM utilizzino le stesse chiavi di crittografia. Questi sono [Analytics](/help/communities/analytics.md) e [ASRP](/help/communities/asrp.md).

A partire da AEM 6.3, il materiale chiave viene memorizzato nel file system e non più nell’archivio.

Per copiare il materiale chiave dall’autore a tutte le altre istanze, è necessario:

* accedere all’istanza di AEM, in genere un’istanza di creazione, che contiene il materiale chiave da copiare

   * individuare il `com.adobe.granite.crypto.file` bundle nel file system locale, ad esempio

      * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21`
      * il `bundle.info` file identificherà il bundle
   * ad esempio, passare alla cartella di dati,

      * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`
   * copiare i file hmac e i file dei nodi principali



* per ogni istanza AEM di destinazione

   * ad esempio, passare alla cartella di dati,

      * `<publish-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`
   * incollare i 2 file precedentemente copiati
   * è necessario [aggiornare il bundle](#refresh-the-granite-crypto-bundle) Granite Crypto se l’istanza AEM di destinazione è in esecuzione


>[!CAUTION]
>
>Se è già stata configurata un&#39;altra funzione di protezione basata sulle chiavi di crittografia, la replica delle chiavi di crittografia potrebbe danneggiare la configurazione. Per assistenza, [contattate l&#39;assistenza](https://helpx.adobe.com/it/marketing-cloud/contact-support.html)clienti.

#### Replica archivio {#repository-replication}

È possibile conservare il materiale chiave memorizzato nell’archivio, come nel caso di AEM 6.2 e versioni precedenti, specificando la seguente proprietà di sistema al primo avvio di ogni istanza di AEM (che crea l’archivio iniziale):

* `-Dcom.adobe.granite.crypto.file.disable=true`

>[!NOTE]
>
>È importante verificare che l&#39;agente di [replica nell&#39;istanza di creazione](#replication-agents-on-author) sia configurato correttamente.

Con il materiale chiave memorizzato nella directory archivio, la procedura per replicare la chiave di crittografia dall’autore ad altre istanze è la seguente:

Utilizzando [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md) :

* individuare [https://&lt;server>:&lt;porta>/crx/de](https://localhost:4502/crx/de)
* select `/etc/key`
* apri `Replication` scheda
* select `Replicate`

* [aggiorna il bundle Granite Crypto](#refresh-the-granite-crypto-bundle)

![](../assets/chlimage_1-130.png)

#### Aggiornare il pacchetto Granite Crypto {#refresh-the-granite-crypto-bundle}

* per ogni istanza di pubblicazione, accedete alla console [Web](/help/sites-deploying/configuring-osgi.md)

   * ad esempio, [https://&lt;server>:&lt;porta>/system/console/bundle](https://localhost:4503/system/console/bundles)

* locate `Adobe Granite Crypto Support` bundle (com.adobe.granite.crypto)
* seleziona **Aggiorna**

![](../assets/chlimage_1-131.png)

* dopo un momento, dovrebbe comparire una finestra di dialogo **Success **Success :
   `Operation completed successfully.`

### Apache HTTP Server {#apache-http-server}

Se utilizzate il server Apache HTTP, accertatevi di utilizzare il nome server corretto per tutte le voci pertinenti.

In particolare, fate attenzione a utilizzare il nome corretto del server, non `localhost`nel `RedirectMatch`.

#### httpd.conf, esempio {#httpd-conf-sample}

```shell
<IfModule alias_module>
     # XAMPP does not have a favicon; this prevents any 404 errors which may arise.
     Redirect 404 /favicon.ico
     <Location /favicon.ico>
         ErrorDocument 404 "No favicon"
     </Location>

    # Return from "Sign Out" generates response header directing you to "/", generating a 404 error
    # The RedirectMatch resolves it correctly when modified for the target Community Site :
    RedirectMatch ^/$ https://[server name]/content/sites/engage/en.html
 ...
 </IfModule>
```

### Dispatcher {#dispatcher}

Se si utilizza un Dispatcher, vedere:

* Documentazione di AEM su [Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html)
* [Installazione di Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-install.html)
* [Configurazione di Dispatcher per Communities](/help/communities/dispatcher.md)
* [Problemi noti](/help/communities/troubleshooting.md#dispatcher-refetch-fails)

## Documentazione di Community correlate {#related-communities-documentation}

* Visitate [Administering Communities Sites](/help/communities/administer-landing.md) per informazioni su come creare un sito community, configurare modelli di sito community, moderare i contenuti della community, gestire i membri e configurare i messaggi.

* Visitate [Developing Communities](/help/communities/communities.md) per informazioni sul framework dei componenti sociali (SCF) e sulla personalizzazione dei componenti e delle funzionalità di Communities.

* Per informazioni su come creare e configurare i componenti di Community, consulta [Authoring dei componenti](/help/communities/author-communities.md) di Communities.

