---
title: Risoluzione dei problemi di AEM durante l’authoring
description: Nella seguente sezione vengono descritti alcuni problemi che potresti riscontrare durante l’utilizzo di AEM e vengono proposte possibili soluzioni.
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
exl-id: 27a6b012-576e-40bc-9b50-c310b3c56c9e
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '429'
ht-degree: 30%

---

# Risoluzione di problemi AEM nell’ambiente di authoring{#troubleshooting-aem-when-authoring}

Nella seguente sezione vengono descritti alcuni problemi che potresti riscontrare durante l’utilizzo di AEM e vengono proposte possibili soluzioni.

>[!NOTE]
>
>In caso di problemi, vale anche la pena controllare l&#39;elenco di [problemi noti](/help/release-notes/release-notes.md) per la tua istanza (pacchetti di versioni e service pack).

>[!NOTE]
>
>Gli utenti con privilegi di amministratore e che desiderano risolvere i problemi relativi all&#39;AEM possono utilizzare i metodi di risoluzione dei problemi descritti in [Risoluzione dei problemi relativi all&#39;AEM (per gli amministratori)](/help/sites-administering/troubleshoot.md). Se non disponi di privilegi sufficienti, consulta l’amministratore di sistema per la risoluzione dei problemi AEM.

## La vecchia versione della pagina è ancora nel sito pubblicato {#old-page-version-still-on-published-site}

* **Problema**:

   * Hai apportato modifiche a una pagina e l&#39;hai replicata nel sito pubblicato, ma nel sito pubblicato viene ancora visualizzata la versione *vecchia* della pagina.

* **Motivo**:

   * Questo può avere diverse cause, il più delle volte la cache (sia nel browser locale che in Dispatcher), anche se a volte può essere un problema con la coda di replica.

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

   * Quando si utilizza l&#39;opzione **Trova e sostituisci**, è possibile che non tutte le istanze del termine `find` vengano sostituite in una pagina.

* **Motivo**:

   * La capacità di **Trova e sostituisci** dipende da come viene salvato il contenuto e se è possibile eseguirne la ricerca. Ad esempio, il testo di un blog viene archiviato nella proprietà `jcr:text` che non è configurata per la ricerca. L&#39;ambito predefinito per il servlet find e replace include le seguenti proprietà:

      * `jcr:title`
      * `jcr:description`
      * `jcr:text`
      * `text`

* **Soluzione**:

   * È possibile modificare queste definizioni con la configurazione per **Day CQ WCM Find Replace Servlet** utilizzando la **console Web**; ad esempio, all&#39;indirizzo

     `http://localhost:4502/system/console/configMgr`
