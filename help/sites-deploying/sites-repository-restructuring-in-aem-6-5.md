---
title: Ristrutturazione dell'archivio siti in AEM 6.5
seo-title: Ristrutturazione dell'archivio siti in AEM 6.5
description: Scoprite come apportare le modifiche necessarie per eseguire la migrazione alla nuova struttura del repository in AEM 6.5 per Siti.
seo-description: Scoprite come apportare le modifiche necessarie per eseguire la migrazione alla nuova struttura del repository in AEM 6.5 per Siti.
uuid: 6dc5f8bd-1680-40af-9b8f-26c1f4bc3304
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
discoiquuid: 3eccb2d5-c325-43a6-9c03-5f93f7e30712
translation-type: tm+mt
source-git-commit: d20ddba254c965e1b0c0fc84a482b7e89d4df5cb
workflow-type: tm+mt
source-wordcount: '1600'
ht-degree: 1%

---


# Ristrutturazione dell&#39;archivio siti in AEM 6.5 {#sites-repository-restructuring-in-aem}

Come descritto nella pagina [Ristrutturazione repository principale di AEM 6.5](/help/sites-deploying/repository-restructuring.md), i clienti che effettuano l&#39;aggiornamento a AEM 6.5 devono utilizzare questa pagina per valutare lo sforzo di lavoro associato alle modifiche del repository che hanno un impatto sulla soluzione  AEM Sites. Alcune modifiche richiedono sforzi di lavoro durante il processo di aggiornamento di AEM 6.5, mentre altre possono essere posticipate fino a un aggiornamento futuro.

**Con aggiornamento 6.5**

