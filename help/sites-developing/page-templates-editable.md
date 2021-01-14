---
title: Modelli di pagina - Modificabili
seo-title: Modelli di pagina - Modificabili
description: Sono stati introdotti modelli modificabili per consentire agli utenti non sviluppatori di creare e modificare modelli, fornire modelli che mantengano una connessione dinamica a qualsiasi pagina da essi creata e rendere il componente pagina più generico
seo-description: Sono stati introdotti modelli modificabili per consentire agli utenti non sviluppatori di creare e modificare modelli, fornire modelli che mantengano una connessione dinamica a qualsiasi pagina da essi creata e rendere il componente pagina più generico
uuid: 61791960-fdef-4e49-878a-11fdf1d4f0ab
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 1099cc44-de6d-499e-8b52-f2f5811ae086
docset: aem65
translation-type: tm+mt
source-git-commit: 149cdd00f745ad897f506434d7156b8147ef5bae
workflow-type: tm+mt
source-wordcount: '3285'
ht-degree: 8%

---


# Modelli di pagina - Modificabili {#page-templates-editable}

Sono stati introdotti modelli modificabili per:

* Consenti agli autori specializzati di [creare e modificare i modelli](/help/sites-authoring/templates.md).

   * Tali autori specializzati sono denominati **autori di modelli**
   * Gli autori dei modelli devono essere membri del gruppo `template-authors`.

* Fornire modelli che mantengano una connessione dinamica a tutte le pagine create da tali modelli. In questo modo tutte le modifiche apportate al modello verranno applicate alle pagine stesse.
* Rendete il componente pagina più generico in modo che possa essere utilizzato senza personalizzazione.

Con i modelli modificabili, le parti che compongono una pagina sono isolate all’interno dei componenti. È possibile configurare le combinazioni di componenti necessarie in un’interfaccia utente, eliminando così la necessità di sviluppare un nuovo componente di pagina per ogni variazione di pagina.

>[!NOTE]
>
>[Sono disponibili anche ](/help/sites-developing/page-templates-static.md) modelli statici.

Questo documento:

* Fornisce una panoramica sulla creazione di modelli modificabili

   * Per informazioni dettagliate, vedere [Creazione di modelli di pagina](/help/sites-authoring/templates.md)

* Descrive le attività di amministrazione/sviluppatore necessarie per creare modelli modificabili
* Descrive le basi tecniche dei modelli modificabili

Questo documento presuppone che si abbia già familiarità con la creazione e la modifica di modelli. Consultate il documento di authoring [Creazione di modelli di pagina](/help/sites-authoring/templates.md), che descrive in dettaglio le capacità dei modelli modificabili come esposti all&#39;autore del modello.

