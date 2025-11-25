---
title: Authoring delle pagine di contenuti con frammenti di contenuto
description: I Frammenti di contenuto di AEM ti consentono di progettare, creare, curare e utilizzare contenuti indipendenti dalla pagina.
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
docset: aem65
exl-id: d5dad844-80ca-4ace-a082-38d892d9ffe2
solution: Experience Manager, Experience Manager Sites
feature: Authoring,Content Fragments
role: User,Admin,Developer
source-git-commit: c77849740fab51377ce60aff5f611e0408dca728
workflow-type: tm+mt
source-wordcount: '1138'
ht-degree: 63%

---

# Authoring delle pagine con frammenti di contenuto{#page-authoring-with-content-fragments}

I frammenti di contenuto di Adobe Experience Manager (AEM) vengono [creati e gestiti come risorse indipendenti dalla pagina](/help/assets/content-fragments/content-fragments.md).

Consentono di creare contenuti indipendenti dal canale, con possibili varianti per canali specifici. Puoi quindi utilizzare questi frammenti, con le relative varianti, durante l’authoring di pagine di contenuto.

Insieme alla funzione di esportazione JSON aggiornata, i frammenti di contenuti strutturati possono anche essere utilizzati per distribuire contenuti AEM, tramite Content Services a canali diversi dalle pagine AEM.

>[!NOTE]
>
>I **frammenti di contenuto** e i **[frammenti di esperienza](/help/sites-authoring/experience-fragments.md)** sono funzioni diverse in AEM:
>
>* **I frammenti di contenuto** sono contenuti editoriali, principalmente testo e immagini correlate. Sono contenuti puri, senza design e layout.
>* I **frammenti di esperienza** sono contenuti completi di layout, frammenti di una pagina web.
>
>I frammenti esperienza possono includere contenuti sotto forma di frammenti di contenuto, ma non viceversa.

>[!CAUTION]
>
>Questa pagina deve essere letta con [Utilizzo dei frammenti di contenuto](/help/assets/content-fragments/content-fragments.md) (e pagine correlate) perché introduce la terminologia e i concetti di base e spiega come creare e gestire i frammenti.

I frammenti di contenuto consentono:

* La **Strategia di marketing e campagne**

   * La revisione dei contenuti tramite frammenti di contenuto gestiti a livello centrale.

* **Creative Pro**

   * Il tracciamento delle risorse creative tramite raccolte associate a frammenti di contenuto.

* **Copywriter**

   * Creazione di contenuti nell’editor frammento di contenuto di AEM.
   * Possono creare varianti del contenuto.
   * Possono associare contenuti rilevanti ai frammenti di contenuto.
   * Possono utilizzare il controllo delle versioni/flusso di lavoro.
   * Possono condividere dei frammenti di contenuto.
   * Possono gestire le traduzioni a livello centrale.

* **Produttori e responsabili dei percorsi**

   * Scelta di frammenti e varianti predefiniti con l’authoring in AEM.
   * Possono contare sul fatto che il frammento e il contenuto associato ad esso sono sempre aggiornati, poiché i copywriter e i creativi effettuano gli aggiornamenti su frammenti e risorse gestiti a livello centrale.
   * Possono contare sul fatto che i contenuti multimediali associati sono sempre curati in base alla rilevanza.
   * Possono creare all’istante varianti di contenuto ad hoc garantendo che queste restino comunque gestite a livello centrale nel frammento.

## Aggiunta di un frammento di contenuto alla pagina  {#adding-a-content-fragment-to-your-page}

1. Apri la pagina per la modifica.

1. Aggiungi il componente **Frammento di contenuto** dal browser **Componenti** o mediante il comando **Inserisci nuovo componente**.

