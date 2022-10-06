---
title: Utilizzo di frammenti di contenuto
description: Scopri come i frammenti di contenuto in Adobe Experience Manager (AEM) consentono di progettare, creare, curare e utilizzare contenuti indipendenti dalla pagina, ideali per la distribuzione headless.
feature: Content Fragments
role: User
exl-id: 0ee883c5-0cea-46b7-a759-600b8ea3bc3e
source-git-commit: b5cf18d8e83786a23005aadf8aafe43d006a2e67
workflow-type: tm+mt
source-wordcount: '1989'
ht-degree: 93%

---

# Utilizzo di frammenti di contenuto {#working-with-content-fragments}

Con Adobe Experience Manager (AEM), i frammenti di contenuto ti consentono di progettare, creare, curare e [pubblicare contenuti indipendenti dalla pagina](/help/sites-authoring/content-fragments.md) Consentono di preparare i contenuti pronti per l’uso in più posizioni/su più canali, ideale per la distribuzione headless.

I frammenti di contenuto contengono contenuto strutturato:

* Sono basati su un [Modello per frammenti di contenuto](/help/assets/content-fragments/content-fragments-models.md), che definisce la struttura del frammento risultante.
* La struttura può essere di tre tipi:
   * Base
      * Ad esempio, un singolo campo di testo su più righe.
      * Può essere utilizzata per preparare contenuti semplici da utilizzare nell’authoring delle pagine.
   * Complessa
      * Combinazione di più campi di tipi di dati diversi, tra cui testo, dati numerici, dati booleani, data e ora.
      * Può essere utilizzata per preparare contenuti più strutturati per l’authoring delle pagine o da distribuire a un’applicazione.
   * Nidificata
      * I tipi di dati di riferimento disponibili consentono di nidificare il contenuto.
      * Questa struttura è spesso utilizzata per la consegna a un’applicazione.

I frammenti di contenuto possono essere consegnati anche in formato JSON, utilizzando le funzionalità di esportazione Sling Model (JSON) dei componenti core di AEM. Questo tipo di consegna:

* consente di utilizzare il componente per gestire gli elementi di un frammento da consegnare;
* consente la consegna in massa, aggiungendo più componenti core per frammenti di contenuto nella pagina utilizzata per la consegna API.

Più avanti e nelle pagine seguenti sono illustrate le attività di creazione, configurazione, manutenzione e utilizzo dei frammenti di contenuto:

* [Abilita funzionalità frammento di contenuto per la tua istanza](/help/assets/content-fragments/content-fragments-configuration-browser.md)
* [Modelli per frammenti di contenuto](/help/assets/content-fragments/content-fragments-models.md): come abilitare, creare e definire i modelli
* [Gestione dei frammenti di contenuto](/help/assets/content-fragments/content-fragments-managing.md): come creare frammenti di contenuto, quindi modificarli, pubblicarli e farvi riferimento.
* [Varianti: authoring dei contenuti di frammenti](/help/assets/content-fragments/content-fragments-variations.md): come creare il contenuto di un frammento e quindi varianti del contenuto principale
* [Markdown](/help/assets/content-fragments/content-fragments-markdown.md): come utilizzare la sintassi markdown per il frammento
* [Utilizzo di contenuti associati](/help/assets/content-fragments/content-fragments-assoc-content.md): come aggiungere contenuti associati
* [Metadati: proprietà dei frammenti](/help/assets/content-fragments/content-fragments-metadata.md): come visualizzare e modificare le proprietà dei frammenti
* Utilizzo [Frammenti di contenuto, insieme a GraphQL, per distribuire contenuti](/help/assets/content-fragments/content-fragments-graphql.md) da utilizzare nelle applicazioni. Per facilitare questa fase, puoi visualizzare un’anteprima [Output JSON](/help/assets/content-fragments/content-fragments-json-preview.md).

