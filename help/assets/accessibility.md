---
title: Funzioni e interfacce accessibili di [!DNL Experience Manager Assets]
description: Scopri in che modo le funzioni di accessibilità in [!DNL Adobe Experience Manager] 6.5 [!DNL Assets] aiutano gli utenti con disabilità.
contentOwner: AG
feature: Gestione risorse
role: User, Architect, Leader
exl-id: 15555941-99a2-4586-8d7b-b22f3ec17805
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '1926'
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

[!DNL Adobe Experience Manager] consente ai creatori e agli editori di contenuti di offrire esperienze straordinarie sul web. Adobe si impegna a includere i creatori con disabilità migliorando l&#39;accessibilità di [!DNL Experience Manager]. Il software viene continuamente migliorato per soddisfare le esigenze di tutti i tipi di utenti e aderire agli standard mondiali che includono persone con disabilità visive, uditive, di mobilità o di altro tipo.

[!DNL Experience Manager] pubblica informazioni sulla conformità che descrivono gli standard a cui aderisce, ne descrivono le funzioni di accessibilità del prodotto e descrivono il livello di conformità. I rapporti sulla conformità per l’accessibilità consentono agli utenti di [!DNL Experience Manager] di comprendere il livello di aderenza ai vari standard. I miglioramenti apportati in [!DNL Assets] consentono a tutti gli utenti di utilizzare le interfacce facilmente tramite tastiera, assistenti vocali, lenti di ingrandimento e altre tecnologie per l’accessibilità.

[!DNL Experience Manager] fornisce diversi livelli di sostegno per i seguenti standard:

