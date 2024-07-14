---
title: Nozioni di base sul blog
description: Scopri come aggiungere la funzione Blog a una pagina in modo che i membri della community con accesso possano pubblicare articoli di blog.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
docset: aem65
exl-id: 51f616e8-4aba-47f6-b948-d5147d84bbb6
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '428'
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

La funzionalità blog è composta da due componenti principali disponibili aggiungendo la [funzione Blog](/help/communities/functions.md#blog-function) o aggiungendo i componenti a una pagina in modalità di modifica dell&#39;autore.

### Blog {#blog}

<table>
 <tbody>
  <tr>
   <td> <strong>tiporisorsa</strong></td>
   <td>social/journal/components/hbs/journal</td>
  </tr>
  <tr>
   <td> <a href="/help/communities/scf.md#add-or-include-a-communities-component"><strong>includibile</strong></a></td>
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

| **tiporisorsa** | social/journal/components/hbs/sidebar |
|---|---|
| [**includibile**](/help/communities/scf.md#add-or-include-a-communities-component) | No |
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

In una struttura del sito della community che include la funzione [Blog](/help/communities/functions.md#blog-function) sono configurati `Blog` e `Blog Sidebar` componenti. La funzione Blog supporta l&#39;identificazione di un [gruppo di utenti membro con privilegi](/help/communities/users.md#privileged-members-group).

### Accesso alle voci blog (UGC) {#accessing-blog-entries-ugc}

Il contenuto UGC deve essere moderato utilizzando uno dei metodi standard per la moderazione.
Vedere [Moderazione del contenuto generato dall&#39;utente](/help/communities/moderate-ugc.md).

A partire da AEM 6.1 Communities, l&#39;utilizzo di un [archivio comune](/help/communities/working-with-srp.md) per UGC include l&#39;accesso programmatico a UGC indipendentemente dall&#39;opzione di archiviazione scelta (ad esempio ASRP, MSRP o JSRP).

**La posizione e il formato dell&#39;UGC nell&#39;archivio sono soggetti a modifiche senza preavviso**.

Consulta:

* [Panoramica del provider di risorse di archiviazione](/help/communities/srp.md) - introduzione e panoramica sull&#39;utilizzo dell&#39;archivio.
* [SRP e UGC Essentials](/help/communities/srp-and-ugc.md) - Metodi ed esempi dell&#39;utilità SRP.
* [Accesso a UGC con SRP](/help/communities/accessing-ugc-with-srp.md) - linee guida per la codifica.
* [Refactoring di SocialUtils](/help/communities/socialutils.md) - mapping dei metodi di utilità obsoleti ai metodi di utilità SRP correnti.

## Editore primario {#primary-publisher}

Quando la distribuzione è una farm di pubblicazione, è necessario identificare un editore principale che esegue il polling degli articoli pianificati per la pubblicazione.

Per ulteriori dettagli, vedere [Autore primario](/help/communities/deploy-communities.md#primary-publisher).

## Consentire contenuti multimediali avanzati {#allowing-rich-media}

La piattaforma AEM blocca i collegamenti da altri siti web per prevenire gli attacchi XSS come descritto in

* [Protect contro il cross-site scripting (XSS)](/help/sites-developing/security.md#protect-against-cross-site-scripting-xss)

A partire da AEM 6.2, le modifiche precedentemente necessarie da apportare manualmente sono incluse nel file di configurazione predefinito AntiSamy.

Rich Media è incorporato in un articolo di blog selezionando l&#39;icona `Embed Media from External Sites`:

![media](assets/media-icon.png)
