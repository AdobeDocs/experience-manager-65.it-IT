---
title: Personalizzazione ed estensione dei frammenti di contenuto
seo-title: Customizing and Extending Content Fragments
description: Un frammento di contenuto estende una risorsa standard.
seo-description: A content fragment extends a standard asset.
topic-tags: extending-aem
content-type: reference
docset: aem65
exl-id: 08c88e70-4df9-4627-8a66-1fabe3aee50b
source-git-commit: 9ad531738ac5e3c9d888f685b47c8b322712a89e
workflow-type: tm+mt
source-wordcount: '2778'
ht-degree: 2%

---


# Personalizzazione ed estensione dei frammenti di contenuto{#customizing-and-extending-content-fragments}

Un frammento di contenuto estende una risorsa standard; vedi:

* [Creazione e gestione di frammenti di contenuto](/help/assets/content-fragments/content-fragments.md) e [Authoring delle pagine con frammenti di contenuto](/help/sites-authoring/content-fragments.md) per ulteriori informazioni sui frammenti di contenuto.

* [Gestione delle risorse](/help/assets/manage-assets.md) e [Personalizzazione ed estensione delle risorse](/help/assets/extending-assets.md) per ulteriori informazioni sulle risorse standard.

## Architettura {#architecture}

Le basi [parti costituenti](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment) di un frammento di contenuto:

* A *Frammento di contenuto,*
* costituito da uno o più *Elemento contenuto* s,
* e che possono avere uno o più *Variazione di contenuto* s.

A seconda del tipo di frammento, vengono utilizzati anche modelli o modelli:

>[!CAUTION]
>
>[Modelli per frammenti di contenuto](/help/assets/content-fragments/content-fragments-models.md) sono consigliati per la creazione di tutti i nuovi frammenti.
>
>I modelli per frammenti di contenuto vengono utilizzati per tutti gli esempi in WKND.

>[!NOTE]
>
>Prima di AEM 6.3, i frammenti di contenuto venivano creati in base a modelli anziché a modelli.
>
>I modelli per frammenti di contenuto sono diventati obsoleti. Possono ancora essere utilizzati per creare frammenti, ma si consiglia invece di utilizzare Modelli per frammenti di contenuto . Non verranno aggiunte nuove funzioni ai modelli di frammento e verranno rimosse in una versione futura.

* Modelli per frammenti di contenuto:

   * Utilizzato per definire frammenti di contenuto contenenti contenuto strutturato.
   * I modelli di frammento di contenuto definiscono la struttura di un frammento di contenuto al momento della creazione.
   * Un frammento fa riferimento al modello; le modifiche al modello possono quindi influire su eventuali frammenti dipendenti.
   * I modelli sono formati da tipi di dati.
   * Le funzioni per aggiungere nuove varianti, ecc., devono aggiornare di conseguenza il frammento.

   >[!CAUTION]
   >
   >Qualsiasi modifica apportata a un modello di frammento di contenuto esistente può avere un impatto sui frammenti dipendenti; questo può portare a proprietà orfane in tali frammenti.

* Modelli di frammento di contenuto:

   * Utilizzato per definire frammenti di contenuto semplici.
   * I modelli definiscono la struttura di base (solo testo) di un frammento di contenuto al momento della creazione.
   * Il modello viene copiato nel frammento quando viene creato; pertanto, ulteriori modifiche al modello non verranno applicate ai frammenti esistenti.
   * Le funzioni per aggiungere nuove varianti, ecc., devono aggiornare di conseguenza il frammento.
   * [Modelli per frammenti di contenuto](/help/sites-developing/content-fragment-templates.md) operano in modo diverso da quello di altri meccanismi di modellazione all’interno dell’ecosistema AEM (ad esempio modelli di pagina, ecc.). Dovrebbero pertanto essere considerati separatamente.
   * Se si basa su un modello, il tipo MIME del contenuto viene gestito sul contenuto effettivo; ciò significa che ogni elemento e variante può avere un tipo MIME diverso.

