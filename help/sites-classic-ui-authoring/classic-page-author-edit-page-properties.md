---
title: Modifica delle proprietà di una pagina
seo-title: Editing Page Properties
description: Le proprietà di una pagina possono variare a seconda del tipo di pagina. Ad esempio, alcune pagine possono essere connesse a una Live Copy, mentre altre no, e le informazioni della Live Copy saranno disponibili ove appropriato.
seo-description: Properties of a page can vary depending on the nature of the page. For example some pages might be connected to a live copy while others are not and the live copy information will be available as appropriate.
uuid: 63d37d1b-52da-489d-b02b-e8b3d17571d1
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 23768c73-ac64-4727-8313-160c8c131b05
exl-id: 1a77e4cd-bbf8-4d05-bb35-fd43c02eaf30
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '763'
ht-degree: 96%

---

# Modifica delle proprietà di una pagina{#editing-page-properties}

Puoi impostare le proprietà richieste per una pagina. Queste possono variare a seconda del tipo di pagina. Ad esempio, alcune pagine possono essere connesse a una Live Copy, mentre altre no, e le informazioni della Live Copy saranno disponibili ove appropriato.

## Proprietà pagina   {#page-properties}

Le proprietà sono distribuite su più schede:

### Base {#basic}

* **Titolo**

   Il titolo della pagina viene visualizzato in diversi punti. Ad esempio, nell’elenco della scheda **Siti web** e nelle viste a scheda o elenco di **Sites**.

   Questo campo è obbligatorio.

* **Tag**

   Qui puoi aggiungere o rimuovere i tag nella pagina modificando l’elenco nella casella di selezione:

   * Dopo aver selezionato un tag, questo viene elencato nella casella di selezione. Per rimuovere un tag dall’elenco, utilizza l’icona x.
   * Per aggiungere un tag nuovo, digita il nome in una casella di selezione vuota.

      Il nuovo tag viene creato non appena premete Invio. Il nuovo tag verrà quindi mostrato in una casella con una piccola stella che lo identifica come nuovo tag.

   * L’elenco a discesa consente di selezionare uno dei tag esistenti.
   * Quando sposti il mouse su un tag nella casella di selezione viene visualizzata una x, che consente di rimuovere il tag dalla pagina in questione.

* **Nascondi in navigazione**

   Questo tasto consente di mostrare o nascondere la pagina nella mappa di navigazione delle pagine.

* **Titolo pagina**

   Titolo da utilizzare nella pagina.

* **Titolo navigazione**

   Puoi specificare un diverso titolo da usare per la navigazione (ad esempio un titolo più conciso). Se questo campo è vuoto, viene utilizzato il **Titolo**.

* **Sottotitolo**

   Sottotitolo da utilizzare nella pagina.

* **Descrizione**

   Descrizione della pagina, del suo ruolo o altri dettagli.

* **Ora di attivazione**

   Data e ora in cui verrà attivata la pagina pubblicata. Dopo la pubblicazione, la pagina rimarrà inattiva fino alla data e all’ora specificate. 

   Lascia vuoti questi campi per le pagine da pubblicare immediatamente (lo scenario più consueto).

* **Ora di disattivazione**

   Data e ora in cui verrà disattivata la pagina pubblicata.

   Anche in questo caso, lascia vuoti questi campi per le pagine da pubblicare immediatamente.

* **URL personalizzato**

   Consente di inserire un URL personalizzato per questa pagina. Questo consente di ottenere un URL più breve e significativo.

   Ad esempio, se l’URL personalizzato è impostato su w `elcome`alla pagina identificata dal percorso / `v1.0/startpage`per il sito web h `ttp://example.com,` allora h `ttp://example.com/welcome`è l’URL personalizzato di h `ttp://example.com/content/v1.0/startpage`

   >[!CAUTION]
   >
   >Gli URL personalizzati:
   >
   >* devono essere univoci, quindi accertati che il valore scelto non sia già utilizzato per un’altra pagina;
   >* non supportano le espressioni regolari.


* **Reindirizza URL personalizzato**

   Specifica se vuoi che la pagina usi l’URL personalizzato.

### Avanzate  {#advanced}

* **Lingua**

   Indica la lingua della pagina.

* **Reindirizza**

   Indica la pagina a cui deve essere automaticamente reindirizzata la pagina corrente.

* **Design**

   Indica il [design](/help/sites-developing/designer.md) da utilizzare per la pagina.

* **Alias**

   Specifica un alias da utilizzare per la pagina.

* **Abilita Gruppo utenti chiuso**

   Abilita o disabilita l’utilizzo di [gruppi utenti chiusi](/help/sites-administering/cug.md).

* **Pagina di accesso**

   Indica la pagina da utilizzare per l’accesso.

* **Gruppi consentiti**

   Gruppi autorizzati ad accedere al gruppo utenti chiuso.

* **Area di autenticazione**

   Nome di autenticazione del gruppo utenti chiuso.

* **Configurazione esportazione**

   Consente di specificare una configurazione di esportazione.

### Miniatura  {#thumbnail}

* **Miniatura pagina**

   Mostra la miniatura della pagina. Operazioni disponibili:

   * **Genera anteprima**

      Genera un’anteprima della pagina da usare come miniatura.

   * **Carica immagine**

      Carica un’immagine da usare come miniatura.

### Cloud Services {#cloud-services}

* **Cloud Services**

   Consente di definire le proprietà per i [servizi cloud](/help/sites-developing/extending-cloud-config.md).

### Personalizzazione {#personalization}

* **Personalizzazione**

   Seleziona un [marchio per specificare l’ambito di targeting](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md).

### Autorizzazioni   {#permissions}

* **Autorizzazioni** (interfaccia touch)

   Consente di visualizzare le [autorizzazioni attive e aggiungere nuove autorizzazioni](/help/sites-administering/user-group-ac-admin.md).

### Blueprint {#blueprint}

* **Blueprint**

   Consente di definire le proprietà per una pagina Blueprint nella [gestione multisito](/help/sites-administering/msm.md). Controlla le circostanze in cui le modifiche verranno propagate alla Live Copy.

### Live Copy  {#live-copy}

* **Livecopy**

   Consente di definire le proprietà per una pagina Live Copy nell’[utilità di gestione multisito](/help/sites-administering/msm.md). Controlla le circostanze in cui le modifiche verranno propagate dalla Blueprint.

### Struttura sito  {#site-structure}

* Fornisce i collegamenti alle pagine che offrono funzionalità a livello di sito, tra cui **Pagina registrazione** e **Pagina offline**.

## Modifica delle proprietà di una pagina {#editing-page-properties-2}

### Modifica delle proprietà pagina per una pagina specifica {#editing-page-properties-for-a-specific-page}

Nella finestra Proprietà pagina vengono definite le varie proprietà della pagina, ad esempio i titoli, che sono visualizzati nel sito web e in altre aree.

1. Aprite la pagina da modificare.

1. Nella barra laterale passate alla scheda **Pagina** e selezionate **Proprietà pagina**. 

   Viene visualizzata una finestra di dialogo con più schede.

1. Apportate le modifiche necessarie, quindi fate clic su **OK** per salvare.
