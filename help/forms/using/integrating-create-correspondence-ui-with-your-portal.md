---
title: Integrazione dell’interfaccia utente per la creazione di corrispondenza con il portale personalizzato
description: Scopri come integrare l’interfaccia utente per la creazione di corrispondenza con il portale personalizzato
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
docset: aem65
feature: Correspondence Management
exl-id: c3b6ee31-ccbb-4446-86c8-f618226fefc4
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '413'
ht-degree: 4%

---

# Integrazione dell’interfaccia utente per la creazione di corrispondenza con il portale personalizzato{#integrating-create-correspondence-ui-with-your-custom-portal}

## Panoramica {#overview}

Questo articolo illustra come integrare la soluzione Create Correspondence con il tuo ambiente.

## Chiamata basata su URL {#url-based-invocation}

Un modo per chiamare l’applicazione Create Correspondence da un portale personalizzato consiste nel preparare l’URL con i seguenti parametri di richiesta:

* l’identificatore per il modello di lettera (utilizzando il parametro cmLetterId).

* URL dei dati XML recuperati dall&#39;origine dati desiderata (utilizzando il parametro cmDataUrl).

Ad esempio, il portale personalizzato prepara l’URL come\
`https://'[server]:[port]'/[contextPath]/aem/forms/createcorrespondence.html?random=[timestamp]&cmLetterId=[letter identifier]&cmDataUrl=[data URL]`, che potrebbe essere il href da un collegamento sul portale.

>[!NOTE]
>
>Una chiamata di questo tipo non è sicura in quanto i parametri necessari vengono trasmessi come richiesta di GET esponendo lo stesso (chiaramente visibile) nell’URL.

>[!NOTE]
>
>Prima di richiamare l’applicazione Create Correspondence, salva e carica i dati per richiamare l’interfaccia utente Create Correspondence in corrispondenza dell’URL dati specificato. Questa operazione può essere eseguita dal portale personalizzato stesso o attraverso un altro processo back-end.

## Chiamata basata su dati in linea {#inline-data-based-invocation}

Un altro modo (e più sicuro) per chiamare l&#39;applicazione Create Correspondence potrebbe essere quello di premere semplicemente l&#39;URL su https://&#39;[server]:[porta]&#39;/[contextPath]/aem/forms/createcorrespondence.html, mentre si inviano parametri e dati per chiamare l&#39;applicazione Create Correspondence come richiesta POST (nascondendoli all&#39;utente finale). Ciò significa anche che ora puoi trasmettere in linea i dati XML per l’applicazione Create Correspondence (come parte della stessa richiesta, utilizzando il parametro cmData), che non era possibile/ideale nell’approccio precedente.

### Parametri per specificare la lettera {#parameters-for-specifying-letter}

| **Nome** | **Tipo** | **Descrizione** |
|---|---|---|
| cmLetterInstanceId | Stringa | Identificatore per l’istanza della lettera. |
| cmLetterId | Stringa | Nome del modello Lettera. |

L&#39;ordine dei parametri nella tabella specifica la preferenza dei parametri utilizzati per il caricamento della lettera.

### Parametri per specificare l&#39;origine dati XML {#parameters-for-specifying-the-xml-data-source}

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
   <td>Dati XML da un file di origine utilizzando protocolli di base quali cq, ftp, http o file.<br /> </td> 
  </tr>
  <tr>
   <td>cmLetterInstanceId</td> 
   <td>Stringa</td> 
   <td>Utilizzo dei dati xml disponibili nell’istanza della lettera.</td> 
  </tr>
  <tr>
   <td>cmUseTestData</td> 
   <td>Booleano</td> 
   <td>Per riutilizzare i dati di test allegati al dizionario dati.</td> 
  </tr>
 </tbody>
</table>

L&#39;ordine dei parametri nella tabella specifica la preferenza dei parametri utilizzati per il caricamento dei dati XML.

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
   <td>Marca temporale</td> 
   <td>Per risolvere i problemi di memorizzazione nella cache del browser.</td> 
  </tr>
 </tbody>
</table>

Se utilizzi il protocollo http o cq per cmDataURL, l’URL di http/cq deve essere accessibile in modo anonimo.
