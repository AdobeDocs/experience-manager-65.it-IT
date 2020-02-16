---
title: Configurazione della sincronizzazione di una Live Copy
seo-title: Configurazione della sincronizzazione di una Live Copy
description: Scopri come configurare la sincronizzazione di una Live Copy.
seo-description: Scopri come configurare la sincronizzazione di una Live Copy.
uuid: a5db0bee-a761-4cff-81dc-31b374525f47
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: 6bcf0fcc-481a-4283-b30d-80b517701280
docset: aem65
translation-type: tm+mt
source-git-commit: 4e5e6ef022dc9f083859e13ab9c86b622fc3d46e

---


# Configurazione della sincronizzazione di una Live Copy{#configuring-live-copy-synchronization}

Esegui le operazioni seguenti per controllare come e quando vengono sincronizzate le Live Copy con il relativo contenuto sorgente.

* Stabilisci se le configurazioni di rollout esistenti soddisfano le tue esigenze o se è necessario crearne una o più.
* Specifica le configurazioni di rollout da usare per le Live Copy.

## Configurazioni di rollout installate e personalizzate {#installed-and-custom-rollout-configurations}

Questa sezione fornisce informazioni sulle configurazioni di rollout installate e sulle azioni di sincronizzazione che utilizzano, nonché su come creare configurazioni personalizzate, se richiesto.

### Attivatori di rollout {#rollout-triggers}

Ogni configurazione di rollout utilizza un attivatore (o trigger) di rollout che determina l’esecuzione dell’implementazione. Le configurazioni di rollout possono utilizzare uno dei seguenti attivatori:

* **Al momento del rollout**: quando viene utilizzato il comando **Rollout** nella pagina blueprint oppure il comando **Sincronizza** nella pagina Live Copy.

* **In caso di modifica**: quando la pagina sorgente viene modificata.

* **Al momento dell’attivazione**: quando la pagina sorgente viene attivata.

* **Alla disattivazione**: quando la pagina sorgente viene disattivata.