### Integrazione con le risorse {#integration-with-assets}

Content Fragment Management (CFM) fa parte di AEM Assets come:

* I frammenti di contenuto sono risorse.
* Utilizzano la funzionalità Assets esistente.
* Sono completamente integrati con Assets (console di amministrazione, ecc.).

#### Mappatura di frammenti di contenuto strutturati sulle risorse {#mapping-structured-content-fragments-to-assets}

![strutturata da frammento a risorsa](assets/fragment-to-assets-structured.png)

I frammenti di contenuto con contenuto strutturato (ovvero basati su un modello di frammento di contenuto) vengono mappati su un’unica risorsa:

* Tutti i contenuti sono memorizzati nella `jcr:content/data` nodo della risorsa:

   * I dati dell’elemento vengono memorizzati sotto il sotto-nodo principale:
      `jcr:content/data/master`

   * Le varianti sono memorizzate sotto un nodo secondario che porta il nome della variante: ad esempio `jcr:content/data/myvariation`

   * I dati di ciascun elemento vengono memorizzati nel rispettivo sottonodo come proprietà con il nome dell’elemento: Ad esempio, il contenuto dell’elemento `text` viene memorizzato come proprietà `text` su `jcr:content/data/master`

* I metadati e il contenuto associato sono memorizzati di seguito `jcr:content/metadata`
Ad eccezione del titolo e della descrizione, che non sono considerati metadati tradizionali e memorizzati su 
`jcr:content`

#### Mappatura di frammenti di contenuto semplici sulle risorse {#mapping-simple-content-fragments-to-assets}

![chlimage_1-90](assets/chlimage_1-90.png)

I frammenti di contenuto semplice (basati su un modello) sono mappati su un composito costituito da una risorsa principale e (facoltativo) da risorse secondarie:

* Tutte le informazioni non relative al contenuto di un frammento (ad esempio titolo, descrizione, metadati, struttura) vengono gestite esclusivamente sulla risorsa principale.
* Il contenuto del primo elemento di un frammento è mappato al rendering originale della risorsa principale.

   * Le varianti (se ce ne sono) del primo elemento sono mappate ad altre rappresentazioni della risorsa principale.

* Eventuali elementi aggiuntivi (se esistenti) sono mappati su risorse secondarie della risorsa principale.

   * Il contenuto principale di questi elementi aggiuntivi viene mappato sul rendering originale della relativa risorsa secondaria.
   * Altre variazioni (se applicabili) di qualsiasi elemento aggiuntivo sono associate ad altre rappresentazioni della rispettiva attività secondaria.

#### Posizione risorsa {#asset-location}

Come per le risorse standard, un frammento di contenuto è conservato in:

`/content/dam`

#### Autorizzazioni delle risorse {#asset-permissions}

Per maggiori dettagli vedi [Frammento di contenuto - Considerazioni sull’eliminazione](/help/assets/content-fragments/content-fragments-delete.md).

#### Integrazione delle funzioni {#feature-integration}

* La funzione Content Fragment Management (CFM) si basa sul core Assets, ma deve essere il più indipendente possibile.
* CFM fornisce le proprie implementazioni per gli elementi nelle viste a schede/colonne/elenco; questi plug in nelle implementazioni di rendering dei contenuti di Assets esistenti.
* Sono stati estesi diversi componenti di Assets per gestire i frammenti di contenuto.

### Utilizzo di frammenti di contenuto nelle pagine {#using-content-fragments-in-pages}

>[!CAUTION]
>
>La [Componente core frammento di contenuto](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html?lang=it) è ora consigliato. Vedi [Sviluppo di componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/overview.html?lang=it) per ulteriori dettagli.

