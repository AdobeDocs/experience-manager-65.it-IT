---
title: Utilizzo del selettore di prodotti e categorie CIF
description: Scopri come utilizzare il selettore di prodotti e categorie CIF nei componenti per l’e-commerce dei clienti per supportare autori ed esperti di marketing a lavorare in modo efficiente con i dati di catalogo e i prodotti commerce.
sub-product: Commerce
topics: Development
version: Cloud Service
activity: develop
audience: developer
feature: Commerce Integration Framework
exl-id: 1e7c3748-92b5-45f1-8dd9-f1816e3e34aa
source-git-commit: db0e9d6105484b37e2e21e49bf0f95cef9da2a62
workflow-type: tm+mt
source-wordcount: '563'
ht-degree: 0%

---

# Picker per l’authoring di contenuti AEM e Commerce {#cif-pickers}

L’authoring di contenuti e commercio AEM fornisce una serie di strumenti di authoring per aiutare gli autori e gli esperti di marketing AEM a lavorare in modo efficiente con i dati di prodotto e i cataloghi commerciali. Il selettore prodotti e il selettore categorie fanno parte del componente aggiuntivo CIF e sono utilizzati dai componenti core CIF. I progetti possono utilizzare questi selettori in qualsiasi finestra di dialogo dei componenti per selezionare prodotti o categorie.

## Selettore prodotti {#product-picker}

Per utilizzare il selettore prodotti in un componente del progetto, uno sviluppatore deve aggiungere `commerce/gui/components/common/cifproductfield` nella finestra di dialogo di un componente. Ad esempio, utilizza quanto segue per `cq:dialog`:

```xml
<product jcr:primaryType="nt:unstructured"
    sling:resourceType="commerce/gui/components/common/cifproductfield"
    fieldDescription="The product or product variant displayed by the teaser"
    fieldLabel="Select Product"
    filter="folderOrProductOrVariant"
    name="./selection"
    selectionId="sku"/>
```

Il campo prodotto consente di navigare fino al prodotto che un utente desidera selezionare tramite le diverse visualizzazioni. Per impostazione predefinita, il campo prodotto restituisce l’ID del prodotto, ma può essere configurato utilizzando `selectionId` attributo.

Il campo del selettore prodotti supporta le seguenti proprietà facoltative:

- selectionId (id, uid, sku, slug, combinedSlug, combinedSku): consente di scegliere l’attributo del prodotto che deve essere restituito dal selettore (impostazione predefinita = id). Se si utilizza lo sku, viene restituito lo sku del prodotto selezionato mentre si utilizza lo sku combinato e viene restituita una stringa come base#variante con lo sku del prodotto di base e della variante selezionata oppure un singolo sku se è selezionato un prodotto di base.
- filter (folderOrProduct, folderOrProductOrVariant) - filtra il contenuto di cui eseguire il rendering dal selettore durante l’esplorazione della struttura del prodotto. folderOrProduct - esegue il rendering di cartelle e prodotti. folderOrProductOrVariant - esegue il rendering di cartelle, prodotti e varianti di prodotti. Se viene eseguito il rendering di un prodotto o di una variante di prodotto, questo diventa selezionabile anche nel selettore. (impostazione predefinita = folderOrProduct)
- multiple (true, false): consente di selezionare uno o più prodotti (default = false)
- emptyText: per configurare il valore di testo vuoto del campo selettore

Inoltre, le proprietà dei campi della finestra di dialogo standard come `name`, `fieldLabel`, o `fieldDescription`, sono supportate.

>[!CAUTION]
>
>Il `cifproductfield` il componente richiede `cif.shell.picker` clientlib. Per aggiungere una libreria client a una finestra di dialogo, puoi utilizzare la proprietà extraClientlibs.
>[!CAUTION]
>
>A partire dalla versione 2.0.0 dei Componenti core CIF, il supporto per `id` è stato rimosso e sostituito con `uid`. L’Adobe consiglia di utilizzare `sku` o `slug` come identificatore del prodotto. Adobe continua a supportare `id` solo per i progetti che utilizzano i Componenti core CIF versione 1.x.

Un esempio di funzionamento completo del `cifproductfield` si trova nella sezione [Componenti core CIF](https://github.com/adobe/aem-core-cif-components/blob/master/ui.apps/src/main/content/jcr_root/apps/core/cif/components/commerce/productteaser/v1/productteaser/_cq_dialog/.content.xml) progetto. Vedi anche [Personalizzazione delle finestre di dialogo](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/customizing.html#customizing-dialogs) della documentazione dei Componenti core AEM.

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

- selectionId(id, uid, slug, urlPath, idAndUrlPath _(obsoleto)_, uidAndUrlPath _(obsoleto)_) - consente di scegliere l&#39;attributo di categoria che deve essere restituito dal selettore (impostazione predefinita = id).
- multiple (true, false): abilita la selezione di una o più categorie (default = false)

Inoltre, le proprietà dei campi della finestra di dialogo standard come `name`, `fieldLabel`, o `fieldDescription` sono supportati anche.

>[!CAUTION]
>
>Come il `cifproductfield` componente il `cifcategoryfield` richiede anche il `cif.shell.picker` clientlib. Per aggiungere una libreria client a una finestra di dialogo, puoi utilizzare `extraClientlibs` proprietà. Consulta [Personalizzazione delle finestre di dialogo](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/customizing.html#customizing-dialogs) della documentazione dei Componenti core AEM.
>[!CAUTION]
>
>A partire dalla versione 2.0.0 dei Componenti core CIF, il supporto per `id` è stato rimosso e sostituito con `uid`. L’Adobe consiglia di utilizzare `uid` o `urlPath` come identificatore di categoria. Adobe continua a supportare `id` E `idAndUrlPath` solo per i progetti che utilizzano i Componenti core CIF versione 1.x.

Un esempio di funzionamento completo del `cifcategoryfield` si trova nella sezione [Componenti core CIF](https://github.com/adobe/aem-core-cif-components/blob/master/ui.apps/src/main/content/jcr_root/apps/core/cif/components/commerce/featuredcategorylist/v1/featuredcategorylist/_cq_dialog/.content.xml) progetto.
