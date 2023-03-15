---
title: Stato delle funzioni dell’interfaccia touch
description: Note sulla versione specifiche per [!DNL Adobe Experience Manager] Interfaccia touch.
exl-id: 7b71e8db-e8c6-4470-bc22-db3d4600b7fc
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1063'
ht-degree: 15%

---

# Stato delle funzioni dell’interfaccia touch {#touch-ui-feature-status}

AEM 6.4 e successivi [L’interfaccia classica è obsoleta](../release-notes/deprecated-removed-features.md). Adobe non apporterà ulteriori miglioramenti all’interfaccia utente classica e gli utenti sono invitati a sfruttare le nuove potenti funzioni disponibili nell’interfaccia touch.

A partire dalla versione 6.0, AEM introdotto una nuova interfaccia utente denominata &quot;interfaccia touch&quot; (semplicemente denominata &quot;interfaccia touch&quot;) allineata alla versione 6.0. [!DNL Adobe Experience Cloud] e alle linee guida generali dell’interfaccia utente di Adobe. Parità di funzioni quasi raggiunta, questa è diventata l’interfaccia standard in AEM con l’interfaccia legacy, orientata al desktop, denominata &quot;interfaccia classica&quot;.

La maggior parte delle funzionalità è presente nell’interfaccia touch, ma alcune non sono ancora complete e verranno aggiunte nelle versioni future.

L’elenco seguente mostra lo stato attuale delle funzionalità implementate in AEM 6.5.

Per consigli per i clienti che eseguono l’aggiornamento a AEM 6.5, consulta [Raccomandazioni in merito all’interfaccia utente per i clienti](/help/sites-deploying/ui-recommendations.md).

>[!NOTE]
>
>Questa pagina tratta solo la parità delle funzioni con l’interfaccia classica. Le funzionalità aggiunte e univoche all’interfaccia touch che non sono presenti nell’interfaccia classica non sono elencate.

>[!NOTE]
>
>L&#39;elenco si prefigge di essere completo, ma non esaustivo.

## Legenda {#legend}

* **Completa**: Questa funzione è completamente disponibile nell’interfaccia touch.
* **Principalmente**: La funzione è disponibile principalmente nell’interfaccia touch.
* **Mancante**: La funzione non è presente nell’interfaccia touch, ma è necessario utilizzare l’interfaccia classica per eseguire questa azione.
* **Sostituito**: La funzione è stata sostituita da una nuova implementazione che funziona in modo diverso.
* **Rimosso**: La funzione non esiste più nell’interfaccia touch e non verrà sostituita.

## Stato della funzione: Amministratore di Sites {#feature-status-sites-admin}

Elenco delle funzionalità per l’amministrazione dei siti nell’interfaccia classica (`/siteadmin`) e lo stato nell’interfaccia touch (`/sites.html`).

