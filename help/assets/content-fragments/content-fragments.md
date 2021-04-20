---
title: Utilizzo di frammenti di contenuto
seo-title: Utilizzo di frammenti di contenuto
description: Scopri come i frammenti di contenuto ti consentono di progettare, creare, curare e utilizzare contenuti indipendenti dalla pagina.
seo-description: Scopri come i frammenti di contenuto ti consentono di progettare, creare, curare e utilizzare contenuti indipendenti dalla pagina.
uuid: d35d5638-43a9-424d-9806-6e8d459980d7
contentOwner: Alison Heimoz
topic-tags: content-fragments
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
discoiquuid: 7ecc1bcf-38a9-4a59-8dd3-79cb90dec33d
docset: aem65
feature: Content Fragments
role: Business Practitioner, Administrator
translation-type: tm+mt
source-git-commit: aec4530fa93eacd151ca069c2da5d1bc92408e10
workflow-type: tm+mt
source-wordcount: '1978'
ht-degree: 7%

---


# Utilizzo di frammenti di contenuto{#working-with-content-fragments}

I frammenti di contenuto Adobe Experience Manager (AEM) consentono di progettare, creare, curare e [pubblicare contenuti indipendenti dalla pagina](/help/sites-authoring/content-fragments.md). Consentono di preparare i contenuti pronti per l’uso in più posizioni/su più canali.

I frammenti di contenuto possono essere consegnati anche in formato JSON, utilizzando le funzionalità di esportazione Sling Model (JSON) dei componenti core AEM. Questo tipo di consegna:

* consente di utilizzare il componente per gestire gli elementi di un frammento da distribuire
* consente la distribuzione in blocco, aggiungendo più componenti core dei frammenti di contenuto nella pagina utilizzata per la distribuzione API

Nelle pagine seguenti sono illustrate le attività di creazione, configurazione e manutenzione dei frammenti di contenuto:

* [Gestione dei frammenti di contenuto](/help/assets/content-fragments/content-fragments-managing.md) : crea i frammenti di contenuto; quindi modifica, pubblica e fai riferimento a
* [Modelli per frammenti di contenuto](/help/assets/content-fragments/content-fragments-models.md) : abilitazione, creazione e definizione dei modelli
* [Varianti - Creazione di contenuti](/help/assets/content-fragments/content-fragments-variations.md)  di frammento - Creazione di contenuti di frammento e creazione di varianti del contenuto principale
* [Markdown](/help/assets/content-fragments/content-fragments-markdown.md) : utilizzo della sintassi Markdown per il frammento
* [Utilizzo del contenuto associato](/help/assets/content-fragments/content-fragments-assoc-content.md)  - aggiunta del contenuto associato
* [Metadati - Proprietà](/help/assets/content-fragments/content-fragments-metadata.md)  frammento - visualizzazione e modifica delle proprietà del frammento

>[!NOTE]
>
>Queste pagine devono essere lette insieme a [Authoring delle pagine con frammenti di contenuto](/help/sites-authoring/content-fragments.md).

Il numero di canali di comunicazione aumenta ogni anno. In genere i canali si riferiscono al meccanismo di consegna, come segue:

* canale fisico; ad esempio desktop, mobile.
* forma di consegna in un canale fisico; Ad esempio, &quot;pagina di dettaglio del prodotto&quot;, &quot;pagina di categoria del prodotto&quot; per desktop o &quot;web mobile&quot;, &quot;app mobile&quot; per dispositivi mobili.

Tuttavia, probabilmente non desideri utilizzare esattamente lo stesso contenuto per tutti i canali: è necessario ottimizzare il contenuto in base al canale specifico.

I frammenti di contenuto consentono di:

* Valuta come raggiungere in modo efficiente i tipi di pubblico target tra i vari canali.
* Crea e gestisci contenuti editoriali neutri per il canale.
* Crea pool di contenuti per una serie di canali.
* Progetta varianti di contenuto per canali specifici.
* Aggiungi le immagini al testo inserendo le risorse (frammenti con file multimediali diversi).

