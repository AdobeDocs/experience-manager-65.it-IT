---
title: Nozioni di base su componenti, funzioni e funzioni
description: Funzionamento di siti, modelli e gruppi della community
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: a43c1c4d-a6c2-4ef9-9047-a945978e618b
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 15%

---

# Nozioni di base su componenti, funzioni e funzioni  {#component-function-and-feature-essentials}

Le funzionalità di Adobe Experience Manager (AEM) Communities richiedono che i visitatori del sito diventino membri e accedano al [sito community](overview.md#communitiessites) prima di poter pubblicare il contenuto. Pertanto, i [modelli di sito community](sites.md), da cui un sito community è [creato](sites-console.md), sono progettati per includere una funzionalità di accesso e profili utente, messaggistica, ricerca, moderazione e traduzione.

Un sito community supporta i membri che creano gruppi community quando la funzione [gruppi community](functions.md#groups-function) è inclusa nel modello di sito community selezionato.

Di seguito sono riportati collegamenti a informazioni essenziali per componenti, funzioni e funzioni di Communities.

## Componenti base {#base-components}

* [Commenti](essentials-comments.md)
* [Recensioni](reviews-basics.md)
* [Tally](tally.md)

   * [Con Mi piace](essentials-liking.md)
   * [Valutazione](rating-basics.md)
   * [Votazione](essentials-voting.md)
   * *Sondaggio (non più disponibile)*

## Componenti con funzioni {#components-with-functions}

* [Flussi attività](essentials-activities.md)
* [Blog](blog-developer-basics.md) ( `Journal`)

* [Calendario](calendar-basics-for-developers.md)
* [Contenuto in primo piano](essentials-featured.md)
* [Libreria file](essentials-file-library.md)
* [Forum](essentials-forum.md)
* [Gruppi](essentials-groups.md)
* [Ideazione](ideation.md)
* [Classifica](leaderboard.md)
* [Domande e risposte](qna-essentials.md) `(QnA)`

## Funzioni {#features}

* [Librerie client](clientlibs.md)
* [Siti community](sites-for-developers.md)
* [Eventi OSGi componenti](events.md)
* [Caricamento laterale componente](sideloading.md)
* [Messaggi](essentials-messaging.md)
* [Editor Rich Text](rte.md)
* [Punteggio e distintivi](configure-scoring.md)
* [Ricerca](search-implementation.md)
* [Grafico social](essentials-socialgraph.md)
* [Provider risorsa di archiviazione](srp-and-ugc.md) `(SRP)`

* [Assegnazione dei tag](tag.md)

## JavaScript {#javadocs}

I [documenti Java online](../../help/sites-developing/reference-materials.md) riflettono le API disponibili nella versione 6.3 di AEM.
Le API delle community si trovano in `com.adobe.cq.social.*` pacchetti.

Per ogni [feature pack](deploy-communities.md#latestfeaturepack), è disponibile un file javadoc jar. Per ulteriori informazioni, visita [Utilizzo di Maven per le community](maven.md#javadocs).

## Informazioni aggiuntive {#additional-information}

* [Framework componenti social network (SCF)](scf.md)

   * [Personalizzazioni lato client](client-customize.md)
   * [Personalizzazioni lato server](server-customize.md)
   * [Panoramica del provider di risorse di archiviazione](srp.md)

* [Linee guida per la codifica](code-guide.md)
* [Tutorial](tutorials.md)
* [Risoluzione dei problemi](troubleshooting.md)
