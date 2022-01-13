---
title: Risoluzione di problemi AEM nell’ambiente di authoring
seo-title: Troubleshooting AEM when Authoring
description: Nella seguente sezione vengono descritti alcuni problemi che potresti riscontrare durante l’utilizzo di AEM e vengono proposte possibili soluzioni.
seo-description: The following section covers some issues that you might encounter when using AEM, together with suggestions on how to troubleshoot them.
uuid: eb95e5ba-1eed-4ffb-80c1-9b8468820c22
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 9b492b17-9029-46ae-9dc0-bb21e6b484df
exl-id: 27a6b012-576e-40bc-9b50-c310b3c56c9e
source-git-commit: d1b4cf87291f7e4a0670a21feca1ebf8dd5e0b5e
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 95%

---

# Risoluzione di problemi AEM nell’ambiente di authoring{#troubleshooting-aem-when-authoring}

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

      `http://localhost:4502/sites.html/content?`

      In questo modo la pagina viene richiesta direttamente da AEM senza passare dal Dispatcher. Se viene visualizzata la pagina aggiornata, significa che è necessario cancellare la cache del Dispatcher.

   * In caso di problemi relativi alla coda di replica, rivolgiti all’amministratore di sistema.

## La barra laterale non è visibile {#sidekick-not-visible}

* **Problema**:

   * La barra laterale non è visibile quando si modifica il contenuto di una pagina nell’ambiente di authoring.

* **Motivo**:

   * In alcuni rari casi è possibile che l’intestazione della barra laterale sia stata posizionata oltre l’ambito della finestra corrente e non puoi quindi riposizionarla.

* **Soluzione**:

   * Disconnettiti dalla sessione corrente ed effettua di nuovo l’accesso. La barra laterale torna nella sua posizione predefinita.

## Trova e sostituisci - Non vengono sostituite tutte le istanze {#find-replace-not-all-instances-are-replaced}

* **Problema:**

   * Quando utilizzi **Trova e sostituisci** può accadere che non tutte le istanze del `find` i termini vengono sostituiti in una pagina.

* **Motivo**:

   * La funzione **Trova e sostituisci** dipende da come è stato salvato il contenuto e se supporta la funzione di ricerca. Ad esempio il testo di un blog è archiviato nella proprietà `jcr:text` che non è configurata per la ricerca. L’ambito predefinito del servlet di ricerca e sostituzione include le seguenti proprietà:

      * `jcr:title`
      * `jcr:description`
      * `jcr:text`
      * `text`

* **Soluzione**:

   * Le definizioni possono essere modificate con la configurazione per **Day CQ WCM Find Replace Servlet** tramite la **console Web**; ad esempio in

      `http://localhost:4502/system/console/configMgr`
