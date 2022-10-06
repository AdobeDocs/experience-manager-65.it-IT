---
title: Ristrutturazione dell’archivio risorse in AEM 6.5
seo-title: Assets Repository Restructuring in AEM 6.5
description: Scopri come apportare le modifiche necessarie per migrare alla nuova struttura dell’archivio in AEM 6.5 per Assets.
seo-description: Learn how to make the necessary changes in order to migrate to the new repository structure in AEM 6.5 for Assets.
uuid: 0e3d8163-6274-4d1b-91c7-32ca927fb83c
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
discoiquuid: 212930fc-3430-4a0a-842c-2fb613ef981f
feature: Upgrading
exl-id: 28ddd23c-5907-4356-af56-ebc7589a2b5d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1035'
ht-degree: 2%

---

# Ristrutturazione dell’archivio risorse in AEM 6.5 {#assets-repository-restructuring-in-aem}

Come descritto nell&#39;elemento padre [Ristrutturazione dell’archivio in AEM 6.5](/help/sites-deploying/repository-restructuring.md) I clienti che eseguono l’aggiornamento a AEM 6.5 devono utilizzare questa pagina per valutare lo sforzo di lavoro associato alle modifiche dell’archivio che influiscono sulla soluzione AEM Assets. Alcune modifiche richiedono un lavoro durante il processo di aggiornamento di AEM 6.5, mentre altre possono essere differite fino a un aggiornamento futuro.

**Con aggiornamento alla versione 6.5**

