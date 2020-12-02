---
title: HTTP2 Distribuzione dei contenuti
description: HTTP/2 migliora il modo in cui i browser e i server comunicano, consentendo un trasferimento più rapido delle informazioni e riducendo al contempo la quantità di potenza di elaborazione necessaria.
uuid: d9deb945-bdf5-4d6b-95c8-8bae4442e618
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: c8e145ad-f021-4043-8190-62151775e296
translation-type: tm+mt
source-git-commit: 0595d89409e0ca21f771be5c55c3ec9548a8449f
workflow-type: tm+mt
source-wordcount: '705'
ht-degree: 0%

---


# HTTP2 Distribuzione di contenuto {#http-delivery-of-content}

 Adobe è entusiasta di annunciare la disponibilità della distribuzione di contenuti HTTP/2 con il vantaggio complessivo di prestazioni migliorate.

## Cos’è HTTP/2? {#what-is-http}

HTTP/2 migliora il modo in cui i browser e i server comunicano, consentendo un trasferimento più rapido delle informazioni, riducendo al contempo la quantità di potenza di elaborazione necessaria.

Il seguente sito Web descrive HTTP/2 e i relativi benefici in modo semplice e breve:

[https://www.engadget.com/2015/02/24/what-you-need-to-know-about-http-2/](https://www.engadget.com/2015/02/24/what-you-need-to-know-about-http-2/)

## Quali sono i vantaggi principali del passaggio a HTTP/2 per la distribuzione dei contenuti? {#what-are-the-key-benefits-of-moving-to-http-for-content-delivery}

Il miglioramento delle prestazioni varia notevolmente in base a fattori quali il codice del sito Web, la modalità di utilizzo di Dynamic Media, il dispositivo, lo schermo e la posizione del consumatore e così via.

 Adobe  proprio test ha prodotto i seguenti risultati:

* Per le immagini, il tempo di risposta è migliorato del 7%-28% a seconda del dispositivo e del browser. I vantaggi più notevoli in termini di prestazioni si sono registrati sui dispositivi iOS.
* Per i visualizzatori, le prestazioni dei tempi di caricamento sono migliorate fino al 15%.

La dimostrazione seguente illustra la differenza tra il caricamento HTTP/1 e HTTP/2:

[https://http2.akamai.com/demo](https://http2.akamai.com/demo)

## Posso passare a HTTP/2? {#am-i-eligible-to-switch-over-to-http}

Per utilizzare HTTP/2, è necessario soddisfare i seguenti requisiti:

* Usa HTTPS sicuro per le tue richieste rich media.
* Utilizza la rete CDN (rete di distribuzione dei contenuti)  Adobe inclusa nella licenza per contenuti multimediali dinamici.
* Utilizzate un dominio dedicato (non-company-h.assetsadobe#.com).

   Se disponete già di un dominio dedicato, potete scegliere di utilizzare il supporto tecnico.

   Se non disponete di un dominio dedicato,  Adobe pianificherà la transizione a HTTP/2 nel 2018.

## Qual è la procedura per abilitare HTTP/2 per l&#39;account Dynamic Media? {#what-is-the-process-for-enabling-http-for-my-dynamic-media-account}

È necessario avviare la richiesta per passare a HTTP/2; non viene eseguita automaticamente.

1. Avviate una richiesta di assistenza tecnica per passare a HTTP2. Consultate [Accesso al portale di supporto AEM](https://helpx.adobe.com/experience-manager/kb/accessing-aem-support-portal.html).

   1. Nella richiesta di assistenza, fornite le seguenti informazioni:

      1. Nome contatto principale, email, telefono.
      1. Tutti i domini da trasferire a HTTP2.
      1. Verifica di utilizzare HTTPS protetto per le richieste rich media.
      1. Verifica di utilizzare la CDN tramite  Adobe e di non essere gestito con una relazione diretta.
      1. Verifica di utilizzare un dominio dedicato. Se utilizzi Dynamic Media, utilizzi già un dominio dedicato.
   1. Il supporto tecnico vi aggiunge alla lista di attesa dei clienti HTTP/2 in base all&#39;ordine in cui sono state inviate le richieste.
   1. Quando  Adobe è pronto per gestire la richiesta, il supporto vi contatterà per coordinare la transizione e impostare una data di destinazione.
   1. Riceverai una notifica dopo il completamento e potrai verificare il corretto passaggio a HTTP2.

      Poiché il browser non dichiara questo fatto, è necessario scaricare un&#39;estensione.

      Per Firefox e Chrome esiste un&#39;estensione chiamata &quot;HTTP/2 e SPDY Indicator&quot;. I browser supportano solo http/2 in modo sicuro, pertanto è necessario chiamare un URL con https per verificare. Se http/2 è supportato, questo è indicato dall&#39;estensione sotto forma di simbolo di Flash blu e di intestazione &quot;X-Firefox-Spdy&quot; : &quot;h2&quot;.


## Quando è possibile passare a HTTP/2? {#when-can-i-expect-to-be-transitioned-over-to-http}

Le richieste verranno elaborate nell&#39;ordine in cui sono ricevute dal supporto tecnico.

>[!NOTE]
>
>Il tempo di attesa potrebbe essere lungo perché la transizione a HTTP/2 comporta la cancellazione della cache. Pertanto, è possibile gestire solo alcune transizioni cliente alla volta.

## Quali sono i rischi legati al passaggio a HTTP/2? {#what-are-the-risks-with-moving-to-http}

La transizione a HTTP/2 cancella la cache sulla rete CDN perché comporta il passaggio a una nuova configurazione CDN.

Il contenuto non memorizzato nella cache arriva direttamente  server  origine dei Adobi fino a quando la cache non viene ricreata. Per questo motivo,  Adobe pianifica di gestire alcune transizioni dei clienti alla volta in modo da mantenere prestazioni accettabili quando si richiamano le richieste dalla nostra origine.

## Come verificare se un URL o un sito Web è attivato con HTTP/2? {#how-can-you-verify-whether-a-url-or-website-is-activated-with-http}

Poiché il browser non dichiara questo fatto, è necessario scaricare un&#39;estensione.

Per Firefox e Chrome esiste un&#39;estensione chiamata &quot;HTTP/2 e SPDY Indicator&quot;. I browser supportano solo http/2 in modo sicuro, pertanto è necessario chiamare un URL con https per verificare. Se http/2 è supportato, questo è indicato dall&#39;estensione sotto forma di simbolo di Flash blu e di intestazione &quot;X-Firefox-Spdy&quot; : &quot;h2&quot;.
