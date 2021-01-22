---
title: Domande frequenti sulla distribuzione dei contenuti HTTP2
description: Informazioni sulla distribuzione dei contenuti HTTP2.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
translation-type: tm+mt
source-git-commit: f786b35e77c6b862f7fc6e45d3d0af56a51e3e95
workflow-type: tm+mt
source-wordcount: '773'
ht-degree: 1%

---


# Domande frequenti sulla distribuzione dei contenuti HTTP2{#http-delivery-of-content-faq}

 Adobe è entusiasta di annunciare la disponibilità della distribuzione di contenuti HTTP/2. Con HTTP/2 noterete un aumento complessivo delle prestazioni.

## Cos’è HTTP/2? {#what-is-http}

HTTP/2 migliora il modo in cui i browser e i server comunicano, consentendo un trasferimento più rapido delle informazioni, riducendo al contempo la quantità di potenza di elaborazione necessaria.

Il seguente sito Web descrive HTTP/2 e i relativi vantaggi in modo semplice e breve:

[https://www.engadget.com/2015/02/24/what-you-need-to-know-about-http-2/](https://www.engadget.com/2015/02/24/what-you-need-to-know-about-http-2/)

## Quali sono i vantaggi principali del passaggio a HTTP/2 per la distribuzione dei contenuti? {#what-are-the-key-benefits-of-moving-to-http-for-content-delivery}

I miglioramenti delle prestazioni variano notevolmente in base a fattori quali il codice del sito Web, la modalità di utilizzo di Dynamic Media, il dispositivo, lo schermo e la posizione del consumatore e così via.

 Adobe  proprio test ha prodotto i seguenti risultati:

* Per le immagini, il tempo di risposta è migliorato del 7%-28% a seconda del dispositivo e del browser. I vantaggi più notevoli in termini di prestazioni si sono registrati sui dispositivi iOS.
* Per i visualizzatori, le prestazioni dei tempi di caricamento sono migliorate fino al 15%.

La dimostrazione seguente illustra la differenza tra il caricamento HTTP/1 e HTTP/2:

[https://http2.akamai.com/demo](https://http2.akamai.com/demo)

## Posso passare a HTTP/2? {#am-i-eligible-to-switch-over-to-http}

Per utilizzare HTTP/2, è necessario soddisfare i seguenti requisiti:

* Usa HTTPS sicuro per le tue richieste rich media.
* Utilizzate la rete CDN (rete di distribuzione dei contenuti)  inclusa nel Adobe come parte della licenza Dynamic Media.
* Utilizzate un dominio dedicato (ovvero `images.company.com` o `mycompany.scene7.com`), non un dominio Dynamic Media generico (ovvero `s7d1.scene7.com`, `s7d2.scene7.com` o `s7d13.scene7.com`).

   Per trovare i domini, apri l&#39; [applicazione desktop Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started), quindi accedi al tuo account o account della società. Quindi toccate **[!UICONTROL Configurazione > Impostazione applicazione > Impostazioni generali]**. Cercare il campo con l&#39;etichetta **Nome server pubblicato**. Se utilizzate un dominio Dynamic Media generico, potete richiedere il passaggio al vostro dominio personalizzato come parte di questa transizione.

## Qual è la procedura per abilitare HTTP/2 per l&#39;account Dynamic Media? {#what-is-the-process-for-enabling-http-for-my-scene-account}

1. È necessario [utilizzare il Admin Console  per creare un caso di supporto](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html) e richiedere di passare a HTTP/2; non viene eseguita automaticamente.
1. Fornite le seguenti informazioni nel caso di assistenza:

   * Nome contatto principale, indirizzo e-mail e numero di telefono.
   * Tutti i domini da trasferire a HTTP2. Ovvero `images.company.com` o `mycompany.scene7.com`.

      Per trovare i domini, apri l&#39; [applicazione desktop Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started), quindi accedi al tuo account o account della società. Quindi toccate **[!UICONTROL Configurazione > Impostazione applicazione > Impostazioni generali]**. Cercare il campo con l&#39;etichetta **[!UICONTROL Nome server pubblicato.]**

   * Verificate di utilizzare il protocollo HTTPS protetto per le richieste rich media.
   * Verifica di utilizzare la CDN tramite  Adobe e di non essere gestito con una relazione diretta.
   * Verifica di utilizzare un dominio dedicato. Ovvero, `images.company.com` o `mycompany.scene7.com`, non un dominio Dynamic Media generico come `s7d1.scene7.com`, `s7d2.scene7.com`, `s7d13.scene7.com`.

      Per trovare i domini, apri l&#39; [applicazione desktop Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started), quindi accedi al tuo account o account della società. Quindi toccate **[!UICONTROL Configurazione > Impostazione applicazione > Impostazioni generali]**. Cercare il campo con l&#39;etichetta **[!UICONTROL Nome server pubblicato.]** Se utilizzate un dominio Dynamic Media generico, potete richiedere il passaggio al vostro dominio personalizzato come parte di questa transizione.

1. Il supporto tecnico aggiunge l’utente alla lista di attesa dei clienti HTTP/2 in base all’ordine in cui sono state inviate le richieste.
1. Quando  Adobe è pronto per gestire la richiesta, il supporto vi contatterà per coordinare la transizione e impostare una data di destinazione.
1. Una volta completato il processo, riceverete una notifica e potrete verificare il corretto passaggio a HTTP2.

## Quando è possibile passare a HTTP/2? {#when-can-i-expect-to-be-transitioned-over-to-http}

Le richieste vengono elaborate nell&#39;ordine in cui vengono ricevute dal supporto tecnico.

>[!NOTE]
>
>Il tempo di attesa potrebbe essere lungo perché la transizione a HTTP/2 comporta la cancellazione della cache. Pertanto, è possibile gestire solo alcune transizioni cliente alla volta.

## Quali sono i rischi legati al passaggio a HTTP/2? {#what-are-the-risks-with-moving-to-http}

La transizione a HTTP/2 cancella la cache sulla rete CDN perché comporta il passaggio a una nuova configurazione CDN.

Il contenuto non memorizzato nella cache arriva direttamente  server  origine dei Adobi fino a quando la cache non viene ricreata. Per questo motivo,  Adobe pianifica di gestire alcune transizioni dei clienti alla volta in modo da mantenere prestazioni accettabili quando si richiamano le richieste dalla nostra origine.

## Come verificare se un URL o un sito Web è attivato con HTTP/2? {#how-can-you-verify-whether-a-url-or-website-is-activated-with-http}

È necessario scaricare un&#39;esternalizzazione da utilizzare con il browser Web. Per Firefox e Chrome esiste un&#39;estensione denominata **[!UICONTROL HTTP/2 e SPDY Indicator.]** I browser supportano solo HTTP/2 in modo sicuro, pertanto è necessario richiamare un URL con HTTPS per la verifica. Se HTTP/2 è supportato, questo è indicato dall’estensione sotto forma di simbolo di Flash blu e di intestazione &quot;X-Firefox-Spdy&quot; : &quot;h2&quot;.
