---
title: Distribuzione di Communities
seo-title: Distribuzione di Communities
description: Come distribuire AEM Communities
seo-description: Come distribuire AEM Communities
uuid: 18d9b424-004d-43b2-968a-318e27a93759
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
content-type: reference
topic-tags: deploying
discoiquuid: c8d7355f-5a70-40d1-bf22-62fab8002ea0
docset: aem65
exl-id: 5b3d572d-e73d-4626-b664-c985949469c9
source-git-commit: 07f8a9f629122102d30676926b225d57e542147d
workflow-type: tm+mt
source-wordcount: '1921'
ht-degree: 2%

---

# Distribuzione di Communities {#deploying-communities}

## Prerequisiti {#prerequisites}

* [Piattaforma AEM 6.5](/help/sites-deploying/deploy.md)

* Licenza AEM Communities

* Licenze opzionali per:

   * [Funzioni di Adobe Analytics for Communities](/help/communities/analytics.md)
   * [MongoDB per MSRP](/help/communities/msrp.md)
   * [Adobe Cloud per ASRP](/help/communities/asrp.md)

## Elenco di controllo dell&#39;installazione {#installation-checklist}

**Per la piattaforma  [AEM](/help/sites-deploying/deploy.md#what-is-aem)**

* Installa gli ultimi [AEM 6.5 Aggiornamenti](#aem64updates)

* Se non utilizzi le porte predefinite (4502, 4503), [configura agenti di replica](#replication-agents-on-author)
* [Replicare la chiave crittografica](#replicate-the-crypto-key)
* Se supporta la globalizzazione, [imposta la traduzione automatica](/help/sites-administering/translation.md)
(impostazione di esempio disponibile per lo sviluppo)

**Per la funzionalit√†  [Community](/help/communities/overview.md)**

* Se distribuisci un [file farm di pubblicazione](/help/sites-deploying/recommended-deploys.md#tarmk-farm), [identifica l&#39;editore principale](#primary-publisher)

* [Attiva il servizio tunnel](#tunnel-service-on-author)
* [Abilita accesso social](/help/communities/social-login.md#adobe-granite-oauth-authentication-handler)
* [Configurare Adobe Analytics](/help/communities/analytics.md)
* Configurare un [servizio e-mail predefinito](/help/communities/email.md)
* Identifica la scelta per [memoria UGC condivisa](/help/communities/working-with-srp.md) (**SRP**)

   * Se MongoDB SRP [(MSRP)](/help/communities/msrp.md)

      * [Installare e configurare MongoDB](/help/communities/msrp.md#mongodb-configuration)
      * [Configura Solr](/help/communities/solr.md)
      * [Seleziona MSRP](/help/communities/srp-config.md)
   * Se il database relazionale SRP [(DSRP)](/help/communities/dsrp.md)

      * [Installare il driver JDBC per MySQL](#jdbc-driver-for-mysql)
      * [Installare e configurare MySQL per DSRP](/help/communities/dsrp-mysql.md)
      * [Configura Solr](/help/communities/solr.md)
      * [Seleziona DSRP](/help/communities/srp-config.md)
   * Se Adobe SRP [(ASRP)](/help/communities/asrp.md)

      * Collabora con il rappresentante del tuo account per il provisioning
      * [Seleziona ASRP](/help/communities/srp-config.md)
   * Se JCR SRP [(JSRP)](/help/communities/jsrp.md)

      * Non √® un archivio UGC condiviso :

         * UGC non viene mai replicato
         * UGC visibile solo su AEM&#39;istanza o cluster in cui √® stato inserito

         * Il valore predefinito √® JSRP
   Per la **[funzione di abilitazione](/help/communities/overview.md#enablement-community)**

   * [Installare e configurare FFmpeg](/help/communities/ffmpeg.md)
   * [Installare il driver JDBC per MySQL](#jdbc-driver-for-mysql)
   * [Installare AEM Communities SCORM-Engine](#scorm-package)
   * [Installare e configurare MySQL per l&#39;abilitazione](/help/communities/mysql.md)





## Versioni pi√Ļ recenti {#latest-releases}

AEM 6.5 Communities GA include il pacchetto Community. Per informazioni sugli aggiornamenti di AEM 6.5 [Communities](/help/release-notes/release-notes.md#experiencemanagercommunities), consulta [AEM Note sulla versione 6.5](/help/release-notes/release-notes.md#communities-release-notes.html).

### Aggiornamenti di AEM 6.5 {#aem-updates}

A partire dalla AEM 6.4, gli aggiornamenti alle Community vengono forniti come parte di AEM Cumulative Fix Pack e Service Pack.

Per gli ultimi aggiornamenti su AEM 6.5, consulta [Adobe Experience Manager 6.4 Cumulative Fix Pack e Service Pack](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/aem-releases-updates.html?lang=it).

### Cronologia versioni {#version-history}

Come in AEM 6.4 e versioni successive, le funzioni e gli hotfix di AEM Communities fanno parte dei pacchetti correzioni cumulativi e dei Service Pack di AEM Communities. Non esistono pertanto pacchetti di funzioni separati.

### Driver JDBC per MySQL {#jdbc-driver-for-mysql}

Due funzionalit√† di Communities utilizzano un database MySQL:

* Per [abilitazione](/help/communities/enablement.md): registrazione di attivit√† SCORM e studenti
* Per [DSRP](/help/communities/dsrp.md): archiviazione di contenuti generati dall‚Äôutente (UGC)

Il connettore MySQL deve essere ottenuto e installato separatamente.

Le misure necessarie sono:

1. Scarica l&#39;archivio ZIP da [https://dev.mysql.com/downloads/connector/j/](https://dev.mysql.com/downloads/connector/j/)

   * La versione deve essere >= 5.1.38

1. Estrai mysql-connector-java-&lt;version>-bin.jar (bundle) dall&#39;archivio
1. Usa la console web per installare e avviare il bundle :

   * Ad esempio, https://localhost:4502/system/console/bundles
   * Seleziona **`Install/Update`**
   * Sfoglia... per selezionare il bundle estratto dall&#39;archivio ZIP scaricato
   * Controlla che il driver JDBC di *Oracle Corporation per MySQLcom.mysql.jdbc* sia attivo e avvialo in caso contrario (o controlla i registri)

1. Se effettui l‚Äôinstallazione su un‚Äôimplementazione esistente dopo la configurazione di JDBC, fai di nuovo riferimento a JDBC nel nuovo connettore salvando nuovamente la configurazione JDBC dalla console web :
   * Ad esempio, https://localhost:4502/system/console/configMgr
   * Individua la configurazione `Day Commons JDBC Connections Pool`
   * Seleziona per aprire
   * Seleziona `Save`

1. Ripeti i passaggi 3 e 4 su tutte le istanze di authoring e pubblicazione

Ulteriori informazioni sull&#39;installazione dei bundle sono disponibili nella pagina [Console web](/help/sites-deploying/web-console.md) .

#### Esempio : Bundle del connettore MySQL installato {#example-installed-mysql-connector-bundle}

![connettore-bundle](assets/connector-bundle.png)

### Pacchetto SCORM {#scorm-package}

SCORM (Shared Content Object Reference Model) √® una raccolta di standard e specifiche per l&#39;e-learning. SCORM definisce anche come il contenuto pu√≤ essere confezionato in un file ZIP trasferibile.

Il motore AEM Communities SCORM √® necessario per la funzione [enablement](/help/communities/overview.md#enablement-community) . Pacchetti Scorm supportati su AEM 6.5 Communities:

* [cq-social-scorm-package, versione 2.3.7](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq640%2Fsocial%2Fscorm%2Fcq-social-scorm-2017-pkg) che include il motore  [SCORM 2017.1](https://rusticisoftware.com/blog/scorm-engine-2017-released/) .

**Per installare un pacchetto SCORM**

1. Installa il [cq-social-scorm-package, versione 2.3.7](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq640%2Fsocial%2Fscorm%2Fcq-social-scorm-2017-pkg) da Package Share.
1. Scarica `/libs/social/config/scorm/database_scormengine_data.sql` dall&#39;istanza cq ed eseguilo in mysql server per creare uno schema scormEngineDB aggiornato.
1. Aggiungi `/content/communities/scorm/RecordResults` nella propriet√† Percorsi esclusi nel filtro CSRF da `https://<hostname>:<port>/system/console/configMgr` agli editori.


#### Registrazione SCORM {#scorm-logging}

Come installato, tutte le attivit√† di abilitazione vengono registrate in modo dettagliato nella console di sistema.

Se lo desideri, puoi impostare il livello di log su WARN per il pacchetto `RusticiSoftware.*`.

Per utilizzare i registri, vedere [Uso dei record di controllo e dei file di registro](/help/sites-deploying/monitoring-and-maintaining.md#working-with-audit-records-and-log-files).

### MLS avanzate AEM {#aem-advanced-mls}

Per la raccolta SRP (MSRP o DSRP) per supportare la ricerca multilingue avanzata (MLS), sono necessari nuovi plug-in Solr oltre a uno schema personalizzato e una configurazione Solr. Tutti gli elementi richiesti vengono assemblati in un file zip scaricabile.

Il download avanzato di MLS (noto anche come &quot;phasetwo&quot;) √® disponibile dall‚Äôarchivio Adobe :

* Fasetwo AEM-SOLR-MLS

   Per ottenere il pacchetto MLS avanzato, vedi [AEM MLS avanzate](deploy-communities.md#aem-advanced-mls) nella sezione di distribuzione della documentazione.

   * Versione 1.2.40, 6 aprile 2016
   * Scarica AEM-SOLR-MLS-phasetwo-1.2.40.zip

Per informazioni dettagliate e sull&#39;installazione, visita [Configurazione solare](/help/communities/solr.md) per SRP.

### Informazioni sui collegamenti alla condivisione dei pacchetti {#about-links-to-package-share}

**Pacchetti visibili in Adobe AEM Cloud**

I collegamenti ai pacchetti in questa pagina non richiedono alcuna istanza in esecuzione di AEM in quanto devono condividere i pacchetti in `adobeaemcloud.com`. Mentre i pacchetti sono visualizzabili, il pulsante `Install` consente di installare i pacchetti in un sito ospitato da Adobe. Se si intende eseguire l&#39;installazione su un&#39;istanza AEM locale, la selezione di `Install` generer√† un errore.

**Come eseguire l&#39;installazione su un&#39;istanza AEM locale**

Per installare i pacchetti visibili in `adobeaemcloud.com` in un&#39;istanza AEM locale, √® necessario prima scaricare il pacchetto su un disco locale :

* Seleziona la scheda **Risorse**
* Seleziona **scarica su disco**

Nell&#39;istanza AEM locale, utilizza il gestore dei pacchetti (ad esempio [https://localhost:4502/crx/packmgr/](https://localhost:4502/crx/packmgr/)) per caricare nell&#39;archivio dei pacchetti AEM locale.

In alternativa, per accedere al pacchetto utilizzando la condivisione del pacchetto dall&#39;istanza AEM locale (ad esempio, [https://localhost:4502/crx/packageshare/](https://localhost:4502/crx/packageshare/)), il pulsante `Download` verr√† scaricato nell&#39;archivio dei pacchetti dell&#39;istanza AEM locale.

Una volta nell&#39;archivio dei pacchetti dell&#39;istanza AEM locale, utilizza il gestore dei pacchetti per installare il pacchetto.

Per ulteriori informazioni, visita [Come lavorare con i pacchetti](/help/sites-administering/package-manager.md#package-share).

## Implementazioni consigliate {#recommended-deployments}

In AEM Communities, un archivio comune viene utilizzato per memorizzare i contenuti generati dagli utenti (UGC) e viene spesso indicato come [provider di risorse di archiviazione (SRP)](/help/communities/working-with-srp.md). La distribuzione consigliata si basa sulla scelta di un‚Äôopzione SRP per lo store comune.

L&#39;archivio comune supporta la moderazione e l&#39;analisi degli UGC nell&#39;ambiente di pubblicazione, eliminando al contempo la necessit√† di [replica](/help/communities/sync.md) di UGC.

* [Archivio](/help/communities/working-with-srp.md)  contenuti community: illustra le opzioni di storage SRP per le AEM community

* [Topologie](/help/communities/topologies.md)  consigliate: discute la topologia da utilizzare in base al caso d‚Äôuso e alla scelta dell‚ÄôSRP

## Aggiornamento {#upgrading}

Durante l&#39;aggiornamento alla piattaforma AEM 6.5 dalle versioni precedenti di AEM, √® importante leggere [Aggiornamento a AEM 6.5](/help/sites-deploying/upgrade.md).

Oltre ad aggiornare la piattaforma, leggi [Aggiornamento ad AEM Communities 6.5](/help/communities/upgrade.md) per informazioni sulle modifiche apportate a Communities.

## Configurazioni {#configurations}

### Editore principale {#primary-publisher}

Quando la distribuzione scelta √® una [farm di pubblicazione](/help/communities/topologies.md#tarmk-publish-farm), un&#39;istanza di pubblicazione AEM deve essere identificata come **`primary publisher`** per le attivit√† che non devono verificarsi su tutte le istanze, ad esempio le funzionalit√† che si basano su **notifiche** o **Adobe Analytics**.

Per impostazione predefinita, la configurazione `AEM Communities Publisher Configuration` OSGi √® configurata con la casella di controllo **`Primary Publisher`** selezionata, in modo che tutte le istanze di pubblicazione in una farm di pubblicazione si identifichino automaticamente come principali.

Pertanto, √® necessario **modificare la configurazione su tutte le istanze di pubblicazione secondarie** per deselezionare la casella di controllo **`Primary Publisher`**.

![editore principale](assets/primary-publisher.png)

Per tutte le altre istanze di pubblicazione (secondarie) in una farm di pubblicazione:

* Accesso con privilegi di amministratore
* Accedi alla [console Web](/help/sites-deploying/configuring-osgi.md)

   * Ad esempio, [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr)

* Individua il `AEM Communities Publisher Configuration`
* Seleziona l‚Äôicona di modifica
* Deseleziona la casella **Editore principale**
* Seleziona **Salva**

### Agenti di replica sull‚Äôautore {#replication-agents-on-author}

La replica viene utilizzata per i contenuti del sito creati nell&#39;ambiente di pubblicazione, ad esempio i gruppi di community, nonch√© per la gestione di membri e gruppi di membri dall&#39;ambiente di authoring tramite il [servizio tunnel](#tunnel-service-on-author).

Per l&#39;editore principale, assicurati che [Replication Agent Config](/help/sites-deploying/replication.md) identifichi correttamente il server di pubblicazione e l&#39;utente autorizzato. L&#39;utente autorizzato predefinito `admin,` dispone gi√† delle autorizzazioni appropriate (√® membro di `Communities Administrators`).

Affinch√© un altro utente disponga delle autorizzazioni appropriate, deve essere aggiunto come membro al gruppo di utenti `administrators` (anche un membro di `Communities Administrators`).

Nell‚Äôambiente di authoring sono disponibili due agenti di replica che richiedono la configurazione corretta del trasporto.

* Accedere alla console Replica sull‚Äôautore

   * Dalla navigazione globale, passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Implementazione]** > **[!UICONTROL Replica]** > **[!UICONTROL Agenti sull&#39;autore]**

* Segui la stessa procedura per entrambi gli agenti :

   * **Agente predefinito (pubblicazione)**
   * **Agente di replica inversa (pubblicazione inversa)**

      1. Seleziona l&#39;agente
      1. Seleziona **modifica**
      1. Seleziona la scheda **Trasporto**
      1. Se non √® presente la porta `4503`, modificare l&#39; **URI** per specificare la porta corretta

      1. Se non l&#39;utente `admin`, modifica **Utente** e **Password** per specificare un membro del gruppo di utenti `administrators`

Le immagini seguenti mostrano i risultati della modifica della porta da 4503 a 6103:

#### Agente predefinito (pubblicazione) {#default-agent-publish}

![default-agent-publish](assets/default-agent-publish.png)

#### Agente di replica inversa (pubblicazione inversa) {#reverse-replication-agent-publish-reverse}

![agente di replica inversa](assets/reverse-replication-agent.png)

### Servizio tunnel su Autore {#tunnel-service-on-author}

Quando si utilizza l&#39;ambiente di authoring per [creare siti](/help/communities/sites-console.md), [modificare propriet√† del sito](/help/communities/sites-console.md#modifying-site-properties) o [gestire membri della community](/help/communities/members.md), √® necessario accedere ai membri (utenti) registrati nell&#39;ambiente di pubblicazione, non agli utenti registrati sull&#39;autore.

Il servizio tunnel fornisce questo accesso utilizzando l&#39;agente di replica sull&#39;autore.

Per attivare il servizio tunnel:

* Accedi con privilegi amministrativi all‚Äôistanza di authoring.
* Se l&#39;editore non √® localhost:4503 o l&#39;utente del trasporto non √® `admin`,
quindi [configura l&#39;agente di replica](#replication-agents-on-author)

* Accedi alla [Console web](/help/sites-deploying/configuring-osgi.md)

   * Ad esempio, [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)

* Individua il `AEM Communities Publish Tunnel Service`
* Seleziona l‚Äôicona di modifica
* Seleziona la casella **enable**
* Seleziona **Salva**

   ![servizio a tunnel](assets/tunnel-service.png)

### Replicare la chiave Crypto {#replicate-the-crypto-key}

Esistono due funzioni di AEM Communities che richiedono che tutte le istanze AEM server utilizzino le stesse chiavi di crittografia. Si tratta di [Analytics](/help/communities/analytics.md) e [ASRP](/help/communities/asrp.md).

A partire dal AEM 6.3, il materiale chiave viene memorizzato nel file system e non pi√Ļ nel repository.

Per copiare il materiale chiave dall‚Äôautore a tutte le altre istanze, √® necessario:

* Accedi all&#39;istanza AEM, in genere un&#39;istanza dell&#39;autore, che contiene il materiale chiave da copiare

   * Individua il bundle `com.adobe.granite.crypto.file` nel file system locale,
ad esempio,

      * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21`
      * Il file `bundle.info` identificher√† il bundle
   * Accedi alla cartella dati,
ad esempio,

      * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`

      * Copia i file hmac e i file dei nodi principali


* Per ogni istanza AEM target

   * Accedi alla cartella dati,
ad esempio,

      * `<publish-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`
   * Incolla i 2 file precedentemente copiati
   * √ą necessario [aggiornare il bundle Granite Crypto](#refresh-the-granite-crypto-bundle) se l&#39;istanza di AEM di destinazione √® attualmente in esecuzione


>[!CAUTION]
>
>Se √® gi√† stata configurata un‚Äôaltra funzione di sicurezza basata sulle chiavi crittografiche, la replica delle chiavi crittografiche potrebbe danneggiare la configurazione. Per assistenza, [contatta l&#39;assistenza clienti](https://helpx.adobe.com/it/marketing-cloud/contact-support.html).

#### Replica dell‚Äôarchivio {#repository-replication}

√ą possibile conservare il materiale chiave memorizzato nell&#39;archivio, come nel caso di AEM 6.2 e versioni precedenti, specificando la seguente propriet√† di sistema al primo avvio di ogni istanza AEM (che crea l&#39;archivio iniziale) :

* `-Dcom.adobe.granite.crypto.file.disable=true`

>[!NOTE]
>
>√ą importante verificare che l&#39; [agente di replica su author](#replication-agents-on-author) sia configurato correttamente.

Con il materiale chiave memorizzato nell‚Äôarchivio, il modo per replicare la chiave crittografica dall‚Äôautore ad altre istanze √® il seguente:

Utilizzando [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md):

* Vai a [https://&lt;server>:&lt;port>/crx/de](https://localhost:4502/crx/de)
* Seleziona `/etc/key`
* Apri la scheda `Replication`
* Seleziona `Replicate`

* [Aggiorna il bundle Granite Crypto](#refresh-the-granite-crypto-bundle)

   ![archivio replicare](assets/replicare-repository.png)

#### Aggiorna il bundle Crypto Granite {#refresh-the-granite-crypto-bundle}

* Su ogni istanza di pubblicazione, accedi alla [Console web](/help/sites-deploying/configuring-osgi.md)

   * Ad esempio, [https://&lt;server>:&lt;port>/system/console/bundles](https://localhost:4503/system/console/bundles)

* Individua il bundle `Adobe Granite Crypto Support` (com.adobe.granite.crypto)
* Seleziona **Aggiorna**

   ![cripto di granito](assets/granite-crypto.png)

* Dopo un momento, viene visualizzata una finestra di dialogo **Success** :
   `Operation completed successfully.`

### Server HTTP Apache {#apache-http-server}

Se utilizzi il server HTTP Apache, assicurati di utilizzare il nome server corretto per tutte le voci pertinenti.

In particolare, fai attenzione a utilizzare il nome server corretto, non `localhost`, nel `RedirectMatch`.

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

Se utilizzi un‚Äôistanza di Dispatcher, consulta:

* Documentazione AEM [Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html)
* [Installazione di Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-install.html)
* [Configurazione di Dispatcher per Communities](/help/communities/dispatcher.md)
* [Problemi noti](/help/communities/troubleshooting.md#dispatcher-refetch-fails)

## Documentazione di Communities correlata {#related-communities-documentation}

* Per informazioni su come creare un sito community, configurare modelli di sito community, moderare i contenuti della community, gestire i membri e configurare i messaggi, visita [Amministrazione siti community](/help/communities/administer-landing.md) .

* Visita [Sviluppo di community](/help/communities/communities.md) per informazioni sul framework dei componenti social (SCF) e sulla personalizzazione dei componenti e delle funzionalit√† di Communities.

* Per informazioni su come eseguire l‚Äôauthoring con e configurare i componenti di Communities, visita [Authoring Communities Components](/help/communities/author-communities.md) .
