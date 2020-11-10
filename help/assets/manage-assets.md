---
title: Gestione delle risorse digitali
description: Scopri le attività di gestione delle risorse come caricare, scaricare, modificare, cercare, eliminare, annotare e aggiornare le risorse digitali.
contentOwner: AG
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: 12c56c27c7f97f1029c757ec6d28f482516149d0
workflow-type: tm+mt
source-wordcount: '9565'
ht-degree: 4%

---


# Gestione delle risorse digitali {#manage-digital-assets}

In [!DNL Adobe Experience Manager Assets] questo documento potete fare di più che semplicemente archiviare e governare le risorse. [!DNL Experience Manager] offre funzionalità di gestione delle risorse di livello aziendale. Potete modificare e condividere le risorse, eseguire ricerche avanzate, creare più rappresentazioni di dozzine di formati di file supportati, gestire versioni e diritti digitali, automatizzare l’elaborazione delle risorse, gestire e governare i metadati, collaborare utilizzando le annotazioni e molto altro ancora.

Questo articolo descrive le attività di base per la gestione delle risorse, come ad esempio creare o caricare; aggiornamenti dei metadati; copiare, spostare ed eliminare; pubblicare, annullare la pubblicazione ed eseguire ricerche nelle risorse. Per comprendere l’interfaccia utente, consulta [Introduzione all’interfaccia](/help/sites-authoring/basic-handling.md)utente delle risorse. Per gestire i frammenti di contenuto, consulta [Gestione delle risorse Frammenti](/help/assets/content-fragments/content-fragments-managing.md) di contenuto.

## Creare le cartelle {#creating-folders}

Quando organizzate una raccolta di risorse, ad esempio tutte `Nature` le immagini, potete creare delle cartelle per mantenerle unite. Potete usare le cartelle per classificare e organizzare le risorse. [!DNL Experience Manager Assets] non richiede l’organizzazione di risorse in cartelle per migliorare il funzionamento.

>[!NOTE]
>
>* La condivisione di una [!DNL Assets] cartella di tipo `sling:OrderedFolder` non è supportata quando si condivide un Marketing Cloud. Se desiderate condividere una cartella, non selezionate [!UICONTROL Ordinato] al momento della creazione di una cartella.
>* [!DNL Experience Manager] non consente l&#39;utilizzo di `subassets` word come nome di una cartella. È una parola chiave riservata al nodo che contiene risorse secondarie per le risorse composte.


1. Andate alla posizione nella cartella delle risorse digitali in cui desiderate creare una nuova cartella. Nel menu, fate clic su **[!UICONTROL Crea]**. Selezionate **[!UICONTROL Nuova cartella]**.
1. Nel campo **[!UICONTROL Titolo]** , inserite un nome di cartella. Per impostazione predefinita, DAM utilizza il titolo fornito come nome della cartella. Una volta creata la cartella, potete ignorare l’impostazione predefinita e specificare un altro nome di cartella.
1. Fai clic su **[!UICONTROL Crea]**. La cartella viene visualizzata nella cartella delle risorse digitali.

I seguenti caratteri (elenco separato da spazi) non sono supportati:

* Il nome di un file di risorsa non può contenere i seguenti caratteri: `* / : [ \\ ] | # % { } ? &`
* Il nome di una cartella di risorse non può contenere i seguenti caratteri: `* / : [ \\ ] | # % { } ? \" . ^ ; + & \t`

Non includete caratteri speciali nelle estensioni dei nomi file delle risorse.

## Upload assets {#uploading-assets}

<!-- TBD the following:
Move this section into a new article. CQDOC-14874 ticket is created for this.
In this complete article, replace emphasis with UICONTROL where appropriate.
-->

Potete caricare vari tipi di risorse (immagini, file PDF, file RAW e così via) dalla cartella locale o da un’unità di rete a [!DNL Experience Manager Assets].

>[!NOTE]
>
>In modalità Dynamic Media - Scene7, potete caricare solo risorse di dimensioni file pari o inferiori a 2 GB.

Potete scegliere di caricare le risorse nelle cartelle a cui è stato assegnato o meno un profilo di elaborazione.

Per le cartelle a cui è assegnato un profilo di elaborazione, il nome del profilo viene visualizzato sulla miniatura nella vista a schede. Nella vista a elenco, il nome del profilo viene visualizzato nella colonna Profilo **di** elaborazione. Consultate Profili [](/help/assets/processing-profiles.md)di elaborazione.

Prima di caricare una risorsa, assicuratevi che sia in un [formato](/help/assets/assets-formats.md) che [!DNL Experience Manager Assets] supporti.

1. Nell’interfaccia [!DNL Assets] utente, individuate il percorso in cui desiderate aggiungere le risorse digitali.
1. Per caricare le risorse, effettuate una delle seguenti operazioni:

   * Sulla barra degli strumenti, fate clic su **[!UICONTROL Crea]**. Scegliere **[!UICONTROL File dal menu]**. Se necessario, potete rinominare il file nella finestra di dialogo visualizzata.
   * In un browser che supporta HTML5, trascinate le risorse direttamente sull’interfaccia [!DNL Assets] utente. La finestra di dialogo per rinominare il file non viene visualizzata.

   ![Opzione Crea per caricare le risorse](assets/create-options.png)

   Per selezionare più file, premete il tasto Ctrl o Comando e selezionate le risorse nella finestra di dialogo del selettore file. Quando usate un iPad, potete selezionare un solo file alla volta.

   Potete mettere in pausa il caricamento di risorse di grandi dimensioni (superiori a 500 MB) e riprenderlo più tardi dalla stessa pagina. Fate clic su **[!UICONTROL Pausa]** accanto alla barra di avanzamento che viene visualizzata all’avvio del caricamento.

   ![Barra di avanzamento del caricamento delle risorse](assets/upload-progress-bar.png)

È possibile configurare la dimensione sopra la quale una risorsa viene considerata una risorsa grande. Ad esempio, potete configurare il sistema affinché consideri le risorse superiori ai 1000 MB (invece dei 500 MB) come risorse grandi. In questo caso, **[!UICONTROL la pausa]** viene visualizzata sulla barra di avanzamento quando vengono caricate risorse di dimensioni superiori a 1000 MB.

Il pulsante Pausa non viene visualizzato se un file maggiore di 1000 MB viene caricato con un file inferiore a 1000 MB. Tuttavia, se annullate il caricamento di file di dimensioni inferiori a 1000 MB, viene visualizzato il pulsante **[!UICONTROL Pausa]** .

Per modificare il limite di dimensioni, configurare la `chunkUploadMinFileSize` proprietà del `fileupload`nodo nell&#39;archivio CRX.

Quando fate clic su **[!UICONTROL Pausa]**, viene attivata l’opzione **[!UICONTROL Riproduci]** . Per riprendere il caricamento, fate clic su **[!UICONTROL Riproduci]**.

![Riprendere il caricamento della risorsa in pausa](assets/resume-paused-upload.png)

Per annullare un caricamento in corso, fate clic su Chiudi (`X`) accanto alla barra di avanzamento. Quando annullate l’operazione di caricamento, [!DNL Assets] elimina la parte parzialmente caricata della risorsa.

La possibilità di riprendere il caricamento è particolarmente utile in situazioni con larghezza di banda ridotta e problemi di rete, in cui il caricamento di una risorsa di grandi dimensioni richiede molto tempo. Potete mettere in pausa l’operazione di caricamento e continuare in seguito quando la situazione migliora. Quando si riprende, il caricamento inizia dal punto in cui è stato messo in pausa.

Durante l’operazione di caricamento, [!DNL Experience Manager] salva le porzioni della risorsa caricata come blocchi di dati nell’archivio CRX. Al termine del caricamento, [!DNL Experience Manager] consolida questi blocchi in un singolo blocco di dati nell’archivio.

Per configurare l’attività di pulizia per i processi di caricamento dei blocchi non ancora completati, passate a `https://[aem_server]:[port]/system/console/configMgr/org.apache.sling.servlets.post.impl.helper.ChunkCleanUpTask`.