* [Linee guida per l’accessibilità dei contenuti web (WCAG) 2.1](https://www.w3.org/TR/WCAG/).
* [Revisione della sezione 508 della legge](https://www.access-board.gov/guidelines-and-standards/communications-and-it/about-the-ict-refresh/final-rule/text-of-the-standards-and-guidelines) sulla riabilitazione.
* [Iniziativa per l’accessibilità - Accessible Rich Internet Applications (WAI-ARIA) di W3C](https://www.w3.org/WAI/standards-guidelines/aria/).
* [IT 301 549](https://en.wikipedia.org/wiki/EN_301_549).

Per leggere un rapporto con dettagli sul livello di conformità, consulta la pagina [Rapporto sulla conformità per l’accessibilità](https://www.adobe.com/accessibility/compliance.html) (ACR) .

Per informazioni sull’accessibilità di [!DNL Dynamic Media], consulta [in [!DNL Dynamic Media]](/help/assets/accessibility-dm.md) .

## Tecnologie di assistenza {#at-support}

Gli utenti disabili spesso si affidano a hardware e software per accedere ai contenuti web e utilizzare prodotti software. Questi strumenti sono noti come tecnologie per l’accessibilità. [!DNL Experience Manager Assets] può utilizzare i seguenti tipi di tecnologie per l’accessibilità (AT) quando si utilizzano le funzionalità di base del software:

* Lettori dello schermo e lente di ingrandimento dello schermo.
* Software di riconoscimento vocale.
* Utilizzo della tastiera: navigazione e scelte rapide.
* Hardware di supporto, compresi i comandi di switch, display Braille aggiornabili e altri dispositivi di input del computer.
* Strumenti di ingrandimento dell’interfaccia utente.

## [!DNL Experience Manager Assets] casi d’uso accessibili {#accessible-assets-use-cases}

In [!DNL Experience Manager], le funzioni di accessibilità soddisfano due requisiti chiave degli utenti [!DNL Experience Manager] e dei loro clienti.

* Per i designer e i creatori di contenuti, sono disponibili funzioni per creare e pubblicare contenuti accessibili che vengono a loro volta utilizzati dai loro clienti e visitatori del sito web. Gli utenti disabili utilizzano i contenuti con l’aiuto di tecnologie per l’accessibilità. Per informazioni dettagliate, consulta [linee guida per l’accessibilità web](/help/managing/web-accessibility.md).
* [!DNL Experience Manager] consente inoltre agli utenti e agli amministratori con disabilità di accedere all’interfaccia utente e ai controlli per creare e gestire i contenuti. L’utente con disabilità può utilizzare tecnologie per l’accessibilità per navigare, utilizzare e gestire la funzionalità [!DNL Assets] .

Le funzioni di base di [!DNL Assets] sono più accessibili che in passato e vengono regolarmente aggiornate per migliorare la conformità agli standard globali. Le operazioni CRUD in [!DNL Assets] hanno un certo grado di accessibilità integrato in quelle. I flussi di lavoro DAM come l’aggiunta, la gestione, la ricerca e la distribuzione delle risorse sono accessibili tramite scelte rapide da tastiera, testo per assistenti vocali, contrasto del colore e così via.

## Supporto per l’uso della tastiera {#keyboard-use}

È inoltre possibile utilizzare la tastiera per utilizzare molti elementi dell’interfaccia utente cliccabili o utilizzabili con un puntatore. Utilizzando una tastiera, gli utenti possono concentrarsi sugli elementi dell’interfaccia utente e intraprendere un’azione appropriata. Gli utenti possono utilizzare direttamente le scelte rapide da tastiera per attivare un comando o un’azione senza doversi concentrare sugli elementi dell’interfaccia utente e attivarli utilizzando la tastiera. Ad esempio, gli utenti possono aprire la timeline di una risorsa sul lato sinistro dell’interfaccia utente accedendo al controllo dell’interfaccia utente tramite tastiera, selezionando `Return` e selezionando `Alt + 2` scelte rapide da tastiera.

<!-- TBD items:

* The option to toggle between list view and card view exposes relevant info to the screen readers. What about column view option? This info can go into ‘basic handling’ info aka article to ‘understand and use the workspace’.
* How to open and browse through the profile popup dialog in [!DNL Experience Manager] UI using a keyboard? The navigation does not match the order of visual display of options on the UI. This info can go into ‘basic handling’ info aka article to ‘understand and use the workspace’. What about setting preferences and impersonating a user?
* Using the [!DNL Experience Manager] tag browser and operating the options like delete tag? This info can go into ‘basic handling’ info aka article to ‘understand and use the workspace’.
* Read-only form fields can be focused with the keyboard. Can users tab to these fields to understand the contents and are they able to copy text from the fields?
-->

### Scelte rapide da tastiera in [!DNL Assets] {#keyboard-shortcuts}

Le azioni seguenti in [!DNL Assets] funzionano con le scelte rapide da tastiera elencate. La maggior parte delle scelte rapide da tastiera applicabili alle [!DNL Experience Manager] console si applica anche a [!DNL Assets]. Consultare [scelte rapide da tastiera per Console](/help/sites-authoring/keyboard-shortcuts.md#keyboard-shortcuts). Scopri come [abilitare o disabilitare le scelte rapide da tastiera](/help/sites-authoring/keyboard-shortcuts.md#deactivating-keyboard-shortcuts).

| Interfaccia utente o scenario | Scelta rapida da tastiera | Azione |
|---|---|---|
| Vista a colonne nell’interfaccia utente di [!DNL Assets] | Tasti freccia Su e Giù | Passa a file e cartelle all’interno della stessa gerarchia. |
| Vista a colonne nell’interfaccia utente di [!DNL Assets] | Tasti freccia sinistra e destra | Passa a file e cartelle sopra o sotto la cartella corrente. |
| Esplorazione delle cartelle in [!DNL Assets] | `/` | Richiama la ricerca aprendo la casella Omnisearch. |
| [!DNL Assets] Console | &amp;grave; | Attiva/disattiva barre laterali |
| [!DNL Assets] Console | `Alt + 1` | Apri la struttura del contenuto. |
| [!DNL Assets] Console | `Alt + 2` | Apri la barra a sinistra [!UICONTROL Navigazione]. |
| [!DNL Assets] Console | `Alt + 3` | Visualizza [!UICONTROL Timeline] di una risorsa selezionata. |
| [!DNL Assets] Console | `Alt + 4` | Apri i riferimenti Live Copy della risorsa selezionata. |
| [!DNL Assets] Console | `Alt + 5` | Avvia la ricerca e la ricerca all’interno della cartella selezionata. |
| Risorsa o cartella selezionata | Backspace | Elimina la risorsa o la cartella selezionata. |
| Risorsa o cartella selezionata | `p` | Apri la pagina Proprietà della risorsa selezionata. |
| Risorsa o cartella selezionata | `e` | Modifica la risorsa selezionata. |
| Risorsa o cartella selezionata | `m` | Sposta la risorsa selezionata. |
| Risorsa o cartella selezionata | `Ctrl + c` | Copia la risorsa selezionata. |
| Risorsa o cartella selezionata | `Esc` | Annulla la selezione. |
| Viene visualizzata la finestra di dialogo ed è nello stato attivo | `Esc` | Finestra di dialogo Chiudi. |
| All’interno di una cartella in DAM | `Ctrl + v` | Incolla la risorsa copiata. |
| [!DNL Assets] Console | `Ctrl + A` | Seleziona tutte le risorse. |
| Pagine delle proprietà delle risorse | `Ctrl + S` | Salva le modifiche. |
| [!DNL Assets] Console | `?` | Elenco delle scelte rapide da tastiera disponibili. |

## Accesso e navigazione [!DNL Assets] interfaccia utente {#login}

Gli utenti possono utilizzare la tastiera per accedere al campo di accesso e compilarlo. I messaggi di errore dovuti a combinazioni errate di nome utente e password nella pagina di accesso vengono annunciati dagli assistenti vocali ogni volta che si verifica l’errore.

Dopo l’accesso, gli utenti DAM possono navigare all’interno dell’ interfaccia utente [!DNL Assets] utilizzando la tastiera. Gli elementi dell’interfaccia utente, come la barra a sinistra, i menu, il profilo utente, la barra di ricerca, i file e le cartelle e le impostazioni di amministrazione e configurazione, sono navigabili tramite tastiera. L’ordine di navigazione da sinistra a destra e dall’alto verso il basso. Quando si naviga utilizzando una tastiera, un’opzione utilizzabile quando è attiva la tastiera viene evidenziata con un contrasto di colore migliore e viene narrata da un assistente vocale. Se appropriato, lo stato, ad esempio espanso, compresso e misto, delle opzioni di messa a fuoco nel menu viene annunciato da un assistente vocale. Inoltre, l’assistente vocale annuncia lo scopo dell’opzione utilizzabile, anziché specificare l’aspetto o il posizionamento dell’interfaccia.

Se un utente espande la guida o l’opzione di profilo utente dal menu, l’assistente vocale annuncia l’opzione o lo stato appropriato. Se un utente espande l’opzione di profilo utente, le opzioni disponibili possono essere selezionate utilizzando una tastiera. Ad esempio, un amministratore può rappresentare un utente diverso. Se un utente cerca una stringa dall&#39;opzione [!UICONTROL Help], un narratore annuncia &quot;Searching Help&quot; per indicare che è in corso una ricerca.

<!-- TBD: Removing for now. Add a more informative video later. Host it on tv.adobe

![Keyboard navigation of top options in [!DNL Experience Manager] user interface](assets/keyboard-navigation-in-aem.gif)

*Figure: Navigating through the options at the top of [!DNL Experience Manager] user interface using `Tab` key.*
-->

## Sfoglia le risorse e visualizza le relative informazioni {#browse}

Nell’interfaccia utente di [!DNL Assets], gli utenti possono utilizzare la tastiera per sfogliare l’elenco delle risorse digitali esistenti nell’archivio DAM, visualizzare in anteprima o scaricare una risorsa, vedere le rappresentazioni generate, cambiare visualizzazione, vedere la cronologia della timeline e della versione, vedere commenti e riferimenti e visualizzare e gestire i metadati.

<!-- TBD: Not sure about the following list items mean:

In [!DNL Experience Manager] header section, when navigating in browse mode, screen reader now announces,
  
  * Suggestions to search in Omnisearch.
  * The state as expanded or collapsed for Solutions, Help, Inbox and User options.
  * The Searching Help status message that is displayed when user enters a search string in Search for Help field under Help option
  * The error message if incorrect value is entered in Impersonate as field under User option and focus correctly moves to the text field (NPR-33804).

Review CQ-4282133 before adding - Close option in a coral-dialog wasn't accessible through keyboard, due to which user cannot trigger close option through keyboard press in version preview dialog. After fix, user can close dialog through close option using keyboard.

* CQ-4273122 - Assets of video/audio type will have aria-label in format "Multimedia player: <Title>" so users relying on screen-reader will get to know that they are video/audio assets.
-->

Quando esplori l’archivio delle risorse, le seguenti funzionalità migliorano l’accessibilità:

* L’assistente vocale annuncia alternative testuali che illustrano lo scopo o la funzionalità delle icone invece dei loro nomi.
* Gli utenti possono accedere e attivare le opzioni dell’interfaccia utente interattiva nell’elenco Riferimenti delle risorse utilizzando i tasti di tastiera.
* Gli elementi di ogni riga nella vista a elenco vengono annunciati come elementi della stessa riga dagli assistenti vocali.
* Durante la navigazione con il tasto `Tab`, l&#39;opzione di chiusura può essere spostata nell&#39;anteprima della versione.
* Quando si utilizza la tastiera per sfogliare, le opzioni dell’interfaccia utente actionable evidenziate hanno una messa a fuoco visiva più evidente con un contrasto maggiore. Rende l&#39;area mirata più identificabile per l&#39;utente.
* L&#39;utilizzo del tasto `Esc` per rimuovere le icone delle azioni rapide dalla visualizzazione miniatura non rimuove lo stato attivo dall&#39;ultimo elemento attivo.
* Con una risorsa selezionata, selezionando `Alt + 4` scelte rapide da tastiera si apre l’elenco [!UICONTROL Riferimenti] nella barra a sinistra. Utilizzando la chiave `Tab`, gli utenti possono navigare tra le voci di riferimento diverse da zero. La navigazione solo attraverso le voci di riferimento diverse da zero consente di risparmiare fatica e tasti.
* I commenti su una risorsa sono disponibili nella timeline della risorsa. È accessibile se si accede alla barra a sinistra utilizzando una tastiera o una scelta rapida da tastiera.
* [!UICONTROL Le ] impostazioni di visualizzazione  [!DNL Experience Manager] sono accessibili da tastiera. Gli utenti possono navigare tra le dimensioni delle schede disponibili utilizzando i tasti freccia, quindi selezionare e spostarsi tra le varie dimensioni per navigare tra i vari elementi nella vista Impostazioni visualizzazione esistente e impostarne altri.

<!-- TBD: Gradually, as more enhancements are done in these categories, add more content.

## Add and upload digital assets {#upload}

## Configure and administer [!DNL Assets] {#config-admin}

* List the a11y fixes in workflows to configure and administer [!DNL Experience Manager Assets]?
* Some enhancements in Processing profiles creation or application to a folder?
* Some enhancements to metadata properties UI?
-->

## Consente di gestire i contenuti digitali {#manage-assets}

Molte attività di gestione delle risorse, come le operazioni CRUD, il download di una risorsa, l’aggiunta di metadati, sono accessibili a diversi gradi. [!DNL Assets] consente di eseguire le attività utilizzando diverse tecnologie per l’accessibilità, ad esempio un assistente vocale e una tastiera.

Guarda un video dimostrativo dell’utilizzo di una tastiera per [sfogliare l’archivio e scaricare una risorsa](https://youtu.be/K3dgqMRQJys).

Per le operazioni con i metadati solitamente eseguite da ruoli come addetti al marketing e amministratori, le seguenti funzioni migliorano l’accessibilità:

* [!UICONTROL È ora possibile accedere da tastiera all’opzione Salva e ] chiudi   nella pagina Proprietà risorsa.
* Gli assistenti vocali annunciano le opzioni per eliminare i tag selezionati nella scheda [!UICONTROL Base] della risorsa [!UICONTROL Proprietà].
* Gli utenti possono utilizzare la finestra di dialogo a comparsa relativa al datepicker con una tastiera. L’elemento dell’interfaccia utente Datepicker viene utilizzato per impostare i tempi di attivazione e disattivazione e selezionare la data.
* La funzionalità di trascinamento tramite tastiera funziona correttamente in [!UICONTROL Editor schema metadati] in modalità Sfoglia dell’assistente vocale.
* Un utente può spostare lo stato attivo utilizzando la tastiera nel campo Aggiungi utente o gruppo in [!UICONTROL Gruppo utenti chiuso] nella scheda [!UICONTROL Autorizzazioni] della cartella [!UICONTROL Proprietà].

## Cercare risorse digitali {#search-assets}

Un’esperienza di ricerca delle risorse rapida e senza soluzione di continuità aumenta la velocità dei contenuti. I casi di utilizzo della velocità dei contenuti fanno parte della funzionalità di base [!DNL Assets] . Per avviare una ricerca dalla barra della ricerca Omnisearch, gli utenti possono utilizzare le scelte rapide da tastiera `/` o `Tab` insieme agli assistenti vocali per individuare rapidamente l’opzione di ricerca. L&#39;assistente vocale legge il nome dell&#39;opzione come &quot;Pulsante di ricerca&quot; quando lo stato attivo è sull&#39;opzione di ricerca ![opzione di ricerca](assets/do-not-localize/search_icon.png). Gli utenti possono selezionare `Return` per aprire la casella Omnisearch. L’assistente vocale non solo narra la parola chiave digitata nella casella di ricerca, ma anche i suggerimenti offerti da [!DNL Experience Manager Assets]. Gli utenti possono utilizzare una combinazione di tasti freccia, `Return` e `Tab` per accedere alle varie opzioni per attivare una ricerca.

La funzionalità di ricerca è resa accessibile dalle seguenti funzionalità:

* Il titolo della pagina, disponibile per un assistente vocale, consente di identificare la pagina come pagina di ricerca delle risorse.
* Gli utenti ricercano le risorse all’interno del campo Omnisearch . Gli utenti possono aprirlo utilizzando la navigazione da tastiera o la scelta rapida da tastiera `/`.
* Gli utenti possono iniziare a digitare la parola chiave di ricerca e quindi selezionare i suggerimenti automatici utilizzando i tasti freccia. Puoi selezionare i suggerimenti evidenziati utilizzando la chiave `Return` e cercare le risorse per i suggerimenti selezionati.
* Gli assistenti vocali possono identificare e annunciare le caselle di controllo a stato misto (in cui, a meno che tu non selezioni tutti i predicati nidificati, le caselle di controllo di primo livello non sono selezionate e sono evidenziate) nel pannello Filtri quando filtri i risultati della ricerca.
* Lo stato attivo si sposta alle opzioni di ricerca dopo la chiusura della casella Omnisearch.

Quando si filtrano i risultati della ricerca:

* La pagina dei risultati della ricerca ha un titolo informativo che consente di comprendere meglio gli utenti degli assistenti vocali.
* Un assistente vocale annuncia le opzioni nel filtro di ricerca come pannello a soffietto espandibile.
* I predicati con opzioni a stato misto vengono annunciati dagli assistenti vocali.

## Condividere le risorse {#share-assets}

<!-- TBD: Anything about accessibility in DA, BP? AAL team confirmed that there's no content for AAL a11y on helpx.
-->

Quando condividi le risorse, le seguenti funzionalità migliorano l’accessibilità:

* Un utente può spostare lo stato attivo utilizzando la tastiera all’interno del campo Cerca e aggiungi indirizzo e-mail nella finestra di dialogo di condivisione del collegamento.

* Nella finestra di dialogo di condivisione dei collegamenti, quando si naviga in modalità Sfoglia, gli assistenti vocali,

   * Non annotare le informazioni della tabella quando la finestra di dialogo viene caricata.
   * Puoi accedere a tutti i suggerimenti elencati.
   * Segnala i suggerimenti visualizzati per i campi Aggiungi indirizzo e-mail e Ricerca .

## Documentazione accessibile {#accessible-docs}

[!DNL Experience Manager] fornisce la documentazione accessibile da utilizzare per le persone con disabilità. I seguenti elementi contribuiscono a rendere accessibile per il momento l’offerta di contenuti, mentre l’Adobe continua a migliorare il modello e il contenuto:

* Il testo può essere letto dagli assistenti vocali.
* Per le immagini e le illustrazioni è disponibile il testo alt.
* È possibile navigare tramite tastiera.
* I rapporti di contrasto consentono di evidenziare alcune parti del sito web della documentazione.

## Fornire feedback {#a11y-feedback}

Per fornire feedback, porre domande e richiedere miglioramenti ai prodotti, relativi all’accessibilità, utilizza i seguenti metodi:

* Compila il modulo all&#39;indirizzo [www.adobe.com/accessibility/feedback.html](https://www.adobe.com/accessibility/feedback.html).
* Inviaci un’e-mail all’indirizzo access@adobe.com.

>[!MORELIKETHIS]
>
>* [Funzioni di accessibilità in [!DNL Dynamic Media]](/help/assets/accessibility-dm.md).
>* [Note sulla versione dei miglioramenti effettuati in ogni versione](/help/release-notes/new-features-latest-service-pack.md) del Service Pack.
>* [[!DNL Adobe Experience Manager] guida all’accessibilità](/help/managing/web-accessibility.md).
>* [Elenco dei rapporti di conformità (ACR) e VPAT per le soluzioni](https://www.adobe.com/accessibility/compliance.html) di Adobe.

