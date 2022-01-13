---
title: Risoluzione di problemi AEM nell’ambiente di authoring
seo-title: Troubleshooting AEM when Authoring
description: Alcuni problemi che potrebbero verificarsi durante l’utilizzo di AEM
seo-description: Some issues that you might encounter when using AEM
uuid: 99af51ea-8628-4811-83f2-ab3f88f0279e
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: da0a5644-2e1d-4394-a6aa-11bb41406ba6
exl-id: 05586b17-35d4-496e-8f0e-293c755eb066
source-git-commit: d1b4cf87291f7e4a0670a21feca1ebf8dd5e0b5e
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 100%

---

# Risoluzione di problemi AEM nell’ambiente di authoring {#troubleshooting-aem-when-authoring}

Nella seguente sezione vengono descritti alcuni problemi che potresti riscontrare durante l’utilizzo di AEM e vengono proposte possibili soluzioni.

>[!NOTE]
>
>Quando si verificano problemi, è anche utile controllare l’elenco dei [Problemi noti](/help/release-notes/release-notes.md) per l’istanza (release e service pack).

>[!NOTE]
>
>Gli utenti con diritti di amministratore possono seguire i metodi di risoluzione di problemi descritti in [Troubleshooting AEM (for Administrators) ](/help/sites-administering/troubleshoot.md)(Risoluzione di problemi in AEM - Per amministratori). Se non disponi delle autorizzazioni necessarie, rivolgiti al tuo amministratore di sistema per la risoluzione dei problemi AEM.

## La vecchia versione della pagina è ancora nel sito pubblicato {#old-page-version-still-on-published-site}

* **Problema**:

   * Hai apportato delle modifiche a una pagina e l’hai replicata sul sito pubblicato, ma nel sito pubblicato viene ancora visualizzata la *vecchia* versione della pagina.

* **Motivo**:

   * Questo può dipendere da diverse cause. In genere si tratta di un problema di cache (del browser locale o del Dispatcher), ma a volte può dipendere da un problema relativo alla coda di replica.

* **Soluzioni**:

   * Esistono diverse possibilità:
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

   * In rari casi, un’azione precedente potrebbe pregiudicare il funzionamento della barra degli strumenti.

* **Soluzione**:

   * Aggiorna la pagina.