1. Puoi effettuare le seguenti operazioni:

   * Apri il browser **Risorse** e applica il filtro **Frammenti di contenuto** (l’impostazione predefinita è Immagini). Poi trascina il frammento desiderato sull’istanza del componente.

   * Seleziona il componente del frammento di contenuto, quindi **Configura** dalla barra degli strumenti. Nella finestra di dialogo, puoi aprire la finestra di dialogo di selezione per sfogliare e selezionare il **Frammento di contenuto** richiesto.

   >[!NOTE]
   >
   >In alternativa, puoi trascinare un frammento di contenuto specifico direttamente nella pagina. In questo modo viene creato automaticamente il componente associato (Frammento di contenuto).

1. Inizialmente viene visualizzato il contenuto dell&#39;elemento **Main** e **Master** (variante). Puoi [selezionare altri elementi e/o varianti](#selecting-the-element-or-variation), secondo necessità.

   ![cfm-6420-01](assets/cfm-6420-01.png)

   >[!NOTE]
   >
   >Per ulteriori informazioni su ulteriori funzionalità di modifica, vedere:
   >
   >
   >
   >    * [Layout dinamico](/help/sites-authoring/responsive-layout.md)
   >    * [Modifica del contenuto di una pagina](/help/sites-authoring/editing-content.md)
   >
   >

### Selezione dell’elemento o della variante {#selecting-the-element-or-variation}

Apri la finestra di dialogo **Configurazione** del frammento per configurare il frammento per la pagina corrente. La finestra di dialogo può dipendere dal componente utilizzato.

Nella finestra di dialogo di configurazione appropriata potete selezionare i parametri disponibili, tra cui:

* **Frammento di contenuto**

  Specifica il frammento da utilizzare.

* **Modalità di visualizzazione**:

   * **Elemento di testo singolo**

   * **Elemento multiplo**

* **Elemento**

   * Il valore predefinito **Principale** è sempre disponibile.
   * Se il frammento è stato creato con un modello appropriato, è disponibile una selezione.

  >[!NOTE]
  >
  >Gli elementi disponibili dipendono dal modello utilizzato.

* **Variazione**

   * Il **Master** predefinito è sempre disponibile.
   * Se per il frammento sono state create delle varianti, è disponibile una selezione.

* **Paragrafi**: specificare l&#39;intervallo di paragrafi da includere:

   * **Tutti**
   * **Intervallo**: ad esempio, `1`, `3-5`, `9-*`

      * **Tratta le intestazioni come paragrafi propri**

* **Tratta le intestazioni come paragrafi propri**

### Collegamento rapido all’Editor frammento di contenuto  {#quick-connection-to-fragment-editor}

Puoi aprire l’origine del frammento in modalità di modifica (la risorsa) mediante l’icona **Modifica** nella barra degli strumenti del componente, Ciò ti consente di [modificare e gestire il frammento di contenuto](/help/assets/content-fragments/content-fragments.md).

>[!CAUTION]
>
>Come sempre, la modifica dell’origine del frammento può avere un impatto su tutte le pagine che fanno riferimento a tale frammento di contenuto.

### Aggiunta di contenuto intermedio  {#adding-in-between-content}

Quando un frammento di contenuto specifico viene aggiunto alla pagina, è disponibile un segnaposto **Trascina qui i componenti** tra ciascun paragrafo HTML (e nella parte superiore/inferiore) del frammento.

