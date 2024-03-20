---
title: 'AEM: Domande frequenti sull’integrazione con Commerce tramite Commerce Integration Framework'
description: 'AEM: Domande frequenti sull’integrazione con Commerce tramite Commerce Integration Framework'
exl-id: d541607f-c4c9-4dd5-aadf-64d4cb5f9f2a
solution: Experience Manager,Commerce
source-git-commit: 1751bfb32386685e3a159939113b9667b5e17f0e
workflow-type: tm+mt
source-wordcount: '956'
ht-degree: 66%

---

# AEM: Domande frequenti sull’integrazione con Commerce tramite Commerce Integration Framework

## 1. CIF GraphQL è utilizzato solo per il commercio o è disponibile per eseguire query sui contenuti creati con AEM JCR?

Adobe ha adottato le API GraphQL di Adobe Commerce come API Commerce ufficiali per tutti i dati relativi all’e-commerce. Quindi, AEM utilizza GraphQL per scambiare dati di e-commerce con Adobe Commerce e con qualsiasi motore di e-commerce tramite I/O Runtime. Questa API GraphQL è indipendente dall’API GraphQL di AEM per accedere ai frammenti di contenuto.

## 2. È possibile memorizzare le risorse dei prodotti (immagini) e farvi riferimento da AEM tramite le funzioni di amministrazione di Adobe Commerce? Come possono essere utilizzate le risorse da Dynamic Media?

