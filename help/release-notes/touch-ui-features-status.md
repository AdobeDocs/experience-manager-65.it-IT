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

AEM 6.4 e versioni successive [L’interfaccia classica è obsoleta](../release-notes/deprecated-removed-features.md). Adobe non apporterà ulteriori miglioramenti all’interfaccia classica e gli utenti sono invitati a sfruttare le nuove potenti funzioni disponibili nell’interfaccia touch.

A partire dalla versione 6.0, l’AEM ha introdotto una nuova interfaccia utente denominata &quot;interfaccia touch&quot; (semplicemente denominata &quot;interfaccia touch&quot;), allineata al [!DNL Adobe Experience Cloud] e alle linee guida generali sull’interfaccia utente di Adobe. Con la parità delle funzioni quasi raggiunta, questa è diventata l’interfaccia utente standard in AEM con l’interfaccia legacy orientata al desktop denominata &quot;interfaccia classica&quot;.

Anche se la maggior parte delle funzionalità sono presenti nell’interfaccia utente touch, alcune non sono ancora complete e verranno aggiunte nelle versioni future.

L’elenco seguente mostra lo stato attuale delle funzionalità implementate in AEM 6.5.

Per raccomandazioni per i clienti che passano a AEM 6.5, consulta [Raccomandazioni sull’interfaccia utente per i clienti](/help/sites-deploying/ui-recommendations.md).

>[!NOTE]
>
>Questa pagina tratta solo la parità di funzioni con l’interfaccia classica. Le funzionalità aggiunte e univoche all’interfaccia utente touch che non sono presenti nell’interfaccia classica non sono elencate.

>[!NOTE]
>
>Questo elenco è completo, ma non esaustivo.

## Legenda {#legend}

* **Completa**: la funzione è completamente disponibile nell’interfaccia utente touch.
* **Principalmente**: questa funzione è disponibile principalmente nell’interfaccia utente touch.
* **Mancante**: la funzione non è presente nell’interfaccia touch; per eseguire questa azione, è necessario utilizzare l’interfaccia classica.
* **Sostituito**: la funzione è stata sostituita con una nuova implementazione che funziona in modo diverso.
* **Rimosso**: la funzione non esiste più nell’interfaccia utente touch e non verrà sostituita.

## Stato della funzione: Amministratore siti {#feature-status-sites-admin}

Questo è un elenco delle funzionalità dell&#39;interfaccia utente classica di Amministratore sito (`/siteadmin`) ha e lo stato nell’interfaccia utente touch (`/sites.html`).

