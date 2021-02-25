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
source-git-commit: 729fbf3a97d3ae3bc91204f8831fd115d9d77f20
workflow-type: tm+mt
source-wordcount: '718'
ht-degree: 0%

---


# HTTP/2 Distribuzione dei contenuti {#http-delivery-of-content}

 Adobe è entusiasta di annunciare la disponibilità della distribuzione di contenuti HTTP/2 con il vantaggio complessivo di prestazioni migliorate.

>[!NOTE]
>
>I clienti devono utilizzare la rete CDN (Content Deliver Network) fornita con Adobe Experience Manager Dynamic Media per beneficiare della distribuzione dei contenuti HTTP/2.

## Cos’è HTTP/2? {#what-is-http}

HTTP/2 migliora il modo in cui i browser e i server comunicano, consentendo un trasferimento più rapido delle informazioni, riducendo al contempo la quantità di potenza di elaborazione necessaria.

Il seguente sito Web descrive HTTP/2 e i relativi vantaggi in modo semplice e breve:

[https://www.engadget.com/2015/02/24/what-you-need-to-know-about-http-2/](https://www.engadget.com/2015/02/24/what-you-need-to-know-about-http-2/)

## Quali sono i vantaggi principali del passaggio a HTTP/2 per la distribuzione dei contenuti? {#what-are-the-key-benefits-of-moving-to-http-for-content-delivery}

Il miglioramento delle prestazioni può variare notevolmente. È basato su molti fattori come il codice del sito Web, la modalità di utilizzo di Dynamic Media, il dispositivo, lo schermo e la posizione del consumatore.

 Adobe  proprio test ha prodotto i seguenti risultati:

* Per le immagini, il tempo di risposta è migliorato del 7%-28% a seconda del dispositivo e del browser. I vantaggi più notevoli in termini di prestazioni si sono registrati sui dispositivi iOS.
* Per i visualizzatori, le prestazioni dei tempi di caricamento sono migliorate fino al 15%.

La dimostrazione seguente illustra la differenza tra il caricamento HTTP/1 e HTTP/2:

[https://http2.akamai.com/demo](https://http2.akamai.com/demo)

## Posso passare a HTTP/2? {#am-i-eligible-to-switch-over-to-http}

Per utilizzare HTTP/2, è necessario soddisfare i seguenti requisiti:

* Usa HTTPS sicuro per le tue richieste rich media.
* Utilizzate la rete CDN (rete di distribuzione dei contenuti)  inclusa nel Adobe come parte della licenza Dynamic Media.
* Utilizzate un dominio dedicato (non-company-h.assetsadobe#.com).

   Se disponete già di un dominio dedicato, potete scegliere il servizio di assistenza tecnica.

   Se non disponete di un dominio dedicato,  Adobe pianifica di pianificare la transizione a HTTP/2 nel 2018.

## Qual è la procedura per abilitare HTTP/2 per l&#39;account Dynamic Media? {#what-is-the-process-for-enabling-http-for-my-dynamic-media-account}

Avviate la richiesta per passare a HTTP/2; non viene eseguita automaticamente.

1. Per passare a HTTP/2, avvia una richiesta di assistenza clienti  Adobe. Consultate [Accesso al portale di supporto AEM](https://helpx.adobe.com/experience-manager/kb/accessing-aem-support-portal.html).

   1. Nella richiesta di assistenza, fornite le seguenti informazioni:

      1. Nome contatto principale, email, telefono.
      1. Tutti i domini da trasferire a HTTP/2.
      1. Verificate di utilizzare il protocollo HTTPS protetto per le richieste rich media.
      1. Verifica di utilizzare il CDN tramite  Adobe e di non essere gestito con una relazione diretta.
      1. Verifica di utilizzare un dominio dedicato. Se usi Dynamic Media, usi un dominio dedicato.
   1. L&#39;Assistenza clienti aggiunge all&#39;elenco di attesa dei clienti HTTP/2 in base all&#39;ordine in cui sono state inviate le richieste.
   1. Quando  Adobe è pronto per gestire la richiesta, l&#39;Assistenza clienti ti contatta per coordinare la transizione e impostare una data di destinazione.
   1. Dopo il completamento dell&#39;operazione, riceverete una notifica e potrete verificare il corretto passaggio a HTTP2.

      Poiché il browser non dichiara questo fatto, è necessario scaricare un&#39;estensione.

      Per Firefox e Chrome, esiste un&#39;estensione chiamata &quot;HTTP/2 e SPDY Indicator&quot;. I browser supportano solo http/2 in modo sicuro, pertanto è necessario chiamare un URL con https per verificare. Se http/2 è supportato, è indicato dall&#39;estensione sotto forma di simbolo di Flash blu e di intestazione &quot;X-Firefox-Spdy&quot; : &quot;h2&quot;.


## Quando è possibile passare a HTTP/2? {#when-can-i-expect-to-be-transitioned-over-to-http}

Le richieste vengono elaborate nell&#39;ordine in cui vengono ricevute dall&#39;Assistenza clienti.

>[!NOTE]
>
>I tempi di attesa possono essere lunghi perché la transizione a HTTP/2 comporta la cancellazione della cache. Pertanto, è possibile gestire solo alcune transizioni cliente alla volta.

## Quali sono i rischi legati al passaggio a HTTP/2? {#what-are-the-risks-with-moving-to-http}

La transizione a HTTP/2 cancella la cache sulla rete CDN perché comporta il passaggio a una nuova configurazione CDN.

Il contenuto non memorizzato nella cache arriva direttamente  server  origine dei Adobi fino a quando la cache non viene ricreata. Come tale,  Adobe pianifica di gestire alcune transizioni dei clienti alla volta in modo da mantenere prestazioni accettabili quando si richiamano le richieste dall&#39;origine.

## Come verificare se un URL o un sito Web è attivato con HTTP/2? {#how-can-you-verify-whether-a-url-or-website-is-activated-with-http}

Poiché il browser non dichiara questo fatto, è necessario scaricare un&#39;estensione.

Per Firefox e Chrome, esiste un&#39;estensione chiamata &quot;HTTP/2 e SPDY Indicator&quot;. I browser supportano solo http/2 in modo sicuro, pertanto è necessario chiamare un URL con https per verificare. Se http/2 è supportato, è indicato dall&#39;estensione sotto forma di simbolo di Flash blu e di intestazione `X-Firefox-Spdy` : `h2`.
