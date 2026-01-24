---
title: Modelli di pagina - Modificabili
description: Sono stati introdotti modelli modificabili che consentono agli sviluppatori di creare e modificare modelli, forniscono modelli che mantengono una connessione dinamica a qualsiasi pagina creata da essi e rendono il componente Pagina più generico
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
docset: aem65
exl-id: dcb66b6d-d731-493e-8936-12d529f6cbde
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: f30decf0e32a520dcda04b89c5c1f5b67ab6e028
workflow-type: tm+mt
source-wordcount: '3187'
ht-degree: 4%

---

# Modelli di pagina - Modificabili {#page-templates-editable}

Sono stati introdotti modelli modificabili per:

* Consenti agli autori specializzati di [creare e modificare modelli](/help/sites-authoring/templates.md).

   * Tali autori specializzati sono denominati **autori di modelli**
   * Gli autori dei modelli devono essere membri del gruppo `template-authors`.

* Fornisci modelli che mantengano una connessione dinamica a qualsiasi pagina creata da essi. In questo modo, eventuali modifiche al modello verranno applicate anche alle pagine.
* Rendi il componente Pagina più generico, in modo che il componente Pagina principale possa essere utilizzato senza personalizzazione.

Con i modelli modificabili, le parti che compongono una pagina vengono isolate all’interno dei componenti. Puoi configurare le combinazioni di componenti necessarie in un’interfaccia utente in modo da eliminare la necessità di sviluppare un nuovo componente pagina per ogni variante di pagina.

>[!NOTE]
>
>Sono inoltre disponibili [modelli statici](/help/sites-developing/page-templates-static.md).

Questo documento:

* Panoramica sulla creazione di modelli modificabili

   * Per ulteriori dettagli, vedere [Creazione di modelli di pagina](/help/sites-authoring/templates.md)

* Descrive le attività di amministrazione/sviluppatore necessarie per creare modelli modificabili
* Descrive le basi tecniche dei modelli modificabili

In questo documento si presuppone che tu abbia già familiarità con la creazione e la modifica di modelli. Consulta il documento di authoring [Creazione di modelli di pagina](/help/sites-authoring/templates.md), che descrive le funzionalità dei modelli modificabili esposti all&#39;autore del modello.

>[!NOTE]
>
>Il seguente tutorial potrebbe essere utile anche per impostare un modello di pagina modificabile in un nuovo progetto:
>[Guida introduttiva ad AEM Sites Parte 2 - Creazione di una pagina base e di un modello](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/project-archetype/pages-templates.html?lang=it)

## Creazione di un nuovo modello {#creating-a-new-template}

