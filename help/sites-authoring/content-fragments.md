---
title: Authoring delle pagine con frammenti di contenuto
seo-title: Authoring delle pagine con frammenti di contenuto
description: I frammenti di contenuto di AEM consentono di progettare, creare, perfezionare e utilizzare contenuti indipendenti dalle pagine
seo-description: I frammenti di contenuto di AEM consentono di progettare, creare, perfezionare e utilizzare contenuti indipendenti dalle pagine
uuid: 987de428-8354-4b23-a552-3ea415122184
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 4049a7a5-4b33-4462-a25f-3c0daeb6a8a9
docset: aem65
translation-type: tm+mt
source-git-commit: 4d47310ebf9d450de52c925642978ba92ef9c1d4

---


# Authoring delle pagine con frammenti di contenuto{#page-authoring-with-content-fragments}

I frammenti di contenuto di Adobe Experience Manager (AEM) vengono [creati e gestiti come risorse indipendenti dalla pagina](/help/assets/content-fragments.md).

Consentono di creare contenuti versatili utilizzabili in qualsiasi canale, con possibili varianti per canali specifici. Puoi quindi utilizzare questi frammenti, con le relative varianti, durante la creazione di pagine di contenuto.

Insieme alla funzione di esportazione JSON aggiornata, i frammenti di contenuti strutturati possono anche essere utilizzati per distribuire contenuti AEM, tramite i Content Services a canali diversi dalle pagine AEM.

>[!NOTE]
>
>I **frammenti di contenuto** e i **[frammenti esperienza](/help/sites-authoring/experience-fragments.md)**sono funzioni diverse in AEM:
>
>* I **frammenti di contenuto** sono contenuti editoriali, in particolare testo e immagini correlate. Sono contenuti puri, privi di design e layout.
>* I **frammenti esperienza** sono contenuti con un layout completo, un frammento di una pagina Web.
>
>
I frammenti esperienza possono includere contenuti sotto forma di frammenti di contenuto, ma non viceversa.

>[!CAUTION]
>
>This page must be read in conjunction with [Working with Content Fragments](/help/assets/content-fragments.md) (and related pages) as it introduces basic terminology and concepts, together with creating and managing fragments.

I frammenti di contenuto si prestano alle seguenti applicazioni:

* **Strategia di marketing e campagne**

   * Revisione dei contenuti tramite frammenti di contenuto gestiti a livello centrale.

* **Creativi professionisti**

   * Monitoraggio delle risorse creative tramite raccolte associate a frammenti di contenuto.

* **Copywriter**

   * Creazione di contenuti nell’Editor frammento di contenuto di AEM.
   * Creazione di varianti del contenuto.
   * Associazione di contenuti rilevanti ai frammenti di contenuto.
   * Uso delle funzioni di gestione versioni/flusso di lavoro.
   * Condivisione dei frammenti di contenuto.
   * Gestione delle traduzioni a livello centrale.

* **Produttori e responsabili viaggi**

   * Scelta di frammenti predefiniti ed elaborazione di varianti con l’authoring in AEM.
   * Garanzia che il frammento e il contenuto associato ad esso sono sempre aggiornati, con tutte le modifiche apportate dai copywriter e i creativi a frammenti e risorse gestiti a livello centrale.
   * Garanzia che i contenuti multimediali associati sono sempre vagliati e selezionati in base alla loro rilevanza.
   * Possibilità di creare al volo varianti di contenuto ad hoc, con la garanzia che queste restano comunque gestite a livello centrale nel frammento.

## Aggiunta di un frammento di contenuto alla pagina {#adding-a-content-fragment-to-your-page}

1. Apri la pagina per la modifica.

1. Aggiungi il componente **Frammento di contenuto** dal browser **Componenti** o mediante il comando **Inserisci nuovo componente**.

1. Puoi:

   * Open the **Assets** browser and filter for **Content Fragments** (the default is Images). Quindi, trascina il frammento desiderato sull’istanza di componente.

   * Seleziona il componente del frammento di contenuto, quindi **Configura** dalla barra degli strumenti. Nella finestra di dialogo, apri finestra di dialogo per sfogliare e selezionare il **Frammento di contenuto** necessario.
   >[!NOTE]
   >
   >In alternativa, puoi trascinare un frammento di contenuto specifico direttamente sulla pagina. In questo modo verrà creato automaticamente il componente associato (frammento di contenuto).

