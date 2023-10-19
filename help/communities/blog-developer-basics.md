---
title: Nozioni di base sul blog
description: Scopri come aggiungere la funzione Blog a una pagina in modo che i membri della community con accesso possano pubblicare articoli di blog.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
docset: aem65
exl-id: 51f616e8-4aba-47f6-b948-d5147d84bbb6
source-git-commit: 62d4a8b3af5031ccc539d78f7d06a8cd1fec7af1
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 2%

---

# Nozioni di base sul blog {#blog-essentials}

Dalle comunità AEM 6.1, un blog è un&#39;attività della comunità. Gli articoli di blog vengono ora pubblicati nell’ambiente di pubblicazione, dove in precedenza era possibile crearli e pubblicarli solo nell’ambiente di authoring.

Gli articoli di blog possono ora essere creati da qualsiasi membro della community, a meno che non siano limitati ai membri privilegiati.

Questa pagina fornisce le informazioni essenziali per l&#39;utilizzo della funzione blog.

>[!NOTE]
>
>L&#39;infrastruttura sottostante della funzione blog è la funzione diario.

## Nozioni di base per lato client {#essentials-for-client-side}

La feature di blog è composta da due componenti principali disponibili aggiungendo il [Funzione blog](/help/communities/functions.md#blog-function) oppure aggiungendo i componenti a una pagina in modalità di modifica dell’autore.

### Blog {#blog}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/journal/components/hbs/journal</td>
  </tr>
  <tr>
   <td> <a href="/help/communities/scf.md#add-or-include-a-communities-component"><strong>incluso</strong></a></td>
   <td>No</td>
  </tr>
  <tr>
   <td> <a href="/help/communities/clientlibs.md"><strong>clientllibs</strong></a></td>
   <td>cq.ckeditor<br /> cq.social.hbs.voting<br /> cq.social.hbs.journal</td>
  </tr>
  <tr>
   <td> <strong>modelli</strong></td>
   <td> /libs/social/journal/components/hbs/journal/journal.hbs<br /> /libs/social/journal/components/hbs/entry_topic/list-item.hbs</td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/journal/components/hbs/journal/clientlibs/journal.css</td>
  </tr>
  <tr>
   <td><strong> proprietà</strong></td>
   <td>vedi <a href="/help/communities/blog-feature.md">Funzione blog</a></td>
  </tr>
 </tbody>
</table>

### Barra laterale blog {#blog-sidebar}

| **resourceType** | social/journal/components/hbs/sidebar |
|---|---|
| [**incluso**](/help/communities/scf.md#add-or-include-a-communities-component) | No |
| [**clientllibs**](/help/communities/clientlibs.md) | cq.social.hbs.journal_sidebar |
| **modelli** | /libs/social/journal/components/hbs/sidebar/sidebar.hbs |
| **css** | /libs/social/journal/components/hbs/sidebar/clientlibs/sidebar.css |
| **proprietà** | vedi [Funzione blog](/help/communities/blog-feature.md) |

* [Personalizzazioni lato client](/help/communities/client-customize.md)

## Nozioni di base per lato server {#essentials-for-server-side}

* [API blog](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/journal/client/api/package-summary.html)

* [Endpoint blog](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/journal/client/endpoints/package-summary.html)

* [Personalizzazioni lato server](/help/communities/server-customize.md)

### Funzione Blog {#blog-function}

Una struttura del sito della community che include [Funzione blog](/help/communities/functions.md#blog-function) ha `Blog` e `Blog Sidebar` componenti configurati. La funzione Blog supporta l’identificazione di un’ [gruppo utenti membro privilegiato](/help/communities/users.md#privileged-members-group).

### Accesso alle voci blog (UGC) {#accessing-blog-entries-ugc}

Il contenuto UGC deve essere moderato utilizzando uno dei metodi standard per la moderazione.
Consulta [Moderazione dei contenuti generati dagli utenti](/help/communities/moderate-ugc.md).

A partire dalla AEM 6.1 Communities, l&#39;utilizzo di un [archivio comune](/help/communities/working-with-srp.md) per UGC include l’accesso programmatico a UGC indipendentemente dall’opzione di archiviazione scelta (ad esempio ASRP, MSRP o JSRP).

**La posizione e il formato dell’UGC nell’archivio sono soggetti a modifiche senza preavviso**.

Consulta :

* [Panoramica del provider di risorse di archiviazione](/help/communities/srp.md) - introduzione e panoramica sull’utilizzo dell’archivio.
* [Nozioni di base su SRP e UGC](/help/communities/srp-and-ugc.md) - Metodi ed esempi di utilità SRP.
* [Accesso a UGC con SRP](/help/communities/accessing-ugc-with-srp.md) - linee guida per la codifica.
* [Refactoring SocialUtils](/help/communities/socialutils.md) - mappatura dei metodi di utilità obsoleti sui metodi di utilità SRP correnti.

## Editore primario {#primary-publisher}

Quando la distribuzione è una farm di pubblicazione, è necessario identificare un editore principale che esegue il polling degli articoli pianificati per la pubblicazione.

Consulta [Editore primario](/help/communities/deploy-communities.md#primary-publisher) per ulteriori dettagli.

## Consentire contenuti multimediali avanzati {#allowing-rich-media}

La piattaforma AEM blocca i collegamenti da altri siti web per prevenire gli attacchi XSS come descritto in

* [Protect contro il cross-site scripting (XSS)](/help/sites-developing/security.md#protect-against-cross-site-scripting-xss)

A partire da AEM 6.2, le modifiche precedentemente necessarie da apportare manualmente sono incluse nel file di configurazione predefinito AntiSamy.

I contenuti multimediali avanzati sono incorporati in un articolo di blog selezionando la `Embed Media from External Sites` icona :

![media](assets/media-icon.png)
