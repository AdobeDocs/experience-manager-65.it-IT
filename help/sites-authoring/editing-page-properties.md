---
title: Modifica delle proprietà di una pagina di contenuto
description: Definisci le proprietà richieste per una pagina in Adobe Experience Manager.
exl-id: 3cd9374f-6f16-40fb-97cf-5f9a750b8dd2
source-git-commit: eaffc71c23c18d26ec5cbb2bbb7524790c4826fe
workflow-type: tm+mt
source-wordcount: '1872'
ht-degree: 42%

---

# Modifica delle proprietà di una pagina{#editing-page-properties}

Puoi impostare le proprietà richieste per una pagina. Queste possono variare a seconda del tipo di pagina. Ad esempio, alcune pagine potrebbero essere collegate a una Live Copy, mentre altre no, e le informazioni Live Copy diventano disponibili in base alle esigenze.

## Proprietà pagina {#page-properties}

Le proprietà sono distribuite su più schede.

### Base {#basic}

* **Titolo**

  Il titolo della pagina viene visualizzato in varie posizioni. Ad esempio, il **Siti Web** e la scheda **Sites** viste a schede/elenco.

  Questo campo è obbligatorio.

* **Tag**

  Qui puoi aggiungere o rimuovere i tag dalla pagina aggiornando l’elenco nella casella di selezione:

   * Dopo aver selezionato un tag, questo viene elencato sotto la casella di selezione. È possibile rimuovere un tag dall’elenco utilizzando la x.
   * È possibile immettere un nuovo tag digitandone il nome in una casella di selezione vuota.

      * Il nuovo tag viene creato quando premi Invio.
      * Il nuovo tag viene visualizzato con una piccola stella sulla destra che indica che si tratta di un nuovo tag.

   * Con la funzionalità a discesa, puoi selezionare tra i tag esistenti.
   * Quando passi il mouse su uno dei tag nella casella di selezione, viene visualizzata una x, che può essere utilizzata per rimuovere quel tag per quella pagina.

  Per ulteriori informazioni sui tag, consulta [Utilizzo dei tag](/help/sites-authoring/tags.md).

* **Nascondi in navigazione**

  Indica se la pagina viene visualizzata o nascosta nella navigazione delle pagine del sito finale.

* **Marchio**

  Applica un’identità del brand coerente tra le pagine aggiungendo un marchio a ciascun titolo della pagina. Questa funzionalità richiede l’utilizzo del Componente Pagina dalla versione 2.14.0 o successiva di [Componenti Core.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=it)

   * **Override**: selezionalo per definire il marchio su questa pagina.
      * Il valore viene ereditato da tutte le pagine secondarie a meno che non abbiano impostati anche i loro valori **Override**.
   * **Valore di override**: testo del marchio da aggiungere al titolo della pagina.
      * Il valore viene aggiunto al titolo della pagina dopo un carattere di barra come &quot;Cycling Tuscany | Always ready for the WKND&quot;
* **Titolo pagina**

  Titolo da utilizzare nella pagina. Generalmente utilizzato dai componenti titolo. Se vuoto, il **Titolo** è utilizzato.

* **Titolo navigazione**

  Puoi specificare un titolo separato da utilizzare nella navigazione (ad esempio, se desideri qualcosa di più conciso). Se vuoto, il **Titolo** è utilizzato.

* **Sottotitolo**

  Sottotitolo da utilizzare nella pagina.

* **Descrizione**

  Descrizione della pagina, il suo scopo o altri dettagli.

* **Ora di attivazione**

  La data e l’ora in cui la pagina pubblicata viene attivata. Quando viene pubblicata, la pagina rimane inattiva fino all’ora specificata.

  Lascia questi campi vuoti per le pagine che desideri pubblicare immediatamente (lo scenario normale).

* **Ora di disattivazione**

  L’ora in cui la pagina pubblicata viene disattivata.

  Lascia di nuovo questi campi vuoti per un’azione immediata.

