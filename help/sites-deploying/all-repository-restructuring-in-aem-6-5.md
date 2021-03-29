---
title: Ristrutturazione dell’archivio comune in AEM 6.5
seo-title: Ristrutturazione dell’archivio comune in AEM 6.5
description: Scopri come apportare le modifiche necessarie per migrare alla nuova struttura dell’archivio in AEM 6.5 comune per tutte le aree di AEM.
seo-description: Scopri come apportare le modifiche necessarie per migrare alla nuova struttura dell’archivio in AEM 6.5 comune per tutte le aree di AEM.
uuid: a4bb64e5-387b-4084-9258-54e68db12f3b
contentOwner: chaikels
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
discoiquuid: 80bd707f-c02d-4616-9b45-90f6c726abea
translation-type: tm+mt
source-git-commit: 8d6818d0f2d90482f930f8e98682670ed6d0dd28
workflow-type: tm+mt
source-wordcount: '2724'
ht-degree: 2%

---


# Ristrutturazione dell&#39;archivio comune in AEM 6.5 {#common-repository-restructuring-in-aem}

Come descritto nella pagina padre [Ristrutturazione archivio in AEM 6.5](/help/sites-deploying/repository-restructuring.md), i clienti che eseguono l&#39;aggiornamento a AEM 6.5 devono utilizzare questa pagina per valutare lo sforzo di lavoro associato alle modifiche dell&#39;archivio che possono avere un impatto su tutte le soluzioni. Alcune modifiche richiedono un lavoro durante il processo di aggiornamento di AEM 6.5, mentre altre possono essere differite fino a un aggiornamento futuro.

**Con aggiornamento alla versione 6.5**

