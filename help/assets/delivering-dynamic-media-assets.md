---
title: Distribuire risorse Dynamic Media
description: Scopri come distribuire risorse Dynamic Media, come video e immagini, alle pagine web.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
docset: aem65
role: User, Admin
exl-id: 274af114-845a-46bd-b091-802cf589687a
feature: Asset Management,Renditions
solution: Experience Manager, Experience Manager Assets
autotag-review: '2026-05-18T18:45:05.823Z'
TQID: 'https://experienceleague.adobe.com/a5ifneRAYCIMHKCGJHGQu9aoQt3EWZu1hiGYItlPZOE'
product_v2: id: e14eb250-3c22-4a07-9061-a78112b2b826id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554
level_v2: id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5id: b5a62a22-46f7-4f0d-b151-3fc640bef588
source-git-commit: 9c96b6744c7af2f061b4dfbf403560047485f9b5
workflow-type: tm+mt
source-wordcount: 324
ht-degree: 11%

---

# Distribuire risorse Dynamic Media{#delivering-dynamic-media-assets}

Il modo in cui distribuisci le risorse Dynamic Media, sia video che immagini, dipende da come viene implementato il sito web.

Dynamic Media offre diverse opzioni:

* Se il tuo sito web è ospitato su Adobe Experience Manager, vuoi aggiungere le risorse Dynamic Media direttamente alla pagina.
* Se il tuo sito web non è su Experience Manager, puoi scegliere:

   * Incorporare il video o l’immagine sul sito web.
   * Collega gli URL all’applicazione web. Utilizza i collegamenti quando desideri distribuire un lettore video come finestra popup o modale.
   * Se il tuo sito è reattivo, puoi [distribuire immagini ottimizzate](/help/assets/responsive-site.md).

>[!NOTE]
>
>L&#39;imaging avanzato funziona con i predefiniti immagine esistenti e utilizza l&#39;intelligenza all&#39;ultimo millisecondo di consegna per ridurre ulteriormente le dimensioni del file immagine in base alla velocità di connessione del browser o della rete. Per ulteriori informazioni, vedere [Smart Imaging](/help/assets/imaging-faq.md).

Per ulteriori informazioni, consulta i seguenti argomenti:

* [Aggiungere risorse Dynamic Media alle pagine web](/help/assets/adding-dynamic-media-assets-to-pages.md)
* [Incorporare il visualizzatore di video o immagini in una pagina web](/help/assets/embed-code.md)
* [Attivazione della protezione hotlinking in Dynamic Media](/help/assets/hotlink-protection.md)
* [Collegamento degli URL all’applicazione Web](/help/assets/linking-urls-to-yourwebapplication.md)
* [Distribuzione di immagini ottimizzate per un sito reattivo](/help/assets/responsive-site.md)
* [Distribuzione di contenuti HTTP2](/help/assets/http2.md)
* [Invalidare la cache CDN tramite Dynamic Media Classic](/help/assets/invalidate-cdn-cache-dm-classic.md)
* [Utilizzo di set di regole per la trasformazione degli URL](/help/assets/using-rulesets-to-transform-urls.md)


## Distribuzione HTTP/2 delle risorse Dynamic Media {#http-delivery-of-dynamic-media-assets}

Experience Manager ora supporta la distribuzione di tutti i contenuti Dynamic Media (immagini e video) tramite HTTP/2. In altre parole, è disponibile un URL pubblicato o un codice di incorporamento per l’immagine o il video da integrare con qualsiasi applicazione che accetta una risorsa in hosting. La risorsa pubblicata viene quindi distribuita tramite il protocollo HTTP/2. Questo metodo di distribuzione migliora il modo in cui browser e server comunicano, consentendo tempi di risposta e di caricamento migliori di tutte le risorse Dynamic Media.

Per ulteriori informazioni, consulta [Domande frequenti sulla distribuzione HTTP/2 del contenuto](/help/sites-administering/scene7-http2faq.md).
