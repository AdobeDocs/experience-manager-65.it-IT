---
title: Distribuzione di risorse Dynamic Media
description: Scopri come distribuire le risorse Dynamic Media
uuid: 23eddf83-34f5-4aae-8b81-d1cd7a098a7e
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: e3b44330-d476-49c6-b7ba-079d0d60e500
docset: aem65
role: Business Practices, amministratore
translation-type: tm+mt
source-git-commit: ebe7042b931869c3b4b7204e3ce7afa52d56f0ef
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 9%

---


# Distribuzione di risorse Dynamic Media{#delivering-dynamic-media-assets}

La modalità di distribuzione delle risorse Dynamic Media, sia video che immagini, dipende da come viene implementato il sito web.

Con l’elemento multimediale dinamico hai a disposizione diverse opzioni:

* Se il sito web è ospitato su AEM, è necessario aggiungere le risorse Dynamic Media direttamente alla pagina.
* Se il sito web non è AEM, puoi scegliere tra:

   * Incorporare il video o l’immagine sul sito web.
   * Collega URL all’applicazione web. Utilizza il collegamento quando desideri distribuire un lettore video come finestra a comparsa o modale.
   * Se il sito è reattivo, è possibile [fornire immagini ottimizzate.](/help/assets/responsive-site.md)

>[!NOTE]
>
>La funzione Smart imaging funziona con i predefiniti per immagini esistenti e utilizza funzionalità intelligenti all’ultimo millisecondo di distribuzione per ridurre ulteriormente le dimensioni dei file immagine in base al browser o alla velocità di connessione di rete. Per ulteriori informazioni, consulta [Smart imaging](/help/assets/imaging-faq.md) .

Per ulteriori informazioni, consulta i seguenti argomenti:

* [Aggiunta di risorse Dynamic Media alle pagine web](/help/assets/adding-dynamic-media-assets-to-pages.md)
* [Incorporamento del visualizzatore di video o immagini in una pagina web](/help/assets/embed-code.md)
* [Attivazione della protezione hotlinking in Dynamic Media](hotlink-protection.md)
* [Collegamento di URL all’applicazione Web](/help/assets/linking-urls-to-yourwebapplication.md)
* [Distribuzione di immagini ottimizzate per un sito reattivo](/help/assets/responsive-site.md)
* [Distribuzione di contenuti HTTP2](/help/assets/http2.md)
* [Annullare la validità della cache CDN tramite Dynamic Media Classic](/help/assets/invalidate-cdn-cache-dm-classic.md)
* [Utilizzo di set di regole per la trasformazione degli URL](/help/assets/using-rulesets-to-transform-urls.md)


## Distribuzione HTTP/2 di risorse Dynamic Media {#http-delivery-of-dynamic-media-assets}

AEM ora supporta la distribuzione di tutti i contenuti Dynamic Media (immagini e video) su HTTP/2. In altre parole, è disponibile un URL o un codice di incorporamento pubblicato per l’immagine o il video da integrare con qualsiasi applicazione che accetta una risorsa in hosting. La risorsa pubblicata viene quindi distribuita tramite il protocollo HTTP/2. Questo metodo di consegna migliora il modo in cui i browser e i server comunicano, consentendo una migliore risposta e tempi di caricamento di tutte le risorse Dynamic Media.

Per ulteriori informazioni, consulta [Domande frequenti sulla distribuzione dei contenuti HTTP/2](/help/sites-administering/scene7-http2faq.md) .
