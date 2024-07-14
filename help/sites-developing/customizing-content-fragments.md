---
title: Personalizzazione ed estensione dei frammenti di contenuto
description: Un frammento di contenuto estende una risorsa standard. Scopri come personalizzarli.
topic-tags: extending-aem
content-type: reference
docset: aem65
exl-id: 08c88e70-4df9-4627-8a66-1fabe3aee50b
solution: Experience Manager, Experience Manager Sites
feature: Content Fragments
role: Developer
source-git-commit: eae057caed533ef16bb541b4ad41b8edd7aaa1c7
workflow-type: tm+mt
source-wordcount: '2728'
ht-degree: 1%

---


# Personalizzazione ed estensione dei frammenti di contenuto{#customizing-and-extending-content-fragments}

Un frammento di contenuto estende una risorsa standard; vedi:

* [Creazione e gestione di frammenti di contenuto](/help/assets/content-fragments/content-fragments.md) e [Authoring di pagine con frammenti di contenuto](/help/sites-authoring/content-fragments.md) per ulteriori informazioni sui frammenti di contenuto.

* [Gestione di Assets](/help/assets/manage-assets.md) e [Personalizzazione ed estensione di Assets](/help/assets/extending-assets.md) per ulteriori informazioni sulle risorse standard.

## Architettura {#architecture}

Le [parti costitutive](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment) di base di un frammento di contenuto sono:

* Un *frammento di contenuto,*
* costituito da uno o più *elementi di contenuto*,
* e che possono avere una o più *Variante di contenuto*.

A seconda del tipo di frammento, vengono utilizzati anche i modelli o i modelli:

>[!CAUTION]
>
>Per la creazione di tutti i nuovi frammenti sono consigliati [modelli per frammenti di contenuto](/help/assets/content-fragments/content-fragments-models.md).
>
>I modelli per frammenti di contenuto vengono utilizzati per tutti gli esempi in WKND.

>[!NOTE]
>
>Prima di AEM 6.3, i frammenti di contenuto venivano creati in base a modelli anziché a modelli.
>
>I modelli per frammenti di contenuto sono ora obsoleti. Possono comunque essere utilizzati per la creazione di frammenti, ma si consiglia l’utilizzo di modelli per frammenti di contenuto. Non verranno aggiunte nuove funzioni ai modelli di frammenti e verranno rimosse in una versione futura.

* Modelli per frammenti di contenuto:

   * Utilizzato per definire frammenti di contenuto che contengono contenuto strutturato.
   * I modelli per frammenti di contenuto definiscono la struttura di un frammento di contenuto al momento della creazione.
   * Un frammento fa riferimento al modello, pertanto le modifiche apportate al modello possono influire o influenzeranno eventuali frammenti dipendenti.
   * I modelli sono costituiti da tipi di dati.
   * Le funzioni per aggiungere nuove varianti e così via devono aggiornare di conseguenza il frammento.

  >[!CAUTION]
  >
  >Eventuali modifiche apportate a un modello per frammenti di contenuto esistente possono influire sui frammenti dipendenti, con conseguenti proprietà orfane.

* Modelli per frammenti di contenuto:

   * Utilizzato per definire frammenti di contenuto semplici.
   * I modelli definiscono la struttura (di base, di solo testo) di un frammento di contenuto al momento della creazione.
   * Il modello viene copiato nel frammento quando viene creato; pertanto, eventuali modifiche al modello non verranno applicate ai frammenti esistenti.
   * Le funzioni per aggiungere nuove varianti e così via devono aggiornare di conseguenza il frammento.
   * [I modelli per frammenti di contenuto](/help/sites-developing/content-fragment-templates.md) funzionano in modo diverso rispetto ad altri meccanismi di modelli all&#39;interno dell&#39;ecosistema AEM (ad esempio i modelli di pagina e così via). Pertanto, essi devono essere considerati separatamente.
   * Se basato su un modello, il tipo MIME del contenuto viene gestito in base al contenuto effettivo; ciò significa che ogni elemento e variante può avere un tipo MIME diverso.

