---
title: Pubblicazione di risorse Dynamic Media
description: Come pubblicare le risorse Dynamic Media
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

Per pubblicare le risorse Dynamic Media, seleziona quelle già caricate e tocca **[!UICONTROL Pubblica]** o **[!UICONTROL Pubblicazione rapida]**. Una volta pubblicate, le risorse Dynamic Media possono essere incluse in una pagina web tramite un URL o incorporando il codice nella pagina.

Puoi anche pubblicare immediatamente le risorse caricate, senza alcun intervento da parte dell’utente. Consulta [Configurare Dynamic Media - Modalità Scene7](config-dms7.md).
In alternativa, puoi pubblicare selettivamente le risorse in Dynamic Media o Adobe Experience Manager, escludendovi a vicenda, utilizzando **[!UICONTROL Pubblicazione selettiva]** a livello di cartella. Consulta [Utilizzare la pubblicazione selettiva in Dynamic Media](/help/assets/selective-publishing.md).

In **[!UICONTROL Vista a schede]**, sotto il nome di una risorsa e a sinistra della data e dell’ora viene visualizzata una piccola icona a forma di globo, per indicare che è stata pubblicata. Nella **[!UICONTROL Vista a elenco]**, la colonna **[!UICONTROL Pubblicato]** indica lo stato di pubblicazione delle risorse.

>[!NOTE]
>
>Se una risorsa è già pubblicata, utilizza Experience Manager per spostarla in un’altra cartella e ripubblicarla dalla nuova posizione. La posizione originale della risorsa pubblicata è ancora disponibile, insieme alla risorsa appena ripubblicata. La risorsa pubblicata originale, tuttavia, viene persa per Experience Manager e non può essere annullata. Di conseguenza, come best practice, è consigliabile annullare la pubblicazione delle risorse prima di spostarle in un’altra cartella.

Se intendi pubblicare le risorse video subito dopo averle codificate, assicurati che sia eseguita la codifica. Durante la codifica dei video, il sistema ti informa che è in corso un flusso di lavoro di elaborazione video. Al termine della codifica video, puoi visualizzare in anteprima le rappresentazioni video. A questo punto, puoi pubblicare i video senza incorrere in errori di pubblicazione.

Vedi anche [Collegare gli URL all’applicazione web](linking-urls-to-yourwebapplication.md).

Vedi anche [Incorporare il visualizzatore di video o immagini Dynamic Media in una pagina web](embed-code.md)

>[!NOTE]
>
>* Per utilizzare l’URL, le risorse devono essere pubblicate. Se le risorse non sono pubblicate, non è possibile copiare e incollare l’URL in un browser web.
>* Per la distribuzione live, è necessario attivare e pubblicare i predefiniti immagine e i predefiniti visualizzatore.
>


Per informazioni dettagliate sulla pubblicazione di un set o di una risorsa, consulta [Pubblicare le risorse](manage-assets.md).

## Distribuzione HTTP/2 delle risorse Dynamic Media {#http-delivery-of-dynamic-media-assets}

Experience Manager ora supporta la distribuzione di tutti i contenuti Dynamic Media (immagini e video) tramite HTTP/2. In altre parole, è disponibile un URL pubblicato o un codice di incorporamento per l’immagine o il video da integrare con qualsiasi applicazione che accetta una risorsa in hosting. La risorsa pubblicata viene quindi distribuita tramite il protocollo HTTP/2. Questo metodo di distribuzione migliora il modo in cui browser e server comunicano, consentendo tempi di risposta e di caricamento migliori per tutte le risorse Dynamic Media.

Per ulteriori informazioni, consulta [Domande frequenti sulla distribuzione HTTP/2 dei contenuti](/help/sites-administering/scene7-http2faq.md).
