---
title: Smart imaging
description: La tecnologia di imaging intelligente sfrutta le caratteristiche di visualizzazione esclusive di ogni utente per distribuire automaticamente le immagini giuste ottimizzate per la propria esperienza, migliorando le prestazioni e il coinvolgimento.
uuid: c11e52ba-8d64-4dc5-b30a-fc10c2b704e5
contentOwner: Rick Brough
topic-tags: dynamic-media
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
discoiquuid: bf8c6bbd-847d-43d7-9ff4-7231bfd8d107
translation-type: tm+mt
source-git-commit: 0595d89409e0ca21f771be5c55c3ec9548a8449f

---


# Immagini intelligenti {#smart-imaging}

## Cos&#39;è l&#39;imaging intelligente? {#what-is-smart-imaging}

La tecnologia di imaging intelligente sfrutta le caratteristiche di visualizzazione esclusive di ogni utente per distribuire automaticamente le immagini giuste ottimizzate per la propria esperienza, migliorando le prestazioni e il coinvolgimento. La funzione di imaging avanzato funziona con i predefiniti per immagini esistenti e utilizza funzionalità intelligenti all’ultimo millisecondo di distribuzione per ridurre ulteriormente le dimensioni dei file immagine in base alla velocità della connessione di rete o del browser.

La tecnologia di imaging intelligente migliora ulteriormente le prestazioni grazie all&#39;integrazione completa con il miglior servizio CDN avanzato. Questo servizio trova la via Internet ottimale tra server, reti e punti di peer con latenza minima e/o tasso di perdita dei pacchetti rispetto alla route predefinita su Internet.

## Quali sono i vantaggi principali dell&#39;imaging intelligente? {#what-are-the-key-benefits-of-smart-imaging}

La funzione di imaging intelligente migliora le prestazioni di distribuzione delle immagini ottimizzando automaticamente le dimensioni dei file immagine in base alle caratteristiche dell’utente. Poiché le immagini costituiscono la maggior parte del tempo di caricamento di una pagina, il miglioramento delle prestazioni può avere un impatto profondo sui KPI aziendali, come conversione più elevata, tempo trascorso sul sito, tasso di rimbalzo del sito inferiore e così via. Adobe ha confrontato le prestazioni della distribuzione delle immagini predefinita con quelle avanzate per l&#39;imaging nei diversi formati di file, browser e impostazioni di qualità (QLT). Complessivamente, le prestazioni potrebbero aumentare del 22-47% a seconda delle impostazioni del predefinito per immagini esistenti e delle caratteristiche specifiche dell’utente finale.

![image2017-11-14_133226](assets/image2017-11-14_133226.png)

## Esistono costi di licenza associati all&#39;imaging intelligente? {#are-there-any-licensing-costs-associated-with-smart-imaging}

No. La funzione di imaging avanzato è inclusa nella licenza esistente di Dynamic Media Classic (Scene7) o di Dynamic Media. Non vi sono costi aggiuntivi per sfruttare questa nuova funzione.

## Come funziona l&#39;imaging intelligente? {#how-does-smart-imaging-work}

Quando un consumatore richiede per la prima volta un’immagine, verifichiamo le caratteristiche dell’utente e la convertiamo nel formato appropriato in base al browser. Inoltre, vengono create simultaneamente tutte le conversioni di formato che vengono quindi memorizzate nella cache della rete CDN. Quando i consumatori che utilizzano browser diversi richiedono successivamente tale immagine, il formato corretto dell’immagine viene automaticamente distribuito direttamente dalla cache CDN. Queste conversioni di formato vengono effettuate senza perdita di dati e non compromettono la fedeltà visiva. La funzione di imaging intelligente converte automaticamente le immagini in diversi formati, in base alla funzionalità del browser, come segue:

* Converti automaticamente in WebP senza perdita di dati per i browser che supportano il formato WebP, come Chrome, Android e Opera.
* Converti automaticamente in JPEGXR senza perdita di dati per i browser che supportano il formato JPEGXR, ad esempio Internet Explorer 9+.
* Convertite automaticamente in JPEG2000 senza perdita di dati per i browser che supportano il formato JPEG2000, ad esempio Safari.
* Per i browser che non supportano tali formati, viene distribuito il formato immagine originariamente richiesto.

## Quali formati immagine sono supportati? {#what-image-formats-are-supported}

I seguenti formati immagine sono supportati per l’imaging intelligente:

* RGB JPEG
* PNG RGB
* TIFF RGB
* CMYK JPEG
* CMYK TIFF

## Come funziona l’imaging intelligente con i nostri predefiniti per immagini già in uso? {#how-does-smart-imaging-work-with-our-existing-image-presets-that-are-already-in-use}

La funzione di imaging avanzato si basa sui predefiniti per immagini esistenti e osserva praticamente tutte le impostazioni delle immagini, come dimensione, qualità, nitidezza e così via. Ciò che cambia è il formato dell&#39;immagine o, in caso di velocità di connessione di rete lenta, l&#39;impostazione della qualità. Per la conversione del formato, manteniamo la fedeltà visiva completa, come definito dalle impostazioni del predefinito per immagini, ma con file di dimensioni inferiori.

