---
title: Blog Essentials
seo-title: Blog Essentials
description: Panoramica del blog
seo-description: Panoramica del blog
uuid: 714cf70c-76a0-4be6-9163-a31ac6bd1643
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: eece7b8f-6ccd-4037-8713-0cd36cfd9e73
docset: aem65
translation-type: tm+mt
source-git-commit: e74d39e63f8b3b5961ea2c31e0ef99c3ab8b06dd
workflow-type: tm+mt
source-wordcount: '446'
ht-degree: 2%

---


# Blog Essentials {#blog-essentials}

A partire da AEM 6.1 Communities, un blog è un&#39;attività della community. Gli articoli dei blog vengono ora pubblicati dall&#39;ambiente di pubblicazione, dove in precedenza, gli articoli dei blog potevano essere creati solo nell&#39;ambiente di authoring e pubblicati.

Gli articoli di blog possono ora essere creati da qualsiasi membro della community, a meno che non siano limitati ai membri privilegiati.

Questa pagina contiene le informazioni essenziali per l’utilizzo della funzione blog.

>[!NOTE]
>
>L&#39;infrastruttura sottostante della funzione blog è la funzione journal.


## Essentials for Client-Side {#essentials-for-client-side}

La funzione blog è composta da due componenti principali disponibili aggiungendo la funzione [](/help/communities/functions.md#blog-function) Blog o aggiungendo i componenti a una pagina in modalità di modifica dell’autore.

### Blog {#blog}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/journal/components/hbs/journal</td>
  </tr>
  <tr>
   <td> <a href="/help/communities/scf.md#add-or-include-a-communities-component"><strong>inclusa</strong></a></td>
   <td>No</td>
  </tr>
  <tr>
   <td> <a href="/help/communities/clientlibs.md"><strong>clientllibs</strong></a></td>
   <td>cq.ckeditor<br /> cq.social.hbs.Voto<br /> cq.social.hbs.journal</td>
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
   <td>consulta Funzione <a href="/help/communities/blog-feature.md">Blog</a></td>
  </tr>
 </tbody>
</table>

### Barra laterale blog {#blog-sidebar}

| **resourceType** | social/journal/components/hbs/sidebar |
|---|---|
| [**inclusa **](/help/communities/scf.md#add-or-include-a-communities-component) | No |
| [**clientllibs **](/help/communities/clientlibs.md) | cq.social.hbs.journal_sidebar |
| **templates** | /libs/social/journal/components/hbs/sidebar/sidebar.hbs |
| **css** | /libs/social/journal/components/hbs/sidebar/clientlibs/sidebar.css |
| **proprietà** | consulta Funzione [Blog](/help/communities/blog-feature.md) |

* [Personalizzazioni lato client](/help/communities/client-customize.md)

## Essentials for Server-Side {#essentials-for-server-side}

* [API blog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/journal/client/api/package-summary.html)

* [Endpoint blog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/journal/client/endpoints/package-summary.html)

* [Personalizzazioni lato server](/help/communities/server-customize.md)

### Funzione Blog {#blog-function}

Una struttura del sito community che include la funzione [](/help/communities/functions.md#blog-function) Blog avrà configurato `Blog` e `Blog Sidebar` componenti. La funzione Blog supporta l&#39;identificazione di un gruppo [utenti membro](/help/communities/users.md#privileged-members-group)privilegiato.

### Accesso a voci di blog (UGC) {#accessing-blog-entries-ugc}

UGC deve essere moderato utilizzando uno dei metodi standard per la moderazione.
Consultate [Moderazione del contenuto](/help/communities/moderate-ugc.md)generato dall&#39;utente.

A partire da AEM 6.1 Communities, l’utilizzo di uno store [](/help/communities/working-with-srp.md) comune per UGC include l’accesso programmatico a UGC, indipendentemente dall’opzione di archiviazione scelta (ad esempio ASRP, MSRP o JSRP).

**La posizione e il formato dell’UGC nel repository sono soggetti a modifiche senza preavviso**.

Consulta :

* [Panoramica](/help/communities/srp.md) del provider delle risorse di storage - introduzione e panoramica sull&#39;utilizzo dell&#39;archivio.
* [SRP e UGC Essentials](/help/communities/srp-and-ugc.md) - Metodi e esempi di utilità SRP.
* [Accesso a UGC con SRP](/help/communities/accessing-ugc-with-srp.md) - linee guida di codifica.
* [Refactoring](/help/communities/socialutils.md) SocialUtils - mappatura di metodi di utilità obsoleti ai metodi di utilità SRP correnti.

## Editore principale {#primary-publisher}

Quando la distribuzione è una farm di pubblicazione, è necessario identificare un editore principale che eseguirà il sondaggio per gli articoli pianificati per la pubblicazione.

Per ulteriori informazioni, vedere Editore [](/help/communities/deploy-communities.md#primary-publisher) principale.

## Consentire contenuti multimediali avanzati {#allowing-rich-media}

La piattaforma AEM blocca i collegamenti da altri siti Web per prevenire attacchi XSS come descritto in

* [Protezione contro gli script tra siti (XSS)](/help/sites-developing/security.md#protect-against-cross-site-scripting-xss)

A partire da AEM 6.2, le modifiche precedentemente richieste per essere effettuate manualmente sono incluse nel file di configurazione AntiSamy predefinito.

Per incorporare contenuti multimediali in un articolo di blog, selezionate l&#39; `Embed Media from External Sites` icona :

![chlimage_1-471](assets/chlimage_1-471.png)

