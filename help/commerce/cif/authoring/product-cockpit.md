---
title: Cockpit prodotto
description: Utilizzo della cabina di comando del prodotto
exl-id: 05ef2604-1d52-4397-a696-0b64717cc3cc
source-git-commit: b00ed4ed146b89aece9af1d267c890a360a236e9
workflow-type: tm+mt
source-wordcount: '416'
ht-degree: 1%

---

# Cockpit prodotto {#product-cockpit}

## Panoramica {#overview}

Il pannello di controllo prodotto fornisce una panoramica unificata dei cataloghi di prodotti collegati e dei contenuti associati. Tutto il contenuto associato dispone di collegamenti per accedervi rapidamente dalla cabina di pilotaggio.

I dati dei prodotti in staging includono qualsiasi mutazione futura, ad esempio nuove categorie, prodotti o proprietà aggiornate.

>[!NOTE]
>
>Il termine catalogo prodotti è intercambiabile con il punto vendita, la vista store e espressioni simili.

## Configurazione {#configuration}

I cataloghi di prodotti devono essere configurati in AEM. Consulta [configurazione di store e cataloghi](/help/commerce/cif/getting-started.md#catalog) per ulteriori informazioni.

L’abilitazione delle funzioni di catalogo in staging richiede l’autenticazione. Consulta [Guida introduttiva](/help/commerce/cif/getting-started.md) per ulteriori informazioni.

>[!NOTE]
>
>Le funzioni del catalogo in staging sono disponibili solo con Adobe Commerce e connettori di terze parti che supportano l’autenticazione basata su token.

## Apertura della cabina di comando del prodotto {#opening-product-cockpit}

Il modo più semplice per accedere al pannello di comando del prodotto è tramite il menu &quot;Commerce&quot; nel menu principale dell’AEM. È inoltre possibile utilizzare Omnisearch (ricerca per Commerce) o aprire `https://<yourAEMInstance>/commerce.html`.

![Menu AEM](/help/commerce/cif/assets/aem-menu.png)

## Esplorazione dei cataloghi di prodotti {#browsing-product-catalogs}

Il pannello di controllo Prodotto è organizzato in modo gerarchico seguendo la struttura del catalogo dei prodotti. Il primo livello mostra il livello principale del catalogo di tutti i cataloghi di prodotti configurati, comprese le metainformazioni del backend di e-commerce.

![Cataloghi configurati](/help/commerce/cif/assets/catalog-overview.png)

Facendo clic su una categoria vengono caricati gli elementi secondari della categoria selezionata.

![Elementi figlio categoria](/help/commerce/cif/assets/catalog-category-children.png)

Facendo clic su un prodotto vengono caricate le varianti di prodotto, se disponibili.

![Varianti prodotto](/help/commerce/cif/assets/catalog-product-variation.png)

>[!NOTE]
>
>I dati del catalogo dei prodotti nell’AEM sono dati recuperati in tempo reale tramite l’endpoint commerce configurato. Nessun dato del catalogo dei prodotti viene memorizzato nell’AEM.

## Ricerca nei cataloghi di prodotti {#searching-product-catalog}

Nella scheda del filtro a sinistra è disponibile una ricerca full-text sull’intero catalogo dei prodotti per trovare rapidamente i prodotti.

![ricerca](/help/commerce/cif/assets/search-cockpit.png)

## Esplorazione del catalogo prodotti di staging {#staged-product-catalogs}

Per impostazione predefinita, la cabina di comando del prodotto mostra i dati live del catalogo dei prodotti. L’utilizzo del &quot;CATALOGO STAGNATO&quot; nella scheda del filtro a sinistra carica il catalogo dei prodotti per qualsiasi data selezionata.

![catalogo di staging](/help/commerce/cif/assets/staged-cockpit.png)

## Proprietà catalogo prodotti {#catalog-properties}

Facendo clic sull&#39;icona delle proprietà di un prodotto o di una categoria si apre la visualizzazione delle proprietà dell&#39;oggetto selezionato. Le proprietà aperte di una variante di prodotto sono uguali alle proprietà del prodotto principale.

### Schede Commerce {#tabs}

Le schede Generale e Variante mostrano le proprietà commerce predefinite provenienti dal backend di e-commerce. Questi dati (inclusi variants) è un dato di sola lettura in AEM in quanto il sistema di registrazione è il back-end commerciale. La scheda Variante viene visualizzata solo per i prodotti con varianti e mostra un elenco di tutte le varianti.

![proprietà catalogo](/help/commerce/cif/assets/catalog-properties.png)

### Schede contenuto AEM {#content-tabs}

In queste schede, raggruppate per tipi di contenuto AEM (Frammenti di esperienza, Frammenti di contenuto, Risorse associate), viene visualizzato il contenuto AEM associato all’oggetto commerce. L&#39;azione &#39;Visualizza dettagli&#39; apre una nuova scheda del browser con il contenuto selezionato.

![proprietà contenuto](/help/commerce/cif/assets/content-properties.png)
