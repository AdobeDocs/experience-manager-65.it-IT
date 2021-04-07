---
title: Risoluzione dei problemi Dynamic Media - Modalità Scene7
description: Risoluzione dei problemi relativi a Dynamic Media quando è in esecuzione in modalità Scene7.
uuid: 77e04ccf-33dc-4d2f-8950-318d4b008f74
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 0d48c031-d3ee-4143-b739-a79ba28fd63a
docset: aem65
role: Business Practitioner, Administrator
exl-id: d4507059-a54d-4dc9-a263-e55dfa27eeb1
feature: Risoluzione dei problemi
translation-type: tm+mt
source-git-commit: 9134130f349c6c7a06ad9658a87f78a86b7dbf9c
workflow-type: tm+mt
source-wordcount: '1286'
ht-degree: 1%

---

# Risoluzione dei problemi Dynamic Media - Modalità Scene7{#troubleshooting-dynamic-media-scene-mode}

Il seguente documento descrive la risoluzione dei problemi relativi alla modalità di esecuzione di Dynamic Media **dynamic_media_scene7**.

## Configurazione e configurazione {#setup-and-configuration}

Assicurati che Dynamic Media sia stato configurato correttamente eseguendo le operazioni seguenti:

* Il comando Start up contiene l&#39;argomento `-r dynamicmedia_scene7` runmode.
* Tutti i pacchetti correzioni cumulativi AEM 6.4 (CFP) sono stati installati prima *prima* di tutti i pacchetti di funzioni Dynamic Media disponibili.
* È installato il Feature Pack 18912 opzionale.

   Questo pacchetto di funzioni opzionale è per il supporto FTP o se stai eseguendo la migrazione delle risorse a Dynamic Media da Dynamic Media Classic.

* Passa all&#39;interfaccia utente dei Cloud Services e verifica che l&#39;account predisposto sia visualizzato in **[!UICONTROL Configurazioni disponibili.]**
* Assicurati che l&#39;agente di replica `Dynamic Media Asset Activation (scene7)` sia abilitato.

   Questo agente di replica si trova in Agenti sull&#39;autore.

## Generale (tutte le risorse) {#general-all-assets}

Di seguito sono riportati alcuni suggerimenti generali per tutte le risorse.

### Proprietà stato sincronizzazione risorse {#asset-synchronization-status-properties}

Le seguenti proprietà delle risorse possono essere riviste in CRXDE Lite per confermare la sincronizzazione della risorsa da AEM a Dynamic Media:

| **Proprietà** | **Esempio** | **Descrizione** |
|---|---|---|
| `<object_node>/jcr:content/metadata/dam:scene7ID` | **`a|364266`** | Indicatore generale che il nodo è collegato a Dynamic Media. |
| `<object_node>/jcr:content/metadata/dam:scene7FileStatus` | **** Testo di PublishCompleteo di errore | Stato del caricamento della risorsa in Dynamic Media. |
| `<object_node>/jcr:content/metadata/dam:scene7File` | **myCompany/myAssetID** | Deve essere popolato per generare URL per la risorsa remota di Dynamic Media. |
| `<object_node>/jcr:content/dam:lastSyncStatus` | **** successore  **non riuscito:`<error text>`** | Stato di sincronizzazione di set (set 360 gradi, set di immagini e così via), predefiniti immagine, predefiniti visualizzatore, aggiornamenti mappa immagine per una risorsa o immagini modificate. |

### Registrazione sincronizzazione {#synchronization-logging}

