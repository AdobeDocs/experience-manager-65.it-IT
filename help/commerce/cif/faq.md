---
title: 'AEM: Domande frequenti sull’integrazione con Commerce tramite Commerce Integration Framework'
description: 'AEM: Domande frequenti sull’integrazione con Commerce tramite Commerce Integration Framework'
exl-id: d541607f-c4c9-4dd5-aadf-64d4cb5f9f2a
solution: Experience Manager,Commerce
feature: Commerce Integration Framework
role: Admin, Developer
source-git-commit: f30decf0e32a520dcda04b89c5c1f5b67ab6e028
workflow-type: tm+mt
source-wordcount: '998'
ht-degree: 51%

---

# AEM: Domande frequenti sull’integrazione con Commerce tramite Commerce Integration Framework

## &#x200B;1. CIF GraphQL è utilizzato solo per l’e-commerce o è disponibile per eseguire query sui contenuti creati con AEM JCR?

Adobe ha adottato le API GraphQL di Adobe Commerce come API Commerce ufficiali per tutti i dati relativi all’e-commerce. Quindi, AEM utilizza GraphQL per scambiare dati di e-commerce con Adobe Commerce e con qualsiasi motore di e-commerce tramite I/O Runtime. Questa API GraphQL è indipendente dall’API GraphQL di AEM per accedere ai frammenti di contenuto.

## &#x200B;2. È possibile archiviare le risorse dei prodotti (immagini) e farvi riferimento da AEM tramite l’amministratore Adobe Commerce? Come possono essere utilizzate le risorse da Dynamic Media?

