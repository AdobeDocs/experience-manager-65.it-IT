---
title: Pubblicazione di risorse multimediali dinamiche
description: Come pubblicare le risorse multimediali dinamiche
uuid: b1bee905-86cf-4284-8d4e-067e11557899
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 99d7025f-d022-4213-83c0-815a4712c573
translation-type: tm+mt
source-git-commit: cec6c4f9a1a75eb049dd4b8461c36c8d58d46f79
workflow-type: tm+mt
source-wordcount: '461'
ht-degree: 3%

---


# Pubblicazione di risorse multimediali dinamiche {#publishing-dynamic-media-assets}

Per pubblicare le risorse per contenuti multimediali dinamici, seleziona le risorse già caricate e tocca **[!UICONTROL Pubblica]** o **[!UICONTROL Pubblicazione rapida.]** Dopo la pubblicazione, le risorse Dynamic Media sono disponibili per l’inclusione in una pagina Web mediante un URL o incorporando il codice nella pagina.

Potete anche pubblicare istantaneamente le risorse caricate, senza alcun intervento da parte dell’utente. Consultate [Configurazione di contenuti multimediali dinamici - Modalità Scene7.](config-dms7.md)
In alternativa, potete pubblicare selettivamente le risorse su elementi multimediali dinamici o AEM, escludendovi vicendevolmente tra di loro, utilizzando  **[!UICONTROL Pubblicazione selettiva a]** livello di cartella. Consultate [Utilizzo della pubblicazione selettiva nei file multimediali dinamici.](/help/assets/selective-publishing.md)

Nella **[!UICONTROL vista a schede]**, un&#39;icona a forma di globo viene visualizzata direttamente sotto il nome di una risorsa e a sinistra della data e dell&#39;ora per indicare che è stata pubblicata. Nella **[!UICONTROL Vista a elenco]**, la colonna **[!UICONTROL Pubblicato]** indica lo stato di pubblicazione delle risorse.

>[!NOTE]
>
>Se una risorsa è già pubblicata, usate AEM per spostare la risorsa in un’altra cartella e ripubblicarla dalla nuova posizione, il percorso originale della risorsa pubblicata è ancora disponibile, insieme alla nuova risorsa pubblicata. La risorsa pubblicata originale, tuttavia, è &quot;perduta&quot; in AEM e non può essere annullata la pubblicazione. Di conseguenza, è consigliabile annullare la pubblicazione delle risorse prima di spostarle in un’altra cartella.

Se intendete pubblicare le risorse video subito dopo la codifica, accertatevi che la codifica sia stata completata. Quando i video vengono ancora codificati, il sistema segnala che è in corso un flusso di lavoro di elaborazione video. Al termine della codifica video, dovreste essere in grado di visualizzare in anteprima le rappresentazioni video. A questo punto, è sicuro pubblicare i video senza che si verifichino errori di pubblicazione.

Vedere anche [Collegamento di URL all&#39;applicazione Web](linking-urls-to-yourwebapplication.md).

Consultate anche [Incorporazione di video per file multimediali dinamici o visualizzatore di immagini in una pagina Web](embed-code.md)

>[!NOTE]
>
>* Per usare l’URL, le risorse devono essere pubblicate. Se le risorse non vengono pubblicate, non sarà possibile copiare e incollare l’URL in un browser Web.
>* I predefiniti per immagini e per visualizzatori devono essere attivati e pubblicati per la distribuzione live.

>



Per informazioni dettagliate sulla pubblicazione di un set o di una risorsa, consultate [Pubblicazione delle risorse.](manage-assets.md)

## Distribuzione HTTP/2 di risorse Dynamic Media {#http-delivery-of-dynamic-media-assets}

AEM ora supporta la distribuzione di tutti i contenuti multimediali dinamici (immagini e video) su HTTP/2. ossia un URL pubblicato o un codice da incorporare per l’immagine o il video può essere integrato con qualsiasi applicazione che accetta una risorsa ospitata. La risorsa pubblicata viene quindi distribuita tramite il protocollo HTTP/2. Questo metodo di distribuzione migliora il modo in cui i browser e i server comunicano, consentendo una migliore risposta e tempi di caricamento di tutte le risorse Dynamic Media.

Per ulteriori informazioni, vedere [Distribuzione HTTP/2 del contenuto alle domande frequenti](/help/sites-administering/scene7-http2faq.md).