La creazione di modelli modificabili viene eseguita principalmente con la console [modelli e l&#39;editor modelli](/help/sites-authoring/templates.md) da un autore di modelli. Questa sezione offre una panoramica di questo processo e segue con una descrizione di ciò che accade a livello tecnico.

Per informazioni sull&#39;utilizzo di modelli modificabili in un progetto AEM, vedere [Creazione di un progetto AEM tramite Lazybones](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-manager/create-aem-project-structure-using-lazybones/m-p/186478?profile.language=it).

Quando crei un modello modificabile:

1. Crea una cartella [&#x200B; per i modelli](#template-folders). Questa cartella non è obbligatoria, ma è una best practice consigliata.
1. Seleziona un tipo di [modello](#template-type). Questo tipo viene copiato per creare la [definizione modello](#template-definitions).

   >[!NOTE]
   >
   >È disponibile una selezione di tipi di modello pronti all’uso. Se necessario, puoi anche [creare tipi di modello specifici per il sito](/help/sites-developing/page-templates-editable.md#creating-template-types).

1. Configura la struttura, i criteri per i contenuti, il contenuto iniziale e il layout del nuovo modello.

   **Struttura**

   * La struttura ti consente di definire componenti e contenuti per il modello.
   * I componenti definiti nella struttura del modello non possono essere spostati in una pagina risultante né eliminati dalle pagine risultanti.

      * Se si crea un modello in una cartella personalizzata all&#39;esterno del contenuto di esempio di `We.Retail`, è possibile scegliere Componenti di base o utilizzare [Componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/overview.html?lang=it).

   * Se desideri che gli autori delle pagine possano aggiungere e rimuovere componenti, aggiungi un sistema di paragrafi al modello.
   * I componenti possono essere sbloccati e bloccati di nuovo per consentire di definire il contenuto iniziale.

   Per informazioni dettagliate su come un autore di modelli definisce la struttura, vedere [Creazione di modelli di pagina](/help/sites-authoring/templates.md#editing-a-template-structure-template-author).

   Per informazioni tecniche sulla struttura, vedere [Struttura](/help/sites-developing/page-templates-editable.md#structure) in questo documento.

   **Criteri**

   * I criteri per contenuto definiscono le proprietà di progettazione di un componente.

      * Ad esempio, i componenti disponibili o le dimensioni minima/massima.

   * Questi criteri sono applicabili al modello (e alle pagine create con il modello).

   Per informazioni dettagliate su come un autore di modelli definisce i criteri, vedere [Creazione di modelli di pagina](/help/sites-authoring/templates.md#editing-a-template-structure-template-author).

   Per informazioni tecniche sui criteri, vedi [Criteri di contenuto](/help/sites-developing/page-templates-editable.md#content-policies) in questo documento.

   **Contenuto iniziale**

   * Il contenuto iniziale definisce il contenuto visualizzato quando una pagina viene creata per la prima volta in base al modello.
   * Il contenuto iniziale può quindi essere modificato dagli autori di pagine.

   Per informazioni dettagliate su come un autore di modelli definisce la struttura, vedere [Creazione di modelli di pagina](/help/sites-authoring/templates.md#editing-a-template-initial-content-author).

   Per informazioni tecniche sul contenuto iniziale, vedere [Contenuto iniziale](/help/sites-developing/page-templates-editable.md#initial-content) in questo documento.

   **Layout**

   * Puoi definire il layout del modello per una serie di dispositivi.
   * Il layout reattivo per i modelli funziona come per la creazione delle pagine.

   Per informazioni dettagliate su come un autore di modelli definisce il layout del modello, vedere [Creazione di modelli di pagina](/help/sites-authoring/templates.md#editing-a-template-layout-template-author).

   Per informazioni tecniche sul layout del modello, vedere [Layout](/help/sites-developing/page-templates-editable.md#layout) in questo documento.

1. Abilita il modello, quindi consenti la creazione di strutture di contenuto specifiche.

   * Un modello può essere abilitato o disabilitato per renderlo disponibile o non disponibile agli autori di pagine.
   * Un modello può essere reso disponibile o non disponibile per alcuni rami di pagina.

   Per informazioni dettagliate su come un autore di modelli abilita un modello, vedere [Creazione di modelli di pagina](/help/sites-authoring/templates.md#enabling-and-allowing-a-template-template-author).

   Per informazioni tecniche sull&#39;abilitazione di un modello, vedere [Abilitazione e autorizzazione di un modello](/help/sites-developing/page-templates-editable.md#enabling-and-allowing-a-template-for-use)e in questo documento

1. Utilizzala per creare pagine di contenuto.

   * Quando si utilizza un modello per creare una pagina, non vi è alcuna differenza visibile né indicazione tra modelli statici e modificabili.
   * Per l’autore della pagina, il processo è trasparente.

   Per informazioni dettagliate su come un autore di pagine utilizza i modelli per creare una pagina, vedere [Creazione e organizzazione delle pagine](/help/sites-authoring/managing-pages.md#templates).

   Per informazioni tecniche sulla creazione di pagine con modelli modificabili, vedere [Pagine di contenuto risultanti](/help/sites-developing/page-templates-editable.md#resultant-content-pages) in questo documento.

>[!TIP]
>
>Non inserire mai informazioni che devono essere internazionalizzate in un modello. Ai fini dell&#39;internalizzazione, si consiglia di utilizzare la funzione di [localizzazione dei Componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/get-started/localization.html?lang=it).

>[!NOTE]
>
>I modelli sono strumenti potenti per semplificare il flusso di lavoro di creazione della pagina. Tuttavia, troppi modelli possono sopraffare gli autori e confondere la creazione di pagine. Una buona regola è mantenere il numero di modelli sotto i 100.
>
>Adobe consiglia di non disporre di più di 1000 modelli a causa di potenziali impatti sulle prestazioni.

>[!NOTE]
>
>La libreria client dell&#39;editor presuppone la presenza dello spazio dei nomi `cq.shared` nelle pagine di contenuto. Se assente, si verifica l&#39;errore JavaScript `Uncaught TypeError: Cannot read property 'shared' of undefined`.
>
>Tutte le pagine di contenuto di esempio contengono `cq.shared`, pertanto qualsiasi contenuto basato su di esse include automaticamente `cq.shared`. Tuttavia, se decidi di creare pagine di contenuto personalizzate da zero senza basarle su contenuto di esempio, devi assicurarti di includere lo spazio dei nomi `cq.shared`.
>
>Per ulteriori informazioni, vedere [Utilizzo delle librerie lato client](/help/sites-developing/clientlibs.md).

## Cartelle modelli {#template-folders}

Per organizzare i modelli, puoi utilizzare le cartelle seguenti:

* **globale**
* Specifico del sito
Le cartelle specifiche del sito create per organizzare i modelli vengono create con un account che dispone dei privilegi di amministratore.

>[!NOTE]
>
>Anche se è possibile nidificare le cartelle, quando l&#39;utente le visualizza nella console **Modelli**, vengono presentate come una struttura semplice.

In un&#39;istanza AEM standard, la cartella **global** esiste nella console modelli. Questa cartella contiene modelli predefiniti e funge da fallback se nella cartella corrente non sono presenti criteri e/o tipi di modello. Puoi aggiungere i modelli predefiniti a questa cartella o crearne una (scelta consigliata).

>[!NOTE]
>
>È consigliabile creare una cartella in cui inserire i modelli personalizzati e non utilizzare la cartella globale.

>[!CAUTION]
>
>Le cartelle devono essere create da un utente con diritti `admin`.

I tipi di modello e i criteri vengono ereditati in tutte le cartelle in base al seguente ordine di precedenza:

1. La cartella corrente.
1. Elemento padre della cartella corrente.
1. `/conf/global`
1. `/apps`
1. `/libs`

Viene creato un elenco di tutte le voci consentite. Se le configurazioni si sovrappongono ( `path`/ `label`), verrà presentata all&#39;utente solo l&#39;istanza più vicina alla cartella corrente.

Per creare una cartella, effettuare le seguenti operazioni:

* A livello di programmazione o con CRXDE Lite
* Utilizzo del browser configurazioni

## Utilizzo di CRXDE Lite {#using-crxde-lite}

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

1. Puoi quindi definire le seguenti proprietà sul nodo principale della cartella:

   `<your-folder-name> [sling:Folder]`

   Nome: `jcr:title`

   * Tipo: `String`

   * Valore: il titolo (per la cartella) che si desidera visualizzare nella console **Modelli**.

1. In *aggiunta* alle autorizzazioni e ai privilegi di authoring standard (ad esempio, `content-authors`), assegna gruppi e definisci i diritti di accesso (ACL) necessari affinché gli autori possano creare modelli nella nuova cartella.

   Il gruppo `template-authors` è il gruppo predefinito che deve essere assegnato. Per ulteriori informazioni, vedere la sezione [ACL e gruppi](/help/sites-developing/page-templates-editable.md#acls-and-groups).

   Consulta [Gestione dei diritti di accesso](/help/sites-administering/user-group-ac-admin.md#access-right-management) per informazioni dettagliate sulla gestione e l&#39;assegnazione dei diritti di accesso.

### Utilizzo del browser configurazioni {#using-the-configuration-browser}

1. Vai a **Navigazione globale** > **Strumenti** > **Browser configurazioni**.

   Le cartelle esistenti sono elencate a sinistra, inclusa la cartella **global**.

1. Fai clic su **Crea**.
1. Nella finestra di dialogo **Crea configurazione**, è necessario configurare i campi seguenti:

   * **Titolo**: specifica un titolo per la cartella di configurazione
   * **Modelli modificabili**: selezionare per consentire modelli modificabili in questa cartella

1. Fai clic su **Crea**.

>[!NOTE]
>
>Nel browser configurazioni è possibile modificare la cartella globale e attivare l&#39;opzione **Modelli modificabili** se si desidera creare modelli in questa cartella. Tuttavia, questa pratica non è una best practice consigliata.
>
>Per ulteriori informazioni, vedere la documentazione del [browser di configurazione](/help/sites-administering/configurations.md).

### ACL e gruppi {#acls-and-groups}

Dopo aver creato le cartelle di modelli (tramite CRXDE o con il Browser configurazioni), per garantire la corretta protezione è necessario definire gli ACL per i gruppi appropriati per le cartelle di modelli.

Le cartelle dei modelli per l&#39;implementazione di riferimento [`We.Retail`](/help/sites-developing/we-retail.md) possono essere utilizzate come esempio.

#### Gruppo di autori di modelli {#the-template-authors-group}

Il gruppo `template-authors` è il gruppo utilizzato per gestire l&#39;accesso ai modelli e viene fornito come standard con AEM, ma è vuoto. Gli utenti devono essere aggiunti al gruppo per il progetto/sito.

>[!CAUTION]
>
>Il gruppo `template-authors` è *only* per gli utenti che devono essere in grado di creare modelli.
>
>La modifica dei modelli è potente e se non viene eseguita correttamente, i modelli esistenti possono andare in pezzi. Pertanto, questo ruolo deve essere mirato e includere solo utenti qualificati.

La tabella seguente descrive le autorizzazioni necessarie per la modifica dei modelli.

<table>
 <tbody>
  <tr>
   <th>Percorso</th>
   <th>Ruolo/Gruppo</th>
   <th>Autorizzazioni<br /> </th>
   <th>Descrizione</th>
  </tr>
  <tr>
   <td rowspan="3"><code>/conf/&lt;<i>your-folder</i>&gt;/settings/wcm/templates</code></td>
   <td>Autori modelli<br /> </td>
   <td>lettura, scrittura, replica</td>
   <td>Autori di modelli che creano, leggono, aggiornano, eliminano e replicano modelli nello spazio <code>/conf</code> specifico del sito</td>
  </tr>
  <tr>
   <td>Utente Web anonimo</td>
   <td>letto</td>
   <td>L’utente web anonimo deve leggere i modelli durante il rendering di una pagina</td>
  </tr>
  <tr>
   <td>Autori di contenuti</td>
   <td>replicare</td>
   <td>replicateGli autori di contenuti devono attivare i modelli di una pagina quando attivano una pagina</td>
  </tr>
  <tr>
   <td rowspan="3"><code>/conf/&lt;<i>your-folder</i>&gt;/settings/wcm/policies</code></td>
   <td><code>Template Author</code></td>
   <td>lettura, scrittura, replica</td>
   <td>Autori di modelli che creano, leggono, aggiornano, eliminano e replicano modelli nello spazio <code>/conf</code> specifico del sito</td>
  </tr>
  <tr>
   <td>Utente Web anonimo</td>
   <td>letto</td>
   <td>L’utente web anonimo deve leggere i criteri durante il rendering di una pagina</td>
  </tr>
  <tr>
   <td>Autori di contenuti</td>
   <td>replicare</td>
   <td>Gli autori di contenuti devono attivare i criteri di un modello di una pagina quando attivano una pagina</td>
  </tr>
  <tr>
   <td rowspan="2"><code>/conf/&lt;site&gt;/settings/template-types</code></td>
   <td>Autore del modello</td>
   <td>letto</td>
   <td>L’autore del modello crea un modello basato su uno dei tipi di modello predefiniti.</td>
  </tr>
  <tr>
   <td>Utente Web anonimo</td>
   <td>nessuno</td>
   <td>L'utente Web anonimo non deve accedere ai tipi di modello</td>
  </tr>
 </tbody>
</table>

Questo gruppo `template-authors` predefinito copre solo le impostazioni del progetto, in cui tutti i membri `template-authors` possono accedere e creare tutti i modelli. Per impostazioni più complesse, dove è necessario che più gruppi di autori di modelli separino l’accesso ai modelli, è necessario creare più gruppi di autori di modelli personalizzati. Tuttavia, le autorizzazioni per i gruppi di autori di modelli continuerebbero a essere le stesse.

#### Modelli legacy in /conf/global {#legacy-templates-under-conf-global}

Non archiviare i modelli in `/conf/global`. Tuttavia, per alcune installazioni legacy, potrebbero ancora essere presenti modelli in questa posizione. *Solo* in tali situazioni legacy deve essere configurato in modo esplicito i seguenti `/conf/global` percorsi.

<table>
 <tbody>
  <tr>
   <th>Percorso</th>
   <th>Ruolo/Gruppo</th>
   <th>Autorizzazioni<br /> </th>
   <th>Descrizione</th>
  </tr>
  <tr>
   <td rowspan="3"><code>/conf/global/settings/wcm/templates</code></td>
   <td>Autori di modelli</td>
   <td>lettura, scrittura, replica</td>
   <td>Autori di modelli che creano, leggono, aggiornano, eliminano e replicano modelli in <code>/conf/global</code></td>
  </tr>
  <tr>
   <td>Utente Web anonimo</td>
   <td>letto</td>
   <td>L’utente web anonimo deve leggere i modelli durante il rendering di una pagina</td>
  </tr>
  <tr>
   <td>Autori di contenuti</td>
   <td>replicare</td>
   <td>Gli autori dei contenuti devono attivare i modelli di una pagina quando attivano una pagina</td>
  </tr>
  <tr>
   <td rowspan="3"><code>/conf/global/settings/wcm/policies</code></td>
   <td><code>Template Author</code></td>
   <td>lettura, scrittura, replica</td>
   <td>Autori di modelli che creano, leggono, aggiornano, eliminano e replicano modelli in <code>/conf/global</code></td>
  </tr>
  <tr>
   <td>Utente Web anonimo</td>
   <td>letto</td>
   <td>L’utente web anonimo deve leggere i criteri durante il rendering di una pagina</td>
  </tr>
  <tr>
   <td>Autori di contenuti</td>
   <td>replicare</td>
   <td>Gli autori di contenuti devono attivare i criteri di un modello di una pagina quando attivano una pagina</td>
  </tr>
  <tr>
   <td rowspan="2"><code>/conf/global/settings/wcm/template-types</code></td>
   <td>Autore del modello</td>
   <td>letto</td>
   <td>L’autore del modello crea un modello basato su uno dei tipi di modello predefiniti</td>
  </tr>
  <tr>
   <td>Utente Web anonimo</td>
   <td>nessuno</td>
   <td>L'utente Web anonimo non deve accedere ai tipi di modello</td>
  </tr>
 </tbody>
</table>

## Tipo di modello {#template-type}

Durante la creazione di un modello, specificare un tipo di modello:

* I tipi di modello forniscono in modo efficace i modelli per un modello. Durante la creazione di un modello, vengono utilizzati la struttura e il contenuto iniziale del tipo di modello selezionato.

   * Il tipo di modello viene copiato per creare il modello.
   * Una volta eseguita la copia, l&#39;unica connessione tra il modello e il tipo di modello è un riferimento statico a scopo informativo.

* I tipi di modello consentono di definire:

   * Tipo di risorsa del componente Pagina.
   * Il criterio del nodo principale, che definisce i componenti consentiti nell’editor di modelli.
   * L’Adobe consiglia di definire i punti di interruzione per la griglia reattiva e la configurazione dell’emulatore mobile in sul tipo di modello. Questo passaggio è facoltativo, perché la configurazione può essere definita anche nel singolo modello (vedi [Tipo di modello e Gruppi di dispositivi mobili](/help/sites-developing/page-templates-editable.md#p-template-type-and-mobile-device-groups-br-p)).

* AEM fornisce una piccola selezione di tipi di modelli predefiniti, ad esempio Pagina di HTML5 e Pagina modulo adattivo.

   * Ulteriori esempi vengono forniti come parte del contenuto di esempio [`We.Retail`](/help/sites-developing/we-retail.md).

* I tipi di modello vengono in genere definiti dagli sviluppatori.

I tipi di modello preconfigurati sono memorizzati in:

* `/libs/settings/wcm/template-types`

>[!CAUTION]
>
>Non modificare nulla nel percorso `/libs`. Il motivo è che il contenuto di `/libs` viene sovrascritto al successivo aggiornamento dell&#39;istanza e potrebbe essere sovrascritto quando si applica un hotfix o un feature pack.

I tipi di modello specifici per il sito devono essere memorizzati nella posizione simile di:

* `/apps/settings/wcm/template-types`

Le definizioni per i tipi di modelli personalizzati devono essere memorizzate in cartelle definite dall&#39;utente (scelta consigliata) o in alternativa in `global`. Ad esempio:

* `/conf/<my-folder-01>/<my-folder-02>/settings/wcm/template-types`
* `/conf/<my-folder>/settings/wcm/template-types`
* `/conf/global/settings/wcm/template-types`

>[!CAUTION]
>
>I tipi di modello devono rispettare la struttura di cartelle corretta (ovvero `/settings/wcm/...`), altrimenti i tipi di modello non vengono trovati.

### Tipo di modello e gruppi di dispositivi mobili {#template-type-and-mobile-device-groups-br}

I [gruppi di dispositivi](/help/sites-developing/mobile.md#device-groups) utilizzati per un modello modificabile (impostato come percorso relativo della proprietà `cq:deviceGroups`) definiscono quali dispositivi mobili sono disponibili come emulatori nella [modalità di layout](/help/sites-authoring/responsive-layout.md) dell&#39;authoring delle pagine. Questo valore può essere impostato in due posizioni:

* Sul tipo di modello modificabile
* Sul modello modificabile

Quando si crea un modello modificabile, il valore viene copiato dal tipo di modello al singolo modello. Se il valore non è impostato sul tipo, può essere impostato sul modello. Una volta creato un modello, non vi è alcuna ereditarietà dal tipo al modello.

>[!CAUTION]
>
>Il valore di `cq:deviceGroups` deve essere impostato come percorso relativo come `mobile/groups/responsive` e non come percorso assoluto come `/etc/mobile/groups/responsive`.

>[!NOTE]
>
>Con [modelli statici](/help/sites-developing/page-templates-static.md), è possibile impostare il valore di `cq:deviceGroups` nella directory principale del sito.
>
>Con i modelli modificabili, questo valore ora è memorizzato a livello di modello e non è supportato a livello di pagina principale.

### Creazione di tipi di modello {#creating-template-types}

Se è stato creato un modello che può fungere da base per altri modelli, è possibile copiarlo come tipo di modello.

1. Crea un modello come faresti con qualsiasi modello modificabile. Consulta [Creazione di modelli di pagina](/help/sites-authoring/templates.md#creating-a-new-template-template-author). Questo può fungere da base per il tipo di modello.
1. Utilizzando CRXDE Lite, copia il modello appena creato dal nodo `templates` al nodo `template-types` nella [cartella modelli](/help/sites-developing/page-templates-editable.md#template-folders).
1. Elimina il modello dal nodo `templates` nella [cartella modelli](/help/sites-developing/page-templates-editable.md#template-folders).
1. Nella copia del modello presente nel nodo `template-types`, eliminare tutte le proprietà `cq:template` e `cq:templateType` da tutti i nodi `jcr:content`.

Puoi anche sviluppare un tipo di modello personalizzato utilizzando come base un modello modificabile di esempio, disponibile su GitHub.

CODICE SU GITHUB

Puoi trovare il codice di questa pagina su GitHub

* [Apri progetto aem-sites-example-custom-template-type su GitHub](https://github.com/Adobe-Marketing-Cloud/aem-sites-example-custom-template-type)
* Scarica il progetto come [file ZIP](https://codeload.github.com/Adobe-Marketing-Cloud/aem-sites-example-custom-template-type/zip/refs/heads/master)

## Definizioni dei modelli {#template-definitions}

Le definizioni per i modelli modificabili sono archiviate [cartelle definite dall&#39;utente](/help/sites-developing/page-templates-editable.md#template-folders) (consigliato) o in alternativa in `global`. Ad esempio:

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

Gli elementi principali sono i seguenti:

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

   * **Tipo**: `String`

   * **Valore**: `draft`, `enabled` o `disabled`

### Struttura {#structure}

Definisce la struttura della pagina risultante:

* Viene unito al contenuto iniziale ( `/initial`) durante la creazione di una pagina.
* Le modifiche apportate alla struttura vengono applicate a tutte le pagine create con il modello.
* Il nodo `root` ( `structure/jcr:content/root`) definisce l&#39;elenco dei componenti disponibili nella pagina risultante.

   * I componenti definiti nella struttura del modello non possono essere spostati o eliminati dalle pagine risultanti.
   * Dopo lo sblocco di un componente, la proprietà `editable` viene impostata su `true`.

   * Dopo lo sblocco di un componente che contiene già contenuto, questo contenuto viene spostato nel ramo `initial`.

* Il nodo `cq:responsive` contiene le definizioni per il layout reattivo.

### Contenuto iniziale {#initial-content}

Definisce il contenuto iniziale di una nuova pagina al momento della creazione:

* Contiene un nodo `jcr:content` copiato in qualsiasi nuova pagina.
* Viene unito alla struttura ( `/structure`) durante la creazione di una pagina.
* Tutte le pagine esistenti vengono aggiornate se il contenuto iniziale viene modificato dopo la creazione.
* Il nodo `root` contiene un elenco di componenti per definire ciò che è disponibile nella pagina risultante.
* Se il contenuto viene aggiunto a un componente in modalità struttura e tale componente viene successivamente sbloccato (o viceversa), tale contenuto viene utilizzato come contenuto iniziale.

### Layout {#layout}

Quando [modifichi un modello, puoi definire il layout](/help/sites-authoring/templates.md). Questa esercitazione utilizza il [layout responsivo standard](/help/sites-authoring/responsive-layout.md) che può anche essere [configurato](/help/sites-administering/configuring-responsive-layout.md).

### Criteri per contenuto {#content-policies}

I criteri di contenuto (o progettazione) definiscono le proprietà di progettazione di un componente, ad esempio la disponibilità del componente o le dimensioni minima/massima. Questi criteri sono applicabili al modello (e alle pagine create con il modello). I criteri per i contenuti possono essere creati e selezionati nell’editor modelli.

* La proprietà `cq:policy` nel nodo `root`
  `/conf/<your-folder>/settings/wcm/templates/<your-template>/policies/jcr:content/root`
Fornisce un riferimento relativo al criterio del contenuto per il sistema paragrafo della pagina.

* La proprietà `cq:policy`, nei nodi espliciti del componente in `root`, fornisce collegamenti ai criteri per i singoli componenti.

* Le definizioni effettive dei criteri sono memorizzate in:
  `/conf/<your-folder>/settings/wcm/policies/wcm/foundation/components`

>[!NOTE]
>
>I percorsi delle definizioni dei criteri dipendono dal percorso del componente. `cq:policy` contiene un riferimento relativo alla configurazione stessa.

>[!NOTE]
>
>Le pagine create da modelli modificabili non offrono una modalità Progettazione nell’editor di pagine.
>
>L&#39;albero `policies` di un modello modificabile ha la stessa gerarchia della configurazione in modalità progettazione di un modello statico in:
>
>`/etc/designs/<my-site>/jcr:content/<component-name>`
>
>La configurazione in modalità progettazione di un modello statico è stata definita per ogni componente pagina.

### Criteri di pagina {#page-policies}

I criteri di pagina consentono di definire il [criterio contenuto](#content-policies) per la pagina (parsys principale), nel modello o nelle pagine risultanti.

### Abilitazione e autorizzazione di un modello per l’utilizzo {#enabling-and-allowing-a-template-for-use}

1. **Abilita il modello**

   Prima di poter utilizzare un modello, è necessario abilitarlo in uno dei modi seguenti:

   * [Abilitazione del modello](/help/sites-authoring/templates.md#enablingatemplateauthor) dalla console **Modelli**.

   * Impostazione della proprietà di stato nel nodo `jcr:content`.

      * Ad esempio, su:

        `/conf/<your-folder>/settings/wcm/templates/<your-template>/jcr:content`

      * Definisci la proprietà:

         * Nome: stato
         * Tipo: String
         * Valore: `enabled`

1. **Modelli consentiti**

   * [Definisci i percorsi dei modelli consentiti nelle **Proprietà pagina**](/help/sites-authoring/templates.md#allowing-a-template-author) della pagina appropriata o della pagina principale di un ramo secondario.
   * Imposta la proprietà:

     `cq:allowedTemplates`
Nel nodo `jcr:content` del ramo richiesto.

   Ad esempio, con un valore di:

   `/conf/<your-folder>/settings/wcm/templates/.*`

## Pagine di contenuto risultanti {#resultant-content-pages}

Pagine create da modelli modificabili:

* Sono state create con una sottostruttura unita da `structure` e `initial` nel modello

* Includere riferimenti alle informazioni contenute nel modello e nel tipo di modello. È possibile ottenere questa funzionalità con un nodo `jcr:content` con le proprietà:

   * `cq:template`
Fornisce il riferimento dinamico al modello effettivo e consente di riflettere le modifiche al modello sulle pagine effettive.

   * `cq:templateType`
Fornisce un riferimento al tipo di modello.

![chlimage_1-71](assets/chlimage_1-71.png)

Il diagramma precedente mostra l’interrelazione tra modelli, contenuto e componenti:

* Controller - `/content/<my-site>/<my-page>`
Pagina risultante che fa riferimento al modello. Il contenuto controlla l&#39;intero processo. In base alle definizioni, accede al modello e ai componenti appropriati.

* Configurazione - `/conf/<my-folder>/settings/wcm/templates/<my-template>`
Il [modello e i criteri dei contenuti correlati](#template-definitions) definiscono la configurazione della pagina.

* Modello: bundle OSGi
I [bundle OSGI](/help/sites-deploying/osgi-configuration-settings.md) implementano la funzionalità.

* Visualizza - `/apps/<my-site>/components`
Sia negli ambienti di authoring che in quelli di pubblicazione, il rendering del contenuto viene eseguito da [componenti](/help/sites-developing/components.md).

Durante il rendering di una pagina:

* **Modelli**:

   * Per accedere al modello corrispondente alla pagina, viene fatto riferimento alla proprietà `cq:template` del nodo `jcr:content`.

* **Componenti**:

   * Il componente page unisce la struttura `structure/jcr:content` del modello con la struttura `jcr:content` della pagina.

   * Il componente Pagina consente all’autore di modificare solo i nodi della struttura del modello contrassegnati come modificabili (e gli eventuali elementi secondari).
   * Durante il rendering di un componente su una pagina, il percorso relativo di tale componente viene preso dal nodo `jcr:content`; viene quindi cercato lo stesso percorso sotto il nodo `policies/jcr:content` del modello.

      * La proprietà `cq:policy` di questo nodo punta al criterio del contenuto effettivo, ovvero contiene la configurazione di progettazione per quel componente.

      * Questa funzionalità consente di disporre di più modelli che riutilizzano le stesse configurazioni dei criteri per i contenuti.
