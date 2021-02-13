---
title: Accessibilità in [!DNL Experience Manager Assets]
description: Scopri in che modo le funzioni di accessibilità in [!DNL Adobe Experience Manager] 6.5 [!DNL Assets] aiutano gli utenti con disabilità.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 863d1bd3f0f188153fcbbb7256d3ac2e3b247f59
workflow-type: tm+mt
source-wordcount: '1919'
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

[!DNL Adobe Experience Manager] consente ai creatori e agli editori di contenuti di distribuire esperienze straordinarie sul Web.  Adobe si adopera per includere i creatori con disabilità migliorando l&#39;accessibilità di [!DNL Experience Manager]. Il software è continuamente migliorato per soddisfare le esigenze di tutti i tipi di utenti e aderire agli standard mondiali che includono individui con disabilità visive, uditive, di mobilità o di altro tipo.

[!DNL Experience Manager] pubblica informazioni sulla conformità che descrivono gli standard a cui aderisce, delineano le funzioni di accessibilità del prodotto e descrivono il livello di conformità. I rapporti sulla conformità dell&#39;accessibilità consentono agli [!DNL Experience Manager] utenti di comprendere il livello di conformità ai vari standard. I miglioramenti apportati in [!DNL Assets] consentono a tutti gli utenti di utilizzare facilmente le interfacce tramite tastiera, assistente vocale, lenti di ingrandimento e altre tecnologie di supporto.

[!DNL Experience Manager] fornisce diversi livelli di supporto per i seguenti standard:

* [Linee guida per l’accessibilità dei contenuti web (WCAG) 2.1](https://www.w3.org/TR/WCAG/).
* [Revisione della sezione 508 della legge](https://www.access-board.gov/guidelines-and-standards/communications-and-it/about-the-ict-refresh/final-rule/text-of-the-standards-and-guidelines) di riabilitazione.
* [Iniziativa di accessibilità - Accessible Rich Internet Applications (WAI-ARIA) di W3C](https://www.w3.org/WAI/standards-guidelines/aria/).
* [IT 301 549](https://en.wikipedia.org/wiki/EN_301_549).

Per leggere un rapporto con dettagli sul livello di conformità, vedere la pagina del rapporto sulla conformità dell&#39;accessibilità [report sulla conformità dell&#39;accessibilità](https://www.adobe.com/accessibility/compliance.html) (ACR).

Per sapere come [!DNL Dynamic Media] è accessibile, vedere [accessibilità in [!DNL Dynamic Media]](/help/assets/accessibility-dm.md).

## Tecnologie di assistenza {#at-support}

Gli utenti disabili spesso si affidano a hardware e software per accedere ai contenuti Web e utilizzare prodotti software. Questi strumenti sono noti come tecnologie di assistenza. [!DNL Experience Manager Assets] può essere utilizzato con i seguenti tipi di tecnologie di assistenza (AT) quando si utilizzano le funzionalità di base del software:

* Lettori dello schermo e lente di ingrandimento dello schermo.
* Software di riconoscimento vocale.
* Utilizzo della tastiera: navigazione e scelte rapide.
* Hardware di supporto, compresi i comandi di interruttore, display Braille aggiornabili e altri dispositivi di input per computer.
* Strumenti di ingrandimento dell’interfaccia utente.

## [!DNL Experience Manager Assets] casi di utilizzo accessibili  {#accessible-assets-use-cases}

In [!DNL Experience Manager], le funzioni di accessibilità soddisfano due requisiti chiave degli utenti [!DNL Experience Manager] e dei loro clienti.

* Per i designer e i creatori di contenuti, esistono funzioni per creare e pubblicare contenuti accessibili, che vengono utilizzate a loro volta dai clienti e dai visitatori del sito Web. Gli utenti disabili utilizzano i contenuti con l&#39;aiuto di tecnologie di assistenza. Per informazioni dettagliate, consultate [Web accessibility guidelines](/help/managing/web-accessibility.md).
* [!DNL Experience Manager] consente inoltre agli utenti e agli amministratori con disabilità di accedere all’interfaccia utente e ai controlli per creare e gestire il contenuto. I singoli disabili possono utilizzare tecnologie di assistenza per navigare, utilizzare e gestire la funzionalità [!DNL Assets].

Le funzioni di base di [!DNL Assets] sono più accessibili che in passato e vengono regolarmente aggiornate per migliorare la conformità agli standard globali. Le operazioni CRUD in [!DNL Assets] hanno un certo grado di accessibilità integrato in tali operazioni. Flussi di lavoro DAM come l&#39;aggiunta, la gestione, la ricerca e la distribuzione di risorse sono accessibili tramite scelte rapide da tastiera, testo dell&#39;assistente vocale, contrasto del colore e così via.

## Supporto per l&#39;uso della tastiera {#keyboard-use}

Molti elementi dell&#39;interfaccia utente cliccabili o utilizzabili con un puntatore possono essere utilizzati anche utilizzando la tastiera. Utilizzando una tastiera, gli utenti possono concentrarsi sugli elementi dell&#39;interfaccia utente e intervenire in modo appropriato. Gli utenti possono utilizzare direttamente le scelte rapide da tastiera per attivare un comando o un&#39;azione senza doversi concentrare sugli elementi dell&#39;interfaccia utente e attivarli utilizzando la tastiera. Ad esempio, gli utenti possono aprire la cronologia di una risorsa sul lato sinistro dell&#39;interfaccia utente accedendo al controllo dell&#39;interfaccia utente utilizzando una tastiera, selezionando `Return` e selezionando `Alt + 2` scelte rapide da tastiera.

<!-- TBD items:

* The option to toggle between list view and card view exposes relevant info to the screen readers. What about column view option? This info can go into ‘basic handling’ info aka article to ‘understand and use the workspace’.
* How to open and browse through the profile popup dialog in [!DNL Experience Manager] UI using a keyboard? The navigation does not match the order of visual display of options on the UI. This info can go into ‘basic handling’ info aka article to ‘understand and use the workspace’. What about setting preferences and impersonating a user?
* Using the [!DNL Experience Manager] tag browser and operating the options like delete tag? This info can go into ‘basic handling’ info aka article to ‘understand and use the workspace’.
* Read-only form fields can be focused with the keyboard. Can users tab to these fields to understand the contents and are they able to copy text from the fields?
-->

### Scelte rapide da tastiera in [!DNL Assets] {#keyboard-shortcuts}

Le seguenti azioni in [!DNL Assets] funzionano con le scelte rapide da tastiera elencate. La maggior parte delle scelte rapide da tastiera applicabili a [!DNL Experience Manager] Console si applica anche a [!DNL Assets]. Vedere [scelte rapide da tastiera per Console](/help/sites-authoring/keyboard-shortcuts.md#keyboard-shortcuts). Vedere come [abilitare o disabilitare le scelte rapide da tastiera](/help/sites-authoring/keyboard-shortcuts.md#deactivating-keyboard-shortcuts).

| Interfaccia utente o scenario | Scelte rapide da tastiera | Azione |
|---|---|---|
| Visualizzazione a colonne nell&#39;interfaccia utente [!DNL Assets] | Tasti freccia Su e Giù | Individuate i file e le cartelle all’interno della stessa gerarchia. |
| Visualizzazione a colonne nell&#39;interfaccia utente [!DNL Assets] | Tasti freccia destra e freccia sinistra | Spostatevi su file e cartelle sopra o sotto la cartella corrente. |
| Esplorazione delle cartelle in [!DNL Assets] | `/` | Richiamate la ricerca aprendo la casella di ricerca Omnisearch. |
| [!DNL Assets] Console | ` | Attiva/disattiva barre laterali |
| [!DNL Assets] Console | `Alt + 1` | Aprite la struttura del contenuto. |
| [!DNL Assets] Console | `Alt + 2` | Aprire la barra a sinistra [!UICONTROL Navigazione]. |
| [!DNL Assets] Console | `Alt + 3` | Visualizza [!UICONTROL Timeline] di una risorsa selezionata. |
| [!DNL Assets] Console | `Alt + 4` | Aprite i riferimenti Live Copy della risorsa selezionata. |
| [!DNL Assets] Console | `Alt + 5` | Avvia la ricerca e la ricerca all’interno della cartella selezionata. |
| Risorsa o cartella selezionata | Backspace | Elimina la risorsa o la cartella selezionata. |
| Risorsa o cartella selezionata | `p` | Aprite la pagina Proprietà della risorsa selezionata. |
| Risorsa o cartella selezionata | `e` | Modificate la risorsa selezionata. |
| Risorsa o cartella selezionata | `m` | Sposta la risorsa selezionata. |
| Risorsa o cartella selezionata | `Ctrl + c` | Copia la risorsa selezionata. |
| Risorsa o cartella selezionata | `Esc` | Deselezionate la selezione. |
| Si apre la finestra di dialogo ed è nello stato attivo | `Esc` | Chiudi, finestra di dialogo. |
| In una cartella in DAM | `Ctrl + v` | Incollate la risorsa copiata. |
| [!DNL Assets] Console | `Ctrl + A` | Selezionate tutte le risorse. |
| Pagine delle proprietà delle risorse | `Ctrl + S` | Salvare le modifiche. |
| [!DNL Assets] Console | `?` | Vedere un elenco delle scelte rapide da tastiera. |

## Accesso e navigazione [!DNL Assets] interfaccia utente {#login}

Gli utenti possono utilizzare la tastiera per navigare nel campo di accesso e compilarlo. I messaggi di errore a causa di combinazioni errate di nome utente e password nella pagina di login vengono annunciati dagli assistenti vocali ogni volta che si verifica l&#39;errore.

Dopo l&#39;accesso, gli utenti DAM possono spostarsi all&#39;interno dell&#39;interfaccia utente [!DNL Assets] utilizzando la tastiera. Gli elementi dell&#39;interfaccia utente, come la barra a sinistra, i menu, il profilo utente, la barra di ricerca, i file e le cartelle, nonché le impostazioni di amministrazione e configurazione, sono accessibili tramite tastiera. L&#39;ordine di navigazione della tastiera è da sinistra a destra e dall&#39;alto verso il basso. Quando si naviga utilizzando una tastiera, un&#39;opzione utilizzabile quando è attiva l&#39;evidenziazione viene evidenziata con un migliore contrasto di colore e narrata da un assistente vocale. Se appropriato, lo stato, ad esempio espanso, compresso e misto, delle opzioni di attivazione nel menu viene annunciato da un assistente vocale. Inoltre, l&#39;assistente vocale annuncia lo scopo dell&#39;opzione fruibile, invece di specificare l&#39;aspetto o il posizionamento dell&#39;interfaccia.

Se un utente espande l&#39;opzione di aiuto o profilo utente dal menu, l&#39;assistente vocale annuncia l&#39;opzione o lo stato appropriato. Se un utente espande l&#39;opzione del profilo utente, è possibile selezionare le opzioni disponibili utilizzando una tastiera. Ad esempio, un amministratore può rappresentare un altro utente. Se un utente cerca una stringa dall&#39;opzione [!UICONTROL Help], un narratore annuncia &quot;Searching Help&quot; per indicare che è in corso una ricerca.

<!-- TBD: Removing for now. Add a more informative video later. Host it on tv.adobe

![Keyboard navigation of top options in [!DNL Experience Manager] user interface](assets/keyboard-navigation-in-aem.gif)

*Figure: Navigating through the options at the top of [!DNL Experience Manager] user interface using `Tab` key.*
-->

## Sfogliare le risorse e visualizzare le relative informazioni {#browse}

Nell&#39;interfaccia utente di [!DNL Assets], gli utenti possono utilizzare la tastiera per sfogliare l&#39;elenco delle risorse digitali esistenti nell&#39;archivio DAM, visualizzare in anteprima o scaricare una risorsa, vedere le rappresentazioni generate, cambiare visualizzazione, visualizzare le rappresentazioni generate, vedere la cronologia della cronologia della cronologia e delle versioni, vedere commenti e riferimenti, nonché visualizzare e gestire i metadati.

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

* L&#39;assistente vocale annuncia alternative testuali che descrivono lo scopo o la funzionalità delle icone invece dei loro nomi.
* Gli utenti possono accedere alle opzioni dell&#39;interfaccia utente interattiva e attivarle nell&#39;elenco Riferimenti delle risorse utilizzando i tasti di tastiera.
* Gli elementi di ciascuna riga nella vista a elenco vengono annunciati come elementi della stessa riga dagli assistenti vocali.
* Durante la navigazione con il tasto `Tab`, l&#39;elemento attivo può passare all&#39;opzione di chiusura nell&#39;anteprima della versione.
* Quando si utilizza la tastiera per la ricerca, le opzioni evidenziate dell&#39;interfaccia utente attivabili hanno una messa a fuoco visiva più evidente e un contrasto migliore. Rende l&#39;area interessata più identificabile per l&#39;utente.
* L&#39;uso del tasto `Esc` per rimuovere le icone delle azioni rapide dalla visualizzazione delle miniature non rimuove lo stato attivo dall&#39;ultimo elemento attivo.
* Con una risorsa selezionata, selezionando `Alt + 4` la scelta rapida da tastiera si apre l&#39;elenco [!UICONTROL Riferimenti] nella barra a sinistra. Utilizzando il tasto `Tab`, gli utenti possono scorrere le voci di riferimento diverse da zero. Se si esplorano solo le voci di riferimento diverse da zero, si evitano sforzi e battute.
* I commenti su una risorsa sono disponibili nella timeline della risorsa. È accessibile se si accede alla barra a sinistra utilizzando una tastiera o una scelta rapida da tastiera.
* [!UICONTROL Visualizza ] impostazioni  [!DNL Experience Manager] sono accessibili tramite una tastiera. Gli utenti possono navigare tra le dimensioni di scheda disponibili utilizzando i tasti freccia e selezionare e spostarsi tra le varie schede per navigare tra gli altri elementi nella visualizzazione Impostazioni di visualizzazione esistente e impostarne altri.

<!-- TBD: Gradually, as more enhancements are done in these categories, add more content.

## Add and upload digital assets {#upload}

## Configure and administer [!DNL Assets] {#config-admin}

* List the a11y fixes in workflows to configure and administer [!DNL Experience Manager Assets]?
* Some enhancements in Processing profiles creation or application to a folder?
* Some enhancements to metadata properties UI?
-->

## Consente di gestire i contenuti digitali {#manage-assets}

Molte attività di gestione delle risorse, come le operazioni CRUD, il download di una risorsa, l’aggiunta di metadati, sono accessibili a diversi livelli. [!DNL Assets] consente di eseguire le attività utilizzando diverse tecnologie di assistenza, ad esempio un assistente vocale e una tastiera.

Guardate un video dimostrativo di come utilizzare una tastiera per [esplorare la directory archivio e scaricare una risorsa](https://youtu.be/K3dgqMRQJys).

Per le operazioni relative ai metadati solitamente eseguite da ruoli quali professionisti del marketing e amministratori, le seguenti funzioni migliorano l&#39;accessibilità:

* [!UICONTROL È ora possibile accedere all’opzione Salva e ] chiudi   nella pagina Proprietà risorsa mediante la tastiera.
* Gli assistenti vocali annunciano le opzioni per eliminare i tag selezionati nella scheda [!UICONTROL Base] della risorsa [!UICONTROL Proprietà].
* Gli utenti possono utilizzare la finestra di dialogo a comparsa del frontespizio con una tastiera. L&#39;elemento dell&#39;interfaccia utente Datepicker viene utilizzato per impostare tempi e tempi di attivazione e selezionare la data.
* La funzionalità di trascinamento mediante la tastiera funziona correttamente in [!UICONTROL Editor schema metadati] in modalità Sfoglia dell&#39;assistente vocale.
* Un utente può spostare lo stato attivo utilizzando la tastiera nel campo Aggiungi utente o gruppo in [!UICONTROL Gruppo utenti chiuso] nella scheda [!UICONTROL Autorizzazioni] della cartella [!UICONTROL Proprietà].

## Ricerca di risorse digitali {#search-assets}

Un’esperienza di ricerca delle risorse rapida e senza soluzione di continuità aumenta la velocità del contenuto. I casi di utilizzo della velocità del contenuto fanno parte della funzionalità [!DNL Assets] di base. Per avviare una ricerca dalla barra di ricerca Omnisearch, gli utenti possono utilizzare la scelta rapida da tastiera `/` o `Tab` insieme agli assistenti vocali per individuare rapidamente l&#39;opzione di ricerca. L&#39;assistente vocale narra il nome dell&#39;opzione come &quot;Pulsante di ricerca&quot; quando è attivo sull&#39;opzione di ricerca ![opzione di ricerca](assets/do-not-localize/search_icon.png). Gli utenti possono selezionare `Return` per aprire la casella corrispondente. L&#39;assistente vocale narra non solo la parola chiave digitata nella casella di ricerca, ma anche i suggerimenti offerti da [!DNL Experience Manager Assets]. Gli utenti possono utilizzare una combinazione di tasti freccia, `Return` e `Tab` per accedere alle varie opzioni per attivare una ricerca.

La funzionalità di ricerca è resa accessibile dalle seguenti funzionalità:

* Il titolo della pagina, disponibile per l’assistente vocale, consente di identificare la pagina come pagina di ricerca delle risorse.
* Gli utenti cercano le risorse direttamente dal campo di ricerca Omnico. Gli utenti possono aprirlo utilizzando la navigazione tramite tastiera o la scelta rapida da tastiera `/`.
* Gli utenti possono iniziare a digitare la parola chiave di ricerca e quindi selezionare i suggerimenti automatici utilizzando i tasti freccia. Potete selezionare i suggerimenti evidenziati utilizzando la chiave `Return` e cercare i suggerimenti selezionati nelle risorse.
* Gli assistenti vocali possono identificare e annunciare le caselle di controllo a stato misto (in cui, a meno che non si selezionino tutti i predicati nidificati, le caselle di controllo di primo livello non vengono selezionate e vengono evidenziate) nel pannello Filtri quando si filtrano i risultati della ricerca.
* Lo stato attivo si sposta alle opzioni di ricerca dopo la chiusura della casella di ricerca Omnico.

Quando filtrate i risultati della ricerca:

* La pagina dei risultati della ricerca ha un titolo informativo per una migliore comprensione degli utenti degli assistenti vocali.
* Un assistente vocale annuncia le opzioni del filtro di ricerca come pulsanti di scelta espandibili.
* I predicati con opzioni con più stati vengono annunciati dagli assistenti vocali.

## Condividere le risorse {#share-assets}

<!-- TBD: Anything about accessibility in DA, BP? AAL team confirmed that there's no content for AAL a11y on helpx.
-->

Quando condividete le risorse, le seguenti funzionalità migliorano l&#39;accessibilità:

* Un utente può spostare lo stato attivo utilizzando la tastiera nel campo Cerca e Aggiungi indirizzo e-mail della finestra di dialogo di condivisione dei collegamenti.

* Nella finestra di dialogo di condivisione dei collegamenti, quando si naviga in modalità Sfoglia, gli assistenti vocali,

   * Non raccontare le informazioni della tabella al caricamento della finestra di dialogo.
   * Potete passare a tutti i suggerimenti elencati.
   * Narrate i suggerimenti visualizzati per Aggiungi indirizzo e-mail e campi di ricerca.

## Documentazione accessibile {#accessible-docs}

[!DNL Experience Manager] fornisce documentazione accessibile da utilizzare per le persone con disabilità. Di seguito sono riportati alcuni elementi utili per rendere accessibile al momento l’offerta di contenuti, mentre  Adobe continua a migliorare il modello e il contenuto:

* Gli assistenti vocali possono leggere il testo.
* Le immagini e le illustrazioni dispongono di testo alternativo.
* La navigazione tramite tastiera è possibile.
* I rapporti di contrasto consentono di evidenziare alcune parti del sito Web della documentazione.

## Fornire feedback {#a11y-feedback}

Per fornire feedback, porre domande e richiedere miglioramenti ai prodotti, relativi all&#39;accessibilità, utilizzate i seguenti metodi:

* Compila il modulo all&#39;indirizzo [www.adobe.com/accessibility/feedback.html](https://www.adobe.com/accessibility/feedback.html).
* Inviateci un&#39;e-mail all&#39;indirizzo access@adobe.com.

>[!MORELIKETHIS]
>
>* [Funzioni di accessibilità in [!DNL Dynamic Media]](/help/assets/accessibility-dm.md).
>* [Note sulla versione dei miglioramenti effettuati in ciascuna versione](/help/release-notes/new-features-latest-service-pack.md) di Service Pack.
>* [[!DNL Adobe Experience Manager] guida](/help/managing/web-accessibility.md) all&#39;accessibilità.
>* [Relazioni di conformità (ACR) ed elenco VPAT per le soluzioni](https://www.adobe.com/accessibility/compliance.html)  Adobe.