È possibile fare riferimento ai frammenti di contenuto da AEM pagine, come per qualsiasi altro tipo di risorsa. AEM fornisce [**Frammento di contenuto** componente principale](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html?lang=it) - a [che consente di includere frammenti di contenuto nelle pagine](/help/sites-authoring/content-fragments.md#adding-a-content-fragment-to-your-page). Puoi anche estendere questo **Frammento di contenuto** componente di base.

* Il componente utilizza il `fragmentPath` per fare riferimento al frammento di contenuto effettivo. La `fragmentPath` la proprietà è gestita allo stesso modo di proprietà simili di altri tipi di attività; ad esempio, quando il frammento di contenuto viene spostato in un’altra posizione.

* Il componente ti consente di selezionare la variante da visualizzare.
* È inoltre possibile selezionare una serie di paragrafi per limitare l’output; ad esempio, può essere utilizzato per l’output a più colonne.
* Il componente permette [contenuto intermedio](/help/sites-developing/components-content-fragments.md#in-between-content):

   * Qui il componente permette di inserire altre risorse (immagini, ecc.) tra i paragrafi del frammento a cui si fa riferimento.
   * Per il contenuto intermedio è necessario:

      * essere consapevole della possibilità di riferimenti instabili; il contenuto intermedio (aggiunto durante l’authoring di una pagina) non presenta alcuna relazione fissa con il paragrafo accanto al quale è posizionato, mediante l’inserimento di un nuovo paragrafo (nell’editor dei frammenti di contenuto) prima che la posizione del contenuto intermedio perda la posizione relativa
      * considera i parametri aggiuntivi (come i filtri di variante e paragrafo) per evitare falsi positivi nei risultati della ricerca

>[!NOTE]
>
>**Modello per frammenti di contenuto:**
>
>Quando si utilizza un frammento di contenuto basato su un modello di frammento di contenuto su una pagina, viene fatto riferimento al modello. Ciò significa che se il modello non è stato pubblicato al momento della pubblicazione della pagina, verrà contrassegnato e il modello verrà aggiunto alle risorse da pubblicare con la pagina.
>
>**Modello per frammento di contenuto:**
>
>Quando si utilizza un frammento di contenuto basato su un modello di frammento di contenuto in una pagina, non esiste alcun riferimento in quanto il modello è stato copiato al momento della creazione del frammento.

#### Configurazione tramite la console OSGi {#configuration-using-osgi-console}

L’implementazione back-end dei frammenti di contenuto, ad esempio, è responsabile della possibilità di cercare le istanze di un frammento utilizzato in una pagina o della gestione di contenuti multimediali diversi. Questa implementazione deve sapere quali componenti vengono utilizzati per il rendering dei frammenti e come viene parametrizzato il rendering.

I parametri di questo possono essere configurati nel [Console web](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console), per il bundle OSGi **Configurazione del componente Frammento di contenuto**.

* **Tipi di risorse**
Un elenco di 
`sling:resourceTypes` può essere fornito per definire i componenti utilizzati per il rendering dei frammenti di contenuto e a cui applicare l’elaborazione in background.

* **Proprietà riferimento**
È possibile configurare un elenco di proprietà per specificare dove memorizzare il riferimento al frammento per il rispettivo componente.

>[!NOTE]
>
>Non esiste una mappatura diretta tra proprietà e tipo di componente.
>
>AEM semplicemente la prima proprietà che si trova in un paragrafo. Quindi dovreste scegliere le proprietà con attenzione.

![screenshot_2019-03-18at100941](assets/screenshot_2019-03-18at100941.png)

Per garantire la compatibilità del componente con l’elaborazione in background del frammento di contenuto, è necessario seguire alcune linee guida:

* Il nome della proprietà in cui è definito l’elemento o gli elementi di cui eseguire il rendering deve essere `element` o `elementNames`.

* Il nome della proprietà in cui è definita la variante di cui eseguire il rendering deve essere `variation` o `variationName`.

* Se è supportato l’output di più elementi (utilizzando `elementNames` per specificare più elementi), la modalità di visualizzazione effettiva è definita dalla proprietà `displayMode`:

   * Se il valore è `singleText` (e è configurato un solo elemento) l’elemento viene rappresentato come un testo con contenuto intermedio, supporto del layout, ecc. Questa è l’impostazione predefinita per i frammenti in cui viene eseguito il rendering di un solo elemento.
   * In caso contrario, viene utilizzato un approccio molto più semplice (potrebbe essere denominato &quot;visualizzazione modulo&quot;), in cui non è supportato alcun contenuto intermedio e il contenuto del frammento viene rappresentato &quot;così com’è&quot;.

* Se viene eseguito il rendering del frammento per `displayMode` == `singleText` (implicitamente o esplicitamente) entrano in gioco le seguenti proprietà aggiuntive:

   * `paragraphScope` definisce se deve essere eseguito il rendering di tutti i paragrafi o solo di un intervallo di paragrafi (valori: `all` rispetto a `range`)

   * if `paragraphScope` == `range` quindi la proprietà `paragraphRange` definisce l’intervallo di paragrafi da sottoporre a rendering

### Integrazione con altri framework {#integration-with-other-frameworks}

I frammenti di contenuto possono essere integrati con:

* **Traduzioni**

   I frammenti di contenuto sono completamente integrati con [Flusso di lavoro di traduzione AEM](/help/sites-administering/tc-manage.md). A livello architettonico, ciò significa:

   * Le singole traduzioni di un frammento di contenuto sono in realtà frammenti separati; ad esempio:

      * si trovano sotto diverse radici linguistiche:

         `/content/dam/<path>/en/<to>/<fragment>`

         rispetto a

         `/content/dam/<path>/de/<to>/<fragment>`

      * ma condividono esattamente lo stesso percorso relativo sotto la radice della lingua:

         `/content/dam/<path>/en/<to>/<fragment>`

         rispetto a

         `/content/dam/<path>/de/<to>/<fragment>`
   * Oltre ai percorsi basati su regole, non esiste un’ulteriore connessione tra le diverse versioni linguistiche di un frammento di contenuto; vengono gestiti come due frammenti separati, anche se l’interfaccia utente fornisce i mezzi per navigare tra le varianti di lingua.
   >[!NOTE]
   >
   >Il flusso di lavoro di traduzione AEM funziona con `/content`:
   >
   >* Poiché i modelli di frammento di contenuto risiedono in `/conf`, non sono incluse in tali traduzioni. È possibile [internazionalizzare le stringhe di interfaccia utente](/help/sites-developing/i18n-dev.md).
   >
   >* I modelli vengono copiati per creare il frammento in modo che ciò sia implicito.


* **Schemi metadati**

   * Frammenti di contenuto (ri)utilizza l’ [schemi di metadati](/help/assets/metadata-schemas.md), che può essere definito con risorse standard.
   * CFM fornisce il proprio schema specifico:

      `/libs/dam/content/schemaeditors/forms/contentfragment`

      se necessario, può essere esteso.

   * Il rispettivo modulo schema viene integrato con l’editor frammento.

## API di gestione dei frammenti di contenuto - Lato server {#the-content-fragment-management-api-server-side}

Puoi utilizzare l’API lato server per accedere ai frammenti di contenuto; vedi:

[com.adobe.cq.dam.cfm](https://www.adobe.io/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/dam/cfm/package-summary.html)

>[!CAUTION]
>
>È consigliabile utilizzare l’API lato server invece di accedere direttamente alla struttura dei contenuti.

### Interfacce chiave {#key-interfaces}

Le tre interfacce seguenti possono fungere da punti di ingresso:

* **Modello frammento** ([FragmentTemplate](https://www.adobe.io/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/dam/cfm/FragmentTemplate.html))

   Utilizzo `FragmentTemplate.createFragment()` per la creazione di un nuovo frammento.

   ```
   Resource templateOrModelRsc = resourceResolver.getResource("...");
   FragmentTemplate tpl = templateOrModelRsc.adaptTo(FragmentTemplate.class);
   ContentFragment newFragment = tpl.createFragment(parentRsc, "A fragment name", "A fragment description.");
   ```

   Questa interfaccia rappresenta:

   * un modello di frammento di contenuto o un modello di frammento di contenuto da cui creare un frammento di contenuto,
   * e (dopo la creazione) le informazioni strutturali di tale frammento

   Queste informazioni possono includere:

   * Accedere ai dati di base (titolo, descrizione)
   * Accedere a modelli/modelli per gli elementi del frammento:

      * Modelli di elementi di elenco
      * Ottenere informazioni strutturali per un dato elemento
      * Accedere al modello di elemento (vedi `ElementTemplate`)
   * Modelli di accesso per le varianti del frammento:

      * Elencare modelli di varianti
      * Ottieni informazioni strutturali per una determinata variante
      * Accedere al modello di variazione (vedi `VariationTemplate`)
   * Ottieni contenuto associato iniziale

   Interfacce che rappresentano informazioni importanti:

   * `ElementTemplate`

      * Ottieni dati di base (nome, titolo)
      * Ottenere il contenuto iniziale dell’elemento
   * `VariationTemplate`

      * Ottenere dati di base (nome, titolo, descrizione)






* **Frammento di contenuto** ([Frammento di contenuto](https://www.adobe.io/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/dam/cfm/ContentFragment.html))

   Questa interfaccia consente di lavorare con un frammento di contenuto in modo astratto.

   >[!CAUTION]
   >
   >È consigliabile accedere a un frammento tramite questa interfaccia. È necessario evitare di modificare direttamente la struttura del contenuto.

   L’interfaccia ti fornisce i mezzi per:

   * Gestire i dati di base (ad esempio nome get; get/set title/description)
   * Accedere ai metadati
   * Elementi di accesso:

      * Elementi elenco
      * Ottieni elementi per nome
      * Crea nuovi elementi (vedi [Avvertenze](#caveats))

      * Accedere ai dati degli elementi (vedi `ContentElement`)
   * Varianti di elenco definite per il frammento
   * Crea nuove varianti a livello globale
   * Gestisci il contenuto associato:

      * Elencare raccolte
      * Aggiungi raccolte
      * Rimuovere le raccolte
   * Accedere al modello o al modello del frammento

   Le interfacce che rappresentano gli elementi principali di un frammento sono:

   * **Elemento contenuto** ([ContentElement](https://www.adobe.io/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/dam/cfm/ContentElement.html))

      * Ottenere dati di base (nome, titolo, descrizione)
      * Ottieni/Imposta contenuto
      * Accedere alle varianti di un elemento:

         * Varianti di elenco
         * Ottieni varianti per nome
         * Crea nuove varianti (vedi [Avvertenze](#caveats))
         * Rimuovere le varianti (vedi [Avvertenze](#caveats))
         * Accedere ai dati sulle varianti (vedi `ContentVariation`)
      * Collegamento per la risoluzione delle varianti (se la variante specificata non è disponibile per un elemento, è possibile applicare una logica di fallback aggiuntiva specifica per l’implementazione)
   * **Variazione di contenuto** ([ContentVariation](https://www.adobe.io/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/dam/cfm/ContentVariation.html))

      * Ottenere dati di base (nome, titolo, descrizione)
      * Ottieni/Imposta contenuto
      * Sincronizzazione semplice in base alle ultime informazioni modificate

   Tutte e tre le interfacce ( `ContentFragment`, `ContentElement`, `ContentVariation`) estendi `Versionable` Interfaccia, che aggiunge funzionalità di controllo delle versioni, necessaria per i frammenti di contenuto:

   * Creare una nuova versione dell’elemento
   * Elencare versioni dell’elemento
   * Ottenere il contenuto di una versione specifica dell’elemento con versione







### Adattamento - Utilizzo di adaptTo() {#adapting-using-adaptto}

È possibile adattare quanto segue:

* `ContentFragment` può essere adattato a:

   * `Resource` - la risorsa Sling sottostante; tenere presente che l&#39;aggiornamento del sottostante `Resource` direttamente, richiede la ricostruzione del `ContentFragment` oggetto.

   * `Asset` - DAM `Asset` astrazione che rappresenta il frammento di contenuto; nota che l&#39;aggiornamento `Asset` direttamente, richiede la ricostruzione del `ContentFragment` oggetto.

* `ContentElement` può essere adattato a:

   * `ElementTemplate` - per accedere alle informazioni strutturali dell&#39;elemento.

* `FragmentTemplate` può essere adattato a:

   * `Resource` - il `Resource` determinazione del modello di riferimento o del modello originale copiato;

      * modifiche apportate tramite `Resource` non vengono riflessi automaticamente nel `FragmentTemplate`.

* `Resource` può essere adattato a:

   * `ContentFragment`
   * `FragmentTemplate`

### Avvertenze {#caveats}

Va osservato che:

* L’API viene implementata per fornire funzionalità supportate dall’interfaccia utente.
* L’intera API è progettata per **not** le modifiche persistono automaticamente (salvo diversa indicazione nel JavaDoc API). Quindi sarà sempre necessario impegnare il risolutore risorse della rispettiva richiesta (o il resolver che si sta effettivamente utilizzando).
* Attività che potrebbero richiedere ulteriore sforzo:

   * La creazione e la rimozione di nuovi elementi non comporta l’aggiornamento della struttura dati di frammenti semplici (basati su un modello di frammento).
   * Creazione di nuove varianti da `ContentElement` non aggiornerà la struttura dei dati (ma le creerà a livello globale da `ContentFragment` ).

   * La rimozione di varianti esistenti non aggiornerà la struttura dati.

## API di gestione dei frammenti di contenuto - Lato client {#the-content-fragment-management-api-client-side}

>[!CAUTION]
>
>Per AEM 6.5 l’API lato client è interna.

### Informazioni aggiuntive {#additional-information}

Consulta le seguenti risorse:

* `filter.xml`

   La `filter.xml` per la gestione dei frammenti di contenuto è configurata in modo che non si sovrapponga al pacchetto di contenuto core Assets.

## Modifica sessioni {#edit-sessions}

Una sessione di modifica viene avviata quando l’utente apre un frammento di contenuto in una delle pagine dell’editor. La sessione di modifica viene terminata quando l’utente esce dall’editor selezionando **Salva** o **Annulla**.

### Requisiti {#requirements}

Requisiti per il controllo di una sessione di modifica:

* La modifica di un frammento di contenuto, che può estendersi su più visualizzazioni (= pagine di HTML), deve essere atomica.
* L&#39;editing dovrebbe essere *transazionale*; alla fine della sessione di modifica le modifiche devono essere salvate o ripristinate (annullate).
* I casi di bordo devono essere gestiti correttamente; ad esempio, quando l’utente lascia la pagina immettendo manualmente un URL o utilizzando la navigazione globale.
* Per evitare la perdita di dati, deve essere disponibile un salvataggio automatico periodico (ogni x minuti).
* Se due utenti modificano contemporaneamente un frammento di contenuto, non sovrascriveranno le rispettive modifiche.

#### Processi {#processes}

I processi in questione sono i seguenti:

* Avvio di una sessione

   * Viene creata una nuova versione del frammento di contenuto.
   * Viene avviato il salvataggio automatico.
   * I cookie sono impostati; definiscono il frammento attualmente modificato e che sia aperta una sessione di modifica.

* Completamento di una sessione

   * Il salvataggio automatico viene interrotto.
   * Al momento del commit:

      * Le ultime informazioni modificate vengono aggiornate.
      * I cookie vengono rimossi.
   * Al momento del ripristino:

      * Viene ripristinata la versione del frammento di contenuto creato all’avvio della sessione di modifica.
      * I cookie vengono rimossi.


* Modifica

   * Tutte le modifiche (salvataggio automatico incluso) vengono eseguite sul frammento di contenuto attivo, non in un’area separata e protetta.
   * Pertanto, tali modifiche si riflettono immediatamente su AEM pagine che fanno riferimento al rispettivo frammento di contenuto

#### Azioni {#actions}

Le azioni possibili sono:

* Inserimento di una pagina

   * Controlla se è già presente una sessione di modifica; controllando il rispettivo cookie.

      * Se esiste, verifica che la sessione di modifica sia stata avviata per il frammento di contenuto in fase di modifica

         * Se il frammento corrente, ristabilire la sessione.
         * In caso contrario, prova ad annullare la modifica del frammento di contenuto precedentemente modificato e a rimuovere i cookie (nessuna sessione di modifica presente in seguito).
      * Se non esiste alcuna sessione di modifica, attendi la prima modifica apportata dall’utente (vedi di seguito).
   * Controlla se in una pagina è già presente un riferimento al frammento di contenuto e visualizza le informazioni appropriate in tal caso.



* Modifica del contenuto

   * Ogni volta che l’utente modifica il contenuto e non è presente alcuna sessione di modifica, viene creata una nuova sessione di modifica (vedi [Avvio di una sessione](#processes)).

* Uscita da una pagina

   * Se è presente una sessione di modifica e le modifiche non sono state mantenute, viene visualizzata una finestra di dialogo di conferma modale per informare l’utente del contenuto potenzialmente perso e consentire loro di rimanere sulla pagina.

## Esempi {#examples}

### Esempio: Accesso a un frammento di contenuto esistente {#example-accessing-an-existing-content-fragment}

A questo scopo, puoi adattare la risorsa che rappresenta l’API a:

`com.adobe.cq.dam.cfm.ContentFragment`

Esempio:

```java
// first, get the resource
Resource fragmentResource = resourceResolver.getResource("/content/dam/fragments/my-fragment");
// then adapt it
if (fragmentResource != null) {
    ContentFragment fragment = fragmentResource.adaptTo(ContentFragment.class);
    // the resource is now accessible through the API
}
```

### Esempio: Creazione di un nuovo frammento di contenuto {#example-creating-a-new-content-fragment}

Per creare un nuovo frammento di contenuto a livello di programmazione, è necessario utilizzare:

`com.adobe.cq.dam.cfm.ContentFragmentManager#create`

Esempio:

```java
Resource templateOrModelRsc = resourceResolver.getResource("...");
FragmentTemplate tpl = templateOrModelRsc.adaptTo(FragmentTemplate.class);
ContentFragment newFragment = tpl.createFragment(parentRsc, "A fragment name", "A fragment description.");
```

### Esempio: Specifica dell&#39;intervallo di salvataggio automatico {#example-specifying-the-auto-save-interval}

L&#39;intervallo di salvataggio automatico (misurato in secondi) può essere definito utilizzando il gestore di configurazione (ConfMgr):

* Nodo: `<*conf-root*>/settings/dam/cfm/jcr:content`
* Nome proprietà: `autoSaveInterval`
* Tipo: `Long`

* Predefinito: `600` (10 minuti); questo è definito in `/libs/settings/dam/cfm/jcr:content`

Se desideri impostare un intervallo di salvataggio automatico di 5 minuti, devi definire la proprietà sul nodo; ad esempio:

* Nodo: `/conf/global/settings/dam/cfm/jcr:content`
* Nome proprietà: `autoSaveInterval`

* Tipo: `Long`

* Valore: `300` (5 minuti equivale a 300 secondi)

## Modelli per frammenti di contenuto {#content-fragment-templates}

Vedi [Modelli per frammenti di contenuto](/help/sites-developing/content-fragment-templates.md) per informazioni complete.

## Componenti per l’authoring delle pagine {#components-for-page-authoring}

Per ulteriori informazioni, consulta

* [Componenti core - Componente frammento di contenuto](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html?lang=it) (consigliato)
* [Componenti per frammenti di contenuto - Componenti per l’authoring delle pagine](/help/sites-developing/components-content-fragments.md#components-for-page-authoring)
