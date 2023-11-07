---
title: Ristrutturazione dell’archivio comune in AEM 6.5
description: Scopri come apportare le modifiche necessarie per migrare alla nuova struttura dell’archivio in AEM 6.5 che sono comuni a tutte le aree dell’AEM.
contentOwner: chaikels
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
exl-id: 2d852d9d-9be3-487a-966a-4902bd7df7f9
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '2689'
ht-degree: 2%

---

# Ristrutturazione dell’archivio comune in AEM 6.5 {#common-repository-restructuring-in-aem}

Come descritto sull’elemento padre [Ristrutturazione dell’archivio in AEM 6.5](/help/sites-deploying/repository-restructuring.md) pagina, i clienti che eseguono l’aggiornamento a AEM 6.5 devono utilizzare questa pagina per valutare l’impegno di lavoro associato alle modifiche dell’archivio che potrebbero influire su tutte le soluzioni. Alcune modifiche richiedono un impegno di lavoro durante il processo di aggiornamento AEM 6.5, mentre altre possono essere differite fino a un aggiornamento futuro.

**Con aggiornamento 6.5**

* [Configurazioni ContextHub](#contexthub-6.5)
* [Istanze flusso di lavoro](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#workflow-instances)
* [Modelli flusso di lavoro](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#workflow-models)
* [Moduli di avvio per flusso di lavoro](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#workflow-launchers)
* [Script flusso di lavoro](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#workflow-scripts)

**Prima di un aggiornamento futuro**

* [Configurazioni ContextHub](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#contexthub-configurations)
* [Progettazioni Cloud Service classiche](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#classic-cloud-services-designs)
* [Progettazioni dashboard classiche](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#classic-dashboards-designs)
* [Progettazioni report classici](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#classic-reports-designs)
* [Progettazioni predefinite](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#default-designs)
* [Endpoint JavaScript di Adobe DTM](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#adobe-dtm-javascript-endpoint)
* [Adobe di endpoint per web hook DTM](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#adobe-dtm-web-hook-endpoint)
* [Attività casella in entrata](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#inbox-tasks)
* [Configurazioni blueprint per Multi-Site Manager](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#multi-site-manager-blueprint-configurations)
* [Configurazioni gadget dashboard progetti AEM](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#aem-projects-dashboard-gadget-configurations)
* [Modello e-mail notifica replica](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#replication-notification-e-mail-template)
* [Tag](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#tags)
* [Servizi cloud di traduzione](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#translation-cloud-services)
* [Lingue di traduzione](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#translation-languages)
* [Regole di traduzione](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#translation-rules)
* [Libreria client widget traduzione](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#translation-widget-client-library)
* [Console Web di attivazione struttura](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#tree-activation-web-console)
* [Cloud Service di connettori di traduzione fornitore](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#vendor-translation-connector-cloud-services)
* [Modelli e-mail di notifica flusso di lavoro](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#workflow-notification-email-templates)

## Con aggiornamento 6.5 {#with-upgrade}

### Configurazioni ContextHub {#contexthub-6.5}

A partire da AEM 6.4, non è presente alcuna configurazione ContextHub predefinita. Pertanto a livello di directory principale del sito `cq:contextHubPathproperty` deve essere impostato per indicare quale configurazione deve essere utilizzata.

1. Passa alla directory principale del sito.
1. Apri le proprietà della pagina principale e seleziona la scheda Personalizzazione.
1. Nel campo Percorso Contexthub immetti il percorso di configurazione ContextHub.

Inoltre, nella configurazione ContextHub, il `sling:resourceType` deve essere aggiornato per essere relativo e non assoluto.

1. Apri le proprietà del nodo di configurazione ContextHub in CRX DE Lite, ad esempio, `/apps/settings/cloudsettings/legacy/contexthub`
1. Cambia `sling:resourceType` da `/libs/granite/contexthub/cloudsettings/components/baseconfiguration` a `granite/contexthub/cloudsettings/components/baseconfiguration`

Cioè il `sling:resourceType` della configurazione ContextHub deve essere relativo anziché assoluto.

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
   <td><strong>Orientamenti per la ristrutturazione</strong></td>
   <td><p>Qualsiasi modello di flusso di lavoro nuovo o modificato deve essere migrato a /conf/global/workflow/models.</p>
    <ol>
     <li>Distribuire i modelli di flusso di lavoro modificati in un'istanza di sviluppo AEM 6.5 locale, in modo che esistano nel percorso precedente.</li>
     <li>Modifica il modello di flusso di lavoro utilizzando l’Editor modello flusso di lavoro AEM in AEM &gt; Strumenti &gt; Flusso di lavoro &gt; Modelli.</li>
     <li>Durante la migrazione dei modelli di flusso di lavoro AEM modificati
      <ol>
       <li>Con l’Editor modello flusso di lavoro aperto, modifica l’URL dell’indirizzo del browser e sostituisci il segmento di percorso /libs/settings/workflow/models con /etc/workflow/models.
        <ul>
         <li>Ad esempio, modifica: <em>http://localhost:4502/editor.html<strong>/libs/settings/workflow/models</strong>/dam/update_asset.html</em> a <em>http://localhost:4502/editor.html<strong>/etc/workflow/models</strong>/dam/update_asset.html</em></li>
        </ul> </li>
      </ol> </li>
     <li>Abilita la modalità Modifica nell’Editor modello flusso di lavoro, che copierà la definizione del modello flusso di lavoro in /conf/global/workflow/models.</li>
     <li>Tocca il pulsante Sync per sincronizzare le modifiche apportate al modello di flusso di lavoro di runtime in /var/workflow/models.</li>
     <li>Esporta entrambi i modelli di flusso di lavoro (/conf/global/workflow/models/&lt;workflow-model&gt;) e modello di flusso di lavoro di runtime (/var/workflow/models/&lt;workflow-model&gt;) e integrarla nel progetto AEM.
      <ol>
       <li>Ad esempio, esportare:
        <ul>
         <li><code>/conf/global/settings/workflow/models/dam/my_workflow_model</code><br /> e </li>
         <li><code>/var/workflow/models/dam/my_workflow_model</code></li>
        </ul> </li>
      </ol> </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td><p>La risoluzione del modello di flusso di lavoro viene eseguita nell'ordine seguente:</p>
    <ol>
     <li><code>/conf/global/settings/workflow/models</code></li>
     <li><code>/libs/settings/workflow/models</code></li>
     <li><code>/etc/workflow/models</code></li>
    </ol> <p>Pertanto, tutte le personalizzazioni dei modelli di flusso di lavoro forniti dall’AEM che persistono nella posizione Precedente devono essere spostate in /conf/global/settings/workflow/models se devono essere mantenute, altrimenti saranno sostituite dalla definizione del modello di flusso di lavoro fornita dall’AEM in /libs/settings/workflow/models.</p> </td>
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
   <td><strong>Orientamenti per la ristrutturazione</strong></td>
   <td><p>Non è richiesta alcuna azione per l’allineamento con la nuova posizione.</p> <p>Le istanze storiche dei flussi di lavoro possono continuare a risiedere nella posizione precedente senza problemi e verranno create nuove istanze dei flussi di lavoro nella nuova posizione.</p> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td>Qualsiasi riferimento esplicito al percorso in
    <code>
     custom
    </code> Il codice della Posizione precedente deve tenere conto anche della Nuova Posizione. Si consiglia di eseguire il refactoring di questo codice per utilizzare le API del flusso di lavoro AEM.</td>
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
   <td><strong>Orientamenti per la ristrutturazione</strong></td>
   <td><p>Qualsiasi modulo di avvio del flusso di lavoro nuovo o modificato deve essere migrato a <code>/conf/global/workflow/launcher/config</code>.</p>
    <ol>
     <li>Copia le configurazioni nuove o modificate dell'Utilità di avvio flusso di lavoro dal percorso precedente al nuovo percorso (<code>/conf/global</code>).</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td><p>La risoluzione dell'utilità di avvio del flusso di lavoro viene eseguita nell'ordine seguente:</p>
    <ol>
     <li><code>/conf/global/settings/workflow/launcher</code></li>
     <li><code>/libs/settings/workflow/launcher</code></li>
     <li><code>/etc/workflow/launcher</code></li>
    </ol> <p>Pertanto, tutte le personalizzazioni di Workflow Launcher fornite dall’AEM e persistenti nella posizione precedente devono essere spostate nella nuova posizione (<code>/conf/global/settings/workflow/launcher</code> se devono essere mantenuti, altrimenti saranno sostituiti dalla definizione Workflow Launcher fornita dall’AEM in <code>/libs/settings/workflow/launcher</code>.</p> </td>
  </tr>
 </tbody>
</table>

### Script flusso di lavoro {#workflow-scripts}

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
   <td><strong>Orientamenti per la ristrutturazione</strong></td>
   <td><p>Qualsiasi script di flusso di lavoro nuovo o modificato deve essere migrato alla nuova posizione e i modelli di flusso di lavoro di riferimento devono essere aggiornati per riflettere la nuova posizione.</p>
    <ol>
     <li>Copiare gli script di flusso di lavoro nuovi o modificati dalla posizione precedente alla nuova posizione.<br />
      <ul>
       <li><code>/apps/workflow/scripts</code> devono essere mantenute nell’SCM.</li>
      </ul> </li>
     <li>Aggiornare eventuali riferimenti agli script del flusso di lavoro nella posizione precedente in Modelli flusso di lavoro per puntare alle nuove posizioni.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td><p>L'AEM 6.4 SP1, quando sarà pubblicato, consente di posticipare la ristrutturazione al 6.5
     <code>
      upgrade
     </code>.</p> <p>Se si effettua l’aggiornamento al AEM 6.4 prima del rilascio del AEM 6.4 SP1, tale ristrutturazione dovrebbe essere effettuata nell’ambito del progetto di aggiornamento. In caso contrario, la modifica e il salvataggio dei passaggi del flusso di lavoro che fanno riferimento a script nel percorso precedente rimuoveranno completamente il riferimento allo script del flusso di lavoro dal passaggio del flusso di lavoro e solo gli script del flusso di lavoro nei nuovi percorsi saranno disponibili nel menu a discesa per la selezione degli script.</p> </td>
  </tr>
 </tbody>
</table>

## Prima di un aggiornamento futuro {#prior-to-upgrade}

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
   <td><strong>Orientamenti per la ristrutturazione</strong></td>
   <td><p>Tutte le configurazioni ContextHub nuove o modificate devono essere migrate nella nuova posizione e le pagine AEM Sites di riferimento devono essere aggiornate per riflettere la nuova posizione.</p>
    <ol>
     <li>Copia tutte le configurazioni ContextHub nuove o modificate dalla posizione precedente alla nuova posizione.</li>
     <li>Associa le configurazioni AEM applicabili alle gerarchie di contenuti AEM.
      <ol>
       <li><strong>Gerarchie di pagine AEM Sites tramite AEM Sites &gt; Pagina &gt; Proprietà pagina &gt; Scheda Avanzate &gt; Configurazione cloud</strong>.</li>
      </ol> </li>
     <li>Dissocia tutte le configurazioni ContextHub legacy migrate dalle gerarchie di contenuti AEM sopra indicate.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td>N/D</td>
  </tr>
 </tbody>
</table>

### Progettazioni Cloud Service classiche {#classic-cloud-services-designs}

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
   <td><strong>Orientamenti per la ristrutturazione</strong></td>
   <td><p>Per qualsiasi design gestito in SCM e non scritto in fase di esecuzione tramite le finestre di dialogo per progettazione.</p>
    <ol>
     <li>Copia le progettazioni dalla posizione precedente alla nuova posizione (<code>/apps</code>).</li>
     <li>Convertire qualsiasi risorsa CSS, JavaScript e statica nella progettazione in una <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">Libreria client</a> con <code>allowProxy = true</code>.</li>
     <li>Aggiornare i riferimenti alla posizione precedente in <span class="code">
       <code>
        cq
       </code>:
       <code>
        designPath
       </code></span> proprietà.</li>
     <li>Aggiorna tutte le pagine che fanno riferimento alla posizione precedente per utilizzare la nuova categoria Libreria client (è necessario aggiornare il codice di implementazione della pagina).</li>
     <li>Aggiorna le regole del Dispatcher AEM per consentire la distribuzione delle librerie client tramite /etc.clientlibs/. servlet proxy</li>
    </ol> <p>Per tutte le progettazioni che NON sono state gestite in SCM e sono state modificate in fase di esecuzione tramite le finestre di dialogo per progettazione.</p>
    <ul>
     <li>Non spostare i design modificabili da <code>/etc</code>.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td>N/D</td>
  </tr>
 </tbody>
</table>

### Progettazioni dashboard classiche {#classic-dashboards-designs}

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
   <td><strong>Orientamenti per la ristrutturazione</strong></td>
   <td><p>Per qualsiasi design gestito in SCM e non scritto in fase di esecuzione tramite le finestre di dialogo per progettazione.</p>
    <ol>
     <li>Copia le progettazioni dalla posizione precedente alla nuova posizione (/apps).</li>
     <li>Convertire qualsiasi risorsa CSS, JavaScript e statica nella progettazione in una <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">Libreria client</a> con <code>allowProxy = true</code>.</li>
     <li>Aggiornare i riferimenti alla posizione precedente in
      <code>
       cq
      </code>:
      <code>
       designPath
      </code> proprietà.</li>
     <li>Aggiorna tutte le pagine che fanno riferimento alla posizione precedente per utilizzare la nuova categoria Libreria client (è necessario aggiornare il codice di implementazione della pagina).</li>
     <li>Aggiorna le regole del Dispatcher AEM per consentire la distribuzione delle librerie client tramite /etc.clientlibs/. servlet proxy</li>
    </ol> <p>Per tutte le progettazioni che NON sono state gestite in SCM e sono state modificate in fase di esecuzione tramite le finestre di dialogo per progettazione.</p>
    <ul>
     <li>Non spostare i design modificabili da <code>/etc</code>.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td>N/D</td>
  </tr>
 </tbody>
</table>

### Progettazioni report classici {#classic-reports-designs}

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
   <td><strong>Orientamenti per la ristrutturazione</strong></td>
   <td><p>Per qualsiasi design gestito in SCM e non scritto in fase di esecuzione tramite le finestre di dialogo per progettazione.</p>
    <ol>
     <li>Copia le progettazioni dalla posizione precedente alla nuova posizione (/apps).</li>
     <li>Convertire qualsiasi risorsa CSS, JavaScript e statica nella progettazione in una <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">Libreria client</a> con <code>allowProxy = true</code>.</li>
     <li>Aggiornare i riferimenti alla posizione precedente in
      <code>
       cq
      </code>:
      <code>
       designPath
      </code> proprietà.</li>
     <li>Aggiorna tutte le pagine che fanno riferimento alla posizione precedente per utilizzare la nuova categoria Libreria client (è necessario aggiornare il codice di implementazione della pagina).</li>
     <li>Aggiorna le regole del Dispatcher AEM per consentire la distribuzione delle librerie client tramite /etc.clientlibs/. servlet proxy</li>
    </ol> <p>Per tutte le progettazioni che NON sono state gestite in SCM e sono state modificate in fase di esecuzione tramite le finestre di dialogo per progettazione.</p>
    <ul>
     <li>Non spostare i design modificabili da <code>/etc</code>.</li>
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
   <td><strong>Orientamenti per la ristrutturazione</strong></td>
   <td><p>Per qualsiasi design gestito in SCM e non scritto in fase di esecuzione tramite le finestre di dialogo per progettazione.</p>
    <ol>
     <li>Copia le progettazioni dalla posizione precedente alla nuova posizione (/apps).</li>
     <li>Convertire qualsiasi risorsa CSS, JavaScript e statica nella progettazione in una <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">Libreria client</a> con <code>allowProxy = true</code>.</li>
     <li>Aggiornare i riferimenti alla posizione precedente in
      <code>
       cq
      </code>:
      <code>
       designPath
      </code> proprietà.</li>
     <li>Aggiorna tutte le pagine che fanno riferimento alla posizione precedente per utilizzare la nuova categoria Libreria client (è necessario aggiornare il codice di implementazione della pagina).</li>
     <li>Aggiorna le regole del Dispatcher AEM per consentire la distribuzione delle librerie client tramite /etc.clientlibs/. servlet proxy</li>
    </ol> <p>Per tutte le progettazioni che NON sono state gestite in SCM e sono state modificate in fase di esecuzione tramite le finestre di dialogo per progettazione.</p>
    <ul>
     <li>Non spostare i design modificabili da <code>/etc</code>.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td>N/D</td>
  </tr>
 </tbody>
</table>

### Endpoint JavaScript di Adobe DTM {#adobe-dtm-javascript-endpoint}

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
   <td><strong>Orientamenti per la ristrutturazione</strong></td>
   <td><p>Non è richiesta alcuna azione.</p> <p>La posizione precedente pubblica funge da endpoint proxy per la nuova posizione privata.</p> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td>N/D</td>
  </tr>
 </tbody>
</table>

### Adobe di endpoint per web hook DTM {#adobe-dtm-web-hook-endpoint}

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
   <td><strong>Orientamenti per la ristrutturazione</strong></td>
   <td><p>Non è richiesta alcuna azione.</p> <p>La posizione precedente pubblica funge da endpoint proxy per la nuova posizione privata.</p> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td>N/D</td>
  </tr>
 </tbody>
</table>

### Attività casella in entrata {#inbox-tasks}

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
   <td><strong>Orientamenti per la ristrutturazione</strong></td>
   <td>Utilizza il <strong>Casella in entrata - Attività di manutenzione rimozione</strong> per rimuovere le attività precedenti dalla posizione precedente in base alle esigenze.</td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td><p>Non è richiesta alcuna azione per eseguire la migrazione delle attività nella nuova posizione.</p>
    <ul>
     <li>Le attività presenti nel percorso precedente continuano a essere disponibili e a funzionare.</li>
     <li>Le nuove attività vengono create nella nuova posizione.</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### Configurazioni blueprint per Multi-Site Manager {#multi-site-manager-blueprint-configurations}

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

### Configurazioni gadget dashboard progetti AEM {#aem-projects-dashboard-gadget-configurations}

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
   <td><strong>Orientamenti per la ristrutturazione</strong></td>
   <td><p>Qualsiasi configurazione di gadget per dashboard progetti AEM nuova o modificata deve essere migrata nella nuova posizione (<code>/apps</code>).</p>
    <ol>
     <li>Copiare nella nuova posizione le configurazioni del gadget per il dashboard dei progetti AEM nuove o modificate dalla posizione precedente (<code>/apps</code>).
      <ol>
       <li>Non copiare le configurazioni del gadget del dashboard dei progetti AEM non modificate in quanto sono ora presenti nella nuova posizione (<code>/libs</code>).</li>
      </ol> </li>
     <li>Aggiornare eventuali modelli di progetti AEM che fanno riferimento alla Posizione precedente in modo che puntino alla nuova posizione appropriata.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td>Se viene applicato il pacchetto di compatibilità AEM 6.4, sarà necessario eseguire le attività di allineamento dell’archivio al momento della rimozione del pacchetto di compatibilità.</td>
  </tr>
 </tbody>
</table>

### Modello e-mail notifica replica {#replication-notification-e-mail-template}

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
   <td><strong>Orientamenti per la ristrutturazione</strong></td>
   <td><p>È necessario eseguire la migrazione di tutti i modelli di posta elettronica per le notifiche di replica nuovi o modificati nella nuova posizione (<code>/apps</code>)</p>
    <ol>
     <li>Copiare nel nuovo percorso i modelli di posta elettronica per le notifiche di replica nuovi o modificati dal percorso precedente (<code>/apps</code>).</li>
     <li>Rimuovere eventuali modelli di posta elettronica di notifica replica migrati dal percorso precedente.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td><p>Gli unici nuovi modelli di posta elettronica per le notifiche di replica supportati sono quelli che supportano le nuove impostazioni internazionali.</p> <p>La risoluzione del modello di posta elettronica per le notifiche di replica viene eseguita nell'ordine seguente:</p>
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
   <td><strong>Orientamenti per la ristrutturazione</strong></td>
   <td><p>Tutti i tag devono essere migrati in <code>/content/cq:tags</code>.</p>
    <ol>
     <li>Copia tutti i tag dalla posizione precedente alla nuova posizione.</li>
     <li>Rimuovi tutti i tag dalla posizione precedente.</li>
     <li>Tramite la console web AEM, riavvia il bundle Day Communique 5 Tagging OSGi all’indirizzo <em>https://serveraddress:serverport/system/console/bundles/com.day.cq.cq-tagging</em> affinché l’AEM riconosca che la Nuova sede contiene contenuti e deve essere utilizzata.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td><p>Il riavvio del bundle OSGi di assegnazione tag Day Communique registrerà la nuova posizione come radice del tag solo se la posizione precedente è vuota.</p> <p>I riferimenti alla posizione precedente continueranno a funzionare dopo la migrazione alla nuova posizione per tutte le funzionalità che utilizzano l’API TagManager dell’AEM per la risoluzione dei tag.</p> <p>Qualsiasi codice personalizzato che fa riferimento esplicitamente al percorso <code>/etc/tags</code> deve essere aggiornato a <span class="code">/content/
      <code>
       cq
      </code>
      <code>
       :tags
      </code></span>, o preferibilmente riscritto per utilizzare l’API Java TagManager, insieme a questa migrazione.</p> </td>
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
   <td><strong>Orientamenti per la ristrutturazione</strong></td>
   <td><p>Qualsiasi nuovo Cloud Service di traduzione deve essere migrato nella nuova posizione (<code>/apps</code>, <code>/conf/global</code> o <code>/conf/&lt;tenant&gt;</code>).</p>
    <ol>
     <li>Migra le configurazioni esistenti nella posizione precedente alla nuova posizione.
      <ul>
       <li>Ricreare manualmente le nuove configurazioni dei Cloud Service di traduzione tramite l’interfaccia utente di creazione dell’AEM all’indirizzo <strong>Strumenti &gt; Cloud Service &gt; Cloud Service di traduzione</strong>.<br /> OPPURE </li>
       <li>Copia le nuove configurazioni dei Cloud Service di traduzione dalla posizione precedente alla nuova posizione (<code>/apps</code>, <code>/conf/global</code> o <code>/conf/&lt;tenant&gt;</code>).</li>
      </ul> </li>
     <li>Associa le configurazioni AEM applicabili alle gerarchie di contenuti AEM.
      <ol>
       <li>Gerarchie di pagine AEM Sites tramite <strong>AEM Sites &gt; Pagina &gt; Proprietà pagina &gt; Scheda Avanzate &gt; Configurazione cloud</strong>.</li>
       <li>Gerarchie di frammenti esperienza AEM tramite <strong>Frammenti esperienza AEM &gt; Frammento esperienza &gt; Proprietà &gt; Scheda Cloud Service &gt; Configurazione cloud</strong>.</li>
       <li>Gerarchie di cartelle di frammenti esperienza AEM tramite <strong>Frammenti esperienza AEM &gt; Cartella &gt; Proprietà &gt; Scheda Cloud Service &gt; Configurazione cloud</strong>.<br /> </li>
       <li>Gerarchie di cartelle di AEM Assets tramite <strong>AEM Assets &gt; Cartella &gt; Proprietà cartella &gt; Scheda Cloud Service &gt; Configurazione</strong>.</li>
       <li>Progetti AEM tramite <strong>Progetti AEM &gt; Progetto &gt; Proprietà progetto &gt; Scheda Avanzate &gt; Configurazione cloud</strong>.</li>
      </ol> </li>
     <li>Dissocia eventuali Cloud Service di traduzione legacy migrati dalle gerarchie di contenuto AEM sopra indicate.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td><p>La risoluzione dei Cloud Service di traduzione viene eseguita nell'ordine seguente:</p>
    <ol>
     <li><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/translations/translationcfg</code></li>
     <li><code>/conf/global/settings/cloudconfigs/translations/translationcfg</code></li>
     <li><code>/apps/settings/cloudconfigs/translations/translationcfg</code></li>
     <li><code>/libs/settings/cloudconfigs/translations/translationcfg</code></li>
    </ol> <p>I Cloud Service di traduzione migrati devono essere compatibili con AEM 6.4.</p> </td>
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
   <td><strong>Orientamenti per la ristrutturazione</strong></td>
   <td><p>Qualsiasi definizione nuova o modificata di Lingua di traduzione richiede la migrazione di tutte le definizioni di Lingua di traduzione nella nuova posizione (<code>/apps</code>).</p>
    <ol>
     <li>Se sono state apportate aggiunte o modifiche alle definizioni della lingua di traduzione, copia tutte le definizioni della lingua di traduzione dalla posizione precedente alla nuova posizione (<code>/apps</code>).</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td><p>La risoluzione del percorso della lingua di traduzione viene eseguita nell'ordine seguente:</p>
    <ol>
     <li><code>/etc/translation/supportedLanguages</code></li>
     <li><code>/apps/settings/translation/supportedLanguage</code></li>
     <li><code>/libs/settings/translation/supportedLanguages</code></li>
    </ol> <p>Questa risoluzione non supporta una sovrapposizione di unione, il che significa che il percorso risolto deve contenere tutte le lingue supportate e non erediterà le lingue supportate da risoluzioni di ordine superiore.</p> </td>
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
   <td><strong>Orientamenti per la ristrutturazione</strong></td>
   <td><p>È necessario eseguire la migrazione di un file XML delle regole di traduzione modificato nella nuova posizione (<code>/apps</code>, o <code>/conf/global</code>).</p> <p>1. Copiare il file XML delle regole di traduzione modificato dalla posizione precedente nella nuova posizione.</p> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td><p>La risoluzione XML delle regole di traduzione della replica viene eseguita nell'ordine seguente:</p>
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

### Libreria client widget traduzione {#translation-widget-client-library}

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
   <td><strong>Orientamenti per la ristrutturazione</strong></td>
   <td><p>Per qualsiasi design gestito in SCM e non scritto in fase di esecuzione tramite le finestre di dialogo per progettazione.</p>
    <ol>
     <li>Copia le progettazioni dalla posizione precedente alla nuova posizione (/apps).</li>
     <li>Convertire qualsiasi risorsa CSS, JavaScript e statica nella progettazione in una <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">Libreria client</a> con <code>allowProxy = true</code>.</li>
     <li>Aggiornare i riferimenti alla posizione precedente in
      <code>
       cq
      </code>:
      <code>
       designPath
      </code> proprietà.</li>
     <li>Aggiorna tutte le pagine che fanno riferimento alla posizione precedente per utilizzare la nuova categoria Libreria client (è necessario aggiornare il codice di implementazione della pagina).</li>
     <li>Aggiorna le regole del Dispatcher AEM per consentire la distribuzione delle librerie client tramite /etc.clientlibs/. servlet proxy</li>
    </ol> <p>Per tutte le progettazioni che NON sono state gestite in SCM e sono state modificate in fase di esecuzione tramite le finestre di dialogo per progettazione.</p>
    <ul>
     <li>Non spostare i design modificabili da <code>/etc</code>.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td>N/D</td>
  </tr>
 </tbody>
</table>

### Console Web di attivazione struttura {#tree-activation-web-console}

| **Posizione precedente** | `/etc/replication/treeactivation` |
|---|---|
| **Nuove posizioni** | `/libs/replication/treeactivation` |
| **Orientamenti per la ristrutturazione** | Non è richiesta alcuna azione. |
| **Note** | La console Web di Attivazione struttura è ora disponibile tramite **Strumenti > Implementazione > Replica > Attiva struttura**. |

{style="table-layout:auto"}

### Cloud Service di connettori di traduzione fornitore {#vendor-translation-connector-cloud-services}

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
   <td><strong>Orientamenti per la ristrutturazione</strong></td>
   <td><p>Qualsiasi nuovo Cloud Service di connettori di traduzione fornitore deve essere migrato nella nuova posizione (<code>/apps</code>, <code>/conf/global</code> o <code>/conf/&lt;tenant&gt;</code>).</p>
    <ol>
     <li>Migra le configurazioni esistenti nella posizione precedente alla nuova posizione.
      <ul>
       <li>Creazione manuale di nuove configurazioni dei Cloud Service di connettori di traduzione fornitore tramite <strong>Interfaccia utente di creazione AEM in Strumenti &gt; Cloud Service &gt; Cloud Service di traduzione</strong>.<br /> OPPURE </li>
       <li>Copia le nuove configurazioni dei Cloud Service del connettore di traduzione fornitore dalla posizione precedente alla nuova posizione (<code>/apps</code>, <code>/conf/global </code>o <code>/conf/&lt;tenant&gt;</code>).</li>
      </ul> </li>
     <li>Associa le configurazioni AEM applicabili alle gerarchie di contenuti AEM.
      <ol>
       <li>Gerarchie di pagine AEM Sites tramite <strong>AEM Sites &gt; Pagina &gt; Proprietà pagina &gt; Scheda Avanzate &gt; Configurazione cloud</strong>.</li>
       <li>Gerarchie di frammenti esperienza AEM tramite <strong>Frammenti esperienza AEM &gt; Frammento esperienza &gt; Proprietà &gt; Scheda Cloud Service &gt; Configurazione cloud</strong>.</li>
       <li>Gerarchie di cartelle di frammenti esperienza AEM tramite <strong>Frammenti esperienza AEM &gt; Cartella &gt; Proprietà &gt; Scheda Cloud Service &gt; Configurazione cloud</strong>.</li>
       <li>Gerarchie di cartelle di AEM Assets tramite <strong>AEM Assets &gt; Cartella &gt; Proprietà cartella &gt; Scheda Cloud Service &gt; Configurazione</strong>.</li>
       <li>Progetti AEM tramite <strong>Progetti AEM &gt; Progetto &gt; Proprietà progetto &gt; Scheda Avanzate &gt; Configurazione cloud</strong>.</li>
      </ol> </li>
     <li>Dissocia eventuali Cloud Service di traduzione legacy migrati dalle gerarchie di contenuto AEM sopra indicate.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td><p>La risoluzione dei Cloud Service di traduzione viene eseguita nell'ordine seguente:</p>
    <ol>
     <li><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/translations/&lt;vendor&gt;</code></li>
     <li><code>/conf/global/settings/cloudconfigs/translations/&lt;vendor&gt;</code></li>
     <li><code>/apps/settings/cloudconfigs/translations/&lt;vendor&gt;</code></li>
     <li><code>/libs/settings/cloudconfigs/translations/&lt;vendor&gt;</code></li>
    </ol> </td>
  </tr>
 </tbody>
</table>

### Modelli e-mail di notifica flusso di lavoro {#workflow-notification-email-templates}

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
   <td><strong>Orientamenti per la ristrutturazione</strong></td>
   <td><p>È necessario eseguire la migrazione di tutti i modelli e-mail di notifica del flusso di lavoro modificati alla nuova posizione (<code>/conf/global</code>).</p>
    <ol>
     <li>Copiare nella nuova posizione tutti i modelli di e-mail di notifica del flusso di lavoro modificati dalla posizione precedente.</li>
     <li>Rimuovi i modelli e-mail di notifica flusso di lavoro migrati dalla posizione precedente.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td><p>La risoluzione del modello e-mail di notifica flusso di lavoro viene eseguita nell'ordine seguente:</p>
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
   <td><strong>Orientamenti per la ristrutturazione</strong></td>
   <td><p>I pacchetti di flusso di lavoro esistenti nella posizione precedente devono essere migrati nella nuova posizione.</p>
    <ol>
     <li>Rimuovi eventuali pacchetti flusso di lavoro nella posizione precedente che non sono referenziati da altri contenuti e che non sono altrimenti necessari.</li>
     <li>Sposta tutti i pacchetti flusso di lavoro nella posizione precedente che non sono referenziati da altri contenuti ma che sono comunque necessari nella nuova posizione.</li>
     <li>Lascia nella posizione precedente tutti i pacchetti del flusso di lavoro a cui fanno riferimento altri contenuti.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td><p>I pacchetti del flusso di lavoro creati tramite la console Miscadmin dell’interfaccia classica vengono mantenuti nella posizione precedente, mentre tutti gli altri vengono mantenuti nella nuova posizione.</p> <p>I pacchetti del flusso di lavoro memorizzati nelle posizioni precedenti o precedenti possono essere gestiti tramite la console Gestione errori dell’interfaccia classica.</p> </td>
  </tr>
 </tbody>
</table>
