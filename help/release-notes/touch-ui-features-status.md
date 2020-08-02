---
title: Stato delle funzioni dell’interfaccia touch
description: Note sulla versione specifiche [!DNL Adobe Experience Manager] per l’interfaccia touch.
translation-type: tm+mt
source-git-commit: d938f52766154b68df2f6db2c8c49a0ad97e7e6d
workflow-type: tm+mt
source-wordcount: '1063'
ht-degree: 14%

---


# Touch UI Feature Status {#touch-ui-feature-status}

AEM 6.4 a partire dall’interfaccia [classica è obsoleta](../release-notes/deprecated-removed-features.md).  Adobe non apporterà ulteriori miglioramenti all’interfaccia classica e gli utenti sono invitati a utilizzare le nuove potenti funzioni disponibili nell’interfaccia touch.

A partire dalla versione 6.0, AEM introdotto una nuova interfaccia utente denominata &quot;interfaccia touch&quot; (interfaccia touch) allineata alle linee guida [!DNL Adobe Experience Cloud] e alle linee guida generali dell’interfaccia utente del Adobe . Raggiunta la parità delle funzioni, questa è diventata l’interfaccia standard in AEM con l’interfaccia precedente, orientata al desktop, detta &quot;interfaccia classica&quot;.

Anche se la maggior parte delle funzionalità sono presenti nell’interfaccia touch, alcune funzioni non sono ancora complete e verranno aggiunte nelle release future.

L&#39;elenco seguente mostra lo stato corrente delle funzionalità come implementato in AEM 6.5.

Per le raccomandazioni per i clienti che eseguono l&#39;aggiornamento a AEM 6.5, vedete Suggerimenti per l&#39;interfaccia [utente per i clienti](/help/sites-deploying/ui-recommendations.md).

>[!NOTE]
>
>Questa pagina tratta solo la parità delle funzioni con l’interfaccia classica. Non sono elencate le funzionalità aggiunte e univoche all’interfaccia touch che non sono presenti nell’interfaccia classica.

>[!NOTE]
>
>L&#39;elenco è completo, ma non esaustivo.

## Legenda {#legend}

* **Completa**: Questa funzione è completamente disponibile nell’interfaccia touch.
* **Principalmente**: Questa funzione è disponibile per la maggior parte nell’interfaccia touch.
* **Mancanti**: La funzione non è disponibile nell’interfaccia touch, ma deve essere utilizzata anche l’interfaccia classica.
* **Sostituito**: La funzione è stata sostituita da una nuova implementazione che funziona in modo diverso.
* **Rimosso**: La funzione non esiste più nell’interfaccia touch e non verrà sostituita.

## Stato funzione: Amministrazione siti {#feature-status-sites-admin}

Si tratta di un elenco delle funzionalità di cui dispone l’amministratore del sito (`/siteadmin`) dell’interfaccia classica e dello stato nell’interfaccia touch (`/sites.html`).

