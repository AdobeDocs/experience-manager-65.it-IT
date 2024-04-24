---
title: Stato delle funzioni dell’interfaccia touch
description: Note sulla versione specifiche per [!DNL Adobe Experience Manager] Interfaccia touch.
exl-id: 7b71e8db-e8c6-4470-bc22-db3d4600b7fc
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
source-git-commit: 10268f617b8a1bb22f1f131cfd88236e7d5beb47
workflow-type: tm+mt
source-wordcount: '1076'
ht-degree: 15%

---

# Stato delle funzioni dell’interfaccia touch {#touch-ui-feature-status}

Adobe Experience Manager (AEM) 6.4 e versioni successive [L’interfaccia classica è obsoleta](../release-notes/deprecated-removed-features.md). Adobe non sta apportando ulteriori miglioramenti all’interfaccia classica e gli utenti sono invitati a utilizzare le nuove potenti funzioni disponibili nell’interfaccia touch.

A partire dalla versione 6.0, l’AEM ha introdotto una nuova interfaccia utente denominata &quot;interfaccia touch&quot; (denominata &quot;interfaccia touch&quot;), allineata al [!DNL Adobe Experience Cloud] e alle linee guida generali sull’interfaccia utente di Adobe. Con la parità delle funzioni quasi raggiunta, questa è diventata l’interfaccia utente standard in AEM con l’interfaccia legacy orientata al desktop denominata &quot;interfaccia classica&quot;.

Anche se la maggior parte delle funzionalità sono presenti nell’interfaccia utente touch, alcune non sono ancora complete e verranno aggiunte nelle versioni future.

