---
title: Risoluzione dei problemi durante l’authoring in AEM
description: Alcuni problemi che potresti riscontrare durante l’utilizzo di AEM.
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
exl-id: 05586b17-35d4-496e-8f0e-293c755eb066
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User,Admin,Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: e2c1b6d3-bb7e-4fe8-8c72-f7b403298e91
    internal-label: Authoring
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 751e1826ed53df7522418e50a206f0fe622256a4
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 43%
---
# Risoluzione di problemi AEM durante l’authoring{#troubleshooting-aem-when-authoring}

Nella seguente sezione vengono descritti alcuni problemi che potresti riscontrare durante l’utilizzo di AEM e vengono proposte possibili soluzioni.

>[!NOTE]
>
>In caso di problemi, vale anche la pena controllare l&#39;elenco di [problemi noti](/help/release-notes/release-notes.md) per la tua istanza (pacchetti di versioni e service pack).

>[!NOTE]
>
>Gli utenti con privilegi di amministratore e che desiderano risolvere i problemi relativi ad AEM possono utilizzare i metodi di risoluzione dei problemi descritti in [Risoluzione dei problemi relativi ad AEM (per amministratori)](/help/sites-administering/troubleshoot.md). Se non disponi di privilegi sufficienti, consulta l’amministratore di sistema per la risoluzione dei problemi di AEM.

## La vecchia versione della pagina è ancora nel sito pubblicato {#old-page-version-still-on-published-site}

* **Problema**:

  * Hai apportato modifiche a una pagina e l&#39;hai replicata nel sito pubblicato, ma nel sito pubblicato viene ancora visualizzata la versione *vecchia* della pagina.

* **Motivo**:

  * Questo può avere diverse cause, il più delle volte la cache (sia nel browser locale che in Dispatcher), anche se a volte può essere un problema con la coda di replica.

* **Soluzioni**:

  * Esistono varie possibilità:
  * Verifica che la pagina sia stata replicata correttamente. Controlla lo stato della pagina e, se necessario, lo stato della coda di replica.
  * Cancella la cache del browser locale e accedi di nuovo alla pagina.
  * Aggiungi `?` alla fine dell&#39;URL della pagina. Ad esempio:

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
