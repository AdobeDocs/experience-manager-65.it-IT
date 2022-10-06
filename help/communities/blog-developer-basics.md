---
title: Blog Essentials
seo-title: Blog Essentials
description: Panoramica del blog
seo-description: Blog overview
uuid: 714cf70c-76a0-4be6-9163-a31ac6bd1643
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: eece7b8f-6ccd-4037-8713-0cd36cfd9e73
docset: aem65
exl-id: 51f616e8-4aba-47f6-b948-d5147d84bbb6
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 2%

---

# Blog Essentials {#blog-essentials}

A partire da AEM 6.1 Communities, un blog è un&#39;attività comunitaria. Gli articoli di blog vengono ora pubblicati dall&#39;ambiente di pubblicazione, dove in precedenza gli articoli di blog potevano essere creati solo nell&#39;ambiente di authoring e pubblicati.

Gli articoli di blog possono ora essere creati da qualsiasi membro della comunità, a meno che non siano limitati ai membri privilegiati.

Questa pagina fornisce le informazioni essenziali per l’utilizzo della funzione blog.

>[!NOTE]
>
>L&#39;infrastruttura sottostante della funzione blog è la funzione di diario.

## Funzionalità di base per lato client {#essentials-for-client-side}

La funzione blog è composta da due componenti principali disponibili aggiungendo il [Funzione blog](/help/communities/functions.md#blog-function) oppure aggiungendo i componenti a una pagina in modalità di modifica dell’autore.

### Blog {#blog}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/journal/components/hbs/journal</td>
  </tr>
  <tr>
   <td> <a href="/help/communities/scf.md#add-or-include-a-communities-component"><strong>comprensivo</strong></a></td>
   <td>No</td>
  </tr>
  <tr>
   <td> <a href="/help/communities/clientlibs.md"><strong>clientlibs</strong></a></td>
   <td>cq.ckeditor<br /> cq.social.hbs.vote<br /> cq.social.hbs.journal</td>
  </tr>
  <tr>
   <td> <strong>templates</strong></td>
   <td> /libs/social/journal/components/hbs/journal/journal.hbs<br /> /libs/social/journal/components/hbs/entry_topic/list-item.hbs</td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/journal/components/hbs/journal/clientlibs/journal.css</td>
  </tr>
  <tr>
   <td><strong> proprietà</strong></td>
   <td>vedere <a href="/help/communities/blog-feature.md">Funzione blog</a></td>
  </tr>
 </tbody>
</table>

### Barra laterale blog {#blog-sidebar}

| **resourceType** | social/journal/components/hbs/sidebar |
|---|---|
| [**comprensivo**](/help/communities/scf.md#add-or-include-a-communities-component) | No |
| [**clientlibs**](/help/communities/clientlibs.md) | cq.social.hbs.journal_sidebar |
| **modelli** | /libs/social/journal/components/hbs/sidebar/sidebar.hbs |
| **css** | /libs/social/journal/components/hbs/sidebar/clientlibs/sidebar.css |
| **proprietà** | vedere [Funzione blog](/help/communities/blog-feature.md) |

* [Personalizzazioni lato client](/help/communities/client-customize.md)

## Funzioni di base per lato server {#essentials-for-server-side}

* [API blog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/journal/client/api/package-summary.html)

* [Endpoint blog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/journal/client/endpoints/package-summary.html)

* [Personalizzazioni lato server](/help/communities/server-customize.md)

### Funzione Blog {#blog-function}

Una struttura del sito community che include [Funzione blog](/help/communities/functions.md#blog-function) avrà configurato `Blog` e `Blog Sidebar` componenti. La funzione Blog supporta l&#39;identificazione di un [gruppo utenti membro privilegiato](/help/communities/users.md#privileged-members-group).

### Accesso alle voci di blog (UGC) {#accessing-blog-entries-ugc}

UGC dovrebbe essere moderato utilizzando uno dei metodi standard per la moderazione.
Vedi [Moderazione dei contenuti generati dagli utenti](/help/communities/moderate-ugc.md).

A partire da AEM 6.1 Comunità, l&#39;uso di un [negozio comune](/help/communities/working-with-srp.md) per UGC include l&#39;accesso programmatico a UGC indipendentemente dall&#39;opzione di archiviazione scelta (come ASRP, MSRP o JSRP).

**La posizione e il formato dell’UGC nell’archivio sono soggetti a modifiche senza preavviso**.

Consulta :

* [Panoramica del provider di risorse di storage](/help/communities/srp.md) - introduzione e panoramica sull’utilizzo dell’archivio.
* [Essenze SRP e UGC](/help/communities/srp-and-ugc.md) - Metodi ed esempi di utilità SRP.
* [Accesso a UGC con SRP](/help/communities/accessing-ugc-with-srp.md) - linee guida per la codifica.
* [Refactoring di SocialUtils](/help/communities/socialutils.md) - mappatura di metodi di utilità obsoleti ai metodi di utilità SRP correnti.

## Editore principale {#primary-publisher}

Quando la distribuzione è una farm di pubblicazione, è necessario identificare un editore principale che eseguirà il polling per gli articoli pianificati da pubblicare.

Vedi [Editore principale](/help/communities/deploy-communities.md#primary-publisher) per ulteriori dettagli.

## Consentire contenuti multimediali avanzati {#allowing-rich-media}

La piattaforma AEM blocca i collegamenti da altri siti web per prevenire attacchi XSS come descritto in

* [Protect contro lo scripting tra siti (XSS)](/help/sites-developing/security.md#protect-against-cross-site-scripting-xss)

A partire da AEM 6.2, le modifiche precedentemente necessarie per essere fatte manualmente sono incluse nel file di configurazione predefinito di AntiSamy.

I contenuti rich media vengono incorporati in un articolo del blog selezionando `Embed Media from External Sites` icona :

![media](assets/media-icon.png)
