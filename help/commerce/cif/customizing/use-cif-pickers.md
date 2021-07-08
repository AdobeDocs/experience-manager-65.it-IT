---
title: Utilizzo del selettore di prodotti e categorie CIF
description: Scopri come utilizzare il selettore di prodotti e categorie CIF nei componenti per l’e-commerce dei clienti per supportare autori e professionisti del marketing nell’utilizzo efficiente dei dati di catalogo e di prodotto commerce.
sub-product: Commerce
topics: Development
version: cloud-service
activity: develop
audience: developer
feature: Commerce Integration Framework
exl-id: 1e7c3748-92b5-45f1-8dd9-f1816e3e34aa
source-git-commit: 2fadfa65242b208a750b0d5392fdd2c41e9ff20e
workflow-type: tm+mt
source-wordcount: '627'
ht-degree: 0%

---

# Selezione AEM contenuti e contenuti commerce {#cif-pickers}

AEM Content &amp; Commerce Authoring fornisce una serie di strumenti di authoring per aiutare AEM autori e gli addetti al marketing a lavorare in modo efficiente con i dati e i cataloghi dei prodotti commerce. Il selettore dei prodotti e il selettore delle categorie fanno parte del componente aggiuntivo CIF e vengono utilizzati dai componenti core CIF. I progetti possono utilizzare questi selettori in qualsiasi finestra di dialogo dei componenti per selezionare prodotti o categorie.

## Selettore prodotti {#product-picker}

Per utilizzare il selettore dei prodotti in un componente del progetto, uno sviluppatore deve aggiungere `commerce/gui/components/common/cifproductfield` a una finestra di dialogo di un componente. Ad esempio, utilizza quanto segue per cq:dialog:

```xml
<product jcr:primaryType="nt:unstructured"
    sling:resourceType="commerce/gui/components/common/cifproductfield"
    fieldDescription="The product or product variant displayed by the teaser"
    fieldLabel="Select Product"
    filter="folderOrProductOrVariant"
    name="./selection"
    selectionId="sku"/>
```

Il campo prodotto consente di navigare al prodotto che un utente desidera selezionare tramite le diverse viste. Per impostazione predefinita, il campo prodotto restituisce l’ID del prodotto, ma può essere configurato utilizzando l’attributo `selectionId` .

Il campo del selettore prodotti supporta le seguenti proprietà facoltative:

- selectionId (id, uid, sku, lumg, combinedSlug, combinedSku) - consente di scegliere l’attributo di prodotto che deve essere restituito dal selettore (default = id). Utilizzando lo SKU si restituisce lo SKU del prodotto selezionato, mentre si utilizza l&#39;opzione combinatoSku e restituisce una stringa come base#variant con lo SKU del prodotto di base e la variante selezionata, oppure una singola SKU se è selezionato un prodotto di base.
- filter (folderOrProduct, folderOrProductOrVariant) - filtra il contenuto di cui deve essere eseguito il rendering dal selettore durante la navigazione nella struttura del prodotto. folderOrProduct - esegue il rendering di cartelle e prodotti. folderOrProductOrVariant - esegue il rendering di cartelle, varianti di prodotti e prodotti. Se viene eseguito il rendering di una variante di prodotto o prodotto, questa diventa selezionabile anche nel selettore. (predefinito = folderOrProduct)
- multiple (true, false) - abilita la selezione di uno o più prodotti (default = false)
- emptyText - per configurare il valore di testo vuoto del campo picker

Inoltre, sono supportate anche le proprietà dei campi del registro grafico standard come `name`, `fieldLabel` o `fieldDescription`.

>[!CAUTION]
>
>Il componente `cifproductfield` richiede la clientlib `cif.shell.picker`. Per aggiungere una clientlib a una finestra di dialogo, puoi utilizzare la proprietà extraClientlibs .
>[!CAUTION]
>
>A partire dalla versione 2.0.0 dei componenti core CIF, il supporto per `id` è stato rimosso e sostituito con `uid`. È vivamente consigliato utilizzare `sku` o `slug` come identificatore del prodotto. Continuiamo a supportare `id` solo per i progetti che utilizzano la versione 1.x dei componenti core CIF.

Un esempio di funzionamento completo di `cifproductfield` è disponibile nel progetto [CIF Core Components](https://github.com/adobe/aem-core-cif-components/blob/master/ui.apps/src/main/content/jcr_root/apps/core/cif/components/commerce/productteaser/v1/productteaser/_cq_dialog/.content.xml) . Consulta anche [Personalizzazione delle finestre di dialogo](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/customizing.html?lang=en#customizing-dialogs) della documentazione dei componenti core AEM.

## Selettore categoria {#category-picker}

Il selettore categoria può essere utilizzato in una finestra di dialogo di un componente e in modo simile al selettore del prodotto.

Il seguente snippet può essere utilizzato in una configurazione cq:dialog:

```xml
<category jcr:primaryType="nt:unstructured" 
    sling:resourceType="commerce/gui/components/common/cifcategoryfield" 
    fieldLabel="Category" 
    name="./categoryId" 
    selectionId="uid" />
```

Il campo del selettore delle categorie supporta le seguenti proprietà facoltative:

- selectionId(id, uid, slug, urlPath, idAndUrlPath _(obsoleto)_, uidAndUrlPath _(obsoleto)_) consente di scegliere l&#39;attributo della categoria che deve essere restituito dal selettore (predefinito = id).
- multiple (true, false) - abilita la selezione di una o più categorie (default = false)

Inoltre, sono supportate anche le proprietà dei campi del registro grafico standard come `name`, `fieldLabel` o `fieldDescription`.

>[!CAUTION]
>
>Come il componente `cifproductfield`, anche il componente `cifcategoryfield` richiede la clientlib `cif.shell.picker`. Per aggiungere una clientlib a una finestra di dialogo, puoi utilizzare la proprietà `extraClientlibs` . Consulta [Personalizzazione delle finestre di dialogo](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/customizing.html?lang=en#customizing-dialogs) della documentazione sui componenti core AEM .
>[!CAUTION]
>
>A partire dalla versione 2.0.0 dei componenti core CIF, il supporto per `id` è stato rimosso e sostituito con `uid`. È vivamente consigliabile utilizzare `uid` o `urlPath` come identificatore di categoria. Continuiamo a supportare `id` e `idAndUrlPath` solo per i progetti che utilizzano i componenti core CIF versione 1.x.

Un esempio di funzionamento completo di `cifcategoryfield` è disponibile nel progetto [CIF Core Components](https://github.com/adobe/aem-core-cif-components/blob/master/ui.apps/src/main/content/jcr_root/apps/core/cif/components/commerce/featuredcategorylist/v1/featuredcategorylist/_cq_dialog/.content.xml) .
