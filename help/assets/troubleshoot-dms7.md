---
title: Risoluzione dei problemi relativi alla modalità Dynamic Media - Scene7
description: Risoluzione di problemi relativi ad Dynamic Media in modalità di esecuzione di Scene7.
uuid: 77e04ccf-33dc-4d2f-8950-318d4b008f74
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 0d48c031-d3ee-4143-b739-a79ba28fd63a
docset: aem65
translation-type: tm+mt
source-git-commit: e916f70549197ac9f95443e972401a78735b0560
workflow-type: tm+mt
source-wordcount: '1282'
ht-degree: 1%

---


# Risoluzione dei problemi relativi alla modalità Dynamic Media - Scene7{#troubleshooting-dynamic-media-scene-mode}

Nel seguente documento viene descritta la risoluzione dei problemi relativi alla modalità di esecuzione di Dynamic Media **dynamicmedia_scene7** .

## Configurazione e configurazione {#setup-and-configuration}

Verificate che Dynamic Media sia stato configurato correttamente effettuando le seguenti operazioni:

* Il comando Start up contiene l&#39;argomento `-r dynamicmedia_scene7` runmode.
* Eventuali pacchetti di correzioni cumulative AEM 6.4 (CFP) sono stati installati prima *di ogni* pacchetto di funzioni Dynamic Media disponibile.
* È installato Feature Pack 18912 opzionale.

   Questo pacchetto di funzioni opzionale è disponibile per il supporto FTP o se state eseguendo la migrazione delle risorse ad Dynamic Media da Dynamic Media Classic (Scene7).

* Andate all&#39;interfaccia utente di Cloud Services e verificate che l&#39;account di provisioning sia visualizzato in Configurazioni **[!UICONTROL disponibili.]**
* Assicurarsi che l&#39;agente di `Dynamic Media Asset Activation (scene7)` replica sia abilitato.

   Questo agente di replica si trova in Agenti in Autore.

## Generale (tutte le risorse) {#general-all-assets}

Di seguito sono riportati alcuni suggerimenti e consigli generali per tutte le risorse.

### Proprietà Stato sincronizzazione risorse {#asset-synchronization-status-properties}

In CRXDE Lite è possibile esaminare le seguenti proprietà della risorsa per confermare la corretta sincronizzazione della risorsa da AEM ad Dynamic Media:

| **Proprietà** | **Esempio** | **Descrizione** |
|---|---|---|
| `<object_node>/jcr:content/metadata/dam:scene7ID` | **`a|364266`** | Indicatore generale che il nodo è collegato ad Dynamic Media. |
| `<object_node>/jcr:content/metadata/dam:scene7FileStatus` | **Testo di PublishComplete** o di errore | Stato del caricamento di una risorsa in Dynamic Media. |
| `<object_node>/jcr:content/metadata/dam:scene7File` | **myCompany/myAssetID** | Deve essere popolato per generare URL per la risorsa remota di Dynamic Media. |
| `<object_node>/jcr:content/dam:lastSyncStatus` | **success** o **fail:`<error text>`** | Stato di sincronizzazione di set (set 360 gradi, set di immagini e così via), predefiniti per immagini, predefiniti per visualizzatori, aggiornamenti per mappe immagine per una risorsa o immagini modificate. |

### Registrazione sincronizzazione {#synchronization-logging}