Ad esempio, supponete che un predefinito per immagini sia definito con formato JPEG, dimensioni 500x500, qualità=85 e maschera di contrasto=0.1,1,5. Quando rileviamo che un utente è sul browser Chrome, l&#39;immagine viene convertita in formato WebP senza perdita di dati, con dimensioni 500x500, qualità=85, e maschera di contrasto=0.1,1,5.

## È necessario modificare URL, predefiniti per immagini o distribuire un nuovo codice sul sito per l’imaging intelligente? {#will-i-have-to-change-any-urls-image-presets-or-deploy-any-new-code-on-my-site-for-smart-imaging}

No. La funzione di imaging avanzato si integra perfettamente con gli URL esistenti delle immagini e con i predefiniti per immagini. Inoltre, la funzione di imaging intelligente non richiede l’aggiunta di codice al sito Web per rilevare diverse caratteristiche utente (browser, larghezza di banda, dispositivo e così via). Tutto questo viene gestito automaticamente da Adobe.

L&#39;unica modifica che potrebbe essere necessaria è l&#39;aggiornamento dell&#39;impostazione **[!UICONTROL Ora di vita]** (TTL). Questa impostazione definisce per quanto tempo le risorse vengono memorizzate nella cache dalla rete CDN. Per ottimizzare le prestazioni dell&#39;imaging intelligente, Adobe consiglia di impostare il TTL a 24 ore o più. Per modificare questa impostazione:

* Se utilizzate Dynamic Media Classic, toccate **[!UICONTROL Configurazione > Impostazione applicazione > Impostazione pubblicazione > Server]** immagini. Impostate il valore **[!UICONTROL Default Cache Time To Live]** (Tempo cache client predefinito su Live) su 24 o più.

* Se utilizzate gli elementi multimediali dinamici, seguite le istruzioni per [configurare le impostazioni](config-dynamic.md) delle immagini per gli elementi multimediali dinamici. Impostate il valore di **[!UICONTROL scadenza]** su 24 ore o più.

>[!NOTE]
>
>Se si imposta TTL &lt;= 1 ora, l&#39;imaging intelligente non funziona.

## L&#39;imaging intelligente funziona con HTTPS? E HTTP/2? {#does-smart-imaging-working-with-https-how-about-http}

La funzione di imaging avanzato funziona con le immagini distribuite tramite HTTP o HTTPS. Inoltre, funziona anche su HTTP/2.

## Posso utilizzare la tecnologia di imaging intelligente? {#am-i-eligible-to-use-smart-imaging}

Per utilizzare l’imaging intelligente, l’account della società Dynamic Media Classic o Dynamic Media su AEM deve soddisfare i seguenti requisiti:

* Utilizzate la rete CDN (Content Delivery Network) inclusa nel pacchetto Adobe come parte della licenza.
* Utilizzate un dominio dedicato (ovvero, `images.company.com` o `mycompany.scene7.com`), non un dominio generico (ovvero, `s7d1.scene7.com`, `s7d2.scene7.com`o `s7d13.scene7.com`).

   Per trovare i domini, accedi al tuo account o account della società.

   Toccate **[!UICONTROL Configurazione > Impostazione applicazione > Impostazioni]** generali. Cercate il campo con l’etichetta Nome **[!UICONTROL server]** pubblicato. Se utilizzi un dominio generico, puoi richiedere di passare al dominio personalizzato come parte di questa transizione.

* Non richiedete immagini CMYK JPEG. Nel quadro dell’elaborazione, l’imaging intelligente converte le immagini JPEG CMYK in RGB. Se è necessario ottenere immagini CMYK JPEG, non è possibile utilizzare l’imaging avanzato.

## Qual è la procedura per abilitare l&#39;imaging intelligente per il mio account? {#what-is-the-process-for-enabling-smart-imaging-for-my-account}

È necessario avviare la richiesta per utilizzare l&#39;imaging intelligente; non è abilitata automaticamente.

1. Avviate una richiesta di assistenza tecnica (e-mail: s7support@adobe.com).
1. Nella richiesta di assistenza, fornite le seguenti informazioni:

   1. Nome contatto principale, email, telefono.
   1. Tutti i domini da abilitare per l’imaging intelligente (ovvero, images.company.com o mycompany.scene7.com).

      Per trovare i domini, accedi al tuo account o account della società.

      Fate clic su **[!UICONTROL Configurazione > Impostazione applicazione > Impostazioni]** generali.

      Cercate il campo con l’etichetta Nome **[!UICONTROL server]** pubblicato.
   1. Verifica di utilizzare la CDN tramite Adobe e di non essere gestito con una relazione diretta.
   1. Verifica di utilizzare un dominio dedicato, ad esempio `images.company.com` o `mycompany.scene7.com`, e non un dominio generico, ad esempio `s7d1.scene7.com`, `s7d2.scene7.com`, `s7d13.scene7.com`.

      Per trovare i domini, accedi al tuo account o account della società.

      Fate clic su **[!UICONTROL Configurazione > Impostazione applicazione > Impostazioni]** generali.

      Cercate il campo con l’etichetta Nome **[!UICONTROL server]** pubblicato. Se utilizzate un dominio Dynamic Media Classic generico, potete richiedere il passaggio al dominio personalizzato come parte di questa transizione.
   1. Indicate se è necessario anche questo per lavorare su HTTP/2

