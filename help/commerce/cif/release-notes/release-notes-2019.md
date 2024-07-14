---
title: Contenuto AEM e note sulla versione 2019 di Commerce
description: Note sulla versione 2019 di Adobe Experience Manager Content and Commerce.
exl-id: 7e61a75d-6b35-46ee-b88a-444c10b2708f
solution: Experience Manager,Commerce
feature: Commerce Integration Framework
role: Admin, Developer
source-git-commit: 10268f617b8a1bb22f1f131cfd88236e7d5beb47
workflow-type: tm+mt
source-wordcount: '946'
ht-degree: 6%

---

# Panoramica sulla versione di Commerce integration framework GitHub

## Data di rilascio: novembre 2019

| GitHub | Versione | Note dettagliate sulla versione |
|:-------|:-----:|---------------------:|
| Connettore CIF | 0,7,1 | [Note sulla versione](https://github.com/adobe/commerce-cif-connector/releases) |
| Componenti core CIF | 0,6,0 | [Note sulla versione](https://github.com/adobe/aem-core-cif-components/releases) |
| Archetipo CIF | 0.6.2. | [Note sulla versione](https://github.com/adobe/aem-cif-project-archetype/releases) |

### Novità {#what-is-new-november}

* Con la nuova opzione &quot;Visualizza con prodotto/categoria&quot; nell’editor Sites, gli autori possono visualizzare in anteprima le pagine dei dettagli e degli elenchi dei prodotti insieme ai prodotti/categorie.

* Gli autori possono assegnare tag alle risorse per SKU di prodotto e cercare risorse specifiche per prodotto per SKU.

* Aggiunta/rimozione del supporto per i coupon nel carrello.

* Braintree il supporto per il pagamento aggiunto nella vetrina Venia AEM.

### Novità {#what-is-improved-november}

* I selettori di categorie/prodotti sono stati migliorati per rispettare la vista specificata dello store di Adobe Commerce in una configurazione multi-store.

* I componenti basati su React sono disponibili come pacchetto npm. Questo consente agli sviluppatori di utilizzare il pacchetto React Components come dipendenza per un nuovo progetto React per consentire la personalizzazione dei componenti esistenti o lo sviluppo di nuovi componenti basati su React.

* La personalizzazione delle query GraphQL è stata semplificata. Questo consente agli sviluppatori di personalizzare i componenti core CIF con meno codice.

## Data di rilascio: ottobre 2019

| GitHub | Versione | Note dettagliate sulla versione |
|:-------|:-----:|---------------------:|
| Connettore CIF | 0,6,0 | [Note sulla versione](https://github.com/adobe/commerce-cif-connector/releases) |
| Componenti core CIF | 0,5,0 | [Note sulla versione](https://github.com/adobe/aem-core-cif-components/releases) |
| Archetipo CIF | 0,5,0 | [Note sulla versione](https://github.com/adobe/aem-cif-project-archetype/releases) |

### Novità {#what-is-new-october}

* Modelli completamente personalizzabili per la pagina dei dettagli e la pagina dell’elenco dei prodotti. Gli autori possono ora creare modelli e trascinare e rilasciare l’elenco dei prodotti e i componenti dei dettagli dei prodotti su tali modelli. Oltre ad aggiungere altri componenti, gli autori possono ora modificare anche il layout di questi modelli, dando loro una libertà illimitata di creare esperienze straordinarie combinando contenuti di marketing e di e-commerce.

* Tutti i componenti core CIF compatibili con l&#39;autore sono stati migliorati per supportare [Sistema di stili dell&#39;AEM](https://experienceleague.adobe.com/docs/experience-manager-65/authoring/siteandpage/style-system.html). Sono stati forniti stili di esempio per il componente elenco prodotti.

* Componenti lato client basati su React per la gestione degli account. Questa versione supporta le seguenti funzionalità: Accesso, Password dimenticata e Creazione di un account.

### Novità {#what-is-improved-october}

* I componenti Dettagli prodotto e Elenco prodotti sono stati migliorati per mostrare dati fittizi per fornire agli autori un’anteprima del layout quando tali componenti vengono inseriti in un modello/pagina.

* Ora i componenti Minicart e Checkout utilizzano gli hook React per migliorare l’estensibilità.

## Data di rilascio: settembre 2019

| GitHub | Versione | Note dettagliate sulla versione |
|:-------|:-----:|---------------------:|
| Connettore CIF | 0,5,0 | [Note sulla versione](https://github.com/adobe/commerce-cif-connector/releases) |
| Componenti core CIF | 0,4,0 | [Note sulla versione](https://github.com/adobe/aem-core-cif-components/releases) |
| Archetipo CIF | 0,4,0 | [Note sulla versione](https://github.com/adobe/aem-cif-project-archetype/releases) |

### Novità {#what-is-new-september}

* La funzione con più modelli consente agli autori di arricchire una pagina di dettagli di prodotto o una pagina di elenco prodotti specifica. Gli autori possono creare facilmente una pagina di dettagli del prodotto o una pagina di elenco dei prodotti personalizzata e utilizzare il selettore di prodotti o categorie per assegnare la pagina personalizzata a un prodotto o a una categoria specifica.

* Associazione di più cataloghi per consentire agli autori di associare più cataloghi nella console dei prodotti AEM. Gli autori possono inoltre modificare e visualizzare le proprietà di associazione del catalogo dopo aver creato l&#39;associazione.

* Checkout lato client e Mini Cart basati su React che utilizzano GraphQL per supportare un percorso acquisti di base completo.

* Il componente Pagamento include i moduli di indirizzo, la selezione del pagamento e la selezione del metodo di spedizione.

### Novità {#what-is-improved-september}

* I componenti Product Teaser e Product Carousel supportano varianti di prodotto.

## Data di rilascio: agosto 2019

| GitHub | Versione | Note dettagliate sulla versione |
|:-------|:-----:|---------------------:|
| Connettore CIF | 0,4,0 | [Note sulla versione](https://github.com/adobe/commerce-cif-connector/releases) |
| Componenti core CIF | 0,3 | [Note sulla versione](https://github.com/adobe/aem-core-cif-components/releases) |
| Archetipo CIF | 0,3 | [Note sulla versione](https://github.com/adobe/aem-cif-project-archetype/releases) |

### Novità {#what-is-new-august}

* L’incorporamento del connettore CIF nell’archetipo dell’CIF è facoltativo per fornire agli sviluppatori maggiore flessibilità.

* I componenti CIF si sono separati dallo stile CSS specifico di &quot;Venia&quot; per consentire agli sviluppatori di applicare lo stile CSS desiderato.

* Funzione multi-store/sito per consentire l’uso dei componenti core CIF su più strutture di siti AEM e consentire all’implementazione client GraphQL sottostante di connettersi a diverse viste store/store di Adobe Commerce.

* Il caching di GraphQL è abilitato per alcune query GraphQL tramite HTTP GET per ridurre i tempi di risposta.

* La vista di descrizione del prodotto è abilitata nella console Prodotti AEM.

* Commerce Teaser estende il componente WCM Teaser per consentire agli autori di aggiungere campi CTA anche a una pagina di dettagli del prodotto o a una pagina dell’elenco dei prodotti.

* Pulsante che consente agli autori di inserire in una pagina AEM e di collegarsi a una pagina AEM, a una pagina dei dettagli del prodotto, a una pagina dell’elenco dei prodotti o a un collegamento esterno.

### Novità {#what-is-improved-august}

* La configurazione dello store di Adobe Commerce è stata spostata da OSGi alla console dei prodotti AEM per rendere la configurazione dell’integrazione più semplice da creare.

## Data di rilascio: luglio 2019

| GitHub | Versione | Note dettagliate sulla versione |
|:-------|:-----:|---------------------:|
| Connettore CIF | 0,3 | [Note sulla versione](https://github.com/adobe/commerce-cif-connector/releases) |
| Componenti core CIF | 0,2 | [Note sulla versione](https://github.com/adobe/aem-core-cif-components/releases) |
| Archetipo CIF | 0,2 | [Note sulla versione](https://github.com/adobe/aem-cif-project-archetype/releases) |

### Novità {#what-is-new-july}

* Primo Archetipo CIF a fornire agli sviluppatori diverse opzioni di distribuzione: 1. Distribuire la vetrina Venia AEM 2. Distribuire lo scaffolding per un nuovo progetto 3. Utilizzare elementi CIF in un progetto esistente

* Navigazione nel catalogo a più livelli per supportare la navigazione tra categorie e sottocategorie.

* Paginazione sulle pagine delle categorie per una migliore esperienza utente.

* Rendering lato client dell’attributo price nei componenti Product Detail ed Product List per supportare il rendering degli attributi dinamici.

* Carosello prodotti lato server per visualizzare un elenco di prodotti in primo piano in uno stile carosello.

* Elenco di categorie in primo piano lato server per visualizzare un elenco di categorie in una pagina AEM.

### Novità {#what-is-improved-july}

* Il supporto per Adobe Commerce 2.3.2 e le correzioni di bug relativi alle proprietà del prodotto vengono visualizzati nella console del prodotto.

## Data di rilascio: giugno 2019

| GitHub | Versione | Note dettagliate sulla versione |
|:-------|:-----:|---------------------:|
| Connettore CIF | 0,2 | [Note sulla versione](https://github.com/adobe/commerce-cif-connector/releases) |
| Componenti core CIF | 0,1,0 | [Note sulla versione](https://github.com/adobe/aem-core-cif-components/releases) |

### Novità {#what-is-new-june}

* Vetrina B2C AEM con stile CSS Venia mobile-first, pagina di destinazione, navigazione dinamica del catalogo tramite pagine di prodotti e categorie, pagina di ricerca dei prodotti e funzionalità del carrello per avviare e accelerare i progetti di e-commerce.

* Connettore CIF e strumenti di authoring (console prodotti, selettore prodotti e selettore categorie) per consentire agli autori di creare esperienze AEM con contenuti commerciali.

* Prima versione dei Componenti core CIF compatibili con Adobe Commerce 2.3.1:
   * Dettagli prodotto
   * Elenco prodotti
   * Product Teaser
   * Navigazione
   * Ricerca prodotti
   * Carrello (REST)
