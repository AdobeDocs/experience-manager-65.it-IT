---
title: Risoluzione dei problemi AEM durante l’authoring
description: Nella seguente sezione vengono descritti alcuni problemi che potresti riscontrare durante l’utilizzo di AEM e vengono proposte possibili soluzioni.
uuid: eb95e5ba-1eed-4ffb-80c1-9b8468820c22
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 9b492b17-9029-46ae-9dc0-bb21e6b484df
exl-id: 27a6b012-576e-40bc-9b50-c310b3c56c9e
source-git-commit: e1a0b114ce16d0e7f6a464e9d30b8f111297bcc6
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 32%

---

# Risoluzione di problemi AEM nell’ambiente di authoring{#troubleshooting-aem-when-authoring}

Nella seguente sezione vengono descritti alcuni problemi che potresti riscontrare durante l’utilizzo di AEM e vengono proposte possibili soluzioni.

>[!NOTE]
>
>Quando si verificano problemi, è anche utile controllare l&#39;elenco di [Problemi noti](/help/release-notes/release-notes.md) per la tua istanza (release e service pack).

>[!NOTE]
>
>Gli utenti con privilegi di amministratore possono utilizzare i metodi di risoluzione dei problemi descritti in [AEM per la risoluzione dei problemi (per gli amministratori)](/help/sites-administering/troubleshoot.md). Se non disponi di privilegi sufficienti, rivolgiti all’amministratore di sistema per informazioni sulla risoluzione dei AEM.

## La vecchia versione della pagina è ancora nel sito pubblicato {#old-page-version-still-on-published-site}

* **Problema**:

   * Hai apportato modifiche a una pagina e l&#39;hai replicata sul sito pubblicato, ma la *vecchio* sul sito di pubblicazione viene ancora visualizzata la versione della pagina.

* **Motivo**:

   * Questo può avere diverse cause, più spesso la cache (sia il browser locale che il Dispatcher), anche se a volte può essere un problema con la coda di replica.

* **Soluzioni**:

   * Ci sono diverse possibilità qui:
   * Verifica che la pagina sia stata replicata correttamente. Controlla lo stato della pagina e, se necessario, lo stato della coda di replica.
   * Cancella la cache del browser locale e accedi di nuovo alla pagina.
   * Aggiungi `?` alla fine dell’URL della pagina, ad esempio:

      `http://localhost:4502/sites.html/content?`

      In questo modo la pagina viene richiesta direttamente da AEM senza passare dal Dispatcher. Se viene visualizzata la pagina aggiornata, significa che è necessario cancellare la cache del Dispatcher.

   * In caso di problemi relativi alla coda di replica, rivolgiti all’amministratore di sistema.

## Barra laterale non visibile {#sidekick-not-visible}

* **Problema**:

   * La barra laterale non è visibile quando si modifica un contenuto di una pagina nell’ambiente di authoring.

* **Motivo**:

   * In rari casi è possibile che l’intestazione della barra laterale sia stata posizionata al di fuori dell’ambito della finestra corrente. Ciò significa che non è possibile riposizionarlo.

* **Soluzione**:

   * Disconnettiti dalla sessione corrente e accedi di nuovo. La barra laterale torna nella posizione predefinita.

## Trova e sostituisci - Non vengono sostituite tutte le istanze {#find-replace-not-all-instances-are-replaced}

* **Problema:**

   * Quando utilizzi **Trova e sostituisci** può accadere che non tutte le istanze del `find` i termini vengono sostituiti in una pagina.

* **Motivo**:

   * La capacità di **Trova e sostituisci** dipende da come è stato salvato il contenuto e se è possibile eseguire ricerche in esso contenute. Ad esempio, il testo di un blog viene memorizzato in `jcr:text` proprietà non configurata per la ricerca. L’ambito predefinito del servlet di ricerca e sostituzione include le seguenti proprietà:

      * `jcr:title`
      * `jcr:description`
      * `jcr:text`
      * `text`

* **Soluzione**:

   * Queste definizioni possono essere modificate con la configurazione di **Day CQ WCM Find Replace Servlet** utilizzando **Console web**; ad esempio, in

      `http://localhost:4502/system/console/configMgr`