>[!NOTE]
>
>Oltre a queste pagine, puoi leggere anche:
>
>* [Authoring delle pagine con frammenti di contenuto](/help/sites-authoring/content-fragments.md).
>* [Personalizzazione ed estensione dei frammenti di contenuto](/help/sites-developing/customizing-content-fragments.md)
>* [Componenti di configurazione dei frammenti di contenuto per il rendering](/help/sites-developing/content-fragments-config-components-rendering.md)
>* [Supporto dei frammenti di contenuto nell’API HTTP di AEM Assets](/help/assets/assets-api-content-fragments.md)
>* [API GraphQL di AEM per l’utilizzo con Frammenti di contenuto](/help/assets/content-fragments/graphql-api-content-fragments.md)


Il numero di canali di comunicazione aumenta ogni anno. In genere i canali si distinguono in base al meccanismo di consegna, come segue:

* Canale fisico, ad esempio desktop o mobile.
* Forma di consegna in un canale fisico, ad esempio “pagina dei dettagli di un prodotto”, “pagina della categoria del prodotto” per desktop oppure “web mobile”, “app mobile” per dispositivi mobili.

Tuttavia, probabilmente non vorrai utilizzare esattamente gli stessi contenuti per tutti i canali: vorrai piuttosto ottimizzarli in base ai singoli canali.

I frammenti di contenuto consentono di:

* valutare come raggiungere in modo efficiente il pubblico target su ciascun canale;
* creare e gestire contenuti editoriali indipendenti dal canale;
* creare pool di contenuti per una serie di canali;
* progettare varianti di contenuto per canali specifici;
* aggiungere immagini al testo inserendo delle risorse (frammenti con elementi multimediali diversi);
* creare contenuti nidificati in base alla complessità dei dati.

I frammenti di contenuto possono quindi essere assemblati per fornire esperienze su diversi canali.

