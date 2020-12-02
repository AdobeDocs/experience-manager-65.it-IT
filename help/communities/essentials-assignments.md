---
title: Assignments Essentials
seo-title: Assignments Essentials
description: Panoramica della funzione Assegnazioni per le community di abilitazione
seo-description: Panoramica della funzione Assegnazioni per le community di abilitazione
uuid: e49fce26-1091-4f37-93e8-c4ec85371811
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 6bac681e-59e1-4786-9c50-6679c936cfd1
docset: aem65
translation-type: tm+mt
source-git-commit: c897f034edbdbeee74869165ed384c3408a857e0
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 13%

---


# Assignments Essentials {#assignments-essentials}

Continua a leggere per conoscere le informazioni essenziali per l&#39;utilizzo della funzione di assegnazione dei siti [community di abilitazione](/help/communities/overview.md#enablement-community).

La funzione di assegnazione consente di assegnare risorse di abilitazione e percorsi di apprendimento ai membri delle comunità di abilitazione.

## Essentials for Client-Side {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/enablement/components/hbs/myassign</td>
  </tr>
  <tr>
   <td> <a href="/help/communities/scf.md#add-or-include-a-communities-component"><strong>inclusa</strong></a></td>
   <td>No</td>
  </tr>
  <tr>
   <td> <a href="/help/communities/clientlibs.md"><strong>clientllibs</strong></a></td>
   <td>cq.social.enablement.hbs.breadcrumbs<br /> cq.social.enablement.hbs.myassign<br /> cq.social.enablement.hbs.resource<br /> cq.social.enablement.hbs.learningpath</td>
  </tr>
  <tr>
   <td> <strong>templates</strong></td>
   <td> /libs/social/enablement/components/hbs/myassigned/myassigned.hbs</td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/enablement/components/hbs/myassigned/clientlibs/myassigned.css</td>
  </tr>
  <tr>
   <td><strong> proprietà</strong></td>
   <td>Vedere <a href="/help/communities/assignments.md">Caratteristica di assegnazione</a></td>
  </tr>
 </tbody>
</table>

### Stato completamento e successo {#completion-and-success-status}

Lo stato di completamento e completamento viene utilizzato nei rapporti e nei banner di stato sulle assegnazioni.

Stato completamento:

* Non assegnato
* Non avviato (nuovo)
* In corso
* Completa

Stato di operazione riuscita:

* Sconosciuto
* Esito positivo
* Operazione non riuscita

Le uniche possibili combinazioni di Stato completamento e Successo sono:

| **Completamento** | **Completato** |
|---|---|
| Non iniziato | Sconosciuto |
| In corso | Sconosciuto |
| Completa | Esito positivo |
| Completa | Operazione non riuscita |

## Essentials for Server-Side {#essentials-for-server-side}

### Funzione Assegnazioni {#assignments-function}

Una struttura del sito community che include la funzione [Assegnazioni](/help/communities/functions.md#assignments-function), include un componente ` [assignments](/help/communities/assignments.md)` configurato.

### API di riferimento {#reference-apis}

* [API di abilitazione](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/enablement/reporting/model/api/package-summary.html)

* [API di reporting](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/reporting/dv/api/package-summary.html)

* [API di Reporting Analytics](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/reporting/analytics/api/package-summary.html)

