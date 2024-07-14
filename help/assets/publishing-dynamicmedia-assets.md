---
title: Pubblicazione di Dynamic Medie Assets
description: Scopri come pubblicare le risorse Dynamic Medie, come video e immagini, inclusa la distribuzione HTTP/2 di tali risorse.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
role: User, Admin
exl-id: 750627fc-2a29-43ff-867e-55cb2e371043
feature: Publishing
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 4%

---

# Pubblicare risorse Dynamic Media {#publishing-dynamic-media-assets}

Per pubblicare le risorse Dynamic Medie, seleziona le risorse già caricate e tocca **[!UICONTROL Publish]** o **[!UICONTROL Quick Publish]**. Una volta pubblicate, le risorse Dynamic Medie possono essere incluse in una pagina web tramite un URL o incorporando il codice nella pagina web.

Puoi anche pubblicare immediatamente le risorse caricate, senza alcun intervento da parte dell’utente. Vedere [Configurare Dynamic Medie - Modalità Scene7](config-dms7.md).
In alternativa, puoi pubblicare selettivamente le risorse in Dynamic Medie o Adobe Experience Manager, escludendole a vicenda, utilizzando **[!UICONTROL Publish selettivo]** a livello di cartella. Vedi [Utilizzare Publish selettivo in Dynamic Medie](/help/assets/selective-publishing.md).

Nella **[!UICONTROL Vista a schede]**, sotto il nome di una risorsa viene visualizzata una piccola icona a forma di globo, a sinistra della data e dell&#39;ora per indicare che è stata pubblicata. Nella **[!UICONTROL Vista a elenco]**, la colonna **[!UICONTROL Pubblicato]** indica lo stato di pubblicazione delle risorse.

>[!NOTE]
>
>Se una risorsa è già pubblicata, utilizza Experience Manager per spostarla in un’altra cartella e ripubblicarla dalla nuova posizione. La posizione originale della risorsa pubblicata è ancora disponibile, insieme alla risorsa appena ripubblicata. La risorsa pubblicata originale, tuttavia, viene persa per Experience Manager e non può essere annullata. Di conseguenza, come best practice, è consigliabile annullare la pubblicazione delle risorse prima di spostarle in un’altra cartella.

Se intendi pubblicare le risorse video subito dopo averle codificate, assicurati che sia eseguita la codifica. Durante la codifica dei video, il sistema ti informa che è in corso un flusso di lavoro di elaborazione video. Al termine della codifica video, puoi visualizzare in anteprima le rappresentazioni video. A questo punto, puoi pubblicare i video senza incorrere in errori di pubblicazione.

Vedi anche [Collegare gli URL all&#39;applicazione Web](linking-urls-to-yourwebapplication.md).

Vedi anche [Incorporare il visualizzatore di video o immagini Dynamic Medie in una pagina Web](embed-code.md)

>[!NOTE]
>
>* Per utilizzare l’URL, è necessario pubblicare Assets. Se le risorse non sono pubblicate, non è possibile copiare e incollare l’URL in un browser web.
>* Per la distribuzione live, è necessario attivare e pubblicare i predefiniti immagine e i predefiniti visualizzatore.
>

Per informazioni dettagliate sulla pubblicazione di un set o di una risorsa, consulta [Risorse Publish](manage-assets.md).

## Distribuzione HTTP/2 delle risorse Dynamic Medie {#http-delivery-of-dynamic-media-assets}

Experience Manager ora supporta la distribuzione di tutti i contenuti Dynamic Medie (immagini e video) tramite HTTP/2. In altre parole, è disponibile un URL pubblicato o un codice di incorporamento per l’immagine o il video da integrare con qualsiasi applicazione che accetta una risorsa in hosting. La risorsa pubblicata viene quindi distribuita tramite il protocollo HTTP/2. Questo metodo di distribuzione migliora il modo in cui browser e server comunicano, consentendo tempi di risposta e di caricamento migliori per tutte le risorse Dynamic Medie.

Per ulteriori informazioni, consulta [Domande frequenti sulla distribuzione HTTP/2 del contenuto](/help/sites-administering/scene7-http2faq.md).
