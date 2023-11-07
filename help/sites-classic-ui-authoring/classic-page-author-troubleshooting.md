---
title: Risoluzione dei problemi di AEM durante l’authoring
description: Nella seguente sezione vengono descritti alcuni problemi che potresti riscontrare durante l’utilizzo di AEM e vengono proposte possibili soluzioni.
uuid: eb95e5ba-1eed-4ffb-80c1-9b8468820c22
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 9b492b17-9029-46ae-9dc0-bb21e6b484df
exl-id: 27a6b012-576e-40bc-9b50-c310b3c56c9e
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '429'
ht-degree: 32%

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

     `http://localhost:4502/sites.html/content?`

     In questo modo la pagina viene richiesta direttamente da AEM senza passare dal Dispatcher. Se viene visualizzata la pagina aggiornata, significa che è necessario cancellare la cache del Dispatcher.

   * In caso di problemi relativi alla coda di replica, rivolgiti all’amministratore di sistema.

## Sidekick non visibile {#sidekick-not-visible}

* **Problema**:

   * Il Sidekick non è visibile quando si modifica una pagina di contenuto nell’ambiente di authoring.

* **Motivo**:

   * In rari casi, l&#39;intestazione della barra laterale potrebbe essere stata posizionata al di fuori dell&#39;ambito della finestra corrente. Ciò significa che non è più possibile riposizionarlo.

* **Soluzione**:

   * Esci dalla sessione corrente e accedi di nuovo. Il Sidekick tornerà alla posizione predefinita.

## Trova e sostituisci: non tutte le istanze vengono sostituite {#find-replace-not-all-instances-are-replaced}

* **Problema:**

   * Quando si utilizza **Trova e sostituisci** può accadere che non tutte le istanze del `find` vengono sostituiti in una pagina.

* **Motivo**:

   * La capacità di **Trova e sostituisci** dipende da come viene salvato il contenuto e se è possibile eseguirne la ricerca. Ad esempio, il testo di un blog viene memorizzato in `jcr:text` proprietà non configurata per la ricerca. L&#39;ambito predefinito per il servlet find e replace include le seguenti proprietà:

      * `jcr:title`
      * `jcr:description`
      * `jcr:text`
      * `text`

* **Soluzione**:

   * Queste definizioni possono essere modificate con la configurazione di **Day CQ WCM Find Replace Servlet** utilizzando **Console web**; ad esempio, in

     `http://localhost:4502/system/console/configMgr`
