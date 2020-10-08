---
title: Implementazione di Communities
seo-title: Implementazione di Communities
description: Come distribuire  AEM Communities
seo-description: Come distribuire  AEM Communities
uuid: 18d9b424-004d-43b2-968a-318e27a93759
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
content-type: reference
topic-tags: deploying
discoiquuid: c8d7355f-5a70-40d1-bf22-62fab8002ea0
docset: aem65
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '1899'
ht-degree: 2%

---


# Implementazione di Communities{#deploying-communities}

## Prerequisiti {#prerequisites}

* [Piattaforma AEM 6.5](/help/sites-deploying/deploy.md)

*  licenza AEM Communities

* Licenze facoltative per:

   * [Funzioni di  Adobe Analytics per Communities](/help/communities/analytics.md)
   * [MongoDB per MSRP](/help/communities/msrp.md)
   * [Adobe Cloud per ASRP](/help/communities/asrp.md)

## Elenco di controllo dell&#39;installazione {#installation-checklist}

**Per la piattaforma[AEM](/help/sites-deploying/deploy.md#what-is-aem)**

* Installa gli ultimi aggiornamenti [AEM 6.5](#aem64updates)

* Se non si utilizzano le porte predefinite (4502, 4503), [configurare gli agenti di replica](#replication-agents-on-author)
* [Replicare la chiave di crittografia](#replicate-the-crypto-key)
* Se supporta la globalizzazione, [imposta la traduzione](/help/sites-administering/translation.md)automatica (è disponibile l&#39;impostazione di esempio per lo sviluppo)

**Per la funzionalità[Community](/help/communities/overview.md)**

* Se distribuite una farm [di](/help/sites-deploying/recommended-deploys.md#tarmk-farm)pubblicazione, [identificate l&#39;editore principale](#primary-publisher)

* [Abilita il servizio tunnel](#tunnel-service-on-author)
* [Abilita login per social network](/help/communities/social-login.md#adobe-granite-oauth-authentication-handler)
* [Configurare  Adobe Analytics](/help/communities/analytics.md)
* Impostazione di un servizio e-mail [predefinito](/help/communities/email.md)
* Identificare la scelta per lo storage [UGC](/help/communities/working-with-srp.md) condiviso (**SRP**)

   * Se MongoDB SRP [(MSRP)](/help/communities/msrp.md)

      * [Installare e configurare MongoDB](/help/communities/msrp.md#mongodb-configuration)
      * [Configura Solr](/help/communities/solr.md)
      * [Select MSRP](/help/communities/srp-config.md)
   * Se il database relazionale SRP [(DSRP)](/help/communities/dsrp.md)

      * [Installare il driver JDBC per MySQL](#jdbc-driver-for-mysql)
      * [Installare e configurare MySQL per DSRP](/help/communities/dsrp-mysql.md)
      * [Configura Solr](/help/communities/solr.md)
      * [Seleziona DSRP](/help/communities/srp-config.md)
   * Se  Adobe SRP [(ASRP)](/help/communities/asrp.md)

      * Consultate il rappresentante commerciale di riferimento per il provisioning
      * [Seleziona ASRP](/help/communities/srp-config.md)
   * Se JCR SRP [(JSRP)](/help/communities/jsrp.md)

      * Store UGC non condiviso:

         * UGC non è mai replicato
         * UGC visibile solo su AEM&#39;istanza o cluster in cui è stato immesso

         * Il valore predefinito è JSRP
   Per la funzione di **[abilitazione](/help/communities/overview.md#enablement-community)**

   * [Installare e configurare FFmpeg](/help/communities/ffmpeg.md)
   * [Installare il driver JDBC per MySQL](#jdbc-driver-for-mysql)
   * [Installazione  AEM Communities SCORM Engine](#scorm-package)
   * [Installazione e configurazione di MySQL per l&#39;abilitazione](/help/communities/mysql.md)





## Latest Releases {#latest-releases}

AEM 6.5 Communities GA navi con il pacchetto Community. Per informazioni sugli aggiornamenti di AEM 6.5 [Communities](/help/release-notes/release-notes.md#experiencemanagercommunities), consulta [AEM Note](/help/release-notes/release-notes.md#communities-release-notes.html)sulla versione 6.5.

### Aggiornamenti di AEM 6.5 {#aem-updates}

A partire dal AEM 6.4, gli aggiornamenti alle Community vengono forniti come parte AEM Cumulative Fix Pack e Service Pack.

Per gli ultimi aggiornamenti a AEM 6.5, consulta [Adobe Experience Manager 6.4 Cumulative Fix Pack e Service Pack](https://helpx.adobe.com/it/experience-manager/aem-releases-updates.html).

### Cronologia versioni {#version-history}

Come AEM 6.4 e oltre,  funzionalità AEM Communities e hotfix fanno parte  pacchetti di correzioni e Service Pack cumulativi AEM Communities. Non esistono pertanto pacchetti di caratteristiche distinti.

### Driver JDBC per MySQL {#jdbc-driver-for-mysql}

Due funzionalità Community utilizzano un database MySQL:

* Per [l&#39;abilitazione](/help/communities/enablement.md): registrazione delle attività SCORM e degli studenti
* Per [DSRP](/help/communities/dsrp.md): memorizzazione di contenuto generato dall&#39;utente (UGC)

Il connettore MySQL deve essere ottenuto e installato separatamente.

Le misure necessarie sono:

1. Scaricate l&#39;archivio ZIP da [https://dev.mysql.com/downloads/connector/j/](https://dev.mysql.com/downloads/connector/j/)

   * La versione deve essere >= 5.1.38

1. Estrarre mysql-Connector-java-&lt;versione>-bin.jar (bundle) dall&#39;archivio
1. Utilizzate la console Web per installare e avviare il bundle:

   * Ad esempio, https://localhost:4502/system/console/bundles
   * Seleziona **`Install/Update`**
   * Sfoglia... per selezionare il bundle estratto dall&#39;archivio ZIP scaricato
   * Verificare che il driver JDBC di *Oracle Corporation per MySQLcom.mysql.jdbc* sia attivo e avviarlo in caso contrario (o controllare i registri)

1. Se l&#39;installazione avviene su una distribuzione esistente dopo la configurazione di JDBC, eseguire un nuovo riferimento JDBC al nuovo connettore salvando nuovamente la configurazione JDBC dalla console Web:
   * Ad esempio, https://localhost:4502/system/console/configMgr
   * Individua `Day Commons JDBC Connections Pool` configurazione
   * Seleziona per aprire
   * Seleziona `Save`

1. Ripetere i passaggi 3 e 4 per tutte le istanze di creazione e pubblicazione

Ulteriori informazioni sull&#39;installazione dei bundle sono disponibili nella pagina Console [](/help/sites-deploying/web-console.md) Web.

#### Esempio: Bundle del connettore MySQL installato {#example-installed-mysql-connector-bundle}

![pacchi di limaggio](assets/chlimage-bundles.png)

### Pacchetto SCORM {#scorm-package}

SCORM (Shareable Content Object Reference Model) è una raccolta di standard e specifiche per l&#39;e-learning. SCORM definisce anche come il contenuto può essere incluso in un file ZIP trasferibile.

Il motore  AEM Communities SCORM è richiesto per la funzione di [abilitazione](/help/communities/overview.md#enablement-community) . Pacchetti Scorm supportati da AEM 6.5 Communities:

* [cq-social-scorm-package, versione 2.3.7](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/social/scorm/cq-social-scorm-pkg) che include il motore [SCORM 2017.1](https://rusticisoftware.com/blog/scorm-engine-2017-released/) .

**Per installare un pacchetto SCORM**

1. Installate il pacchetto [cq-social-scorm, versione 2.3.7](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/social/scorm/cq-social-scorm-pkg) , da Package Share.
1. Scaricate `/libs/social/config/scorm/database_scormengine_data.sql` dall&#39;istanza cq ed eseguitela in server mysql per creare uno schema scormEngineDB aggiornato.
1. Aggiungi `/content/communities/scorm/RecordResults` nella proprietà Percorsi esclusi nel filtro CSRF dagli `https://<hostname>:<port>/system/console/configMgr` editori.


#### Registrazione SCORM {#scorm-logging}

Durante l&#39;installazione, tutte le attività di abilitazione vengono registrate in modo dettagliato nella console del sistema.

Se desiderato, il livello di registro può essere impostato su WARN per il `RusticiSoftware.*` pacchetto.

Per utilizzare i registri, vedere [Uso dei record di controllo e dei file](/help/sites-deploying/monitoring-and-maintaining.md#working-with-audit-records-and-log-files)di registro.

### AEM Advanced MLS {#aem-advanced-mls}

Per la raccolta SRP (MSRP o DSRP) per supportare la ricerca multilingue avanzata (MLS), sono necessari nuovi plug-in Solr oltre a uno schema personalizzato e alla configurazione Solr. Tutti gli elementi richiesti vengono assemblati in un file zip scaricabile.

Il download avanzato MLS (noto anche come &#39;phasetwo&#39;) è disponibile dall&#39;archivio del Adobe :

* [AEM-SOLR-MLS-phasetwo](https://repo.adobe.com/nexus/content/repositories/releases/com/adobe/tat/AEM-SOLR-MLS-phasetwo/1.2.40/)

   * Versione 1.2.40, 6 aprile 2016
   * Scarica AEM-SOLR-MLS-phasetwo-1.2.40.zip

Per informazioni dettagliate e sull&#39;installazione, visitare Configurazione [](/help/communities/solr.md) solare per SRP.

### Informazioni sui collegamenti a Package Share {#about-links-to-package-share}

**Pacchetti visibili in  Adobe AEM Cloud**

I collegamenti ai pacchetti in questa pagina non richiedono alcuna istanza di AEM in esecuzione, in quanto devono creare pacchetti di condivisione `adobeaemcloud.com`. Mentre i pacchetti sono visualizzabili, il `Install` pulsante consente di installare i pacchetti in un sito ospitato in un Adobe . Se si desidera eseguire l&#39;installazione in un&#39;istanza AEM locale, la selezione `Install` genererà un errore.

**Come eseguire l&#39;installazione sull&#39;istanza AEM locale**

Per installare i pacchetti visibili in `adobeaemcloud.com` un&#39;istanza AEM locale, è necessario prima scaricare il pacchetto su un disco locale:

* Select the **Assets** tab
* Seleziona **download su disco**

Nell&#39;istanza AEM locale, utilizzate il gestore pacchetti (ad esempio [https://localhost:4502/crx/packmgr/](https://localhost:4502/crx/packmgr/)) per caricare nell&#39;archivio AEM pacchetti locale.

In alternativa, accedendo al pacchetto utilizzando la condivisione del pacchetto dall&#39;istanza AEM locale (ad esempio, [https://localhost:4502/crx/packageshare/](https://localhost:4502/crx/packageshare/)), il `Download` pulsante verrà scaricato nell&#39;archivio del pacchetto dell&#39;istanza AEM locale.

Una volta entrati nell&#39;archivio pacchetti dell&#39;istanza AEM locale, utilizzate il gestore pacchetti per installare il pacchetto.

Per ulteriori informazioni, vedere [Come utilizzare i pacchetti](/help/sites-administering/package-manager.md#package-share).

## Implementazioni consigliate {#recommended-deployments}

In  AEM Communities, uno store comune viene utilizzato per memorizzare il contenuto generato dall&#39;utente (UGC) ed è spesso denominato fornitore di risorse di [storage (SRP)](/help/communities/working-with-srp.md). La distribuzione consigliata si basa sulla scelta di un&#39;opzione SRP per lo store comune.

Lo store comune supporta la moderazione e l&#39;analisi di UGC nell&#39;ambiente di pubblicazione, eliminando al contempo la necessità di [replicare](/help/communities/sync.md) UGC.

* [Archivio](/help/communities/working-with-srp.md) contenuti community: illustra le opzioni di storage SRP per le comunità AEM

* [Topologie](/help/communities/topologies.md) consigliate: illustra la topologia da utilizzare in base al caso di utilizzo e alla scelta SRP

## Aggiornamento {#upgrading}

Quando eseguite l&#39;aggiornamento alla piattaforma AEM 6.5 dalle versioni precedenti di AEM, è importante leggere [Aggiornamento a AEM 6.5](/help/sites-deploying/upgrade.md).

Oltre ad aggiornare la piattaforma, leggi [Aggiornamento ad  AEM Communities 6.5](/help/communities/upgrade.md) per informazioni sulle modifiche apportate a Communities.

## Configurazioni {#configurations}

### Editore principale {#primary-publisher}

Se la distribuzione scelta è una farm [di](/help/communities/topologies.md#tarmk-publish-farm)pubblicazione, un&#39;istanza AEM pubblicazione deve essere identificata come **`primary publisher`** per le attività che non devono verificarsi in tutte le istanze, ad esempio per le funzioni che si basano su **notifiche** o su **Adobe Analytics**.

Per impostazione predefinita, la configurazione `AEM Communities Publisher Configuration` OSGi è configurata con la **`Primary Publisher`** casella di controllo selezionata, in modo che tutte le istanze di pubblicazione in una farm di pubblicazione si identifichino automaticamente come principali.

Pertanto, è necessario **modificare la configurazione su tutte le istanze** di pubblicazione secondarie per deselezionare la **`Primary Publisher`** casella di controllo.

![chlimage_1-411](assets/chlimage_1-411.png)

Per tutte le altre istanze di pubblicazione (secondarie) in una farm di pubblicazione:

* Accesso con privilegi di amministratore
* Accedere alla console [Web](/help/sites-deploying/configuring-osgi.md)

   * Ad esempio, [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr)

* Individua la variabile `AEM Communities Publisher Configuration`
* Selezionate l’icona di modifica
* Deselezionare la casella Editore **** principale
* Seleziona **Salva**

### Agenti di replica sull&#39;autore {#replication-agents-on-author}

La replica viene utilizzata per il contenuto del sito creato nell&#39;ambiente di pubblicazione, ad esempio i gruppi di community, nonché per la gestione di membri e gruppi di membri dall&#39;ambiente di authoring tramite il servizio [](#tunnel-service-on-author)tunnel.

Per l&#39;editore principale, accertatevi che [Replication Agent Config](/help/sites-deploying/replication.md) identifichi correttamente il server di pubblicazione e l&#39;utente autorizzato. L&#39;utente autorizzato predefinito `admin,` dispone già delle autorizzazioni appropriate (è membro di `Communities Administrators`).

Affinché un altro utente disponga delle autorizzazioni appropriate, deve essere aggiunto come membro al gruppo di `administrators` utenti (anche membro di `Communities Administrators`).

Nell’ambiente di authoring sono disponibili due agenti di replica che richiedono la corretta configurazione del trasporto.

* Accedere alla console Replica durante l’authoring

   * Dalla navigazione globale, andate a **[!UICONTROL Strumenti]** > **[!UICONTROL Distribuzione]** > **[!UICONTROL Replica]** > **[!UICONTROL Agenti sull’autore]**

* Seguire la stessa procedura per entrambi gli agenti:

   * **Agente predefinito (pubblicazione)**
   * **Agente replica inversa (pubblicazione invertita)**

      1. Selezionare l&#39;agente
      1. Select **edit**
      1. Select the **Transport** tab
      1. Se non è una porta `4503`, modificate l&#39; **URI** per specificare la porta corretta

      1. In caso contrario, modificate `admin`l’ **utente** e la **password** per specificare un membro del gruppo di `administrators` utenti

Le immagini seguenti mostrano i risultati della modifica della porta da 4503 a 6103 tramite:

#### Agente predefinito (pubblicazione) {#default-agent-publish}

![chlimage_1-412](assets/chlimage_1-412.png)

#### Agente replica inversa (pubblicazione invertita) {#reverse-replication-agent-publish-reverse}

![chlimage_1-413](assets/chlimage_1-413.png)

### Servizio Tunnel sull&#39;autore {#tunnel-service-on-author}

Quando si utilizza l’ambiente di authoring per [creare siti](/help/communities/sites-console.md), [modificare le proprietà](/help/communities/sites-console.md#modifying-site-properties) del sito o [gestire membri](/help/communities/members.md)della comunità, è necessario accedere ai membri (utenti) registrati nell’ambiente di pubblicazione, non agli utenti registrati nell’autore.

Il servizio tunnel fornisce questo accesso tramite l&#39;agente di replica in fase di creazione.

Per abilitare il servizio tunnel:

* Effettuate l’accesso con privilegi amministrativi nell’istanza di authoring.
* Se l&#39;editore non è localhost:4503 o l&#39;utente del trasporto non lo è, `admin`[configurare l&#39;agente di replica](#replication-agents-on-author)

* Accesso alla console [Web](/help/sites-deploying/configuring-osgi.md)

   * Ad esempio, [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)

* Individua la variabile `AEM Communities Publish Tunnel Service`
* Selezionate l’icona di modifica
* Selezionare la casella di **attivazione**
* Seleziona **Salva**

   ![chlimage_1-414](assets/chlimage_1-414.png)

### Replicare la chiave Crypto {#replicate-the-crypto-key}

Esistono due funzionalità di  AEM Communities che richiedono che tutte AEM istanze del server utilizzino le stesse chiavi di crittografia. Si tratta di [Analytics](/help/communities/analytics.md) e [ASRP](/help/communities/asrp.md).

A partire dal AEM 6.3, il materiale chiave è memorizzato nel file system e non più nella directory archivio.

Per copiare il materiale chiave dall’autore a tutte le altre istanze, è necessario:

* Accedere all&#39;istanza AEM, in genere un&#39;istanza di creazione, che contiene il materiale chiave da copiare

   * Individuare il `com.adobe.granite.crypto.file` bundle nel file system locale, ad esempio

      * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21`
      * Il `bundle.info` file identificherà il bundle
   * Individuare la cartella di dati, ad esempio

      * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`

      * Copiare i file hmac e i file dei nodi principali


* Per ogni istanza di AEM di destinazione

   * Individuare la cartella di dati, ad esempio

      * `<publish-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`
   * Incolla i 2 file precedentemente copiati
   * È necessario [aggiornare il bundle](#refresh-the-granite-crypto-bundle) Granite Crypto se l&#39;istanza AEM di destinazione è in esecuzione


>[!CAUTION]
>
>Se è già stata configurata un&#39;altra funzione di protezione basata sulle chiavi di crittografia, la replica delle chiavi di crittografia potrebbe danneggiare la configurazione. Per assistenza, [contattate l&#39;assistenza](https://helpx.adobe.com/it/marketing-cloud/contact-support.html)clienti.

#### Replica archivio {#repository-replication}

È possibile conservare il materiale chiave memorizzato nell&#39;archivio, come nel caso di AEM 6.2 e versioni precedenti, specificando la seguente proprietà di sistema al primo avvio di ogni istanza AEM (che crea l&#39;archivio iniziale):

* `-Dcom.adobe.granite.crypto.file.disable=true`

>[!NOTE]
>
>È importante verificare che l&#39;agente di [replica nell&#39;istanza di creazione](#replication-agents-on-author) sia configurato correttamente.

Con il materiale chiave memorizzato nella directory archivio, la procedura per replicare la chiave di crittografia dall’autore ad altre istanze è la seguente:

Utilizzo di [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md):

* Passa a [https://&lt;server>:&lt;porta>/crx/de](https://localhost:4502/crx/de)
* Seleziona `/etc/key`
* Apri, `Replication` scheda
* Seleziona `Replicate`

* [Aggiornare il bundle Granite Crypto](#refresh-the-granite-crypto-bundle)

   ![chlimage_1-415](assets/chlimage_1-415.png)

#### Aggiornare il pacchetto Granite Crypto {#refresh-the-granite-crypto-bundle}

* Per ogni istanza di pubblicazione, accedete alla console [Web](/help/sites-deploying/configuring-osgi.md)

   * Ad esempio, [https://&lt;server>:&lt;porta>/system/console/bundle](https://localhost:4503/system/console/bundles)

* Individua `Adobe Granite Crypto Support` bundle (com.adobe.granite.crypto)
* Seleziona **aggiornamento**

   ![chlimage_1-416](assets/chlimage_1-416.png)

* Dopo un momento, dovrebbe comparire una finestra di dialogo **Successo** :
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

Se utilizzi un dispatcher, vedi:

* Documentazione [del dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html) AEM
* [Installazione di Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-install.html)
* [Configurazione del dispatcher per Communities](/help/communities/dispatcher.md)
* [Problemi noti](/help/communities/troubleshooting.md#dispatcher-refetch-fails)

## Documentazione di Community correlate {#related-communities-documentation}

* Visitate [Administering Communities Sites](/help/communities/administer-landing.md) per informazioni su come creare un sito community, configurare modelli di sito community, moderare i contenuti della community, gestire i membri e configurare i messaggi.

* Visitate [Developing Communities](/help/communities/communities.md) per informazioni sul framework dei componenti sociali (SCF) e sulla personalizzazione dei componenti e delle funzionalità di Communities.

* Per informazioni su come creare e configurare i componenti di Community, consulta [Authoring dei componenti](/help/communities/author-communities.md) di Communities.

