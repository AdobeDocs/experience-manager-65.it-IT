---
title: Modelli
seo-title: Modelli
description: I modelli vengono utilizzati per creare una pagina che verrà utilizzata come base per la nuova pagina
seo-description: I modelli vengono utilizzati per creare una pagina che verrà utilizzata come base per la nuova pagina
uuid: 6fa3dafc-dfa1-42d8-b296-d4be57449411
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 7c723773-7c23-43d7-85dc-53e54556b648
legacypath: /content/docs/en/aem/6-1/develop/the-basics/templates
translation-type: tm+mt
source-git-commit: 2fc35bfd93585a586cb1d4e3299261611db49ba6

---


# Modelli{#templates}

I modelli vengono utilizzati in vari punti di AEM:

* When [creating a page you need to select a template](#templates-pages); this will be used as the base for the new page. The template defines the structure of the resultant page, any initial content and the [components](/help/sites-authoring/default-components.md) that can be used (design properties).

* Per [creare un frammento di contenuto è necessario selezionare anche un modello](#templates-content-fragments). Questo modello definisce la struttura, gli elementi iniziali e le varianti.

Vengono descritti in dettaglio i seguenti modelli:

* [Modelli di pagina - Modificabili](/help/sites-developing/page-templates-editable.md)
* [Modelli di pagina - Statici](/help/sites-developing/page-templates-static.md)
* [Modelli di frammento di contenuto](/help/sites-developing/content-fragment-templates.md)
* [Rendering dei modelli adattivi](/help/sites-developing/templates-adaptive-rendering.md)

## Modelli - Pagine {#templates-pages}

AEM offre ora due tipi di modelli di base per la creazione di pagine:

>[!NOTE]
>
>Quando si utilizza un modello per [creare una nuova pagina](/help/sites-authoring/managing-pages.md#creating-a-new-page) , non vi è alcuna differenza visibile (per l’autore della pagina) e non vi sono indicazioni sul tipo di modello utilizzato.

### Modelli modificabili {#editable-templates}

I modelli modificabili sono ora considerati best practice per lo sviluppo con AEM.

I vantaggi dei modelli modificabili:

* Può essere [creato](/help/sites-authoring/templates.md#creating-a-new-template-template-author) e [modificato](/help/sites-authoring/templates.md#editing-a-template-structure-template-author) dagli autori.

* Sono stati introdotti per consentire di definire quanto segue per tutte le pagine create con il modello:

   * la struttura
   * il contenuto iniziale
   * criteri di contenuto

* Una volta creata la nuova pagina, viene mantenuta una connessione dinamica tra la pagina e il modello; ciò significa che le modifiche alla struttura del modello verranno applicate a tutte le pagine create con tale modello (le modifiche al contenuto iniziale non verranno applicate).
* Utilizza i criteri di contenuto (modificati dall&#39;editor modelli) per mantenere le proprietà di progettazione (non utilizza la modalità Progettazione nell&#39;editor pagina).
* Sono memorizzati in `/conf`
* Per ulteriori informazioni, consulta Modelli [](/help/sites-developing/page-templates-editable.md) modificabili.

>[!NOTE]
>
>È disponibile un articolo della community AEM che spiega come sviluppare un sito Experience Manager con Modelli modificabili. Consultate [Creazione di un sito Web Adobe Experience Manager 6.5 tramite Modelli](https://helpx.adobe.com/experience-manager/using/first_aem64_website.html)modificabili.

### Modelli statici {#static-templates}

Modelli statici:

* Devono essere definiti e configurati dai tuoi sviluppatori.
* Questo era il sistema di modelli originale di AEM ed è disponibile per molte versioni.
* Un modello statico è una gerarchia di nodi con la stessa struttura della pagina da creare, ma senza alcun contenuto effettivo.
* Vengono copiate per creare la nuova pagina, dopo di essa non esiste alcuna connessione dinamica.
* Uses [Design Mode](/help/sites-authoring/default-components-designmode.md) to persist design properties.
* Sono memorizzati in `/apps`
* Per ulteriori informazioni, consulta Modelli [](/help/sites-developing/page-templates-static.md) statici.

>[!NOTE]
>
>A partire da AEM 6.5, l’utilizzo di Modelli statici non è considerato una best practice. Utilizzate invece Modelli modificabili.
>
>[Gli strumenti di modernizzazione](modernization-tools.md) AEM consentono di migrare da modelli statici a modelli modificabili.

### Disponibilità del modello {#template-availability}

>[!CAUTION]
>
>AEM offre più proprietà per controllare i modelli consentiti in **Siti**. Tuttavia, combinarle può portare a regole molto complesse che sono difficili da monitorare e gestire.
>
>Adobe consiglia pertanto di iniziare in modo semplice definendo:
>
>* solo la `cq:allowedTemplates` proprietà
   >
   >
* solo nella directory principale del sito
>
>
Ad esempio, consulta We.Retail: `/content/we-retail/jcr:content`
>
>Le proprietà `allowedPaths`, `allowedParents`e `allowedChildren` possono essere inserite anche nei modelli per definire regole più sofisticate. Tuttavia, quando possibile, è *molto* più semplice definire ulteriori `cq:allowedTemplates` proprietà nelle sottosezioni del sito, se è necessario limitare ulteriormente i modelli consentiti.
>
>Un ulteriore vantaggio è rappresentato dal fatto che le `cq:allowedTemplates` proprietà possono essere aggiornate da un autore nella scheda **Avanzate** delle Proprietà **di** pagina. Le altre proprietà del modello non possono essere aggiornate utilizzando l&#39;interfaccia (standard), pertanto per ogni modifica è necessario che uno sviluppatore mantenga le regole e implementi il codice.

Quando si crea una nuova pagina nell’interfaccia di amministrazione del sito, l’elenco dei modelli disponibili dipende dalla posizione della nuova pagina e dalle limitazioni alla posizione specificate in ciascun modello.

Le proprietà seguenti determinano se un modello `T` può essere utilizzato per inserire una nuova pagina come figlio di una pagina `P`. Ciascuna di queste proprietà è una stringa con più valori contenente zero o più espressioni regolari utilizzate per la corrispondenza con i percorsi:

* La `cq:allowedTemplates` proprietà del `jcr:content` nodo secondario di `P` o di un predecessore di `P`.

* La `allowedPaths` proprietà di `T`.

* La `allowedParents` proprietà di `T`.

* La `allowedChildren` proprietà del modello di `P`.

La valutazione funziona come segue:

* La prima `cq:allowedTemplates` proprietà non vuota trovata durante l&#39;ascendente della gerarchia di pagina che inizia con `P` viene confrontata con il percorso di `T`. Se nessuno dei valori corrisponde, `T` viene rifiutato.

* Se `T` esiste una `allowedPaths` proprietà non vuota, ma nessuno dei valori corrisponde al percorso di `P`, `T` viene rifiutato.

* Se entrambe le proprietà di cui sopra sono vuote o inesistenti, `T` viene rifiutato a meno che non appartengano alla stessa applicazione di `P`. `T` appartiene alla stessa applicazione come `P` if e solo se il nome del secondo livello del percorso `T` è uguale al nome del secondo livello del percorso di `P`. Ad esempio, il modello `/apps/geometrixx/templates/foo` appartiene alla stessa applicazione della pagina `/content/geometrixx`.

* Se `T` esiste una `allowedParents` proprietà non vuota, ma nessuno dei valori corrisponde al percorso di `P`, `T` viene rifiutato.

* Se il modello di `P` dispone di una `allowedChildren` proprietà non vuota, ma nessuno dei valori corrisponde al percorso di `T`, `T` viene rifiutato.

* In tutti gli altri casi, `T` è consentito.

Il diagramma seguente illustra il processo di valutazione dei modelli:

![chlimage_1-176](assets/chlimage_1-176.png)

#### Limitazione dei modelli utilizzati nelle pagine figlie {#limiting-templates-used-in-child-pages}

Per limitare i modelli che possono essere utilizzati per creare pagine figlie in una determinata pagina, utilizzate la `cq:allowedTemplates` proprietà del `jcr:content` nodo della pagina per specificare l&#39;elenco di modelli da consentire come pagine figlie. Ogni valore nell&#39;elenco deve essere un percorso assoluto a un modello per una pagina figlia consentita, ad esempio `/apps/geometrixx/templates/contentpage`.

È possibile utilizzare la `cq:allowedTemplates` proprietà sul nodo del modello `jcr:content` per applicare questa configurazione a tutte le pagine create di recente che utilizzano questo modello.

Se desiderate aggiungere altri vincoli, ad esempio per quanto riguarda la gerarchia del modello, potete utilizzare le `allowedParents/allowedChildren` proprietà del modello. Potete quindi specificare esplicitamente che le pagine create da un modello T devono essere pagine padre/figlio di pagine create da un modello T.

## Modelli - Frammenti di contenuto {#templates-content-fragments}

Per ulteriori informazioni, consulta Modelli [di frammenti di](/help/sites-developing/content-fragment-templates.md) contenuto.
