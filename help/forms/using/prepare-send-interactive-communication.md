---
title: Preparazione e invio di comunicazioni interattive tramite l'interfaccia utente dell'agente
seo-title: Preparazione e invio di comunicazioni interattive tramite l'interfaccia utente dell'agente
description: L'interfaccia utente dell'agente consente agli agenti di preparare e inviare la comunicazione interattiva al processo di post. L'agente apporta le modifiche necessarie secondo quanto consentito e invia la comunicazione interattiva a un processo di pubblicazione, ad esempio e-mail o stampa.
seo-description: Preparazione e invio di comunicazioni interattive tramite l'interfaccia utente dell'agente
uuid: d1a19b83-f630-4648-9ad2-a22374e31aa9
topic-tags: interactive-communications
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 110c86ea-9bd8-4018-bfcc-ca33e6b3f3ba
translation-type: tm+mt
source-git-commit: 4c4a5a15e9cbb5cc22bc5999fb40f1d6db3bb091
workflow-type: tm+mt
source-wordcount: '1641'
ht-degree: 0%

---


# Preparazione e invio di comunicazioni interattive tramite l&#39;interfaccia utente dell&#39;agente {#prepare-and-send-interactive-communication-using-the-agent-ui}

L&#39;interfaccia utente dell&#39;agente consente agli agenti di preparare e inviare la comunicazione interattiva al processo di post. L&#39;agente apporta le modifiche necessarie secondo quanto consentito e invia la comunicazione interattiva a un processo di pubblicazione, ad esempio e-mail o stampa.

## Panoramica {#overview}

Dopo aver creato una comunicazione interattiva, l&#39;agente può aprire la comunicazione interattiva nell&#39;interfaccia utente dell&#39;agente e preparare una copia specifica per il destinatario immettendo i dati e gestendo il contenuto e gli allegati. Infine, l&#39;agente può inviare la comunicazione interattiva a un processo di post.

Durante la preparazione della comunicazione interattiva tramite l&#39;interfaccia utente dell&#39;agente, l&#39;agente gestisce i seguenti aspetti della comunicazione interattiva nell&#39;interfaccia utente dell&#39;agente prima di inviarla a un processo di post:

* **Dati**: Nella scheda Dati dell&#39;interfaccia utente dell&#39;agente vengono visualizzate tutte le variabili modificabili dall&#39;agente e le proprietà del modello di dati del modulo sbloccato nella comunicazione interattiva. Queste variabili/proprietà vengono create durante la modifica o la creazione di frammenti di documento inclusi nella comunicazione interattiva. La scheda Dati include anche tutti i campi creati nel modello XDP/canale di stampa. La scheda Dati viene visualizzata solo quando sono presenti variabili, proprietà del modello dati del modulo o campi nella comunicazione interattiva modificabili dall&#39;agente.
* **Contenuto**: Nella scheda Contenuto, l&#39;agente gestisce il contenuto, ad esempio frammenti di documento e variabili di contenuto, nella comunicazione interattiva. Durante la creazione della comunicazione interattiva nelle proprietà di tali frammenti di documento, l&#39;agente può apportare le modifiche desiderate nel frammento di documento. L&#39;agente può inoltre riordinare, aggiungere o rimuovere un frammento di documento e aggiungere interruzioni di pagina, se consentito.
* **Allegati**: La scheda Allegati viene visualizzata nell’interfaccia utente dell’agente solo se la comunicazione interattiva contiene degli allegati o se l’agente dispone dell’accesso alla libreria. L&#39;agente può o non può essere autorizzato a modificare gli allegati.

## Preparazione della comunicazione interattiva tramite l’interfaccia utente dell’agente {#prepare-interactive-communication-using-the-agent-ui}

1. Selezionare **[!UICONTROL Moduli]** > **[!UICONTROL Moduli e documenti]**.
1. Selezionate la comunicazione interattiva appropriata e toccate **[!UICONTROL Apri interfaccia utente]** agente.

   >[!NOTE]
   >
   >L’interfaccia utente dell’agente funziona solo se la comunicazione interattiva selezionata dispone di un canale di stampa.

   ![openagentiui](assets/openagentiui.png)

   In base al contenuto e alle proprietà della comunicazione interattiva, l&#39;interfaccia utente dell&#39;agente viene visualizzata con le seguenti tre schede: Dati, contenuti e allegati.

   ![agentuitabo](assets/agentuitabs.png)

   Immettete i dati, gestite il contenuto e gestite gli allegati.

