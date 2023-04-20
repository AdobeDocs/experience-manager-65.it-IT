---
title: Modifica delle proprietà della pagina di contenuto
description: Imposta le proprietà richieste per una pagina.
uuid: d3a2183b-8082-4cfc-aeed-26facbf3f3e6
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 1e9dd0d7-209a-4989-b66b-bca0d04b437a
docset: aem65
exl-id: 3cd9374f-6f16-40fb-97cf-5f9a750b8dd2
source-git-commit: e1a0b114ce16d0e7f6a464e9d30b8f111297bcc6
workflow-type: tm+mt
source-wordcount: '1885'
ht-degree: 61%

---

# Modifica delle proprietà di una pagina{#editing-page-properties}

Puoi impostare le proprietà richieste per una pagina. Queste possono variare a seconda del tipo di pagina. Ad esempio, alcune pagine potrebbero essere collegate a una Live Copy, mentre altre no, e le informazioni della Live Copy saranno rese disponibili a seconda delle necessità.

## Proprietà pagina   {#page-properties}

Le proprietà sono distribuite su più schede.

### Base {#basic}

* **Titolo**

   Il titolo della pagina viene visualizzato in varie posizioni. Ad esempio, il **Siti Web** l&#39;elenco delle schede e **Sites** viste a schede o a elenco.

   Questo campo è obbligatorio.

* **Tag**

   Qui puoi aggiungere o rimuovere i tag nella pagina modificando l’elenco nella casella di selezione:

   * Dopo aver selezionato un tag, questo viene elencato nella casella di selezione. È possibile rimuovere un tag dall’elenco utilizzando la x.
   * Per aggiungere un tag completamente nuovo, digitane il nome in una casella di selezione vuota.

      * Il nuovo tag viene creato quando premi Invio.
      * Il nuovo tag viene quindi mostrato con un asterisco a destra che lo identifica come nuovo tag.
   * Con l’elenco a discesa puoi selezionare uno dei tag esistenti.
   * Quando passi il mouse su uno dei tag nella casella di selezione, viene visualizzata una x, che può essere utilizzata per rimuovere quel tag per quella pagina.

   Per ulteriori informazioni sui tag, consulta [Utilizzo dei tag](/help/sites-authoring/tags.md).

* **Nascondi in navigazione**

   Indica se la pagina viene visualizzata o nascosta nella navigazione delle pagine del sito finale.

* **Marchio**

   Applica un’identità del brand coerente tra le pagine aggiungendo un marchio a ciascun titolo della pagina. Questa funzionalità richiede l’utilizzo del Componente Pagina dalla versione 2.14.0 o successiva di [Componenti Core.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=it)

   * **Override**: selezionalo per definire il marchio su questa pagina.
      * Il valore viene ereditato da tutte le pagine figlie a meno che non abbiano impostati anche i loro valori **Override**.
   * **Valore di override**: testo del marchio da aggiungere al titolo della pagina.
      * Il valore viene aggiunto al titolo della pagina dopo un carattere di barra come &quot;Cycling Tuscany | Always ready for the WKND&quot;
* **Titolo pagina**

   Titolo da utilizzare nella pagina. Generalmente utilizzato dai componenti titolo. Se viene lasciato vuoto, sarà utilizzato il **Titolo**.

* **Titolo navigazione**

   Puoi specificare un diverso titolo da usare nella navigazione (ad esempio, se desideri un elemento più conciso). Se vuoto, il **Titolo** verrà utilizzato.

* **Sottotitolo**

   Sottotitolo da utilizzare nella pagina.

* **Descrizione**

   Descrizione della pagina, del suo scopo o altri dettagli da aggiungere.

* **Ora di attivazione**

   Data e ora in cui verrà attivata la pagina pubblicata. Dopo la pubblicazione, la pagina rimarrà inattiva fino alla data e all’ora specificate.

   Lascia vuoti questi campi per le pagine da pubblicare immediatamente (lo scenario più consueto).

* **Ora di disattivazione**

   Data e ora in cui verrà disattivata la pagina pubblicata.

   Lascia nuovamente vuoti questi campi per un&#39;azione immediata.

