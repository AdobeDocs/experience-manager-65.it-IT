---
title: Distribuire elementi multimediali dinamici
description: Scopri come distribuire risorse Dynamic Medie, come video e immagini, alle pagine web.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
docset: aem65
role: User, Admin
exl-id: 274af114-845a-46bd-b091-802cf589687a
feature: Asset Management,Renditions
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 9%

---

# Distribuire elementi multimediali dinamici{#delivering-dynamic-media-assets}

Il modo in cui distribuisci le risorse Dynamic Medie, sia video che immagini, dipende da come viene implementato il sito web.

Dynamic Medie offre diverse opzioni:

* Se il tuo sito web è ospitato su Adobe Experience Manager, vuoi aggiungere le risorse Dynamic Medie direttamente alla pagina.
* Se il tuo sito web non è sull’Experience Manager, puoi scegliere:

   * Incorporare il video o l’immagine sul sito web.
   * Collega gli URL all’applicazione web. Utilizza i collegamenti quando desideri distribuire un lettore video come finestra popup o modale.
   * Se il tuo sito è reattivo, puoi [distribuire immagini ottimizzate](/help/assets/responsive-site.md).

>[!NOTE]
>
>L&#39;imaging avanzato funziona con i predefiniti immagine esistenti e utilizza l&#39;intelligenza all&#39;ultimo millisecondo di consegna per ridurre ulteriormente le dimensioni del file immagine in base alla velocità di connessione del browser o della rete. Per ulteriori informazioni, vedere [Smart Imaging](/help/assets/imaging-faq.md).

Per ulteriori informazioni, consulta i seguenti argomenti:

* [Aggiungere risorse Dynamic Medie alle pagine web](/help/assets/adding-dynamic-media-assets-to-pages.md)
* [Incorporare il visualizzatore di video o immagini in una pagina web](/help/assets/embed-code.md)
* [Attivazione della protezione hotlinking in Dynamic Media](/help/assets/hotlink-protection.md)
* [Collegamento degli URL all’applicazione Web](/help/assets/linking-urls-to-yourwebapplication.md)
* [Distribuzione di immagini ottimizzate per un sito reattivo](/help/assets/responsive-site.md)
* [Distribuzione HTTP2 dei contenuti](/help/assets/http2.md)
* [Invalidare la cache CDN tramite Dynamic Media Classic](/help/assets/invalidate-cdn-cache-dm-classic.md)
* [Utilizzo di set di regole per la trasformazione degli URL](/help/assets/using-rulesets-to-transform-urls.md)


## Distribuzione HTTP/2 delle risorse Dynamic Medie {#http-delivery-of-dynamic-media-assets}

Experience Manager ora supporta la distribuzione di tutti i contenuti Dynamic Medie (immagini e video) tramite HTTP/2. In altre parole, è disponibile un URL pubblicato o un codice di incorporamento per l’immagine o il video da integrare con qualsiasi applicazione che accetta una risorsa in hosting. La risorsa pubblicata viene quindi distribuita tramite il protocollo HTTP/2. Questo metodo di distribuzione migliora il modo in cui browser e server comunicano, consentendo tempi di risposta e di caricamento migliori per tutte le risorse Dynamic Medie.

Per ulteriori informazioni, consulta [Domande frequenti sulla distribuzione HTTP/2 del contenuto](/help/sites-administering/scene7-http2faq.md).