### Integrazione con Assets {#integration-with-assets}

La gestione dei frammenti di contenuto (CFM) fa parte di AEM Assets in quanto:

* I frammenti di contenuto sono risorse.
* Utilizzano le funzionalità esistenti di Assets.
* Sono completamente integrati con Assets (console di amministrazione, ecc.).

#### Mappatura di frammenti di contenuto strutturati su Assets {#mapping-structured-content-fragments-to-assets}

![frammento-a-risorse-strutturato](assets/fragment-to-assets-structured.png)

I frammenti di contenuto con contenuto strutturato (ovvero, basati su un modello per frammenti di contenuto) sono mappati su una singola risorsa:

* Tutto il contenuto è archiviato nel nodo `jcr:content/data` della risorsa:

   * I dati dell’elemento vengono memorizzati nel sottonodo principale:
     `jcr:content/data/master`

   * Le varianti vengono memorizzate in un sottonodo che porta il nome della variante:
ad esempio, `jcr:content/data/myvariation`

   * I dati di ciascun elemento vengono memorizzati nel rispettivo sottonodo come una proprietà con il nome dell’elemento:
ad esempio, il contenuto dell&#39;elemento `text` è archiviato come proprietà `text` in `jcr:content/data/master`

* I metadati e il contenuto associato sono memorizzati sotto `jcr:content/metadata`
Ad eccezione del titolo e della descrizione, che non sono considerati metadati tradizionali e memorizzati in `jcr:content`

#### Mappatura di frammenti di contenuto semplici su Assets {#mapping-simple-content-fragments-to-assets}

![chlimage_1-90](assets/chlimage_1-90.png)

I frammenti di contenuto semplici (basati su un modello) sono mappati su un contenuto composito costituito da una risorsa principale e da risorse secondarie (facoltative):

* Tutte le informazioni non relative al contenuto di un frammento (come titolo, descrizione, metadati, struttura) vengono gestite esclusivamente sulla risorsa principale.
* Il contenuto del primo elemento di un frammento è mappato alla rappresentazione originale della risorsa principale.

   * Le varianti (se presenti) del primo elemento sono mappate ad altre rappresentazioni della risorsa principale.

* Elementi aggiuntivi (se esistenti) sono mappati su risorse secondarie della risorsa principale.

   * Il contenuto principale di questi elementi aggiuntivi corrisponde alla rappresentazione originale della rispettiva risorsa secondaria.
   * Altre varianti (se applicabili) di eventuali elementi aggiuntivi sono associate ad altre rappresentazioni della rispettiva risorsa secondaria.

#### Posizione risorsa {#asset-location}

Come per le risorse standard, un frammento di contenuto si trova in:

`/content/dam`

#### Autorizzazioni risorse {#asset-permissions}

