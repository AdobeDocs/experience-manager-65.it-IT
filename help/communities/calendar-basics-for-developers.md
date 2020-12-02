---
title: Funzioni di base del calendario
seo-title: Funzioni di base del calendario
description: Panoramica delle funzioni calendario
seo-description: Panoramica delle funzioni calendario
uuid: 14ff7a83-b2a7-4f7e-8ee7-88f336329a1a
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 88932a3c-ba7f-47ba-9e0b-206755c2d42e
translation-type: tm+mt
source-git-commit: 82affd528f2526384b319fe89082e0f574ab5855
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 2%

---


# Calendario Essentials {#calendar-essentials}

Questa pagina fornisce informazioni essenziali sull’utilizzo della funzione calendario.

## Essentials for Client-Side {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/calendario/componenti/hbs/calendario</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>inclusa</strong></a></td>
   <td>No</td>
  </tr>
  <tr>
   <td> <a href="client-customize.md#clientlibs-for-scf"><strong>clientllibs</strong></a></td>
   <td>cq.social.hbs.calendar</td>
  </tr>
  <tr>
   <td> <strong>templates</strong></td>
   <td>/libs/social/calendar/components/hbs/calendar/calendar.hbs</td>
   <td> </td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td>/libs/social/calendar/components/hbs/calendar/clientlibs/css/calendar.css<br /> /libs/social/calendar/components/hbs/calendar/clientlibs/css/jqueryui.css</td>
  </tr>
  <tr>
   <td><strong> proprietà</strong></td>
   <td>vedere <a href="calendar.md">Utilizzo dei calendari</a></td>
  </tr>
 </tbody>
</table>

* [Personalizzazioni lato client](client-customize.md)

## Essentials for Server-Side {#essentials-for-server-side}

* [API calendario](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/calendar/client/api/package-summary.html)

* [Endpoint calendario](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/calendar/client/endpoints/package-summary.html)

* [Personalizzazioni lato server](server-customize.md)

### Funzione Calendario {#calendar-function}

Una struttura del sito community che include la funzione [Calendario](functions.md#calendar-function) avrà un componente `calendar` configurato. La funzione Calendario supporta l&#39;identificazione di un [gruppo di utenti con privilegi](users.md#privileged-members-group).

### Accesso ai post del calendario (UGC) {#accessing-calendar-posts-ugc}

A partire da AEM 6.1 Communities, l&#39;utilizzo di un [store comune](working-with-srp.md) per UGC include l&#39;accesso programmatico a UGC indipendentemente dall&#39;opzione di storage scelta (come ASRP, MSRP o JSRP).

**La posizione e il formato dell’UGC nel repository sono soggetti a modifiche senza preavviso**.

Consulta:

* [Panoramica](srp.md)  del provider di risorse di storage - introduzione e utilizzo del repository
* [Funzioni essenziali](srp-and-ugc.md)  SRP e UGC - Metodi di utilità SRP ed esempi
* [Accesso a UGC con SRP](accessing-ugc-with-srp.md)  - linee guida di codifica
* [Refactoring](socialutils.md)  SocialUtils: mappatura di metodi di utilità obsoleti ai metodi di utilità SRP correnti

