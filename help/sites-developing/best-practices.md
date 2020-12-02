---
title: 'Best practice  '
seo-title: 'Best practice  '
description: ' team di progettazione e consulenza di Adobe hanno sviluppato una serie completa di best practice per AEM sviluppatori'
seo-description: ' team di progettazione e consulenza di Adobe hanno sviluppato una serie completa di best practice per AEM sviluppatori'
uuid: f962c31f-8140-482f-b189-16376e23bfed
contentOwner: Justin Edelson
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 99678c1a-81f3-4fb3-bf73-98f0691c3fb6
translation-type: tm+mt
source-git-commit: e562939f1c64d8345b4c2a28e4b882200d9e4c07
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 12%

---


# Best practice  {#best-practices}

## Best practice per gli sviluppatori - Guida introduttiva {#best-practices-for-developers-getting-started}

 team di progettazione e consulenza di Adobe hanno sviluppato una serie completa di best practice per AEM sviluppatori.  conformità degli sviluppatori di Adobi a queste best practice per sviluppare aggiornamenti AEM prodotti di base e codice cliente per le implementazioni dei clienti.

Prima di avviare il progetto di sviluppo AEM, controlla innanzitutto le best practice seguenti:

* [Pratiche di sviluppo](/help/sites-developing/development-practices.md)
* [Architettura dei contenuti](/help/sites-developing/content-architecture.md)
* [Architettura del software](/help/sites-developing/software-architecture.md)
* [Suggerimenti sulla codifica](/help/sites-developing/coding-tips.md)
* [Code Pitfall](/help/sites-developing/code-pitfalls.md)
* [Interazione JCR](/help/sites-developing/jcr-integration.md)
* [Bundle OSGi](/help/sites-developing/osgi-bundles.md)
* [Best practice per le API Java](https://docs.adobe.com/content/help/en/experience-manager-learn/foundation/development/understand-java-api-best-practices.html)

### Informazioni aggiuntive sulle best practice {#additional-best-practices-information}

Le aree seguenti dispongono di documentazione specifica per lo sviluppo delle best practice:

* [Sites](#sites)
* [Community](/help/sites-developing/best-practices.md#communities)
* [Tooling/HTL](/help/sites-developing/best-practices.md#tooling-htl)

Nelle tabelle che seguono è riportata una descrizione di ciascun documento con il collegamento relativo.

Per le best practice relative all’amministrazione, alla distribuzione e alla manutenzione o all’authoring, consulta uno dei seguenti argomenti:

* [Best practice di amministrazione](/help/sites-administering/administer-best-practices.md)
* [Best practice di authoring](/help/sites-authoring/best-practices.md)
* [Best practice di distribuzione](/help/sites-deploying/best-practices.md)

## Sites {#sites}

Per la gestione e l’authoring dei contenuti dei siti web sono disponibili le best practice illustrate di seguito:

<table>
 <tbody>
  <tr>
   <td>Alcune delle teorie dietro l’interfaccia touch standard.</td>
   <td><p><a href="/help/sites-developing/touch-ui-concepts.md">Interfaccia touch: Concetti</a></p> <p><a href="/help/sites-developing/touch-ui-structure.md">Interfaccia touch: Struttura</a></p> </td>
   <td>Questi documenti forniscono una panoramica dei concetti e della struttura dell’interfaccia touch.</td>
  </tr>
  <tr>
   <td>Interfaccia touch: Personalizzazione delle console </td>
   <td><a href="/help/sites-developing/customizing-consoles-touch.md">Personalizzazione delle console dell’interfaccia touch</a></td>
   <td>Questo documento descrive il modo migliore per estendere le console per l’interfaccia touch.</td>
  </tr>
  <tr>
   <td>Interfaccia touch: Personalizzazione dell’authoring delle pagine</td>
   <td><a href="/help/sites-developing/customizing-page-authoring-touch.md">Personalizzazione dell’authoring delle pagine nell’interfaccia touch</a></td>
   <td>Descrive come estendere l’authoring delle pagine per l’interfaccia touch.</td>
  </tr>
  <tr>
   <td>Flussi di lavoro</td>
   <td><a href="/help/sites-developing/workflows-best-practices.md">Sviluppo ed estensione dei flussi di lavoro</a></td>
   <td><p>I flussi di lavoro consentono di automatizzare le attività di Adobe Experience Manager (AEM) e possono rappresentare una grande quantità di elaborazione che si verifica in un ambiente AEM, pertanto è vivamente consigliato pianificare con attenzione le implementazioni dei flussi di lavoro.</p> </td>
  </tr>
 </tbody>
</table>

## Communities {#communities}

[AEM ](/help/communities/overview.md) Comunità semplifica la creazione e la gestione delle comunità locali.

Alcune best practice per Community sono descritte di seguito:

|  |  |  |
|---|---|---|
| Procedure ottimali per l&#39;utilizzo dei contenuti generati dagli utenti (UGC) | [Linee guida sulla codifica](/help/communities/code-guide.md) | Linee guida per lo sviluppo di codice flessibile e portatile per il [social component framework](/help/communities/scf.md) (SCF). |
| Esempio di utilizzo dei componenti Community | [Guida ai componenti community](/help/communities/components-guide.md) | Uno strumento di sviluppo interattivo. |

## Tooling/HTL {#tooling-htl}

HTML Template Language (HTL) è un nuovo sistema di modelli HTML, introdotto con AEM 6.0. Sostituisce JSP e ESP come sistema di AEM preferito.

|  |  |  |
|---|---|---|
| Panoramica di HTL | [Panoramica e sintassi HTL](https://docs.adobe.com/content/help/it-IT/experience-manager-htl/using/overview.html) | Questo documento descrive il concetto di HTL, come passare a HTL, un progetto, una sintassi, espressioni e istruzioni di esempio |
| Utilizzo dell&#39;API in Java | [API di utilizzo Java HTL](https://helpx.adobe.com/experience-manager/htl/using/use-api.html) | L&#39;API Use-API Java HTL consente a un file HTL di accedere ai metodi helper in una classe Java personalizzata. |

>[!NOTE]
>
>Per la procedura ottimale per l’impostazione di un nuovo progetto AEM, con i dettagli Componenti principali, Modelli modificabili, Librerie client e sviluppo di componenti potrebbe essere utile seguire un’esercitazione con più parti:
>[Guida introduttiva ad AEM Sites: tutorial WKND](https://helpx.adobe.com/experience-manager/kt/sites/using/getting-started-wknd-tutorial-develop.html)