Questi frammenti di contenuto possono quindi essere assemblati per fornire esperienze su diversi canali.

## Frammenti di contenuto e servizi di contenuto {#content-fragments-and-content-services}

AEM Content Services è progettato per generalizzare la descrizione e la distribuzione dei contenuti in/da AEM oltre l’attenzione sulle pagine web.

Forniscono contenuti a canali che non sono pagine web AEM tradizionali, utilizzando metodi standardizzati utilizzabili da qualsiasi cliente. Questi canali possono includere:

* Applicazioni a pagina singola
* Applicazioni mobile native
* altri canali e punti di contatto esterni a AEM

La consegna viene effettuata in formato JSON.

I frammenti di contenuto AEM possono essere utilizzati per descrivere e gestire contenuti strutturati. Il contenuto strutturato è definito in modelli che possono contenere diversi tipi di contenuto; compresi testo, dati numerici, booleano, data e ora e altro ancora.

Insieme alle funzionalità di esportazione JSON dei componenti di base AEM, questo contenuto strutturato può quindi essere utilizzato per distribuire contenuti AEM a canali diversi dalle AEM pagine.

>[!NOTE]
>
>I **frammenti di contenuto** e i **[frammenti esperienza](/help/sites-authoring/experience-fragments.md)** sono funzioni diverse in AEM:
>* I **frammenti di contenuto** sono contenuti editoriali, in particolare testo e immagini correlate. Sono contenuti puri, privi di design e layout.
>* I **frammenti esperienza** sono contenuti con un layout completo, un frammento di una pagina Web.

