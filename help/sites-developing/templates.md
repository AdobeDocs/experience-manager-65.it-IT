---
title: Modelli
description: I modelli vengono utilizzati durante la creazione di una pagina utilizzata come base per la nuova pagina.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
legacypath: /content/docs/en/aem/6-1/develop/the-basics/templates
exl-id: 59f01bb1-4ff1-42b6-afc9-56d448b1f803
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '924'
ht-degree: 0%

---

# Modelli{#templates}

I modelli vengono utilizzati in vari punti dell’AEM:

* [Quando crei una pagina, selezioni un modello](#templates-pages). Questo modello viene utilizzato come base per la nuova pagina. Il modello definisce la struttura della pagina, l’eventuale contenuto iniziale e il [componenti](/help/sites-authoring/default-components.md) utilizzabili (proprietà di progettazione).

* [Quando crei un frammento di contenuto, selezioni anche un modello](#templates-content-fragments). Questo modello definisce la struttura, gli elementi iniziali e le varianti.

Sono trattati in dettaglio i seguenti modelli:

* [Modelli di pagina - Modificabili](/help/sites-developing/page-templates-editable.md)
* [Modelli di pagina - Statici](/help/sites-developing/page-templates-static.md)
* [Modelli per frammenti di contenuto](/help/sites-developing/content-fragment-templates.md)
* [Rendering modello adattivo](/help/sites-developing/templates-adaptive-rendering.md)

## Modelli - Pagine {#templates-pages}

AEM ora offre due tipi di modelli di base per la creazione di pagine:

>[!NOTE]
>
>Quando si utilizza un modello per [creare una pagina](/help/sites-authoring/managing-pages.md#creating-a-new-page), non ci sono differenze visibili (per l’autore della pagina) e nessuna indicazione del tipo di modello utilizzato.

### Modelli modificabili {#editable-templates}

I modelli modificabili sono ora considerati best practice per lo sviluppo con AEM.

Vantaggi dei modelli modificabili:

* Può essere [creato](/help/sites-authoring/templates.md#creating-a-new-template-template-author) e [modificato](/help/sites-authoring/templates.md#editing-a-template-structure-template-author) dai tuoi autori.

* Sono state introdotte per consentire di definire quanto segue per tutte le pagine create con il modello:

   * la struttura
   * il contenuto iniziale
   * criteri per contenuti

* Dopo la creazione della nuova pagina, viene mantenuta una connessione dinamica tra la pagina e il modello. Ciò significa che le modifiche alla struttura del modello vengono applicate a tutte le pagine create con tale modello, mentre le modifiche al contenuto iniziale non vengono applicate.
* Utilizza i criteri per contenuto (modificati dall’editor modelli) per mantenere le proprietà di progettazione (non utilizza la modalità Progettazione nell’editor pagina).
* Sono archiviati in `/conf`
* Consulta [Modelli modificabili](/help/sites-developing/page-templates-editable.md) per ulteriori informazioni.

>[!NOTE]
>
>Consulta [Utilizzo di modelli di pagina modificabili per sviluppare un sito di Experienci Manager](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/page-authoring/template-editor-feature-video-use.html?lang=en).

### Modelli statici {#static-templates}

Modelli statici:

* Deve essere definito e configurato dagli sviluppatori.
* Il sistema di modelli originale dell’AEM che è stato reso disponibile per molte versioni.
* Un modello statico è una gerarchia di nodi con la stessa struttura della pagina da creare, ma senza alcun contenuto effettivo.
* Vengono copiati per creare la pagina, ma in seguito non esiste alcuna connessione dinamica.
* Usa [Modalità Progettazione](/help/sites-authoring/default-components-designmode.md) per mantenere le proprietà di progettazione.
* Sono archiviati in `/apps`
* Consulta [Modelli statici](/help/sites-developing/page-templates-static.md) per ulteriori informazioni.

>[!NOTE]
>
>A partire dalla versione 6.5 dell’AEM, l’uso di modelli statici non è considerato una best practice. Utilizza invece i modelli modificabili.
>
>[Modernizzazione dell’AEM](modernization-tools.md) Gli strumenti consentono di passare da modelli statici a modificabili.

### Disponibilità dei modelli {#template-availability}

>[!CAUTION]
>
>L’AEM offre più proprietà per controllare i modelli consentiti in **Sites**. Tuttavia, la loro combinazione può portare a regole complesse difficili da tracciare e gestire.
>
>Pertanto, l’Adobe consiglia di iniziare da semplice, definendo:
>
>* solo il `cq:allowedTemplates` proprietà
>
>* solo nella directory principale del sito
>
>Ad esempio, vedi We.Retail: `/content/we-retail/jcr:content`
>
>Le proprietà `allowedPaths`, `allowedParents`, e `allowedChildren` può essere posizionato anche sui modelli per definire regole più sofisticate. Tuttavia, quando possibile, è *molto* definizione più semplice `cq:allowedTemplates` proprietà nelle sottosezioni del sito, se è necessario limitare ulteriormente i modelli consentiti.
>
>Un ulteriore vantaggio è che il `cq:allowedTemplates` Le proprietà possono essere aggiornate da un autore in **Avanzate** scheda di **Proprietà pagina**. Le altre proprietà del modello non possono essere aggiornate utilizzando l’interfaccia utente (standard), pertanto avrebbe bisogno di uno sviluppatore per mantenere le regole e una distribuzione del codice per ogni modifica.

Durante la creazione di una pagina nell’interfaccia di amministrazione del sito, l’elenco dei modelli disponibili dipende dalla posizione della nuova pagina e dalle restrizioni sul posizionamento specificate in ciascun modello.

Le seguenti proprietà determinano se un modello `T` viene utilizzato per inserire una nuova pagina come pagina figlia di `P`. Ciascuna di queste proprietà è una stringa con più valori contenente zero o più espressioni regolari utilizzate per la corrispondenza con i percorsi:

* Il `cq:allowedTemplates` proprietà del `jcr:content` sottonodo di `P` o un predecessore di `P`.

* Il `allowedPaths` proprietà di `T`.

* Il `allowedParents` proprietà di `T`.

* Il `allowedChildren` proprietà del modello di `P`.

La valutazione funziona come segue:

* Il primo non vuoto `cq:allowedTemplates` è stata trovata una proprietà durante l’ascensione della gerarchia delle pagine che inizia con `P` corrisponde al percorso di `T`. Se nessuno dei valori corrisponde, `T` è stato rifiutato.

* Se `T` ha un valore non vuoto `allowedPaths` , ma nessuno dei valori corrisponde al percorso di `P`, `T` è stato rifiutato.

* Se entrambe le proprietà di cui sopra sono vuote o inesistenti, `T` viene rifiutato a meno che non appartenga alla stessa applicazione di `P`. `T` appartiene alla stessa applicazione di `P` se e solo se il nome del secondo livello del percorso di `T` è uguale al nome del secondo livello del percorso di `P`. Ad esempio, il modello `/apps/geometrixx/templates/foo` appartiene alla stessa applicazione della pagina `/content/geometrixx`.

* Se `T` ha un valore non vuoto `allowedParents` , ma nessuno dei valori corrisponde al percorso di `P`, `T` è stato rifiutato.

* Se il modello di `P` ha un valore non vuoto `allowedChildren` , ma nessuno dei valori corrisponde al percorso di `T`, `T` è stato rifiutato.

* In tutti gli altri casi: `T` è consentito.

Il diagramma seguente illustra il processo di valutazione del modello:

![chlimage_1-176](assets/chlimage_1-176.png)

#### Limitazione dei modelli utilizzati nelle pagine figlie {#limiting-templates-used-in-child-pages}

Per limitare i modelli utilizzabili per creare pagine figlie in una determinata pagina, utilizza `cq:allowedTemplates` proprietà di `jcr:content` nodo della pagina per specificare l’elenco di modelli consentiti come pagine figlie. Ogni valore nell’elenco deve essere il percorso assoluto di un modello per una pagina figlia consentita, ad esempio, `/apps/geometrixx/templates/contentpage`.

È possibile utilizzare `cq:allowedTemplates` proprietà del modello  `jcr:content` per applicare questa configurazione a tutte le nuove pagine create che utilizzano questo modello.

Per aggiungere altri vincoli, ad esempio relativi alla gerarchia dei modelli, è possibile utilizzare `allowedParents/allowedChildren` proprietà nel modello. È quindi possibile specificare esplicitamente che le pagine create da un modello devono essere padri/figli di pagine create da un modello T.

## Modelli - Frammenti di contenuto {#templates-content-fragments}

Consulta [Modelli per frammenti di contenuto](/help/sites-developing/content-fragment-templates.md).
