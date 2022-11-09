---
title: Modifica delle proprietà di una pagina
seo-title: Editing Page Properties
description: Puoi impostare le proprietà richieste per una pagina.
seo-description: Define the required properties for a page
uuid: d3a2183b-8082-4cfc-aeed-26facbf3f3e6
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 1e9dd0d7-209a-4989-b66b-bca0d04b437a
docset: aem65
exl-id: 3cd9374f-6f16-40fb-97cf-5f9a750b8dd2
source-git-commit: 63f066013c34a5994e2c6a534d88db0c464cc905
workflow-type: tm+mt
source-wordcount: '1884'
ht-degree: 90%

---

# Modifica delle proprietà di una pagina  {#editing-page-properties}

Puoi impostare le proprietà richieste per una pagina. Queste possono variare a seconda del tipo di pagina. Ad esempio, alcune pagine possono essere connesse a una Live Copy, mentre altre no, e le informazioni della Live Copy saranno disponibili ove appropriato.

## Proprietà pagina   {#page-properties}

Le proprietà sono distribuite su più schede.

### Base {#basic}

* **Titolo**

   Il titolo della pagina viene visualizzato in diversi punti. Ad esempio, nell’elenco della scheda **Siti web** e nelle viste a scheda o elenco di **Sites**.

   Questo campo è obbligatorio.

* **Tag**

   Qui puoi aggiungere o rimuovere i tag nella pagina modificando l’elenco nella casella di selezione:

   * Dopo aver selezionato un tag, questo viene elencato nella casella di selezione. Per rimuovere un tag dall’elenco, utilizza l’icona x.
   * Per aggiungere un tag nuovo, digita il nome in una casella di selezione vuota.

      * Il nuovo tag viene creato quando premi Invio.
      * Un asterisco a destra del nome lo identifica come nuovo tag.
   * L’elenco a discesa consente di selezionare uno dei tag esistenti.
   * Quando sposti il mouse su un tag nella casella di selezione viene visualizzata una x, che consente di rimuovere il tag dalla pagina in questione.

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

   Titolo da utilizzare nella pagina. Generalmente utilizzato dai componenti titolo. Se questo campo è vuoto, viene utilizzato il **Titolo**.

* **Titolo navigazione**

   Puoi specificare un diverso titolo da usare per la navigazione (ad esempio un titolo più conciso). Se questo campo è vuoto, viene utilizzato il **Titolo**.

* **Sottotitolo**

   Sottotitolo da utilizzare nella pagina.

* **Descrizione**

   La descrizione della pagina, del suo ruolo o altri dettagli.

* **Ora di attivazione**

   Data e ora in cui verrà attivata la pagina pubblicata. Dopo la pubblicazione, la pagina rimarrà inattiva fino alla data e all’ora specificate. 

   Lascia vuoti questi campi per le pagine da pubblicare immediatamente (lo scenario più consueto).

* **Ora di disattivazione**

   Data e ora in cui verrà disattivata la pagina pubblicata.

   Lascia questi campi vuoti per un’azione immediata.

* **URL personalizzato**

   Consente di immettere un URL personalizzato per questa pagina, se desideri inserire un URL più breve e/o più significativo.

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

   Specifica se vuoi che la pagina usi l’URL personalizzato.

### Avanzate  {#advanced}

* **Lingua**

   Indica la lingua della pagina.

* **Directory principale lingua**

   Deve essere selezionata, se la pagina è la pagina principale di una copia lingua.

* **Reindirizza**

   Indica la pagina a cui deve essere automaticamente reindirizzata la pagina corrente.

* **Design**

   Indica il [design](/help/sites-developing/designer.md) da utilizzare per la pagina.

