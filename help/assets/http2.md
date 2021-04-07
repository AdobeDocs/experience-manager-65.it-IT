---
title: Distribuzione di contenuti HTTP2
description: HTTP/2 migliora il modo in cui i browser e i server comunicano, consentendo un trasferimento più rapido delle informazioni riducendo al contempo la quantità di potenza di elaborazione necessaria.
uuid: d9deb945-bdf5-4d6b-95c8-8bae4442e618
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: c8e145ad-f021-4043-8190-62151775e296
role: Business Practitioner, Administrator
exl-id: 9eb9f309-33e5-4694-84d2-fb2cd3de50a6
feature: Pubblicazione,Configurazione
translation-type: tm+mt
source-git-commit: c9aec973faf4caef741961d92a6f258646aeddb7
workflow-type: tm+mt
source-wordcount: '726'
ht-degree: 2%

---

# Distribuzione di contenuti HTTP/2 {#http-delivery-of-content}

Adobe è orgogliosa di annunciare la disponibilità della distribuzione HTTP/2 dei contenuti che offre il vantaggio complessivo di prestazioni migliorate.

>[!NOTE]
>
>Questa funzione richiede l’utilizzo della rete CDN preconfigurata fornita con Adobe Experience Manager Dynamic Media. Qualsiasi altra CDN personalizzata non è supportata con questa funzione.

## Cos’è HTTP/2? {#what-is-http}

HTTP/2 migliora il modo in cui i browser e i server comunicano, consentendo un trasferimento più rapido delle informazioni riducendo al contempo la quantità di potenza di elaborazione necessaria.

Il seguente sito web descrive in modo breve e semplice HTTP/2 e i relativi vantaggi:

[https://www.engadget.com/2015/02/24/what-you-need-to-know-about-http-2/](https://www.engadget.com/2015/02/24/what-you-need-to-know-about-http-2/)

## Quali sono i vantaggi principali del passaggio a HTTP/2 per la distribuzione dei contenuti? {#what-are-the-key-benefits-of-moving-to-http-for-content-delivery}

Il miglioramento delle prestazioni può variare notevolmente. Si basa su molti fattori come il codice del tuo sito web, il modo in cui utilizzi Dynamic Media, il dispositivo, lo schermo e la posizione del consumatore.

I test eseguiti da Adobe hanno dato i seguenti risultati:

* Per le immagini, il tempo di risposta è migliorato del 7%-28% a seconda del dispositivo e del browser. I vantaggi più importanti in termini di prestazioni sono stati i dispositivi iOS.
* Per i visualizzatori, le prestazioni del tempo di caricamento sono migliorate del 15%.

La dimostrazione seguente illustra la differenza tra il caricamento HTTP/1 e HTTP/2:

[https://http2.akamai.com/demo](https://http2.akamai.com/demo)

## Posso passare a HTTP/2? {#am-i-eligible-to-switch-over-to-http}

Per utilizzare HTTP/2, è necessario soddisfare i seguenti requisiti:

* Utilizza HTTPS sicuro per le richieste rich media.
* Utilizza la rete CDN (content delivery network) in bundle Adobe come parte della tua licenza Dynamic Media.
* Utilizza un dominio dedicato (non-company-h.assetsadobe#.com).

   Se disponi già di un dominio dedicato, puoi effettuare il consenso tramite il supporto tecnico.

   Se non disponi di un dominio dedicato, Adobe pianifica la transizione a HTTP/2 nel 2018.

## Qual è la procedura per abilitare HTTP/2 per il mio account Dynamic Media? {#what-is-the-process-for-enabling-http-for-my-dynamic-media-account}

Avvii la richiesta per passare a HTTP/2; non viene fatto automaticamente per te.

1. Per passare a HTTP/2, avvia una richiesta di assistenza clienti di Adobe. Consulta [Accesso al portale di supporto AEM](https://helpx.adobe.com/experience-manager/kb/accessing-aem-support-portal.html).

   1. Fornisci le seguenti informazioni nella richiesta di assistenza:

      1. Nome contatto principale, e-mail, telefono.
      1. Tutti i domini da passare a HTTP/2.
      1. Verifica di utilizzare HTTPS protetto per le richieste rich media.
      1. Verifica di utilizzare la CDN tramite Adobe e non sono gestiti con una relazione diretta.
      1. Verifica di utilizzare un dominio dedicato. Se utilizzi Dynamic Media, utilizza un dominio dedicato.
   1. L’Assistenza clienti ti aggiunge all’elenco di attesa dei clienti HTTP/2 in base all’ordine in cui sono state inviate le richieste.
   1. Quando Adobe è pronto per gestire la richiesta, l’Assistenza clienti ti contatta per coordinare la transizione e impostare una data di destinazione.
   1. Ricevi una notifica dopo il completamento e puoi verificare la riuscita della transizione a HTTP2.

      Poiché il browser non dichiara questo fatto, è necessario scaricare un&#39;estensione.

      Per Firefox e Chrome, esiste un&#39;estensione chiamata &quot;HTTP/2 e SPDY Indicator&quot;. I browser supportano solo http/2 in modo sicuro, pertanto è necessario chiamare un URL con https per verificare. Se http/2 è supportato, è indicato dall&#39;estensione sotto forma di un simbolo di Flash blu e un&#39;intestazione &quot;X-Firefox-Spdy&quot; : &quot;h2&quot;.


## Quando posso aspettarmi la transizione verso HTTP/2? {#when-can-i-expect-to-be-transitioned-over-to-http}

Le richieste vengono elaborate nell’ordine in cui vengono ricevute dall’Assistenza clienti.

>[!NOTE]
>
>Ci può essere un lungo lead time perché la transizione a HTTP/2 comporta la cancellazione della cache. Pertanto, è possibile gestire solo alcune transizioni dei clienti alla volta.

## Quali sono i rischi connessi al passaggio a HTTP/2? {#what-are-the-risks-with-moving-to-http}

La transizione a HTTP/2 cancella la cache alla rete CDN perché comporta il passaggio a una nuova configurazione CDN.

Il contenuto non memorizzato nella cache colpisce direttamente i server di origine di Adobe fino a quando la cache non viene ricostruita nuovamente. Di conseguenza, Adobe prevede di gestire alcune transizioni dei clienti alla volta in modo da mantenere prestazioni accettabili durante l’estrazione delle richieste dall’origine.

## Come si verifica se un URL o un sito web è attivato con HTTP/2? {#how-can-you-verify-whether-a-url-or-website-is-activated-with-http}

Poiché il browser non dichiara questo fatto, è necessario scaricare un&#39;estensione.

Per Firefox e Chrome, esiste un&#39;estensione chiamata &quot;HTTP/2 e SPDY Indicator&quot;. I browser supportano solo http/2 in modo sicuro, pertanto è necessario chiamare un URL con https per verificare. Se http/2 è supportato, è indicato dall&#39;estensione sotto forma di un simbolo di Flash blu e un&#39;intestazione `X-Firefox-Spdy` : `h2`.
