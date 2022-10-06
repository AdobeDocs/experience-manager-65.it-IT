---
title: Tipi di nodo personalizzati
seo-title: Custom Node Types
description: AEM è basato su Sling e utilizza un archivio JCR con tipi di nodo offerti da entrambi, ma AEM fornisce anche una serie di tipi di nodo personalizzati
seo-description: AEM is based on Sling and uses a JCR repository with node types offered by both, but AEM also provides a range of custom node types
uuid: f2022504-e433-4b42-9cc1-eef41086483a
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: aae186eb-e059-4a9d-b02d-86a86c86589d
exl-id: bfd50aa9-579e-47d5-997d-ec764c782497
source-git-commit: 2bae11eafb875f01602c39c0dba00a888e11391a
workflow-type: tm+mt
source-wordcount: '1877'
ht-degree: 9%

---

# Tipi di nodo personalizzati{#custom-node-types}

Poiché AEM è basato su Sling e utilizza un archivio JCR, i tipi di nodo offerti da entrambi sono disponibili per l&#39;uso:

* [Tipi di nodo JCR](https://www.adobe.io/experience-manager/reference-materials/spec/jcr/2.0/3_Repository_Model.html#3.1.7-Node-Types)
* [Tipi di nodi Sling](https://cwiki.apache.org/confluence/display/SLING/Sling+Node+Types)

Oltre a questi. AEM fornisce una serie di tipi di nodo personalizzati.

## Audit {#audit}

### cq:AuditEvent {#cq-auditevent}

**Descrizione**

Definisce il tipo di nodo di un nodo evento di controllo.

* `@prop cq:time`
* `@prop cq:userid`
* `@prop cq:path`
* `@prop cq:type`
* `@prop cq:category`
* `@prop cq:properties`

**Definizione**

* `[cq:AuditEvent]`
   * `- * (undefined)`
   * `- * (undefined) multiple`
   * `+ * (nt:base) = nt:base multiple version`
* `- cq:time (date)`
* `- cq:userid (string)`
* `- cq:path (string)`
* `- cq:type (string)`
* `- cq:category (string)`
* `- cq:properties (binary)`

## Commenti {#comment}

### cq:Commento {#cq-comment}

**Descrizione**

Definisce il tipo di nodo di un nodo di commento.

* `@prop userIdentifier`

**Definizione**

* `[cq:Comment] > mix:title, mix:created, mix:language, nt:unstructured, cq:Taggable`
* `- email (string)`
* `- ip (string)`
* `- referer (string)`
* `- url (string)`
* `- userAgent (string)`
* `- userIdentifier (string)`
* `- authorizableId (string)`

### cq:CommentAttachment {#cq-commentattachment}

**Descrizione**

Definisce il tipo di nodo di un `commentattachment` nodo

**Definizione**

* `[cq:CommentAttachment] > nt:file`
   * `- * (undefined)`
   * `- * (undefined) multiple`

### cq:CommentContent {#cq-commentcontent}

**Descrizione**

Definisce il tipo di nodo di un nodo di contenuto del commento

**Definizione**

* `[cq:Comment] > mix:title, mix:created, mix:language, nt:unstructured, cq:Taggable`
* `- email (string)`
* `- ip (string)`
* `- referer (string)`
* `- url (string)`
* `- userAgent (string)`
* `- userIdentifier (string)`
* `- authorizableId (string)`

### cq:GeoLocation {#cq-geolocation}

**Descrizione**

Un mixin che definisce una posizione geografica in gradi decimali (DD)

* `@prop latitude` - latitudine codificata come doppia con gradi decimali
* `@prop longitude` - la longitudine viene codificata come doppia utilizzando i gradi decimali

**Definizione**

* `[cq:GeoLocation] mixin`
* `- latitude (double)`
* `- longitude (double)`

### cq:Trackback {#cq-trackback}

**Descrizione**

Definisce il tipo di nodo di un nodo di trackback.

**Definizione**

* `[cq:Trackback] > mix:title, mix:created, mix:language, nt:unstructured`

## Core {#core}

### cq:Page {#cq-page}

**Descrizione**

Definisce la pagina CQ predefinita.

* `@node jcr:content` - Contenuto principale della pagina.

**Definizione**

* `[cq:Page] > nt:hierarchyNode orderable`
   * `+ jcr:content (nt:base) = nt:unstructured copy primary`
   * `+ * (nt:base) = nt:base version`

### cq:PseudoPage {#cq-pseudopage}

**Descrizione**

Definisce un tipo mixin che contrassegna i nodi come pagine pseudo-pagine. Ciò significa che possono essere adattati per il supporto di modifica di pagina e WCM.

**Definizione**

* `[cq:PseudoPage] mixin`

### cq:PageContent {#cq-pagecontent}

**Descrizione**

Definisce il nodo predefinito per il contenuto della pagina, con le proprietà minime utilizzate da WCM.

* `@prop jcr:title` - Titolo della pagina.
* `@prop jcr:description` - Descrizione della pagina.
* `@prop cq:template` - Percorso del modello utilizzato per creare la pagina.
* `@prop cq:allowedTemplates` - Elenco di espressioni regolari utilizzate per determinare il percorso o i percorsi del modello consentito.
* `@prop pageTitle` - Titolo generalmente visualizzato nel `<title>` tag .
* `@prop navTitle` - Titolo di solito utilizzato nella navigazione.
* `@prop hideInNav` - Specifica se la pagina deve essere nascosta nella navigazione.
* `@prop onTime` - Tempo di validità della pagina.
* `@prop offTime` - Tempo di validità della pagina.
* `@prop cq:lastModified` - Data dell’ultima modifica apportata alla pagina (o ai relativi paragrafi).
* `@prop cq:lastModifiedBy` - Ultimo utente che ha modificato la pagina (o i relativi paragrafi).
* `@prop jcr:language` - Lingua del contenuto della pagina.

>[!NOTE]
>
>Non è obbligatorio che il contenuto della pagina utilizzi questo tipo.

**Definizione**
* `[cq:PageContent] > nt:unstructured, mix:title, mix:created, cq:OwnerTaggable, sling:VanityPath, cq:ReplicationStatus, sling:Resource orderable`
   * `- cq:template (string)`
   * `- cq:allowedTemplates (string) multiple`
   * `- pageTitle (string)`
   * `- navTitle (string)`
   * `- hideInNav (boolean)`
   * `- onTime (date)`
   * `- offTime (date)`
   * `- cq:lastModified (date)`
   * `- cq:lastModifiedBy (string)`
   * `- cq:designPath (string)`
   * `- jcr:language (string)`

### cq:Template {#cq-template}

**Descrizione**

Definisce un modello CQ.

* `@node jcr:content` - Contenuto predefinito per le nuove pagine.
* `@node icon.png` - File contenente un&#39;icona caratteristica.
* `@node thumbnail.png` - File contenente una caratteristica immagine miniatura.
* `@node workflows` - Assegnazione automatica della configurazione del flusso di lavoro. La configurazione seguirà la seguente struttura:
   * `+ workflows`
      * `+ name1`
         * `- cq:path`
            * `- cq:workflowName`
* `@prop allowedParents` - Pattern di espressioni regolari per determinare il percorso o i percorsi dei modelli consentiti come modelli principali.
* `@prop allowedChildren` - Pattern di espressioni regolari per determinare il percorso o i percorsi dei modelli consentiti come modelli figlio.
* `@prop ranking` - Posizionamento nell’elenco dei modelli nella finestra di dialogo crea pagina.

**Definizione**

* `[cq:Template] > nt:hierarchyNode, mix:title`
   * `- * (undefined)`
   * `- * (undefined) multiple`
   * `+ * (nt:base) = nt:base multiple version`
   * `+ jcr:content (nt:base) copy`
   * `+ icon.png (nt:file) copy`
   * `+ thumbnail.png (nt:file) copy`
   * `+ workflows (nt:base) copy`
   * `- allowedParents (string) multiple`
   * `- allowedChildren (string) multiple`
   * `- ranking (long)`

### cq:Component {#cq-component}

**Descrizione**

Definisce un componente CQ.

* `@prop jcr:title` - Titolo del componente.
* `@prop jcr:description` - Descrizione del componente.
* `@node dialog` - Finestra di dialogo principale.
* `@prop dialogPath` - Percorso di dialogo principale (alternativo al dialogo).
* `@node design_dialog` - Finestra di dialogo Progettazione.
* `@prop cq:cellName` - Nome della cella di progettazione.
* `@prop cq:isContainer` - Indica se si tratta di un componente contenitore. In questo modo si forza l’utilizzo dei nomi di cella dei componenti secondari anziché dei nomi di percorso. Ad esempio, il `parsys` è un componente contenitore . Se questo valore non è definito, il controllo viene effettuato in base all&#39;esistenza di un `cq:childEditConfig`.
* `@prop cq:noDecoration` - Se vero, nessuna decorazione `div` I tag vengono disegnati quando si include questo componente.
* `@node cq:editConfig` - La configurazione che definisce i parametri della barra di modifica.
* `@node cq:childEditConfig` - La configurazione di modifica ereditata dai componenti secondari.
* `@node cq:htmlTag` - Definisce gli attributi di tag aggiuntivi aggiunti al &quot;circostante&quot; `div` quando il componente è incluso.
* `@node icon.png`- File contenente un&#39;icona caratteristica.
* `@node thumbnail.png` - File contenente una caratteristica immagine miniatura.
* `@prop allowedParents` - Pattern di espressioni regolari per determinare il percorso o i percorsi dei componenti consentiti come componenti padre.
* `@prop allowedChildren` - Pattern di espressioni regolari per determinare i percorsi dei componenti consentiti come componenti secondari.
* `@node virtual` - Contiene i sottonodi che riflettono i componenti virtuali utilizzati per il trascinamento e il rilascio del componente.
* `@prop componentGroup` - Nome del gruppo di componenti utilizzato per il trascinamento del componente.
* `@node cq:infoProviders` - Contiene i sottonodi, ciascuno dei quali ha una proprietà `className` che si riferisce a un `PageInfoProvider`.

**Definizione**

* `[cq:Component] > nt:folder, mix:title, sling:ResourceSuperType`
   * `- * (undefined)`
   * `- * (undefined) multiple`
   * `+ * (nt:base) = nt:base multiple version`
   * `+ dialog (nt:base) = nt:unstructured copy`
   * `- dialogPath (string)`
   * `+ design_dialog (nt:base) = nt:unstructured copy`
   * `- cq:cellName (string)`
   * `- cq:isContainer (boolean)`
   * `- cq:noDecoration (boolean)`
   * `+ cq:editConfig (cq:EditConfig) = cq:EditConfig copy`
   * `+ cq:childEditConfig (cq:EditConfig) = cq:EditConfig copy`
   * `+ cq:htmlTag (nt:base) = nt:unstructured copy`
   * `+ icon.png (nt:file) copy`
   * `+ thumbnail.png (nt:file) copy`
   * `- allowedParents (string) multiple`
   * `- allowedChildren (string) multiple`
   * `+ virtual (nt:base) = sling:Folder copy`
   * `- componentGroup (string)`
   * `+ cq:infoProviders (nt:base) = nt:unstructured copy`

### cq:ComponentMixin {#cq-componentmixin}

**Descrizione**

Definisce un componente CQ come tipo mixin.

**Definizione**

`[cq:ComponentMixin] > cq:Component mixin`

### cq:EditConfig {#cq-editconfig}

**Descrizione**

Definisce la configurazione per la &quot;editbar&quot;.

* `@prop cq:dialogMode` - Modalità della finestra di dialogo:
   * `floating` - per una finestra di dialogo mobile normale
   * `inline` - editing in linea
   * `auto` - rilevamento automatico (a seconda dello spazio disponibile)
* `@node cq:inplaceEditing` - Configurazione di modifica locale per questo componente.
* `@prop cq:layout`- Layout della barra di modifica:
   * `editbar` - barra di modifica
   * `rollover` - roll over frame
   * `auto` - rilevamento automatico
* `@node cq:formParameters`- Parametri aggiuntivi da aggiungere al modulo di dialogo.
* `@prop cq:actions`- Elenco di azioni (pulsanti a barre di modifica o voci di menu).
* `@node cq:actionConfigs` - Configurazioni widget per le voci di menu o di barre di modifica.
* `@prop cq:emptyText` - Testo da visualizzare se non è presente alcun contenuto visivo.
* `@node cq:dropTargets` - Raccolta di `{@link cq:DropTargetConfig}` nodi.

**Definizione**

* `[cq:EditConfig] > nt:unstructured, nt:hierarchyNode orderable`
   * `- cq:dialogMode (string) < 'auto', 'floating', 'inline'`
   * `- cq:layout (string) < 'editbar', 'rollover', 'auto' + cq:formParameters (nt:base) = nt:unstructured`
   * `- cq:actions (string) multiple`
   * `+ cq:actionConfigs (nt:base) = nt:unstructured`
   * `- cq:emptyText (string)`
   * `+ cq:dropTargets (nt:base) = nt:unstructured`
   * `+ cq:listeners (nt:base) = cq:EditListenersConfig`

### cq:DropTargetConfig {#cq-droptargetconfig}

**Descrizione**

Configura una destinazione di rilascio di un componente. Il nome del nodo verrà utilizzato come ID per il trascinamento.

* `@prop accept` - Elenco dei tipi di mime accettati da questo obiettivo di rilascio; ad esempio `["image/*"]`
* `@prop groups` - Elenco dei gruppi di trascinamento che accettano un’origine.
* `@prop propertyName` - Nome della proprietà utilizzata per memorizzare il riferimento.

**Definizione**

* `[cq:DropTargetConfig] > nt:unstructured orderable`
   * `- accept (string) multiple`
   * `- groups (string) multiple`
   * `- propertyName (string)`
   * `+ parameters (nt:base) = nt:unstructured`

### cq:VirtualComponent {#cq-virtualcomponent}

**Descrizione**

Definisce un componente CQ virtuale. Attualmente sono utilizzati solo per la nuova procedura guidata di trascinamento del componente.

* `@prop jcr:title` - Titolo del componente.
* `@prop jcr:description` - Descrizione del componente.
* `@node cq:editConfig` - Modifica la configurazione che definisce i parametri della barra di modifica.
* `@node cq:childEditConfig`- Modifica la configurazione ereditata dai componenti secondari.
* `@node icon.png` - File contenente un&#39;icona caratteristica.
* `@node thumbnail.png` - File contenente una caratteristica immagine miniatura.
* `@prop allowedParents` - Pattern di espressioni regolari per determinare i percorsi dei componenti consentiti come componenti padre.
* `@prop allowedChildren` - Pattern di espressioni regolari per determinare i percorsi dei componenti consentiti come componenti secondari.
* `@prop componentGroup` - Nome del gruppo di componenti per il trascinamento del componente.

**Definizione**

`[cq:VirtualComponent] > nt:folder, mix:title`
`- * (undefined)`
`- * (undefined) multiple`
`+ * (nt:base) = nt:base multiple version`
`+ cq:editConfig (cq:EditConfig) = cq:EditConfig copy`
`+ icon.png (nt:file) copy`
`+ thumbnail.png (nt:file) copy`
`- allowedParents (string) multiple`
`- allowedChildren (string) multiple`
`- componentGroup (string)`

### cq:EditListenersConfig {#cq-editlistenersconfig}

**Descrizione**

Definisce i listener (lato client) da eseguire su un evento di modifica. I valori devono fare riferimento a una funzione di listener lato client valida o contenere una scelta rapida predefinita:

* `REFRESH_PAGE`
* `REFRESH_SELF`
* `REFRESH_PARENT`

* `@prop aftercreate` - Viene attivato dopo la creazione di un componente.
* `@prop afteredit` - Viene attivato dopo che un componente è stato modificato (modificato).
* `@prop afterdelete` - Viene attivato dopo l’eliminazione di un componente.
* `@prop afterinsert` - Viene attivato dopo l’aggiunta di un componente a questo contenitore.
* `@prop afterremove` - Si attiva dopo che un componente è stato rimosso da questo contenitore.
* `@prop aftermove` - Viene attivato dopo lo spostamento dei componenti in questo contenitore.

**Definizione**

* `[cq:EditListenersConfig]`
   * `- &ast; (undefined)`
   * `- &ast; (undefined) multiple`
   * `+ &ast; (nt:base) = nt:base multiple version`
   * `- aftercreate (string)`
   * `- afteredit (string)`
   * `- afterdelete (string)`
   * `- afterinsert (string)`
   * `- afterremove (string)`
   * `- aftermove (string)`

## DAM {#dam}

### dam:AssetContent {#dam-assetcontent}

**Descrizione**

Contenuto di una risorsa DAM.

**Definizione**

* `[dam:AssetContent] > nt:unstructured`
   * `+ metadata (nt:unstructured)`
   * `+ renditions (nt:folder)`

### dam:Asset {#dam-asset}

**Descrizione**

Risorsa DAM.

**Definizione**

`[dam:Asset] > nt:hierarchyNode`
`+ jcr:content (dam:AssetContent) = dam:AssetContent copy primary`
`+ * (nt:base) = nt:base version`

### dam:Miniatura {#dam-thumbnail}

**Descrizione**

Miniatura per rappresentare una risorsa DAM.

**Definizione**

* `[dam:Thumbnails]`
   * `mixin`
   * `+ dam:thumbnails (nt:folder)`

## Elenco dei contenitori di consegna {#delivery-container-list}

### cq:containerList {#cq-containerlist}

**Descrizione**

Elenco contenitori.

**Definizione**

* `[cq:containerList]`
   * `mixin`

## Pagina di consegna {#delivery-page}

### cq:Cq4PageAttributes {#cq-cq-pageattributes}

**Descrizione**

`cq:attributes` è il tipo di nodo per i tag di versione ContentBus. Questo nodo ha solo una serie di proprietà; di cui tre sono &quot;create&quot;, &quot;csd&quot; e &quot;timestampe&quot; predefiniti.

* `@prop created (long) mandatory copy` - Timestamp della creazione delle informazioni sulla versione, in genere l’ora del check-in della versione precedente o dell’ora della creazione della pagina.
* `@prop csd (string) mandatory copy` - attributo standard csd, copia della proprietà cq:csd del nodo della pagina
* `@prop timestamp (long) mandatory copy` - Timestamp dell&#39;ultima modifica della versione, in genere tempo di archiviazione.
* `@prop * (string) copy` - Attributi aggiuntivi, con versione con il nodo principale.

**Definizione**

* `[cq:Cq4PageAttributes] > nt:base`
   * `- created (long) mandatory copy`
   * `- csd (string) mandatory copy`
   * `- timestamp (long) mandatory copy`
   * `- &ast; (string) copy`

### cq:Cq4ContentPage {#cq-cq-contentpage}

**Descrizione**

Tipo di nodo `cq:contentPage` contiene le definizioni dei nodi di proprietà e figlio per le pagine di contenuto ContentBus. Solo quando questo tipo di mixin viene aggiunto a un nodo di tipo `cq:page`, un nodo diventa una pagina di contenuto ContentBus.

Gli elementi in una `cq:Cq4ContentPage` sono:

* `@prop cq:csd` - Il CSD ContentBus della pagina.
* `@node cq:content` - Il contenuto della pagina. Questo nodo figlio non esiste se il nodo della pagina è nello stato &quot;Esistente senza contenuto&quot; o &quot;Eliminato&quot;.
* `@node cq:attributes` - Elenco degli attributi di pagina, precedentemente noti come tag di versione. Questo nodo è obbligatorio per il tipo cq:contentPage. Viene eseguito il controllo delle versioni del nodo attributi quando si esegue il controllo delle versioni della pagina.

**Definizione**

* `[cq:Cq4ContentPage]`
   * `- cq:csd (string) mandatory copy`
   * `+ cq:attributes (cq:Cq4PageAttributes)`

## Importazione {#importer}

### cq:PollConfig {#cq-pollconfig}

**Descrizione**

Configurazione del sondaggio.

* `@prop source (String) mandatory` - URI origine dati, obbligatorio e non vuoto
* `@prop target (String)` - La posizione di destinazione in cui vengono archiviati i dati recuperati dall’origine dati. Questo è facoltativo e predefinito al nodo cq:PollConfig .
* `@prop interval (Long)` - L&#39;intervallo in secondi a cui eseguire il polling dei dati nuovi o aggiornati dall&#39;origine dati. Questo è facoltativo e il valore predefinito è 30 minuti (1800 secondi).
* [Creazione di servizi di importazione dati personalizzati per Adobe Experience Manager](https://helpx.adobe.com/experience-manager/using/polling.html)

**Definizione**

* `[cq:PollConfig]`
   * `mixin`
   * `- source (String) mandatory`
   * `- target (String)`
   * `- interval (Long)`

### cq:PollConfigFolder {#cq-pollconfigfolder}

**Descrizione**

Comodità del tipo di nodo principale per creare facilmente nodi di configurazione del poll.

**Definizione**

`[cq:PollConfigFolder] > sling:Folder, cq:PollConfig`

## Dove si trova {#location}

### cq:GeoLocation {#cq-geolocation-1}

**Descrizione**

Un mixin che definisce una posizione geografica in gradi decimali (DD).

* `@prop latitude` - Latitudine codificata come doppia con gradi decimali.
* `@prop longitude` - La longitudine viene codificata come doppia utilizzando i gradi decimali.

**Definizione**

* `[cq:GeoLocation]`
   * `mixin`
   * `- latitude (double)`
   * `- longitude (double)`

## Mailer {#mailer}

### cq:mailerMessage {#cq-mailermessage}

**Descrizione**

Tipi di nodi MailerService. Il mailer utilizza i nodi con questo mixin come nodi principali delle definizioni dei messaggi.

**Definizione**

* `[cq:mailerMessage]`
   * `mixin`
   * `- messageStatus (string)`
   * `= 'new'`
   * `mandatory autocreated`

## MSM {#msm}

### cq:LiveRelationship {#cq-liverelationship}

**Descrizione**

Definisce un mixin LiveRelationship. Un nodo sorgente principale (di controllo) e un nodo Live Copy (controllato) possono essere virtualmente collegati tramite una LiveRelationship.

**Definizione**

* `[cq:LiveRelationship] mixin`
   * `- cq:lastRolledout (date)`
   * `- cq:lastRolledoutBy (string)`
   * `- cq:sourceUUID (string)`

### cq:LiveSync {#cq-livesync}

**Descrizione**

Definisce un mixin LiveSync. Se un nodo è coinvolto in una LiveRelationship con un nodo di origine principale (che controlla) e un nodo Live Copy (controllato), viene contrassegnato come LiveSync.

* `@prop cq:master` - Percorso della sorgente primaria (controllo) di LiveRelationship.
* `@prop cq:isDeep` - Definisce se la relazione è disponibile per i figli.
* `@prop cq:syncTrigger` - Definisce quando viene attivata la sincronizzazione.
* `@node * LiveSyncAction` - Azioni da eseguire sulla sincronizzazione

**Definizione**

`[cq:LiveSync] > cq:LiveRelationship mixin orderable`
`+ * (cq:LiveSyncAction) = cq:LiveSyncAction`
`+ cq:LiveSyncConfig (nt:base) = cq:LiveSyncConfig`

### cq:LiveSyncCancelled {#cq-livesynccancelled}

**Descrizione**

Definisce un mixin LiveSyncCancelled. Annulla il comportamento LiveSync di un nodo Live Copy (controllato) che può essere coinvolto in una LiveRelationship a causa di uno dei suoi genitori.

* `@prop cq:isCancelledForChildren` - Definisce se un LiveSync viene annullato; anche per i bambini.

**Definizione**

* `[cq:LiveSyncCancelled] > cq:LiveRelationship mixin`
   * `- cq:isCancelledForChildren (boolean)`

### cq:LiveSyncAction {#cq-livesyncaction}

**Descrizione**

Definisce un LiveSyncAction collegato a un LiveSync.

* `@prop name` - Nome azione
* `@prop value` - Valore azione

**Definizione**

* `[cq:LiveSyncAction] > nt:unstructured`

### cq:LiveSyncConfig {#cq-livesyncconfig}

**Descrizione**

Configurazione di Live Sync.

**Definizione**

* `[cq:LiveSyncConfig]`
   * `- cq:master (string) mandatory`
   * `- cq:isDeep (boolean)`
   * `- cq:trigger (string) /** deprecated **/`

Per AEM 5.4 aggiungi alla fine dell’elenco:

* `- cq:rolloutConfigs (string) multiple /** deprecated **/`

### cq:BlueprintAction {#cq-blueprintaction}

**Descrizione**

Azione Blueprint

**Definizione**

* `[cq:BlueprintAction] > nt:unstructured`

## Platform {#platform}

### cq:Console {#cq-console}

**Descrizione**

Definisce il tipo di nodo di un nodo della console.

**Definizione**

* `[cq:Console] > sling:VanityPath, mix:title`
   * `mixin`

## Replica {#replication}

### cq:ReplicationStatus {#cq-replicationstatus}

**Descrizione**

Definisce il mixin delle informazioni sullo stato di replica.

* `@prop cq:lastPublished`- Data dell’ultima pubblicazione della pagina (non più in uso).
* `@prop cq:lastPublishedBy`- L’utente che ha pubblicato la pagina per ultima (non più utilizzata).
* `@prop cq:lastReplicated` - Data dell&#39;ultima replica della pagina.
* `@prop cq:lastReplicatedBy` - Utente che ha replicato la pagina per ultima.
* `@prop cq:lastReplicationAction` - L&#39;azione di replica: attiva o disattiva.
* `@prop cq:lastReplicationStatus` - Lo stato di replica (non più utilizzato).

**Definizione**

* `[cq:ReplicationStatus]`
   * `mixin`
   * `- cq:lastPublished (date) ignore`
   * `- cq:lastPublishedBy (string) ignore`
   * `- cq:lastReplicated (date) ignore`
   * `- cq:lastReplicatedBy (string) ignore`
   * `- cq:lastReplicationAction (string) ignore`
   * `- cq:lastReplicationStatus (string) ignore`

## Sicurezza {#security}

### cq:ApplicationPrivilege {#cq-applicationprivilege}

**Descrizione**

Definisce un privilegio di applicazione.

**Definizione**

* `[cq:ApplicationPrivilege] mixin`

### cq:PrivilegeAcl {#cq-privilegeacl}

**Descrizione**

Definisce un ACL del privilegio dell&#39;applicazione.

* `@prop cq:isPathDependent`
* `@node * ACEs`

**Definizione**

* `[cq:PrivilegeAcl] > cq:ApplicationPrivilege mixin orderable`
   * `- cq:isPathDependent (boolean)`
   * `+ * (cq:PrivilegeAce) = cq:PrivilegeAce`

### cq:PrivilegeAce {#cq-privilegeace}

**Descrizione**

Definisce un ACE privilegio dell&#39;applicazione.

* `@prop path`
* `@prop deny`

**Definizione**

* `[cq:PrivilegeAce]`
   * `- path mandatory`
   * `- deny (boolean)`

### cq:ApplicationPrivilege {#cq-applicationprivilege-1}

**Descrizione**

Definisce un privilegio di applicazione.

**Definizione**

* `[cq:ApplicationPrivilege] mixin`

### cq:PrivilegeAcl {#cq-privilegeacl-1}

**Descrizione**

Definisce un ACL del privilegio dell&#39;applicazione.

* `@prop cq:isPathDependent`
* `@node * ACEs`

**Definizione**

* `[cq:PrivilegeAcl] > cq:ApplicationPrivilege mixin orderable`
   * `- cq:isPathDependent (boolean)`
   * `+ * (cq:PrivilegeAce) = cq:PrivilegeAce`

### cq:PrivilegeAce {#cq-privilegeace-1}

**Descrizione**

Definisce un ACE privilegio dell&#39;applicazione.

* `@prop path`
* `@prop deny`

**Definizione**

* `[cq:PrivilegeAce]`
   * `- path mandatory`
   * `- deny (boolean)`

## Importazione siti {#site-importer}

### cq:ComponentExtractorSource {#cq-componentextractorsource}

**Descrizione**

Definisce un tipo mixin che contrassegna i file che possono essere aperti con l&#39;estrattore di componenti.

**Definizione**

`[cq:ComponentExtractorSource] mixin`

## Assegnazione tag {#tagging}

### cq:Tag {#cq-tag}

**Descrizione**

Definisce un singolo tag, ma può anche contenere tag, creando in tal modo una tassonomia

**Definizione**

* `[cq:Tag] > nt:base, mix:title`
   * `- sling:resourceType (String)`
   * `- * (undefined) multiple`
   * `- * (undefined)`
   * `+ * (nt:base) = cq:Tag version`

### cq:Taggable {#cq-taggable}

**Descrizione**

Miscelazione di base astratta per il contenuto variabile.

* `@node cq:tags`

**Definizione**

* `[cq:Taggable]`
   * `- cq:tags (string) multiple`

### cq:OwnerTaggable {#cq-ownertaggable}

**Descrizione**

Solo gli autori/proprietari possono assegnare tag al contenuto (tag moderati/gestiti).

**Definizione**

* `[cq:OwnerTaggable] > cq:Taggable`

### cq:UserTaggable {#cq-usertaggable}

**Descrizione**

Qualsiasi sito web pubblico/utente può assegnare tag al contenuto (stile Web2.0), utilizzato all&#39;interno di cq:userContent.

**Definizione**

* `[cq:UserTaggable] > cq:Taggable`
   * `mixin`

### cq:AllowUserContent {#cq-allowsusercontent}

**Descrizione**

Aggiunge un `cq:userContent` sottonodo che può essere modificato dagli utenti. Ogni utente avrà il proprio `cq:userContent/<userid>` sottonodo, che ha tipicamente il mixin `cq:UserTaggable`.

**Definizione**

* `[cq:AllowsUserContent]`
   * `mixin`
   * `+ cq:userContent (nt:unstructured)`

Variante estesa, che definisce in modo più esplicito la variabile `cq:userContent` albero

* `[cq:AllowsUserContent]`
   * `mixin`
   * `+ cq:userContent (cq:UserContent)`

### cq:UserContent {#cq-usercontent}

**Descrizione**

Può essere modificato dagli utenti.

**Definizione**

* `[cq:UserContent] > nt:unstructured`
   * `// userids`
   * `+ * (cq:UserData)`
   * `// other content`
   * `+ * (nt:base)`

### cq:UserData {#cq-userdata}

**Descrizione**

Dati utente

**Definizione**

* `[cq:UserData] > nt:unstructured, cq:UserTaggable`

## Widget {#widgets}

### cq:ClientLibraryFolder {#cq-clientlibraryfolder}

**Descrizione**

Cartella libreria client

**Definizione**

* `[cq:ClientLibraryFolder] > sling:Folder`
   * `- categories (string) multiple`
   * `- dependencies (string) multiple`

### cq:Widget {#cq-widget}

**Descrizione**

Widget

**Definizione**

* `[cq:Widget] > nt:unstructured orderable`
   * `- xtype (string)`
   * `- name (string)`
   * `- title (string)`
   * `+ items (nt:base) = cq:WidgetCollection copy`

### cq:WidgetCollection {#cq-widgetcollection}

**Descrizione**

Raccolta Widget

**Definizione**

* `[cq:WidgetCollection] > nt:unstructured`
   * `orderable`
   * `+ * (cq:Widget) = cq:Widget copy`

### cq:Dialog {#cq-dialog}

**Descrizione**

Finestra di dialogo

**Definizione**

* `[cq:Dialog] > cq:Widget orderable`

### cq:Panel {#cq-panel}

**Descrizione**

Pannello

**Definizione**

`[cq:Panel] > cq:Widget orderable`

### cq:TabPanel {#cq-tabpanel}

**Descrizione**

Pannello a schede

**Definizione**

* `[cq:TabPanel]` > `cq:Panel orderable`
   * `- activeTab (long)`

### cq:Field {#cq-field}

**Descrizione**

Campo

**Definizione**

* `[cq:Field] > cq:Widget orderable`
   * `- fieldLabel (string)`
   * `- value (string)`
   * `- ignoreData (boolean)`

## Wiki {#wiki}

### wiki:argomento {#wiki-topic}

**Descrizione**

Argomento Wiki

**Definizione**

* `[wiki:Topic] > nt:unstructured, nt:hierarchyNode, mix:versionable, mix:lockable`
   * `+ * (wiki:Topic) version`
   * `+ wiki:attachments (nt:folder) = nt:folder version`
   * `+ wiki:properties (wiki:Properties) = wiki:Properties copy`
   * `- wiki:text (string) mandatory primary`
   * `- wiki:lastModified (date) mandatory`
   * `- wiki:lastModifiedBy (string) mandatory`
   * `- wiki:topicName`
   * `- wiki:topicTitle`
   * `- wiki:lockedBy`
   * `- wiki:logMessage (string)`
   * `- wiki:quietSave (boolean)`

### wiki:Utente {#wiki-user}

**Descrizione**

Utente wiki

**Definizione**

* `[wiki:User] mixin`
   * `- wiki:subscriptions (string) multiple`

### wiki:Proprietà {#wiki-properties}

**Descrizione**

Proprietà Wiki

**Definizione**

* `[wiki:Properties]`
   * `- wiki:isGlobal (boolean)`
   * `- * (undefined)`

## Flusso di lavoro {#workflow}

### cq:Workflow {#cq-workflow}

**Descrizione**

Rappresenta un&#39;istanza di flusso di lavoro.

**Definizione**

* `[cq:Workflow] > nt:base, mix:referenceable`
   * `- modelId (String)`
   * `- modelVersion (String)`
   * `- startTime (Date)`
   * `- endTime (Date)`
   * `- initiator (String)`
   * `- &ast; (undefined)`
   * `- &ast; (undefined) multiple`
   * `- sling:resourceType (String) = "cq/workflow/components/instance" mandatory autocreated`
   * `+ workflowStack (nt:unstructured)`
   * `+ wait (nt:unstructured)`
   * `+ orTab (nt:unstructured)`
   * `+ data (cq:WorkflowData)`
   * `+ history (nt:unstructured)`
   * `+ metaData (nt:unstructured)`
   * `+ workItems (nt:unstructured)`

### cq:WorkItem {#cq-workitem}

**Descrizione**

Elemento di lavoro.

**Definizione**

* `[cq:WorkItem]`
   * `- assignee (String)`
   * `- workflowId (String)`
   * `- nodeId (String)`
   * `- startTime (Date)`
   * `- endTime (Date)`
   * `- dueTime (Date)`
   * `- sling:resourceType (String) = "cq/workflow/components/workitem" mandatory autocreated`
   * `+ metaData (nt:unstructured)`

### cq:Payload {#cq-payload}

**Descrizione**

Payload

**Definizione**

* `[cq:Payload]`
   * `- path (Path)`
   * `- uuid (String)`
   * `- jcr:url (String)`
   * `- binary (Binary)`
   * `- javaObject (String)`
   * `- * (undefined)`
   * `- * (undefined) multiple`

### cq:WorkflowData {#cq-workflowdata}

**Descrizione**

Dati del flusso di lavoro

**Definizione**

* `[cq:WorkflowData]`
   * `- * (undefined)`
   * `- * (undefined) multiple`
   * `+ payload (cq:Payload)`
   * `+ metaData (nt:unstructured) copy`

### cq:WorkflowModel {#cq-workflowmodel}

**Descrizione**

Assegnazione automatica della configurazione del flusso di lavoro. La configurazione seguirà questa struttura qui sotto:
* `workflows`
   * `+ name1`
      * `- cq:path`
      * `- cq:workflowName`
   * `+ workflows (nt:base)`

**Definizione**

* `[cq:WorkflowModel] > nt:base, mix:versionable`
   * `orderable`
   * `- title (String)`
   * `- description (String)`
   * `- sling:resourceType (String) = "cq/workflow/components/model" mandatory autocreated`
   * `+ nodes (nt:unstructured)`
      * `copy`
   * `+ transitions (nt:unstructured)`
      * `copy`
   * `+ metaData (nt:unstructured)`
      * `copy`

### cq:WorkflowNode {#cq-workflownode}

**Descrizione**

nodo del flusso di lavoro

**Definizione**

* `[cq:WorkflowNode] orderable`
   * `- title (String)`
   * `- description (String)`
   * `- maxIdleTime (long)`
   * `- type (String)`
   * `- * (undefined)`
   * `- * (undefined) multiple`
   * `+ metaData (nt:unstructured)`
      * `copy`
   * `+ timeoutConfiguration (nt:unstructured)`
      * `copy`

### cq:WorkflowTransition {#cq-workflowtransition}

**Descrizione**

Transizione del flusso di lavoro

**Definizione**

* `[cq:WorkflowTransition] orderable`
   * `- from (String)`
   * `- to (String)`
   * `- rule (String)`
   * `+ metaData (nt:unstructured)`
      * `copy`

### cq:OrTab {#cq-ortab}

**Descrizione**

Oppure, scheda

**Definizione**

* `[cq:OrTab]`
   * `- workflowId (String) // not compulsory as this node will already be attached to the workflow node`
   * `- nodeId (String)`

### cq:Wait {#cq-wait}

**Descrizione**

Attendi

**Definizione**

* `[cq:Wait]`
   * `- workflowId (String) // not compulsory as this node will be already attached to the workflow node`
   * `- destNodeId (String)`
   * `- fromNodeId (String)`

### cq:WorkflowStack {#cq-workflowstack}

**Descrizione**

Flusso di lavoro

**Definizione**

* `[cq:WorkflowStack]`
   * `- containeeInstanceId (String)`
   * `- parentInstanceId (String)`
   * `- nodeId (String)`

### cq:ProcessStack {#cq-processstack}

**Descrizione**

stack di processi

**Definizione**

* `[cq:ProcessStack]`
   * `- workflowId (String) // not compulsory as this node will be already attached to the workflow node`
   * `- containerWorkflowModelId (String)`
   * `- containerWorkflowNodeId`
   * `- containerWorkflowEndNodeId // still needed (if name already defines that id)`

### cq:WorkflowLauncher {#cq-workflowlauncher}

**Descrizione**

Lancio dei flussi di lavoro

**Definizione**

* `[cq:WorkflowLauncher]`
   * `- nodetype (String)`
   * `- glob (String)`
   * `- eventType (Long)`
   * `- description (String)`
   * `- condition (String)`
   * `- workflow (String)`
   * `- * (undefined)`
   * `- * (undefined) multiple`
