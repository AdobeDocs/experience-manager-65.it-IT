---
title: Ristrutturazione dell'archivio di asset in AEM 6.5
description: Scopri come apportare le modifiche necessarie per migrare alla nuova struttura dell’archivio in Adobe Experience Manager (AEM) 6.5 per Assets.
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
feature: Upgrading
exl-id: 28ddd23c-5907-4356-af56-ebc7589a2b5d
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1047'
ht-degree: 2%

---

# Ristrutturazione dell&#39;archivio di asset in AEM 6.5 {#assets-repository-restructuring-in-aem}

Come descritto sull’elemento padre [Ristrutturazione dell’archivio in AEM 6.5](/help/sites-deploying/repository-restructuring.md) I clienti che eseguono l’aggiornamento a Adobe Experience Manager (AEM) 6.5 devono utilizzare questa pagina per valutare l’impegno di lavoro associato alle modifiche dell’archivio che influiscono sulla soluzione AEM Assets. Alcune modifiche richiedono un impegno di lavoro durante il processo di aggiornamento AEM 6.5, mentre altre possono essere differite fino a un aggiornamento futuro.

**Con aggiornamento 6.5**

* [Varie](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#misc)

**Prima di aggiornamenti futuri**

* [Modello di notifica e-mail per evento risorsa/raccolta](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#asset-collection-event-e-mail-notification-template)
* [Progettazioni condivisioni risorse classiche](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#classic-asset-share-designs)
* [Scarica modello di notifica e-mail per risorsa](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#download-asset-e-mail-notification-template)
* [Esempio di licenze DRM](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#example-drm-licenses)
* [Modello di notifica tramite posta elettronica condivisione collegamenti](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#link-share-e-mail-notification-template)
* [Script flusso di lavoro InDesign](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#indesign-workflow-scripts)
* [Configurazioni di trascodifica video](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#video-transcoding-configurations)
* [Varie](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#misc2)

## Con aggiornamento 6.5 {#with-upgrade}

### Varie {#misc}

<table>
 <tbody>
  <tr>
   <td><strong>Posizione precedente</strong></td>
   <td>/etc/dam/jobs</td>
  </tr>
  <tr>
   <td><strong>Nuove posizioni</strong></td>
   <td>/var/dam/jobs</td>
  </tr>
  <tr>
   <td><strong>Orientamenti per la ristrutturazione</strong></td>
   <td><p>Se un codice personalizzato dipende da questa posizione, ovvero il codice si basa esplicitamente su questo percorso, è necessario aggiornare il codice per utilizzare la nuova posizione prima di eseguire l'aggiornamento. Idealmente, le API Java™ vengono utilizzate quando disponibili per ridurre le dipendenze da qualsiasi percorso specifico nel JCR.</p> <p>Percorso temporaneo in cui inserire un file zip da scaricare per il client. Non è necessario eseguire l’aggiornamento da quando il client richiede di scaricare la risorsa. Genera un file nella nuova posizione.</p> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td>N/D</td>
  </tr>
 </tbody>
</table>

## Prima di aggiornamenti futuri {#prior-to-upgrade}

### Modello di notifica e-mail per evento risorsa/raccolta {#asset-collection-event-e-mail-notification-template}

<table>
 <tbody>
  <tr>
   <td><strong>Posizione precedente</strong></td>
   <td><code>/etc/notification/email/default</code></td>
  </tr>
  <tr>
   <td><strong>Nuove posizioni</strong></td>
   <td><p><code>/libs/settings/dam/notification</code></p> <p><code>/apps/settings/dam/notification</code></p> </td>
  </tr>
  <tr>
   <td><strong>Orientamenti per la ristrutturazione</strong></td>
   <td><p>Se i modelli di posta elettronica sono stati modificati dal cliente, eseguire le azioni seguenti per allinearli alla nuova struttura dell'archivio:</p>
    <ol>
     <li>Il <code>/libs/settings/dam/notification</code> copia del modello di posta elettronica da <strong><code>/etc/notification/email/default</code></strong> a <strong><code>/apps/settings/notification/email/default</code></strong>
      <ol>
       <li>Perché la destinazione è in<strong> <code>/apps</code></strong>, la modifica deve essere resa persistente in SCM.</li>
      </ol> </li>
     <li>Rimuovi la cartella: <strong><code>/etc/dam/notification/email/default</code></strong> dopo lo spostamento dei modelli di posta elettronica al suo interno.<br />
      <ol>
       <li>Se non sono stati apportati aggiornamenti al modello di posta elettronica in<strong> <code>/etc/notification/email/default</code></strong>, la cartella può essere rimossa poiché il modello di posta elettronica originale esiste in <strong><code>/libs/settings/notification/email/default</code></strong> nell’ambito dell’installazione dell’AEM 4.</li>
      </ol> </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td>N/D<br /> </td>
  </tr>
 </tbody>
</table>

### Progettazioni condivisioni risorse classiche {#classic-asset-share-designs}

<table>
 <tbody>
  <tr>
   <td><strong>Posizione precedente</strong></td>
   <td><code>/etc/designs/assetshare</code></td>
  </tr>
  <tr>
   <td><strong>Nuove posizioni</strong></td>
   <td><p><code>/libs/settings/wcm/designs/assetshare</code></p> <p><code>/apps/settings/wcm/designs/assetshare</code></p> </td>
  </tr>
  <tr>
   <td><strong>Orientamenti per la ristrutturazione</strong></td>
   <td><p>Per qualsiasi design gestito in SCM e non scritto in fase di esecuzione tramite finestre di dialogo per progettazione, eseguire le azioni seguenti per allinearlo al modello più recente:</p>
    <ol>
     <li>Copia le progettazioni dalla posizione precedente alla nuova posizione in <code>/apps</code>.</li>
     <li>Convertire qualsiasi risorsa CSS, JavaScript e statica nella progettazione in una <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">Libreria client</a> con <code>allowProxy = true</code>.</li>
     <li>Aggiornare i riferimenti alla posizione precedente in <code>cq:designPath</code> proprietà a titolo di <strong>AEM &gt; Amministratore DAM &gt; Pagina condivisione risorse &gt; Proprietà pagina &gt; Scheda Avanzate &gt; Campo di progettazione</strong>.</li>
     <li>Per utilizzare la nuova categoria Libreria client, aggiorna tutte le pagine che fanno riferimento alla posizione precedente. Questo richiede l’aggiornamento del codice di implementazione della pagina.</li>
     <li>Aggiorna le regole di Dispatcher in modo da poter consentire la distribuzione di librerie client tramite <code>/etc.clientlibs/</code> servlet proxy</li>
    </ol> <p>Per le progettazioni non gestite in SCM e le progettazioni modificate in fase di esecuzione tramite le finestre di dialogo per progettazione, non spostare le progettazioni modificabili da <code>/etc</code>.</p> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td>N/D<br /> </td>
  </tr>
 </tbody>
</table>

### Scarica modello di notifica e-mail per risorsa {#download-asset-e-mail-notification-template}

<table>
 <tbody>
  <tr>
   <td><strong>Posizione precedente</strong></td>
   <td><code>/etc/dam/workflow/notification/email/downloadasset</code></td>
  </tr>
  <tr>
   <td><strong>Nuove posizioni</strong></td>
   <td><p><code>/libs/settings/dam/workflownotification/email/downloadasset</code></p> <p><code>/apps/settings/dam/workflownotification/email/downloadasset</code></p> </td>
  </tr>
  <tr>
   <td><strong>Orientamenti per la ristrutturazione</strong></td>
   <td><p>Se i modelli di posta elettronica (<strong>downloadasset</strong> o <strong>transientworkflowcompleted</strong>) sono stati modificati, quindi segui la procedura seguente per allinearli alla nuova struttura:</p>
    <ol>
     <li>Il modello di posta elettronica aggiornato deve essere copiato da <strong><code>/etc/dam/workflow/notification/email/downloadasset</code></strong> a <strong><code>/apps/settings/dam/workflow/notification/email/downloadasset</code></strong>
      <ol>
       <li>Perché la destinazione è in<strong> <code>/apps</code></strong>, la modifica deve essere resa persistente in SCM.</li>
      </ol> </li>
     <li>Rimuovi la cartella: <code>/etc/dam/workflow/notification/email/downloadasset </code>dopo lo spostamento dei modelli di posta elettronica al suo interno.<br />
      <ol>
       <li>Se non sono stati apportati aggiornamenti al modello di posta elettronica in<strong> <code>/etc</code></strong>, la cartella può essere rimossa poiché il modello di posta elettronica originale esiste in <strong><code>/libs/settings/dam/workflownotification/email/downloadasset</code></strong> come parte dell’installazione di AEM 6.4.</li>
      </ol> </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td>Mentre <code>/conf/global/settings/dam/workflownotification/email/downloadasset</code> è tecnicamente supportato per la ricerca (ha la precedenza prima di /apps tramite la normale ricerca Sling CAConfig, ma dopo <code>/etc</code>) il modello può essere inserito in <code>/conf/global/settings/dam/workflownotification/email/downloadasset</code>. Tuttavia, questa operazione non è consigliata in quanto non esiste un'interfaccia utente di runtime per facilitare la modifica del modello di posta elettronica.</td>
  </tr>
 </tbody>
</table>

### Esempio di licenze DRM {#example-drm-licenses}

| **Posizione precedente** | `/etc/dam/drm/licenses/` |
|---|---|
| **Nuove posizioni** | `/libs/settings/dam/drm` |
| **Orientamenti per la ristrutturazione** | N/D |
| **Note** | N/D |

### Modello di notifica tramite posta elettronica condivisione collegamenti {#link-share-e-mail-notification-template}

<table>
 <tbody>
  <tr>
   <td><strong>Posizione precedente</strong></td>
   <td><code>/etc/dam/adhocassetshare</code></td>
  </tr>
  <tr>
   <td><strong>Nuove posizioni</strong></td>
   <td><p><code>/libs/settings/dam/adhocassetshare</code></p> <p><code>/apps/settings/dam/adhocassetshare</code></p> </td>
  </tr>
  <tr>
   <td><strong>Orientamenti per la ristrutturazione</strong></td>
   <td><p>Se il modello e-mail è stato modificato dal cliente, per allinearlo alla nuova struttura dell’archivio:</p>
    <ol>
     <li>Il modello di posta elettronica aggiornato deve essere copiato da <strong><code>/etc/dam/adhocassetshare</code></strong> a <strong><code>/apps/settings/dam/adhocassetshare</code></strong>
      <ol>
       <li>Perché la destinazione è in<strong><code>/apps</code></strong>, la modifica deve essere resa persistente in SCM.</li>
      </ol> </li>
     <li>Rimuovi la cartella: <strong><code>/etc/dam/adhocassetshare</code></strong> dopo lo spostamento dei modelli di posta elettronica al suo interno.<br />
      <ol>
       <li>Se non sono stati apportati aggiornamenti al modello di posta elettronica in<strong> <code>/etc</code></strong>, la cartella può essere rimossa poiché il modello di posta elettronica originale esiste in <strong><code>/libs/settings/dam/adhocassetshare</code></strong> come parte dell’installazione di AEM 6.4.</li>
      </ol> </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td>Mentre <code>/conf/global/settings/dam/adhocassetshare</code> è tecnicamente supportato per la ricerca (ha la precedenza prima <code>/apps</code> tramite la consueta ricerca Sling CAConfig, ma dopo <code>/etc</code>), il modello può essere inserito in <code>/conf/global/settings/dam/adhocassetshare</code>. Tuttavia, questa operazione non è consigliata in quanto non esiste un'interfaccia utente di runtime per facilitare la modifica del modello di posta elettronica</td>
  </tr>
 </tbody>
</table>

### Script flusso di lavoro InDesign {#indesign-workflow-scripts}

<table>
 <tbody>
  <tr>
   <td><strong>Posizione precedente</strong></td>
   <td><code>/etc/dam/indesign/scripts</code></td>
  </tr>
  <tr>
   <td><strong>Nuove posizioni</strong></td>
   <td><p><code>/libs/settings/dam/indesign</code></p> <p><code>/apps/settings/dam/indesign</code></p> </td>
  </tr>
  <tr>
   <td><strong>Orientamenti per la ristrutturazione</strong></td>
   <td><p>Per allinearsi alla nuova struttura dell’archivio:</p>
    <ol>
     <li>Copia tutti gli script personalizzati o modificati da <strong><code>/etc/dam/indesign/scripts</code></strong> a <strong><code>/apps/settings/dam/indesign/scripts</code></strong><br />
      <ol>
       <li>È possibile copiare script nuovi o modificati solo come script non modificati forniti da AEM tramite <strong><code>/libs/settings</code></strong> AEM 6.5</li>
      </ol> </li>
     <li>Individua tutti i modelli di flusso di lavoro che utilizzano il passaggio WF del processo di estrazione file multimediali e
      <ol>
       <li>Per ogni istanza del passaggio del flusso di lavoro, aggiorna i percorsi nella configurazione in modo che puntino esplicitamente agli script corretti in<strong> <code>/apps/settings/dam/indesign/scripts</code></strong> o <strong><code>/libs/settings/dam/indesign/scripts</code></strong> se del caso.</li>
      </ol> </li>
     <li>Rimuovi<strong> <code>/etc/dam/indesign/scripts</code></strong> interamente.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td>Si consiglia di memorizzare gli script personalizzati in <code>/apps</code>, poiché è la posizione in cui deve essere memorizzato il codice.</td>
  </tr>
 </tbody>
</table>

### Configurazioni di trascodifica video {#video-transcoding-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>Posizione precedente</strong></td>
   <td><code>/etc/dam/video</code></td>
  </tr>
  <tr>
   <td><strong>Nuove posizioni</strong></td>
   <td><p><code>/libs/settings/dam/video</code></p> <p><code>/apps/settings/dam/video</code></p> </td>
  </tr>
  <tr>
   <td><strong>Orientamenti per la ristrutturazione</strong></td>
   <td><p>Le personalizzazioni a livello di progetto devono essere tagliate e incollate in equivalenti <code>/apps</code> o <code>/conf</code> percorsi, se applicabile.</p> <p>Per allinearsi alla struttura dell’archivio AEM 6.4:</p>
    <ol>
     <li>Copia le configurazioni video modificate da <code>/etc/dam/video</code> a <code>/apps/settings/dam/video</code></li>
     <li>Rimuovi <code>/etc/dam/video</code></li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td>N/D</td>
  </tr>
 </tbody>
</table>

### Configurazioni predefiniti visualizzatore {#viewer-preset-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>Posizione precedente</strong></td>
   <td><code>/etc/dam/presets/viewer</code></td>
  </tr>
  <tr>
   <td><strong>Nuove posizioni</strong></td>
   <td><p><code>/libs/settings/dam/dm/presets/viewer</code></p> <p><code>/conf/global/settings/dam/dm/presets/viewer</code></p> </td>
  </tr>
  <tr>
   <td><strong>Orientamenti per la ristrutturazione</strong></td>
   <td><p>Per il predefinito visualizzatore pronto all’uso, è disponibile solo nella nuova posizione.</p> <p>Per il predefinito per visualizzatori personalizzati:</p>
    <ul>
     <li>esegui uno script di migrazione da cui spostare il nodo <code>/etc</code> a <code>/conf</code>. Lo script si trova in <em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></li>
     <li>oppure puoi modificare la configurazione e salvarla automaticamente nella nuova posizione.</li>
    </ul> <p>Non è necessario modificare il codice copyURL/embed per puntare a <code>/conf</code>. La richiesta esistente a <code>/etc</code> viene reindirizzato al contenuto corretto da <code>/conf</code>.</p> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td>N/D</td>
  </tr>
 </tbody>
</table>

### Varie {#misc2}

<table>
 <tbody>
  <tr>
   <td><strong>Posizione precedente</strong></td>
   <td><p><code>/etc/clientlibs/foundation/asseteditor</code></p> <p><code>/etc/clientlibs/foundation/assetshare</code></p> <p><code>/etc/clientlibs/foundation/assetinsights</code></p> </td>
  </tr>
  <tr>
   <td><strong>Nuove posizioni</strong></td>
   <td><code>/libs/dam/clientlibs</code></td>
  </tr>
  <tr>
   <td><strong>Orientamenti per la ristrutturazione</strong></td>
   <td><p>Regola eventuali riferimenti per puntare alle nuove risorse in <code>/libs</code> utilizzando <code>/etc.clientlibs/</code> consenti prefisso proxy.</p> <p>Infine, effettua la pulizia rimuovendo le cartelle per le clientlibs migrate da <code>/etc/clientlibs/foundation/</code></p> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td>N/D<br /> </td>
  </tr>
 </tbody>
</table>