* [Segmenti ContextHub](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#contexthub-segments)

**Prima dell&#39;aggiornamento futuro**

* [ Adobe Analytics Client Libraries](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#adobe-analytics-client-libraries)
* [Design classici da Microsoft Word a pagina Web](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#classic-microsoft-word-to-web-page-designs)
* [Configurazioni emulatore dispositivo mobile](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#mobile-device-emulator-configurations)
* [Configurazioni Blueprint Manager multisito](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#multi-site-manager-blueprint-configurations)
* [Configurazioni di rollout di Multi-Site Manager](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#multi-site-manager-rollout-configurations)
* [Modello e-mail notifica evento pagina](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#page-event-notification-e-mail-template)
* [Scaffolding pagina](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#page-scaffolding)
* [Griglia reattiva](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#responsive-grid-less)
* [Modelli statici](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#static-template-designs)
* [ librerie client di ricerca e integrazione Promote Adobe](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#adobe-search-and-promote-integration-client-libraries)
* [ Adobe Target Integration Client Libraries](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#adobe-target-integration-client-libraries)
* [Librerie client di WCM Foundation](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#wcm-foundation-client-libraries)

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
   <td><p><code>/apps/settings/wcm/segments</code> </p> <p><code>/conf/settings/settings/wcm/segments</code> </p> <p><code>/conf/&lt;tenant&gt;/settings/wcm/segments</code></p> </td>
  </tr>
  <tr>
   <td><strong>Orientamenti per la ristrutturazione</strong></td>
   <td><p>Se i segmenti ContextHub nuovi o modificati devono essere modificati nel controllo del codice sorgente anziché essere modificati in AEM, devono essere migrati nella nuova posizione:</p>
    <ol>
     <li>Copiare eventuali segmenti ContextHub nuovi o modificati dalla posizione precedente alla nuova posizione appropriata (/<code>apps</code>, <code>/conf/global</code> o <code>/conf/&lt;tenant&gt;</code>)</li>
     <li>Aggiorna i riferimenti ai segmenti ContextHub nella posizione precedente ai segmenti ContextHub migrati nelle nuove posizioni (<code>/apps</code>, <code>/conf/global</code>, <code>/conf/&lt;tenant&gt;</code>).</li>
    </ol> <p>La seguente query QueryBuilder individua tutti i riferimenti ai segmenti ContextHub nelle posizioni precedenti.<br /> <br /> <code class="code">path=/content
       property=cq:segments
       property.operation=like
       property.value=/etc/segmentation/contexthub/%</code><br /> <br /> Questo può essere eseguito tramite  <a href="/help/sites-developing/querybuilder-api.md" target="_blank">AEM interfaccia utente</a> del debugger di QueryBuilder. Notate che si tratta di una query di attraversamento, quindi non eseguitela rispetto alla produzione e accertatevi che i limiti di attraversamento vengano regolati in base alle esigenze.</p> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td><p>I segmenti ContextHub persistenti nella posizione precedente vengono visualizzati in sola lettura in <strong>AEM &gt; Personalizzazione &gt; Audiences</strong>.</p> <p>Se i segmenti ContextHub devono essere modificabili in AEM, devono essere migrati nella nuova posizione (<code>/conf/global</code> o <code>/conf/&lt;tenant&gt;</code>). Eventuali nuovi segmenti di ContentHub creati in AEM vengono memorizzati nella nuova posizione (<code>/conf/global</code> o <code>/conf/&lt;tenant&gt;</code>).</p> <p> Proprietà pagina AEM Sites consentono solo di selezionare la posizione precedente (<code>/etc</code>) o una singola nuova posizione (<code>/apps</code>, <code>/conf/global</code> o <code>/conf/&lt;tenant&gt;</code>), pertanto i segmenti ContextHub devono essere migrati di conseguenza.</p> <p>Eventuali segmenti ContextHub non utilizzati dai siti di riferimento AEM possono essere rimossi e non migrati nella nuova posizione:</p>
    <ul>
     <li>/etc/segmentation/geometrixx/</li>
     <li>/etc/segmentation/geometrixx-outdoors</li>
    </ul> <p>Nota: Se il ClientContext è in uso, si consiglia di eseguire la conversione in ContextHub.</p> </td>
  </tr>
 </tbody>
</table>

## Prima dell&#39;aggiornamento futuro {#prior-to-upgrade}

###  librerie client Adobe Analytics {#adobe-analytics-client-libraries}

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
   <td><p>L'uso personalizzato di queste librerie client deve fare riferimento alla libreria client per categoria e non per percorso:</p>
    <ol>
     <li>Eventuali riferimenti alla libreria client per percorso nella posizione precedente devono essere aggiornati per utilizzare il framework di riferimento della libreria client <a href="/help/sites-developing/clientlibs.md#referencing-client-side-libraries" target="_blank">AEM</a>.</li>
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
   <td><p>La modifica di queste librerie client non è mai stata supportata.</p> <p>Per ottenere le categorie Libreria client, visitare ciascun nodo <code>cq:ClientLIbraryFolder</code> tramite CRXDELite ed esaminare la proprietà category.</p>
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

### Progettazione classiche di pagine da Microsoft Word a Web {#classic-microsoft-word-to-web-page-designs}

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
   <td><p>Per tutte le progettazioni gestite in SCM e non scritte in fase di esecuzione tramite le finestre di dialogo Progettazione.</p>
    <ol>
     <li>Copiate le progettazioni dalla posizione precedente alla nuova posizione (<code>/apps</code>).</li>
     <li>Convertite eventuali risorse CSS, JavaScript e statiche nella progettazione in una <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">libreria client</a> con <code>allowProxy = true</code>.</li>
     <li>Aggiorna i riferimenti alla posizione precedente nella proprietà cq:designPath.</li>
     <li>Aggiorna tutte le pagine che fanno riferimento al percorso precedente per utilizzare la nuova categoria Libreria client (per questo è necessario aggiornare il codice di implementazione Pagina).</li>
     <li>Aggiorna AEM regole del dispatcher per consentire la trasmissione delle librerie client tramite il servlet proxy <code>/etc.clientlibs/</code>.</li>
    </ol> <p>Per qualsiasi progettazione NON gestita in SCM e modificata in fase di esecuzione tramite le finestre di dialogo Progettazione:</p>
    <ul>
     <li>Non spostare Designer modificabili da <code>/etc</code>.</li>
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
   <td>Qualsiasi nuova configurazione dell'emulatore di dispositivi mobili deve essere migrata nella nuova posizione.
    <ol>
     <li>Copiate le nuove configurazioni dell'emulatore di dispositivi mobili dal percorso precedente alla nuova posizione (<code>/apps</code>, <code>/conf/global</code>, <code>/conf/&lt;tenant&gt;</code>).</li>
     <li>Per tutte  pagine AEM Sites che dipendono da queste configurazioni dell'emulatore di dispositivi mobili, aggiorna la pagina <span class="code">
       <code>
        jcr
       </code>
       <code>
        :content
       </code></span> nodo: <br /> <span class="code">[cq:Page]/jcr:content@cq:
       <code>
        deviceGroups
       </code> = String[ mobile/group/reattivo ]</span></li>
     <li>Per tutti i modelli modificabili che dipendono da queste configurazioni dell'emulatore di dispositivi mobili, aggiorna i modelli modificabili, indicando la <span class="code">
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
   <td><p>La risoluzione delle configurazioni dell'emulatore del dispositivo mobile si verifica nell'ordine seguente:</p>
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

### Configurazioni Blueprint Manager multisito {#multi-site-manager-blueprint-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>Posizione precedente</strong></td>
   <td><code>/etc/blueprints</code></td>
  </tr>
  <tr>
   <td><strong>Nuove posizioni</strong></td>
   <td><p><code>/apps/msm</code> (configurazioni Blueprint cliente)</p> <p><code>/libs/msm</code> (configurazioni di Blueprint Box per schermi, Commerce)</p> </td>
  </tr>
  <tr>
   <td><strong>Orientamenti per la ristrutturazione</strong></td>
   <td><p>Eventuali nuove configurazioni di Blueprint Manager multisito o modificate devono essere trasferite nella nuova posizione (<code>/apps</code>).</p>
    <ol>
     <li>Copiate le configurazioni Blueprint Manager multisito o modificate dalla posizione precedente alla nuova posizione (<code>/apps</code>).</li>
     <li>Rimuovere tutte le configurazioni di blueprint Manager multisito migrate dalla posizione precedente.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td><p>Tutte le configurazioni di Blueprint Manager multisito AEM sono disponibili nella nuova posizione in <code>/libs</code>.</p> <p>Il contenuto non fa riferimento alle configurazioni Blue Manager multisito, pertanto non sono presenti riferimenti di contenuto da regolare.</p> </td>
  </tr>
 </tbody>
</table>

### Configurazioni di rollout di più siti Manager {#multi-site-manager-rollout-configurations}

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
   <td><p>Tutte le configurazioni di rollout manager multisito nuove o modificate devono essere trasferite nella nuova posizione.</p>
    <ol>
     <li>Copiate le configurazioni di rollout manager multisito nuove o modificate dalla posizione precedente alla nuova posizione (<code>/apps</code>).</li>
     <li>Aggiornate i riferimenti AEM pagine alle configurazioni di rollout Manager multisito nella posizione precedente, per indicare le controparti nelle nuove posizioni (<code>/libs</code> o <code>/apps</code>).</li>
    </ol> <p>Rimuovere le configurazioni di rollout Manager multisito migrate dalla posizione precedente.</p> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td>La mancata rimozione delle configurazioni di rollout Manager multisito migrate dalla posizione precedente determina la visualizzazione di opzioni di rollout duplicate per gli autori AEM.</td>
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
   <td><p>I nuovi modelli e-mail di notifica degli eventi di pagina supportati sono solo quelli che supportano le nuove impostazioni internazionali.</p> <p>La risoluzione del modello e-mail evento pagina si verifica nel seguente ordine:</p>
    <ol>
     <li><code>/etc/notification/email/default/com.day.cq.wcm.core.page</code></li>
     <li><code>/apps/settings/notification-templates/com.day.cq.wcm.core.page</code></li>
     <li><code>/libs/settings/notification-templates/com.day.cq.wcm.core.page</code></li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td><p>Eventuali modelli e-mail di notifica evento pagina nuovi o modificati devono essere migrati nella nuova posizione in <code>/apps</code>:</p>
    <ol>
     <li>Copiate i modelli e-mail di notifica evento pagina nuovi o modificati dal percorso precedente al nuovo percorso (<code>/apps</code>).</li>
     <li>Rimuovete eventuali modelli e-mail di notifica eventi pagina migrati dal percorso precedente.</li>
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
   <td><strong>Orientamenti per la ristrutturazione</strong></td>
   <td>Lo scaffolding creato in Posizione precedente utilizza il framework Scaffolding legacy e non può essere migrato nella Nuova posizione. Per allineare con la nuova posizione, qualsiasi Scaffolding legacy deve essere risviluppato utilizzando il framework Scaffolding supportato.</td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td>N/D<br /> </td>
  </tr>
 </tbody>
</table>

### Griglia reattiva {#responsive-grid-less}

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
   <td><p>Eventuali riferimenti alla posizione precedente nei file LESS personalizzati devono essere aggiornati per essere importati dalla nuova posizione.</p>
    <ul>
     <li>Aggiorna tutti i file LESS personalizzati che fanno riferimento a grid_base.less nella Posizione precedente per fare riferimento alla nuova posizione.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td>Facendo riferimento a un file <code>grid_base.less</code> non esistente, la modalità di layout dell'Editor pagina e modelli non funziona e si verifica un'interruzione del layout di pagina.</td>
  </tr>
 </tbody>
</table>

### Progettazione modelli statici {#static-template-designs}

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
   <td><p>Per tutte le progettazioni gestite in SCM e non scritte in fase di esecuzione tramite le finestre di dialogo Progettazione.</p>
    <ol>
     <li>Copiate le progettazioni dalla posizione precedente alla nuova posizione (<code>/apps</code>).</li>
     <li>Convertite eventuali risorse CSS, JavaScript e statiche nella progettazione in una <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">libreria client</a> con <code>allowProxy = true</code>.</li>
     <li>Aggiornare i riferimenti alla posizione precedente nella proprietà <code>cq:designPath</code> tramite <strong>AEM &gt; Siti &gt; Pagine del sito personalizzate &gt; Proprietà pagina &gt; scheda Avanzate &gt; Campo di progettazione</strong>.</li>
     <li>Aggiorna tutte le pagine che fanno riferimento al percorso precedente per utilizzare la nuova categoria Libreria client (per questo è necessario aggiornare il codice di implementazione Pagina).</li>
     <li>Aggiorna AEM regole del dispatcher per consentire la trasmissione delle librerie client tramite il servlet proxy <code>/etc.clientlibs/</code>.</li>
    </ol> <p>Per qualsiasi progettazione NON gestita in SCM e modificata in fase di esecuzione tramite le finestre di dialogo Progettazione:</p>
    <ul>
     <li>Non spostare Designer modificabili da <code>/etc</code>.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td>L'approccio consigliato consiste nel creare  AEM Sites e pagine utilizzando Modelli modificabili che utilizzano Struttura, Contenuto e Criteri al posto di Designer.</td>
  </tr>
 </tbody>
</table>

###  librerie client di ricerca e integrazione Promote {#adobe-search-and-promote-integration-client-libraries}

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
   <td><strong>Orientamenti per la ristrutturazione</strong></td>
   <td><p>Qualsiasi utilizzo personalizzato di queste librerie client deve fare riferimento alla libreria client per categoria, e non per percorso.</p>
    <ol>
     <li>Eventuali riferimenti alla libreria client per percorso nella posizione precedente devono essere aggiornati per utilizzare il framework di riferimento della libreria client <a href="/help/sites-developing/clientlibs.md#referencing-client-side-libraries" target="_blank">AEM</a>.</li>
     <li>Se AEM framework di riferimento della libreria client non può essere utilizzato, è possibile fare riferimento al percorso assoluto delle librerie client tramite AEM servlet proxy libreria client:</li>
    </ol>
    <ul>
     <li><code>/etc.clientlibs/cq/searchpromote/clientlibs/searchpromotei.js</code></li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td><p>La modifica di queste librerie client non è mai stata supportata.</p> <p>Per ottenere le categorie Libreria client, visitare ogni nodo cq:ClientLIbraryFolder tramite CRXDELite ed esaminare la proprietà category:</p>
    <ul>
     <li><code>/libs/cq/searchpromote/clientlibs/searchpromote</code></li>
    </ul> </td>
  </tr>
 </tbody>
</table>

###  Adobe Target Integration Client Libraries {#adobe-target-integration-client-libraries}

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
   <td><p>Qualsiasi utilizzo personalizzato di queste librerie client deve fare riferimento alla libreria client per categoria, e non per percorso.</p>
    <ol>
     <li>Eventuali riferimenti alla libreria client per percorso nella posizione precedente devono essere aggiornati per utilizzare il framework di riferimento della libreria client <a href="/help/sites-developing/clientlibs.md#referencing-client-side-libraries" target="_blank">AEM</a>.</li>
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
   <td><p>La modifica di queste librerie client non è mai stata supportata.</p> <p>Per ottenere le categorie Libreria client, visitare ogni nodo cq:ClientLIbraryFolder tramite CRXDELite ed esaminare la proprietà category:</p>
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
   <td><strong>Orientamenti per la ristrutturazione</strong></td>
   <td><p>Qualsiasi utilizzo personalizzato di queste librerie client deve fare riferimento alla libreria client per categoria, e non per percorso.</p>
    <ol>
     <li>Eventuali riferimenti alla libreria client per percorso nella posizione precedente devono essere aggiornati per utilizzare il framework di riferimento della libreria client <a href="/help/sites-developing/clientlibs.md#referencing-client-side-libraries" target="_blank">AEM</a>.</li>
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
   <td><p>La modifica di queste librerie client non è mai stata supportata.</p> <p>Per ottenere le categorie Libreria client, visitare ciascun nodo <code>cq:ClientLIbraryFolder</code> tramite CRXDELite ed esaminare la proprietà category:</p>
    <ul>
     <li><code>/libs/wcm/foundation/clientlibs/accessibility</code></li>
     <li><code>/libs/wcm/foundation/clientlibs/main</code></li>
    </ul> </td>
  </tr>
 </tbody>
</table>

