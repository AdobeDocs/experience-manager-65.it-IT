---
title: Configurazione di Dynamic Media - Modalità Scene7
description: Scopri come configurare la modalità Dynamic Media - Scene7.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
docset: aem65
role: User, Admin
exl-id: badd0f5c-2eb7-430d-ad77-fa79c4ff025a
feature: Configurazione,Modalità Scene7
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '6153'
ht-degree: 5%

---

# Configurazione di Dynamic Media - Modalità Scene7{#configuring-dynamic-media-scene-mode}

Se utilizzi l’impostazione Adobe Experience Manager per ambienti diversi, ad esempio sviluppo, staging e produzione, configura Cloud Services Dynamic Media per ciascuno di tali ambienti.

## Diagramma dell&#39;architettura di Dynamic Media - Modalità Scene7 {#architecture-diagram-of-dynamic-media-scene-mode}

Il diagramma dell&#39;architettura seguente descrive il funzionamento della modalità Dynamic Media - Scene7.

Con la nuova architettura, Experience Manager è responsabile delle risorse di origine primaria e delle sincronizzazioni con Dynamic Media per l’elaborazione e la pubblicazione delle risorse:

1. Quando la risorsa di origine principale viene caricata in Experience Manager, viene replicata in Dynamic Media. A questo punto, Dynamic Media gestisce l’elaborazione e la generazione di rendering delle risorse, ad esempio la codifica video e le varianti dinamiche di un’immagine. <!-- (In Dynamic Media - Scene7 mode, be aware that you can only upload assets whose file sizes are 2 GB or less.) Jira ticket CQ-4286561 fixed this issue. DM-S7 NOW SUPPORTS THE UPLOAD OF ASSETS LARGER THAN 2 GB. -->
1. Dopo la generazione dei rendering, Experience Manager può accedere in modo sicuro e visualizzare in anteprima i rendering Dynamic Media remoti (nessun file binario viene inviato nuovamente all’istanza di Experience Manager).
1. Quando il contenuto è pronto per essere pubblicato e approvato, attiva il servizio Dynamic Media per inviare contenuti ai server di consegna e memorizzare in cache il contenuto nella rete CDN (Content Delivery Network).

![chlimage_1-550](assets/chlimage_1-550.png)

>[!IMPORTANT]
>
>Il seguente elenco di funzioni richiede l’utilizzo della rete CDN preconfigurata fornita con Adobe Experience Manager - Dynamic Media. Qualsiasi altra rete CDN personalizzata non è supportata con queste funzioni.
>
>* [Imaging avanzato](/help/assets/imaging-faq.md)
* [Annullamento della validità della cache](/help/assets/invalidate-cdn-cache-dynamic-media.md)
* [Protezione del collegamento ipertestuale](/help/assets/hotlink-protection.md)
* [Distribuzione HTTP/2 dei contenuti](/help/assets/http2.md)
* Reindirizzamento URL a livello CDN
* Akamai ChinaCDN (per una consegna ottimale in Cina)


## Abilitazione di Dynamic Media in modalità Scene7 {#enabling-dynamic-media-in-scene-mode}

