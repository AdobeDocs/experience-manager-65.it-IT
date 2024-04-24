---
title: Creazione di esperienze Commerce
description: Il componente aggiuntivo CIF estende l’authoring Adobe Experience Manager con funzionalità specifiche per l’e-commerce.
exl-id: 2db51bd7-8fc7-4ae8-8d6f-e5035fbe954d
solution: Experience Manager,Commerce
feature: Commerce Integration Framework
role: Admin, Developer
source-git-commit: 10268f617b8a1bb22f1f131cfd88236e7d5beb47
workflow-type: tm+mt
source-wordcount: '713'
ht-degree: 0%

---

# Creazione di esperienze Commerce {#authoring-commerce-experiences}

## Panoramica {#overview}

Il componente aggiuntivo CIF estende l’authoring AEM con funzionalità specifiche per l’e-commerce. Questo consente agli autori di creare e gestire in modo efficiente esperienze relative al commercio, accedendo ai dati e ai contenuti dei prodotti senza uscire dal contesto.

## Pickers {#pickers}

I selettori di prodotti e categorie sono finestre di dialogo modali dell’interfaccia utente che offrono agli autori di AEM un modo comodo per trovare e selezionare prodotti o categorie quando necessario. I Componenti core, le associazioni di contenuti e i modelli di prodotto sono le aree tipiche con configurazioni che richiedono i dati del catalogo dei prodotti. I selettori supportano varie opzioni di configurazione, come la selezione multipla, la selezione delle varianti e la preselezione dei valori.

### Selettore prodotti {#product-picker}

Questo selettore può offrire una navigazione nella struttura del catalogo o una ricerca full-text per trovare il prodotto. I prodotti con variante offrono un’icona di cartella nella colonna &quot;Tipo&quot;. Fai clic sull’icona della cartella per aprire le varianti del prodotto selezionato.

![Selettore prodotti](/help/commerce/cif/assets/authoring/product-picker.png)

Facendo clic sulla categoria principale, l’autore ritorna al livello del prodotto.

![Selettore prodotti](/help/commerce/cif/assets/authoring/product-picker-variation.png)

**Esempio di teaser di prodotto**

![Componente teaser senza selezione](/help/commerce/cif/assets/authoring/teaser_component_without_selection.png)

La finestra di dialogo per la configurazione di questo componente richiede un prodotto. L’CIF utilizza lo SKU come identificatore del prodotto. Gli autori possono immettere manualmente lo SKU oppure fare clic sull’icona della cartella per aprire il selettore prodotti. Dopo aver selezionato e chiuso il selettore, nella finestra di dialogo del componente viene visualizzato il nome del prodotto selezionato

![Componente teaser con selezione](/help/commerce/cif/assets/authoring/teaser_component_with_selection.png)

### Selettore categorie {#category-picker}

Questo selettore può offrire una navigazione nella struttura del catalogo per trovare la categoria.

![Selettore categorie](/help/commerce/cif/assets/authoring/category-picker.png)

**Esempio di carosello categorie**

![Componente Carosello senza selezione](/help/commerce/cif/assets/authoring/carousel_component_without_selection.png)

La finestra di dialogo per configurazione di questo componente richiede le categorie 1: n. L’CIF utilizza l’UID/ID come identificatore della categoria. Gli autori possono immettere manualmente l’UID oppure fare clic sull’icona della cartella per aprire il selettore delle categorie. Dopo aver selezionato e chiuso il selettore, nella finestra di dialogo del componente viene visualizzato il nome della categoria selezionata.

![Componente Carosello con selezione](/help/commerce/cif/assets/authoring/carousel_component_with_selection.png)

## Editor universale {#universal-editor}

L’editor universale è esteso con funzionalità che consentono di accedere in tempo reale ai dati di prodotto e ai contenuti di prodotto associati.

### Accesso ai dati di prodotto {#access-product-data}

La scheda Risorse nel pannello laterale dell’editor consente di accedere ai dati dei prodotti selezionando il tipo &quot;Prodotti&quot;. I dati vengono recuperati in tempo reale dall’endpoint commerce configurato. Il filtro è una ricerca full-text sull’endpoint commerce per trovare prodotti specifici.

![Pannello laterale dati prodotto](/help/commerce/cif/assets/authoring/products-side-panel.png)

Analogamente alle risorse, i prodotti possono essere aggiunti a una pagina (creando un componente Product Teaser per impostazione predefinita) o a componenti (attualmente supportati sono Product Teaser e Product Carousel).

### Aggiunta di collegamenti nei campi di testo mediante l’editor Rich Text {#rte}

Le pagine del catalogo dei prodotti CIF sono pagine virtuali di cui viene eseguito il rendering immediato. Pertanto, non è possibile incorporare collegamenti ipertestuali come per le normali pagine AEM. L’CIF aggiunge una nuova azione &quot;Collegamenti Commerce&quot; all’editor Rich Text. Questa azione funziona esattamente come la normale azione &quot;Collegamento ipertestuale&quot;, ma consente agli autori di selezionare un prodotto o una categoria utilizzando i selettori.

![RTE](/help/commerce/cif/assets/authoring/RTE.png)

    >[!NOTA]
    >
    >Se vengono selezionati sia la categoria che il prodotto, verrà utilizzato il prodotto.

Questo crea un collegamento segnaposto che viene sostituito da un collegamento reale quando viene eseguito il rendering della pagina.

### Accesso al contenuto prodotto associato {#associated-content}

Se Universal Editor riconosce i prodotti 1:n in una pagina, il pannello laterale mostra automaticamente la scheda &quot;Contenuto Commerce associato&quot;. Questa scheda consente agli autori di accedere rapidamente ai contenuti AEM a cui è stato applicato il tag del prodotto (vedere [arricchire i dati di prodotto con i contenuti AEM associati](./enrich-product-associated-content.md) per ulteriori informazioni). Questa scheda offre elenchi a discesa per filtrare in base al tipo di contenuto e a prodotti specifici se nella pagina sono presenti più prodotti. L’utilizzo del contenuto funziona esattamente come l’utilizzo del contenuto della scheda &quot;Risorse&quot;.

![Pannello laterale dati prodotto](/help/commerce/cif/assets/authoring/associated-commerce-content-tab.png)

### Anteprima dati prodotto in staging {#staged-data}

La modalità Timewarp nell’editor consente agli autori di visualizzare in anteprima e sfogliare un’esperienza AEM con i dati del catalogo dei prodotti in staging in base alla data Timewarp.

![Timewarp](/help/commerce/cif/assets/authoring/timewarp.png)

I componenti visualizzano un indicatore visivo se la data utilizzata è pubblicata nell’area intermedia.

![Indicatore Staged](/help/commerce/cif/assets/authoring/staged-indicator.png)

## Omnisearch {#omnisearch}

L’utilizzo di Omnisearch è un modo semplice per i professionisti di trovare i contenuti AEM e i dati del catalogo dei prodotti utilizzando la ricerca full-text. Omnisearch eseguirà una ricerca full-text in AEM e nel backend di e-commerce per trovare gli oggetti del catalogo dei prodotti nel backend di e-commerce e il contenuto dell’AEM. I risultati dell’AEM includono anche contenuti che sono stati taggati con dati di prodotto/categoria.

![Omnisearch](/help/commerce/cif/assets/authoring/omnisearch.png)

Il risultato è raggruppato per tipo.

    >[!NOTA]
    >
    >La ricerca full-text in Omnisearch non supporta i frammenti di contenuto associati. Utilizza SKU o UID per trovare i frammenti di contenuto associati.