>[!NOTE]
>
>L’utilizzo dell’attivatore durante la modifica può influire sulle prestazioni. Per ulteriori informazioni, consulta la sezione sulle [best practice per MSM](/help/sites-administering/msm-best-practices.md#onmodify).

### Configurazioni di rollout installate {#installed-rollout-configurations}

Nella tabella seguente sono elencate le configurazioni di rollout che vengono installate con AEM. La tabella contiene le azioni di attivazione e sincronizzazione per ciascuna configurazione di rollout. Se le azioni di configurazione di rollout installate non soddisfano le tue esigenze, puoi [creare una nuova configurazione di rollout](#creating-a-rollout-configuration).

<table>
 <tbody>
  <tr>
   <th>Nome</th>
   <th>Descrizione</th>
   <th>Attivatore</th>
   <th>Azioni di sincronizzazione<br /><br />  vedi anche <a href="#installed-synchronization-actions">Azioni di sincronizzazione installate</a></th>
  </tr>
  <tr>
   <td>Configurazione di rollout standard</td>
   <td>Configurazione di rollout standard che consente di avviare il processo di rollout all’attivazione del rollout ed esegue le seguenti azioni: crea, aggiorna, elimina contenuto e ordina nodi figlio.</td>
   <td>Al momento del rollout</td>
   <td>contentUpdate<br /> contentCopy<br /> contentDelete<br /> referencesUpdate<br /> productUpdate<br /> orderChildren</td>
  </tr>
  <tr>
   <td>Attiva in caso di attivazione Blueprint</td>
   <td>Pubblica la Live Copy quando il sorgente viene pubblicato.</td>
   <td>Al momento dell’attivazione</td>
   <td>targetActivate</td>
  </tr>
  <tr>
   <td>Disattiva in caso di disattivazione Blueprint</td>
   <td>Disattiva la Live Copy quando il sorgente è disattivato.</td>
   <td>Alla disattivazione</td>
   <td>targetDeactivate<br /> </td>
  </tr>
  <tr>
   <td>Invia dopo modifica</td>
   <td><p>Invia il contenuto alla Live Copy quando il sorgente viene modificato.</p> <p>Utilizza questa configurazione di rollout con moderazione, in quanto utilizza l’attivatore In caso di modifica.</p> </td>
   <td>In caso di modifica</td>
   <td>contentUpdate<br /> contentCopy<br /> contentDelete<br /> referencesUpdate<br /> orderChildren<br /> </td>
  </tr>
  <tr>
   <td>Invia dopo modifica (superficiale)</td>
   <td><p>Invia il contenuto alla Live Copy quando la pagina blueprint viene modificata, senza aggiornare i riferimenti (ad esempio per le copie superficiali).</p> <p>Utilizza questa configurazione di rollout con moderazione, in quanto utilizza l’attivatore In caso di modifica.</p> </td>
   <td>In caso di modifica</td>
   <td>contentUpdate<br /> contentCopy<br /> contentDelete<br /> orderChildren</td>
  </tr>
  <tr>
   <td>Promuovi lancio</td>
   <td>Configurazione rollout standard per la promozione di pagine di lanci.</td>
   <td>Al momento del rollout</td>
   <td>contentUpdate<br /> contentCopy<br /> contentDelete<br /> referencesUpdate<br /> orderChildren<br /> markLiveRelationship</td>
  </tr>
  <tr>
   <td>Configurazione di rollout del contenuto di pagina del catalogo</td>
   <td>Applica i modelli pagina da una blueprint del catalogo.</td>
   <td>Al momento del rollout</td>
   <td>contentUpdate<br /> contentCopy<br /> contentDelete<br /> referencesUpdate<br /> productCreateUpdate<br /> orderChildren</td>
  </tr>
  <tr>
   <td>Configurazione di rollout dell’aggiornamento pagina del catalogo</td>
   <td>Applica le proprietà di destinazione da una blueprint del catalogo. Va eseguita dopo la configurazione di rollout del contenuto di pagina del catalogo.</td>
   <td>Al momento del rollout</td>
   <td>catalogRolloutHooks</td>
  </tr>
  <tr>
   <td>Configurazione di rollout pubblicazioni DPS</td>
   <td>Configurazione di rollout della pubblicazione DPS, che consente di avviare il processo di rollout con l’attivatore di rollout, escludendo le proprietà di associazione FolioProducer per il rollout iniziale</td>
   <td>Al momento del rollout</td>
   <td>contentUpdate<br /> contentCopy<br /> contentDelete<br /> referencesUpdate<br /> orderChildren<br /> dpsMetadataFilter</td>
  </tr>
  <tr>
   <td>Configurazione di rollout catalogo Legacy (5.6.0)</td>
   <td>Obsoleto. Utilizza Catalog Generator invece di MSM per i rollout di cataloghi.</td>
   <td>Al momento del rollout</td>
   <td>editProperties</td>
  </tr>
 </tbody>
</table>

### Azioni di sincronizzazione installate {#installed-synchronization-actions}

Nella tabella seguente sono elencate le azioni di sincronizzazione che vengono installate con AEM. If the installed actions do not meet your requirements, you can [Create a New Synchronization Action](/help/sites-developing/extending-msm.md#creating-a-new-synchronization-action).

<table>
 <tbody>
  <tr>
   <th>Nome azione</th>
   <th>Descrizione</th>
   <th>Proprietà<br /> </th>
  </tr>
  <tr>
   <td>contentCopy</td>
   <td>Quando i nodi del sorgente non esistono nella Live Copy, copia i nodi in quest’ultima. <a href="#excluding-properties-and-node-types-from-synchronization">Configurate il servizio</a> di azione Copia contenuto CQ MSM per specificare i tipi di nodo, gli elementi paragrafo e le proprietà pagina da escludere. <br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>contentDelete</td>
   <td><p>Elimina i nodi della Live Copy che non esistono nell'origine. <a href="#excluding-properties-and-node-types-from-synchronization">Configurate il servizio</a> CQ MSM Content Delete Action per specificare i tipi di nodo, gli elementi paragrafo e le proprietà pagina da escludere. </p> </td>
   <td> </td>
  </tr>
  <tr>
   <td>contentUpdate</td>
   <td>Aggiorna il contenuto della Live Copy con le modifiche apportate dal sorgente. <a href="#excluding-properties-and-node-types-from-synchronization">Configurate il servizio</a> Azione aggiornamento contenuto CQ MSM per specificare i tipi di nodo, gli elementi paragrafo e le proprietà pagina da escludere. <br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>editProperties</td>
   <td><p>Modifica le proprietà della Live Copy. La proprietà editMap determina quali proprietà vengono modificate e il loro valore. Il valore della proprietà editMap deve essere nel formato seguente:</p> <p><code>[property_name_1]#[current_value]#</code>[new_value],<br /> <code>[property_name_2]#[current_value]#</code>[new_value],<br /> ... ,<br /> <code>[property_name_n]#[current_value]#</code>[new_value]</p> <p>The <code>current_value</code> and <code>new_value</code> items are regular expressions. <br /> </p> <p>Ad esempio, considera il seguente valore per editMap:</p> <p><code>sling:resourceType#/</code>(contentpage|homepage)#/<br /> mobilecontentpage,<br /> cq:template#/contentpage#/mobilecontentpage</p> <p>Questo valore modifica le proprietà dei nodi della Live Copy nel modo seguente:</p>
    <ul>
     <li>The <code>sling:resourceType</code> properties that are either set to <code>contentpage</code> or to <code>homepage</code> are set to <code>mobilecontentpage.</code></li>
     <li>The <code>cq:template</code> properties that are set to <code>contentpage</code> are set to <code>mobilecontentpage.</code></li>
    </ul> </td>
   <td><p> </p> <p>editMap: (stringa) identifica la proprietà, il valore corrente e il nuovo valore. Per informazioni, consulta la descrizione.<br /> </p> </td>
  </tr>
  <tr>
   <td>notify</td>
   <td>Invia un evento di pagina segnalando che la pagina è stata soggetta a rollout. Per ricevere una notifica, è necessario innanzitutto iscriversi a eventi di rollout.</td>
   <td> </td>
  </tr>
  <tr>
   <td>orderChildren</td>
   <td>Nella Live Copy, ordina gli elementi secondari (nodi), in base all’ordine della blueprint<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>referencesUpdate</td>
   <td><p>Nella Live Copy, questa azione di sincronizzazione aggiorna i riferimenti, ad esempio i link.<br /> Cerca i percorsi nelle pagine Live Copy che puntano a una risorsa all’interno della blueprint. Quando viene trovato un percorso, lo aggiorna per indicare il punto in cui si trova la risorsa correlata all’interno della Live Copy (anziché della blueprint). I riferimenti che hanno destinazioni esterne alla blueprint non vengono modificati.</p> <p><a href="#excluding-properties-and-node-types-from-synchronization">Configurate il servizio</a> Azione aggiornamento riferimenti CQ MSM per specificare i tipi di nodo, gli elementi paragrafo e le proprietà pagina da escludere. </p> </td>
   <td> </td>
  </tr>
  <tr>
   <td>targetVersion</td>
   <td><p>Crea una versione della pagina Live Copy.</p> <p>Questa deve essere l’unica azione di sincronizzazione inclusa in una configurazione di rollout.</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td>targetActivate</td>
   <td><p>Attiva la Live Copy.</p> <p>Questa deve essere l’unica azione di sincronizzazione inclusa in una configurazione di rollout.</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td>targetDeactivate</td>
   <td><p>Disattiva la Live Copy.</p> <p>Questa deve essere l’unica azione di sincronizzazione inclusa in una configurazione di rollout.</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td>workflow</td>
   <td><p>Avvia il flusso di lavoro definito dalla proprietà target (solo per le pagine) e impiega la Live Copy come payload.</p> <p>Il percorso di destinazione è quello del nodo del modello, ad esempio /etc/workflow/models/request_for_activation/jcr:content/model</p> </td>
   <td>target: (stringa) il percorso del modello di flusso di lavoro.<br /> </td>
  </tr>
  <tr>
   <td>mandatory</td>
   <td><p>Imposta l’autorizzazione di diversi ACL nella pagina Live Copy in sola lettura per un determinato gruppo di utenti. I seguenti ACL sono configurati:</p>
    <ul>
     <li>ActionSet.ACTION_NAME_REMOVE</li>
     <li>ActionSet.ACTION_NAME_SET_PROPERTY</li>
     <li>ActionSet.ACTION_NAME_ACL_MODIFY</li>
    </ul> <p>Usa questa azione solo per le pagine.</p> </td>
   <td>target: (stringa) l’ID del gruppo per cui stai impostando le autorizzazioni. <br /> </td>
  </tr>
  <tr>
   <td>mandatoryContent</td>
   <td><p>Imposta l’autorizzazione di diversi ACL nella pagina Live Copy in sola lettura per un determinato gruppo di utenti. I seguenti ACL sono configurati:</p>
    <ul>
     <li>ActionSet.ACTION_NAME_SET_PROPERTY</li>
     <li>ActionSet.ACTION_NAME_ACL_MODIFY</li>
    </ul> <p>Usa questa azione solo per le pagine.</p> </td>
   <td>target: (stringa) l’ID del gruppo per cui stai impostando le autorizzazioni. </td>
  </tr>
  <tr>
   <td>mandatoryStructure</td>
   <td>Imposta l’autorizzazione dell’ACL ActionSet.ACTION_NAME_REMOVE nella pagina Live Copy in sola lettura per un determinato gruppo di utenti. Usa questa azione solo per le pagine.</td>
   <td>target: (stringa) l’ID del gruppo per cui stai impostando le autorizzazioni. </td>
  </tr>
  <tr>
   <td>VersionCopyAction</td>
   <td>Se la pagina blueprint/sorgente è stata pubblicata almeno una volta, crea una pagina Live Copy utilizzando la versione pubblicata. Nota: questa azione è disponibile solo per la creazione di una pagina Live Copy basata su una pagina sorgente pubblicata e non per l’aggiornamento di una pagina Live Copy esistente. </td>
   <td> </td>
  </tr>
  <tr>
   <td>PageMoveAction</td>
   <td><p>PageMoveAction si applica quando una pagina è stata spostata nella blueprint.</p> <p>L’azione copia e non sposta la pagina Live Copy (correlata) dalla posizione prima dello spostamento a quella successiva.</p> <p>PageMoveAction non modifica la pagina Live Copy nella posizione in cui si trovava prima dello spostamento. Di conseguenza, per configurazioni di rollout consecutive, ha lo stato di LiveRelationship privo di Blueprint.</p> <p><a href="#excluding-properties-and-node-types-from-synchronization">Configura il servizio Azione di spostamento di pagine di CQ MSM</a> per specificare i tipi di nodo, gli elementi di paragrafo e le proprietà di pagina da escludere. </p> <p>Questa deve essere l’unica azione di sincronizzazione inclusa in una configurazione di rollout.</p> </td>
   <td><p>prop_referenceUpdate: (booleano) imposta su true per aggiornare i riferimenti. Il valore predefinito è true.</p> <p> </p> </td>
  </tr>
  <tr>
   <td>productCreateUpdate</td>
   <td>Crea o aggiorna le risorse Prodotto all’interno di un catalogo. Questa azione deve essere utilizzata in una delle situazioni seguenti:
    <ul>
     <li>Creazione o rollout di un catalogo (o sezione di catalogo)</li>
     <li>Un utente ripristina l’eredità di sincronizzazione per un componente del prodotto.</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td>markLiveRelationship</td>
   <td>Indica una relazione live per il contenuto creato da un lancio.</td>
   <td> </td>
  </tr>
  <tr>
   <td>catalogRolloutHooks</td>
   <td>Esegue gli hook di rollout specifici per la generazione del catalogo. Chiama i metodi executePageRolloutHooks ed executeProductRolloutHooks del CatalogGenerator.<br />Fai riferimento a com.adobe.cq.commerce.pim.api.CatalogGenerator in AEM Javadocs.</td>
   <td> </td>
  </tr>
  <tr>
   <td>productUpdate</td>
   <td>Aggiornamenti delle pagine dei prodotti in una Live Copy di un catalogo di prodotti</td>
   <td> </td>
  </tr>
 </tbody>
</table>

### Creazione di una configurazione di rollout {#creating-a-rollout-configuration}

Puoi [creare una configurazione di rollout](/help/sites-developing/extending-msm.md#creating-a-new-rollout-configuration) quando quelle installate non soddisfano le tue esigenze applicative:

* [Crea la configurazione di rollout](/help/sites-developing/extending-msm.md#create-the-rollout-configuration).
* [Aggiungi le azioni di sincronizzazione alla configurazione di rollout](/help/sites-developing/extending-msm.md#add-synchronization-actions-to-the-rollout-configuration).

La nuova configurazione di rollout è quindi disponibile quando imposti le configurazioni di rollout su una pagina blueprint o Live Copy.

### Esclusione delle proprietà e dei tipi di nodo dalla sincronizzazione {#excluding-properties-and-node-types-from-synchronization}

Puoi configurare diversi servizi OSGi che supportano le azioni di sincronizzazione corrispondenti in modo che non influiscano su proprietà e tipi di nodo specifici. Ad esempio, molte proprietà e sottonodi relativi al funzionamento interno di AEM non devono essere inclusi in una Live Copy. Deve essere copiato solo il contenuto rilevante all’utente della pagina.

When working with AEM there are several methods of managing the configuration settings for such services; see [Configuring OSGi](/help/sites-deploying/configuring-osgi.md) for more details and the recommended practices.

Nella tabella seguente sono elencate le azioni di sincronizzazione per le quali è possibile specificare i nodi da escludere. La tabella fornisce i nomi dei servizi da configurare mediante la Console web e il PID per la configurazione mediante un nodo di archivio.

| Azione sincronizzazione | Nome servizio nella console Web | Service PID |
|---|---|---|
| contentCopy | Azione Copia contenuto CQ MSM | com.day.cq.wcm.msm.impl.actions.ContentCopyActionFactory |
| contentDelete | Azione di eliminazione contenuto CQ MSM | com.day.cq.wcm.msm.impl.actions.ContentDeleteActionFactory |
| contentUpdate | Azione aggiornamento contenuto CQ MSM | com.day.cq.wcm.msm.impl.actions.ContentUpdateActionFactory |
| PageMoveAction | Azione di spostamento pagina CQ MSM | com.day.cq.wcm.msm.impl.actions.PageMoveActionFactory |
| referencesUpdate | Azione aggiornamento riferimenti MSM CQ | com.day.cq.wcm.msm.impl.actions.ReferencesUpdateActionFactory |

La tabella seguente descrive le proprietà che puoi configurare:

<table>
 <tbody>
  <tr>
   <th>Proprietà console Web / proprietà OSGi</th>
   <th>Descrizione</th>
  </tr>
  <tr>
   <td><p>Nodetype esclusi</p> <p>cq.wcm.msm.action.excludednodetypes</p> </td>
   <td>Un'espressione regolare che corrisponde ai tipi di nodo da escludere dall'azione di sincronizzazione.</td>
  </tr>
  <tr>
   <td><p>Elementi paragrafo esclusi</p> <p>cq.wcm.msm.action.excludedParagraphItems</p> </td>
   <td>Un'espressione regolare che corrisponde agli elementi paragrafo da escludere dall'azione di sincronizzazione.</td>
  </tr>
  <tr>
   <td><p>Proprietà pagina escluse</p> <p>cq.wcm.msm.action.Excludedprops</p> </td>
   <td>Un'espressione regolare che corrisponde alle proprietà della pagina da escludere dall'azione di sincronizzazione.</td>
  </tr>
  <tr>
   <td><p>Tipi di nodo misti ignorati</p> <p>cq.wcm.msm.action.IgnoreMixin</p> </td>
   <td>Disponibile solo per CQ MSM Content Update Action. Un’espressione regolare che corrisponde ai nomi del nodo Mixin che devono essere esclusi dall’azione di sincronizzazione.</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Nell’interfaccia utente classica, l’icona di blocco visualizzata nella finestra di dialogo Proprietà di pagina per le pagine Live Copy non riflette la configurazione della proprietà Proprietà pagina escluse. L’icona di blocco viene visualizzata anche per le proprietà escluse dall’azione di sincronizzazione.

>[!NOTE]
>
>Nell’interfaccia utente ottimizzata per touch, vedi anche [Configurazione dei blocchi MSM nelle proprietà di pagina (interfaccia utente ottimizzata per touch)](/help/sites-developing/extending-msm.md#configuring-msm-locks-on-pagep-roperties-touch-optimized-ui).

#### Azione di aggiornamento dei contenuti di CQ MSM - Esclusioni {#cq-msm-content-update-action-exclusions}

Diverse proprietà e tipi di nodo sono esclusi per impostazione predefinita; essi sono definiti nella configurazione OSGi dell’**Azione di aggiornamento dei contenuti di CQ MSM**, in **Proprietà pagina escluse**.

Per impostazione predefinita, le proprietà che corrispondono alle seguenti espressioni regolari vengono escluse (ovvero non aggiornate) durante il rollout:

![chlimage_1](assets/chlimage_1.png)

Puoi modificare le espressioni che definiscono l’elenco di esclusione secondo le tue esigenze.

Ad esempio, se desideri includere il **Titolo** della pagina nelle modifiche considerate per il rollout, rimuovi `jcr:title` dalle esclusioni. Ad esempio, con il codice regex:

`jcr:(?!(title)$).*`

>[!CAUTION]
>
>Prima della versione 5.5 SP2, le proprietà pagina escluse venivano configurate nella console di sistema in **Day CQ WCM Rollout Manager**. A partire dalla versione 5.5 SP2, le impostazioni delle proprietà delle pagine escluse all’interno di tale pannello vengono ignorate. Property exclusion on rollout is configured as described above, in **CQ MSM Content Update Action**.
>
>Pertanto, se hai modificato manualmente questa impostazione in un’installazione precedente alla versione 5.5 SP2 e stai effettuando l’aggiornamento alla versione 5.5 SP2 o successiva, *devi trasferire manualmente queste impostazioni dal vecchio pannello di configurazione a quello nuovo*.

### Configurazione della sincronizzazione per l’aggiornamento dei riferimenti {#configuring-synchronization-for-updating-references}

Puoi configurare diversi servizi OSGi che supportano le azioni di sincronizzazione corrispondenti, relative all’aggiornamento dei riferimenti.

When working with AEM there are several methods of managing the configuration settings for such services; see [Configuring OSGi](/help/sites-deploying/configuring-osgi.md) for more details and the recommended practices.

Nella tabella seguente sono elencate le azioni di sincronizzazione per cui è possibile specificare l’aggiornamento dei riferimenti. La tabella fornisce i nomi dei servizi da configurare mediante la Console web e il PID per la configurazione mediante un nodo di archivio.

<table>
 <tbody>
  <tr>
   <th>Proprietà console Web / proprietà OSGi</th>
   <th>Descrizione</th>
  </tr>
  <tr>
   <td><p>Riferimento aggiornamento tra LiveCopy nidificate</p> <p>cq.wcm.msm.impl.action.referencesupdate.prop_updateNested</p> </td>
   <td>Disponibile solo per l'azione di aggiornamento riferimenti MSM CQ. Selezionare questa opzione (Console Web) o impostare questa proprietà booleana su true (configurazione archivio) per sostituire i riferimenti per qualsiasi risorsa all'interno del ramo della LiveCopy superiore.</td>
  </tr>
  <tr>
   <td><p>Aggiorna pagine di riferimento</p> <p>cq.wcm.msm.impl.actions.pagemove.prop_referenceUpdate</p> </td>
   <td>Disponibile solo per CQ MSM Page Move Action. Select this option (Web Console) or set this boolean property to <code>true</code> (repository configuration) to update any references to use the original page to instead reference the LiveCopy page.</td>
  </tr>
 </tbody>
</table>

## Specifica delle configurazioni di rollout da utilizzare {#specifying-the-rollout-configurations-to-use}

MSM ti consente di specificare i set di configurazioni di rollout che vengono utilizzate generalmente e, quando è necessario, puoi sostituirle per specifiche Live Copy. MSM fornisce diverse posizioni per specificare le configurazioni di rollout da utilizzare. La posizione determina se la configurazione viene applicata a una Live Copy specifica.

Il seguente elenco di posizioni, in cui puoi specificare le configurazioni di rollout da utilizzare, descrive come MSM determina quali configurazioni di rollout utilizzare per una Live Copy:

* **[Proprietà di pagina della Live Copy](/help/sites-administering/msm-sync.md#setting-the-rollout-configurations-for-a-live-copy-page):**quando una pagina Live Copy è configurata per l’utilizzo di una o più configurazioni di rollout, MSM utilizza tali configurazioni di rollout.
* **[Proprietà di pagina blueprint](/help/sites-administering/msm-sync.md#setting-the-rollout-configuration-for-a-blueprint-page):**quando una Live Copy è basata su una blueprint e la pagina Live Copy non è configurata con una configurazione di rollout, viene utilizzata la configurazione di rollout associata alla pagina blueprint sorgente.
* **** Proprietà pagina padre Live Copy: Quando né la pagina Live Copy né la pagina origine blueprint sono configurate con una configurazione di rollout, viene utilizzata la configurazione di rollout applicata alla pagina padre della pagina Live Copy.
* **[](/help/sites-administering/msm-sync.md#setting-the-system-default-rollout-configuration)Valore predefinito **del sistema: Quando non è possibile determinare la configurazione di rollout della pagina padre della Live Copy, viene utilizzata la configurazione di rollout predefinita del sistema.

Ad esempio, una blueprint utilizza il sito di riferimento We.Retail come contenuto sorgente. Un sito viene creato dalla blueprint. Ogni voce dell’elenco seguente descrive uno scenario diverso rispetto all’uso delle configurazioni di rollout:

* Nessuna delle pagine blueprint o delle Live Copy è configurata per l’utilizzo di una configurazione di rollout. MSM utilizza la configurazione di rollout predefinita del sistema per tutte le pagine Live Copy.
* La pagina principale del sito di riferimento We.Retail è configurata con diverse configurazioni di rollout. MSM utilizza queste configurazioni di rollout per tutte le pagine Live Copy.
* La pagina principale del sito di riferimento We.Retail è configurata con diverse configurazioni di rollout e la pagina principale del sito di live copy è configurata con un set diverso di configurazioni di rollout. MSM utilizza le configurazioni di rollout che sono configurate nella pagina principale del sito Live Copy.

### Impostazione delle configurazioni di rollout per una pagina Live Copy {#setting-the-rollout-configurations-for-a-live-copy-page}

Configura una pagina Live Copy con le configurazioni di rollout da utilizzare quando la pagina sorgente è soggetta a rollout. Per impostazione predefinita, le pagine secondarie ereditano la configurazione. Quando imposti la configurazione di rollout da utilizzare, sovrascrivi di fatto la configurazione che la pagina Live Copy eredita dalla sua pagina padre.

Puoi anche impostare le configurazioni di rollout per una pagina Live Copy quando [crei la Live Copy](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-page).

1. Utilizza la console **Sites** per selezionare la pagina Live Copy.
1. Seleziona **Proprietà** nella barra degli strumenti.
1. Apri la scheda **Live Copy.**

   La sezione **Configurazione** mostra le configurazioni di rollout ereditate dalla pagina.

   ![chlimage_1-1](assets/chlimage_1-1.png)

1. Se necessario, regola il flag **Ereditarietà Live Copy**. Se è selezionato, la configurazione Live Copy ha effetto su tutti gli elementi figlio.

1. Deseleziona la proprietà **Eredita configurazione rollout da padre**, quindi seleziona una o più configurazioni di rollout dall’elenco.

   Le configurazioni di rollout selezionate vengono visualizzate nell’elenco a discesa.

   ![chlimage_1-2](assets/chlimage_1-2.png)

1. Tocca o fai clic su **Salva**.

### Impostazione della configurazione di rollout per una pagina blueprint {#setting-the-rollout-configuration-for-a-blueprint-page}

Configura una pagina blueprint con le configurazioni di rollout da utilizzare quando la pagina blueprint è soggetta a rollout.

Considera che le pagine secondarie della pagina blueprint ereditano la configurazione. Quando imposti la configurazione di rollout da utilizzare, potresti sovrascrivere la configurazione che la pagina eredita dal sua pagina padre.

1. Utilizza la console **Sites** per selezionare la pagina principale della blueprint.
1. Seleziona **Proprietà** nella barra degli strumenti.
1. Apri la scheda **Blueprint.**
1. Seleziona una o più **Configurazioni di rollout** con il selettore a discesa.
1. Per confermare gli aggiornamenti, seleziona **Salva**.

### Impostazione della configurazione di rollout predefinita del sistema {#setting-the-system-default-rollout-configuration}

Specifica una configurazione di rollout da usare come predefinita del sistema. Per specificare il valore predefinito, configura il servizio OSGi:

* **Day CQ WCM Live Relationship Manager**:  il PID del servizio è `com.day.cq.wcm.msm.impl.LiveRelationshipManagerImpl`

Configura il servizio utilizzando la [Console web](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) o un [nodo di archivio](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository).

* Nella console web, il nome della proprietà da configurare è: Default rollout config (Configurazione rollout predefinita).
* Using a repository node, the name of the property to configure is `liverelationshipmgr.relationsconfig.default`.

Imposta il valore di questa proprietà sul percorso della configurazione di rollout da utilizzare come impostazione predefinita del sistema. The default value is `/etc/msm/rolloutconfigs/default`, which is the **Standard Rollout Config**.
