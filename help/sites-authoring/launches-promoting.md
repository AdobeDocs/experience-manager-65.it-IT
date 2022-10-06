---
title: Promozione dei lanci
seo-title: Promoting Launches
description: Con la promozione delle pagine di lancio si sposta il contenuto nella sorgente (produzione) prima della pubblicazione.
seo-description: You need to promote launch pages to move the content back into the source (production) before publishing.
uuid: 2dc41817-fcfb-4485-a085-7b57b9fe89ec
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 3d4737ef-f758-4540-bc8f-ecd9f05f6bb0
docset: aem65
legacypath: /content/docs/en/aem/6-0/author/site-page-features/launches
exl-id: f59f12a2-ecd6-49cf-90ad-621719fe51bf
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '756'
ht-degree: 99%

---

# Promozione dei lanci{#promoting-launches}

Con la promozione delle pagine di lancio si sposta il contenuto nella sorgente (produzione) prima della pubblicazione. Quando una pagina di lancio viene promossa, la pagina corrispondente nelle pagine sorgente viene sostituita con il contenuto della pagina promossa. Quando si promuove una pagina di lancio, sono disponibili le seguenti opzioni:

* Promuovere solo la pagina corrente o l’intero lancio.
* Promuovere le pagine figlie della pagina corrente.
* Promuovere il lancio completo o solo le pagine che sono state modificate.
* Eliminare il lancio dopo la promozione.

