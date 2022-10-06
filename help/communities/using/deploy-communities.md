---
title: Distribuzione di Communities
seo-title: Deploying Communities
description: Come distribuire AEM Communities
seo-description: How to deploy AEM Communities
content-type: reference
topic-tags: deploying
source-git-commit: 14a33b14043869614efcdbf8cb413333d0fa644b
workflow-type: tm+mt
source-wordcount: '1881'
ht-degree: 2%

---


# Distribuzione di Communities{#deploying-communities}

## Prerequisiti {#prerequisites}

* [Piattaforma AEM 6.5](/help/sites-deploying/deploy.md)

* Licenza AEM Communities

* Licenze opzionali per:

   * [Funzioni di Adobe Analytics for Communities](/help/communities/analytics.md)
   * [MongoDB per MSRP](/help/communities/msrp.md)
   * [Adobe Cloud per ASRP](/help/communities/asrp.md)

## Elenco di controllo dell&#39;installazione {#installation-checklist}

**Per [piattaforma AEM](/help/sites-deploying/deploy.md#what-is-aem)**:

* Installa la versione più recente [Aggiornamenti di AEM 6.5](#aem64updates).

* Se non si utilizzano le porte predefinite (4502, 4503), allora [configurare gli agenti di replica](#replication-agents-on-author).
* [Replicare la chiave di crittografia](#replicate-the-crypto-key)
* Sostenere la globalizzazione, [configurazione della traduzione automatica](/help/sites-administering/translation.md)
(è disponibile l’impostazione di esempio per lo sviluppo).

**Per [Funzionalità community](/help/communities/overview.md)**:

* Se distribuisci un [pubblica azienda](/help/sites-deploying/recommended-deploys.md#tarmk-farm), [identificare l&#39;editore principale](#primary-publisher)

* [Attiva il servizio tunnel](#tunnel-service-on-author)
* [Abilita accesso social](/help/communities/social-login.md#adobe-granite-oauth-authentication-handler)
* [Configurare Adobe Analytics](/help/communities/analytics.md)
* Imposta un [servizio e-mail predefinito](/help/communities/email.md)
* Identifica la scelta per [archiviazione UGC condivisa](/help/communities/working-with-srp.md) (**SRP**)

   * Se MongoDB SRP [(MSRP)](/help/communities/msrp.md)

      * [Installare e configurare MongoDB](/help/communities/msrp.md#mongodb-configuration)
      * [Configura Solr](/help/communities/solr.md)
      * [Seleziona MSRP](/help/communities/srp-config.md)
   * Se SRP database relazionale [(DSRP)](/help/communities/dsrp.md)

      * [Installare il driver JDBC per MySQL](#jdbc-driver-for-mysql)
      * [Installare e configurare MySQL per DSRP](/help/communities/dsrp-mysql.md)
      * [Configura Solr](/help/communities/solr.md)
      * [Seleziona DSRP](/help/communities/srp-config.md)
   * Se Adobe SRP [(ASRP)](/help/communities/asrp.md)

      * Collabora con il rappresentante del tuo account per il provisioning.
      * [Seleziona ASRP](/help/communities/srp-config.md)
   * Se JCR SRP [(JSRP)](/help/communities/jsrp.md)

      * Non è un archivio UGC condiviso:

         * UGC non viene mai replicato.
         * UGC è visibile solo su AEM&#39;istanza o cluster in cui è stato inserito.
      * Il valore predefinito è JSRP

   Per **[funzione di abilitazione](/help/communities/overview.md#enablement-community)**

   * [Installare e configurare FFmpeg](/help/communities/ffmpeg.md)
   * [Installare il driver JDBC per MySQL](#jdbc-driver-for-mysql)
   * [Installare AEM Communities SCORM-Engine](#scorm-package)
   * [Installare e configurare MySQL per l&#39;abilitazione](/help/communities/mysql.md)






## Versioni più recenti {#latest-releases}

AEM 6.5 Communities GA include il pacchetto Community. Per informazioni sugli aggiornamenti a AEM 6.5 [Community](/help/release-notes/release-notes.md#experiencemanagercommunities), fai riferimento a [Note sulla versione di AEM 6.5](/help/release-notes/release-notes.md#communities-release-notes.html).

### Aggiornamenti di AEM 6.5 {#aem-updates}

A partire dalla AEM 6.4, gli aggiornamenti alle Community vengono forniti come parte di AEM Cumulative Fix Pack e Service Pack.

Per gli ultimi aggiornamenti a AEM 6.5, vedi [Adobe Experience Manager 6.4 Cumulative Fix Pack e Service Pack](https://helpx.adobe.com/it/experience-manager/aem-releases-updates.html).

### Cronologia versioni {#version-history}

Come in AEM 6.4 e versioni successive, le funzioni e gli hotfix di AEM Communities fanno parte dei pacchetti correzioni cumulativi e dei Service Pack di AEM Communities. Non esistono pertanto pacchetti di funzioni separati.

### Driver JDBC per MySQL {#jdbc-driver-for-mysql}

Due funzionalità di Communities utilizzano un database MySQL:

* Per [abilitazione](/help/communities/enablement.md): registrazione di attività SCORM e studenti
* Per [DSRP](/help/communities/dsrp.md): archiviazione di contenuti generati dall’utente (UGC)

Il connettore MySQL deve essere ottenuto e installato separatamente.

Le misure necessarie sono:

1. Scarica l&#39;archivio ZIP da [https://dev.mysql.com/downloads/connector/j/](https://dev.mysql.com/downloads/connector/j/)

   * La versione deve essere >= 5.1.38

1. Estrai `mysql-connector-java-&lt;version&gt;-bin.jar (bundle) from the archive`
1. Usa la console web per installare e avviare il bundle :

   * Ad esempio, https://localhost:4502/system/console/bundles
   * Seleziona **`Install/Update`**
   * Sfoglia... per selezionare il bundle estratto dall&#39;archivio ZIP scaricato
   * Controlla che *Driver JDBC di Oracle Corporation per MySQLcom.mysql.jdbc* è attivo e avvialo in caso contrario (o controlla i registri)

1. Se esegui l’installazione su un’implementazione esistente dopo la configurazione di JDBC, effettua un rebind JDBC al nuovo connettore salvando nuovamente la configurazione JDBC dalla console Web :

   * Ad esempio, https://localhost:4502/system/console/configMgr
   * Individua `Day Commons JDBC Connections Pool` e seleziona per aprire la configurazione.
   * Seleziona `Save`.

1. Ripeti i passaggi 3 e 4 su tutte le istanze di authoring e pubblicazione.

Ulteriori informazioni sull&#39;installazione dei bundle sono disponibili sul [Console web](/help/sites-deploying/web-console.md#bundles) pagina.

#### Esempio : Bundle del connettore MySQL installato {#example-installed-mysql-connector-bundle}

![](../assets/mysql-connector.png)

### Pacchetto SCORM {#scorm-package}

SCORM (Shared Content Object Reference Model) è una raccolta di standard e specifiche per l&#39;e-learning. SCORM definisce anche come il contenuto può essere confezionato in un file ZIP trasferibile.

Il motore AEM Communities SCORM è richiesto per [abilitazione](/help/communities/overview.md#enablement-community) funzionalità. Pacchetti Scorm supportati su AEM 6.5 Communities:

* [cq-social-scorm-package, versione 2.3.7](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/social/scorm/cq-social-scorm-pkg) che include [SCORM 2017.1](https://rusticisoftware.com/blog/scorm-engine-2017-released/) motore.

**Per installare un pacchetto SCORM**

1. Installa il [cq-social-scorm-package, versione 2.3.7](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/social/scorm/cq-social-scorm-pkg) da Package Share
1. Scarica `/libs/social/config/scorm/database_scormengine_data.sql` dall&#39;istanza cq e eseguiscila in mysql server per creare uno schema scormEngineDB aggiornato.
1. Aggiungi `/content/communities/scorm/RecordResults` in Proprietà Percorsi esclusi nel filtro CSRF da `https://<hostname>:<port>/system/console/configMgr` sugli editori.

#### Registrazione SCORM {#scorm-logging}

Come installato, tutte le attività di abilitazione vengono registrate in modo dettagliato nella console di sistema.

Se lo desideri, puoi impostare il livello di log su WARN per `RusticiSoftware.*` pacchetto.

Per lavorare con i registri, consulta [Utilizzo dei record di controllo e dei file di registro](/help/sites-deploying/monitoring-and-maintaining.md#working-with-audit-records-and-log-files).

### MLS avanzate AEM {#aem-advanced-mls}

Per la raccolta SRP (MSRP o DSRP) per supportare la ricerca multilingue avanzata (MLS), sono necessari nuovi plug-in Solr oltre a uno schema personalizzato e una configurazione Solr. Tutti gli elementi richiesti vengono assemblati in un file zip scaricabile.

Il download avanzato di MLS (noto anche come &quot;phasetwo&quot;) è disponibile dall’archivio Adobe :

* [Fasetwo AEM-SOLR-MLS](https://repo1.maven.org/maven2/com/adobe/tat/AEM-SOLR-MLS-phasetwo/1.2.40/)

   * Versione 1.2.40, 6 aprile 2016
   * Scarica AEM-SOLR-MLS-phasetwo-1.2.40.zip

Per informazioni dettagliate e sull&#39;installazione, visita [Configurazione Solr](/help/communities/solr.md) per SRP

### Informazioni sui collegamenti alla condivisione dei pacchetti {#about-links-to-package-share}

**Pacchetti visibili in Adobe AEM Cloud**

I collegamenti ai pacchetti in questa pagina non richiedono alcuna istanza in esecuzione di AEM in quanto devono condividere i pacchetti in `adobeaemcloud.com`. Mentre i pacchetti sono visualizzabili, la `Install` Il pulsante è per installare i pacchetti in un sito ospitato da Adobe. Se si desidera eseguire l&#39;installazione in un&#39;istanza AEM locale, selezionare `Install` genererà un errore.

**Come eseguire l&#39;installazione su un&#39;istanza AEM locale**

Per installare i pacchetti visibili in `adobeaemcloud.com` in un&#39;istanza AEM locale, il pacchetto deve prima essere scaricato su un disco locale :

* Seleziona la **Risorse** scheda
* Seleziona **scaricare su disco**

Nell’istanza di AEM locale, utilizza il gestore dei pacchetti (ad esempio [https://localhost:4502/crx/packmgr/](https://localhost:4502/crx/packmgr/)), per caricare nell’archivio locale dei pacchetti AEM.

In alternativa, puoi accedere al pacchetto utilizzando la condivisione del pacchetto dall’istanza AEM locale (ad esempio, [https://localhost:4502/crx/packageshare/](https://localhost:4502/crx/packageshare/)), `Download` verrà scaricato nell’archivio dei pacchetti dell’istanza AEM locale.

Una volta nell&#39;archivio dei pacchetti dell&#39;istanza AEM locale, utilizza il gestore dei pacchetti per installare il pacchetto.

Per ulteriori informazioni, visita [Come lavorare con i pacchetti](/help/sites-administering/package-manager.md#package-share).

## Implementazioni consigliate {#recommended-deployments}

In AEM Communities, un archivio comune viene utilizzato per memorizzare i contenuti generati dagli utenti (UGC) e viene spesso indicato come [provider di risorse di archiviazione (SRP)](/help/communities/working-with-srp.md). La distribuzione consigliata si basa sulla scelta di un’opzione SRP per lo store comune.

L&#39;archivio comune supporta la moderazione e l&#39;analisi degli UGC nell&#39;ambiente di pubblicazione, eliminando al contempo la necessità di [replica](/help/communities/sync.md) dell&#39;UGC.

* [Archivio dei contenuti della community](/help/communities/working-with-srp.md) : illustra le opzioni di storage SRP per le AEM community

* [Topologie consigliate](/help/communities/topologies.md) : discute la topologia da utilizzare in base al caso d’uso e alla scelta dell’SRP

## Aggiornamento {#upgrading}

Quando esegui l’aggiornamento alla piattaforma AEM 6.5 dalle versioni precedenti di AEM, è importante leggere [Aggiornamento a AEM 6.5](/help/sites-deploying/upgrade.md).

Oltre all’aggiornamento della piattaforma, consulta [Aggiornamento ad AEM Communities 6.5](/help/communities/upgrade.md) per informazioni sulle modifiche apportate a Communities.

## Configurazioni {#configurations}

### Editore principale {#primary-publisher}

Quando la distribuzione scelta è un [pubblica azienda](/help/communities/topologies.md#tarmk-publish-farm), quindi un&#39;istanza di pubblicazione AEM deve essere identificata come **`primary publisher`** per le attività che non devono verificarsi su tutte le istanze, ad esempio le funzionalità che si basano su **Notifiche** o **Adobe Analytics**.

Per impostazione predefinita, la `AEM Communities Publisher Configuration` La configurazione OSGi è configurata con **`Primary Publisher`** casella di controllo selezionata, in modo che tutte le istanze di pubblicazione in una farm di pubblicazione si identifichino automaticamente come principali.

È pertanto necessario **modifica la configurazione in tutte le istanze di pubblicazione secondarie** per deselezionare **`Primary Publisher`** casella di controllo.

![](../assets/primary-publisher.png)

Per tutte le altre istanze di pubblicazione (secondarie) in una farm di pubblicazione :

* Accesso con privilegi di amministratore
* Accedere al [console web](/help/sites-deploying/configuring-osgi.md)

   * Ad esempio: [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr)

* Individua il `AEM Communities Publisher Configuration`
* Seleziona l’icona di modifica
* Deseleziona **Editore principale** casella di controllo
* Seleziona **Salva**

### Agenti di replica sull’autore {#replication-agents-on-author}

La replica viene utilizzata per il contenuto del sito creato nell’ambiente di pubblicazione, ad esempio i gruppi della community, nonché per la gestione di membri e gruppi di membri dall’ambiente di authoring tramite l’ [servizio tunnel](#tunnel-service-on-author).

Per l&#39;editore principale, assicurati che [Configurazione dell&#39;agente di replica](/help/sites-deploying/replication.md) identifica correttamente il server di pubblicazione e l&#39;utente autorizzato. Utente autorizzato predefinito, `admin` dispone già delle autorizzazioni appropriate (è membro di `Communities Administrators`).

Affinché un altro utente disponga delle autorizzazioni appropriate, deve essere aggiunto come membro al `administrators` gruppo di utenti (anche membro di `Communities Administrators`).

Nell’ambiente di authoring sono disponibili due agenti di replica che richiedono la configurazione corretta del trasporto.

* Accedere alla console Replica sull’autore

   * Dalla navigazione globale : **Strumenti, distribuzione, replica, agenti sull&#39;autore**

* Segui la stessa procedura per entrambi gli agenti :

   * **Agente predefinito (pubblicazione)**
   * **Agente di replica inversa (pubblicazione inversa)**

      1. Selezionare l&#39;agente.
      1. Seleziona **modifica**.
      1. Seleziona la **Trasporti** scheda
      1. Se non la porta `4503`, modifica il **URI** per specificare la porta corretta.

      1. Se non utente `admin`, modifica il **Utente** e **Password** per specificare un membro della `administrators` gruppo di utenti.

Le immagini seguenti mostrano i risultati della modifica della porta da 4503 a 6103 da :

#### Agente predefinito (pubblicazione) {#default-agent-publish}

![configure-limits](../assets/default-agent-publish.png)

#### Agente di replica inversa (pubblicazione inversa) {#reverse-replication-agent-publish-reverse}

![](../assets/reverse-replication-agent.png)

### Servizio tunnel su Autore {#tunnel-service-on-author}

Quando si utilizza l’ambiente di authoring in [creare siti](/help/communities/sites-console.md), [modificare le proprietà del sito](/help/communities/sites-console.md#modifying-site-properties) o [gestire membri della community](/help/communities/members.md), è necessario accedere ai membri (utenti) registrati nell’ambiente di pubblicazione, non agli utenti registrati sull’autore.

Il servizio tunnel fornisce questo accesso utilizzando l&#39;agente di replica sull&#39;autore.

Per abilitare il servizio tunnel:

* On **autore**, accedi con privilegi amministrativi.
* Se l&#39;editore non è localhost:4503 o l&#39;utente del trasporto non lo è `admin`, quindi [configurare l&#39;agente di replica](#replication-agents-on-author).

* Accedere al [Console web](/help/sites-deploying/configuring-osgi.md)

   * Ad esempio: [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)

* Individua il `AEM Communities Publish Tunnel Service`
* Seleziona l’icona di modifica
* Seleziona la **abilita** casella di controllo
* select **Salva**

![](../assets/tunnel-service.png)

### Replicare la chiave Crypto {#replicate-the-crypto-key}

Esistono due funzioni di AEM Communities che richiedono che tutte le istanze AEM server utilizzino le stesse chiavi di crittografia. Questi sono [Analytics](/help/communities/analytics.md) e [ASRP](/help/communities/asrp.md).

A partire da AEM 6.3, il materiale chiave viene memorizzato nel file system e non più nel repository.

Per copiare il materiale chiave dall’autore a tutte le altre istanze, è necessario:

* Accedi all&#39;istanza AEM, in genere un&#39;istanza dell&#39;autore, che contiene il materiale chiave da copiare

   * Individua il `com.adobe.granite.crypto.file` nel file system locale

      Ad esempio:

      * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21`
      * La `bundle.info` il file identificherà il bundle
   * Ad esempio, nella cartella dati,

      * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`
   * Copia i file hmac e i file dei nodi principali.



* Per ogni istanza AEM target

   * Ad esempio, nella cartella dati,

      * `<publish-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`
   * Incolla i 2 file precedentemente copiati
   * È necessario [aggiorna il bundle Granite Crypto](#refresh-the-granite-crypto-bundle) se l&#39;istanza di AEM di destinazione è attualmente in esecuzione.


>[!CAUTION]
>
>Se è già stata configurata un’altra funzione di sicurezza basata sulle chiavi crittografiche, la replica delle chiavi crittografiche potrebbe danneggiare la configurazione. Per assistenza, [contattare l&#39;assistenza clienti](https://helpx.adobe.com/it/marketing-cloud/contact-support.html).

#### Replica dell’archivio {#repository-replication}

È possibile conservare il materiale chiave memorizzato nell&#39;archivio, come nel caso di AEM 6.2 e versioni precedenti, specificando la seguente proprietà di sistema al primo avvio di ogni istanza AEM (che crea l&#39;archivio iniziale) :

* `-Dcom.adobe.granite.crypto.file.disable=true`

>[!NOTE]
>
>È importante verificare che la [agente di replica sull&#39;autore](#replication-agents-on-author) è configurato correttamente.

Con il materiale chiave memorizzato nell’archivio, il modo per replicare la chiave crittografica dall’autore ad altre istanze è il seguente:

Utilizzo [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md) :

* Sfoglia per [https://&lt;server>:&lt;port>/crx/de](https://localhost:4502/crx/de)
* Seleziona `/etc/key`
* Apri `Replication` scheda
* Seleziona `Replicate`

* [aggiorna il bundle Granite Crypto](#refresh-the-granite-crypto-bundle)

![](../assets/replicare-repository.png)

#### Aggiorna il bundle Crypto Granite {#refresh-the-granite-crypto-bundle}

* In ogni istanza di pubblicazione, accedi al [Console web](/help/sites-deploying/configuring-osgi.md)

   * Ad esempio: [https://&lt;server>:&lt;port>/system/console/bundle](https://localhost:4503/system/console/bundles)

* Individua `Adobe Granite Crypto Support` bundle (com.adobe.granite.crypto)
* Seleziona **Aggiorna**

![](../assets/refresh-granite-bundle.png)

* Dopo un momento, un **Completato** viene visualizzata la finestra di dialogo:
   `Operation completed successfully.`

### Server HTTP Apache {#apache-http-server}

Se utilizzi il server HTTP Apache, assicurati di utilizzare il nome server corretto per tutte le voci pertinenti.

In particolare, fare attenzione a utilizzare il nome server corretto, non `localhost`, nella `RedirectMatch`.

#### campione httpd.conf {#httpd-conf-sample}

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

Se utilizzi un’istanza di Dispatcher, consulta :

* AEM [Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html) documentazione
* [Installazione di Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-install.html)
* [Configurazione di Dispatcher per Communities](/help/communities/dispatcher.md)
* [Problemi noti](/help/communities/troubleshooting.md#dispatcher-refetch-fails)

## Documentazione di Communities correlata {#related-communities-documentation}

* Visita [Amministrazione di siti di Communities](/help/communities/administer-landing.md) per informazioni sulla creazione di un sito community, sulla configurazione di modelli di sito community, sulla moderazione dei contenuti della community, sulla gestione dei membri e sulla configurazione della messaggistica.

* Visita [Sviluppo di Communities](/help/communities/communities.md) per informazioni sul framework dei componenti sociali (SCF) e sulla personalizzazione dei componenti e delle funzionalità di Communities.

* Visita [Authoring dei componenti di Communities](/help/communities/author-communities.md) per scoprire come creare e configurare i componenti di Communities.