* [Varie](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#misc)

**Prima dell’aggiornamento futuro**

* [Modello di notifica e-mail evento Asset/Collection](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#asset-collection-event-e-mail-notification-template)
* [Progettazioni di condivisione risorse classiche](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#classic-asset-share-designs)
* [Scarica il modello di notifica per e-mail delle risorse](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#download-asset-e-mail-notification-template)
* [Esempio di licenze DRM](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#example-drm-licenses)
* [Modello di notifica della condivisione dei collegamenti e-mail](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#link-share-e-mail-notification-template)
* [Script del flusso di lavoro di InDesign](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#indesign-workflow-scripts)
* [Configurazioni di transcodifica video](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#video-transcoding-configurations)
* [Varie](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#misc2)

## Con aggiornamento alla versione 6.5 {#with-upgrade}

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
   <td><strong>Orientamento alla ristrutturazione</strong></td>
   <td><p>Se un codice personalizzato dipende da questa posizione (ad es. il codice si basa esplicitamente su questo percorso) quindi il codice deve essere aggiornato per utilizzare la nuova posizione prima dell'aggiornamento; Idealmente le API Java sono utilizzate quando disponibili per ridurre le dipendenze su qualsiasi percorso specifico nel JCR.</p> <p>Posizione temporanea per il blocco del file zip per il client da scaricare. Non è necessario eseguire l’aggiornamento da quando il client richiede di scaricare la risorsa. Verrà generato un file nella nuova posizione.</p> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td>N/D</td>
  </tr>
 </tbody>
</table>

## Prima dell’aggiornamento futuro {#prior-to-upgrade}

### Modello di notifica e-mail evento Asset/Collection {#asset-collection-event-e-mail-notification-template}

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
   <td><strong>Orientamento alla ristrutturazione</strong></td>
   <td><p>Se i modelli di posta elettronica sono stati modificati dal cliente, eseguire le azioni seguenti per allinearsi alla nuova struttura del repository:</p>
    <ol>
     <li>La <code>/libs/settings/dam/notification</code> il modello di posta elettronica deve essere copiato da <strong><code>/etc/notification/email/default</code></strong> a <strong><code>/apps/settings/notification/email/default</code></strong>
      <ol>
       <li>Perché la destinazione è in<strong> <code>/apps</code></strong> questa modifica deve essere mantenuta in SCM.</li>
      </ol> </li>
     <li>Rimuovi la cartella: <strong><code>/etc/dam/notification/email/default</code></strong> dopo lo spostamento dei modelli di posta elettronica al suo interno.<br />
      <ol>
       <li>Se non sono stati apportati aggiornamenti al modello di posta elettronica in<strong> <code>/etc/notification/email/default</code></strong>, la cartella può essere rimossa poiché il modello di posta elettronica originale esiste in <strong><code>/libs/settings/notification/email/default</code></strong> come parte dell'installazione AEM 4.</li>
      </ol> </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td>N/D<br /> </td>
  </tr>
 </tbody>
</table>

### Progettazioni di condivisione risorse classiche {#classic-asset-share-designs}

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
   <td><strong>Orientamento alla ristrutturazione</strong></td>
   <td><p>Per tutte le progettazioni gestite in SCM e non scritte in fase di esecuzione tramite le finestre di dialogo di progettazione, eseguire le azioni seguenti per allinearsi al modello più recente:</p>
    <ol>
     <li>Copia le progettazioni dalla posizione precedente alla nuova posizione in <code>/apps</code>.</li>
     <li>Convertire CSS, JavaScript e risorse statiche nella progettazione in un <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">Libreria client</a> con <code>allowProxy = true</code>.</li>
     <li>Aggiorna i riferimenti alla posizione precedente nel <code>cq:designPath</code> proprietà tramite <strong>AEM &gt; Amministratore DAM &gt; Pagina Condivisione risorse &gt; Proprietà pagina &gt; Scheda Avanzate &gt; Campo struttura</strong>.</li>
     <li>Aggiorna le pagine che fanno riferimento alla posizione precedente per utilizzare la nuova categoria Libreria client . È necessario aggiornare il codice di implementazione della pagina.</li>
     <li>Aggiorna le regole del Dispatcher per consentire il servizio delle librerie client tramite il <code>/etc.clientlibs/</code> servlet proxy.</li>
    </ol> <p>Per tutte le progettazioni non gestite in SCM e modificate in fase di esecuzione tramite le finestre di dialogo di progettazione, non spostare le progettazioni modificabili da <code>/etc</code>.</p> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td>N/D<br /> </td>
  </tr>
 </tbody>
</table>

### Scarica il modello di notifica per e-mail delle risorse {#download-asset-e-mail-notification-template}

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
   <td><strong>Orientamento alla ristrutturazione</strong></td>
   <td><p>Se i modelli di posta elettronica (<strong>downloadasset</strong> o <strong>transientworkflow completato</strong>) sono state modificate, quindi segui la procedura seguente per allinearla alla nuova struttura:</p>
    <ol>
     <li>Il modello di posta elettronica aggiornato deve essere copiato da <strong><code>/etc/dam/workflow/notification/email/downloadasset</code></strong> a <strong><code>/apps/settings/dam/workflow/notification/email/downloadasset</code></strong>
      <ol>
       <li>Perché la destinazione è in<strong> <code>/apps</code></strong> questa modifica deve essere mantenuta in SCM.</li>
      </ol> </li>
     <li>Rimuovi la cartella: <code>/etc/dam/workflow/notification/email/downloadasset </code>dopo lo spostamento dei modelli di posta elettronica al suo interno.<br />
      <ol>
       <li>Se non sono stati apportati aggiornamenti al modello di posta elettronica in<strong> <code>/etc</code></strong>, la cartella può essere rimossa poiché il modello di posta elettronica originale esiste in <strong><code>/libs/settings/dam/workflownotification/email/downloadasset</code></strong> come parte dell'installazione di AEM 6.4.</li>
      </ol> </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td>Quando <code>/conf/global/settings/dam/workflownotification/email/downloadasset</code> è tecnicamente supportato per la ricerca (ha la precedenza prima di /apps tramite la tipica ricerca Sling CAConfig, ma dopo <code>/etc</code>) il modello può essere inserito in <code>/conf/global/settings/dam/workflownotification/email/downloadasset</code>. Tuttavia, questo non è consigliato in quanto non esiste alcuna interfaccia utente di runtime per facilitare la modifica del modello di posta elettronica.</td>
  </tr>
 </tbody>
</table>

### Esempio di licenze DRM {#example-drm-licenses}

| **Posizione precedente** | `/etc/dam/drm/licenses/` |
|---|---|
| **Nuove posizioni** | `/libs/settings/dam/drm` |
| **Orientamento alla ristrutturazione** | N/D |
| **Note** | N/D |

### Modello di notifica della condivisione dei collegamenti e-mail {#link-share-e-mail-notification-template}

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
   <td><strong>Orientamento alla ristrutturazione</strong></td>
   <td><p>Se il modello e-mail è stato modificato dal cliente, per allinearlo alla nuova struttura del repository:</p>
    <ol>
     <li>Il modello di posta elettronica aggiornato deve essere copiato da <strong><code>/etc/dam/adhocassetshare</code></strong> a <strong><code>/apps/settings/dam/adhocassetshare</code></strong>
      <ol>
       <li>Perché la destinazione è in<strong> <code>/apps</code></strong> questa modifica deve essere mantenuta in SCM.</li>
      </ol> </li>
     <li>Rimuovi la cartella: <strong><code>/etc/dam/adhocassetshare</code></strong> dopo lo spostamento dei modelli di posta elettronica al suo interno.<br />
      <ol>
       <li>Se non sono stati apportati aggiornamenti al modello di posta elettronica in<strong> <code>/etc</code></strong>, la cartella può essere rimossa poiché il modello di posta elettronica originale esiste in <strong><code>/libs/settings/dam/adhocassetshare</code></strong> come parte dell'installazione di AEM 6.4.</li>
      </ol> </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td>Quando <code>/conf/global/settings/dam/adhocassetshare</code> è tecnicamente supportato per la ricerca (ha la precedenza prima di <code>/apps</code> tramite la ricerca CAConfig solita, ma dopo <code>/etc</code>), il modello può essere inserito in <code>/conf/global/settings/dam/adhocassetshare</code>. Tuttavia, questo non è consigliato in quanto non esiste alcuna interfaccia utente di runtime per facilitare la modifica del modello di posta elettronica</td>
  </tr>
 </tbody>
</table>

### Script del flusso di lavoro di InDesign {#indesign-workflow-scripts}

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
   <td><strong>Orientamento alla ristrutturazione</strong></td>
   <td><p>Per allinearsi alla nuova struttura del repository:</p>
    <ol>
     <li>Copia tutti gli script personalizzati o modificati da <strong><code>/etc/dam/indesign/scripts</code></strong> a <strong><code>/apps/settings/dam/indesign/scripts</code></strong><br />
      <ol>
       <li>Solo gli script nuovi o modificati come script non modificati forniti da AEM saranno disponibili tramite <strong><code>/libs/settings</code></strong> nella AEM 6.5</li>
      </ol> </li>
     <li>Individua tutti i modelli di flusso di lavoro che utilizzano il passaggio WF del processo di estrazione dei file multimediali e
      <ol>
       <li>Per ogni istanza del passaggio del flusso di lavoro, aggiorna i percorsi nella configurazione in modo che puntino esplicitamente agli script appropriati in<strong> <code>/apps/settings/dam/indesign/scripts</code></strong> o <strong><code>/libs/settings/dam/indesign/scripts</code></strong> se del caso.</li>
      </ol> </li>
     <li>Rimuovi<strong> <code>/etc/dam/indesign/scripts</code></strong> interamente.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td>È consigliabile memorizzare gli script personalizzati in <code>/apps</code>, poiché si tratta del percorso in cui deve essere memorizzato il codice.</td>
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
   <td><strong>Orientamento alla ristrutturazione</strong></td>
   <td><p>Le personalizzazioni a livello di progetto devono essere tagliate e incollate sotto un livello equivalente <code>/apps</code> o <code>/conf</code> percorsi, a seconda dei casi.</p> <p>Per allinearsi alla struttura dell'archivio AEM 6.4:</p>
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
   <td><strong>Orientamento alla ristrutturazione</strong></td>
   <td><p>Per il predefinito visualizzatore, sarà disponibile solo nella nuova posizione.</p> <p>Per il predefinito visualizzatore personalizzato:</p>
    <ul>
     <li>dovrai eseguire uno script di migrazione per spostare il nodo da <code>/etc</code> a <code>/conf</code>. Lo script si trova in <em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></li>
     <li>oppure puoi modificare la configurazione e salvarla automaticamente nella nuova posizione.</li>
    </ul> <p>Non è necessario regolare il codice copyURL/embed per puntare a <code>/conf</code>. La richiesta esistente a <code>/etc</code> verrà reindirizzato al contenuto corretto da <code>/conf</code>.</p> </td>
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
   <td><strong>Orientamento alla ristrutturazione</strong></td>
   <td><p>Adeguare eventuali riferimenti alle nuove risorse in <code>/libs</code> utilizzando <code>/etc.clientlibs/</code> consenti prefisso proxy.</p> <p>Infine, ripulisci rimuovendo le cartelle per i clientlibs migrati da <code>/etc/clientlibs/foundation/</code></p> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td>N/D<br /> </td>
  </tr>
 </tbody>
</table>
