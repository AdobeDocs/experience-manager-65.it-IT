---
title: Cockpit prodotto
description: Utilizzo di Product Cockpit
exl-id: 05ef2604-1d52-4397-a696-0b64717cc3cc
source-git-commit: ed11891c27910154df1bfec6225aecd8a9245bff
workflow-type: tm+mt
source-wordcount: '424'
ht-degree: 1%

---

# Cockpit prodotto {#product-cockpit}

## Panoramica {#overview}

Il Product Cockpit offre una panoramica unificata dei cataloghi di prodotti collegati e dei contenuti associati. Tutti i contenuti associati dispongono di collegamenti per accedervi rapidamente dal cockpit.

I dati dei prodotti in fase di staging includono qualsiasi mutazione futura, ad esempio nuove categorie, prodotti o proprietà aggiornate.

>[!NOTE]
>
>Il termine catalogo dei prodotti è intercambiabile con l&#39;archivio, la vista Store e espressioni simili di e-commerce.

## Configurazione {#configuration}

I cataloghi di prodotti devono essere configurati in AEM. Vedi [configurazione di store e cataloghi](/help/commerce/cif/getting-started.md#catalog) per ulteriori informazioni.

L’abilitazione delle funzioni di catalogo in fase di staging richiede l’autenticazione. Vedi [Introduzione](/help/commerce/cif/getting-started.md) per ulteriori informazioni.

>[!NOTE]
>
>Le funzioni del catalogo di staging sono disponibili solo con i connettori Adobe Commerce e di terze parti che supportano l’autenticazione basata sui token.

## Apertura del prodotto Cockpit {#opening-product-cockpit}

Il modo più semplice per accedere al Product Cockpit è tramite il menu &#39;Commerce&#39; AEM menu principale. È anche possibile utilizzare Omnisearch (ricerca di commercio) o aprire `https://<yourAEMInstance>/commerce.html`.

![menu AEM](/help/commerce/cif/assets/aem-menu.png)

## Navigazione nei cataloghi di prodotti {#browsing-product-catalogs}

Il Product Cockpit è organizzato in modo gerarchico seguendo la struttura del catalogo dei prodotti. Il primo livello mostra il livello di directory principale del catalogo di tutti i cataloghi di prodotti configurati, comprese le metadati del back-end di commerce.

![Cataloghi configurati](/help/commerce/cif/assets/catalog-overview.png)

Facendo clic su una categoria verranno caricati gli elementi secondari della categoria selezionata.

![Categoria bambini](/help/commerce/cif/assets/catalog-category-children.png)

Se disponibile, facendo clic su un prodotto verranno caricate le varianti di prodotto.

![Varianti di prodotto](/help/commerce/cif/assets/catalog-product-variation.png)

>[!NOTE]
>
>I dati del catalogo di prodotto in AEM sono dati recuperati in tempo reale tramite l’endpoint di e-commerce configurato. Nessun dato di catalogo prodotti archiviato in AEM.

## Ricerca nei cataloghi di prodotti {#searching-product-catalog}

Nella scheda filtro a sinistra è disponibile una ricerca full-text sull’intero catalogo dei prodotti per trovare rapidamente i prodotti.

![ricerca](/help/commerce/cif/assets/search-cockpit.png)

## Navigazione nel catalogo dei prodotti in fase di sviluppo {#staged-product-catalogs}

Per impostazione predefinita, il cockpit prodotto mostra i dati del catalogo prodotti in tempo reale. Utilizzando &quot;STAGED CATALOG&quot; nella scheda filtro a sinistra, il catalogo prodotti verrà caricato per qualsiasi data selezionata.

![catalogo in serie](/help/commerce/cif/assets/staged-cockpit.png)

## Proprietà catalogo prodotti {#catalog-properties}

Facendo clic sull’icona delle proprietà di un prodotto o di una categoria si aprirà la vista delle proprietà dell’oggetto selezionato. Le proprietà aperte di una variante di prodotto sono uguali per aprire le proprietà principali del prodotto.

### Schede Commerce {#tabs}

Le schede generale e variante mostrano le proprietà di e-commerce predefinite provenienti dal back-end di e-commerce. Questi dati (incl. varianti) è un dato di sola lettura in AEM in quanto il sistema di record è il back-end commerce. La scheda variante viene visualizzata solo per i prodotti con varianti e mostra un elenco di tutte le varianti.

![proprietà del catalogo](/help/commerce/cif/assets/catalog-properties.png)

### Schede Contenuto AEM {#content-tabs}

Queste schede, raggruppate per tipi di contenuto AEM (Frammenti esperienza, Frammenti di contenuto, Risorse associate), mostrano AEM contenuto associato all’oggetto commerce. L’azione &quot;Visualizza dettagli&quot; apre una nuova scheda del browser con il contenuto selezionato.

![proprietà del contenuto](/help/commerce/cif/assets/content-properties.png)