Gli errori e i problemi di sincronizzazione vengono registrati in `error.log` (AEM directory del server `/crx-quickstart/logs/`). È disponibile una registrazione sufficiente per determinare la causa principale della maggior parte dei problemi, tuttavia è possibile aumentare la registrazione su DEBUG sul pacchetto `com.adobe.cq.dam.ips` tramite la console Sling ([https://localhost:4502/system/console/slinglog](https://localhost:4502/system/console/slinglog)) per raccogliere ulteriori informazioni.

### Sposta, copia, elimina {#move-copy-delete}

Prima di eseguire un&#39;operazione Sposta, Copia o Elimina, eseguire le operazioni seguenti:

* Per immagini e video, verifica che esista un valore `<object_node>/jcr:content/metadata/dam:scene7ID` prima di eseguire le operazioni di spostamento, copia o eliminazione.
* Per i predefiniti per immagini e visualizzatori, verifica che esista un valore `https://<server>/crx/de/index.jsp#/etc/dam/presets/viewer/testpreset/jcr%3Acontent/metadata` prima di eseguire le operazioni di spostamento, copia o eliminazione.
* Se manca il valore dei metadati sopra riportato, è necessario ricaricare le risorse prima di spostare, copiare o eliminare le operazioni.

### Controllo della versione {#version-control}

Quando sostituisci una risorsa Dynamic Media esistente (nome e posizione identici), puoi mantenere entrambe le risorse o sostituire o creare una versione:

* Mantenere entrambi crea una nuova risorsa con un nome univoco per l’URL della risorsa pubblicata. Ad esempio, `image.jpg` è la risorsa originale e `image1.jpg` è la nuova risorsa caricata.

* La creazione di una versione non è supportata nella distribuzione in modalità Dynamic Media - Scene7. La nuova versione sostituirà la risorsa esistente in consegna.

## Immagini e set {#images-and-sets}

Se riscontri problemi con immagini e set, consulta le seguenti indicazioni per la risoluzione dei problemi.

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
       <li>Controlla se il predefinito nel JCR <code>/etc/dam/presets/viewer/&lt;preset&gt; has lastReplicationAction</code> è definito. Tieni presente che questa posizione si applica se hai effettuato l’aggiornamento da AEM 6.x a 6.4 e hai rinunciato alla migrazione. In caso contrario, la posizione è <code>/conf/global/settings/dam/dm/presets/viewer</code>.</li>
       <li>Verifica che la risorsa nel JCR sia <code>dam:scene7FileStatus</code><strong> </strong>sotto Metadati sia visualizzata come <code>PublishComplete</code>.</li>
      </ul> </li>
    </ol> </td>
   <td><p>Aggiorna pagina/passa a un'altra pagina e torna (la barra laterale JSP deve essere ricompilata)</p> <p>Se questo non funziona:</p>
    <ul>
     <li>Pubblica la risorsa.</li>
     <li>Ricarica e pubblica la risorsa.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Selettore risorse nell’editor impostato bloccato nel caricamento perpetuo</td>
   <td><p>Problema noto da risolvere in 6.4</p> </td>
   <td><p>Chiudi il selettore e riaprilo.</p> </td>
  </tr>
  <tr>
   <td><strong></strong> Il pulsante di selezione non è attivo dopo aver selezionato una risorsa come parte della modifica di un set</td>
   <td><p> </p> <p>Problema noto da risolvere in 6.4</p> <p> </p> </td>
   <td><p>Fai clic prima su un’altra cartella nel Selettore risorse e torna indietro per selezionare la risorsa.</p> </td>
  </tr>
  <tr>
   <td>Il punto attivo del carosello si sposta dopo il passaggio tra le diapositive</td>
   <td><p>Verificare che tutte le diapositive abbiano le stesse dimensioni.</p> </td>
   <td><p>Utilizza solo immagini con la stessa dimensione per il carosello.</p> </td>
  </tr>
  <tr>
   <td>L’immagine non viene visualizzata in anteprima con il visualizzatore Dynamic Media</td>
   <td><p>Verifica che la risorsa contenga <code>dam:scene7File</code> nelle proprietà dei metadati (CRXDE Lite)</p> </td>
   <td><p>Verifica che tutte le risorse abbiano completato l’elaborazione.</p> </td>
  </tr>
  <tr>
   <td>La risorsa caricata non viene visualizzata nel selettore delle risorse</td>
   <td><p>Verifica che la risorsa abbia la proprietà <code>jcr:content</code> &gt; <strong><code>dam:assetState</code></strong> = <code>processed</code> (CRXDE Lite)</p> </td>
   <td><p>Verifica che tutte le risorse abbiano completato l’elaborazione.</p> </td>
  </tr>
  <tr>
   <td>Il banner nella vista a schede mostra <strong>Nuovo</strong> quando la risorsa non ha iniziato l’elaborazione</td>
   <td>Controlla la risorsa <code>jcr:content</code> &gt; <code>dam:assetState</code> = se <code>unprocessed</code> non è stato rilevato dal flusso di lavoro.</td>
   <td>Attendi che la risorsa venga raccolta dal flusso di lavoro.</td>
  </tr>
  <tr>
   <td>Le immagini o i set non visualizzano l’URL o il codice di incorporamento del visualizzatore</td>
   <td>Controlla se il predefinito per visualizzatori è stato pubblicato.</td>
   <td><p>Vai a <strong>Strumenti</strong> &gt; <strong>Risorse</strong> &gt; <strong>Predefiniti visualizzatore</strong> e pubblica il predefinito visualizzatore.</p> </td>
  </tr>
 </tbody>
</table>

## Video {#video}

In caso di problemi con il video, consulta le seguenti indicazioni per la risoluzione dei problemi.

<table>
 <tbody>
  <tr>
   <td><strong>Problema</strong></td>
   <td><strong>Come eseguire il debug</strong></td>
   <td><strong>Soluzione</strong></td>
  </tr>
  <tr>
   <td>Impossibile visualizzare in anteprima il video</td>
   <td>
    <ul>
     <li>Verifica che alla cartella sia assegnato un profilo video (se non è supportato). Se non è supportato, viene visualizzata solo un’immagine.</li>
     <li>Il profilo video deve contenere più di un predefinito di codifica per generare un set AVS (le codifiche singole vengono considerate come contenuto video per i file MP4; per i file non supportati, trattati come non elaborati).</li>
     <li>Verifica che l'elaborazione del video sia stata completata confermando <code>dam:scene7FileAvs</code> di <code>dam:scene7File</code> nei metadati.</li>
    </ul> </td>
   <td>
    <ol>
     <li>Assegna un profilo video alla cartella.</li>
     <li>Modifica il profilo video per includere più di un predefinito di codifica.</li>
     <li>Attendere il completamento dell'elaborazione del video.</li>
     <li>Ricarica il video e assicurati che il flusso di lavoro Codifica video Dynamic Media non sia in esecuzione.<br /> </li>
     <li>Ricarica il video.</li>
    </ol> </td>
  </tr>
  <tr>
   <td>Il video non è codificato</td>
   <td>
    <ul>
     <li>Verifica che la modalità di esecuzione sia <code>dynamicmedia_scene7</code>.</li>
     <li>Verifica se il servizio cloud Dynamic Media è configurato.</li>
     <li>Controlla se un profilo video è associato alla cartella di caricamento.</li>
    </ul> </td>
   <td>
    <ol>
     <li>Controlla la tua istanza AEM con <code>-r dynamicmedia_scene7</code></li>
     <li>Verifica che la configurazione di Dynamic Media in Cloud Services sia configurata correttamente.</li>
     <li>Verifica che la cartella disponga di un profilo video. Inoltre, controlla il profilo video.</li>
    </ol> </td>
  </tr>
  <tr>
   <td>L'elaborazione video richiede troppo tempo</td>
   <td><p>Per determinare se la codifica video è ancora in corso o se è stato immesso uno stato di errore:</p>
    <ul>
     <li>Controlla lo stato del video <code>https://localhost:4502/crx/de/index.jsp#/content/dam/folder/videomp4/jcr%3Acontent</code> &gt; <code>dam:assetState</code></li>
     <li>Monitora il video dalla console del flusso di lavoro <code>https://localhost:4502/libs/cq/workflow/content/console.html</code> &gt; Istanze, archivio, errori .</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Rendering video mancante</td>
   <td><p>Quando il video viene caricato, ma non sono presenti rappresentazioni codificate:</p>
    <ul>
     <li>Verifica che alla cartella sia assegnato un profilo video.</li>
     <li>Verifica che l'elaborazione del video sia stata completata confermando <code>dam:scene7FileAvs</code> nei metadati.</li>
    </ul> </td>
   <td>
    <ol>
     <li>Assegna un profilo video alla cartella.</li>
     <li>Attendere il completamento dell'elaborazione del video.<br /> </li>
    </ol> </td>
  </tr>
 </tbody>
</table>

## Visualizzatori {#viewers}

Se riscontri problemi con i visualizzatori, consulta le seguenti indicazioni per la risoluzione dei problemi.

<table>
 <tbody>
  <tr>
   <td><strong>Problema</strong></td>
   <td><strong>Come eseguire il debug</strong></td>
   <td><strong>Soluzione</strong></td>
  </tr>
  <tr>
   <td>I predefiniti per visualizzatori non vengono pubblicati</td>
   <td><p>Passare alla pagina di diagnostica di sample manager: <code>https://localhost:4502/libs/dam/gui/content/s7dam/samplemanager/samplemanager.html</code></p> <p>Osserva i valori calcolati. Quando funziona correttamente, dovresti vedere:</p> <p><code>_DMSAMPLE status: 0 unsyced assets - activation not necessary
       _OOTB status: 0 unsyced assets - 0 unactivated assets</code></p> <p><strong>Nota</strong>: La sincronizzazione delle risorse del visualizzatore può richiedere circa 10 minuti dopo la configurazione delle impostazioni cloud di Dynamic Media.</p> <p>Se le risorse non attivate rimangono, fai clic su uno dei pulsanti <strong>Elenca tutte le risorse non attivate</strong> per visualizzare i dettagli.</p> </td>
   <td>
    <ol>
     <li>Passa all’elenco dei predefiniti per visualizzatori in strumenti di amministrazione: <code>https://localhost:4502/libs/dam/gui/content/s7dam/samplemanager/samplemanager.html</code></li>
     <li>Seleziona tutti i predefiniti visualizzatore, quindi fai clic su <strong>Pubblica</strong>.</li>
     <li>Torna a Sample manager e osserva che il conteggio delle risorse non attivate è ora zero.</li>
    </ol> </td>
  </tr>
  <tr>
   <td>L’immagine del predefinito per visualizzatori restituisce 404 dall’anteprima nei dettagli della risorsa o copia l’URL/codice da incorporare</td>
   <td><p>In CRXDE Lite procedi come segue:</p>
    <ol>
     <li>Passa alla cartella <code>&lt;sync-folder&gt;/_CSS/_OOTB</code> all’interno della cartella di sincronizzazione Dynamic Media (ad esempio, <code>/content/dam/_CSS/_OOTB</code>),</li>
     <li>Trova il nodo di metadati della risorsa problematica (ad esempio, <code>&lt;sync-folder&gt;/_CSS/_OOTB/CarouselDotsLeftButton_dark_sprite.png/jcr:content/metadata/</code>).</li>
     <li>Verifica la presenza delle proprietà <code>dam:scene7*</code> . Se la risorsa è stata sincronizzata e pubblicata correttamente, il set <code>dam:scene7FileStatus</code> è impostato su <strong>PublishComplete</strong>.</li>
     <li>Tentativo di richiedere l’immagine direttamente da Dynamic Media concatenando i valori delle seguenti proprietà e valori letterali stringa
      <ul>
       <li><code>dam:scene7Domain</code></li>
       <li><code>"is/content"</code></li>
       <li><code>dam:scene7Folder</code></li>
       <li><code>&lt;asset-name&gt;</code></li>
       <li>Esempio: <code>https://&lt;server&gt;/is/content/myfolder/_CSS/_OOTB/CarouselDotsLeftButton_dark_sprite.png</code></li>
      </ul> </li>
    </ol> </td>
   <td><p>Se le risorse di esempio o l’immagine predefinita del visualizzatore non sono state sincronizzate o pubblicate, riavvia l’intero processo di copia/sincronizzazione:</p>
    <ol>
     <li>Passa a CRXDE Lite.
      <ul>
       <li>Elimina <code>&lt;sync-folder&gt;/_CSS/_OOTB</code>.</li>
      </ul> </li>
     <li>Passa al gestore dei pacchetti CRX: <code>https://localhost:4502/crx/packmgr/</code><a href="https://localhost:4502/crx/packmgr/"></a>
      <ol>
       <li>Cerca un pacchetto visualizzatore nell’elenco (inizia con <code>cq-dam-scene7-viewers-content</code>)</li>
       <li>Fare clic su <strong>Reinstalla</strong>.</li>
      </ol> </li>
     <li>In Cloud Services, accedi alla pagina Configurazione Dynamic Media, quindi apri la finestra di dialogo di configurazione per la configurazione Dynamic Media - S7.
      <ul>
       <li>Non apportare modifiche, fai clic su <strong>Salva</strong>. Questo attiva nuovamente la logica per creare e sincronizzare le risorse di esempio, i CSS predefiniti per visualizzatori e le immagini.<br />  </li>
      </ul> </li>
    </ol> </td>
  </tr>
 </tbody>
</table>
