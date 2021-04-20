---
title: Ristrutturazione dell’archivio siti in AEM 6.5
seo-title: Ristrutturazione dell’archivio siti in AEM 6.5
description: Scopri come apportare le modifiche necessarie per migrare alla nuova struttura dell’archivio in AEM 6.5 per Sites.
seo-description: Scopri come apportare le modifiche necessarie per migrare alla nuova struttura dell’archivio in AEM 6.5 per Sites.
uuid: 6dc5f8bd-1680-40af-9b8f-26c1f4bc3304
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
discoiquuid: 3eccb2d5-c325-43a6-9c03-5f93f7e30712
feature: Upgrading
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1601'
ht-degree: 1%

---


# Ristrutturazione dell’archivio siti in AEM 6.5 {#sites-repository-restructuring-in-aem}

Come descritto nella pagina padre [Ristrutturazione archivio AEM 6.5](/help/sites-deploying/repository-restructuring.md) , i clienti che eseguono l’aggiornamento a AEM 6.5 devono utilizzare questa pagina per valutare lo sforzo di lavoro associato alle modifiche dell’archivio che influiscono sulla soluzione AEM Sites. Alcune modifiche richiedono un lavoro durante il processo di aggiornamento di AEM 6.5, mentre altre possono essere differite fino a un aggiornamento futuro.

**Con aggiornamento alla versione 6.5**