>[!NOTE]
>
>Dopo aver promosso le pagine del lancio a destinazione (**Produzione**), puoi attivare le pagine di **Produzione** come entità (per rendere il processo più rapido). Aggiungi le pagine a un pacchetto di flusso di lavoro e utilizza quest’ultimo come payload per l’attivazione di un pacchetto di pagine. Prima di promuovere il lancio è necessario creare il pacchetto di workflow. Vedi [Elaborazione di pagine promosse con flusso di lavoro AEM](#processing-promoted-pages-using-aem-workflow).

>[!CAUTION]
>
>Non è possibile promuovere contemporaneamente un singolo lancio. Due azioni di promozione sullo stesso lancio nello stesso momento possono causare un errore: `Launch could not be promoted` (con gli errori di conflitto nel registro).

>[!CAUTION]
>
>Quando promuovi i lanci per le pagine *modificate*, vengono considerate le modifiche nei rami sia sorgente che lancio.

## Promozione delle pagine di lancio {#promoting-launch-pages}

>[!NOTE]
>
>Riguarda l’azione manuale per promuovere le pagine di lancio quando esiste un solo livello di lancio. Consulta:
>
>* [Promozione di un lancio nidificato](#promoting-a-nested-launch) in caso di più lanci nella struttura.
>* [Lanci: ordine degli eventi](/help/sites-authoring/launches.md#launches-the-order-of-events) per ulteriori dettagli sulla promozione e la pubblicazione automatica.
>


Puoi promuovere un lancio dalla console **Sites** o dalla console **Lanci**:

1. Apri:

   * la console **Sites**:

      1. Apri la [barra dei riferimenti](/help/sites-authoring/author-environment-tools.md#showingpagereferences) e seleziona la pagina sorgente desiderata utilizzando la [modalità di selezione](/help/sites-authoring/basic-handling.md) (oppure seleziona e apri la barra dei riferimenti, l’ordine non è importante). Verranno visualizzati tutti i riferimenti.

      1. Seleziona **Lanci** (ad esempio Lanci (1)) per visualizzare un elenco dei lanci specifici.
      1. Seleziona il lancio specifico per visualizzare le azioni disponibili.
      1. Seleziona **Promuovi lancio** per aprire la procedura guidata.
   * la console **Lanci**:

      1. Seleziona il lancio che ti interessa (tocca o fai clic sulla miniatura).
      1. Seleziona **Promuovi**.


1. Nel primo passaggio puoi specificare i seguenti parametri:

   * **Destinazione**

      * **Elimina lancio dopo la promozione**
   * **Ambito**

      * **Promuovi tutto il lancio**
      * **Promuovi pagine modificate**
      * **Promuovi la pagina corrente**
      * **Promuovi la pagina corrente e le sottopagine**

   Ad esempio, quando selezioni solo la promozione delle pagine modificate:

   ![launches-pd-06](assets/launches-pd-06.png)

   >[!NOTE]
   >
   >Riguarda un singolo lancio; per lanci nidificati, vedi [Promozione di un lancio nidificato](#promoting-a-nested-launch).

1. Seleziona **Avanti** per continuare.
1. Puoi rivedere le pagine da promuovere, a seconda dell’intervallo di pagine scelto:

   ![chlimage_1-102](assets/chlimage_1-102.png)

1. Seleziona **Promuovi**.

## Promozione di pagine di lancio durante la modifica {#promoting-launch-pages-when-editing}

Durante la modifica di una pagina di lancio, l’azione **Promuovi lancio** è disponibile anche da **Informazioni pagina**. Si aprirà la procedura guidata per raccogliere le informazioni necessarie.

![chlimage_1-103](assets/chlimage_1-103.png)

>[!NOTE]
>
>Questa funzione è disponibile per i lanci singoli e per i [lanci nidificati](#promoting-a-nested-launch).

## Promozione di un lancio nidificato {#promoting-a-nested-launch}

Dopo aver creato un lancio nidificato, puoi promuoverlo di nuovo su qualsiasi sorgente, compresa la sorgente principale (produzione).

![chlimage_1-104](assets/chlimage_1-104.png)

1. Come per la [Creazione di un lancio nidificato](#creatinganestedlaunchlaunchwithinalaunch), accedi e seleziona il lancio richiesto nella console **Lanci** o nella barra **Riferimenti**.
1. Seleziona **Promuovi lancio** per aprire la procedura guidata.

1. Immetti i dettagli necessari:

   * **Destinazione**

      * **Destinazione della promozione** Puoi promuovere a una delle sorgenti.

      * **Elimina lancio dopo la promozione** Dopo la promozione del lancio selezionato e dei lanci nidificati al suo interno, esso verrà eliminato.
   * **Ambito** Puoi scegliere se promuovere l’intero lancio o solo le pagine che sono state modificate. Nel secondo caso, puoi scegliere di includere o escludere le pagine secondarie. La configurazione predefinita prevede di promuovere le modifiche solo per la pagina corrente:

      * **Promuovi tutto il lancio**
      * **Promuovi pagine modificate**
      * **Promuovi la pagina corrente**
      * **Promuovi la pagina corrente e le sottopagine**

   ![chlimage_1-105](assets/chlimage_1-105.png)

1. Seleziona **Avanti**.
1. Rivedi i dettagli della promozione prima di selezionare **Promuovi**:

   ![chlimage_1-106](assets/chlimage_1-106.png)

   >[!NOTE]
   >
   >Le pagine elencate dipendono dall’**Ambito** definito ed eventualmente dalle pagine che sono state modificate.

1. Le modifiche verranno promosse e riportate nella console **Lanci**:

   ![chlimage_1-107](assets/chlimage_1-107.png)

## Elaborazione di pagine promosse tramite Flusso di lavoro AEM {#processing-promoted-pages-using-aem-workflow}

I modelli di flusso di lavoro consentono di eseguire operazioni di elaborazione collettive sulle pagine di lancio promosse:

1. Crea un pacchetto di flusso di lavoro.
1. Quando gli autori promuovono le pagine di lanci, queste vengono memorizzate nel pacchetto di flusso di lavoro.
1. Avvia un modello di flusso di lavoro utilizzando il pacchetto come payload.

Per avviare automaticamente un flusso di lavoro quando vengono promosse le pagine, [configura un programma di avvio del flusso di lavoro](/help/sites-administering/workflows-starting.md#workflows-launchers) per il nodo del pacchetto.

Ad esempio, puoi generare automaticamente le richieste di attivazione pagina non appena un autore promuove una pagina di lancio. Configura un programma di avvio per avviare il flusso di lavoro Attivazione richiesta quando viene modificato il nodo del pacchetto.

![chlimage_1-108](assets/chlimage_1-108.png)