[Dynamic Media è disattivato per impostazione predefinita. ](https://business.adobe.com/products/experience-manager/assets/dynamic-media.html) Per sfruttare le funzionalità di Dynamic Media, è necessario abilitarle.

>[!WARNING]
Dynamic Media - La modalità Scene7 è destinata solo all’ *istanza di authoring di Experience Manager*. Di conseguenza, devi configurare `runmode=dynamicmedia_scene7` nell’istanza di authoring di Experience Manager, *not* l’istanza Publish di Experience Manager.

Per abilitare Dynamic Media, è necessario avviare l&#39;Experience Manager utilizzando la modalità di esecuzione `dynamicmedia_scene7` dalla riga di comando immettendo quanto segue in una finestra terminale (la porta di esempio utilizzata è 4502):

```shell
java -Xms4096m -Xmx4096m -Doak.queryLimitInMemory=500000 -Doak.queryLimitReads=500000 -jar cq-quickstart-6.5.0.jar -gui -r author,dynamicmedia_scene7 -p 4502
```

## (Facoltativo) Migrazione di predefiniti e configurazioni Dynamic Media da 6.3 a 6.5 Zero Downtime {#optional-migrating-dynamic-media-presets-and-configurations-from-to-zero-downtime}

L’aggiornamento di Experience Manager Dynamic Media dalla versione 6.3 alla versione 6.4 o 6.5 ora include la possibilità di eseguire installazioni senza tempi di inattività. Per migrare tutti i predefiniti e le configurazioni da `/etc` a `/conf` in CRXDE Lite, assicurati di eseguire il seguente comando curl.

>[!NOTE]
Se esegui l’istanza di Experience Manager in modalità di compatibilità, ovvero se hai installato il pacchetto di compatibilità, non è necessario eseguire questi comandi.

Per tutti gli aggiornamenti, sia con che senza il pacchetto di compatibilità, puoi copiare i predefiniti predefiniti predefiniti per visualizzatori forniti originariamente con Dynamic Media eseguendo il seguente comando curl Linux®:

`curl -u admin:admin -X POST https://<server_address>:<server_port>/libs/settings/dam/dm/presets/viewer.pushviewerpresets.json`

Per migrare eventuali predefiniti e configurazioni personalizzate creati da `/etc` a `/conf`, esegui il seguente comando curl Linux®:

`curl -u admin:admin -X POST https://<server_address>:<server_port>/libs/settings/dam/dm/presets.migratedmcontent.json`

## Installazione del feature pack 18912 per la migrazione di massa delle risorse {#installing-feature-pack-for-bulk-asset-migration}

L&#39;installazione del feature pack 18912 è *opzionale*.

Il Feature Pack 18912 consente di caricare in massa le risorse tramite FTP oppure di migrare le risorse da Dynamic Media - modalità ibrida o Dynamic Media Classic in modalità Dynamic Media - Scene7 in Experience Manager. È disponibile da [Adobe Professional Services](https://business.adobe.com/customers/consulting-services/main.html).

Per ulteriori informazioni, consulta [Installazione del feature pack 18912 per la migrazione di massa delle risorse](/help/assets/bulk-ingest-migrate.md) .

## Creazione di una configurazione Dynamic Media nei Cloud Services {#configuring-dynamic-media-cloud-services}

**Prima di configurare Dynamic Media**  - Dopo aver ricevuto l&#39;e-mail di provisioning con le credenziali Dynamic Media, è necessario aprire l&#39;applicazione [ desktop ](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)Dynamic Media Classic, quindi accedere al tuo account per modificare la password. La password fornita nell&#39;e-mail di provisioning è generata dal sistema e destinata solo a essere una password temporanea. È importante aggiornare la password in modo che il Cloud Service Dynamic Media sia configurato con le credenziali corrette.

![dynamic icmediaconfiguration2update](assets/dynamicmediaconfiguration2updated.png)

**Per creare una configurazione Dynamic Media nei Cloud Services:**

1. In modalità Autore Experience Manager, tocca il logo Experience Manager per accedere alla console di navigazione globale e tocca l’icona Strumenti , quindi tocca **[!UICONTROL Cloud Services]** > **[!UICONTROL Configurazione Dynamic Media]**.
1. Nella pagina del Browser configurazioni Dynamic Media, seleziona il riquadro a sinistra e tocca **[!UICONTROL global (globale)]** (non toccare o selezionare l’icona della cartella a sinistra di **[!UICONTROL global]**), quindi tocca **[!UICONTROL Crea]**.
1. Nella pagina **[!UICONTROL Crea configurazione Dynamic Media]**, immetti un titolo, l&#39;indirizzo e-mail dell&#39;account Dynamic Media, la password, quindi seleziona la tua area geografica. Queste informazioni vengono fornite per Adobe nell’e-mail di provisioning. Se non hai ricevuto l’e-mail, contatta l’Assistenza clienti di Adobe.

   Tocca **[!UICONTROL Connetti a Dynamic Media]**.

   >[!NOTE]
   Dopo aver ricevuto l&#39;e-mail di provisioning con le credenziali Dynamic Media, apri l&#39; [applicazione desktop Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started), quindi accedi al tuo account per modificare la tua password. La password fornita nell&#39;e-mail di provisioning è generata dal sistema e destinata solo a essere una password temporanea. È importante aggiornare la password in modo che il Cloud Service Dynamic Media sia configurato con le credenziali corrette.

1. Quando la connessione ha esito positivo, imposta quanto segue. Le intestazioni con asterisco (*) sono obbligatorie:

   * **[!UICONTROL Società]** : il nome dell&#39;account Dynamic Media. Hai più account Dynamic Media. Ad esempio, puoi avere diversi marchi secondari, divisioni, staging o ambienti di produzione.

   * **[!UICONTROL Percorso cartella principale della società]**

   * **[!UICONTROL Pubblicazione delle risorse]** : puoi scegliere tra le tre opzioni seguenti:
      * **** Significa immediatamente che quando le risorse vengono caricate, il sistema le acquisisce e fornisce l’URL/da incorporare all’istante. Non è necessario alcun intervento degli utenti per pubblicare le risorse.
      * **[!UICONTROL Al momento]** dell’attivazione, devi pubblicare esplicitamente la risorsa prima prima di fornire un collegamento URL/Incorpora .<br><!-- CQDOC-17478, Added March 9, 2021-->A partire da Experience Manager 6.5.8, l’istanza Publish di Experience Manager riflette valori di metadati Dynamic Media precisi, ad esempio  `dam:scene7Domain` e  `dam:scene7FileStatus` solo in modalità  **[!UICONTROL On]** Activationpublish . Per abilitare questa funzionalità, installare Service Pack 8, quindi riavviare Experience Manager. Vai a Gestione configurazione Sling. Trova la configurazione per `Scene7ActivationJobConsumer Component` o creane una nuova). Seleziona la casella di controllo **[!UICONTROL Replica metadati dopo la pubblicazione da parte di Dynamic Media]**, quindi tocca **[!UICONTROL Salva]**.

         ![Casella di controllo Replica metadati dopo la pubblicazione di Dynamic Media](assets-dm/replicate-metadata-setting.png)

      * **[!UICONTROL Pubblicazione selettivaQuesta opzione consente di controllare le cartelle pubblicate in Dynamic Media.]** Consente di utilizzare funzioni quali Ritaglio avanzato o rappresentazioni dinamiche, oppure di determinare quali cartelle vengono pubblicate esclusivamente in Experience Manager per la visualizzazione dell’anteprima. Le stesse risorse sono *non* pubblicate in Dynamic Media per la distribuzione nel dominio pubblico.<br>Puoi impostare questa opzione qui in  **[!UICONTROL Dynamic Media Cloud]** Configuration oppure, se lo desideri, puoi scegliere di impostare questa opzione a livello di cartella, in  **[!UICONTROL Proprietà]** di una cartella.<br>Consulta [Utilizzo della pubblicazione selettiva in Dynamic Media](/help/assets/selective-publishing.md).<br>Se successivamente modifichi questa configurazione o la modifichi a livello di cartella, queste modifiche interessano solo le nuove risorse caricate da quel momento in poi. Lo stato di pubblicazione delle risorse esistenti nella cartella rimane invariato finché non le cambi manualmente dalla finestra di dialogo **[!UICONTROL Pubblicazione rapida]** o **[!UICONTROL Gestisci pubblicazione]**.
   * **[!UICONTROL Server di anteprima protetto]** : consente di specificare il percorso URL del server di anteprima delle rappresentazioni protette. In altre parole, dopo la generazione delle rappresentazioni, Experience Manager può accedere in modo sicuro e visualizzare in anteprima le rappresentazioni Dynamic Media remote (nessun file binario viene inviato nuovamente all’istanza di Experience Manager).
A meno che non si disponga di una disposizione speciale per utilizzare il server della propria azienda o un server speciale, Adobe consiglia di lasciare questa impostazione come specificato.

   * **[!UICONTROL Sincronizza tutto il contenuto]**  -  <!-- NEW OPTION, CQDOC-15371, Added March 4, 2020-->Selezionato per impostazione predefinita. Deseleziona questa opzione se desideri includere o escludere in modo selettivo le risorse dalla sincronizzazione con Dynamic Media. Deselezionando questa opzione puoi scegliere tra le due seguenti modalità di sincronizzazione Dynamic Media:

   * **[!UICONTROL Modalità di sincronizzazione elementi Dynamic Media]**
      * **[!UICONTROL Abilitata per impostazione predefinita]** : la configurazione viene applicata a tutte le cartelle per impostazione predefinita, a meno che non si contrassegni una cartella specifica per l’esclusione.  <!-- you can then deselect the folders that you do not want the configuration applied to.-->
      * **[!UICONTROL Disabilitata per impostazione predefinita]** : la configurazione non viene applicata ad alcuna cartella finché non contrassegni esplicitamente una cartella selezionata per la sincronizzazione con Dynamic Media.
Per contrassegnare una cartella selezionata per la sincronizzazione con Dynamic Media, seleziona una cartella di risorse, quindi tocca **[!UICONTROL Proprietà]** sulla barra degli strumenti. Nella scheda **[!UICONTROL Dettagli]**, nell&#39;elenco a discesa **[!UICONTROL Modalità di sincronizzazione Dynamic Media]** , scegli una delle tre opzioni seguenti. Al termine, tocca **[!UICONTROL Salva]**. *Ricorda: queste tre opzioni non sono disponibili se hai selezionato **[!UICONTROL Sincronizza tutto il contenuto]**in precedenza.* Consulta anche  [Utilizzo della pubblicazione selettiva a livello di cartella in Dynamic Media](/help/assets/selective-publishing.md).
         * **[!UICONTROL Ereditato]**  - Nessun valore di sincronizzazione esplicito sulla cartella; la cartella eredita invece il valore di sincronizzazione da una delle cartelle precedenti o dalla modalità predefinita nella configurazione cloud. Lo stato dettagliato per le visualizzazioni ereditate viene visualizzato tramite una descrizione comandi.
         * **[!UICONTROL Abilita per sottocartelle]**  - Includi tutto ciò che si trova in questa sottostruttura per la sincronizzazione con Dynamic Media. Le impostazioni specifiche per la cartella sostituiscono la modalità predefinita nella configurazione cloud.
         * **[!UICONTROL Disabilitata per le sottocartelle]**  - Escludi tutto ciò che si trova in questa struttura secondaria dalla sincronizzazione con Dynamic Media.

   >[!NOTE]
   In DMS7 non è supportato il controllo delle versioni. Inoltre, l’attivazione ritardata si applica solo se l’opzione **[!UICONTROL Pubblica risorse]** della pagina Modifica configurazione Dynamic Media è impostata su **[!UICONTROL All’attivazione]** e soltanto fino alla prima attivazione della risorsa.
   Dopo l’attivazione di una risorsa, tutti gli aggiornamenti vengono immediatamente pubblicati in tempo reale su S7 Delivery.

1. Tocca **[!UICONTROL Salva]**.
1. Per visualizzare in anteprima in modo sicuro il contenuto Dynamic Media prima della pubblicazione, è necessario &quot;inserire nell&#39;elenco Consentiti&quot; l’istanza di authoring di Experience Manager per connettersi a Dynamic Media:

   * Apri l&#39; [applicazione desktop Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started), quindi accedi al tuo account. Le credenziali e i dettagli di accesso sono stati forniti da Adobe al momento del provisioning. Se non si dispone di tali informazioni, contattare il supporto tecnico.

   * Nella barra di navigazione in alto a destra della pagina, tocca **[!UICONTROL Configurazione]** > **[!UICONTROL Impostazione applicazione]** > **[!UICONTROL Impostazioni pubblicazione]** > **[!UICONTROL Server immagini]**.

   * Nella pagina Pubblica su Image Server, seleziona **[!UICONTROL Test Image Server]** dall’elenco a discesa Contesto pubblicazione.
   * Per il filtro indirizzi client, tocca **[!UICONTROL Aggiungi]**.
   * Per abilitare (attivare) l’indirizzo, selezionare la casella di controllo. Immetti l’indirizzo IP dell’istanza di authoring di Experience Manager (non dell’IP di Dispatcher).
   * Tocca **[!UICONTROL Salva]**.

La configurazione di base è terminata. è possibile utilizzare la modalità Dynamic Media - Scene7.

Se desideri personalizzare ulteriormente la configurazione, puoi eventualmente completare una qualsiasi delle attività descritte in [(Facoltativo) Configurazione delle impostazioni avanzate in Dynamic Media - Modalità Scene7](#optional-configuring-advanced-settings-in-dynamic-media-scene-mode).

## (Facoltativo) Configurazione delle impostazioni avanzate in modalità Dynamic Media - Scene7 {#optional-configuring-advanced-settings-in-dynamic-media-scene-mode}

Se desideri personalizzare ulteriormente la configurazione e l&#39;impostazione della modalità Dynamic Media - Scene7 o ottimizzarne le prestazioni, puoi completare una o più delle seguenti attività *facoltative*:

* [(Facoltativo) Configurazione e configurazione di Dynamic Media - Impostazioni della modalità Scene7](#optional-setup-and-configuration-of-dynamic-media-scene7-mode-settings)

* [(Facoltativo) Ottimizzazione delle prestazioni di Dynamic Media - Modalità Scene7](#optional-tuning-the-performance-of-dynamic-media-scene-mode)

* [(Facoltativo) Filtraggio delle risorse per la replica](#optional-filtering-assets-for-replication)

### (Facoltativo) Configurazione e configurazione di Dynamic Media - Impostazioni della modalità Scene7 {#optional-setup-and-configuration-of-dynamic-media-scene7-mode-settings}

Quando sei in modalità di esecuzione `dynamicmedia_scene7`, utilizza l’interfaccia utente di Dynamic Media Classic per modificare le impostazioni di Dynamic Media.

Alcune delle attività di cui sopra richiedono l&#39;apertura dell&#39; [applicazione desktop Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started), quindi l&#39;accesso al tuo account.

Le attività di configurazione e configurazione includono:

* [Configurazione pubblicazione per Image Server](#publishing-setup-for-image-server)
* [Configurazione delle impostazioni generali dell&#39;applicazione](#configuring-application-general-settings)
* [Configurazione della gestione del colore](#configuring-color-management)
* [Modifica dei tipi MIME per i formati supportati](#editing-mime-types-for-supported-formats)
* [Aggiunta di tipi MIME per i formati non supportati](#adding-mime-types-for-unsupported-formats)
* [Creazione di predefiniti per set di batch per generare automaticamente set di immagini e set 360 gradi](#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets)

#### Configurazione pubblicazione per Image Server {#publishing-setup-for-image-server}

Le impostazioni di Configurazione pubblicazione determinano il modo in cui le risorse vengono distribuite per impostazione predefinita da Dynamic Media. Se non viene specificata alcuna impostazione, Dynamic Media distribuisce una risorsa in base alle impostazioni predefinite definite in Configurazione pubblicazione. Ad esempio, una richiesta di fornire un’immagine che non include un attributo di risoluzione genera un’immagine con l’impostazione Risoluzione oggetto predefinita.

Per configurare l&#39;impostazione di pubblicazione: in Dynamic Media Classic, tocca **[!UICONTROL Configurazione]** > **[!UICONTROL Impostazione applicazione]** > **[!UICONTROL Impostazioni pubblicazione]** > **[!UICONTROL Server immagini]**.

La schermata Image Server stabilisce le impostazioni predefinite per la distribuzione delle immagini. Per una descrizione di ciascuna impostazione, consulta la schermata dell’interfaccia utente .

* **[!UICONTROL Richiedi attributi]** : queste impostazioni impongono limiti alle immagini che possono essere consegnate dal server.
* **[!UICONTROL Attributi richiesta predefiniti]** : queste impostazioni si riferiscono all&#39;aspetto predefinito delle immagini.
* **[!UICONTROL Attributi comuni delle miniature]** : queste impostazioni si riferiscono all&#39;aspetto predefinito delle immagini in miniatura.
* **[!UICONTROL Valori predefiniti per i campi del catalogo]**: queste impostazioni si riferiscono alla risoluzione e al tipo di miniatura predefinito delle immagini.
* **[!UICONTROL Attributi di gestione del colore]** : queste impostazioni determinano quali profili di colore ICC vengono utilizzati.
* **[!UICONTROL Attributi di compatibilità]** : questa impostazione consente ai paragrafi iniziali e finali nei livelli di testo di essere trattati come nella versione 3.6 per la compatibilità con le versioni precedenti.
* **[!UICONTROL Supporto per la localizzazione]** : queste impostazioni consentono di gestire più attributi di impostazione internazionale. Consente inoltre di specificare una stringa di mappa delle impostazioni internazionali in modo da definire le lingue che si desidera supportare per le varie descrizioni a comparsa nei visualizzatori. Per ulteriori informazioni sulla configurazione del **[supporto per la localizzazione]**, consulta [Considerazioni sulla configurazione della localizzazione delle risorse](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/setup/publish-setup.html?lang=en#considerations-when-setting-up-localization-of-assets).

#### Configurazione delle impostazioni generali dell&#39;applicazione {#configuring-application-general-settings}

Per aprire la pagina Impostazioni generali applicazione, nella barra di navigazione globale di Dynamic Media Classic, tocca **[!UICONTROL Configurazione]** > **[!UICONTROL Configurazione applicazione]** > **[!UICONTROL Impostazioni generali]**.

**[!UICONTROL Server]**  - Al momento del provisioning dell’account, Dynamic Media fornisce automaticamente i server assegnati alla tua azienda. Questi server vengono utilizzati per creare stringhe URL per il sito Web e le applicazioni. Queste chiamate URL sono specifiche del tuo account. Non modificare nessuno dei nomi dei server, a meno che non sia esplicitamente richiesto dall’Assistenza clienti di Adobe.

**[!UICONTROL Sovrascrivi immagini]** : Dynamic Media non consente a due file di avere lo stesso nome. L&#39;ID URL di ogni elemento (il nome del file meno l&#39;estensione) deve essere univoco. Queste opzioni specificano come vengono caricate le risorse sostitutive: se sostituiscono l&#39;originale o diventano duplicati. Le risorse duplicate vengono rinominate con un &quot;-1&quot; (ad esempio, chair.tif viene rinominato chair-1.tif). Queste opzioni interessano le risorse caricate in una cartella diversa dall’originale o le risorse con un’estensione di nome file diversa dall’originale (come JPG, TIF o PNG).

* **[!UICONTROL Sovrascrivi nella cartella corrente, nome/estensione]**  immagine di base - Questa opzione è la regola più rigida per la sostituzione. Richiede di caricare l&#39;immagine di sostituzione nella stessa cartella dell&#39;originale e che l&#39;immagine di sostituzione abbia la stessa estensione del nome file dell&#39;originale. Se tali requisiti non sono soddisfatti, viene creato un duplicato.

>[!NOTE]
Per mantenere la coerenza con l’Experience Manager, scegli sempre questa impostazione: **Sovrascrivi nella cartella corrente, stesso nome/estensione dell&#39;immagine di base**

* **[!UICONTROL Sovrascrivi in qualsiasi cartella, stesso nome/estensione della risorsa base]**  - Richiede che l&#39;immagine sostitutiva abbia la stessa estensione del nome file dell&#39;immagine originale (ad esempio, sedia.jpg deve sostituire sedia.jpg, non sedia.tif). Tuttavia, puoi caricare l’immagine di sostituzione in una cartella diversa dall’originale. L&#39;immagine aggiornata si trova nella nuova cartella; il file non può più essere trovato nella posizione originale
* **[!UICONTROL Sovrascrivi in qualsiasi cartella, lo stesso nome della risorsa di base indipendentemente dall&#39;estensione]**  - Questa opzione è la regola di sostituzione più inclusiva. Puoi caricare un’immagine sostitutiva in una cartella diversa dall’originale, caricare un file con un’estensione diversa del nome del file e sostituire il file originale. Se il file originale si trova in una cartella diversa, l&#39;immagine sostitutiva si trova nella nuova cartella in cui è stata caricata.

**[!UICONTROL Profili colore predefiniti]**  - Per ulteriori informazioni, consulta  [Configurazione della ](#configuring-color-management) gestione colore .

>[!NOTE]
Per impostazione predefinita, il sistema mostra 15 rappresentazioni quando selezioni **[!UICONTROL Rappresentazioni]** e 15 predefiniti visualizzatore quando fai clic su **[!UICONTROL Visualizzatori]** nella vista Dettaglio della risorsa. Puoi aumentare questo limite. Consulta [Aumento del numero di predefiniti immagine da visualizzare](/help/assets/managing-image-presets.md#increasing-or-decreasing-the-number-of-image-presets-that-display) o [Aumento del numero di predefiniti visualizzatore da visualizzare](/help/assets/managing-viewer-presets.md#increasing-the-number-of-viewer-presets-that-display).


#### Configurazione della gestione del colore {#configuring-color-management}

La gestione del colore dei contenuti multimediali dinamici consente di colorare le risorse corrette. Con la correzione del colore, le risorse acquisite mantengono lo spazio colore (RGB, CMYK, Grigio) e il profilo colore incorporato. Quando si richiede un rendering dinamico, il colore dell&#39;immagine viene corretto nello spazio colore di destinazione utilizzando l&#39;output CMYK, RGB o Grigio. Consulta [Configurazione dei predefiniti per immagini](/help/assets/managing-image-presets.md).

Per configurare le proprietà colore predefinite in modo che la correzione colore sia abilitata quando le immagini sono richieste:

1. Apri l&#39; [applicazione desktop Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started), quindi accedi al tuo account utilizzando le credenziali fornite durante il provisioning.
1. Passa a **[!UICONTROL Configurazione > Impostazione applicazione]**.
1. Espandi l’area **[!UICONTROL Publish Setup (Impostazione pubblicazione)]** e seleziona **[!UICONTROL Image Server]**. Per le istanze di pubblicazione, imposta **[!UICONTROL Contesto di pubblicazione]** su **[!UICONTROL Image Server]**.
1. Scorri fino alla proprietà da modificare. Ad esempio, una proprietà nell&#39;area **[!UICONTROL Attributi di gestione del colore]**.

   È possibile impostare le seguenti proprietà di correzione del colore:

   * **[!UICONTROL Spazio colore predefinito CMYK]**  - Nome del profilo colore CMYK predefinito
   * **[!UICONTROL Spazio colore predefinito su scala di grigi]**  - Nome del profilo colore grigio predefinito
   * **[!UICONTROL Spazio]**  colore predefinito RGB - Nome del profilo colore RGB predefinito
   * **[!UICONTROL Intento di rendering della conversione colore]**  - Specifica l&#39;intento di rendering. I valori accettabili sono: **[!UICONTROL percettivo]**, **[!UICONTROL colometrico relativo]**, **[!UICONTROL saturazione]**, **[!UICONTROL colometrico assoluto]**. L&#39;Adobe consiglia **[!UICONTROL relativo]** come impostazione predefinita.

1. Tocca **[!UICONTROL Salva]**.

Ad esempio, puoi impostare **[!UICONTROL Spazio colore predefinito RGB]** su *sRGB* e **[!UICONTROL Spazio colore predefinito CMYK]** su *WebCoated*.

In questo modo si effettua quanto segue:

* Abilita la correzione del colore per le immagini RGB e CMYK.
* Le immagini RGB che non hanno un profilo colore sono considerate nello spazio colore *sRGB*.
* Le immagini CMYK prive di un profilo colore sono considerate nello spazio colore *WebCoated*.
* Rendering dinamici che restituiscono l’output RGB, restituiscilo nello spazio colore *sRGB*.
* Rendering dinamici che restituiscono l&#39;output CMYK, restituiscilo nello spazio colore *WebCoated*.

#### Modifica dei tipi MIME per i formati supportati {#editing-mime-types-for-supported-formats}

Puoi definire quali tipi di risorse vengono elaborati da Dynamic Media e personalizzare parametri avanzati di elaborazione delle risorse. Ad esempio, puoi specificare i parametri di elaborazione delle risorse per effettuare le seguenti operazioni:

* Converti un Adobe PDF in una risorsa eCatalog.
* Converti un documento Adobe Photoshop (.PSD) in una risorsa modello banner per la personalizzazione.
* Rasterizza un file Adobe Illustrator (.AI) o un file di PostScript® incapsulato Adobe Photoshop (.EPS).
* [I ](/help/assets/video-profiles.md) profili video e i profili  [ ](/help/assets/image-profiles.md) di imaging possono essere utilizzati rispettivamente per definire l’elaborazione di video e immagini.

Consulta [Caricamento delle risorse](/help/assets/manage-assets.md#uploading-assets).

**Per modificare i tipi MIME per i formati supportati:**

1. Ad Experience Manager, tocca il logo Experience Manager per accedere alla console di navigazione globale, quindi tocca **[!UICONTROL Strumenti]** > **[!UICONTROL Generale]** > **[!UICONTROL CRXDE Lite]**.
1. Nella barra a sinistra, passa a quanto segue:

   `/conf/global/settings/cloudconfigs/dmscene7/jcr:content/mimeTypes`

   ![Tipi MIME](assets/mimetypes.png)

1. Nella cartella mimeTypes , seleziona un tipo di mime.
1. Sul lato destro della pagina CRXDE Lite, nella parte inferiore:

   * fai doppio clic sul campo **[!UICONTROL abilitato]** . Per impostazione predefinita, tutti i tipi di MIME delle risorse sono abilitati (impostati su **[!UICONTROL true]**), il che significa che le risorse vengono sincronizzate in Dynamic Media per l’elaborazione. Se desideri escludere l’elaborazione di questo tipo di MIME delle risorse, modifica questa impostazione in **[!UICONTROL false]**.

   * tocca due volte **[!UICONTROL jobParam]** per aprire il relativo campo di testo associato. Consulta [Tipi di MIME supportati](/help/assets/assets-formats.md#supported-mime-types) per un elenco dei valori dei parametri di elaborazione consentiti che puoi utilizzare per un determinato tipo di MIME.

1. Effettua una delle operazioni seguenti:

   * Ripeti i passaggi 3-4 per modificare altri tipi MIME.
   * Nella barra dei menu della pagina CRXDE Lite, tocca **[!UICONTROL Salva tutto]**.

1. Nell’angolo in alto a sinistra della pagina, tocca **[!UICONTROL CRXDE Lite]** per tornare all’Experience Manager.

#### Aggiunta di tipi MIME per i formati non supportati {#adding-mime-types-for-unsupported-formats}

In Experience Manager Assets puoi aggiungere tipi MIME personalizzati per i formati non supportati. Assicurati che qualsiasi nuovo nodo aggiunto in CRXDE Lite non venga eliminato per Experience Manager spostando il tipo MIME prima di `image_`. Inoltre, assicurati che il relativo valore abilitato sia impostato su **[!UICONTROL false]**.

**Per aggiungere tipi MIME per i formati non supportati:**

1. Ad Experience Manager, tocca **[!UICONTROL Strumenti]** > **[!UICONTROL Operazioni]** > **[!UICONTROL Console web]**.

   ![2019-08-02_16-13-14](assets/2019-08-02_16-13-14.png)

1. Viene visualizzata una nuova scheda del browser alla pagina **[!UICONTROL Configurazione della console Web Adobe Experience Manager]**.

   ![2019-08-02_16-17-29](assets/2019-08-02_16-17-29.png)

1. Nella pagina, scorri verso il basso fino al nome *Adobe CQ Scene7 Asset MIME type Service*, come illustrato nella schermata successiva. A destra del nome, tocca **[!UICONTROL Modifica i valori di configurazione]** (icona a forma di matita).

   ![2019-08-02_16-44-56](assets/2019-08-02_16-44-56.png)

1. Nella pagina **Adobe CQ Scene7 Asset MIME type Service** , tocca un’icona a forma di segno più &lt;+>. La posizione nella tabella in cui tocchi il segno più per aggiungere il nuovo tipo di MIME è insignificante.

   ![2019-08-02_16-27-27](assets/2019-08-02_16-27-27.png)

1. Digita `DWG=image/vnd.dwg` nel campo di testo vuoto appena aggiunto.

   L’esempio `DWG=image/vnd.dwg` è solo a scopo dimostrativo. Il tipo MIME che aggiungi qui può essere qualsiasi altro formato non supportato.

   ![2019-08-02_16-36-36](assets/2019-08-02_16-36-36.png)

1. Nell’angolo in basso a destra della pagina, tocca **[!UICONTROL Salva]**.

   A questo punto, è possibile chiudere la scheda del browser con la pagina di configurazione della console Web di Adobe Experience Manager aperta.

1. Torna alla scheda del browser con la console di Experience Manager aperta.
1. Ad Experience Manager, tocca **[!UICONTROL Strumenti]** > **[!UICONTROL Generale]** > **[!UICONTROL CRXDE Lite]**.

   ![2019-08-02_16-55-41](assets/2019-08-02_16-55-41.png)

1. Nella barra a sinistra, passa a quanto segue:

   `conf/global/settings/cloudconfigs/dmscene7/jcr:content/mimeTypes`

1. Trascina il tipo mime `image_vnd.dwg` e rilascialo direttamente sopra `image_` nell’albero come mostrato nella schermata seguente.

   ![crxdelite_cqdoc-14627](assets/crxdelite_cqdoc-14627.png)

1. Con il tipo mime `image_vnd.dwg` ancora selezionato, dalla scheda **[!UICONTROL Proprietà]** nella riga **[!UICONTROL abilitato]**, sotto l&#39;intestazione di colonna **[!UICONTROL Valore]**, tocca due volte il valore per aprire l&#39;elenco a discesa **[!UICONTROL Valore]**.
1. Digita `false` nel campo (oppure seleziona **[!UICONTROL false]** dall’elenco a discesa).

   ![2019-08-02_16-60-30](assets/2019-08-02_16-60-30.png)

1. Nell’angolo in alto a sinistra della pagina CRXDE Lite, tocca **[!UICONTROL Salva tutto]**.

#### Creazione di predefiniti per set di batch per generare automaticamente set di immagini e set 360 gradi {#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets}

Utilizza i predefiniti per set di batch per automatizzare la creazione di set di immagini o set 360 gradi durante il caricamento delle risorse in Dynamic Media.

Innanzitutto, definisci la convenzione di denominazione per il raggruppamento delle risorse in un set. Quindi crea un Batch Set Preset che è un set di istruzioni autonomo con nome univoco. Deve definire come creare il set utilizzando immagini che corrispondono alle convenzioni di denominazione definite nella composizione preimpostata.

Quando carichi dei file, Dynamic Media crea automaticamente un set con tutti i file che corrispondono alla convenzione di denominazione definita nei predefiniti attivi.

##### Configurazione della denominazione predefinita

Crea una convenzione di denominazione predefinita utilizzata in qualsiasi ricetta predefinita per set di batch. La convenzione di denominazione predefinita selezionata nella definizione del predefinito del set di batch è probabilmente tutto ciò che è necessario per la società per generare i set in batch. Viene creato un predefinito per set di batch per utilizzare la convenzione di denominazione predefinita definita dall’utente. È possibile creare un numero illimitato di predefiniti per set di batch con convenzioni di denominazione alternative e personalizzate necessarie per un determinato set di contenuti nei casi in cui vi sia un’eccezione alla denominazione predefinita definita dall’azienda.

Sebbene non sia necessaria l’impostazione di una convenzione di denominazione predefinita per utilizzare le funzionalità di preimpostazione di set di batch, è consigliabile utilizzare la convenzione di denominazione predefinita. Consente di definire tutti gli elementi della convenzione di denominazione che si desidera raggruppare in un set in modo da semplificare la creazione di set di batch.

In alternativa, è possibile utilizzare **[!UICONTROL Visualizza codice]** senza campi modulo disponibili. In questa visualizzazione puoi creare le definizioni delle convenzioni di denominazione utilizzando esclusivamente espressioni regolari.

Sono disponibili due elementi per la definizione, la corrispondenza e il nome di base. Questi campi consentono di definire tutti gli elementi di una convenzione di denominazione e identificare la parte della convenzione utilizzata per denominare il set in cui sono contenuti. La convenzione di denominazione individuale di un’azienda utilizza spesso una o più righe di definizione per ciascuno di questi elementi. Puoi utilizzare altrettante righe per la definizione univoca e raggrupparle in elementi distinti, ad esempio per l’immagine principale, l’elemento Colore, l’elemento Vista alternativa e l’elemento Campione.

**Per configurare la denominazione predefinita:**

1. Apri l&#39; [applicazione desktop Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started), quindi accedi al tuo account.

   Le credenziali e i dettagli di accesso sono stati forniti da Adobe al momento del provisioning. Se non si dispone di tali informazioni, contattare il supporto tecnico.

1. Nella barra di navigazione vicino alla parte superiore della pagina, tocca **[!UICONTROL Configurazione]** > **[!UICONTROL Impostazione applicazione]** > **[!UICONTROL Predefiniti set di batch]** > **[!UICONTROL Denominazione predefinita]**.
1. Per specificare come visualizzare e immettere le informazioni di ciascun elemento, seleziona **[!UICONTROL Visualizza modulo]** o **[!UICONTROL Visualizza codice]**.

   È possibile selezionare la casella di controllo **[!UICONTROL Visualizza codice]** per visualizzare il valore dell&#39;espressione regolare creato accanto alle selezioni del modulo. È possibile immettere o modificare questi valori per definire gli elementi della convenzione di denominazione, se la visualizzazione del modulo vi limita per qualsiasi motivo. Se i valori non possono essere analizzati nella visualizzazione modulo, i campi modulo diventano inattivi.

   >[!NOTE]
   I campi modulo disattivati non eseguono alcuna convalida per verificare che le espressioni regolari siano corrette. Vengono visualizzati i risultati dell’espressione regolare che si sta creando per ogni elemento dopo la riga Risultato. L’espressione regolare completa è visibile nella parte inferiore della pagina.

1. Espandi ogni elemento in base alle esigenze e immetti le convenzioni di denominazione che desideri utilizzare.
1. Se necessario, effettuare una delle seguenti operazioni:

   * Tocca **[!UICONTROL Aggiungi]** per aggiungere un’altra convenzione di denominazione per un elemento.
   * Tocca **[!UICONTROL Rimuovi]** per eliminare una convenzione di denominazione per un elemento.

1. Effettua una delle operazioni seguenti:

   * Tocca **[!UICONTROL Salva con nome]** e digita un nome per il predefinito.
   * Tocca **[!UICONTROL Salva]** se modifichi un predefinito esistente.

##### Creazione di un predefinito per set di batch

Dynamic Media utilizza i predefiniti per set di batch per organizzare le risorse in set di immagini (immagini alternative, opzioni colore, 360 giri) da visualizzare nei visualizzatori. I predefiniti per set di batch vengono eseguiti automaticamente insieme ai processi di caricamento delle risorse in Dynamic Media.

Puoi creare, modificare e gestire i predefiniti per set di batch. Esistono due forme di definizioni di predefiniti per set di batch: uno per una convenzione di denominazione predefinita che è possibile impostare e uno per le convenzioni di denominazione personalizzate create al volo.

È possibile utilizzare il metodo campo modulo per definire un predefinito per set di batch o il metodo del codice, che consente di utilizzare espressioni regolari. Come per la denominazione predefinita, è possibile scegliere Visualizza codice nello stesso momento in cui si sta definendo nella visualizzazione modulo e utilizzare espressioni regolari per creare le definizioni. In alternativa, puoi deselezionare entrambe le visualizzazioni per utilizzare esclusivamente l’una o l’altra.

**Per creare un predefinito per set di batch:**

1. Apri l&#39; [applicazione desktop Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started), quindi accedi al tuo account.

   Le credenziali e i dettagli di accesso sono stati forniti da Adobe al momento del provisioning. Se non si dispone di tali informazioni, contattare il supporto tecnico.

1. Nella barra di navigazione vicino alla parte superiore della pagina, tocca **[!UICONTROL Configurazione]** > **[!UICONTROL Impostazione applicazione]** > **[!UICONTROL Predefiniti set di batch]** > **[!UICONTROL Predefinito set di batch]**.

   **[!UICONTROL Visualizza modulo]**, nell’angolo superiore destro della pagina Dettagli, è la visualizzazione predefinita.

1. Nel pannello Elenco predefiniti, tocca **[!UICONTROL Aggiungi]** per attivare i campi di definizione nel pannello Dettagli sul lato destro dello schermo.
1. Nel pannello Dettagli, nel campo Nome predefinito , digita un nome per il predefinito.
1. Selezionare un tipo di predefinito dal menu a discesa Tipo set di batch.
1. Effettua una delle operazioni seguenti:

   * Se utilizzi una convenzione di denominazione predefinita impostata in precedenza in **[!UICONTROL Impostazione applicazione]** > **[!UICONTROL Predefiniti set di batch]** > **[!UICONTROL Denominazione predefinita]**, espandi **[!UICONTROL Convenzioni di denominazione delle risorse]**, quindi tocca **[!UICONTROL Predefinito]** nell’elenco a discesa Denominazione file.

   * Per definire una nuova convenzione di denominazione durante la configurazione del predefinito, espandi **[!UICONTROL Convenzioni di denominazione delle risorse]**, quindi tocca **[!UICONTROL Personalizzato]** nell’elenco a discesa Denominazione file .

1. Per Ordine di sequenza, definite l&#39;ordine in cui le immagini vengono visualizzate dopo il raggruppamento del set in Dynamic Media.

   Per impostazione predefinita, le risorse vengono ordinate in modo alfanumerico. Tuttavia, per definire l’ordine è possibile utilizzare un elenco di espressioni regolari separate da virgola.

1. Per Imposta convenzione di denominazione e creazione, specifica il suffisso o il prefisso al nome di base definito nella convenzione di denominazione delle risorse. Inoltre, definisci dove viene creato il set all’interno della struttura di cartelle Dynamic Media.

   Se definisci un numero elevato di set, mantieni i set separati dalle cartelle contenenti le risorse stesse. Ad esempio, crea una cartella Set di immagini e inserisci qui i set generati.

1. Nel pannello Dettagli, tocca **[!UICONTROL Salva]**.
1. Tocca **[!UICONTROL Attivo]** accanto al nuovo nome del predefinito.

   L’attivazione del predefinito assicura che quando carichi le risorse in Dynamic Media, il Batch Set Preset venga applicato per generare il set.

##### Creazione di un set di batch predefinito per la generazione automatica di un set 360 gradi 2D

È possibile utilizzare il tipo di set di batch **[!UICONTROL Set 360 gradi a più assi]** per creare una ricetta che automatizza la generazione di set 360 gradi 2D. Il raggruppamento delle immagini utilizza espressioni regolari Riga e Colonna in modo che le risorse immagine siano correttamente allineate nella posizione corrispondente nell’array multidimensionale. Non esiste un numero minimo o massimo di righe o colonne che è necessario avere in un set 360 gradi a più assi.

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

Il raggruppamento per la parte del nome della risorsa condivisa del set 360 gradi viene aggiunto al campo **[!UICONTROL Match]** (Corrispondenza) (come evidenziato). La parte variabile del nome della risorsa, contenente la riga e la colonna, viene aggiunta rispettivamente ai campi **[!UICONTROL Riga]** e **[!UICONTROL Colonna]**.

Quando il set 360 gradi viene caricato e pubblicato, puoi attivare il nome della definizione del set 360 gradi 2D che è riportato in **[!UICONTROL Predefiniti set di batch]**, nella finestra di dialogo **[!UICONTROL Opzioni processo di caricamento]**.

**Per creare un Batch Set Preset per la generazione automatica di un Set 360 gradi 2D:**

1. Apri l&#39; [applicazione desktop Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started), quindi accedi al tuo account.

   Le credenziali e i dettagli di accesso sono stati forniti da Adobe al momento del provisioning. Se non si dispone di tali informazioni, contattare il supporto tecnico.

1. Nella barra di navigazione vicino alla parte superiore della pagina, tocca **[!UICONTROL Configurazione]** > **[!UICONTROL Impostazione applicazione]** > **[!UICONTROL Predefiniti set di batch]** > **[!UICONTROL Predefinito set di batch]**.

   **[!UICONTROL Visualizza modulo]**, nell’angolo superiore destro della pagina Dettagli, è la visualizzazione predefinita.

1. Nel pannello Elenco predefiniti, tocca **[!UICONTROL Aggiungi]** per attivare i campi di definizione nel pannello Dettagli sul lato destro dello schermo.
1. Nel pannello Dettagli, nel campo Nome predefinito , digita un nome per il predefinito.
1. Nel menu a discesa Tipo set di batch, seleziona **[!UICONTROL Set risorse]**.
1. Nell’elenco a discesa Tipo secondario , seleziona **[!UICONTROL Set 360 gradi con più assi]**.
1. Espandi **[!UICONTROL Convenzioni di denominazione delle risorse]**, quindi tocca **[!UICONTROL Personalizzato]** nell’elenco a discesa Denominazione file .
1. Utilizza gli attributi **[!UICONTROL Match (Corrispondenza)]** e, facoltativamente, **[!UICONTROL Nome base]** per definire un’espressione regolare per la denominazione delle risorse dell’immagine che compongono il raggruppamento.

   Ad esempio, l’espressione regolare Corrispondenza letterale può avere un aspetto simile al seguente:

   `(w+)-w+-w+`

1. Espandi **[!UICONTROL Posizione colonna riga]**, quindi definisci il formato del nome per la posizione della risorsa immagine all’interno della matrice set 360 gradi 2D.

   Utilizzare le parentesi per abbracciare la posizione della riga o della colonna nel nome del file.

   Ad esempio, per l’espressione regolare della riga, può avere un aspetto simile al seguente:

   `\w+-R([0-9]+)-\w+`

   o

   `\w+-(\d+)-\w+`

   Per l’espressione regolare della colonna, può essere simile al seguente:

   `\w+-\w+-C([0-9]+)`

   o

   `\w+-\w+-C(\d+)`

   I campioni di cui sopra sono solo a scopo dimostrativo. Puoi creare l’espressione regolare in base alle tue esigenze.

   >[!NOTE]
   Se la combinazione di espressioni regolari per riga e colonna non è in grado di determinare la posizione della risorsa all’interno della matrice del set 360 gradi multidimensionale, la risorsa non viene aggiunta al set. Viene registrato anche un errore.

1. Per Imposta convenzione di denominazione e creazione, specifica il suffisso o il prefisso al nome di base definito nella convenzione di denominazione delle risorse.

   Inoltre, definisci dove viene creato il set 360 gradi all’interno della struttura di cartelle di Dynamic Media Classic.

   Se definisci un numero elevato di set, mantieni i set separati dalle cartelle contenenti le risorse stesse. Ad esempio, crea una cartella Set 360 gradi in cui inserire i set generati.

1. Nel pannello Dettagli, tocca **[!UICONTROL Salva]**.
1. Tocca **[!UICONTROL Attivo]** accanto al nuovo nome del predefinito.

   L’attivazione del predefinito assicura che quando carichi le risorse in Dynamic Media, il Batch Set Preset venga applicato per generare il set.

### (Facoltativo) Ottimizzazione delle prestazioni di Dynamic Media - Modalità Scene7 {#optional-tuning-the-performance-of-dynamic-media-scene-mode}

Per mantenere la modalità Dynamic Media - Scene7 in esecuzione senza problemi, l&#39;Adobe consiglia i seguenti suggerimenti per l&#39;ottimizzazione delle prestazioni/della scalabilità di sincronizzazione:

* Aggiornamento dei parametri di processo predefiniti per l&#39;elaborazione di diversi formati di file.
* Aggiornamento dei thread di lavoro predefiniti del flusso di lavoro Granite (risorse video) in coda.
* Aggiornamento dei thread di lavoro temporanei di coda predefiniti del flusso di lavoro Granite (immagini e risorse non video).
* Aggiornamento delle connessioni di caricamento massime nel server Dynamic Media Classic.

#### Aggiornamento dei parametri di processo predefiniti per l&#39;elaborazione di diversi formati di file

Puoi ottimizzare i parametri dei processi per velocizzarne l’elaborazione quando carichi i file. Ad esempio, se carichi i file PSD ma non desideri elaborarli come modelli, puoi impostare l’estrazione del livello su false (disattivato). In questo caso, il parametro del processo di sintonizzazione viene visualizzato come segue: `process=None&createTemplate=false`.

Se desideri attivare la creazione di modelli, utilizza i seguenti parametri: `process=MaintainLayers&layerNaming=AppendName&createTemplate=true`.

<!-- THIS PARAGRAPH WAS REPLACED WITH THE TWO PARAGRAPHS DIRECTLY ABOVE BASED ON CQDOC-17657 You can tune job parameters for faster processing when you upload files. For example, if you are uploading PSD files, but do not want to process them as templates, you can set layer extraction to false (off). In such case, the tuned job parameter would appear as `process=None&createTemplate=false`. -->

L&#39;Adobe consiglia di utilizzare i seguenti parametri di processo &quot;sintonizzati&quot; per i file PDF, PostScript® e PSD:

<!-- OLD PDF JOB PARAMETERS `pdfprocess=Rasterize&resolution=150&colorspace=Auto&pdfbrochure=false&keywords=false&links=false` -->

<!-- OLD POSTSCRIPT JOB PARAMETERS `psprocess=Rasterize&psresolution=150&pscolorspace=Auto&psalpha=false&psextractsearchwords=false&aiprocess=Rasterize&airesolution=150&aicolorspace=Auto&aialpha=false` -->

| Tipo di file | Parametri di lavoro consigliati |
| ---| ---|
| PDF | `pdfprocess=Thumbnail&resolution=150&colorspace=Auto&pdfbrochure=false&keywords=false&links=false` |
| PostScript® | `psprocess=Rasterize&psresolution=150&pscolorspace=Auto&psalpha=false&psextractsearchwords=false&aiprocess=Thumbnail&airesolution=150&aicolorspace=Auto&aialpha=false` |
| PSD | `process=None&layerNaming=AppendName&anchor=Center&createTemplate=false&extractText=false&extendLayers=false` |

<!-- CQDOC-17657 for PSD entry in table above -->

Per aggiornare uno qualsiasi di questi parametri, segui i passaggi descritti in [Abilitazione del supporto dei parametri di processo di caricamento di Dynamic Media Classic/Assets basato su tipi MIME](/help/sites-administering/scene7.md#enabling-mime-type-based-assets-scene-upload-job-parameter-support).

#### Aggiornamento della coda del flusso di lavoro transitorio di Granite {#updating-the-granite-transient-workflow-queue}

La coda del flusso di lavoro di transito Granite viene utilizzata per il flusso di lavoro **[!UICONTROL Aggiorna risorsa DAM]** . In Dynamic Media viene utilizzato per l’acquisizione e l’elaborazione delle immagini.

**Per aggiornare la coda del flusso di lavoro transitorio di Granite:**

1. Vai su [https://&lt;server>/system/console/configMgr](https://localhost:4502/system/console/configMgr) e cerca **Coda: Coda flusso di lavoro transitorio Granite**.

   >[!NOTE]
   È necessaria una ricerca di testo invece di un URL diretto perché il PID OSGi viene generato in modo dinamico.

1. Nel campo **[!UICONTROL Processi paralleli massimi]** , modifica il numero nel valore desiderato.

   Puoi aumentare **[!UICONTROL Processi paralleli massimi]** per supportare in modo adeguato il caricamento di file pesanti in Dynamic Media. Il valore esatto dipende dalla capacità hardware. In alcuni scenari, ovvero una migrazione iniziale o un caricamento in serie una tantum, puoi utilizzare un valore elevato. Tuttavia, l’utilizzo di un valore elevato (come il doppio del numero di core) può avere effetti negativi su altre attività simultanee. Di conseguenza, verifica e regola il valore in base al tuo caso d’uso specifico.

<!--    By default, the maximum number of parallel jobs depends on the number of available CPU cores. For example, on a 4-core server, it assigns 2 worker threads. (A value between 0.0 and 1.0 is ratio based, or any numbers greater than 1 will assign the number of worker threads.)

   Adobe recommends that 32 **[!UICONTROL Maximum Parallel Jobs]** be configured to adequately support heavy upload of files to Dynamic Media Classic (Scene7). -->

![chlimage_1](assets/chlimage_1.jpeg)

1. Tocca **[!UICONTROL Salva]**.

#### Aggiornamento della coda del flusso di lavoro Granite {#updating-the-granite-workflow-queue}

La coda del flusso di lavoro Granite viene utilizzata per i flussi di lavoro non transitori. In Dynamic Media, veniva utilizzato per elaborare i video con il flusso di lavoro **[!UICONTROL Codifica video Dynamic Media]** .

**Per aggiornare la coda del flusso di lavoro Granite:**

1. Passa a `https://<server>/system/console/configMgr` e cerca **Coda: Coda flusso di lavoro Granite**.

   >[!NOTE]
   È necessaria una ricerca di testo invece di un URL diretto perché il PID OSGi viene generato in modo dinamico.

1. Nel campo **[!UICONTROL Processi paralleli massimi]** , modifica il numero nel valore desiderato.

   Puoi aumentare il numero massimo di processi paralleli per supportare in modo adeguato il caricamento di file pesanti in Dynamic Media. Il valore esatto dipende dalla capacità hardware. In alcuni scenari, ovvero una migrazione iniziale o un caricamento in serie una tantum, puoi utilizzare un valore elevato. Tuttavia, l’utilizzo di un valore elevato (come il doppio del numero di core) può avere effetti negativi su altre attività simultanee. Di conseguenza, verifica e regola il valore in base al tuo caso d’uso specifico.

   ![chlimage_1-1](assets/chlimage_1-1.jpeg)

1. Tocca **[!UICONTROL Salva]**.

#### Aggiornamento della connessione di caricamento Dynamic Media Classic {#updating-the-scene-upload-connection}

L’impostazione Scene7 Upload Connection sincronizza le risorse di Experience Manager con i server Dynamic Media Classic.

**Per aggiornare la connessione di caricamento Dynamic Media Classic:**

1. Accedi a `https://<server>/system/console/configMgr/com.day.cq.dam.scene7.impl.Scene7UploadServiceImpl`
1. Nel campo **[!UICONTROL Numero di connessioni]** e/o nel campo **[!UICONTROL Timeout processo attivo]**, cambia il numero come desiderato.

   L&#39;impostazione **[!UICONTROL Numero di connessioni]** controlla il numero massimo di connessioni HTTP consentite, ad Experience Manager per il caricamento in Dynamic Media; in genere, il valore predefinito di dieci connessioni è sufficiente.

   L’impostazione **[!UICONTROL Timeout processo attivo]** determina il tempo di attesa per la pubblicazione delle risorse Dynamic Media caricate nel server di consegna. Per impostazione predefinita, questo valore è di 2100 secondi o 35 minuti.

   Per la maggior parte dei casi d’uso, è sufficiente impostare 2100.

   ![chlimage_1-2](assets/chlimage_1-2.jpeg)

1. Tocca **[!UICONTROL Salva]**.

### (Facoltativo) Filtraggio delle risorse per la replica {#optional-filtering-assets-for-replication}

Nelle implementazioni non Dynamic Media, replichi tutte le risorse *tutte* (sia immagini che video) dall’ambiente di authoring di Experience Manager al nodo Pubblicazione di Experience Manager. Questo flusso di lavoro è necessario perché anche i server di pubblicazione Experience Manager distribuiscono le risorse.

Tuttavia, nelle implementazioni di Dynamic Media, poiché le risorse vengono distribuite tramite il Cloud Service, non è necessario replicare le stesse risorse nei nodi di pubblicazione di Experience Manager. Questo flusso di lavoro &quot;pubblicazione ibrida&quot; evita costi di storage aggiuntivi e tempi di elaborazione più lunghi per la replica delle risorse. Altri contenuti, come le pagine del sito, continuano a essere serviti dai nodi di pubblicazione di Experience Manager.

I filtri ti consentono di *escludere* risorse dalla replica nel nodo di pubblicazione Experience Manager.

#### Utilizzo di filtri risorse predefiniti per la replica {#using-default-asset-filters-for-replication}

Se utilizzi Dynamic Media per l’imaging, il video o entrambi, puoi utilizzare i filtri predefiniti forniti da Adobe così come sono. I seguenti filtri sono attivi per impostazione predefinita:

|  | Filtro | Tipo MIME | Rappresentazioni |
| --- | --- | --- | --- |
| Consegna immagini Dynamic Media | filter-image<br>set di filtri | Inizia con **image/**<br> Contains **applications/** e termina con **set**. | I &quot;filtri-images&quot; preconfigurati (si applicano alle risorse di immagini singole, comprese le immagini interattive) e i &quot;set di filtri&quot; (si applica ai set 360 gradi, ai set di immagini, ai set di file multimediali diversi e ai set di caroselli) escluderanno dalla replica le rappresentazioni originali dell’immagine e delle immagini statiche.<br> |
| Distribuzione video Dynamic Media | filter-video | Inizia con **video/** | Il &quot;filtro video&quot; predefinito:<br> ・ escludere dalla replica le rappresentazioni video originali e le miniature statiche. |

>[!NOTE]
I filtri si applicano ai tipi MIME e non possono essere specifici del percorso.

#### Personalizzazione dei filtri delle risorse per la replica {#customizing-asset-filters-for-replication}

1. Ad Experience Manager, tocca il logo Experience Manager per accedere alla console di navigazione globale e tocca **[!UICONTROL Strumenti]** > **[!UICONTROL Generale]** > **[!UICONTROL CRXDE Lite]**.
1. Nella struttura ad albero delle cartelle a sinistra, passa a `/etc/replication/agents.author/publish/jcr:content/damRenditionFilters` per controllare i filtri.

   ![chlimage_1-17](assets/chlimage_1-2.png)

1. Per definire il tipo di MIME per il filtro, potete individuare il tipo di MIME come segue:

   Nella barra a sinistra, espandi `content > dam > <locate_your_asset> > jcr:content > metadata`, quindi individua `dc:format` nella tabella.

   L’immagine seguente è un esempio del percorso di una risorsa a `dc:format`.

   ![chlimage_1-18](assets/chlimage_1-3.png)

   Nota che il `dc:format` per la risorsa `Fiji Red.jpg` è `image/jpeg`.

   Affinché questo filtro sia applicato a tutte le immagini, indipendentemente dal formato, imposta il valore su `image/*` dove `*` è un&#39;espressione regolare applicata a tutte le immagini di qualsiasi formato.

   Per applicare il filtro solo alle immagini di tipo JPEG, immetti un valore di `image/jpeg`.

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

   Se desideri replicare solo l’originale, immetti `+original`.