>[!NOTE]
>
>I **frammenti di contenuto** e i **[frammenti di esperienza](/help/sites-authoring/experience-fragments.md)** sono funzioni diverse in AEM:
>* I **frammenti di contenuto** sono contenuti editoriali che possono essere utilizzati per accedere a dati strutturati, tra cui testi, numeri e date. Sono contenuti puri, con definizione e struttura, ma senza elementi visivi aggiuntivi di design e/o layout.
>* I **frammenti di esperienza** sono contenuti completi di layout, frammenti di una pagina web.
>
>I frammenti esperienza possono includere contenuti sotto forma di frammenti di contenuto, ma non viceversa.
>
>Per ulteriori informazioni consulta anche [Frammenti di contenuto e frammenti di esperienza in AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/content-fragments/understand-content-fragments-and-experience-fragments.html?lang=it#content-fragments).

>[!NOTE]
>
>Prima di AEM 6.3, venivano creati frammenti di contenuto con l’uso di modelli anziché modelli. I modelli non sono più disponibili per la creazione di nuovi frammenti, ma tutti i frammenti creati con tale modello sono ancora supportati.

## Frammenti di contenuto e Content Services {#content-fragments-and-content-services}

AEM Content Services è progettato per generalizzare la descrizione e la consegna dei contenuti in/da AEM, non limitandosi alle pagine web.

Fornisce contenuti a canali diversi dalle tradizionali pagine web di AEM, utilizzando metodi standardizzati utilizzabili da qualsiasi cliente. Questi canali possono includere:

* Applicazioni a pagina singola
* Applicazioni mobile native
* Altri canali e punti di contatto esterni ad AEM

La consegna viene effettuata in formato JSON utilizzando il modulo di esportazione JSON.

I frammenti di contenuto di AEM possono essere utilizzati per descrivere e gestire contenuti strutturati. Il contenuto strutturato è definito in modelli che possono contenere diversi tipi di contenuto, compresi testo, dati numerici, dati booleani, data e ora e altro ancora.

Insieme alle funzionalità di esportazione JSON dei componenti core di AEM, tali contenuti strutturati possono quindi essere utilizzati per consegnare contenuti AEM a canali diversi dalle pagine AEM.

<!--
>[!NOTE]
>
>See [Headless and AEM](/help/implementing/developing/headless/introduction.md) for an introduction to Headless Development for AEM Sites.
-->

>[!NOTE]
>
>AEM supporta anche la traduzione del contenuto dei frammenti.

<!--
>[!NOTE]
>
>AEM also supports the translation of fragment content. See [Translating Assets](/help/assets/translate-assets.md) for further information.
-->

## Tipo di contenuto {#content-type}

I frammenti di contenuto sono:

* Memorizzati come **Risorse**:

   * I frammenti di contenuto (e le relative varianti) possono essere creati e mantenuti dal **Risorse** console.
   * Vengono creati e modificati nell’Editor frammenti di contenuto.

* Utilizzati nell’[editor pagina tramite il componente Frammento di contenuto](/help/sites-authoring/content-fragments.md) (componente di riferimento):

   * Il componente **Frammento di contenuto** è disponibile per gli autori delle pagine. Consente loro di fare riferimento e distribuire il frammento di contenuto richiesto in formato HTML o JSON.

* Accessibili tramite l’[API GraphQL di AEM](/help/assets/content-fragments/graphql-api-content-fragments.md).

I frammenti di contenuto sono una struttura di contenuto che:

* è priva di layout o design (in modalità Testo formattato è possibile formattare del testo);
* contiene una o più [parti costituenti](#constituent-parts-of-a-content-fragment);
* può [contenere immagini o essere connessa ad esse](#fragments-with-visual-assets);
* può utilizzare [contenuto intermedio](#in-between-content-when-page-authoring-with-content-fragments) se referenziato in una pagina;

* è indipendente dal meccanismo di consegna (ad esempio, pagina, canale).

### Frammenti con risorse visive {#fragments-with-visual-assets}

Per dare agli autori un maggiore controllo sui contenuti, le immagini possono essere aggiunte a e/o integrate con un frammento di contenuto.

Le risorse possono essere utilizzate con un frammento di contenuto in diversi modi, ciascuno con i propri vantaggi:

* Tramite **Inserisci risorsa** per inserire una risorsa in un frammento (frammenti con elementi multimediali diversi)

   * Sono parte integrante del frammento (vedi [Parti costitutive di un frammento di contenuto](#constituent-parts-of-a-content-fragment)).
   * Viene definita la posizione della risorsa.
   * Per ulteriori informazioni consulta [Inserimento di risorse nel frammento](/help/assets/content-fragments/content-fragments-variations.md#inserting-assets-into-your-fragment) nell’editor di frammenti.

   >[!NOTE]
   >
   >Le risorse visive inserite nel frammento di contenuto stesso sono associate al paragrafo precedente. Quando il frammento viene aggiunto a una pagina e quindi viene aggiunto del contenuto intermedio, queste risorse si spostano in relazione a tale paragrafo.

* Come **Contenuto associato**

   * È collegato a un frammento, ma non è una parte fissa del frammento (vedi [Parti costitutive di un frammento di contenuto](#constituent-parts-of-a-content-fragment)).
   * Offre una certa flessibilità di posizionamento.
   * È facilmente disponibile per l’uso (come contenuto intermedio) quando si utilizza il frammento su una pagina.
   * Per ulteriori informazioni vedi [Contenuto associato](/help/assets/content-fragments/content-fragments-assoc-content.md).

* Risorse disponibili nel **browser Risorse** dell’editor pagina

   * Offrono massima flessibilità nella selezione di una risorsa.
   * Offre una certa flessibilità di posizionamento.
   * Non supportano il concetto di approvazione per un frammento specifico.

<!--
  * See [Assets Browser](/help/sites-authoring/environment-tools.md#assets-browser) for more information.
-->

### Parti costitutive di un frammento di contenuto {#constituent-parts-of-a-content-fragment}

Le risorse dei frammenti di contenuto sono composte dalle seguenti parti (direttamente o indirettamente):

* **Elementi del frammento**

   * Gli elementi sono correlati ai campi di dati che contengono il contenuto.
   * Per creare il frammento di contenuto, puoi utilizzare un modello di contenuto. Gli elementi (campi) specificati nel modello definiscono la struttura del frammento. Questi elementi (campi) possono essere di diversi tipi di dati.

* **Paragrafi del frammento**

   * Blocchi di testo, spesso con più righe, delimitati come singole entità.

   * Nelle modalità [Testo formattato](/help/assets/content-fragments/content-fragments-variations.md#rich-text) e [Markdown](/help/assets/content-fragments/content-fragments-variations.md#markdown), un paragrafo può essere formattato come intestazione, in tal caso appartiene a un’unica unità insieme al paragrafo seguente.

   * Consentono di controllare i contenuti durante l’authoring delle pagine.

* **Risorse inserite in un frammento (frammenti con elementi multimediali diversi)**

   * Risorse (immagini) inserite nel frammento effettivo e utilizzate come contenuto interno di un frammento.
   * Sono incorporate nel sistema paragrafo del frammento.
   * Possono essere formattate quando il [frammento viene utilizzato o inserito come riferimento in una pagina](/help/sites-authoring/content-fragments.md).
   * Possono solo essere aggiunte, eliminate o spostate all’interno di un frammento utilizzando l’editor di frammenti. Queste azioni non possono essere eseguite nell’editor pagina.
   * Possono essere aggiunte, eliminate o spostate all’interno di un frammento solo utilizzando il formato [Testo formattato nell’editor di frammenti](/help/assets/content-fragments/content-fragments-variations.md#inserting-assets-into-your-fragment).
   * Possono essere aggiunte solo a elementi di testo su più righe (qualsiasi tipo di frammento).
   * Sono associate al testo che precede (paragrafo).

      >[!CAUTION]
      >
      >Le risorse possono essere rimosse (inavvertitamente) da un frammento se si passa al formato Testo normale.

      >[!NOTE]
      >
      >È inoltre possibile aggiungere le risorse come [contenuto aggiuntivo (intermedio)](/help/sites-authoring/content-fragments.md#using-associated-content) quando si utilizza un frammento su una pagina, utilizzando Contenuto associato o risorse dal Browser risorse.

* **Contenuto associato**

   * Contenuti esterni a un frammento, ma con rilevanza editoriale per esso. In genere si tratta di immagini, video o altri frammenti.
   * Le singole risorse all’interno di una raccolta sono disponibili per essere utilizzate con il frammento nell’editor pagina quando questo viene aggiunto a una pagina. Sono quindi elementi opzionali, a seconda dei requisiti del canale specifico.
   * Le risorse sono [associate a frammenti tramite raccolte](/help/assets/content-fragments/content-fragments-assoc-content.md); le raccolte associate consentono all’autore di decidere quali risorse utilizzare durante l’authoring della pagina.

      * Le raccolte possono essere associate ai frammenti come contenuto predefinito, oppure possono essere associate dagli autori durante la creazione dei frammenti.
      * Le [raccolte di risorse (DAM)](/help/assets/manage-collections.md) sono la base del contenuto associato dei frammenti.
   * Volendo, puoi anche aggiungere il frammento stesso a una raccolta per facilitare il tracciamento.

* **Metadati del frammento**

   * Utilizzano gli [schemi di metadati delle risorse](/help/assets/metadata-schemas.md).
   * È possibile creare i tag quando:

      * si crea e si effettua l’authoring del frammento;
      * oppure in un secondo tempo:

         * visualizzando e modificando le **Proprietà** del frammento dalla console;
         * modificando i **Metadati** nell’editor di frammenti.

   >[!CAUTION]
   >
   >I profili di elaborazione dei metadati non sono applicabili ai frammenti di contenuto.

* **Principale**

   * Parte integrante del frammento

      * Ogni frammento di contenuto dispone di un’istanza Principale.
      * L’elemento Principale non può essere eliminato.
   * L’elemento Principale è accessibile nella sezione **[Varianti](/help/assets/content-fragments/content-fragments-variations.md)** dell’editor di frammenti.
   * l’elemento Principale non è una variante in sé, ma è la base di tutte le varianti.


* **Varianti**

   * Sono rappresentazioni di testo dei frammenti a scopo editoriale; possono essere relative a un canale ma non necessariamente, e possono anche essere utilizzate per modifiche locali ad hoc.
   * Sono create come copie dell’elemento **Principale**, ma possono essere modificate secondo necessità; di solito c’è una sovrapposizione di contenuti tra le varianti stesse.
   * Possono essere definite durante l’authoring del frammento.
   * Sono memorizzate nel frammento, per evitare la dispersione delle copie del contenuto.
   * Le varianti possono essere [sincronizzate](/help/assets/content-fragments/content-fragments-variations.md#synchronizing-with-master) con l’elemento principale se il suo contenuto viene aggiornato.
   * Il testo può essere [riepilogato](/help/assets/content-fragments/content-fragments-variations.md#summarizing-text) per ridurlo rapidamente a una lunghezza predefinita.
   * Sono disponibili nella scheda [Varianti](/help/assets/content-fragments/content-fragments-variations.md) dell’editor di frammenti.

### Contenuto intermedio nell’authoring di pagine con frammenti di contenuto {#in-between-content-when-page-authoring-with-content-fragments}

Contenuto intermedio:

* Può essere utilizzato nell’Editor pagina quando si lavora con frammenti di contenuto.
* Una volta utilizzato o inserito mediante riferimento in una pagina, diventa [contenuto aggiuntivo all’interno del flusso di un frammento](/help/sites-authoring/content-fragments.md#adding-in-between-content).
* Può essere utilizzato nell’[Editor pagina quando si lavora con frammenti di contenuto](/help/sites-authoring/content-fragments.md).
* Il contenuto intermedio può essere aggiunto a qualsiasi frammento, in cui è visibile un solo elemento.
* È possibile utilizzare il contenuto associato, così come le risorse e/o i componenti dal browser appropriato.

>[!CAUTION]
>
>Il contenuto intermedio è contento di pagina. Non viene memorizzato nel frammento di contenuto.

### Elementi necessari per i frammenti {#required-by-fragments}

Per creare frammenti di contenuto sono necessari i seguenti elementi:

* **Modello di contenuto**

   * Viene [abilitato tramite il Browser configurazioni](/help/assets/content-fragments/content-fragments-configuration-browser.md).
   * Viene [creato utilizzando gli strumenti](/help/assets/content-fragments/content-fragments-models.md).
   * È necessario per [creare un frammento](/help/assets/content-fragments/content-fragments-managing.md#creating-content-fragments).
   * Definisce la struttura di un frammento (titolo, elementi di contenuto, definizioni tag).
   * La definizione di un modello di contenuto richiede un titolo e un elemento dati; tutto il resto è facoltativo.
   * Il modello può definire eventuale contenuto predefinito.
   * Durante l’authoring del contenuto di un frammento, gli autori non possono modificare la struttura definita.
   * Le modifiche apportate a un modello dopo la creazione dei frammenti di contenuto dipendenti possono influire su tali frammenti di contenuto.

Per utilizzare i frammenti di contenuto nell’authoring delle pagine è inoltre necessario:

* **Componente Frammento di contenuto**

   * Essenziale per la distribuzione del frammento in formato HTML e/o JSON.
   * Obbligatorio per [fare riferimento al frammento in una pagina](/help/sites-authoring/content-fragments.md).
   * Responsabile del layout e della distribuzione di un frammento, ovvero i canali.
   * I frammenti devono disporre di uno o più componenti dedicati per definire il layout e fornire alcuni o tutti gli elementi/varianti e i contenuti associati.
   * Quando si trascina un frammento su una pagina in fase di authoring, il componente richiesto viene associato automaticamente.

## Esempio di utilizzo {#example-usage}

Un frammento, con i relativi elementi e varianti, può essere utilizzato per creare contenuti coerenti per più canali. Durante la progettazione del frammento è necessario considerare quali elementi verranno utilizzati e dove.