In questo modo è possibile aggiungere contenuto aggiuntivo [nel contenuto intermedio (ovvero nel contenuto intermedio)](/help/assets/content-fragments/content-fragments.md#in-between-content-when-page-authoring-with-content-fragments) nel contenuto del frammento (in qualsiasi punto disponibile), senza dover modificare il frammento principale.

Per il contenuto intermedio è possibile:

* aggiungere componenti dal [browser Componenti](/help/sites-authoring/author-environment-tools.md#components-browser).
* aggiungere risorse dal [bowser Risorse](/help/sites-authoring/author-environment-tools.md#assets-browser).
* usare [Contenuto associato](#using-associated-content) come origine per il contenuto intermedio.

>[!CAUTION]
>
>Il contenuto intermedio è il contenuto della pagina. Non viene memorizzato nel frammento di contenuto.

![cfm-6420-02](assets/cfm-6420-02.png)

>[!NOTE]
>
>È inoltre possibile [inserire risorse visive (immagini) nel frammento stesso](/help/assets/content-fragments/content-fragments-variations.md#inserting-assets-into-your-fragment).
>
>Le risorse visive inserite nel frammento stesso sono associate al paragrafo precedente nel frammento. Ciò significa che non è possibile posizionare contenuto intermedio tra una risorsa visiva e il paragrafo precedente.

>[!CAUTION]
>
>Dopo aver aggiunto contenuto intermedio a un frammento di contenuto nella pagina, se si modifica la struttura del frammento di contenuto sottostante (ovvero nell’editor frammento di contenuto) si potrebbero verificare risultati erronei o imprevisti.
>
>In questo caso, il contenuto intermedio rimane invariato:
>
>* I componenti intermedi hanno una posizione assoluta all’interno della sequenza di componenti nel flusso del frammento. Questa posizione non cambia, anche quando cambia il contenuto dei paragrafi nel frammento.
>
>  Questo potrebbe dare l’impressione di una modifica nella posizione relativa, poiché i paragrafi intermedi non hanno alcuna relazione contestuale con i paragrafi (del frammento) accanto ai quali sono posizionati,
>* a meno che le due strutture di paragrafo non siano in conflitto. In questo caso il contenuto intermedio non viene visualizzato, ma resta comunque presente nel codice interno.
>

### Uso di contenuti associati  {#using-associated-content}

Se hai [contenuto associato](/help/assets/content-fragments/content-fragments-assoc-content.md) al [frammento di contenuto](/help/assets/content-fragments/content-fragments.md), queste risorse sono disponibili nel pannello laterale (dopo aver inserito il frammento nella pagina del contenuto). Il contenuto associato è di fatto una fonte speciale di contenuto per il [contenuto intermedio](#adding-in-between-content).

>[!NOTE]
>
>Esistono vari metodi per aggiungere [risorse visive (ad esempio immagini)](/help/assets/content-fragments/content-fragments.md#fragments-with-visual-assets) al frammento e/o alla pagina.

>[!NOTE]
>
>Se in una pagina sono presenti più frammenti di contenuto, nella scheda **Contenuto associato** sono visualizzate le risorse appropriate per tutti i frammenti.

Dopo aver aggiunto alla pagina un frammento con contenuto associato, nel pannello laterale viene aperta una nuova scheda (**Contenuto associato**).

Da qui puoi trascinare le risorse nella posizione richiesta (su un componente esistente o nella posizione in cui viene creato il componente appropriato):

![cfm-6420-03](assets/cfm-6420-03.png)

### Risorse inserite nel frammento {#assets-inserted-into-the-fragment}

Se sono state inserite delle risorse (ad esempio immagini) nel frammento stesso, le opzioni per la modifica di tali risorse nell’editor pagina sono limitate. <!-- Removed link as it was a 404 on helpx -->

Ad esempio, per un’immagine è possibile:

* Ritaglia, ruota o capovolge l’immagine.
* Aggiungi un titolo o un testo alternativo.
* Specifica una dimensione.
* Puoi anche configurare il layout.

Altre modifiche, ad esempio sposta, copia ed elimina devono essere effettuate nell’editor frammenti.

### Pubblicazione {#publishing}

I frammenti devono essere pubblicati in modo da poter essere utilizzati sulle pagine web pubblicate:

* Un frammento può essere pubblicato dopo [la creazione del frammento nella console Assets](/help/assets/content-fragments/content-fragments.md#publishingandreferencingafragment).
* Se in una pagina in corso di pubblicazione viene utilizzato un frammento *non pubblicato*, è anche possibile pubblicare ora il frammento.