>[!NOTE]
>
>L&#39;esercitazione seguente potrebbe interessare anche la configurazione di un modello di pagina modificabile in un nuovo progetto:
>[Guida introduttiva  AEM Sites Part 2 - Creazione di una pagina di base e di un modello](https://helpx.adobe.com/experience-manager/kt/sites/using/getting-started-wknd-tutorial-develop/part2.html)

## Creazione di un nuovo modello {#creating-a-new-template}

La creazione di modelli modificabili viene realizzata principalmente con la [console dei modelli ed editor di modelli](/help/sites-authoring/templates.md) da un autore di modelli. Questa sezione fornisce una panoramica di questo processo e una descrizione di quanto avviene a livello tecnico.

Per informazioni sull&#39;utilizzo di modelli modificabili in un progetto AEM vedere [Creazione di un progetto AEM tramite Lazybones](https://helpx.adobe.com/experience-manager/using/aem_lazybones.html).

Durante la creazione di un nuovo modello modificabile:

1. Create una cartella [per i modelli](#template-folders). Questa operazione non è obbligatoria, ma è consigliata.
1. Selezionare un [tipo di modello](#template-type). Viene copiato per creare la [definizione del modello](#template-definitions).

   >[!NOTE]
   >
   >Sono disponibili una selezione di tipi di modelli out-of-the-box. Potete anche [creare tipi di modelli specifici per il sito](/help/sites-developing/page-templates-editable.md#creating-template-types), se necessario.

1. Configurate la struttura, i criteri di contenuto, il contenuto iniziale e il layout del nuovo modello.

   **Struttura**

   * La struttura consente di definire componenti e contenuti per il modello.
   * I componenti definiti nella struttura del modello non possono essere spostati su una pagina risultante, né eliminati da alcuna pagina risultante.

      * Se create un modello in una cartella personalizzata all&#39;esterno del contenuto di esempio di We.Retail, potete scegliere i componenti di base o utilizzare [Componenti di base](https://helpx.adobe.com/experience-manager/core-components/using/developing.html).
   * Se desideri che gli autori delle pagine siano in grado di aggiungere e rimuovere componenti, aggiungi un sistema di paragrafi al modello.
   * I componenti possono essere sbloccati e bloccati di nuovo per consentire di definire il contenuto iniziale.

   Per informazioni dettagliate sulla definizione della struttura da parte dell&#39;autore di un modello, vedere [Creazione di modelli di pagina](/help/sites-authoring/templates.md#editing-a-template-structure-template-author).

   Per i dettagli tecnici della struttura, vedere [Struttura](/help/sites-developing/page-templates-editable.md#structure) in questo documento.

   **Criteri**

   * I criteri di contenuto definiscono le proprietà di progettazione di un componente.

      * Ad esempio, i componenti disponibili o le dimensioni minime e massime.
   * Questi sono applicabili al modello (e alle pagine create con tale modello).

   Per informazioni dettagliate sulla definizione dei criteri da parte dell&#39;autore di un modello, vedere [Creazione di modelli di pagina](/help/sites-authoring/templates.md#editing-a-template-structure-template-author).

   Per informazioni tecniche sui criteri, consultare [Criteri di contenuto](/help/sites-developing/page-templates-editable.md#content-policies) in questo documento.

   **Contenuto iniziale**

   * Contenuto iniziale definisce il contenuto che verrà visualizzato quando una pagina viene creata per la prima volta in base al modello.
   * Il contenuto iniziale può essere modificato dagli autori della pagina.

   Per informazioni dettagliate sulla definizione della struttura da parte dell&#39;autore di un modello, vedere [Creazione di modelli di pagina](/help/sites-authoring/templates.md#editing-a-template-initial-content-author).

   Per informazioni tecniche sui contenuti iniziali, consultate [Contenuto iniziale](/help/sites-developing/page-templates-editable.md#initial-content) in questo documento.

   **Layout**

   * È possibile definire il layout del modello per una serie di dispositivi.
   * Il Layout reattivo per i modelli funziona come per la creazione delle pagine.

   Per informazioni dettagliate sulla modalità in cui un autore del modello definisce il layout del modello, vedere [Creazione di modelli di pagina](/help/sites-authoring/templates.md#editing-a-template-layout-template-author).

   Per informazioni tecniche sul layout del modello, vedere [Layout](/help/sites-developing/page-templates-editable.md#layout) in questo documento.

1. Attivate il modello, quindi consentitelo per specifiche strutture ad albero del contenuto.

   * Un modello può essere abilitato o disabilitato per renderlo disponibile o non disponibile per gli autori di pagine.
   * Un modello può essere reso disponibile o non disponibile per alcuni rami di pagina.

   Per informazioni dettagliate sull&#39;abilitazione di un modello da parte dell&#39;autore di un modello, vedere [Creazione di modelli di pagina](/help/sites-authoring/templates.md#enabling-and-allowing-a-template-template-author).

   Per informazioni tecniche sull&#39;abilitazione di un modello, vedere [Abilitazione e abilitazione di un modello per noi](/help/sites-developing/page-templates-editable.md#enabling-and-allowing-a-template-for-use)e in questo documento

1. Utilizzatelo per creare pagine di contenuto.

   * Quando si utilizza un modello per creare una nuova pagina, non vi è alcuna differenza visibile e nessuna indicazione tra modelli statici e modificabili.
   * Per l’autore della pagina, il processo è trasparente.

   Per informazioni dettagliate sull&#39;utilizzo dei modelli da parte dell&#39;autore di una pagina per creare una pagina, vedere [Creazione e organizzazione di pagine](/help/sites-authoring/managing-pages.md#templates).

   Per informazioni tecniche sulla creazione di pagine con modelli modificabili, consultare [Pagine di contenuti risultanti](/help/sites-developing/page-templates-editable.md#resultant-content-pages) in questo documento.

>[!TIP]
>
>Non inserire mai informazioni che devono essere internazionalizzate in un modello. A scopo di internalizzazione, si consiglia di usare la funzione di localizzazione [dei componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/get-started/localization.html).

>[!NOTE]
>
>I modelli sono strumenti potenti per semplificare il flusso di lavoro di creazione delle pagine. Tuttavia, troppi modelli possono sopraffare gli autori e rendere confusa la creazione delle pagine. Una buona regola è mantenere il numero di modelli al di sotto di 100.
>
> Adobe non consiglia di avere più di 1000 modelli a causa di potenziali impatti sulle prestazioni.

>[!NOTE]
>
>La libreria client dell&#39;editor presuppone la presenza dello spazio dei nomi `cq.shared` nelle pagine di contenuto, e se è assente, si verificherà l&#39;errore JavaScript `Uncaught TypeError: Cannot read property 'shared' of undefined`.
>
>Tutte le pagine di contenuto di esempio contengono `cq.shared`, pertanto qualsiasi contenuto basato su di esse include automaticamente `cq.shared`. Tuttavia, se decidete di creare da zero pagine di contenuto personalizzate senza basarle su contenuti di esempio, dovete includere lo spazio dei nomi `cq.shared`.
>
>Per ulteriori informazioni, vedere [Utilizzo di librerie lato client](/help/sites-developing/clientlibs.md).

## Cartelle modello {#template-folders}

Per organizzare i modelli potete utilizzare le cartelle seguenti:

* **globale**
* Specifico per il sito
Le cartelle specifiche del sito create per organizzare i modelli vengono create con un account che dispone di privilegi di amministratore.

>[!NOTE]
>
>Anche se potete nidificare le cartelle, quando l&#39;utente le visualizza nella console **Templates**, queste vengono presentate come una struttura semplice.

In un’istanza AEM standard la cartella **globale** esiste già nella console modelli. Questa contiene i modelli predefiniti e funge da fallback se nella cartella corrente non sono presenti criteri e/o tipi di modello. Potete aggiungere i modelli predefiniti a questa cartella o creare una nuova cartella (scelta consigliata).

>[!NOTE]
>
>È consigliabile creare una nuova cartella in cui memorizzare i modelli personalizzati e non utilizzare la cartella globale.

>[!CAUTION]
>
>Le cartelle devono essere create da un utente con diritti `admin`.

I tipi di modello e i criteri vengono ereditati in tutte le cartelle in base al seguente ordine di precedenza:

1. La cartella corrente.
1. Elemento padre/i della cartella corrente.
1. `/conf/global`
1. `/apps`
1. `/libs`

Viene creato un elenco di tutte le voci consentite. Se le configurazioni si sovrappongono ( `path`/ `label`), all&#39;utente viene presentata solo l&#39;istanza più vicina alla cartella corrente.

Per creare una nuova cartella, potete effettuare le seguenti operazioni:

* Programmaticamente o con CRXDE Lite
* Utilizzo del browser di configurazione

## Utilizzo del CRXDE Lite {#using-crxde-lite}

1. È possibile creare una nuova cartella (in /conf) per l’istanza a livello di programmazione o con CRXDE Lite.

   Deve essere utilizzata la seguente struttura:

   ```xml
   /conf
       <your-folder-name> [sling:Folder]
           settings [sling:Folder]
               wcm [cq:Page]
                   templates [cq:Page]
                   policies [cq:Page]
   ```

1. È quindi possibile definire le seguenti proprietà sul nodo principale della cartella:

   `<your-folder-name> [sling:Folder]`

   Nome: `jcr:title`

   * Tipo: `String`

   * Valore: Titolo (per la cartella) che si desidera visualizzare nella console **Templates**.

1. In *aggiunta* alle autorizzazioni e ai privilegi di authoring standard (ad esempio `content-authors`) è ora necessario assegnare i gruppi e definire i diritti di accesso (ACL) richiesti agli autori per poter creare i modelli nella nuova cartella.

   Il gruppo `template-authors` è il gruppo predefinito che deve essere assegnato. Per ulteriori informazioni, vedere la sezione [ACL e gruppi](/help/sites-developing/page-templates-editable.md#acls-and-groups) riportata di seguito.

   Per informazioni dettagliate sulla gestione e l&#39;assegnazione dei diritti di accesso, vedere [Accesso a Rights Management](/help/sites-administering/user-group-ac-admin.md#access-right-management).

### Utilizzo del browser di configurazione {#using-the-configuration-browser}

1. Andate a **Navigazione globale** -> **Strumenti** > **Browser di configurazione**.

   Le cartelle esistenti sono elencate a sinistra, inclusa la cartella **globale**.

1. Fai clic su **Crea**.
1. Nella finestra di dialogo **Crea configurazione** è necessario configurare i seguenti campi:

   * **Titolo**: Fornire un titolo per la cartella di configurazione
   * **Modelli** modificabili: Fare clic per consentire la modifica dei modelli all&#39;interno di questa cartella

1. Fai clic su **Crea**

>[!NOTE]
>
>Nel browser di configurazione, potete modificare la cartella globale e attivare l&#39;opzione **Modelli modificabili** se desiderate creare dei modelli all&#39;interno di questa cartella, ma questa è una procedura consigliata.
>
>Per ulteriori informazioni, consulta la documentazione del [browser di configurazione](/help/sites-administering/configurations.md).

### ACL e gruppi {#acls-and-groups}

Una volta create le cartelle dei modelli (tramite CRXDE o con il browser di configurazione), gli ACL devono essere definiti per i gruppi appropriati per le cartelle dei modelli per garantire la protezione adeguata.

Le cartelle dei modelli per l&#39;implementazione di riferimento [We.Retail](/help/sites-developing/we-retail.md) possono essere utilizzate come esempio.

#### Il gruppo di autori dei modelli {#the-template-authors-group}

Il gruppo `template-authors` è il gruppo utilizzato per gestire l&#39;accesso ai modelli ed è dotato di AEM standard, ma è vuoto. Gli utenti devono essere aggiunti al gruppo per il progetto/sito.

>[!CAUTION]
>
>Il gruppo `template-authors` è *solo* per gli utenti che devono essere in grado di creare nuovi modelli.
>
>La modifica dei modelli è molto efficace e, se non viene eseguita correttamente, i modelli esistenti possono essere interrotti. Questo ruolo dovrebbe pertanto essere mirato e includere solo utenti qualificati.

Nella tabella seguente sono elencate le autorizzazioni necessarie per la modifica dei modelli.

<table>
 <tbody>
  <tr>
   <th>Percorso</th>
   <th>Ruolo/Gruppo</th>
   <th>Autorizzazioni <br /> </th>
   <th>Descrizione</th>
  </tr>
  <tr>
   <td rowspan="3"><code>/conf/&lt;<i>your-folder</i>&gt;/settings/wcm/templates</code></td>
   <td>Autori modello<br /> </td>
   <td>lettura, scrittura, replica</td>
   <td>Autori di modelli che creano, leggono, aggiornano, eliminano e replicano modelli nello spazio <code>/conf</code> specifico del sito</td>
  </tr>
  <tr>
   <td>Utente Web anonimo</td>
   <td>read</td>
   <td>Utente Web anonimo deve leggere i modelli durante il rendering di una pagina</td>
  </tr>
  <tr>
   <td>Autori contenuto</td>
   <td>replica</td>
   <td>Gli autori di replicheContent devono attivare i modelli di una pagina durante l’attivazione di una pagina</td>
  </tr>
  <tr>
   <td rowspan="3"><code>/conf/&lt;<i>your-folder</i>&gt;/settings/wcm/policies</code></td>
   <td><code>Template Author</code></td>
   <td>lettura, scrittura, replica</td>
   <td>Autori di modelli che creano, leggono, aggiornano, eliminano e replicano modelli nello spazio <code>/conf</code> specifico del sito</td>
  </tr>
  <tr>
   <td>Utente Web anonimo</td>
   <td>read</td>
   <td>Utente Web anonimo deve leggere i criteri durante il rendering di una pagina</td>
  </tr>
  <tr>
   <td>Autori contenuto</td>
   <td>replica</td>
   <td>Quando si attiva una pagina, gli autori dei contenuti devono attivare i criteri di un modello di pagina</td>
  </tr>
  <tr>
   <td rowspan="2"><code>/conf/&lt;site&gt;/settings/template-types</code></td>
   <td>Autore del modello</td>
   <td>read</td>
   <td>L’autore del modello crea un nuovo modello basato su uno dei tipi di modello predefiniti.</td>
  </tr>
  <tr>
   <td>Utente Web anonimo</td>
   <td>nessuno</td>
   <td>L'utente Web anonimo non deve accedere ai tipi di modello</td>
  </tr>
 </tbody>
</table>

Questo gruppo predefinito `template-authors` copre solo le impostazioni di progetto, dove tutti i membri `template-authors` possono accedere e creare tutti i modelli. Per le impostazioni più complesse, in cui sono necessari gruppi di autori di modelli multipli per l&#39;accesso separato ai modelli, è necessario creare un numero maggiore di gruppi di autori di modelli personalizzati. Tuttavia, le autorizzazioni per i gruppi di autori dei modelli rimarrebbero invariate.

#### Modelli precedenti in /conf/global {#legacy-templates-under-conf-global}

I modelli non devono più essere memorizzati in `/conf/global`, tuttavia per alcune installazioni precedenti potrebbero essere ancora presenti dei modelli in questo percorso. SOLO in tali situazioni precedenti, i seguenti percorsi `/conf/global` dovrebbero essere configurati in modo esplicito.

<table>
 <tbody>
  <tr>
   <th>Percorso</th>
   <th>Ruolo/Gruppo</th>
   <th>Autorizzazioni <br /> </th>
   <th>Descrizione</th>
  </tr>
  <tr>
   <td rowspan="3"><code>/conf/global/settings/wcm/templates</code></td>
   <td>Autori modello</td>
   <td>lettura, scrittura, replica</td>
   <td>Autori di modelli che creano, leggono, aggiornano, eliminano e replicano i modelli in <code>/conf/global</code></td>
  </tr>
  <tr>
   <td>Utente Web anonimo</td>
   <td>read</td>
   <td>Utente Web anonimo deve leggere i modelli durante il rendering di una pagina</td>
  </tr>
  <tr>
   <td>Autori contenuto</td>
   <td>replica</td>
   <td>Gli autori dei contenuti devono attivare i modelli di una pagina durante l’attivazione</td>
  </tr>
  <tr>
   <td rowspan="3"><code>/conf/global/settings/wcm/policies</code></td>
   <td><code>Template Author</code></td>
   <td>lettura, scrittura, replica</td>
   <td>Autori di modelli che creano, leggono, aggiornano, eliminano e replicano i modelli in <code>/conf/global</code></td>
  </tr>
  <tr>
   <td>Utente Web anonimo</td>
   <td>read</td>
   <td>Utente Web anonimo deve leggere i criteri durante il rendering di una pagina</td>
  </tr>
  <tr>
   <td>Autori contenuto</td>
   <td>replica</td>
   <td>Quando si attiva una pagina, gli autori dei contenuti devono attivare i criteri di un modello di pagina</td>
  </tr>
  <tr>
   <td rowspan="2"><code>/conf/global/settings/wcm/template-types</code></td>
   <td>Autore del modello</td>
   <td>read</td>
   <td>L’autore del modello crea un nuovo modello basato su uno dei tipi di modello predefiniti</td>
  </tr>
  <tr>
   <td>Utente Web anonimo</td>
   <td>nessuno</td>
   <td>L'utente Web anonimo non deve accedere ai tipi di modello</td>
  </tr>
 </tbody>
</table>

## Tipo di modello {#template-type}

Quando create un nuovo modello, dovete specificare un tipo di modello:

* I tipi di modello forniscono efficacemente i modelli per un modello. Quando create un nuovo modello, la struttura e il contenuto iniziale del tipo di modello selezionato vengono usati per creare il nuovo modello.

   * Il tipo di modello viene copiato per creare il modello.
   * Una volta eseguita la copia, l&#39;unica connessione tra il modello e il tipo di modello è un riferimento statico a scopo informativo.

* I tipi di modello consentono di definire:

   * Il tipo di risorsa del componente pagina.
   * Il criterio del nodo principale, che definisce i componenti consentiti nell&#39;editor modelli.
   * È consigliabile definire i punti di interruzione per la griglia reattiva e l&#39;impostazione dell&#39;emulatore mobile sul tipo di modello. Questo è facoltativo, perché la configurazione può essere definita anche sul singolo modello (vedere [Tipo di modello e Gruppi di dispositivi mobili](/help/sites-developing/page-templates-editable.md#p-template-type-and-mobile-device-groups-br-p)).

* AEM fornisce una piccola selezione di tipi di modelli predefiniti, ad esempio Pagina HTML5 e Pagina modulo adattiva.

   * Altri esempi sono forniti come parte del contenuto di esempio [We.Retail](/help/sites-developing/we-retail.md).

* I tipi di modelli sono generalmente definiti dagli sviluppatori.

I tipi di modelli forniti vengono memorizzati in:

* `/libs/settings/wcm/template-types`

>[!CAUTION]
>
>Non è necessario modificare nulla nel percorso `/libs`. Questo perché il contenuto di `/libs` viene sovrascritto al successivo aggiornamento dell&#39;istanza (e potrebbe essere sovrascritto quando si applica un hotfix o un feature pack).

I tipi di modello specifici per il sito devono essere memorizzati nella posizione comparabile di:

* `/apps/settings/wcm/template-types`

Le definizioni per i tipi di modelli personalizzati devono essere memorizzate in cartelle definite dall&#39;utente (consigliato) o in alternativa in `global`. Esempio:

* `/conf/<my-folder-01>/<my-folder-02>/settings/wcm/template-types`
* `/conf/<my-folder>/settings/wcm/template-types`
* `/conf/global/settings/wcm/template-types`

>[!CAUTION]
>
>I tipi di modello devono rispettare la struttura corretta delle cartelle (ovvero `/settings/wcm/...`), in caso contrario i tipi di modello non verranno trovati.

### Tipo di modello e gruppi di dispositivi mobili {#template-type-and-mobile-device-groups-br}

I [gruppi di dispositivi](/help/sites-developing/mobile.md#device-groups) utilizzati per un modello modificabile (impostati come percorso relativo della proprietà `cq:deviceGroups`) definiscono quali dispositivi mobili sono disponibili come emulatori nella [modalità di layout](/help/sites-authoring/responsive-layout.md) dell&#39;authoring delle pagine. Questo valore può essere impostato in due posizioni:

* Nel tipo di modello modificabile
* Nel modello modificabile

Quando create un nuovo modello modificabile, il valore viene copiato dal tipo di modello al singolo modello. Se il valore non è impostato sul tipo, può essere impostato sul modello. Una volta creato il modello, non esiste alcuna ereditarietà dal tipo al modello.

>[!CAUTION]
>
>Il valore di `cq:deviceGroups` deve essere impostato come percorso relativo, ad esempio `mobile/groups/responsive`, e non come percorso assoluto, ad esempio `/etc/mobile/groups/responsive`.

>[!NOTE]
>
>Con [modelli statici](/help/sites-developing/page-templates-static.md), il valore di `cq:deviceGroups` può essere impostato nella radice del sito.
>
>Con i modelli modificabili, questo valore ora viene memorizzato a livello di modello e non è supportato a livello di pagina principale.

### Creazione di tipi di modelli {#creating-template-types}

Se avete creato un modello che può fungere da base per altri modelli, potete copiare il modello come tipo di modello.

1. Create un modello come fareste con qualsiasi altro modello modificabile [come indicato qui](/help/sites-authoring/templates.md#creating-a-new-template-template-author), che fungerà da base per il tipo di modello.
1. Utilizzando CRXDE Lite, copiare il modello appena creato dal nodo `templates` al nodo `template-types` sotto la cartella [template](/help/sites-developing/page-templates-editable.md#template-folders).
1. Eliminate il modello dal nodo `templates` sotto la cartella [template](/help/sites-developing/page-templates-editable.md#template-folders).
1. Nella copia del modello che si trova sotto il nodo `template-types`, eliminare tutte le proprietà `cq:template` e `cq:templateType` `jcr:content`.

Potete anche sviluppare un tipo di modello personalizzato utilizzando un modello modificabile di esempio come base, disponibile su GitHub.

CODICE SU GITHUB

Puoi trovare il codice di questa pagina su GitHub

* [Apri progetto di tipo &quot;aem-sites-example-custom-template-type&quot; su GitHub](https://github.com/Adobe-Marketing-Cloud/aem-sites-example-custom-template-type)
* Scarica il progetto come [un file ZIP](https://github.com/Adobe-Marketing-Cloud/aem-sites-example-custom-template-type/archive/master.zip)

## Definizioni dei modelli {#template-definitions}

Le definizioni per i modelli modificabili sono memorizzate in [cartelle definite dall&#39;utente](/help/sites-developing/page-templates-editable.md#template-folders) (consigliato) o in alternativa in `global`. Esempio:

* `/conf/<my-folder>/settings/wcm/templates`
* `/conf/<my-folder-01>/<my-folder-02>/settings/wcm/templates`
* `/conf/global/settings/wcm/templates`

Il nodo principale del modello è di tipo `cq:Template` con una struttura di ossatura di:

```xml
<template-name>
  initial
    jcr:content
      root
        <component>
        ...
        <component>
  jcr:content
    @property status
  policies
    jcr:content
      root
        @property cq:policy
        <component>
          @property cq:policy
        ...
        <component>
          @property cq:policy
  structure
    jcr:content
      root
        <component>
        ...
        <component>
      cq:responsive
        breakpoints
  thumbnail.png
```

Gli elementi principali sono:

* `<template-name>`

   * ` [initial](#initial-content)`
   * `jcr:content`
   * ` [structure](#structure)`
   * ` [policies](#policies)`
   * `thumbnail.png`

### jcr:content {#jcr-content}

Questo nodo contiene le proprietà per il modello:

* **Nome**: `jcr:title`

* **Nome**: `status`

   * ``**Tipo**: `String`

   * **Valore**:  `draft`,  `enabled` oppure  `disabled`

### Struttura {#structure}

Definisce la struttura della pagina risultante:

* Viene unito al contenuto iniziale ( `/initial`) durante la creazione di una nuova pagina.
* Le modifiche apportate alla struttura si rifletteranno sulle pagine create con il modello.
* Il nodo `root` ( `structure/jcr:content/root`) definisce l&#39;elenco dei componenti che saranno disponibili nella pagina risultante.

   * I componenti definiti nella struttura del modello non possono essere spostati né eliminati dalle pagine risultanti.
   * Quando un componente viene sbloccato, la proprietà `editable` viene impostata su `true`.

   * Quando un componente che già contiene contenuto viene sbloccato, il contenuto verrà spostato nel ramo `initial`.

* Il nodo `cq:responsive` contiene le definizioni per il layout reattivo.

### Contenuto iniziale {#initial-content}

Definisce il contenuto iniziale di una nuova pagina al momento della creazione:

* Contiene un nodo `jcr:content` che viene copiato in qualsiasi nuova pagina.
* Viene unito alla struttura ( `/structure`) durante la creazione di una nuova pagina.
* Eventuali pagine esistenti non verranno aggiornate se il contenuto iniziale viene modificato dopo la creazione.
* Il nodo `root` contiene un elenco di componenti per definire ciò che sarà disponibile nella pagina risultante.
* Se il contenuto viene aggiunto a un componente in modalità struttura e tale componente viene successivamente sbloccato (o viceversa), tale contenuto viene utilizzato come contenuto iniziale.

### Layout {#layout}

Durante la [modifica di un modello è possibile definire il layout](/help/sites-authoring/templates.md), utilizza [layout reattivo standard](/help/sites-authoring/responsive-layout.md) che può essere anche [configurato](/help/sites-administering/configuring-responsive-layout.md).

### Criteri contenuto {#content-policies}

I criteri relativi ai contenuti (o alle progettazioni) definiscono le proprietà di progettazione (o design) di un componente. Ad esempio, i componenti disponibili o le dimensioni minime e massime. Questi sono applicabili al modello (e alle pagine create con tale modello). I criteri di contenuto possono essere creati e selezionati nell&#39;editor modelli.

* La proprietà `cq:policy`, sul nodo `root`
   `/conf/<your-folder>/settings/wcm/templates/<your-template>/policies/jcr:content/root`
Fornisce un riferimento relativo al criterio del contenuto per il sistema paragrafo della pagina.

* La proprietà `cq:policy`, nei nodi espliciti dei componenti in `root`, fornisce collegamenti ai criteri per i singoli componenti.

* Le definizioni effettive dei criteri sono memorizzate in:
   `/conf/<your-folder>/settings/wcm/policies/wcm/foundation/components`

>[!NOTE]
>
>I percorsi delle definizioni dei criteri dipendono dal percorso del componente. `cq:policy` contiene un riferimento relativo alla configurazione stessa.

>[!NOTE]
>
>Le pagine create da modelli modificabili non offrono una modalità Progettazione nell’editor pagina.
>
>La struttura `policies` di un modello modificabile ha la stessa gerarchia della configurazione della modalità di progettazione di un modello statico in:
>
>`/etc/designs/<my-site>/jcr:content/<component-name>`
>
>La configurazione della modalità di progettazione di un modello statico è stata definita per ciascun componente di pagina.

### Criteri di pagina {#page-policies}

I criteri di pagina consentono di definire i [criteri di contenuto](#content-policies) per la pagina (parsys principale), nel modello o nelle pagine risultanti.

### Abilitazione e abilitazione di un modello per l&#39;uso di {#enabling-and-allowing-a-template-for-use}

1. **Abilita modello**

   Per poter utilizzare un modello, è necessario che sia attivato:

   * [Abilitazione del ](/help/sites-authoring/templates.md#enablingatemplateauthor) modello dalla console  **** Modelli.

   * Impostazione della proprietà status sul nodo `jcr:content`.

      * Ad esempio, on:
         `/conf/<your-folder>/settings/wcm/templates/<your-template>/jcr:content`

      * Definire la proprietà:

         * Nome: status
         * Tipo: Stringa
         * Valore: `enabled`

1. **Modelli consentiti**

   * [Definire i percorsi dei modelli consentiti nelle proprietà  **pagina**](/help/sites-authoring/templates.md#allowing-a-template-author) della pagina o della pagina principale appropriata di un ramo secondario.
   * Impostare la proprietà:
      `cq:allowedTemplates`
In 
`jcr:content` del ramo richiesto.
   Ad esempio, con un valore di:

   `/conf/<your-folder>/settings/wcm/templates/.*`

## Pagine contenuto risultanti {#resultant-content-pages}

Pagine create da modelli modificabili:

* Vengono creati con una sottostruttura ad albero che viene unita da `structure` e `initial` nel modello

* Contiene riferimenti alle informazioni contenute nel modello e nel tipo di modello. Questo si ottiene con un nodo `jcr:content` con le proprietà:

   * `cq:template`
Fornisce il riferimento dinamico al modello effettivo; consente di riflettere le modifiche apportate al modello sulle pagine effettive.

   * `cq:templateType`
Fornisce un riferimento al tipo di modello.

![chlimage_1-71](assets/chlimage_1-71.png)

Il diagramma precedente mostra come i modelli, i contenuti e i componenti si interfacciano:

* Controller - `/content/<my-site>/<my-page>`
Pagina risultante che fa riferimento al modello. Il contenuto controlla l’intero processo. In base alle definizioni, accede al modello e ai componenti appropriati.

* Configurazione - `/conf/<my-folder>/settings/wcm/templates/<my-template>`
Il modello [e i relativi criteri di contenuto](#template-definitions) definiscono la configurazione della pagina.

* Modello - Pacchetti OSGi
I [bundle OSGI](/help/sites-deploying/osgi-configuration-settings.md) implementano la funzionalità.

* Visualizza - `/apps/<my-site>/components`
Sia nell’ambiente di creazione che in quello di pubblicazione, il rendering del contenuto viene eseguito da [components](/help/sites-developing/components.md).

Durante il rendering di una pagina:

* **Modelli**:

   * Viene fatto riferimento alla proprietà `cq:template` del relativo nodo `jcr:content` per accedere al modello che corrisponde a tale pagina.

* **Componenti**:

   * Il componente pagina unisce la struttura `structure/jcr:content` del modello alla struttura `jcr:content` della pagina.

   * Il componente Pagina consente solo all’autore di modificare i nodi della struttura del modello contrassegnati come modificabili (così come altri elementi secondari).
   * Quando si esegue il rendering di un componente su una pagina, il percorso relativo di tale componente viene tracciato dal nodo `jcr:content`; viene quindi ricercato lo stesso percorso nel nodo `policies/jcr:content` del modello.

      * La proprietà `cq:policy` di questo nodo fa riferimento al criterio del contenuto effettivo (ovvero contiene la configurazione di progettazione per quel componente).

      * Questo consente di avere più modelli che riutilizzano le stesse configurazioni dei criteri per i contenuti.
