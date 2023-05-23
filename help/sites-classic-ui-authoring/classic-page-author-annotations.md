---
title: Annotazioni durante la modifica di una pagina
description: L’aggiunta di contenuto alle pagine del sito web è spesso soggetta a discussioni prima che questo venga effettivamente pubblicato. Per facilitare questa fase, molti componenti direttamente correlati al contenuto consentono di aggiungere un’annotazione.
page-status-flag: de-activated
uuid: d8d6ba76-f2aa-4044-98bf-5d506742d90d
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 9bee0197-f275-49cc-922d-62cba826c4e5
exl-id: d60e9601-d15b-4378-a33e-e90961f63195
source-git-commit: e1a0b114ce16d0e7f6a464e9d30b8f111297bcc6
workflow-type: tm+mt
source-wordcount: '782'
ht-degree: 7%

---

# Annotazioni durante la modifica di una pagina{#annotations-when-editing-a-page}

L’aggiunta di contenuto alle pagine del sito web è spesso soggetta a discussioni prima che questo venga effettivamente pubblicato. Per facilitare questa fase, molti componenti direttamente correlati al contenuto (anziché, ad esempio, al layout) consentono di aggiungere un’annotazione.

Un’annotazione posiziona un marcatore colorato o una nota adesiva sulla pagina. può contenere commenti o domande inseriti da un utente e destinati ad altri autori o revisori.

>[!NOTE]
>
>Nella definizione di un singolo tipo di componente è possibile specificare se l’aggiunta di annotazioni è supportata o meno per le istanze del componente.

>[!NOTE]
>
>Le annotazioni create nell’interfaccia classica vengono visualizzate anche nell’interfaccia touch. Tuttavia, gli schizzi sono specifici dell’interfaccia utente e vengono visualizzati solo nell’interfaccia utente in cui sono stati creati.

>[!CAUTION]
>
>Se si elimina una risorsa (ad esempio un paragrafo), vengono anche eliminate tutte le annotazioni e gli schizzi associati ad essa, indipendentemente dalla loro posizione sulla pagina.

>[!NOTE]
>
>A seconda delle tue esigenze, puoi anche sviluppare un flusso di lavoro per inviare una notifica quando vengono aggiunte, aggiornate o eliminate delle annotazioni.

## Annotazioni {#annotations}

A seconda della struttura del paragrafo, l’annotazione è disponibile come opzione nel menu di scelta rapida (in genere il pulsante destro del mouse quando si posiziona sul paragrafo richiesto) o come pulsante sulla barra di modifica del paragrafo.

In entrambi i casi, seleziona **Annota**. Al paragrafo verrà applicata un’annotazione colorata con nota adesiva, che si trova immediatamente in modalità Modifica e consente di aggiungere direttamente il testo:

![chlimage_1-137](assets/chlimage_1-137.png)

È possibile spostare l’annotazione in una nuova posizione sulla pagina. Fai clic sull’area del bordo superiore, quindi tieni premuto e trascina simultaneamente l’annotazione nella nuova posizione. Questo può essere in qualsiasi punto della pagina, anche se in genere ha senso mantenerlo connesso al paragrafo in qualche modo.

Le annotazioni (inclusi gli schizzi correlati) sono incluse anche nelle azioni di copia, taglio o cancellazione eseguite sul paragrafo a cui sono associate; per le azioni di copia o taglio, la posizione dell&#39;annotazione (e degli schizzi correlati) rimane invariata rispetto al paragrafo di origine.

È inoltre possibile aumentare o diminuire le dimensioni dell’annotazione trascinando l’angolo in basso a destra.

Ai fini del tracciamento, la riga del piè di pagina indica l’utente che ha creato l’annotazione e la data. Gli autori successivi possono modificare la stessa annotazione (il piè di pagina verrà aggiornato) o creare una nuova annotazione per lo stesso paragrafo.

La conferma viene richiesta quando si seleziona di eliminare l’annotazione (se si elimina un’annotazione, vengono eliminati anche gli schizzi associati all’annotazione).

Le tre icone in alto a sinistra consentono di ridurre al minimo l’annotazione (insieme a eventuali schizzi correlati), modificare il colore e aggiungere gli schizzi.

>[!NOTE]
>
>Le annotazioni sono visibili solo in modalità di modifica nell’ambiente di authoring.
>
>Non sono visibili in un ambiente di pubblicazione, né nelle modalità Anteprima o Progettazione disponibili in un ambiente di authoring.

>[!NOTE]
>
>Non è possibile aggiungere annotazioni a una pagina che è stata bloccata da un altro utente.

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

* Il cursore si trasforma in un reticolo incrociato quando siete in modalità sketch. Puoi disegnare più linee distinte.
* La linea dello schizzo riflette il colore dell’annotazione e può essere:

   * mano libera

      la modalità predefinita; terminare rilasciando il pulsante del mouse.

   * dritto:

      tenere premuto `ALT` e fare clic sui punti iniziale e finale; terminare con un doppio clic.

* Dopo aver terminato la modalità di sketch, potete fare clic su una linea di sketch per selezionarla.
* Spostate uno sketch selezionandolo, quindi trascinandolo nella posizione desiderata.
* Uno schizzo sovrappone il contenuto. Ciò significa che all’interno dei 4 angoli dello schizzo non è possibile fare clic sul paragrafo sottostante, ad esempio se è necessario modificare o accedere a un collegamento. Se si verifica un problema (ad esempio, se uno schizzo copre una vasta area della pagina), minimizza l’annotazione appropriata, in quanto questa operazione ridurrà anche tutti gli schizzi correlati, consentendo l’accesso all’area sottostante.
* Per eliminare un singolo schizzo, selezionatelo, quindi premete il tasto **Elimina** chiave (**fn**-**backspace** su un MAC).

* Se si sposta o si copia un paragrafo, verranno spostate o copiate anche tutte le annotazioni correlate e i relativi schizzi, mantenendo la stessa posizione rispetto al paragrafo.
* Se eliminate un’annotazione, verranno eliminati anche tutti gli schizzi associati ad essa.
