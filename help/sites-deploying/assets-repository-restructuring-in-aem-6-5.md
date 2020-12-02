---
title: Ristrutturazione del repository delle risorse in AEM 6.5
seo-title: Ristrutturazione del repository delle risorse in AEM 6.5
description: Scopri come apportare le modifiche necessarie per eseguire la migrazione alla nuova struttura del repository in AEM 6.5 per Assets.
seo-description: Scopri come apportare le modifiche necessarie per eseguire la migrazione alla nuova struttura del repository in AEM 6.5 per Assets.
uuid: 0e3d8163-6274-4d1b-91c7-32ca927fb83c
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
discoiquuid: 212930fc-3430-4a0a-842c-2fb613ef981f
translation-type: tm+mt
source-git-commit: d20ddba254c965e1b0c0fc84a482b7e89d4df5cb
workflow-type: tm+mt
source-wordcount: '1060'
ht-degree: 2%

---


# Ristrutturazione dell&#39;archivio risorse in AEM 6.5 {#assets-repository-restructuring-in-aem}

Come descritto nella pagina [Ristrutturazione repository principale di AEM 6.5](/help/sites-deploying/repository-restructuring.md), i clienti che effettuano l&#39;aggiornamento a AEM 6.5 devono utilizzare questa pagina per valutare lo sforzo di lavoro associato alle modifiche del repository che hanno un impatto sulla soluzione  AEM Assets. Alcune modifiche richiedono sforzi di lavoro durante il processo di aggiornamento di AEM 6.5, mentre altre possono essere posticipate fino a un aggiornamento futuro.

**Con aggiornamento 6.5**

