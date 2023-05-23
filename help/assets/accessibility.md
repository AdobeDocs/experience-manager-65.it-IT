---
title: Funzioni e interfacce accessibili di [!DNL Experience Manager Assets]
description: Scopri le funzioni di accessibilità in [!DNL Adobe Experience Manager] 6,5 [!DNL Assets] aiutare gli utenti con disabilità.
contentOwner: AG
feature: Asset Management
role: User, Architect, Leader
exl-id: 15555941-99a2-4586-8d7b-b22f3ec17805
source-git-commit: 399ae241593b5cc14ef1c2efd090f0d1fae7c2df
workflow-type: tm+mt
source-wordcount: '1924'
ht-degree: 2%

---

<!--
Possible topics to cover in this article are below.

* Compile a list of enhancements done in the last ~1 year.
* Showcase a few prominent use cases (search?) in a screencast.
* Top-level actions supported, such as clickable UI elements, keyboard shortcuts, popup dialogs, etc.
* List all UIs that are keyboard navigable.
* Unified list of the product tasks supported, such as, search assets, download assets, add or editing metadata, use DM Viewers, etc.
* Do we need to add support matrix of user tasks with browser and screen reader combinations. Everything may not work in all browsers and/or using all screen readers.
* Any exceptions that users should be aware of. It may help to call out (it may be done in ACR) what tasks are NOT supported.
* CTAs – what's next and more info from AEM team:
  * Link to ACRs on a.com.
  * Generic a11y info by Adobe to begin with.
  * Link to a11y-specific online methods to report issues, seek support, or request enhancements, if any. Asked the a11y team on Slack.
-->

# Funzioni di accessibilità in [!DNL Adobe Experience Manager Assets] {#accessibility-in-aem-assets}

[!DNL Adobe Experience Manager] consente ai creatori e agli editori di contenuti di offrire esperienze incredibili sul web. Adobe si impegna a includere i creatori con disabilità migliorando l’accessibilità di [!DNL Experience Manager]. Il software viene continuamente migliorato per soddisfare le esigenze di tutti i tipi di utenti e rispettare gli standard mondiali che includono le persone con disabilità visive, uditive, di mobilità o di altro tipo.

[!DNL Experience Manager] pubblica informazioni sulla conformità che descrivono gli standard a cui aderisce, descrivono le funzioni di accessibilità del prodotto e descrivono il livello di conformità. Aiuto per i rapporti sulla conformità per l’accessibilità [!DNL Experience Manager] gli utenti comprendono il livello di aderenza ai vari standard. I miglioramenti apportati in [!DNL Assets] consente a tutti gli utenti di utilizzare facilmente le interfacce tramite tastiera, utilità per la lettura dello schermo, lenti di ingrandimento e altre tecnologie per l&#39;accessibilità.

[!DNL Experience Manager] offre diversi livelli di supporto per i seguenti standard:

