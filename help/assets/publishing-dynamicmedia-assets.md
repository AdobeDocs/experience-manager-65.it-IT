---
title: Pubblicazione delle risorse Dynamic Media
description: Come pubblicare risorse Dynamic Media
uuid: b1bee905-86cf-4284-8d4e-067e11557899
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 99d7025f-d022-4213-83c0-815a4712c573
role: User, Admin
exl-id: 750627fc-2a29-43ff-867e-55cb2e371043
feature: Publishing
source-git-commit: 363e5159d290ecfbf4338f6b9793e11b613389a5
workflow-type: tm+mt
source-wordcount: '461'
ht-degree: 4%

---

# Pubblicare risorse Dynamic Media {#publishing-dynamic-media-assets}

Per pubblicare le risorse Dynamic Media, seleziona le risorse già caricate e tocca **[!UICONTROL Pubblica]** o **[!UICONTROL Pubblicazione rapida]**. Dopo la pubblicazione delle risorse Dynamic Media, sono disponibili per l’inclusione in una pagina web tramite un URL o incorporando il codice nella pagina.

Puoi anche pubblicare istantaneamente le risorse caricate, senza alcun intervento dell’utente. Vedi [Configurare Dynamic Media - Modalità Scene7](config-dms7.md).
Oppure puoi pubblicare in modo selettivo le risorse su Dynamic Media o Adobe Experience Manager, reciprocamente esclusive, utilizzando **[!UICONTROL Pubblicazione selettiva]** a livello di cartella. Vedi [Utilizzo della pubblicazione selettiva in Dynamic Media](/help/assets/selective-publishing.md).

In **[!UICONTROL Vista a schede]**, sotto il nome di una risorsa viene visualizzata una piccola icona a forma di globo, a sinistra della data e dell’ora per indicare che è stata pubblicata. Nella **[!UICONTROL Vista a elenco]**, la colonna **[!UICONTROL Pubblicato]** indica lo stato di pubblicazione delle risorse.

>[!NOTE]
>
>Se una risorsa è già stata pubblicata, utilizza Experience Manager per spostare la risorsa in un’altra cartella e ripubblicarla dalla nuova posizione. La posizione originale della risorsa pubblicata è ancora disponibile, insieme alla nuova risorsa ripubblicata. La risorsa pubblicata originale, tuttavia, è &quot;persa&quot; in Experience Manager e non può essere annullata. Pertanto, come best practice, annulla la pubblicazione delle risorse prima di spostarle in un’altra cartella.

Se intendi pubblicare le risorse video subito dopo averle codificate, accertati di effettuare la codifica. Durante la codifica dei video, il sistema ti informa che è in corso un flusso di lavoro di elaborazione video. Al termine della codifica video, puoi visualizzare in anteprima le rappresentazioni video. A questo punto, è sicuro per te pubblicare i video senza che si verifichino errori di pubblicazione.

Vedi anche [Collegare gli URL all’applicazione Web](linking-urls-to-yourwebapplication.md).

Vedi anche [Incorporare il visualizzatore video o immagine Dynamic Media in una pagina web](embed-code.md)

>[!NOTE]
>
>* Per utilizzare l’URL, le risorse devono essere pubblicate. Se le risorse non vengono pubblicate, la copia e l’incolla dell’URL in un browser web non funziona.
>* I predefiniti per immagini e visualizzatori devono essere attivati e pubblicati per la distribuzione in diretta.
>


Per informazioni dettagliate sulla pubblicazione di un set o di una risorsa, consulta [Pubblicare le risorse](manage-assets.md).

## Distribuzione di risorse Dynamic Media HTTP/2 {#http-delivery-of-dynamic-media-assets}

Experience Manager ora supporta la distribuzione di tutti i contenuti Dynamic Media (immagini e video) su HTTP/2. In altre parole, è disponibile un URL o un codice di incorporamento pubblicato per l’immagine o il video da integrare con qualsiasi applicazione che accetta una risorsa in hosting. La risorsa pubblicata viene quindi distribuita tramite il protocollo HTTP/2. Questo metodo di consegna migliora il modo in cui i browser e i server comunicano, consentendo una migliore risposta e tempi di caricamento di tutte le risorse Dynamic Media.

Per ulteriori informazioni, consulta [Domande frequenti sulla distribuzione di contenuti HTTP/2](/help/sites-administering/scene7-http2faq.md).
