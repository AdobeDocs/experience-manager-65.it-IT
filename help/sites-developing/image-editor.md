---
title: Editor immagine
seo-title: Editor immagine
description: L’Editor immagine è un elemento fondamentale di AEM e può essere sfruttato dai componenti per facilitare la manipolazione delle immagini da parte degli autori di contenuti.
seo-description: L’Editor immagine è un elemento fondamentale di AEM e può essere sfruttato dai componenti per facilitare la manipolazione delle immagini da parte degli autori di contenuti.
uuid: de6ac71b-380a-4b67-b697-ac34a79a9cc4
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: components
discoiquuid: f6347492-cf48-4835-b8fd-ce9a75a09abe
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '331'
ht-degree: 6%

---


# Editor immagine{#image-editor}

L’Editor immagine è un elemento fondamentale di AEM e può essere sfruttato dai componenti per facilitare la manipolazione delle immagini da parte degli autori di contenuti.

>[!CAUTION]
>
>Per utilizzare le funzioni dell&#39;Editor immagini descritte in questo articolo, è necessario installare il [feature pack 24267](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq640/featurepack/cq-6.4.0-featurepack-24267).

## Unità relative per mappa immagine {#relative-units-for-image-map}

L’Editor immagine persiste nelle aree delle mappe immagine sia come unità assolute che come unità relative. Le unità relative sono utili se fornite come attributi di dati per ridimensionare dinamicamente una mappa immagine (relativa alle dimensioni dell’immagine) sul lato client in un componente immagine reattivo.

### imageMap, proprietà {#imagemap-property}

Le coordinate della mappa immagine vengono memorizzate in JCR come proprietà `imageMap` dall’Editor immagini. Ha il seguente formato.

Le aree di mappa vengono memorizzate nel modo seguente:

`[area1][area2][...]`

Formato area:

`[SHAPE(COORDINATES)"HREF"|"TARGET"|"ALT"|(RELATIVE_COORDINATES)]`

Esempio:

`[rect(0,0,10,10)"https://www.adobe.com"|"_self"|"alt"|(0,0,0.8,0.8)]`
`[circle(10,10,10)"https://www.adobe.com"|"_self"|"alt"|(0.8,0.8,0.8)]`

## Supporto per immagini SVG {#support-for-svg-images}

La grafica vettoriale scalabile (SVG) è supportata dall’Editor immagini.

* Sono supportati il trascinamento di una risorsa SVG da DAM e il caricamento di un file SVG da un file system locale.

## Abilitazione dei plug-in per tipo MIME {#enabling-plugins-by-mime-type}

In alcune situazioni le azioni di creazione devono essere limitate per alcuni tipi MIME, a causa della mancanza di supporto nell&#39;elaborazione sul lato server. Ad esempio, la modifica di immagini SVG potrebbe non essere consentita.

I plug-in nell&#39;Editor immagine possono essere attivati selettivamente dal tipo MIME impostando una proprietà `supportedMimeTypes` sul nodo di configurazione del singolo plug-in.

### Esempio {#example}

Ad esempio, è possibile ritagliare solo le immagini GIF, JPEG, PNG, WEBP e TIFF.

La proprietà `supportedMimeTypes` deve quindi essere impostata come una stringa dei tipi MIME consentiti sul nodo di configurazione del plug-in sul nodo `cq:editConfig` del componente immagine.

`/apps/core/wcm/components/image/v2/image/cq:editConfig`

```xml
 jcr:primaryType="cq:EditConfig">
     <cq:dropTargets jcr:primaryType="nt:unstructured">
         <image ...>
            ...
         </image>
     </cq:dropTargets>
     <cq:inplaceEditing
         jcr:primaryType="cq:InplaceEditingConfig"
         active="{Boolean}true"
         editorType="image">
         <config jcr:primaryType="nt:unstructured">
             <plugins jcr:primaryType="nt:unstructured">
                 <crop
                     jcr:primaryType="nt:unstructured"
                     supportedMimeTypes="[image/gif,image/jpeg,image/png,image/webp,image/tiff]"
                     features="*">
                     <aspectRatios jcr:primaryType="nt:unstructured">
                        ...
                     </aspectRatios>
                 </crop>
                 ...
             </plugins>
             <ui jcr:primaryType="nt:unstructured">
                 ...
             </ui>
         </config>
     </cq:inplaceEditing>
 </jcr:root>
```

