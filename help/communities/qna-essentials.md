---
title: Nozioni di base su QnA
seo-title: QnA Essentials
description: Funzione forum Domande e risposte
seo-description: Questions and answers forum feature
uuid: c718a8e3-b3bd-4db9-8c0f-6dd973d40583
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: ceace3aa-78a5-485e-b519-630479e087d8
exl-id: a7b295c1-cc9d-4881-8016-804b21fc1098
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 2%

---

# Nozioni di base su QnA {#qna-essentials}

Questa pagina fornisce le informazioni essenziali per l’utilizzo della funzione forum Domande e Risposte (QnA).

## Funzionalità di base per lato client {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> resourceType</td>
   <td>social/qna/components/hbs/qnaforum</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component">comprensivo</a></td>
   <td>No</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md">clientlibs</a></td>
   <td>cq.ckeditor<br /> cq.social.hbs.vote<br /> cq.social.hbs.qna</td>
  </tr>
  <tr>
   <td> templates</td>
   <td> /libs/social/qna/components/hbs/qnaforum/qnaforum.hbs<br /> /libs/social/qna/components/hbs/qnaforum/activity-title.hbs</td>
  </tr>
  <tr>
   <td> css</td>
   <td> /libs/social/qna/components/hbs/qnaforum/clientlibs/qnaforum.css</td>
  </tr>
  <tr>
   <td> proprietà</td>
   <td>Vedi <a href="working-with-qna.md">Funzione forum Q&amp;A</a></td>
  </tr>
 </tbody>
</table>

* [Personalizzazioni lato client](client-customize.md)

## Funzioni di base per lato server {#essentials-for-server-side}

* [API QnA](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/qna/client/api/package-summary.html)

* [Endpoint QnA](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/qna/client/endpoints/package-summary.html)

* [Personalizzazioni lato server](server-customize.md)

### Funzione D/R {#qna-function}

Una struttura del sito community che include [Funzione QnA](functions.md#qna-function) avrà configurato un `QnA` , nonché le impostazioni che influiscono sulla moderazione e l’assegnazione tag. La funzione QnA supporta l&#39;identificazione di un [gruppo utenti membro privilegiato](users.md#privileged-members-group).

### Accesso ai post del forum QnA (UGC) {#accessing-qna-forum-posts-ugc}

UGC dovrebbe essere moderato utilizzando uno dei metodi standard per la moderazione.
Vedi [Moderazione dei contenuti generati dagli utenti](moderate-ugc.md).

A partire da AEM 6.1 Comunità, l&#39;uso di un [negozio comune](working-with-srp.md) per UGC include l&#39;accesso programmatico a UGC indipendentemente dall&#39;opzione di archiviazione scelta (come ASRP, MSRP o JSRP).

**La posizione e il formato dell’UGC nell’archivio sono soggetti a modifiche senza preavviso**.

Consulta:

* [Panoramica del provider di risorse di storage](srp.md) - introduzione e panoramica sull’utilizzo dell’archivio.
* [Essenze SRP e UGC](srp-and-ugc.md) - Metodi ed esempi di utilità SRP.
* [Accesso a UGC con SRP](accessing-ugc-with-srp.md) - linee guida per la codifica.
* [Refactoring di SocialUtils](socialutils.md) - mappatura di metodi di utilità obsoleti ai metodi di utilità SRP correnti.