1. Il supporto tecnico vi aggiungerà all’elenco di attesa per i clienti con immagini intelligenti in base all’ordine in cui sono state inviate le richieste.
1. Quando Adobe sarà pronta a gestire la richiesta, il supporto vi contatterà per coordinare e impostare una data di destinazione.
1. Facoltativo: Potete provare l&#39;imaging intelligente in Fase di sviluppo prima che Adobe introduca la nuova funzione in produzione.
1. Una volta completato il corso, riceverete una notifica.
1. Per ottimizzare le prestazioni dell&#39;imaging intelligente, Adobe consiglia di impostare l&#39;opzione Time to Live (TTL) su 24 ore o più. Il TTL definisce il tempo in cui le risorse vengono memorizzate nella cache dalla rete CDN. Per modificare questa impostazione:

   1. Se utilizzate Dynamic Media Classic, fate clic su **[!UICONTROL Configurazione > Impostazione applicazione > Impostazione pubblicazione > Server]** immagini. Impostate il valore **[!UICONTROL Default Cache Time To Live]** (Tempo cache client predefinito su Live) su 24 o più.
   1. Se utilizzate Contenuti multimediali dinamici, seguite [queste istruzioni](config-dynamic.md). Impostate il valore **[!UICONTROL Scadenza]** su 24 ore o più.

## Quando posso aspettarmi che il mio account sia abilitato con la tecnologia di imaging intelligente? {#when-can-i-expect-my-account-to-be-enabled-with-smart-imaging}

Le richieste vengono elaborate nell&#39;ordine in cui vengono ricevute dal supporto tecnico, in base all&#39;Elenco di attesa.

>[!NOTE]
Il tempo di attesa potrebbe essere lungo, perché l&#39;attivazione della funzione di imaging intelligente implica la cancellazione della cache. Pertanto, è possibile gestire solo alcune transizioni cliente in un dato momento.

## Quali sono i rischi legati al passaggio al sistema di imaging intelligente? {#what-are-the-risks-with-switching-over-to-use-smart-imaging}

La transizione verso l’imaging intelligente cancella la cache sulla rete CDN perché comporta il passaggio a una nuova configurazione di Dynamic Media Classic o Dynamic Media su AEM.

Durante la transizione iniziale, le immagini non memorizzate nella cache arrivano direttamente sui server di origine Adobe fino alla ricostruzione della cache. Per questo motivo, Adobe pianifica di gestire alcune transizioni tra clienti alla volta, in modo da mantenere prestazioni accettabili quando si richiamano richieste dalla nostra origine. Per la maggior parte dei clienti, la cache è completamente integrata nuovamente alla rete CDN entro circa 1-2 giorni.

## Come posso verificare se la funzione di imaging intelligente funziona come previsto?  {#how-can-i-verify-whether-smart-imaging-is-working-as-expected}

1. Dopo aver configurato l’account con l’imaging intelligente, caricate nel browser l’URL di un’immagine Dynamic Media Classic(S7)/Dynamic Media.
1. Aprite il riquadro per gli sviluppatori di Chrome facendo clic su **[!UICONTROL Visualizza > Sviluppatore > Strumenti]** per sviluppatori nel browser. Oppure scegliete uno strumento di sviluppo browser a vostra scelta.

1. Verificate che la cache sia disattivata quando gli strumenti di sviluppo sono aperti.

   1. In Windows, andate alle impostazioni nel riquadro degli strumenti dello sviluppatore, quindi selezionate la casella di controllo **[!UICONTROL Disattiva cache (mentre i devtools sono aperti)]** .
   1. In Mac, nel riquadro dello sviluppatore, nella scheda **[!UICONTROL Rete]** , selezionate **[!UICONTROL Disattiva cache]** .

1. Nella richiesta iniziale l’immagine non verrà ottimizzata. In genere, sono necessari circa 15 minuti per restituire l’immagine ottimizzata se non è presente nella cache CDN.
1. Osserva il tipo di contenuto viene trasformato nel formato appropriato. La schermata seguente mostra l&#39;immagine PNG convertita dinamicamente in WebP su Chrome.
1. Ripetete questo test su diversi browser e condizioni utente.

>[!NOTE]
Non tutte le immagini sono convertite. L&#39;imaging avanzato decide se la conversione è necessaria per migliorare le prestazioni. In alcuni casi, in assenza di un guadagno di prestazioni previsto, l&#39;immagine non viene convertita.

![image2017-11-14_15398](assets/image2017-11-14_15398.png)