* [Segmenti ContextHub](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#contexthub-segments)

**Prima dell’aggiornamento futuro**

* [Librerie client di Adobe Analytics](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#adobe-analytics-client-libraries)
* [Progettazioni classiche di pagine da Microsoft Word a Web](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#classic-microsoft-word-to-web-page-designs)
* [Configurazioni dell&#39;emulatore del dispositivo mobile](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#mobile-device-emulator-configurations)
* [Configurazioni blueprint di Multi-Site Manager](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#multi-site-manager-blueprint-configurations)
* [Configurazioni di rollout di Multi-Site Manager](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#multi-site-manager-rollout-configurations)
* [Modello e-mail di notifica evento pagina](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#page-event-notification-e-mail-template)
* [Scaffolding delle pagine](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#page-scaffolding)
* [Griglia reattiva inferiore](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#responsive-grid-less)
* [Modelli statici](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#static-template-designs)
* [Librerie client di integrazione di Adobe Search e Promote](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#adobe-search-and-promote-integration-client-libraries)
* [Librerie client di integrazione di Adobe Target](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#adobe-target-integration-client-libraries)
* [Librerie client di WCM Foundation](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#wcm-foundation-client-libraries)

## Aggiornamento 6.5 {#with-upgrade}

### Segmenti ContextHub {#contexthub-segments}

<table>
 <tbody>
  <tr>
   <td><strong>Posizione precedente</strong></td>
   <td><code>/etc/segmentation/contexthub</code></td>
  </tr>
  <tr>
   <td><strong>Nuove posizioni</strong></td>
   <td><p><code>/apps/settings/wcm/segments</code> </p> <p><code>/conf/settings/settings/wcm/segments</code> </p> <p><code>/conf/&lt;tenant&gt;/settings/wcm/segments</code></p> </td>
  </tr>
  <tr>
   <td><strong>Orientamento alla ristrutturazione</strong></td>
   <td><p>Se i segmenti ContextHub nuovi o modificati devono essere modificati nel controllo del codice sorgente anziché essere modificati in AEM, è necessario migrarli nella nuova posizione:</p>
    <ol>
     <li>Copia i segmenti ContextHub nuovi o modificati dalla posizione precedente alla nuova posizione appropriata (/<code>apps</code>, <code>/conf/global</code> o <code>/conf/&lt;tenant&gt;</code>)</li>
     <li>Aggiorna i riferimenti ai segmenti ContextHub nella posizione precedente ai segmenti ContextHub migrati nelle nuove posizioni (<code>/apps</code>, <code>/conf/global</code>, <code>/conf/&lt;tenant&gt;</code>).</li>
    </ol> <p>La seguente query QueryBuilder individua tutti i riferimenti ai segmenti ContextHub nelle posizioni precedenti.<br /> <br /> <code class="code">path=/content
       property=cq:segments
       property.operation=like
       property.value=/etc/segmentation/contexthub/%</code><br /> <br /> Questa operazione può essere eseguita tramite  <a href="/help/sites-developing/querybuilder-api.md" target="_blank">AEM’interfaccia utente</a> di Debugger di QueryBuilder. Tieni presente che si tratta di una query di attraversamento, quindi non eseguirla rispetto alla produzione e assicurati che i limiti di attraversamento vengano regolati in base alle esigenze.</p> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td><p>I segmenti ContextHub persistono nella posizione precedente vengono visualizzati come di sola lettura in <strong>AEM &gt; Personalizzazione &gt; Audiences</strong>.</p> <p>Se i segmenti ContextHub devono essere modificabili in AEM, è necessario eseguire la migrazione nella nuova posizione (<code>/conf/global</code> o <code>/conf/&lt;tenant&gt;</code>). Eventuali nuovi segmenti di ContentHub creati in AEM vengono mantenuti nella nuova posizione (<code>/conf/global</code> o <code>/conf/&lt;tenant&gt;</code>).</p> <p>Le Proprietà pagina di AEM Sites consentono solo di selezionare la posizione precedente (<code>/etc</code>) o una singola nuova posizione (<code>/apps</code>, <code>/conf/global</code> o <code>/conf/&lt;tenant&gt;</code>), pertanto i segmenti ContextHub devono essere migrati di conseguenza.</p> <p>Eventuali segmenti ContextHub non utilizzati dai siti di riferimento AEM possono essere rimossi e non migrati nella nuova posizione:</p>
    <ul>
     <li>/etc/segmentation/geometrixx/</li>
     <li>/etc/segmentation/geometrixx-outdoors</li>
    </ul> <p>Nota: Se il ClientContext è in uso, si consiglia di convertire in ContextHub.</p> </td>
  </tr>
 </tbody>
</table>

## Aggiornamento precedente a {#prior-to-upgrade}

### Librerie client Adobe Analytics {#adobe-analytics-client-libraries}

<table>
 <tbody>
  <tr>
   <td><strong>Posizione precedente</strong></td>
   <td><p><code>/etc/clientlibs/foundation/sitecatalyst</code></p> </td>
  </tr>
  <tr>
   <td><strong>Nuove posizioni</strong></td>
   <td><code>/libs/cq/analytics/clientlibs/analytics</code></td>
  </tr>
  <tr>
   <td><strong>Orientamento alla ristrutturazione</strong></td>
   <td><p>Qualsiasi utilizzo personalizzato di queste librerie client deve fare riferimento alla libreria client per categoria e non per percorso:</p>
    <ol>
     <li>Eventuali riferimenti alla libreria client in base al percorso nella posizione precedente devono essere aggiornati per utilizzare <a href="/help/sites-developing/clientlibs.md#referencing-client-side-libraries" target="_blank">AEM framework di riferimento della libreria client</a>.</li>
     <li>Se AEM framework di riferimento della libreria client non può essere utilizzato, è possibile fare riferimento al percorso assoluto delle librerie client tramite AEM servlet proxy libreria client.
      <ul>
       <li><code>/etc.clientlibs/cq/analytics/clientlibs/sitecatalyst/appmeasurement.js</code></li>
       <li><code>/etc.clientlibs/cq/analytics/clientlibs/sitecatalyst/plugins.js</code></li>
       <li><code>/etc.clientlibs/cq/analytics/clientlibs/sitecatalyst/sitecatalyst.js</code></li>
       <li><code>/etc.clientlibs/cq/analytics/clientlibs/sitecatalyst/tracking.js</code></li>
       <li><code>/etc.clientlibs/cq/analytics/clientlibs/sitecatalyst/util.js</code></li>
      </ul> </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td><p>La modifica di queste librerie client non è mai stata supportata.</p> <p>Per ottenere le categorie della Libreria client, visita ogni nodo <code>cq:ClientLIbraryFolder</code> tramite CRXDELite ed esamina la proprietà categories.</p>
    <ul>
     <li><code>/libs/cq/analytics/clientlibs/sitecatalyst/appmeasurement</code></li>
     <li><code>/libs/cq/analytics/clientlibs/sitecatalyst/plugins</code></li>
     <li><code>/libs/cq/analytics/clientlibs/sitecatalyst/sitecatalyst</code></li>
     <li><code>/libs/cq/analytics/clientlibs/sitecatalyst/tracking</code></li>
     <li><code>/libs/cq/analytics/clientlibs/sitecatalyst/util</code></li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### Progettazione classica di pagine Web da Microsoft Word {#classic-microsoft-word-to-web-page-designs}

<table>
 <tbody>
  <tr>
   <td><strong>Posizione precedente</strong></td>
   <td><code>/etc/designs/wordDesign</code></td>
  </tr>
  <tr>
   <td><strong>Nuove posizioni</strong></td>
   <td><p><code>/libs/settings/wcm/designs/wordDesign</code></p> <p><code>/apps/settings/wcm/designs/wordDesign</code></p> </td>
  </tr>
  <tr>
   <td><strong>Orientamento alla ristrutturazione</strong></td>
   <td><p>Per tutte le progettazioni gestite in SCM e non scritte in fase di esecuzione tramite le finestre di dialogo di progettazione.</p>
    <ol>
     <li>Copia le progettazioni dalla posizione precedente alla nuova posizione (<code>/apps</code>).</li>
     <li>Converti qualsiasi risorsa CSS, JavaScript e statica nella progettazione in una <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">libreria client</a> con <code>allowProxy = true</code>.</li>
     <li>Aggiorna i riferimenti alla posizione precedente nella proprietà cq:designPath .</li>
     <li>Aggiorna le pagine che fanno riferimento alla posizione precedente per utilizzare la nuova categoria Libreria client (è necessario aggiornare il codice di implementazione della pagina).</li>
     <li>Aggiorna AEM regole del Dispatcher per consentire il servizio delle librerie client tramite il servlet proxy <code>/etc.clientlibs/</code> .</li>
    </ol> <p>Per tutte le progettazioni NON gestite in SCM e modificate in fase di esecuzione tramite le finestre di dialogo di progettazione:</p>
    <ul>
     <li>Non spostare progettazioni modificabili dall’autore fuori da <code>/etc</code>.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td>N/D<br /> </td>
  </tr>
 </tbody>
</table>

### Configurazioni dell&#39;emulatore di dispositivi mobili {#mobile-device-emulator-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>Posizione precedente</strong></td>
   <td><p><code>/etc/mobile</code></p> </td>
  </tr>
  <tr>
   <td><strong>Nuove posizioni</strong></td>
   <td><p><code>/libs/settings/mobile</code></p> <p><code>/apps/settings/mobile</code></p> <p><code>/conf/global/settings/mobile</code></p> <p><code>/conf/&lt;tenant&gt;/settings/mobile</code></p> </td>
  </tr>
  <tr>
   <td><strong>Orientamento alla ristrutturazione</strong></td>
   <td>Eventuali nuove configurazioni di emulatore di dispositivi mobili devono essere migrate nella nuova posizione.
    <ol>
     <li>Copia le nuove configurazioni dell’emulatore di dispositivi mobili dalla posizione precedente alla nuova posizione (<code>/apps</code>, <code>/conf/global</code>, <code>/conf/&lt;tenant&gt;</code>).</li>
     <li>Per qualsiasi pagina AEM Sites dipendente da queste configurazioni dell’emulatore di dispositivi mobili, aggiorna la pagina <span class="code">
       <code>
        jcr
       </code>
       Nodo <code>
        :content
       </code></span>: <br /> <span class="code">[cq:Page]/jcr:content@cq:
       <code>
        deviceGroups
       </code> = String[ mobile/groups/responsive ]</span></li>
     <li>Per tutti i modelli modificabili che dipendono da queste configurazioni dell'emulatore di dispositivi mobili, aggiorna i modelli modificabili, indicando il valore <span class="code">
       <code>
        cq
       </code>:
       <code>
        deviceGroups
       </code></span> nella nuova posizione.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td><p>La risoluzione delle configurazioni dell'emulatore del dispositivo mobile si verifica nel seguente ordine:</p>
    <ol>
     <li><code>/conf/&lt;tenant&gt;/settings/mobile</code></li>
     <li><code>/conf/global/settings/mobile</code></li>
     <li><code>/apps/settings/mobile</code></li>
     <li><code>/libs/settings/mobile</code></li>
     <li><code>/etc/mobile</code></li>
    </ol> </td>
  </tr>
 </tbody>
</table>

### Configurazioni blueprint di Multi-Site Manager {#multi-site-manager-blueprint-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>Posizione precedente</strong></td>
   <td><code>/etc/blueprints</code></td>
  </tr>
  <tr>
   <td><strong>Nuove posizioni</strong></td>
   <td><p><code>/apps/msm</code> (Configurazioni Blueprint cliente)</p> <p><code>/libs/msm</code> (Configurazioni di Blueprint pronte per Screens, Commerce)</p> </td>
  </tr>
  <tr>
   <td><strong>Orientamento alla ristrutturazione</strong></td>
   <td><p>Eventuali configurazioni di blueprint Manager nuove o modificate devono essere migrate nella nuova posizione (<code>/apps</code>).</p>
    <ol>
     <li>Copia le configurazioni di Blueprint Manager nuove o modificate da Posizione precedente a Nuova posizione (<code>/apps</code>).</li>
     <li>Rimuovi eventuali configurazioni di blueprint Multi-Site Manager migrate dalla posizione precedente.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td><p>Tutte le configurazioni di blueprint Multi-Site Manager fornite AEM esistono nella nuova posizione in <code>/libs</code>.</p> <p>Il contenuto non fa riferimento alle configurazioni blu di Multi-Site Manager, pertanto non sono presenti riferimenti di contenuto da regolare.</p> </td>
  </tr>
 </tbody>
</table>

### Configurazioni di rollout di Multi-Site Manager {#multi-site-manager-rollout-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>Posizione precedente</strong></td>
   <td><p><code>/etc/msm/rolloutConfigs</code></p> </td>
  </tr>
  <tr>
   <td><strong>Nuove posizioni</strong></td>
   <td><p><code>/libs/msm/wcm/rolloutconfigs</code></p> <p><code>/apps/msm/wcm/rolloutconfigs</code></p> </td>
  </tr>
  <tr>
   <td><strong>Orientamento alla ristrutturazione</strong></td>
   <td><p>Tutte le configurazioni di rollout di Multi-Site Manager nuove o modificate devono essere migrate nella nuova posizione.</p>
    <ol>
     <li>Copia le configurazioni di rollout di Multi-Site Manager nuove o modificate dalla posizione precedente alla nuova posizione (<code>/apps</code>).</li>
     <li>Aggiorna i riferimenti nelle pagine AEM alle configurazioni di rollout di Multi-site Manager nella posizione precedente, in modo che i relativi riferimenti nelle nuove posizioni (<code>/libs</code> o <code>/apps</code>).</li>
    </ol> <p>Rimuovi le configurazioni di rollout di Multi-Site Manager migrate dalla posizione precedente.</p> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td>La mancata rimozione delle configurazioni di rollout di Multi-Site Manager migrate dalla posizione precedente determina la visualizzazione di opzioni di rollout duplicate agli autori AEM.</td>
  </tr>
 </tbody>
</table>

### Modello e-mail per notifica eventi pagina {#page-event-notification-e-mail-template}

<table>
 <tbody>
  <tr>
   <td><strong>Posizione precedente</strong></td>
   <td><p><code>/etc/notification/email/default/com.day.cq.wcm.core.page</code></p> </td>
  </tr>
  <tr>
   <td><strong>Nuove posizioni</strong></td>
   <td><p><code>/libs/settings/notification-templates/com.day.cq.wcm.core.page</code></p> <p><code>/apps/settings/notification-templates/com.day.cq.wcm.core.page</code></p> </td>
  </tr>
  <tr>
   <td><strong>Orientamento alla ristrutturazione</strong></td>
   <td><p>I nuovi modelli e-mail di notifica degli eventi di pagina supportati solo supportano le nuove impostazioni internazionali.</p> <p>La risoluzione del modello di posta elettronica dell’evento pagina si verifica nell’ordine seguente:</p>
    <ol>
     <li><code>/etc/notification/email/default/com.day.cq.wcm.core.page</code></li>
     <li><code>/apps/settings/notification-templates/com.day.cq.wcm.core.page</code></li>
     <li><code>/libs/settings/notification-templates/com.day.cq.wcm.core.page</code></li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td><p>Eventuali modelli e-mail di notifica degli eventi di pagina nuovi o modificati devono essere migrati nella nuova posizione in <code>/apps</code>:</p>
    <ol>
     <li>Copia i modelli e-mail di notifica degli eventi di pagina nuovi o modificati dalla posizione precedente alla nuova posizione (<code>/apps</code>).</li>
     <li>Rimuovi i modelli di posta elettronica per le notifiche degli eventi di pagina migrati dal percorso precedente.</li>
    </ol> </td>
  </tr>
 </tbody>
</table>

### Scaffolding pagina {#page-scaffolding}

<table>
 <tbody>
  <tr>
   <td><strong>Posizione precedente</strong></td>
   <td><code>/etc/scaffolding</code></td>
  </tr>
  <tr>
   <td><strong>Nuove posizioni</strong></td>
   <td><p><span class="code">/libs/settings/
      <code>
       wcm
      </code>/template-types/scaffolding/scaffolding</span></p> <p><span class="code">/apps/settings/
      <code>
       wcm
      </code>/template-types/scaffolding/scaffolding</span></p> </td>
  </tr>
  <tr>
   <td><strong>Orientamento alla ristrutturazione</strong></td>
   <td>Lo scaffolding creato nella posizione precedente utilizza il framework Scaffolding legacy e non può essere migrato nella nuova posizione. Per allinearsi alla nuova posizione, qualsiasi Scaffolding legacy deve essere risviluppato utilizzando il framework Scaffolding supportato.</td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td>N/D<br /> </td>
  </tr>
 </tbody>
</table>

### Griglia reattiva MENO {#responsive-grid-less}

<table>
 <tbody>
  <tr>
   <td><strong>Posizione precedente</strong></td>
   <td><code>/etc/clientlibs/wcm/foundation/grid/grid_base.less</code></td>
  </tr>
  <tr>
   <td><strong>Nuove posizioni</strong></td>
   <td><code>/libs/wcm/foundation/clientlibs/grid/grid_base.less</code></td>
  </tr>
  <tr>
   <td><strong>Orientamento alla ristrutturazione</strong></td>
   <td><p>Eventuali riferimenti alla posizione precedente nei file LESS personalizzati devono essere aggiornati per importare dalla nuova posizione.</p>
    <ul>
     <li>Aggiornare i file LESS personalizzati che fanno riferimento a grid_base.less nella posizione precedente per fare riferimento alla nuova posizione.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td>Se si fa riferimento a un file <code>grid_base.less</code> non esistente, la modalità Layout dell’Editor pagina e modelli non funziona e si verifica un’interruzione del layout di pagina.</td>
  </tr>
 </tbody>
</table>

### Modelli statici {#static-template-designs}

<table>
 <tbody>
  <tr>
   <td><strong>Posizione precedente</strong></td>
   <td><code>/etc/designs/&lt;custom-site&gt;</code></td>
  </tr>
  <tr>
   <td><strong>Nuove posizioni</strong></td>
   <td><code>/apps/settings/wcm/designs/&lt;custom-site&gt;</code></td>
  </tr>
  <tr>
   <td><strong>Orientamento alla ristrutturazione</strong></td>
   <td><p>Per tutte le progettazioni gestite in SCM e non scritte in fase di esecuzione tramite le finestre di dialogo di progettazione.</p>
    <ol>
     <li>Copia le progettazioni dalla posizione precedente alla nuova posizione (<code>/apps</code>).</li>
     <li>Converti qualsiasi risorsa CSS, JavaScript e statica nella progettazione in una <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">libreria client</a> con <code>allowProxy = true</code>.</li>
     <li>Aggiorna i riferimenti alla posizione precedente nella proprietà <code>cq:designPath</code> tramite <strong>AEM &gt; Siti &gt; Pagine del sito personalizzate &gt; Proprietà pagina &gt; Scheda avanzata &gt; Campo di progettazione</strong>.</li>
     <li>Aggiorna le pagine che fanno riferimento alla posizione precedente per utilizzare la nuova categoria Libreria client (è necessario aggiornare il codice di implementazione della pagina).</li>
     <li>Aggiorna AEM regole del Dispatcher per consentire il servizio delle librerie client tramite il servlet proxy <code>/etc.clientlibs/</code> .</li>
    </ol> <p>Per tutte le progettazioni NON gestite in SCM e modificate in fase di esecuzione tramite le finestre di dialogo di progettazione:</p>
    <ul>
     <li>Non spostare progettazioni modificabili dall’autore fuori da <code>/etc</code>.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td>L’approccio consigliato consiste nella creazione di AEM Sites e pagine utilizzando modelli modificabili che utilizzano Contenuto struttura e criteri al posto dei progetti.</td>
  </tr>
 </tbody>
</table>

### Librerie client di integrazione di Adobe Search and Promote {#adobe-search-and-promote-integration-client-libraries}

<table>
 <tbody>
  <tr>
   <td><strong>Posizione precedente</strong></td>
   <td><p><code>/etc/clientlibs/foundation/searchpromote</code></p> </td>
  </tr>
  <tr>
   <td><strong>Nuove posizioni</strong></td>
   <td><code>/libs/cq/searchpromote/clientlibs/searchpromote</code></td>
  </tr>
  <tr>
   <td><strong>Orientamento alla ristrutturazione</strong></td>
   <td><p>Qualsiasi utilizzo personalizzato di queste librerie client deve fare riferimento alla libreria client per categoria e non per percorso.</p>
    <ol>
     <li>Eventuali riferimenti alla libreria client in base al percorso nella posizione precedente devono essere aggiornati per utilizzare <a href="/help/sites-developing/clientlibs.md#referencing-client-side-libraries" target="_blank">AEM framework di riferimento della libreria client</a>.</li>
     <li>Se AEM framework di riferimento della libreria client non può essere utilizzato, è possibile fare riferimento al percorso assoluto delle librerie client tramite AEM servlet proxy libreria client:</li>
    </ol>
    <ul>
     <li><code>/etc.clientlibs/cq/searchpromote/clientlibs/searchpromotei.js</code></li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td><p>La modifica di queste librerie client non è mai stata supportata.</p> <p>Per ottenere le categorie della Libreria client, visita ogni nodo cq:ClientLIbraryFolder tramite CRXDELite ed esamina la proprietà categories:</p>
    <ul>
     <li><code>/libs/cq/searchpromote/clientlibs/searchpromote</code></li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### Librerie client di integrazione Adobe Target {#adobe-target-integration-client-libraries}

<table>
 <tbody>
  <tr>
   <td><strong>Posizione precedente</strong></td>
   <td><p><code>/etc/clientlibs/foundation/target</code></p> </td>
  </tr>
  <tr>
   <td><strong>Nuove posizioni</strong></td>
   <td><code>/libs/cq/testandtarget/clientlibs/testandtarget</code></td>
  </tr>
  <tr>
   <td><strong>Orientamento alla ristrutturazione</strong></td>
   <td><p>Qualsiasi utilizzo personalizzato di queste librerie client deve fare riferimento alla libreria client per categoria e non per percorso.</p>
    <ol>
     <li>Eventuali riferimenti alla libreria client in base al percorso nella posizione precedente devono essere aggiornati per utilizzare <a href="/help/sites-developing/clientlibs.md#referencing-client-side-libraries" target="_blank">AEM framework di riferimento della libreria client</a>.</li>
     <li>Se AEM framework di riferimento della libreria client non può essere utilizzato, è possibile fare riferimento al percorso assoluto delle librerie client tramite AEM servlet proxy libreria client:</li>
    </ol>
    <ul>
     <li><code>/etc.clientlibs/cq/testandtarget/clientlibs/testandtarget/testandtarget.js</code></li>
     <li><code>/etc.clientlibs/cq/testandtarget/clientlibs/testandtarget/atjs.js</code></li>
     <li><code>/etc.clientlibs/cq/testandtarget/clientlibs/testandtarget/atjs-integration.js</code></li>
     <li><code>/etc.clientlibs/cq/testandtarget/clientlibs/testandtarget/init.js</code></li>
     <li><code>/etc.clientlibs/cq/testandtarget/clientlibs/testandtarget/mbox.js</code></li>
     <li><code>/etc.clientlibs/cq/testandtarget/clientlibs/testandtarget/parameters.js</code></li>
     <li><code>/etc.clientlibs/cq/testandtarget/clientlibs/testandtarget/util.js</code></li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td><p>La modifica di queste librerie client non è mai stata supportata.</p> <p>Per ottenere le categorie della Libreria client, visita ogni nodo cq:ClientLIbraryFolder tramite CRXDELite ed esamina la proprietà categories:</p>
    <ul>
     <li><code>/libs/cq/testandtarget/clientlibs/testandtarget/testandtarget</code></li>
     <li><code>/libs/cq/testandtarget/clientlibs/testandtarget/atjs</code></li>
     <li><code>/libs/cq/testandtarget/clientlibs/testandtarget/atjs-integration</code></li>
     <li><code>/libs/cq/testandtarget/clientlibs/testandtarget/init</code></li>
     <li><code>/libs/cq/testandtarget/clientlibs/testandtarget/mbox</code></li>
     <li><code>/libs/cq/testandtarget/clientlibs/testandtarget/parameters</code></li>
     <li><code>/libs/cq/testandtarget/clientlibs/testandtarget/util</code></li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### Librerie client di WCM Foundation {#wcm-foundation-client-libraries}

<table>
 <tbody>
  <tr>
   <td><strong>Posizione precedente</strong></td>
   <td><p><code>/etc/clientlibs/wcm/foundation</code></p> </td>
  </tr>
  <tr>
   <td><strong>Nuove posizioni</strong></td>
   <td><code>/libs/wcm/foundation/clientlibs</code></td>
  </tr>
  <tr>
   <td><strong>Orientamento alla ristrutturazione</strong></td>
   <td><p>Qualsiasi utilizzo personalizzato di queste librerie client deve fare riferimento alla libreria client per categoria e non per percorso.</p>
    <ol>
     <li>Eventuali riferimenti alla libreria client in base al percorso nella posizione precedente devono essere aggiornati per utilizzare <a href="/help/sites-developing/clientlibs.md#referencing-client-side-libraries" target="_blank">AEM framework di riferimento della libreria client</a>.</li>
     <li>Se AEM framework di riferimento della libreria client non può essere utilizzato, è possibile fare riferimento al percorso assoluto delle librerie client tramite AEM servlet proxy libreria client.</li>
    </ol>
    <ul>
     <li><code>/etc.clientlibs/wcm/foundation/clientlibs/accessibility.css</code></li>
     <li><code>/etc.clientlibs/wcm/foundation/clientlibs/main.css</code></li>
     <li><code>/etc.clientlibs/wcm/foundation/clientlibs/main.js</code></li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td><p>La modifica di queste librerie client non è mai stata supportata.</p> <p>Per ottenere le categorie della Libreria client, visita ogni nodo <code>cq:ClientLIbraryFolder</code> tramite CRXDELite ed esamina la proprietà categories:</p>
    <ul>
     <li><code>/libs/wcm/foundation/clientlibs/accessibility</code></li>
     <li><code>/libs/wcm/foundation/clientlibs/main</code></li>
    </ul> </td>
  </tr>
 </tbody>
</table>