Non è disponibile alcuna integrazione ufficiale AEM Assets - Adobe Commerce. È disponibile un connettore per i partner su [marketplace](https://marketplace.magento.com/partner/bounteous_ecomm).

In alternativa, come soluzione alternativa, puoi memorizzare le risorse dei prodotti (immagini) in AEM Assets, ma devi memorizzare manualmente gli URL delle risorse in Adobe Commerce. Dynamic Medie fa parte di AEM Assets e funziona allo stesso modo.

## 3. Ha importanza dove viene implementata la soluzione Commerce? (on-premise o nel cloud)

No, non ha importanza dove viene implementata la soluzione Commerce. L&#39;CIF e la vetrina dell&#39;AEM lavorano indipendentemente dal modello di implementazione. Tuttavia, se la soluzione viene implementata con l’architettura di riferimento E2E consigliata, i test E2E possono essere eseguiti in base ai KPI delle prestazioni che rappresentano un tipico profilo cliente di un’azienda. Questo processo fornisce informazioni aggiuntive che possono essere utilizzate come benchmark.

## 4. In che modo vengono create le pagine di catalogo o di prodotto in AEM? Come persistono in AEM?

Le pagine di catalogo e di prodotto vengono create e memorizzate nella cache in AEM in base a modelli generici per pagine di catalogo e di prodotto. Nessun dato di prodotto o catalogo viene importato e memorizzato in AEM.

## 5. Quando si aggiornano i dati di prodotti nella soluzione Commerce, questi vengono trasmessi in tempo reale ad AEM? Oppure si tratta di un’elaborazione in batch?

Il componente aggiuntivo CIF utilizzato con AEM consente il flusso di dati dalla soluzione commerce all’AEM on-demand. Pertanto, questo flusso di lavoro non è un processo push in tempo reale o batch se è presente un aggiornamento nella soluzione commerce.

## 6. Quali sono le dimensioni del catalogo supportate da AEM con CIF?

Il supporto per la dimensione del catalogo dipende da alcuni aspetti aggiuntivi da considerare. Qual è il rapporto di cache dei dati e delle pagine del catalogo? Quante richieste simultanee prevedi durante le ore di punta? Quanto sono scalabili le API delle soluzioni Commerce?

## 7. Che ruolo svolge un sistema PIM in questo framework?

I dati PIM vengono esposti all’AEM e ai client tramite richieste GraphQL. Adobe consiglia di integrare un sistema PIM con il motore di e-commerce (Adobe Commerce o altri) in modo che i dati PIM possano essere recuperati dal motore di e-commerce.

## 8. È possibile memorizzare nella cache anche i prezzi e altri dati tramite Dispatcher? Questo potrebbe comportare problemi di invalidazione frequente della cache?

I dati dinamici come prezzo o inventario non vengono memorizzati nella cache di Dispatcher. I dati dinamici vengono recuperati lato client con i componenti Web direttamente tramite le API GraphQL. Nella cache di Dispatcher vengono memorizzati solo i dati statici (come i dati di prodotto o categoria). Se i dati del prodotto cambiano, è necessario annullare la validità della cache.

## 9. Come funziona l’annullamento della validità della cache per il Dispatcher AEM con AEM e Commerce?

Adobe consiglia di impostare l’annullamento della validità della cache basata su TTL per le pagine memorizzate nella cache di Dispatcher. Per informazioni dinamiche come prezzo o azioni, Adobe consiglia di eseguire il rendering della data lato client. Per ulteriori informazioni sull’invalidazione della cache basata su TTL, consulta [Dispatcher AEM](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17458.html?lang=it)

## 10. Vi sono consigli sulla ricerca unificata nei contenuti AEM con Commerce?

Viene fornita un’implementazione di riferimento per la ricerca di prodotti, ma non viene eseguita alcuna ricerca unificata con i contenuti. Questa funzione è specifica per il cliente e può essere risolta meglio a livello di progetto.

## 11. Come funziona la ricerca con AEM e Commerce utilizzando CIF?

CIF fornisce i componenti Barra di ricerca e Risultati di ricerca. Il componente Barra di ricerca invia una richiesta GraphQL con il termine di ricerca alla soluzione Commerce, che restituisce un elenco di prodotti che include nome del prodotto, prezzo, SLUG e così via. Il componente Risultato di ricerca visualizza quindi i risultati della ricerca in una visualizzazione a galleria su una pagina di risultati di ricerca creata su AEM. Il componente Ricerca supporta la ricerca full-text. Utilizza la chiave SLUG/url per creare un riferimento al PDP.

## 12. Come possono essere utilizzati i dati di prodotto in MSM o nelle traduzioni?

I dati del prodotto sono generalmente già tradotti in PIM o in Adobe Commerce. L’integrazione AEM - Adobe Commerce supporta la connessione a più store e viste store di Adobe Commerce. In genere, in una configurazione MSM un sito AEM è collegato a una vista store di Adobe Commerce.

## 13. Esiste un modo per migliorare i dati di prodotto con testo commerciale? In caso affermativo, dove? In AEM o nella soluzione Commerce?

L’Adobe consiglia di gestire i dati e i contenuti relativi al marketing nell’AEM. Arricchisci i dati di prodotto dalla soluzione Commerce con attributi aggiuntivi utilizzando Frammenti di contenuto oppure crea e collega Frammenti di esperienza per contenuti non strutturati con i tuoi prodotti.

## 14. In che modo un&#39;azienda garantisce la conformità PCI quando utilizza l&#39;AEM per l&#39;intero livello di presentazione?

Adobe consiglia di utilizzare metodi di pagamento astratti. In questo modo il client browser comunica direttamente con il provider del gateway dei pagamenti e Adobe non mantiene o trasmette la data del titolare della carta né le soluzioni commerce. Questo approccio richiede solo una conformità PCI di livello 3. Tuttavia, vi sono altri elementi da considerare per assicurare la piena conformità allo standard PCI, come il modo in cui i dipendenti interagiscono con il sistema e i dati. Per ulteriori informazioni sulla conformità PCI di Adobe Commerce, consulta [Conformità PCI](https://business.adobe.com/it/products/magento/pci-compliance.html)

## 15. Se vengono utilizzate le versioni AEM e Adobe Commerce Cloud, questa soluzione congiunta è conforme allo standard PCI?

Sì, il questionario di autovalutazione D e l’attestato di conformità sono disponibili su richiesta.

## 16. Come è possibile richiedere una licenza di prova di I/O Runtime?

Per richiedere una licenza di prova per utilizzare I/O Runtime, visita [questa pagina](https://adobeio.typeform.com/to/obqgRm).