| Funzione obsoleta | Stato | Commenti |
|--- |--- |--- |
| Naviga nella gerarchia del sito | Completa | L’AEM 6.4 ha introdotto una [visualizzazione struttura contenuto](/help/sites-authoring/basic-handling.md#content-tree). |
| Avvia flusso di lavoro | Completa |  |
| Crea nuova pagina | Completa |  |
| Crea nuovo sito | Completa |  |
| Crea nuovo lancio | Completa |  |
| Crea nuova Live Copy | Completa |  |
| Crea cartella | Completa |  |
| Mostra stato pubblicazione | Completa | A partire da AEM 6.5, lo stato del flusso di lavoro viene visualizzato nella vista a elenco. |
| Ricerca | Completa |  |
| Copia e incolla pagina (duplicato) | Completa |  |
| Sposta pagine | Completa |  |
| Pubblica pagine | Completa |  |
| Pubblica pagine senza diritti di replica | Completa |  |
| Pubblica più tardi | Completa |  |
| Pubblica struttura | Completa |  |
| Annulla pubblicazione pagine | Completa |  |
| Annulla pubblicazione pagine senza diritti di replica | Completa |  |
| Annulla pubblicazione più tardi | Completa |  |
| Eliminare | Completa |  |
| Blocca/Sblocca | Completa |  |
| Visualizza/Modifica proprietà | Completa |  |
| Imposta autorizzazioni su pagina/e | Completa |  |
| Cronologia versioni | Completa |  |
| Ripristina versione | Completa |  |
| Ripristina struttura e ripristina pagine eliminate | Mancante | Utilizza l’interfaccia classica. |
| Mostra differenza tra la versione precedente e quella corrente | Completa |  |
| Azioni Live Copy (rollout) | Completa |  |
| Vedi copie per lingua | Completa |  |
| Trova e sostituisci | Mancante | Utilizza l’interfaccia classica. |
| Casella in entrata delle notifiche (eventi JCR) | Mancante | Utilizza l’interfaccia classica. Verrà sostituito con un’implementazione diversa. |
| Riferimenti | Completa | Visualizzazione dei collegamenti alle pagine in arrivo aggiunti a AEM 6.5. |

## Stato delle funzioni: Editor pagina {#feature-status-page-editor}

Questo è un elenco di funzionalità dell&#39;Editor pagina per l&#39;interfaccia utente classica (`/cf#`) ha e lo stato nel touch-screen (`/editor.html`).

| Funzione obsoleta | Stato | Commenti |
|--- |--- |--- |
| Modifica pagine Web | Completa |  |
| Modifica pagine web per dispositivi mobili | Completa |  |
| Modifica contenuto importato tramite Importazione progettazione | Completa |  |
| Modifica e-mail | Completa |  |
| Modifica app ibride per dispositivi mobili | Completa |  |
| Modifica Forms | Completa |  |
| Modifica offerte | Completa |  |
| Modifica modelli flussi di lavoro | Completa |  |
| Modalità: Modifica e Anteprima | Completa |  |
| Anteprima reattiva | Completa |  |
| Modalità: Modifica progettazione | Completa |  |
| Modalità: scaffolding | Completa |  |
| Modalità: Stato Live Copy | Completa |  |
| Aggiungere annotazioni | Completa |  |
| Modifica delle proprietà | Completa |  |
| Rollout pagina | Completa |  |
| Avvia e mostra flusso di lavoro | Completa |  |
| Gestione dei pacchetti del flusso di lavoro | Principalmente | Completamente accessibile nell’interfaccia touch. Nell’interfaccia classica sono ancora presenti più payload di flusso di lavoro. |
| Blocca/Sblocca pagina | Completa |  |
| Pubblica pagina | Completa |  |
| Annulla pubblicazione pagina | Completa |  |
| Copia pagina | Rimosso | Utilizza Site Admin per [copia pagine](/help/sites-authoring/managing-pages.md#copying-and-pasting-a-page). |
| Sposta pagina | Rimosso | Utilizza Site Admin per [sposta pagine](/help/sites-authoring/managing-pages.md#moving-or-renaming-a-page). |
| Elimina pagina | Rimosso | Utilizza Site Admin per [eliminare pagine](/help/sites-authoring/managing-pages.md#deleting-a-page). |
| Mostra riferimenti | Rimosso | Utilizza Site Admin per visualizzare [elenco dettagliato dei riferimenti](/help/sites-authoring/author-environment-tools.md#references). |
| Registro di controllo | Rimosso | Utilizzare Amministrazione sito e [apri barra attività](/help/sites-authoring/author-environment-tools.md#events-timeline). |
| Crea versione | Rimosso | Utilizza Site Admin per [creare nuove versioni](/help/sites-authoring/working-with-page-versions.md#creating-a-new-version). |
| Ripristina versione | Rimosso | Utilizza Site Admin per [ripristinare le versioni](/help/sites-authoring/working-with-page-versions.md#reverting-to-a-page-version). |
| Cambia avvii | Rimosso | Utilizza Site Admin per [passare da un avvio all&#39;altro](/help/sites-authoring/launches-promoting.md). |
| Traduci pagina | Rimosso | Utilizza Site Admin per [aggiungi pagina ai progetti di traduzione](/help/sites-administering/tc-manage.md). |
| Timewarp (scegli data/ora e sfoglia il sito come appariva) | Completa |  |
| Imposta autorizzazioni | Completa |  |
| Interfaccia utente ClientContext | Sostituito | Utilizza il [ContextHub](/help/sites-authoring/ch-previewing.md) Interfaccia utente in corso. |
| Finder di contenuti per i vari tipi di media | Completa |  |
| Elenco dei componenti | Completa |  |
| Copiare e incollare componenti | Completa |  |
| Elenco dei componenti negli Appunti | Mancante |  |
| Annulla/Ripeti | Completa |  |
| Trascina contenuto nel segnaposto del componente | Completa |  |
| Trascina il contenuto direttamente nel segnaposto parsys con creazione automatica del componente | Completa |  |

## Stato delle funzioni: editor di testo, tabelle e immagini {#feature-status-text-table-and-image-editors}

Elenco delle funzionalità dell’editor di testo, tabelle e immagini dell’interfaccia classica e dello stato dell’interfaccia touch.

| Funzione obsoleta | Stato | Commenti |
|--- |--- |--- |
| Editor Rich Text | Completa | Utilizzabile sul posto, nella finestra di dialogo e a schermo intero. |
| Abilitare/disabilitare i plug-in dell’editor Rich Text | Completa | Può essere eseguito utilizzando [Editor modelli](/help/sites-authoring/templates.md). |
| Usa editor Rich Text per testo normale | Completa |  |
| Plug-in RTE: collegamenti e ancoraggio | Completa |  |
| Plug-in Editor Rich Text: Mappa caratteri | Completa |  |
| Plug-in Editor Rich Text: Copia/Incolla | Completa |  |
| Plug-in RTE: Incolla da Microsoft Word | Completa |  |
| Plug-in RTE: Trova e sostituisci | Completa |  |
| Plug-in RTE: formati di testo (grassetto, ...) | Completa |  |
| Plug-in RTE: secondario e apice | Completa |  |
| Plug-in Editor Rich Text: Giustifica | Completa |  |
| Plug-in Editor Rich Text: Elenchi (punto elenco/numeri) | Completa |  |
| Plug-in Editor Rich Text: Formato paragrafo | Completa |  |
| Plug-in Editor Rich Text: Stili di testo | Completa |  |
| Plug-in Editor Rich Text: Editor origine (Modifica HTML) | Completa | Disponibile solo nella finestra di dialogo e a schermo intero. |
| Plug-in RTE: controllo ortografico | Completa |  |
| Plug-in RTE: tabella (Editor tabella incorporato) | Completa |  |
| Plug-in Editor Rich Text: Annulla/Ripristina | Completa |  |
| Plug-in RTE: Consenti immagini in linea | Completa |  |
| Editor tabella | Completa | Utilizzabile sul posto, nella finestra di dialogo e a schermo intero. |
| Trascina l’immagine nella cella della tabella | Completa | Utilizzabile in linea |
| Editor immagine | Completa | Utilizzabile sul posto, nella finestra di dialogo e a schermo intero. |
| Abilitare/disabilitare i plug-in IPE | Completa | L’AEM 6.3 ha introdotto un’interfaccia utente nella [Editor modelli](/help/sites-authoring/templates.md). |
| Plug-in IPE: ritaglio | Completa |  |
| Plug-in IPE: capovolgimento | Completa |  |
| Plug-in IPE: Annulla/Ripristina | Completa |  |
| Plug-in IPE: mappa immagine | Completa |  |
| Plug-in IPE: rotazione | Completa |  |
| Plug-in IPE: zoom | Completa |  |

## Stato della funzione: Strumenti {#feature-status-tools}

Questo è un elenco di vari strumenti di cui dispone l’interfaccia classica e lo stato dell’interfaccia touch.

| Funzione obsoleta | Stato | Commenti |
|--- |--- |--- |
| Gestione attività | Sostituito | 6.0 ha introdotto progetti e compiti. |
| Casella in entrata flusso di lavoro | Completa |  |
| Configurazione da flusso di lavoro a modello pagina (`/etc/workflow/wcm/templates.html`) | Mancante | Utilizza l’interfaccia classica. |
| Interfaccia utente amministratore assegnazione tag | Completa |  |
| Centro controllo MSM/blueprint | Completa |  |
| Interfaccia utente di Gestione blueprint | Completa |  |
| Interfaccia utente configurazione rollout | Mancante | Utilizza l’interfaccia classica. |
| Interfaccia utente per utenti, gruppi e autorizzazioni | Principalmente completo | Per la modifica avanzata delle autorizzazioni, utilizza l’interfaccia classica. |
| Rimuovi versioni (`/etc/versioning/purge.html`) | Mancante | Utilizza l’interfaccia classica. |
| Verifica collegamenti esterni (`/etc/linkchecker.html`) | Mancante | Utilizza l’interfaccia classica. |
| Editor in blocco (`/etc/importers/bulkeditor.html`) | Mancante | Utilizza l’interfaccia classica. |
| Carica le miniature per aggiungerle o sovrascriverle | Mancante | Utilizza l’interfaccia classica. |
