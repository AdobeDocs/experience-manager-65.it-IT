---
title: Best practice per gli sviluppatori AEM
description: I team di progettazione e consulenza Adobe hanno sviluppato un set completo di best practice per gli sviluppatori AEM.
contentOwner: Justin Edelson
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: 0a478e80-c1b2-46c1-a6be-794d78b85d69
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 3%

---

# Best practice{#best-practices}

## Procedure consigliate per gli sviluppatori - Guida introduttiva {#best-practices-for-developers-getting-started}

I team di progettazione e consulenza Adobe hanno sviluppato un set completo di best practice per gli sviluppatori AEM. Gli sviluppatori Adobe aderiscono a queste best practice durante lo sviluppo di aggiornamenti di base dei prodotti AEM e del codice cliente per le implementazioni dei clienti.

Prima di iniziare il progetto di sviluppo dell’AEM, esamina le seguenti best practice:

* [Procedure di sviluppo](/help/sites-developing/development-practices.md)
* [Architettura dei contenuti](/help/sites-developing/content-architecture.md)
* [Architettura software](/help/sites-developing/software-architecture.md)
* [Suggerimenti per la codifica](/help/sites-developing/coding-tips.md)
* [Insidie del codice](/help/sites-developing/code-pitfalls.md)
* [Interazione JCR](/help/sites-developing/jcr-integration.md)
* [Bundle OSGi](/help/sites-developing/osgi-bundles.md)
* [Best practice per l’API Java](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/understand-java-api-best-practices.html)

### Informazioni aggiuntive sulle best practice {#additional-best-practices-information}

Nelle seguenti aree è disponibile una documentazione specifica per lo sviluppo di best practice:

* [Sites](#sites)
* [Communities](/help/sites-developing/best-practices.md#communities)
* [Strumenti/HTL](/help/sites-developing/best-practices.md#tooling-htl)

I documenti specifici sono descritti e collegati nelle tabelle seguenti.

Per le best practice sull’amministrazione, la distribuzione e la manutenzione o l’authoring, consulta una delle seguenti sezioni:

* [Amministrazione delle best practice](/help/sites-administering/administer-best-practices.md)
* [Best practice di authoring](/help/sites-authoring/best-practices.md)
* [Implementazione delle best practice](/help/sites-deploying/best-practices.md)

## Sites {#sites}

Per la gestione e l’authoring dei contenuti del sito web, vengono descritte alcune best practice:

<table>
 <tbody>
  <tr>
   <td>Alcune delle teorie alla base dell’interfaccia utente standard touch.</td>
   <td><p><a href="/help/sites-developing/touch-ui-concepts.md">Interfaccia touch: concetti</a></p> <p><a href="/help/sites-developing/touch-ui-structure.md">Interfaccia touch: struttura</a></p> </td>
   <td>Questi documenti forniscono una panoramica dei concetti e della struttura dell’interfaccia touch.</td>
  </tr>
  <tr>
   <td>Interfaccia touch: personalizzazione delle console </td>
   <td><a href="/help/sites-developing/customizing-consoles-touch.md">Personalizzazione delle console dell’interfaccia touch</a></td>
   <td>Questo documento descrive il modo migliore per estendere le console per l’interfaccia utente touch.</td>
  </tr>
  <tr>
   <td>Interfaccia touch: personalizzazione dell’authoring delle pagine</td>
   <td><a href="/help/sites-developing/customizing-page-authoring-touch.md">Personalizzazione dell’authoring delle pagine dell’interfaccia utente touch</a></td>
   <td>Descrive come estendere l’authoring delle pagine per l’interfaccia utente touch.</td>
  </tr>
  <tr>
   <td>Flussi di lavoro</td>
   <td><a href="/help/sites-developing/workflows-best-practices.md">Sviluppo ed estensione dei flussi di lavoro</a></td>
   <td><p>I flussi di lavoro consentono di automatizzare le attività di Adobe Experience Manager (AEM) e possono rappresentare una grande quantità di elaborazione che si verifica in un ambiente AEM, pertanto si consiglia vivamente di pianificare con attenzione le implementazioni dei flussi di lavoro.</p> </td>
  </tr>
 </tbody>
</table>

## Communities {#communities}

[AEM Communities](/help/communities/overview.md) semplifica la creazione e la gestione di community on-premise.

Di seguito sono descritte alcune best practice per le community:

|  |  |  |
|---|---|---|
| Best practice per l’utilizzo di contenuti generati dagli utenti (UGC, User Generated Content) | [Linee guida per la codifica](/help/communities/code-guide.md) | Linee guida per lo sviluppo di codice flessibile e portatile per [framework della componente social](/help/communities/scf.md) (SCF). |
| Esempio di utilizzo dei componenti community | [Guida ai componenti della community](/help/communities/components-guide.md) | Uno strumento di sviluppo interattivo. |

## Strumenti/HTL {#tooling-htl}

HTL (HTML Template Language) è un nuovo sistema di modelli di HTML introdotto con AEM 6.0. Sostituisce JSP ed ESP come sistema di modelli preferito dell’AEM.

|  |  |  |
|---|---|---|
| Panoramica di HTL | [Panoramica e sintassi di HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html?lang=it) | Questo documento descrive cosa è HTL, come passare ad HTL, un progetto di esempio, la sintassi, le espressioni e le istruzioni |
| Utilizzo dell’API in Java | [API di utilizzo Java HTL](https://helpx.adobe.com/experience-manager/htl/using/use-api.html) | Java Use-API per HTL consente a un file HTL di accedere a metodi helper in una classe Java personalizzata. |

>[!NOTE]
>
>Il seguente tutorial in più parti potrebbe essere utile per la best practice per impostare un nuovo progetto AEM, con informazioni dettagliate sui Componenti core, i modelli modificabili, le librerie client e lo sviluppo di componenti:
>[Guida introduttiva ad AEM Sites: esercitazione WKND](https://helpx.adobe.com/experience-manager/kt/sites/using/getting-started-wknd-tutorial-develop.html)