>[!CAUTION]
>
>Il valore predefinito quando viene attivato il caricamento del blocco è 500 MB e la dimensione del blocco è 50 MB. Se modificate [Apache Jackrabbit Oak TokenConfiguration](https://helpx.adobe.com/experience-manager/kb/How-to-set-token-session-expiration-AEM.html) in modo da impostare `timeout configuration` un valore inferiore al tempo necessario per il caricamento di una risorsa, potete incontrare una situazione di timeout sessione mentre è in corso il caricamento della risorsa. Pertanto, è necessario modificare l’ `chunkUploadMinFileSize` e `chunksize`, in modo che ogni richiesta di blocco aggiorni la sessione.
>
>In considerazione del timeout della scadenza delle credenziali, della latenza, della larghezza di banda e dei caricamenti simultanei previsti, il valore più alto che consente di garantire che vengano selezionati i seguenti elementi:
>
>* Per fare in modo che il caricamento dei blocchi sia abilitato per i file con dimensioni tali da causare la scadenza delle credenziali durante il caricamento.
   >
   >
* Per assicurarsi che ogni blocco venga completato prima della scadenza della credenziale.


Se caricate una risorsa con lo stesso nome di una già disponibile nel percorso in cui state caricando la risorsa, viene visualizzata una finestra di dialogo di avviso.

Potete scegliere di sostituire una risorsa esistente, crearne un’altra o tenerle entrambe rinominando la nuova risorsa caricata. Se sostituite una risorsa esistente, i metadati della risorsa e le eventuali modifiche precedenti (ad esempio, annotazione o ritaglio) apportate alla risorsa esistente vengono eliminati. Se scegliete di mantenere entrambe le risorse, la nuova risorsa viene rinominata con un numero `1` aggiunto al nome.

![Finestra di dialogo Conflitto nome per risolvere il conflitto tra i nomi delle risorse](assets/resolve-naming-conflict.png)

>[!NOTE]
>
>Quando selezionate **[!UICONTROL Sostituisci]** nella finestra di dialogo Conflitto  nome, l’ID risorsa viene rigenerato per la nuova risorsa. Questo ID è diverso dall’ID della risorsa precedente.
>
>Se Asset Insights è abilitato per tenere traccia di impression/clic con  Adobe Analytics, l’ID risorsa rigenerato invalida i dati acquisiti per la risorsa in Analytics.

Se la risorsa caricata esiste in [!DNL Assets], la finestra di dialogo **[!UICONTROL Duplicati rilevati]** avvisa che state tentando di caricare una risorsa duplicata. La finestra di dialogo viene visualizzata solo se il valore `SHA 1` checksum del binario della risorsa esistente corrisponde al valore checksum della risorsa caricata. In questo caso, i nomi delle risorse non contano.

>[!NOTE]
>
>La finestra di dialogo [!UICONTROL Duplicati rilevati] viene visualizzata solo quando è attivata la funzione di rilevamento duplicati. Per abilitare la funzione di rilevamento dei duplicati, consultate [Abilitare il rilevamento](/help/assets/duplicate-detection.md)dei duplicati.

![Finestra di dialogo Duplica risorsa rilevata](assets/duplicate-asset-detected.png)

Per mantenere la risorsa duplicata in [!DNL Assets], fate clic su **[!UICONTROL Mantieni]**. Per eliminare la risorsa duplicata caricata, fate clic su **[!UICONTROL Elimina]**.

[!DNL Experience Manager Assets] impedisce il caricamento di risorse con i caratteri proibiti nel nome del file. Se provate a caricare una risorsa con un nome file contenente un carattere non consentito o più, [!DNL Assets] visualizza un messaggio di avviso e interrompe il caricamento fino a quando non rimuovete questi caratteri o lo caricate con un nome consentito.

Per rispettare convenzioni di denominazione dei file specifiche per la vostra azienda, la finestra di dialogo [!UICONTROL Carica risorse] consente di specificare nomi lunghi per i file caricati.

Tuttavia, i seguenti caratteri (elenco separato da spazi) non sono supportati:

* il nome del file di risorse non deve contenere `* / : [ \\ ] | # % { } ? &`
* il nome della cartella di risorse non deve contenere `* / : [ \\ ] | # % { } ? \" . ^ ; + & \t`

Non includete caratteri speciali nelle estensioni dei nomi file delle risorse.

![La finestra di dialogo di avanzamento del caricamento mostra lo stato dei file e dei file caricati correttamente che non possono essere caricati](assets/bulk-upload-progress.png)

Inoltre, l’interfaccia [!DNL Assets] utente mostra la risorsa più recente caricata o la cartella creata per la prima volta.

Se annullate l’operazione di caricamento prima del caricamento dei file, [!DNL Assets] interrompe il caricamento del file corrente e aggiorna il contenuto. Tuttavia, i file già caricati non vengono eliminati.

Nella finestra di dialogo di avanzamento del caricamento [!DNL Assets] viene visualizzato il numero di file caricati correttamente e i file che non sono stati caricati correttamente.

### Caricamenti seriali {#serialuploads}

Il caricamento di numerose risorse in massa richiede notevoli risorse di I/O, il che potrebbe avere un impatto negativo sulle prestazioni della [!DNL Assets] distribuzione. In particolare, se si dispone di una connessione Internet lenta, il tempo di caricamento aumenta drasticamente a causa di un picco di I/O del disco. Inoltre, il browser Web potrebbe introdurre ulteriori restrizioni al numero di richieste di POST [!DNL Assets] che possono essere gestite per il caricamento simultaneo di risorse. Di conseguenza, l’operazione di caricamento non riesce o si interrompe prematuramente. In altre parole, [!DNL Experience Manager Assets] potrebbe mancare alcuni file durante l&#39;acquisizione di un gruppo di file o non riuscire completamente a caricare alcun file.

Per ovviare a questa situazione, [!DNL Assets] durante un’operazione di caricamento in blocco viene inserita una risorsa alla volta (caricamento seriale), anziché tutte le risorse.

Per impostazione predefinita, il caricamento seriale delle risorse è attivato. Per disattivare la funzione e consentire il caricamento simultaneo, sovrapponete il `fileupload` nodo in Crx-de e impostate il valore della `parallelUploads` proprietà su `true`.

### Caricare le risorse mediante FTP {#uploading-assets-using-ftp}

Dynamic Media consente il caricamento batch delle risorse tramite server FTP. Se intendete caricare risorse di grandi dimensioni (>1 GB) o intere cartelle e sottocartelle, utilizzate l’FTP. Potete anche impostare il caricamento FTP in modo che avvenga su base programmata ricorrente.

>[!NOTE]
>
>In modalità Dynamic Media - Scene7, potete caricare solo risorse di dimensioni file pari o inferiori a 2 GB.

>[!NOTE]
>
>Per caricare le risorse tramite FTP in modalità Dynamic Media - Scene7, installate Feature Pack 18912 sulle istanze dell&#39; [!DNL Experience Manager] autore. Contatta [Assistenza](https://helpx.adobe.com/it/contact/enterprise-support.ec.html) clienti del Adobe per accedere al FP-18912 e completare la configurazione del tuo account FTP. Per ulteriori informazioni, consultate [Installare feature pack 18912 per la migrazione](/help/assets/bulk-ingest-migrate.md)in massa delle risorse.
>
>Se utilizzate l’FTP per caricare le risorse, le impostazioni di caricamento specificate in [!DNL Experience Manager] vengono ignorate. Vengono invece utilizzate le regole di elaborazione dei file, come definite in Dynamic Media Classic.

**Per caricare le risorse tramite FTP**

1. Utilizzando il client FTP desiderato, effettuate l&#39;accesso al server FTP utilizzando il nome utente e la password FTP ricevuti dall&#39;e-mail di provisioning. Nel client FTP, caricate i file o le cartelle sul server FTP.
1. [Accedete a Dynamic Media Classic](https://www.adobe.com/marketing-cloud/experience-manager/scene7-login.html) utilizzando le credenziali ricevute dall&#39;e-mail di provisioning. Nella barra di navigazione globale, fate clic su **[!UICONTROL Carica]**.

1. Nella pagina Carica, accanto all’angolo in alto a sinistra, fate clic sulla scheda **[!UICONTROL Mediante FTP]** .
1. Sul lato sinistro della pagina, scegliete una cartella FTP da cui caricare i file; sul lato destro della pagina, scegliete una cartella di destinazione.
1. Nell’angolo inferiore destro della pagina, fate clic su Opzioni **** processo e impostate le opzioni desiderate in base alle risorse nella cartella selezionata.

   Consultate Opzioni [processo di](#upload-job-options)caricamento.

   >[!NOTE]
   >
   >Quando caricate le risorse tramite FTP, le opzioni di caricamento impostate in Dynamic Media Classic (S7) hanno la precedenza rispetto ai parametri di elaborazione delle risorse impostati in [!DNL Experience Manager].

1. Nell’angolo inferiore destro della finestra di dialogo Opzioni processo di caricamento, fate clic su **[!UICONTROL Salva]**.
1. Nell’angolo inferiore destro della pagina Carica, fate clic su **[!UICONTROL Invia caricamento]**.

   Per visualizzare l’avanzamento del caricamento, nella barra di navigazione globale fate clic su **[!UICONTROL Processi]**. Nella pagina Processi viene visualizzato l’avanzamento del caricamento. Potete continuare a lavorare [!DNL Experience Manager] e tornare alla pagina Processi in Dynamic Media Classic in qualsiasi momento per controllare un processo in corso.
Per annullare un processo di caricamento in corso, fate clic su **[!UICONTROL Annulla]** accanto alla durata.

#### Opzioni processo di caricamento {#upload-job-options}

| Opzione Carica | Sottoopzione | Descrizione |
|---|---|---|
| Nome processo |  | Il nome predefinito precompilato nel campo di testo include la parte del nome immessa dall&#39;utente e la data e l&#39;ora. Per questo processo di caricamento potete usare il nome predefinito o immettere un nome personalizzato per la creazione. <br>Il processo e gli altri processi di caricamento e pubblicazione vengono registrati nella pagina Processi, dove è possibile controllarne lo stato. |
| Pubblica dopo il caricamento |  | Pubblica automaticamente le risorse caricate. |
| Sovrascrivi in qualsiasi cartella, nome come risorsa base, indipendentemente dall’estensione |  | Selezionate questa opzione se desiderate che i file caricati sostituiscano quelli esistenti con gli stessi nomi. Il nome di questa opzione potrebbe essere diverso, a seconda delle impostazioni in Impostazione **[!UICONTROL applicazione > Impostazioni]** **[!UICONTROL generali >]** Carica nell’applicazione **[!UICONTROL >]** Sovrascrivi immagini ****. |
| Annulla compressione file ZIP o Tar durante il caricamento |  |  |
| Opzioni processo |  | Fate clic su Opzioni **** processo per aprire la finestra di dialogo Opzioni [!UICONTROL processo di] caricamento e scegliete le opzioni che interessano l’intero processo di caricamento. Queste opzioni sono le stesse per tutti i tipi di file.<br>Potete scegliere le opzioni predefinite per caricare i file dalla pagina Impostazioni generali applicazione. Per aprire questa pagina, scegliete **[!UICONTROL Configurazione]** > Impostazione **** applicazione. Fate clic sul pulsante Opzioni **[!UICONTROL di caricamento]** predefinite per aprire la finestra di dialogo Opzioni [!UICONTROL processo di] caricamento. |
|  | Quando  | Selezionate Una tantum o Periodico. Per impostare un processo periodico, scegliete un’opzione Ripeti (Quotidianamente, Settimanalmente, Mensilmente o Personalizzato) per specificare quando eseguire il processo di caricamento FTP. Quindi specificate le opzioni di pianificazione in base alle esigenze. |
|  | Includi sottocartelle | Caricate tutte le sottocartelle all’interno della cartella che desiderate caricare. I nomi della cartella e delle relative sottocartelle caricate vengono inseriti automaticamente in [!DNL Experience Manager Assets]. |
|  | Opzioni di ritaglio | Per ritagliare manualmente dai lati di un’immagine, selezionate il menu Ritaglio e scegliete Manuale. Immettete quindi il numero di pixel da ritagliare da ogni lato o da uno dei lati dell’immagine. La quantità di immagine che viene ritagliata dipende dall’impostazione ppi (pixel per pollice) nel file immagine. Ad esempio, se l’immagine viene visualizzata a 150 ppi e immettete 75 nelle caselle di testo, viene ritagliato mezzo pollice da ogni lato.<br> Per ritagliare automaticamente i pixel dello spazio bianco da un’immagine, aprite il menu Ritaglio, scegliete Manuale e immettete i valori in pixel nei campi In alto, A destra, In basso e A sinistra per ritagliare dai lati. Potete anche scegliere Rifila dal menu Ritaglio e scegliere le seguenti opzioni:<br> **Rifila in base a** <ul><li>**Colore** - Scegliete l’opzione Colore. Dal menu Angolo scegliete quindi l’angolo dell’immagine con il colore che rappresenta meglio quello dello spazio bianco da ritagliare.</li><li>**Trasparenza** - Scegliete l’opzione Trasparenza.<br> **Tolleranza** - Trascinate il cursore per specificare una tolleranza da 0 a 1. Per rifilare in base al colore, specificate 0 per ritagliare i pixel solo se corrispondono esattamente al colore selezionato nell’angolo dell’immagine. Con valori più vicini a 1 viene invece tollerata una maggiore differenza di colore.<br>Per rifilare in base alla trasparenza, l’impostazione 0 ritaglia i pixel solo se sono trasparenti. Con valori più vicini a 1 viene invece tollerata una minore trasparenza.</li></ul><br>Tenete presente che queste opzioni di ritaglio non sono distruttive. |
|  | Opzioni profilo colore | Scegliete una conversione del colore quando create file ottimizzati per la distribuzione:<ul><li>Mantenimento colore predefinito: mantiene i colori dell’immagine sorgente ogni volta che le immagini contengono informazioni sullo spazio colore; non esiste alcuna conversione del colore. Quasi tutte le immagini presentano già il profilo colore appropriato. Tuttavia, se un’immagine sorgente CMYK non contiene un profilo colore incorporato, i colori vengono convertiti nello spazio colore sRGB (standard Rosso Verde Blu). sRGB è lo spazio colore consigliato per la visualizzazione di immagini sulle pagine Web.</li><li>Mantieni spazio colore originale: Mantiene i colori originali senza alcuna conversione colore. Per le immagini senza un profilo colore incorporato, qualsiasi conversione colore viene effettuata utilizzando i profili colore predefiniti configurati nelle impostazioni di pubblicazione. I profili colore potrebbero non essere allineati con il colore nei file creati con questa opzione. Pertanto, si consiglia di utilizzare l’opzione Mantenimento colore predefinito.</li><li>Personalizzato da > Per<br> aprire i menu in modo da poter scegliere uno spazio colore Converti da e Converti in. Questa opzione avanzata ha la priorità sulle informazioni di colore incorporate nel file sorgente. Selezionate questa opzione quando tutte le immagini che state inviando contengono dati di profilo colore errati o mancanti.</li></ul> |
|  | Opzioni di modifica delle immagini | Potete mantenere le maschere di ritaglio nelle immagini e scegliere un profilo colore.<br> Consultate [Impostazione delle opzioni di modifica delle immagini al momento del caricamento](#setting-image-editing-options-at-upload). |
|  | Opzioni PostScript | Potete rasterizzare i file di PostScript®, ritagliare i file, mantenere lo sfondo trasparente, scegliere una risoluzione e uno spazio colore.<br> Consultate [Impostazione delle opzioni](#setting-postscript-and-illustrator-upload-options)di caricamento PostScript e  Illustrator. |
|  | Opzioni Photoshop | Potete creare modelli da file  Adobe® Photoshop®, mantenere i livelli, specificare i nomi dei livelli, estrarre del testo e specificare il modo in cui le immagini vengono ancorate ai modelli.<br> I modelli non sono supportati in [!DNL Experience Manager].<br> Consultate [Impostazione delle opzioni](#setting-photoshop-upload-options)di caricamento di Photoshop. |
|  | Opzioni PDF | Potete rasterizzare i file, estrarre parole di ricerca e collegamenti, generare automaticamente un eCatalog, impostare la risoluzione e scegliere uno spazio colore.<br> Gli eCatalog non sono supportati in [!DNL Experience Manager]. <br> Consultate [Impostazione delle opzioni](#setting-pdf-upload-options)di caricamento PDF. |
|  |  opzioni Illustrator | Potete rasterizzare  file Adobe Illustrator®, mantenere lo sfondo trasparente, scegliere una risoluzione e uno spazio colore.<br> Consultate [Impostazione delle opzioni](#setting-postscript-and-illustrator-upload-options)di caricamento PostScript e  Illustrator. |
|  | Opzioni eVideo | Potete transcodificare un file video scegliendo un predefinito per video.<br> Consultate [Impostazione delle opzioni](#setting-evideo-upload-options)di caricamento per eVideo. |
|  | Predefiniti set di batch | Per creare un set di immagini o un set 360 gradi dai file caricati, fate clic sulla colonna Attivo per il predefinito che desiderate usare. Potete selezionare più predefiniti. Potete creare i predefiniti nella pagina Impostazione applicazione/Predefiniti set di batch di Dynamic Media Classic.<br> Consultate [Configurazione dei predefiniti per set di batch per la generazione automatica di set di immagini e set](config-dms7.md#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets) 360 gradi per ulteriori informazioni sulla creazione di predefiniti per set di batch.<br> Consultate [Impostazione dei predefiniti per set di batch al momento del caricamento](#setting-batch-set-presets-at-upload). |

#### Impostazione delle opzioni di modifica delle immagini al momento del caricamento {#setting-image-editing-options-at-upload}

Quando caricate dei file immagine, inclusi i file AI, EPS e PSD, potete effettuare le seguenti operazioni di modifica nella finestra di dialogo Opzioni [!UICONTROL processo di] caricamento:

* Ritagliare gli spazi bianchi dal bordo delle immagini (vedere la descrizione nella tabella precedente).
* Ritagliare manualmente dai lati delle immagini (vedere la descrizione nella tabella precedente).
* Scegliete un profilo colore (consultate la descrizione dell’opzione nella tabella precedente).
* Create una maschera da un tracciato di ritaglio.
* Rendere le immagini più nitide con opzioni di maschera di contrasto
* Foratura sfondo

<!--
| Option | Sub-option | Description |
|---|---|---|
| Create Mask From Clipping Path | | Create a mask for the image based on its clipping path information. This option applies to images created with image-editing applications in which a clipping path was created. |
| Unsharp Masking | | Lets you fine-tune a sharpening filter effect on the final downsampled image, controlling the intensity of the effect, the radius of the effect (as measured in pixels), and a threshold of contrast that is ignored.<br> This effect uses the same options as Photoshop’s Unsharp Mask filter. Contrary to what the name suggests, Unsharp Mask is a sharpening filter. Under Unsharp Masking, set the options you want. Setting options are described in the following: |
| | Amount | Controls the amount of contrast that is applied to edge pixels.<br> Think of it as the intensity of the effect. The main difference between the amount values of Unsharp Mask in Dynamic Media and the amount values in Adobe Photoshop, is that Photoshop has an amount range of 1% to 500%. Whereas, in Dynamic Media, the value range is 0.0 to 5.0. A value of 5.0 is the rough equivalent of 500% in Photoshop; a value of 0.9 is the equivalent of 90%, and so on. |
| | Radius | Controls the radius of the effect. The value range is 0-250.<br> The effect is run on all pixels in an image and radiates out from all pixels in all directions. The radius is measured in pixels. For example, to get a similar sharpening effect for a 2000 x 2000 pixel image and 500 x 500 pixel image, you would set a radius of two pixels on the 2000 x 2000 pixel image and a radius value of one pixel on the 500 x 500 pixel image. A larger value is used for an image that has more pixels. |
| | Threshold | Threshold is a range of contrast that is ignored when the Unsharp Mask filter is applied. It is important so that no "noise" is introduced to an image when this filter is used. The value range is 0-255, which is the number of brightness steps in a grayscale image. 0=black, 128=50% gray and 255=white.<br> For example, a threshold value of 12 ignores slight variations is skin tone brightness to avoid adding noise, but still add edge contrast to areas such as where eyelashes meet skin.<br> For example, if you have a photo of someone’s face, the Unsharp Mask affects the parts of the image, such as where eyelashes and skin meet to create an obvious area of contrast, and the smooth skin itself. Even the smoothest skin exhibits subtle changes in brightness values. If you do not use a threshold value, the filter accentuates these subtle changes in skin pixels. In turn, a noisy and undesirable effect is created while contrast on the eyelashes is increased, enhancing sharpness.<br> To avoid this issue, a threshold value is introduced that tells the filter to ignore pixels that do not change contrast dramatically, like smooth skin.<br> In the zipper graphic shown earlier, notice the texture next to the zippers. Image noise is exhibited because the threshold values were too low to suppress the noise. |
| | Monochrome | Select to unsharp-mask image brightness (intensity).<br> Deselect to unsharp-mask each color component separately. |
| Knockout Background | | Automatically removes the background of an image when you upload it. This technique is useful to draw attention to a particular object and make it stand out from a busy background. Select to enable or “turn on” the Knockout Background feature and the following sub-options: |
| | Corner | Required.<br> The corner of the image that is used to define the background color to knockout.<br> You can choose from **Upper Left**, **Bottom Left**, **Upper Right**, or **Bottom Right**. |
| | Fill Method | Required.<br> Controls pixel transparency from the Corner location that you set.<br> You can choose from the following fill methods: <ul><li>**Flood Fill** - turns all pixels transparent that match the Corner that you have specified and are connected to it.</li><li>**Match Pixel** - turns all matching pixels transparent, regardless of their location on the image.</li></ul> |
| | Tolerance | Optional.<br> Controls the allowable amount of variation in pixel color matching based on the Corner location that you set.<br> Use a value of 0.0 to match pixel colors exactly or, use a value of 1.0 to allow for the greatest variation. |
-->

#### Impostare le opzioni di caricamento PostScript e  Illustrator {#setting-postscript-and-illustrator-upload-options}

Quando caricate i file immagine PostScript (EPS) o  Illustrator (AI), potete formattarli in vari modi. Potete rasterizzare i file, mantenere lo sfondo trasparente, scegliere una risoluzione e uno spazio colore. Le opzioni per formattare i file PostScript e  Illustrator sono disponibili nella finestra di dialogo Opzioni [!UICONTROL processo di] caricamento, in Opzioni  PostScript e [!UICONTROL Opzioni]Illustrator.

| Opzione | Sottoopzione | Descrizione |
|---|---|---|
| Elaborazione |  | Scegliete **[!UICONTROL Rasterizza]** per convertire la grafica vettoriale nel file in formato bitmap. |
| Mantieni sfondo trasparente nell’immagine di rendering |  | Mantenere la trasparenza dello sfondo del file. |
| Risoluzione |  | Determina l’impostazione della risoluzione. Questa impostazione determina la quantità di pixel visualizzati per pollice nel file. |
| Spazio colore |  | Dal menu Spazio colore scegliete una delle seguenti opzioni di spazio colore: |
|  | Rileva automaticamente | Conserva lo spazio colore del file. |
|  | Forza come RGB | Effettua la conversione nello spazio colore RGB. |
|  | Forza come CMYK | Effettua la conversione nello spazio colore CMYK. |
|  | Forza come scala di grigio | Effettua la conversione nello spazio colore Scala di grigio. |

#### Impostare le opzioni di caricamento di Photoshop {#setting-photoshop-upload-options}

I file Photoshop Document (PSD) vengono utilizzati più spesso per creare modelli di immagine. Quando caricate un file PSD, potete creare automaticamente dal file un modello di immagine (selezionate l’opzione [!UICONTROL Crea modello] nella schermata Carica).

Dynamic Media crea più immagini da un file PSD con livelli, se usate il file per creare un modello; crea un’immagine per ciascun livello.

Utilizzate le opzioni  Ritaglio e le opzioni [!UICONTROL Profilo]colore descritte sopra, con le opzioni di caricamento Photoshop.

>[!NOTE]
>
>I modelli non sono supportati in [!DNL Experience Manager].

| Opzione | Sottoopzione | Descrizione |
|---|---|---|
| Mantieni livelli |  | Estrae i livelli eventualmente presenti nel file PSD in singole risorse. I livelli delle risorse restano associati al file PSD. Per visualizzarli, aprite il file PSD in visualizzazione Dettagli e selezionate il pannello dei livelli. |
| Crea modello |  | Crea un modello dai livelli presenti nel file PSD. |
| Estrai testo |  | Estrae il testo in modo che gli utenti possano cercare il testo in un visualizzatore. |
| Estendere i livelli alle dimensioni dello sfondo |  | Estende le dimensioni dei livelli di immagine estratti alle dimensioni del livello di sfondo. |
| Denominazione dei livelli |  | I livelli nel file PSD vengono caricati come immagini separate. |
|  | Nome livello | Denomina le immagini in base ai nomi dei rispettivi livelli nel file PSD. Ad esempio, un livello denominato Price Tag nel file PSD originale diventa un’immagine denominata Price Tag. Tuttavia, se i nomi dei livelli nel file PSD sono nomi di livello Photoshop predefiniti (Sfondo, Livello 1, Livello 2 e così via), le immagini vengono denominate in base ai numeri dei rispettivi livelli nel file PSD, non in base ai nomi dei livelli predefiniti. |
|  | Photoshop e numero livello | Denomina le immagini in base ai numeri dei rispettivi livelli nel file PSD, ignorando i nomi dei livelli originali. Le immagini vengono denominate con il nome del file Photoshop e un numero del livello aggiunto. Ad esempio, il secondo livello di un file denominato Spring Ad.psd è denominato Spring Ad_2 anche se in Photoshop aveva un nome non predefinito. |
|  | Photoshop e nome livello | Denomina le immagini dopo il file PSD seguito dal nome o dal numero del livello. Il numero del livello viene utilizzato se i nomi del livello nel file PSD sono nomi di livello Photoshop predefiniti. Ad esempio, un livello denominato Price Tag in un file PSD denominato SpringAd è denominato Spring Ad_Price Tag. Un livello con il nome predefinito Layer 2 è denominato Spring Ad_2. |
| Ancoraggio |  | Specificate in che modo le immagini vengono ancorate nei modelli generati dalla composizione a livelli generata dal file PSD. Per impostazione predefinita, l’ancoraggio è al centro. Un ancoraggio centrale consente alle immagini sostitutive di riempire al meglio lo stesso spazio, indipendentemente dalle proporzioni dell’immagine sostitutiva. Le immagini con proporzioni diverse che sostituiscono l’immagine, quando fanno riferimento al modello e utilizzano la sostituzione dei parametri, occupano in modo efficace lo stesso spazio. Passate a un’impostazione diversa se l’applicazione richiede che le immagini sostitutive riempiano lo spazio allocato nel modello. |

#### Impostazione delle opzioni di caricamento PDF {#setting-pdf-upload-options}

Quando caricate un file PDF, potete formattarlo in vari modi. Potete ritagliare le pagine, estrarre le parole di ricerca, immettere una risoluzione in pixel per pollice e scegliere uno spazio colore. I file PDF contengono spesso un margine di rifilo, indicatori di taglio, crocini di registro e altri indicatori di stampa. Potete ritagliare questi indicatori dai lati delle pagine mentre caricate un file PDF.

>[!NOTE]
>
>Gli eCatalog non sono supportati in [!DNL Experience Manager].

Scegliete tra le seguenti opzioni:

| Opzione | Sottoopzione | Descrizione |
|---|---|---|
| Elaborazione | Rasterizza | (Impostazione predefinita) Estrae le pagine del file PDF e converte la grafica vettoriale in immagini bitmap. Scegliete questa opzione per creare un eCatalog. |
| Estrai | Cerca parole | Estrae le parole dal file PDF in modo che sia possibile effettuare ricerche nel file mediante parole chiave in un visualizzatore di eCatalog. |
|  | Collegamenti | Estrae i collegamenti dai file PDF e li converte in mappe immagine utilizzate in un visualizzatore di eCatalog. |
| Genera automaticamente eCatalog da PDF con più pagine |  | Crea automaticamente un eCatalog dal file PDF. L’eCatalog viene denominato in base al file PDF caricato. Questa opzione è disponibile solo se il file PDF viene rasterizzato durante il caricamento. |
| Risoluzione |  | Determina l’impostazione della risoluzione. Questa impostazione determina la quantità di pixel visualizzati per pollice nel file PDF. Il valore predefinito è 150. |
| Spazio colore |  | Dal menu Spazio colore scegliete uno spazio colore per il file PDF. La maggior parte dei file PDF contiene immagini a colori sia RGB che CMYK. Lo spazio colore RGB è preferibile per la visualizzazione online. |
|  | Rileva automaticamente | Conserva lo spazio colore del file PDF. |
|  | Forza come RGB | Effettua la conversione nello spazio colore RGB. |
|  | Forza come CMYK | Effettua la conversione nello spazio colore CMYK. |
|  | Forza come scala di grigio | Effettua la conversione nello spazio colore Scala di grigio. |

#### Impostare le opzioni di caricamento per eVideo {#setting-evideo-upload-options}

Per transcodificare un file video scegliendo tra diversi predefiniti per video.

| Opzione | Sottoopzione | Descrizione |
|---|---|---|
| Video adattivo |  | Un predefinito di codifica singolo che funziona con qualsiasi proporzione per creare video da distribuire a dispositivi mobili, tablet e computer desktop. I video sorgente caricati e codificati con questo predefinito sono impostati su un’altezza specifica. Tuttavia, la larghezza viene ridimensionata automaticamente per mantenere le proporzioni del video. <br>Come procedura ottimale si consiglia di utilizzare la codifica per video adattivi. |
| Predefiniti codifica singola | Ordina predefiniti di codifica | Selezionate Nome o Dimensione per ordinare i predefiniti di codifica elencati in Desktop, Mobile e Tablet per nome o per dimensione di risoluzione. |
|  | Desktop | Create un file MP4 per distribuire un&#39;esperienza video in streaming o progressiva ai computer desktop. Selezionate una o più proporzioni con la dimensione di risoluzione e la velocità dati di destinazione desiderate. |
|  | Mobile | Create un file MP4 da distribuire su iPhone o dispositivi mobili Android. Selezionate una o più proporzioni con la dimensione di risoluzione e la velocità dati di destinazione desiderate. |
|  | Tablet | Create un file MP4 da distribuire su dispositivi iPad o tablet Android. Selezionate una o più proporzioni con la dimensione di risoluzione e la velocità dati di destinazione desiderate. |

#### Imposta predefiniti per set di batch al caricamento {#setting-batch-set-presets-at-upload}

Per creare automaticamente un set di immagini o un set 360 gradi dalle immagini caricate, fate clic sulla colonna Attivo per il predefinito da usare. Potete selezionare più predefiniti.

Consultate [Configurazione dei predefiniti per set di batch per la generazione automatica di set di immagini e set](/help/assets/config-dms7.md#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets) 360 gradi per ulteriori informazioni sulla creazione di predefiniti per set di batch.

### Caricamenti in streaming {#streamed-uploads}

Se caricate molte risorse su Adobe Experience Manager, le richieste di I/O al server aumentano drasticamente, riducendo l’efficienza del caricamento e causando anche il timeout di alcune attività di caricamento. [!DNL Experience Manager Assets] supporta il caricamento in streaming delle risorse. Il caricamento in streaming riduce l’I/O del disco durante l’operazione di caricamento, evitando la memorizzazione delle risorse in una cartella temporanea sul server prima di copiarla nell’archivio. Al contrario, i dati vengono trasferiti direttamente nella directory archivio. In questo modo, si riduce il tempo necessario per caricare risorse di grandi dimensioni e la possibilità di timeout. Il caricamento in streaming è abilitato per impostazione predefinita in [!DNL Assets].

>[!NOTE]
>
>Il caricamento dello streaming è disattivato per Adobe Experience Manager eseguito su un server JEE con una versione servlet-api inferiore a 3.1.

### Estrai archivio ZIP contenente le risorse {#extractzip}

Potete caricare gli archivi ZIP come qualsiasi altra risorsa supportata. Le stesse regole del nome file si applicano ai file ZIP. [!DNL Experience Manager] consente di estrarre un archivio ZIP in una posizione DAM. Se i file di archivio non contengono ZIP come estensione, abilita il rilevamento del tipo di file utilizzando il contenuto.

Selezionate un archivio ZIP alla volta, fate clic su **[!UICONTROL Estrai archivio]** e selezionate una cartella di destinazione. Selezionare un&#39;opzione per gestire eventuali conflitti. Se le risorse nel file ZIP sono già presenti nella cartella di destinazione, potete selezionare una delle seguenti opzioni: saltate l’estrazione, sostituite i file esistenti, mantenete entrambe le risorse rinominando o create una nuova versione.

Al termine dell’estrazione, [!DNL Experience Manager] inviate una notifica nell’area di notifica. Durante [!DNL Experience Manager] l&#39;estrazione del file ZIP, è possibile tornare al lavoro senza interrompere l&#39;estrazione.

![Notifica dell&#39;estrazione di file ZIP](assets/Zip-extraction-notification.png)

Alcune limitazioni della funzione sono:

* Se nella destinazione esiste una cartella con lo stesso nome, le risorse del file ZIP vengono estratte nella cartella esistente.
* Se annullate l’estrazione, le risorse già estratte non vengono eliminate.
* Non potete selezionare due file ZIP contemporaneamente ed estrarli. Potete estrarre un solo archivio ZIP alla volta.
* Durante il caricamento di un archivio ZIP, se nella finestra di dialogo di caricamento viene visualizzato un errore del server 500, riprovare dopo l&#39;installazione del service pack più recente.

## Visualizzare le risorse {#previewing-assets}

Per visualizzare l’anteprima di una risorsa, effettuate le seguenti operazioni.

1. Dall’interfaccia [!DNL Assets] utente, individuate la posizione della risorsa da visualizzare in anteprima.
1. Fate clic sulla risorsa desiderata per aprirla.

1. Nella modalità di anteprima, le opzioni di zoom sono disponibili per i tipi [di immagini](/help/assets/assets-formats.md#supported-raster-image-formats) supportati (con modifica interattiva).

   Per ingrandire una risorsa, fate clic `+` (o fate clic sulla lente di ingrandimento della risorsa). Per ridurre lo zoom, fate clic `-`. Quando ingrandite, potete osservare da vicino qualsiasi area dell’immagine eseguendo il panning. La freccia di reimpostazione dello zoom consente di tornare alla visualizzazione originale. Per ripristinare le dimensioni originali della visualizzazione, fate clic su **[!UICONTROL Ripristina]** ![Ripristina visualizzazione](assets/do-not-localize/revert.png).

**Visualizzare in anteprima le risorse utilizzando solo i tasti di scelta rapida**

Per visualizzare in anteprima una risorsa mediante la tastiera, effettuate le seguenti operazioni:

1. Dall’interfaccia [!DNL Assets] utente, individuate la risorsa desiderata utilizzando `Tab` e i tasti freccia.

1. Premete `Enter` il tasto sulla risorsa desiderata per aprirla. Potete ingrandire le risorse in modalità di anteprima.

1. Per ingrandire la risorsa:
   1. Utilizzate `Tab` il tasto per spostare lo stato attivo nell&#39;opzione di zoom in.
   1. Utilizzate `Enter` il tasto per ingrandire l&#39;immagine.

   Per ridurre la visualizzazione, usate `Tab` il tasto per spostare la messa a fuoco sull’opzione di zoom out e premete `Enter`.

1. Utilizzare `Shift` + `Tab` per spostare la messa a fuoco sull&#39;immagine.

1. Utilizzate i tasti freccia per spostarsi intorno all&#39;immagine ingrandita.

>[!MORELIKETHIS]
>
>* [Visualizzare l’anteprima delle risorse](/help/assets/previewing-assets.md)multimediali dinamiche.
>* [Visualizzare le risorse](managing-linked-subassets.md#viewing-subassets)secondarie.


## Modificare le proprietà e i metadati {#editing-properties}

1. Andate alla posizione della risorsa per modificarne i metadati.

1. Selezionate la risorsa, quindi fate clic su **[!UICONTROL Proprietà]** dalla barra degli strumenti per visualizzare le proprietà della risorsa. In alternativa, scegliete l’azione rapida **[!UICONTROL Proprietà]** sulla scheda delle risorse.

   ![Proprietà azione rapida nella vista scheda della risorsa](assets/properties_quickaction.png)

1. Nella pagina [!UICONTROL Proprietà] , modificate le proprietà dei metadati in varie schede. Ad esempio, nella scheda **[!UICONTROL Base]** , modificare il titolo, la descrizione e così via.

   >[!NOTE]
   >
   >Il layout della pagina [!UICONTROL Proprietà] e le proprietà dei metadati disponibili dipendono dallo schema di metadati sottostante. Per informazioni su come modificare il layout della pagina [!UICONTROL Proprietà] , consultate Schemi [di](/help/assets/metadata-schemas.md)metadati.

1. Per pianificare una data/ora specifica per l’attivazione della risorsa, utilizza il selettore data posto accanto al campo **[!UICONTROL On Time (All’ora)]**.

   ![Selezione data e ora oppure uso dei tasti di scelta rapida nel campo Ora di attivazione per aggiungere data e ora per l’attivazione delle risorse](assets/datepicker.png)

   *Figura: Utilizzate il selettore data per pianificare l&#39;attivazione della risorsa.*

1. Per disattivare la risorsa dopo una determinata durata, scegliete la data/ora di disattivazione dal selettore data accanto al campo **[!UICONTROL Ora]** disattivazione. La data di disattivazione deve essere successiva alla data di attivazione di una risorsa. Dopo la [!UICONTROL disattivazione], una risorsa e le relative rappresentazioni non sono disponibili né tramite l&#39;interfaccia [!DNL Assets] Web né tramite l&#39;API HTTP.

1. Nel campo **[!UICONTROL Tag]** , selezionare uno o più tag. Per aggiungere un tag personalizzato, digitate il nome del tag nella casella e premete Invio. Il nuovo tag viene salvato in [!DNL Experience Manager]. [!DNL YouTube] richiede i tag per la pubblicazione. Consultate [pubblicare i video su YouTube](video.md#publishing-videos-to-youtube).

   >[!NOTE]
   >
   >Per creare i tag, è necessario disporre dell&#39;autorizzazione di scrittura `/content/cq:tags/default` nell&#39;archivio CRX.

1. To provide a rating to the asset, click the **[!UICONTROL Advanced]** tab and then click the star at the appropriate position to assign the desired rating.

   ![Scheda Avanzate in Proprietà risorsa per assegnare la valutazione](assets/ratings.png)

   Il punteggio assegnato alla risorsa viene visualizzato in **[!UICONTROL Valutazioni]** personali. La valutazione media che la risorsa ricevuta dagli utenti che hanno valutato la risorsa viene visualizzata in **[!UICONTROL Valutazione]**. Inoltre, la suddivisione dei punteggi di rating che contribuiscono al punteggio medio è visualizzata in Disaggregazione **[!UICONTROL valutazione]**. Potete cercare le risorse in base alla media dei punteggi di valutazione.

1. Per visualizzare le statistiche di utilizzo della risorsa, fai clic sulla scheda **[!UICONTROL Insights]** (Approfondimenti).

   Le statistiche di utilizzo includono quanto segue:

   * Numero di volte in cui la risorsa è stata visualizzata o scaricata
   * Canali/dispositivi attraverso i quali è stata utilizzata la risorsa
   * Soluzioni creative in cui la risorsa è stata utilizzata di recente

   Per ulteriori dettagli, consulta [Informazioni approfondite](/help/assets/asset-insights.md)sulle risorse.

1. Fai clic su **[!UICONTROL Salva e chiudi]**.
1. Passate all&#39;interfaccia [!DNL Assets] utente. Le proprietà dei metadati modificate, inclusi titolo, descrizione, valutazioni e così via, vengono visualizzate sulla scheda delle risorse nella vista a schede e nelle relative colonne nella vista Elenco.

## Copiare le risorse {#copying-assets}

Quando copiate una risorsa o una cartella, viene copiata l’intera risorsa o la cartella, insieme alla relativa struttura del contenuto. Una risorsa o una cartella copiata viene duplicata nel percorso di destinazione. La risorsa nella posizione di origine non viene modificata.

Alcuni attributi univoci per una particolare copia di una risorsa non vengono riportati avanti. Alcuni esempi sono:

* ID risorsa, data e ora di creazione, versioni e cronologia delle versioni. Alcune di queste proprietà sono indicate dalle proprietà `jcr:uuid`, `jcr:created`e `cq:name`.

* L’ora di creazione e i percorsi di riferimento sono univoci per ciascuna risorsa e per ciascuna delle relative rappresentazioni.

Le altre proprietà e informazioni sui metadati vengono mantenute. Durante la copia di una risorsa non viene creata una copia parziale.

1. Nell’ [!DNL Assets] interfaccia, selezionate una o più risorse e fate clic su **[!UICONTROL Copia]** nella barra degli strumenti. In alternativa, seleziona l’opzione **[!UICONTROL Copia]** ![copia nella barra degli strumenti dell’interfaccia](assets/do-not-localize/copy_icon.png) Risorse per effettuare le azioni rapide dalla scheda delle risorse.

   >[!NOTE]
   >
   >Se utilizzate l’azione rapida [!UICONTROL Copia] , potete copiare una sola risorsa alla volta.

1. Andate alla posizione in cui desiderate copiare le risorse.

   >[!NOTE]
   >
   >Se copiate una risorsa nella stessa posizione, [!DNL Experience Manager] viene generata automaticamente una variante del nome. Ad esempio, se copiate una risorsa con titolo `Square`, [!DNL Experience Manager] viene automaticamente generato il titolo della relativa copia come `Square1`.

1. Fate clic sull’opzione **[!UICONTROL Incolla]** ![Incolla nella barra degli strumenti](assets/do-not-localize/paste.png) Risorse, disponibile nella barra degli strumenti. Le risorse vengono quindi copiate in questa posizione.

   >[!NOTE]
   >
   >L’opzione **[!UICONTROL Incolla]** è disponibile nella barra degli strumenti fino al completamento dell’operazione Incolla.

## Spostare e rinominare le risorse {#moving-or-renaming-assets}

Quando spostate le risorse (o le cartelle) in un’altra posizione, le risorse (o cartelle) non vengono duplicate, a differenza di quando copiate la risorsa. Le risorse (o le cartelle) vengono posizionate nel percorso di destinazione e rimosse dal percorso di origine. Potete inoltre rinominare la risorsa quando la spostate nella nuova posizione.
Se spostate una risorsa pubblicata in un percorso diverso, potete ripubblicare la risorsa. Per impostazione predefinita, l’operazione di spostamento su una risorsa pubblicata viene automaticamente annullata dalla pubblicazione. Una risorsa spostata viene ripubblicata se l’autore seleziona l’opzione [!UICONTROL Ripubblica] quando sposta la risorsa.

![Quando si sposta una risorsa già pubblicata, è possibile ripubblicarla](assets/republish-on-move.png)

Per spostare risorse o cartelle:

1. Andate alla posizione della risorsa da spostare.

1. Selezionate la risorsa e fate clic sull’opzione **[!UICONTROL Sposta]** nella barra degli strumenti.
   ![Opzione Sposta nella barra degli strumenti Risorse](assets/do-not-localize/move.png)

1. Nella procedura guidata [!UICONTROL Sposta risorse] , effettuate una delle seguenti operazioni:

   * Dopo averlo spostato, specificate il nome della risorsa. Quindi fate clic su **[!UICONTROL Avanti]** per proseguire.

   * Fate clic su **[!UICONTROL Annulla]** per interrompere il processo.
   >[!NOTE]
   >
   >* Potete specificare lo stesso nome per la risorsa se nella nuova posizione non è presente alcuna risorsa con lo stesso nome. Tuttavia, se spostate la risorsa in una posizione in cui esiste una risorsa con lo stesso nome, usate un nome diverso. Se usate lo stesso nome, il sistema genera automaticamente una variante del nome. Ad esempio, se la risorsa ha il nome Square, il sistema genera il nome Square1 per la relativa copia.
   >* Durante la ridenominazione, gli spazi bianchi non sono consentiti nel nome del file.


1. Nella finestra di dialogo **[!UICONTROL Seleziona destinazione]** , effettuate una delle seguenti operazioni:

   * Andate alla nuova posizione delle risorse, quindi fate clic su **[!UICONTROL Avanti]** per proseguire.

   * Fate clic su **[!UICONTROL Indietro]** per tornare alla schermata **[!UICONTROL Rinomina]** .

1. Se le risorse che state spostando dispongono di pagine, risorse o raccolte di riferimento, accanto alla scheda **[!UICONTROL Seleziona destinazione]** viene visualizzata la scheda **[!UICONTROL Regola riferimenti]** .

   Effettuate una delle seguenti operazioni nella schermata **[!UICONTROL Regola riferimenti]** :

   * Specificate i riferimenti da modificare in base ai nuovi dettagli, quindi fate clic su **[!UICONTROL Sposta]** per proseguire.

   * Nella colonna **[!UICONTROL Regola]** , selezionate o deselezionate i riferimenti alle risorse.
   * Fate clic su **[!UICONTROL Indietro]** per tornare alla schermata **[!UICONTROL Seleziona destinazione]** .

   * Fate clic su **[!UICONTROL Annulla]** per interrompere l&#39;operazione di spostamento.

   Se non aggiornate i riferimenti, continueranno a indicare il percorso precedente della risorsa. Se regolate i riferimenti, questi vengono aggiornati al nuovo percorso della risorsa.

### Spostare le risorse tramite trascinamento {#move-using-drag}

Potete spostare le risorse (o cartelle) in una cartella di pari livello trascinandole nella posizione di destinazione, invece di utilizzare l’opzione [!UICONTROL Sposta] nell’interfaccia utente. Tuttavia, questa operazione è possibile solo nella vista a elenco.

Se si spostano le risorse trascinandole, non viene aperta la procedura guidata [!UICONTROL Sposta risorsa] . Pertanto, durante lo spostamento non è possibile rinominare le risorse. Inoltre, le risorse già pubblicate vengono ripubblicate trascinandole per spostarle, senza richiedere l&#39;approvazione dell&#39;utente per la ripubblicazione.

![Spostare le risorse nelle cartelle di pari livello trascinandole](assets/move-by-drag.gif)

## Gestire le rappresentazioni {#managing-renditions}

1. Potete aggiungere o rimuovere rappresentazioni per una risorsa, tranne l’originale. Andate alla posizione della risorsa per la quale desiderate aggiungere o rimuovere le rappresentazioni.

1. Fate clic sulla risorsa per aprirne la pagina.
1. Nell&#39;interfaccia del Experience Manager , selezionare **[!UICONTROL Rendering]** dall&#39;elenco.
1. Nel pannello **[!UICONTROL Rappresentazioni]** , visualizzate l’elenco delle rappresentazioni generate per la risorsa.

   ![Pannello Rappresentazioni nella pagina Dettagli risorse](assets/renditions_panel.png)

   >[!NOTE]
   >
   >Per impostazione predefinita, [!DNL Assets] non visualizza la rappresentazione originale della risorsa in modalità di anteprima. Gli amministratori possono utilizzare le sovrapposizioni per configurare [!DNL Assets] la visualizzazione delle rappresentazioni originali in modalità di anteprima.

1. Selezionate una rappresentazione per visualizzare o eliminare la rappresentazione.

   **Eliminare una rappresentazione**

   Selezionate una rappresentazione dal pannello **[!UICONTROL Rappresentazioni]** , quindi fate clic sull&#39;opzione **[!UICONTROL Elimina rappresentazione]** ![per eliminare un&#39;opzione di rappresentazione](assets/do-not-localize/deleteoutline.png) dalla barra degli strumenti. Le rappresentazioni non possono essere eliminate in blocco al termine dell’elaborazione delle risorse. Per le singole risorse, potete rimuovere manualmente i rendering dall’interfaccia utente. Per più risorse, potete personalizzare  Experience Manager per eliminare rappresentazioni specifiche o per eliminare le risorse e caricare nuovamente le risorse eliminate.

   **Caricare una nuova rappresentazione**

   Andate alla pagina dei dettagli della risorsa, quindi fate clic sull&#39;opzione **[!UICONTROL Aggiungi rappresentazione]** Aggiungi rappresentazione per caricare la nuova opzione di rappresentazione ![](assets/do-not-localize/add.png) nella barra degli strumenti per caricare una nuova rappresentazione per la risorsa.

   >[!NOTE]
   >
   >Se selezioni un rendering dal pannello **[!UICONTROL Rendering]**, la barra degli strumenti cambia contesto, visualizzando solo le azioni del rendering specifico. Options, such as the [!UICONTROL Upload Rendition] option is not displayed. Per visualizzare queste opzioni nella barra degli strumenti, vai alla pagina dei dettagli della risorsa.

   Potete configurare le dimensioni per la rappresentazione da visualizzare nella pagina dei dettagli di un’immagine o di una risorsa video. In base alle dimensioni specificate, [!DNL Assets] visualizza la rappresentazione con le dimensioni esatte o più vicine.

   Per configurare le dimensioni di rendering di un’immagine a livello di dettaglio della risorsa, sovrapponi il nodo `renditionpicker` (`libs/dam/gui/content/assets/assetpage/jcr:content/body/content/content/items/assetdetail/items/col1/items/assetview/renditionpicker`) e configura il valore della proprietà larghezza.  Per personalizzare il rendering sulla pagina dei dettagli della risorsa in base alle dimensioni dell’immagine, configura la proprietà **[!UICONTROL size (Long) in KB (dimensione (lunga) in KB)]** al posto della larghezza. Per la personalizzazione basata sulle dimensioni, la proprietà `preferOriginal` assegna le preferenze all’originale se la dimensione del rendering corrispondente è maggiore.

   Allo stesso modo, potete personalizzare l&#39;immagine della pagina Annotazione sovrapponendo `libs/dam/gui/content/assets/annotate/jcr:content/body/content/content/items/content/renditionpicker`.

   ![Sovrapposizione del nodo del selettore delle rappresentazioni in CRXDE per personalizzare l&#39;immagine della pagina Annotazione](assets/renditionpicker-node-crxde.png)

   Per configurare le dimensioni di rappresentazione per una risorsa video, andate al `videopicker` nodo nell’archivio CRX nella posizione `/libs/dam/gui/content/assets/assetpage/jcr:content/body/content/content/items/assetdetail/items/col1/items/assetview/videopicker`, sovrapponete il nodo, quindi modificate la proprietà appropriata.

   >[!NOTE]
   >
   >Le annotazioni video sono supportate solo sui browser con formati video compatibili con HTML5. Inoltre, a seconda del browser, sono supportati diversi formati video.

Per ulteriori informazioni sulla generazione e la visualizzazione di risorse secondarie, consultate [gestire le risorse](managing-linked-subassets.md#generate-subassets)secondarie.

## Delete assets {#deleting-assets}

Per eliminare le risorse, un utente deve disporre di autorizzazioni di eliminazione per `dam/asset`. Se disponete solo di autorizzazioni di modifica, potete modificare solo i metadati della risorsa e aggiungere delle annotazioni alla risorsa. Tuttavia, non potete eliminare la risorsa o i relativi metadati.

Per risolvere o rimuovere i riferimenti in entrata da altre pagine, aggiornate i riferimenti pertinenti prima di eliminare una risorsa. Per impedire agli utenti di eliminare le risorse di riferimento e di lasciare i collegamenti interrotti, disattivate l’opzione di eliminazione forzata mediante una sovrapposizione.

Per eliminare una risorsa o una cartella contenente una risorsa:

1. Andate alla posizione della risorsa o alla cartella da eliminare.

1. Selezionate la risorsa o la cartella, quindi fate clic sull’opzione **[!UICONTROL Elimina]** ![Elimina](assets/do-not-localize/deleteoutline.png) dalla barra degli strumenti.

   Una volta confermata l&#39;eliminazione:

   * Se la risorsa non dispone di riferimenti, viene eliminata.

   * Se la risorsa dispone di riferimenti, un messaggio di errore vi informa che **Una o più risorse dispongono di riferimenti**. Potete selezionare **[!UICONTROL Forza eliminazione]** o **[!UICONTROL Annulla]**.
   >[!NOTE]
   >
   >* Per risolvere o rimuovere i riferimenti in entrata da altre pagine, aggiornate i riferimenti pertinenti prima di eliminare una risorsa. Inoltre, disattivate il pulsante Forza eliminazione con una sovrapposizione, per impedire agli utenti di eliminare le risorse di riferimento e di lasciare i collegamenti interrotti.
   >* È possibile eliminare una *cartella* che contiene i file di risorse estratti. Prima di eliminare una cartella, accertatevi che gli utenti non dispongano di risorse digitali.


>[!NOTE]
>
>Se eliminate una cartella utilizzando il metodo indicato sopra dall’interfaccia utente, vengono eliminati anche i gruppi di utenti associati.
>
>Tuttavia, i gruppi di utenti ridondanti, non utilizzati e generati automaticamente possono essere eliminati dall’archivio utilizzando `clean` il metodo JMX nell’istanza di creazione (`http://[server]:[port]/system/console/jmx/com.day.cq.dam.core.impl.team%3Atype%3DClean+redundant+groups+for+Assets`).

## Scaricare le risorse {#downloading-assets}

Consultate [Scaricare risorse da  Experience Manager](/help/assets/download-assets-from-aem.md).

## Publish assets {#publishing-assets}

>[!NOTE]
>
>Per ulteriori informazioni specifiche per gli elementi multimediali dinamici, consultate [Pubblicazione di risorse per file multimediali dinamici.](/help/assets/publishing-dynamicmedia-assets.md)

1. Andate alla posizione delle risorse o delle cartelle da pubblicare.

1. Either select the **[!UICONTROL Publish]** quick action from the asset card, or select the asset and click the **[!UICONTROL Quick Publish]** option from the toolbar.
1. Se la risorsa fa riferimento ad altre risorse, i relativi riferimenti sono elencati nella procedura guidata. Vengono visualizzati solo i riferimenti non pubblicati o modificati dopo l’ultima pubblicazione o l’annullamento della pubblicazione. Scegliete i riferimenti da pubblicare.

   >[!NOTE]
   >
   >Le cartelle vuote, che fanno parte di una cartella pubblicata, non vengono pubblicate.

1. Fate clic su **[!UICONTROL Pubblica]** per confermare l’attivazione delle risorse.

>[!CAUTION]
>
>Se pubblicate una risorsa in fase di elaborazione, viene pubblicato solo il contenuto originale. Mancano le rappresentazioni. Attendere il completamento dell’elaborazione, quindi pubblicare o pubblicare nuovamente la risorsa al termine dell’elaborazione.

## Annullare la pubblicazione delle risorse {#unpublishing-assets}

1. Andate alla posizione della cartella di risorse o risorse che desiderate rimuovere dall’ambiente di pubblicazione (Annulla pubblicazione).

1. Selezionate la risorsa o la cartella da annullare la pubblicazione, quindi fate clic sull’opzione **[!UICONTROL Gestisci pubblicazione]** ![gestisci pubblicazione nella barra degli strumenti](assets/do-not-localize/globe-publication.png) .

1. Selezionate l’azione **[!UICONTROL Annulla pubblicazione]** dall’elenco.

   ![Annulla pubblicazione, azione](assets/unpublish_action.png)

1. Per annullare la pubblicazione della risorsa in un secondo momento, selezionate **[!UICONTROL Annulla pubblicazione più tardi]**, quindi selezionate una data per annullare la pubblicazione della risorsa.
1. Pianificate una data in cui la risorsa non sarà disponibile dall’ambiente di pubblicazione.
1. Se la risorsa fa riferimento ad altre risorse, scegliete i riferimenti da annullare la pubblicazione. Fate clic su **[!UICONTROL Annulla pubblicazione]**.
1. Nella finestra di dialogo di conferma, fate clic su:

   * **[!UICONTROL Annulla]** per interrompere l’azione
   * **[!UICONTROL Annulla pubblicazione]** per confermare che le risorse non sono più pubblicate (non sono più disponibili nell’ambiente di pubblicazione) alla data specificata.

   >[!NOTE]
   >
   >Per annullare la pubblicazione di una risorsa complessa, annullate la pubblicazione solo della risorsa. Evitate di annullare la pubblicazione dei riferimenti, in quanto ad essi potrebbero fare riferimento altre risorse pubblicate.

## Gruppo utenti chiuso {#closed-user-group}

Per limitare l’accesso a specifiche cartelle di risorse pubblicate viene utilizzato un gruppo di utenti chiuso (CUG) [!DNL Experience Manager]. Se create un gruppo di utenti chiuso per una cartella, l’accesso alla cartella (comprese le risorse e le sottocartelle) è limitato solo ai membri o ai gruppi assegnati. Per accedere alla cartella, devono accedere utilizzando le credenziali di protezione.

I COG consentono di limitare l’accesso alle risorse. Potete anche configurare una pagina di login per la cartella.

1. Selezionate una cartella dall’ [!DNL Assets] interfaccia, quindi fate clic sull’opzione [!UICONTROL Proprietà] nella barra degli strumenti per visualizzare la pagina delle proprietà.
1. Dalla scheda **[!UICONTROL Autorizzazioni]** , aggiungete membri o gruppi in Gruppo **[!UICONTROL utenti]** chiuso.

   ![Aggiunta di un utente a un gruppo di utenti chiuso](assets/add_user.png)

1. Per visualizzare una schermata di login quando gli utenti accedono alla cartella, selezionate l’opzione **[!UICONTROL Abilita]** . Quindi, selezionate il percorso di una pagina di login in [!DNL Experience Manager]e salvate le modifiche.

   ![Abilita e seleziona la pagina di login da visualizzare quando l’utente accede alla cartella](assets/login_page.png)

   >[!NOTE]
   >
   >Se non specificate il percorso di una pagina di login, [!DNL Experience Manager] visualizza la pagina di login predefinita nell’istanza di pubblicazione.

1. Pubblicate la cartella, quindi provate ad accedervi dall’istanza di pubblicazione. Viene visualizzata una schermata di login.
1. Se siete un membro CUG, immettete le vostre credenziali di protezione. La cartella viene visualizzata dopo l’ [!DNL Experience Manager] autenticazione.

## Cercare risorse {#assetsearch}

La ricerca delle risorse è fondamentale per l’utilizzo di un sistema di gestione delle risorse digitali, sia per l’ulteriore utilizzo da parte dei creativi, per una gestione affidabile delle risorse da parte degli utenti aziendali e degli esperti di marketing, sia per l’amministrazione da parte degli amministratori DAM.

Per ricerche semplici, avanzate e personalizzate per individuare e utilizzare le risorse più appropriate, consultate [Cercare risorse in  Experience Manager](search-assets.md).

## Azioni rapide {#quick-actions}

Le icone delle azioni rapide sono disponibili per una singola risorsa alla volta. A seconda del dispositivo, effettuate le seguenti operazioni per visualizzare le icone delle azioni rapide:

* Dispositivi touch: Toccate e tenete premuto. Ad esempio, su un iPad potete toccare e tenere premuto un contenuto per visualizzare le azioni rapide.
* Dispositivi non touch: Puntatore al passaggio del mouse. Ad esempio, su un dispositivo desktop, se passate il puntatore sulla miniatura della risorsa viene visualizzata la barra delle azioni rapide.

### Spostarsi e selezionare le risorse {#navigating-and-selecting-assets}

Potete visualizzare, navigare e selezionare le risorse con una qualsiasi delle viste disponibili (Scheda, Colonna ed Elenco) tramite l&#39;opzione **[!UICONTROL Seleziona]** .

Nelle viste a elenco e a colonne, quando passate il puntatore sulla miniatura della risorsa viene visualizzata l’opzione **[!UICONTROL Seleziona]** .

Nella vista a schede, l&#39;opzione **[!UICONTROL Seleziona]** viene visualizzata come azione rapida.

![Seleziona azione rapida nella vista a schede](assets/select_quick_action.png)

Quando sfogliate una cartella o una raccolta nell&#39;interfaccia [!DNL Assets] utente di un browser, potete selezionare tutte le risorse visualizzate o caricate utilizzando l&#39;opzione [!UICONTROL Seleziona tutto] nell&#39;angolo superiore destro. Inizialmente, solo 100 risorse vengono caricate nella vista a schede e 200 vengono caricate nella vista a elenco. Durante lo scorrimento della pagina dei risultati di ricerca vengono caricate più risorse. L’opzione [!UICONTROL Seleziona tutto] seleziona solo le risorse caricate.

Per ulteriori informazioni, consultate [Visualizzare e selezionare le risorse](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources).

## Modificare le immagini {#editing-images}

Gli strumenti di modifica nell’ [!DNL Assets] interfaccia consentono di eseguire piccoli processi di modifica sulle risorse di immagine. Potete ritagliare, ruotare, capovolgere ed eseguire altri processi di modifica sulle immagini. Potete anche aggiungere mappe immagine alle risorse.

>[!NOTE]
>
>Per alcuni componenti, la modalità Schermo intero dispone di opzioni aggiuntive.

1. Per aprire una risorsa in modalità di modifica, effettuate una delle seguenti operazioni:

   * Selezionate la risorsa e fate clic su **[!UICONTROL Modifica]** nella barra degli strumenti.
   * Fate clic sull&#39;opzione **[!UICONTROL Modifica]** che viene visualizzata su una risorsa nella vista a schede.
   * Fate clic su **[!UICONTROL Modifica]** dall’opzione ![Modifica nella barra degli strumenti](assets/do-not-localize/edit_icon.png).

1. Per ritagliare l’immagine, fate clic su **[!UICONTROL Ritaglia]** ![opzione per ritagliare un’immagine](assets/do-not-localize/crop.png).

1. Seleziona l’opzione desiderata dall’elenco. L’area di ritaglio viene visualizzata sull’immagine in base all’opzione scelta. L’opzione **Mano libera** consente di ritagliare l’immagine senza limitazioni di proporzioni.

   ![Opzioni di ritaglio](assets/crop-options.png)

1. Selezionate l’area da ritagliare e ridimensionatela o riposizionatela sull’immagine.

1. Per ripristinare l’immagine non ritagliata o mantenere l’immagine ritagliata, usate le opzioni **** Annulla ![](assets/do-not-localize/undo.png) Annulla e **[!UICONTROL Ripristina]** barra degli strumenti ![](assets/do-not-localize/redo.png) .
1. Fate clic sull’opzione **[!UICONTROL Ruota]** appropriata per ruotare l’immagine in senso orario o antiorario.

   ![Opzioni di rotazione in senso orario e antiorario](assets/do-not-localize/rotate-options.png)

1. Fate clic sulle opzioni **[!UICONTROL Rifletti]** appropriate per riflettere l’immagine in orizzontale e ![riflettere l’opzione](assets/do-not-localize/flip-horizontal.png) orizzontale o verticale per ![riflettere l’opzione](assets/do-not-localize/flip-vertical.png)verticale.

1. Per completare la modifica delle immagini, fate clic sull’opzione **[!UICONTROL Fine]** ![fine](assets/do-not-localize/check-ok-done-icon.png). Facendo clic su **Fine** viene avviata anche la rigenerazione delle rappresentazioni.

>[!NOTE]
>
>La modifica delle immagini è supportata per i formati di file BMP, GIF, PNG e JPEG.

Potete anche aggiungere mappe immagine utilizzando l’editor immagini. Per informazioni dettagliate, consultate [Aggiunta di mappe](/help/assets/image-maps.md)immagine.

>[!NOTE]
>
>Per modificare un file TXT, impostare **Day CQ Link Externalizer** da Configuration Manager.

## Timeline  {#timeline}

La timeline consente di visualizzare vari eventi per un elemento selezionato, ad esempio flussi di lavoro attivi per una risorsa, commenti/annotazioni, registri attività e versioni.

![Ordinare le voci della cronologia per una risorsa](assets/sort_timeline.gif)

*Figura: Ordinare le voci della cronologia per una risorsa.*

>[!NOTE]
>
>Nella console [](/help/assets/manage-collections.md#navigating-the-collections-console)Raccolte, l&#39;elenco **[!UICONTROL Mostra tutto]** contiene opzioni per visualizzare solo commenti e flussi di lavoro. Inoltre, la timeline viene visualizzata solo per le raccolte di livello principale elencate nella console. Non viene visualizzato se vi spostate all&#39;interno di una qualsiasi delle raccolte.

>[!NOTE]
>
>La timeline contiene diverse [opzioni specifiche per i frammenti](/help/assets/content-fragments/content-fragments-managing.md#timeline-for-content-fragments)di contenuto.

## Annotazione delle risorse {#annotating}

Le annotazioni sono commenti o note esplicative aggiunti alle immagini o ai video. Le annotazioni consentono agli addetti al marketing di collaborare e lasciare commenti sulle risorse.

Le annotazioni video sono supportate solo sui browser con formati video compatibili con HTML5. I formati video che [!DNL Assets] supportano dipendono dal browser.

>[!NOTE]
>
>Per i frammenti di contenuto, [le annotazioni vengono create nell’editor](/help/assets/content-fragments/content-fragments-variations.md#annotating-a-content-fragment)frammento.

1. Andate alla posizione della risorsa alla quale desiderate aggiungere delle annotazioni.
1. Fate clic sull’opzione **[!UICONTROL Annota]** da una delle seguenti opzioni:

   * [Azioni rapide](/help/assets/manage-assets.md#quick-actions)
   * Dalla barra degli strumenti dopo aver selezionato la risorsa o aver aperto la pagina della risorsa.

1. Aggiungi un commento nella casella **[!UICONTROL Commento]** posta nella parte inferiore della timeline. In alternativa, contrassegna un’area sull’immagine e aggiungi un’annotazione nella finestra di dialogo **[!UICONTROL Aggiungi annotazione]**.

   ![Commento nella finestra di dialogo Aggiungi annotazione](assets/annotation-comment-box.png)

1. Per notificare all’utente un’annotazione, specificate l’indirizzo e-mail dell’utente e aggiungete il commento. Ad esempio, per notificare ad Aaron MacDonald un&#39;annotazione, immettete @aa. I suggerimenti per tutti gli utenti corrispondenti vengono visualizzati in un elenco. Selezionare l&#39;indirizzo e-mail di Aaron dall&#39;elenco per contrassegnare il commento con il relativo tag. Analogamente, potete assegnare tag a più utenti in qualsiasi punto dell’annotazione, prima o dopo.

   ![Specificate l&#39;indirizzo e-mail dell&#39;utente e aggiungete un commento per inviare una notifica all&#39;utente](assets/annotation-add-user-email.png)

   >[!NOTE]
   >
   >Per un utente non amministratore, i suggerimenti vengono visualizzati solo se l&#39;utente dispone di autorizzazioni di lettura nel `/home` percorso in CRXDE.

1. Dopo aver aggiunto l’annotazione, fate clic su **[!UICONTROL Aggiungi]** per salvarla. Una notifica per l’annotazione viene inviata ad Aaron.

   >[!NOTE]
   >
   >Potete aggiungere più annotazioni prima di salvarle.

1. Fate clic su **[!UICONTROL Chiudi]** per uscire dalla modalità Annotazione.
1. Per visualizzare la notifica, accedete a [!DNL Assets] con le credenziali di Aaron MacDonald e fate clic sull&#39;opzione **[!UICONTROL Notifiche]** per visualizzare la notifica.

   >[!NOTE]
   >
   >Potete anche aggiungere delle annotazioni alle risorse video. Durante l&#39;annotazione dei video, il lettore si mette in pausa per consentire di inserire delle annotazioni in un fotogramma. Per informazioni dettagliate, consultate [Gestione delle risorse](/help/assets/managing-video-assets.md)video.

1. Per scegliere un colore diverso in modo da poter differenziare gli utenti, fate clic sull’opzione Profilo e fate clic su **[!UICONTROL Preferenze]** personali.

   ![Selezionate l’opzione di profilo utente e quindi Preferenze utente per aprire Preferenze utente](assets/User-profile-preferences.png)

   Specify the desired color in the **[!UICONTROL Annotation Color]** box and then click **[!UICONTROL Accept]**.

   ![Selezionate il colore dell’annotazione nelle Preferenze utente per impostare il colore Persona utente](assets/Annotation-color.png)

>[!NOTE]
>
>Potete inoltre aggiungere annotazioni a una raccolta. Tuttavia, se una raccolta contiene raccolte figlie, potete aggiungere solo annotazioni/commenti alla raccolta principale. L&#39;opzione Annota non è disponibile per le raccolte figlie.

### Visualizzare le annotazioni salvate {#viewing-saved-annotations}

1. Per visualizzare le annotazioni salvate per una risorsa, andate alla posizione della risorsa e aprite la pagina della risorsa.

1. Nell’interfaccia del Experience Manager , scegliete **[!UICONTROL Timeline]**.
1. Dall’elenco **[!UICONTROL Mostra tutti]** nella timeline, seleziona **[!UICONTROL Commenti]** per filtrare i risultati in base alle annotazioni.

   Fate clic su un commento nel pannello **[!UICONTROL Timeline]** per visualizzare l’annotazione corrispondente sull’immagine.

   ![Pannello Timeline per visualizzare le annotazioni sull’immagine](assets/timeline-view-annotations.png)

   Fate clic su **[!UICONTROL Elimina]** per eliminare un particolare commento.

### Stampa annotazioni {#printing-annotations}

Se una risorsa dispone di annotazioni o è stata sottoposta a un flusso di lavoro di revisione, potete stampare la risorsa insieme alle annotazioni e rivedere lo stato come file PDF per la revisione offline.

Potete anche scegliere di stampare solo le annotazioni o lo stato della revisione.

Per stampare le annotazioni e verificare lo stato, fare clic su **[!UICONTROL Stampa]** e seguire le istruzioni della procedura guidata. L’opzione **[!UICONTROL Stampa]** viene visualizzata nella barra degli strumenti solo se alla risorsa è stata assegnata almeno un’annotazione o uno stato di revisione.

1. Dall’ [!DNL Assets] interfaccia, aprite la pagina di anteprima di una risorsa.
1. Effettua una delle operazioni seguenti:

   * Per stampare tutte le annotazioni e lo stato della revisione, saltate il punto 3 e andate direttamente al punto 4.
   * Per stampare annotazioni specifiche e verificare lo stato, aprite la [timeline](/help/assets/manage-assets.md#timeline) e passate al punto 3.

1. Per stampare annotazioni specifiche, selezionate le annotazioni dalla timeline.

   ![Selezionare un&#39;annotazione dalla timeline per stamparla](assets/timeline-select-annotations.png)

   Per stampare solo lo stato della revisione, selezionatelo dalla timeline.

1. Click **[!UICONTROL Print]** from the toolbar.

1. Nella finestra di dialogo Stampa, scegliete la posizione in cui visualizzare le annotazioni o lo stato della revisione sul PDF. Ad esempio, se desiderate che le annotazioni o lo stato vengano stampati in alto a destra della pagina che contiene l’immagine stampata, utilizzate l’impostazione **In alto a sinistra** . È selezionato per impostazione predefinita.

   ![Selezionare la posizione dell&#39;annotazione/stato revisione da visualizzare sul PDF dalla finestra di dialogo Stampa](assets/Print-annotation-dialog.png)

   È possibile scegliere altre impostazioni, a seconda della posizione in cui si desidera visualizzare le annotazioni o lo stato nel PDF stampato. Se vuoi che le annotazioni o lo stato vengano visualizzati in una pagina separata dalla risorsa stampata, scegli **[!UICONTROL Pagina successiva]**.

   >[!NOTE]
   >
   >Il rendering delle annotazioni lunghe potrebbe non essere corretto nel file PDF. Per un rendering ottimale,  Adobe consiglia di limitare le annotazioni a 50 parole.

1. Fate clic su **[!UICONTROL Stampa]**. A seconda dell’opzione scelta al passaggio 2, il PDF generato visualizza annotazioni/stato nella posizione specificata. Ad esempio, se scegli di stampare sia le annotazioni che lo stato di revisione utilizzando l’impostazione **In alto a sinistra**, l’output generato sarà simile al file PDF qui riportato.

   ![Stato di annotazione e revisione su PDF generato](assets/annotation-status-pdf.png)

1. Scaricate l’opzione ![Scarica per PDF](assets/do-not-localize/download.png) o stampate le opzioni di ![stampa su PDF](assets/do-not-localize/print.png) utilizzando le opzioni in alto a destra.

   >[!NOTE]
   >
   >Se la risorsa dispone di risorse secondarie, potete stampare tutte le risorse secondarie insieme alle relative specifiche annotazioni a livello di pagina.

   Per modificare l&#39;aspetto del file PDF di cui è stato effettuato il rendering, ad esempio il colore, la dimensione e lo stile del font, il colore dello sfondo dei commenti e degli stati, aprire la configurazione **[!UICONTROL PDF]** Annotation da Configuration Manager e modificare le opzioni desiderate. Ad esempio, per modificare il colore di visualizzazione dello stato approvato, modificate il codice colore nel campo corrispondente. Per informazioni sulla modifica del colore font delle annotazioni, vedere [Annotazione](/help/assets/manage-assets.md#annotating).

   ![Configurazione per la stampa delle annotazioni di risorsa su un documento PDF](assets/annotation-print-pdf-config.png)

   Tornare al file PDF di cui è stato effettuato il rendering e aggiornarlo. Il PDF aggiornato riflette le modifiche apportate.

Se una risorsa include annotazioni in lingue straniere (in particolare lingue non latine), dovete prima configurare CQ-DAM-Handler-Gibson Font Manager Service sul [!DNL Experience Manager] server per poter stampare tali annotazioni. Quando si configura CQ-DAM-Handler-Gibson Font Manager Service, fornire il percorso in cui si trovano i font per le lingue desiderate.

1. Aprite la pagina di configurazione CQ-DAM-Handler-Gibson Font Manager Service dall’URL `https://[aem_server]:[port]/system/console/configMgr/com.day.cq.dam.handler.gibson.fontmanager.impl.FontManagerServiceImpl`.
1. Per configurare CQ-DAM-Handler-Gibson Font Manager Service, effettuate una delle seguenti operazioni:

   * Nell&#39;opzione della directory Font di sistema, specificate il percorso completo della directory dei font nel sistema. Ad esempio, se siete un utente Mac, potete specificare il percorso come */Library/Fonts* nell&#39;opzione di directory Font di sistema. [!DNL Experience Manager] recupera i font da questa directory.
   * Create una directory denominata `fonts` all’interno della `crx-quickstart` cartella. CQ-DAM-Handler-Gibson Font Manager Service recupera automaticamente i font nella posizione `crx-quickstart/fonts`. Potete ignorare questo percorso predefinito dall&#39;opzione di directory Font del server di Adobe .

   * Create una nuova cartella per i font nel sistema e memorizzate i font desiderati nella cartella. Quindi, specificate il percorso completo della cartella nell&#39;opzione di directory Font cliente.

1. Accedere alla configurazione PDF di Annotation dall&#39;URL `https://[aem_server]:[4502]/system/console/configMgr/com.day.cq.dam.core.impl.annotation.pdf.AnnotationPdfConfig`.
1. Configurare il PDF di annotazione con il set corretto di font-family come segue:

   * Includere la stringa `<font_family_name_of_custom_font, sans-serif>` nell&#39;opzione font-family. Ad esempio, se desiderate stampare le annotazioni in CJK (cinese, giapponese e coreano), includete la stringa `Arial Unicode MS, Noto Sans, Noto Sans CJK JP, sans-serif` nell&#39;opzione font-family. Se desiderate stampare le annotazioni in hindi, scaricate il font appropriato e configurate la famiglia di font come Arial Unicode MS, Noto Sans, Noto Sans CJK JP, Noto Sans Devanagari, sans-serif.

1. Riavviate la [!DNL Experience Manager] distribuzione.

Di seguito è riportato un esempio di come è possibile configurare [!DNL Experience Manager] per la stampa di annotazioni in CJK (cinese, giapponese e coreano):

1. Scaricate i font Google Noto CJK dai seguenti collegamenti e archiviateli nella directory dei font configurata in Font Manager Service.

   * Tutti in un font Super CJK: [https://www.google.com/get/noto/help/cjk/](https://www.google.com/get/noto/help/cjk/)
   * Noto Sans (per le lingue europee): [https://www.google.com/get/noto/](https://www.google.com/get/noto/)
   * Nessun font per una lingua selezionata: [https://www.google.com/get/noto/](https://www.google.com/get/noto/)

1. Configurate il file PDF di annotazione impostando il parametro font-family su `Arial Unicode MS, Noto Sans, Noto Sans CJK JP, sans-serif`. Questa configurazione è disponibile per impostazione predefinita e funziona per tutte le lingue europee e CJK.
1. Se la lingua scelta è diversa dalle lingue indicate al punto 2, aggiungere una voce appropriata (separate da virgola) alla famiglia di font predefinita.

## Creare, gestire, visualizzare in anteprima e ripristinare le versioni delle risorse {#asset-versioning}

Il controllo delle versioni crea un’istantanea delle risorse digitali in un momento preciso. La gestione delle versioni consente di ripristinare le risorse a uno stato precedente in un secondo momento. Ad esempio, se desiderate annullare una modifica apportata a una risorsa, ripristinate la versione non modificata della risorsa. In [!DNL Experience Manager]potete creare una versione, visualizzare la revisione corrente, visualizzare le differenze affiancate tra due versioni delle immagini e ripristinare la versione precedente di una risorsa.

Potete creare versioni [!DNL Experience Manager] nei seguenti scenari:

* Caricate una risorsa con lo stesso nome file che esiste nella stessa posizione. Può trattarsi di una nuova risorsa o di una versione modificata della stessa risorsa.
* Modificate un’immagine in [!DNL Experience Manager] e salvate le modifiche.
* Modificate i metadati di una risorsa.
* Utilizzate l&#39;app [!DNL Experience Manager] desktop per estrarre una risorsa esistente, modificarla e [caricare le modifiche](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html?lang=en#edit-assets-upload-updated-assets).

Potete inoltre abilitare il controllo automatico delle versioni tramite un flusso di lavoro. Quando create una versione per una risorsa, i metadati e le rappresentazioni vengono salvati insieme alla versione. Le rappresentazioni sono alternative per il rendering delle stesse immagini, ad esempio una rappresentazione PNG di un file JPEG caricato.

1. Andate alla posizione della risorsa per la quale desiderate creare una versione e fate clic su di essa per aprirne l’anteprima. Nell’angolo superiore sinistro della pagina, aprite il menu e selezionate **[!UICONTROL Timeline]**.

   ![Dal menu di navigazione a sinistra, selezionate l&#39;opzione della timeline](assets/timeline.png)

   *Figura: Aprite il menu dall&#39;area in alto a sinistra della pagina e selezionate l&#39;opzione [!UICONTROL Timeline] .*

1. Per creare una versione della risorsa:

   * Fate clic su **[!UICONTROL Azioni]** in basso.
   * Fate clic su **[!UICONTROL Salva come versione]** per creare una versione per la risorsa. Se necessario, aggiungete un’etichetta e un commento.
   * Fate clic su **[!UICONTROL Crea]** per creare una versione.

      ![Creare la versione della risorsa dalla barra laterale](assets/create-new-version-from-timeline.png)

      *Figura: Create una versione di una risorsa dalla barra laterale sinistra [!UICONTROL Timeline] .*

1. Per visualizzare una versione di una risorsa:

   * Fate clic su **[!UICONTROL Mostra tutto]** nella [!UICONTROL timeline].
   * Fate clic su **[!UICONTROL Versioni]**. Tutte le versioni create per una risorsa sono elencate nella barra laterale sinistra.

   * Selezionate una versione specifica della risorsa e fate clic su **[!UICONTROL Anteprima versione]**.

1. Per ripristinare una versione precedente della risorsa, effettuate le seguenti operazioni. Dopo il ripristino, questa versione viene visualizzata nell&#39; [!DNL Assets] interfaccia ed è disponibile per l&#39;utilizzo.

   * Fate clic su una versione della risorsa. Se necessario, aggiungete un’etichetta e un commento.
   * Click **[!UICONTROL Revert to this Version]**.

      ![Selezionate una versione per ripristinarla](assets/select_version.png)

      *Figura: Selezionate una versione e ripristinatela. Diventa la versione corrente e sarà quindi disponibile per gli utenti DAM.*

1. Per confrontare due versioni di un’immagine, effettuate le seguenti operazioni:
   * Fare clic sulla versione da confrontare con la versione corrente.
   * Trascinate il cursore verso sinistra per sovrapporre la versione corrente alla versione corrente e confrontare.

   ![Utilizza il cursore per confrontare le versioni selezionate di una risorsa con la versione corrente](assets/version-slider.gif)

   *Figura: Usate il cursore per confrontare facilmente le versioni selezionate di una risorsa con la versione corrente.*

### Avviare un flusso di lavoro su una risorsa {#starting-a-workflow-on-an-asset}

Per applicare un flusso di lavoro per elaborare una risorsa, consultate [Avviare il flusso di lavoro su una risorsa](/help/assets/assets-workflow.md#apply-a-workflow-to-an-asset).

## Raccolte {#collections}

Una raccolta è un set ordinato di risorse. Utilizzate le raccolte per condividere risorse correlate tra utenti o per raggruppare risorse simili in un cluster per semplificare l&#39;individuazione.

* Una raccolta può includere risorse da posizioni diverse perché contiene solo riferimenti a tali risorse. Ciascuna raccolta mantiene l&#39;integrità referenziale delle risorse.
* Potete condividere le raccolte con più utenti con diversi livelli di privilegi, tra cui la modifica, la visualizzazione e così via.

Consultate [Gestione delle raccolte](/help/assets/manage-collections.md) per informazioni dettagliate sulla gestione delle raccolte.
