---
title: Modifica delle proprietà di pagina
description: Le proprietà di una pagina possono variare a seconda della natura della pagina. Ad esempio, alcune pagine potrebbero essere collegate a una Live Copy, mentre altre no, e le informazioni sulla Live Copy saranno disponibili nel modo appropriato.
uuid: 63d37d1b-52da-489d-b02b-e8b3d17571d1
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 23768c73-ac64-4727-8313-160c8c131b05
exl-id: 1a77e4cd-bbf8-4d05-bb35-fd43c02eaf30
source-git-commit: e1a0b114ce16d0e7f6a464e9d30b8f111297bcc6
workflow-type: tm+mt
source-wordcount: '763'
ht-degree: 31%

---

# Modifica delle proprietà di una pagina{#editing-page-properties}

Puoi impostare le proprietà richieste per una pagina. Queste possono variare a seconda del tipo di pagina. Ad esempio, alcune pagine potrebbero essere collegate a una Live Copy, mentre altre no, e le informazioni della Live Copy saranno rese disponibili a seconda delle necessità.

## Proprietà pagina   {#page-properties}

Le proprietà sono distribuite su più schede:

### Base {#basic}

* **Titolo**

   Il titolo della pagina viene visualizzato in varie posizioni. Ad esempio, il **Siti Web** e la scheda **Sites** viste a schede/elenco.

   Questo campo è obbligatorio.

* **Tag**

   Qui puoi aggiungere o rimuovere i tag nella pagina modificando l’elenco nella casella di selezione:

   * Dopo aver selezionato un tag, questo viene elencato nella casella di selezione. È possibile rimuovere un tag dall’elenco utilizzando la x.
   * Per aggiungere un tag completamente nuovo, digitane il nome in una casella di selezione vuota.

      Il nuovo tag verrà effettivamente creato quando premi Invio. Il nuovo tag verrà quindi visualizzato in una casella, con una piccola stella a destra che indica che si tratta di un nuovo tag.

   * Con l’elenco a discesa puoi selezionare uno dei tag esistenti.
   * Quando si passa il mouse su una voce di tag nel riquadro di selezione, viene visualizzata una x, che può essere utilizzata per rimuovere il tag per la pagina.

* **Nascondi in navigazione**

   Un interruttore per indicare se la pagina viene visualizzata o nascosta nella navigazione della pagina.

* **Titolo pagina**

   Titolo da utilizzare nella pagina.

* **Titolo navigazione**

   Puoi specificare un titolo separato da utilizzare nella navigazione (ad esempio, se desideri qualcosa di più conciso). Se vuoto, **Titolo** verrà utilizzato.

* **Sottotitolo**

   Sottotitolo da utilizzare nella pagina.

* **Descrizione**

   Descrizione della pagina, il suo scopo o altri dettagli.

* **Ora di attivazione**

   La data e l’ora in cui verrà attivata la pagina pubblicata. Quando viene pubblicata, la pagina rimarrà inattiva fino all’ora specificata.

   Lascia questi campi vuoti per le pagine che desideri pubblicare immediatamente (lo scenario più consueto).

* **Ora di disattivazione**

   L’ora in cui la pagina pubblicata verrà disattivata.

   Di nuovo, lascia vuoti questi campi per le pagine che desideri pubblicare immediatamente.

* **URL personalizzato**

   Consente di immettere un URL personalizzato per questa pagina. Ciò ti consente di avere un URL più breve e più espressivo.

   Ad esempio, se l’URL personalizzato è impostato su w `elcome`alla pagina identificata dal percorso / `v1.0/startpage`per il sito web h `ttp://example.com,` allora h `ttp://example.com/welcome`sarebbe l’URL personalizzato di h `ttp://example.com/content/v1.0/startpage`

   >[!CAUTION]
   >
   >Gli URL personalizzati:
   >
   >* deve essere univoco, quindi accertati che il valore non sia già utilizzato da un’altra pagina.
   >* non supportano i pattern regex.


* **Reindirizza URL personalizzato**

   Indica se desideri che la pagina utilizzi il Vanity URL.

### Avanzate  {#advanced}

* **Lingua**

   Lingua della pagina.

* **Reindirizza**

   Indica la pagina a cui deve essere automaticamente reindirizzata la pagina.

* **Design**

   Indicare [progettazione](/help/sites-developing/designer.md) da utilizzare per questa pagina.

* **Alias**

   Specificare un alias da utilizzare per la pagina.

* **Abilita gruppo utenti chiuso**

   Abilita (o disabilita) l&#39;uso di [gruppi utenti chiusi](/help/sites-administering/cug.md) (CUG).

* **Pagina di accesso**

   Pagina da utilizzare per l’accesso.

* **Gruppi consentiti**

   Gruppi idonei per l’accesso al CUG.

* **Realm**

   Nome area di autenticazione per il gruppo utenti chiusi.

* **Configurazione esportazione**

   Specifica una configurazione di esportazione.

### Miniatura  {#thumbnail}

* **Miniatura pagina**

   Mostra l&#39;immagine di anteprima della pagina. Operazioni disponibili:

   * **Genera anteprima**

      Genera un’anteprima della pagina da utilizzare come miniatura.

   * **Carica immagine**

      Carica un&#39;immagine da usare come miniatura.

### Servizi cloud {#cloud-services}

* **Servizi cloud**

   Definisci le proprietà per [servizi cloud](/help/sites-developing/extending-cloud-config.md).

### Personalizzazione {#personalization}

* **Personalizzazione**

   Seleziona un [marchio per specificare l’ambito di targeting](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md).

### Autorizzazioni   {#permissions}

* **Autorizzazioni** (interfaccia touch)

   Visualizza [autorizzazioni valide e nuove autorizzazioni](/help/sites-administering/user-group-ac-admin.md).

### Blueprint {#blueprint}

* **Blueprint**

   Definire le proprietà per una pagina Blueprint in [gestione multisito](/help/sites-administering/msm.md). Controlla le circostanze in cui le modifiche verranno propagate alla Live Copy.

### Live Copy  {#live-copy}

* **Livecopy**

   Definire le proprietà per una pagina Live Copy in [gestione multisito](/help/sites-administering/msm.md). Controlla le circostanze in cui le modifiche verranno propagate dalla Blueprint.

### Struttura sito  {#site-structure}

* Fornisce i collegamenti alle pagine che offrono funzionalità a livello di sito, tra cui **Pagina registrazione** e **Pagina offline**.

## Modifica delle proprietà di una pagina {#editing-page-properties-2}

### Modifica delle proprietà di una pagina specifica {#editing-page-properties-for-a-specific-page}

Le Proprietà pagina definiscono le varie proprietà della pagina, ad esempio i titoli, quando vengono visualizzati sul sito web e altri.

1. Apri la pagina da modificare.

1. Nella barra laterale aprire **Pagina** , quindi seleziona **Proprietà pagina...**

   Viene visualizzata una finestra di dialogo con più schede.

1. Apporta le modifiche necessarie, quindi fai clic su **OK** per salvare.