L’elenco seguente mostra lo stato delle funzionalità implementate in AEM 6.5.

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
| Naviga nella gerarchia del sito | Completato | L’AEM 6.4 ha introdotto una [visualizzazione struttura contenuto](/help/sites-authoring/basic-handling.md#content-tree). |
| Avvia flusso di lavoro | Completato |  |
| Crea nuova pagina | Completato |  |
| Crea nuovo sito | Completato |  |
| Crea nuovo lancio | Completato |  |
| Crea nuova Live Copy | Completato |  |
| Crea cartella | Completato |  |
| Mostra stato pubblicazione | Completato | A partire da AEM 6.5, lo stato del flusso di lavoro viene visualizzato nella vista a elenco. |
| Ricerca | Completato |  |
| Copia e incolla pagina (duplicato) | Completato |  |
| Sposta pagine | Completato |  |
| Pubblicare le pagine | Completato |  |
| Pubblicare pagine senza diritti di replica | Completato |  |
| Pubblica più tardi | Completato |  |
| Pubblica struttura | Completato |  |
| Annullare la pubblicazione delle pagine | Completato |  |
| Annullare la pubblicazione delle pagine senza diritti di replica | Completato |  |
| Annulla pubblicazione più tardi | Completato |  |
| Eliminare | Completato |  |
| Blocca/Sblocca | Completato |  |
| Visualizza/Modifica proprietà | Completato |  |
| Impostare le autorizzazioni sulle pagine | Completato |  |
| Cronologia delle versioni | Completato |  |
| Ripristina versione | Completato |  |
| Ripristina struttura e ripristina pagine eliminate | Mancante | Utilizza l’interfaccia classica. |
| Mostra differenza tra la versione precedente e quella corrente | Completato |  |
| Azioni Live Copy (rollout) | Completato |  |
| Vedi copie per lingua | Completato |  |
| Trova e sostituisci | Mancante | Utilizza l’interfaccia classica. |
| Casella in entrata delle notifiche (eventi JCR) | Mancante | Utilizza l’interfaccia classica. Sostituito con un’implementazione diversa in futuro. |
| Riferimenti | Completato | Visualizzazione dei collegamenti alle pagine in arrivo aggiunti a AEM 6.5. |

## Stato delle funzioni: Editor pagina {#feature-status-page-editor}

Questo è un elenco di funzionalità dell&#39;Editor pagina per l&#39;interfaccia utente classica (`/cf#`) ha e lo stato nel touch-screen (`/editor.html`).

| Funzione obsoleta | Stato | Commenti |
|--- |--- |--- |
| Modifica pagine Web | Completato |  |
| Modifica pagine web per dispositivi mobili | Completato |  |
| Modifica contenuto importato tramite Importazione progettazione | Completato |  |
| Modifica e-mail | Completato |  |
| Modifica app ibride per dispositivi mobili | Completato |  |
| Modifica Forms | Completato |  |
| Modifica offerte | Completato |  |
| Modifica modelli flussi di lavoro | Completato |  |
| Modalità: Modifica e Anteprima | Completato |  |
| Anteprima reattiva | Completato |  |
| Modalità: Modifica progettazione | Completato |  |
| Modalità: scaffolding | Completato |  |
| Modalità: Stato Live Copy | Completato |  |
| Aggiungere annotazioni | Completato |  |
| Modifica proprietà | Completato |  |
| Rollout pagina | Completato |  |
| Avvia e mostra flusso di lavoro | Completato |  |
| Gestione dei pacchetti del flusso di lavoro | Principalmente | Accessibile nell’interfaccia touch. Nell’interfaccia classica sono ancora presenti più payload di flusso di lavoro. |
| Blocca/Sblocca pagina | Completato |  |
| Pubblica pagina | Completato |  |
| Annulla pubblicazione pagina | Completato |  |
| Copia pagina | Rimosso | Utilizza Site Admin per [copia pagine](/help/sites-authoring/managing-pages.md#copying-and-pasting-a-page). |
| Sposta pagina | Rimosso | Utilizza Site Admin per [sposta pagine](/help/sites-authoring/managing-pages.md#moving-or-renaming-a-page). |
| Elimina pagina | Rimosso | Utilizza Site Admin per [eliminare pagine](/help/sites-authoring/managing-pages.md#deleting-a-page). |
| Mostra riferimenti | Rimosso | Utilizza Site Admin per visualizzare [elenco dettagliato dei riferimenti](/help/sites-authoring/author-environment-tools.md#references). |
| Registro di controllo | Rimosso | Utilizzare Amministrazione sito e [apri barra attività](/help/sites-authoring/author-environment-tools.md#events-timeline). |
| Crea versione | Rimosso | Utilizza Site Admin per [creare nuove versioni](/help/sites-authoring/working-with-page-versions.md#creating-a-new-version). |
| Ripristina versione | Rimosso | Utilizza Site Admin per [ripristinare le versioni](/help/sites-authoring/working-with-page-versions.md#reverting-to-a-page-version). |
| Cambia avvii | Rimosso | Utilizza Site Admin per [passare da un avvio all&#39;altro](/help/sites-authoring/launches-promoting.md). |
| Traduci pagina | Rimosso | Utilizza Site Admin per [aggiungi pagina ai progetti di traduzione](/help/sites-administering/tc-manage.md). |
| Timewarp (scegli la data/ora e sfoglia il sito come è apparso) | Completato |  |
| Imposta autorizzazioni | Completato |  |
| Interfaccia utente ClientContext | Sostituito | Utilizza il [ContextHub](/help/sites-authoring/ch-previewing.md) Interfaccia utente in corso. |
| Finder di contenuti per i vari tipi di media | Completato |  |
| Elenco dei componenti | Completato |  |
| Copiare e incollare componenti | Completato |  |
| Elenco dei componenti negli Appunti | Mancante |  |
| Annulla/Ripeti | Completato |  |
| Trascina contenuto nel segnaposto del componente | Completato |  |
| Trascina il contenuto direttamente nel segnaposto parsys con creazione automatica del componente | Completato |  |

## Stato delle funzioni: editor di testo, tabelle e immagini {#feature-status-text-table-and-image-editors}

Elenco delle funzionalità dell’editor di testo, tabelle e immagini dell’interfaccia classica e dello stato dell’interfaccia touch.

| Funzione obsoleta | Stato | Commenti |
|--- |--- |--- |
| Editor Rich Text | Completato | Utilizzabile sul posto, nella finestra di dialogo e a schermo intero. |
| Abilitare/disabilitare i plug-in dell’editor Rich Text | Completato | Può essere eseguita utilizzando [Editor modelli](/help/sites-authoring/templates.md). |
| Usa editor Rich Text per testo normale | Completato |  |
| Plug-in RTE: collegamenti e ancoraggio | Completato |  |
| Plug-in Editor Rich Text: Mappa caratteri | Completato |  |
| Plug-in Editor Rich Text: Copia/Incolla | Completato |  |
| Plug-in RTE: Incolla da Microsoft® Word | Completato |  |
| Plug-in RTE: Trova e sostituisci | Completato |  |
| Plug-in RTE: formati di testo (grassetto, ...) | Completato |  |
| Plug-in RTE: secondario e apice | Completato |  |
| Plug-in Editor Rich Text: Giustifica | Completato |  |
| Plug-in Editor Rich Text: Elenchi (punti elenco/numeri) | Completato |  |
| Plug-in Editor Rich Text: Formato paragrafo | Completato |  |
| Plug-in Editor Rich Text: Stili di testo | Completato |  |
| Plug-in Editor Rich Text: Editor origine (Modifica HTML) | Completato | Disponibile solo nella finestra di dialogo e a schermo intero. |
| Plug-in RTE: controllo ortografico | Completato |  |
| Plug-in RTE: tabella (Editor tabella incorporato) | Completato |  |
| Plug-in Editor Rich Text: Annulla/Ripristina | Completato |  |
| Plug-in RTE: Consenti immagini in linea | Completato |  |
| Editor tabella | Completato | Utilizzabile sul posto, nella finestra di dialogo e a schermo intero. |
| Trascina l’immagine nella cella della tabella | Completato | Utilizzabile in linea |
| Editor immagine | Completato | Utilizzabile sul posto, nella finestra di dialogo e a schermo intero. |
| Abilitare/disabilitare i plug-in IPE | Completato | L’AEM 6.3 ha introdotto un’interfaccia utente nella [Editor modelli](/help/sites-authoring/templates.md). |
| Plug-in IPE: ritaglio | Completato |  |
| Plug-in IPE: capovolgimento | Completato |  |
| Plug-in IPE: Annulla/Ripristina | Completato |  |
| Plug-in IPE: mappa immagine | Completato |  |
| Plug-in IPE: rotazione | Completato |  |
| Plug-in IPE: zoom | Completato |  |

## Stato della funzione: Strumenti {#feature-status-tools}

Questo è un elenco di vari strumenti di cui dispone l’interfaccia classica e lo stato dell’interfaccia touch.

| Funzione obsoleta | Stato | Commenti |
|--- |--- |--- |
| Gestione attività | Sostituito | 6.0 ha introdotto progetti e compiti. |
| Casella in entrata flusso di lavoro | Completato |  |
| Configurazione da flusso di lavoro a modello pagina (`/etc/workflow/wcm/templates.html`) | Mancante | Utilizza l’interfaccia classica. |
| Interfaccia utente amministratore assegnazione tag | Completato |  |
| Centro controllo MSM/blueprint | Completato |  |
| Interfaccia utente di Gestione blueprint | Completato |  |
| Interfaccia utente configurazione rollout | Mancante | Utilizza l’interfaccia classica. |
| Interfaccia utente per utenti, gruppi e autorizzazioni | Principalmente completo | Per la modifica avanzata delle autorizzazioni, utilizza l’interfaccia classica. |
| Rimuovi versioni (`/etc/versioning/purge.html`) | Mancante | Utilizza l’interfaccia classica. |
| Verifica collegamenti esterni (`/etc/linkchecker.html`) | Mancante | Utilizza l’interfaccia classica. |
| Editor in blocco (`/etc/importers/bulkeditor.html`) | Mancante | Utilizza l’interfaccia classica. |
| Carica le miniature per aggiungerle o sovrascriverle | Mancante | Utilizza l’interfaccia classica. |
