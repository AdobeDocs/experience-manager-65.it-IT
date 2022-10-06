---
title: Modelli
seo-title: Templates
description: I modelli vengono utilizzati per creare una pagina che verrà utilizzata come base per la nuova pagina
seo-description: Templates are used when creating a page which will be used as the base for the new page
uuid: 6fa3dafc-dfa1-42d8-b296-d4be57449411
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 7c723773-7c23-43d7-85dc-53e54556b648
legacypath: /content/docs/en/aem/6-1/develop/the-basics/templates
exl-id: 59f01bb1-4ff1-42b6-afc9-56d448b1f803
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '963'
ht-degree: 1%

---

# Modelli{#templates}

I modelli vengono utilizzati in vari punti di AEM:

* Quando [creazione di una pagina da selezionare come modello](#templates-pages); verrà utilizzato come base per la nuova pagina. Il modello definisce la struttura della pagina risultante, gli eventuali contenuti iniziali e il [componenti](/help/sites-authoring/default-components.md) che possono essere utilizzati (proprietà di progettazione).

* Quando [creazione di un frammento di contenuto è necessario selezionare anche un modello](#templates-content-fragments). Questo modello definisce la struttura, gli elementi iniziali e le varianti.

Vengono descritti in dettaglio i seguenti modelli:

* [Modelli di pagina - Modificabili](/help/sites-developing/page-templates-editable.md)
* [Modelli di pagina - Statici](/help/sites-developing/page-templates-static.md)
* [Modelli per frammenti di contenuto](/help/sites-developing/content-fragment-templates.md)
* [Rendering di modelli adattivi](/help/sites-developing/templates-adaptive-rendering.md)

## Modelli - Pagine {#templates-pages}

AEM ora offre due tipi di modelli di base per la creazione di pagine:

>[!NOTE]
>
>Quando si utilizza un modello per [creare una nuova pagina](/help/sites-authoring/managing-pages.md#creating-a-new-page) non esiste alcuna differenza visibile (per l’autore della pagina) e non vi è alcuna indicazione del tipo di modello utilizzato.

### Modelli modificabili {#editable-templates}

I modelli modificabili sono ora considerati best practice per lo sviluppo con AEM.

Vantaggi dei modelli modificabili:

* Può essere [creato](/help/sites-authoring/templates.md#creating-a-new-template-template-author) e [modificato](/help/sites-authoring/templates.md#editing-a-template-structure-template-author) dai tuoi autori.

* Sono stati introdotti per consentire di definire quanto segue per le pagine create con il modello:

   * la struttura
   * il contenuto iniziale
   * criteri dei contenuti

* Dopo la creazione della nuova pagina viene mantenuta una connessione dinamica tra la pagina e il modello; ciò significa che le modifiche alla struttura del modello verranno applicate a tutte le pagine create con tale modello (le modifiche al contenuto iniziale non verranno applicate).
* Utilizza i criteri del contenuto (modificati dall’editor dei modelli) per mantenere le proprietà di progettazione (non utilizza la modalità Progettazione nell’editor di pagine).
* Sono memorizzati in `/conf`
* Vedi [Modelli modificabili](/help/sites-developing/page-templates-editable.md) per ulteriori informazioni.

>[!NOTE]
>
>È disponibile un articolo AEM della community che spiega come sviluppare un sito di Experience Manager con modelli modificabili, consulta [Creazione di un sito web Adobe Experience Manager 6.5 utilizzando i modelli modificabili](https://helpx.adobe.com/experience-manager/using/first_aem64_website.html).

### Modelli statici {#static-templates}

Modelli statici:

* Deve essere definito e configurato dagli sviluppatori.
* Questo era il sistema di modelli originale di AEM ed è disponibile per molte versioni.
* Un modello statico è una gerarchia di nodi con la stessa struttura della pagina da creare, ma senza alcun contenuto effettivo.
* Vengono copiati per creare la nuova pagina, dopo di ciò non esiste alcuna connessione dinamica.
* Usi [Modalità Progettazione](/help/sites-authoring/default-components-designmode.md) per mantenere le proprietà di progettazione.
* Sono memorizzati in `/apps`
* Vedi [Modelli statici](/help/sites-developing/page-templates-static.md) per ulteriori informazioni.

>[!NOTE]
>
>A partire dalla AEM 6.5, l’utilizzo di modelli statici non è considerata una best practice. In alternativa, utilizza i modelli modificabili .
>
>[Modernizzazione AEM](modernization-tools.md) Gli strumenti consentono di migrare da modelli statici a modelli modificabili.

### Disponibilità dei modelli {#template-availability}

>[!CAUTION]
>
>AEM offre più proprietà per controllare i modelli consentiti in **Sites**. Tuttavia, combinarle può portare a regole molto complesse che sono difficili da monitorare e gestire.
>
>Pertanto, Adobe consiglia di iniziare con semplicità, definendo:
>
>* solo il `cq:allowedTemplates` property
>
>* solo nella directory principale del sito
>
>Ad esempio, consulta We.Retail: `/content/we-retail/jcr:content`
>
>Proprietà `allowedPaths`, `allowedParents`e `allowedChildren` può anche essere posizionato sui modelli per definire regole più sofisticate. Tuttavia, quando possibile, è *molto* più semplice da definire `cq:allowedTemplates` nelle sottosezioni del sito se è necessario limitare ulteriormente i modelli consentiti.
>
>Un vantaggio aggiuntivo è rappresentato dal `cq:allowedTemplates` le proprietà possono essere aggiornate da un autore nel **Avanzate** della scheda **Proprietà pagina**. Le altre proprietà del modello non possono essere aggiornate utilizzando l’interfaccia utente (standard), pertanto per ogni modifica sarebbe necessario uno sviluppatore per mantenere le regole e una distribuzione del codice.

Quando crei una nuova pagina nell’interfaccia di amministrazione del sito, l’elenco dei modelli disponibili dipende dalla posizione della nuova pagina e dalle restrizioni di posizionamento specificate in ciascun modello.

Le proprietà seguenti determinano se un modello `T` può essere utilizzato per inserire una nuova pagina come pagina figlia di `P`. Ciascuna di queste proprietà è una stringa con più valori contenente zero o più espressioni regolari utilizzate per la corrispondenza con i percorsi:

* La `cq:allowedTemplates` proprietà `jcr:content` sottonodo di `P` o un antenato di `P`.

* La `allowedPaths` proprietà di `T`.

* La `allowedParents` proprietà di `T`.

* La `allowedChildren` proprietà del modello di `P`.

La valutazione funziona come segue:

* Il primo non vuoto `cq:allowedTemplates` trovato durante l&#39;ascesa della gerarchia di pagina che inizia con `P` viene confrontato con il percorso di `T`. Se nessuno dei valori corrisponde, `T` è rifiutato.

* Se `T` non è vuoto `allowedPaths` , ma nessuno dei valori corrisponde al percorso di `P`, `T` è rifiutato.

* Se entrambe le proprietà di cui sopra sono vuote o inesistenti, `T` è rifiutato a meno che non appartenga alla stessa domanda `P`. `T` appartiene alla stessa applicazione `P` se e solo se il nome del secondo livello del percorso `T` è lo stesso del nome del secondo livello del percorso `P`. Ad esempio, il modello `/apps/geometrixx/templates/foo` appartiene alla stessa applicazione della pagina `/content/geometrixx`.

* Se `T` non è vuoto `allowedParents` , ma nessuno dei valori corrisponde al percorso di `P`, `T` è rifiutato.

* Se il modello di `P` non è vuoto `allowedChildren` , ma nessuno dei valori corrisponde al percorso di `T`, `T` è rifiutato.

* In tutti gli altri casi, `T` è consentito.

Il diagramma seguente illustra il processo di valutazione del modello:

![chlimage_1-176](assets/chlimage_1-176.png)

#### Limitazione dei modelli utilizzati nelle pagine figlie {#limiting-templates-used-in-child-pages}

Per limitare i modelli che possono essere utilizzati per creare pagine figlie sotto una determinata pagina, utilizza la funzione `cq:allowedTemplates` proprietà di `jcr:content` nodo della pagina per specificare l’elenco di modelli da consentire come pagine figlie. Ogni valore nell’elenco deve essere un percorso assoluto a un modello per una pagina figlio consentita, ad esempio `/apps/geometrixx/templates/contentpage`.

È possibile utilizzare `cq:allowedTemplates` nella proprietà del modello  `jcr:content` per applicare questa configurazione a tutte le pagine appena create che utilizzano questo modello.

Se desideri aggiungere altri vincoli, ad esempio per quanto riguarda la gerarchia dei modelli, puoi utilizzare la funzione `allowedParents/allowedChildren` nel modello. È quindi possibile specificare esplicitamente che le pagine create da un modello T devono essere padre/figlio di pagine create da un modello T.

## Modelli - Frammenti di contenuto {#templates-content-fragments}

Vedi [Modelli per frammenti di contenuto](/help/sites-developing/content-fragment-templates.md) per informazioni complete.
