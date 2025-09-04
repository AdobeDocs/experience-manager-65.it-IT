---
title: Distribuzione HTTP2 dei contenuti
description: Scopri come HTTP/2 migliora il modo in cui browser e server comunicano, consentendo un trasferimento più rapido delle informazioni e riducendo la quantità di potenza di elaborazione necessaria.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
role: User, Admin
exl-id: 9eb9f309-33e5-4694-84d2-fb2cd3de50a6
feature: Publishing,Configuration
solution: Experience Manager, Experience Manager Assets
source-git-commit: f749892bf7fba9889adfc930771178154b92fa5d
workflow-type: tm+mt
source-wordcount: '735'
ht-degree: 3%

---

# Distribuzione HTTP/2 dei contenuti {#http-delivery-of-content}

Adobe è orgogliosa di annunciare la disponibilità della distribuzione HTTP/2 dei contenuti che offre il vantaggio complessivo di prestazioni migliorate.

>[!NOTE]
>
>Questa funzione richiede l’utilizzo della rete CDN preconfigurata inclusa in Adobe Experience Manager Dynamic Media. Qualsiasi altra rete CDN personalizzata non è supportata con questa funzione.

## Cos’è HTTP/2? {#what-is-http}

HTTP/2 migliora il modo in cui browser e server comunicano, consentendo un trasferimento più rapido delle informazioni e riducendo la quantità di potenza di elaborazione necessaria.

Il seguente sito web descrive HTTP/2 e i relativi vantaggi in modo breve e semplice:

[Informazioni su HTTP/2](https://www.engadget.com/2015-02-24-what-you-need-to-know-about-http-2.html)

## Quali sono i vantaggi principali del passaggio a HTTP/2 per la distribuzione dei contenuti? {#what-are-the-key-benefits-of-moving-to-http-for-content-delivery}

Il miglioramento delle prestazioni può variare notevolmente. Si basa su molti fattori, quali il codice del sito web, il modo in cui utilizzi Dynamic Media, il dispositivo, lo schermo e la posizione del consumatore.

I test eseguiti da Adobe hanno prodotto i seguenti risultati:

* Per le immagini, il tempo di risposta è migliorato del 7%-28% a seconda del dispositivo e del browser. I miglioramenti delle prestazioni più importanti si sono verificati sui dispositivi iOS.
* Per i visualizzatori, il tempo di caricamento è aumentato del 15%.

<!--
The following demonstration illustrates the difference between HTTP/1 versus HTTP/2 loading:

[https://http2.akamai.com/demo](https://http2.akamai.com/demo) -->

## Posso passare a HTTP/2? {#am-i-eligible-to-switch-over-to-http}

Per utilizzare HTTP/2, è necessario soddisfare i seguenti requisiti:

* Utilizza HTTPS sicuro per le richieste rich media.
* Utilizza la rete CDN (Content Delivery Network) inclusa in Adobe come parte della licenza Dynamic Media.
* Utilizza un dominio dedicato (non aziendale: h.assetsadobe#.com).

  Se disponi già di un dominio dedicato, puoi dare il consenso tramite l’Assistenza clienti di Adobe.

  Se non disponi di un dominio dedicato, Adobe pianifica di pianificare la transizione a HTTP/2 nel 2018.

## Qual è il processo per abilitare HTTP/2 per il mio account Dynamic Media? {#what-is-the-process-for-enabling-http-for-my-dynamic-media-account}

La richiesta di passare a HTTP/2 viene avviata automaticamente, ma non eseguita automaticamente.

1. Per passare a HTTP/2, avvia una richiesta di assistenza clienti Adobe. Vedere [Aprire un ticket di supporto](https://experienceleague.adobe.com/it?support-solution=General&lang=en&support-tab=home#support).

   1. Fornisci le seguenti informazioni nella richiesta di supporto:

      1. Nome del contatto principale, e-mail, telefono.
      1. Tutti i domini da trasferire su HTTP/2.
      1. Verifica di utilizzare HTTPS sicuro per le richieste rich media.
      1. Verifica di utilizzare la rete CDN tramite Adobe e di non essere gestita con una relazione diretta.
      1. Verifica di utilizzare un dominio dedicato. Se utilizzi Dynamic Media, utilizza un dominio dedicato.

   1. L’Assistenza clienti ti aggiunge alla lista di attesa dei clienti HTTP/2 in base all’ordine in cui sono state inviate le richieste.
   1. Quando Adobe è pronto a gestire la richiesta, l’Assistenza clienti ti contatta per coordinare la transizione e impostare una data di scadenza.
   1. Riceverai una notifica dopo il completamento e potrai verificare se la transizione a HTTP2 è andata a buon fine.

      Poiché il browser non dichiara questo fatto, è necessario scaricare un’estensione.

      Per Firefox e Chrome, c&#39;è un&#39;estensione chiamata &quot;HTTP/2 and SPDY Indicator&quot;. I browser supportano solo http/2 in modo sicuro, pertanto è necessario chiamare un URL con https per verificare. Se http/2 è supportato, l’estensione indica i. L&#39;estensione è sotto forma di un simbolo Flash blu e di un&#39;intestazione `X-Firefox-Spdy` : `h2`.

## Quando posso aspettarmi che avvenga la transizione a HTTP/2? {#when-can-i-expect-to-be-transitioned-over-to-http}

Le richieste vengono elaborate in base all’ordine in cui l’Assistenza clienti le riceve.

>[!NOTE]
>
>Ci può essere un lead time lungo perché la transizione a HTTP/2 comporta la cancellazione della cache. Pertanto, è possibile gestire solo poche transizioni cliente alla volta.

## Quali sono i rischi associati al passaggio a HTTP/2? {#what-are-the-risks-with-moving-to-http}

La transizione a HTTP/2 cancella la cache sulla rete CDN perché comporta lo spostamento a una nuova configurazione della rete CDN.

Il contenuto non memorizzato in cache colpisce direttamente i server di origine di Adobe fino a quando la cache non viene nuovamente generata. Adobe prevede quindi di gestire alcune transizioni cliente alla volta in modo da mantenere prestazioni accettabili durante il richiamo delle richieste dall’origine.

## Come verificare se un URL o un sito web è attivato con HTTP/2? {#how-can-you-verify-whether-a-url-or-website-is-activated-with-http}

Poiché il browser non dichiara questo fatto, è necessario scaricare un’estensione.

Per Firefox e Chrome, c&#39;è un&#39;estensione chiamata &quot;HTTP/2 and SPDY Indicator&quot;. I browser supportano solo http/2 in modo sicuro, pertanto è necessario chiamare un URL con https per verificare. Se http/2 è supportato, l&#39;estensione lo indica. L&#39;estensione è sotto forma di un simbolo Flash blu e di un&#39;intestazione `X-Firefox-Spdy` : `h2`.
