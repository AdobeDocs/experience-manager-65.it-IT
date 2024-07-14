---
title: Modelli
description: I modelli vengono utilizzati durante la creazione di una pagina utilizzata come base per la nuova pagina.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
legacypath: /content/docs/en/aem/6-1/develop/the-basics/templates
exl-id: 59f01bb1-4ff1-42b6-afc9-56d448b1f803
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '924'
ht-degree: 0%

---

# Modelli{#templates}

I modelli vengono utilizzati in vari punti dell’AEM:

* [Quando si crea una pagina, si seleziona un modello](#templates-pages). Questo modello viene utilizzato come base per la nuova pagina. Il modello definisce la struttura della pagina, il contenuto iniziale e i [componenti](/help/sites-authoring/default-components.md) utilizzabili (proprietà di progettazione).

* [Quando si crea un frammento di contenuto, si seleziona anche un modello](#templates-content-fragments). Questo modello definisce la struttura, gli elementi iniziali e le varianti.

Sono trattati in dettaglio i seguenti modelli:

* [Modelli di pagina - Modificabili](/help/sites-developing/page-templates-editable.md)
* [Modelli di pagina - Statici](/help/sites-developing/page-templates-static.md)
* [Modelli per frammenti di contenuto](/help/sites-developing/content-fragment-templates.md)
* [Rendering modello adattivo](/help/sites-developing/templates-adaptive-rendering.md)

## Modelli - Pagine {#templates-pages}

AEM ora offre due tipi di modelli di base per la creazione di pagine:

>[!NOTE]
>
>Quando si utilizza un modello per [creare una pagina](/help/sites-authoring/managing-pages.md#creating-a-new-page), non vi è alcuna differenza visibile (per l&#39;autore della pagina) né alcuna indicazione del tipo di modello utilizzato.

### Modelli modificabili {#editable-templates}

I modelli modificabili sono ora considerati best practice per lo sviluppo con AEM.

Vantaggi dei modelli modificabili:

* I tuoi autori possono [creare](/help/sites-authoring/templates.md#creating-a-new-template-template-author) e [modificare](/help/sites-authoring/templates.md#editing-a-template-structure-template-author).

* Sono state introdotte per consentire di definire quanto segue per tutte le pagine create con il modello:

   * la struttura
   * il contenuto iniziale
   * criteri per contenuti

* Dopo la creazione della nuova pagina, viene mantenuta una connessione dinamica tra la pagina e il modello. Ciò significa che le modifiche alla struttura del modello vengono applicate a tutte le pagine create con tale modello, mentre le modifiche al contenuto iniziale non vengono applicate.
* Utilizza i criteri per contenuto (modificati dall’editor modelli) per mantenere le proprietà di progettazione (non utilizza la modalità Progettazione nell’editor pagina).
* Sono archiviati in `/conf`
* Per ulteriori informazioni, vedere [Modelli modificabili](/help/sites-developing/page-templates-editable.md).

>[!NOTE]
>
>Consulta [Utilizzo di modelli di pagina modificabili per sviluppare un sito di Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/page-authoring/template-editor-feature-video-use.html?lang=it).

### Modelli statici {#static-templates}

Modelli statici:

* Deve essere definito e configurato dagli sviluppatori.
* Il sistema di modelli originale dell’AEM che è stato reso disponibile per molte versioni.
* Un modello statico è una gerarchia di nodi con la stessa struttura della pagina da creare, ma senza alcun contenuto effettivo.
* Vengono copiati per creare la pagina, ma in seguito non esiste alcuna connessione dinamica.
* Utilizza la [modalità progettazione](/help/sites-authoring/default-components-designmode.md) per mantenere le proprietà di progettazione.
* Sono archiviati in `/apps`
* Per ulteriori informazioni, vedere [Modelli statici](/help/sites-developing/page-templates-static.md).

>[!NOTE]
>
>A partire dalla versione 6.5 dell’AEM, l’uso di modelli statici non è considerato una best practice. Utilizza invece i modelli modificabili.
>
>Gli strumenti di [modernizzazione AEM](modernization-tools.md) possono aiutarti a migrare da modelli statici a modificabili.

### Disponibilità dei modelli {#template-availability}

>[!CAUTION]
>
>AEM offre più proprietà per controllare i modelli consentiti in **Sites**. Tuttavia, la loro combinazione può portare a regole complesse difficili da tracciare e gestire.
>
>Pertanto, l’Adobe consiglia di iniziare da semplice, definendo:
>
>* solo la proprietà `cq:allowedTemplates`
>
>* solo nella directory principale del sito
>
>Ad esempio, vedere We.Retail: `/content/we-retail/jcr:content`
>
>Le proprietà `allowedPaths`, `allowedParents` e `allowedChildren` possono anche essere posizionate nei modelli per definire regole più sofisticate. Tuttavia, quando possibile, è *molto* più semplice definire ulteriori `cq:allowedTemplates` proprietà nelle sottosezioni del sito se è necessario limitare ulteriormente i modelli consentiti.
>
>Un ulteriore vantaggio consiste nel fatto che le proprietà `cq:allowedTemplates` possono essere aggiornate da un autore nella scheda **Avanzate** delle **Proprietà pagina**. Le altre proprietà del modello non possono essere aggiornate utilizzando l’interfaccia utente (standard), pertanto avrebbe bisogno di uno sviluppatore per mantenere le regole e una distribuzione del codice per ogni modifica.

Durante la creazione di una pagina nell’interfaccia di amministrazione del sito, l’elenco dei modelli disponibili dipende dalla posizione della nuova pagina e dalle restrizioni sul posizionamento specificate in ciascun modello.

Le seguenti proprietà determinano se un modello `T` viene utilizzato per posizionare una nuova pagina come elemento figlio della pagina `P`. Ciascuna di queste proprietà è una stringa con più valori contenente zero o più espressioni regolari utilizzate per la corrispondenza con i percorsi:

* Proprietà `cq:allowedTemplates` del sottonodo `jcr:content` di `P` o predecessore di `P`.

* La proprietà `allowedPaths` di `T`.

* La proprietà `allowedParents` di `T`.

* La proprietà `allowedChildren` del modello di `P`.

La valutazione funziona come segue:

* La prima proprietà `cq:allowedTemplates` non vuota trovata durante l&#39;ascesa della gerarchia di pagine a partire da `P` viene confrontata con il percorso di `T`. Se nessuno dei valori corrisponde, `T` viene rifiutato.

* Se `T` ha una proprietà `allowedPaths` non vuota, ma nessuno dei valori corrisponde al percorso di `P`, `T` verrà rifiutato.

* Se entrambe le proprietà di cui sopra sono vuote o inesistenti, `T` verrà rifiutato a meno che non appartenga alla stessa applicazione di `P`. `T` appartiene alla stessa applicazione di `P` se e solo se il nome del secondo livello del percorso di `T` è uguale al nome del secondo livello del percorso di `P`. Ad esempio, il modello `/apps/geometrixx/templates/foo` appartiene alla stessa applicazione della pagina `/content/geometrixx`.

* Se `T` ha una proprietà `allowedParents` non vuota, ma nessuno dei valori corrisponde al percorso di `P`, `T` verrà rifiutato.

* Se il modello di `P` ha una proprietà `allowedChildren` non vuota, ma nessuno dei valori corrisponde al percorso di `T`, `T` verrà rifiutato.

* In tutti gli altri casi, `T` è consentito.

Il diagramma seguente illustra il processo di valutazione del modello:

![chlimage_1-176](assets/chlimage_1-176.png)

#### Limitazione dei modelli utilizzati nelle pagine figlie {#limiting-templates-used-in-child-pages}

Per limitare i modelli utilizzabili per creare pagine figlie in una determinata pagina, utilizzare la proprietà `cq:allowedTemplates` di `jcr:content` nodo della pagina per specificare l&#39;elenco di modelli consentiti come pagine figlie. Ogni valore nell&#39;elenco deve essere il percorso assoluto di un modello per una pagina figlio consentita, ad esempio `/apps/geometrixx/templates/contentpage`.

È possibile utilizzare la proprietà `cq:allowedTemplates` nel nodo `jcr:content` del modello per applicare questa configurazione a tutte le pagine appena create che utilizzano questo modello.

Per aggiungere altri vincoli, ad esempio relativi alla gerarchia dei modelli, è possibile utilizzare le proprietà `allowedParents/allowedChildren` nel modello. È quindi possibile specificare esplicitamente che le pagine create da un modello devono essere padri/figli di pagine create da un modello T.

## Modelli - Frammenti di contenuto {#templates-content-fragments}

Consulta [Modelli per frammenti di contenuto](/help/sites-developing/content-fragment-templates.md).
