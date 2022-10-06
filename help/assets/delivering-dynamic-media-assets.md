---
title: Distribuire elementi multimediali dinamici
description: Scopri come distribuire le risorse Dynamic Media
uuid: 23eddf83-34f5-4aae-8b81-d1cd7a098a7e
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: e3b44330-d476-49c6-b7ba-079d0d60e500
docset: aem65
role: User, Admin
exl-id: 274af114-845a-46bd-b091-802cf589687a
feature: Asset Management,Renditions
source-git-commit: f4b7566abfa0a8dbb490baa0e849de6c355a3f06
workflow-type: tm+mt
source-wordcount: '310'
ht-degree: 15%

---

# Distribuire elementi multimediali dinamici{#delivering-dynamic-media-assets}

La modalità di distribuzione delle risorse Dynamic Media, sia video che immagini, dipende da come viene implementato il sito web.

Con Dynamic Media hai diverse opzioni:

* Se il sito web è ospitato su Adobe Experience Manager, è necessario aggiungere le risorse Dynamic Media direttamente alla pagina.
* Se il tuo sito web non è disponibile come Experience Manager, puoi scegliere tra:

   * Incorporare il video o l’immagine sul sito web.
   * Collegamento degli URL all’applicazione Web. Utilizza il collegamento quando desideri distribuire un lettore video come finestra a comparsa o modale.
   * Se il sito è reattivo, puoi [fornire immagini ottimizzate](/help/assets/responsive-site.md).

>[!NOTE]
>
>La funzione Smart imaging funziona con i predefiniti per immagini esistenti e utilizza funzionalità intelligenti all’ultimo millisecondo di distribuzione per ridurre ulteriormente le dimensioni dei file immagine in base al browser o alla velocità di connessione di rete. Vedi [Imaging avanzato](/help/assets/imaging-faq.md) per ulteriori informazioni.

Per ulteriori informazioni, consulta i seguenti argomenti:

* [Aggiungere risorse Dynamic Media alle pagine web](/help/assets/adding-dynamic-media-assets-to-pages.md)
* [Incorporare il visualizzatore di video o immagini in una pagina web](/help/assets/embed-code.md)
* [Attivazione della protezione hotlinking in Dynamic Media](/help/assets/hotlink-protection.md)
* [Collegamento degli URL all’applicazione Web](/help/assets/linking-urls-to-yourwebapplication.md)
* [Distribuzione di immagini ottimizzate per un sito reattivo](/help/assets/responsive-site.md)
* [Distribuzione di contenuti HTTP2](/help/assets/http2.md)
* [Invalidare la cache CDN tramite Dynamic Media Classic](/help/assets/invalidate-cdn-cache-dm-classic.md)
* [Utilizzo di set di regole per la trasformazione degli URL](/help/assets/using-rulesets-to-transform-urls.md)


## Distribuzione di risorse Dynamic Media HTTP/2 {#http-delivery-of-dynamic-media-assets}

Experience Manager ora supporta la distribuzione di tutti i contenuti Dynamic Media (immagini e video) su HTTP/2. In altre parole, è disponibile un URL o un codice di incorporamento pubblicato per l’immagine o il video da integrare con qualsiasi applicazione che accetta una risorsa in hosting. La risorsa pubblicata viene quindi distribuita tramite il protocollo HTTP/2. Questo metodo di consegna migliora il modo in cui i browser e i server comunicano, consentendo una migliore risposta e tempi di caricamento di tutte le risorse Dynamic Media.

Per ulteriori informazioni, consulta [Domande frequenti sulla distribuzione di contenuti HTTP/2](/help/sites-administering/scene7-http2faq.md).
