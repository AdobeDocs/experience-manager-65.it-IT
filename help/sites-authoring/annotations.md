---
title: Annotazioni durante la modifica di una pagina di contenuto
description: Molti componenti direttamente correlati al contenuto consentono di aggiungere un’annotazione.
uuid: 157be55c-8ab8-472e-be32-0dcc02bfa41d
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: aa89326a-ad33-4b0b-8d09-c68c5a5c790a
exl-id: de1ae7e3-db3a-4b5e-8a4f-ae111227181f
source-git-commit: e1a0b114ce16d0e7f6a464e9d30b8f111297bcc6
workflow-type: tm+mt
source-wordcount: '634'
ht-degree: 45%

---

# Annotazioni durante la modifica di una pagina{#annotations-when-editing-a-page}

L’aggiunta di contenuti alle pagine del sito web è spesso soggetta a discussioni prima che venga effettivamente pubblicato. Per facilitare questa fase, molti componenti direttamente correlati al contenuto (a differenza, ad esempio, del layout) consentono di aggiungere un’annotazione.

Un’annotazione si presenta come una nota colorata applicata alla pagina. può contenere commenti o domande inseriti da un utente e destinati ad altri autori o revisori.

>[!NOTE]
>
>Nella definizione di un singolo tipo di componente è possibile specificare se l’aggiunta di annotazioni è supportata o meno per le istanze del componente.

>[!NOTE]
>
>Le annotazioni create nell’interfaccia classica vengono visualizzate nell’interfaccia touch. Tuttavia, gli schizzi sono specifici per l’interfaccia utente e vengono visualizzati solo nell’interfaccia in cui sono stati creati.

>[!CAUTION]
>
>Se si elimina una risorsa (ad esempio, un paragrafo), vengono anche eliminate tutte le annotazioni e gli schizzi associati ad essa, indipendentemente dalla loro posizione sulla pagina.

>[!NOTE]
>
>Se necessario, puoi anche sviluppare un flusso di lavoro per inviare una notifica quando vengono aggiunte, aggiornate o eliminate delle annotazioni.

## Annotazioni {#annotations}

Per la creazione e la visualizzazione delle annotazioni viene utilizzata una [modalità](/help/sites-authoring/author-environment-tools.md#page-modes) speciale.

>[!NOTE]
>
>Sono disponibili anche i [commenti](/help/sites-authoring/basic-handling.md#timeline) per fornire feedback in una pagina.

>[!NOTE]
>
>È possibile annotare una varietà di risorse:
>
>* [Aggiunta di annotazioni alle risorse](/help/assets/manage-assets.md#annotating)
>* [Aggiunta di annotazioni alle risorse video](/help/assets/managing-video-assets.md#annotate-video-assets)
>


### Aggiunta di annotazioni a un componente {#annotating-a-component}

La modalità Annota consente di creare, modificare, spostare o eliminare annotazioni nel contenuto:

1. Per accedere alla modalità Annota , usate l’icona nella barra degli strumenti (in alto a destra) durante la modifica di una pagina:

   ![](do-not-localize/screen_shot_2018-03-22at110414.png)

   È ora possibile visualizzare tutte le annotazioni esistenti.

   >[!NOTE]
   >
   >Per uscire dalla modalità Annotazione tocca o fai clic sull’icona Annota (simbolo x) a destra della barra degli strumenti superiore.

1. Tocca o fai clic sull’icona Aggiungi annotazione (simbolo + a sinistra della barra degli strumenti) per iniziare ad aggiungere annotazioni.

   >[!NOTE]
   >
   >Per interrompere l’aggiunta di annotazioni (e tornare alla visualizzazione), tocca o fai clic sull’icona Annulla (simbolo x in un cerchio bianco) a sinistra della barra degli strumenti superiore.

1. Tocca o fai clic sul componente richiesto (i componenti ai quali è possibile aggiungere annotazioni saranno evidenziati da un bordo blu) per aggiungere l’annotazione e aprire la finestra di dialogo:

   ![screen_shot_2018-03-22at110606](assets/screen_shot_2018-03-22at110606.png)

   Utilizzando il campo e/o l’icona appropriata puoi effettuare le seguenti operazioni:

   * Inserisci il testo dell’annotazione.
   * Crea uno schizzo (linee e forme) per evidenziare un’area del componente.

      Il cursore assume la forma di un mirino quando si crea uno schizzo. Puoi disegnare più linee distinte. La linea dello schizzo ha lo stesso colore dell’annotazione e può essere una freccia, un cerchio o un ovale.
   ![](do-not-localize/screen_shot_2018-03-22at110640.png)

   * Scegli o modifica il colore:

   ![](do-not-localize/chlimage_1-19.png)

   * Elimina l’annotazione.

   ![](do-not-localize/screen_shot_2018-03-22at110647.png)

1. Per chiudere la finestra di dialogo dell’annotazione, toccate o fate clic all’esterno della finestra di dialogo. Viene visualizzata una vista troncata (la prima parola) dell’annotazione con eventuali sketch:

   ![screen_shot_2018-03-22at110850](assets/screen_shot_2018-03-22at110850.png)

1. Dopo aver modificato un’annotazione, puoi effettuare le seguenti operazioni:

   * Tocca o fai clic sul marcatore di testo per aprire l’annotazione. Una volta aperta l’annotazione, è possibile visualizzare il testo completo, apportare modifiche o eliminare l’annotazione.

      * Gli schizzi non possono essere eliminati in modo indipendente dall’annotazione.
   * Riposiziona il marcatore di testo.
   * Tocca o fai clic su una linea di uno schizzo per selezionarlo e trascinarlo nella posizione desiderata.
   * Sposta o copia un componente.

      * Vengono spostate o copiate anche tutte le annotazioni e gli schizzi associati, mantenendo la stessa posizione relativa al paragrafo.


1. Per uscire dalla modalità Annotazione e tornare alla modalità precedentemente utilizzata, tocca o fai clic sull’icona Annota (simbolo x) a destra della barra degli strumenti superiore.

>[!NOTE]
>
>Non è possibile aggiungere annotazioni a una pagina che è stata bloccata da un altro utente.

### Indicatore di annotazione {#annotation-indicator}

Le annotazioni non vengono visualizzate in modalità Modifica, ma il contrassegno in alto a destra della barra degli strumenti mostra il numero di annotazioni esistenti per la pagina corrente. Il contrassegno sostituisce l’icona Annotazioni predefinita, ma continua a fungere da collegamento rapido per attivare o disattivare la modalità Annota:

![chlimage_1-242](assets/chlimage_1-242.png)
