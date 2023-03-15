---
title: Note sulla versione 2021 di AEM Content and Commerce
description: Note sulla versione 2021 di AEM Content and Commerce
exl-id: 7e61a75d-6b35-46ee-b88a-444c10b2708f
source-git-commit: a467009851937c4a10b165a3d253c47bf990bbc5
workflow-type: tm+mt
source-wordcount: '978'
ht-degree: 9%

---

# Panoramica sulla versione di Commerce Integration Framework GitHub

## Data di rilascio: Novembre 2019

| GitHub | Versione | Note dettagliate sulla versione |
|:-------|:-----:|---------------------:|
| Connettore CIF | 0.7.1 | [Note sulla versione](https://github.com/adobe/commerce-cif-connector/releases) |
| Componenti core CIF | 0.6.0 | [Note sulla versione](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF Archetype | 0.6.2 | [Note sulla versione](https://github.com/adobe/aem-cif-project-archetype/releases) |

### Novità {#what-is-new-november}

* Gli autori possono visualizzare in anteprima i dettagli del prodotto e le pagine dell’elenco dei prodotti con prodotti/categorie con una nuova opzione &quot;Visualizza con prodotto/categoria&quot; nell’editor Sites.

* Gli autori possono assegnare tag alle risorse per SKU del prodotto e cercare le risorse specifiche per prodotto per SKU.

* Aggiungi/rimuovi il supporto coupon aggiunto nel carrello.

* Braintree il supporto per i pagamenti aggiunto AEM Venia store front.

### Miglioramenti {#what-is-improved-november}

* Selezione di categorie/prodotti migliorata per rispettare la visualizzazione specifica dell&#39;Adobe Commerce Store in una configurazione multi-store.

* Componenti basati su React disponibili come pacchetto npm. Questo consente agli sviluppatori di utilizzare il pacchetto React Components come dipendenza per un nuovo progetto React per consentire la personalizzazione dei componenti esistenti o sviluppare nuovi componenti basati su React.

* Personalizzazione delle query GraphQL semplificata. Questo consente agli sviluppatori di personalizzare i componenti CIF di base con meno codice.

## Data di rilascio: Ottobre 2019

| GitHub | Versione | Note dettagliate sulla versione |
|:-------|:-----:|---------------------:|
| Connettore CIF | 0.6.0 | [Note sulla versione](https://github.com/adobe/commerce-cif-connector/releases) |
| Componenti core CIF | 0.5.0 | [Note sulla versione](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF Archetype | 0.5.0 | [Note sulla versione](https://github.com/adobe/aem-cif-project-archetype/releases) |

### Novità {#what-is-new-october}

* Modelli completamente modificabili per la pagina dei dettagli del prodotto e la pagina dell’elenco dei prodotti. Gli autori possono ora creare nuovi modelli e trascinare e rilasciare l’elenco dei prodotti e i componenti di dettaglio dei prodotti su questi modelli. Oltre ad aggiungere altri componenti, gli autori possono ora modificare anche il layout di questi modelli, offrendo loro la libertà illimitata di creare esperienze straordinarie combinando contenuti di marketing e di e-commerce.

* Tutti i componenti core CIF compatibili con l’autore sono stati migliorati per supportare [Sistema di stili AEM](https://helpx.adobe.com/experience-manager/6-5/sites/authoring/using/style-system.html). Sono stati forniti stili di esempio per il componente elenco prodotti.

* Componenti lato client basati su React per la gestione degli account. Questa versione supporta le seguenti funzionalità: Accesso, Password dimenticata e Crea account.

### Miglioramenti {#what-is-improved-october}

* I dettagli del prodotto e i componenti dell’elenco dei prodotti sono stati migliorati per mostrare i dati fittizi, in modo da fornire agli autori un’anteprima del layout quando questi componenti vengono inseriti in un modello/pagina.

* I componenti Minicart e Checkout ora utilizzano gli hook di React per una migliore estensibilità.

## Data di rilascio: Settembre 2019

| GitHub | Versione | Note dettagliate sulla versione |
|:-------|:-----:|---------------------:|
| Connettore CIF | 0.5.0 | [Note sulla versione](https://github.com/adobe/commerce-cif-connector/releases) |
| Componenti core CIF | 0.4.0 | [Note sulla versione](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF Archetype | 0.4.0 | [Note sulla versione](https://github.com/adobe/aem-cif-project-archetype/releases) |

### Novità {#what-is-new-september}

* Funzione multi-modello per consentire agli autori di arricchire una pagina di dettaglio del prodotto o una pagina dell’elenco di prodotti specifici. Gli autori possono creare facilmente una pagina di dettaglio del prodotto personalizzata o una pagina di elenco prodotti e utilizzare il selettore prodotto o categoria per assegnare la pagina personalizzata a uno o più prodotti o categorie specifici.

* Il binding a più cataloghi consente agli autori di eseguire il binding di più cataloghi nella console AEM prodotto. Gli autori possono inoltre modificare e visualizzare le proprietà di binding del catalogo dopo la creazione del binding.

* Acquisto sul lato client basato su React e Mini carrello utilizzando GraphQL per supportare un percorso di acquisto di base completo.

* Il componente Pagamento include i moduli indirizzo, la selezione dei pagamenti e la selezione dei metodi di spedizione.

### Miglioramenti {#what-is-improved-september}

* I componenti Product Teaser e Product Carousel supportano le varianti di prodotto.

## Data di rilascio: Agosto 2019

| GitHub | Versione | Note dettagliate sulla versione |
|:-------|:-----:|---------------------:|
| Connettore CIF | 0.4.0 | [Note sulla versione](https://github.com/adobe/commerce-cif-connector/releases) |
| Componenti core CIF | 0.3.0 | [Note sulla versione](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF Archetype | 0.3.0 | [Note sulla versione](https://github.com/adobe/aem-cif-project-archetype/releases) |

### Novità {#what-is-new-august}

* L’integrazione del connettore CIF in CIF Archetype è opzionale per offrire agli sviluppatori una maggiore flessibilità.

* I componenti CIF disaccoppiati dallo stile CSS specifico &quot;Venia&quot; per consentire agli sviluppatori di applicare lo stile CSS desiderato.

* Funzionalità per più store/siti per consentire l’utilizzo di componenti core CIF su più strutture di siti AEM e consentire all’implementazione client GraphQL sottostante di connettersi a diverse viste store/store di Adobe Commerce.

* La memorizzazione in cache GraphQL è abilitata per alcune query GraphQL tramite HTTP per ridurre i tempi di risposta.

* Vista descrizione prodotto abilitata nella console Prodotti AEM.

* Commerce Teaser estende il componente WCM Teaser per consentire agli autori di aggiungere campi CTA anche a una pagina di dettagli prodotto o a una pagina di elenco prodotti.

* Pulsante per consentire agli autori di inserire in una pagina AEM un collegamento a una pagina AEM, a una pagina di dettagli del prodotto, a una pagina dell’elenco dei prodotti o a un collegamento esterno.

### Miglioramenti {#what-is-improved-august}

* La configurazione dell’archivio Adobe Commerce è stata spostata da OSGi a AEM console del prodotto per rendere la configurazione dell’integrazione più semplice per gli autori.

## Data di rilascio: Luglio 2019

| GitHub | Versione | Note dettagliate sulla versione |
|:-------|:-----:|---------------------:|
| Connettore CIF | 0.3.0 | [Note sulla versione](https://github.com/adobe/commerce-cif-connector/releases) |
| Componenti core CIF | 0.2.0 | [Note sulla versione](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF Archetype | 0.2.0 | [Note sulla versione](https://github.com/adobe/aem-cif-project-archetype/releases) |

### Novità {#what-is-new-july}

* Primo Archetipo CIF per fornire agli sviluppatori diverse opzioni di distribuzione: 1.Distribuzione AEM vetrina Venia 2. Distribuire l’impalcatura per un nuovo progetto 3. Utilizzare elementi CIF in un progetto esistente

* Navigazione tra cataloghi a più livelli per supportare la navigazione tra categorie e sottocategorie.

* Paginazione su pagine di categorie per un UX migliore.

* Rendering lato client dell’attributo del prezzo nei componenti Product Detail e Product List per supportare il rendering degli attributi dinamici.

* Carosello di prodotti lato server per visualizzare l’elenco dei prodotti in primo piano in stile carosello.

* Elenco categorie in primo piano lato server per visualizzare l&#39;elenco delle categorie su una pagina AEM.

### Miglioramenti {#what-is-improved-july}

* Il supporto per Adobe Commerce 2.3.2 e le correzioni di bug relativi alle proprietà del prodotto vengono visualizzati nella console del prodotto.

## Data di rilascio: Giugno 2019

| GitHub | Versione | Note dettagliate sulla versione |
|:-------|:-----:|---------------------:|
| Connettore CIF | 0.2.0 | [Note sulla versione](https://github.com/adobe/commerce-cif-connector/releases) |
| Componenti core CIF | 0.1.0 | [Note sulla versione](https://github.com/adobe/aem-core-cif-components/releases) |

### Novità {#what-is-new-june}

* AEM vetrina B2C con stile CSS Venia per dispositivi mobili, pagina di destinazione, navigazione dinamica del catalogo tramite pagine di prodotti e categorie, pagina di ricerca dei prodotti e funzionalità del carrello per avviare e accelerare i progetti di e-commerce.

* Connettore CIF e strumenti di creazione (console prodotto, selettore prodotto e selettore categoria) per consentire agli autori di creare esperienze in AEM con contenuti commerce.

* Prima versione dei componenti core CIF compatibili con Adobe Commerce 2.3.1:
   * Dettagli prodotto
   * Elenco prodotti
   * Product Teaser
   * Navigazione
   * Ricerca di prodotti
   * Carrello (REST)
