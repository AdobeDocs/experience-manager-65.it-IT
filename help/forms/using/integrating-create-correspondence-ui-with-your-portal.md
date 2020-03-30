---
title: Integrazione dell'interfaccia utente Crea corrispondenza con il portale personalizzato
seo-title: Integrazione dell'interfaccia utente Crea corrispondenza con il portale personalizzato
description: Scopri come integrare l’interfaccia utente per la creazione della corrispondenza con il tuo portale personalizzato
seo-description: Scopri come integrare l’interfaccia utente per la creazione della corrispondenza con il tuo portale personalizzato
uuid: 68ef5bf2-b271-4c44-8840-6c495069164d
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: 0d3bb98e-7139-4d8e-b110-6ebd11debda1
docset: aem65
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# Integrazione dell&#39;interfaccia utente Crea corrispondenza con il portale personalizzato{#integrating-create-correspondence-ui-with-your-custom-portal}

## Panoramica {#overview}

In questo articolo viene illustrato come integrare la soluzione Crea corrispondenza con il proprio ambiente.

## Chiamata basata su URL {#url-based-invocation}

Un modo per chiamare l’applicazione Crea corrispondenza da un portale personalizzato è preparare l’URL con i seguenti parametri di richiesta:

* identificatore per il modello di lettera (utilizzando il parametro cmLetterId).

* l&#39;URL dei dati XML recuperati dall&#39;origine dati desiderata (utilizzando il parametro cmDataUrl).

Ad esempio, il portale personalizzato prepara l&#39;URL come\
`https://'[server]:[port]'/[contextPath]/aem/forms/createcorrespondence.html?random=[timestamp]&cmLetterId=[letter identifier]&cmDataUrl=[data URL]`, che può essere il href di un collegamento nel portale.

>[!NOTE]
>
>Le chiamate in questo modo non sono sicure poiché i parametri necessari vengono passati come una richiesta GET, esponendo lo stesso (chiaramente visibile) nell&#39;URL.

>[!NOTE]
>
>Prima di chiamare l’applicazione Crea corrispondenza, salvate e caricate i dati per chiamare l’interfaccia utente Crea corrispondenza all’URL data specificato. Questo può essere fatto dal portale personalizzato stesso o attraverso un altro processo back-end.

## Chiamata in linea basata sui dati {#inline-data-based-invocation}

Un altro metodo (e più sicuro) per chiamare l’applicazione Create Correspondence potrebbe essere quello di accedere semplicemente all’URL in https://&#39;[server]:[port]&#39;/[contextPath]/aem/forms/createcorrespondence.html, inviando i parametri e i dati per chiamare l’applicazione Create Correspondence come richiesta POST (nascondendoli dall’utente finale). Ciò significa anche che ora è possibile trasmettere i dati XML per l&#39;applicazione Create Correspondence in linea (come parte della stessa richiesta, utilizzando il parametro cmData), che non era possibile/ideale nell&#39;approccio precedente.

### Parametri per la specifica della lettera {#parameters-for-specifying-letter}

| **Nome** | **Tipo** | **Descrizione** |
|---|---|---|
| cmLetterInstanceId | Stringa | Identificatore per l’istanza della lettera. |
| cmLetterId | Stringa | Nome del modello Lettera. |

L&#39;ordine dei parametri nella tabella specifica la preferenza dei parametri utilizzati per caricare la lettera.

### Parametri per la specifica dell&#39;origine dati XML {#parameters-for-specifying-the-xml-data-source}

<table>
 <tbody>
  <tr>
   <td><strong>Nome</strong></td> 
   <td><strong>Tipo</strong></td> 
   <td><strong>Descrizione</strong></td> 
  </tr>
  <tr>
   <td>cmDataUrl<br /> </td> 
   <td>URL</td> 
   <td>Dati XML da un file di origine che utilizzano protocolli di base come cq, ftp, http o file.<br /> </td> 
  </tr>
  <tr>
   <td>cmLetterInstanceId</td> 
   <td>Stringa</td> 
   <td>Utilizzo dei dati xml disponibili in Letter Instance (Istanza Lettera).</td> 
  </tr>
  <tr>
   <td>cmUseTestData</td> 
   <td>Booleano</td> 
   <td>Per riutilizzare i dati di prova allegati nel dizionario dati.</td> 
  </tr>
 </tbody>
</table>

L&#39;ordine dei parametri nella tabella specifica la preferenza dei parametri utilizzati per caricare i dati XML.

### Altri parametri {#other-parameters}

<table>
 <tbody>
  <tr>
   <td><strong>Nome</strong></td> 
   <td><strong>Tipo</strong></td> 
   <td><strong>Descrizione</strong></td> 
  </tr>
  <tr>
   <td>cmPreview<br /> </td> 
   <td>Booleano</td> 
   <td>True per aprire la lettera in modalità di anteprima<br /> </td> 
  </tr>
  <tr>
   <td>Casuale</td> 
   <td>Timestamp</td> 
   <td>Per risolvere i problemi di memorizzazione nella cache del browser.</td> 
  </tr>
 </tbody>
</table>

Se utilizzate il protocollo http o cq per cmDataURL, l&#39;URL di http/cq dovrebbe essere accessibile in modo anonimo.
