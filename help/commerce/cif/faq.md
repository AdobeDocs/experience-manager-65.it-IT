---
title: Domande frequenti sull'integrazione di AEM e commerce tramite Commerce Integration Framework
description: Domande frequenti sull'integrazione di AEM e commerce tramite Commerce Integration Framework
exl-id: d541607f-c4c9-4dd5-aadf-64d4cb5f9f2a
source-git-commit: 9defa6d1843007e9375d839f72f6993c691a37c0
workflow-type: tm+mt
source-wordcount: '960'
ht-degree: 23%

---

# Domande frequenti sull&#39;integrazione di AEM e commerce tramite Commerce Integration Framework

## 1. CIF GraphQL è utilizzato solo per l’e-commerce o è disponibile per eseguire query sui contenuti creati su AEM JCR?

Adobe ha adottato le API GraphQL di Adobe Commerce come API di e-commerce ufficiale per tutti i dati relativi all’e-commerce. Pertanto, AEM utilizza GraphQL per scambiare dati di e-commerce con Adobe Commerce e con qualsiasi motore di e-commerce tramite I/O Runtime. Questa API GraphQL è indipendente AEM API GraphQL per accedere ai frammenti di contenuto.

## 2. È possibile memorizzare le risorse di prodotto (immagini) e farvi riferimento da AEM tramite l’amministratore di Adobe Commerce? Come possono essere utilizzate le risorse da Dynamic Media?

