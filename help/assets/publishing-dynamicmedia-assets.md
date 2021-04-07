---
title: Pubblicazione delle risorse Dynamic Media
description: Come pubblicare risorse Dynamic Media
uuid: b1bee905-86cf-4284-8d4e-067e11557899
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 99d7025f-d022-4213-83c0-815a4712c573
role: Business Practitioner, Administrator
exl-id: 750627fc-2a29-43ff-867e-55cb2e371043
feature: Pubblicazione
translation-type: tm+mt
source-git-commit: 9134130f349c6c7a06ad9658a87f78a86b7dbf9c
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 5%

---

# Pubblicazione delle risorse Dynamic Media {#publishing-dynamic-media-assets}

Per pubblicare le risorse Dynamic Media, seleziona le risorse già caricate e tocca **[!UICONTROL Pubblica]** o **[!UICONTROL Pubblicazione rapida.]** Dopo la pubblicazione delle risorse Dynamic Media, sono disponibili per l’inclusione in una pagina web tramite un URL o incorporando il codice nella pagina.

Puoi anche pubblicare istantaneamente le risorse caricate senza alcun intervento da parte dell’utente. Consulta [Configurazione di Dynamic Media - Modalità Scene7 .](config-dms7.md)
In alternativa, puoi pubblicare selettivamente le risorse in Dynamic Media o AEM, reciprocamente esclusive, utilizzando  **[!UICONTROL Pubblicazione selettiva]** a livello di cartella. Consulta [Utilizzo della pubblicazione selettiva in Dynamic Media.](/help/assets/selective-publishing.md)

Nella **[!UICONTROL Vista a schede]**, sotto il nome di una risorsa viene visualizzata una piccola icona a forma di globo, a sinistra della data e dell’ora per indicare che è stata pubblicata. Nella **[!UICONTROL Vista a elenco]**, la colonna **[!UICONTROL Pubblicato]** indica lo stato di pubblicazione delle risorse.

>[!NOTE]
>
>Se una risorsa è già stata pubblicata, utilizza AEM per spostarla in un’altra cartella e ripubblicarla dalla nuova posizione, la posizione originale della risorsa pubblicata è ancora disponibile, insieme alla nuova risorsa pubblicata. La risorsa pubblicata originale, tuttavia, è &quot;persa&quot; in AEM e non può essere annullata. Pertanto, come best practice, annulla la pubblicazione delle risorse prima di spostarle in un’altra cartella.

Se intendi pubblicare le risorse video subito dopo averle codificate, accertati che la codifica sia completa. Quando i video vengono ancora codificati, il sistema ti informa che è in corso un flusso di lavoro di elaborazione video. Al termine della codifica video, dovresti essere in grado di visualizzare in anteprima le rappresentazioni video. A questo punto, è sicuro per te pubblicare i video senza che si verifichino errori di pubblicazione.

Consulta anche [Collegamento di URL all&#39;applicazione Web](linking-urls-to-yourwebapplication.md).

Consulta anche [Incorporare il visualizzatore video o immagine Dynamic Media in una pagina web](embed-code.md)

>[!NOTE]
>
>* Per utilizzare l’URL, le risorse devono essere pubblicate. Se le risorse non vengono pubblicate, non sarà possibile copiare e incollare l’URL in un browser web.
>* I predefiniti per immagini e visualizzatori devono essere attivati e pubblicati per la distribuzione in diretta.

>



Per informazioni dettagliate sulla pubblicazione di un set o di una risorsa, consulta [Pubblicazione di risorse.](manage-assets.md)

## Distribuzione HTTP/2 di risorse Dynamic Media {#http-delivery-of-dynamic-media-assets}

AEM ora supporta la distribuzione di tutti i contenuti Dynamic Media (immagini e video) su HTTP/2. In altre parole, è disponibile un URL o un codice di incorporamento pubblicato per l’immagine o il video da integrare con qualsiasi applicazione che accetta una risorsa in hosting. La risorsa pubblicata viene quindi distribuita tramite il protocollo HTTP/2. Questo metodo di consegna migliora il modo in cui i browser e i server comunicano, consentendo una migliore risposta e tempi di caricamento di tutte le risorse Dynamic Media.

Per ulteriori informazioni, consulta [Distribuzione HTTP/2 dei contenuti con domande frequenti](/help/sites-administering/scene7-http2faq.md) .
