---
title: Distribuzione di risorse Dynamic Media
description: Scopri come distribuire risorse multimediali dinamiche
uuid: 23eddf83-34f5-4aae-8b81-d1cd7a098a7e
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: e3b44330-d476-49c6-b7ba-079d0d60e500
docset: aem65
translation-type: tm+mt
source-git-commit: 3eacfe8a79d155dddde8908d05b05790d048b0c5
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 15%

---


# Distribuzione di risorse Dynamic Media{#delivering-dynamic-media-assets}

La modalità di distribuzione delle risorse multimediali dinamiche (video e immagini) dipende dall’implementazione del sito Web.

Con l’elemento multimediale dinamico hai a disposizione diverse opzioni:

* Se il sito web è ospitato su AEM, allora è necessario aggiungere le risorse dell’elemento multimediale dinamico direttamente sulla pagina.
* Se il sito Web non è AEM, potete scegliere tra:

   * Incorporamento del video o dell’immagine nel sito Web.
   * Collegare gli URL all’applicazione Web. Usate il collegamento per distribuire un lettore video come finestra a comparsa o modale.
   * Se il sito è reattivo, è possibile [distribuire immagini ottimizzate.](/help/assets/responsive-site.md)

>[!NOTE]
>
>La funzione di imaging avanzato funziona con i predefiniti per immagini esistenti e utilizza funzionalità intelligenti all’ultimo millisecondo di distribuzione per ridurre ulteriormente le dimensioni dei file immagine in base alla velocità della connessione di rete o del browser. Per ulteriori informazioni, vedere [Smart Imaging](/help/assets/imaging-faq.md).

Per ulteriori informazioni, consulta i seguenti argomenti:

* [Aggiunta di risorse multimediali dinamiche alle pagine Web](/help/assets/adding-dynamic-media-assets-to-pages.md)
* [Incorporazione di un visualizzatore video o di immagini in una pagina Web](/help/assets/embed-code.md)
* [Attivazione della protezione hotlinking in Dynamic Media](hotlink-protection.md)
* [Collegamento di URL all&#39;applicazione Web](/help/assets/linking-urls-to-yourwebapplication.md)
* [Distribuzione di immagini ottimizzate per un sito reattivo](/help/assets/responsive-site.md)
* [HTTP2 Distribuzione dei contenuti](/help/assets/http2.md)
* [Annullamento della validità della cache CDN tramite Dynamic Media Classic](/help/assets/invalidate-cdn-cache-dm-classic.md)
* [Utilizzo dei set di regole per trasformare gli URL](/help/assets/using-rulesets-to-transform-urls.md)


## Distribuzione HTTP/2 di risorse Dynamic Media {#http-delivery-of-dynamic-media-assets}

AEM ora supporta la distribuzione di tutti i contenuti multimediali dinamici (immagini e video) su HTTP/2. ossia un URL pubblicato o un codice da incorporare per l’immagine o il video può essere integrato con qualsiasi applicazione che accetta una risorsa ospitata. La risorsa pubblicata viene quindi distribuita tramite il protocollo HTTP/2. Questo metodo di distribuzione migliora il modo in cui i browser e i server comunicano, consentendo una migliore risposta e tempi di caricamento di tutte le risorse Dynamic Media.

Per ulteriori informazioni, consulta [Distribuzione HTTP/2 dei contenuti Domande frequenti](/help/sites-administering/scene7-http2faq.md).