* **URL personalizzato**

  Immetti un URL personalizzato per questa pagina, che può consentire di avere un URL più breve e/o più espressivo.

  Ad esempio, se l’URL personalizzato è impostato su `welcome`alla pagina identificata dal percorso `/v1.0/startpage`per il sito web `http://example.com,` allora `http://example.com/welcome`sarebbe l’URL personalizzato di `http://example.com/content/v1.0/startpage`

  >[!CAUTION]
  >
  >Gli URL personalizzati:
  >
  >* Deve essere univoco. Assicurati che il valore non sia già utilizzato da un’altra pagina.
  >* non supportano le espressioni regolari;
  >* non devono essere impostati su una pagina esistente.
  >

  Configura Dispatcher per abilitare l’accesso agli URL personalizzati. Consulta [Abilitazione dell’accesso agli URL personalizzati](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#enabling-access-to-vanity-urls-vanity-urls) per ulteriori dettagli.

* **Reindirizza URL personalizzato**

  Indica se desideri che la pagina utilizzi il Vanity URL.

### Avanzate  {#advanced}

* **Lingua**

  Lingua della pagina.

* **Directory principale lingua**

  Deve essere selezionato se la pagina è la directory principale di una copia per lingua.

* **Reindirizza**

  Indica la pagina a cui deve essere automaticamente reindirizzata la pagina.

* **Design**

  Indicare [progettazione](/help/sites-developing/designer.md) da utilizzare per questa pagina.

* **Alias**

  Specificare un alias da utilizzare per la pagina.

   * Ad esempio, se definisci un alias di `private` per la pagina`/content/wknd/us/en/magazine/members-only`, è possibile accedere a questa pagina tramite `/content/wknd/us/en/magazine/private`
   * La creazione di un alias imposta la proprietà `sling:alias` sul nodo della pagina, che influisce solo sulla risorsa, non sul percorso dell&#39;archivio.
   * Le pagine accessibili da alias nell’editor non possono essere pubblicate. Le [opzioni di pubblicazione](/help/sites-authoring/publishing-pages.md) nell’editor sono disponibili solo per le pagine accessibili tramite i relativi percorsi effettivi.
   * Per maggiori dettagli, vedi [Nomi di pagina localizzati in Best practice per la gestione di SEO e URL](/help/managing/seo-and-url-management.md#localized-page-names).

* **Ereditato da &lt;*percorso*>**

  Indica se la pagina viene ereditata. e da dove.

* **Configurazione cloud**

  Percorso della configurazione.

* **Modelli consentiti**

  [Definire l’elenco dei modelli disponibili](/help/sites-authoring/templates.md#allowingatemplate) all’interno di questa sub-filiale.

* **Abilita** (Autenticazione richiesta)

  Attiva (o disattiva) l’utilizzo dell’autenticazione per accedere alla pagina.

  >[!NOTE]
  >
  >Nella scheda **[Autorizzazioni](/help/sites-authoring/editing-page-properties.md#permissions)** è possibile definire gruppi utenti chiusi per la pagina.

  >[!CAUTION]
  >
  >Il **[Autorizzazioni](/help/sites-authoring/editing-page-properties.md#main-pars-procedure-949394300)** consente di modificare le configurazioni CUG in base alla presenza del `granite:AuthenticationRequired` mixin. Se le autorizzazioni di pagina sono configurate utilizzando configurazioni CUG obsolete, in base alla presenza di `cq:cugEnabled` , viene visualizzato un messaggio di avvertenza in **Autenticazione richiesta** e l’opzione non è modificabile, né il [Autorizzazioni](/help/sites-authoring/editing-page-properties.md#permissions) modificabile.
  >
  >
  >In questo caso, le autorizzazioni per il gruppo utenti chiusi devono essere modificate nel [interfaccia classica](/help/sites-classic-ui-authoring/classic-page-author-edit-page-properties.md).

* **Pagina di accesso**

  Pagina da utilizzare per l’accesso.

* **Configurazione esportazione**

  Specifica una configurazione di esportazione.

### Miniatura  {#thumbnail}

Mostra l&#39;immagine di anteprima della pagina. Operazioni disponibili:

* **Genera anteprima**

  Genera un’anteprima della pagina da utilizzare come miniatura.

* **Carica immagine**

  Carica un&#39;immagine da usare come miniatura.

* **Seleziona immagine**

  Seleziona una risorsa esistente da usare come miniatura.

* **Versione precedente**

  Questa opzione diventa disponibile dopo aver modificato la miniatura. Se non desideri mantenere la modifica, puoi annullarla prima di salvare.

### Social media {#social-media}

* **Condivisione social media**

  Definisce le opzioni di condivisione disponibili sulla pagina. Espone le opzioni disponibili per [Condivisione del componente core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/sharing.html?lang=en).

   * **Abilita condivisione utenti per Facebook**
   * **Abilita condivisione utenti per Pinterest**
   * **Variante XF preferita**
Definire la variante del frammento esperienza utilizzata per generare i metadati per una pagina

### Servizi cloud {#cloud-services}

* **Servizi cloud**

  Definisci le proprietà per [servizi cloud](/help/sites-developing/extending-cloud-config.md).

### Personalizzazione {#personalization}

* **Configurazioni ContextHub**

  Seleziona la [Configurazione ContextHub](/help/sites-developing/ch-configuring.md) e [Percorso segmenti](/help/sites-administering/segmentation.md).

* **Configurazione targeting**

  Seleziona un [marchio per specificare l’ambito di targeting](/help/sites-authoring/target-adobe-campaign.md).

  >[!NOTE]
  >Questa opzione richiede che l’account utente appartenga al gruppo `Target Adminstrators`.

### Autorizzazioni  {#permissions}

* **Autorizzazioni**

  In questa scheda puoi effettuare le seguenti operazioni:

   * [Aggiungere autorizzazioni](/help/sites-administering/user-group-ac-admin.md)
   * [Modificare un gruppo utenti chiuso](/help/sites-administering/cug.md#applying-your-closed-user-group-to-content-pages)

   * Visualizza le [autorizzazioni effettive](/help/sites-administering/user-group-ac-admin.md)

  >[!CAUTION]
  >
  >Il **Autorizzazioni** consente di modificare le configurazioni del gruppo utenti chiusi (CUG) in base alla presenza del `granite:AuthenticationRequired` mixin. Se le autorizzazioni di pagina sono configurate utilizzando configurazioni CUG obsolete, in base alla presenza di `cq:cugEnabled` viene visualizzato un messaggio di avvertenza e le autorizzazioni del gruppo utenti chiusi non sono modificabili, né il requisito di autenticazione [Avanzate](/help/sites-authoring/editing-page-properties.md#advanced) scheda modificabile.
  >
  >
  >In questo caso, le autorizzazioni per il gruppo utenti chiusi devono essere modificate nel [interfaccia classica](/help/sites-classic-ui-authoring/classic-page-author-edit-page-properties.md).

  >[!NOTE]
  >
  >La scheda Autorizzazioni non consente la creazione di gruppi CUG vuoti, che può essere utile come modo semplice per negare l’accesso a ogni utente. A questo scopo, è necessario utilizzare CRX Explorer. Consulta il documento [Amministrazione di utenti, gruppi e diritti di accesso](/help/sites-administering/user-group-ac-admin.md) per ulteriori informazioni.

### Blueprint {#blueprint}

* **Blueprint**

  Definire le proprietà per una pagina Blueprint in [gestione multisito](/help/sites-administering/msm.md). Controlla le circostanze in cui le modifiche vengono propagate alla Live Copy.

### Live Copy  {#live-copy}

* **Livecopy**

  Definire le proprietà per una pagina Live Copy in [gestione multisito](/help/sites-administering/msm.md). Controlla le circostanze in cui le modifiche vengono propagate dalla blueprint.

### Struttura sito  {#site-structure}

* Fornisce collegamenti alle pagine che forniscono funzionalità a livello di sito, ad esempio **Pagina registrazione**, **Pagina offline**, tra gli altri.

## Modifica delle proprietà di una pagina {#editing-page-properties-1}

Puoi definire le proprietà di pagina:

* Dalla console **Sites**:

   * [Crea una nuova pagina](/help/sites-authoring/managing-pages.md#creating-a-new-page) (un sottoinsieme delle proprietà)

   * Tocca o fai clic su **Proprietà**

      * Per una singola pagina
      * Per più pagine (solo un sottoinsieme delle proprietà è disponibile per la modifica in blocco)

* Dall’editor di pagine:

   * Tramite **Informazioni pagina** (quindi **Apri proprietà**)

### Dalla console Sites - Pagina singola {#from-the-sites-console-single-page}

Tocca o fai clic su **Proprietà** per definire le proprietà di pagina:

1. Nella console **Sites** individua il punto della pagina di cui desideri visualizzare e modificare le proprietà.

1. Seleziona l’opzione **Proprietà** per la pagina desiderata, utilizzando:

   * [Azioni rapide](/help/sites-authoring/basic-handling.md#quick-actions)
   * [Modalità di selezione](/help/sites-authoring/basic-handling.md#selectionmode)

   Le proprietà di pagina vengono visualizzate utilizzando le relative schede.

1. Visualizza o modifica le proprietà a seconda delle esigenze.

1. Quindi utilizza **Salva** per salvare gli aggiornamenti seguiti da **Chiudi** in modo da poter tornare alla console.

### Durante la modifica di una pagina {#when-editing-a-page}

Quando modifichi una pagina, puoi utilizzare **Informazioni pagina** per definire le proprietà di pagina:

1. Apri la pagina di cui desideri modificare le proprietà.

1. Seleziona l’icona **Informazioni pagina** per aprire il menu di selezione.

   ![screen_shot_2018-03-22at095740](assets/screen_shot_2018-03-22at095740.png)

1. Seleziona **Apri proprietà** e viene visualizzata una finestra di dialogo che consente di modificare le proprietà, ordinate in base alla scheda appropriata. A destra della barra degli strumenti sono disponibili anche i seguenti pulsanti:

   * **Annulla**
   * **Salva e chiudi**

1. Usa il pulsante **Salva e chiudi** per salvare le modifiche.

### Dalla console Sites - Pagine multiple {#from-the-sites-console-multiple-pages}

Dalla sezione **Sites** , è possibile selezionare più pagine e quindi utilizzare **Visualizza proprietà** per visualizzare e/o modificare le proprietà della pagina. Questa operazione è definita modifica in serie delle proprietà della pagina.

>[!NOTE]
>
>La modifica in blocco delle proprietà è disponibile anche per Assets. È simile, ma differisce in alcuni punti. Consulta [Modifica delle proprietà di più risorse](/help/assets/metadata.md) per i dettagli.
>
>È inoltre disponibile [Editor in blocco](/help/sites-administering/bulk-editor.md). Questo editor consente di cercare contenuti da più pagine utilizzando GQL (Google Query Language), e quindi di modificarli direttamente utilizzando l’editor in blocco prima di salvare le modifiche apportate alle pagine originarie.

Puoi selezionare più pagine per la modifica in serie utilizzando diversi metodi, tra i quali:

* Quando esplori la console **Sites**
* Dopo l’utilizzo di **Ricerca** per individuare un set di pagine

![epp-01](assets/epp-01.png)

Dopo aver selezionato le pagine e aver toccato o fatto clic sull’opzione **Proprietà**, vengono visualizzate le proprietà per la modifica in serie:

![epp-02](assets/epp-02.png)

Puoi eseguire la modifica in serie solo su pagine che:

* condividono lo stesso tipo di risorsa;
* non fanno parte di una Live Copy.

   * Se una delle pagine fa parte di una Live Copy, all’apertura delle proprietà viene visualizzato un messaggio di avviso.

Dopo aver inserito Modifica in serie, potete effettuare le seguenti operazioni:

* **Visualizza**

  Quando si visualizzano le proprietà di pagina per più pagine, è possibile visualizzare quanto segue:

   * Un elenco delle pagine interessate

      * Se necessario, puoi selezionare/deselezionare

   * Schede

      * Come per la visualizzazione delle proprietà di una singola pagina, le proprietà sono ordinate in schede.

   * Un sottoinsieme di proprietà

      * Puoi vedere le proprietà che sono disponibili su tutte le pagine selezionate e che sono state esplicitamente definite come disponibili per la modifica in serie.
      * Se la tua selezione include una sola pagina, tutte le proprietà sono visibili.

   * Proprietà condivise con un valore comune

      * Nella modalità Visualizza vengono mostrate solo le proprietà con un valore comune.
      * Quando il campo ha più valori (ad esempio Tag), questi vengono visualizzati solo quando *tutto* sono comuni. Se solo alcune sono comuni, vengono visualizzate solo durante la modifica.

  Se non esiste nessuna proprietà con un valore comune, viene visualizzato un messaggio.

* **Modifica**

  Quando si modificano le proprietà di pagina per più pagine:

   * Puoi aggiornare i valori nei campi disponibili.

      * I nuovi valori vengono applicati a tutte le pagine selezionate quando selezioni **Fine**.
      * Quando il campo è multivalore (ad esempio Tag), è possibile aggiungere un nuovo valore o rimuovere un valore comune.

   * I campi in comune ma con valori diversi nelle varie pagine sono contrassegnati da un valore speciale, ad esempio il testo `<Mixed Entries>`.

>[!NOTE]
>
>Il componente Pagina può essere configurato in modo da specificare i campi disponibili per la modifica in serie. Consulta [Configurazione della pagina per la modifica in serie delle proprietà di pagina](/help/sites-developing/bulk-editing.md).
