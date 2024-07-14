---
title: Annotazioni durante la modifica di una pagina
description: L’aggiunta di contenuto alle pagine del sito web è spesso soggetta a discussioni prima di essere effettivamente pubblicata. Per facilitare questa fase, molti componenti direttamente correlati al contenuto consentono di aggiungere un’annotazione.
page-status-flag: de-activated
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
exl-id: d60e9601-d15b-4378-a33e-e90961f63195
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '763'
ht-degree: 8%

---

# Annotazioni durante la modifica di una pagina{#annotations-when-editing-a-page}

L’aggiunta di contenuto alle pagine del sito web è spesso soggetta a discussioni prima di essere effettivamente pubblicata. Per facilitare questa fase, molti componenti direttamente correlati al contenuto (anziché, ad esempio, al layout) ti consentono di aggiungere un’annotazione.

Un’annotazione posiziona un marcatore colorato o una nota adesiva sulla pagina. può contenere commenti o domande inseriti da un utente e destinati ad altri autori o revisori.

>[!NOTE]
>
>Nella definizione di un singolo tipo di componente è possibile specificare se l’aggiunta di annotazioni è supportata o meno per le istanze del componente.

>[!NOTE]
>
>Le annotazioni create nell’interfaccia utente classica vengono visualizzate nell’interfaccia touch. Tuttavia, gli schizzi sono specifici dell’interfaccia utente e vengono visualizzati solo nell’interfaccia utente in cui sono stati creati.

>[!CAUTION]
>
>Se si elimina una risorsa (ad esempio un paragrafo), vengono anche eliminate tutte le annotazioni e gli schizzi associati ad essa, indipendentemente dalla loro posizione sulla pagina.

>[!NOTE]
>
>Se necessario, puoi anche sviluppare un flusso di lavoro per inviare una notifica quando vengono aggiunte, aggiornate o eliminate delle annotazioni.

## Annotazioni {#annotations}

A seconda della struttura del paragrafo, l’annotazione è disponibile come opzione nel menu di scelta rapida (in genere il pulsante destro del mouse quando si posiziona sul paragrafo richiesto) o come pulsante sulla barra di modifica del paragrafo.

In entrambi i casi, selezionare **Annota**. Al paragrafo viene applicata un’annotazione colorata con nota adesiva. La modalità Modifica è attiva immediatamente e consente di aggiungere testo direttamente:

![chlimage_1-137](assets/chlimage_1-137.png)

È possibile spostare l’annotazione in una nuova posizione sulla pagina. Fai clic sull’area del bordo superiore, quindi tieni premuto e trascina simultaneamente l’annotazione nella nuova posizione. Questo può essere in qualsiasi punto della pagina, anche se spesso è utile mantenerlo connesso al paragrafo in qualche modo.

Le annotazioni (inclusi gli schizzi correlati) sono incluse anche nelle azioni di copia, taglio o eliminazione eseguite sul paragrafo al quale sono associate. Per le azioni di copia o di taglio, la posizione dell&#39;annotazione (e degli schizzi correlati) rimane invariata rispetto al paragrafo di origine.

È inoltre possibile aumentare o diminuire le dimensioni dell’annotazione trascinando l’angolo in basso a destra.

Ai fini del tracciamento, la linea del piè di pagina indica l’utente che ha creato l’annotazione e la data. Gli autori successivi possono modificare la stessa annotazione (il piè di pagina viene aggiornato) o crearne un’altra per lo stesso paragrafo.

La conferma viene richiesta quando si seleziona di eliminare l’annotazione (l’eliminazione di un’annotazione comporta anche l’eliminazione di tutti gli schizzi associati all’annotazione).

Le tre icone in alto a sinistra consentono di ridurre a icona l’annotazione (insieme a eventuali schizzi correlati), modificare il colore e aggiungere schizzi.

>[!NOTE]
>
>Le annotazioni sono visibili solo in modalità di modifica nell’ambiente di authoring.
>
>Non sono visibili in un ambiente di pubblicazione, né nelle modalità Anteprima o Progettazione disponibili in un ambiente di authoring.

>[!NOTE]
>
>Non è possibile aggiungere annotazioni a una pagina bloccata da un altro utente.

## Schizzi di annotazione {#annotation-sketches}

>[!NOTE]
>
>Gli schizzi non sono disponibili in Internet Explorer, pertanto:
>
>* l’icona non viene visualizzata.
>* gli schizzi esistenti, creati in un altro browser, non verranno visualizzati.
>

Gli schizzi sono una caratteristica delle annotazioni che consente di creare semplici elementi grafici a linee in qualsiasi punto della finestra del browser (parte visibile):

![chlimage_1-138](assets/chlimage_1-138.png)

* Il cursore si trasforma in un reticolo incrociato quando siete in modalità sketch. È possibile disegnare più linee distinte.
* La linea dello schizzo riflette il colore dell’annotazione e può essere:

   * mano libera

     la modalità predefinita; terminare rilasciando il pulsante del mouse.

   * dritto:

     tenere premuto `ALT` e fare clic sui punti iniziale e finale; terminare con un doppio clic.

* Dopo aver chiuso la modalità di sketch, potete fare clic su una linea di sketch per selezionarla.
* Spostate uno sketch selezionandolo, quindi trascinandolo nella posizione desiderata.
* Uno schizzo sovrappone il contenuto. Ciò significa che all&#39;interno dei quattro angoli dello sketch non è possibile fare clic sul paragrafo sottostante. Ad esempio, se devi modificare o accedere a un collegamento. Se si verifica un problema (ad esempio, se uno schizzo copre una vasta area della pagina), minimizza l’annotazione appropriata, in quanto questa operazione ridurrà anche tutti gli schizzi correlati, consentendo l’accesso all’area sottostante.
* Per eliminare un singolo schizzo: seleziona lo schizzo richiesto, quindi premi il tasto **Elimina** (**fn**-**backspace** in un Mac).

* Se si sposta o si copia un paragrafo, verranno spostate o copiate anche tutte le annotazioni correlate e i relativi schizzi, mantenendo la stessa posizione rispetto al paragrafo.
* Se eliminate un’annotazione, verranno eliminati anche tutti gli schizzi associati ad essa.
