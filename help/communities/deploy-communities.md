---
title: Distribuzione delle community
description: Scopri come distribuire community e funzioni della community in Adobe Experience Manager.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
content-type: reference
topic-tags: deploying
docset: aem65
exl-id: 5b3d572d-e73d-4626-b664-c985949469c9
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1658'
ht-degree: 0%

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

**Per la [piattaforma AEM](/help/sites-deploying/deploy.md#what-is-aem)**

* Installa gli ultimi [aggiornamenti AEM 6.5](#aem64updates)

* Se non si utilizzano le porte predefinite (4502, 4503), [configurare gli agenti di replica](#replication-agents-on-author)
* [Replica la chiave di crittografia](#replicate-the-crypto-key)
* Se supporta la globalizzazione, [imposta traduzione automatica](/help/sites-administering/translation.md)
(viene fornita una configurazione di esempio per lo sviluppo)

**Per la funzionalità [Communities](/help/communities/overview.md)**

* Se si distribuisce una [farm di pubblicazione](/help/sites-deploying/recommended-deploys.md#tarmk-farm), [identificare l&#39;editore primario](#primary-publisher)

* [Abilita il servizio tunnel](#tunnel-service-on-author)
* [Abilita accesso social network](/help/communities/social-login.md#adobe-granite-oauth-authentication-handler)
* [Configurare Adobe Analytics](/help/communities/analytics.md)
* Configura un [servizio e-mail predefinito](/help/communities/email.md)
* Identifica la scelta per [archiviazione UGC condivisa](/help/communities/working-with-srp.md) (**SRP**)

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

      * Rivolgiti al rappresentante del tuo account per il provisioning
      * [Seleziona ASRP](/help/communities/srp-config.md)

   * Se JCR SRP [(JSRP)](/help/communities/jsrp.md)

      * Non è un archivio condiviso UGC (User-Generated Content):

         * UGC non viene mai replicato
         * UGC è visibile solo nell’istanza o nel cluster AEM in cui è stato immesso

         * Il valore predefinito è JSRP

## Ultime versioni {#latest-releases}

AEM 6.5 Communities GA include il pacchetto Communities. Per ulteriori informazioni sugli aggiornamenti di AEM 6.5 [Communities](/help/release-notes/release-notes.md#experiencemanagercommunities), consulta le [Note sulla versione di AEM 6.5](/help/release-notes/release-notes.md#communities-release-notes.html).

### Aggiornamenti AEM 6.5 {#aem-updates}

A partire da AEM 6.4, gli aggiornamenti alle community vengono forniti come parte dei Cumulative Fix Pack e Service Pack di AEM.

Per gli ultimi aggiornamenti di AEM 6.5, vedere [Adobe Experience Manager 6.4 Cumulative Fix Pack e Service Pack](https://experienceleague.adobe.com/it/docs/experience-manager-release-information/aem-release-updates/aem-releases-updates).

### Cronologia delle versioni {#version-history}

Come per AEM 6.4 e versioni successive, le funzioni e gli hotfix di AEM Communities fanno parte di Cumulative Fix Pack e Service Pack di AEM Communities. Non esistono, quindi, feature pack separate.

### Driver JDBC per MySQL {#jdbc-driver-for-mysql}

Una funzionalità di Communities utilizza un database MySQL:

* Per [DSRP](/help/communities/dsrp.md): archiviazione UGC

Il connettore MySQL deve essere ottenuto e installato separatamente.

I passaggi necessari sono i seguenti:

1. Scarica l&#39;archivio ZIP da [https://dev.mysql.com/downloads/connector/j/](https://dev.mysql.com/downloads/connector/j/)

   * La versione deve essere >= 5.1.38

1. Estrai mysql-connector-java-&lt;versione>-bin.jar (bundle) dall’archivio
1. Utilizza la console web per installare e avviare il bundle:

   * Ad esempio, https://localhost:4502/system/console/bundles
   * Seleziona **`Install/Update`**
   * Sfoglia... per selezionare il bundle estratto dall’archivio ZIP scaricato
   * Verificare che il driver JDBC di *Oracle Corporation per MySQLcom.mysql.jdbc* sia attivo e avviarlo in caso contrario (oppure controllare i registri)

1. Se l’installazione viene eseguita su una distribuzione esistente dopo la configurazione di JDBC, riassocia JDBC al nuovo connettore salvando nuovamente la configurazione JDBC dalla console Web:
   * Ad esempio, https://localhost:4502/system/console/configMgr
   * Individua configurazione `Day Commons JDBC Connections Pool`
   * Seleziona per aprire
   * Seleziona `Save`

1. Ripeti i passaggi 3 e 4 su tutte le istanze di authoring e pubblicazione

Ulteriori informazioni sull&#39;installazione dei bundle sono disponibili nella pagina [Console Web](/help/sites-deploying/web-console.md).

#### Esempio: pacchetto del connettore MySQL installato {#example-installed-mysql-connector-bundle}

![bundle connettore](assets/connector-bundle.png)



### AEM Advanced MLS {#aem-advanced-mls}

Affinché la raccolta SRP (MSRP o DSRP) supporti la ricerca multilingue avanzata, sono necessari nuovi plug-in Solr oltre a uno schema personalizzato e alla configurazione Solr. Tutti gli elementi richiesti vengono inseriti in un file zip scaricabile.

Il download MLS avanzato (noto anche come `phasetwo`) è disponibile dall&#39;archivio Adobe:

* AEM-SOLR-MLS-phasetwo

  Per ottenere il pacchetto MLS avanzato, vedere [MLS avanzato AEM](deploy-communities.md#aem-advanced-mls) nella sezione relativa alla distribuzione della documentazione.

   * Versione 1.2.40, 6 aprile 2016
   * Scarica AEM-SOLR-MLS-phasetwo-1.2.40.zip

Per informazioni dettagliate e sull&#39;installazione, visitare [Configurazione Solr](/help/communities/solr.md) per SRP.

### Informazioni sui collegamenti a Package Share {#about-links-to-package-share}

**Pacchetti visibili in Adobe AEM Cloud**

I collegamenti ai pacchetti in questa pagina non richiedono alcuna istanza in esecuzione di AEM in quanto sono collegati a Condivisione pacchetti in `adobeaemcloud.com`. Mentre i pacchetti sono visualizzabili, il pulsante `Install` consente di installare i pacchetti in un sito ospitato di Adobe. Se si desidera eseguire l&#39;installazione in un&#39;istanza AEM locale, la selezione di `Install` genera un errore.

**Installazione nell&#39;istanza AEM locale**

Per installare i pacchetti visibili in `adobeaemcloud.com` in un&#39;istanza AEM locale, è necessario prima scaricare il pacchetto in un disco locale:

* Seleziona la scheda **Assets**
* Seleziona **scarica su disco**

Nell&#39;istanza AEM locale, utilizzare Gestione pacchetti (ad esempio, [https://localhost:4502/crx/packmgr/](https://localhost:4502/crx/packmgr/)) per caricare nell&#39;archivio dei pacchetti dell&#39;AEM locale.

In alternativa, se si accede al pacchetto utilizzando Condivisione pacchetti dall&#39;istanza AEM locale (ad esempio, [https://localhost:4502/crx/packageshare/](https://localhost:4502/crx/packageshare/)), il pulsante `Download` viene scaricato nel repository del pacchetto dell&#39;istanza AEM locale.

Una volta inserito nell’archivio dei pacchetti dell’istanza AEM locale, utilizza Gestione pacchetti per installare il pacchetto.

Per ulteriori informazioni, visitare [Come utilizzare i pacchetti](/help/sites-administering/package-manager.md#package-share).

## Distribuzioni consigliate {#recommended-deployments}

In AEM Communities viene utilizzato un archivio comune per memorizzare UGC, spesso indicato come [provider di risorse di archiviazione (SRP)](/help/communities/working-with-srp.md). La distribuzione consigliata è incentrata sulla scelta di un’opzione SRP per l’archivio comune.

L&#39;archivio comune supporta la moderazione e l&#39;analisi di UGC nell&#39;ambiente di pubblicazione, eliminando la necessità di [replica](/help/communities/sync.md) di UGC.

* [Archivio contenuti community](/help/communities/working-with-srp.md): illustra le opzioni di archiviazione SRP per AEM Communities

* [Topologie consigliate](/help/communities/topologies.md): illustra la topologia da utilizzare a seconda del caso d&#39;uso e della scelta SRP

## Aggiornamento {#upgrading}

Durante l&#39;aggiornamento alla piattaforma AEM 6.5 da versioni precedenti dell&#39;AEM, è importante leggere [Aggiornamento a AEM 6.5](/help/sites-deploying/upgrade.md).

Oltre all&#39;aggiornamento della piattaforma, leggere [Aggiornamento ad AEM Communities 6.5](/help/communities/upgrade.md) per informazioni sulle modifiche delle community.

## Configurazioni {#configurations}

### Editore primario {#primary-publisher}

Quando la distribuzione scelta è una [farm di pubblicazione](/help/communities/topologies.md#tarmk-publish-farm), è necessario identificare un&#39;istanza di pubblicazione AEM come **`primary publisher`** per le attività che non devono verificarsi in tutte le istanze. Ad esempio, funzionalità basate su **notifiche** o **Adobe Analytics**.

Per impostazione predefinita, la configurazione OSGi `AEM Communities Publisher Configuration` è configurata con la casella di controllo **`Primary Publisher`** selezionata, in modo che tutte le istanze di pubblicazione in una farm di pubblicazione si identifichino autonomamente come primarie.

Pertanto, è necessario **modificare la configurazione in tutte le istanze di pubblicazione secondarie** per deselezionare la casella di controllo **`Primary Publisher`**.

![editore-primario](assets/primary-publisher.png)

Per tutte le altre istanze di pubblicazione (secondarie) in una farm di pubblicazione:

* Accesso con privilegi di amministratore
* Accedi alla [console Web](/help/sites-deploying/configuring-osgi.md)

   * Ad esempio, [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr)

* Individua `AEM Communities Publisher Configuration`
* Seleziona l’icona Modifica
* Deseleziona la casella **Autore primario**
* Seleziona **Salva**

### Agenti di replica per l’autore {#replication-agents-on-author}

La replica viene utilizzata per il contenuto del sito creato nell&#39;ambiente di pubblicazione, ad esempio i gruppi della community, e per la gestione di membri e gruppi di membri dall&#39;ambiente di authoring mediante il servizio [tunnel](#tunnel-service-on-author).

Per l&#39;editore principale, verificare che la [configurazione agente di replica](/help/sites-deploying/replication.md) identifichi correttamente il server di pubblicazione e l&#39;utente autorizzato. L&#39;utente autorizzato predefinito `admin,` dispone già delle autorizzazioni appropriate (è membro di `Communities Administrators`).

Affinché un altro utente disponga delle autorizzazioni appropriate, è necessario aggiungerlo come membro al gruppo di utenti `administrators` (anche membro di `Communities Administrators`).

Nell’ambiente di authoring sono presenti due agenti di replica che richiedono la corretta configurazione del trasporto.

* Accedere alla console Replica durante l’authoring

   * Dalla navigazione globale, passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Distribuzione]** > **[!UICONTROL Replica]** > **[!UICONTROL Agenti per l&#39;autore]**

* Seguire la stessa procedura per entrambi gli agenti:

   * **Agente predefinito (pubblicazione)**
   * **Agente replica inversa (pubblicazione inversa)**

      1. Seleziona l’agente
      1. Seleziona **modifica**
      1. Seleziona la scheda **Trasporto**
      1. Se non è la porta `4503`, modificare **URI** per specificare la porta corretta

      1. Se non si tratta dell&#39;utente `admin`, modificare **Utente** e **Password** per specificare un membro del gruppo di utenti `administrators`

Le immagini seguenti mostrano i risultati della modifica della porta da 4503 a 6103 da parte di:

#### Agente predefinito (pubblicazione) {#default-agent-publish}

![default-agent-publish](assets/default-agent-publish.png)

#### Agente replica inversa (pubblicazione inversa) {#reverse-replication-agent-publish-reverse}

![agente di replica inversa](assets/reverse-replication-agent.png)

### Servizio tunnel nell&#39;ambiente Author {#tunnel-service-on-author}

Quando si utilizza l&#39;ambiente di authoring per [creare siti](/help/communities/sites-console.md), [modificare le proprietà del sito](/help/communities/sites-console.md#modifying-site-properties) o [gestire i membri della community](/help/communities/members.md), è necessario accedere ai membri (utenti) registrati nell&#39;ambiente di pubblicazione e non agli utenti registrati nell&#39;ambiente di authoring.

Il servizio tunnel fornisce questo accesso utilizzando l’agente di replica sull’istanza di authoring.

Per attivare il servizio tunnel:

* Accedi con privilegi di amministratore all’istanza di authoring.
* Se l&#39;editore non è localhost:4503 o l&#39;utente di trasporto non è `admin`,
quindi [configurare l&#39;agente di replica](#replication-agents-on-author)

* Accedi alla [console Web](/help/sites-deploying/configuring-osgi.md)

   * Ad esempio, [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)

* Individua `AEM Communities Publish Tunnel Service`
* Seleziona l’icona Modifica
* Seleziona la casella **abilita**
* Seleziona **Salva**

  ![servizio-tunnel](assets/tunnel-service.png)

### Replica la chiave di crittografia {#replicate-the-crypto-key}

Esistono due funzioni di AEM Communities che richiedono che tutte le istanze del server AEM utilizzino le stesse chiavi di crittografia. Sono [Analytics](/help/communities/analytics.md) e [ASRP](/help/communities/asrp.md).

A partire dalla versione 6.3 dell’AEM, il materiale principale viene memorizzato nel file system e non più nell’archivio.

Per copiare il materiale chiave dall&#39;autore a tutte le altre istanze, è necessario:

* Accedere all’istanza AEM, in genere un’istanza Autore, contenente il materiale chiave da copiare

   * Individuare il bundle `com.adobe.granite.crypto.file` nel file system locale
ad esempio:

      * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21`
      * Il file `bundle.info` identifica il bundle

   * Accedi alla cartella dati,
ad esempio:

      * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`

      * Copiare i file hmac e del nodo principale

* Per ogni istanza AEM target

   * Accedi alla cartella dati,
ad esempio:

      * `<publish-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`

   * Incolla i due file copiati in precedenza
   * È necessario [aggiornare il bundle Granite Crypto](#refresh-the-granite-crypto-bundle) se l&#39;istanza AEM di destinazione è in esecuzione

>[!CAUTION]
>
>Se è già stata configurata un&#39;altra funzionalità di protezione basata sulle chiavi di crittografia, la replica delle chiavi di crittografia potrebbe danneggiare la configurazione. Per assistenza, [contatta l&#39;assistenza clienti](https://experienceleague.adobe.com/?support-solution=General&amp;support-tab=homehome?lang=it#support).

#### Replica archivio {#repository-replication}

Come nel caso dell’AEM 6.2 e versioni precedenti, è possibile conservare il materiale principale conservato nel deposito. Specificare la proprietà di sistema `-Dcom.adobe.granite.crypto.file.disable=true` al primo avvio di ogni istanza AEM (che crea l&#39;archivio iniziale).

>[!NOTE]
>
>Verificare che l&#39;agente di replica [in Author](#replication-agents-on-author) sia configurato correttamente.

Con il materiale della chiave memorizzato nell’archivio, il modo per replicare la chiave crittografica dall’istanza di authoring ad altre istanze è il seguente:

Utilizzo di [CRXDE Liti](/help/sites-developing/developing-with-crxde-lite.md):

* Passa a [https://&lt;server>:&lt;porta>/crx/de](https://localhost:4502/crx/de)
* Seleziona `/etc/key`
* Apri scheda `Replication`
* Seleziona `Replicate`

* [Aggiorna il bundle Granite Crypto](#refresh-the-granite-crypto-bundle)

  ![archivio replicare](assets/replicare-repository.png)

#### Aggiorna il pacchetto di crittografia Granite {#refresh-the-granite-crypto-bundle}

* In ogni istanza di pubblicazione, accedere alla [console Web](/help/sites-deploying/configuring-osgi.md)

   * Ad esempio, [https://&lt;server>:&lt;porta>/system/console/bundles](https://localhost:4503/system/console/bundles)

* Individua bundle `Adobe Granite Crypto Support` (com.adobe.granite.crypto)
* Seleziona **Aggiorna**

  ![granite-crypto](assets/granite-crypto.png)

* Dopo qualche istante verrà visualizzata una finestra di dialogo **Operazione riuscita**:
  `Operation completed successfully.`

### Server HTTP Apache {#apache-http-server}

Se utilizzi il server HTTP Apache, assicurati di utilizzare il nome del server corretto per tutte le voci rilevanti.

In particolare, prestare attenzione a utilizzare il nome server corretto, non `localhost`, in `RedirectMatch`.

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

* Documentazione di [Dispatcher](https://experienceleague.adobe.com/it/docs/experience-manager-release-information/aem-release-updates/aem-releases-updates) per AEM
* [Installazione di Dispatcher](https://experienceleague.adobe.com/en/docs/experience-manager-dispatcher/using/getting-started/dispatcher-install)
* [Configurazione di Dispatcher per Communities](/help/communities/dispatcher.md)
* [Problemi noti](/help/communities/troubleshooting.md#dispatcher-refetch-fails)

## Documentazione delle community correlate {#related-communities-documentation}

* Visita [Amministrazione di siti community](/help/communities/administer-landing.md) per scoprire come creare un sito community, configurare modelli di sito community, moderare il contenuto della community, gestire i membri e configurare i messaggi.

* Visita [Sviluppo di community](/help/communities/communities.md) per scoprire il framework dei componenti social network (SCF) e personalizzare i componenti e le funzionalità di Communities.

* Visita [Authoring dei componenti delle community](/help/communities/author-communities.md) per scoprire come creare e configurare i componenti delle community.
