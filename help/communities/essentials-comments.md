---
title: Nozioni di base sui commenti
seo-title: Comments Essentials
description: Panoramica del componente Commenti
seo-description: Comments component overview
uuid: 58b7bb58-f598-4bcb-93ae-b7795cab51cd
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 18f54a1c-52aa-414d-b494-1f19b5c10345
exl-id: 8b4034f7-2f97-45ad-96d4-51cfbeae5991
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '344'
ht-degree: 4%

---

# Nozioni di base sui commenti {#comments-essentials}

Questa pagina fornisce le funzionalità essenziali per l’utilizzo del sistema di commenti (componente commenti) e le opzioni per la gestione del contenuto generato dall’utente (UGC) prodotto quando i membri pubblicano commenti o risposte.

Il componente commenti stabilisce un sistema di commento in modo che ogni singolo post sia rappresentato da un componente commento (singolare). È il sistema di commenti che viene incluso nella pagina. Il sistema di commento crea i singoli commenti quando viene richiamato.

## Funzionalità di base per lato client {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td> social/commons/components/hbs/comments</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>comprensivo</strong></a></td>
   <td>Sì - le proprietà sono modificabili in <i>progettazione </i>modalità</td>
  </tr>
  <tr>
   <td> <a href="client-customize.md#clientlibs-for-scf"><strong>clientlibs</strong></a></td>
   <td>cq.ckeditor<br /> cq.social.hbs.comments<br /> cq.social.hbs.vote</td>
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
   <td> Vedi <a href="comments.md">Utilizzo dei commenti</a></td>
  </tr>
 </tbody>
</table>

[Personalizzazioni lato client](client-customize.md)

### Una istanza per pagina {#one-instance-per-page}

L’impaginazione e l’uso degli URL per il caching e il collegamento richiedono che l’URL sia univoco per sistema di commenti. Pertanto, è consentita una sola istanza di un sistema di commenti per pagina.

Altre caratteristiche includono già il sistema di commenti. Secondo questi principi, il contenuto deve essere:

* [Blog](blog-developer-basics.md)
* [Calendario](calendar-basics-for-developers.md)
* [Libreria file](essentials-file-library.md)
* [Forum](essentials-forum.md)
* [D/R](qna-essentials.md)
* [Recensioni](reviews-basics.md)

### Elenco di motivi per segnalazione {#flag-reason-list}

L’elenco dei motivi di contrassegno può essere personalizzato aggiungendo flagreasonlist.hbs all’app per sovrascrivere l’elemento presente

* `/libs/social/commons/components/hbs/comments/comment/flagreasonlist.hbs`

Questo vale per qualsiasi componente che estende un sistema di commenti.

## Funzioni di base per lato server {#essentials-for-server-side}

* [API dei commenti](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/commons/comments/api/package-summary.html)

* [Endpoint commenti](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/commons/comments/endpoints/package-summary.html)

* [Personalizzazioni lato server](server-customize.md)

### Accesso ai commenti inviati (UGC) {#accessing-posted-comments-ugc}

UGC dovrebbe essere moderato utilizzando uno dei metodi standard per la moderazione.
Vedi [Moderazione dei contenuti generati dagli utenti](moderate-ugc.md).

A partire da AEM 6.1 Comunità, l&#39;uso di un [negozio comune](working-with-srp.md) per UGC include l&#39;accesso programmatico a UGC indipendentemente dall&#39;opzione di archiviazione scelta (come ASRP, MSRP o JSRP).

**La posizione e il formato dell’UGC nell’archivio sono soggetti a modifiche senza preavviso**.

Consulta:

* [Panoramica del provider di risorse di storage](srp.md) - Introduzione e panoramica sull’utilizzo dell’archivio.
* [Essenze SRP e UGC](srp-and-ugc.md) - Metodi ed esempi di utilità SRP.
* [Accesso a UGC con SRP](accessing-ugc-with-srp.md) - Linee guida per la codifica.
* [Refactoring di SocialUtils](socialutils.md) - Mappatura di metodi di utilità obsoleti ai metodi di utilità SRP correnti.
