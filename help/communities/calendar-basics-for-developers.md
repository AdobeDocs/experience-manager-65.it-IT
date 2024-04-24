---
title: Elementi di base di Calendar
description: Scopri come utilizzare la funzione Calendario in Experience Manager Communities. Il Calendario supporta l'identificazione dei gruppi di utenti membri con privilegi.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 069e379d-c6fd-49ca-b337-df6fd466e023
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '204'
ht-degree: 2%

---

# Elementi di base di Calendar {#calendar-essentials}

Questa pagina fornisce informazioni essenziali sull&#39;utilizzo della funzione calendario.

## Nozioni di base per lato client {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/calendario/componenti/hbs/calendario</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>incluso</strong></a></td>
   <td>No</td>
  </tr>
  <tr>
   <td> <a href="client-customize.md#clientlibs-for-scf"><strong>clientllibs</strong></a></td>
   <td>cq.social.hbs.calendar</td>
  </tr>
  <tr>
   <td> <strong>modelli</strong></td>
   <td>/libs/social/calendar/components/hbs/calendar/calendar.hbs</td>
   <td> </td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td>/libs/social/calendar/components/hbs/calendar/clientlibs/css/calendar.css<br /> /libs/social/calendar/components/hbs/calendar/clientlibs/css/jqueryui.css</td>
  </tr>
  <tr>
   <td><strong> proprietà</strong></td>
   <td>vedi <a href="calendar.md">Utilizzo dei calendari</a></td>
  </tr>
 </tbody>
</table>

* [Personalizzazioni lato client](client-customize.md)

## Nozioni di base per lato server {#essentials-for-server-side}

* [API calendario](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/calendar/client/api/package-summary.html)

* [Endpoint calendario](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/calendar/client/endpoints/package-summary.html)

* [Personalizzazioni lato server](server-customize.md)

### Funzione Calendario {#calendar-function}

Una struttura del sito della community che include [Funzione calendario](functions.md#calendar-function) ha un `calendar` componente configurato. La funzione Calendar supporta l’identificazione di un’ [gruppo utenti membro privilegiato](users.md#privileged-members-group).

### Accesso ai post del calendario (UGC) {#accessing-calendar-posts-ugc}

A partire dalla AEM 6.1 Communities, l&#39;utilizzo di un [archivio comune](working-with-srp.md) per UGC include l’accesso programmatico a UGC indipendentemente dall’opzione di archiviazione scelta (ad esempio ASRP, MSRP o JSRP).

**La posizione e il formato dell’UGC nell’archivio sono soggetti a modifiche senza preavviso**.

Consulta:

* [Panoramica del provider di risorse di archiviazione](srp.md) - introduzione e panoramica sull’utilizzo dell’archivio
* [Nozioni di base su SRP e UGC](srp-and-ugc.md) - Metodi ed esempi di utilità SRP
* [Accesso a UGC con SRP](accessing-ugc-with-srp.md) - linee guida per la codifica
* [Refactoring SocialUtils](socialutils.md) - mappatura dei metodi di utilità obsoleti sui metodi di utilità SRP correnti
