---
title: OPZIONE A - Configura Dynamic Media - Modalità Scene7
description: Scopri come configurare la modalità Dynamic Media - Scene7.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
docset: aem65
role: User, Admin
mini-toc-levels: 3
hide: true
hidefromtoc: true
feature: Configuration,Scene7 Mode
exl-id: null
source-git-commit: bfa41deb156ffd0adb8138c11548912bc954f084
workflow-type: tm+mt
source-wordcount: '11558'
ht-degree: 3%

---

# OPZIONE A - Configura Dynamic Media - Modalità Scene7{#configuring-dynamic-media-scene-mode}

>[!NOTE]
>
>OPZIONE A - I DUE NUOVI ARGOMENTI CHE HO SCRITTO VENGONO ELIMINATI. MA PRIMA DI ELIMINARE GLI ARGOMENTI, TUTTI I LORO CONTENUTI SONO STATI TRASFERITI IN QUESTO ARGOMENTO, NELLE RISPETTIVE AREE IN CUI HO GIÀ PARLATO DI IMPOSTAZIONI GENERALI E CONFIGURAZIONE PUBBLICAZIONE.

Se utilizzi l’impostazione Adobe Experience Manager per ambienti diversi, ad esempio sviluppo, staging e produzione, configura Cloud Services Dynamic Media per ciascuno di tali ambienti.

## Diagramma dell&#39;architettura di Dynamic Media - Modalità Scene7 {#architecture-diagram-of-dynamic-media-scene-mode}

**RICK: MANTIENI COSÌ COME È**

Il diagramma dell&#39;architettura seguente descrive il funzionamento della modalità Dynamic Media - Scene7.

Con la nuova architettura, Experience Manager è responsabile delle risorse di origine primaria e delle sincronizzazioni con Dynamic Media per l’elaborazione e la pubblicazione delle risorse:

1. Quando la risorsa di origine principale viene caricata in Experience Manager, viene replicata in Dynamic Media. A questo punto, Dynamic Media gestisce l’elaborazione e la generazione di rendering delle risorse, ad esempio la codifica video e le varianti dinamiche di un’immagine.
(In modalità Dynamic Media - Scene7, la dimensione predefinita del file di caricamento è inferiore o uguale a 2 GB. Per abilitare le dimensioni dei file di caricamento da 2 GB fino a 15 GB, vedi [(Facoltativo) Configura Dynamic Media - Modalità Scene7 per il caricamento di risorse superiori a 2 GB](#optional-config-dms7-assets-larger-than-2gb).)
1. Dopo la generazione dei rendering, Experience Manager può accedere in modo sicuro e visualizzare in anteprima i rendering Dynamic Media remoti (nessun file binario viene inviato nuovamente all’istanza di Experience Manager).
1. Quando il contenuto è pronto per essere pubblicato e approvato, attiva il servizio Dynamic Media per inviare contenuti ai server di consegna e memorizzare in cache il contenuto nella rete CDN (Content Delivery Network).

![chlimage_1-550](assets/chlimage_1-550.png)

>[!IMPORTANT]
>
>Il seguente elenco di funzioni richiede l’utilizzo della rete CDN preconfigurata fornita con Adobe Experience Manager - Dynamic Media. Qualsiasi altra rete CDN personalizzata non è supportata con queste funzioni.
>
>* [Imaging avanzato](/help/assets/imaging-faq.md)
>* [Annullamento della validità della cache](/help/assets/invalidate-cdn-cache-dynamic-media.md)
>* [Protezione del collegamento ipertestuale](/help/assets/hotlink-protection.md)
>* [Distribuzione HTTP/2 dei contenuti](/help/assets/http2.md)
>* Reindirizzamento URL a livello CDN
>* Akamai ChinaCDN (per una consegna ottimale in Cina)


## Abilitare Dynamic Media in modalità Scene7 {#enabling-dynamic-media-in-scene-mode}

**RICK: MANTIENI COSÌ COME È**

[Dynamic Media è disattivato per impostazione predefinita. ](https://business.adobe.com/products/experience-manager/assets/dynamic-media.html) Per sfruttare le funzionalità di Dynamic Media, è necessario abilitarle.

>[!WARNING]
>
>Dynamic Media - La modalità Scene7 è per *Solo istanza di authoring di Experience Manager*. Di conseguenza, devi configurare `runmode=dynamicmedia_scene7` sull’istanza di authoring di Experience Manager, *not* l’istanza Publish di Experience Manager.

Per abilitare Dynamic Media, è necessario avviare Experience Manager utilizzando `dynamicmedia_scene7` modalità di esecuzione dalla riga di comando immettendo quanto segue in una finestra terminale (la porta di esempio utilizzata è 4502):

```shell
java -Xms4096m -Xmx4096m -Doak.queryLimitInMemory=500000 -Doak.queryLimitReads=500000 -jar cq-quickstart-6.5.0.jar -gui -r author,dynamicmedia_scene7 -p 4502
```

## (Facoltativo) Migrazione di predefiniti e configurazioni Dynamic Media da 6.3 a 6.5 Zero Downtime {#optional-migrating-dynamic-media-presets-and-configurations-from-to-zero-downtime}

**RICK: MANTIENI COSÌ COME È**

L’aggiornamento di Experience Manager Dynamic Media dalla versione 6.3 alla versione 6.4 o 6.5 ora include la possibilità di eseguire installazioni senza tempi di inattività. Per migrare tutti i predefiniti e le configurazioni da `/etc` a `/conf` in CRXDE Lite, assicurati di eseguire il seguente comando curl.

>[!NOTE]
>
>Se esegui l’istanza di Experience Manager in modalità di compatibilità, ovvero se hai installato il pacchetto di compatibilità, non è necessario eseguire questi comandi.

Per tutti gli aggiornamenti, sia con che senza il pacchetto di compatibilità, puoi copiare i predefiniti predefiniti predefiniti per visualizzatori forniti originariamente con Dynamic Media eseguendo il seguente comando curl Linux®:

`curl -u admin:admin -X POST https://<server_address>:<server_port>/libs/settings/dam/dm/presets/viewer.pushviewerpresets.json`

Per migrare eventuali predefiniti e configurazioni di visualizzatore personalizzati creati da `/etc` a `/conf`, esegui il seguente comando curl Linux®:

`curl -u admin:admin -X POST https://<server_address>:<server_port>/libs/settings/dam/dm/presets.migratedmcontent.json`

## Installa feature pack 18912 per la migrazione di massa delle risorse {#installing-feature-pack-for-bulk-asset-migration}

**RICK: MANTIENI COSÌ COME È**

L&#39;installazione del feature pack 18912 è *facoltativo*.

Il Feature Pack 18912 consente di caricare in massa le risorse tramite FTP oppure di migrare, ad Experience Manager, le risorse da Dynamic Media - Modalità ibrida o Dynamic Media Classic in modalità Dynamic Media - Scene7. È disponibile da [Adobe Professional Services](https://business.adobe.com/customers/consulting-services/main.html).

Vedi [Installa feature pack 18912 per la migrazione di massa delle risorse](/help/assets/bulk-ingest-migrate.md) per ulteriori informazioni.

## Creare una configurazione Dynamic Media nei Cloud Services {#configuring-dynamic-media-cloud-services}

**RICK: MANTIENI COSÌ COME È**

**Prima di configurare Dynamic Media** - Dopo aver ricevuto l&#39;e-mail di provisioning con le credenziali Dynamic Media, devi aprire la [applicazione desktop Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started), quindi accedi al tuo account per modificare la tua password. La password fornita nell&#39;e-mail di provisioning è generata dal sistema e destinata solo a essere una password temporanea. È importante aggiornare la password in modo che il Cloud Service Dynamic Media sia configurato con le credenziali corrette.

![dynamic icmediaconfiguration2update](assets/dynamicmediaconfiguration2updated.png)

**Per creare una configurazione Dynamic Media nei Cloud Services:**

1. In modalità Creazione Experience Manager, seleziona il logo Experience Manager per accedere alla console di navigazione globale, quindi seleziona l’icona Strumenti , quindi vai a **[!UICONTROL Cloud Services]** > **[!UICONTROL Configurazione Dynamic Media]**.
1. Nella pagina Browser configurazione Dynamic Media, seleziona nel riquadro a sinistra **[!UICONTROL globale]** (non selezionare l’icona della cartella a sinistra di **[!UICONTROL globale]**), quindi seleziona **[!UICONTROL Crea]**.
1. Sulla **[!UICONTROL Crea configurazione Dynamic Media]** , inserisci un titolo, l&#39;indirizzo e-mail dell&#39;account Dynamic Media, la password, quindi seleziona la tua area geografica. Queste informazioni vengono fornite per Adobe nell’e-mail di provisioning. Se non hai ricevuto l’e-mail, contatta l’Assistenza clienti di Adobe.

   Seleziona **[!UICONTROL Connessione a Dynamic Media]**.

   >[!NOTE]
   **RICK: MANTENETE COSÌ?** Dopo aver ricevuto l’e-mail di provisioning con le credenziali Dynamic Media, apri la [applicazione desktop Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started), quindi accedi al tuo account per modificare la tua password. La password fornita nell&#39;e-mail di provisioning è generata dal sistema e destinata solo a essere una password temporanea. È importante aggiornare la password in modo che il Cloud Service Dynamic Media sia configurato con le credenziali corrette.

1. Quando la connessione ha esito positivo, imposta quanto segue. Le intestazioni con asterisco (*) sono obbligatorie:

   * **[!UICONTROL Azienda]** - il nome dell&#39;account Dynamic Media. Hai più account Dynamic Media. Ad esempio, puoi avere diversi marchi secondari, divisioni, staging o ambienti di produzione.

   * **[!UICONTROL Percorso cartella principale della società]**

   * **[!UICONTROL Pubblicazione delle risorse]** - È possibile scegliere tra le tre opzioni seguenti:
      * **[!UICONTROL Immediatamente]** significa che quando le risorse vengono caricate, il sistema le acquisisce e fornisce l’URL/da incorporare immediatamente. Non è necessario alcun intervento degli utenti per pubblicare le risorse.
      * **[!UICONTROL All&#39;attivazione]** significa che devi pubblicare esplicitamente la risorsa prima prima di fornire un collegamento URL/Incorpora .<br><!-- CQDOC-17478, Added March 9, 2021-->A partire da Experience Manager 6.5.8, l&#39;istanza Publish di Experience Manager riflette valori di metadati precisi di Dynamic Media, come `dam:scene7Domain` e `dam:scene7FileStatus` in **[!UICONTROL All&#39;attivazione]** solo modalità di pubblicazione. Per abilitare questa funzionalità, installare Service Pack 8, quindi riavviare Experience Manager. Vai a Gestione configurazione Sling. Trova la configurazione per `Scene7ActivationJobConsumer Component` o creane uno nuovo). Seleziona la casella di controllo **[!UICONTROL Replicare i metadati dopo la pubblicazione di Dynamic Media]**, quindi seleziona **[!UICONTROL Salva]**.

         ![Casella di controllo Replica metadati dopo la pubblicazione di Dynamic Media](assets-dm/replicate-metadata-setting.png)

      * **[!UICONTROL Pubblicazione selettiva]** Questa opzione consente di controllare quali cartelle vengono pubblicate in Dynamic Media. Consente di utilizzare funzioni quali Ritaglio avanzato o rappresentazioni dinamiche, oppure di determinare quali cartelle vengono pubblicate esclusivamente in Experience Manager per la visualizzazione dell’anteprima. Le stesse risorse *not* pubblicato in Dynamic Media per la distribuzione nel dominio pubblico.<br>Puoi impostare questa opzione qui nel **[!UICONTROL Configurazione Dynamic Media Cloud]** oppure, se si preferisce, è possibile scegliere di impostare questa opzione a livello di cartella, in una cartella **[!UICONTROL Proprietà]**.<br>Vedi [Utilizzo della pubblicazione selettiva in Dynamic Media](/help/assets/selective-publishing.md).<br>Se successivamente modifichi questa configurazione o la modifichi a livello di cartella, queste modifiche interessano solo le nuove risorse caricate da quel momento in poi. Lo stato di pubblicazione delle risorse esistenti nella cartella rimane invariato finché non le cambi manualmente da **[!UICONTROL Pubblicazione rapida]** o **[!UICONTROL Gestisci pubblicazione]** finestra di dialogo.
   * **[!UICONTROL Server di anteprima protetto]** - consente di specificare il percorso URL del server di anteprima delle rappresentazioni protette. In altre parole, dopo la generazione delle rappresentazioni, Experience Manager può accedere in modo sicuro e visualizzare in anteprima le rappresentazioni Dynamic Media remote (nessun file binario viene inviato nuovamente all’istanza di Experience Manager).
A meno che non si disponga di una disposizione speciale per utilizzare il server della propria azienda o un server speciale, Adobe consiglia di lasciare questa impostazione come specificato.

   * **[!UICONTROL Sincronizza tutti i contenuti]** - <!-- NEW OPTION, CQDOC-15371, Added March 4, 2020-->Selezionato per impostazione predefinita. Deseleziona questa opzione se desideri includere o escludere in modo selettivo le risorse dalla sincronizzazione con Dynamic Media. Deselezionando questa opzione puoi scegliere tra le due seguenti modalità di sincronizzazione Dynamic Media:

   * **[!UICONTROL Modalità di sincronizzazione elementi Dynamic Media]**
      * **[!UICONTROL Abilitato per impostazione predefinita]** - La configurazione viene applicata a tutte le cartelle per impostazione predefinita, a meno che non si contrassegni una cartella specifica per l&#39;esclusione. <!-- you can then deselect the folders that you do not want the configuration applied to.-->
      * **[!UICONTROL Disabilitata per impostazione predefinita]** - La configurazione non viene applicata ad alcuna cartella finché non si contrassegna esplicitamente una cartella selezionata per la sincronizzazione con Dynamic Media.
Per contrassegnare una cartella selezionata per la sincronizzazione con Dynamic Media, seleziona una cartella di risorse, quindi seleziona sulla barra degli strumenti **[!UICONTROL Proprietà]**. Sulla **[!UICONTROL Dettagli]** nella scheda **[!UICONTROL Modalità di sincronizzazione Dynamic Media]** dall’elenco a discesa, scegli una delle tre opzioni seguenti. Al termine, seleziona **[!UICONTROL Salva]**. *Ricorda: queste tre opzioni non sono disponibili se selezionate **[!UICONTROL Sincronizza tutti i contenuti]**prima.* Vedi anche [Utilizzo di Pubblicazione selettiva a livello di cartella in Dynamic Media](/help/assets/selective-publishing.md).
         * **[!UICONTROL Ereditato]** - Nessun valore di sincronizzazione esplicito sulla cartella; la cartella eredita invece il valore di sincronizzazione da una delle cartelle precedenti o dalla modalità predefinita nella configurazione cloud. Lo stato dettagliato per le visualizzazioni ereditate viene visualizzato tramite una descrizione comandi.
         * **[!UICONTROL Abilita per sottocartelle]** - Includi tutto ciò che si trova in questa sottostruttura per la sincronizzazione con Dynamic Media. Le impostazioni specifiche per la cartella sostituiscono la modalità predefinita nella configurazione cloud.
         * **[!UICONTROL Disabilitato per le sottocartelle]** - Escludere tutti gli elementi di questo sottoalbero dalla sincronizzazione con Dynamic Media.

   >[!NOTE]
   In DMS7 non è supportato il controllo delle versioni. Inoltre, l’attivazione ritardata si applica solo se l’opzione **[!UICONTROL Pubblica risorse]** della pagina Modifica configurazione Dynamic Media è impostata su **[!UICONTROL All’attivazione]** e soltanto fino alla prima attivazione della risorsa.
   Dopo l’attivazione di una risorsa, tutti gli aggiornamenti vengono immediatamente pubblicati in tempo reale su S7 Delivery.

1. Seleziona **[!UICONTROL Salva]**.
1. Per visualizzare in anteprima in modo sicuro il contenuto Dynamic Media prima della pubblicazione, è necessario &quot;inserire nell&#39;elenco Consentiti&quot; l’istanza di authoring di Experience Manager per connettersi a Dynamic Media:

   * **RICK: ARGOMENTO COLLEGAMENTO A NUOVO ARGOMENTO DI CONFIGURAZIONE PUBBLICAZIONE** Apri [applicazione desktop Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started), quindi accedi al tuo account. Le credenziali e i dettagli di accesso sono stati forniti da Adobe al momento del provisioning. Se non disponi di tali informazioni, contatta l’Assistenza clienti Adobe.

   * Nella barra di navigazione in alto a destra della pagina, individua **[!UICONTROL Configurazione]** > **[!UICONTROL Impostazione applicazione]** > **[!UICONTROL Pubblica installazione]** > **[!UICONTROL Server immagini]**.

   * Nella pagina Pubblica su Image Server, seleziona l’elenco a discesa Contesto pubblicazione **[!UICONTROL Test Image Serving]**.
   * Per Filtro indirizzi client, selezionare **[!UICONTROL Aggiungi]**.
   * Per abilitare (attivare) l’indirizzo, selezionare la casella di controllo. Immetti l’indirizzo IP dell’istanza di authoring di Experience Manager (non dell’IP di Dispatcher).
   * Seleziona **[!UICONTROL Salva]**.

La configurazione di base è terminata. è possibile utilizzare la modalità Dynamic Media - Scene7.

Se desideri personalizzare ulteriormente la configurazione, puoi facoltativamente completare una qualsiasi delle attività in [(Facoltativo) Configurare le impostazioni avanzate in modalità Dynamic Media - Scene7](#optional-configuring-advanced-settings-in-dynamic-media-scene-mode).

## (Facoltativo) Configurare le impostazioni avanzate in modalità Dynamic Media - Scene7 {#optional-configuring-advanced-settings-in-dynamic-media-scene-mode}

**RICK: MANTIENI COSÌ COME È**

Se desideri personalizzare ulteriormente la configurazione e l&#39;impostazione della modalità Dynamic Media - Scene7 o ottimizzarne le prestazioni, puoi completare una o più delle seguenti operazioni *facoltativo* attività:

* [(Facoltativo) Configura Dynamic Media - Modalità Scene7 per il caricamento di risorse superiori a 2 GB](#optional-config-dms7-assets-larger-than-2gb)

* [(Facoltativo) Configurazione e configurazione di Dynamic Media - Impostazioni della modalità Scene7](#optional-setup-and-configuration-of-dynamic-media-scene7-mode-settings)

* [(Facoltativo) Ottimizzare le prestazioni di Dynamic Media - Modalità Scene7](#optional-tuning-the-performance-of-dynamic-media-scene-mode)

* [(Facoltativo) Filtrare le risorse per la replica](#optional-filtering-assets-for-replication)

### (Facoltativo) Configura Dynamic Media - Modalità Scene7 per il caricamento di risorse superiori a 2 GB {#optional-config-dms7-assets-larger-than-2gb}

**RICK: MANTIENI COSÌ COME È**

In modalità Dynamic Media - Scene7, la dimensione predefinita del file di caricamento delle risorse è inferiore o uguale a 2 GB. Tuttavia, puoi anche configurare il caricamento di risorse di dimensioni superiori a 2 GB e fino a 15 GB.

Se desideri utilizzare questa funzione, prendi nota dei seguenti prerequisiti e punti:

* Devi eseguire Experience Manager 6.5 con Service Pack 6.5.4.0 o successivo in modalità Dynamic Media - Scene7.
* Questa grande funzione di caricamento è supportata solo per [*Managed Services*](https://business.adobe.com/products/experience-manager/managed-services.html) clienti.
* Assicurati che l’istanza di Experience Manager sia configurata con l’archiviazione BLOB di Amazon S3 o Microsoft® Azure.

   >[!NOTE]
   Configura l’archiviazione BLOB di Azure con una chiave di accesso e una chiave segreta perché questa funzione di caricamento di grandi dimensioni non è supportata con AzureSas nella configurazione dell’archiviazione BLOB.

* di Oak [Download di accesso binario diretto](https://jackrabbit.apache.org/oak/docs/features/direct-binary-access.html) è abilitato (Oak&#39;s *Caricamento accesso binario diretto* non è richiesto).

   Per abilitare il download Direct Binary Access, imposta la proprietà `presignedHttpDownloadURIExpirySeconds > 0` nella configurazione del datastore. Il valore deve essere sufficientemente lungo per scaricare binari di grandi dimensioni e riprovare.

* Le risorse di dimensioni superiori a 15 GB non vengono caricate. (Il limite di dimensione è impostato nel passaggio 8 seguente.)
* Quando il **[!UICONTROL Rielaborazione Dynamic Media]** il flusso di lavoro risorse viene attivato in una cartella e rielabora tutte le risorse di grandi dimensioni già sincronizzate con l’azienda Dynamic Media. Tuttavia, se una risorsa di grandi dimensioni non è ancora sincronizzata nella cartella, non carica la risorsa. Pertanto, per sincronizzare le risorse grandi esistenti in Dynamic Media, puoi eseguire **[!UICONTROL Rielaborazione Dynamic Media]** flusso di lavoro delle risorse sulle singole risorse.

**Per configurare la modalità Dynamic Media - Scene7 per il caricamento di risorse di dimensioni superiori a 2 GB:**

1. In Experience Manager, seleziona il logo Experience Manager per accedere alla console di navigazione globale, quindi accedi a . **[!UICONTROL Strumenti]** > **[!UICONTROL Generale]** > **[!UICONTROL CRXDE Lite]**.

1. Nella finestra di CRXDE Lite, effettuare una delle seguenti operazioni:

   * Nella barra a sinistra, individua il seguente percorso:

      `/libs/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload`

   * Copia e incolla il percorso sopra nel campo del percorso CRXDE Lite sotto la barra degli strumenti, quindi premi `Enter`.

1. Nella barra a sinistra, fai clic con il pulsante destro del mouse su `fileupload`, quindi dal menu a comparsa, seleziona **[!UICONTROL Nodo di sovrapposizione]**.

   ![Opzione Sovrapponi nodo](/help/assets/assets-dm/uploadassets15gb_a.png)

1. Nella finestra di dialogo Sovrapponi nodo selezionare il **[!UICONTROL Tipi di nodo corrispondenti]** casella di controllo per attivare (attivare) l&#39;opzione, quindi selezionare **[!UICONTROL OK]**.

   ![Finestra di dialogo Sovrapponi nodo](/help/assets/assets-dm/uploadassets15gb_b.png)

1. Dalla finestra di CRXDE Lite, effettuare una delle seguenti operazioni:

   * Nella barra a sinistra, individua il seguente percorso del nodo di sovrapposizione:

      `/apps/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload`

   * Copia e incolla il percorso sopra nel campo del percorso CRXDE Lite sotto la barra degli strumenti, quindi premi `Enter`.

1. In **[!UICONTROL Proprietà]** nella scheda **[!UICONTROL Nome]** colonna, individuare `sizeLimit`.
1. A destra del `sizeLimit` nome, sotto **[!UICONTROL Valore]** fare doppio clic sul campo del valore.
1. Immetti il valore appropriato in byte in modo da poter aumentare il limite di dimensione alla dimensione massima desiderata per il caricamento. Ad esempio, per aumentare il limite di dimensione della risorsa da caricare a 10 GB, immetti `10737418240` nel campo value.
Puoi immettere un valore fino a 15 GB (`2013265920` byte). In questo caso, le risorse caricate di dimensioni superiori a 15 GB non vengono caricate.


   ![Valore limite dimensione](/help/assets/assets-dm/uploadassets15gb_c.png)

1. Nell’angolo in alto a sinistra della finestra di CRXDE Lite, seleziona **[!UICONTROL Salva tutto]**.

   *Ora imposta il timeout per il gestore processi esterni del flusso di lavoro di Adobe Granite eseguendo le operazioni seguenti:*

1. In Experience Manager, seleziona il logo Experience Manager per accedere alla console di navigazione globale.
1. Effettua una delle seguenti operazioni:

   * Passa al seguente percorso URL:

      `localhost:4502/system/console/configMgr/com.adobe.granite.workflow.core.job.ExternalProcessJobHandler`

   * Copia e incolla il percorso sopra nel campo URL del browser. Assicurati di sostituire `localhost:4502` con la tua istanza di Experience Manager.

1. In **[!UICONTROL Adobe Granite Workflow External Process Job Handler]** nella finestra di dialogo **[!UICONTROL Timeout massimo]** imposta il valore su `18000` minuti (cinque ore). Il valore predefinito è 10800 minuti (tre ore).

   ![Valore massimo timeout](/help/assets/assets-dm/uploadassets15gb_d.png)

1. Nell’angolo inferiore destro della finestra di dialogo, seleziona **[!UICONTROL Salva]**.

   *Ora imposta il timeout per il passaggio del processo di caricamento binario diretto di Scene7 facendo quanto segue:*

1. In Experience Manager, seleziona il logo Experience Manager per accedere alla console di navigazione globale.
1. Passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Flusso di lavoro]** > **[!UICONTROL Modelli]**.
1. Nella pagina Modelli di flusso di lavoro , seleziona **[!UICONTROL Codifica video Dynamic Media]**.
1. Sulla barra degli strumenti, seleziona **[!UICONTROL Modifica]**.
1. Nella pagina del flusso di lavoro, fai doppio clic sul pulsante **[!UICONTROL Caricamento binario diretto Scene7]** fase del processo.
1. In **[!UICONTROL Proprietà passaggio]** nella finestra di dialogo **[!UICONTROL Comune]** nella scheda **[!UICONTROL Impostazioni avanzate]** a) **[!UICONTROL Timeout]** immettere un valore di `18000` minuti (cinque ore). Il valore predefinito è `3600` minuti (un&#39;ora).
1. Seleziona **[!UICONTROL OK]**.
1. Seleziona **[!UICONTROL Sincronizzazione]**.
1. Ripeti i passaggi 14-21 per il **[!UICONTROL Risorsa di aggiornamento DAM]** modello di flusso di lavoro e **[!UICONTROL Rielaborazione Dynamic Media]** modello di flusso di lavoro.

### (Facoltativo) Configura l&#39;installazione di Dynamic Media Publish {#optional-setup-and-configuration-of-dynamic-media-scene7-mode-settings}

**RICK: TUTTO IL CONTENUTO DALL’ARGOMENTO CONFIGURAZIONE NUOVA PUBBLICAZIONE AGGIUNTO QUI**

>[!IMPORTANT]
Dynamic Media Publish Setup è disponibile solo se:
* Stai eseguendo Dynamic Media in modalità Scene7.
* Hai un *esistente* **[!UICONTROL Configurazione Dynamic Media]** in **[!UICONTROL Cloud Services]**) in Adobe Experience Manager 6.5 o in Experience Manager as a Cloud Service.
* Sei un amministratore di sistema di Experience Manager con privilegi di amministratore.


Le impostazioni della pagina Configurazione pubblicazione di Dynamic Media determinano il modo in cui le risorse vengono distribuite per impostazione predefinita dai server Dynamic Media di Adobe ai siti web o alle applicazioni. Se non viene specificata alcuna impostazione, il server Dynamic Media di Adobe distribuisce una risorsa in base a un’impostazione predefinita in una pagina Configurazione pubblicazione. Ad esempio, una richiesta di consegna di un’immagine che non include un attributo di risoluzione genera un’immagine con l’impostazione Risoluzione oggetti predefinita nella pagina Image Server.

Gli amministratori possono modificare le impostazioni predefinite nelle pagine Image Server, Image Renderer e Vignette per stabilire le impostazioni predefinite per la distribuzione delle risorse dai server.

>[!NOTE]
Dynamic Media Publish Setup è destinato all&#39;utilizzo da parte di sviluppatori e programmatori di siti web esperti. L’Adobe consiglia agli utenti che modificano una qualsiasi di queste impostazioni di pubblicazione predefinite di avere familiarità con Dynamic Media Adobe, gli standard e le convenzioni del protocollo HTTP e la tecnologia di imaging di base.

**Per configurare Dynamic Media Publish Setup:**

1. In modalità Creazione Experience Manager, seleziona il logo Experience Manager per accedere alla console di navigazione globale.
1. Nella barra a sinistra, seleziona l’icona Strumenti , quindi vai a **[!UICONTROL Risorse]** > **[!UICONTROL Installazione di Dynamic Media Publish]**.
1. Nella pagina Image Server , imposta il contesto Image Server - Publish e quindi utilizza le cinque schede per configurare le impostazioni di pubblicazione predefinite.

   * [Server immagini](#image-server)
   * [Sicurezza](#security-tab) scheda
   * [Gestione catalogo](#catalog-management-tab) scheda
   * [Attributi della richiesta](#request-attributes-tab) scheda
   * [Attributi comuni delle miniature](#common-thumbnail-attributes-tab) scheda
   * [Attributi di gestione del colore](#color-management-attributes-tab) scheda

   ![Pagina di installazione di Dynamic Media Publish](/help/assets/assets-dm/dm-publish-setup.png)
   *Pagina di installazione di Dynamic Media Publish, con **[!UICONTROL Attributi della richiesta]**scheda selezionata.*<br><br>

1. Al termine, seleziona **[!UICONTROL Salva]**.

#### Server immagini {#image-server}

La pagina Image Server stabilisce le impostazioni predefinite per la distribuzione delle immagini dai server di immagini. Le impostazioni sono disponibili in cinque categorie

| Contesto di pubblicazione | Descrizione |
| --- | --- |
| Image Server | Specifica il contesto per le impostazioni di pubblicazione. |
| Image Server test | Specifica il contesto in cui verificare le impostazioni di pubblicazione.<br>Vedi [Verificare le risorse prima di renderle pubbliche](#test-assets-before-making-public). |

#### Scheda Sicurezza {#security-tab}

**[!UICONTROL Indirizzo client]** - Consente di specificare uno o più indirizzi IP o intervalli di indirizzi IP. Se specificato, le richieste a questo catalogo immagini provenienti da un client con un indirizzo IP non elencato vengono rifiutate. Questa regola si applica sia alla distribuzione di immagini che di immagini renderizzate.

#### Scheda Gestione catalogo {#catalog-management-tab}

**[!UICONTROL Percorso del file di definizione del set di regole]** - Specifica il file che contiene le definizioni dei set di regole per il catalogo immagini.

Vedi anche [RuleSetFile](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-rulesetfile.html) nella Guida di riferimento visualizzatori di Dynamic Media.

#### Scheda Attributi richiesta {#request-attributes-tab}

Queste impostazioni riguardano l&#39;aspetto predefinito delle immagini.

| Impostazione | Descrizione |
| --- | --- |
| **[!UICONTROL Limite dimensioni immagine di risposta]** | Obbligatorio.<br>Specifica la larghezza e l&#39;altezza massime dell&#39;immagine di risposta restituite al client. Il server restituisce un errore se una richiesta causa un&#39;immagine di risposta la cui larghezza, altezza o entrambi sono maggiori di questa impostazione.<br>Vedi anche [MaxPix](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-maxpix.html) nella Guida di riferimento visualizzatori di Dynamic Media. |
| **[!UICONTROL Modalità di offuscamento richiesta]** | Abilita questa opzione se desideri applicare la codifica base64 alle richieste valide.<br>Vedi anche [RequestObfuscation](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-requestobfuscation.html) nella Guida di riferimento visualizzatori di Dynamic Media. |
| **[!UICONTROL Modalità di blocco richieste]** | Abilita se desideri un semplice blocco hash incluso nelle richieste.<br>Vedi anche [RequestLock](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-requestlock.html) nella Guida di riferimento visualizzatori di Dynamic Media. |
| **[!UICONTROL Attributi richiesta predefiniti]** |  |
| **[!UICONTROL Suffisso file immagine predefinito]** | Obbligatorio.<br>Estensione predefinita del file di dati aggiunta ai valori dei campi Percorso e MaskPath del catalogo se il percorso non include un suffisso di file.<br>Vedi anche [DefaultExt](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultext.html) nella Guida di riferimento visualizzatori di Dynamic Media. |
| **[!UICONTROL Nome tipo di font predefinito]** | Specifica quale font viene utilizzato se una richiesta di livello di testo non fornisce alcun font. Se specificato, deve essere un valore valido per il nome del font nella mappa dei font di questo catalogo di immagini o nella mappa dei font del catalogo predefinito.<br>Vedi anche [DefaultFont](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultfont.html) nella Guida di riferimento visualizzatori di Dynamic Media. |
| **[!UICONTROL Immagine predefinita]** | Fornisce un&#39;immagine predefinita da restituire in risposta a una richiesta in cui l&#39;immagine richiesta non viene trovata.<br>Vedi anche [DefaultImage](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-is-cat-defaultimage.html) nella Guida di riferimento visualizzatori di Dynamic Media. |
| **[!UICONTROL Modalità immagine predefinita]** | Quando la casella di scorrimento è attivata (cursore a destra), la **[!UICONTROL Immagine predefinita]** sostituisce ogni livello mancante nell&#39;immagine sorgente con l&#39;immagine predefinita e restituisce il composito come di consueto. Quando la casella di scorrimento è disattivata (cursore a sinistra), l&#39;immagine predefinita sostituisce l&#39;intera immagine composita, anche se l&#39;immagine mancante è solo uno dei vari livelli.<br>Vedi anche [DefaultImageMode](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultimagemode.html) nella Guida di riferimento visualizzatori di Dynamic Media. |
| **[!UICONTROL Dimensioni vista predefinite]** | Obbligatorio.<br>Il server vincola le immagini di risposta a non superare questa larghezza e altezza, se la richiesta non specifica esplicitamente la dimensione di visualizzazione utilizzando `wid=`, `hei=`oppure `scl=`.<br>Vedi anche [DefaultPix](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultpix.html) nella Guida di riferimento visualizzatori di Dynamic Media. |
| **[!UICONTROL Dimensioni miniatura predefinite]** | Obbligatorio.<br>Utilizzato al posto dell&#39;attributo **[!UICONTROL Dimensione predefinita della visualizzazione]** per le richieste miniature (`req=tmb`). Il server vincola le immagini di risposta a una dimensione non superiore a questa larghezza e altezza, se viene richiesta una miniatura (`req=tmb`) non specifica esplicitamente la dimensione utilizzando `wid=`, `hei=`oppure `scl=`.<br>Vedi anche [DefaultThumbPix](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultthumbpix.html) nella Guida di riferimento visualizzatori di Dynamic Media. |
| **[!UICONTROL Colore di sfondo predefinito]** | Specifica il valore RGB utilizzato per compilare un&#39;area qualsiasi di un&#39;immagine di risposta che non contiene dati immagine effettivi.<br>Vedi anche [BkgColor](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-bkgcolor.html) nella Guida di riferimento visualizzatori di Dynamic Media. |
| **[!UICONTROL Attributi di codifica JPEG]** |  |
| **[!UICONTROL Qualità]** | Specifica gli attributi predefiniti per le immagini di risposta di JPEG. La **[!UICONTROL Qualità]** Il campo è definito nell&#39;intervallo da 1 a 100.<br>Vedi anche [JpegQuality](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-jpegquality.html) nella Guida di riferimento visualizzatori di Dynamic Media. |
| **[!UICONTROL Downsampling cromaticità]** | Attivare o disattivare il downsampling cromatico utilizzato dagli encoder JPEG. |
| **[!UICONTROL Metodo di ricampionamento predefinito]** | Specifica gli attributi di ricampionamento e interpolazione predefiniti da utilizzare per il ridimensionamento dei dati immagine. Usa quando `resMode` non è specificato in una richiesta.<br>Vedi anche [ResMode](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-is-cat-resmode.html) nella Guida di riferimento visualizzatori di Dynamic Media. |

#### Scheda Attributi comuni delle miniature {#common-thumbnail-attributes-tab}

Queste impostazioni riguardano l’aspetto e l’allineamento predefiniti delle immagini in miniatura.

| Impostazione | Descrizione |
| --- | --- |
| **[!UICONTROL Colore di sfondo predefinito per la miniatura]** | Specifica il valore RGB utilizzato per riempire l&#39;area di un&#39;immagine miniatura di output che non contiene dati immagine effettivi. Utilizzato solo per le richieste di miniature (`req=tmb`) e quando **[!UICONTROL Tipo di miniatura predefinito]** è impostato su **[!UICONTROL Adatta]** o **[!UICONTROL Texture]**.<br>Vedi anche [Colore pollice](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbbkgcolor.html) nella Guida di riferimento visualizzatori di Dynamic Media. |
| **[!UICONTROL Allineamento orizzontale]** | Specifica l&#39;allineamento orizzontale dell&#39;immagine miniatura nel rettangolo dell&#39;immagine di risposta specificato da `wid=` e `hei=` valori.<br>Utilizzato solo per le richieste di miniature (`req=tmb`) e quando **[!UICONTROL Tipo di miniatura predefinito]** è impostato su **[!UICONTROL Adatta]**.<br>Ci sono tre allineamenti orizzontali tra cui scegliere: **[!UICONTROL Allineamento al centro]**, **[!UICONTROL Allineamento a sinistra]** e **[!UICONTROL Allineamento a destra]**.<br>Vedi anche [AllineaOrizzontale](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbhorizalign.html) nella Guida di riferimento visualizzatori di Dynamic Media. |
| **[!UICONTROL Allineamento verticale]** | Specifica l&#39;allineamento verticale dell&#39;immagine miniatura nel rettangolo dell&#39;immagine di risposta specificato da `wid=` e `hei=` valori. Utilizzato solo per le richieste di miniature (`req=tmb`) e quando **[!UICONTROL Tipo di miniatura predefinito]** è impostato su **[!UICONTROL Adatta]**.<br>Ci sono tre allineamenti verticali tra cui scegliere: **[!UICONTROL Allineamento superiore]**, **[!UICONTROL Allineamento al centro]** e **[!UICONTROL Allineamento in basso]**.<br>Vedi anche [ThumbVertAlign](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbvertalign.html) nella Guida di riferimento visualizzatori di Dynamic Media. |
| **[!UICONTROL Durata predefinita cache]** | Fornisce un intervallo di scadenza predefinito in ore nel caso in cui un particolare record di catalogo non contenga un valore di scadenza del catalogo valido. Imposta su `-1` da contrassegnare come non scaduto mai. <br>Vedi anche [Scadenza](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-expiration.html) nella Guida di riferimento visualizzatori di Dynamic Media. |
| **[!UICONTROL Tipo di miniatura predefinito]** | Fornisce un valore predefinito per il tipo di miniatura nel caso in cui un particolare record di catalogo non contenga un valore ThumbType del catalogo valido. Utilizzato solo per le richieste di miniature (`req=tmb`).<br>Sono disponibili tre tipi di miniature tra cui scegliere: **[!UICONTROL Ritaglio]**, **[!UICONTROL Adatta]** e **[!UICONTROL Texture]**.<br>Vedi anche [ThumbType](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbtype.html) nella Guida di riferimento visualizzatori di Dynamic Media. |
| **[!UICONTROL Risoluzione miniature predefinita]** | Fornisce un valore predefinito per la risoluzione dell&#39;oggetto miniatura nel caso in cui un particolare record di catalogo non contenga un valore ThumbRes di catalogo valido. Utilizzato solo per le richieste di miniature (`req=tmb`) e quando **[!UICONTROL Tipo di miniatura predefinito]** è impostato su **[!UICONTROL Texture]**.<br>Vedi anche [ThumbRes](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbres.html) nella Guida di riferimento visualizzatori di Dynamic Media. |

#### Scheda Attributi di gestione del colore {#color-management-attributes-tab}

Queste impostazioni determinano quali profili di colore ICC vengono utilizzati per le immagini.

**Intento di rendering della conversione del colore**
Un intento di rendering della conversione del colore consente di ignorare l’intento di rendering predefinito dei profili di lavoro per determinare come vengono regolati i colori di origine. Utilizzato quando:

1. Uno dei profili ICC predefiniti è lo spazio colore di destinazione di una conversione del colore.
1. Una periferica di output (stampante o monitor) è caratterizzata da questo profilo.
1. Inoltre, l&#39;intento di rendering specificato è valido per questo profilo.

Tenti di rendering diversi utilizzano regole diverse per determinare come vengono regolati i colori di origine.

Ad esempio, puoi impostare il **[!UICONTROL Spazio colore predefinito di RGB]** a **[!UICONTROL sRGB]** e **[!UICONTROL Spazio colore predefinito CMYK]** a **[!UICONTROL WebCoated]**.

In questo modo si effettua quanto segue:

* Abilita la correzione del colore per le immagini RGB e CMYK.
* Si presume che le immagini di RGB prive di un profilo colore siano presenti nel *sRGB* spazio colore.
* Si presume che le immagini CMYK prive di un profilo colore siano in *WebCoated* spazio colore.
* Rendering dinamici che restituiscono l’output di RGB, restituiscilo nel *sRGB* spazio colore.
* Rendering dinamici che restituiscono l’output CMYK, restituiscilo nel *WebCoated* spazio colore.

Vedi anche [IccRenderIntent](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccrenderintent.html) nella Guida di riferimento visualizzatori di Dynamic Media.

>[!NOTE]
In generale, è consigliabile utilizzare l’intento di rendering predefinito per l’impostazione colore selezionata, che è stata testata da Adobe per soddisfare gli standard di settore. Ad esempio, se scegli un’impostazione di colore per Nord America o Europa, l’intento predefinito di rendering della conversione del colore è **[!UICONTROL Colormetrica relativa]**. Se scegli un’impostazione di colore per il Giappone, l’intento predefinito di rendering della conversione del colore è **[!UICONTROL Percettivo]**.

| Impostazione | Caratteristiche |
| --- | --- |
| **[!UICONTROL Spazio colore predefinito CMYK]** | Specifica il nome del profilo colore ICC da utilizzare come profilo di lavoro per i dati CMYK. Se **[!UICONTROL Nessuno specificato]** se si sceglie , la gestione del colore è disabilitata per questo catalogo di immagini quando sono coinvolte immagini sorgente CMYK. Tutti gli spazi di lavoro CMYK dipendono dal dispositivo, il che significa che sono basati su combinazioni effettive di inchiostro e carta. L&#39;Adobe degli spazi di lavoro CMYK si basa sulle condizioni di stampa commerciale standard.<br> Vedi anche [IccProfileCMYK](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilecmyk.html) nella Guida di riferimento visualizzatori di Dynamic Media. |
| **[!UICONTROL Scala di grigio spazio colore predefinito]** | Specifica il nome del profilo colore ICC da utilizzare come profilo di lavoro per i dati in scala di grigi. Se **[!UICONTROL Nessuno specificato]** se si sceglie , la gestione del colore viene disabilitata per questo catalogo di immagini quando sono coinvolte immagini sorgente in scala di grigi.<br>Vedi anche [IccProfileGray](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilegray.html) nella Guida di riferimento visualizzatori di Dynamic Media. |
| **[!UICONTROL Spazio colore predefinito di RGB]** | Specifica il nome del profilo colore ICC da utilizzare come profilo di lavoro per i dati di RGB. Se **[!UICONTROL Nessuno specificato]** se si sceglie , la gestione del colore è disabilitata per questo catalogo di immagini quando sono interessate immagini di sorgenti RGB. In generale, è meglio scegliere **[!UICONTROL Adobe RGB]** o **[!UICONTROL sRGB]**, anziché il profilo di un dispositivo specifico (ad esempio un profilo di monitoraggio). **[!UICONTROL sRGB]** è consigliato quando si preparano le immagini per il web o i dispositivi mobili, in quanto definisce lo spazio colore del monitor standard utilizzato per visualizzare le immagini sul web. **[!UICONTROL sRGB]** è anche una buona scelta quando si lavora con immagini provenienti da fotocamere digitali consumer, perché la maggior parte di queste telecamere utilizza sRGB come spazio colore predefinito.<br>Vedi anche [IccProfileRBG](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilergb.html) nella Guida di riferimento visualizzatori di Dynamic Media. |
| **[!UICONTROL Intento di rendering della conversione colore]** | **[!UICONTROL Percettivo]** - Mira a preservare il rapporto visivo tra i colori in modo che sia percepito come naturale per l’occhio umano, anche se i valori dei colori stessi possono cambiare. Questo intento è adatto per immagini fotografiche con molti colori fuori gamma. Questa impostazione è l’intento di rendering standard per l’industria di stampa giapponese. |
|  | **[!UICONTROL Colorimetrico relativo]** - Confronta l&#39;estrema evidenziazione dello spazio colore sorgente a quello dello spazio colore di destinazione e sposta tutti i colori di conseguenza. I colori fuori gamma vengono spostati sul colore riproducibile più vicino nello spazio colore di destinazione. Colorimetrico relativo conserva più i colori originali in un&#39;immagine rispetto a Perceptual. Questa impostazione è l’intento di rendering standard per la stampa in Nord America ed Europa. |
|  | **[!UICONTROL Saturazione]** - Cerca di produrre colori vividi in un&#39;immagine a scapito della precisione del colore. Questo intento di rendering è adatto a elementi grafici aziendali come grafici o grafici, in cui i colori satura brillante sono più importanti della relazione esatta tra i colori. |
|  | **[!UICONTROL Colorimetrico assoluto]** - Lascia invariati i colori che rientrano nella gamma di destinazione. I colori fuori gamma vengono ritagliati. Non viene eseguita alcuna scala dei colori al punto bianco di destinazione. Questo intento mira a mantenere la precisione del colore a scapito della conservazione delle relazioni tra i colori ed è adatto per la correzione per simulare l&#39;output di un particolare dispositivo. Questo intento è utile per visualizzare in anteprima come il colore della carta influisce sui colori stampati. |

### Verificare le risorse prima di renderle pubbliche {#test-assets-before-making-public}

Il test protetto consente di definire un ambiente di test sicuro e di creare una solida soluzione business-to-business basata su un set configurabile di indirizzi IP e intervalli. Questa funzionalità ti consente di abbinare le distribuzioni Dynamic Media di Adobe all’architettura della gestione dei contenuti e del sistema aziendale.

Con Secure Testing è possibile visualizzare in anteprima la versione di staging del sito web con contenuto non pubblicato.

Se lo desideri, crea un ambiente di staging anziché rendere le risorse disponibili al pubblico per i seguenti motivi:

* Anteprima dei siti web prima del lancio pubblico (sito web di staging).
* Distribuisci risorse che richiedono accesso limitato, ad esempio eCatalog che mostrano i prezzi in un’applicazione web B2B.
* Utilizza le risorse dietro un firewall come parte del sistema di gestione delle informazioni sui prodotti, dell’applicazione per il servizio clienti, del sito di formazione e così via.

>[!NOTE]
La verifica sicura non influisce sull’accesso a Adobe Dynamic Media Classic. La sicurezza Adobe Dynamic Media Classic rimane coerente e richiede le credenziali usuali per l’accesso a Adobe Dynamic Media Classic e ai servizi Web correlati.

#### Come funziona il test sicuro {#how-test-assets-works}

La maggior parte delle aziende gestisce Internet dietro un firewall. L’accesso a Internet è possibile tramite determinati percorsi e in genere attraverso una gamma limitata di indirizzi IP pubblici.

Dalla tua rete aziendale, puoi capire il tuo indirizzo IP pubblico utilizzando siti web come [https://www.whatismyip.com](https://www.whatismyip.com/) oppure richiedi queste informazioni alla tua organizzazione IT aziendale.

Con Secure Testing, Adobe Dynamic Media stabilisce un server di immagini dedicato per gli ambienti di staging o le applicazioni interne. Qualsiasi richiesta a questo server controlla l&#39;indirizzo IP di origine. Se la richiesta in entrata non si trova nell’elenco di indirizzi IP approvato, viene restituita una risposta di errore. L’amministratore aziendale di Adobe Dynamic Media configura l’elenco approvato di indirizzi IP per l’ambiente Secure Testing della propria azienda.

Poiché la posizione della richiesta originale deve essere confermata, il traffico del servizio Secure Testing non viene instradato attraverso una rete di distribuzione del contenuto come il traffico pubblico di Dynamic Media Image Server. Le richieste al servizio Secure Testing hanno una latenza leggermente più elevata rispetto ai server immagini pubblici di Dynamic Media.

Le risorse non pubblicate sono immediatamente disponibili dai servizi Secure Testing, senza necessità di pubblicare. In questo modo, puoi eseguire un’anteprima prima che le risorse vengano pubblicate sul server di immagini rivolto al pubblico.

>[!NOTE]
I servizi di verifica protetta utilizzano il server di catalogo configurato con un contesto di pubblicazione interno. Pertanto, se la tua azienda è configurata per la pubblicazione su Secure Testing, tutte le risorse caricate in Adobe Dynamic Media diventano immediatamente disponibili sui servizi Secure Testing. Questa funzionalità è valida anche se le risorse sono contrassegnate per la pubblicazione al momento del caricamento.

I servizi di verifica sicura supportano attualmente i seguenti tipi di risorse e funzionalità:

* Immagini.
* Vignette (richieste server di rendering).
* Richieste server di rendering (supportate, ma richieste esplicitamente dal cliente).
* Set, compresi set di immagini, eCatalog, set di rendering e set di file multimediali.
* Visualizzatori Dynamic Media rich media standard.
* Adobe pagine JSP Dynamic Media OnDemand.
* Contenuto statico, ad esempio file PDF e video distribuiti progressivamente.
* Streaming video HTTP.
* Streaming video progressivo.

Al momento non sono supportati i seguenti tipi di risorse e funzionalità:

* Ricerca di Adobe Dynamic Media Classic Info o eCatalog
* Streaming video RTMP
* Web-stampa
* Servizi UGC (User-Generated Content)

>[!IMPORTANT]
Il supporto per risorse di immagini vettoriali nuove o esistenti UGC in Adobe Dynamic Media è terminato il 30 settembre 2021.

#### Test del servizio Secure Testing {#test-secure-testing-service}

Per garantire il funzionamento previsto del servizio di test Secure, procedi come segue:

##### Prepara l&#39;account

1. Contatta l’Assistenza clienti Adobe e richiedi l’abilitazione del test protetto sul tuo account.
1. In Adobe Experience Manager, seleziona **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Installazione di Dynamic Media Publish]**.
1. Nella pagina Image Server , **[!UICONTROL Contesto di pubblicazione]** elenco a discesa, seleziona **[!UICONTROL Test Image Serving]**.
1. Seleziona la **[!UICONTROL Sicurezza]** scheda .
1. Per **[!UICONTROL Indirizzo client]** filtro, seleziona **[!UICONTROL Aggiungi]**.
1. In **[!UICONTROL Indirizzo IP]** campo , digita un indirizzo IP.
1. In **[!UICONTROL Maschera]** campo, digitare una maschera di rete.

   >[!NOTE]
   Se si aggiungono più di un indirizzo IP e una maschera di rete, ciò consente efficacemente *tutto* Gli indirizzi IP per effettuare chiamate alle risorse e vengono visualizzati tutti.

1. Effettua una delle operazioni seguenti:

   * Per aggiungere altri indirizzi IP, ripeti i tre passaggi precedenti.
   * Procedi al passaggio successivo.

1. Nell’angolo in alto a destra della pagina Image Server, seleziona **[!UICONTROL Salva]**.
1. Carica le immagini desiderate nel tuo account Dynamic Media di Adobe.

<!--    See [Upload files](uploading-files.md#uploading_files). -->

1. Assicurati che alcune delle immagini siano contrassegnate per la pubblicazione e altre non siano contrassegnate, quindi invia il lavoro di pubblicazione.

<!--    See [Publish files](publishing-files.md#publishing_files). -->

1. Determinare il nome del servizio Secure Testing andando a **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Impostazione generale Dynamic Media]**.
1. Sulla **[!UICONTROL Server]** , trova il nome del server a destra di **[!UICONTROL Nome server pubblicato]**.

Se il nome del server è mancante o se l’URL del server non funziona, contatta l’Assistenza Adobe.

##### Preparare le varianti del sito web

Sono necessarie due varianti di un sito web che collega le risorse pubblicate e non pubblicate:

* Versione pubblica : collega le risorse utilizzando la sintassi URL Dynamic Media tradizionale.
* Versione di staging : collega le risorse utilizzando la stessa sintassi ma con il nome del sito di Secure Testing.

##### Eseguire i test

Esegui i seguenti test:

1. Verifica se le risorse sono visibili dalla rete aziendale.

   Dall&#39;interno della rete aziendale identificata dall&#39;intervallo di indirizzi IP precedentemente definito, la versione di staging del sito web visualizza tutte le immagini, contrassegnate per la pubblicazione o meno. Puoi eseguire il test senza rendere accidentalmente disponibili le immagini prima dell’approvazione dell’anteprima o del lancio del prodotto.

   Conferma che la versione pubblica del sito mostri le risorse pubblicate come precedentemente sperimentato con Adobe Dynamic Media.

1. Dall’esterno della rete aziendale, verifica che le risorse non pubblicate (cioè non contrassegnate per la pubblicazione) siano protette dall’accesso di terze parti.

   Accedi alla rete dall’esterno (ad esempio dal computer di casa o tramite una connessione 4G/5G), quindi verifica che la versione pubblica del sito mostri tutte le risorse pubblicate ma nessuno dei contenuti non pubblicati.

   Conferma che la versione di staging non mostri alcuna risorsa perché accedi al servizio Secure Testing da un indirizzo IP non approvato.

### Configurare le impostazioni generali di Dynamic Media {#configuring-application-general-settings}

>[!IMPORTANT]
Dynamic Media General Setting è disponibile solo se:
* Stai eseguendo Dynamic Media in modalità Scene7.
* Hai un *esistente* **[!UICONTROL Configurazione Dynamic Media]** in **[!UICONTROL Cloud Services]**) in Adobe Experience Manager 6.5 o in Experience Manager as a Cloud Service.
* Sei un amministratore di sistema di Experience Manager con privilegi di amministratore.


Al momento della creazione dell’account, Adobe Dynamic Media fornisce automaticamente i server assegnati all’azienda. Questi server vengono utilizzati per creare stringhe URL per il sito Web e le applicazioni. Queste chiamate URL sono specifiche del tuo account.

Vedi anche [Test del servizio di test Secure](/help/assets/dm-publish-settings.md#test-assets-before-making-public).

**Per configurare l&#39;impostazione generale Dynamic Media:**

1. In modalità Creazione Experience Manager, seleziona il logo Experience Manager per accedere alla console di navigazione globale.
1. Nella barra a sinistra, seleziona l’icona Strumenti , quindi vai a **[!UICONTROL Risorse]** > **[!UICONTROL Impostazione generale Dynamic Media]**.
1. Nella pagina Server , imposta la **[!UICONTROL Nome server pubblicato]** e **[!UICONTROL Nome server di origine]**, quindi utilizza le cinque schede per configurare le impostazioni di pubblicazione predefinite.

   * [Server](#server-general-setting)
   * [Carica nell’applicazione](#upload-to-application)
   * [Modifica delle immagini](#image-editing-tab) scheda
   * [PostScript](#postscript-tab) scheda
   * [Photoshop](#photoshop-tab) scheda
   * [PDF](#pdf-tab) scheda
   * [Illustrator](#illustrator-tab) scheda

   ![Pagina Impostazioni generali di Dynamic Media](/help/assets/assets-dm/dm-general-settings.png)
   *pagina Impostazioni generali di Dynamic Media, con **[!UICONTROL Modifica delle immagini]**scheda selezionata.*<br><br>

1. Al termine, seleziona **[!UICONTROL Salva]**.

#### Server {#server-general-setting}

Al momento della creazione dell’account, Adobe Dynamic Media fornisce automaticamente i server assegnati all’azienda. Questi server vengono utilizzati per creare stringhe URL per il sito Web e le applicazioni. Queste chiamate URL sono specifiche del tuo account.

| Opzione | Descrizione |
| --- | --- |
| **[!UICONTROL Nome server pubblicato]** | Obbligatorio.<br>Questo server è il server CDN live (Content Deliver Network) utilizzato in tutte le chiamate URL generate dal sistema che sono specifiche per il tuo account. Non modificare il nome del server a meno che non venga richiesto da Adobe Technical Support. Il nome deve utilizzare `https://` nel percorso. |
| **[!UICONTROL Nome server origine]** | Obbligatorio.<br>Questo server viene utilizzato solo per il test di controllo della qualità. Non modificare il nome del server a meno che non venga richiesto da Adobe Technical Support. |

#### Carica nell’applicazione {#upload-to-application}

* **[!UICONTROL Sovrascrivi immagini]**

   Adobe Dynamic Media non consente a due file di avere lo stesso nome. L’ID Dynamic Media Adobe di ogni elemento (il nome dell’immagine meno l’estensione del nome del file) deve essere univoco. A causa di questa regola, **[!UICONTROL Carica nell’applicazione]** ha una sovrascrittura. L’effetto esatto di questa opzione dipende dall’opzione Sovrascrivi immagini selezionata. Queste opzioni specificano come vengono caricate le immagini sostitutive: se sostituiscono le immagini originali o diventano immagini duplicate. Le immagini duplicate vengono rinominate con un `-1`. Ad esempio: `chair.tif` viene rinominato `chair-1.tif`. Queste opzioni interessano le immagini caricate in una cartella diversa dall’originale o le immagini con un’estensione di nome file diversa dall’originale, ad esempio JPG, TIF o PNG.

   | Opzione Sovrascrivi immagini | Descrizione |
   | --- | --- |
   | **[!UICONTROL Sovrascrivi in cartella corrente, nome/estensione come risorsa base]** | Predefiniti.<br>Questa opzione è la regola più rigida per la sostituzione. Richiede di caricare l&#39;immagine di sostituzione nella stessa cartella dell&#39;originale e che l&#39;immagine di sostituzione abbia la stessa estensione del nome file dell&#39;originale. Se tali requisiti non sono soddisfatti, viene creato un duplicato. |
   | **[!UICONTROL Sovrascrivi in cartella corrente, nome come risorsa base, ignora estensione]** | Richiede di caricare l&#39;immagine sostitutiva nella stessa cartella dell&#39;originale, tuttavia l&#39;estensione del nome file può essere diversa dall&#39;originale. Ad esempio, sedia.tif sostituisce sedia.jpg. |
   | **[!UICONTROL Sovrascrivi in qualsiasi cartella, nome/estensione come risorsa base]** | Richiede che l&#39;immagine sostitutiva abbia la stessa estensione del nome del file dell&#39;immagine originale (ad esempio, sedia.jpg deve sostituire sedia.jpg, non sedia.tif). Tuttavia, puoi caricare l’immagine di sostituzione in una cartella diversa dall’originale. L&#39;immagine aggiornata si trova nella nuova cartella; non è più possibile trovare il file nella posizione originale. |
   | **[!UICONTROL Sovrascrivi in qualsiasi cartella, nome come risorsa base, ignora estensione]** | Questa opzione è la regola di sostituzione più inclusiva. Puoi caricare un’immagine sostitutiva in una cartella diversa dall’originale, caricare un file con un’estensione diversa del nome del file e sostituire il file originale. Se il file originale si trova in una cartella diversa, l&#39;immagine sostitutiva si trova nella nuova cartella in cui è stata caricata. |

* **[!UICONTROL Mantieni ritaglio]**

   Controlla la conservazione di qualsiasi definizione di ritaglio manuale esistente.

   Vedi anche `preserveCrop` in [UploadPostJob](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-upload-post-job.html) e [ReprocessAssetsJob](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-reprocess-assets-job.html), entrambe nella Guida di riferimento visualizzatori di Dynamic Media.

#### Opzioni di caricamento predefinite {#default-upload-options}

##### Scheda Modifica immagine {#image-editing-tab}

Questo filtro consente di regolare con precisione un effetto filtro di nitidezza sull’immagine ricampionata verso il basso finale. Consente di controllare l’intensità dell’effetto, il raggio dell’effetto (misurato in pixel) e una soglia di contrasto da ignorare.

L’effetto Maschera definizione dettagli utilizza le stesse opzioni del filtro Maschera definizione dettagli di Photoshop. Contrariamente a quanto suggerisce il nome, Maschera definizione dettagli è un filtro di nitidezza.

| Opzioni Maschera definizione dettagli | Descrizione |
| --- | --- |
| **[!UICONTROL Quantità]** | Obbligatorio.<br>Controlla la quantità di contrasto applicata ai pixel del bordo.<br>Pensatelo come l&#39;intensità dell&#39;effetto. La differenza principale tra i valori di quantità di Maschera definizione dettagli in Adobe Dynamic Media e i valori di quantità in Adobe Photoshop, è che Photoshop ha un intervallo di quantità compreso tra l’1% e il 500%. In Adobe Dynamic Media, invece, l’intervallo di valori è `0.0` a `5.0`. Un valore di 5.0 in Adobe Dynamic Media corrisponde approssimativamente al 500% in Photoshop; il valore 0,9 equivale al 90% e così via. |
| **[!UICONTROL Raggio]** | Obbligatorio.<br>Controlla il raggio dell&#39;effetto.<br>L&#39;intervallo di valori è `0` a `250`. L&#39;effetto viene eseguito su tutti i pixel di un&#39;immagine e si irradiano da tutti i pixel in tutte le direzioni. Il raggio viene misurato in pixel. Ad esempio, per ottenere un effetto di nitidezza simile per un&#39;immagine da 2000 x 2000 pixel e un&#39;immagine da 500 x 500 pixel, è necessario impostare un raggio di due pixel sull&#39;immagine da 2000 x 2000 pixel. Quindi imposta un valore di raggio di un pixel sull&#39;immagine da 500 x 500 pixel. Per un’immagine con più pixel viene utilizzato un valore più grande. |
| **[!UICONTROL Soglia]** | Obbligatorio.<br>La soglia è un intervallo di contrasto ignorato quando viene applicato il filtro Maschera definizione dettagli. Questo effetto è importante in modo che non venga introdotto alcun &quot;rumore&quot; a un&#39;immagine quando si utilizza questo filtro. L&#39;intervallo di valori è `0` - `255`, indica il numero di passaggi di luminosità in un&#39;immagine in scala di grigi. `0`=nero `128`=50% grigio e `255`=bianco.<br>Un valore soglia di `12` ignora le variazioni lievi è la luminosità del tono della pelle per evitare l’aggiunta di rumore, ma continua ad aggiungere contrasto ai bordi per le aree di contrasto, ad esempio dove le ciglia incontrano la pelle.<br>Se si dispone di una foto del volto di un utente, la Maschera definizione dettagli influisce sulle parti a contrasto dell’immagine. Ad esempio, dove ciglia e pelle si incontrano per creare un&#39;area ovvia di contrasto, e la pelle liscia stessa. Anche la pelle più liscia presenta sottili cambiamenti nei valori di luminosità. Se non utilizzi un valore di soglia, il filtro accentua queste sottili modifiche nei pixel dell’interfaccia. A sua volta, viene creato un effetto rumoroso e indesiderato mentre il contrasto sulle ciglia viene aumentato, aumentando la nitidezza.<br>Per evitare questo problema, viene introdotto un valore di soglia che indica al filtro di ignorare i pixel che non cambiano radicalmente il contrasto, come la pelle liscia.<br>Nell&#39;immagine della cerniera mostrata in precedenza, notate la texture accanto alle cerniere. Il rumore dell&#39;immagine è visibile perché i valori di soglia erano troppo bassi per eliminare il rumore. |
| **[!UICONTROL Monocromatico]** | Selezionare per applicare una maschera di contrasto alla luminosità dell&#39;immagine (intensità).<br>Deseleziona per applicare una maschera di contrasto a ciascun componente di colore separatamente. |

Vedi anche [Nitidezza delle immagini in Adobe Dynamic Media e su Image Server](/help/assets/assets/sharpening_images.pdf).

##### Scheda PostScript {#postscript-tab}

È possibile rasterizzare i file Adobe PostScript®, mantenere sfondi trasparenti, scegliere una risoluzione e scegliere uno spazio colore.

È possibile utilizzare i file Adobe PostScript® (EPS) in Adobe Dynamic Media. Adobe Dynamic Media offre comandi per configurare questi file durante il caricamento.

Quando carichi i file immagine PostScript (EPS), puoi formattarli in vari modi. È possibile rasterizzare i file, mantenere lo sfondo trasparente, scegliere una risoluzione e scegliere uno spazio colore.

| Opzione PostScript | Descrizione |
| --- | --- |
| **[!UICONTROL Elaborazione]** | Scegliete Rasterizza per convertire la grafica vettoriale nel file in formato bitmap. |
| **[!UICONTROL Mantieni sfondo trasparente nelle immagini renderizzate]** | Mantiene la trasparenza di sfondo del file. |
| **[!UICONTROL Risoluzione (pixel/pollici)]** | Determina l&#39;impostazione della risoluzione. Questa impostazione determina quanti pixel vengono visualizzati per pollice nel file. |
| **[!UICONTROL Spazio colore]** | ・ **[!UICONTROL Rileva automaticamente]** - Mantiene lo spazio colore del file.<br>・ **[!UICONTROL Forza come RGB]** - Si converte nello spazio colore RGB.<br>・ **[!UICONTROL Forza come CMYK]** - Si converte nello spazio colore CMYK.<br>・ **[!UICONTROL Forza come scala di grigi]** - Converte lo spazio colore in scala di grigi. |

##### Scheda Photoshop {#photoshop-tab}

È possibile creare modelli da file Adobe® Photoshop®, mantenere i livelli, specificare il nome dei livelli, estrarre il testo e specificare il modo in cui le immagini vengono ancorate ai modelli.

| Opzione Photoshop | Descrizione |
| --- | --- |
| **[!UICONTROL Mantieni livelli]** | Racchiude gli eventuali livelli di PSD in singole risorse. I livelli delle risorse rimangono associati al PSD. Per visualizzarli, aprite il file PSD in Vista dettagli e selezionate il pannello dei livelli. Consulta Visualizzazione e modifica dei livelli in un file PSD. |
| **[!UICONTROL Crea modello]** | Crea un modello dai livelli nel file PSD. |
| **[!UICONTROL Estrai testo]** | Estrae il testo in modo che gli utenti possano cercare il testo in un visualizzatore. |
| **[!UICONTROL Estendi livelli a dimensione sfondo]** | Estende le dimensioni dei livelli immagine ritagliati alle dimensioni del livello di sfondo. |
| **[!UICONTROL Denominazione livelli]** | Estende le dimensioni dei livelli immagine ritagliati alle dimensioni del livello di sfondo.<br>・ **[!UICONTROL Nome livello]** - Assegna un nome alle immagini dopo i relativi nomi di livello nel file PSD. Ad esempio, un livello denominato Tag prezzo nel file PSD originale diventa un’immagine denominata Tag prezzo . Tuttavia, se i nomi dei livelli nel file PSD sono nomi di livello Photoshop predefiniti (Sfondo, Livello 1, Livello 2 e così via), le immagini vengono denominate in base ai numeri dei rispettivi livelli nel file PSD. <br>・ **[!UICONTROL Photoshop e numero di livello]** - Assegna un nome alle immagini dopo i relativi numeri di livello nel file PSD, ignorando i nomi dei livelli originali. Le immagini vengono denominate con il nome del file Photoshop e un numero di livello aggiunto. Ad esempio, il secondo livello di un file denominato `Spring Ad.psd` è denominato `Spring Ad_2` anche se aveva un nome non predefinito in Photoshop.<br>・ **[!UICONTROL Nome Photoshop e livello]** - Assegna un nome alle immagini dopo il file PSD seguito dal nome del livello o dal numero del livello. Il numero del livello viene utilizzato se i nomi dei livelli nel file PSD sono nomi di livello Photoshop predefiniti. Ad esempio, un livello denominato `Price Tag` in un file PSD denominato `SpringAd` è denominato `Spring Ad_Price Tag`. Viene chiamato un livello con il nome predefinito Livello 2 `Spring Ad_2`. |
| **[!UICONTROL Ancoraggio]** | Specifica il modo in cui le immagini vengono ancorate nei modelli generati dalla composizione a livelli prodotta dal file PSD. Per impostazione predefinita, l’ancoraggio è al centro. Un ancoraggio centrale consente alle immagini sostitutive di riempire al meglio lo stesso spazio, indipendentemente dalle proporzioni dell&#39;immagine sostitutiva. Le immagini con un aspetto diverso che sostituiscono questa immagine, quando fanno riferimento al modello e utilizzano la sostituzione di parametri, occupano effettivamente lo stesso spazio. Passa a un’impostazione diversa se l’applicazione richiede le immagini sostitutive per riempire lo spazio allocato nel modello. |

##### Scheda PDF {#pdf-tab}

È possibile scegliere di rasterizzare i file, estrarre parole di ricerca e collegamenti, impostare la risoluzione e scegliere uno spazio colore.

| opzione PDF | Descrizione |
| --- | --- |
| **[!UICONTROL Elaborazione]** | ・ **[!UICONTROL Nessuno]** - Non viene eseguita alcuna elaborazione del PDF.<br>・ **[!UICONTROL Miniatura]** - Copia ogni pagina nel file PDF e la converte in un’immagine in miniatura.<br> ・ **[!UICONTROL Rasterizza]** - Esegue la rimozione delle pagine nel file PDF e converte la grafica vettoriale in immagini bitmap. Per creare un eCatalog, scegli questa opzione. |
| **[!UICONTROL Estrai]** | ・ **[!UICONTROL Nessuno]** - Nessun termine o collegamento di ricerca estratto da PDF.<br>・ **[!UICONTROL Parole di ricerca]** - Estrae le parole di ricerca dal file PDF in modo che la ricerca nel file possa essere eseguita per parola chiave in un visualizzatore di eCatalog.<br>・ **[!UICONTROL Collegamenti]** - Estrae i collegamenti dai file PDF e li converte in mappe immagine utilizzate in un visualizzatore di eCatalog.<br>・ **[!UICONTROL Ricerca di parole e collegamenti]** - Estrae sia le parole di ricerca che i collegamenti da utilizzare in un visualizzatore eCatalog. |
| **[!UICONTROL Risoluzione (pixel/pollici)]** | Determina l&#39;impostazione della risoluzione. Questa impostazione determina quanti pixel vengono visualizzati per pollice nel file PDF. Il valore predefinito è 150. |
| **[!UICONTROL Spazio colore]** | ・ **[!UICONTROL Rileva automaticamente]** - Mantiene lo spazio colore del file PDF.<br>・ **[!UICONTROL Forza come RGB]** - Si converte nello spazio colore RGB.<br>・ **[!UICONTROL Forza come CMYK]** - Si converte nello spazio colore CMYK.<br>・ **[!UICONTROL Forza come scala di grigi]** - Converte lo spazio colore in scala di grigi. |

##### Scheda Illustrator {#illustrator-tab}

È possibile rasterizzare i file Adobe Illustrator®, mantenere sfondi trasparenti, scegliere una risoluzione e scegliere uno spazio colore.

È possibile utilizzare file Adobe® Illustrator® (AI) in Adobe Dynamic Media. Adobe Dynamic Media offre comandi per configurare questi file durante il caricamento.

Quando carichi i file immagine di Illustrator (AI), puoi formattarli in vari modi. È possibile rasterizzare i file, mantenere lo sfondo trasparente, scegliere una risoluzione e scegliere uno spazio colore. Le opzioni per la formattazione dei file PostScript e Illustrator sono disponibili nella schermata Carica in Opzioni PostScript e Opzioni Illustrator nella casella Opzioni processo di caricamento.


| Opzione Illustrator | Descrizione |
| --- | --- |
| **[!UICONTROL Elaborazione]** | Scegliete Rasterizza per convertire la grafica vettoriale nel file in formato bitmap. |
| **[!UICONTROL Mantieni sfondo trasparente nelle immagini renderizzate]** | Mantiene la trasparenza di sfondo del file. |
| **[!UICONTROL Risoluzione (pixel/pollici)]** | Determina l&#39;impostazione della risoluzione. Questa impostazione determina quanti pixel vengono visualizzati per pollice nel file. |
| **[!UICONTROL Spazio colore]** | ・ **[!UICONTROL Rileva automaticamente]** - Mantiene lo spazio colore del file.<br>・ **[!UICONTROL Forza come RGB]** - Si converte nello spazio colore RGB.<br>・ **[!UICONTROL Forza come CMYK]** - Si converte nello spazio colore CMYK.<br>・ **[!UICONTROL Forza come scala di grigi]** - Converte lo spazio colore in scala di grigi. |


**[!UICONTROL Profili colore predefiniti]** - Vedi [Configurare la gestione del colore](#configuring-color-management) per ulteriori informazioni.

>[!NOTE]
Per impostazione predefinita, il sistema mostra 15 rappresentazioni quando selezioni **[!UICONTROL Rappresentazioni]** e 15 predefiniti visualizzatore quando fai clic su **[!UICONTROL Visualizzatori]** nella vista Dettaglio della risorsa. Puoi aumentare questo limite. Vedi [Aumenta il numero di predefiniti immagine da visualizzare](/help/assets/managing-image-presets.md#increasing-or-decreasing-the-number-of-image-presets-that-display) o [Aumenta il numero di predefiniti visualizzatore da visualizzare](/help/assets/managing-viewer-presets.md#increasing-the-number-of-viewer-presets-that-display).

### (Facoltativo) Attività di configurazione aggiuntive

Le attività di configurazione e configurazione opzionali includono:

* [Modifica tipi MIME per i formati supportati](#editing-mime-types-for-supported-formats) **RICK: MANTENERE?**
* [Aggiungi tipi MIME per i formati non supportati](#adding-mime-types-for-unsupported-formats) **RICK: MANTENERE?**
* [Creare predefiniti per set di batch per generare automaticamente set di immagini e set 360 gradi](#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets) **RICK: MANTENERE?**

* **[!UICONTROL Attributi di compatibilità]** - **RICK: C&#39;È ANCORA BISOGNO? ERA A CLASSIC** Questa impostazione consente di trattare i paragrafi iniziali e finali nei livelli di testo come nella versione 3.6 per garantire la compatibilità con le versioni precedenti.
* **[!UICONTROL Supporto per la localizzazione]** - **RICK: C&#39;È ANCORA BISOGNO? ERA A CLASSIC** Queste impostazioni consentono di gestire più attributi internazionali. Consente inoltre di specificare una stringa di mappa delle impostazioni internazionali in modo da definire le lingue che si desidera supportare per le varie descrizioni a comparsa nei visualizzatori. Per ulteriori informazioni sulla configurazione **[Supporto per la localizzazione]**, vedi [Considerazioni sulla localizzazione delle risorse](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/setup/publish-setup.html#considerations-when-setting-up-localization-of-assets).

#### Modifica tipi MIME per i formati supportati {#editing-mime-types-for-supported-formats}

**RICK: MANTENETE COSÌ?**

Puoi definire quali tipi di risorse vengono elaborati da Dynamic Media e personalizzare parametri avanzati di elaborazione delle risorse. Ad esempio, puoi specificare i parametri di elaborazione delle risorse per effettuare le seguenti operazioni:

* Converti un Adobe PDF in una risorsa eCatalog.
* Converti un documento Adobe Photoshop (.PSD) in una risorsa modello banner per la personalizzazione.
* Rasterizza un file Adobe Illustrator (.AI) o un file di PostScript® incapsulato Adobe Photoshop (.EPS).
* [Profili video](/help/assets/video-profiles.md) e [Profili immagine](/help/assets/image-profiles.md) può essere utilizzato rispettivamente per definire l’elaborazione di video e immagini.

Consulta [Caricamento delle risorse](/help/assets/manage-assets.md#uploading-assets).

**Per modificare i tipi MIME per i formati supportati:**

1. In Experience Manager, seleziona il logo Experience Manager per accedere alla console di navigazione globale, quindi accedi a . **[!UICONTROL Strumenti]** > **[!UICONTROL Generale]** > **[!UICONTROL CRXDE Lite]**.
1. Nella barra a sinistra, passa a quanto segue:

   `/conf/global/settings/cloudconfigs/dmscene7/jcr:content/mimeTypes`

   ![Tipi MIME](assets/mimetypes.png)

1. Nella cartella mimeTypes , seleziona un tipo di mime.
1. Sul lato destro della pagina CRXDE Lite, nella parte inferiore:

   * Fai doppio clic sul pulsante **[!UICONTROL abilitato]** campo . Per impostazione predefinita, tutti i tipi di MIME delle risorse sono abilitati (impostati su **[!UICONTROL true]**), il che significa che le risorse vengono sincronizzate in Dynamic Media per l’elaborazione. Se desideri escludere l’elaborazione di questo tipo di MIME delle risorse, modifica questa impostazione in **[!UICONTROL false]**.

   * Doppio tocco **[!UICONTROL jobParam]** per aprire il relativo campo di testo associato. Vedi [Tipi mime supportati](/help/assets/assets-formats.md#supported-mime-types) per un elenco dei valori dei parametri di elaborazione consentiti è possibile utilizzare per un determinato tipo di MIME.

1. Effettua una delle operazioni seguenti:

   * Ripeti i passaggi 3-4 per modificare altri tipi MIME.
   * Nella barra dei menu della pagina CRXDE Lite, seleziona **[!UICONTROL Salva tutto]**.

1. Nell’angolo in alto a sinistra della pagina, seleziona **[!UICONTROL CRXDE Lite]** per tornare all&#39;Experience Manager.

#### Aggiunta di tipi MIME per i formati non supportati {#adding-mime-types-for-unsupported-formats}

**RICK: MANTENETE COSÌ?**

In Experience Manager Assets puoi aggiungere tipi MIME personalizzati per i formati non supportati. Assicurati che qualsiasi nuovo nodo aggiunto in CRXDE Lite non venga eliminato per Experience Manager spostando il tipo MIME prima di `image_`. Inoltre, assicurati che il valore abilitato sia impostato su **[!UICONTROL false]**.

**Per aggiungere tipi MIME per i formati non supportati:**

1. Dall’Experience Manager, passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Operazioni]** > **[!UICONTROL Console web]**.

   ![2019-08-02_16-13-14](assets/2019-08-02_16-13-14.png)

1. Viene visualizzata una nuova scheda del browser **[!UICONTROL Configurazione della console Web di Adobe Experience Manager]** pagina.

   ![2019-08-02_16-17-29](assets/2019-08-02_16-17-29.png)

1. Nella pagina, scorri verso il basso fino al nome *Adobe CQ Scene7 Asset MIME type Service*, come illustrato nella schermata successiva. A destra del nome, seleziona la **[!UICONTROL Modifica i valori di configurazione]** (icona a forma di matita).

   ![2019-08-02_16-44-56](assets/2019-08-02_16-44-56.png)

1. Sulla **Servizio Adobe CQ Scene7 Asset MIME type** , selezionare un&#39;icona del segno più &lt;+>. La posizione nella tabella in cui si seleziona il segno più per aggiungere il nuovo tipo di MIME è insignificante.

   ![2019-08-02_16-27-27](assets/2019-08-02_16-27-27.png)

1. Tipo `DWG=image/vnd.dwg` nel campo di testo vuoto appena aggiunto.

   L&#39;esempio `DWG=image/vnd.dwg` è solo a scopo dimostrativo. Il tipo MIME che aggiungi qui può essere qualsiasi altro formato non supportato.

   ![2019-08-02_16-36-36](assets/2019-08-02_16-36-36.png)

1. Nell’angolo inferiore destro della pagina, seleziona **[!UICONTROL Salva]**.

   A questo punto, è possibile chiudere la scheda del browser con la pagina di configurazione della console Web di Adobe Experience Manager aperta.

1. Torna alla scheda del browser con la console di Experience Manager aperta.
1. Dall’Experience Manager, passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Generale]** > **[!UICONTROL CRXDE Lite]**.

   ![2019-08-02_16-55-41](assets/2019-08-02_16-55-41.png)

1. Nella barra a sinistra, passa a quanto segue:

   `conf/global/settings/cloudconfigs/dmscene7/jcr:content/mimeTypes`

1. Trascina il tipo di mime `image_vnd.dwg` e rilasciarlo direttamente sopra `image_` nell&#39;albero come visto nella schermata seguente.

   ![crxdelite_cqdoc-14627](assets/crxdelite_cqdoc-14627.png)

1. Con il tipo mime `image_vnd.dwg` ancora selezionato, dal **[!UICONTROL Proprietà]** nella scheda **[!UICONTROL abilitato]** riga, sotto **[!UICONTROL Valore]** intestazione di colonna, tocca due volte il valore per aprire la **[!UICONTROL Valore]** elenco a discesa.
1. Tipo `false` nel campo (o seleziona **[!UICONTROL false]** dall’elenco a discesa).

   ![2019-08-02_16-60-30](assets/2019-08-02_16-60-30.png)

1. Nell’angolo in alto a sinistra della pagina CRXDE Lite, seleziona **[!UICONTROL Salva tutto]**.

#### Creare predefiniti per set di batch per generare automaticamente set di immagini e set 360 gradi {#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets}

**RICK: MANTENETE COSÌ?**

Utilizza i predefiniti per set di batch per automatizzare la creazione di set di immagini o set 360 gradi durante il caricamento delle risorse in Dynamic Media.

Innanzitutto, definisci la convenzione di denominazione per il raggruppamento delle risorse in un set. Quindi crea un Batch Set Preset che è un set di istruzioni autonomo con nome univoco. Deve definire come creare il set utilizzando immagini che corrispondono alle convenzioni di denominazione definite nella composizione preimpostata.

Quando carichi dei file, Dynamic Media crea automaticamente un set con tutti i file che corrispondono alla convenzione di denominazione definita nei predefiniti attivi.

##### Configurare la denominazione predefinita

Crea una convenzione di denominazione predefinita utilizzata in qualsiasi ricetta predefinita per set di batch. La convenzione di denominazione predefinita selezionata nella definizione del predefinito del set di batch è probabilmente tutto ciò che è necessario per la società per generare i set in batch. Viene creato un predefinito per set di batch per utilizzare la convenzione di denominazione predefinita definita dall’utente. È possibile creare un numero illimitato di predefiniti per set di batch con convenzioni di denominazione alternative e personalizzate necessarie per un determinato set di contenuti nei casi in cui vi sia un’eccezione alla denominazione predefinita definita dall’azienda.

Sebbene non sia necessaria l’impostazione di una convenzione di denominazione predefinita per utilizzare le funzionalità di preimpostazione di set di batch, è consigliabile utilizzare la convenzione di denominazione predefinita. Consente di definire tutti gli elementi della convenzione di denominazione che si desidera raggruppare in un set in modo da semplificare la creazione di set di batch.

In alternativa, puoi utilizzare **[!UICONTROL Visualizza codice]** senza campi modulo disponibili. In questa visualizzazione puoi creare le definizioni delle convenzioni di denominazione utilizzando esclusivamente espressioni regolari.

Sono disponibili due elementi per la definizione, la corrispondenza e il nome di base. Questi campi consentono di definire tutti gli elementi di una convenzione di denominazione e identificare la parte della convenzione utilizzata per denominare il set in cui sono contenuti. La convenzione di denominazione individuale di un’azienda utilizza spesso una o più righe di definizione per ciascuno di questi elementi. Puoi utilizzare altrettante righe per la definizione univoca e raggrupparle in elementi distinti, ad esempio per l’immagine principale, l’elemento Colore, l’elemento Vista alternativa e l’elemento Campione.

**Per configurare la denominazione predefinita:**

**RICK: MANTENETE COSÌ?**

1. Apri [applicazione desktop Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started), quindi accedi al tuo account.

   Le credenziali e i dettagli di accesso sono stati forniti da Adobe al momento del provisioning. Se non disponi di tali informazioni, contatta l’Assistenza clienti Adobe.

1. Nella barra di navigazione accanto alla parte superiore della pagina, individua **[!UICONTROL Configurazione]** > **[!UICONTROL Impostazione applicazione]** > **[!UICONTROL Predefiniti set di batch]** > **[!UICONTROL Denominazione predefinita]**.
1. Per specificare come visualizzare e immettere le informazioni di ciascun elemento, seleziona **[!UICONTROL Visualizza modulo]** o **[!UICONTROL Visualizza codice]**.

   È possibile selezionare la **[!UICONTROL Visualizza codice]** casella di controllo per visualizzare la creazione del valore dell’espressione regolare accanto alle selezioni del modulo. È possibile immettere o modificare questi valori per definire gli elementi della convenzione di denominazione, se la visualizzazione del modulo vi limita per qualsiasi motivo. Se i valori non possono essere analizzati nella visualizzazione modulo, i campi modulo diventano inattivi.

   >[!NOTE]
   I campi modulo disattivati non eseguono alcuna convalida per verificare che le espressioni regolari siano corrette. Vengono visualizzati i risultati dell’espressione regolare che si sta creando per ogni elemento dopo la riga Risultato. L’espressione regolare completa è visibile nella parte inferiore della pagina.

1. Espandi ogni elemento in base alle esigenze e immetti le convenzioni di denominazione che desideri utilizzare.
1. Se necessario, effettuare una delle seguenti operazioni:

   * Seleziona **[!UICONTROL Aggiungi]** per aggiungere un’altra convenzione di denominazione per un elemento.
   * Seleziona **[!UICONTROL Rimuovi]** per eliminare una convenzione di denominazione per un elemento.

1. Effettua una delle operazioni seguenti:

   * Seleziona **[!UICONTROL Salva con nome]** e digita un nome per il predefinito.
   * Seleziona **[!UICONTROL Salva]** se stai modificando un predefinito esistente.

##### Creare un predefinito per set di batch

Dynamic Media utilizza i predefiniti per set di batch per organizzare le risorse in set di immagini (immagini alternative, opzioni colore, 360 giri) da visualizzare nei visualizzatori. I predefiniti per set di batch vengono eseguiti automaticamente insieme ai processi di caricamento delle risorse in Dynamic Media.

Puoi creare, modificare e gestire i predefiniti per set di batch. Esistono due forme di definizioni di predefiniti per set di batch: uno per una convenzione di denominazione predefinita che è possibile impostare e uno per le convenzioni di denominazione personalizzate create al volo.

È possibile utilizzare il metodo campo modulo per definire un predefinito per set di batch o il metodo del codice, che consente di utilizzare espressioni regolari. Come per la denominazione predefinita, è possibile scegliere Visualizza codice nello stesso momento in cui si sta definendo nella visualizzazione modulo e utilizzare espressioni regolari per creare le definizioni. In alternativa, puoi deselezionare entrambe le visualizzazioni per utilizzare esclusivamente l’una o l’altra.

**Per creare un predefinito per set di batch:**

**RICK: MANTENETE COSÌ?**

1. Apri [applicazione desktop Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started), quindi accedi al tuo account.

   Le credenziali e i dettagli di accesso sono stati forniti da Adobe al momento del provisioning. Se non disponi di tali informazioni, contatta l’Assistenza clienti Adobe.

1. Nella barra di navigazione accanto alla parte superiore della pagina, individua **[!UICONTROL Configurazione]** > **[!UICONTROL Impostazione applicazione]** > **[!UICONTROL Predefiniti set di batch]** > **[!UICONTROL Preimpostazione set di batch]**.

   **[!UICONTROL Visualizza modulo]**, come impostato nell’angolo superiore destro della pagina Dettagli, è la visualizzazione predefinita.

1. Nel pannello Elenco predefiniti, seleziona **[!UICONTROL Aggiungi]** per attivare i campi di definizione nel pannello Dettagli sul lato destro dello schermo.
1. Nel pannello Dettagli, nel campo Nome predefinito , digita un nome per il predefinito.
1. Selezionare un tipo di predefinito dal menu a discesa Tipo set di batch.
1. Effettua una delle operazioni seguenti:

   * Se utilizzi una convenzione di denominazione predefinita impostata in precedenza in **[!UICONTROL Impostazione applicazione]** > **[!UICONTROL Predefiniti set di batch]** > **[!UICONTROL Denominazione predefinita]**, espandi **[!UICONTROL Convenzioni di denominazione delle risorse]**, quindi seleziona **[!UICONTROL Predefinito]**.

   * Per definire una nuova convenzione di denominazione durante la configurazione del predefinito, espandi **[!UICONTROL Convenzioni di denominazione delle risorse]**, quindi seleziona **[!UICONTROL Personalizzato]**.

1. Per Ordine di sequenza, definite l&#39;ordine in cui le immagini vengono visualizzate dopo il raggruppamento del set in Dynamic Media.

   Per impostazione predefinita, le risorse vengono ordinate in modo alfanumerico. Tuttavia, per definire l’ordine è possibile utilizzare un elenco di espressioni regolari separate da virgola.

1. Per Imposta convenzione di denominazione e creazione, specifica il suffisso o il prefisso al nome di base definito nella convenzione di denominazione delle risorse. Inoltre, definisci dove viene creato il set all’interno della struttura di cartelle Dynamic Media.

   Se definisci un numero elevato di set, mantieni i set separati dalle cartelle contenenti le risorse stesse. Ad esempio, crea una cartella Set di immagini e inserisci qui i set generati.

1. Nel pannello Dettagli, seleziona **[!UICONTROL Salva]**.
1. Seleziona **[!UICONTROL Attivo]** accanto al nuovo nome predefinito.

   L’attivazione del predefinito assicura che quando carichi le risorse in Dynamic Media, il Batch Set Preset venga applicato per generare il set.

##### Creare un set di batch predefinito per la generazione automatica di un set 360 gradi 2D

È possibile utilizzare il tipo di set di batch **[!UICONTROL Set 360 gradi con più assi]** per creare una ricetta che automatizza la generazione di set 360 gradi 2D. Il raggruppamento delle immagini utilizza espressioni regolari Riga e Colonna in modo che le risorse immagine siano correttamente allineate nella posizione corrispondente nell’array multidimensionale. Non esiste un numero minimo o massimo di righe o colonne che è necessario avere in un set 360 gradi a più assi.

Ad esempio, supponi di voler creare un set 360 gradi con più assi denominato `spin-2dspin`. Hai un set di immagini per set 360 gradi che contengono tre righe, con 12 immagini per riga. Le immagini vengono denominate come segue:

```
spin-01-01
 spin-01-02
 …
 spin-01-12
 spin-02-01
 …
 spin-03-12
```

Con queste informazioni, la ricetta Tipo set di batch può essere creata come segue:

![chlimage_1-560](assets/chlimage_1-560.png)

Il raggruppamento per la parte del nome della risorsa condivisa del set 360 gradi viene aggiunto al **[!UICONTROL Corrispondenza]** (come evidenziato). La parte variabile del nome della risorsa, contenente la riga e la colonna, viene aggiunta rispettivamente ai campi **[!UICONTROL Riga]** e **[!UICONTROL Colonna]**.

Quando il set 360 gradi viene caricato e pubblicato, puoi attivare il nome della definizione del set 360 gradi 2D che è riportato in **[!UICONTROL Predefiniti set di batch]**, nella finestra di dialogo **[!UICONTROL Opzioni processo di caricamento]**.

**Per creare un Batch Set Preset per la generazione automatica di un Set 360 gradi 2D:**

**RICK: MANTENETE COSÌ?**

1. Apri [applicazione desktop Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started), quindi accedi al tuo account.

   Le credenziali e i dettagli di accesso sono stati forniti da Adobe al momento del provisioning. Se non disponi di tali informazioni, contatta l’Assistenza clienti Adobe.

1. Nella barra di navigazione accanto alla parte superiore della pagina, individua **[!UICONTROL Configurazione]** > **[!UICONTROL Impostazione applicazione]** > **[!UICONTROL Predefiniti set di batch]** > **[!UICONTROL Preimpostazione set di batch]**.

   **[!UICONTROL Visualizza modulo]**, come impostato nell’angolo superiore destro della pagina Dettagli, è la visualizzazione predefinita.

1. Nel pannello Elenco predefiniti, seleziona **[!UICONTROL Aggiungi]** per attivare i campi di definizione nel pannello Dettagli sul lato destro dello schermo.
1. Nel pannello Dettagli, nel campo Nome predefinito , digita un nome per il predefinito.
1. Nel menu a discesa Tipo set di batch, seleziona **[!UICONTROL Set risorse]**.
1. Nell’elenco a discesa Sottotipo , seleziona **[!UICONTROL Set 360 gradi con più assi]**.
1. Espandi **[!UICONTROL Convenzioni di denominazione delle risorse]**, quindi seleziona **[!UICONTROL Personalizzato]**.
1. Utilizza gli attributi **[!UICONTROL Match (Corrispondenza)]** e, facoltativamente, **[!UICONTROL Nome base]** per definire un’espressione regolare per la denominazione delle risorse dell’immagine che compongono il raggruppamento.

   Ad esempio, l’espressione regolare Corrispondenza letterale può avere un aspetto simile al seguente:

   `(w+)-w+-w+`

1. Espandi **[!UICONTROL Posizione colonna riga]**, quindi definisci il formato del nome per la posizione della risorsa immagine all’interno della matrice Set 360 gradi 2D.

   Utilizzare le parentesi per abbracciare la posizione della riga o della colonna nel nome del file.

   Ad esempio, per l’espressione regolare della riga, può avere un aspetto simile al seguente:

   `\w+-R([0-9]+)-\w+`

   oppure

   `\w+-(\d+)-\w+`

   Per l’espressione regolare della colonna, può essere simile al seguente:

   `\w+-\w+-C([0-9]+)`

   oppure

   `\w+-\w+-C(\d+)`

   I campioni di cui sopra sono solo a scopo dimostrativo. Puoi creare l’espressione regolare in base alle tue esigenze.

   >[!NOTE]
   Se la combinazione di espressioni regolari per riga e colonna non è in grado di determinare la posizione della risorsa all’interno della matrice del set 360 gradi multidimensionale, la risorsa non viene aggiunta al set. Viene registrato anche un errore.

1. Per Imposta convenzione di denominazione e creazione, specifica il suffisso o il prefisso al nome di base definito nella convenzione di denominazione delle risorse.

   Inoltre, definisci dove viene creato il set 360 gradi all’interno della struttura delle cartelle Dynamic Media Classic.

   Se definisci un numero elevato di set, mantieni i set separati dalle cartelle contenenti le risorse stesse. Ad esempio, crea una cartella Set 360 gradi in cui inserire i set generati.

1. Nel pannello Dettagli, seleziona **[!UICONTROL Salva]**.
1. Seleziona **[!UICONTROL Attivo]** accanto al nuovo nome predefinito.

   L’attivazione del predefinito assicura che quando carichi le risorse in Dynamic Media, il Batch Set Preset venga applicato per generare il set.

### (Facoltativo) Ottimizzare le prestazioni di Dynamic Media - Modalità Scene7 {#optional-tuning-the-performance-of-dynamic-media-scene-mode}

**RICK: MANTENETE COSÌ?**

Per mantenere la modalità Dynamic Media - Scene7 in esecuzione senza problemi, l&#39;Adobe consiglia i seguenti suggerimenti per l&#39;ottimizzazione delle prestazioni/della scalabilità di sincronizzazione:

* Aggiornamento dei parametri di processo predefiniti per l&#39;elaborazione di diversi formati di file.
* Aggiornamento dei thread di lavoro predefiniti del flusso di lavoro Granite (risorse video) in coda.
* Aggiornamento dei thread di lavoro temporanei di coda predefiniti del flusso di lavoro Granite (immagini e risorse non video).
* Aggiornamento delle connessioni di caricamento massime nel server Dynamic Media Classic.

#### Aggiornare i parametri di processo predefiniti per l’elaborazione di diversi formati di file

**RICK: MANTENETE COSÌ?**

Puoi ottimizzare i parametri dei processi per velocizzarne l’elaborazione quando carichi i file. Ad esempio, se carichi i file PSD ma non desideri elaborarli come modelli, puoi impostare l’estrazione del livello su false (disattivato). In questo caso, il parametro del processo di sintonizzazione viene visualizzato come segue: `process=None&createTemplate=false`.

Se desideri attivare la creazione di modelli, utilizza i seguenti parametri: `process=MaintainLayers&layerNaming=AppendName&createTemplate=true`.

<!-- THIS PARAGRAPH WAS REPLACED WITH THE TWO PARAGRAPHS DIRECTLY ABOVE BASED ON CQDOC-17657 You can tune job parameters for faster processing when you upload files. For example, if you are uploading PSD files, but do not want to process them as templates, you can set layer extraction to false (off). In such case, the tuned job parameter would appear as `process=None&createTemplate=false`. -->

Adobe consiglia di utilizzare i seguenti parametri di processo &quot;ottimizzati&quot; per i file PDF, PostScript® e PSD:

<!-- OLD PDF JOB PARAMETERS `pdfprocess=Rasterize&resolution=150&colorspace=Auto&pdfbrochure=false&keywords=false&links=false` -->

<!-- OLD POSTSCRIPT JOB PARAMETERS `psprocess=Rasterize&psresolution=150&pscolorspace=Auto&psalpha=false&psextractsearchwords=false&aiprocess=Rasterize&airesolution=150&aicolorspace=Auto&aialpha=false` -->

| Tipo di file | Parametri di lavoro consigliati |
| ---| ---|
| PDF | `pdfprocess=Thumbnail&resolution=150&colorspace=Auto&pdfbrochure=false&keywords=false&links=false` |
| PostScript® | `psprocess=Rasterize&psresolution=150&pscolorspace=Auto&psalpha=false&psextractsearchwords=false&aiprocess=Thumbnail&airesolution=150&aicolorspace=Auto&aialpha=false` |
| PSD | `process=None&layerNaming=AppendName&anchor=Center&createTemplate=false&extractText=false&extendLayers=false` |

<!-- CQDOC-17657 for PSD entry in table above -->

Per aggiornare uno qualsiasi di questi parametri, segui i passaggi descritti in [Abilitazione del supporto per i parametri di processo di caricamento di Assets/Dynamic Media Classic basati su tipi MIME](/help/sites-administering/scene7.md#enabling-mime-type-based-assets-scene-upload-job-parameter-support).

#### Aggiorna la coda del flusso di lavoro transitorio di Granite {#updating-the-granite-transient-workflow-queue}

**RICK: MANTENETE COSÌ?**

La coda del flusso di lavoro di transito Granite viene utilizzata per **[!UICONTROL Risorsa di aggiornamento DAM]** workflow. In Dynamic Media viene utilizzato per l’acquisizione e l’elaborazione delle immagini.

**Per aggiornare la coda del flusso di lavoro transitorio di Granite:**

1. Passa a [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr) e cerca **Coda: Coda flusso di lavoro transitorio di Granite**.

   >[!NOTE]
   È necessaria una ricerca di testo invece di un URL diretto perché il PID OSGi viene generato in modo dinamico.

1. In **[!UICONTROL Processi paralleli massimi]** modifica il numero nel valore desiderato.

   È possibile aumentare **[!UICONTROL Processi paralleli massimi]** per supportare adeguatamente il caricamento di file pesanti in Dynamic Media. Il valore esatto dipende dalla capacità hardware. In alcuni scenari, ovvero una migrazione iniziale o un caricamento in serie una tantum, puoi utilizzare un valore elevato. Tuttavia, l’utilizzo di un valore elevato (come il doppio del numero di core) può avere effetti negativi su altre attività simultanee. Di conseguenza, verifica e regola il valore in base al tuo caso d’uso specifico.

<!--    By default, the maximum number of parallel jobs depends on the number of available CPU cores. For example, on a 4-core server, it assigns 2 worker threads. (A value between 0.0 and 1.0 is ratio based, or any numbers greater than 1 will assign the number of worker threads.)

   Adobe recommends that 32 **[!UICONTROL Maximum Parallel Jobs]** be configured to adequately support heavy upload of files to Dynamic Media Classic (Scene7). -->

![chlimage_1](assets/chlimage_1.jpeg)

1. Seleziona **[!UICONTROL Salva]**.

#### Aggiorna la coda del flusso di lavoro Granite {#updating-the-granite-workflow-queue}

**RICK: MANTENETE COSÌ?**

La coda del flusso di lavoro Granite viene utilizzata per i flussi di lavoro non transitori. In Dynamic Media, elaborava i video con il **[!UICONTROL Codifica video Dynamic Media]** workflow.

**Per aggiornare la coda del flusso di lavoro Granite:**

1. Passa a `https://<server>/system/console/configMgr` e cerca **Coda: Coda flusso di lavoro Granite**.

   >[!NOTE]
   È necessaria una ricerca di testo invece di un URL diretto perché il PID OSGi viene generato in modo dinamico.

1. In **[!UICONTROL Processi paralleli massimi]** modifica il numero nel valore desiderato.

   Puoi aumentare il numero massimo di processi paralleli per supportare in modo adeguato il caricamento di file pesanti in Dynamic Media. Il valore esatto dipende dalla capacità hardware. In alcuni scenari, ovvero una migrazione iniziale o un caricamento in serie una tantum, puoi utilizzare un valore elevato. Tuttavia, l’utilizzo di un valore elevato (come il doppio del numero di core) può avere effetti negativi su altre attività simultanee. Di conseguenza, verifica e regola il valore in base al tuo caso d’uso specifico.

   ![chlimage_1-1](assets/chlimage_1-1.jpeg)

1. Seleziona **[!UICONTROL Salva]**.

#### Aggiornare la connessione di caricamento Dynamic Media Classic {#updating-the-scene-upload-connection}

**RICK: MANTENETE COSÌ?**

L’impostazione Scene7 Upload Connection sincronizza le risorse di Experience Manager con i server Dynamic Media Classic.

**Per aggiornare la connessione di caricamento Dynamic Media Classic:**

1. Accedi a `https://<server>/system/console/configMgr/com.day.cq.dam.scene7.impl.Scene7UploadServiceImpl`
1. In **[!UICONTROL Numero di connessioni]** e/o **[!UICONTROL Timeout processo attivo]** modifica il numero come desiderato.

   La **[!UICONTROL Numero di connessioni]** controlla il numero massimo di connessioni HTTP consentite, ad Experience Manager per il caricamento su Dynamic Media; in genere, il valore predefinito di dieci connessioni è sufficiente.

   La **[!UICONTROL Timeout processo attivo]** determina il tempo di attesa per le risorse Dynamic Media caricate da pubblicare nel server di consegna. Per impostazione predefinita, questo valore è di 2100 secondi o 35 minuti.

   Per la maggior parte dei casi d’uso, è sufficiente impostare 2100.

   ![chlimage_1-2](assets/chlimage_1-2.jpeg)

1. Seleziona **[!UICONTROL Salva]**.

### (Facoltativo) Filtrare le risorse per la replica {#optional-filtering-assets-for-replication}

**RICK: MANTIENI COSÌ COME È**

In implementazioni non Dynamic Media, puoi replicare *tutto* risorse (sia immagini che video) dall’ambiente di authoring di Experience Manager al nodo di pubblicazione di Experience Manager. Questo flusso di lavoro è necessario perché anche i server di pubblicazione Experience Manager distribuiscono le risorse.

Tuttavia, nelle implementazioni di Dynamic Media, poiché le risorse vengono distribuite tramite il Cloud Service, non è necessario replicare le stesse risorse nei nodi di pubblicazione di Experience Manager. Questo flusso di lavoro &quot;pubblicazione ibrida&quot; evita costi di storage aggiuntivi e tempi di elaborazione più lunghi per la replica delle risorse. Altri contenuti, come le pagine del sito, continuano a essere serviti dai nodi di pubblicazione di Experience Manager.

I filtri forniscono un modo per *escludere* risorse dalla replica nel nodo di pubblicazione di Experience Manager.

#### Utilizzare filtri di risorse predefiniti per la replica {#using-default-asset-filters-for-replication}

**RICK: MANTIENI COSÌ COME È**

Se utilizzi Dynamic Media per l’imaging, il video o entrambi, puoi utilizzare i filtri predefiniti forniti da Adobe così come sono. I seguenti filtri sono attivi per impostazione predefinita:

|  | Filtro | Tipo MIME | Rappresentazioni |
| --- | --- | --- | --- |
| Consegna immagini Dynamic Media | filter-image<br>set di filtri | Inizia con **immagine/**<br> Contiene **applicazioni/** e termina con **set**. | Le &quot;immagini filtro&quot; predefinite (applicabili alle risorse di immagini singole, comprese le immagini interattive) e i &quot;set di filtri&quot; (applicabili ai set 360 gradi, ai set di immagini, ai set di file multimediali diversi e ai set di caroselli) consentono di:<br>・ Escludere dalla replica le rappresentazioni originali delle immagini e statiche. |
| Distribuzione video Dynamic Media | filter-video | Inizia con **video/** | Il &quot;video filtro&quot; preconfigurato:<br>・ Escludere dalla replica le rappresentazioni video originali e le miniature statiche. |

>[!NOTE]
I filtri si applicano ai tipi MIME e non possono essere specifici del percorso.

#### Personalizzare i filtri delle risorse per la replica {#customizing-asset-filters-for-replication}

**RICK: MANTIENI COSÌ COME È**

1. In Experience Manager, seleziona il logo Experience Manager per accedere alla console di navigazione globale e passa a . **[!UICONTROL Strumenti]** > **[!UICONTROL Generale]** > **[!UICONTROL CRXDE Lite]**.
1. Nella struttura ad albero delle cartelle a sinistra, passa a `/etc/replication/agents.author/publish/jcr:content/damRenditionFilters` per rivedere i filtri.

   ![chlimage_1-17](assets/chlimage_1-2.png)

1. Per definire il tipo di MIME per il filtro, potete individuare il tipo di MIME come segue:

   Nella barra a sinistra, espandi `content > dam > <locate_your_asset> > jcr:content > metadata`, quindi nella tabella, individua `dc:format`.

   L’immagine seguente è un esempio del percorso di una risorsa verso `dc:format`.

   ![chlimage_1-18](assets/chlimage_1-3.png)

   Tieni presente che `dc:format` per la risorsa `Fiji Red.jpg` è `image/jpeg`.

   Per applicare questo filtro a tutte le immagini, indipendentemente dal formato, imposta il valore su `image/*` dove `*` è un&#39;espressione regolare applicata a tutte le immagini di qualsiasi formato.

   Affinché il filtro si applichi solo alle immagini del tipo JPEG, immetti un valore di `image/jpeg`.

1. Definisci quali rappresentazioni desideri includere o escludere dalla replica.

   I caratteri utilizzabili per filtrare la replica includono:

   | Carattere da utilizzare | Filtrare le risorse per la replica |
   | --- | --- |
   | * | Carattere jolly |
   | + | Include le risorse per la replica |
   | - | Esclude le risorse dalla replica |

   Accedi a `content/dam/<locate your asset>/jcr:content/renditions`.

   L’immagine seguente è un esempio delle rappresentazioni di una risorsa.

   ![chlimage_1-4](assets/chlimage_1-4.png)

   Se si desidera replicare solo l&#39;originale, si immetterà `+original`.
