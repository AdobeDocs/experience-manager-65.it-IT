---
title: Ristrutturazione dell’archivio Sites in AEM 6.5
description: Scopri come apportare le modifiche necessarie per migrare alla nuova struttura dell’archivio in AEM 6.5 per Sites.
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
feature: Upgrading
exl-id: b4531792-06dd-4545-9dbb-57224be20dc7
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1464'
ht-degree: 1%

---

# Ristrutturazione dell’archivio Sites in AEM 6.5 {#sites-repository-restructuring-in-aem}

Come descritto sull’elemento padre [Ristrutturazione dell’archivio in AEM 6.5](/help/sites-deploying/repository-restructuring.md) pagina, i clienti che eseguono l’aggiornamento a AEM 6.5 devono utilizzare questa pagina per valutare l’impegno di lavoro associato alle modifiche dell’archivio che influiscono sulla soluzione AEM Sites. Alcune modifiche richiedono un impegno di lavoro durante il processo di aggiornamento AEM 6.5, mentre altre possono essere differite fino a un aggiornamento futuro.

**Con aggiornamento 6.5**

* [Segmenti ContextHub](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#contexthub-segments)

**Prima di un aggiornamento futuro**

* [Librerie client di Adobe Analytics](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#adobe-analytics-client-libraries)
* [Progettazioni classiche da Microsoft Word a pagine Web](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#classic-microsoft-word-to-web-page-designs)
* [Configurazioni emulatore dispositivo mobile](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#mobile-device-emulator-configurations)
* [Configurazioni blueprint per Multi-Site Manager](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#multi-site-manager-blueprint-configurations)
* [Configurazioni di rollout di Multi-Site Manager](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#multi-site-manager-rollout-configurations)
* [Modello e-mail notifica evento pagina](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#page-event-notification-e-mail-template)
* [Scaffolding pagine](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#page-scaffolding)
* [Griglia reattiva MENO](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#responsive-grid-less)
* [Progettazioni modelli statici](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#static-template-designs)
<!-- Search&Promote is end-of-life September 1, 2022 * [Adobe Search and Promote Integration Client Libraries](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#adobe-search-and-promote-integration-client-libraries) -->
* [Librerie client di integrazione Adobe Target](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#adobe-target-integration-client-libraries)
* [Librerie client WCM Foundation](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#wcm-foundation-client-libraries)

## Con aggiornamento 6.5 {#with-upgrade}

### Segmenti ContextHub {#contexthub-segments}

<table>
 <tbody>
  <tr>
   <td><strong>Posizione precedente</strong></td>
   <td><code>/etc/segmentation/contexthub</code></td>
  </tr>
  <tr>
   <td><strong>Nuove posizioni</strong></td>
   <td><p><code>/apps/settings/wcm/segments</code><br /> </p> <p><code>/conf/settings/settings/wcm/segments</code><br /> </p> <p><code>/conf/&lt;tenant&gt;/settings/wcm/segments</code></p> </td>
  </tr>
  <tr>
   <td><strong>Orientamenti per la ristrutturazione</strong></td>
   <td><p>Se alcuni segmenti ContextHub nuovi o modificati vengono modificati nel controllo del codice sorgente anziché essere modificati in AEM, è necessario migrarli alla nuova posizione:</p>
    <ol>
     <li>Copia tutti i segmenti ContextHub nuovi o modificati dalla posizione precedente alla nuova posizione appropriata (/<code>apps</code>, <code>/conf/global</code> o <code>/conf/&lt;tenant&gt;</code>)</li>
     <li>Aggiorna i riferimenti ai segmenti ContextHub nella posizione precedente nei segmenti ContextHub migrati nelle nuove posizioni (<code>/apps</code>, <code>/conf/global</code>, <code>/conf/&lt;tenant&gt;</code>).</li>
    </ol> <p>La query QueryBuilder seguente individua tutti i riferimenti ai segmenti ContextHub nelle posizioni precedenti.<br /> <br /> <code class="code">path=/content
       property=cq:segments
       property.operation=like
       property.value=/etc/segmentation/contexthub/%</code><br /> <br /> Questa operazione può essere eseguita tramite <a href="/help/sites-developing/querybuilder-api.md" target="_blank">Interfaccia utente di Debugger di AEM QueryBuilder</a>. Tieni presente che si tratta di una query di attraversamento, pertanto non eseguirla in produzione e assicurati che i limiti di attraversamento vengano corretti in base alle esigenze.</p> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td><p>I segmenti ContextHub persistenti nella posizione precedente vengono visualizzati in sola lettura in <strong>AEM &gt; Personalizzazione &gt; Tipi di pubblico</strong>.</p> <p>Se i segmenti ContextHub devono essere modificabili in AEM, è necessario migrarli alla nuova posizione (<code>/conf/global</code> o <code>/conf/&lt;tenant&gt;</code>). Tutti i nuovi segmenti di ContentHub creati in AEM vengono salvati nella nuova posizione (<code>/conf/global</code> o <code>/conf/&lt;tenant&gt;</code>).</p> <p>Le proprietà della pagina di AEM Sites consentono solo la posizione precedente (<code>/etc</code>) o un'unica nuova posizione (<code>/apps</code>, <code>/conf/global</code> o <code>/conf/&lt;tenant&gt;</code>) per essere selezionato, pertanto è necessario migrare di conseguenza i segmenti ContextHub.</p> <p>Eventuali segmenti ContextHub inutilizzati dai siti di riferimento AEM possono essere rimossi e non migrati alla nuova posizione:</p>
    <ul>
     <li>/etc/segmentation/geometrixx/</li>
     <li>/etc/segmentation/geometrixx-outdoors</li>
    </ul> <p>Nota: se il ClientContext è in uso, si consiglia di convertirlo in ContextHub.</p> </td>
  </tr>
 </tbody>
</table>

## Prima di un aggiornamento futuro {#prior-to-upgrade}

### Librerie client di Adobe Analytics {#adobe-analytics-client-libraries}

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
   <td><strong>Orientamenti per la ristrutturazione</strong></td>
   <td><p>Qualsiasi utilizzo personalizzato di queste librerie client deve fare riferimento alla libreria client per categoria e non per percorso:</p>
    <ol>
     <li>Eventuali riferimenti alla libreria client per percorso nel percorso precedente devono essere aggiornati per l’utilizzo <a href="/help/sites-developing/clientlibs.md#referencing-client-side-libraries" target="_blank">Framework di riferimento della libreria client AEM</a>.</li>
     <li>Se non è possibile utilizzare il framework di riferimento della libreria client AEM, è possibile fare riferimento al percorso assoluto delle librerie client tramite il servlet proxy della libreria client AEM.
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
   <td><p>La modifica di queste librerie client non è mai stata supportata.</p> <p>Per ottenere le categorie della libreria client, visita ciascuna <code>cq:ClientLIbraryFolder</code> tramite CRXDELite e controlla la proprietà Categories.</p>
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

### Progettazioni classiche da Microsoft Word a pagine Web {#classic-microsoft-word-to-web-page-designs}

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
   <td><strong>Orientamenti per la ristrutturazione</strong></td>
   <td><p>Per qualsiasi design gestito in SCM e non scritto in fase di esecuzione tramite le finestre di dialogo per progettazione.</p>
    <ol>
     <li>Copia le progettazioni dalla posizione precedente alla nuova posizione (<code>/apps</code>).</li>
     <li>Convertire qualsiasi risorsa CSS, JavaScript e statica nella progettazione in una <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">Libreria client</a> con <code>allowProxy = true</code>.</li>
     <li>Aggiornare i riferimenti alla posizione precedente nella proprietà cq:designPath.</li>
     <li>Aggiorna tutte le pagine che fanno riferimento alla posizione precedente per utilizzare la nuova categoria Libreria client (è necessario aggiornare il codice di implementazione della pagina).</li>
     <li>Aggiorna le regole del Dispatcher AEM per consentire la distribuzione delle librerie client tramite <code>/etc.clientlibs/</code> servlet proxy</li>
    </ol> <p>Per tutte le progettazioni che NON sono state gestite in SCM e che sono state modificate in fase di esecuzione tramite le finestre di dialogo di progettazione:</p>
    <ul>
     <li>Non spostare i design modificabili da <code>/etc</code>.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td>N/D<br /> </td>
  </tr>
 </tbody>
</table>

### Configurazioni emulatore dispositivo mobile {#mobile-device-emulator-configurations}

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
   <td><strong>Orientamenti per la ristrutturazione</strong></td>
   <td>Tutte le nuove configurazioni dell’emulatore di dispositivi mobili devono essere migrate alla nuova posizione.
    <ol>
     <li>Copia le nuove configurazioni dell’emulatore di dispositivi mobili dalla posizione precedente alla nuova posizione (<code>/apps</code>, <code>/conf/global</code>, <code>/conf/&lt;tenant&gt;</code>).</li>
     <li>Per tutte le pagine AEM Sites che dipendono da queste configurazioni dell’emulatore di dispositivi mobili, aggiorna il <span class="code">
       <code>
        jcr
       </code>
       <code>
        :content
       </code></span> nodo: <br /> <span class="code">[cq:Page]/jcr:content@cq:
       <code>
        deviceGroups
       </code> = String[ mobile/groups/responsive ]</span></li>
     <li>Per tutti i modelli modificabili che dipendono da queste configurazioni dell’emulatore di dispositivi mobili, aggiorna i modelli modificabili, puntando il <span class="code">
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
   <td><p>La risoluzione delle configurazioni dell’emulatore di dispositivi mobili avviene nell’ordine seguente:</p>
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

### Configurazioni blueprint per Multi-Site Manager {#multi-site-manager-blueprint-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>Posizione precedente</strong></td>
   <td><code>/etc/blueprints</code></td>
  </tr>
  <tr>
   <td><strong>Nuove posizioni</strong></td>
   <td><p><code>/apps/msm</code> (Configurazioni blueprint cliente)</p> <p><code>/libs/msm</code> (Configurazioni blueprint predefinite per Screens, Commerce)</p> </td>
  </tr>
  <tr>
   <td><strong>Orientamenti per la ristrutturazione</strong></td>
   <td><p>Qualsiasi configurazione blueprint di Multi-Site Manager nuova o modificata deve essere migrata alla nuova posizione (<code>/apps</code>).</p>
    <ol>
     <li>Copia tutte le configurazioni blueprint di Multi-Site Manager nuove o modificate dalla posizione precedente alla nuova posizione (<code>/apps</code>).</li>
     <li>Rimuovi tutte le configurazioni blueprint di Multi-Site Manager migrate dalla posizione precedente.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td><p>Tutte le configurazioni blueprint per Multi-Site Manager fornite dall’AEM esistono nella nuova posizione in <code>/libs</code>.</p> <p>Il contenuto non fa riferimento alle configurazioni blu di Multi-Site Manager, pertanto non sono presenti riferimenti al contenuto da regolare.</p> </td>
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
   <td><strong>Orientamenti per la ristrutturazione</strong></td>
   <td><p>Tutte le configurazioni di rollout di Multi-Site Manager nuove o modificate devono essere migrate alla nuova posizione.</p>
    <ol>
     <li>Copia tutte le configurazioni di rollout di Multi-Site Manager nuove o modificate dalla posizione precedente alla nuova posizione (<code>/apps</code>).</li>
     <li>Aggiornare tutti i riferimenti nelle pagine AEM alle configurazioni di rollout di Multi-Site Manager nella posizione precedente, per puntare alle controparti nelle nuove posizioni (<code>/libs</code> o <code>/apps</code>).</li>
    </ol> <p>Rimuovi le configurazioni di rollout di Multi-Site Manager migrate dalla posizione precedente.</p> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td>Se non si rimuovono le configurazioni di rollout di Multi-Site Manager migrate dalla posizione precedente, gli autori AEM visualizzano opzioni di rollout duplicate.</td>
  </tr>
 </tbody>
</table>

### Modello e-mail notifica evento pagina {#page-event-notification-e-mail-template}

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
   <td><strong>Orientamenti per la ristrutturazione</strong></td>
   <td><p>Gli unici nuovi modelli di posta elettronica di notifica eventi pagina supportati sono quelli che supportano le nuove impostazioni internazionali.</p> <p>La risoluzione del modello di posta elettronica eventi pagina viene eseguita nell'ordine seguente:</p>
    <ol>
     <li><code>/etc/notification/email/default/com.day.cq.wcm.core.page</code></li>
     <li><code>/apps/settings/notification-templates/com.day.cq.wcm.core.page</code></li>
     <li><code>/libs/settings/notification-templates/com.day.cq.wcm.core.page</code></li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td><p>Qualsiasi modello di posta elettronica di notifica eventi pagina nuovo o modificato deve essere migrato nella nuova posizione in <code>/apps</code>:</p>
    <ol>
     <li>Copiare nella nuova posizione tutti i modelli di messaggio di notifica eventi pagina nuovi o modificati dalla posizione precedente (<code>/apps</code>).</li>
     <li>Rimuovere i modelli di posta elettronica di notifica eventi pagina migrati dalla posizione precedente.</li>
    </ol> </td>
  </tr>
 </tbody>
</table>

### Scaffolding pagine {#page-scaffolding}

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
   <td><strong>Orientamenti per la ristrutturazione</strong></td>
   <td>Lo scaffolding creato nella posizione precedente utilizza il framework di scaffolding legacy e non può essere migrato nella nuova posizione. Per allinearsi alla nuova posizione, qualsiasi scaffolding legacy deve essere risviluppato utilizzando il framework di scaffolding supportato.</td>
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
   <td><strong>Orientamenti per la ristrutturazione</strong></td>
   <td><p>Eventuali riferimenti alla posizione precedente nei file LESS personalizzati devono essere aggiornati per l’importazione dalla nuova posizione.</p>
    <ul>
     <li>Aggiornare tutti i file LESS personalizzati di riferimento che fanno riferimento a grid_base.less nella posizione precedente per fare riferimento alla nuova posizione.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td>Con riferimento a un non esistente <code>grid_base.less</code> Il file impedisce il funzionamento della modalità Layout dell’Editor pagina e modello e altera il layout della pagina.</td>
  </tr>
 </tbody>
</table>

### Progettazioni modelli statici {#static-template-designs}

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
   <td><strong>Orientamenti per la ristrutturazione</strong></td>
   <td><p>Per qualsiasi design gestito in SCM e non scritto in fase di esecuzione tramite le finestre di dialogo per progettazione.</p>
    <ol>
     <li>Copia le progettazioni dalla posizione precedente alla nuova posizione (<code>/apps</code>).</li>
     <li>Convertire qualsiasi risorsa CSS, JavaScript e statica nella progettazione in una <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">Libreria client</a> con <code>allowProxy = true</code>.</li>
     <li>Aggiornare i riferimenti alla posizione precedente in <code>cq:designPath</code> proprietà tramite <strong>AEM &gt; Sites &gt; Pagine del sito personalizzate &gt; Proprietà pagina &gt; Scheda Avanzate &gt; Campo di progettazione</strong>.</li>
     <li>Aggiorna tutte le pagine che fanno riferimento alla posizione precedente per utilizzare la nuova categoria Libreria client (è necessario aggiornare il codice di implementazione della pagina).</li>
     <li>Aggiorna le regole del Dispatcher AEM per consentire la distribuzione delle librerie client tramite <code>/etc.clientlibs/</code> servlet proxy</li>
    </ol> <p>Per tutte le progettazioni che NON sono state gestite in SCM e che sono state modificate in fase di esecuzione tramite le finestre di dialogo di progettazione:</p>
    <ul>
     <li>Non spostare i design modificabili da <code>/etc</code>.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td>L’approccio consigliato è quello di creare AEM Sites e pagine utilizzando modelli modificabili che utilizzano Contenuto struttura e Criteri al posto di Progettazioni.</td>
  </tr>
 </tbody>
</table>

<!-- Search&Promote is end of life as of September 1, 2022 ### Adobe Search and Promote Integration Client Libraries {#adobe-search-and-promote-integration-client-libraries}

<table>
 <tbody>
  <tr>
   <td><strong>Previous location</strong></td>
   <td><p><code>/etc/clientlibs/foundation/searchpromote</code></p> </td>
  </tr>
  <tr>
   <td><strong>New location(s)</strong></td>
   <td><code>/libs/cq/searchpromote/clientlibs/searchpromote</code></td>
  </tr>
  <tr>
   <td><strong>Restructuring guidance</strong></td>
   <td><p>Any custom use of these Client Libraries should reference the Client Library by category, and not by path.</p>
    <ol>
     <li>Any references to the Client Library by path at the Previous Location should be updated to use <a href="/help/sites-developing/clientlibs.md#referencing-client-side-libraries" target="_blank">AEM's Client Library referencing framework</a>.</li>
     <li>If AEM's Client Library referencing framework cannot be used, the absolute path of the Client Libraries can be referenced via AEM's Client Library Proxy servlet:</li>
    </ol>
    <ul>
     <li><code>/etc.clientlibs/cq/searchpromote/clientlibs/searchpromotei.js</code></li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Notes</strong></td>
   <td><p>Editing of these Client Libraries was never supported.</p> <p>To obtain the Client Library categories, visit each cq:ClientLIbraryFolder node via CRXDELite and inspect the categories property:</p>
    <ul>
     <li><code>/libs/cq/searchpromote/clientlibs/searchpromote</code></li>
    </ul> </td>
  </tr>
 </tbody>
</table> -->

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
   <td><strong>Orientamenti per la ristrutturazione</strong></td>
   <td><p>Qualsiasi utilizzo personalizzato di queste librerie client deve fare riferimento alla libreria client per categoria e non per percorso.</p>
    <ol>
     <li>Eventuali riferimenti alla libreria client per percorso nel percorso precedente devono essere aggiornati per l’utilizzo <a href="/help/sites-developing/clientlibs.md#referencing-client-side-libraries" target="_blank">Framework di riferimento della libreria client AEM</a>.</li>
     <li>Se non è possibile utilizzare il framework di riferimento della libreria client AEM, è possibile fare riferimento al percorso assoluto delle librerie client tramite il servlet proxy della libreria client AEM:</li>
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
   <td><p>La modifica di queste librerie client non è mai stata supportata.</p> <p>Per ottenere le categorie della libreria client, visita ogni nodo cq:ClientLIbriaryFolder tramite CRXDELite e controlla la proprietà Categories:</p>
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

### Librerie client WCM Foundation {#wcm-foundation-client-libraries}

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
   <td><strong>Orientamenti per la ristrutturazione</strong></td>
   <td><p>Qualsiasi utilizzo personalizzato di queste librerie client deve fare riferimento alla libreria client per categoria e non per percorso.</p>
    <ol>
     <li>Eventuali riferimenti alla libreria client per percorso nel percorso precedente devono essere aggiornati per l’utilizzo <a href="/help/sites-developing/clientlibs.md#referencing-client-side-libraries" target="_blank">Framework di riferimento della libreria client AEM</a>.</li>
     <li>Se non è possibile utilizzare il framework di riferimento della libreria client AEM, è possibile fare riferimento al percorso assoluto delle librerie client tramite il servlet proxy della libreria client AEM.</li>
    </ol>
    <ul>
     <li><code>/etc.clientlibs/wcm/foundation/clientlibs/accessibility.css</code></li>
     <li><code>/etc.clientlibs/wcm/foundation/clientlibs/main.css</code></li>
     <li><code>/etc.clientlibs/wcm/foundation/clientlibs/main.js</code></li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td><p>La modifica di queste librerie client non è mai stata supportata.</p> <p>Per ottenere le categorie della libreria client, visita ciascuna <code>cq:ClientLIbraryFolder</code> tramite CRXDELite ed esamina la proprietà Categories:</p>
    <ul>
     <li><code>/libs/wcm/foundation/clientlibs/accessibility</code></li>
     <li><code>/libs/wcm/foundation/clientlibs/main</code></li>
    </ul> </td>
  </tr>
 </tbody>
</table>