* **Alias**

   Specifica un alias da utilizzare per la pagina.

   * Ad esempio, se definisci un alias di `private` per la pagina`/content/wknd/us/en/magazine/members-only`, è possibile accedere a questa pagina tramite `/content/wknd/us/en/magazine/private`
   * La creazione di un alias imposta la proprietà `sling:alias` sul nodo della pagina, che influisce solo sulla risorsa, non sul percorso dell&#39;archivio.
   * Le pagine a cui si accede tramite alias nell’editor non possono essere pubblicate. Le [opzioni di pubblicazione](/help/sites-authoring/publishing-pages.md) nell’editor sono disponibili solo per le pagine accessibili tramite i relativi percorsi effettivi.
   * Per maggiori dettagli vedi [Nomi di pagina localizzati nelle best practice SEO (Search Engine Optimization) e Gestione URL](/help/managing/seo-and-url-management.md#localized-page-names).

* **Ereditato da &lt;*percorso*>**

   Indica se la pagina viene ereditata e da dove.

* **Configurazione cloud**

   Percorso della configurazione.

* **Modelli consentiti**

   [Definisci l’elenco di modelli che saranno disponibili](/help/sites-authoring/templates.md#allowingatemplate) in questo ramo secondario.

* **Attiva** (richiesta di autenticazione)

   Attiva (o disattiva) l’uso dell’autenticazione per accedere alla pagina.

   >[!NOTE]
   >
   >Nella scheda **[Autorizzazioni](/help/sites-authoring/editing-page-properties.md#permissions)** è possibile definire gruppi utenti chiusi per la pagina.

   >[!CAUTION]
   >
   >La **[Autorizzazioni](/help/sites-authoring/editing-page-properties.md#main-pars-procedure-949394300)** consente di modificare le configurazioni del gruppo utenti chiuso in base alla presenza del gruppo `granite:AuthenticationRequired` mixin. Se le autorizzazioni della pagina sono configurate utilizzando configurazioni CUG obsolete, in base alla presenza di `cq:cugEnabled` , in viene visualizzato un messaggio di avviso **Autenticazione richiesta** e l&#39;opzione non sarà modificabile, né il [Autorizzazioni](/help/sites-authoring/editing-page-properties.md#permissions) sia modificabile.
   >
   >
   >In questo caso, le autorizzazioni del gruppo utenti chiuso devono essere modificate [nell’interfaccia classica](/help/sites-classic-ui-authoring/classic-page-author-edit-page-properties.md).

* **Pagina di accesso**

   Indica la pagina da utilizzare per l’accesso.

* **Configurazione esportazione**

   Consente di specificare una configurazione di esportazione.

### Miniatura  {#thumbnail}

Mostra la miniatura della pagina. Operazioni disponibili:

* **Genera anteprima**

   Genera un’anteprima della pagina da usare come miniatura.

* **Carica immagine**

   Carica un’immagine da usare come miniatura.

* **Seleziona immagine**

   Seleziona una risorsa esistente da usare come miniatura.

* **Versione precedente**

   Questa opzione diventa disponibile dopo aver apportato una modifica alla miniatura. Se non desideri mantenere la modifica, puoi ripristinarla prima di salvare.

### Social media {#social-media}

* **Condivisione social media**

   Definisce le opzioni di condivisione disponibili sulla pagina. Rende disponibili le opzioni per la [Condivisione dei componenti di base](https://helpx.adobe.com/experience-manager/core-components/using/sharing.html).

   * **Abilita condivisione da parte degli utenti su Facebook**
   * **Abilita condivisione da parte degli utenti su Pinterest**
   * **Variante XF preferita**
Consente di definire la variante del frammento esperienza utilizzato per generare i metadati della pagina.

### Cloud Services {#cloud-services}

* **Cloud Services**

   Consente di definire le proprietà per i [servizi cloud](/help/sites-developing/extending-cloud-config.md).

### Personalizzazione {#personalization}

* **Configurazioni ContextHub**

   Seleziona la [Configurazione ContextHub](/help/sites-developing/ch-configuring.md) e il [Percorso segmenti](/help/sites-administering/segmentation.md).

* **Configurazione targeting**

   Seleziona un [marchio per specificare l’ambito di targeting](/help/sites-authoring/target-adobe-campaign.md).

   >[!NOTE]
   >Questa opzione richiede che l’account utente appartenga al gruppo `Target Adminstrators`.

### Autorizzazioni  {#permissions}

* **Autorizzazioni**

   In questa scheda puoi:

   * [Aggiungere autorizzazioni](/help/sites-administering/user-group-ac-admin.md)
   * [Modificare un gruppo utenti chiuso](/help/sites-administering/cug.md#applying-your-closed-user-group-to-content-pages)

   * Visualizzare le [Autorizzazioni effettive](/help/sites-administering/user-group-ac-admin.md)
   >[!CAUTION]
   >
   >La **Autorizzazioni** consente di modificare le configurazioni del gruppo utenti chiuso in base alla presenza del gruppo `granite:AuthenticationRequired` mixin. Se le autorizzazioni della pagina utilizzano configurazioni del gruppo utenti chiuso obsolete, basate sulla proprietà `cq:cugEnabled`, viene visualizzato un messaggio di avvertenza e non sarà possibile modificare né l’opzione né l&#39;Autenticazione nella scheda [Avanzate](/help/sites-authoring/editing-page-properties.md#advanced).
   >
   >
   >In questo caso, le autorizzazioni del gruppo utenti chiuso devono essere modificate [nell’interfaccia classica](/help/sites-classic-ui-authoring/classic-page-author-edit-page-properties.md).

   >[!NOTE]
   >
   >La scheda Autorizzazioni non consente di creare gruppi utenti chiusi che siano vuoti; una soluzione utile per negare l’accesso a tutti gli utenti. A questo scopo devi usare CRX Explorer. Vedere il documento [Amministrazione di diritti di accesso, gruppi e utenti](/help/sites-administering/user-group-ac-admin.md) per ulteriori informazioni.

### Blueprint {#blueprint}

* **Blueprint**

   Consente di definire le proprietà per una pagina Blueprint nella [gestione multisito](/help/sites-administering/msm.md). Controlla le circostanze in cui le modifiche verranno propagate alla Live Copy.

### Live Copy  {#live-copy}

* **Livecopy**

   Consente di definire le proprietà per una pagina Live Copy nell’[utilità di gestione multisito](/help/sites-administering/msm.md). Controlla le circostanze in cui le modifiche verranno propagate dalla Blueprint.

### Struttura sito  {#site-structure}

* Fornisce i collegamenti alle pagine che offrono funzionalità a livello di sito, tra cui **Pagina registrazione** e **Pagina offline**.

## Modifica delle proprietà di una pagina {#editing-page-properties-1}

Puoi definire le proprietà di pagina:

* Dalla console **Sites**:

   * [Crea una nuova pagina](/help/sites-authoring/managing-pages.md#creating-a-new-page) (un sottoinsieme delle proprietà)

   * Tocca o fai clic su **Proprietà**

      * Per una singola pagina
      * Per più pagine (solo un sottoinsieme di proprietà è disponibile per la modifica in blocco)

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
>La modifica in serie delle proprietà è disponibile anche per le risorse. È molto simile, ma differisce per alcuni aspetti. Per ulteriori informazioni, consulta [Modificare le proprietà di risorse multiple](/help/assets/metadata.md).
>
>È disponibile anche lo strumento di [Modifica collettiva](/help/sites-administering/bulk-editor.md), che consente di cercare contenuti da più pagine tramite GQL (Google Query Language), e quindi di modificare il contenuto direttamente sullo strumento prima di salvare le modifiche sulle pagine originate.

Puoi selezionare più pagine per la modifica in serie utilizzando diversi metodi, tra i quali:

* Utilizzare la console **Sites**.
* Dopo aver utilizzato **Cerca** per individuare un insieme di pagine.

![epp-01](assets/epp-01.png)

Dopo aver selezionato le pagine e aver toccato o fatto clic sull’opzione **Proprietà**, vengono visualizzate le proprietà per la modifica in serie:

![epp-02](assets/epp-02.png)

Puoi eseguire la modifica in serie solo su pagine che:

* condividono lo stesso tipo di risorsa;
* non fanno parte di una Live Copy.

   * Se una delle pagine fa parte di una Live Copy, all’apertura delle proprietà viene visualizzato un messaggio di avviso.

Dopo aver attivato la funzione Modifica in serie, puoi effettuare le seguenti operazioni:

* **Visualizza**

   Quando visualizzi le Proprietà pagina per pagine multiple puoi vedere:

   * Un elenco delle pagine interessate.

      * Puoi selezionarle/deselezionarle se necessario.
   * Schede

      * Come per la visualizzazione delle proprietà di una pagina singola, le proprietà sono ordinate in schede.
   * Un sottoinsieme di proprietà.

      * Puoi vedere le proprietà che sono disponibili su tutte le pagine selezionate e che sono state esplicitamente definite come disponibili per la modifica in serie.
      * Se la tua selezione include una sola pagina, tutte le proprietà sono visibili.
   * Proprietà condivise con un valore comune

      * Nella modalità Visualizza vengono mostrate solo le proprietà con un valore comune.
      * Quando il campo ha più valori (ad esempio Tag), questi vengono visualizzati solo se *tutti* i valori sono applicati alle pagine selezionate. Se le pagine hanno in comune solo alcuni valori, questi verranno visualizzati solo in fase di modifica.

   Se non esiste nessuna proprietà con un valore comune, viene visualizzato un messaggio.

* **Modifica**

   Quando modifichi le Proprietà pagina per pagine multiple:

   * Puoi aggiornare i valori nei campi disponibili.

      * I nuovi valori saranno applicati a tutte le pagine selezionate quando fai clic su **Fine**.
      * Quando il campo ha valori multipli (ad esempio i Tag), puoi aggiungere un nuovo valore o rimuovere un valore comune.
   * I campi in comune ma con valori diversi nelle varie pagine saranno contraddistinti da uno speciale valore, ad esempio `<Mixed Entries>`.


>[!NOTE]
>
>Il componente di pagina può essere configurato in modo da specificare i campi disponibili per la modifica collettiva. Consulta [Configurazione della pagina per la modifica collettiva delle proprietà di pagina](/help/sites-developing/bulk-editing.md).