Non è disponibile alcuna integrazione ufficiale AEM Assets - Adobe Commerce. Connettore partner disponibile nel [marketplace](https://marketplace.magento.com/partner/bounteous_ecomm).

In alternativa, come soluzione alternativa, puoi memorizzare le risorse dei prodotti (immagini) in AEM Assets, ma devi memorizzare manualmente gli URL delle risorse in Adobe Commerce. Dynamic Media fa parte di AEM Assets e funziona allo stesso modo.

## &#x200B;3. Importa dove viene implementata la soluzione commerce? (on-premise o nel cloud)

No, non ha importanza dove viene implementata la soluzione per l’e-commerce. CIF e la vetrina AEM funzionano indipendentemente dal modello di distribuzione. Tuttavia, se la soluzione viene implementata con l’architettura di riferimento E2E consigliata, i test E2E possono essere eseguiti in base ai KPI delle prestazioni che rappresentano un tipico profilo cliente di un’azienda. Questo processo fornisce informazioni aggiuntive che possono essere utilizzate come benchmark.

## &#x200B;4. Come vengono create le pagine di catalogo o di prodotto in AEM? Come persistono in AEM?

Le pagine di catalogo e di prodotto vengono create e memorizzate nella cache in AEM in base a modelli generici per pagine di catalogo e di prodotto. Nessun dato di prodotto o catalogo viene importato e memorizzato in AEM.

## &#x200B;5. Quando aggiorni i dati di prodotto nella tua soluzione commerce, si tratta di un push in tempo reale ad AEM? Oppure si tratta di un’elaborazione in batch?

Il componente aggiuntivo CIF utilizzato con AEM consente il flusso di dati dalla soluzione commerce ad AEM on-demand. Pertanto, questo flusso di lavoro non è un processo push in tempo reale o batch se è presente un aggiornamento nella soluzione commerce.

## &#x200B;6. Quali sono le dimensioni del catalogo supportate da AEM con CIF?

Il supporto per la dimensione del catalogo dipende da alcuni aspetti aggiuntivi da considerare. Qual è il rapporto di cache dei dati e delle pagine del catalogo? Quante richieste simultanee prevedi durante le ore di punta? Quanto sono scalabili le API delle soluzioni per l’e-commerce?

## &#x200B;7. Qual è il ruolo di PIM in questo framework?

I dati PIM vengono esposti ad AEM e ai client tramite richieste GraphQL. Adobe consiglia di integrare un sistema PIM con il motore di e-commerce (Adobe Commerce o altri) in modo che i dati PIM possano essere recuperati dal motore di e-commerce.

## &#x200B;8. È possibile memorizzare nella cache anche i prezzi e altri dati tramite Dispatcher? Questo potrebbe comportare problemi di invalidazione frequente della cache?

I dati dinamici come prezzo o inventario non vengono memorizzati nella cache di Dispatcher. I dati dinamici vengono recuperati lato client con i componenti Web direttamente tramite le API GraphQL. Nella cache di Dispatcher vengono memorizzati solo i dati statici (come i dati di prodotto o categoria). Se i dati del prodotto cambiano, è necessario annullare la validità della cache.

## &#x200B;9. Come funziona l’annullamento della validità della cache per AEM Dispatcher con AEM e commerce?

Adobe consiglia di impostare l’annullamento della validità della cache basata su TTL per le pagine memorizzate nella cache di Dispatcher. Per informazioni dinamiche come prezzo o azioni, Adobe consiglia di eseguire il rendering della data lato client. Per ulteriori informazioni sull&#39;annullamento della validità della cache basata su TTL, vedere [AEM Dispatcher](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17458.html?lang=it)

## &#x200B;10. Esistono consigli sulla ricerca unificata nei contenuti AEM con Commerce?

Viene fornita un’implementazione di riferimento per la ricerca di prodotti, ma non viene eseguita alcuna ricerca unificata con i contenuti. Questa funzione è specifica per il cliente e può essere risolta meglio a livello di progetto.

## &#x200B;11. Come funziona la ricerca con AEM e Commerce utilizzando CIF?

CIF fornisce i componenti Barra di ricerca e Risultati di ricerca. Il componente Barra di ricerca invia una richiesta GraphQL con il termine di ricerca alla soluzione per l’e-commerce, che restituisce un elenco di prodotti che include nome del prodotto, prezzo, SLUG e così via. Il componente Risultato di ricerca visualizza quindi i risultati della ricerca in una visualizzazione a galleria su una pagina di risultati di ricerca creata su AEM. Il componente Ricerca supporta la ricerca full-text. Utilizza la chiave SLUG/url per creare un riferimento al PDP.

## &#x200B;12. Come possono essere utilizzati i dati di prodotto in MSM o nelle traduzioni?

I dati del prodotto sono generalmente già tradotti in PIM o in Adobe Commerce. L’integrazione AEM - Adobe Commerce supporta la connessione a più store e viste store di Adobe Commerce. In genere, in una configurazione MSM un sito AEM è collegato a una vista store di Adobe Commerce.

## &#x200B;13. Esiste un modo per migliorare i dati del prodotto con testo commerciale? In caso affermativo, dove? In AEM o nella soluzione per l’e-commerce?

Adobe consiglia di gestire i dati e i contenuti relativi al marketing in AEM. Arricchisci i dati di prodotto dalla soluzione Commerce con attributi aggiuntivi utilizzando Frammenti di contenuto oppure crea e collega Frammenti di esperienza per contenuti non strutturati con i tuoi prodotti.

## &#x200B;14. In che modo un’azienda garantisce la conformità PCI quando utilizza AEM per l’intero livello di presentazione?

Adobe consiglia di utilizzare metodi di pagamento astratti. In questo modo il client browser comunica direttamente con il provider del gateway dei pagamenti e Adobe non conserva né trasmette la data del titolare della carta né le soluzioni commerce. Questo approccio richiede solo una conformità PCI di livello 3. Tuttavia, vi sono altri elementi da considerare per assicurare la piena conformità allo standard PCI, come il modo in cui i dipendenti interagiscono con il sistema e i dati. Per ulteriori informazioni sulla conformità PCI di Adobe Commerce, vedere [Conformità PCI](https://business.adobe.com/it/products/magento/pci-compliance.html)

## &#x200B;15. Se utilizzo le versioni cloud di AEM e Adobe Commerce, questa soluzione congiunta è compatibile con PCI?

Sì, il questionario di autovalutazione D e l’attestato di conformità sono disponibili su richiesta.

## &#x200B;16. Come posso richiedere una licenza di prova di I/O Runtime?

Per informazioni dettagliate sulla richiesta di una licenza di prova per l’utilizzo di I/O Runtime, consulta [Ottenere l’accesso](https://developer.adobe.com/runtime/docs/guides/overview/getting_access/).