### Inserisci dati {#enter-data}

1. Nella scheda Dati, immettere i dati per le variabili, le proprietà del modello dati del modulo e i campi del modello di stampa (XDP), a seconda delle necessità. Compila tutti i campi obbligatori contrassegnati da un asterisco (&amp;ast;) per abilitare il pulsante **Invia** .

   Toccate il valore di un campo dati nell’anteprima della comunicazione interattiva per evidenziare il campo dati corrispondente nella scheda Dati o viceversa.

### Gestione contenuto {#manage-content}

Nella scheda Contenuto, gestite il contenuto, ad esempio frammenti di documento e variabili di contenuto, nella comunicazione interattiva.

1. Select **[!UICONTROL Content]**. Viene visualizzata la scheda del contenuto della comunicazione interattiva.

   ![agentuicontenttab](assets/agentuicontenttab.png)

1. Modificare i frammenti di documento, come necessario, nella scheda Contenuto. Per attivare il frammento rilevante nella gerarchia dei contenuti, è possibile toccare la riga o il paragrafo corrispondente nell&#39;anteprima della comunicazione interattiva oppure toccare il frammento direttamente nella gerarchia Contenuto.

   Ad esempio, il frammento di documento con la riga &quot;Effettuare un pagamento online ora... &quot; è selezionato nell&#39;anteprima nell&#39;immagine seguente e lo stesso frammento di documento è stato selezionato nella scheda Contenuto.

   ![contentmodulefocus](assets/contentmodulefocus.png)

   Nella scheda Contenuto o Dati, toccando Evidenzia moduli selezionati nel contenuto ( ![evidenziato modulesincontentccr](assets/highlightselectedmodulesincontentccr.png)) in alto a sinistra dell&#39;anteprima, è possibile disattivare o abilitare la funzionalità per passare al frammento di documento quando testo, paragrafo o campo di dati pertinenti vengono toccati o selezionati nell&#39;anteprima.

   I frammenti che possono essere modificati dall’agente durante la creazione della comunicazione interattiva sono contrassegnati dall’icona Modifica contenuto selezionato ( ![iconeditedselect content](assets/iconeditselectedcontent.png)). Toccate l’icona Modifica contenuto selezionato per avviare il frammento in modalità di modifica e apportare le modifiche necessarie. Utilizzate le seguenti opzioni per formattare e gestire il testo:

   * [Opzioni di formattazione](#formattingtext)

      * [Copia e incolla testo formattato da altre applicazioni](#pasteformattedtext)
      * [Evidenziare parti di testo](#highlightemphasize)
   * [Caratteri speciali](#specialcharacters)
   * [Scelte rapide da tastiera](/help/forms/using/keyboard-shortcuts.md)

   Per ulteriori informazioni sulle azioni disponibili per vari frammenti di documento nell&#39;interfaccia utente di Agent, vedere [Azioni e informazioni disponibili nell&#39;interfaccia](#actionsagentui)utente di Agent.

1. Per aggiungere un&#39;interruzione di pagina all&#39;output di stampa della comunicazione interattiva, posizionare il cursore nel punto in cui si desidera inserire un&#39;interruzione di pagina e selezionare Interruzione di pagina prima o Interruzione di pagina dopo ( ![interruzione di pagina prima](assets/pagebreakbeforeafter.png)).

   Nella comunicazione interattiva viene inserito un segnaposto per interruzione di pagina esplicito. Per vedere in che modo un&#39;interruzione di pagina esplicita influisce sulla comunicazione interattiva, consultate l&#39;anteprima di stampa.

   ![esplicitpagebreak](assets/explicitpagebreak.png)

   Continuate a gestire gli allegati della comunicazione interattiva.

### Gestione allegati {#manage-attachments}

1. Selezionare **[!UICONTROL Allegato]**. L&#39;interfaccia utente dell&#39;agente visualizza gli allegati disponibili come configurati durante la creazione della comunicazione interattiva.

   È possibile scegliere di non inviare un allegato insieme alla comunicazione interattiva toccando l&#39;icona della vista e toccando la croce nell&#39;allegato per eliminarlo (se l&#39;agente può eliminare o nascondere l&#39;allegato) dalla comunicazione interattiva. Per gli allegati specificati come obbligatori durante la creazione della comunicazione interattiva, le icone Visualizza ed Elimina sono disattivate.

   ![Attachmentsagentui](assets/attachmentsagentui.png)

1. Toccate l&#39;icona Accesso ![libreria (accesso](assets/libraryaccess.png)libreria) per accedere alla libreria Contenuto per inserire risorse DAM come allegati.

   >[!NOTE]
   >
   >L&#39;icona Accesso libreria è disponibile solo se l&#39;accesso alla libreria è stato abilitato durante la creazione della comunicazione interattiva (nelle proprietà Contenitore documento del canale Stampa).

1. Se l&#39;ordine degli allegati non era bloccato durante la creazione della comunicazione interattiva, è possibile riordinare gli allegati selezionando un allegato e toccando le frecce verso il basso e verso l&#39;alto.
1. Utilizzate Anteprima Web e Anteprima di stampa per verificare se le due uscite sono conformi alle vostre esigenze.

   Se ritenete che le anteprime siano soddisfacenti, toccate **[!UICONTROL Invia]** per inviare/inviare la comunicazione interattiva a un processo di pubblicazione. Oppure, per apportare modifiche, uscire dall’anteprima per tornare alle modifiche apportate.

## Formattazione del testo {#formattingtext}

Durante la modifica di un frammento di testo nell’interfaccia utente dell’agente, la barra degli strumenti cambia a seconda del tipo di modifiche che si desidera apportare: Font, Paragrafo o Elenco:

![typeofformattingtoolbar](assets/typeofformattingtoolbar.png) , barra degli strumenti ![Font](do-not-localize/fonttoolbar.png)

Barra dei font

![Barra degli strumenti Paragrafo](do-not-localize/paragraphtoolbar.png)

Barra degli strumenti Paragrafo

![Elenco, barra degli strumenti](do-not-localize/listtoolbar.png)

Elenco, barra degli strumenti

### Evidenziare/enfatizzare parti di testo {#highlightemphasize}

Per evidenziare\enfatizzare parti di testo in un frammento modificabile, selezionare il testo e toccare Evidenzia colore.

![highlightextagentui](assets/highlighttextagentui.png)

### Incolla testo formattato {#pasteformattedtext}

![pastedtext](assets/pastedtext.png)

### Inserire caratteri speciali nel testo {#specialcharacters}

L&#39;interfaccia utente dell&#39;agente supporta 210 caratteri speciali. L&#39;amministratore può [aggiungere il supporto per più o meno caratteri speciali personalizzati in base alla personalizzazione](/help/forms/using/custom-special-characters.md).

#### Consegna dell&#39;allegato {#attachmentdelivery}

* Quando viene eseguito il rendering della comunicazione interattiva utilizzando le API lato server come PDF interattivo o non interattivo, il PDF di cui è stato effettuato il rendering contiene allegati come allegati PDF.
* Quando un processo di post associato a una comunicazione interattiva viene caricato come parte dell&#39;interfaccia utente Invia tramite agente, gli allegati vengono passati come parametro List&lt;com.adobe.idp.Document> inAttachmentDocs.
* I flussi di lavoro che utilizzano il meccanismo di distribuzione, come l&#39;e-mail e la stampa, distribuiscono anche gli allegati insieme alla versione PDF della comunicazione interattiva.

## Azioni e informazioni disponibili nell’interfaccia utente dell’agente {#actionsagentui}

### Document fragments {#document-fragments}

![](do-not-localize/contentoptionsdocfragments.png)

* **Frecce** Su/Giù: Frecce per spostare i frammenti di documento verso l’alto o il basso nella comunicazione interattiva.
* **Elimina**: Se consentito, eliminare il frammento di documento dalla comunicazione interattiva.
* **Interruzione di pagina prima** (applicabile ai frammenti secondari dell&#39;area di destinazione): Inserisce un&#39;interruzione di pagina prima del frammento del documento.
* **Rientro**: Aumentare o diminuire il rientro di un frammento di documento.
* **Interruzione di pagina dopo** (applicabile ai frammenti secondari dell&#39;area di destinazione): Inserisce un&#39;interruzione di pagina dopo il frammento del documento.

![docfragoptions](assets/docfragoptions.png)

* Modifica (solo frammenti di testo): Aprire l&#39;editor Rich Text per modificare il frammento del documento di testo. Per ulteriori informazioni, vedere [Formattazione del testo](#formattingtext).

* Selezione (icona occhio): Include\esclude frammento di documento dalla comunicazione interattiva.
* Valori non compilati (info): Indica il numero di variabili non compilate nel frammento di documento.

### Elenca frammenti di documento {#list-document-fragments}

![list,](assets/listoptions.png)

* Inserisci riga vuota: Inserisce una nuova riga vuota.
* Selezione (icona occhio): Include\esclude frammento di documento dalla comunicazione interattiva.
* Ignora elenchi puntati/numerati: Consente di saltare elenchi puntati/numerati nel frammento di documento elenco.
* Valori non compilati (info): Indica il numero di variabili non compilate nel frammento di documento.

## Salva le comunicazioni interattive come bozza {#save-as-draft}

È possibile utilizzare l&#39;interfaccia utente agente per salvare una o più bozze per ogni comunicazione interattiva e recuperare la bozza in un secondo momento per continuare a lavorarci. È possibile specificare un nome diverso per ciascuna bozza per identificarla.

Adobe consiglia di eseguire queste istruzioni in sequenza per salvare correttamente una comunicazione interattiva come bozza.

### Abilitare la funzione Salva come bozza {#before-save-as-draft}

Per impostazione predefinita, la funzione Salva come bozza non è abilitata. Per attivare la funzione, effettuate le seguenti operazioni:

1. Implementare l&#39;interfaccia [ccrDocumentInstance](https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/index.html) Service Provider Interface (SPI). L&#39;SPI consente di salvare la versione bozza della comunicazione interattiva nel database con un ID bozza come identificatore univoco.
1. Passa a `https://'[server]:[port]'/system/console/configMgr`.
1. Toccate **[!UICONTROL Crea configurazione]** corrispondenza.
1. Selezionate **[!UICONTROL Abilita salvataggio con CCRDocumentInstanceService]** e toccate **[!UICONTROL Salva]**.

### Salvataggio di una comunicazione interattiva come bozza {#save-as-draft-agent-ui}

Per salvare una comunicazione interattiva come bozza, effettuate le seguenti operazioni:

1. Selezionare una comunicazione interattiva in Forms Manager e toccare **[!UICONTROL Apri interfaccia utente]** agente.

1. Apportate le modifiche necessarie nell&#39;interfaccia utente dell&#39;agente e toccate **[!UICONTROL Salva come bozza]**.

1. Specificate il nome della bozza nel campo **[!UICONTROL Nome]** e toccate **[!UICONTROL Fine]**.

Dopo aver salvato la comunicazione interattiva come bozza, toccate **[!UICONTROL Salva modifiche]** per salvare eventuali ulteriori modifiche alla bozza.

### Recuperare la bozza di una comunicazione interattiva {#retrieve-draft}

Dopo aver salvato una comunicazione interattiva come bozza, potete recuperarla per continuare a lavorarci. Recuperate la comunicazione interattiva utilizzando:

`https://server:port/aem/forms/createcorrespondence.hmtl?draftid=[draftid]`

[draft] si riferisce all&#39;identificatore univoco per la versione bozza che viene generata dopo il salvataggio di una comunicazione interattiva come bozza.

>[!NOTE]
>
>Se dopo il salvataggio come bozza apportate delle modifiche alla comunicazione interattiva, la versione bozza non viene aperta.
