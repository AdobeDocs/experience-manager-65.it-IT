---
title: Ristrutturazione del repository comune in AEM 6.5
seo-title: Ristrutturazione del repository comune in AEM 6.5
description: Scopri come apportare le modifiche necessarie per eseguire la migrazione alla nuova struttura del repository in AEM 6.5, comune per tutte le aree di AEM.
seo-description: Scopri come apportare le modifiche necessarie per eseguire la migrazione alla nuova struttura del repository in AEM 6.5, comune per tutte le aree di AEM.
uuid: a4bb64e5-387b-4084-9258-54e68db12f3b
contentOwner: chaikels
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
discoiquuid: 80bd707f-c02d-4616-9b45-90f6c726abea
translation-type: tm+mt
source-git-commit: d20ddba254c965e1b0c0fc84a482b7e89d4df5cb

---


# Ristrutturazione del repository comune in AEM 6.5 {#common-repository-restructuring-in-aem}

Come descritto nella pagina Ristrutturazione [repository padre in AEM 6.5](/help/sites-deploying/repository-restructuring.md) , i clienti che effettuano l’aggiornamento ad AEM 6.5 devono utilizzare questa pagina per valutare lo sforzo di lavoro associato alle modifiche del repository che possono avere un impatto su tutte le soluzioni. Alcune modifiche richiedono sforzi durante il processo di aggiornamento di AEM 6.5, mentre altre possono essere posticipate fino a un aggiornamento futuro.

**Con aggiornamento 6.5**

