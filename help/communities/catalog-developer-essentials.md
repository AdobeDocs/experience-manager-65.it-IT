---
title: Catalog Essentials
seo-title: Catalog Essentials
description: Panoramica del catalogo
seo-description: Panoramica del catalogo
uuid: 788512bb-fa38-48fb-a769-1eaae6bb95a1
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 542467ef-3793-4347-8424-c365c5a166f6
translation-type: tm+mt
source-git-commit: 41de9fff615b5b2f77d835740dfb1d33aa81e59b
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 3%

---


# Nozioni di base del catalogo {#catalog-essentials}

Questa pagina fornisce le informazioni essenziali per l&#39;utilizzo della funzione di catalogo per l&#39;abilitazione dei siti della community.

La funzione catalogo, se inclusa in un sito community, consente ai membri della community di sfogliare e selezionare le risorse di abilitazione elencate in un catalogo.

Il componente [ `enablement catalog` ](catalog.md) consente ai membri della community di accedere a un catalogo di [risorse di abilitazione](resources.md). L’utilizzo di tag AEM è una parte importante della gestione dell’aspetto delle risorse di abilitazione in un catalogo.

Vedere [Risorse per l&#39;abilitazione dei tag](tag-resources.md).

## Essentials for Client-Side {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/enablement/components/hbs/catalog</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>inclusa</strong></a></td>
   <td>No</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientllibs</strong></a></td>
   <td>cq.social.enablement.hbs.breadcrumbs<br /> cq.social.enablement.hbs.catalog<br /> cq.social.enablement.hbs.resource<br /> cq.social.enablement.hbs.learningpath</td>
  </tr>
  <tr>
   <td> <strong>templates</strong></td>
   <td> /libs/social/enablement/components/hbs/catalog/catalog.hbs<br /> </td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/enablement/components/hbs/catalog/clientlibs/catalog.css</td>
  </tr>
  <tr>
   <td><strong> proprietà</strong></td>
   <td>Vedere <a href="catalog.md">Funzioni del catalogo</a></td>
  </tr>
 </tbody>
</table>

## Essentials for Server-Side {#essentials-for-server-side}

### Funzione Catalogo {#catalog-function}

Una struttura del sito community che include la funzione [Catalog](functions.md#catalog-function), include un componente `enablement catalog` configurato.

### Pre-filtri {#pre-filters}

Quando una funzione Catalogo è stata aggiunta a un sito community, è possibile limitare le risorse di abilitazione e i percorsi di apprendimento visualizzati nel catalogo specificando un pre-filtro. A questo scopo, è possibile impostare le proprietà sull’istanza della risorsa catalogo per il sito.

Utilizzando l&#39;esempio della [Esercitazione di abilitazione](getting-started-enablement.md):

* Sull’autore
* Utilizzo di [CRXDE](../../help/sites-developing/developing-with-crxde-lite.md)

   * Ad esempio [https://&lt;server>:&lt;porta>/crx/de](http://localhost:4502/crx/de)

* Passate alla risorsa del catalogo nella pagina del catalogo

   * Esempio, `/content/sites/enable/en/catalog/jcr:content/content/primary/catalog`

* Aggiunta di un nodo di filtri figlio

   * Selezionare il nodo `catalog`
   * Selezionare **[!UICONTROL Crea nodo]**

      * Nome: `filters`
      * Tipo: `nt:unstructured`
      * Selezionare **[!UICONTROL Salva tutto]**

* Aggiungi la proprietà `se_resource-tags` al nodo `filters`

   * Selezionare il nodo `filters`
   * Aggiungere una proprietà Multi

      * Nome: `se_resource-tags`
      * Tipo: Stringa
      * Valore: *&lt;immettere un [TagID](#pre-filter-tagids)>*
         * Selezionare **[!UICONTROL Multi]**
         * Selezionare **[!UICONTROL Aggiungi]**

            * Nella finestra di dialogo a comparsa, selezionare `+` per aggiungere altri ID di tag pre-filtro

* Ripubblica il sito della community

![configure-catalog](assets/configure-catalog.png)

#### ID tag pre-filtro {#pre-filter-tagids}

Il pre-filtro [TagIDs](../../help/sites-developing/framework.md#tagid) deve corrispondere esattamente ai tag applicati alle risorse di abilitazione. Questi sono visibili nella cartella `resources` del sito come valori della proprietà `se_resource-tags`.

![configure-Filters](assets/configure-catalog1.png)

### API di riferimento {#reference-apis}

* [API di abilitazione](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/enablement/client/api/package-summary.html)

* [API di reporting](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/enablement/client/reporting/api/package-summary.html)

* [API di Reporting Analytics](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/enablement/client/reporting/analytics/api/package-summary.html)

