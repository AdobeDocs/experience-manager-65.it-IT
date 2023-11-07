---
title: Risoluzione dei problemi durante la creazione in AEM
description: Alcuni problemi che possono verificarsi quando si utilizza AEM.
uuid: 99af51ea-8628-4811-83f2-ab3f88f0279e
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: da0a5644-2e1d-4394-a6aa-11bb41406ba6
exl-id: 05586b17-35d4-496e-8f0e-293c755eb066
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 47%

---

# Risoluzione di problemi AEM nell’ambiente di authoring{#troubleshooting-aem-when-authoring}

Nella seguente sezione vengono descritti alcuni problemi che potresti riscontrare durante l’utilizzo di AEM e vengono proposte possibili soluzioni.

>[!NOTE]
>
>Quando si verificano problemi, vale anche la pena controllare l&#39;elenco di [Problemi noti](/help/release-notes/release-notes.md) per la tua istanza (release e service pack).

>[!NOTE]
>
>Gli utenti con privilegi di amministratore e che desiderano risolvere i problemi relativi all&#39;AEM possono utilizzare i metodi di risoluzione dei problemi descritti in [Risoluzione dei problemi AEM (per amministratori)](/help/sites-administering/troubleshoot.md). Se non disponi di privilegi sufficienti, consulta l’amministratore di sistema per la risoluzione dei problemi AEM.

## La vecchia versione della pagina è ancora nel sito pubblicato {#old-page-version-still-on-published-site}

* **Problema**:

   * Hai apportato modifiche a una pagina e l’hai replicata nel sito pubblicato, ma il *vecchio* La versione della pagina viene ancora visualizzata sul sito pubblicato.

* **Motivo**:

   * Questo può avere diverse cause, nella maggior parte dei casi la cache (nel browser locale o in Dispatcher), anche se a volte può essere un problema con la coda di replica.

* **Soluzioni**:

   * Esistono varie possibilità:
   * Verifica che la pagina sia stata replicata correttamente. Controlla lo stato della pagina e, se necessario, lo stato della coda di replica.
   * Cancella la cache del browser locale e accedi di nuovo alla pagina.
   * Aggiungi `?` alla fine dell’URL della pagina, ad esempio:

      * `http://localhost:4502/sites.html/content?`
      * In questo modo la pagina viene richiesta direttamente da AEM senza passare dal Dispatcher. Se viene visualizzata la pagina aggiornata, significa che è necessario cancellare la cache del Dispatcher.

   * In caso di problemi relativi alla coda di replica, rivolgiti all’amministratore di sistema.

## Azioni per componenti non visibili sulla barra degli strumenti {#component-actions-not-visible-on-toolbar}

* **Problema**:

   * Non tutte le azioni disponibili per i componenti sono visibili quando si modifica il contenuto di una pagina nell’ambiente di authoring.

* **Motivo**:

   * In rari casi, un’azione precedente potrebbe influire sulla barra degli strumenti.

* **Soluzione**:

   * Aggiorna la pagina.