* [Istanze flusso di lavoro](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#workflow-instances)
* [Modelli flusso di lavoro](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#workflow-models)
* [Moduli di avvio per flusso di lavoro](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#workflow-launchers)
* [Script flusso di lavoro](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#workflow-scripts)

**Prima dell&#39;aggiornamento futuro**

* [Configurazioni ContextHub](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#contexthub-configurations)
* [Progettazione servizi cloud classici](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#classic-cloud-services-designs)
* [Design classici per dashboard](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#classic-dashboards-designs)
* [Progettazione report classici](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#classic-reports-designs)
* [Strutture predefinite](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#default-designs)
* [Endpoint JavaScript di Adobe DTM](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#adobe-dtm-javascript-endpoint)
* [Endpoint web-snap Adobe DTM](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#adobe-dtm-web-hook-endpoint)
* [Attività Inbox](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#inbox-tasks)
* [Configurazioni Blueprint Manager multisito](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#multi-site-manager-blueprint-configurations)
* [Configurazioni del gadget per il dashboard di AEM Projects](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#aem-projects-dashboard-gadget-configurations)
* [Modello e-mail notifica replica](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#replication-notification-e-mail-template)
* [Tag](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#tags)
* [Servizi cloud di traduzione](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#translation-cloud-services)
* [Lingue di traduzione](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#translation-languages)
* [Regole di traduzione](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#translation-rules)
* [Libreria Client Widget di traduzione](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#translation-widget-client-library)
* [Console Web attivazione albero](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#tree-activation-web-console)
* [Servizi cloud del connettore di traduzione fornitori](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#vendor-translation-connector-cloud-services)
* [Modelli e-mail notifica flusso di lavoro](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#workflow-notification-email-templates)

## Con aggiornamento 6.5 {#with-upgrade}

### Modelli flusso di lavoro {#workflow-models}

<table>
 <tbody>
  <tr>
   <td><strong>Posizione precedente</strong></td>
   <td><code>/etc/workflow/models</code></td>
  </tr>
  <tr>
   <td><strong>Nuove posizioni</strong></td>
   <td><p><code>/libs/settings/workflow/models</code></p> <p><code>/conf/global/settings/workflow/models</code></p> <p><code>/var/workflow/models</code></p> </td>
  </tr>
  <tr>
   <td><strong>Orientamenti per la ristrutturazione</strong></td>
   <td><p>Eventuali modelli di flussi di lavoro nuovi o modificati devono essere migrati in /conf/global/workflow/models.</p>
    <ol>
     <li>Distribuisci i modelli di flussi di lavoro modificati in un’istanza di sviluppo locale di AEM 6.4, in modo che siano già presenti nel percorso precedente.</li>
     <li>Modificate il modello di flusso di lavoro utilizzando l'Editor modello di flusso di lavoro di AEM in AEM &gt; Strumenti &gt; Flusso di lavoro &gt; Modelli.</li>
     <li>Durante la migrazione dei modelli di flussi di lavoro forniti da AEM modificati
      <ol>
       <li>Con l’Editor modello flusso di lavoro aperto, modificate l’URL dell’indirizzo del browser e sostituite il segmento di percorso /libs/settings/workflow/models con /etc/workflow/models.
        <ul>
         <li>Ad esempio, modificare: <em>http://localhost:4502/editor.html<strong>/libs/settings/workflow/models</strong>/dam/update_asset.html</em> a <em>http://localhost:4502/editor.html<strong>/etc/workflow/models</strong>/dam/update_asset.html</em></li>
        </ul> </li>
      </ol> </li>
     <li>Attiva la modalità Modifica nell’Editor modello flusso di lavoro, che copierà la definizione del modello di flusso di lavoro in /conf/global/workflow/models.</li>
     <li>Toccate il pulsante Sinc. per sincronizzare le modifiche al modello Flusso di lavoro runtime in /var/workflow/models.</li>
     <li>Esportate sia il modello di flusso di lavoro (/conf/global/workflow/models/&lt;workflow-model&gt;) che il modello di flusso di lavoro in fase di esecuzione (/var/workflow/models/&lt;workflow-model&gt;) e integrate nel progetto AEM.
      <ol>
       <li>Ad esempio, export:
        <ul>
         <li><code>/config/settings/workflow/models/dam/my_workflow_model</code> e </li>
         <li><code>/var/workflow/models/dam/my_workflow_model</code></li>
        </ul> </li>
      </ol> </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td><p>La risoluzione del modello di flusso di lavoro si verifica nell'ordine seguente:</p>
    <ol>
     <li><code>/conf/global/settings/workflow/models</code></li>
     <li><code>/libs/settings/workflow/models</code></li>
     <li><code>/etc/workflow/models</code></li>
    </ol> <p>Di conseguenza, tutte le personalizzazioni dei modelli di flussi di lavoro forniti da AEM presenti nella posizione Precedente devono essere spostate in /conf/global/settings/workflow/models se devono essere conservati. In caso contrario verranno sostituite dalla definizione del modello di flussi di lavoro fornita da AEM in /libs/settings/workflow/models.</p> </td>
  </tr>
 </tbody>
</table>

### Istanze flusso di lavoro {#workflow-instances}

<table>
 <tbody>
  <tr>
   <td><strong>Posizione precedente</strong></td>
   <td><code>/etc/workflow/instances</code></td>
  </tr>
  <tr>
   <td><strong>Nuove posizioni</strong></td>
   <td><code>/var/workflow/instances</code></td>
  </tr>
  <tr>
   <td><strong>Orientamenti per la ristrutturazione</strong></td>
   <td><p>Per allineare la nuova posizione non è necessaria alcuna azione.</p> <p>Le istanze storiche del flusso di lavoro possono continuare a risiedere nel percorso precedente in modo sicuro e le nuove istanze del flusso di lavoro verranno create nella nuova posizione.</p> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td>Eventuali riferimenti espliciti al percorso nel <code>
     custom
    </code> codice per la posizione precedente devono tenere conto anche della nuova posizione. È consigliabile che questo codice venga modificato per utilizzare le API del flusso di lavoro AEM.</td>
  </tr>
 </tbody>
</table>

### Moduli di avvio per flusso di lavoro {#workflow-launchers}

<table>
 <tbody>
  <tr>
   <td><strong>Posizione precedente</strong></td>
   <td><code>/etc/workflow/launcher/config</code></td>
  </tr>
  <tr>
   <td><strong>Nuove posizioni</strong></td>
   <td><p><code>/libs/settings/workflow/launcher/config</code></p> <p><code>/conf/global/settings/workflow/launcher/config</code></p> </td>
  </tr>
  <tr>
   <td><strong>Orientamenti per la ristrutturazione</strong></td>
   <td><p>Eventuali avviatori di flussi di lavoro nuovi o modificati devono essere migrati in <code>/conf/global/workflow/launcher/config</code>.</p>
    <ol>
     <li>Copiate le configurazioni nuove o modificate di Workflow Launcher dalla posizione precedente alla nuova posizione (<code>/conf/global</code>).</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td><p>La risoluzione di Workflow Launcher si verifica nel seguente ordine:</p>
    <ol>
     <li><code>/conf/global/settings/workflow/launcher</code></li>
     <li><code>/libs/settings/workflow/launcher</code></li>
     <li><code>/etc/workflow/launcher</code></li>
    </ol> <p>Di conseguenza, tutte le personalizzazioni di Workflow Launcher fornito da AEM persistenti nella posizione Precedente devono essere spostate nella nuova posizione (<code>/conf/global/settings/workflow/launcher</code> se devono essere mantenute, altrimenti saranno sostituite dalla definizione di Workflow Launcher fornita da AEM in <code>/libs/settings/workflow/launcher</code>.</p> </td>
  </tr>
 </tbody>
</table>

### Script flusso di lavoro {#workflow-scripts}

<table>
 <tbody>
  <tr>
   <td><strong>Posizione precedente</strong></td>
   <td><code>/etc/workflow/scripts</code></td>
  </tr>
  <tr>
   <td><strong>Nuove posizioni</strong></td>
   <td><p><code>/libs/workflow/scripts</code></p> <p><code>/apps/workflow/scripts</code></p> </td>
  </tr>
  <tr>
   <td><strong>Orientamenti per la ristrutturazione</strong></td>
   <td><p>Eventuali script di flussi di lavoro nuovi o modificati devono essere migrati nella nuova posizione e i modelli di flussi di lavoro di riferimento aggiornati in base alla nuova posizione.</p>
    <ol>
     <li>Copiate eventuali script di flusso di lavoro nuovi o modificati dal percorso precedente a quello nuovo.<br />
      <ul>
       <li><code>/apps/workflow/scripts</code> devono essere mantenuti in SCM.</li>
      </ul> </li>
     <li>Aggiornate i riferimenti agli script del flusso di lavoro nella posizione precedente nei modelli del flusso di lavoro in modo che puntino alle nuove posizioni.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td><p>AEM 6.4 SP1, al momento del rilascio, consente di posticipare la ristrutturazione fino alle 6.5 <code>
      upgrade
     </code>.</p> <p>Se l’aggiornamento ad AEM 6.4 prima del rilascio di AEM 6.4 SP1, la ristrutturazione deve essere eseguita nell’ambito del progetto di aggiornamento. In caso contrario, la modifica e il salvataggio dei passaggi del flusso di lavoro che fanno riferimento agli script nel percorso precedente rimuoveranno completamente il riferimento allo script del flusso di lavoro dal passaggio del flusso di lavoro, e solo gli script del flusso di lavoro nelle nuove posizioni saranno disponibili nel menu a discesa di selezione degli script.</p> </td>
  </tr>
 </tbody>
</table>

## Prima dell&#39;aggiornamento futuro {#prior-to-upgrade}

### Configurazioni ContextHub {#contexthub-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>Posizione precedente</strong></td>
   <td><code>/etc/cloudsettings</code></td>
  </tr>
  <tr>
   <td><strong>Nuove posizioni</strong></td>
   <td><p><code>/libs/settings/cloudsettings</code></p> <p><code>/conf/global/settings/cloudsettings</code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudsettings</code></p> </td>
  </tr>
  <tr>
   <td><strong>Orientamenti per la ristrutturazione</strong></td>
   <td><p>Eventuali configurazioni ContextHub nuove o modificate devono essere migrate nella nuova posizione e le pagine AEM Sites che fanno riferimento devono essere aggiornate per riflettere la nuova posizione.</p>
    <ol>
     <li>Copiate le configurazioni ContextHub nuove o modificate dalla posizione precedente alla nuova posizione.</li>
     <li>Associate le configurazioni AEM applicabili alle gerarchie di contenuti di AEM.
      <ol>
       <li><strong>Gerarchie di pagine AEM Sites tramite AEM Sites &gt; Page Properties &gt; Advanced Tab &gt; Cloud Configuration</strong>(Siti AEM &gt; Siti AEM &gt; Pagina &gt; Proprietà pagina &gt; scheda Avanzate &gt; Cloud Configuration (Configurazione cloud).</li>
      </ol> </li>
     <li>Separa le configurazioni ContextHub migrate dalle gerarchie di contenuti AEM sopra indicate.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td>N/D</td>
  </tr>
 </tbody>
</table>

### Progettazione servizi cloud classici {#classic-cloud-services-designs}

<table>
 <tbody>
  <tr>
   <td><strong>Posizione precedente</strong></td>
   <td><code>/etc/designs/cloudservices</code></td>
  </tr>
  <tr>
   <td><strong>Nuove posizioni</strong></td>
   <td><p><code>/libs/settings/wcm/designs/cloudservices</code></p> <p><code>/apps/settings/wcm/designs/cloudservices</code></p> </td>
  </tr>
  <tr>
   <td><strong>Orientamenti per la ristrutturazione</strong></td>
   <td><p>Per qualsiasi progettazione gestita in SCM e non scritta in fase di esecuzione tramite le finestre di dialogo Progettazione.</p>
    <ol>
     <li>Copiate le progettazioni dalla posizione precedente alla nuova posizione (<code>/apps</code>).</li>
     <li>Convertite eventuali risorse CSS, JavaScript e statiche nella struttura in una libreria <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank"></a> client con <code>allowProxy = true</code>.</li>
     <li>Aggiorna i riferimenti alla posizione precedente nel <span class="code">percorso <code>
        cq
       </code>:
       <code>
        designPath
       </code></span> property.</li>
     <li>Aggiorna tutte le pagine che fanno riferimento al percorso precedente per utilizzare la nuova categoria Libreria client (per questo è necessario aggiornare il codice di implementazione Pagina).</li>
     <li>Aggiorna le regole del dispatcher AEM per consentire la trasmissione delle librerie client tramite /etc.clientlibs/. servlet proxy.</li>
    </ol> <p>Per tutte le progettazioni NON gestite in SCM e modificate runtime tramite le finestre di dialogo Progettazione.</p>
    <ul>
     <li>Non spostate Designer dall' <code>/etc</code>esterno.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td>N/D</td>
  </tr>
 </tbody>
</table>

### Design classici per dashboard {#classic-dashboards-designs}

<table>
 <tbody>
  <tr>
   <td><strong>Posizione precedente</strong></td>
   <td><code>/etc/designs/dashboards</code></td>
  </tr>
  <tr>
   <td><strong>Nuove posizioni</strong></td>
   <td><p><code>/libs/settings/wcm/designs/dashboards</code></p> <p><code>/apps/settings/wcm/designs/dashboards</code></p> </td>
  </tr>
  <tr>
   <td><strong>Orientamenti per la ristrutturazione</strong></td>
   <td><p>Per qualsiasi progettazione gestita in SCM e non scritta in fase di esecuzione tramite le finestre di dialogo Progettazione.</p>
    <ol>
     <li>Copiate le progettazioni dalla posizione precedente alla nuova posizione (/app).</li>
     <li>Convertite eventuali risorse CSS, JavaScript e statiche nella struttura in una libreria <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank"></a> client con <code>allowProxy = true</code>.</li>
     <li>Aggiorna i riferimenti alla posizione precedente in <code>
       cq
      </code>:
       <code>
       designPath
      </code> property.</li>
     <li>Aggiorna tutte le pagine che fanno riferimento al percorso precedente per utilizzare la nuova categoria Libreria client (per questo è necessario aggiornare il codice di implementazione Pagina).</li>
     <li>Aggiorna le regole del dispatcher AEM per consentire la trasmissione delle librerie client tramite /etc.clientlibs/. servlet proxy.</li>
    </ol> <p>Per tutte le progettazioni NON gestite in SCM e modificate runtime tramite le finestre di dialogo Progettazione.</p>
    <ul>
     <li>Non spostate Designer dall' <code>/etc</code>esterno.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td>N/D</td>
  </tr>
 </tbody>
</table>

### Progettazione report classici {#classic-reports-designs}

<table>
 <tbody>
  <tr>
   <td><strong>Posizione precedente</strong></td>
   <td><code>/etc/designs/reports</code></td>
  </tr>
  <tr>
   <td><strong>Nuove posizioni</strong></td>
   <td><p><code>/libs/settings/wcm/designs/reports</code></p> <p><code>/apps/settings/wcm/designs/reports</code></p> </td>
  </tr>
  <tr>
   <td><strong>Orientamenti per la ristrutturazione</strong></td>
   <td><p>Per qualsiasi progettazione gestita in SCM e non scritta in fase di esecuzione tramite le finestre di dialogo Progettazione.</p>
    <ol>
     <li>Copiate le progettazioni dalla posizione precedente alla nuova posizione (/app).</li>
     <li>Convertite eventuali risorse CSS, JavaScript e statiche nella struttura in una libreria <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank"></a> client con <code>allowProxy = true</code>.</li>
     <li>Aggiorna i riferimenti alla posizione precedente in <code>
       cq
      </code>:
       <code>
       designPath
      </code> property.</li>
     <li>Aggiorna tutte le pagine che fanno riferimento al percorso precedente per utilizzare la nuova categoria Libreria client (per questo è necessario aggiornare il codice di implementazione Pagina).</li>
     <li>Aggiorna le regole del dispatcher AEM per consentire la trasmissione delle librerie client tramite /etc.clientlibs/. servlet proxy.</li>
    </ol> <p>Per tutte le progettazioni NON gestite in SCM e modificate runtime tramite le finestre di dialogo Progettazione.</p>
    <ul>
     <li>Non spostate Designer dall' <code>/etc</code>esterno.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td>N/D</td>
  </tr>
 </tbody>
</table>

### Strutture predefinite {#default-designs}

<table>
 <tbody>
  <tr>
   <td><strong>Posizione precedente</strong></td>
   <td><code>/etc/designs/default</code></td>
  </tr>
  <tr>
   <td><strong>Nuove posizioni</strong></td>
   <td><p><code>/libs/settings/wcm/designs/default</code></p> <p><code>/apps/settings/wcm/designs/default</code></p> </td>
  </tr>
  <tr>
   <td><strong>Orientamenti per la ristrutturazione</strong></td>
   <td><p>Per qualsiasi progettazione gestita in SCM e non scritta in fase di esecuzione tramite le finestre di dialogo Progettazione.</p>
    <ol>
     <li>Copiate le progettazioni dalla posizione precedente alla nuova posizione (/app).</li>
     <li>Convertite eventuali risorse CSS, JavaScript e statiche nella struttura in una libreria <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank"></a> client con <code>allowProxy = true</code>.</li>
     <li>Aggiorna i riferimenti alla posizione precedente in <code>
       cq
      </code>:
       <code>
       designPath
      </code> property.</li>
     <li>Aggiorna tutte le pagine che fanno riferimento al percorso precedente per utilizzare la nuova categoria Libreria client (per questo è necessario aggiornare il codice di implementazione Pagina).</li>
     <li>Aggiorna le regole del dispatcher AEM per consentire la trasmissione delle librerie client tramite /etc.clientlibs/. servlet proxy.</li>
    </ol> <p>Per tutte le progettazioni NON gestite in SCM e modificate runtime tramite le finestre di dialogo Progettazione.</p>
    <ul>
     <li>Non spostate Designer dall' <code>/etc</code>esterno.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td>N/D</td>
  </tr>
 </tbody>
</table>

### Endpoint JavaScript di Adobe DTM {#adobe-dtm-javascript-endpoint}

<table>
 <tbody>
  <tr>
   <td><strong>Posizione precedente</strong></td>
   <td><code>/etc/clientlibs/dtm</code></td>
  </tr>
  <tr>
   <td><strong>Nuove posizioni</strong></td>
   <td><code>/var/cq/dtm/clientlibs</code></td>
  </tr>
  <tr>
   <td><strong>Orientamenti per la ristrutturazione</strong></td>
   <td><p>Nessuna azione richiesta.</p> <p>La posizione pubblica precedente funge da endpoint proxy per la nuova posizione privata.</p> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td>N/D</td>
  </tr>
 </tbody>
</table>

### Endpoint web-snap Adobe DTM {#adobe-dtm-web-hook-endpoint}

<table>
 <tbody>
  <tr>
   <td><strong>Posizione precedente</strong></td>
   <td><code>/etc/dtm-hook</code></td>
  </tr>
  <tr>
   <td><strong>Nuove posizioni</strong></td>
   <td><code>/var/cq/dtm/web-hook</code></td>
  </tr>
  <tr>
   <td><strong>Orientamenti per la ristrutturazione</strong></td>
   <td><p>Nessuna azione richiesta.</p> <p>La posizione pubblica precedente funge da endpoint proxy per la nuova posizione privata.</p> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td>N/D</td>
  </tr>
 </tbody>
</table>

### Attività Inbox {#inbox-tasks}

<table>
 <tbody>
  <tr>
   <td><strong>Posizione precedente</strong></td>
   <td><code>/etc/taskmanagement</code></td>
  </tr>
  <tr>
   <td><strong>Nuove posizioni</strong></td>
   <td><code>/var/taskmanagement</code></td>
  </tr>
  <tr>
   <td><strong>Orientamenti per la ristrutturazione</strong></td>
   <td>Utilizzare l'attività <strong>di manutenzione rimozione</strong> inbox per rimuovere le attività precedenti dalla posizione precedente, come necessario.</td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td><p>Non è richiesta alcuna azione per la migrazione delle attività nella nuova posizione.</p>
    <ul>
     <li>Le attività presenti nella Posizione precedente continuano a essere disponibili e funzionanti.</li>
     <li>Nella nuova posizione vengono create nuove attività.</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### Configurazioni Blueprint Manager multisito {#multi-site-manager-blueprint-configurations}

<table>
 <tbody>
  <tr>
   <td><strong><em></em>Posizione precedente</strong></td>
   <td><code>/etc/blueprints</code></td>
  </tr>
  <tr>
   <td><strong>Nuove posizioni</strong></td>
   <td><p><code>/libs/msm</code></p> <p><code>/apps/msm</code></p> </td>
  </tr>
  <tr>
   <td><strong>Orientamenti per la ristrutturazione</strong></td>
   <td>
    <ol>
     <li>Copia configurazioni personalizzate da <code>/etc/blueprints</code> a <code>/apps/msm</code>.</li>
     <li>Rimuovi <code>/etc/blueprints</code>.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td>N/D</td>
  </tr>
 </tbody>
</table>

### Configurazioni del gadget per il dashboard di AEM Projects {#aem-projects-dashboard-gadget-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>Posizione precedente</strong></td>
   <td><code>/etc/projects/dashboard/gadgets</code></td>
  </tr>
  <tr>
   <td><strong>Nuove posizioni</strong></td>
   <td><p><code>/libs/cq/core/content/projects/dashboard/gadgets</code></p> <p><code>/apps/cq/core/content/projects/dashboard/gadgets</code></p> </td>
  </tr>
  <tr>
   <td><strong>Orientamenti per la ristrutturazione</strong></td>
   <td><p>Qualsiasi configurazione del gadget del dashboard di progetti AEM nuova o modificata deve essere migrata nella nuova posizione (<code>/apps</code>).</p>
    <ol>
     <li>Copiate le configurazioni di gadget per dashboard di AEM Projects nuove o modificate dalla posizione precedente alla nuova posizione (<code>/apps</code>).
      <ol>
       <li>Non copiate le configurazioni del gadget del dashboard di AEM Projects, che ora sono già presenti nella nuova posizione (<code>/libs</code>).</li>
      </ol> </li>
     <li>Aggiornate i modelli di progetti AEM che fanno riferimento alla posizione precedente in modo che puntino alla nuova posizione appropriata.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td>Se viene applicato il pacchetto di compatibilità AEM 6.4, sarà necessario eseguire le attività di allineamento dell'archivio al momento della rimozione del pacchetto di compatibilità.</td>
  </tr>
 </tbody>
</table>

### Modello e-mail notifica replica {#replication-notification-e-mail-template}

<table>
 <tbody>
  <tr>
   <td><strong>Posizione precedente</strong></td>
   <td><code>/etc/notification/email/default/com.day.cq.replication</code></td>
  </tr>
  <tr>
   <td><strong>Nuove posizioni</strong></td>
   <td><p><code>/libs/settings/notification-templates/com.day.cq.replication</code></p> <p><code>/apps/settings/notification-templates/com.day.cq.replication</code></p> </td>
  </tr>
  <tr>
   <td><strong>Orientamenti per la ristrutturazione</strong></td>
   <td><p>Eventuali modelli e-mail di notifica della replica nuovi o modificati devono essere migrati nella nuova posizione (<code>/apps</code>)</p>
    <ol>
     <li>Copiate i modelli e-mail di notifica della replica nuovi o modificati dal percorso precedente alla nuova posizione (<code>/apps</code>).</li>
     <li>Rimuovete eventuali modelli e-mail di notifica della replica migrati dal percorso precedente.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td><p>I soli nuovi modelli e-mail di notifica della replica supportati sono quelli che supportano le nuove impostazioni internazionali.</p> <p>La risoluzione del modello e-mail di notifica della replica si verifica nel seguente ordine:</p>
    <ol>
     <li><code>/etc/notification/email/default/com.day.cq.replication</code></li>
     <li><code class="code">/apps/settings/notification-templates/com.day.cq.replication
        </code></li>
     <li><code>/libs/settings/notification-templates/com.day.cq.replication</code></li>
    </ol> </td>
  </tr>
 </tbody>
</table>

### Tag {#tags}

<table>
 <tbody>
  <tr>
   <td><strong>Posizione precedente</strong></td>
   <td><code>/etc/tags</code></td>
  </tr>
  <tr>
   <td><strong>Nuove posizioni</strong></td>
   <td><code>/content/cq:tags</code></td>
  </tr>
  <tr>
   <td><strong>Orientamenti per la ristrutturazione</strong></td>
   <td><p>Tutti i tag devono essere migrati in <code>/content/cq:tags</code>.</p>
    <ol>
     <li>Copiate tutti i tag dalla posizione precedente alla nuova posizione.</li>
     <li>Rimuovere tutti i tag dalla posizione precedente.</li>
     <li>Tramite la console Web AEM, riavviate il bundle Day Communique 5 Tagging OSGi all’indirizzo <em>https://serveraddress:serverport/system/console/bundles/com.day.cq.cq-tagging</em> for AEM per riconoscere che la nuova posizione contiene contenuto e deve essere utilizzata.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td><p>Riavviare il bundle Day Communique Tagging OSGi registrerà la nuova posizione come radice del tag solo se la posizione precedente è vuota.</p> <p>I riferimenti alla posizione precedente continueranno a funzionare dopo la migrazione alla nuova posizione per tutte le funzionalità che sfruttano l’API TagManager di AEM per la risoluzione dei tag.</p> <p>Eventuali codici personalizzati che fanno riferimento in modo esplicito al percorso <code>/etc/tags</code> devono essere aggiornati a <span class="code">/content/ <code>
       cq
      </code><code>
       :tags
      </code></span>, o eventualmente riscritti per sfruttare l'API Java TagManager, insieme a questa migrazione.</p> </td>
  </tr>
 </tbody>
</table>

### Servizi cloud di traduzione {#translation-cloud-services}

<table>
 <tbody>
  <tr>
   <td><strong>Posizione precedente</strong></td>
   <td><code>/etc/cloudservices/translation</code></td>
  </tr>
  <tr>
   <td><strong>Nuove posizioni</strong></td>
   <td><p><code>/libs/settings/cloudconfigs/translation/translationcfg</code></p> <p><code>/apps/settings/cloudconfigs/translation/translationcfg</code></p> <p><code>/conf/global/settings/cloudconfigs/translation/translationcfg</code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/translation/translationcfg</code></p> </td>
  </tr>
  <tr>
   <td><strong>Orientamenti per la ristrutturazione</strong></td>
   <td><p>Eventuali nuovi servizi di Translation Cloud devono essere migrati nella nuova posizione (<code>/apps</code>, <code>/conf/global</code> o <code>/conf/&lt;tenant&gt;</code>).</p>
    <ol>
     <li>Migra le configurazioni esistenti nella posizione precedente alla nuova posizione.
      <ul>
       <li>Create manualmente nuove configurazioni di Servizi cloud di traduzione tramite l’interfaccia utente di authoring di AEM in <strong>Strumenti &gt; Servizi cloud &gt; Servizi</strong>cloud di traduzione.<br /> OPPURE </li>
       <li>Copiate le nuove configurazioni di Servizi cloud di traduzione dalla posizione precedente alla nuova posizione (<code>/apps</code>, <code>/conf/global</code> o <code>/conf/&lt;tenant&gt;</code>).</li>
      </ul> </li>
     <li>Associate le configurazioni AEM applicabili alle gerarchie di contenuti di AEM.
      <ol>
       <li>Gerarchie di pagine di AEM Sites tramite <strong>AEM Sites &gt; Page Properties &gt; Advanced Tab &gt; Cloud Configuration</strong>(Siti AEM &gt; Siti AEM &gt; Pagina &gt; Proprietà pagina &gt; scheda Avanzate &gt; Cloud Configuration (Configurazione cloud).</li>
       <li>Gerarchie di frammenti esperienza AEM tramite frammenti esperienza <strong>AEM &gt; Frammento esperienza &gt; Proprietà &gt; scheda Servizi cloud &gt; Configurazione</strong>cloud.</li>
       <li>Gerarchie di cartelle di frammenti esperienza AEM tramite frammenti esperienza <strong>AEM &gt; Cartella &gt; Proprietà &gt; scheda Servizi cloud &gt; Configurazione</strong>cloud.<br /> </li>
       <li>Gerarchie di cartelle di Risorse AEM tramite Risorse <strong>AEM &gt; Cartella &gt; Proprietà cartella &gt; scheda Servizi cloud &gt; Configurazione</strong>.</li>
       <li>Progetti AEM tramite Progetti <strong>AEM &gt; Progetto &gt; Proprietà progetto &gt; scheda Avanzate &gt; Configurazione</strong>cloud.</li>
      </ol> </li>
     <li>Separa i servizi di Translation Cloud legacy migrati dalle gerarchie di contenuti di AEM sopra indicate.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td><p>La risoluzione dei servizi di traduzione cloud viene eseguita nel seguente ordine:</p>
    <ol>
     <li><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/translations/translationcfg</code></li>
     <li><code>/conf/global/settings/cloudconfigs/translations/translationcfg</code></li>
     <li><code>/apps/settings/cloudconfigs/translations/translationcfg</code></li>
     <li><code>/libs/settings/cloudconfigs/translations/translationcfg</code></li>
    </ol> <p>I servizi cloud di traduzione migrata devono essere compatibili con AEM 6.4.</p> </td>
  </tr>
 </tbody>
</table>

### Lingue di traduzione {#translation-languages}

<table>
 <tbody>
  <tr>
   <td><strong>Posizione precedente</strong></td>
   <td><code>/etc/translation/supportedLanguages</code></td>
  </tr>
  <tr>
   <td><strong>Nuove posizioni</strong></td>
   <td><p><code>/libs/settings/translation/supportedLanguages</code></p> <p><code>/apps/settings/translation/supportedLanguages</code></p> </td>
  </tr>
  <tr>
   <td><strong>Orientamenti per la ristrutturazione</strong></td>
   <td><p>Qualsiasi definizione nuova o modificata della lingua di traduzione richiede la migrazione di tutte le definizioni della lingua di traduzione nella nuova posizione (<code>/apps</code>).</p>
    <ol>
     <li>Se sono state apportate aggiunte o modifiche alle definizioni della lingua di traduzione, copiate tutte le definizioni della lingua di traduzione dalla posizione precedente alla nuova posizione (<code>/apps</code>).</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td><p>La risoluzione del percorso della lingua di traduzione si verifica nell'ordine seguente:</p>
    <ol>
     <li><code>/etc/translation/supportedLanguages</code></li>
     <li><code>/apps/settings/translation/supportedLanguage</code></li>
     <li><code>/libs/settings/translation/supportedLanguages</code></li>
    </ol> <p>Questa risoluzione non supporta l'unione di una sovrapposizione, il che significa che il percorso risolto deve contenere tutte le Lingue Supportate e non erediterà le Lingue Supportate dalle risoluzioni in ordine superiore.</p> </td>
  </tr>
 </tbody>
</table>

### Translation Rules {#translation-rules}

<table>
 <tbody>
  <tr>
   <td><strong>Posizione precedente</strong></td>
   <td><code>/etc/workflow/models/translation/translation_rules.xml</code></td>
  </tr>
  <tr>
   <td><strong>Nuove posizioni</strong></td>
   <td><p><code>/libs/settings/translation/rules/translation_rules.xml</code></p> <p><code>/apps/settings/translation/rules/translation_rules.xml</code></p> <p><code>/conf/global/settings/translation/rules/translation_rules.xml</code></p> </td>
  </tr>
  <tr>
   <td><strong>Orientamenti per la ristrutturazione</strong></td>
   <td><p>Un file XML modificato delle regole di conversione deve essere migrato nella nuova posizione (<code>/apps</code>, o <code>/conf/global</code>).</p> <p>1. Copiate il file XML delle regole di traduzione modificato dalla posizione precedente alla nuova posizione.</p> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td><p>La risoluzione XML delle regole di conversione replica si verifica nell'ordine seguente:</p>
    <ol>
     <li><code>/conf/global/settings/translation/rules/translation_rules.xml</code></li>
     <li><code class="code">/apps/settings/translation/rules/translation_rules.xml
        </code></li>
     <li><code class="code">/etc/workflow/models/translation/translation_rules.xml
        </code></li>
     <li><code>/libs/settings/translation/rules/translation_rules.xml</code></li>
    </ol> </td>
  </tr>
 </tbody>
</table>

### Libreria Client Widget di traduzione {#translation-widget-client-library}

<table>
 <tbody>
  <tr>
   <td><strong>Posizione precedente</strong></td>
   <td><code>/etc/designs/translation/translationwidget</code></td>
  </tr>
  <tr>
   <td><strong>Nuove posizioni</strong></td>
   <td><p><code>/libs/settings/wcm/designs/translation/translationwidget</code></p> <p><code>/apps/settings/wcm/designs/translation/translationwidget</code></p> </td>
  </tr>
  <tr>
   <td><strong>Orientamenti per la ristrutturazione</strong></td>
   <td><p>Per qualsiasi progettazione gestita in SCM e non scritta in fase di esecuzione tramite le finestre di dialogo Progettazione.</p>
    <ol>
     <li>Copiate le progettazioni dalla posizione precedente alla nuova posizione (/app).</li>
     <li>Convertite eventuali risorse CSS, JavaScript e statiche nella struttura in una libreria <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank"></a> client con <code>allowProxy = true</code>.</li>
     <li>Aggiorna i riferimenti alla posizione precedente in <code>
       cq
      </code>:
       <code>
       designPath
      </code> property.</li>
     <li>Aggiorna tutte le pagine che fanno riferimento al percorso precedente per utilizzare la nuova categoria Libreria client (per questo è necessario aggiornare il codice di implementazione Pagina).</li>
     <li>Aggiorna le regole del dispatcher AEM per consentire la trasmissione delle librerie client tramite /etc.clientlibs/. servlet proxy.</li>
    </ol> <p>Per tutte le progettazioni NON gestite in SCM e modificate runtime tramite le finestre di dialogo Progettazione.</p>
    <ul>
     <li>Non spostate Designer dall' <code>/etc</code>esterno.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td>N/D</td>
  </tr>
 </tbody>
</table>

### Console Web attivazione albero {#tree-activation-web-console}

| **Posizione precedente** | `/etc/replication/treeactivation` |
|---|---|
| **Nuove posizioni** | `/libs/replication/treeactivation` |
| **Orientamenti per la ristrutturazione** | Nessuna azione richiesta. |
| **Note** | La console Web Attivazione albero è ora disponibile tramite **Strumenti > Distribuzione > Replica > Attiva albero**. |

### Servizi cloud del connettore di traduzione fornitori {#vendor-translation-connector-cloud-services}

<table>
 <tbody>
  <tr>
   <td><strong>Posizione precedente</strong></td>
   <td><code>/etc/cloudservices/&lt;vendor&gt;</code></td>
  </tr>
  <tr>
   <td><strong>Nuove posizioni</strong></td>
   <td><p><code>/libs/settings/cloudconfigs/translation/&lt;vendor&gt;</code></p> <p><code class="code">/apps/settings/cloudconfigs/translation/&lt;vendor&gt;
       </code></p> <p><code class="code">/conf/global/settings/cloudconfigs/translation/&lt;vendor&gt;
       </code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/translation/&lt;vendor&gt;</code></p> </td>
  </tr>
  <tr>
   <td><strong>Orientamenti per la ristrutturazione</strong></td>
   <td><p>Eventuali nuovi servizi cloud del connettore di traduzione fornitore devono essere migrati nella nuova posizione (<code>/apps</code>, <code>/conf/global</code> o <code>/conf/&lt;tenant&gt;</code>).</p>
    <ol>
     <li>Migra le configurazioni esistenti nella posizione precedente alla nuova posizione.
      <ul>
       <li>Crea manualmente nuove configurazioni di Servizi cloud per il connettore di traduzione fornitori tramite l’interfaccia utente di authoring di <strong>AEM in Strumenti &gt; Servizi cloud &gt; Servizi</strong>di traduzione cloud.<br /> OPPURE </li>
       <li>Copia le nuove configurazioni del connettore di traduzione fornitore Servizi cloud dalla posizione precedente alla nuova posizione (<code>/apps</code>, <code>/conf/global </code>o <code>/conf/&lt;tenant&gt;</code>).</li>
      </ul> </li>
     <li>Associate le configurazioni AEM applicabili alle gerarchie di contenuti di AEM.
      <ol>
       <li>Gerarchie di pagine di AEM Sites tramite <strong>AEM Sites &gt; Page Properties &gt; Advanced Tab &gt; Cloud Configuration</strong>(Siti AEM &gt; Siti AEM &gt; Pagina &gt; Proprietà pagina &gt; scheda Avanzate &gt; Cloud Configuration (Configurazione cloud).</li>
       <li>Gerarchie di frammenti esperienza AEM tramite frammenti esperienza <strong>AEM &gt; Frammento esperienza &gt; Proprietà &gt; scheda Servizi cloud &gt; Configurazione</strong>cloud.</li>
       <li>Gerarchie di cartelle di frammenti esperienza AEM tramite frammenti esperienza <strong>AEM &gt; Cartella &gt; Proprietà &gt; scheda Servizi cloud &gt; Configurazione</strong>cloud.</li>
       <li>Gerarchie di cartelle di Risorse AEM tramite Risorse <strong>AEM &gt; Cartella &gt; Proprietà cartella &gt; scheda Servizi cloud &gt; Configurazione</strong>.</li>
       <li>Progetti AEM tramite Progetti <strong>AEM &gt; Progetto &gt; Proprietà progetto &gt; scheda Avanzate &gt; Configurazione</strong>cloud.</li>
      </ol> </li>
     <li>Separa i servizi di Translation Cloud legacy migrati dalle gerarchie di contenuti di AEM sopra indicate.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td><p>La risoluzione dei servizi di traduzione cloud viene eseguita nel seguente ordine:</p>
    <ol>
     <li><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/translations/&lt;vendor&gt;</code></li>
     <li><code>/conf/global/settings/cloudconfigs/translations/&lt;vendor&gt;</code></li>
     <li><code>/apps/settings/cloudconfigs/translations/&lt;vendor&gt;</code></li>
     <li><code>/libs/settings/cloudconfigs/translations/&lt;vendor&gt;</code></li>
    </ol> </td>
  </tr>
 </tbody>
</table>

### Modelli e-mail notifica flusso di lavoro {#workflow-notification-email-templates}

<table>
 <tbody>
  <tr>
   <td><strong>Posizione precedente</strong></td>
   <td><code>/etc/workflow/notification</code></td>
  </tr>
  <tr>
   <td><strong>Nuove posizioni</strong></td>
   <td><p><code>/libs/settings/workflow/notification</code></p> <p><code>/conf/global/settings/workflow/notification</code></p> </td>
  </tr>
  <tr>
   <td><strong>Orientamenti per la ristrutturazione</strong></td>
   <td><p>Eventuali modelli e-mail di notifica dei flussi di lavoro modificati devono essere migrati nella nuova posizione (<code>/conf/global</code>).</p>
    <ol>
     <li>Copiate i modelli e-mail di notifica dei flussi di lavoro modificati dalla posizione precedente alla nuova posizione.</li>
     <li>Rimuovi i modelli e-mail di notifica del flusso di lavoro migrati dalla posizione precedente.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td><p>La risoluzione del modello e-mail di notifica del flusso di lavoro si verifica nel seguente ordine:</p>
    <ol>
     <li><code>/etc/workflow/notification</code></li>
     <li><code>/conf/global/settings/workflow/notification</code></li>
     <li><code>/libs/settings/workflow/notification</code></li>
    </ol> </td>
  </tr>
 </tbody>
</table>

### Pacchetti di flussi di lavoro {#workflow-packages}

<table>
 <tbody>
  <tr>
   <td><strong>Posizione precedente</strong></td>
   <td><code>/etc/workflow/packages</code></td>
  </tr>
  <tr>
   <td><strong>Nuove posizioni</strong></td>
   <td><code>/var/workflow/packages</code></td>
  </tr>
  <tr>
   <td><strong>Orientamenti per la ristrutturazione</strong></td>
   <td><p>I pacchetti di flussi di lavoro esistenti nella posizione precedente devono essere migrati nella nuova posizione.</p>
    <ol>
     <li>Rimuovete tutti i pacchetti di flussi di lavoro nella posizione precedente a cui non viene fatto riferimento da altri contenuti e che altrimenti non sono richiesti.</li>
     <li>Sposta tutti i pacchetti di flussi di lavoro nella posizione precedente a cui non viene fatto riferimento da altri contenuti, ma che sono altrimenti richiesti nella nuova posizione.</li>
     <li>Lasciate eventuali pacchetti di flussi di lavoro a cui fanno riferimento altri contenuti nella posizione precedente.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td><p>I pacchetti di flussi di lavoro creati tramite la console Miscadmin dell’interfaccia classica vengono memorizzati nella posizione precedente, mentre tutti gli altri vengono memorizzati nella nuova posizione.</p> <p>I pacchetti di workflow memorizzati nelle posizioni precedenti o iniziali possono essere gestiti tramite la console di amministrazione dell’interfaccia classica.</p> </td>
  </tr>
 </tbody>
</table>

