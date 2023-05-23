---
title: Nozioni di base su componenti, funzioni e funzioni
seo-title: Component, Function and Feature Essentials
description: Funzionamento di siti, modelli e gruppi della community
seo-description: How community sites, templates, and groups function
uuid: 6edfca2d-fe5b-4261-b033-51dc2f9dbfd7
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 2d308756-79d1-4d69-b51c-d4b6e692a137
exl-id: a43c1c4d-a6c2-4ef9-9047-a945978e618b
source-git-commit: 942db8fe3dad16be53dc6abe0e519d97a659e480
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 17%

---

# Nozioni di base su componenti, funzioni e funzioni  {#component-function-and-feature-essentials}

Le funzioni di AEM Communities richiedono che i visitatori del sito diventino membri e accedano al [sito community](overview.md#communitiessites) prima di poter pubblicare il contenuto. Pertanto, [modelli per sito community](sites.md), da cui è stato creato un sito community [creato](sites-console.md), sono progettati per includere una funzione di accesso, nonché profili utente, messaggi, ricerca, moderazione e traduzione.

Un sito community supporta i membri che creano gruppi community quando [funzione gruppi community](functions.md#groups-function) è incluso nel modello di sito community selezionato.

Di seguito sono riportati collegamenti a informazioni essenziali su componenti, funzioni e funzioni di Communities.

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

Il [javadoc online](../../help/sites-developing/reference-materials.md) riflette le API disponibili nella versione AEM 6.3.
Le API delle community sono in `com.adobe.cq.social.*` pacchetti.

Per ogni [feature pack](deploy-communities.md#latestfeaturepack), è disponibile un file javadoc jar. Per ulteriori informazioni, visita [Utilizzo di Maven per le community](maven.md#javadocs).

## Informazioni aggiuntive {#additional-information}

* [Framework componenti social network (SCF)](scf.md)

   * [Personalizzazioni lato client](client-customize.md)
   * [Personalizzazioni lato server](server-customize.md)
   * [Panoramica del provider di risorse di archiviazione](srp.md)

* [Linee guida per la codifica](code-guide.md)
* [Esercitazioni](tutorials.md)
* [Risoluzione dei problemi](troubleshooting.md)
