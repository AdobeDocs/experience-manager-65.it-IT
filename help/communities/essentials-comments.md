---
title: Elementi essenziali dei commenti
seo-title: Elementi essenziali dei commenti
description: Panoramica del componente Commenti
seo-description: Panoramica del componente Commenti
uuid: 58b7bb58-f598-4bcb-93ae-b7795cab51cd
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 18f54a1c-52aa-414d-b494-1f19b5c10345
translation-type: tm+mt
source-git-commit: c897f034edbdbeee74869165ed384c3408a857e0
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 4%

---


# Osservazioni Essentials {#comments-essentials}

Questa pagina fornisce le informazioni fondamentali sull’utilizzo del sistema di commenti (componente commenti) e delle opzioni per la gestione del contenuto generato dall’utente (UGC) prodotto quando i membri pubblicano commenti o risposte.

Il componente Commenti stabilisce un sistema di commenti in modo che ogni singolo post sia rappresentato da un componente Commento (singolo). È il sistema di commenti che viene incluso nella pagina. Il sistema dei commenti crea i singoli commenti quando viene richiamato.

## Essentials for Client-Side {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td> social/commons/components/hbs/comments</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>inclusa</strong></a></td>
   <td>Sì - le proprietà sono modificabili in <i>modalità di progettazione </i>modo</td>
  </tr>
  <tr>
   <td> <a href="client-customize.md#clientlibs-for-scf"><strong>clientlibs</strong></a></td>
   <td>cq.ckeditor<br /> cq.social.hbs.comments<br /> cq.social.hbs.registration</td>
  </tr>
  <tr>
   <td> <strong>templates</strong></td>
   <td> /libs/social/commons/components/hbs/comments/comments.hbs<br /> </td>
  </tr>
  <tr>
   <td> <strong>CSS</strong></td>
   <td> /libs/social/commons/components/hbs/comments/clientlibs/commentsystem.css</td>
  </tr>
  <tr>
   <td><strong> proprietà</strong></td>
   <td> Vedere <a href="comments.md">Uso dei commenti</a></td>
  </tr>
 </tbody>
</table>

[Personalizzazioni lato client](client-customize.md)

### Un&#39;istanza per pagina {#one-instance-per-page}

L’impaginazione e l’uso di URL per il caching e il collegamento richiedono che l’URL sia univoco per sistema di commenti. Pertanto, è consentita solo un&#39;istanza di un sistema di commenti per pagina.

Altre funzionalità includono già il sistema dei commenti. Secondo questi principi, il contenuto deve essere:

* [Blog](blog-developer-basics.md)
* [Calendario](calendar-basics-for-developers.md)
* [Libreria file](essentials-file-library.md)
* [Forum](essentials-forum.md)
* [D/R](qna-essentials.md)
* [Recensioni](reviews-basics.md)

### Elenco di motivi per segnalazione {#flag-reason-list}

L&#39;elenco dei motivi di segnalazione può essere personalizzato aggiungendo flagrasonlist.hbs all&#39;app per sovrascrivere il contenuto

* `/libs/social/commons/components/hbs/comments/comment/flagreasonlist.hbs`

Questo vale per qualsiasi componente che estende un sistema di commenti.

## Essentials for Server-Side {#essentials-for-server-side}

* [API Commenti](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/commons/comments/api/package-summary.html)

* [Endpoint commenti](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/commons/comments/endpoints/package-summary.html)

* [Personalizzazioni lato server](server-customize.md)

### Accesso ai commenti inviati (UGC) {#accessing-posted-comments-ugc}

UGC deve essere moderato utilizzando uno dei metodi standard per la moderazione.
Consultate [Moderazione dei contenuti generati dall&#39;utente](moderate-ugc.md).

A partire da AEM 6.1 Communities, l&#39;utilizzo di un [store comune](working-with-srp.md) per UGC include l&#39;accesso programmatico a UGC indipendentemente dall&#39;opzione di storage scelta (come ASRP, MSRP o JSRP).

**La posizione e il formato dell’UGC nel repository sono soggetti a modifiche senza preavviso**.

Consulta:

* [Panoramica](srp.md)  del provider delle risorse di storage - Introduzione e panoramica sull&#39;utilizzo dell&#39;archivio.
* [SRP e UGC Essentials](srp-and-ugc.md)  - Metodi e esempi di utilità SRP.
* [Accesso a UGC con linee guida SRP](accessing-ugc-with-srp.md) - Codifica.
* [Refactoring](socialutils.md)  SocialUtils - Mappatura di metodi di utilità obsoleti ai metodi di utilità SRP correnti.