| Funzione obsoleta | Stato | Commenti |
|--- |--- |--- |
| Spostarsi nella gerarchia del sito | Completa | AEM 6.4 introduce [visualizzazione struttura contenuto](/help/sites-authoring/basic-handling.md#content-tree). |
| Avvia flusso di lavoro | Completa |  |
| Crea nuova pagina | Completa |  |
| Crea nuovo sito | Completa |  |
| Crea nuovo lancio | Completa |  |
| Creare una nuova Live Copy | Completa |  |
| Crea cartella | Completa |  |
| Mostra stato di pubblicazione | Completa | A partire AEM 6.5, lo stato del flusso di lavoro viene visualizzato nella vista a elenco. |
| Ricerca | Completa |  |
| Copia e incolla pagina (duplicato) | Completa |  |
| Sposta pagina/e | Completa |  |
| Pubblicare le pagine | Completa |  |
| Pubblicare pagine senza diritti di replica | Completa |  |
| Pubblica più tardi | Completa |  |
| Pubblica albero | Completa |  |
| Annullare la pubblicazione di pagine | Completa |  |
| Annullare la pubblicazione di pagine senza diritti di replica | Completa |  |
| Annulla pubblicazione più tardi | Completa |  |
| Eliminare | Completa |  |
| Blocca/Sblocca | Completa |  |
| Visualizza/Modifica proprietà | Completa |  |
| Impostare le autorizzazioni sulle pagine | Completa |  |
| Cronologia delle versioni | Completa |  |
| Ripristina versione | Completa |  |
| Ripristinare la struttura ad albero e ripristinare le pagine eliminate | Mancante | Utilizzare l’interfaccia classica. |
| Mostra differenza tra versione precedente e versione corrente | Completa |  |
| Azioni Livecopy (rollout) | Completa |  |
| Vedere copie per lingua | Completa |  |
| Trova e sostituisci | Mancante | Utilizzare l’interfaccia classica. |
| Casella in entrata notifica (eventi JCR) | Mancante | Utilizzare l’interfaccia classica. Verrà sostituito con un’implementazione diversa. |
| Riferimenti | Completa | Visualizzazione dei collegamenti alle pagine in entrata aggiunti alla AEM 6.5. |

## Stato della funzione: Editor pagina {#feature-status-page-editor}

Elenco delle funzionalità dell’interfaccia classica Editor pagina (`/cf#`) e lo stato in touch-enabled (`/editor.html`).

| Funzione obsoleta | Stato | Commenti |
|--- |--- |--- |
| Modifica pagine Web | Completa |  |
| Modifica pagine web mobili | Completa |  |
| Modificare i contenuti importati tramite Importazione progettazione | Completa |  |
| Modifica e-mail | Completa |  |
| Modificare le app mobili ibride | Completa |  |
| Modifica Forms | Completa |  |
| Modifica offerte | Completa |  |
| Modifica modelli di flussi di lavoro | Completa |  |
| Modalità: Modifica e anteprima | Completa |  |
| Anteprima reattiva | Completa |  |
| Modalità: Modifica progettazione | Completa |  |
| Modalità: Scaffolding | Completa |  |
| Modalità: Stato Live Copy | Completa |  |
| Aggiungi annotazioni | Completa |  |
| Modifica delle proprietà | Completa |  |
| Pagina di rollout | Completa |  |
| Avvia e mostra il flusso di lavoro | Completa |  |
| Gestione dei pacchetti dei flussi di lavoro | Principalmente | Completamente accessibile nell’interfaccia touch. Payload per flussi di lavoro multipli viene comunque presentato nell’interfaccia classica. |
| Blocca/Sblocca pagina | Completa |  |
| Pubblica pagina | Completa |  |
| Annulla pubblicazione pagina | Completa |  |
| Copia pagina | Rimosso | Usa amministratore del sito per [copiare le pagine](/help/sites-authoring/managing-pages.md#copying-and-pasting-a-page). |
| Sposta pagina | Rimosso | Usa amministratore del sito per [spostare le pagine](/help/sites-authoring/managing-pages.md#moving-or-renaming-a-page). |
| Elimina pagina | Rimosso | Usa amministratore del sito per [eliminare le pagine](/help/sites-authoring/managing-pages.md#deleting-a-page). |
| Mostra riferimenti | Rimosso | Utilizza l’ amministratore del sito per visualizzare le [elenco dettagliato di riferimento](/help/sites-authoring/author-environment-tools.md#references). |
| Registro di controllo | Rimosso | Utilizza Site Admin e [barra delle attività aperta](/help/sites-authoring/author-environment-tools.md#events-timeline). |
| Crea versione | Rimosso | Usa amministratore del sito per [creare nuove versioni](/help/sites-authoring/working-with-page-versions.md#creating-a-new-version). |
| Ripristina versione | Rimosso | Usa amministratore del sito per [ripristina versioni](/help/sites-authoring/working-with-page-versions.md#reverting-to-a-page-version). |
| Avvii switch | Rimosso | Usa amministratore del sito per [passare da un avvio all&#39;altro](/help/sites-authoring/launches-promoting.md). |
| Traduci pagina | Rimosso | Usa amministratore del sito per [aggiungi pagina ai progetti di traduzione](/help/sites-administering/tc-manage.md). |
| Timewarp (scegli data/ora e sfoglia il sito così come ha guardato) | Completa |  |
| Impostare le autorizzazioni | Completa |  |
| Interfaccia utente Client Context | Sostituito | Utilizza la [ContextHub](/help/sites-authoring/ch-previewing.md) L’interfaccia utente continua. |
| Content Finder per i vari tipi di contenuti multimediali | Completa |  |
| Elenco dei componenti | Completa |  |
| Copiare e incollare i componenti | Completa |  |
| Elenco dei componenti negli Appunti | Mancante |  |
| Annulla/Ripeti | Completa |  |
| Trascina il contenuto nel segnaposto del componente | Completa |  |
| Trascina i contenuti direttamente nel segnaposto parsys con la creazione automatica dei componenti | Completa |  |

## Stato della funzione: Editor di testo, tabelle e immagini {#feature-status-text-table-and-image-editors}

Elenco delle funzionalità disponibili nell’interfaccia classica per l’editor di testo, tabelle e immagini e dello stato nell’interfaccia touch.

| Funzione obsoleta | Stato | Commenti |
|--- |--- |--- |
| Editor Rich Text | Completa | Utilizzabile in-place, nella finestra di dialogo e a schermo intero. |
| Abilitare/disabilitare i plug-in RTE | Completa | Può essere eseguito utilizzando [Editor modelli](/help/sites-authoring/templates.md). |
| Usa editor Rich Text per testo normale | Completa |  |
| Plug-in RTE: Collegamenti e ancoraggio | Completa |  |
| Plug-in RTE: Mappa dei caratteri | Completa |  |
| Plug-in RTE: Copia/Incolla | Completa |  |
| Plug-in RTE: Incolla da Microsoft Word | Completa |  |
| Plug-in RTE: Trova e sostituisci | Completa |  |
| Plug-in RTE: Formati di testo (grassetto, ...) | Completa |  |
| Plug-in RTE: Sottoscritto | Completa |  |
| Plug-in RTE: Giustifica | Completa |  |
| Plug-in RTE: Elenchi (puntini/numeri) | Completa |  |
| Plug-in RTE: Formato paragrafo | Completa |  |
| Plug-in RTE: Stili testo | Completa |  |
| Plug-in RTE: Editor origine (Modifica HTML) | Completa | Disponibile solo nella finestra di dialogo e a schermo intero. |
| Plug-in RTE: Controllo ortografia | Completa |  |
| Plug-in RTE: Tabella (Editor tabella incorporato) | Completa |  |
| Plug-in RTE: Annulla/Ripristina | Completa |  |
| Plug-in RTE: Consenti immagini in linea | Completa |  |
| Editor tabella | Completa | Utilizzabile in-place, nella finestra di dialogo e a schermo intero. |
| Trascina l’immagine nella cella della tabella | Completa | Utilizzabile in linea |
| Editor immagine | Completa | Utilizzabile in-place, nella finestra di dialogo e a schermo intero. |
| Abilitare/disabilitare i plug-in IPE | Completa | AEM 6.3 ha introdotto un’interfaccia utente nel [Editor modelli](/help/sites-authoring/templates.md). |
| Plug-in IPE: Ritaglio | Completa |  |
| Plug-in IPE: Capovolgimento | Completa |  |
| Plug-in IPE: Annulla/Ripristina | Completa |  |
| Plug-in IPE: Mappa immagine | Completa |  |
| Plug-in IPE: Ruota | Completa |  |
| Plug-in IPE: Zoom | Completa |  |

## Stato della funzione: Strumenti {#feature-status-tools}

Elenco dei vari strumenti disponibili nell’interfaccia classica e dello stato nell’interfaccia touch.

| Funzione obsoleta | Stato | Commenti |
|--- |--- |--- |
| Gestione attività | Sostituito | 6.0 ha introdotto progetti e attività. |
| Casella in entrata flusso di lavoro | Completa |  |
| Configurazione del modello da flusso di lavoro a pagina (`/etc/workflow/wcm/templates.html`) | Mancante | Utilizzare l’interfaccia classica. |
| Assegnazione di tag all’interfaccia utente amministratore | Completa |  |
| Centro di controllo MSM/Blueprint | Completa |  |
| Interfaccia utente di Blueprint Manager | Completa |  |
| Interfaccia utente di configurazione del rollout | Mancante | Utilizzare l’interfaccia classica. |
| Interfaccia utente utente utente, gruppi e autorizzazioni | Più completo | Per la modifica avanzata delle autorizzazioni, utilizza l’interfaccia classica. |
| Elimina versioni (`/etc/versioning/purge.html`) | Mancante | Utilizzare l’interfaccia classica. |
| Verifica collegamenti esterni (`/etc/linkchecker.html`) | Mancante | Utilizzare l’interfaccia classica. |
| Modifiche in serie (`/etc/importers/bulkeditor.html`) | Mancante | Utilizzare l’interfaccia classica. |
| Carica le miniature per aggiungerle o sovrascriverle | Mancante | Utilizzare l’interfaccia classica. |
