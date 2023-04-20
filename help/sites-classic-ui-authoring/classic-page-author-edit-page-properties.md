---
title: Modifica delle proprietà di una pagina
description: Le proprietà di una pagina possono variare a seconda del tipo di pagina. Ad esempio, alcune pagine potrebbero essere collegate a una Live Copy, mentre altre no, e le informazioni della Live Copy saranno disponibili a seconda delle necessità.
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

   Il titolo della pagina viene visualizzato in varie posizioni. Ad esempio, il **Siti Web** l&#39;elenco delle schede e **Sites** viste a schede o a elenco.

   Questo campo è obbligatorio.

* **Tag**

   Qui puoi aggiungere o rimuovere i tag nella pagina modificando l’elenco nella casella di selezione:

   * Dopo aver selezionato un tag, questo viene elencato nella casella di selezione. È possibile rimuovere un tag dall’elenco utilizzando la x.
   * Per aggiungere un tag completamente nuovo, digitane il nome in una casella di selezione vuota.

      Il nuovo tag viene creato non appena premi Invio. Il nuovo tag verrà quindi mostrato in una casella, con una piccola stella a destra che lo identifica come nuovo tag.

   * Con l’elenco a discesa puoi selezionare uno dei tag esistenti.
   * Quando passi il mouse su una voce di tag nella casella di selezione viene visualizzata una x; può essere utilizzato per rimuovere il tag per la pagina.

* **Nascondi in navigazione**

   Un interruttore di attivazione/disattivazione per indicare se la pagina viene visualizzata o nascosta nella navigazione delle pagine.

* **Titolo pagina**

   Titolo da utilizzare nella pagina.

* **Titolo navigazione**

   Puoi specificare un diverso titolo da usare nella navigazione (ad esempio, se desideri un elemento più conciso). Se vuoto, il **Titolo** verrà utilizzato.

* **Sottotitolo**

   Sottotitolo da utilizzare nella pagina.

* **Descrizione**

   Descrizione della pagina, il suo scopo o altri dettagli.

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
   >* deve essere univoco, quindi accertati che il valore non sia già utilizzato da un’altra pagina.
   >* non supportano i pattern regex.


* **Reindirizza URL personalizzato**

   Indica se desideri che la pagina utilizzi l’URL personalizzato.

### Avanzate  {#advanced}

* **Lingua**

   Lingua della pagina.

* **Reindirizza**

   Indica la pagina a cui deve essere automaticamente reindirizzata la pagina corrente.

* **Design**

   Indica il [progettazione](/help/sites-developing/designer.md) da utilizzare per questa pagina.

* **Alias**

   Specifica un alias da utilizzare per la pagina.

* **Abilita gruppo utenti chiuso**

   Abilita o disabilita l’utilizzo di [gruppi di utenti chiusi](/help/sites-administering/cug.md) (CUG).

* **Pagina di accesso**

   Pagina da utilizzare per l’accesso.

* **Gruppi consentiti**

   Gruppi autorizzati ad accedere al gruppo di utenti chiuso.

* **Realm**

   Nome dell&#39;ambito del gruppo di utenti chiuso.

* **Configurazione esportazione**

   Specifica una configurazione di esportazione.

### Miniatura  {#thumbnail}

* **Miniatura pagina**

   Mostra la miniatura della pagina. Operazioni disponibili:

   * **Genera anteprima**

      Genera un’anteprima della pagina da utilizzare come miniatura.

   * **Carica immagine**

      Carica un’immagine da usare come miniatura.

### Servizi cloud {#cloud-services}

* **Servizi cloud**

   Consente di definire le proprietà per [servizi cloud](/help/sites-developing/extending-cloud-config.md).

### Personalizzazione {#personalization}

* **Personalizzazione**

   Seleziona un [marchio per specificare l’ambito di targeting](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md).

### Autorizzazioni   {#permissions}

* **Autorizzazioni** (interfaccia touch)

   Visualizza la [autorizzazioni efficaci e aggiunta di nuove autorizzazioni](/help/sites-administering/user-group-ac-admin.md).

### Blueprint {#blueprint}

* **Blueprint**

   Consente di definire le proprietà per una pagina Blueprint all&#39;interno di [gestione multisito](/help/sites-administering/msm.md). Controlla le circostanze in cui le modifiche verranno propagate alla Live Copy.

### Live Copy  {#live-copy}

* **Livecopy**

   Consente di definire le proprietà per una pagina Live Copy all’interno di [gestione multisito](/help/sites-administering/msm.md). Controlla le circostanze in cui le modifiche verranno propagate dalla Blueprint.

### Struttura sito  {#site-structure}

* Fornisce i collegamenti alle pagine che offrono funzionalità a livello di sito, tra cui **Pagina registrazione** e **Pagina offline**.

## Modifica delle proprietà di una pagina {#editing-page-properties-2}

### Modifica delle proprietà di una pagina specifica {#editing-page-properties-for-a-specific-page}

Le Proprietà pagina definiscono le varie proprietà della pagina, ad esempio i titoli, quando vengono visualizzati sul sito web e su altre.

1. Apri la pagina da modificare.

1. Nella barra laterale apri la **Pagina** scheda e seleziona **Proprietà pagina..**

   Viene visualizzata una finestra di dialogo con più schede.

1. Apporta le modifiche necessarie, quindi fai clic su **OK** da salvare.
