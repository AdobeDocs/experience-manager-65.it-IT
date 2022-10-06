---
title: Annotazioni durante la modifica di una pagina
seo-title: Annotations when Editing a Page
description: Quando si aggiunge del contenuto alle pagine di un sito Web è spesso necessario discuterne con i colleghi prima di pubblicarlo. Per semplificare le cose, molti componenti direttamente correlati al contenuto supportano l’inserimento di annotazioni.
seo-description: Adding content to the pages of your website is often subject to discussions prior to it actually being published. To aid this, many components directly related to content allow you to add an annotation.
page-status-flag: de-activated
uuid: d8d6ba76-f2aa-4044-98bf-5d506742d90d
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 9bee0197-f275-49cc-922d-62cba826c4e5
exl-id: d60e9601-d15b-4378-a33e-e90961f63195
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '782'
ht-degree: 95%

---

# Annotazioni durante la modifica di una pagina{#annotations-when-editing-a-page}

Quando si aggiunge del contenuto alle pagine di un sito web è spesso necessario discuterne con i colleghi prima di pubblicarlo. Per facilitare questa fase, molti componenti direttamente correlati al contenuto (a differenza, ad esempio, dei componenti per il layout) supportano l’inserimento di annotazioni.

Un’annotazione si presenta come una nota colorata applicata alla pagina. può contenere commenti o domande inseriti da un utente e destinati ad altri autori o revisori.

>[!NOTE]
>
>Nella definizione di un singolo tipo di componente è possibile specificare se l’aggiunta di annotazioni è supportata o meno per le istanze del componente.

>[!NOTE]
>
>Le annotazioni create nell’interfaccia classica vengono mostrate anche nell’interfaccia touch. Le annotazioni di tipo schizzo sono invece elementi specifici dell’interfaccia utente e vengono visualizzati solo nell’interfaccia con cui sono stati creati.

>[!CAUTION]
>
>Se si elimina una risorsa (ad esempio, un paragrafo), vengono anche eliminate tutte le annotazioni e gli schizzi associati ad essa, indipendentemente dalla loro posizione sulla pagina.

>[!NOTE]
>
>A seconda delle esigenze è inoltre possibile sviluppare un flusso di lavoro per inviare notifiche quando vengono aggiunte, aggiornate o eliminate delle annotazioni.

## Annotazioni {#annotations}

A seconda della progettazione del paragrafo, l’annotazione è disponibile come opzione nel menu di scelta rapida (in genere disponibile quando si fa clic con il pulsante destro del mouse sul paragrafo) oppure come pulsante nella barra di modifica del paragrafo.

In entrambi i casi, seleziona **Annota**. Una nota colorata viene applicata al paragrafo, in modalità Modifica, pronta per l’inserimento di un commento:

![chlimage_1-137](assets/chlimage_1-137.png)

Se necessario, sposta l’annotazione altrove sulla pagina. Fai clic sul bordo superiore della nota, quindi tieni premuto e trascina l’annotazione fino alla posizione desiderata. La potete posizionare ovunque sulla pagina, ma in genere si consiglia di collegarla al paragrafo a cui fa riferimento.

Le annotazioni (ed eventuali schizzi correlati) vengono inoltre incluse in qualsiasi operazione Copia, Taglia e Incolla eseguita sui paragrafi ai quali sono collegate. Per le operazioni Copia o Taglia, viene mantenuta la posizione dell’annotazione (e dei relativi schizzi) in relazione al paragrafo di origine.

È inoltre possibile aumentare o diminuire le dimensioni dell’annotazione trascinando l’angolo in basso a destra.

Per motivi di tracciamento, nella riga piè di pagina viene indicato l’utente che ha creato l’annotazione e l’ora in cui è stata creata. Altri autori possono quindi modificare l’annotazione (il piè di pagina viene aggiornato di conseguenza) o creare una nuova annotazione per lo stesso paragrafo.

L’eliminazione di un’annotazione è preceduta da una richiesta di conferma. Quando si elimina un’annotazione vengono anche eliminati eventuali schizzi associati ad essa.

Le tre icone in alto a sinistra consentono di ridurre l’annotazione (ed eventuali schizzi), cambiarne il colore e aggiungere degli schizzi.

>[!NOTE]
>
>Le annotazioni sono visibili solo in modalità Modifica nell’ambiente di authoring.
>
>Non sono invece visibili nell’ambiente di pubblicazione, né nelle modalità Anteprima o Progettazione dell’ambiente Authoring.

>[!NOTE]
>
>Non è possibile aggiungere annotazioni a una pagina che è stata bloccata da un altro utente.

## Schizzi per annotazione {#annotation-sketches}

>[!NOTE]
>
>Gli schizzi non sono disponibili in Internet Explorer, pertanto:
>
>* l’icona non è disponibile;
>* eventuali schizzi esistenti creati in altri browser non vengono mostrati.
>


Gli schizzi sono una funzione di annotazione per la creazione di grafica semplice, composta di linee, ovunque nella porzione visibile della finestra del browser:

![chlimage_1-138](assets/chlimage_1-138.png)

* In modalità schizzo, il cursore diventa una crocetta. Puoi disegnare più linee distinte.
* La linea dello schizzo ha lo stesso colore dell’annotazione e può essere:

   * a mano libera

      modalità predefinita; per terminare il disegno, rilasciate il pulsante del mouse.

   * retta

      tenete premuto il tasto `ALT` e fate clic sui punti iniziale e finale; per terminare, fate doppio clic.

* Una volta usciti dalla modalità schizzo, potete fare clic su una linea per selezionare lo schizzo.
* Per spostare uno schizzo, selezionatelo e trascinatelo fino alla posizione desiderata.
* Gli schizzi vengono sovrapposti ai contenuti. Questo significa che nell’area racchiusa entro i quattro angoli di uno schizzo, non è possibile fare clic sul paragrafo sottostante (ad esempio, se occorre modificarlo o accedere a un collegamento). Se questo diventa problematico (ad esempio, se uno schizzo copre un’area estesa della pagina), è sufficiente ridurre la relativa annotazione: anche tutti gli schizzi correlati vengono ridotti e l’area sottostante diventa accessibile.
* Per eliminare un singolo schizzo, selezionatelo e premete il tasto **Canc** (in Mac, **fn**-**Ritorno unitario**).

* Se si sposta o copia un paragrafo, vengono spostate o copiate anche tutte le relative annotazioni con gli schizzi ad esse associati, mantenendo la stessa posizione relativa al paragrafo.
* Se si elimina un’annotazione, vengono eliminati anche tutti gli schizzi ad essa associati.
