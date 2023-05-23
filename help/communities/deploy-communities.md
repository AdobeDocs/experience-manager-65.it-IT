---
title: Distribuzione delle community
seo-title: Deploying Communities
description: Come distribuire AEM Communities
seo-description: How to deploy AEM Communities
uuid: 18d9b424-004d-43b2-968a-318e27a93759
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
content-type: reference
topic-tags: deploying
discoiquuid: c8d7355f-5a70-40d1-bf22-62fab8002ea0
docset: aem65
exl-id: 5b3d572d-e73d-4626-b664-c985949469c9
source-git-commit: 9f9f80eb4cb74b687c7fadd41d0f8ea4ee967865
workflow-type: tm+mt
source-wordcount: '1699'
ht-degree: 2%

---

# Distribuzione delle community {#deploying-communities}

## Prerequisiti {#prerequisites}

* [Piattaforma AEM 6.5](/help/sites-deploying/deploy.md)

* Licenza AEM Communities

* Licenze facoltative per:

   * [Funzioni di Adobe Analytics for Communities](/help/communities/analytics.md)
   * [MongoDB per MSRP](/help/communities/msrp.md)
   * [Adobe Cloud per ASRP](/help/communities/asrp.md)

## Elenco di controllo per l’installazione {#installation-checklist}