>
>
I frammenti esperienza possono includere contenuti sotto forma di frammenti di contenuto, ma non viceversa.
>
>Per ulteriori informazioni, consulta anche [Informazioni sui frammenti di contenuto e i frammenti di esperienza in AEM](https://docs.adobe.com/content/help/en/experience-manager-learn/sites/content-fragments/understand-content-fragments-and-experience-fragments.html).

>[!CAUTION]
>
>I frammenti di contenuto non sono disponibili nell’interfaccia classica.
>
>Il componente Frammento di contenuto può essere visualizzato nella barra laterale dell’interfaccia classica, ma ulteriori funzionalità non sono disponibili.

>[!NOTE]
>
>AEM supporta anche la traduzione del contenuto del frammento. Per ulteriori informazioni, consulta [Creazione di progetti di traduzione per frammenti di contenuto](/help/assets/creating-translation-projects-for-content-fragments.md) .

## Tipi di frammento di contenuto {#types-of-content-fragment}

I frammenti di contenuto possono essere:

* Frammenti semplici
Non hanno una struttura predefinita. Contengono solo testo e immagini.
Si basano sul modello Frammento semplice .

* Frammenti contenenti contenuto strutturato
Si basano su un [modello di frammento di contenuto](/help/assets/content-fragments/content-fragments-models.md) che predefinisce una struttura per il frammento risultante.
Questi possono anche essere utilizzati per realizzare Content Services utilizzando l’esportatore JSON.

## Tipo di contenuto {#content-type}

I frammenti di contenuto sono:

* Memorizzato come **Risorse**:

   * I frammenti di contenuto (e le relative varianti) possono essere creati e gestiti dalla console **Risorse**.
   * Authoring e modifica nell’Editor frammento di contenuto.

* Utilizzato nell’ [editor di pagine tramite il componente Frammento di contenuto](/help/sites-authoring/content-fragments.md) (componente di riferimento):

   * Il componente **Frammento di contenuto** è disponibile per gli autori di pagine. Consente loro di fare riferimento e distribuire il frammento di contenuto richiesto in formato HTML o JSON.

I frammenti di contenuto sono una struttura di contenuto che:

* Sono prive di layout o design (in modalità RTF è possibile formattare del testo).
* Contenere una o più parti [costituenti](#constituent-parts-of-a-content-fragment).
* Può [contenere o essere connesso a immagini](#fragments-with-visual-assets).
* Può utilizzare [contenuto intermedio](#in-between-content-when-page-authoring-with-content-fragments) quando si fa riferimento a una pagina.

* Sono indipendenti dal meccanismo di consegna (ad esempio, pagina, canale).

### Frammenti con risorse visive {#fragments-with-visual-assets}

Per dare agli autori un maggiore controllo sui contenuti, le immagini possono essere aggiunte a e/o integrate con un frammento di contenuto.

Le risorse possono essere utilizzate con un frammento di contenuto in diversi modi; ciascuno con i propri vantaggi:

* **Inserire un** elemento in un frammento (frammenti con file multimediali diversi)

   * Sono parte integrante del frammento (consulta [Parti componenti di un frammento di contenuto](#constituent-parts-of-a-content-fragment)).
   * Definisci la posizione della risorsa.
   * Per ulteriori informazioni, consulta [Inserimento di risorse nel frammento](/help/assets/content-fragments/content-fragments-variations.md#inserting-assets-into-your-fragment) nell’Editor frammento .

   >[!NOTE]
   >
   >Le risorse visive inserite nel frammento di contenuto stesso sono associate al paragrafo precedente. Quando il frammento viene aggiunto a una pagina, queste risorse vengono spostate in relazione a tale paragrafo quando viene aggiunto del contenuto intermedio.

* **Contenuto associato**

   * sono collegati a un frammento; ma non una parte fissa del frammento (vedere [Parti componenti di un frammento di contenuto](#constituent-parts-of-a-content-fragment)).
   * Consente una certa flessibilità per il posizionamento.
   * Sono facilmente disponibili per l’uso (come nel contenuto intermedio) quando si utilizza il frammento su una pagina.
   * Per ulteriori informazioni, consulta [Contenuto associato](/help/assets/content-fragments/content-fragments-assoc-content.md) .

* Risorse disponibili nel **browser Risorse** dell’editor pagina

   * Consenti flessibilità completa per la selezione di una risorsa.
   * Consente una certa flessibilità per il posizionamento.
   * Non fornisce il concetto di approvazione per un frammento specifico.
   * Per ulteriori informazioni, consulta [Browser risorse](/help/sites-authoring/author-environment-tools.md#assets-browser) .

### Parti costitutive di un frammento di contenuto {#constituent-parts-of-a-content-fragment}

Le risorse dei frammenti di contenuto sono composte dalle seguenti parti (direttamente o indirettamente):

* **Elementi frammento**

   * Gli elementi sono correlati ai campi di dati che contengono contenuto.
   * Per i frammenti con contenuto strutturato, è possibile utilizzare un modello di contenuto per creare il frammento di contenuto. Gli elementi (campi) specificati nel modello definiscono la struttura del frammento. Questi elementi (campi) possono essere di diversi tipi di dati.
   * Per frammenti semplici:

      * Il contenuto è contenuto in uno o più campi di testo a più righe o elementi.
      * Gli elementi sono definiti nel modello di frammento (non è possibile definirli durante la creazione del frammento, consulta [Modelli di frammento di contenuto](/help/sites-developing/content-fragment-templates.md)).

* **Paragrafi frammento**

   * Blocchi di testo, ovvero:

      * separati da spazi verticali (ritorno a capo)
      * in elementi di testo su più righe; in frammenti semplici o strutturati
   * Nelle modalità [Rich Text](/help/assets/content-fragments/content-fragments-variations.md#rich-text) e [Markdown](/help/assets/content-fragments/content-fragments-variations.md#markdown), un paragrafo può essere formattato come intestazione, in tal caso appartiene a un’unica unità insieme al paragrafo seguente.

   * Abilita il controllo dei contenuti durante la creazione delle pagine.


* **Risorse inserite in un frammento (frammenti di file multimediali diversi)**

   * Risorse (immagini) inserite nel frammento effettivo e utilizzate come contenuto interno di un frammento.
   * Sono incorporati nel sistema paragrafo del frammento.
   * Può essere formattato quando il frammento [viene utilizzato/a cui si fa riferimento in una pagina](/help/sites-authoring/content-fragments.md).
   * È possibile aggiungere, eliminare o spostare solo all’interno di un frammento utilizzando l’editor frammenti. Queste azioni non possono essere eseguite nell’editor pagina.
   * È possibile aggiungere, eliminare o spostare solo all’interno di un frammento utilizzando il formato [RTF nell’editor frammenti](/help/assets/content-fragments/content-fragments-variations.md#inserting-assets-into-your-fragment).
   * Può essere aggiunto solo a elementi di testo su più righe (qualsiasi tipo di frammento).
   * sono allegati al testo precedente (paragrafo).

   >[!CAUTION]
   >
   >Può essere rimosso (inavvertitamente) da un frammento passando al formato Testo normale.

   >[!NOTE]
   >
   >Le risorse possono anche essere aggiunte come [contenuto aggiuntivo (intermedio)](/help/sites-authoring/content-fragments.md#using-associated-content) quando si utilizza un frammento in una pagina; utilizzando Contenuto associato o risorse dal browser Risorse.

* **Contenuto associato**

   * Si tratta di contenuti esterni a un frammento, ma con rilevanza editoriale per esso. In genere immagini, video o altri frammenti.
   * Le singole risorse all’interno della raccolta sono disponibili per l’utilizzo con il frammento nell’editor di pagine quando viene aggiunto a una pagina. Ciò significa che sono opzionali, a seconda dei requisiti del canale specifico.
   * Le risorse sono [associate ai frammenti tramite raccolte](/help/assets/content-fragments/content-fragments-assoc-content.md); le raccolte associate consentono all’autore di decidere quali risorse utilizzare durante la creazione della pagina.

      * Le raccolte possono essere associate ai frammenti tramite modelli, come contenuto predefinito o da parte degli autori durante la creazione dei frammenti.
      * [Le ](/help/assets/manage-collections.md) raccolte risorse (DAM) sono la base per il contenuto associato dei frammenti.
   * Facoltativamente, puoi anche aggiungere il frammento stesso a una raccolta per facilitare il tracciamento.


* **Metadati frammento**

   * Utilizza gli schemi di metadati [Assets](/help/assets/metadata.md).
   * I tag possono essere creati quando:

      * Creare e creare il frammento
      * O successivo:

         * Visualizzando/modificando il frammento **Proprietà** dalla console
         * Modificando i **metadati** nell’editor frammenti

   >[!CAUTION]
   >
   >I profili di elaborazione dei metadati non si applicano ai frammenti di contenuto.

* **Principale**

   * Parte integrante del frammento

      * Ogni frammento di contenuto dispone di un’istanza di Master.
      * Impossibile eliminare il master.
   * Master è accessibile nell’editor frammenti in **[Variazioni](/help/assets/content-fragments/content-fragments-variations.md)**.
   * Master non è una variazione in quanto tale, ma è la base di tutte le variazioni.


* **Varianti**

   * rappresentazioni di testo di frammento specifiche per scopi editoriali; può essere correlato al canale ma non è obbligatorio, può anche essere per modifiche locali ad hoc.
   * Sono create come copie di **Master**, ma possono essere modificate come necessario; di solito c&#39;è una sovrapposizione dei contenuti tra le varianti stesse.
   * Può essere definito durante l’authoring dei frammenti o predefinito nei modelli di frammento.
   * Memorizzato nel frammento, per evitare la dispersione delle copie del contenuto.
   * Le varianti possono essere [sincronizzate](/help/assets/content-fragments/content-fragments-variations.md#synchronizing-with-master) con Master se il contenuto principale è stato aggiornato.
   * Può essere [Riepilogato](/help/assets/content-fragments/content-fragments-variations.md#summarizing-text) per troncare rapidamente il testo fino a una lunghezza predefinita.
   * Disponibile nella scheda [Variazioni](/help/assets/content-fragments/content-fragments-variations.md) dell’editor frammenti.

### Contenuto intermedio durante l’authoring della pagina con frammenti di contenuto {#in-between-content-when-page-authoring-with-content-fragments}

Contenuto intermedio:

* È disponibile per l’uso nell’ [Editor pagina quando si lavora con Frammenti di contenuto](/help/sites-authoring/content-fragments.md).
* È [contenuto aggiuntivo aggiunto all&#39;interno del flusso di un frammento](/help/sites-authoring/content-fragments.md#adding-in-between-content) una volta utilizzato/a cui è stato fatto riferimento in una pagina.
* Il contenuto intermedio può essere aggiunto a qualsiasi frammento, in cui è visibile un solo elemento.
* È possibile utilizzare il contenuto associato, così come le risorse e/o i componenti dal browser appropriato.

>[!CAUTION]
>
>Il contenuto intermedio è contento di pagina. Non viene memorizzato nel frammento di contenuto.

### Obbligatorio per frammenti {#required-by-fragments}

Per creare, modificare e utilizzare frammenti di contenuto è inoltre necessario effettuare le operazioni riportate di seguito.

* **Modello di contenuto**

   * Sono abilitati [e quindi creati utilizzando Tools](/help/assets/content-fragments/content-fragments-models.md).
   * Obbligatorio per [creare un frammento strutturato](/help/assets/content-fragments/content-fragments-managing.md#creating-content-fragments).
   * Definisce la struttura di un frammento (titolo, elementi di contenuto, definizioni di tag).
   * Le definizioni dei modelli di contenuto richiedono un titolo e un elemento dati; tutto il resto è facoltativo. Il modello definisce un ambito minimo del frammento e, se applicabile, del contenuto predefinito. Gli autori non possono modificare la struttura definita durante la creazione del contenuto di un frammento.

* **Modello frammento**

   * Obbligatorio per [creare un frammento semplice](/help/assets/content-fragments/content-fragments-managing.md#creating-content-fragments).
   * Generalmente [sviluppato durante l&#39;implementazione del progetto](/help/sites-developing/content-fragment-templates.md); non può essere creato durante l’authoring.
   * Definisce le proprietà di base di un frammento semplice (titolo, numero di elementi di testo, definizioni di tag).
   * Le definizioni dei modelli richiedono un titolo e un elemento di testo; tutto il resto è facoltativo. Il modello definisce un ambito minimo del frammento e, se applicabile, del contenuto predefinito. In seguito, gli autori possono estendere un frammento oltre a quanto definito nel modello.

* **Componente Frammento di contenuto**

   * Strumentale per la distribuzione del frammento in formato HTML e/o JSON.
   * Obbligatorio per [fare riferimento al frammento in una pagina](/help/sites-authoring/content-fragments.md).
   * Responsabile del layout e della consegna di un frammento; ovvero canali.
   * I frammenti devono disporre di uno o più componenti dedicati per definire il layout e fornire alcuni o tutti gli elementi/varianti e i contenuti associati.
   * Quando si trascina un frammento su una pagina in fase di creazione, il componente richiesto viene associato automaticamente.

## Esempio di utilizzo {#example-usage}

Un frammento, con i relativi elementi e varianti, può essere utilizzato per creare contenuti coerenti per più canali. Durante la progettazione del frammento è necessario considerare gli elementi da utilizzare in che punto.

### Esempio di We.Retail {#we-retail-sample}

Un frammento di esempio è disponibile in:

`https://localhost:4502/assets.html/content/dam/we-retail/en/experiences/arctic-surfing-in-lofoten`