Errori e problemi di sincronizzazione vengono registrati `error.log` (directory del server AEM `/crx-quickstart/logs/`). È disponibile una registrazione sufficiente per determinare la causa principale della maggior parte dei problemi, tuttavia è possibile aumentare la registrazione in DEBUG sul `com.adobe.cq.dam.ips` pacchetto tramite Sling Console ([https://localhost:4502/system/console/slinglog](https://localhost:4502/system/console/slinglog)) per raccogliere ulteriori informazioni.

### Sposta, Copia, Elimina {#move-copy-delete}

Prima di eseguire un&#39;operazione Sposta, Copia o Elimina, effettuate le seguenti operazioni:

* Per immagini e video, verificate che esista un `<object_node>/jcr:content/metadata/dam:scene7ID` valore prima di eseguire operazioni di spostamento, copia o eliminazione.
* Per i predefiniti per immagini e visualizzatori, verificate che esista un `https://<server>/crx/de/index.jsp#/etc/dam/presets/viewer/testpreset/jcr%3Acontent/metadata` valore prima di eseguire le operazioni di spostamento, copia o eliminazione.
* Se questo valore di metadati non è presente, è necessario caricare nuovamente le risorse prima di spostare, copiare o eliminare le operazioni.

### Controllo della versione {#version-control}

Quando sostituite una risorsa Dynamic Media esistente (nome e posizione identici), potete mantenere entrambe le risorse oppure sostituire o creare una versione:

* Entrambi gli elementi creeranno una nuova risorsa con un nome univoco per l’URL della risorsa pubblicata. Ad esempio, `image.jpg` è la risorsa originale e `image1.jpg` la nuova risorsa caricata.

* La creazione di una versione non è supportata in Dynamic Media - Distribuzione in modalità Scene7. La nuova versione sostituirà la risorsa esistente in fase di distribuzione.

## Immagini e set {#images-and-sets}

In caso di problemi con immagini e set, consultate le seguenti istruzioni per la risoluzione dei problemi.

<table>
 <tbody>
  <tr>
   <td><strong>Problema</strong></td>
   <td><strong>Come eseguire il debug</strong></td>
   <td><strong>Soluzione</strong></td>
  </tr>
  <tr>
   <td>Impossibile accedere al pulsante Copia URL/Incorpora nella visualizzazione dei dettagli della risorsa</td>
   <td>
    <ol>
     <li><p>Vai a CRX/DE:</p>
      <ul>
       <li>Verificate se il predefinito nel JCR <code>/etc/dam/presets/viewer/&lt;preset&gt; has lastReplicationAction</code> è definito. Tieni presente che questa posizione si applica se hai effettuato l’aggiornamento da AEM 6.x a 6.4 e hai rinunciato alla migrazione. In caso contrario, la posizione è <code>/conf/global/settings/dam/dm/presets/viewer</code>.</li>
       <li>Verificate che la risorsa nel JCR sia presente <code>dam:scene7FileStatus</code><strong> in Metadati e sia visualizzata come </strong><code>PublishComplete</code>.</li>
      </ul> </li>
    </ol> </td>
   <td><p>Aggiorna pagina/passa a un'altra pagina e torna (la barra laterale JSP deve essere ricompilata)</p> <p>Se questo non funziona:</p>
    <ul>
     <li>Pubblicare la risorsa.</li>
     <li>Caricate nuovamente la risorsa e pubblicatela.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Selettore risorse nell’editor set bloccato nel caricamento perpetuo</td>
   <td><p>Problema noto da risolvere in 6.4</p> </td>
   <td><p>Chiudete il selettore e riapritelo.</p> </td>
  </tr>
  <tr>
   <td><strong>Il pulsante Seleziona</strong> non è attivo dopo aver selezionato una risorsa come parte della modifica di un set</td>
   <td><p> </p> <p>Problema noto da risolvere in 6.4</p> <p> </p> </td>
   <td><p>Fate clic prima su un’altra cartella nel selettore delle risorse e tornate indietro per selezionare la risorsa.</p> </td>
  </tr>
  <tr>
   <td>Il punto di attivazione del carosello si sposta dopo il passaggio tra le diapositive</td>
   <td><p>Verificate che tutte le diapositive abbiano le stesse dimensioni.</p> </td>
   <td><p>Utilizzate solo immagini con la stessa dimensione per il carosello.</p> </td>
  </tr>
  <tr>
   <td>L'immagine non viene visualizzata in anteprima con il visualizzatore Dynamic Media</td>
   <td><p>Verificate che la risorsa contenga <code>dam:scene7File</code> nelle proprietà Metadati (CRXDE Lite)</p> </td>
   <td><p>Verificate che tutte le risorse abbiano completato l'elaborazione.</p> </td>
  </tr>
  <tr>
   <td>La risorsa caricata non viene visualizzata nel selettore delle risorse</td>
   <td><p>La risorsa di controllo ha una proprietà <code>jcr:content</code> &gt; <strong><code>dam:assetState</code></strong> = <code>processed</code> (CRXDE Lite)</p> </td>
   <td><p>Verificate che tutte le risorse abbiano completato l'elaborazione.</p> </td>
  </tr>
  <tr>
   <td>Il banner nella vista a schede mostra <strong>Nuovo</strong> quando la risorsa non ha iniziato l'elaborazione</td>
   <td>Controlla risorsa <code>jcr:content</code> &gt; <code>dam:assetState</code> = se non <code>unprocessed</code> è stata scelta dal flusso di lavoro.</td>
   <td>Attendi che la risorsa venga scelta dal flusso di lavoro.</td>
  </tr>
  <tr>
   <td>Le immagini o i set non visualizzano l’URL del visualizzatore o il codice da incorporare</td>
   <td>Verificate che il predefinito per visualizzatori sia stato pubblicato.</td>
   <td><p>Passate a <strong>Strumenti</strong> &gt; <strong>Risorse</strong> &gt; Predefiniti <strong>per</strong> visualizzatori e pubblicate il predefinito per visualizzatori.</p> </td>
  </tr>
 </tbody>
</table>

## Video {#video}

In caso di problemi con il video, consulta le seguenti istruzioni per la risoluzione dei problemi.

<table>
 <tbody>
  <tr>
   <td><strong>Problema</strong></td>
   <td><strong>Come eseguire il debug</strong></td>
   <td><strong>Soluzione</strong></td>
  </tr>
  <tr>
   <td>Impossibile visualizzare l'anteprima del video</td>
   <td>
    <ul>
     <li>Verificate che alla cartella sia assegnato un profilo video (se il formato file non è supportato). Se non è supportato, viene visualizzata solo un'immagine.</li>
     <li>Il profilo video deve contenere più di un predefinito di codifica per generare un set AVS (le singole codifiche vengono trattate come contenuto video per i file MP4); per i file non supportati, trattati come non elaborati).</li>
     <li>Verificate che il video abbia terminato l’elaborazione confermando <code>dam:scene7FileAvs</code> i <code>dam:scene7File</code> metadati.</li>
    </ul> </td>
   <td>
    <ol>
     <li>Assegnate un profilo video alla cartella.</li>
     <li>Modificate il profilo video per includere più di un predefinito di codifica.</li>
     <li>Attendere il completamento dell'elaborazione video.</li>
     <li>Caricate nuovamente il video, accertatevi che il flusso di lavoro Dynamic Media Encode Video non sia in esecuzione.<br /> </li>
     <li>Caricate nuovamente il video.</li>
    </ol> </td>
  </tr>
  <tr>
   <td>Il video non è codificato</td>
   <td>
    <ul>
     <li>Verificare che la modalità di esecuzione sia <code>dynamicmedia_scene7</code>.</li>
     <li>Verificate che il servizio cloud Dynamic Media sia configurato.</li>
     <li>Controllate se un profilo video è associato alla cartella di caricamento.</li>
    </ul> </td>
   <td>
    <ol>
     <li>Controlla l’istanza di AEM con <code>-r dynamicmedia_scene7</code></li>
     <li>Verifica che la configurazione di Dynamic Media in Servizi cloud sia configurata correttamente.</li>
     <li>Verificate che la cartella disponga di un profilo video. Inoltre, controllate il profilo video.</li>
    </ol> </td>
  </tr>
  <tr>
   <td>L'elaborazione video richiede troppo tempo</td>
   <td><p>Per determinare se la codifica video è ancora in corso o se è stato immesso un errore:</p>
    <ul>
     <li>Controllare lo stato del video <code>https://localhost:4502/crx/de/index.jsp#/content/dam/folder/videomp4/jcr%3Acontent</code> &gt; <code>dam:assetState</code></li>
     <li>Monitora il video dalla console del flusso di lavoro <code>https://localhost:4502/libs/cq/workflow/content/console.html</code> &gt; Istanze, Archivio, Errori.</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Rendering video mancante</td>
   <td><p>Quando il video viene caricato, ma non esistono rappresentazioni codificate:</p>
    <ul>
     <li>Verificate che alla cartella sia assegnato un profilo video.</li>
     <li>Verificate che il video abbia terminato l’elaborazione confermando <code>dam:scene7FileAvs</code> i metadati.</li>
    </ul> </td>
   <td>
    <ol>
     <li>Assegnate un profilo video alla cartella.</li>
     <li>Attendere il completamento dell'elaborazione video.<br /> </li>
    </ol> </td>
  </tr>
 </tbody>
</table>

## Visualizzatori {#viewers}

In caso di problemi con i visualizzatori, consultate le seguenti istruzioni per la risoluzione dei problemi.

<table>
 <tbody>
  <tr>
   <td><strong>Problema</strong></td>
   <td><strong>Come eseguire il debug</strong></td>
   <td><strong>Soluzione</strong></td>
  </tr>
  <tr>
   <td>Predefiniti visualizzatore non pubblicati</td>
   <td><p>Passate alla pagina di diagnostica di esempio manager: <code>https://localhost:4502/libs/dam/gui/content/s7dam/samplemanager/samplemanager.html</code></p> <p>Osservare i valori calcolati. Quando funziona correttamente, dovresti vedere:</p> <p><code>_DMSAMPLE status: 0 unsyced assets - activation not necessary
       _OOTB status: 0 unsyced assets - 0 unactivated assets</code></p> <p><strong>Nota</strong>: Dopo la configurazione delle impostazioni cloud di Dynamic Media, potrebbero essere necessari circa 10 minuti per la sincronizzazione delle risorse del visualizzatore.</p> <p>Se le risorse non attivate rimangono, fate clic su uno dei pulsanti <strong>Elenca tutte le risorse</strong> non attivate per visualizzare i dettagli.</p> </td>
   <td>
    <ol>
     <li>Passate all’elenco dei predefiniti per visualizzatori negli strumenti di amministrazione: <code>https://localhost:4502/libs/dam/gui/content/s7dam/samplemanager/samplemanager.html</code></li>
     <li>Selezionate tutti i predefiniti per visualizzatori, quindi fate clic su <strong>Pubblica</strong>.</li>
     <li>Tornate alla gestione degli esempi e tenete presente che il conteggio delle risorse non attivate è ora pari a zero.</li>
    </ol> </td>
  </tr>
  <tr>
   <td>L’immagine del predefinito per visualizzatori restituisce 404 dall’anteprima nei dettagli delle risorse o dal codice URL/incorporato</td>
   <td><p>In CRXDE Lite effettuate le seguenti operazioni:</p>
    <ol>
     <li>Andate alla <code>&lt;sync-folder&gt;/_CSS/_OOTB</code> cartella di sincronizzazione Dynamic Media (ad esempio, <code>/content/dam/_CSS/_OOTB</code>),</li>
     <li>Individuate il nodo di metadati della risorsa problematica (ad esempio, <code>&lt;sync-folder&gt;/_CSS/_OOTB/CarouselDotsLeftButton_dark_sprite.png/jcr:content/metadata/</code>).</li>
     <li>Verificare la presenza di <code>dam:scene7*</code> proprietà. Se la risorsa è stata sincronizzata e pubblicata correttamente, il <code>dam:scene7FileStatus</code> set è <strong>PubblicaCompletato</strong>.</li>
     <li>Tentativo di richiedere l'immagine direttamente da Dynamic Media concatenando i valori delle seguenti proprietà e stringhe letterali
      <ul>
       <li><code>dam:scene7Domain</code></li>
       <li><code>"is/content"</code></li>
       <li><code>dam:scene7Folder</code></li>
       <li><code>&lt;asset-name&gt;</code></li>
       <li>Esempio: <code>https://&lt;server&gt;/is/content/myfolder/_CSS/_OOTB/CarouselDotsLeftButton_dark_sprite.png</code></li>
      </ul> </li>
    </ol> </td>
   <td><p>Se le risorse campione o l’immagine del predefinito per visualizzatori non sono sincronizzate o pubblicate, riavviate l’intero processo di copia/sincronizzazione:</p>
    <ol>
     <li>Passare a CRXDE Lite.
      <ul>
       <li>Elimina <code>&lt;sync-folder&gt;/_CSS/_OOTB</code>.</li>
      </ul> </li>
     <li>Andate al gestore pacchetti CRX: <code>https://localhost:4502/crx/packmgr/</code><a href="https://localhost:4502/crx/packmgr/"></a>
      <ol>
       <li>Cerca il pacchetto del visualizzatore nell’elenco (inizia con <code>cq-dam-scene7-viewers-content</code>)</li>
       <li>Fate clic su <strong>Reinstalla</strong>.</li>
      </ol> </li>
     <li>In Servizi cloud, andate alla pagina Configurazione Dynamic Media, quindi aprite la finestra di dialogo di configurazione per la configurazione Dynamic Media - S7.
      <ul>
       <li>Non apportare modifiche, fate clic su <strong>Salva</strong>. Questo attiva di nuovo la logica per creare e sincronizzare le risorse campione, i predefiniti per visualizzatori CSS e la grafica.<br />  </li>
      </ul> </li>
    </ol> </td>
  </tr>
 </tbody>
</table>

