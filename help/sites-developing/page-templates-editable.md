---
title: Modelli di pagina - Modificabili
seo-title: Page Templates - Editable
description: I modelli modificabili sono stati introdotti in , consentono agli utenti non sviluppatori di creare e modificare modelli, forniscono modelli che mantengono una connessione dinamica a qualsiasi pagina da essi creata e rendono il componente pagina più generico
seo-description: Editable templates have been introduced to, allow non-developers to create and edit templates, provide templates that retain a dynamic connection to any pages created from them, and make the page component more generic
uuid: 61791960-fdef-4e49-878a-11fdf1d4f0ab
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 1099cc44-de6d-499e-8b52-f2f5811ae086
docset: aem65
exl-id: dcb66b6d-d731-493e-8936-12d529f6cbde
source-git-commit: ae56ffafff38fe60530a8850732de58ba8c8f8f9
workflow-type: tm+mt
source-wordcount: '3252'
ht-degree: 9%

---

# Modelli di pagina - Modificabili {#page-templates-editable}

Sono stati introdotti modelli modificabili per:

* Consenti agli autori specializzati di [creare e modificare modelli](/help/sites-authoring/templates.md).

   * Questi autori specializzati sono chiamati **autori di modelli**
   * Gli autori dei modelli devono essere membri del gruppo `template-authors` gruppo.

* Fornisci modelli che mantengono una connessione dinamica a tutte le pagine create da essi. In questo modo tutte le modifiche apportate al modello verranno applicate alle pagine stesse.
* Rendete il componente pagina più generico in modo che il componente pagina di base possa essere utilizzato senza personalizzazione.

Con i modelli modificabili, le parti che compongono una pagina vengono isolate all’interno dei componenti. È possibile configurare le combinazioni di componenti necessarie in un’interfaccia utente, eliminando in tal modo la necessità di sviluppare un nuovo componente di pagina per ogni variante di pagina.

>[!NOTE]
>
>[Modelli statici](/help/sites-developing/page-templates-static.md) sono anche disponibili.

Questo documento:

* Offre una panoramica della creazione di modelli modificabili

   * Per maggiori dettagli vedi [Creazione di modelli di pagina](/help/sites-authoring/templates.md)

* Descrive le attività di amministrazione/sviluppatore necessarie per creare modelli modificabili
* Descrive le basi tecniche dei modelli modificabili

Questo documento presuppone che tu abbia già familiarità con la creazione e la modifica dei modelli. Vedere il documento di authoring [Creazione di modelli di pagina](/help/sites-authoring/templates.md), che descrive le funzionalità dei modelli modificabili esposte all’autore del modello.