Per ulteriori dettagli vedi [Frammento di contenuto - Considerazioni sull&#39;eliminazione](/help/assets/content-fragments/content-fragments-delete.md).

#### Integrazione delle funzioni {#feature-integration}

* La funzione di gestione dei frammenti di contenuto (CFM) si basa sul core Assets, ma deve essere il più indipendente possibile.
* CFM fornisce le proprie implementazioni per gli elementi nelle viste a schede/colonne/elenchi; queste si collegano alle implementazioni esistenti di rendering dei contenuti Assets.
* Diversi componenti Assets sono stati estesi per gestire i frammenti di contenuto.

### Utilizzo dei frammenti di contenuto nelle pagine {#using-content-fragments-in-pages}

>[!CAUTION]
>
>Il [componente core Frammento di contenuto](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html?lang=it) è ora consigliato. Per ulteriori dettagli, vedere [Sviluppo di componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/overview.html).

È possibile fare riferimento ai frammenti di contenuto dalle pagine AEM, come qualsiasi altro tipo di risorsa. AEM fornisce il componente di base ](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html?lang=it) [**Frammento di contenuto** - un componente [che consente di includere frammenti di contenuto nelle pagine](/help/sites-authoring/content-fragments.md#adding-a-content-fragment-to-your-page). Puoi anche estendere questo componente core **Frammento di contenuto**.

* Il componente utilizza la proprietà `fragmentPath` per fare riferimento al frammento di contenuto effettivo. La proprietà `fragmentPath` viene gestita nello stesso modo di proprietà simili di altri tipi di risorse, ad esempio quando il frammento di contenuto viene spostato in un’altra posizione.

* Il componente ti consente di selezionare la variante da visualizzare.
* Inoltre, è possibile selezionare un intervallo di paragrafi per limitare l’output; ad esempio, può essere utilizzato per l’output a più colonne.
* Il componente consente [contenuto intermedio](/help/sites-developing/components-content-fragments.md#in-between-content):

   * In questo caso il componente consente di inserire altre risorse (immagini e così via) tra i paragrafi del frammento di riferimento.
   * Per i contenuti intermedi è necessario:

      * tieni presente la possibilità di riferimenti instabili; il contenuto intermedio (aggiunto durante l’authoring di una pagina) non ha una relazione fissa con il paragrafo a cui è posizionato, inserendo un nuovo paragrafo (nell’editor frammento di contenuto) prima che la posizione del contenuto intermedio possa perdere la posizione relativa
      * considera i parametri aggiuntivi (come i filtri di variante e di paragrafo) per evitare falsi positivi nei risultati di ricerca

>[!NOTE]
>
>**Modello per frammenti di contenuto:**
>
>Quando si utilizza un frammento di contenuto basato su un modello di frammento di contenuto su una pagina, viene fatto riferimento al modello. Ciò significa che se il modello non è stato pubblicato al momento della pubblicazione della pagina, verrà contrassegnato e il modello verrà aggiunto alle risorse da pubblicare con la pagina.
>
>**Modello per frammenti di contenuto:**
>
>Quando si utilizza un frammento di contenuto basato su un modello di frammento di contenuto su una pagina, non esiste alcun riferimento in quanto il modello è stato copiato durante la creazione del frammento.

#### Configurazione tramite la console OSGi {#configuration-using-osgi-console}

L’implementazione back-end dei frammenti di contenuto è, ad esempio, responsabile della possibilità di cercare le istanze di un frammento utilizzato su una pagina o della gestione di contenuti multimediali diversi. Questa implementazione deve sapere quali componenti vengono utilizzati per il rendering dei frammenti e come viene parametrizzato il rendering.

I parametri per questo possono essere configurati nella [console Web](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console), per il bundle OSGi **configurazione del componente Frammento di contenuto**.

* **Tipi di risorse**
È possibile fornire un elenco di `sling:resourceTypes` per definire i componenti utilizzati per il rendering dei frammenti di contenuto e a cui applicare l&#39;elaborazione in background.

* **Proprietà riferimento**
È possibile configurare un elenco di proprietà per specificare dove viene memorizzato il riferimento al frammento per il rispettivo componente.

>[!NOTE]
>
>Non esiste alcuna mappatura diretta tra la proprietà e il tipo di componente.
>
>L&#39;AEM prende semplicemente la prima proprietà che si trova su un paragrafo. Quindi devi scegliere le proprietà con attenzione.

![screenshot_2019-03-18at100941](assets/screenshot_2019-03-18at100941.png)

Sono ancora presenti alcune linee guida da seguire per garantire che il componente sia compatibile con l’elaborazione in background del frammento di contenuto:

* Il nome della proprietà in cui sono definiti gli elementi da sottoporre a rendering deve essere `element` o `elementNames`.

* Il nome della proprietà in cui è definita la variante da sottoporre a rendering deve essere `variation` o `variationName`.

* Se l&#39;output di più elementi è supportato (utilizzando `elementNames` per specificare più elementi), la modalità di visualizzazione effettiva è definita dalla proprietà `displayMode`:

   * Se il valore è `singleText` (ed è configurato un solo elemento), l&#39;elemento viene riprodotto come testo con contenuto intermedio, supporto del layout e così via. Questa è l’impostazione predefinita per i frammenti in cui viene eseguito il rendering di un solo elemento.
   * In caso contrario, viene utilizzato un approccio molto più semplice (che potrebbe essere denominato &quot;visualizzazione modulo&quot;), in cui non è supportato alcun contenuto intermedio e il contenuto del frammento viene renderizzato &quot;così com’è&quot;.

* Se il rendering del frammento viene eseguito per `displayMode` == `singleText` (in modo implicito o esplicito), entrano in gioco le seguenti proprietà aggiuntive:

   * `paragraphScope` definisce se è necessario eseguire il rendering di tutti i paragrafi o solo di un intervallo di paragrafi (valori: `all` rispetto a `range`)

   * se `paragraphScope` == `range`, la proprietà `paragraphRange` definisce l&#39;intervallo di paragrafi di cui eseguire il rendering

### Integrazione con altri framework {#integration-with-other-frameworks}

I frammenti di contenuto possono essere integrati con:

* **Traduzioni**

  I frammenti di contenuto sono completamente integrati con il [flusso di lavoro di traduzione AEM](/help/sites-administering/tc-manage.md). A livello architettonico, ciò significa:

   * Le singole traduzioni di un frammento di contenuto sono in realtà frammenti separati; ad esempio:

      * si trovano in diverse radici linguistiche:

        `/content/dam/<path>/en/<to>/<fragment>`

        rispetto a

        `/content/dam/<path>/de/<to>/<fragment>`

      * ma condividono esattamente lo stesso percorso relativo sotto la directory principale della lingua:

        `/content/dam/<path>/en/<to>/<fragment>`

        rispetto a

        `/content/dam/<path>/de/<to>/<fragment>`

   * Oltre ai percorsi basati su regole, non esiste un’ulteriore connessione tra le diverse versioni linguistiche di un frammento di contenuto; vengono gestiti come due frammenti separati, anche se l’interfaccia utente fornisce i mezzi per navigare tra le varianti di lingua.

  >[!NOTE]
  >
  >Il flusso di lavoro di traduzione AEM funziona con `/content`:
  >
  >* Poiché i modelli per frammenti di contenuto risiedono in `/conf`, non sono inclusi in tali traduzioni. È possibile [internazionalizzare le stringhe dell&#39;interfaccia utente](/help/sites-developing/i18n-dev.md).
  >
  >* I modelli vengono copiati per creare il frammento, in modo che questo sia implicito.

* **Schemi metadati**

   * I frammenti di contenuto (ri)utilizzano gli [schemi di metadati](/help/assets/metadata-schemas.md), che possono essere definiti con risorse standard.
   * CFM fornisce uno schema specifico:

     `/libs/dam/content/schemaeditors/forms/contentfragment`

     se necessario, è possibile estenderla.

   * Il rispettivo modulo schema è integrato con l’editor di frammenti.

## API di gestione dei frammenti di contenuto - Lato server {#the-content-fragment-management-api-server-side}

Puoi utilizzare l’API lato server per accedere ai frammenti di contenuto; vedi:

[com.adobe.cq.dam.cfm](https://www.adobe.io/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/dam/cfm/package-summary.html)

>[!CAUTION]
>
>Si consiglia vivamente di utilizzare l’API lato server invece di accedere direttamente alla struttura del contenuto.

### Interfacce chiave {#key-interfaces}

Le tre interfacce seguenti possono fungere da punti di ingresso:

* **Modello frammento** ([Modello frammento](https://www.adobe.io/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/dam/cfm/FragmentTemplate.html))

  Utilizza `FragmentTemplate.createFragment()` per creare un frammento.

  ```
  Resource templateOrModelRsc = resourceResolver.getResource("...");
  FragmentTemplate tpl = templateOrModelRsc.adaptTo(FragmentTemplate.class);
  ContentFragment newFragment = tpl.createFragment(parentRsc, "A fragment name", "A fragment description.");
  ```

  Questa interfaccia rappresenta:

   * un modello per frammenti di contenuto o un modello per frammenti di contenuto dal quale creare un frammento di contenuto,
   * e (dopo la creazione) le informazioni strutturali di quel frammento

  Queste informazioni possono includere:

   * Accedere ai dati di base (titolo, descrizione)
   * Accedi a modelli/modelli per gli elementi del frammento:

      * Elencare modelli di elementi
      * Ottenere informazioni strutturali per un determinato elemento
      * Accedere al modello di elemento (vedere `ElementTemplate`)

   * Accedi ai modelli per le varianti del frammento:

      * Elencare modelli di varianti
      * Ottenere informazioni strutturali per una determinata variante
      * Accedere al modello di variante (vedere `VariationTemplate`)

   * Ottieni contenuto associato iniziale

  Interfacce che rappresentano informazioni importanti:

   * `ElementTemplate`

      * Ottieni dati di base (nome, titolo)
      * Ottieni contenuto elemento iniziale

   * `VariationTemplate`

      * Ottenere dati di base (nome, titolo, descrizione)

* **Frammento di contenuto** ([Frammento di contenuto](https://www.adobe.io/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/dam/cfm/ContentFragment.html))

  Questa interfaccia consente di lavorare con un frammento di contenuto in modo astratto.

  >[!CAUTION]
  >
  >Si consiglia vivamente di accedere a un frammento tramite questa interfaccia. È necessario evitare di modificare direttamente la struttura del contenuto.

  L’interfaccia consente di:

   * Gestisci dati di base (ad esempio, nome, titolo/descrizione get/set)
   * Accedere ai metadati
   * Elementi di accesso:

      * Elementi elenco
      * Ottieni elementi per nome
      * Crea nuovi elementi (vedi [Avvertenze](#caveats))

      * Accedere ai dati degli elementi (vedere `ContentElement`)

   * Elenca le varianti definite per il frammento
   * Creare nuove varianti a livello globale
   * Gestisci contenuto associato:

      * Elencare raccolte
      * Aggiungere raccolte
      * Rimuovi raccolte

   * Accedere al modello o al modello del frammento

  Le interfacce che rappresentano gli elementi principali di un frammento sono:

   * **Elemento contenuto** ([Elemento contenuto](https://www.adobe.io/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/dam/cfm/ContentElement.html))

      * Ottenere dati di base (nome, titolo, descrizione)
      * Ottieni/Imposta contenuto
      * Accedere alle varianti di un elemento:

         * Varianti elenco
         * Ottieni varianti per nome
         * Crea nuove varianti (vedi [Avvertenze](#caveats))
         * Rimuovi varianti (vedi [Avvertenze](#caveats))
         * Accedere ai dati della variante (vedere `ContentVariation`)

      * Scelta rapida per la risoluzione delle varianti (applicazione di alcune logiche di fallback aggiuntive specifiche per l’implementazione se la variante specificata non è disponibile per un elemento)

   * **Variante contenuto** ([Variante contenuto](https://www.adobe.io/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/dam/cfm/ContentVariation.html))

      * Ottenere dati di base (nome, titolo, descrizione)
      * Ottieni/Imposta contenuto
      * Sincronizzazione semplice, basata sulle informazioni modificate più di recente

  Tutte e tre le interfacce ( `ContentFragment`, `ContentElement`, `ContentVariation`) estendono l&#39;interfaccia `Versionable`, che aggiunge funzionalità di controllo delle versioni, necessarie per i frammenti di contenuto:

   * Crea una nuova versione dell’elemento
   * Elencare le versioni dell’elemento
   * Ottenere il contenuto di una versione specifica dell&#39;elemento con versione

### Adattamento - Utilizzo di adaptTo() {#adapting-using-adaptto}

È possibile adattare:

* `ContentFragment` può essere adattato a:

   * `Resource`: la risorsa Sling sottostante. Si noti che l&#39;aggiornamento diretto di `Resource` sottostante richiede la ricompilazione dell&#39;oggetto `ContentFragment`.

   * `Asset`: l&#39;astrazione DAM `Asset` che rappresenta il frammento di contenuto. Si noti che l&#39;aggiornamento diretto di `Asset` richiede la ricompilazione dell&#39;oggetto `ContentFragment`.

* `ContentElement` può essere adattato a:

   * `ElementTemplate` - per accedere alle informazioni strutturali dell&#39;elemento.

* `FragmentTemplate` può essere adattato a:

   * `Resource` - `Resource` che determina il modello di riferimento o il modello originale copiato;

      * le modifiche apportate tramite `Resource` non vengono applicate automaticamente in `FragmentTemplate`.

* `Resource` può essere adattato a:

   * `ContentFragment`
   * `FragmentTemplate`

### Avvertenze {#caveats}

Si noti che:

* L’API è implementata per fornire funzionalità supportate dall’interfaccia utente.
* L&#39;intera API è progettata per **non** mantenere le modifiche automaticamente (a meno che non sia indicato diversamente in API JavaDoc). Pertanto, dovrai sempre eseguire il commit del risolutore risorse della rispettiva richiesta (o del risolutore che stai utilizzando).
* Attività che potrebbero richiedere un ulteriore impegno:

   * La creazione o la rimozione di nuovi elementi non aggiorna la struttura dati dei frammenti semplici (in base a un modello di frammento).
   * La creazione di nuove varianti da `ContentElement` non aggiornerà la struttura dei dati, ma la creazione a livello globale da `ContentFragment` consentirà.

   * La rimozione delle varianti esistenti non aggiorna la struttura dati.

## API di gestione dei frammenti di contenuto - Lato client {#the-content-fragment-management-api-client-side}

>[!CAUTION]
>
>Per AEM 6.5 l’API lato client è interna.

### Informazioni aggiuntive {#additional-information}

Consulta le seguenti risorse:

* `filter.xml`

  `filter.xml` per la gestione dei frammenti di contenuto è configurato in modo da non sovrapporsi al pacchetto di contenuti di base di Assets.

## Modifica sessioni {#edit-sessions}

Una sessione di modifica viene avviata quando l’utente apre un frammento di contenuto in una delle pagine dell’editor. La sessione di modifica è terminata quando l&#39;utente esce dall&#39;editor selezionando **Salva** o **Annulla**.

### Requisiti {#requirements}

I requisiti per il controllo di una sessione di modifica sono i seguenti:

* La modifica di un frammento di contenuto, che può estendersi su più visualizzazioni (= pagine HTML), deve essere atomica.
* La modifica deve essere anche *transazionale*; al termine della sessione di modifica le modifiche devono essere applicate (salvate) o riportate (annullate).
* I casi Edge devono essere gestiti correttamente; questi includono situazioni come quando l’utente esce dalla pagina immettendo manualmente un URL o utilizzando la navigazione globale.
* Per evitare perdite di dati, è necessario che sia disponibile un salvataggio automatico periodico (ogni x minuti).
* Se un frammento di contenuto viene modificato contemporaneamente da due utenti, questi non devono sovrascrivere le rispettive modifiche.

#### Processi {#processes}

I processi coinvolti sono:

* Avvio di una sessione

   * Viene creata una nuova versione del frammento di contenuto.
   * Salvataggio automatico avviato.
   * I cookie sono impostati, definiscono il frammento attualmente modificato e indica che è aperta una sessione di modifica.

* Completamento di una sessione

   * Salvataggio automatico interrotto.
   * Al commit:

      * Le informazioni dell’ultima modifica vengono aggiornate.
      * I cookie vengono rimossi.

   * Al momento del rollback:

      * Viene ripristinata la versione del frammento di contenuto creato all’avvio della sessione di modifica.
      * I cookie vengono rimossi.

* Modifica

   * Tutte le modifiche (salvataggio automatico incluso) vengono eseguite sul frammento di contenuto attivo, non in un’area separata e protetta.
   * Pertanto, tali modifiche vengono immediatamente applicate alle pagine AEM che fanno riferimento al rispettivo frammento di contenuto

#### Azioni {#actions}

Le azioni possibili sono:

* Inserimento di una pagina

   * Verifica se è già presente una sessione di modifica controllando il rispettivo cookie.

      * Se ne esiste una, verifica che la sessione di modifica sia stata avviata per il frammento di contenuto attualmente in fase di modifica

         * Se il frammento corrente, ristabilisci la sessione.
         * In caso contrario, prova ad annullare la modifica per il frammento di contenuto modificato in precedenza e a rimuovere i cookie (nessuna sessione di modifica successiva).

      * Se non esiste alcuna sessione di modifica, attendi la prima modifica apportata dall’utente (vedi sotto).

   * Verifica se in una pagina è già presente un riferimento al frammento di contenuto e, in tal caso, visualizza le informazioni appropriate.

* Modifica del contenuto

   * Ogni volta che l&#39;utente modifica il contenuto e non è presente alcuna sessione di modifica, viene creata una nuova sessione di modifica (vedere [Avvio di una sessione](#processes)).

* Uscita da una pagina

   * Se è presente una sessione di modifica e le modifiche non sono state rese permanenti, viene visualizzata una finestra di dialogo di conferma modale per notificare all’utente i contenuti potenzialmente persi e consentirne la permanenza nella pagina.

## Esempi {#examples}

### Esempio: accesso a un frammento di contenuto esistente {#example-accessing-an-existing-content-fragment}

A questo scopo, puoi adattare la risorsa che rappresenta l’API a:

`com.adobe.cq.dam.cfm.ContentFragment`

Ad esempio:

```java
// first, get the resource
Resource fragmentResource = resourceResolver.getResource("/content/dam/fragments/my-fragment");
// then adapt it
if (fragmentResource != null) {
    ContentFragment fragment = fragmentResource.adaptTo(ContentFragment.class);
    // the resource is now accessible through the API
}
```

### Esempio: creazione di un frammento di contenuto {#example-creating-a-new-content-fragment}

Per creare un frammento di contenuto a livello di programmazione, è necessario utilizzare:

`com.adobe.cq.dam.cfm.ContentFragmentManager#create`

Ad esempio:

```java
Resource templateOrModelRsc = resourceResolver.getResource("...");
FragmentTemplate tpl = templateOrModelRsc.adaptTo(FragmentTemplate.class);
ContentFragment newFragment = tpl.createFragment(parentRsc, "A fragment name", "A fragment description.");
```

### Esempio: specifica dell&#39;intervallo di salvataggio automatico {#example-specifying-the-auto-save-interval}

L&#39;intervallo di salvataggio automatico (misurato in secondi) può essere definito utilizzando Gestione configurazione (ConfMgr):

* Nodo: `<*conf-root*>/settings/dam/cfm/jcr:content`
* Nome proprietà: `autoSaveInterval`
* Tipo: `Long`

* Predefinito: `600` (10 minuti); definito il `/libs/settings/dam/cfm/jcr:content`

Se desideri impostare un intervallo di salvataggio automatico di 5 minuti, devi definire la proprietà sul nodo; ad esempio:

* Nodo: `/conf/global/settings/dam/cfm/jcr:content`
* Nome proprietà: `autoSaveInterval`

* Tipo: `Long`

* Valore: `300` (5 minuti equivalgono a 300 secondi)

## Modelli per frammenti di contenuto {#content-fragment-templates}

Per informazioni complete, consulta [Modelli per frammenti di contenuto](/help/sites-developing/content-fragment-templates.md).

## Componenti per l’authoring delle pagine {#components-for-page-authoring}

Per ulteriori informazioni, consulta

* [Componenti core - Componente frammento di contenuto](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html?lang=it) (consigliato)
* [Componenti Frammento di contenuto: componenti per l’authoring delle pagine](/help/sites-developing/components-content-fragments.md#components-for-page-authoring)