| Funzione obsoleta | Stato | Commento |
|--- |--- |--- |
| Naviga gerarchia sito | Completa | AEM 6.4 ha introdotto una visualizzazione [ad albero del](/help/sites-authoring/basic-handling.md#content-tree)contenuto. |
| Avvia flusso di lavoro | Completa |  |
| Crea nuova pagina | Completa |  |
| Crea nuovo sito | Completa |  |
| Crea nuovo lancio | Completa |  |
| Creare una nuova Live Copy | Completa |  |
| Crea cartella | Completa |  |
| Mostra stato pubblicazione | Completa | A partire da AEM 6.5, lo stato del flusso di lavoro viene visualizzato nella vista a elenco. |
| Ricerca | Completa |  |
| Copiare e incollare la pagina (duplicato) | Completa |  |
| Sposta pagine | Completa |  |
| Pubblicare le pagine | Completa |  |
| Pubblicare pagine senza diritti di replica | Completa |  |
| Pubblica più tardi | Completa |  |
| Pubblica albero | Completa |  |
| Annullamento della pubblicazione delle pagine | Completa |  |
| Annullamento della pubblicazione delle pagine senza diritti di replica | Completa |  |
| Annulla pubblicazione più tardi | Completa |  |
| Elimina | Completa |  |
| Blocca/Sblocca | Completa |  |
| Visualizza/Modifica proprietà | Completa |  |
| Impostazione delle autorizzazioni sulle pagine | Completa |  |
| Cronologia versioni | Completa |  |
| Ripristina versione | Completa |  |
| Ripristinare la struttura ad albero e ripristinare le pagine eliminate | Mancante | Usa interfaccia classica. |
| Mostra differenza tra la versione precedente e quella corrente | Completa |  |
| Azioni Live Copy (Roll-out) | Completa |  |
| Vedere copie della lingua | Completa |  |
| Trova e sostituisci | Mancante | Usa interfaccia classica. |
| Casella in entrata notifica (eventi JCR) | Mancante | Usa interfaccia classica. Sarà sostituito con un&#39;implementazione diversa. |
| Riferimenti | Completa | Visualizzazione dei collegamenti di pagina in entrata aggiunti alla AEM 6.5. |

## Stato funzione: Editor pagina {#feature-status-page-editor}

Si tratta di un elenco delle funzionalità dell’interfaccia classica Editor pagina (`/cf#`) e dello stato in abilitato per il tocco (`/editor.html`).

| Funzione obsoleta | Stato | Commento |
|--- |--- |--- |
| Modifica pagine Web | Completa |  |
| Modifica pagine Web per dispositivi mobili | Completa |  |
| Modificare il contenuto importato tramite Importazione progettazione | Completa |  |
| Modifica e-mail | Completa |  |
| Modifica di app mobili ibride | Completa |  |
| Modifica Forms | Completa |  |
| Modifica offerte | Completa |  |
| Modifica modelli flussi di lavoro | Completa |  |
| Modalità: Modifica e anteprima | Completa |  |
| Anteprima reattiva | Completa |  |
| Modalità: Modifica progettazione | Completa |  |
| Modalità: Scaffolding | Completa |  |
| Modalità: Stato Live Copy | Completa |  |
| Aggiunta di annotazioni | Completa |  |
| Modifica delle proprietà | Completa |  |
| Pagina di rollout | Completa |  |
| Avvia e mostra flusso di lavoro | Completa |  |
| Gestione pacchetto flusso di lavoro | Principalmente | Completamente accessibile nell’interfaccia touch. Payload di flussi di lavoro multipli ancora presentati nell’interfaccia classica. |
| Blocca/Sblocca pagina | Completa |  |
| Pubblica pagina | Completa |  |
| Annulla pubblicazione pagina | Completa |  |
| Copia pagina | Rimosso | Utilizzate Site Admin per [copiare le pagine](/help/sites-authoring/managing-pages.md#copying-and-pasting-a-page). |
| Sposta pagina | Rimosso | Utilizzate Amministrazione sito per [spostare le pagine](/help/sites-authoring/managing-pages.md#moving-or-renaming-a-page). |
| Elimina pagina | Rimosso | Utilizzate Amministrazione sito per [eliminare le pagine](/help/sites-authoring/managing-pages.md#deleting-a-page). |
| Mostra riferimenti | Rimosso | Utilizzate Amministrazione sito per visualizzare l&#39;elenco [di riferimento](/help/sites-authoring/author-environment-tools.md#references)dettagliato. |
| Registro di controllo | Rimosso | Utilizzate Site Admin (Amministratore sito) e [aprite la barra](/help/sites-authoring/author-environment-tools.md#events-timeline)delle attività. |
| Crea versione | Rimosso | Utilizzate Site Admin (Amministratore sito) per [creare nuove versioni](/help/sites-authoring/working-with-page-versions.md#creating-a-new-version). |
| Ripristina versione | Rimosso | Utilizzate Site Admin per [ripristinare le versioni](/help/sites-authoring/working-with-page-versions.md#reverting-to-a-page-version). |
| Interrompi avvii | Rimosso | Utilizzate Site Admin (Amministratore sito) per [passare da un avvio all&#39;altro](/help/sites-authoring/launches-promoting.md). |
| Traduci pagina | Rimosso | Utilizzate Site Admin (Amministratore sito) per [aggiungere una pagina ai progetti](/help/sites-administering/tc-manage.md)di traduzione. |
| Timewarp (scegli data/ora e naviga nel sito così come appariva) | Completa |  |
| Imposta autorizzazioni | Completa |  |
| Interfaccia utente ClientContext | Sostituito | Utilizzare l&#39;interfaccia utente [ContextHub](/help/sites-authoring/ch-previewing.md) in futuro. |
| Content Finder per i vari tipi di supporti | Completa |  |
| Elenco componenti | Completa |  |
| Copiare e incollare componenti | Completa |  |
| Elenco di componenti negli Appunti | Mancante |  |
| Annulla/Ripristina | Completa |  |
| Trascinare il contenuto nel segnaposto del componente | Completa |  |
| Trascinate i contenuti direttamente nel segnaposto parsys con la creazione automatica dei componenti | Completa |  |

## Stato funzione: Editor di testo, tabelle e immagini {#feature-status-text-table-and-image-editors}

Si tratta di un elenco delle funzionalità dell’interfaccia classica Testo, Tabella e Editor immagine e dello stato nell’interfaccia touch.

| Funzione obsoleta | Stato | Commento |
|--- |--- |--- |
| Editor Rich Text | Completa | Utilizzabile in posizione, nella finestra di dialogo e a schermo intero. |
| Abilitare/disabilitare i plug-in RTE | Completa | Può essere eseguito utilizzando l&#39;Editor [](/help/sites-authoring/templates.md)modelli. |
| Usa editor Rich Text per testo semplice | Completa |  |
| Plug-in RTE: Collegamenti e ancoraggio | Completa |  |
| Plug-in RTE: Mappa carattere | Completa |  |
| Plug-in RTE: Copia/Incolla | Completa |  |
| Plug-in RTE: Incolla da Microsoft Word | Completa |  |
| Plug-in RTE: Trova e sostituisci | Completa |  |
| Plug-in RTE: Formati di testo (grassetto, ...) | Completa |  |
| Plug-in RTE: Sottoscrittura | Completa |  |
| Plug-in RTE: Giustifica | Completa |  |
| Plug-in RTE: Elenchi (elenchi puntati/numeri) | Completa |  |
| Plug-in RTE: Formato paragrafo | Completa |  |
| Plug-in RTE: Stili di testo | Completa |  |
| Plug-in RTE: Editor origine (Modifica HTML) | Completa | Disponibile solo nella finestra di dialogo e a schermo intero. |
| Plug-in RTE: Controllo ortografia | Completa |  |
| Plug-in RTE: Tabella (Editor tabella incorporato) | Completa |  |
| Plug-in RTE: Annulla/Ripristina | Completa |  |
| Plug-in RTE: Consenti immagini in linea | Completa |  |
| Editor tabella | Completa | Utilizzabile in posizione, nella finestra di dialogo e a schermo intero. |
| Trascinare l&#39;immagine nella cella della tabella | Completa | Utilizzabile in linea |
| Editor immagine | Completa | Utilizzabile in posizione, nella finestra di dialogo e a schermo intero. |
| Abilitare/disabilitare i plug-in IPE | Completa | AEM 6.3 ha introdotto un’interfaccia utente nell’Editor [](/help/sites-authoring/templates.md)modelli. |
| Plug-in IPE: Ritaglio | Completa |  |
| Plug-in IPE: Capovolgimento | Completa |  |
| Plug-in IPE: Annulla/Ripristina | Completa |  |
| Plug-in IPE: Mappa immagine | Completa |  |
| Plug-in IPE: Ruota | Completa |  |
| Plug-in IPE: Zoom | Completa |  |

## Stato funzione: Strumenti {#feature-status-tools}

Si tratta di un elenco di diversi strumenti disponibili nell’interfaccia classica e dello stato nell’interfaccia touch.

| Funzione obsoleta | Stato | Commento |
|--- |--- |--- |
| Gestione attività | Sostituito | 6.0 ha introdotto progetti e attività. |
| Inbox flusso di lavoro | Completa |  |
| Configurazione da flusso di lavoro a modello pagina (`/etc/workflow/wcm/templates.html`) | Mancante | Usa interfaccia classica. |
| Interfaccia utente amministratore dei tag | Completa |  |
| Centro di controllo MSM/Blueprint | Completa |  |
| Interfaccia utente di Blueprint Manager | Completa |  |
| Interfaccia utente di configurazione del rollout | Mancante | Usa interfaccia classica. |
| Interfaccia utente utente, gruppi e autorizzazioni | Completa | Per la modifica avanzata delle autorizzazioni, utilizza l’interfaccia classica. |
| Rimuovi versioni (`/etc/versioning/purge.html`) | Mancante | Usa interfaccia classica. |
| Verifica collegamenti esterni (`/etc/linkchecker.html`) | Mancante | Usa interfaccia classica. |
| Editor di massa (`/etc/importers/bulkeditor.html`) | Mancante | Usa interfaccia classica. |
| Caricare le miniature per aggiungerle o sovrascriverle | Mancante | Usa interfaccia classica. |
