---
title: Integrazione dell’interfaccia utente Crea corrispondenza con il portale personalizzato
seo-title: Integrating Create Correspondence UI with your custom portal
description: Scopri come integrare l’interfaccia utente per la corrispondenza con il tuo portale personalizzato
seo-description: Learn how to integrate create correspondence UI with your custom portal
uuid: 68ef5bf2-b271-4c44-8840-6c495069164d
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: 0d3bb98e-7139-4d8e-b110-6ebd11debda1
docset: aem65
feature: Correspondence Management
exl-id: c3b6ee31-ccbb-4446-86c8-f618226fefc4
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '413'
ht-degree: 4%

---

# Integrazione dell’interfaccia utente Crea corrispondenza con il portale personalizzato{#integrating-create-correspondence-ui-with-your-custom-portal}

## Panoramica {#overview}

Questo articolo descrive come integrare Crea soluzione di corrispondenza con il tuo ambiente.

## Chiamata basata su URL {#url-based-invocation}

Un modo per chiamare l’applicazione Crea corrispondenza da un portale personalizzato è quello di preparare l’URL con i seguenti parametri di richiesta:

* identificatore del modello di lettera (utilizzando il parametro cmLetterId ).

* l&#39;URL dei dati XML recuperati dall&#39;origine dati desiderata (utilizzando il parametro cmDataUrl ).

Ad esempio, il portale personalizzato prepara l’URL come\
`https://'[server]:[port]'/[contextPath]/aem/forms/createcorrespondence.html?random=[timestamp]&cmLetterId=[letter identifier]&cmDataUrl=[data URL]`, che potrebbe essere il href da un collegamento sul portale.

>[!NOTE]
>
>Le chiamate in questo modo non sono sicure in quanto i parametri necessari vengono trasmessi come richiesta di GET, esponendo gli stessi (chiaramente visibili) nell&#39;URL.

>[!NOTE]
>
>Prima di chiamare l’applicazione Create Correspondence, salva e carica i dati per chiamare l’interfaccia utente Create Correspondence in corrispondenza del dataURL specificato. Questo può essere fatto dal portale personalizzato stesso o attraverso un altro processo back-end.

## Chiamata in linea basata su dati {#inline-data-based-invocation}

Un altro modo (e più sicuro) per chiamare l&#39;applicazione Create Correspondence potrebbe essere semplicemente visitare l&#39;URL all&#39;indirizzo https://&#39;[server]:[porta]&#39;/[contextPath]/aem/forms/createcorrespondence.html, durante l’invio dei parametri e dei dati per chiamare l’applicazione Create Correspondence come richiesta di POST (nasconderli dall’utente finale). Ciò significa anche che ora è possibile trasmettere i dati XML per l&#39;applicazione Create Correspondence in linea (come parte della stessa richiesta, utilizzando il parametro cmData), che non era possibile/ideale nell&#39;approccio precedente.

### Parametri per la specifica della lettera {#parameters-for-specifying-letter}

| **Nome** | **Tipo** | **Descrizione** |
|---|---|---|
| cmLetterInstanceId | Stringa | Identificatore per l&#39;istanza della lettera. |
| cmLetterId | Stringa | Nome del modello Lettera. |

L’ordine dei parametri nella tabella specifica la preferenza dei parametri utilizzati per caricare la lettera.

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
   <td>Dati XML da un file di origine utilizzando protocolli di base come cq, ftp, http o file.<br /> </td> 
  </tr>
  <tr>
   <td>cmLetterInstanceId</td> 
   <td>Stringa</td> 
   <td>Utilizzo dei dati xml disponibili in Letter Instance.</td> 
  </tr>
  <tr>
   <td>cmUseTestData</td> 
   <td>Booleano</td> 
   <td>Per riutilizzare i dati di test allegati nel dizionario dati.</td> 
  </tr>
 </tbody>
</table>

L’ordine dei parametri nella tabella specifica la preferenza dei parametri utilizzati per caricare i dati XML.

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
   <td>True per aprire la lettera in modalità anteprima<br /> </td> 
  </tr>
  <tr>
   <td>Casuale</td> 
   <td>Timestamp</td> 
   <td>Per risolvere i problemi di memorizzazione in cache del browser.</td> 
  </tr>
 </tbody>
</table>

Se utilizzi il protocollo http o cq per cmDataURL, l&#39;URL di http/cq dovrebbe essere accessibile in modo anonimo.