* **URL personalizzato**

   Permette di inserire un URL personalizzato per questa pagina, che può consentirti di avere un URL più breve e/o più significativo.

   Ad esempio, se l’URL personalizzato è impostato su `welcome`alla pagina identificata dal percorso `/v1.0/startpage`per il sito web `http://example.com,` then `http://example.com/welcome`è l’URL personalizzato di `http://example.com/content/v1.0/startpage`

   >[!CAUTION]
   >
   >Gli URL personalizzati:
   >
   >* devono essere univoci, quindi accertati che il valore scelto non sia già utilizzato per un’altra pagina;
   >* non supportano le espressioni regolari;
   >* non devono essere impostati su una pagina esistente.


   Devi anche configurare Dispatcher per abilitare l’accesso agli URL personalizzati. Vedi [Abilitazione dell’accesso agli URL personalizzati](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#enabling-access-to-vanity-urls-vanity-urls) per ulteriori dettagli.

* **Reindirizza URL personalizzato**

   Indica se desideri che la pagina utilizzi l’URL personalizzato.

### Avanzate  {#advanced}

* **Lingua**

   Lingua della pagina.

* **Directory principale lingua**

   È necessario controllare se la pagina è la pagina principale di una copia per lingua.

* **Reindirizza**

   Indica la pagina a cui deve essere automaticamente reindirizzata la pagina corrente.

* **Design**

   Indica il [progettazione](/help/sites-developing/designer.md) da utilizzare per questa pagina.

* **Alias**

   Specifica un alias da utilizzare per la pagina.

   * Ad esempio, se definisci un alias di `private` per la pagina`/content/wknd/us/en/magazine/members-only`, è possibile accedere a questa pagina tramite `/content/wknd/us/en/magazine/private`
   * La creazione di un alias imposta la proprietà `sling:alias` sul nodo della pagina, che influisce solo sulla risorsa, non sul percorso dell&#39;archivio.
   * Le pagine a cui si accede tramite alias nell’editor non possono essere pubblicate. Le [opzioni di pubblicazione](/help/sites-authoring/publishing-pages.md) nell’editor sono disponibili solo per le pagine accessibili tramite i relativi percorsi effettivi.
   * Per maggiori dettagli, consulta [Nomi di pagina localizzati nelle best practice per la gestione di SEO e URL](/help/managing/seo-and-url-management.md#localized-page-names).

* **Ereditato da &lt;*path*>**

   Indica se la pagina viene ereditata. e da dove.

* **Configurazione cloud**

   Percorso della configurazione.

* **Modelli consentiti**

   [Definire l’elenco di modelli disponibili](/help/sites-authoring/templates.md#allowingatemplate) all’interno di questo ramo secondario.

* **Abilita** (Autenticazione richiesta)

   Abilita o disabilita l’utilizzo dell’autenticazione per accedere alla pagina.

   >[!NOTE]
   >
   >Nella scheda **[Autorizzazioni](/help/sites-authoring/editing-page-properties.md#permissions)** è possibile definire gruppi utenti chiusi per la pagina.

   >[!CAUTION]
   >
   >La **[Autorizzazioni](/help/sites-authoring/editing-page-properties.md#main-pars-procedure-949394300)** consente di modificare le configurazioni del gruppo utenti chiuso in base alla presenza del gruppo `granite:AuthenticationRequired` mixin. Se le autorizzazioni della pagina sono configurate utilizzando configurazioni CUG obsolete, in base alla presenza di `cq:cugEnabled` , in viene visualizzato un messaggio di avviso **Autenticazione richiesta** e l&#39;opzione non sarà modificabile, né il [Autorizzazioni](/help/sites-authoring/editing-page-properties.md#permissions) sia modificabile.
   >
   >
   >In tal caso, le autorizzazioni del gruppo utenti chiuso devono essere modificate nella sezione [interfaccia classica](/help/sites-classic-ui-authoring/classic-page-author-edit-page-properties.md).

* **Pagina di accesso**

   Pagina da utilizzare per l’accesso.

* **Configurazione esportazione**

   Specifica una configurazione di esportazione.

### Miniatura  {#thumbnail}

Mostra la miniatura della pagina. Operazioni disponibili:

* **Genera anteprima**

   Genera un’anteprima della pagina da utilizzare come miniatura.

* **Carica immagine**

   Carica un’immagine da usare come miniatura.

* **Seleziona immagine**

   Seleziona una risorsa esistente da usare come miniatura.

* **Versione precedente**

   Questa opzione diventa disponibile dopo aver apportato una modifica alla miniatura. Se non desideri mantenere la modifica, puoi annullarla prima di salvare.

### Social media {#social-media}

* **Condivisione social media**

   Definisce le opzioni di condivisione disponibili sulla pagina. Espone le opzioni disponibili per il [Condivisione dei componenti core](https://helpx.adobe.com/experience-manager/core-components/using/sharing.html).

   * **Abilita condivisione da parte degli utenti in Facebook**
   * **Abilita condivisione da parte degli utenti in Pinterest**
   * **Variante XF preferita**
Definire la variante del frammento esperienza utilizzato per generare i metadati per la pagina

### Servizi cloud {#cloud-services}

* **Servizi cloud**

   Consente di definire le proprietà per [servizi cloud](/help/sites-developing/extending-cloud-config.md).

### Personalizzazione {#personalization}

* **Configurazioni ContextHub**

   Seleziona la [Configurazione ContextHub](/help/sites-developing/ch-configuring.md) e [Percorso segmenti](/help/sites-administering/segmentation.md).

* **Configurazione targeting**

   Seleziona un [marchio per specificare l’ambito di targeting](/help/sites-authoring/target-adobe-campaign.md).

   >[!NOTE]
   >Questa opzione richiede che l’account utente appartenga al gruppo `Target Adminstrators`.

### Autorizzazioni  {#permissions}

* **Autorizzazioni**

   In questa scheda puoi:

   * [Aggiungere autorizzazioni](/help/sites-administering/user-group-ac-admin.md)
   * [Modificare un gruppo utenti chiuso](/help/sites-administering/cug.md#applying-your-closed-user-group-to-content-pages)

   * Visualizza le [autorizzazioni effettive](/help/sites-administering/user-group-ac-admin.md)
   >[!CAUTION]
   >
   >La **Autorizzazioni** consente di modificare le configurazioni del gruppo utenti chiuso in base alla presenza del gruppo `granite:AuthenticationRequired` mixin. Se le autorizzazioni della pagina sono configurate utilizzando configurazioni CUG obsolete, in base alla presenza di `cq:cugEnabled` , viene visualizzato un messaggio di avviso e le autorizzazioni del gruppo utenti chiuso non saranno modificabili, né il requisito di autenticazione relativo al gruppo [Avanzate](/help/sites-authoring/editing-page-properties.md#advanced) può essere modificata.
   >
   >
   >In tal caso, le autorizzazioni del gruppo utenti chiuso devono essere modificate nella sezione [interfaccia classica](/help/sites-classic-ui-authoring/classic-page-author-edit-page-properties.md).

   >[!NOTE]
   >
   >La scheda Autorizzazioni non consente la creazione di gruppi CUG vuoti, il che può essere utile come modo semplice per negare l’accesso a ogni utente. Per fare questo CRX Explorer deve essere utilizzato. Vedere il documento [Amministrazione di diritti di accesso, gruppi e utenti](/help/sites-administering/user-group-ac-admin.md) per ulteriori informazioni.

### Blueprint {#blueprint}

* **Blueprint**

   Consente di definire le proprietà per una pagina Blueprint all&#39;interno di [gestione multisito](/help/sites-administering/msm.md). Controlla le circostanze in cui le modifiche verranno propagate alla Live Copy.

### Live Copy  {#live-copy}

* **Livecopy**

   Consente di definire le proprietà per una pagina Live Copy all’interno di [gestione multisito](/help/sites-administering/msm.md). Controlla le circostanze in cui le modifiche verranno propagate dalla Blueprint.

### Struttura sito  {#site-structure}

* Fornisce i collegamenti alle pagine che offrono funzionalità a livello di sito, tra cui **Pagina registrazione** e **Pagina offline**.

## Modifica delle proprietà di una pagina {#editing-page-properties-1}

Puoi definire le proprietà della pagina:

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

1. Quindi, seleziona **Salva** per salvare le modifiche e **Chiudi** per tornare alla console.

### Durante la modifica di una pagina {#when-editing-a-page}

Quando modifichi una pagina puoi utilizzare **Informazioni pagina** per definire le proprietà di pagina:

1. Apri la pagina di cui desideri modificare le proprietà.

1. Seleziona l’icona **Informazioni pagina** per aprire il menu di selezione.

   ![screen_shot_2018-03-22at095740](assets/screen_shot_2018-03-22at095740.png)

1. Seleziona **Apri proprietà** viene visualizzata una finestra di dialogo che consente di modificare le proprietà, organizzate nella scheda appropriata. A destra della barra degli strumenti sono disponibili anche i seguenti pulsanti:

   * **Annulla**
   * **Salva e chiudi**

1. Usa il pulsante **Salva e chiudi** per salvare le modifiche.

### Dalla console Sites - Pagine multiple {#from-the-sites-console-multiple-pages}

Dalla console **Sites** è possibile selezionare più pagine e quindi utilizzare **Visualizza proprietà** per visualizzare e/o modificare le proprietà della pagina. Questa operazione è definita modifica in serie delle proprietà di pagina.

>[!NOTE]
>
>La modifica in serie delle proprietà è disponibile anche per le risorse. È molto simile, ma differisce per alcuni aspetti. Vedi [Modifica delle proprietà di più risorse](/help/assets/metadata.md) per i dettagli.
>
>C&#39;è anche la [Editor in serie](/help/sites-administering/bulk-editor.md), che consente di cercare contenuti da più pagine tramite GQL (Google Query Language) e quindi di modificare il contenuto direttamente nell’editor in blocco prima di salvare le modifiche nelle pagine originarie.

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

Dopo aver attivato la funzione Modifica in serie, puoi effettuare le seguenti operazioni:

* **Visualizza**

   Quando visualizzi Proprietà pagina per più pagine puoi vedere:

   * Un elenco delle pagine interessate

      * Se necessario, seleziona o deseleziona
   * Schede

      * Come per la visualizzazione delle proprietà di una singola pagina, le proprietà sono ordinate in schede.
   * Un sottoinsieme di proprietà

      * Puoi vedere le proprietà che sono disponibili su tutte le pagine selezionate e che sono state esplicitamente definite come disponibili per la modifica in serie.
      * Se la tua selezione include una sola pagina, tutte le proprietà sono visibili.
   * Proprietà condivise con un valore comune

      * Nella modalità Visualizza vengono mostrate solo le proprietà con un valore comune.
      * Quando il campo ha più valori (ad esempio Tag), questi vengono visualizzati solo se *tutti* i valori sono applicati alle pagine selezionate. Se le pagine hanno in comune solo alcuni valori, questi verranno visualizzati solo in fase di modifica.

   Se non esiste nessuna proprietà con un valore comune, viene visualizzato un messaggio.

* **Modifica**

   Durante la modifica delle proprietà pagina per più pagine:

   * Puoi aggiornare i valori nei campi disponibili.

      * I nuovi valori verranno applicati a tutte le pagine selezionate quando si seleziona **Fine**.
      * Quando il campo è multivalore (ad esempio Tag), è possibile aggiungere un nuovo valore o rimuovere un valore comune.
   * I campi in comune ma con valori diversi nelle varie pagine saranno contraddistinti da uno speciale valore, ad esempio `<Mixed Entries>`.


>[!NOTE]
>
>Il componente pagina può essere configurato per specificare i campi disponibili per la modifica collettiva. Vedi [Configurazione della pagina per la modifica collettiva delle proprietà di pagina](/help/sites-developing/bulk-editing.md).
