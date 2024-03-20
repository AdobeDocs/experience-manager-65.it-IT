---
title: Tipi di nodo personalizzati
description: Adobe Experience Manager (AEM) è basato su Sling e utilizza un archivio JCR con tipi di nodo offerti da entrambi, ma AEM fornisce anche una serie di tipi di nodo personalizzati
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
exl-id: bfd50aa9-579e-47d5-997d-ec764c782497
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1848'
ht-degree: 5%

---

# Tipi di nodo personalizzati{#custom-node-types}

Poiché Adobe Experience Manager (AEM) è basato su Sling e utilizza un archivio JCR, i tipi di nodo offerti da entrambi sono disponibili per l’utilizzo:

* [Tipi di nodo JCR](https://developer.adobe.com/experience-manager/reference-materials/spec/jcr/2.0/3_Repository_Model.html#3.1.7-Node-Types)
* [Tipi di nodo Sling](https://cwiki.apache.org/confluence/display/SLING/Sling+Node+Types)

Oltre a questi tipi di nodo, l’AEM fornisce una serie di tipi di nodo personalizzati.

## Audit {#audit}

### cq:AuditEvent {#cq-auditevent}

**Descrizione**

Definisce il tipo di nodo di un nodo evento di audit.

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

### cq:Comment {#cq-comment}

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

Definisce il tipo di nodo di una `commentattachment` nodo

**Definizione**

* `[cq:CommentAttachment] > nt:file`
   * `- * (undefined)`
   * `- * (undefined) multiple`

### cq:CommentContent {#cq-commentcontent}

**Descrizione**

Definisce il tipo di nodo di un nodo di contenuto commento

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

* `@prop latitude` - latitudine codificata come doppia utilizzando i gradi decimali
* `@prop longitude` - longitudine codificata come doppio utilizzando i gradi decimali

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

Definisce un tipo mixin che contrassegna i nodi come pseudo-pagine. In altre parole, possono essere adattate per il supporto di modifica di pagine e WCM.

**Definizione**

* `[cq:PseudoPage] mixin`

### cq:PageContent {#cq-pagecontent}

**Descrizione**

Definisce il nodo predefinito per il contenuto della pagina, con le proprietà minime utilizzate da WCM.

* `@prop jcr:title` - Titolo della pagina.
* `@prop jcr:description` - Descrizione della pagina.
* `@prop cq:template` : percorso del modello utilizzato per creare la pagina.
* `@prop cq:allowedTemplates` - Elenco di espressioni regolari utilizzate per determinare i percorsi del modello consentito.
* `@prop pageTitle` - Titolo visualizzato nella `<title>` tag.
* `@prop navTitle` - Titolo utilizzato nella navigazione.
* `@prop hideInNav` - Specifica se la pagina deve essere nascosta nella navigazione.
* `@prop onTime` - Ora di validità della pagina.
* `@prop offTime` - Ora in cui la pagina non è più valida.
* `@prop cq:lastModified` - Data dell’ultima modifica della pagina (o dei suoi paragrafi).
* `@prop cq:lastModifiedBy` - Ultimo utente a modificare la pagina (o i relativi paragrafi).
* `@prop jcr:language` : lingua del contenuto della pagina.

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
* `@node icon.png` : file contenente un’icona caratteristica.
* `@node thumbnail.png` - File contenente una miniatura caratteristica.
* `@node workflows` - Configurazione del flusso di lavoro con assegnazione automatica. La configurazione segue la struttura seguente:
   * `+ workflows`
      * `+ name1`
         * `- cq:path`
            * `- cq:workflowName`
* `@prop allowedParents` - Modelli di espressioni regolari per determinare i percorsi ai modelli consentiti come modelli principali.
* `@prop allowedChildren` - Modelli di espressioni regolari per determinare i percorsi ai modelli consentiti come modelli secondari.
* `@prop ranking` : posizione all’interno dell’elenco dei modelli nella finestra di dialogo crea pagina.

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
* `@prop dialogPath` - Percorso della finestra di dialogo primaria (alternativa alla finestra di dialogo).
* `@node design_dialog` - Finestra di dialogo per progettazione.
* `@prop cq:cellName` - Nome della cella di progettazione.
* `@prop cq:isContainer` - Indica se si tratta di un componente contenitore. Forza l&#39;utilizzo dei nomi di cella dei componenti figlio al posto dei nomi di percorso. Ad esempio, il `parsys` è un componente contenitore. Se questo valore non è definito, il controllo viene eseguito in base all&#39;esistenza di un `cq:childEditConfig`.
* `@prop cq:noDecoration` - Se è vero, nessuna decorazione `div` I tag vengono disegnati quando si include questo componente.
* `@node cq:editConfig` : configurazione che definisce i parametri per la barra di modifica.
* `@node cq:childEditConfig` : configurazione di modifica ereditata dai componenti figlio.
* `@node cq:htmlTag` - Definisce gli attributi di tag aggiuntivi aggiunti al &quot;circostante&quot; `div` quando il componente è incluso.
* `@node icon.png`: file contenente un’icona caratteristica.
* `@node thumbnail.png` - File contenente una miniatura caratteristica.
* `@prop allowedParents` - Modelli di espressioni regolari per determinare i percorsi di componenti consentiti come componenti principali.
* `@prop allowedChildren` - Modelli di espressioni regolari per determinare i percorsi di componenti consentiti come componenti figlio.
* `@node virtual` : contiene sottonodi che riflettono i componenti virtuali utilizzati per il trascinamento e il rilascio dei componenti.
* `@prop componentGroup` - Nome del gruppo di componenti, utilizzato per il trascinamento e il rilascio del componente.
* `@node cq:infoProviders` - Contiene sottonodi, ciascuno dei quali ha una proprietà `className` che si riferisce a un `PageInfoProvider`.

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

Definisce la configurazione della &quot;barra di modifica&quot;.

* `@prop cq:dialogMode` - Modalità del dialogo:
   * `floating` - per una normale finestra di dialogo mobile
   * `inline` - modifica in linea
   * `auto` - rilevamento automatico (a seconda dello spazio disponibile)
* `@node cq:inplaceEditing` : configurazione della modifica locale per questo componente.
* `@prop cq:layout`- Layout della barra di modifica:
   * `editbar` - barra di modifica
   * `rollover` - frame di rollover
   * `auto` - rilevamento automatico
* `@node cq:formParameters`- Parametri aggiuntivi da aggiungere al modulo della finestra di dialogo.
* `@prop cq:actions`- Elenco di azioni (pulsanti della barra di modifica o voci di menu).
* `@node cq:actionConfigs` - Configurazioni dei widget per le voci della barra di modifica o del menu.
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

Configura una destinazione di rilascio di un componente. Il nome di questo nodo viene utilizzato come ID per il trascinamento.

* `@prop accept` - Elenco dei tipi MIME accettati da questo drop target; ad esempio, `["image/*"]`
* `@prop groups` - Elenco dei gruppi di trascinamento che accettano un&#39;origine.
* `@prop propertyName` - Nome della proprietà utilizzata per memorizzare il riferimento.

**Definizione**

* `[cq:DropTargetConfig] > nt:unstructured orderable`
   * `- accept (string) multiple`
   * `- groups (string) multiple`
   * `- propertyName (string)`
   * `+ parameters (nt:base) = nt:unstructured`

### cq:VirtualComponent {#cq-virtualcomponent}

**Descrizione**

Definisce un componente CQ virtuale. Attualmente utilizzato solo per la procedura guidata di trascinamento del nuovo componente.

* `@prop jcr:title` - Titolo del componente.
* `@prop jcr:description` - Descrizione del componente.
* `@node cq:editConfig` - Modifica la configurazione che definisce i parametri per la barra di modifica.
* `@node cq:childEditConfig`: modifica la configurazione ereditata dai componenti figlio.
* `@node icon.png` : file contenente un’icona caratteristica.
* `@node thumbnail.png` - File contenente una miniatura caratteristica.
* `@prop allowedParents` - Modelli di espressioni regolari per determinare i percorsi di componenti consentiti come componenti principali.
* `@prop allowedChildren` - Modelli di espressioni regolari per determinare i percorsi di componenti consentiti come componenti figlio.
* `@prop componentGroup` - Nome del gruppo di componenti da trascinare.

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

Definisce i listener (lato client) da eseguire su un evento di modifica. I valori devono fare riferimento a una funzione listener lato client valida o contenere un collegamento predefinito:

* `REFRESH_PAGE`
* `REFRESH_SELF`
* `REFRESH_PARENT`

* `@prop aftercreate` : viene attivato dopo la creazione di un componente.
* `@prop afteredit` - Generato dopo la modifica di un componente (modificato).
* `@prop afterdelete` - Generato dopo l&#39;eliminazione di un componente.
* `@prop afterinsert` : viene attivato dopo l&#39;aggiunta di un componente a questo contenitore.
* `@prop afterremove` - Generato dopo la rimozione di un componente dal contenitore.
* `@prop aftermove` - Generato dopo lo spostamento dei componenti in questo contenitore.

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

### dam:Thumbnail {#dam-thumbnail}

**Descrizione**

Miniatura per rappresentare una risorsa DAM.

**Definizione**

* `[dam:Thumbnails]`
   * `mixin`
   * `+ dam:thumbnails (nt:folder)`

## Elenco dei contenitori di consegna {#delivery-container-list}

### cq:containerList {#cq-containerlist}

**Descrizione**

Elenco dei contenitori.

**Definizione**

* `[cq:containerList]`
   * `mixin`

## Pagina di consegna {#delivery-page}

### cq:Cq4PageAttributes {#cq-cq-pageattributes}

**Descrizione**

Tipo di nodo `cq:attributes` è per i tag di versione ContentBus. Questo nodo ha solo una serie di proprietà; di queste tre sono predefinite, &quot;created&quot;, &quot;csd&quot; e &quot;timestamp&quot;.

* `@prop created (long) mandatory copy` - Timestamp della creazione delle informazioni sulla versione, in genere l’ora di archiviazione della versione precedente o l’ora di creazione della pagina.
* `@prop csd (string) mandatory copy` : attributo standard csd, copia della proprietà cq:csd del nodo della pagina
* `@prop timestamp (long) mandatory copy` - Timestamp dell’ultima modifica della versione, in genere ora di archiviazione.
* `@prop * (string) copy` - Attributi aggiuntivi, con versione del nodo principale.

**Definizione**

* `[cq:Cq4PageAttributes] > nt:base`
   * `- created (long) mandatory copy`
   * `- csd (string) mandatory copy`
   * `- timestamp (long) mandatory copy`
   * `- &ast; (string) copy`

### cq:Cq4ContentPage {#cq-cq-contentpage}

**Descrizione**

Tipo di nodo `cq:contentPage` contiene le definizioni di proprietà e nodi figlio per le pagine di contenuto ContentBus. Solo quando questo tipo mixin viene aggiunto a un nodo di tipo `cq:page`, un nodo diventa una pagina di contenuto ContentBus.

Gli elementi in una `cq:Cq4ContentPage` sono:

* `@prop cq:csd` - il CSD del ContentBus della pagina.
* `@node cq:content` - Il contenuto della pagina. Questo nodo secondario non esiste se il nodo della pagina si trova nello stato &quot;Esistente senza contenuto&quot; o &quot;Eliminato&quot;.
* `@node cq:attributes` : l’elenco degli attributi della pagina, precedentemente noti come tag di versione. Questo nodo è obbligatorio per il tipo cq:contentPage. Quando viene creata una versione della pagina, nel nodo degli attributi viene creata una versione.

**Definizione**

* `[cq:Cq4ContentPage]`
   * `- cq:csd (string) mandatory copy`
   * `+ cq:attributes (cq:Cq4PageAttributes)`

## Importazione {#importer}

### cq:PollConfig {#cq-pollconfig}

**Descrizione**

Configurazione sondaggio.

* `@prop source (String) mandatory` - URI origine dati. Obbligatorio e non può essere vuoto.
* `@prop target (String)` : il percorso di destinazione in cui vengono memorizzati i dati recuperati dall’origine dati. Facoltativo e viene impostato automaticamente sul nodo cq:PollConfig.
* `@prop interval (Long)` : l’intervallo in secondi in cui eseguire il polling per dati nuovi o aggiornati dall’origine dati. Facoltativo e il valore predefinito è 30 minuti (1800 secondi).
* [Creazione di servizi di importazione dati personalizzati per Adobe Experience Manager](https://helpx.adobe.com/experience-manager/using/polling.html)

**Definizione**

* `[cq:PollConfig]`
   * `mixin`
   * `- source (String) mandatory`
   * `- target (String)`
   * `- interval (Long)`

### cq:PollConfigFolder {#cq-pollconfigfolder}

**Descrizione**

Comodità del tipo di nodo principale per creare facilmente nodi di configurazione polling.

**Definizione**

`[cq:PollConfigFolder] > sling:Folder, cq:PollConfig`

## Dove si trova {#location}

### cq:GeoLocation {#cq-geolocation-1}

**Descrizione**

Un mixin che definisce una posizione geografica in gradi decimali (DD).

* `@prop latitude` - Latitudine codificata come doppia utilizzando i gradi decimali.
* `@prop longitude` - Longitudine codificata come doppia utilizzando i gradi decimali.

**Definizione**

* `[cq:GeoLocation]`
   * `mixin`
   * `- latitude (double)`
   * `- longitude (double)`

## Mailer {#mailer}

### cq:mailerMessage {#cq-mailermessage}

**Descrizione**

Tipi di nodo MailerService. Il mailer utilizza nodi che hanno questo mixin come nodi principali delle definizioni dei messaggi.

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

Definisce un mixin LiveSync. Se un nodo è coinvolto in una LiveRelationship con un nodo sorgente principale (di controllo) e un nodo Live Copy (controllato), viene contrassegnato come LiveSync.

* `@prop cq:master` : percorso della sorgente primaria (che controlla) della LiveRelationship.
* `@prop cq:isDeep` - Definisce se la relazione è disponibile per gli elementi figlio.
* `@prop cq:syncTrigger` - Definisce quando viene attivata la sincronizzazione.
* `@node * LiveSyncAction` - Azioni da eseguire alla sincronizzazione

**Definizione**

`[cq:LiveSync] > cq:LiveRelationship mixin orderable`
`+ * (cq:LiveSyncAction) = cq:LiveSyncAction`
`+ cq:LiveSyncConfig (nt:base) = cq:LiveSyncConfig`

### cq:LiveSyncCanceled {#cq-livesynccancelled}

**Descrizione**

Definisce un mixin LiveSyncCanceled. Annulla il comportamento LiveSync di un nodo Live Copy (controllato) che potrebbe essere coinvolto in una LiveRelationship a causa di uno dei suoi nodi principali.

* `@prop cq:isCancelledForChildren` - Definisce se un LiveSync viene annullato; anche per gli elementi figlio.

**Definizione**

* `[cq:LiveSyncCancelled] > cq:LiveRelationship mixin`
   * `- cq:isCancelledForChildren (boolean)`

### cq:LiveSyncAction {#cq-livesyncaction}

**Descrizione**

Definisce un elemento LiveSyncAction associato a un elemento LiveSync.

* `@prop name` - Nome azione
* `@prop value` - Valore azione

**Definizione**

* `[cq:LiveSyncAction] > nt:unstructured`

### cq:LiveSyncConfig {#cq-livesyncconfig}

**Descrizione**

Configurazione Live Sync.

**Definizione**

* `[cq:LiveSyncConfig]`
   * `- cq:master (string) mandatory`
   * `- cq:isDeep (boolean)`
   * `- cq:trigger (string) /** deprecated **/`

Per AEM 5.4 aggiungere alla fine dell’elenco:

* `- cq:rolloutConfigs (string) multiple /** deprecated **/`

### cq:BlueprintAction {#cq-blueprintaction}

**Descrizione**

Azione blueprint

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

Definisce il mixin delle informazioni sullo stato della replica.

* `@prop cq:lastPublished`- Data dell’ultima pubblicazione della pagina (non più utilizzata).
* `@prop cq:lastPublishedBy`: l’ultimo utente che ha pubblicato la pagina (non più utilizzato).
* `@prop cq:lastReplicated` : data dell’ultima replica della pagina.
* `@prop cq:lastReplicatedBy` : l’ultimo utente che ha replicato la pagina.
* `@prop cq:lastReplicationAction` - Azione di replica: attiva o disattiva.
* `@prop cq:lastReplicationStatus` : stato della replica (non più utilizzato).

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

Definisce un ACL di privilegio applicazione.

* `@prop cq:isPathDependent`
* `@node * ACEs`

**Definizione**

* `[cq:PrivilegeAcl] > cq:ApplicationPrivilege mixin orderable`
   * `- cq:isPathDependent (boolean)`
   * `+ * (cq:PrivilegeAce) = cq:PrivilegeAce`

### cq:PrivilegeAce {#cq-privilegeace}

**Descrizione**

Definisce un ACE privilegio applicazione.

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

Definisce un ACL di privilegio applicazione.

* `@prop cq:isPathDependent`
* `@node * ACEs`

**Definizione**

* `[cq:PrivilegeAcl] > cq:ApplicationPrivilege mixin orderable`
   * `- cq:isPathDependent (boolean)`
   * `+ * (cq:PrivilegeAce) = cq:PrivilegeAce`

### cq:PrivilegeAce {#cq-privilegeace-1}

**Descrizione**

Definisce un ACE privilegio applicazione.

* `@prop path`
* `@prop deny`

**Definizione**

* `[cq:PrivilegeAce]`
   * `- path mandatory`
   * `- deny (boolean)`

## Importazione siti {#site-importer}

### cq:ComponentExtractorSource {#cq-componentextractorsource}

**Descrizione**

Definisce un tipo mixin che contrassegna i file che possono essere aperti con l’estrattore di componenti.

**Definizione**

`[cq:ComponentExtractorSource] mixin`

## Assegnazione dei tag {#tagging}

### cq:Tag {#cq-tag}

**Descrizione**

Definisce un singolo tag, ma può anche contenere tag, creando così una tassonomia

**Definizione**

* `[cq:Tag] > nt:base, mix:title`
   * `- sling:resourceType (String)`
   * `- * (undefined) multiple`
   * `- * (undefined)`
   * `+ * (nt:base) = cq:Tag version`

### cq:Taggable {#cq-taggable}

**Descrizione**

Mixin di base astratto per contenuti con tag.

* `@node cq:tags`

**Definizione**

* `[cq:Taggable]`
   * `- cq:tags (string) multiple`

### cq:OwnerTaggable {#cq-ownertaggable}

**Descrizione**

Solo gli autori/proprietari possono assegnare tag al contenuto (tag moderati/amministrati).

**Definizione**

* `[cq:OwnerTaggable] > cq:Taggable`

### cq:UserTaggable {#cq-usertaggable}

**Descrizione**

Qualsiasi utente/sito web pubblico può assegnare tag al contenuto (stile Web2.0), utilizzato all’interno di cq:userContent.

**Definizione**

* `[cq:UserTaggable] > cq:Taggable`
   * `mixin`

### cq:AllowsUserContent {#cq-allowsusercontent}

**Descrizione**

Aggiunge un `cq:userContent` sottonodo che può essere modificato dagli utenti. Ogni utente ha il proprio `cq:userContent/<userid>` sottonodo, che in genere ha il mixin `cq:UserTaggable`.

**Definizione**

* `[cq:AllowsUserContent]`
   * `mixin`
   * `+ cq:userContent (nt:unstructured)`

Variante estesa, che definisce più esplicitamente la `cq:userContent` albero

* `[cq:AllowsUserContent]`
   * `mixin`
   * `+ cq:userContent (cq:UserContent)`

### cq:UserContent {#cq-usercontent}

**Descrizione**

Può essere modificata dagli utenti.

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

Insieme Widget

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

### wiki:Argomento {#wiki-topic}

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

Proprietà wiki

**Definizione**

* `[wiki:Properties]`
   * `- wiki:isGlobal (boolean)`
   * `- * (undefined)`

## Flusso di lavoro {#workflow}

### cq:Workflow {#cq-workflow}

**Descrizione**

Rappresenta un&#39;istanza del flusso di lavoro.

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

Dati flusso di lavoro

**Definizione**

* `[cq:WorkflowData]`
   * `- * (undefined)`
   * `- * (undefined) multiple`
   * `+ payload (cq:Payload)`
   * `+ metaData (nt:unstructured) copy`

### cq:WorkflowModel {#cq-workflowmodel}

**Descrizione**

Configurazione del flusso di lavoro con assegnazione automatica. La configurazione segue questa struttura:
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

Nodo flusso di lavoro

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

Scheda Oppure

**Definizione**

* `[cq:OrTab]`
   * `- workflowId (String) // not compulsory as this node will already be attached to the workflow node`
   * `- nodeId (String)`

### cq:Wait {#cq-wait}

**Descrizione**

Attendere

**Definizione**

* `[cq:Wait]`
   * `- workflowId (String) // not compulsory as this node will be already attached to the workflow node`
   * `- destNodeId (String)`
   * `- fromNodeId (String)`

### cq:WorkflowStack {#cq-workflowstack}

**Descrizione**

Stack di flussi di lavoro

**Definizione**

* `[cq:WorkflowStack]`
   * `- containeeInstanceId (String)`
   * `- parentInstanceId (String)`
   * `- nodeId (String)`

### cq:ProcessStack {#cq-processstack}

**Descrizione**

Stack di processi

**Definizione**

* `[cq:ProcessStack]`
   * `- workflowId (String) // not compulsory as this node will be already attached to the workflow node`
   * `- containerWorkflowModelId (String)`
   * `- containerWorkflowNodeId`
   * `- containerWorkflowEndNodeId // still needed (if name already defines that id)`

### cq:WorkflowLauncher {#cq-workflowlauncher}

**Descrizione**

Modulo di avvio flusso di lavoro

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