* [Configurazioni ContextHub](#contexthub-6.5)
* [Istanze flusso di lavoro](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#workflow-instances)
* [Modelli flusso di lavoro](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#workflow-models)
* [Moduli di avvio per flusso di lavoro](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#workflow-launchers)
* [Script di flusso di lavoro](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#workflow-scripts)

**Prima dell’aggiornamento futuro**

* [Configurazioni ContextHub](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#contexthub-configurations)
* [Progettazione Cloud Services classici](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#classic-cloud-services-designs)
* [Progettazione di dashboard classici](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#classic-dashboards-designs)
* [Progettazione report classici](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#classic-reports-designs)
* [Progettazioni predefinite](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#default-designs)
* [Endpoint JavaScript di Adobe DTM](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#adobe-dtm-javascript-endpoint)
* [Endpoint Web-Hook DTM Adobe](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#adobe-dtm-web-hook-endpoint)
* [Casella in entrata - Attività](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#inbox-tasks)
* [Configurazioni blueprint di Multi-Site Manager](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#multi-site-manager-blueprint-configurations)
* [Configurazioni del gadget per dashboard di progetti AEM](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#aem-projects-dashboard-gadget-configurations)
* [Modello e-mail di notifica di replica](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#replication-notification-e-mail-template)
* [Tag](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#tags)
* [Servizi cloud di traduzione](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#translation-cloud-services)
* [Lingue di traduzione](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#translation-languages)
* [Regole di traduzione](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#translation-rules)
* [Libreria client per i Widget di traduzione](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#translation-widget-client-library)
* [Console Web di attivazione della struttura](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#tree-activation-web-console)
* [Cloud Services connettore di traduzione fornitore](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#vendor-translation-connector-cloud-services)
* [Modelli e-mail per notifiche flusso di lavoro](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#workflow-notification-email-templates)

## Aggiornamento 6.5 {#with-upgrade}

### Configurazioni ContextHub {#contexthub-6.5}

A partire da AEM 6.4, non esiste una configurazione ContextHub predefinita. Pertanto, a livello principale del sito è necessario impostare `cq:contextHubPathproperty` per indicare quale configurazione deve essere utilizzata.

1. Passa alla directory principale del sito.
1. Apri le proprietà della pagina principale e seleziona la scheda Personalizzazione .
1. Nel campo Percorso contexthub inserisci il percorso di configurazione ContextHub.

Inoltre, nella configurazione ContextHub, il `sling:resourceType` deve essere aggiornato per essere relativo e non assoluto.

1. Apri le proprietà del nodo di configurazione ContextHub in CRX DE Lite, ad esempio `/apps/settings/cloudsettings/legacy/contexthub`
1. Cambia `sling:resourceType` da `/libs/granite/contexthub/cloudsettings/components/baseconfiguration` a `granite/contexthub/cloudsettings/components/baseconfiguration`

Ad esempio, la `sling:resourceType` della configurazione ContextHub deve essere relativa anziché assoluta.

### Modelli flusso di lavoro {#workflow-models}

<table style="table-layout:auto">
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
   <td><strong>Orientamento alla ristrutturazione</strong></td>
   <td><p>Eventuali modelli di flussi di lavoro nuovi o modificati devono essere migrati a /conf/global/workflow/models.</p>
    <ol>
     <li>Distribuisci i modelli di flusso di lavoro modificati in un'istanza di sviluppo AEM 6.5 locale, in modo che siano presenti nel percorso precedente.</li>
     <li>Modifica il modello di flusso di lavoro utilizzando AEM Workflow Model Editor in AEM &gt; Strumenti &gt; Flusso di lavoro &gt; Modelli.</li>
     <li>Durante la migrazione dei modelli di flusso di lavoro modificati forniti da AEM
      <ol>
       <li>Con l'Editor modello flusso di lavoro aperto, modifica l'URL dell'indirizzo del browser e sostituisci il segmento del percorso /libs/settings/workflow/models con /etc/workflow/models.
        <ul>
         <li>Ad esempio, modifica: <em>http://localhost:4502/editor.html<strong>/libs/settings/workflow/models</strong>/dam/update_asset.html</em> a <em>http://localhost:4502/editor.html<strong>/etc/workflow/models</strong>/dam/update_asset.html</em></li>
        </ul> </li>
      </ol> </li>
     <li>Attiva la modalità Modifica nell'Editor modello flusso di lavoro che copierà la definizione del modello di flusso di lavoro in /conf/global/workflow/models.</li>
     <li>Tocca il pulsante Sincronizza per sincronizzare le modifiche al modello del flusso di lavoro runtime in /var/workflow/models.</li>
     <li>Esporta sia il modello di flusso di lavoro (/conf/global/workflow/models/&lt;workflow-model&gt;) che il modello di flusso di lavoro runtime (/var/workflow/models/&lt;workflow-model&gt;) e integralo nel progetto AEM.
      <ol>
       <li>Ad esempio, esporta:
        <ul>
         <li><code>/config/settings/workflow/models/dam/my_workflow_model</code> e </li>
         <li><code>/var/workflow/models/dam/my_workflow_model</code></li>
        </ul> </li>
      </ol> </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td><p>La risoluzione del modello di flusso di lavoro si verifica nel seguente ordine:</p>
    <ol>
     <li><code>/conf/global/settings/workflow/models</code></li>
     <li><code>/libs/settings/workflow/models</code></li>
     <li><code>/etc/workflow/models</code></li>
    </ol> <p>Pertanto, tutte le personalizzazioni dei modelli di flusso di lavoro forniti da AEM che persistono nella posizione precedente devono essere spostate in /conf/global/settings/workflow/models se devono essere mantenute, altrimenti saranno sostituite dalla definizione del modello di flusso di lavoro fornito da AEM in /libs/settings/workflow/models.</p> </td>
  </tr>
 </tbody>
</table>

### Istanze flusso di lavoro {#workflow-instances}

<table style="table-layout:auto">
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
   <td><strong>Orientamento alla ristrutturazione</strong></td>
   <td><p>Per allineare la nuova posizione non è necessaria alcuna azione.</p> <p>Le istanze del flusso di lavoro storiche possono continuare a risiedere nella posizione precedente in modo sicuro e le nuove istanze del flusso di lavoro verranno create nella nuova posizione.</p> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td>Qualsiasi riferimento esplicito a un percorso in
    Anche il codice <code>
     custom
    </code> della posizione precedente deve tenere conto della nuova posizione. Si consiglia di eseguire il refactoring di questo codice per utilizzare le API del flusso di lavoro AEM.</td>
  </tr>
 </tbody>
</table>

### Moduli di avvio per flusso di lavoro {#workflow-launchers}

<table style="table-layout:auto">
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
   <td><strong>Orientamento alla ristrutturazione</strong></td>
   <td><p>Eventuali moduli di avvio dei flussi di lavoro nuovi o modificati devono essere migrati a <code>/conf/global/workflow/launcher/config</code>.</p>
    <ol>
     <li>Copia le configurazioni nuove o modificate di Workflow Launcher dalla posizione precedente alla nuova posizione (<code>/conf/global</code>).</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td><p>La risoluzione di Workflow Launcher si verifica nel seguente ordine:</p>
    <ol>
     <li><code>/conf/global/settings/workflow/launcher</code></li>
     <li><code>/libs/settings/workflow/launcher</code></li>
     <li><code>/etc/workflow/launcher</code></li>
    </ol> <p>Pertanto, tutte le personalizzazioni di Workflow Launcher AEM fornite persistono nella posizione precedente devono essere spostate nella nuova posizione (<code>/conf/global/settings/workflow/launcher</code>) se devono essere mantenute, altrimenti saranno sostituite dalla definizione di Workflow Launcher AEM fornita in <code>/libs/settings/workflow/launcher</code>.</p> </td>
  </tr>
 </tbody>
</table>

### Script di flusso di lavoro {#workflow-scripts}

<table style="table-layout:auto">
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
   <td><strong>Orientamento alla ristrutturazione</strong></td>
   <td><p>Eventuali script di flusso di lavoro nuovi o modificati devono essere migrati nella nuova posizione e i modelli di flusso di lavoro di riferimento aggiornati per riflettere la nuova posizione.</p>
    <ol>
     <li>Copia gli script di flusso di lavoro nuovi o modificati dalla posizione precedente alla nuova posizione.<br />
      <ul>
       <li><code>/apps/workflow/scripts</code> devono essere mantenuti in SCM.</li>
      </ul> </li>
     <li>Aggiorna tutti i riferimenti agli script del flusso di lavoro nella posizione precedente nei modelli di flusso di lavoro per puntare alle nuove posizioni.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td><p>AEM 6.4 SP1, quando viene rilasciato, lo rende in modo che questa ristrutturazione possa essere differita fino alla versione 6.5
     <code>
      upgrade
     </code>.</p> <p>Se si esegue l’aggiornamento a AEM 6.4 prima del rilascio di AEM 6.4 SP1, questa ristrutturazione deve essere eseguita come parte del progetto di aggiornamento. Senza farlo, la modifica e il salvataggio dei passaggi del flusso di lavoro che fanno riferimento agli script nella posizione precedente rimuoverà completamente il riferimento allo script del flusso di lavoro dal passaggio del flusso di lavoro, e solo gli script del flusso di lavoro in nuove posizioni saranno disponibili nel menu a discesa di selezione dello script.</p> </td>
  </tr>
 </tbody>
</table>

## Aggiornamento precedente a {#prior-to-upgrade}

### Configurazioni ContextHub {#contexthub-configurations}

<table style="table-layout:auto">
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
   <td><strong>Orientamento alla ristrutturazione</strong></td>
   <td><p>Eventuali configurazioni ContextHub nuove o modificate devono essere migrate nella nuova posizione e le pagine AEM Sites di riferimento devono essere aggiornate per riflettere la nuova posizione.</p>
    <ol>
     <li>Copia le configurazioni ContextHub nuove o modificate dalla posizione precedente alla nuova posizione.</li>
     <li>Associa le configurazioni di AEM applicabili alle gerarchie di contenuto AEM.
      <ol>
       <li><strong>Gerarchie di pagine AEM Sites tramite AEM Sites &gt; Pagina &gt; Proprietà pagina &gt; Scheda Avanzate &gt; Configurazione</strong> cloud.</li>
      </ol> </li>
     <li>Disassociare le configurazioni ContextHub legacy migrate dalle gerarchie di contenuto AEM sopra indicate.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td>N/D</td>
  </tr>
 </tbody>
</table>

### Progettazioni di Cloud Services classici {#classic-cloud-services-designs}

<table style="table-layout:auto">
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
   <td><strong>Orientamento alla ristrutturazione</strong></td>
   <td><p>Per tutte le progettazioni gestite in SCM e non scritte in fase di esecuzione tramite le finestre di dialogo di progettazione.</p>
    <ol>
     <li>Copia le progettazioni dalla posizione precedente alla nuova posizione (<code>/apps</code>).</li>
     <li>Converti qualsiasi risorsa CSS, JavaScript e statica nella progettazione in una <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">libreria client</a> con <code>allowProxy = true</code>.</li>
     <li>Aggiorna i riferimenti alla posizione precedente in <span class="code">
       <code>
        cq
       </code>:
       Proprietà <code>
        designPath
       </code></span> .</li>
     <li>Aggiorna le pagine che fanno riferimento alla posizione precedente per utilizzare la nuova categoria Libreria client (è necessario aggiornare il codice di implementazione della pagina).</li>
     <li>Aggiorna AEM regole del Dispatcher per consentire il servizio delle librerie client tramite /etc.clientlibs/.. servlet proxy.</li>
    </ol> <p>Per tutte le progettazioni NON gestite in SCM e modificate in fase di esecuzione tramite le finestre di dialogo di progettazione.</p>
    <ul>
     <li>Non spostare progettazioni modificabili dall’autore fuori da <code>/etc</code>.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td>N/D</td>
  </tr>
 </tbody>
</table>

### Progettazioni di dashboard classiche {#classic-dashboards-designs}

<table style="table-layout:auto">
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
   <td><strong>Orientamento alla ristrutturazione</strong></td>
   <td><p>Per tutte le progettazioni gestite in SCM e non scritte in fase di esecuzione tramite le finestre di dialogo di progettazione.</p>
    <ol>
     <li>Copia le progettazioni dalla posizione precedente alla nuova posizione (/apps).</li>
     <li>Converti qualsiasi risorsa CSS, JavaScript e statica nella progettazione in una <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">libreria client</a> con <code>allowProxy = true</code>.</li>
     <li>Aggiorna i riferimenti alla posizione precedente nel
      <code>
       cq
      </code>:
      Proprietà <code>
       designPath
      </code> .</li>
     <li>Aggiorna le pagine che fanno riferimento alla posizione precedente per utilizzare la nuova categoria Libreria client (è necessario aggiornare il codice di implementazione della pagina).</li>
     <li>Aggiorna AEM regole del Dispatcher per consentire il servizio delle librerie client tramite /etc.clientlibs/.. servlet proxy.</li>
    </ol> <p>Per tutte le progettazioni NON gestite in SCM e modificate in fase di esecuzione tramite le finestre di dialogo di progettazione.</p>
    <ul>
     <li>Non spostare progettazioni modificabili dall’autore fuori da <code>/etc</code>.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td>N/D</td>
  </tr>
 </tbody>
</table>

### Progettazione report classici {#classic-reports-designs}

<table style="table-layout:auto">
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
   <td><strong>Orientamento alla ristrutturazione</strong></td>
   <td><p>Per tutte le progettazioni gestite in SCM e non scritte in fase di esecuzione tramite le finestre di dialogo di progettazione.</p>
    <ol>
     <li>Copia le progettazioni dalla posizione precedente alla nuova posizione (/apps).</li>
     <li>Converti qualsiasi risorsa CSS, JavaScript e statica nella progettazione in una <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">libreria client</a> con <code>allowProxy = true</code>.</li>
     <li>Aggiorna i riferimenti alla posizione precedente nel
      <code>
       cq
      </code>:
      Proprietà <code>
       designPath
      </code> .</li>
     <li>Aggiorna le pagine che fanno riferimento alla posizione precedente per utilizzare la nuova categoria Libreria client (è necessario aggiornare il codice di implementazione della pagina).</li>
     <li>Aggiorna AEM regole del Dispatcher per consentire il servizio delle librerie client tramite /etc.clientlibs/.. servlet proxy.</li>
    </ol> <p>Per tutte le progettazioni NON gestite in SCM e modificate in fase di esecuzione tramite le finestre di dialogo di progettazione.</p>
    <ul>
     <li>Non spostare progettazioni modificabili dall’autore fuori da <code>/etc</code>.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td>N/D</td>
  </tr>
 </tbody>
</table>

### Progettazioni predefinite {#default-designs}

<table style="table-layout:auto">
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
   <td><strong>Orientamento alla ristrutturazione</strong></td>
   <td><p>Per tutte le progettazioni gestite in SCM e non scritte in fase di esecuzione tramite le finestre di dialogo di progettazione.</p>
    <ol>
     <li>Copia le progettazioni dalla posizione precedente alla nuova posizione (/apps).</li>
     <li>Converti qualsiasi risorsa CSS, JavaScript e statica nella progettazione in una <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">libreria client</a> con <code>allowProxy = true</code>.</li>
     <li>Aggiorna i riferimenti alla posizione precedente nel
      <code>
       cq
      </code>:
      Proprietà <code>
       designPath
      </code> .</li>
     <li>Aggiorna le pagine che fanno riferimento alla posizione precedente per utilizzare la nuova categoria Libreria client (è necessario aggiornare il codice di implementazione della pagina).</li>
     <li>Aggiorna AEM regole del Dispatcher per consentire il servizio delle librerie client tramite /etc.clientlibs/.. servlet proxy.</li>
    </ol> <p>Per tutte le progettazioni NON gestite in SCM e modificate in fase di esecuzione tramite le finestre di dialogo di progettazione.</p>
    <ul>
     <li>Non spostare progettazioni modificabili dall’autore fuori da <code>/etc</code>.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td>N/D</td>
  </tr>
 </tbody>
</table>

### Endpoint JavaScript DTM Adobe {#adobe-dtm-javascript-endpoint}

<table style="table-layout:auto">
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
   <td><strong>Orientamento alla ristrutturazione</strong></td>
   <td><p>Non è richiesta alcuna azione.</p> <p>La posizione precedente pubblica funge da endpoint proxy per la nuova posizione privata.</p> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td>N/D</td>
  </tr>
 </tbody>
</table>

### Endpoint Web-Hook DTM Adobe {#adobe-dtm-web-hook-endpoint}

<table style="table-layout:auto">
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
   <td><strong>Orientamento alla ristrutturazione</strong></td>
   <td><p>Non è richiesta alcuna azione.</p> <p>La posizione precedente pubblica funge da endpoint proxy per la nuova posizione privata.</p> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td>N/D</td>
  </tr>
 </tbody>
</table>

### Casella in entrata Attività {#inbox-tasks}

<table style="table-layout:auto">
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
   <td><strong>Orientamento alla ristrutturazione</strong></td>
   <td>Utilizzare l' <strong>Casella in entrata Elimina attività di manutenzione</strong> per rimuovere le attività precedenti dalla posizione precedente, in base alle esigenze.</td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td><p>Non è necessaria alcuna azione per la migrazione delle attività nella nuova posizione.</p>
    <ul>
     <li>Le attività presenti nella posizione precedente continuano a essere disponibili e funzionano.</li>
     <li>Le nuove attività vengono create nella nuova posizione.</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### Configurazioni blueprint di Multi-Site Manager {#multi-site-manager-blueprint-configurations}

<table style="table-layout:auto">
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
   <td><strong>Orientamento alla ristrutturazione</strong></td>
   <td>
    <ol>
     <li>Copia le configurazioni personalizzate da <code>/etc/blueprints</code> a <code>/apps/msm</code>.</li>
     <li>Rimuovi <code>/etc/blueprints</code>.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td>N/D</td>
  </tr>
 </tbody>
</table>

### Configurazioni del gadget per dashboard di progetti AEM {#aem-projects-dashboard-gadget-configurations}

<table style="table-layout:auto">
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
   <td><strong>Orientamento alla ristrutturazione</strong></td>
   <td><p>Tutte le configurazioni del Gadget dashboard di progetti nuovi o modificati devono essere migrate nella nuova posizione (<code>/apps</code>).</p>
    <ol>
     <li>Copia le configurazioni del Gadget dashboard di progetti nuovi o modificati dalla posizione precedente alla nuova posizione (<code>/apps</code>).
      <ol>
       <li>Non copiare le configurazioni del Gadget dashboard di progetti AEM non modificati, poiché ora esistono nella nuova posizione (<code>/libs</code>).</li>
      </ol> </li>
     <li>Aggiorna i modelli di progetti AEM che fanno riferimento alla posizione precedente per puntare alla nuova posizione appropriata.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td>Se viene applicato il pacchetto di compatibilità AEM 6.4, sarà necessario eseguire le attività di allineamento dell’archivio al momento della rimozione del pacchetto di compatibilità.</td>
  </tr>
 </tbody>
</table>

### Modello e-mail di notifica di replica {#replication-notification-e-mail-template}

<table style="table-layout:auto">
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
   <td><strong>Orientamento alla ristrutturazione</strong></td>
   <td><p>Eventuali modelli e-mail di notifica di replica nuovi o modificati devono essere migrati nella nuova posizione (<code>/apps</code>)</p>
    <ol>
     <li>Copiare i modelli di posta elettronica per le notifiche di replica nuovi o modificati dal percorso precedente in un nuovo percorso (<code>/apps</code>).</li>
     <li>Rimuovere i modelli e-mail di notifica di replica migrati dal percorso precedente.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td><p>Gli unici modelli di posta elettronica supportati per le notifiche di replica sono quelli per supportare nuove impostazioni internazionali.</p> <p>La risoluzione del modello di posta elettronica per le notifiche di replica si verifica nel seguente ordine:</p>
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

<table style="table-layout:auto">
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
   <td><strong>Orientamento alla ristrutturazione</strong></td>
   <td><p>Tutti i tag devono essere migrati a <code>/content/cq:tags</code>.</p>
    <ol>
     <li>Copia tutti i tag dalla posizione precedente alla nuova posizione.</li>
     <li>Rimuovi tutti i tag dalla posizione precedente.</li>
     <li>Tramite la Console Web AEM, riavvia il bundle OSGi Day Communique 5 Tagging su <em>https://serveraddress:serverport/system/console/bundles/com.day.cq.cq-tagging</em> per AEM riconoscere che la Nuova posizione contiene contenuti e deve essere utilizzata.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td><p>Il riavvio del bundle Day Communique Tagging OSGi registrerà la nuova posizione come radice dei tag solo se la posizione precedente è vuota.</p> <p>I riferimenti alla posizione precedente continueranno a funzionare dopo la migrazione a nuova posizione per tutte le funzionalità che sfruttano AEM’API TagManager per la risoluzione dei tag.</p> <p>Qualsiasi codice personalizzato che faccia riferimento esplicitamente al percorso <code>/etc/tags</code> deve essere aggiornato a <span class="code">/content/
      <code>
       cq
      </code>
      <code>
       :tags
      </code></span>, o preferibilmente riscritto per sfruttare l’API Java TagManager, in parallelo con questa migrazione.</p> </td>
  </tr>
 </tbody>
</table>

### Servizi cloud di traduzione {#translation-cloud-services}

<table style="table-layout:auto">
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
   <td><strong>Orientamento alla ristrutturazione</strong></td>
   <td><p>Eventuali nuovi Cloud Services di traduzione devono essere migrati nella nuova posizione (<code>/apps</code>, <code>/conf/global</code> o <code>/conf/&lt;tenant&gt;</code>).</p>
    <ol>
     <li>Esegui la migrazione delle configurazioni esistenti nella posizione precedente alla nuova posizione.
      <ul>
       <li>Ricrea manualmente nuove configurazioni di Cloud Services di traduzione tramite l’interfaccia utente di authoring AEM in <strong>Strumenti &gt; Cloud Services &gt; Cloud Services di traduzione</strong>.<br /> OPPURE </li>
       <li>Copia le nuove configurazioni dei Cloud Services di traduzione dalla posizione precedente alla nuova posizione (<code>/apps</code>, <code>/conf/global</code> o <code>/conf/&lt;tenant&gt;</code>).</li>
      </ul> </li>
     <li>Associa le configurazioni di AEM applicabili alle gerarchie di contenuto AEM.
      <ol>
       <li>Gerarchie di pagine AEM Sites tramite <strong>AEM Sites &gt; Pagina &gt; Proprietà pagina &gt; Scheda avanzata &gt; Configurazione cloud</strong>.</li>
       <li>AEM gerarchie di frammenti esperienza tramite <strong>AEM Frammenti esperienza &gt; Frammento esperienza &gt; Proprietà &gt; Scheda Cloud Services &gt; Configurazione cloud</strong>.</li>
       <li>AEM gerarchie di cartelle di frammenti esperienza tramite <strong>AEM Frammenti esperienza &gt; Cartella &gt; Proprietà &gt; Scheda Cloud Services &gt; Configurazione cloud</strong>.<br /> </li>
       <li>Gerarchie di cartelle AEM Assets tramite <strong>AEM Assets &gt; Cartella &gt; Proprietà cartella &gt; Scheda Cloud Services &gt; Configurazione</strong>.</li>
       <li>AEM progetti tramite <strong>AEM Progetti &gt; Progetto &gt; Proprietà progetto &gt; Scheda Avanzate &gt; Configurazione cloud</strong>.</li>
      </ol> </li>
     <li>Separa i Cloud Services di traduzione legacy migrati dalle gerarchie di contenuto AEM sopra indicate.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td><p>La risoluzione dei Cloud Services di traduzione si verifica nel seguente ordine:</p>
    <ol>
     <li><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/translations/translationcfg</code></li>
     <li><code>/conf/global/settings/cloudconfigs/translations/translationcfg</code></li>
     <li><code>/apps/settings/cloudconfigs/translations/translationcfg</code></li>
     <li><code>/libs/settings/cloudconfigs/translations/translationcfg</code></li>
    </ol> <p>I Cloud Services di traduzione migrati devono essere compatibili con AEM 6.4.</p> </td>
  </tr>
 </tbody>
</table>

### Lingue di traduzione {#translation-languages}

<table style="table-layout:auto">
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
   <td><strong>Orientamento alla ristrutturazione</strong></td>
   <td><p>Qualsiasi definizione nuova o modificata di Lingua di traduzione richiede una migrazione di tutte le definizioni di Lingua di traduzione alla nuova posizione (<code>/apps</code>).</p>
    <ol>
     <li>Se sono state apportate aggiunte o modifiche alle definizioni delle lingue di traduzione, copia tutte le definizioni delle lingue di traduzione dalla posizione precedente nella nuova posizione (<code>/apps</code>).</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td><p>La risoluzione del percorso della lingua di traduzione si verifica nel seguente ordine:</p>
    <ol>
     <li><code>/etc/translation/supportedLanguages</code></li>
     <li><code>/apps/settings/translation/supportedLanguage</code></li>
     <li><code>/libs/settings/translation/supportedLanguages</code></li>
    </ol> <p>Questa risoluzione non supporta una sovrapposizione di unione, il che significa che il percorso risolto deve contenere tutte le lingue supportate e non erediterà le lingue supportate dalle risoluzioni di ordine superiore.</p> </td>
  </tr>
 </tbody>
</table>

### Regole di traduzione {#translation-rules}

<table style="table-layout:auto">
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
   <td><strong>Orientamento alla ristrutturazione</strong></td>
   <td><p>Un file XML delle regole di traduzione modificato deve essere migrato nella nuova posizione (<code>/apps</code> o <code>/conf/global</code>).</p> <p>1. Copia il file XML delle regole di traduzione modificato dalla posizione precedente alla nuova posizione.</p> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td><p>La risoluzione XML delle regole di traduzione della replica si verifica nel seguente ordine:</p>
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

### Libreria client per i widget di traduzione {#translation-widget-client-library}

<table style="table-layout:auto">
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
   <td><strong>Orientamento alla ristrutturazione</strong></td>
   <td><p>Per tutte le progettazioni gestite in SCM e non scritte in fase di esecuzione tramite le finestre di dialogo di progettazione.</p>
    <ol>
     <li>Copia le progettazioni dalla posizione precedente alla nuova posizione (/apps).</li>
     <li>Converti qualsiasi risorsa CSS, JavaScript e statica nella progettazione in una <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">libreria client</a> con <code>allowProxy = true</code>.</li>
     <li>Aggiorna i riferimenti alla posizione precedente nel
      <code>
       cq
      </code>:
      Proprietà <code>
       designPath
      </code> .</li>
     <li>Aggiorna le pagine che fanno riferimento alla posizione precedente per utilizzare la nuova categoria Libreria client (è necessario aggiornare il codice di implementazione della pagina).</li>
     <li>Aggiorna AEM regole del Dispatcher per consentire il servizio delle librerie client tramite /etc.clientlibs/.. servlet proxy.</li>
    </ol> <p>Per tutte le progettazioni NON gestite in SCM e modificate in fase di esecuzione tramite le finestre di dialogo di progettazione.</p>
    <ul>
     <li>Non spostare progettazioni modificabili dall’autore fuori da <code>/etc</code>.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td>N/D</td>
  </tr>
 </tbody>
</table>

### Console Web di attivazione albero {#tree-activation-web-console}

| **Posizione precedente** | `/etc/replication/treeactivation` |
|---|---|
| **Nuove posizioni** | `/libs/replication/treeactivation` |
| **Orientamento alla ristrutturazione** | Non è richiesta alcuna azione. |
| **Note** | La console Web Attivazione albero è ora disponibile tramite **Strumenti > Implementazione > Replica > Attiva albero**. |

{style=&quot;table-layout:auto&quot;}

### Cloud Services connettore traduzione fornitore {#vendor-translation-connector-cloud-services}

<table style="table-layout:auto">
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
   <td><strong>Orientamento alla ristrutturazione</strong></td>
   <td><p>Eventuali nuovi Cloud Services del connettore di traduzione fornitore devono essere migrati nella nuova posizione (<code>/apps</code>, <code>/conf/global</code> o <code>/conf/&lt;tenant&gt;</code>).</p>
    <ol>
     <li>Esegui la migrazione delle configurazioni esistenti nella posizione precedente alla nuova posizione.
      <ul>
       <li>Creare manualmente le configurazioni dei nuovi Cloud Services del connettore di traduzione fornitore tramite l' <strong>AEM interfaccia utente di authoring in Strumenti &gt; Cloud Services &gt; Cloud Services di traduzione</strong>.<br /> OPPURE </li>
       <li>Copia le nuove configurazioni dei Cloud Services del connettore di traduzione fornitore dalla posizione precedente alla nuova posizione (<code>/apps</code>, <code>/conf/global </code>o <code>/conf/&lt;tenant&gt;</code>).</li>
      </ul> </li>
     <li>Associa le configurazioni di AEM applicabili alle gerarchie di contenuto AEM.
      <ol>
       <li>Gerarchie di pagine AEM Sites tramite <strong>AEM Sites &gt; Pagina &gt; Proprietà pagina &gt; Scheda avanzata &gt; Configurazione cloud</strong>.</li>
       <li>AEM gerarchie di frammenti esperienza tramite <strong>AEM Frammenti esperienza &gt; Frammento esperienza &gt; Proprietà &gt; Scheda Cloud Services &gt; Configurazione cloud</strong>.</li>
       <li>AEM gerarchie di cartelle di frammenti esperienza tramite <strong>AEM Frammenti esperienza &gt; Cartella &gt; Proprietà &gt; Scheda Cloud Services &gt; Configurazione cloud</strong>.</li>
       <li>Gerarchie di cartelle AEM Assets tramite <strong>AEM Assets &gt; Cartella &gt; Proprietà cartella &gt; Scheda Cloud Services &gt; Configurazione</strong>.</li>
       <li>AEM progetti tramite <strong>AEM Progetti &gt; Progetto &gt; Proprietà progetto &gt; Scheda Avanzate &gt; Configurazione cloud</strong>.</li>
      </ol> </li>
     <li>Separa i Cloud Services di traduzione legacy migrati dalle gerarchie di contenuto AEM sopra indicate.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td><p>La risoluzione dei Cloud Services di traduzione si verifica nel seguente ordine:</p>
    <ol>
     <li><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/translations/&lt;vendor&gt;</code></li>
     <li><code>/conf/global/settings/cloudconfigs/translations/&lt;vendor&gt;</code></li>
     <li><code>/apps/settings/cloudconfigs/translations/&lt;vendor&gt;</code></li>
     <li><code>/libs/settings/cloudconfigs/translations/&lt;vendor&gt;</code></li>
    </ol> </td>
  </tr>
 </tbody>
</table>

### Modelli e-mail per notifiche flusso di lavoro {#workflow-notification-email-templates}

<table style="table-layout:auto">
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
   <td><strong>Orientamento alla ristrutturazione</strong></td>
   <td><p>Eventuali modelli e-mail di notifica del flusso di lavoro modificati devono essere migrati nella nuova posizione (<code>/conf/global</code>).</p>
    <ol>
     <li>Copia i modelli e-mail di notifica del flusso di lavoro modificati dalla posizione precedente alla nuova posizione.</li>
     <li>Rimuovi i modelli e-mail di notifica del flusso di lavoro migrati dalla posizione precedente.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td><p>La risoluzione del modello e-mail di notifica del flusso di lavoro si verifica nell’ordine seguente:</p>
    <ol>
     <li><code>/etc/workflow/notification</code></li>
     <li><code>/conf/global/settings/workflow/notification</code></li>
     <li><code>/libs/settings/workflow/notification</code></li>
    </ol> </td>
  </tr>
 </tbody>
</table>

### Pacchetti flusso di lavoro {#workflow-packages}

<table style="table-layout:auto">
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
   <td><strong>Orientamento alla ristrutturazione</strong></td>
   <td><p>I pacchetti del flusso di lavoro esistenti nella posizione precedente devono essere migrati nella nuova posizione.</p>
    <ol>
     <li>Rimuovi tutti i pacchetti del flusso di lavoro nella posizione precedente a cui non viene fatto riferimento da altri contenuti e che altrimenti non sono necessari.</li>
     <li>Sposta tutti i pacchetti del flusso di lavoro nella posizione precedente a cui non viene fatto riferimento da altri contenuti, ma che sono comunque necessari nella nuova posizione.</li>
     <li>Lascia tutti i pacchetti del flusso di lavoro a cui fanno riferimento altri contenuti della posizione precedente.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td><p>I pacchetti del flusso di lavoro creati tramite la console Miscadmin dell’interfaccia classica vengono mantenuti nella posizione precedente, mentre tutti gli altri vengono mantenuti nella nuova posizione.</p> <p>I pacchetti del flusso di lavoro memorizzati nelle posizioni precedenti o lew possono essere gestiti tramite la console Miscadmin dell'interfaccia classica.</p> </td>
  </tr>
 </tbody>
</table>