1. Initially the content from the **Main** Element and **Master** (variation) will be shown. Puoi [selezionare altri elementi e/o varianti](#selecting-the-element-or-variation), come richiesto.

   ![cfm-6420-01](assets/cfm-6420-01.png)

   >[!NOTE]
   >
   >Per informazioni su ulteriori funzionalità di modifica, vedi anche:
   >
   >
   >
   >    * [Layout reattivo](/help/sites-authoring/responsive-layout.md)
   >    * [Modifica del contenuto di una pagina](/help/sites-authoring/editing-content.md)


### Selezione dell’elemento o della variante {#selecting-the-element-or-variation}

Apri la finestra di dialogo **Configurazione** del frammento per configurare il frammento per la pagina corrente. La finestra di dialogo può dipendere dal componente utilizzato.

Nella finestra di dialogo di configurazione appropriata puoi selezionare i parametri disponibili, tra cui:

* **Frammento di contenuto**

   Specifica il frammento da utilizzare.

* **Modalità di visualizzazione**:

   * **Elemento di testo singolo**

   * **Vari elementi**

* **Elemento**

   * L’elemento predefinito **Principale** è sempre disponibile.
   * Una selezione è disponibile se il frammento è stato creato con un modello appropriato. 
   >[!NOTE]
   >
   >Gli elementi disponibili dipendono dal modello utilizzato.

* **Variante**

   * La variante predefinita **Principale** è sempre disponibile.
   * Una selezione è disponibile se per il frammento sono state create delle varianti.

* **Paragrafi**: specifica l’intervallo di paragrafi da includere:

   * **Tutti**
   * **Intervallo**: ad esempio, `1`, `3-5`, `9-*`

      * **Tratta le intestazioni come paragrafi propri**

* **Tratta le intestazioni come paragrafi propri**

### Collegamento rapido all’Editor frammento di contenuto {#quick-connection-to-fragment-editor}

Puoi aprire l’origine del frammento in modalità di modifica (la risorsa) mediante l’icona **Modifica** nella barra degli strumenti del componente, così da poter [modificare e gestire il frammento di contenuto](/help/assets/content-fragments.md).

>[!CAUTION]
>
>Come sempre, la modifica dell’origine del frammento ha un impatto su tutte le pagine che fanno riferimento a tale frammento di contenuto.

### Aggiunta di contenuto intermedio {#adding-in-between-content}

Quando si aggiunge alla pagina un frammento di contenuto specifico, è disponibile un segnaposto **Trascina qui i componenti** fra ciascun paragrafo HTML (nonché all’inizio e alla fine) del frammento.

Questo consente di aggiungere ulteriori contenuti [intermedi (ad esempio, contenuti intermedi)](/help/assets/content-fragments.md#inbetweencontent) all’interno del contenuto del frammento (nei punti disponibili), senza dover modificare il frammento principale.

Per il contenuto intermedio puoi effettuare le seguenti operazioni:

* Aggiungere componenti dal [browser Componenti](/help/sites-authoring/author-environment-tools.md#components-browser).
* Aggiungere risorse dal [browser Risorse](/help/sites-authoring/author-environment-tools.md#assets-browser).
* Use [Associated Content](#using-associated-content) as a source for in-between content.

>[!CAUTION]
>
>Il contenuto intermedio è contento di pagina. Non viene memorizzato nel frammento di contenuto.

![cfm-6420-02](assets/cfm-6420-02.png)

>[!NOTE]
>
>Puoi anche [inserire risorse visive (immagini) nel frammento stesso](/help/assets/content-fragments-variations.md#inserting-assets-into-your-fragment).
>
>Le risorse visive inserite nel frammento stesso sono associate al paragrafo precedente nel frammento. Non è pertanto possibile inserire contenuto intermedio tra una risorsa visiva e il paragrafo precedente.

>[!CAUTION]
>
>Dopo aver aggiunto contenuto intermedio a un frammento di contenuto nella pagina, se si modifica la struttura del frammento di contenuto sottostante (ovvero nell’Editor frammento di contenuto) si potrebbero verificare risultati erronei o imprevisti.
>
>In questi casi, il contenuto intermedio viene mantenuto inalterato:
>
>* I componenti intermedi hanno una posizione assoluta all’interno della sequenza di componenti nel flusso del frammento. Questa posizione resta invariata, anche quando cambia il contenuto dei paragrafi nel frammento.
   >  Questo può far apparire il paragrafo come se fosse stato modificato il posizionamento relativo, poiché i paragrafi intermedi non hanno alcuna relazione contestuale con i paragrafi (frammento) a cui sono posizionati accanto.
>* a meno che le due strutture di paragrafo non siano in conflitto. In questo caso il contenuto intermedio non viene visualizzato, ma resta comunque presente nel codice interno.
>



### Uso di contenuti associati {#using-associated-content}

Se sono presenti [contenuti associati](/help/assets/content-fragments-assoc-content.md) al [frammento di contenuto](/help/assets/content-fragments.md), tali risorse saranno disponibili nel pannello laterale (dopo che avrai inserito il frammento nella pagina del contenuto). Il contenuto associato è sostanzialmente un’origine speciale di contenuti per il [contenuto intermedio](#adding-in-between-content).

>[!NOTE]
>
>Esistono diversi metodi per aggiungere [risorse visive (ad es. immagini)](/help/assets/content-fragments.md#fragments-with-visual-assets) al frammento e/o alla pagina.

>[!NOTE]
>
>Se sulla stessa pagina sono presenti più frammenti di contenuto, la scheda **Contenuto associato** visualizza le risorse appropriate per tutti i frammenti.

Una volta aggiunto alla pagina un frammento con contenuto associato, nel pannello laterale viene aperta una nuova scheda (**Contenuto associato**) . 

Da qui puoi trascinare le risorse nella posizione richiesta (su un componente esistente o nella posizione in cui sarà creato il componente appropriato):

![cfm-6420-03](assets/cfm-6420-03.png)

### Risorse inserite nel frammento {#assets-inserted-into-the-fragment}

Se sono state inserite risorse (ad es. immagini) nel frammento stesso, le opzioni per la modifica di tali risorse nell’editor pagina sono limitate. <!-- Removed link as it was a 404 on helpx -->

Ad esempio, per un’immagine è possibile

* Ritagliare, ruotare o capovolgere l’immagine.
* Aggiungere un titolo o testo alternativo.
* Specificare una dimensione.
* Puoi anche configurare il layout.

Altre modifiche, come spostamento, copia, eliminazione devono essere eseguite nell’editor frammento.

### Pubblicazione {#publishing}

I frammenti devono essere pubblicati in modo che possano essere utilizzati nelle pagine Web pubblicate:

* Un frammento può essere pubblicato dopo che è stato [creato nella console Risorse](/help/assets/content-fragments.md#publishingandreferencingafragment).
* Se in una pagina in corso di pubblicazione viene utilizzato un *frammento non pubblicato*, è possibile pubblicare anche quest’ultimo allo stesso tempo.