>[!NOTE]
>
>L’esercitazione seguente potrebbe interessare anche l’impostazione di un modello di pagina modificabile in un nuovo progetto:
>[Guida introduttiva ad AEM Sites Parte 2 - Creazione di una pagina e di un modello di base](https://helpx.adobe.com/experience-manager/kt/sites/using/getting-started-wknd-tutorial-develop/part2.html)

## Creazione di un nuovo modello {#creating-a-new-template}

La creazione di modelli modificabili viene eseguita principalmente con [console e editor modelli](/help/sites-authoring/templates.md) da un autore di modelli. Questa sezione fornisce una panoramica di questo processo e ne segue una descrizione a livello tecnico.

Per informazioni su come utilizzare i modelli modificabili in un progetto AEM consulta [Creazione di un progetto AEM utilizzando Lazybones](https://helpx.adobe.com/experience-manager/using/aem_lazybones.html).

Durante la creazione di un nuovo modello modificabile:

1. Crea un [cartella dei modelli](#template-folders). Questa operazione non è obbligatoria, ma è consigliata la best practice.
1. Seleziona una [tipo di modello](#template-type). Viene copiato per creare il [definizione del modello](#template-definitions).

   >[!NOTE]
   >
   >Viene fornita una selezione di tipi di modelli pronti all’uso. È inoltre possibile [creare tipi di modelli specifici per il sito](/help/sites-developing/page-templates-editable.md#creating-template-types) se necessario.

1. Configura la struttura, i criteri dei contenuti, il contenuto iniziale e il layout del nuovo modello.

   **Struttura**

   * La struttura ti consente di definire componenti e contenuti per il modello.
   * I componenti definiti nella struttura del modello non possono essere spostati su una pagina risultante, né eliminati da alcuna pagina risultante.

      * Se crei un modello in una cartella personalizzata al di fuori del contenuto di esempio di We.Retail, puoi scegliere Componenti di base o utilizzare [Componenti core](https://helpx.adobe.com/experience-manager/core-components/using/developing.html).
   * Se desideri che gli autori delle pagine siano in grado di aggiungere e rimuovere componenti, aggiungi un sistema di paragrafi al modello.
   * I componenti possono essere sbloccati e bloccati di nuovo per consentire di definire il contenuto iniziale.

   Per informazioni dettagliate su come un autore di modelli definisce la struttura, consulta [Creazione di modelli di pagina](/help/sites-authoring/templates.md#editing-a-template-structure-template-author).

   Per i dettagli tecnici della struttura, vedi [Struttura](/help/sites-developing/page-templates-editable.md#structure) in questo documento.

   **Criteri**

   * I criteri dei contenuti definiscono le proprietà di progettazione di un componente.

      * Ad esempio, i componenti disponibili o le dimensioni minime e massime.
   * Questi sono applicabili al modello (e alle pagine create con tale modello).

   Per informazioni dettagliate su come un autore di modelli definisce i criteri, consulta [Creazione di modelli di pagina](/help/sites-authoring/templates.md#editing-a-template-structure-template-author).

   Per i dettagli tecnici delle politiche, consulta [Criteri di contenuto](/help/sites-developing/page-templates-editable.md#content-policies) in questo documento.

   **Contenuto iniziale**

   * Il contenuto iniziale definisce il contenuto che verrà visualizzato quando una pagina viene creata per la prima volta in base al modello.
   * Il contenuto iniziale può quindi essere modificato dagli autori delle pagine.

   Per informazioni dettagliate su come un autore di modelli definisce la struttura, consulta [Creazione di modelli di pagina](/help/sites-authoring/templates.md#editing-a-template-initial-content-author).

   Per informazioni tecniche sul contenuto iniziale, consulta [Contenuto iniziale](/help/sites-developing/page-templates-editable.md#initial-content) in questo documento.

   **Layout**

   * È possibile definire il layout del modello per una serie di dispositivi.
   * Il Layout reattivo per i modelli funziona come per la creazione delle pagine.

   Per informazioni dettagliate sulla definizione del layout del modello da parte dell’autore, consulta [Creazione di modelli di pagina](/help/sites-authoring/templates.md#editing-a-template-layout-template-author).

   Per informazioni tecniche sul layout dei modelli, consulta [Layout](/help/sites-developing/page-templates-editable.md#layout) in questo documento.

1. Abilita il modello, quindi lo consenti per strutture di contenuto specifiche.

   * Un modello può essere abilitato o disabilitato per renderlo disponibile o non disponibile agli autori di pagine.
   * Un modello può essere reso disponibile o non disponibile per alcuni rami di pagina.

   Per informazioni dettagliate su come un autore di modelli abilita un modello, consulta [Creazione di modelli di pagina](/help/sites-authoring/templates.md#enabling-and-allowing-a-template-template-author).

   Per informazioni tecniche sull’abilitazione di un modello, consulta [Abilitazione e autorizzazione di un modello per noi](/help/sites-developing/page-templates-editable.md#enabling-and-allowing-a-template-for-use)e in questo documento

1. Utilizzalo per creare pagine di contenuto.

   * Quando si utilizza un modello per creare una nuova pagina, non vi è alcuna differenza visibile e nessuna indicazione tra modelli statici e modificabili.
   * Per l’autore della pagina, il processo è trasparente.

   Per informazioni dettagliate su come un autore di pagine utilizza i modelli per creare una pagina, consulta [Creazione e organizzazione delle pagine](/help/sites-authoring/managing-pages.md#templates).

   Per informazioni tecniche sulla creazione di pagine con modelli modificabili, consulta [Pagine dei contenuti risultanti](/help/sites-developing/page-templates-editable.md#resultant-content-pages) in questo documento.

>[!TIP]
>
>Non inserire mai informazioni che devono essere internazionalizzate in un modello. Ai fini dell&#39;internalizzazione, la [funzionalità di localizzazione dei componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/get-started/localization.html?lang=it) sono consigliati.

>[!NOTE]
>
>I modelli sono strumenti potenti per semplificare il flusso di lavoro di creazione della pagina. Tuttavia, troppi modelli possono sopraffare gli autori e confondere la creazione di pagine. Una buona regola è mantenere il numero di modelli sotto i 100.
>
>Adobe consiglia di non disporre di più di 1000 modelli a causa di potenziali impatti sulle prestazioni.

>[!NOTE]
>
>La libreria client dell&#39;editor presuppone la presenza di `cq.shared` spazio dei nomi nelle pagine di contenuto e se è assente nell&#39;errore JavaScript `Uncaught TypeError: Cannot read property 'shared' of undefined` risulterà.
>
>Tutte le pagine di contenuto di esempio contengono `cq.shared`, quindi qualsiasi contenuto basato su di essi include automaticamente `cq.shared`. Tuttavia, se decidi di creare da zero pagine di contenuto personalizzate senza basarle su contenuti di esempio, devi assicurarti di includere il `cq.shared` spazio dei nomi.
>
>Vedi [Utilizzo delle librerie lato client](/help/sites-developing/clientlibs.md) per ulteriori informazioni.

## Cartelle dei modelli {#template-folders}

Per organizzare i modelli è possibile utilizzare le cartelle seguenti:

* **globale**
* Specifiche del sito Le cartelle specifiche del sito create per organizzare i modelli vengono create con un account che dispone di privilegi di amministratore.

>[!NOTE]
>
>Anche se è possibile nidificare le cartelle, quando l’utente le visualizza nel **Modelli** console sono presentate come una struttura piatta.

In un’istanza AEM standard la cartella **globale** esiste già nella console modelli. Questa contiene i modelli predefiniti e funge da fallback se nella cartella corrente non sono presenti criteri e/o tipi di modello. È possibile aggiungere i modelli predefiniti a questa cartella o creare una nuova cartella (scelta consigliata).

>[!NOTE]
>
>È consigliabile creare una nuova cartella contenente i modelli personalizzati e non utilizzare la cartella globale.

>[!CAUTION]
>
>Le cartelle devono essere create da un utente con `admin` diritti.

I tipi di modello e i criteri vengono ereditati in tutte le cartelle in base al seguente ordine di precedenza:

1. La cartella corrente.
1. Elemento padre/i della cartella corrente.
1. `/conf/global`
1. `/apps`
1. `/libs`

Viene creato un elenco di tutte le voci consentite. Se una qualsiasi configurazione si sovrappone ( `path`/ `label`), all’utente viene presentata solo l’istanza più vicina alla cartella corrente.

Per creare una nuova cartella è possibile effettuare le seguenti operazioni:

* Programmaticamente o con CRXDE Lite
* Utilizzo del browser di configurazione

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

   * Valore: Titolo (per la cartella) che si desidera visualizzare nel **Modelli** console.

1. In *aggiunta* alle autorizzazioni e ai privilegi di authoring standard (ad esempio `content-authors`) devi ora assegnare i gruppi e definire i diritti di accesso richiesti (ACL, Access Rights) affinché gli autori possano creare modelli nella nuova cartella.

   La `template-authors` gruppo è il gruppo predefinito che deve essere assegnato. Vedi la sezione seguente [ACL e gruppi](/help/sites-developing/page-templates-editable.md#acls-and-groups) per i dettagli.

   Vedi [Accesso alla gestione dei diritti](/help/sites-administering/user-group-ac-admin.md#access-right-management) per informazioni complete sulla gestione e l&#39;assegnazione dei diritti di accesso.

### Utilizzo del browser di configurazione {#using-the-configuration-browser}

1. Vai a **Navigazione globale** -> **Strumenti** > **Browser di configurazione**.

   Le cartelle esistenti sono elencate a sinistra, tra cui **globale** cartella.

1. Fai clic su **Crea**.
1. In **Crea configurazione** è necessario configurare i campi seguenti nella finestra di dialogo:

   * **Titolo**: Fornire un titolo per la cartella di configurazione
   * **Modelli modificabili**: Selezione di modelli modificabili all’interno della cartella

1. Fai clic su **Crea**

>[!NOTE]
>
>Nel Browser configurazioni, puoi modificare la cartella globale e attivare la **Modelli modificabili** se desideri creare modelli all’interno di questa cartella, tuttavia questa non è la best practice consigliata.
>
>Consulta la sezione [Browser di configurazione](/help/sites-administering/configurations.md) documentazione per ulteriori informazioni.

### ACL e gruppi {#acls-and-groups}

Una volta create le cartelle dei modelli (tramite CRXDE o con il browser di configurazione), le ACL devono essere definite per i gruppi appropriati per le cartelle dei modelli per garantire la corretta sicurezza.

Le cartelle di modelli per [Implementazione di riferimento di We.Retail](/help/sites-developing/we-retail.md) può essere utilizzato come esempio.

#### Gruppo autori modelli {#the-template-authors-group}

La `template-authors` gruppo è il gruppo utilizzato per gestire l’accesso ai modelli ed è standard con AEM, ma è vuoto. Gli utenti devono essere aggiunti al gruppo per il progetto/sito.

>[!CAUTION]
>
>La `template-authors` gruppo *only* per gli utenti che devono essere in grado di creare nuovi modelli.
>
>La modifica dei modelli è molto potente e, se non viene eseguita correttamente, i modelli esistenti possono essere interrotti. Pertanto questo ruolo dovrebbe essere concentrato e includere solo gli utenti qualificati.

Nella tabella seguente sono descritte le autorizzazioni necessarie per la modifica dei modelli.

<table>
 <tbody>
  <tr>
   <th>Percorso </th>
   <th>Ruolo/Gruppo</th>
   <th>Autorizzazioni<br /> </th>
   <th>Descrizione</th>
  </tr>
  <tr>
   <td rowspan="3"><code>/conf/&lt;<i>your-folder</i>&gt;/settings/wcm/templates</code></td>
   <td>Autori di modelli<br /> </td>
   <td>leggere, scrivere, replicare</td>
   <td>Autori di modelli che creano, leggono, aggiornano, eliminano e replicano modelli in siti specifici <code>/conf</code> spazio</td>
  </tr>
  <tr>
   <td>Utente web anonimo</td>
   <td>read</td>
   <td>Utente web anonimo deve leggere i modelli durante il rendering di una pagina</td>
  </tr>
  <tr>
   <td>Autori di contenuti</td>
   <td>replicare</td>
   <td>Gli autori replicateContent devono attivare i modelli di una pagina quando si attiva una pagina</td>
  </tr>
  <tr>
   <td rowspan="3"><code>/conf/&lt;<i>your-folder</i>&gt;/settings/wcm/policies</code></td>
   <td><code>Template Author</code></td>
   <td>leggere, scrivere, replicare</td>
   <td>Autori di modelli che creano, leggono, aggiornano, eliminano e replicano modelli in siti specifici <code>/conf</code> spazio</td>
  </tr>
  <tr>
   <td>Utente web anonimo</td>
   <td>read</td>
   <td>L'utente web anonimo deve leggere i criteri durante il rendering di una pagina</td>
  </tr>
  <tr>
   <td>Autori di contenuti</td>
   <td>replicare</td>
   <td>Quando si attiva una pagina, gli autori dei contenuti devono attivare i criteri di un modello di pagina</td>
  </tr>
  <tr>
   <td rowspan="2"><code>/conf/&lt;site&gt;/settings/template-types</code></td>
   <td>Autore del modello</td>
   <td>read</td>
   <td>L’autore del modello crea un nuovo modello basato su uno dei tipi di modello predefiniti.</td>
  </tr>
  <tr>
   <td>Utente web anonimo</td>
   <td>nessuno</td>
   <td>L'utente Web anonimo non deve accedere ai tipi di modello</td>
  </tr>
 </tbody>
</table>

Questa impostazione predefinita `template-authors` il gruppo copre solo le impostazioni del progetto, dove tutte `template-authors` i membri possono accedere e creare tutti i modelli. Per configurazioni più complesse, in cui sono necessari gruppi di autori di modelli multipli per separare l’accesso ai modelli, è necessario creare gruppi di autori di modelli più personalizzati. Tuttavia, le autorizzazioni per i gruppi di autori dei modelli rimarrebbero invariate.

#### Modelli legacy sotto /conf/global {#legacy-templates-under-conf-global}

I modelli non devono più essere memorizzati in `/conf/global`tuttavia, per alcune installazioni legacy potrebbero essere ancora presenti modelli in questa posizione. SOLO in tali situazioni precedenti dovrebbe `/conf/global` i percorsi devono essere configurati in modo esplicito.

<table>
 <tbody>
  <tr>
   <th>Percorso </th>
   <th>Ruolo/Gruppo</th>
   <th>Autorizzazioni<br /> </th>
   <th>Descrizione</th>
  </tr>
  <tr>
   <td rowspan="3"><code>/conf/global/settings/wcm/templates</code></td>
   <td>Autori di modelli</td>
   <td>leggere, scrivere, replicare</td>
   <td>Autori di modelli che creano, leggono, aggiornano, eliminano e replicano modelli in <code>/conf/global</code></td>
  </tr>
  <tr>
   <td>Utente web anonimo</td>
   <td>read</td>
   <td>Utente web anonimo deve leggere i modelli durante il rendering di una pagina</td>
  </tr>
  <tr>
   <td>Autori di contenuti</td>
   <td>replicare</td>
   <td>Quando si attiva una pagina, gli autori dei contenuti devono attivare i modelli di pagina</td>
  </tr>
  <tr>
   <td rowspan="3"><code>/conf/global/settings/wcm/policies</code></td>
   <td><code>Template Author</code></td>
   <td>leggere, scrivere, replicare</td>
   <td>Autori di modelli che creano, leggono, aggiornano, eliminano e replicano modelli in <code>/conf/global</code></td>
  </tr>
  <tr>
   <td>Utente web anonimo</td>
   <td>read</td>
   <td>L'utente web anonimo deve leggere i criteri durante il rendering di una pagina</td>
  </tr>
  <tr>
   <td>Autori di contenuti</td>
   <td>replicare</td>
   <td>Quando si attiva una pagina, gli autori dei contenuti devono attivare i criteri di un modello di pagina</td>
  </tr>
  <tr>
   <td rowspan="2"><code>/conf/global/settings/wcm/template-types</code></td>
   <td>Autore del modello</td>
   <td>read</td>
   <td>L’autore del modello crea un nuovo modello basato su uno dei tipi di modello predefiniti</td>
  </tr>
  <tr>
   <td>Utente web anonimo</td>
   <td>nessuno</td>
   <td>L'utente Web anonimo non deve accedere ai tipi di modello</td>
  </tr>
 </tbody>
</table>

## Tipo di modello {#template-type}

Quando si crea un nuovo modello, è necessario specificare un tipo di modello:

* I tipi di modello forniscono efficacemente i modelli per un modello. Quando si crea un nuovo modello, la struttura e il contenuto iniziale del tipo di modello selezionato vengono utilizzati per creare il nuovo modello.

   * Il tipo di modello viene copiato per creare il modello.
   * Una volta effettuata la copia, l’unica connessione tra il modello e il tipo di modello è un riferimento statico a scopo informativo.

* I tipi di modello consentono di definire:

   * Il tipo di risorsa del componente pagina.
   * Il criterio del nodo principale, che definisce i componenti consentiti nell’editor modelli.
   * È consigliabile definire i punti di interruzione per la griglia reattiva e la configurazione dell’emulatore mobile in sul tipo di modello. Questo è facoltativo, perché la configurazione può essere definita anche sul singolo modello (vedi [Tipo di modello e gruppi di dispositivi mobili](/help/sites-developing/page-templates-editable.md#p-template-type-and-mobile-device-groups-br-p)).

* AEM fornisce una piccola selezione di tipi di modelli predefiniti, ad esempio Pagina di HTML5 e Pagina modulo adattivo.

   * Altri esempi sono forniti come parte del [We.Retail](/help/sites-developing/we-retail.md) contenuto di esempio.

* I tipi di modello sono generalmente definiti dagli sviluppatori.

I tipi di modelli predefiniti sono memorizzati in:

* `/libs/settings/wcm/template-types`

>[!CAUTION]
>
>Non devi cambiare nulla nel `/libs` percorso. Questo perché il contenuto di `/libs` viene sovrascritto la prossima volta che aggiorni l’istanza (e può essere sovrascritto quando applichi un hotfix o un feature pack).

I tipi di modelli specifici per il sito devono essere memorizzati nel percorso comparabile di:

* `/apps/settings/wcm/template-types`

Le definizioni dei tipi di modelli personalizzati devono essere memorizzate in cartelle definite dall&#39;utente (consigliato) o in alternativa in `global`. Esempio:

* `/conf/<my-folder-01>/<my-folder-02>/settings/wcm/template-types`
* `/conf/<my-folder>/settings/wcm/template-types`
* `/conf/global/settings/wcm/template-types`

>[!CAUTION]
>
>I tipi di modello devono rispettare la struttura di cartelle corretta (ovvero `/settings/wcm/...`), altrimenti i tipi di modello non verranno trovati.

### Tipo di modello e gruppi di dispositivi mobili {#template-type-and-mobile-device-groups-br}

La [gruppi di dispositivi](/help/sites-developing/mobile.md#device-groups) utilizzato per un modello modificabile (impostato come percorso relativo della proprietà `cq:deviceGroups`) definisci quali dispositivi mobili sono disponibili come emulatori nel [modalità layout](/help/sites-authoring/responsive-layout.md) di authoring delle pagine. Questo valore può essere impostato in due posizioni:

* Sul tipo di modello modificabile
* Sul modello modificabile

Quando si crea un nuovo modello modificabile, il valore viene copiato dal tipo di modello al singolo modello. Se il valore non è impostato sul tipo, può essere impostato sul modello. Una volta creato un modello, non esiste alcuna ereditarietà dal tipo al modello.

>[!CAUTION]
>
>Il valore di `cq:deviceGroups` deve essere impostato come percorso relativo, ad esempio `mobile/groups/responsive` e non come percorso assoluto come `/etc/mobile/groups/responsive`.

>[!NOTE]
>
>Con [modelli statici](/help/sites-developing/page-templates-static.md), il valore di `cq:deviceGroups` potrebbe essere impostato nella directory principale del sito.
>
>Con i modelli modificabili, questo valore viene ora memorizzato a livello di modello e non è supportato a livello di pagina principale.

### Creazione di tipi di modelli {#creating-template-types}

Se hai creato un modello che può fungere da base per altri modelli, puoi copiarlo come tipo di modello.

1. Crea un modello come qualsiasi altro modello modificabile [come documentato qui](/help/sites-authoring/templates.md#creating-a-new-template-template-author), che fungerà da base per il tipo di modello.
1. Utilizzando CRXDE Lite, copia il modello appena creato dal `templates` al nodo `template-types` sotto il nodo [cartella dei modelli](/help/sites-developing/page-templates-editable.md#template-folders).
1. Elimina il modello dal `templates` sotto il nodo [cartella dei modelli](/help/sites-developing/page-templates-editable.md#template-folders).
1. Nella copia del modello che si trova sotto il `template-types` nodo, elimina tutto `cq:template` e `cq:templateType` proprietà da tutti `jcr:content` nodi.

Puoi anche sviluppare un tipo di modello personalizzato utilizzando un modello modificabile di esempio come base, disponibile su GitHub.

CODICE SU GITHUB

Puoi trovare il codice di questa pagina su GitHub

* [Apri progetto aem-sites-example-custom-template-type su GitHub](https://github.com/Adobe-Marketing-Cloud/aem-sites-example-custom-template-type)
* Scarica il progetto come [un file ZIP](https://github.com/Adobe-Marketing-Cloud/aem-sites-example-custom-template-type/archive/master.zip)

## Definizioni dei modelli {#template-definitions}

Vengono memorizzate le definizioni dei modelli modificabili [cartelle definite dall&#39;utente](/help/sites-developing/page-templates-editable.md#template-folders) (consigliato) o in alternativa in `global`. Esempio:

* `/conf/<my-folder>/settings/wcm/templates`
* `/conf/<my-folder-01>/<my-folder-02>/settings/wcm/templates`
* `/conf/global/settings/wcm/templates`

Il nodo principale del modello è di tipo `cq:Template` con struttura ossea di:

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

Questo nodo contiene le proprietà del modello:

* **Nome**: `jcr:title`

* **Nome**: `status`

   * **Tipo**: `String`

   * **Valore**: `draft`, `enabled` o `disabled`

### Struttura {#structure}

Definisce la struttura della pagina risultante:

* Viene unito al contenuto iniziale ( `/initial`) durante la creazione di una nuova pagina.
* Le modifiche apportate alla struttura verranno applicate a tutte le pagine create con il modello.
* La `root` ( `structure/jcr:content/root`Il nodo ) definisce l’elenco dei componenti che saranno disponibili nella pagina risultante.

   * I componenti definiti nella struttura del modello non possono essere spostati o eliminati dalle pagine risultanti.
   * Quando un componente viene sbloccato, la `editable` è impostata su `true`.

   * Quando un componente che contiene già è sbloccato, il contenuto viene spostato in `initial` ramo.

* La `cq:responsive` node contiene le definizioni del layout dinamico.

### Contenuto iniziale {#initial-content}

Definisce il contenuto iniziale di una nuova pagina al momento della creazione:

* Contiene un `jcr:content` che viene copiato in una nuova pagina.
* È unito alla struttura ( `/structure`) durante la creazione di una nuova pagina.
* Eventuali pagine esistenti non verranno aggiornate se il contenuto iniziale viene modificato dopo la creazione.
* La `root` node contiene un elenco di componenti per definire cosa sarà disponibile nella pagina risultante.
* Se il contenuto viene aggiunto a un componente in modalità struttura e successivamente viene sbloccato (o viceversa), viene utilizzato come contenuto iniziale.

### Layout {#layout}

Quando [modifica di un modello da definire](/help/sites-authoring/templates.md), utilizza [layout dinamico standard](/help/sites-authoring/responsive-layout.md) che può anche [configurato](/help/sites-administering/configuring-responsive-layout.md).

### Criteri di contenuto {#content-policies}

I criteri relativi al contenuto (o alla progettazione) definiscono le proprietà di progettazione di un componente, ad esempio la disponibilità del componente o le dimensioni minime/massime. Questi sono applicabili al modello (e alle pagine create con tale modello). I criteri del contenuto possono essere creati e selezionati nell’editor modelli.

* La proprietà `cq:policy`, sul `root` nodo
   `/conf/<your-folder>/settings/wcm/templates/<your-template>/policies/jcr:content/root`
Fornisce un riferimento relativo al criterio del contenuto per il sistema paragrafo della pagina.

* La proprietà `cq:policy`, sui nodi espliciti del componente sotto `root`, fornisce collegamenti ai criteri per i singoli componenti.

* Le definizioni effettive dei criteri sono memorizzate in:
   `/conf/<your-folder>/settings/wcm/policies/wcm/foundation/components`

>[!NOTE]
>
>I percorsi delle definizioni dei criteri dipendono dal percorso del componente. `cq:policy` contiene un riferimento relativo alla configurazione stessa.

>[!NOTE]
>
>Le pagine create da modelli modificabili non offrono una modalità Progettazione nell’editor di pagine.
>
>La `policies` la struttura di un modello modificabile ha la stessa gerarchia della configurazione della modalità di progettazione di un modello statico in:
>
>`/etc/designs/<my-site>/jcr:content/<component-name>`
>
>La configurazione in modalità di progettazione di un modello statico è stata definita per ciascun componente della pagina.

### Criteri di pagina {#page-policies}

I criteri di pagina consentono di definire [informativa sui contenuti](#content-policies) per la pagina (parsys principale), nel modello o nelle pagine risultanti.

### Abilitazione e autorizzazione di un modello per l’uso {#enabling-and-allowing-a-template-for-use}

1. **Attiva il modello**

   Prima di poter utilizzare un modello, è necessario attivarlo tramite:

   * [Abilitazione del modello](/help/sites-authoring/templates.md#enablingatemplateauthor) dal **Modelli** console.

   * Impostazione della proprietà di stato nel `jcr:content` nodo.

      * Ad esempio, su:
         `/conf/<your-folder>/settings/wcm/templates/<your-template>/jcr:content`

      * Definisci la proprietà:

         * Nome: status
         * Tipo: Stringa
         * Valore: `enabled`

1. **Modelli consentiti**

   * [Definisci i percorsi dei modelli consentiti nel **Proprietà pagina**](/help/sites-authoring/templates.md#allowing-a-template-author) della pagina o della pagina principale appropriata di un ramo secondario.
   * Imposta la proprietà:
      `cq:allowedTemplates`
Sulla 
`jcr:content` nodo del ramo richiesto.
   Ad esempio, con un valore di:

   `/conf/<your-folder>/settings/wcm/templates/.*`

## Pagine dei contenuti risultanti {#resultant-content-pages}

Pagine create da modelli modificabili:

* Sono create con una sottostruttura da cui è stata eseguita l’unione `structure` e `initial` nel modello

* Avere riferimenti alle informazioni contenute nel modello e nel tipo di modello. Ciò è possibile con un `jcr:content` nodo con le proprietà:

   * `cq:template`
Fornisce il riferimento dinamico al modello effettivo; consente di visualizzare le modifiche apportate al modello nelle pagine effettive.

   * `cq:templateType`
Fornisce un riferimento al tipo di modello.

![chlimage_1-71](assets/chlimage_1-71.png)

Il diagramma precedente mostra come i modelli, i contenuti e i componenti si rapportano:

* Controller - `/content/<my-site>/<my-page>`
La pagina risultante che fa riferimento al modello. Il contenuto controlla l’intero processo. In base alle definizioni, accede al modello e ai componenti appropriati.

* Configurazione - `/conf/<my-folder>/settings/wcm/templates/<my-template>`
La [criteri di contenuto e modelli correlati](#template-definitions) definisci la configurazione della pagina.

* Modello - Bundle OSGi [Bundle OSGI](/help/sites-deploying/osgi-configuration-settings.md) implementa la funzionalità .

* Visualizza - `/apps/<my-site>/components`
Sia nell’ambiente di authoring che in quello di pubblicazione, il rendering del contenuto viene eseguito da [componenti](/help/sites-developing/components.md).

Durante il rendering di una pagina:

* **Modelli**:

   * La `cq:template` proprietà `jcr:content` verrà fatto riferimento al nodo per accedere al modello corrispondente a tale pagina.

* **Componenti**:

   * Il componente pagina unisce il `structure/jcr:content` struttura del modello con `jcr:content` struttura della pagina.

   * Il componente pagina consente solo all’autore di modificare i nodi della struttura del modello che sono stati contrassegnati come modificabili (così come altri elementi secondari).
   * Quando si esegue il rendering di un componente su una pagina, il percorso relativo di tale componente viene ricavato dal `jcr:content` nodo; lo stesso percorso `policies/jcr:content` Viene quindi eseguita la ricerca nel nodo del modello.

      * La `cq:policy` di questo nodo fa riferimento al criterio del contenuto effettivo (ovvero contiene la configurazione di progettazione per quel componente).

      * Questo consente di avere più modelli che riutilizzano le stesse configurazioni dei criteri per i contenuti.