* [Linee guida per l’accessibilità dei contenuti web (WCAG) 2.1](https://www.w3.org/TR/WCAG/).
* [Articolo 508 riveduto della legge sulla riabilitazione](https://www.access-board.gov/guidelines-and-standards/communications-and-it/about-the-ict-refresh/final-rule/text-of-the-standards-and-guidelines).
* [Iniziativa per l’accessibilità - Applicazioni Internet avanzate accessibili (WAI-ARIA) di W3C](https://www.w3.org/WAI/standards-guidelines/aria/).
* [EN 301 549](https://en.wikipedia.org/wiki/EN_301_549).

Per leggere un rapporto con i dettagli del livello di conformità, consulta [Rapporto di conformità per l’accessibilità](https://www.adobe.com/accessibility/compliance.html) (ACR).

Per sapere come [!DNL Dynamic Media] è accessibile, vedi [accessibilità in [!DNL Dynamic Media]](/help/assets/accessibility-dm.md).

## Tecnologie assistive {#at-support}

Gli utenti con disabilità si affidano spesso a hardware e software per accedere ai contenuti web e utilizzare prodotti software. Questi strumenti sono noti come tecnologie per l’accessibilità. [!DNL Experience Manager Assets] può lavorare con i seguenti tipi di tecnologie di assistenza (AT) quando si utilizzano le funzionalità principali del software:

* Lettori di schermo e lente di ingrandimento dello schermo.
* Software di riconoscimento vocale.
* Utilizzo della tastiera: navigazione e scelte rapide.
* Hardware di assistenza, compresi i comandi degli interruttori, display Braille aggiornabili e altri dispositivi di input del computer.
* Strumenti di ingrandimento dell’interfaccia utente.

## [!DNL Experience Manager Assets] casi d’uso accessibili {#accessible-assets-use-cases}

In entrata [!DNL Experience Manager], le funzioni di accessibilità soddisfano due requisiti chiave di [!DNL Experience Manager] utenti e i loro clienti.

* I creatori e i progettisti di contenuti dispongono di funzioni per creare e pubblicare contenuti accessibili che vengono utilizzati a loro volta dai clienti e dai visitatori del sito web. Le persone con disabilità utilizzano il contenuto con l’aiuto di tecnologie per l’accessibilità. Per ulteriori informazioni, consulta [linee guida per l’accessibilità web](/help/managing/web-accessibility.md).
* [!DNL Experience Manager] consente inoltre agli utenti e agli amministratori con disabilità di accedere all’interfaccia utente e ai controlli per creare e gestire i contenuti. Le persone con disabilità possono utilizzare tecnologie per l’accessibilità per navigare, utilizzare e gestire [!DNL Assets] funzionalità.

Funzioni principali di [!DNL Assets] sono più accessibili di prima e vengono regolarmente aggiornati per migliorare la conformità agli standard globali. Le operazioni CRUD in [!DNL Assets] dispongono di un certo grado di accessibilità integrato in tali elementi. I flussi di lavoro DAM, come l’aggiunta, la gestione, la ricerca e la distribuzione di risorse, sono accessibili tramite scelte rapide da tastiera, testo per utilità di lettura dello schermo, contrasto dei colori e così via.

## Supporto per l’utilizzo della tastiera {#keyboard-use}

Molti elementi dell’interfaccia utente che possono essere cliccati o utilizzati con un puntatore possono anche essere attivati utilizzando la tastiera. Utilizzando una tastiera, gli utenti possono concentrarsi sugli elementi dell’interfaccia utente e intraprendere un’azione appropriata. Gli utenti possono utilizzare direttamente le scelte rapide da tastiera per attivare un comando o un’azione senza dover concentrarsi sugli elementi dell’interfaccia utente e attivarli tramite la tastiera. Ad esempio, gli utenti possono aprire la timeline di una risorsa sul lato sinistro dell’interfaccia utente navigando sul controllo dell’interfaccia utente tramite tastiera e selezionando `Return`, e selezione `Alt + 2` scelte rapide da tastiera.

<!-- TBD items:

* The option to toggle between list view and card view exposes relevant info to the screen readers. What about column view option? This info can go into ‘basic handling’ info aka article to ‘understand and use the workspace’.
* How to open and browse through the profile popup dialog in [!DNL Experience Manager] UI using a keyboard? The navigation does not match the order of visual display of options on the UI. This info can go into ‘basic handling’ info aka article to ‘understand and use the workspace’. What about setting preferences and impersonating a user?
* Using the [!DNL Experience Manager] tag browser and operating the options like delete tag? This info can go into ‘basic handling’ info aka article to ‘understand and use the workspace’.
* Read-only form fields can be focused with the keyboard. Can users tab to these fields to understand the contents and are they able to copy text from the fields?
-->

### Scelte rapide da tastiera [!DNL Assets] {#keyboard-shortcuts}

Le azioni seguenti in [!DNL Assets] utilizzare le scelte rapide da tastiera elencate. La maggior parte delle scelte rapide da tastiera applicabili a [!DNL Experience Manager] Le console sono applicabili anche a [!DNL Assets]. Consulta [scelte rapide da tastiera per le console](/help/sites-authoring/keyboard-shortcuts.md#keyboard-shortcuts). Scopri come [attivare o disattivare le scelte rapide da tastiera](/help/sites-authoring/keyboard-shortcuts.md#deactivating-keyboard-shortcuts).

| Interfaccia utente o scenario | Scelta rapida da tastiera | Azione |
|---|---|---|
| Vista a colonne in [!DNL Assets] interfaccia utente | Tasti freccia su e freccia giù | Consente di passare a file e cartelle all&#39;interno della stessa gerarchia. |
| Vista a colonne in [!DNL Assets] interfaccia utente | Tasti freccia sinistra e destra | Passa ai file e alle cartelle al di sopra o al di sotto della cartella corrente. |
| Esplorazione delle cartelle in [!DNL Assets] | `/` | Richiama la ricerca aprendo la casella Omnisearch. |
| [!DNL Assets] Console | &grave; | Attiva/disattiva barre laterali |
| [!DNL Assets] Console | `Alt + 1` | Apri la struttura del contenuto. |
| [!DNL Assets] Console | `Alt + 2` | Apri [!UICONTROL Navigazione] barra a sinistra. |
| [!DNL Assets] Console | `Alt + 3` | Visualizzazione [!UICONTROL Timeline] di una risorsa selezionata. |
| [!DNL Assets] Console | `Alt + 4` | Apri i riferimenti Live Copy della risorsa selezionata. |
| [!DNL Assets] Console | `Alt + 5` | Avvia la ricerca nella cartella selezionata. |
| Risorsa o cartella selezionata | Backspace | Elimina la risorsa o la cartella selezionata. |
| Risorsa o cartella selezionata | `p` | Apri la pagina Proprietà della risorsa selezionata. |
| Risorsa o cartella selezionata | `e` | Modifica la risorsa selezionata. |
| Risorsa o cartella selezionata | `m` | Sposta la risorsa selezionata. |
| Risorsa o cartella selezionata | `Ctrl + c` | Copia la risorsa selezionata. |
| Risorsa o cartella selezionata | `Esc` | Annulla la selezione. |
| La finestra di dialogo si apre ed è attiva | `Esc` | Chiudi la finestra di dialogo. |
| All’interno di una cartella in DAM | `Ctrl + v` | Incolla la risorsa copiata. |
| [!DNL Assets] Console | `Ctrl + A` | Seleziona tutte le risorse. |
| Pagine delle proprietà della risorsa | `Ctrl + S` | Salva le modifiche. |
| [!DNL Assets] Console | `?` | Visualizzare un elenco di scelte rapide da tastiera. |

## Accedi e naviga [!DNL Assets] interfaccia utente {#login}

Gli utenti possono utilizzare la tastiera per passare al campo di accesso e compilarlo per effettuare l’accesso. I messaggi di errore dovuti a combinazioni errate di nome utente e password nella pagina di accesso vengono visualizzati dagli assistenti vocali ogni volta che si verifica l’errore.

Dopo aver effettuato l’accesso, gli utenti DAM possono navigare in [!DNL Assets] tramite la tastiera. Gli elementi dell’interfaccia utente, come la barra a sinistra, i menu, il profilo utente, la barra di ricerca, i file e le cartelle e le impostazioni di amministrazione e configurazione sono navigabili da tastiera. L&#39;ordine di navigazione della tastiera è da sinistra a destra e dall&#39;alto al basso. Quando si naviga utilizzando una tastiera, un’opzione actionable, se messa a fuoco, viene evidenziata con un contrasto di colore migliore e narrata da un assistente vocale. Se appropriato, lo stato, ad esempio espanso, compresso e misto, delle opzioni attivate nel menu viene annunciato da un assistente vocale. Inoltre, l’assistente vocale annuncia lo scopo dell’opzione utilizzabile, anziché, ad esempio, l’aspetto o il posizionamento dell’interfaccia.

Se un utente espande l’opzione Aiuto o Profilo utente dal menu, l’assistente vocale annuncia l’opzione o lo stato appropriato. Se un utente espande l’opzione del profilo utente, è possibile selezionare le opzioni disponibili utilizzando una tastiera. Ad esempio, un amministratore può rappresentare un altro utente. Se un utente cerca una stringa da [!UICONTROL Aiuto] , un narratore annuncia &quot;Ricerca nella Guida&quot; per indicare che è in corso una ricerca.

<!-- TBD: Removing for now. Add a more informative video later. Host it on tv.adobe

![Keyboard navigation of top options in [!DNL Experience Manager] user interface](assets/keyboard-navigation-in-aem.gif)

*Figure: Navigating through the options at the top of [!DNL Experience Manager] user interface using `Tab` key.*
-->

## Sfogliare le risorse e visualizzare le informazioni correlate {#browse}

In [!DNL Assets] interfaccia utente, gli utenti possono utilizzare la tastiera per sfogliare l’elenco delle risorse digitali esistenti nell’archivio DAM, visualizzare in anteprima o scaricare una risorsa, vedere le rappresentazioni generate, passare da una vista all’altra, vedere le rappresentazioni generate, vedere la timeline e la cronologia delle versioni, vedere commenti e riferimenti e visualizzare e gestire i metadati.

<!-- TBD: Not sure about the following list items mean:

In [!DNL Experience Manager] header section, when navigating in browse mode, screen reader now announces,
  
  * Suggestions to search in Omnisearch.
  * The state as expanded or collapsed for Solutions, Help, Inbox and User options.
  * The Searching Help status message that is displayed when user enters a search string in Search for Help field under Help option
  * The error message if incorrect value is entered in Impersonate as field under User option and focus correctly moves to the text field (NPR-33804).

Review CQ-4282133 before adding - Close option in a coral-dialog wasn't accessible through keyboard, due to which user cannot trigger close option through keyboard press in version preview dialog. After fix, user can close dialog through close option using keyboard.

* CQ-4273122 - Assets of video/audio type will have aria-label in format "Multimedia player: <Title>" so users relying on screen-reader will get to know that they are video/audio assets.
-->

Durante la navigazione nell’archivio delle risorse, le seguenti funzionalità migliorano l’accessibilità:

* L’assistente vocale annuncia alternative testuali che illustrano lo scopo o la funzionalità delle icone al posto del nome.
* Gli utenti possono accedere e attivare le opzioni dell’interfaccia utente interattiva nell’elenco Riferimenti delle risorse utilizzando i tasti di tastiera.
* Gli elementi in ogni riga nella vista a elenco vengono annunciati dagli assistenti vocali come elementi della stessa riga.
* Durante la navigazione tramite `Tab` , lo stato attivo può passare all’opzione chiudi nell’anteprima della versione.
* Quando si utilizza la tastiera per sfogliare, le opzioni dell’interfaccia utente attivabili evidenziate hanno una messa a fuoco visiva più prominente con un contrasto maggiore. Rende l’area mirata più identificabile per l’utente.
* Uso del `Esc` per rimuovere le icone di azione rapida dalla visualizzazione miniature, non rimuove lo stato attivo dalla tastiera dall&#39;ultimo elemento attivo.
* Con una risorsa selezionata, seleziona `Alt + 4` la scelta rapida da tastiera apre [!UICONTROL Riferimenti] nella barra a sinistra. Utilizzo di `Tab` chiave, gli utenti possono navigare tra le voci di riferimento diverse da zero. L&#39;esplorazione delle sole voci di riferimento diverse da zero consente di risparmiare sforzi e pressioni di tasti.
* I commenti su una risorsa sono disponibili nella timeline della risorsa. È accessibile se si accede alla barra a sinistra utilizzando una tastiera o una scelta rapida da tastiera.
* [!UICONTROL Impostazioni vista] in [!DNL Experience Manager] sono accessibili tramite una tastiera. Gli utenti possono navigare tra le dimensioni disponibili delle schede utilizzando i tasti freccia e selezionare e tabulare per spostarsi e impostare altri elementi nella vista Impostazioni vista esistente.

<!-- TBD: Gradually, as more enhancements are done in these categories, add more content.

## Add and upload digital assets {#upload}

## Configure and administer [!DNL Assets] {#config-admin}

* List the a11y fixes in workflows to configure and administer [!DNL Experience Manager Assets]?
* Some enhancements in Processing profiles creation or application to a folder?
* Some enhancements to metadata properties UI?
-->

## Consente di gestire i contenuti digitali {#manage-assets}

Molte attività di gestione delle risorse, come le operazioni CRUD, il download di una risorsa e l’aggiunta di metadati, sono accessibili a vari livelli. [!DNL Assets] consente di eseguire le attività utilizzando varie tecnologie di assistenza, ad esempio un assistente vocale e una tastiera.

Guarda un video che illustra come utilizzare una tastiera per [sfogliare l’archivio e scaricare una risorsa](https://youtu.be/K3dgqMRQJys).

Per le operazioni sui metadati che vengono in genere eseguite da ruoli quali addetti al marketing e amministratori, le seguenti funzioni migliorano l’accessibilità:

* [!UICONTROL Salva e chiudi] opzione sulla risorsa [!UICONTROL Proprietà] è ora possibile accedere a questa pagina utilizzando la tastiera.
* Gli assistenti vocali annunciano le opzioni per eliminare i tag selezionati in [!UICONTROL Base] scheda della risorsa [!UICONTROL Proprietà].
* Gli utenti possono utilizzare la finestra di dialogo a comparsa Datepicker con una tastiera. L’elemento dell’interfaccia utente Datepicker viene utilizzato per impostare orari di attivazione e orari di disattivazione e per selezionare la data.
* La funzionalità di trascinamento tramite tastiera funziona correttamente in [!UICONTROL Editor schema metadati] in modalità sfoglia dell’assistente vocale.
* Un utente può spostare lo stato attivo utilizzando la tastiera sul campo Aggiungi utente o gruppo in [!UICONTROL Gruppo utenti chiuso] nel [!UICONTROL Autorizzazioni] scheda della cartella [!UICONTROL Proprietà].

## Cercare risorse digitali {#search-assets}

Un’esperienza di ricerca delle risorse rapida e semplice velocizza le operazioni relative ai contenuti. I casi di utilizzo della velocità dei contenuti fanno parte di core [!DNL Assets] funzionalità. Per avviare una ricerca dalla barra di Omnisearch, gli utenti possono utilizzare i tasti di scelta rapida `/` o utilizzare `Tab` insieme agli assistenti vocali per individuare rapidamente l’opzione di ricerca. L’assistente vocale legge il nome dell’opzione come &quot;Pulsante di ricerca&quot; quando lo stato attivo si trova sull’opzione di ricerca ![opzione di ricerca](assets/do-not-localize/search_icon.png). Gli utenti possono selezionare `Return` per aprire la casella Omnisearch. L’assistente vocale non solo legge la parola chiave digitata nella casella di ricerca, ma legge anche i suggerimenti offerti da [!DNL Experience Manager Assets]. Gli utenti possono utilizzare una combinazione di tasti di direzione, `Return`, e `Tab` per accedere alle varie opzioni per attivare una ricerca.

La funzionalità di ricerca è resa accessibile dalle seguenti funzionalità:

* Il titolo della pagina, se disponibile per un assistente vocale, consente di identificare la pagina come pagina di ricerca delle risorse.
* Gli utenti cercano le risorse all’interno del campo Omnisearch. Gli utenti possono aprirla utilizzando la navigazione da tastiera o la scelta rapida da tastiera `/`.
* Gli utenti possono iniziare a digitare la parola chiave di ricerca e quindi selezionare i suggerimenti automatici utilizzando i tasti freccia. Il suggerimento evidenziato può essere selezionato utilizzando `Return` La chiave e le risorse vengono cercate per il suggerimento selezionato.
* Gli assistenti vocali possono identificare e annunciare le caselle di controllo a stato misto (in cui, a meno che non si selezionino tutti i predicati nidificati, le caselle di controllo di primo livello non sono selezionate e sono barrate) nel pannello Filtri durante il filtraggio dei risultati di ricerca.
* Lo stato attivo dell’utente si sposta sulle opzioni di ricerca dopo la chiusura della casella Omnisearch.

Quando si filtrano i risultati di ricerca:

* La pagina dei risultati della ricerca ha un titolo informativo per una migliore comprensione degli utenti di utilità per la lettura dello schermo.
* Un assistente vocale annuncia le opzioni nel filtro di ricerca come fisarmoniche espandibili.
* I predicati con opzioni a stati misti vengono annunciati dagli assistenti vocali.

## Condividere le risorse {#share-assets}

<!-- TBD: Anything about accessibility in DA, BP? AAL team confirmed that there's no content for AAL a11y on helpx.
-->

Quando si condividono le risorse, le seguenti funzionalità migliorano l’accessibilità:

* Un utente può spostare lo stato attivo utilizzando la tastiera nel campo Cerca e aggiungi indirizzo e-mail della finestra di dialogo di condivisione del collegamento.

* Nella finestra di dialogo di condivisione dei collegamenti, in modalità Sfoglia, gli assistenti vocali

   * Non narrare le informazioni della tabella quando la finestra di dialogo viene caricata.
   * Consente di accedere a tutti i suggerimenti elencati.
   * Racconta i suggerimenti visualizzati per i campi Aggiungi indirizzo e-mail e Cerca.

## Documentazione accessibile {#accessible-docs}

[!DNL Experience Manager] fornisce una documentazione accessibile per l’utilizzo da parte di persone con disabilità. Di seguito è riportato come rendere accessibile per il momento l’offerta di contenuti, mentre Adobe continua a migliorare il modello e il contenuto:

* Gli assistenti vocali possono leggere il testo.
* Per le immagini e le illustrazioni è disponibile testo alternativo.
* La navigazione da tastiera è possibile.
* I rapporti di contrasto aiutano a evidenziare alcune parti del sito web della documentazione.

## Fornisci feedback {#a11y-feedback}

Per fornire un feedback, porre domande e richiedere miglioramenti al prodotto relativi all’accessibilità, utilizza i metodi seguenti:

* Compila il modulo in [www.adobe.com/accessibility/feedback.html](https://www.adobe.com/accessibility/feedback.html).
* Inviaci un&#39;e-mail all&#39;indirizzo access@adobe.com.

>[!MORELIKETHIS]
>
>* [Funzioni di accessibilità in [!DNL Dynamic Media]](/help/assets/accessibility-dm.md).
>* [Note sulla versione dei miglioramenti eseguiti in ogni versione del Service Pack](/help/release-notes/release-notes.md).
>* [[!DNL Adobe Experience Manager] guida all’accessibilità](/help/managing/web-accessibility.md).
>* [Relazioni di conformità (ACR) e elenco VPAT per soluzioni Adobi](https://www.adobe.com/accessibility/compliance.html).

