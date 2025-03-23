---
title: Utilizzo del selettore prodotti e categorie di CIF
description: Scopri come utilizzare il selettore di prodotti e categorie CIF nei componenti commerce del cliente per supportare autori ed esperti di marketing nell’utilizzo efficiente dei dati di catalogo e dei prodotti commerce.
sub-product: Commerce
topics: Development
version: Experience Manager as a Cloud Service
activity: develop
audience: developer
feature: Commerce Integration Framework
exl-id: 1e7c3748-92b5-45f1-8dd9-f1816e3e34aa
solution: Experience Manager,Commerce
role: Admin, Developer
source-git-commit: a45b09c52d780a954e606d4cae73a3a02a8a6aa4
workflow-type: tm+mt
source-wordcount: '563'
ht-degree: 0%

---

# Selettori per l’authoring di contenuti AEM e Commerce {#cif-pickers}

AEM Content &amp; Commerce Authoring fornisce una serie di strumenti di authoring per aiutare autori e addetti al marketing AEM a lavorare in modo efficiente con i dati di prodotto e i cataloghi commerce. Il selettore prodotti e il selettore categorie fanno parte del componente aggiuntivo CIF e sono utilizzati dai componenti core di CIF. I progetti possono utilizzare questi selettori in qualsiasi finestra di dialogo dei componenti per selezionare prodotti o categorie.

## Selettore prodotti {#product-picker}

Per utilizzare il selettore prodotti in un componente del progetto, uno sviluppatore deve aggiungere `commerce/gui/components/common/cifproductfield` alla finestra di dialogo di un componente. Ad esempio, utilizzare quanto segue per `cq:dialog`:

```xml
<product jcr:primaryType="nt:unstructured"
    sling:resourceType="commerce/gui/components/common/cifproductfield"
    fieldDescription="The product or product variant displayed by the teaser"
    fieldLabel="Select Product"
    filter="folderOrProductOrVariant"
    name="./selection"
    selectionId="sku"/>
```

Il campo prodotto consente di navigare fino al prodotto che un utente desidera selezionare tramite le diverse visualizzazioni. Per impostazione predefinita, il campo prodotto restituisce l&#39;ID del prodotto, ma può essere configurato utilizzando l&#39;attributo `selectionId`.

Il campo del selettore prodotti supporta le seguenti proprietà facoltative:

- selectionId (id, uid, sku, slug, combinedSlug, combinedSku): consente di scegliere l’attributo del prodotto che deve essere restituito dal selettore (impostazione predefinita = id). Se si utilizza lo sku, viene restituito lo sku del prodotto selezionato mentre si utilizza lo sku combinato e viene restituita una stringa come base#variante con lo sku del prodotto di base e della variante selezionata oppure un singolo sku se è selezionato un prodotto di base.
- filter (folderOrProduct, folderOrProductOrVariant) - filtra il contenuto di cui eseguire il rendering dal selettore durante l’esplorazione della struttura del prodotto. folderOrProduct - esegue il rendering di cartelle e prodotti. folderOrProductOrVariant - esegue il rendering di cartelle, prodotti e varianti di prodotti. Se viene eseguito il rendering di un prodotto o di una variante di prodotto, questo diventa selezionabile anche nel selettore. (impostazione predefinita = folderOrProduct)
- multiple (true, false): consente di selezionare uno o più prodotti (default = false)
- emptyText: per configurare il valore di testo vuoto del campo selettore

Sono inoltre supportate le proprietà dei campi di dialogo standard come `name`, `fieldLabel` o `fieldDescription`.

>[!CAUTION]
>
>Il componente `cifproductfield` richiede clientlib `cif.shell.picker`. Per aggiungere una libreria client a una finestra di dialogo, puoi utilizzare la proprietà extraClientlibs.
>[!CAUTION]
>
>A partire dalla versione 2.0.0 dei Componenti core CIF, il supporto per `id` è stato rimosso e sostituito con `uid`. Adobe consiglia di utilizzare `sku` o `slug` come identificatore del prodotto. Adobe continua a supportare `id` solo per i progetti che utilizzano i Componenti core CIF versione 1.x.

Un esempio completo di funzionamento di `cifproductfield` è disponibile nel progetto [Componenti core CIF](https://github.com/adobe/aem-core-cif-components/blob/master/ui.apps/src/main/content/jcr_root/apps/core/cif/components/commerce/productteaser/v1/productteaser/_cq_dialog/.content.xml). Consulta anche [Personalizzazione delle finestre di dialogo](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/customizing.html#customizing-dialogs) nella documentazione dei Componenti core AEM.

## Selettore categorie {#category-picker}

Il selettore categorie può essere utilizzato anche nella finestra di dialogo di un componente, in modo simile al selettore prodotti.

Il seguente snippet può essere utilizzato in una configurazione cq:dialog:

```xml
<category jcr:primaryType="nt:unstructured" 
    sling:resourceType="commerce/gui/components/common/cifcategoryfield" 
    fieldLabel="Category" 
    name="./categoryId" 
    selectionId="uid" />
```

Il campo del selettore delle categorie supporta le seguenti proprietà facoltative:

- selectionId(id, uid, slug, urlPath, idAndUrlPath _(obsoleto)_, uidAndUrlPath _(obsoleto)_) - consente di scegliere l&#39;attributo di categoria da restituire dal selettore (impostazione predefinita = id).
- multiple (true, false): abilita la selezione di una o più categorie (default = false)

Sono inoltre supportate le proprietà dei campi di dialogo standard come `name`, `fieldLabel` o `fieldDescription`.

>[!CAUTION]
>
>Come il componente `cifproductfield`, anche il componente `cifcategoryfield` richiede clientlib `cif.shell.picker`. Per aggiungere una clientlib a una finestra di dialogo, è possibile utilizzare la proprietà `extraClientlibs`. Consulta [Personalizzazione delle finestre di dialogo](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/customizing.html#customizing-dialogs) nella documentazione dei Componenti core di AEM.
>[!CAUTION]
>
>A partire dalla versione 2.0.0 dei Componenti core CIF, il supporto per `id` è stato rimosso e sostituito con `uid`. Adobe consiglia di utilizzare `uid` o `urlPath` come identificatore di categoria. Adobe continua a supportare `id` e `idAndUrlPath` solo per i progetti che utilizzano i Componenti core CIF versione 1.x.

Un esempio completo di funzionamento di `cifcategoryfield` è disponibile nel progetto [Componenti core CIF](https://github.com/adobe/aem-core-cif-components/blob/master/ui.apps/src/main/content/jcr_root/apps/core/cif/components/commerce/featuredcategorylist/v1/featuredcategorylist/_cq_dialog/.content.xml).