**Per [Piattaforma AEM](/help/sites-deploying/deploy.md#what-is-aem)**

* Installa più recente [Aggiornamenti AEM 6.5](#aem64updates)

* Se non si utilizzano le porte predefinite (4502, 4503), [configurare gli agenti di replica](#replication-agents-on-author)
* [Replica la chiave di crittografia](#replicate-the-crypto-key)
* Sostenendo la globalizzazione, [imposta traduzione automatica](/help/sites-administering/translation.md)
(viene fornita una configurazione di esempio per lo sviluppo)

**Per [Funzionalità community](/help/communities/overview.md)**

* Se si distribuisce un [farm di pubblicazione](/help/sites-deploying/recommended-deploys.md#tarmk-farm), [identificare l’editore principale](#primary-publisher)

* [Abilita il servizio tunnel](#tunnel-service-on-author)
* [Abilita accesso social network](/help/communities/social-login.md#adobe-granite-oauth-authentication-handler)
* [Configurare Adobe Analytics](/help/communities/analytics.md)
* Configurare un [servizio e-mail predefinito](/help/communities/email.md)
* Identificare la scelta per [archiviazione UGC condivisa](/help/communities/working-with-srp.md) (**SRP**)

   * Se MongoDB SRP [(MSRP)](/help/communities/msrp.md)

      * [Installare e configurare MongoDB](/help/communities/msrp.md#mongodb-configuration)
      * [Configura Solr](/help/communities/solr.md)
      * [Seleziona MSRP](/help/communities/srp-config.md)
   * Se SRP del database relazionale [(DSRP)](/help/communities/dsrp.md)

      * [Installare il driver JDBC per MySQL](#jdbc-driver-for-mysql)
      * [Installare e configurare MySQL per DSRP](/help/communities/dsrp-mysql.md)
      * [Configura Solr](/help/communities/solr.md)
      * [Seleziona DSRP](/help/communities/srp-config.md)
   * Se Adobe SRP [(ASRP)](/help/communities/asrp.md)

      * Rivolgiti al rappresentante del tuo account per il provisioning
      * [Seleziona ASRP](/help/communities/srp-config.md)
   * Se JCR SRP [(JSRP)](/help/communities/jsrp.md)

      * Non è un archivio UGC condiviso:

         * UGC non viene mai replicato
         * UGC visibile solo nell’istanza o nel cluster AEM in cui è stato immesso

         * Il valore predefinito è JSRP




## Ultime versioni {#latest-releases}

AEM 6.5 Communities GA include il pacchetto Communities. Per informazioni sugli aggiornamenti di AEM 6.5 [Community](/help/release-notes/release-notes.md#experiencemanagercommunities), fare riferimento [Note sulla versione di AEM 6.5](/help/release-notes/release-notes.md#communities-release-notes.html).

### Aggiornamenti AEM 6.5 {#aem-updates}

A partire da AEM 6.4, gli aggiornamenti alle community vengono forniti come parte dei Cumulative Fix Pack e Service Pack di AEM.

Per gli ultimi aggiornamenti di AEM 6.5, vedi [Adobe Experience Manager 6.4 Cumulative Fix Pack e Service Pack](https://helpx.adobe.com/it/experience-manager/aem-releases-updates.html).

### Cronologia delle versioni {#version-history}

Come per AEM 6.4 e versioni successive, le funzioni e gli hotfix di AEM Communities fanno parte di Cumulative Fix Pack e Service Pack di AEM Communities. Non esistono, quindi, feature pack separate.

### Driver JDBC per MySQL {#jdbc-driver-for-mysql}

Una funzionalità di Communities utilizza un database MySQL:

* Per [DSRP](/help/communities/dsrp.md): archiviazione di contenuti generati dagli utenti (UGC, User Generated Content)

Il connettore MySQL deve essere ottenuto e installato separatamente.

I passaggi necessari sono i seguenti:

1. Scarica l’archivio ZIP da [https://dev.mysql.com/downloads/connector/j/](https://dev.mysql.com/downloads/connector/j/)

   * La versione deve essere >= 5.1.38

1. Estrai mysql-connector-java-&lt;version>-bin.jar (bundle) dall’archivio
1. Utilizza la console web per installare e avviare il bundle:

   * Ad esempio, https://localhost:4502/system/console/bundles
   * Seleziona **`Install/Update`**
   * Sfoglia... per selezionare il bundle estratto dall’archivio ZIP scaricato
   * Controlla che *Driver JDBC di Oracle Corporation per MySQLcom.mysql.jdbc* è attivo e avvialo in caso contrario (oppure controlla i registri)

1. Se l’installazione viene eseguita su una distribuzione esistente dopo la configurazione di JDBC, riassocia JDBC al nuovo connettore salvando nuovamente la configurazione JDBC dalla console Web:
   * Ad esempio, https://localhost:4502/system/console/configMgr
   * Individua `Day Commons JDBC Connections Pool` configurazione
   * Seleziona per aprire
   * Seleziona `Save`

1. Ripeti i passaggi 3 e 4 su tutte le istanze di authoring e pubblicazione

Ulteriori informazioni sull’installazione dei bundle sono disponibili sul sito [Console web](/help/sites-deploying/web-console.md) pagina.

#### Esempio: pacchetto del connettore MySQL installato {#example-installed-mysql-connector-bundle}

![connector-bundle](assets/connector-bundle.png)



### AEM Advanced MLS {#aem-advanced-mls}

Affinché la raccolta SRP (MSRP o DSRP) supporti la ricerca multilingue avanzata, sono necessari nuovi plug-in Solr oltre a uno schema personalizzato e alla configurazione Solr. Tutti gli elementi richiesti vengono inseriti in un file zip scaricabile.

Il download MLS avanzato (noto anche come &#39;phasetwo&#39;) è disponibile dall&#39;archivio Adobe:

* AEM-SOLR-MLS-phasetwo

   Per ottenere il pacchetto MLS avanzato, vedi [AEM Advanced MLS](deploy-communities.md#aem-advanced-mls) nella sezione distribuzione della documentazione.

   * Versione 1.2.40, 6 aprile 2016
   * Scarica AEM-SOLR-MLS-phasetwo-1.2.40.zip

Per maggiori informazioni sull&#39;installazione, visitare il sito Web [Configurazione Solr](/help/communities/solr.md) per SRP.

### Informazioni sui collegamenti a Package Share {#about-links-to-package-share}

**Pacchetti visibili in Adobe AEM Cloud**

I collegamenti ai pacchetti in questa pagina non richiedono alcuna istanza in esecuzione di AEM in quanto sono per la condivisione dei pacchetti in `adobeaemcloud.com`. Mentre i pacchetti sono visualizzabili, il `Install` per installare i pacchetti in un sito ospitato di Adobe. Se si intende eseguire l&#39;installazione in un&#39;istanza AEM locale, selezionare `Install` genererà un errore.

**Come eseguire l’installazione su un’istanza AEM locale**

Per installare i pacchetti visibili in `adobeaemcloud.com` in un&#39;istanza AEM locale, il pacchetto deve prima essere scaricato su un disco locale:

* Seleziona la **Risorse** scheda
* Seleziona **scarica su disco**

Nell’istanza AEM locale, utilizza Gestione pacchetti (ad esempio [https://localhost:4502/crx/packmgr/](https://localhost:4502/crx/packmgr/)), per caricare nell’archivio dei pacchetti AEM locale.

In alternativa, è possibile accedere al pacchetto utilizzando la condivisione pacchetti dall’istanza AEM locale (ad esempio, [https://localhost:4502/crx/packageshare/](https://localhost:4502/crx/packageshare/)), il `Download` scarica nell’archivio dei pacchetti dell’istanza AEM locale.

Una volta inserito nell’archivio dei pacchetti dell’istanza AEM locale, utilizza Gestione pacchetti per installare il pacchetto.

Per ulteriori informazioni, visita [Come utilizzare i pacchetti](/help/sites-administering/package-manager.md#package-share).

## Distribuzioni consigliate {#recommended-deployments}

In AEM Communities, un archivio comune viene utilizzato per memorizzare i contenuti generati dagli utenti (UGC, User Generated Content) ed è spesso indicato come [provider di risorse di archiviazione (SRP)](/help/communities/working-with-srp.md). La distribuzione consigliata è incentrata sulla scelta di un’opzione SRP per l’archivio comune.

Common Store supporta la moderazione e l’analisi di UGC nell’ambiente di pubblicazione, eliminando al contempo la necessità di [replica](/help/communities/sync.md) di UGC.

* [Archivio contenuti community](/help/communities/working-with-srp.md) : illustra le opzioni di archiviazione SRP per le comunità AEM

* [Topologie consigliate](/help/communities/topologies.md) : descrive la topologia da utilizzare a seconda del caso d’uso e della scelta SRP

## Aggiornamento {#upgrading}

Quando si esegue l’aggiornamento alla piattaforma AEM 6.5 da versioni precedenti dell’AEM, è importante leggere [Aggiornamento a AEM 6.5](/help/sites-deploying/upgrade.md).

Oltre all’aggiornamento della piattaforma, leggi [Aggiornamento ad AEM Communities 6.5](/help/communities/upgrade.md) per informazioni sulle modifiche apportate alle community.

## Configurazioni {#configurations}

### Editore primario {#primary-publisher}

Quando la distribuzione scelta è un [farm di pubblicazione](/help/communities/topologies.md#tarmk-publish-farm), quindi un’istanza di pubblicazione dell’AEM deve essere identificata come **`primary publisher`** per attività che non devono verificarsi su tutte le istanze, come le funzioni che si basano su **notifiche** o **Adobe Analytics**.

Per impostazione predefinita, il `AEM Communities Publisher Configuration` Configurazione OSGi configurata con **`Primary Publisher`** , in modo tale che tutte le istanze di pubblicazione in una farm di pubblicazione si identifichino autonomamente come primarie.

È pertanto necessario: **modifica la configurazione su tutte le istanze di pubblicazione secondarie** per deselezionare **`Primary Publisher`** casella di controllo.

![primary-publisher](assets/primary-publisher.png)

Per tutte le altre istanze di pubblicazione (secondarie) in una farm di pubblicazione:

* Accesso con privilegi di amministratore
* Accedere a [console web](/help/sites-deploying/configuring-osgi.md)

   * Ad esempio: [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr)

* Individua il `AEM Communities Publisher Configuration`
* Seleziona l’icona Modifica
* Deseleziona la **Editore primario** casella
* Seleziona **Salva**

### Agenti di replica per l’autore {#replication-agents-on-author}

La replica viene utilizzata per i contenuti del sito creati nell&#39;ambiente di pubblicazione, ad esempio i gruppi della community, nonché per la gestione di membri e gruppi di membri dall&#39;ambiente di authoring utilizzando [servizio tunnel](#tunnel-service-on-author).

Per l’editore principale, assicurati che [Configurazione agente di replica](/help/sites-deploying/replication.md) identifica correttamente il server di pubblicazione e l’utente autorizzato. Utente autorizzato predefinito, `admin,` dispone già delle autorizzazioni appropriate (è membro di `Communities Administrators`).

Affinché altri utenti possano disporre delle autorizzazioni appropriate, è necessario aggiungerli come membri al `administrators` gruppo di utenti (anche membro di `Communities Administrators`).

Nell’ambiente di authoring sono presenti due agenti di replica che richiedono la corretta configurazione del trasporto.

* Accedere alla console Replica durante l’authoring

   * Dalla navigazione globale, accedi a **[!UICONTROL Strumenti]** > **[!UICONTROL Distribuzione]** > **[!UICONTROL Replica]** > **[!UICONTROL Agenti per creazione]**

* Seguire la stessa procedura per entrambi gli agenti:

   * **Agente predefinito (pubblicazione)**
   * **Agente replica inversa (pubblicazione inversa)**

      1. Seleziona l’agente
      1. Seleziona **modifica**
      1. Seleziona la **Trasporto** scheda
      1. Se non porta `4503`, modifica il **URI** per specificare la porta corretta

      1. Se non utente `admin`, modifica il **Utente** e **Password** per specificare un membro del `administrators` gruppo utenti

Le immagini seguenti mostrano i risultati della modifica della porta da 4503 a 6103 da parte di:

#### Agente predefinito (pubblicazione) {#default-agent-publish}

![default-agent-publish](assets/default-agent-publish.png)

#### Agente replica inversa (pubblicazione inversa) {#reverse-replication-agent-publish-reverse}

![reverse-replication-agent](assets/reverse-replication-agent.png)

### Servizio tunnel nell&#39;ambiente Author {#tunnel-service-on-author}

Quando si utilizza l’ambiente di authoring per [creare siti](/help/communities/sites-console.md), [modifica proprietà sito](/help/communities/sites-console.md#modifying-site-properties) o [gestisci membri community](/help/communities/members.md), è necessario accedere ai membri (utenti) registrati nell’ambiente di pubblicazione e non agli utenti registrati nell’ambiente di authoring.

Il servizio tunnel fornisce questo accesso utilizzando l’agente di replica sull’istanza di authoring.

Per attivare il servizio tunnel:

* Accedi con privilegi di amministratore all’istanza di authoring.
* Se l&#39;autore non è localhost:4503 o l&#39;utente di trasporto non è `admin`, quindi [configurare l’agente di replica](#replication-agents-on-author)

* Accedere a [Console web](/help/sites-deploying/configuring-osgi.md)

   * Ad esempio: [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)

* Individua il `AEM Communities Publish Tunnel Service`
* Seleziona l’icona Modifica
* Controlla la **abilita** casella
* Seleziona **Salva**

   ![servizio tunnel](assets/tunnel-service.png)

### Replica la chiave di crittografia {#replicate-the-crypto-key}

Esistono due funzioni di AEM Communities che richiedono che tutte le istanze del server AEM utilizzino le stesse chiavi di crittografia. Questi sono [Analytics](/help/communities/analytics.md) e [ASRP](/help/communities/asrp.md).

A partire dalla versione 6.3 dell’AEM, il materiale principale viene memorizzato nel file system e non più nell’archivio.

Per copiare il materiale chiave dall’autore a tutte le altre istanze, è necessario:

* Accedi all’istanza AEM, in genere un’istanza Autore, che contiene il materiale chiave da copiare

   * Individua il `com.adobe.granite.crypto.file` nel file system locale, ad esempio,

      * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21`
      * Il `bundle.info` il file identificherà il bundle
   * Accedi alla cartella dati, ad esempio

      * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`

      * Copiare i file hmac e del nodo principale


* Per ogni istanza AEM target

   * Accedi alla cartella dati, ad esempio

      * `<publish-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`
   * Incolla i 2 file copiati in precedenza
   * È necessario [aggiorna il bundle Granite Crypto](#refresh-the-granite-crypto-bundle) se l’istanza AEM di destinazione è attualmente in esecuzione


>[!CAUTION]
>
>Se è già stata configurata un&#39;altra funzionalità di protezione basata sulle chiavi di crittografia, la replica delle chiavi di crittografia potrebbe danneggiare la configurazione. Per assistenza, [contatta l’assistenza clienti](https://helpx.adobe.com/it/marketing-cloud/contact-support.html).

#### Replica archivio {#repository-replication}

È possibile conservare il materiale chiave memorizzato nel repository, come nel caso di AEM 6.2 e versioni precedenti, specificando la seguente proprietà di sistema al primo avvio di ogni istanza AEM (che crea l’archivio iniziale):

* `-Dcom.adobe.granite.crypto.file.disable=true`

>[!NOTE]
>
>È importante verificare che [agente di replica sull’autore](#replication-agents-on-author) è configurato correttamente.

Con il materiale della chiave memorizzato nell’archivio, il modo per replicare la chiave crittografica dall’istanza di authoring ad altre istanze è il seguente:

Utilizzo di [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md):

* Sfoglia per [https://&lt;server>:&lt;port>/crx/de](https://localhost:4502/crx/de)
* Seleziona `/etc/key`
* Apri `Replication` scheda
* Seleziona `Replicate`

* [Aggiorna il bundle Granite Crypto](#refresh-the-granite-crypto-bundle)

   ![replicare-archivio](assets/replicare-repository.png)

#### Aggiorna il pacchetto di crittografia Granite {#refresh-the-granite-crypto-bundle}

* In ogni istanza di pubblicazione, accedi a [Console web](/help/sites-deploying/configuring-osgi.md)

   * Ad esempio: [https://&lt;server>:&lt;port>/system/console/bundle](https://localhost:4503/system/console/bundles)

* Individua `Adobe Granite Crypto Support` bundle (com.adobe.granite.crypto)
* Seleziona **Aggiorna**

   ![granite-crypto](assets/granite-crypto.png)

* Dopo un momento, **Completato** viene visualizzata la finestra di dialogo:
   `Operation completed successfully.`

### Server HTTP Apache {#apache-http-server}

Se utilizzi il server HTTP Apache, assicurati di utilizzare il nome del server corretto per tutte le voci rilevanti.

In particolare, fai attenzione a usare il nome del server corretto, non `localhost`, nella `RedirectMatch`.

#### esempio httpd.conf {#httpd-conf-sample}

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

Se utilizzi un Dispatcher, consulta:

* AEM [Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html) documentazione
* [Installazione di Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-install.html)
* [Configurazione di Dispatcher per le community](/help/communities/dispatcher.md)
* [Problemi noti](/help/communities/troubleshooting.md#dispatcher-refetch-fails)

## Documentazione delle community correlate {#related-communities-documentation}

* Visita [Amministrazione di siti community](/help/communities/administer-landing.md) informazioni sulla creazione di un sito community, sulla configurazione di modelli di sito community, sulla moderazione del contenuto della community, sulla gestione dei membri e sulla configurazione dei messaggi.

* Visita [Comunità in via di sviluppo](/help/communities/communities.md) per scoprire il framework dei componenti social (SCF) e personalizzare i componenti e le funzioni di Communities.

* Visita [Authoring dei componenti delle community](/help/communities/author-communities.md) per scoprire come effettuare l’authoring con e configurare i componenti di Communities.