* [Misc](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#misc)

**Prima dell&#39;aggiornamento futuro**

* [Modello di notifica e-mail evento Asset/Collection](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#asset-collection-event-e-mail-notification-template)
* [Progettazione di condivisione risorse classiche](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#classic-asset-share-designs)
* [Scarica modello di notifica e-mail risorsa](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#download-asset-e-mail-notification-template)
* [Esempi di licenze DRM](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#example-drm-licenses)
* [Modello di notifica e-mail condivisione collegamenti](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#link-share-e-mail-notification-template)
* [ script di flusso di lavoro InDesign](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#indesign-workflow-scripts)
* [Configurazioni di transcodifica video](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#video-transcoding-configurations)
* [Misc](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#misc2)

## Con aggiornamento 6.5 {#with-upgrade}

### Misc {#misc}

<table>
 <tbody>
  <tr>
   <td><strong>Posizione precedente</strong></td>
   <td>/etc/dam/Jobs</td>
  </tr>
  <tr>
   <td><strong>Nuove posizioni</strong></td>
   <td>/var/dam/jobs</td>
  </tr>
  <tr>
   <td><strong>Orientamenti per la ristrutturazione</strong></td>
   <td><p>Se un codice personalizzato dipende da questa posizione (ad esempio il codice si basa esplicitamente su questo percorso), quindi il codice deve essere aggiornato per utilizzare la nuova posizione prima dell'aggiornamento; Idealmente le API Java vengono utilizzate quando disponibili per ridurre le dipendenze da un percorso specifico nel JCR.</p> <p>Percorso temporaneo per il blocco del file zip per il download del client. Non è necessario effettuare l’aggiornamento dal momento in cui il client richiede di scaricare la risorsa. Il file verrà generato nella nuova posizione.</p> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td>N/D</td>
  </tr>
 </tbody>
</table>

## Prima dell&#39;aggiornamento futuro {#prior-to-upgrade}

### Modello di notifica e-mail evento risorsa/raccolta {#asset-collection-event-e-mail-notification-template}

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
   <td><p>Se i modelli e-mail sono stati modificati dal cliente, eseguire le azioni seguenti per allineare con la nuova struttura del repository:</p>
    <ol>
     <li>Il modello di posta elettronica <code>/libs/settings/dam/notification</code> deve essere copiato da <strong><code>/etc/notification/email/default</code></strong> a <strong><code>/apps/settings/notification/email/default</code></strong>
      <ol>
       <li>Poiché la destinazione è in <strong> <code>/apps</code></strong> questa modifica deve essere persistente in SCM.</li>
      </ol> </li>
     <li>Rimuovete la cartella: <strong><code>/etc/dam/notification/email/default</code></strong> dopo lo spostamento dei modelli di posta elettronica all'interno.<br />
      <ol>
       <li>Se non sono stati apportati aggiornamenti al modello e-mail in <strong> <code>/etc/notification/email/default</code></strong>, è possibile rimuovere la cartella poiché il modello e-mail originale esiste in <strong><code>/libs/settings/notification/email/default</code></strong> come parte dell'installazione AEM 4.</li>
      </ol> </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td>N/D<br /> </td>
  </tr>
 </tbody>
</table>

### Design classici per la condivisione di risorse {#classic-asset-share-designs}

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
   <td><p>Per tutte le progettazioni gestite in SCM e non scritte in fase di esecuzione tramite le finestre di dialogo Progettazione, eseguire le azioni seguenti per l'allineamento al modello più recente:</p>
    <ol>
     <li>Copiate le progettazioni dalla posizione precedente alla nuova posizione in <code>/apps</code>.</li>
     <li>Convertite eventuali risorse CSS, JavaScript e statiche nella progettazione in una <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">libreria client</a> con <code>allowProxy = true</code>.</li>
     <li>Aggiorna i riferimenti alla posizione precedente nella proprietà <code>cq:designPath</code> tramite <strong>AEM &gt; Amministratore DAM &gt; Pagina condivisione risorse &gt; Proprietà pagina &gt; scheda Avanzate &gt; Campo di progettazione</strong>.</li>
     <li>Aggiorna tutte le pagine che fanno riferimento al percorso precedente per utilizzare la nuova categoria Libreria client. Ciò richiede l’aggiornamento del codice di implementazione della pagina.</li>
     <li>Aggiornate le regole del dispatcher per consentire la trasmissione delle librerie client tramite il servlet proxy <code>/etc.clientlibs/</code>.</li>
    </ol> <p>Per qualsiasi progettazione non gestita in SCM e modificata in fase di esecuzione tramite le finestre di dialogo Progettazione, non spostare i progetti modificabili da <code>/etc</code>.</p> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td>N/D<br /> </td>
  </tr>
 </tbody>
</table>

### Download del modello di notifica e-mail delle risorse {#download-asset-e-mail-notification-template}

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
   <td><p>Se i modelli e-mail (<strong>downloadasset</strong> o <strong>transientworkflowcompleted</strong>) sono stati modificati, segui la procedura seguente per allineare la nuova struttura:</p>
    <ol>
     <li>Il modello di posta elettronica aggiornato deve essere copiato da <strong><code>/etc/dam/workflow/notification/email/downloadasset</code></strong> a <strong><code>/apps/settings/dam/workflow/notification/email/downloadasset</code></strong>
      <ol>
       <li>Poiché la destinazione è in <strong> <code>/apps</code></strong> questa modifica deve essere persistente in SCM.</li>
      </ol> </li>
     <li>Rimuovete la cartella: <code>/etc/dam/workflow/notification/email/downloadasset </code>dopo lo spostamento dei modelli di posta elettronica all'interno.<br />
      <ol>
       <li>Se non sono stati eseguiti aggiornamenti al modello e-mail in <strong> <code>/etc</code></strong>, è possibile rimuovere la cartella perché il modello e-mail originale esiste in <strong><code>/libs/settings/dam/workflownotification/email/downloadasset</code></strong> come parte dell'installazione AEM 6.4.</li>
      </ol> </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td>Mentre <code>/conf/global/settings/dam/workflownotification/email/downloadasset</code> è tecnicamente supportato per la ricerca (ha la precedenza prima di /apps tramite la ricerca CAConfig Sling usuale, ma dopo <code>/etc</code>) il modello potrebbe essere posizionato in <code>/conf/global/settings/dam/workflownotification/email/downloadasset</code>. Tuttavia, questo non è consigliato in quanto non esiste alcuna interfaccia utente di runtime per facilitare la modifica del modello e-mail.</td>
  </tr>
 </tbody>
</table>

### Licenze DRM di esempio {#example-drm-licenses}

| **Posizione precedente** | `/etc/dam/drm/licenses/` |
|---|---|
| **Nuove posizioni** | `/libs/settings/dam/drm` |
| **Orientamenti per la ristrutturazione** | N/D |
| **Note** | N/D |

### Modello notifica e-mail condivisione collegamenti {#link-share-e-mail-notification-template}

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
   <td><p>Se il modello e-mail è stato modificato dal cliente, per allinearlo con la nuova struttura del repository:</p>
    <ol>
     <li>Il modello di posta elettronica aggiornato deve essere copiato da <strong><code>/etc/dam/adhocassetshare</code></strong> a <strong><code>/apps/settings/dam/adhocassetshare</code></strong>
      <ol>
       <li>Poiché la destinazione è in <strong> <code>/apps</code></strong> questa modifica deve essere persistente in SCM.</li>
      </ol> </li>
     <li>Rimuovete la cartella: <strong><code>/etc/dam/adhocassetshare</code></strong> dopo lo spostamento dei modelli di posta elettronica all'interno.<br />
      <ol>
       <li>Se non sono stati apportati aggiornamenti al modello e-mail in <strong> <code>/etc</code></strong>, è possibile rimuovere la cartella perché il modello e-mail originale esiste in <strong><code>/libs/settings/dam/adhocassetshare</code></strong> come parte dell'installazione AEM 6.4.</li>
      </ol> </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td>Sebbene <code>/conf/global/settings/dam/adhocassetshare</code> sia tecnicamente supportato per la ricerca (ha la precedenza prima di <code>/apps</code> tramite la tipica ricerca CAConfig Sling, ma dopo <code>/etc</code>), il modello può essere posizionato in <code>/conf/global/settings/dam/adhocassetshare</code>. Tuttavia, non è consigliabile in quanto non esiste alcuna interfaccia utente di runtime per facilitare la modifica del modello e-mail</td>
  </tr>
 </tbody>
</table>

###  script di flusso di lavoro InDesign {#indesign-workflow-scripts}

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
   <td><p>Per allineare con la nuova struttura del repository:</p>
    <ol>
     <li>Copiare tutti gli script personalizzati o modificati da <strong><code>/etc/dam/indesign/scripts</code></strong> a <strong><code>/apps/settings/dam/indesign/scripts</code></strong><br />
      <ol>
       <li>È possibile copiare solo script nuovi o modificati come script non modificati forniti da AEM tramite <strong><code>/libs/settings</code></strong> in AEM 6.5</li>
      </ol> </li>
     <li>Individua tutti i modelli di workflow che utilizzano il passaggio WF del processo di estrazione file multimediali e
      <ol>
       <li>Per ogni istanza del Passaggio flusso di lavoro, aggiornare i percorsi nella configurazione in modo che puntino esplicitamente agli script appropriati in <strong> <code>/apps/settings/dam/indesign/scripts</code></strong> o <strong><code>/libs/settings/dam/indesign/scripts</code></strong>, a seconda dei casi.</li>
      </ol> </li>
     <li>Rimuovere <strong> <code>/etc/dam/indesign/scripts</code></strong> completamente.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td>Si consiglia di memorizzare gli script personalizzati in <code>/apps</code>, in quanto si tratta della posizione in cui memorizzare il codice.</td>
  </tr>
 </tbody>
</table>

### Configurazioni di transcodifica video {#video-transcoding-configurations}

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
   <td><p>Le personalizzazioni a livello di progetto devono essere tagliate e incollate in percorsi <code>/apps</code> o <code>/conf</code> equivalenti, a seconda dei casi.</p> <p>Per allineare con la struttura del repository di AEM 6.4:</p>
    <ol>
     <li>Copiare le configurazioni video modificate da <code>/etc/dam/video</code> a <code>/apps/settings/dam/video</code></li>
     <li>Rimuovi <code>/etc/dam/video</code></li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td>N/D</td>
  </tr>
 </tbody>
</table>

### Configurazioni dei predefiniti per visualizzatori {#viewer-preset-configurations}

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
   <td><p>Per il predefinito per visualizzatori preimpostato, sarà disponibile solo nella nuova posizione.</p> <p>Per il predefinito per visualizzatori personalizzati:</p>
    <ul>
     <li>sarà necessario eseguire uno script di migrazione per spostare il nodo da <code>/etc</code> a <code>/conf</code>. Lo script si trova in <em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></li>
     <li>oppure potete modificare la configurazione e salvarle automaticamente nella nuova posizione.</li>
    </ul> <p>Non è necessario regolare il codice copyURL/embed per puntare a <code>/conf</code>. La richiesta esistente a <code>/etc</code> verrà reinstradata al contenuto corretto da <code>/conf</code>.</p> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td>N/D</td>
  </tr>
 </tbody>
</table>

### Misc {#misc2}

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
   <td><p>Regolate i riferimenti per puntare alle nuove risorse in <code>/libs</code> utilizzando il prefisso proxy <code>/etc.clientlibs/</code> consenti.</p> <p>Infine, eliminate le cartelle per i clientlibs migrati da <code>/etc/clientlibs/foundation/</code></p> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td>N/D<br /> </td>
  </tr>
 </tbody>
</table>

