---
title: Configurare Dynamic Medie - Modalità Scene7
description: Scopri come configurare Dynamic Medie in modalità Scene7.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
docset: aem65
role: User, Admin
mini-toc-levels: 4
exl-id: badd0f5c-2eb7-430d-ad77-fa79c4ff025a
feature: Configuration,Scene7 Mode
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '6508'
ht-degree: 3%

---

# Configurare Dynamic Medie - Modalità Scene7{#configuring-dynamic-media-scene-mode}

Se si utilizza la configurazione Adobe Experience Manager per ambienti diversi, ad esempio sviluppo, staging e produzione, configurare i Cloud Service Dynamic Medie per ciascuno di tali ambienti.

## Diagramma dell’architettura di Dynamic Medie - Modalità Scene7 {#architecture-diagram-of-dynamic-media-scene-mode}

Il seguente diagramma dell’architettura descrive il funzionamento della modalità Dynamic Medie - Scene7.

Con la nuova architettura, Experience Manager è responsabile delle risorse di origine primaria e si sincronizza con Dynamic Medie per l’elaborazione e la pubblicazione delle risorse:

1. Quando la risorsa di origine principale viene caricata in Experience Manager, viene replicata in Dynamic Medie. A questo punto, Dynamic Medie gestisce tutte le attività di elaborazione delle risorse e generazione del rendering, come la codifica video e le varianti dinamiche di un’immagine.
In modalità Dynamic Medie - Scene7, la dimensione predefinita del file caricato è pari o inferiore a 2 GB. Per abilitare il caricamento di file di dimensioni comprese tra 2 GB e 15 GB, vedere [(Facoltativo) Configurare la modalità Dynamic Medie - Scene7 per il caricamento di risorse superiori a 2 GB](#optional-config-dms7-assets-larger-than-2gb).)
1. Dopo la generazione delle rappresentazioni, Experience Manager può accedere in modo sicuro e visualizzare in anteprima le rappresentazioni Dynamic Medie remote (nessun binario viene inviato nuovamente all’istanza Experience Manager).
1. Quando il contenuto è pronto per essere pubblicato e approvato, attiva il servizio Dynamic Medie per inviare contenuti ai server di distribuzione e memorizzarli nella cache della rete CDN (Content Delivery Network).

![chlimage_1-550](assets/chlimage_1-550.png)

>[!IMPORTANT]
>
>Per visualizzare il seguente elenco di funzioni è necessario utilizzare la rete CDN preconfigurata fornita in bundle con Adobe Experience Manager - Dynamic Medie. Qualsiasi altra rete CDN personalizzata non è supportata con queste funzioni.
>
>* [Imaging avanzato](/help/assets/imaging-faq.md)
>* [Annullamento validità cache](/help/assets/invalidate-cdn-cache-dynamic-media.md)
>* [Protezione hotlink](/help/assets/hotlink-protection.md)
>* [Distribuzione HTTP/2 dei contenuti](/help/assets/http2.md)
>* Reindirizzamento URL a livello di CDN
>* Akamai ChinaCDN (per una consegna ottimale in Cina)

## Abilita Dynamic Medie in modalità Scene7 {#enabling-dynamic-media-in-scene-mode}

[Dynamic Medie](https://business.adobe.com/products/experience-manager/assets/dynamic-media.html) è disabilitato per impostazione predefinita. Per sfruttare le funzioni di Dynamic Medie, devi attivarle.

>[!WARNING]
>
>Dynamic Medie - La modalità Scene7 è solo per l&#39;istanza Autore *Experience Manager*. Di conseguenza, devi configurare `runmode=dynamicmedia_scene7` nell&#39;istanza Autore Experience Manager, *non* nell&#39;istanza Publish Experience Manager.

Per abilitare Dynamic Medie, avviare Experience Manager utilizzando la modalità di esecuzione `dynamicmedia_scene7` dalla riga di comando immettendo quanto segue in una finestra del terminale (la porta di esempio utilizzata è 4502):

```shell {.line-numbers}
java -Xms4096m -Xmx4096m -Doak.queryLimitInMemory=500000 -Doak.queryLimitReads=500000 -jar cq-quickstart-6.5.0.jar -gui -r author,dynamicmedia_scene7 -p 4502
```

## (Facoltativo) Migrazione di predefiniti e configurazioni Dynamic Medie da 6.3 a 6.5 Senza downtime {#optional-migrating-dynamic-media-presets-and-configurations-from-to-zero-downtime}

L’aggiornamento di Experience Manager Dynamic Medie dalla versione 6.3 alla versione 6.4 o 6.5 ora include la possibilità di eseguire distribuzioni senza tempi di inattività. Per eseguire la migrazione di tutti i predefiniti e le configurazioni da `/etc` a `/conf` in CRXDE Lite, assicurati di eseguire il seguente comando curl.

>[!NOTE]
>
>Se si esegue l&#39;istanza Experience Manager in modalità di compatibilità, ovvero se è installato il pacchetto di compatibilità, non è necessario eseguire questi comandi.

Per tutti gli aggiornamenti, con o senza il pacchetto di compatibilità, puoi copiare i predefiniti predefiniti visualizzatore forniti originariamente con Dynamic Medie eseguendo il seguente comando curl Linux®:

`curl -u admin:admin -X POST https://<server_address>:<server_port>/libs/settings/dam/dm/presets/viewer.pushviewerpresets.json`

Per migrare i predefiniti e le configurazioni del visualizzatore personalizzato creati da `/etc` a `/conf`, eseguire il comando curl Linux® seguente:

`curl -u admin:admin -X POST https://<server_address>:<server_port>/libs/settings/dam/dm/presets.migratedmcontent.json`

## Installare il 18912 del feature pack per la migrazione in blocco delle risorse {#installing-feature-pack-for-bulk-asset-migration}

L&#39;installazione del 18912 del feature pack è *facoltativa*.

Il Feature Pack 18912 consente di acquisire in blocco le risorse tramite FTP o di migrare le risorse dalla modalità Dynamic Medie - Ibrido o Dynamic Media Classic alla modalità Dynamic Medie - Scene7 su Experience Manager. È disponibile da [Adobe Professional Services](https://business.adobe.com/customers/consulting-services/main.html).

Per ulteriori informazioni, consulta [Installare 18912 feature pack per la migrazione in blocco delle risorse](/help/assets/bulk-ingest-migrate.md).

## Creare una configurazione Dynamic Medie in Cloud Service {#configuring-dynamic-media-cloud-services}

<!-- **Before you configure Dynamic Media** - After you receive your provisioning email with Dynamic Media credentials, you must open the [Dynamic Media Classic desktop application](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started), then sign in to your account to change your password. The password provided in the provisioning email is system-generated and intended to be a temporary password only. It is important that you update the password so that Dynamic Media Cloud Service is set up with the correct credentials.

   ![dynamicmediaconfiguration2updated](assets/dynamicmediaconfiguration2updated.png)

**To create a Dynamic Media Configuration in Cloud Services:** -->

1. In modalità Autore Experience Manager, seleziona il logo di Experience Manager per accedere alla console di navigazione globale, fai clic sull&#39;icona Strumenti, quindi vai a **[!UICONTROL Cloud Service]** > **[!UICONTROL Configurazione Dynamic Medie]**.
1. Nel riquadro sinistro della pagina Browser configurazioni Dynamic Medie selezionare **[!UICONTROL global]** (non selezionare l&#39;icona della cartella a sinistra di **[!UICONTROL global]**), quindi selezionare **[!UICONTROL Create]**.
1. Nella pagina **[!UICONTROL Crea configurazione Dynamic Medie]** immettere un titolo, l&#39;indirizzo e-mail dell&#39;account Dynamic Medie, la password, quindi selezionare l&#39;area geografica. Queste informazioni sono fornite da un Adobe nell’e-mail di provisioning. Se non hai ricevuto l’e-mail, contatta l’Assistenza clienti Adobe.

   Selezionare **[!UICONTROL Connetti a Dynamic Medie]**.

1. Nella finestra di dialogo **[!UICONTROL Cambia password]** immettere una nuova password composta da 8-25 caratteri nel campo **[!UICONTROL Nuova password]**. La password deve contenere almeno uno dei seguenti elementi:

   * Lettera maiuscola
   * Lettera minuscola
   * Numero
   * Carattere speciale: `# $ & . - _ : { }`

   Il campo **[!UICONTROL Password corrente]** è stato precompilato intenzionalmente e nascosto dall&#39;interazione.

   Se necessario, è possibile controllare l&#39;ortografia di una password digitata o ridigitata selezionando l&#39;icona dell&#39;occhio della password per visualizzare la password. Seleziona nuovamente l’icona per nascondere la password.

1. Nel campo **[!UICONTROL Ripeti password]**, digita nuovamente la nuova password, quindi seleziona **[!UICONTROL Fine]**.

   La nuova password viene salvata quando si seleziona **[!UICONTROL Salva]** nell&#39;angolo superiore destro della pagina **[!UICONTROL Crea configurazione Dynamic Medie]**.

   Se hai selezionato **[!UICONTROL Annulla]** nella finestra di dialogo **[!UICONTROL Modifica password]**, devi comunque immettere una nuova password quando salvi la configurazione di Dynamic Medie appena creata.

   Vedere anche [Modificare la password in Dynamic Medie](#change-dm-password).

1. Quando la connessione ha esito positivo, impostare quanto segue. Le intestazioni con un asterisco (*) sono obbligatorie:

   * **[!UICONTROL Società]**: il nome dell&#39;account Dynamic Medie.
     >[!IMPORTANT]
     >
     >In un&#39;istanza di Experience Manager è supportata una sola configurazione Dynamic Medie nei Cloud Service. Non aggiungere più di una configurazione. Più configurazioni Dynamic Medie in un&#39;istanza Experience Manager sono _non_ supportate o consigliate da Adobe.

     <!-- CQDOC-19579 and CQDOC-19612 -->

     Vedere anche [Configurare l&#39;account alias società Dynamic Medie](/help/assets/dm-alias-account.md).

   * **[!UICONTROL Percorso cartella principale società]**

   * **[!UICONTROL Pubblicazione di Assets]** - È possibile scegliere tra le tre opzioni seguenti:
      * **[!UICONTROL Immediatamente]** significa che quando le risorse vengono caricate, il sistema le acquisisce e fornisce l&#39;URL/Incorpora immediatamente. Non è necessario alcun intervento da parte dell’utente per pubblicare le risorse.
      * **[!UICONTROL All&#39;attivazione]** significa che devi pubblicare esplicitamente la risorsa prima di fornire un URL o un collegamento di incorporamento.<br><!-- CQDOC-17478, Added March 9, 2021-->A partire dall&#39;Experience Manager 6.5.8, l&#39;istanza di Experience Manager Publish riflette valori di metadati di Dynamic Medie accurati, ad esempio `dam:scene7Domain` e `dam:scene7FileStatus` solo nella modalità di pubblicazione **[!UICONTROL All&#39;attivazione]**. Per abilitare questa funzionalità, installare Service Pack 8, quindi riavviare Experience Manager. Vai a Gestione configurazione Sling. Trovare la configurazione per `Scene7ActivationJobConsumer Component` o crearne una nuova). Selezionare la casella di controllo **[!UICONTROL Replica metadati dopo la pubblicazione di Dynamic Medie]**, quindi selezionare **[!UICONTROL Salva]**.

        ![Casella di controllo Replica metadati dopo pubblicazione Dynamic Medie](assets-dm/replicate-metadata-setting.png)

      * **[!UICONTROL Publish selettivo]** Questa opzione consente di controllare quali cartelle vengono pubblicate in Dynamic Medie. Consente di utilizzare funzioni quali Ritaglio avanzato o rappresentazioni dinamiche oppure di determinare quali cartelle vengono pubblicate esclusivamente in Experience Manager per la visualizzazione in anteprima. Le stesse risorse sono *not* pubblicate in Dynamic Medie per la distribuzione nel dominio pubblico.<br>È possibile impostare questa opzione qui nella **[!UICONTROL Configurazione cloud Dynamic Medie]** oppure, se si preferisce, è possibile scegliere di impostare questa opzione a livello di cartella, nelle **[!UICONTROL Proprietà]** di una cartella.<br>Consulta [Utilizzare Publish selettivo in Dynamic Medie](/help/assets/selective-publishing.md).<br>Se successivamente modifichi questa configurazione o la modifichi a livello di cartella, le modifiche interesseranno solo le nuove risorse caricate da quel momento in poi. Lo stato di pubblicazione delle risorse esistenti nella cartella rimane invariato finché non vengono modificate manualmente da **[!UICONTROL Quick Publish]** o dalla finestra di dialogo **[!UICONTROL Gestisci pubblicazione]**.

   * **[!UICONTROL Server di anteprima protetto]** - consente di specificare il percorso URL del server di anteprima delle copie trasformate protette. In altre parole, dopo la generazione delle rappresentazioni, Experience Manager può accedere in modo sicuro e visualizzare in anteprima le rappresentazioni Dynamic Medie remote (nessun binario viene inviato nuovamente all’istanza Experience Manager).
Adobe A meno che non si disponga di una disposizione speciale per utilizzare il server della propria società o un server speciale, si consiglia di lasciare questa impostazione come specificato.

   * **[!UICONTROL Sincronizza tutto il contenuto]** - <!-- NEW OPTION, CQDOC-15371, Added March 4, 2020-->Selezionato per impostazione predefinita. Deseleziona questa opzione se desideri includere o escludere selettivamente le risorse dalla sincronizzazione con Dynamic Medie. Deselezionando questa opzione è possibile scegliere tra le due seguenti modalità di sincronizzazione di Dynamic Medie:

   * **[!UICONTROL Modalità di sincronizzazione Dynamic Medie]**
      * **[!UICONTROL Attivata per impostazione predefinita]** - La configurazione viene applicata a tutte le cartelle per impostazione predefinita, a meno che non si contrassegni una cartella specificamente per l&#39;esclusione. <!-- you can then deselect the folders that you do not want the configuration applied to.-->
      * **[!UICONTROL Disabilitata per impostazione predefinita]** - La configurazione non viene applicata ad alcuna cartella fino a quando non contrassegni esplicitamente una cartella selezionata per la sincronizzazione con Dynamic Medie.
Per contrassegnare una cartella selezionata per la sincronizzazione con Dynamic Medie, seleziona una cartella di risorse, quindi sulla barra degli strumenti seleziona **[!UICONTROL Proprietà]**. Nella scheda **[!UICONTROL Dettagli]**, nell&#39;elenco a discesa **[!UICONTROL Modalità di sincronizzazione Dynamic Medie]**, scegliere una delle tre opzioni seguenti. Al termine, seleziona **[!UICONTROL Salva]**. *Ricorda: queste tre opzioni non sono disponibili se hai selezionato **[!UICONTROL Sincronizza tutto il contenuto]**in precedenza.* Vedere anche [Utilizzare Selective Publish a livello di cartella in Dynamic Medie](/help/assets/selective-publishing.md).
         * **[!UICONTROL Ereditato]** - Nessun valore di sincronizzazione esplicito nella cartella. La cartella eredita invece il valore di sincronizzazione da una delle cartelle precedenti o dalla modalità predefinita nella configurazione cloud. Lo stato dettagliato per ereditato viene visualizzato tramite una descrizione comando.
         * **[!UICONTROL Abilita per le sottocartelle]** - Includi tutto in questa sottostruttura per la sincronizzazione con Dynamic Medie. Le impostazioni specifiche della cartella sovrascrivono la modalità predefinita nella configurazione cloud.
         * **[!UICONTROL Disattivato per le sottocartelle]** - Escludi tutto ciò che si trova in questa sottostruttura dalla sincronizzazione con Dynamic Medie.

   >[!NOTE]
   >
   >Il controllo delle versioni non è supportato in modalità Dynamic Medie - Scene7. Inoltre, l’attivazione ritardata si applica solo se l’opzione **[!UICONTROL Pubblica risorse]** della pagina Modifica configurazione Dynamic Media è impostata su **[!UICONTROL All’attivazione]** e soltanto fino alla prima attivazione della risorsa.
   >
   >Dopo l’attivazione di una risorsa, tutti gli aggiornamenti vengono immediatamente pubblicati in tempo reale in S7 Delivery.

1. Seleziona **[!UICONTROL Salva]**.
1. Per visualizzare in anteprima in modo sicuro il contenuto Dynamic Medie prima che venga pubblicato, Experience Manager Author utilizza la convalida basata su token e quindi per impostazione predefinita Experience Manager Author visualizza in anteprima il contenuto Dynamic Medie. Tuttavia, puoi &quot;inserire nell&#39;elenco Consentiti&quot; più IP per consentire agli utenti di accedere ai contenuti in anteprima in modo sicuro. Per configurare questa azione in Experience Manager, vedere [Configurazione di Installazione di Dynamic Medie Publish per Image Server - Scheda Sicurezza](/help/assets/dm-publish-settings.md#security-tab).

Se si desidera personalizzare ulteriormente la configurazione, ad esempio abilitando le autorizzazioni ACL (Access Control List), è possibile completare facoltativamente qualsiasi attività in [(Facoltativo) Configura impostazioni avanzate in modalità Dynamic Medie - Scene7](#optional-configuring-advanced-settings-in-dynamic-media-scene-mode).

<!-- 1. To securely preview Dynamic Media content before it gets published, Experience Manager uses token-based validation and hence Experience Manager Author previews Dynamic Media content by default. However, you can *allowlist* more IPs to provide users access to securely preview content. To set up this action in Experience Manager, see [Configure Dynamic Media Publish Setup for Image Server - Security tab](/help/assets/dm-publish-settings.md#security-tab).     * In Experience Manager Author mode, select the Experience Manager logo to access the global navigation console.
    * In the left rail, select the **[!UICONTROL Tools]** icon, then go to **[!UICONTROL Assets]** > **[!UICONTROL Dynamic Media Publish Setup]**.
    * On the Dynamic Media Image Server page, in the **[!UICONTROL Publish Context]** drop-down list, select **[!UICONTROL Test Image Serving]**.
    * Select the **[!UICONTROL Security]** tab.
    * For the **[!UICONTROL Client address]**, select **[!UICONTROL Add]**.
    * Enter the IP address of the Experience Manager Author instance (not Dispatcher IP).
    * In the upper-right corner of the page, select **[!UICONTROL Save]**. -->

La configurazione di base è terminata; puoi utilizzare la modalità Dynamic Medie - Scene7.

### Cambia la password in Dynamic Medie {#change-dm-password}

La scadenza della password in Dynamic Medie è impostata su 100 anni dalla data di sistema corrente.

La password deve contenere almeno uno dei seguenti elementi:

* Lettera maiuscola
* Lettera minuscola
* Numero
* Carattere speciale: `# $ & . - _ : { }`

Se necessario, è possibile controllare l&#39;ortografia di una password digitata o ridigitata selezionando l&#39;icona dell&#39;occhio della password per visualizzare la password. Seleziona nuovamente l’icona per nascondere la password.

La password modificata viene salvata quando si seleziona **[!UICONTROL Salva]** nell&#39;angolo superiore destro della pagina **[!UICONTROL Modifica configurazione Dynamic Medie]**.

**Per cambiare la password in Dynamic Medie:**

1. In modalità Autore Experience Manager, seleziona il logo di Experience Manager per accedere alla console di navigazione globale.
1. Sulla sinistra della console, seleziona l&#39;icona Strumenti, quindi vai a **[!UICONTROL Cloud Service] > [!UICONTROL Configurazione Dynamic Medie]**.
1. Nel riquadro a sinistra della pagina Browser configurazioni Dynamic Medie selezionare **[!UICONTROL global]**. Non selezionare l&#39;icona della cartella a sinistra di **[!UICONTROL global]**. Quindi, seleziona **[!UICONTROL Modifica]**.
1. Nella pagina **[!UICONTROL Modifica configurazione Dynamic Medie]**, sotto il campo **[!UICONTROL Password]**, selezionare **[!UICONTROL Modifica password]**.
1. Nella finestra di dialogo **[!UICONTROL Modifica password]** eseguire le operazioni seguenti:

   * Nel campo **[!UICONTROL Nuova password]** immettere una nuova password.

     Il campo **[!UICONTROL Password corrente]** è stato precompilato intenzionalmente e nascosto dall&#39;interazione.

   * Nel campo **[!UICONTROL Ripeti password]**, digita nuovamente la nuova password, quindi seleziona **[!UICONTROL Fine]**.

1. Nell&#39;angolo superiore destro della pagina **[!UICONTROL Modifica configurazione Dynamic Medie]**, selezionare **[!UICONTROL Salva]**, quindi selezionare **[!UICONTROL OK]**.

## (Facoltativo) Configurazione delle impostazioni avanzate in modalità Dynamic Medie - Scene7 {#optional-configuring-advanced-settings-in-dynamic-media-scene-mode}

Se desideri personalizzare ulteriormente la configurazione e l&#39;installazione di Dynamic Medie - modalità Scene7 o ottimizzarne le prestazioni, puoi completare una o più delle seguenti *attività facoltative*:

* [(Facoltativo) Abilitare le autorizzazioni ACL in modalità Dynamic Medie - Scene7](#optional-enable-acl)

* [(Facoltativo) Configura Dynamic Medie in modalità Scene7 per il caricamento di risorse superiori a 2 GB](#optional-config-dms7-assets-larger-than-2gb)

* [(Facoltativo) Configurazione di Dynamic Medie - Impostazioni modalità Scene7](#optional-setup-and-configuration-of-dynamic-media-scene7-mode-settings)

* [(Facoltativo) Ottimizzazione delle prestazioni di Dynamic Medie in modalità Scene7](#optional-tuning-the-performance-of-dynamic-media-scene-mode)

* [(Facoltativo) Filtrare le risorse per la replica](#optional-filtering-assets-for-replication)

### (Facoltativo) Abilitare le autorizzazioni dell’elenco di controllo degli accessi in modalità Dynamic Medie - Scene7 {#optional-enable-acl}

Quando si esegue la modalità Dynamic Medie - Scene7 su AEM, al momento vengono inoltrate `/is/image` richieste al server immagini di anteprima protetto senza verificare le autorizzazioni ACL (Access Control List) in Platform Server Servlet. È tuttavia possibile *abilitare* le autorizzazioni ACL. In questo modo, le `/is/image` richieste autorizzate verranno inoltrate. Se un utente non è autorizzato ad accedere alla risorsa, viene visualizzato un errore &quot;403 - Non consentito&quot;.

**Per abilitare le autorizzazioni ACL in Dynamic Medie - Modalità Scene7:**

1. Dall&#39;Experience Manager passare a **[!UICONTROL Strumenti]** > **[!UICONTROL Operazioni]** > **[!UICONTROL Console Web]**.

   ![2019-08-02_16-13-14](assets/2019-08-02_16-13-14.png)

1. Viene visualizzata una nuova scheda del browser alla pagina **[!UICONTROL Configurazione console Web Adobe Experience Manager]**.

   ![2019-08-02_16-17-29](assets/2019-08-02_16-17-29.png)

1. Nella pagina scorrere fino al nome *Adobe CQ Scene7 PlatformServer*.

1. A destra del nome, seleziona l&#39;icona della matita (**[!UICONTROL Modifica i valori di configurazione]**).

1. Nella pagina **com.adobe.cq.dam.s7imaging.impl.ps.PlatformServerServlet.name** selezionare la casella di controllo relativa alle due impostazioni seguenti:

   * `com.adobe.cq.dam.s7imaging.impl.ps.PlatformServerServlet.cache.enable.name` - Se attivata, questa impostazione memorizza nella cache i risultati delle autorizzazioni per 120 secondi (due minuti) (impostazione predefinita) per il salvataggio.
   * `com.adobe.cq.dam.s7imaging.impl.ps.PlatformServerServlet.validate.userAccess.name` - Se abilitata, questa impostazione convalida l&#39;accesso di un utente durante l&#39;anteprima delle risorse tramite Dynamic Medie Image Server.

   ![Abilitare le impostazioni dell&#39;elenco di controllo di accesso in Dynamic Medie - modalità Scene7](/help/assets/assets-dm/acl.png)

1. Seleziona **[!UICONTROL Salva]** nell&#39;angolo inferiore destro della pagina.

### (Facoltativo) Configura Dynamic Medie in modalità Scene7 per il caricamento di risorse superiori a 2 GB {#optional-config-dms7-assets-larger-than-2gb}

In modalità Dynamic Medie - Scene7, la dimensione predefinita del file di caricamento delle risorse è pari o inferiore a 2 GB. Tuttavia, puoi facoltativamente configurare il caricamento di risorse di dimensioni superiori a 2 GB e fino a 15 GB.

Se intendi utilizzare questa funzione, tieni presenti i seguenti prerequisiti e punti:

* È necessario eseguire Experience Manager 6.5 con Service Pack 6.5.4.0 o versione successiva in modalità Dynamic Medie - Scene7.
* Questa funzionalità di caricamento di grandi dimensioni è supportata solo per i clienti [*Managed Services*](https://business.adobe.com/products/experience-manager/managed-services.html).
* Verifica che l’istanza Experience Manager sia configurata con l’archiviazione BLOB di Amazon S3 o Microsoft® Azure.

  >[!NOTE]
  >
  >Configura l’archiviazione BLOB di Azure con una chiave di accesso e una chiave segreta perché questa funzione di caricamento di grandi dimensioni non è supportata con AzureSas nella configurazione dell’archiviazione BLOB.

* Il [download dell&#39;accesso binario diretto](https://jackrabbit.apache.org/oak/docs/features/direct-binary-access.html) di Oak è abilitato (non è necessario il *caricamento dell&#39;accesso binario diretto* di Oak).

  Per abilitare il download dell&#39;accesso binario diretto, impostare la proprietà `presignedHttpDownloadURIExpirySeconds > 0` nella configurazione dell&#39;archivio dati. Il valore deve essere sufficientemente lungo per scaricare file binari più grandi ed eventualmente riprovare.

* Assets di dimensioni superiori a 15 GB non viene caricato. (Il limite di dimensione viene impostato al punto 8.)
* Quando il flusso di lavoro **[!UICONTROL Rielabora risorse Dynamic Medie]** viene attivato in una cartella, vengono rielaborate tutte le risorse di grandi dimensioni già sincronizzate con la società Dynamic Medie. Tuttavia, se nella cartella non sono ancora sincronizzate risorse di grandi dimensioni, la risorsa non viene caricata. Pertanto, per sincronizzare risorse di grandi dimensioni esistenti in Dynamic Medie, puoi eseguire il flusso di lavoro **[!UICONTROL Rielabora Dynamic Medie]** risorse per le singole risorse.

**Per configurare Dynamic Medie - Modalità Scene7 per il caricamento di risorse superiori a 2 GB:**

1. In Experience Manager, seleziona il logo di Experience Manager per accedere alla console di navigazione globale, quindi passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Generale]** > **[!UICONTROL CRXDE Liti]**.

1. Nella finestra di CRXDE Lite eseguire una delle operazioni seguenti:

   * Nella barra a sinistra, passa al seguente percorso:

     `/libs/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload`

   * Copiare e incollare il percorso precedente nel campo Percorso CRXDE Liti sotto la barra degli strumenti, quindi premere `Enter`.

1. Nella barra a sinistra, fai clic con il pulsante destro del mouse su `fileupload`, quindi seleziona **[!UICONTROL Sovrapponi nodo]** dal menu a comparsa.

   ![Opzione Sovrapponi nodo](/help/assets/assets-dm/uploadassets15gb_a.png)

1. Nella finestra di dialogo Sovrapponi nodo selezionare la casella di controllo **[!UICONTROL Corrispondenza tipi di nodo]** per attivare l&#39;opzione, quindi selezionare **[!UICONTROL OK]**.

   ![Finestra di dialogo Sovrapponi nodo](/help/assets/assets-dm/uploadassets15gb_b.png)

1. Dalla finestra di CRXDE Lite, effettuare una delle seguenti operazioni:

   * Nella barra a sinistra, passa al seguente percorso del nodo di sovrapposizione:

     `/apps/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload`

   * Copiare e incollare il percorso precedente nel campo Percorso CRXDE Liti sotto la barra degli strumenti, quindi premere `Enter`.

1. Nella scheda **[!UICONTROL Proprietà]**, nella colonna **[!UICONTROL Nome]**, individua `sizeLimit`.
1. A destra del nome `sizeLimit`, nella colonna **[!UICONTROL Valore]** fare doppio clic sul campo del valore.
1. Immetti il valore appropriato in byte in modo da poter aumentare il limite di dimensioni fino alla dimensione di caricamento massima desiderata. Ad esempio, per aumentare il limite di dimensioni della risorsa da caricare a 10 GB, immetti `10737418240` nel campo del valore.
È possibile immettere un valore fino a 15 GB (`2013265920` byte). In questo caso, le risorse caricate di dimensioni superiori a 15 GB non vengono caricate.

   ![Valore limite dimensioni](/help/assets/assets-dm/uploadassets15gb_c.png)

1. Selezionare **[!UICONTROL Salva tutto]** nell&#39;angolo superiore sinistro della finestra di CRXDE Lite.

   *Impostare ora il timeout per l&#39;Adobe Granite Workflow External Process Job Handler eseguendo le operazioni seguenti:*

1. In Experience Manager, seleziona il logo di Experience Manager per accedere alla console di navigazione globale.
1. Effettuare una delle seguenti operazioni:

   * Passa al seguente percorso URL:

     `localhost:4502/system/console/configMgr/com.adobe.granite.workflow.core.job.ExternalProcessJobHandler`

   * Copia e incolla il percorso precedente nel campo URL del browser. Assicurati di sostituire `localhost:4502` con la tua istanza Experience Manager.

1. Nella finestra di dialogo **[!UICONTROL Adobe Granite Workflow External Process Job Handler]**, nel campo **[!UICONTROL Max Timeout]**, impostare il valore su `18000` secondi (cinque ore). Il valore predefinito è 10800 secondi (tre ore).

   ![Valore di timeout massimo](/help/assets/assets-dm/uploadassets15gb_d.png)

1. Nell&#39;angolo inferiore destro della finestra di dialogo, seleziona **[!UICONTROL Salva]**.

   *Impostare ora il timeout per il passaggio del processo di caricamento binario diretto di Scene7 eseguendo le operazioni seguenti:*

1. In Experience Manager, seleziona il logo di Experience Manager per accedere alla console di navigazione globale.
1. Passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Flusso di lavoro]** > **[!UICONTROL Modelli]**.
1. Nella pagina Modelli flusso di lavoro, selezionare **[!UICONTROL Codifica video Dynamic Medie]**.
1. Sulla barra degli strumenti, selezionare **[!UICONTROL Modifica]**.
1. Nella pagina del flusso di lavoro, fai doppio clic sul passaggio del processo **[!UICONTROL Caricamento binario diretto Scene7]**.
1. Nella finestra di dialogo **[!UICONTROL Proprietà passaggio]**, nella scheda **[!UICONTROL Comune]**, sotto l&#39;intestazione **[!UICONTROL Impostazioni avanzate]**, nel campo **[!UICONTROL Timeout]**, immettere un valore di `18000` secondi (cinque ore). Il valore predefinito è `3600` secondi (un&#39;ora).
1. Selezionare **[!UICONTROL OK]**.
1. Seleziona **[!UICONTROL Sincronizza]**.
1. Ripeti i passaggi 14-21 per il modello di flusso di lavoro **[!UICONTROL Risorsa di aggiornamento DAM]** e per il modello di flusso di lavoro **[!UICONTROL Rielabora Dynamic Medie]**.

### (Facoltativo) Configurazione di Dynamic Medie - Impostazioni modalità Scene7 {#optional-setup-and-configuration-of-dynamic-media-scene7-mode-settings}

<!-- When you are in run mode `dynamicmedia_scene7`, use the Dynamic Media Classic user interface to change your Dynamic Media settings. -->

* [Configurazione di Dynamic Medie Publish Setup per il server immagini](/help/assets/dm-publish-settings.md)
* [Configurazione impostazioni generali di Dynamic Medie](/help/assets/dm-general-settings.md)
* [Configura gestione colore](#configuring-color-management)
* [Modifica tipi MIME per i formati supportati](#editing-mime-types-for-supported-formats)
* [Aggiungere tipi MIME per formati non supportati](#adding-mime-types-for-unsupported-formats)
* [Creazione di set di batch predefiniti per generare automaticamente set di immagini e set 360 gradi](#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets) (operazione eseguita nell&#39;interfaccia utente di Dynamic Media Classic)

#### Configurazione di Dynamic Medie Publish Setup per il server immagini {#publishing-setup-for-image-server}

La pagina Configurazione di Dynamic Medie Publish stabilisce le impostazioni predefinite che determinano il modo in cui le risorse vengono consegnate dai server Dynamic Medie Adobe ai siti web o alle applicazioni.

Consulta [Configurare Dynamic Medie Publish Setup per Image Server](/help/assets/dm-publish-settings.md).

#### Configurazione impostazioni generali di Dynamic Medie {#configuring-application-general-settings}

Configura l&#39;URL di Dynamic Medie **[!UICONTROL Publish Server Name]** e l&#39;URL di **[!UICONTROL Origin Server Name]**. Puoi anche specificare **[!UICONTROL Impostazioni di caricamento nell&#39;applicazione]** e **[!UICONTROL Opzioni di caricamento predefinite]** in base al tuo caso d&#39;uso specifico.

Consulta [Configurare le impostazioni generali di Dynamic Medie](/help/assets/dm-general-settings.md).

#### Configura gestione colore {#configuring-color-management}

La gestione del colore di Dynamic Medie consente di correggere il colore delle risorse. Con la correzione del colore, le risorse acquisite mantengono lo spazio colore (RGB, CMYK, Grigio) e il profilo colore incorporato. Quando si richiede una rappresentazione dinamica, il colore dell&#39;immagine viene corretto nello spazio colore di destinazione utilizzando l&#39;output CMYK, RGB o Grigio.

Consulta [Configurare i predefiniti immagine](/help/assets/managing-image-presets.md).

>[!NOTE]
>
>Per impostazione predefinita, il sistema mostra 15 rappresentazioni quando selezioni **[!UICONTROL Rappresentazioni]** e 15 predefiniti visualizzatore quando selezioni **[!UICONTROL Visualizzatori]** nella visualizzazione Dettaglio della risorsa. Puoi aumentare questo limite. Vedere [Aumentare il numero di predefiniti immagine visualizzati](/help/assets/managing-image-presets.md#increasing-or-decreasing-the-number-of-image-presets-that-display) o [Aumentare il numero di predefiniti visualizzatore visualizzati](/help/assets/managing-viewer-presets.md#increasing-the-number-of-viewer-presets-that-display).

#### Modifica tipi MIME per i formati supportati {#editing-mime-types-for-supported-formats}

Puoi definire quali tipi di risorse vengono elaborati da Dynamic Medie e personalizzare parametri avanzati di elaborazione delle risorse. Ad esempio, puoi specificare i parametri di elaborazione delle risorse per effettuare le seguenti operazioni:

* Convertire un’Adobe PDF in una risorsa eCatalog.
* Converti un documento di Adobe Photoshop (con estensione PSD) in una risorsa modello banner per la personalizzazione.
* Rasterizza un file Adobe Illustrator (.AI) o un file Adobe Photoshop Encapsulated PostScript® (.EPS).
* È possibile utilizzare [Profili video](/help/assets/video-profiles.md) e [Profili immagine](/help/assets/image-profiles.md) per definire l&#39;elaborazione di video e immagini, rispettivamente.

Vedi [Caricamento di Assets](/help/assets/manage-assets.md#uploading-assets).

**Per modificare i tipi MIME per i formati supportati:**

1. In Experience Manager, seleziona il logo di Experience Manager per accedere alla console di navigazione globale, quindi passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Generale]** > **[!UICONTROL CRXDE Liti]**.
1. Nella barra a sinistra, accedi a:

   `/conf/global/settings/cloudconfigs/dmscene7/jcr:content/mimeTypes`

   ![Tipi MIME](assets/mimetypes.png)

1. Nella cartella mimeTypes, seleziona un tipo mime.
1. Nella parte inferiore, sul lato destro della pagina CRXDE Lite:

   * Fare doppio clic sul campo **[!UICONTROL enabled]**. Per impostazione predefinita, tutti i tipi di risorse mime sono abilitati (impostati su **[!UICONTROL true]**), il che significa che le risorse vengono sincronizzate con Dynamic Medie per l&#39;elaborazione. Se desideri escludere questo tipo di risorsa mime dall&#39;elaborazione, modifica questa impostazione in **[!UICONTROL false]**.

   * Selezionare **[!UICONTROL jobParam]** per aprire il relativo campo di testo associato. Per un elenco dei valori dei parametri di elaborazione consentiti che è possibile utilizzare per un determinato tipo MIME, vedere [Tipi MIME supportati](/help/assets/assets-formats.md#supported-mime-types).

1. Effettua una delle operazioni seguenti:

   * Ripeti i passaggi 3-4 per modificare più tipi MIME.
   * Nella barra dei menu della pagina CRXDE Lite, seleziona **[!UICONTROL Salva tutto]**.

1. Nell&#39;angolo superiore sinistro della pagina, seleziona **[!UICONTROL CRXDE Liti]** per tornare a Experience Manager.

#### Aggiunta di tipi MIME per formati non supportati {#adding-mime-types-for-unsupported-formats}

In Experience Manager Assets è possibile aggiungere tipi MIME personalizzati per formati non supportati. Verificare che qualsiasi nuovo nodo aggiunto in CRXDE Lite non venga eliminato da Experience Manager spostando il tipo MIME prima di `image_`. Assicurarsi inoltre che il valore abilitato sia impostato su **[!UICONTROL false]**.

**Per aggiungere tipi MIME per formati non supportati:**

1. Dall&#39;Experience Manager passare a **[!UICONTROL Strumenti]** > **[!UICONTROL Operazioni]** > **[!UICONTROL Console Web]**.

   ![2019-08-02_16-13-14](assets/2019-08-02_16-13-14.png)

1. Viene visualizzata una nuova scheda del browser alla pagina **[!UICONTROL Configurazione console Web Adobe Experience Manager]**.

   ![2019-08-02_16-17-29](assets/2019-08-02_16-17-29.png)

1. Nella pagina, scorri verso il basso fino al nome *Adobe CQ Scene7 Asset MIME type Service*, come illustrato nella schermata successiva. A destra del nome, selezionare **[!UICONTROL Modifica i valori di configurazione]** (icona a forma di matita).

   ![2019-08-02_16-44-56](assets/2019-08-02_16-44-56.png)

1. Nella pagina **Adobe CQ Scene7 Asset MIME type Service**, seleziona l&#39;icona del segno più &lt;+>. La posizione nella tabella in cui selezioni il segno più per aggiungere il nuovo tipo mime è insignificante.

   ![2019-08-02_16-27-27](assets/2019-08-02_16-27-27.png)

1. Digitare `DWG=image/vnd.dwg` nel campo di testo vuoto appena aggiunto.

   L&#39;esempio `DWG=image/vnd.dwg` è solo a scopo dimostrativo. Il tipo MIME aggiunto qui può essere qualsiasi altro formato non supportato.

   ![2019-08-02_16-36-36](assets/2019-08-02_16-36-36.png)

1. Nell&#39;angolo inferiore destro della pagina, seleziona **[!UICONTROL Salva]**.

   A questo punto, è possibile chiudere la scheda del browser che include la pagina Apri configurazione console Web Adobe Experience Manager.

1. Torna alla scheda del browser che presenta la console di Experience Manager aperta.
1. Dall&#39;Experience Manager passare a **[!UICONTROL Strumenti]** > **[!UICONTROL Generale]** > **[!UICONTROL CRXDE Liti]**.

   ![2019-08-02_16-55-41](assets/2019-08-02_16-55-41.png)

1. Nella barra a sinistra, accedi a:

   `conf/global/settings/cloudconfigs/dmscene7/jcr:content/mimeTypes`

1. Trascina il tipo mime `image_vnd.dwg` e rilascialo direttamente sopra `image_` nella struttura, come illustrato nella schermata seguente.

   ![crxdelite_cqdoc-14627](assets/crxdelite_cqdoc-14627.png)

1. Con il tipo mime `image_vnd.dwg` ancora selezionato, dalla scheda **[!UICONTROL Proprietà]**, nella riga **[!UICONTROL enabled]**, nell&#39;intestazione della colonna **[!UICONTROL Valore]**, selezionare due volte il valore per aprire l&#39;elenco a discesa **[!UICONTROL Valore]**.
1. Digita `false` nel campo (oppure seleziona **[!UICONTROL false]** dall&#39;elenco a discesa).

   ![2019-08-02_16-60-30](assets/2019-08-02_16-60-30.png)

1. Selezionare **[!UICONTROL Salva tutto]** nell&#39;angolo superiore sinistro della pagina CRXDE Liti.

#### Creare predefiniti set di batch per generare automaticamente set di immagini e set 360 gradi {#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets}

Utilizza i predefiniti per set di batch per automatizzare la creazione di set di immagini o set 360 gradi durante il caricamento delle risorse in Dynamic Medie.

Innanzitutto, definisci la convenzione di denominazione per il raggruppamento delle risorse in un set. Quindi crea un predefinito per set di batch costituito da un set di istruzioni autonomo con un nome univoco. Deve definire come creare il set utilizzando immagini che corrispondano alle convenzioni di denominazione definite nella ricetta predefinita.

Quando caricate i file, Dynamic Medie crea automaticamente un set con tutti i file che corrispondono alla convenzione di denominazione definita nei predefiniti attivi.

##### Configurare la denominazione predefinita

Crea una convenzione di denominazione predefinita utilizzata in qualsiasi composizione predefinita per set di batch. La convenzione di denominazione predefinita selezionata nella definizione del predefinito per set di batch è probabilmente tutto ciò che serve alla società per generare set in batch. Un predefinito per set di batch viene creato per utilizzare la convenzione di denominazione predefinita definita dall&#39;utente. È possibile creare tutti i predefiniti per set di batch con convenzioni di denominazione alternative e personalizzate necessarie per un particolare set di contenuti nei casi in cui vi sia un’eccezione alla denominazione predefinita definita dall’azienda.

Sebbene la configurazione di una convenzione di denominazione predefinita non sia necessaria per utilizzare la funzionalità di impostazione predefinita per set di batch, è consigliabile utilizzare la convenzione di denominazione predefinita. Consente di definire tutti gli elementi della convenzione di denominazione che si desidera raggruppare in un set, in modo da semplificare la creazione di set batch.

In alternativa, è possibile utilizzare **[!UICONTROL Visualizza codice]** senza campi modulo disponibili. In questa vista puoi creare le definizioni delle convenzioni di denominazione interamente utilizzando espressioni regolari.

Sono disponibili due elementi per la definizione, Corrispondenza (Match) e Nome base (Base Name). Questi campi ti consentono di definire tutti gli elementi di una convenzione di denominazione e di identificare la parte della convenzione utilizzata per denominare il set in cui sono contenuti. La convenzione di denominazione individuale di un’azienda spesso utilizza una o più righe di definizione per ciascuno di questi elementi. È possibile utilizzare un numero illimitato di righe per la definizione univoca e raggrupparle in elementi distinti, ad esempio per l&#39;immagine principale, l&#39;elemento Colore, l&#39;elemento Visualizzazione alternativa e l&#39;elemento Campione.

**Per configurare la denominazione predefinita:**

1. Apri l&#39;[applicazione desktop Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started), quindi accedi al tuo account.

   Le credenziali e i dettagli di accesso sono stati forniti da Adobe al momento del provisioning. Se non disponi di queste informazioni, contatta l’Assistenza clienti Adobe.

1. Sulla barra di spostamento nella parte superiore della pagina, passare a **[!UICONTROL Configurazione]** > **[!UICONTROL Configurazione applicazione]** > **[!UICONTROL Predefiniti set di batch]** > **[!UICONTROL Denominazione predefinita]**.
1. Per specificare come visualizzare e immettere le informazioni di ciascun elemento, seleziona **[!UICONTROL Visualizza modulo]** o **[!UICONTROL Visualizza codice]**.

   È possibile selezionare la casella di controllo **[!UICONTROL Visualizza codice]** per visualizzare la creazione del valore dell&#39;espressione regolare insieme alle selezioni del modulo. È possibile immettere o modificare questi valori per definire gli elementi della convenzione di denominazione, se la vista della maschera vi limita per qualsiasi motivo. Se non è possibile analizzare i valori nella visualizzazione del modulo, i campi del modulo diventano inattivi.

   >[!NOTE]
   >
   >I campi modulo disattivati non eseguono alcuna verifica della correttezza delle espressioni regolari. Vengono visualizzati i risultati dell&#39;espressione regolare che si sta creando per ogni elemento dopo la riga Risultato. L’espressione regolare completa è visibile nella parte inferiore della pagina.

1. Espandi ogni elemento in base alle esigenze e immetti le convenzioni di denominazione che desideri utilizzare.
1. Se necessario, effettuare una delle seguenti operazioni:

   * Selezionare **[!UICONTROL Aggiungi]** per aggiungere un&#39;altra convenzione di denominazione per un elemento.
   * Selezionare **[!UICONTROL Rimuovi]** per eliminare una convenzione di denominazione per un elemento.

1. Effettua una delle operazioni seguenti:

   * Selezionare **[!UICONTROL Salva con nome]** e digitare un nome per il predefinito.
   * Seleziona **[!UICONTROL Salva]** se stai modificando un predefinito esistente.

##### Creare un predefinito per set di batch

Dynamic Medie utilizza i predefiniti per set di batch per organizzare le risorse in set di immagini (immagini alternative, opzioni di colore, 360 giri) da visualizzare nei visualizzatori. I predefiniti per set di batch vengono eseguiti automaticamente insieme ai processi di caricamento delle risorse in Dynamic Medie.

Puoi creare, modificare e gestire i predefiniti per set di batch. Esistono due forme di definizioni di predefiniti per set di batch: una per una convenzione di denominazione predefinita che puoi impostare e una per le convenzioni di denominazione personalizzate che puoi creare al volo.

È possibile utilizzare il metodo campo modulo per definire un predefinito per set di batch oppure il metodo codice, che consente di utilizzare espressioni regolari. Come nella Denominazione predefinita, è possibile scegliere Visualizza codice contemporaneamente alla definizione nella Vista modulo e utilizzare espressioni regolari per creare le definizioni. In alternativa, è possibile deselezionare una delle due visualizzazioni per utilizzare esclusivamente una delle due.

**Per creare un predefinito per set di batch:**

1. Apri l&#39;[applicazione desktop Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started), quindi accedi al tuo account.

   Le credenziali e i dettagli di accesso sono stati forniti da Adobe al momento del provisioning. Se non disponi di queste informazioni, contatta l’Assistenza clienti Adobe.

1. Sulla barra di spostamento nella parte superiore della pagina, passare a **[!UICONTROL Configurazione]** > **[!UICONTROL Configurazione applicazione]** > **[!UICONTROL Predefiniti set di batch]** > **[!UICONTROL Predefinito set di batch]**.

   La visualizzazione predefinita è **[!UICONTROL Visualizza modulo]**, impostata nell&#39;angolo superiore destro della pagina Dettagli.

1. Nel pannello Elenco predefiniti, seleziona **[!UICONTROL Aggiungi]** per attivare i campi di definizione nel pannello Dettagli sul lato destro dello schermo.
1. Nel campo Nome predefinito del pannello Dettagli, digitate un nome per il predefinito.
1. Nel menu a discesa Tipo set di batch, selezionare un tipo di predefinito.
1. Effettua una delle operazioni seguenti:

   * Se utilizzi una convenzione di denominazione predefinita che hai impostato in precedenza in **[!UICONTROL Configurazione applicazione]** > **[!UICONTROL Predefiniti set di batch]** > **[!UICONTROL Denominazione predefinita]**, espandi **[!UICONTROL Convenzioni di denominazione risorse]**, quindi seleziona **[!UICONTROL Predefinito]** nell&#39;elenco a discesa Denominazione file.

   * Per definire una nuova convenzione di denominazione durante la configurazione del predefinito, espandi **[!UICONTROL Convenzioni di denominazione delle risorse]**, quindi seleziona **[!UICONTROL Personalizzato]** nell&#39;elenco a discesa Denominazione file.

1. Per Ordine sequenze, definite l&#39;ordine di visualizzazione delle immagini dopo il raggruppamento del set in Dynamic Medie.

   Per impostazione predefinita, le risorse sono ordinate in ordine alfanumerico. Tuttavia, puoi utilizzare un elenco separato da virgole di espressioni regolari per definire l’ordine.

1. Per Imposta convenzione di denominazione e creazione, specificate il suffisso o il prefisso del nome di base definito nella convenzione di denominazione delle risorse. Inoltre, definisci dove viene creato il set all’interno della struttura di cartelle di Dynamic Medie.

   Se definisci un numero elevato di set, mantieni i set separati dalle cartelle che contengono le risorse stesse. Ad esempio, crea una cartella Set di immagini e inserisci qui i set generati.

1. Nel pannello Dettagli, seleziona **[!UICONTROL Salva]**.
1. Seleziona **[!UICONTROL Attivo]** accanto al nuovo nome del predefinito.

   L’attivazione del predefinito assicura che, quando si caricano le risorse in Dynamic Medie, venga applicato il predefinito per set di batch per generare il set.

##### Creare un predefinito per set di batch per la generazione automatica di un set 360 gradi 2D

È possibile utilizzare il tipo di set di batch **[!UICONTROL Set 360 gradi a più assi]** per creare una ricetta che automatizza la generazione di set 360 gradi 2D. Il raggruppamento di immagini utilizza espressioni regolari Row e Column per allineare correttamente le risorse immagine nella posizione corrispondente nell’array multidimensionale. Non esiste un numero minimo o massimo di righe o colonne da avere in un set 360 gradi con più assi.

Ad esempio, si supponga di voler creare un set 360 gradi con più assi denominato `spin-2dspin`. Hai un set di immagini set 360 gradi che contengono tre righe, con 12 immagini per riga. Le immagini sono denominate come segue:

```xml {.line-numbers}
spin-01-01
 spin-01-02
 …
 spin-01-12
 spin-02-01
 …
 spin-03-12
```

Con queste informazioni, la composizione del tipo di set di batch può essere creata come segue:

![chlimage_1-560](assets/chlimage_1-560.png)

Il raggruppamento per la parte del nome della risorsa condivisa del set 360 gradi è stato aggiunto al campo **[!UICONTROL Corrispondenza]** (come evidenziato). La parte variabile del nome della risorsa, contenente la riga e la colonna, viene aggiunta rispettivamente ai campi **[!UICONTROL Riga]** e **[!UICONTROL Colonna]**.

Quando il set 360 gradi viene caricato e pubblicato, puoi attivare il nome della definizione del set 360 gradi 2D che è riportato in **[!UICONTROL Predefiniti set di batch]**, nella finestra di dialogo **[!UICONTROL Opzioni processo di caricamento]**.

**Per creare un predefinito per set di batch per la generazione automatica di un set 360 gradi 2D:**

1. Apri l&#39;[applicazione desktop Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started), quindi accedi al tuo account.

   Le credenziali e i dettagli di accesso sono stati forniti da Adobe al momento del provisioning. Se non disponi di queste informazioni, contatta l’Assistenza clienti Adobe.

1. Sulla barra di spostamento nella parte superiore della pagina, passare a **[!UICONTROL Configurazione]** > **[!UICONTROL Configurazione applicazione]** > **[!UICONTROL Predefiniti set di batch]** > **[!UICONTROL Predefinito set di batch]**.

   La visualizzazione predefinita è **[!UICONTROL Visualizza modulo]**, impostata nell&#39;angolo superiore destro della pagina Dettagli.

1. Nel pannello Elenco predefiniti, seleziona **[!UICONTROL Aggiungi]** per attivare i campi di definizione nel pannello Dettagli sul lato destro dello schermo.
1. Nel campo Nome predefinito del pannello Dettagli, digitate un nome per il predefinito.
1. Nel menu a discesa Tipo set di batch, seleziona **[!UICONTROL Set risorse]**.
1. Nell&#39;elenco a discesa Sottotipo selezionare **[!UICONTROL Set 360 gradi con asse multiplo]**.
1. Espandi **[!UICONTROL Convenzioni di denominazione risorse]**, quindi seleziona **[!UICONTROL Personalizzato]** nell&#39;elenco a discesa Denominazione file.
1. Utilizza gli attributi **[!UICONTROL Match (Corrispondenza)]** e, facoltativamente, **[!UICONTROL Nome base]** per definire un’espressione regolare per la denominazione delle risorse dell’immagine che compongono il raggruppamento.

   Ad esempio, l’espressione regolare Match letterale può avere l’aspetto seguente:

   `(w+)-w+-w+`

1. Espandere **[!UICONTROL Posizione colonna riga]**, quindi definire il formato del nome per la posizione della risorsa immagine all&#39;interno della matrice del set 360 gradi 2D.

   Utilizzare le parentesi per includere la posizione della riga o della colonna nel nome del file.

   Ad esempio, per l’espressione regolare di riga, può avere l’aspetto seguente:

   `\w+-R([0-9]+)-\w+`

   oppure

   `\w+-(\d+)-\w+`

   Per l’espressione regolare della colonna, può avere l’aspetto seguente:

   `\w+-\w+-C([0-9]+)`

   oppure

   `\w+-\w+-C(\d+)`

   I campioni di cui sopra sono esclusivamente a scopo dimostrativo. Puoi creare le espressioni regolari in base alle tue esigenze.

   >[!NOTE]
   >
   >Se la combinazione di espressioni regolari di riga e colonna non è in grado di determinare la posizione della risorsa all’interno della matrice multidimensionale del set 360 gradi, la risorsa non viene aggiunta al set. Viene inoltre registrato un errore.

1. Per Imposta convenzione di denominazione e creazione, specificate il suffisso o il prefisso del nome di base definito nella convenzione di denominazione delle risorse.

   Inoltre, definisci dove viene creato il set 360 gradi all’interno della struttura di cartelle di Dynamic Media Classic.

   Se definisci un numero elevato di set, mantieni i set separati dalle cartelle che contengono le risorse stesse. Ad esempio, crea una cartella Set 360 gradi per inserire qui i set generati.

1. Nel pannello Dettagli, seleziona **[!UICONTROL Salva]**.
1. Seleziona **[!UICONTROL Attivo]** accanto al nuovo nome del predefinito.

   L’attivazione del predefinito assicura che, quando si caricano le risorse in Dynamic Medie, venga applicato il predefinito per set di batch per generare il set.

### (Facoltativo) Ottimizzazione delle prestazioni di Dynamic Medie in modalità Scene7 {#optional-tuning-the-performance-of-dynamic-media-scene-mode}

Per garantire un funzionamento ottimale della modalità Dynamic Medie - Scene7, Adobe consiglia i seguenti suggerimenti per l’ottimizzazione delle prestazioni e della scalabilità della sincronizzazione:

* Aggiornamento dei parametri predefiniti del processo per l’elaborazione di diversi formati di file.
* Aggiornamento dei thread di lavoro in coda del flusso di lavoro predefinito di Granite (risorse video).
* Aggiornamento dei thread di lavoro in coda predefiniti per il flusso di lavoro transitorio di Granite (immagini e risorse non video).
* Aggiornamento del numero massimo di connessioni di caricamento al server Dynamic Media Classic.

#### Aggiornare i parametri predefiniti del job per l&#39;elaborazione di diversi formati di file

Puoi regolare i parametri dei processi per velocizzare l’elaborazione quando carichi i file. Ad esempio, se caricate i file PSD ma non desiderate elaborarli come modelli, potete impostare l&#39;estrazione del livello su false (off). In questo caso, il parametro del processo ottimizzato viene visualizzato come segue: `process=None&createTemplate=false`.

Se si desidera attivare la creazione del modello, utilizzare i seguenti parametri: `process=MaintainLayers&layerNaming=AppendName&createTemplate=true`.

<!-- THIS PARAGRAPH WAS REPLACED WITH THE TWO PARAGRAPHS DIRECTLY ABOVE BASED ON CQDOC-17657 You can tune job parameters for faster processing when you upload files. For example, if you are uploading PSD files, but do not want to process them as templates, you can set layer extraction to false (off). In such case, the tuned job parameter would appear as `process=None&createTemplate=false`. -->

L’Adobe consiglia di utilizzare i seguenti parametri di processo &quot;ottimizzati&quot; per i file PDF, PostScript® e PSD:

<!-- OLD PDF JOB PARAMETERS `pdfprocess=Rasterize&resolution=150&colorspace=Auto&pdfbrochure=false&keywords=false&links=false` -->

<!-- OLD POSTSCRIPT JOB PARAMETERS `psprocess=Rasterize&psresolution=150&pscolorspace=Auto&psalpha=false&psextractsearchwords=false&aiprocess=Rasterize&airesolution=150&aicolorspace=Auto&aialpha=false` -->

| Tipo di file | Parametri di processo consigliati |
| ---| ---|
| PDF | `pdfprocess=Thumbnail&resolution=150&colorspace=Auto&pdfbrochure=false&keywords=false&links=false` |
| PostScript® | `psprocess=Rasterize&psresolution=150&pscolorspace=Auto&psalpha=false&psextractsearchwords=false&aiprocess=Thumbnail&airesolution=150&aicolorspace=Auto&aialpha=false` |
| PSD | `process=None&layerNaming=AppendName&anchor=Center&createTemplate=false&extractText=false&extendLayers=false` |

<!-- CQDOC-17657 for PSD entry in table above -->

Per aggiornare uno di questi parametri, seguire i passaggi descritti in [Abilitazione del supporto dei parametri del processo di caricamento Assets/Dynamic Media Classic basato sul tipo MIME](/help/sites-administering/scene7.md#enabling-mime-type-based-assets-scene-upload-job-parameter-support).

#### Aggiornare la coda del flusso di lavoro transitorio di Granite {#updating-the-granite-transient-workflow-queue}

La coda del flusso di lavoro di transito Granite è utilizzata per il flusso di lavoro **[!UICONTROL Risorsa di aggiornamento DAM]**. In Dynamic Medie, viene utilizzato per l’acquisizione e l’elaborazione delle immagini.

**Per aggiornare la coda del flusso di lavoro transitorio Granite:**

1. Passa a [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr) e cerca **Coda: coda flussi di lavoro transitori Granite**.

   >[!NOTE]
   >
   >È necessaria una ricerca di testo invece di un URL diretto, perché il PID OSGi viene generato in modo dinamico.

1. Nel campo **[!UICONTROL Maximum Parallel Jobs]** (Numero massimo processi paralleli), modifica il numero impostando il valore desiderato.

   Puoi aumentare il numero massimo di **[!UICONTROL processi paralleli]** per supportare adeguatamente il caricamento di file in Dynamic Medie. Il valore esatto dipende dalla capacità hardware. In alcuni scenari, ovvero una migrazione iniziale o un caricamento in blocco una tantum, puoi utilizzare un valore elevato. Tuttavia, l’utilizzo di un valore elevato (ad esempio due volte il numero di core) può avere effetti negativi su altre attività simultanee. In questo modo, testa e regola il valore in base al tuo caso d’uso particolare.

<!--    By default, the maximum number of parallel jobs depends on the number of available CPU cores. For example, on a 4-core server, it assigns 2 worker threads. (A value between 0.0&ndash;1.0 is ratio based, or any numbers greater than 1 will assign the number of worker threads.)

   Adobe recommends that 32 **[!UICONTROL Maximum Parallel Jobs]** be configured to adequately support heavy upload of files to Dynamic Media Classic (Scene7). -->

![chlimage_1](assets/chlimage_1.jpeg)

1. Seleziona **[!UICONTROL Salva]**.

#### Aggiornare la coda del flusso di lavoro Granite {#updating-the-granite-workflow-queue}

La coda del flusso di lavoro Granite viene utilizzata per flussi di lavoro non transitori. In Dynamic Medie, utilizzava per elaborare video con il flusso di lavoro **[!UICONTROL Codifica video Dynamic Medie]**.

**Per aggiornare la coda del flusso di lavoro Granite:**

1. Passare a `https://<server>/system/console/configMgr` e cercare **Coda: coda flusso di lavoro Granite**.

   >[!NOTE]
   >
   >È necessaria una ricerca di testo invece di un URL diretto, perché il PID OSGi viene generato in modo dinamico.

1. Nel campo **[!UICONTROL Maximum Parallel Jobs]** (Numero massimo processi paralleli), modifica il numero impostando il valore desiderato.

   Puoi aumentare il numero massimo di processi paralleli per supportare in modo adeguato il caricamento di file su Dynamic Medie. Il valore esatto dipende dalla capacità hardware. In alcuni scenari, ovvero una migrazione iniziale o un caricamento in blocco una tantum, puoi utilizzare un valore elevato. Tuttavia, l’utilizzo di un valore elevato (ad esempio due volte il numero di core) può avere effetti negativi su altre attività simultanee. In questo modo, testa e regola il valore in base al tuo caso d’uso particolare.

   ![chlimage_1-1](assets/chlimage_1-1.jpeg)

1. Seleziona **[!UICONTROL Salva]**.

#### Aggiornare la connessione di caricamento Dynamic Media Classic {#updating-the-scene-upload-connection}

L’impostazione Scene7 Upload Connection sincronizza le risorse Experience Manager con i server Dynamic Media Classic.

**Per aggiornare la connessione di caricamento Dynamic Media Classic:**

1. Passa a `https://<server>/system/console/configMgr/com.day.cq.dam.scene7.impl.Scene7UploadServiceImpl`
1. Nel campo **[!UICONTROL Numero di connessioni]** e/o nel campo **[!UICONTROL Timeout processo attivo]**, modificare il numero come desiderato.

   L&#39;impostazione **[!UICONTROL Numero di connessioni]** controlla il numero massimo di connessioni HTTP consentite, ad Experience Manager il caricamento di Dynamic Medie. In genere, il valore predefinito di dieci connessioni è sufficiente.

   L&#39;impostazione **[!UICONTROL Timeout processo attivo]** determina il tempo di attesa per la pubblicazione delle risorse Dynamic Medie caricate nel server di consegna. Questo valore è 2100 secondi (35 minuti) per impostazione predefinita.

   Per la maggior parte dei casi d’uso è sufficiente impostare 2100.

   ![chlimage_1-2](assets/chlimage_1-2.jpeg)

1. Seleziona **[!UICONTROL Salva]**.

### (Facoltativo) Filtrare le risorse per la replica {#optional-filtering-assets-for-replication}

Nelle distribuzioni non Dynamic Medie, replichi *tutte* le risorse (sia immagini che video) dall&#39;ambiente di authoring Experience Manager al nodo Publish Experience Manager. Questo flusso di lavoro è necessario perché anche i server Publish di Experience Manager distribuiscono le risorse.

Tuttavia, nelle implementazioni di Dynamic Medie, poiché le risorse vengono distribuite tramite il Cloud Service, non è necessario replicarle sui nodi di pubblicazione Experience Manager. Questo flusso di lavoro di &quot;pubblicazione ibrida&quot; evita costi di storage aggiuntivi e tempi di elaborazione più lunghi per la replica delle risorse. Altri contenuti, come le pagine del sito, continuano a essere distribuiti dai nodi di pubblicazione dell’Experience Manager.

I filtri consentono di *escludere* risorse dalla replica nel nodo di pubblicazione Experience Manager.

#### Utilizzare i filtri delle risorse predefiniti per la replica {#using-default-asset-filters-for-replication}

Se utilizzi Dynamic Medie per l’imaging, il video o entrambi, puoi utilizzare i filtri predefiniti che Adobe fornisce così come sono. I seguenti filtri sono attivi per impostazione predefinita:

|   | Filtro | Tipo MIME | Rappresentazioni |
| --- | --- | --- | --- |
| Consegna immagini Dynamic Medie | filter-image<br>filter-sets | Inizia con **image/**<br> Contiene **applications/** e termina con **set**. | Le impostazioni predefinite &quot;filter-images&quot; (valide per le singole immagini, incluse le immagini interattive) e &quot;filter-sets&quot; (valide per i set 360 gradi, i set di immagini, i set di file multimediali diversi e i set carosello):<br>· Escludono dalla replica le rappresentazioni dell&#39;immagine originale e dell&#39;immagine statica. |
| Consegna video Dynamic Medie | filter-video | Inizia con **video/** | Il &quot;video filtro&quot; predefinito:<br>· Esclude dalla replica il video originale e le rappresentazioni di miniature statiche. |

>[!NOTE]
>
>I filtri si applicano ai tipi MIME e non possono essere specifici del percorso.

#### Personalizzare i filtri delle risorse per la replica {#customizing-asset-filters-for-replication}

1. In Experience Manager, seleziona il logo di Experience Manager per accedere alla console di navigazione globale e passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Generale]** > **[!UICONTROL CRXDE Liti]**.
1. Nella struttura di cartelle a sinistra, passa a `/etc/replication/agents.author/publish/jcr:content/damRenditionFilters` per rivedere i filtri.

   ![chlimage_1-17](assets/chlimage_1-2.png)

1. Per definire il tipo MIME per il filtro, puoi individuare il tipo MIME nel modo seguente:

   Nella barra a sinistra, espandi `content > dam > <locate_your_asset> > jcr:content > metadata`, quindi nella tabella individua `dc:format`.

   L&#39;immagine seguente è un esempio del percorso di una risorsa per `dc:format`.

   ![chlimage_1-18](assets/chlimage_1-3.png)

   Si noti che `dc:format` per la risorsa `Fiji Red.jpg` è `image/jpeg`.

   Per applicare questo filtro a tutte le immagini, indipendentemente dal formato, impostare il valore su `image/*`, dove `*` è un&#39;espressione regolare applicata a tutte le immagini di qualsiasi formato.

   Per applicare il filtro solo alle immagini di tipo JPEG, immettere il valore `image/jpeg`.

1. Definisci quali rappresentazioni includere o escludere dalla replica.

   I caratteri che puoi utilizzare per filtrare la replica includono:

   | Carattere da utilizzare | Filtrare le risorse per la replica |
   | --- | --- |
   | * | Carattere jolly |
   | + | Include le risorse per la replica |
   | - | Esclusione di risorse dalla replica |

   Accedi a `content/dam/<locate your asset>/jcr:content/renditions`.

   L’immagine seguente è un esempio delle rappresentazioni di una risorsa.

   ![chlimage_1-4](assets/chlimage_1-4.png)

   Se si desidera replicare solo l&#39;originale, immettere `+original`.
