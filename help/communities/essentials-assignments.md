---
title: Componenti di base per le assegnazioni
seo-title: Componenti di base per le assegnazioni
description: Panoramica della funzione Assegnazioni per le community di abilitazione
seo-description: Panoramica della funzione Assegnazioni per le community di abilitazione
uuid: e49fce26-1091-4f37-93e8-c4ec85371811
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 6bac681e-59e1-4786-9c50-6679c936cfd1
docset: aem65
exl-id: 75cef5da-4f93-4721-99c0-ad44c8ab76d4
source-git-commit: 1d334c42088342954feb34f6179dc5b134f81bb8
workflow-type: tm+mt
source-wordcount: '222'
ht-degree: 13%

---

# Componenti di base per le assegnazioni {#assignments-essentials}

Continua a leggere per conoscere le informazioni essenziali per l&#39;utilizzo della funzione di assegnazione dei siti [enablement community](/help/communities/overview.md#enablement-community).

La funzione assegnazioni consente di assegnare risorse di abilitazione e percorsi di apprendimento ai membri delle comunità di abilitazione.

## Funzionalità di base per lato client {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/enablement/components/hbs/myassigned</td>
  </tr>
  <tr>
   <td> <a href="/help/communities/scf.md#add-or-include-a-communities-component"><strong>comprensivo</strong></a></td>
   <td>No</td>
  </tr>
  <tr>
   <td> <a href="/help/communities/clientlibs.md"><strong>clientlibs</strong></a></td>
   <td>cq.social.enablement.hbs.breadcrumbs<br /> cq.social.enablement.hbs.myassigned<br /> cq.social.enablement.hbs.resource<br /> cq.social.enablement.hbs.learningpath</td>
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
   <td>Consultare <a href="/help/communities/assignments.md">Assegnazioni Feature</a></td>
  </tr>
 </tbody>
</table>

### Stato di completamento e successo {#completion-and-success-status}

Lo stato Completato e Completato viene utilizzato nei rapporti e nei banner di stato Assegnazioni.

Stato completamento:

* Non assegnato
* Non avviato (nuovo)
* In corso
* Completa

Stato di operazione riuscita:

* Sconosciuto
* Esito positivo
* Operazione non riuscita

Le uniche combinazioni possibili di stato di completamento e successo sono:

| **Completamento** | **Completato** |
|---|---|
| Non iniziato | Sconosciuto |
| In corso | Sconosciuto |
| Completa | Esito positivo |
| Completa | Operazione non riuscita |

## Funzioni di base per lato server {#essentials-for-server-side}

### Funzione Assegnazioni {#assignments-function}

Una struttura del sito community che include la [funzione Assegnazioni](/help/communities/functions.md#assignments-function), include un componente ` [assignments](/help/communities/assignments.md)` configurato.

### API di riferimento {#reference-apis}

* [API di abilitazione](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/enablement/reporting/model/api/package-summary.html)

* [API di reporting](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/reporting/dv/api/package-summary.html)

* [API di Reporting Analytics](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/reporting/dv/model/api/package-summary.html)