Non è disponibile alcuna integrazione ufficiale AEM Assets - Adobe Commerce. È disponibile un connettore partner sul [mercato](https://marketplace.magento.com/partner/bounteous_ecomm).

Oppure, come soluzione alternativa, puoi archiviare le risorse dei prodotti (immagini) in AEM Assets, ma devi memorizzare manualmente gli URL delle risorse in Adobe Commerce. Dynamic Media fa parte di AEM Assets e funziona allo stesso modo.

## 3. Importa dove viene distribuita la soluzione di e-commerce? on-premise o nel cloud?

No, non importa dove viene distribuita la soluzione commerce. CIF e la vetrina AEM funzionano indipendentemente dal modello di distribuzione. Tuttavia, se la soluzione viene implementata con l’architettura di riferimento E2E consigliata, i test E2E possono essere eseguiti in base a KPI delle prestazioni che rappresentano un tipico profilo cliente aziendale. Questo processo fornisce informazioni aggiuntive che possono essere utilizzate come benchmark.

## 4. In che modo vengono create le pagine di catalogo o di prodotto in AEM? Come persistono in AEM?

Le pagine di catalogo e di prodotto vengono create e memorizzate nella cache in AEM in base a modelli generici per pagine di catalogo e di prodotto. Nessun dato di prodotto o catalogo viene importato e memorizzato in AEM.

## 5. Quando aggiorni i dati di prodotto nella tua soluzione commerce, è un push in tempo reale a AEM? oppure si tratta di un processo batch?

Il componente aggiuntivo CIF utilizzato con AEM consente il flusso dei dati dalla soluzione commerce a AEM on-demand. Pertanto, questo flusso di lavoro non è un processo push in tempo reale o batch quando è presente un aggiornamento nella soluzione commerce.

## 6. Qual è la dimensione del catalogo AEM con il supporto CIF?

Il supporto per le dimensioni del catalogo dipende da alcuni aspetti aggiuntivi da considerare. Qual è il rapporto di cache dei dati e delle pagine del catalogo? Quante richieste simultanee ci si aspetta durante le ore di punta? Quanto sono scalabili le API delle soluzioni commerce?

## 7. Che ruolo svolge un sistema PIM in questo framework?

I dati PIM vengono esposti ai AEM e ai client tramite le richieste GraphQL. Si consiglia di Adobe di integrare PIM con il motore di e-commerce (Adobe Commerce o altri) in modo che i dati PIM possano essere recuperati dal motore di e-commerce.

## 8. È possibile memorizzare nella cache anche i prezzi e altri dati tramite Dispatcher? Questo potrebbe comportare problemi di invalidazione frequente della cache?

I dati dinamici come prezzo o inventario non vengono memorizzati nella cache di Dispatcher. I dati dinamici vengono recuperati lato client con i componenti Web direttamente tramite le API GraphQL. Nella cache di Dispatcher vengono memorizzati solo i dati statici (come i dati di prodotto o categoria). Se i dati di prodotto cambiano, è necessaria l’invalidazione della cache.

## 9. Come funziona l’invalidazione della cache per AEM Dispatcher con AEM e commerce?

Adobe consiglia di impostare l’invalidazione della cache basata su TTL per le pagine memorizzate nella cache del Dispatcher. Per informazioni dinamiche come prezzo o stock, Adobe consiglia di eseguire il rendering della data lato client. Per ulteriori informazioni sull’annullamento della validità della cache basata su TTL, consulta [Dispatcher AEM](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17458.html?lang=en)

## 10. Vi sono consigli sulla ricerca unificata nei contenuti AEM con Commerce?

Viene fornita un’implementazione di riferimento per la ricerca di prodotti, ma non viene eseguita alcuna ricerca unificata con i contenuti. Questa funzione è specifica per il cliente ed è più efficace a livello di progetto.

## 11. Come funziona la ricerca con AEM e commercio utilizzando CIF?

CIF fornisce i componenti Barra di ricerca e Risultati di ricerca. Il componente Barra di ricerca invia una richiesta GraphQL con il termine di ricerca alla soluzione commerce che restituisce un elenco di prodotti che include nome prodotto, prezzo, SLUG e così via. Il componente Risultato di ricerca visualizza quindi i risultati della ricerca in una visualizzazione a galleria su una pagina di risultati di ricerca creata su AEM. Il componente Ricerca supporta la ricerca full-text. Utilizza la chiave SLUG/url per creare un riferimento al PDP.

## 12. Come possono essere utilizzati i dati di prodotto in MSM o nelle traduzioni?

I dati di prodotto sono già tradotti in PIM o in Adobe Commerce. L&#39;integrazione AEM - Adobe Commerce supporta la connessione a più store e viste store di Adobe Commerce. In una configurazione MSM, in genere un sito AEM è collegato a una visualizzazione archivio Adobe Commerce.

## 13. Esiste un modo per migliorare i dati di prodotto con testo commerciale? In caso affermativo, a che punto si trova? In AEM o nella soluzione commerce?

Adobe consiglia di gestire i dati e il contenuto relativi al marketing in AEM. Decorare i dati di prodotto dalla soluzione commerce con attributi aggiuntivi utilizzando Frammenti di contenuto oppure creare e collegare frammenti di esperienza per contenuti non strutturati con i prodotti.

## 14. In che modo un’azienda garantisce la conformità PCI quando si utilizza AEM per l’intero livello di presentazione?

L&#39;Adobe consiglia di utilizzare metodi di pagamento astratti. In questo modo il client browser comunica direttamente con il provider del gateway dei pagamenti in modo che l&#39;Adobe non conservi o passi la data del titolare della carta, né le soluzioni commerce. Questo approccio richiede solo una conformità PCI di livello 3. Tuttavia, ci sono altri elementi da considerare completamente conformi allo standard PCI, come il modo in cui i dipendenti interagiscono con il sistema e i dati. Per ulteriori informazioni sulla conformità PCI di Adobe Commerce, consulta [Conformità PCI](https://business.adobe.com/products/magento/pci-compliance.html)

## 15. Se utilizzo versioni cloud AEM e Adobe Commerce, questa soluzione comune è compatibile con PCI?

Sì, il Questionario di autovalutazione D e la Certificazione di conformità sono disponibili su richiesta.

## 16. Come posso richiedere una licenza di prova di I/O Runtime?

Per richiedere una licenza di prova per utilizzare I/O Runtime, visita [questa pagina](https://adobeio.typeform.com/to/obqgRm).
