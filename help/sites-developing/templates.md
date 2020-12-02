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
workflow-type: tm+mt
source-wordcount: '982'
ht-degree: 1%

---


# Modelli{#templates}

I modelli vengono utilizzati in vari punti della AEM:

* Quando si crea una pagina [è necessario selezionare un modello](#templates-pages); verrà utilizzato come base per la nuova pagina. Il modello definisce la struttura della pagina risultante, qualsiasi contenuto iniziale e i [componenti](/help/sites-authoring/default-components.md) utilizzabili (proprietà di progettazione).

* Quando si crea un frammento di contenuto [è necessario selezionare anche un modello](#templates-content-fragments). Questo modello definisce la struttura, gli elementi iniziali e le varianti.

Vengono descritti in dettaglio i seguenti modelli:

* [Modelli di pagina - Modificabili](/help/sites-developing/page-templates-editable.md)
* [Modelli di pagina - Statici](/help/sites-developing/page-templates-static.md)
* [Modelli di frammento di contenuto](/help/sites-developing/content-fragment-templates.md)
* [Rendering dei modelli adattivi](/help/sites-developing/templates-adaptive-rendering.md)

## Modelli - Pagine {#templates-pages}

AEM ora offre due tipi di modelli di base per la creazione di pagine:

>[!NOTE]
>
>Quando si utilizza un modello per [creare una nuova pagina](/help/sites-authoring/managing-pages.md#creating-a-new-page) non esiste alcuna differenza visibile (per l&#39;autore della pagina) né alcuna indicazione del tipo di modello utilizzato.

### Modelli modificabili {#editable-templates}

I modelli modificabili sono ora considerati best practice per lo sviluppo con AEM.

I vantaggi dei modelli modificabili:

* Gli autori possono creare [e ](/help/sites-authoring/templates.md#creating-a-new-template-template-author) e [modificare](/help/sites-authoring/templates.md#editing-a-template-structure-template-author).

* Sono stati introdotti per consentire di definire quanto segue per tutte le pagine create con il modello:

   * la struttura
   * il contenuto iniziale
   * criteri di contenuto

* Una volta creata la nuova pagina, viene mantenuta una connessione dinamica tra la pagina e il modello; ciò significa che le modifiche alla struttura del modello verranno applicate a tutte le pagine create con tale modello (le modifiche al contenuto iniziale non verranno applicate).
* Utilizza i criteri di contenuto (modificati dall&#39;editor modelli) per mantenere le proprietà di progettazione (non utilizza la modalità Progettazione nell&#39;editor pagina).
* Sono memorizzati in `/conf`
* Per ulteriori informazioni, vedere [Modelli modificabili](/help/sites-developing/page-templates-editable.md).

>[!NOTE]
>
>È disponibile un articolo AEM della community che spiega come sviluppare un sito  Experience Manager con Modelli modificabili. Consultate [Creazione di un sito Web Adobe Experience Manager 6.5 tramite Modelli modificabili](https://helpx.adobe.com/experience-manager/using/first_aem64_website.html).

### Modelli statici {#static-templates}

Modelli statici:

* Devono essere definiti e configurati dai tuoi sviluppatori.
* Questo era il modello originale di AEM ed è stato disponibile per molte versioni.
* Un modello statico è una gerarchia di nodi con la stessa struttura della pagina da creare, ma senza alcun contenuto effettivo.
* Vengono copiate per creare la nuova pagina, dopo di essa non esiste alcuna connessione dinamica.
* Utilizza [Modalità progettazione](/help/sites-authoring/default-components-designmode.md) per mantenere le proprietà di progettazione.
* Sono memorizzati in `/apps`
* Per ulteriori informazioni, vedere [Modelli statici](/help/sites-developing/page-templates-static.md).

>[!NOTE]
>
>A partire dal AEM 6.5, l&#39;uso di Modelli statici non è considerato una procedura ottimale. Utilizzate invece Modelli modificabili.
>
>[AEM strumenti ](modernization-tools.md) Modernizzazione è possibile migrare da modelli statici a modelli modificabili.

### Disponibilità del modello {#template-availability}

>[!CAUTION]
>
>AEM offre più proprietà per controllare i modelli consentiti in **Sites**. Tuttavia, combinarle può portare a regole molto complesse che sono difficili da monitorare e gestire.
>
>Pertanto,  Adobe consiglia di iniziare in modo semplice, definendo:
>
>* solo la proprietà `cq:allowedTemplates`
   >
   >
* solo nella directory principale del sito
>
>
Ad esempio, consulta We.Retail: `/content/we-retail/jcr:content`
>
>Le proprietà `allowedPaths`, `allowedParents` e `allowedChildren` possono essere inserite anche nei modelli per definire regole più sofisticate. Tuttavia, quando possibile, è *molto* più semplice definire ulteriori proprietà `cq:allowedTemplates` nelle sottosezioni del sito, se è necessario limitare ulteriormente i modelli consentiti.
>
>Un ulteriore vantaggio è rappresentato dal fatto che le proprietà `cq:allowedTemplates` possono essere aggiornate da un autore nella scheda **Advanced** della scheda **Proprietà pagina**. Le altre proprietà del modello non possono essere aggiornate utilizzando l&#39;interfaccia (standard), pertanto per ogni modifica è necessario che uno sviluppatore mantenga le regole e implementi il codice.

Quando si crea una nuova pagina nell’interfaccia di amministrazione del sito, l’elenco dei modelli disponibili dipende dalla posizione della nuova pagina e dalle limitazioni alla posizione specificate in ciascun modello.

Le proprietà seguenti determinano se un modello `T` può essere utilizzato per inserire una nuova pagina come elemento secondario di pagina `P`. Ciascuna di queste proprietà è una stringa con più valori che contiene zero o più espressioni regolari utilizzate per la corrispondenza con i percorsi:

* La proprietà `cq:allowedTemplates` del nodo secondario `jcr:content` di `P` o di un predecessore di `P`.

* La proprietà `allowedPaths` di `T`.

* La proprietà `allowedParents` di `T`.

* La proprietà `allowedChildren` del modello di `P`.

La valutazione funziona come segue:

* La prima proprietà `cq:allowedTemplates` non vuota trovata durante l&#39;ascendente della gerarchia di pagina che inizia con `P` viene confrontata con il percorso di `T`. Se nessuno dei valori corrisponde, `T` viene rifiutato.

* Se `T` dispone di una proprietà `allowedPaths` non vuota, ma nessuno dei valori corrisponde al percorso di `P`, `T` viene rifiutato.

* Se entrambe le proprietà di cui sopra sono vuote o inesistenti, `T` viene rifiutato a meno che non appartengano alla stessa applicazione di `P`. `T` appartiene alla stessa applicazione  `P` if e solo se il nome del secondo livello del percorso  `T` è lo stesso del nome del secondo livello del percorso di  `P`. Ad esempio, il modello `/apps/geometrixx/templates/foo` appartiene alla stessa applicazione della pagina `/content/geometrixx`.

* Se `T` ha una proprietà `allowedParents` non vuota, ma nessuno dei valori corrisponde al percorso di `P`, `T` viene rifiutato.

* Se il modello di `P` ha una proprietà `allowedChildren` non vuota, ma nessuno dei valori corrisponde al percorso di `T`, `T` viene rifiutato.

* In tutti gli altri casi, `T` è consentito.

Il diagramma seguente illustra il processo di valutazione dei modelli:

![chlimage_1-176](assets/chlimage_1-176.png)

#### Limitazione dei modelli utilizzati nelle pagine figlie {#limiting-templates-used-in-child-pages}

Per limitare i modelli che possono essere utilizzati per creare pagine figlie in una determinata pagina, utilizzate la proprietà `cq:allowedTemplates` del nodo `jcr:content` della pagina per specificare l&#39;elenco di modelli da consentire come pagine figlie. Ogni valore nell&#39;elenco deve essere un percorso assoluto a un modello per una pagina figlia consentita, ad esempio `/apps/geometrixx/templates/contentpage`.

È possibile utilizzare la proprietà `cq:allowedTemplates` nel nodo `jcr:content` del modello per applicare questa configurazione a tutte le pagine create di recente che utilizzano questo modello.

Se desiderate aggiungere altri vincoli, ad esempio per quanto riguarda la gerarchia del modello, potete utilizzare le proprietà `allowedParents/allowedChildren` del modello. Potete quindi specificare esplicitamente che le pagine create da un modello T devono essere pagine padre/figlio di pagine create da un modello T.

## Modelli - Frammenti di contenuto {#templates-content-fragments}

Per ulteriori informazioni, vedere [Modelli di frammento di contenuto](/help/sites-developing/content-fragment-templates.md).
