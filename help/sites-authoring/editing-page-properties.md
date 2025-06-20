---
title: Modifica delle proprietà di una pagina
description: Definisci le proprietà richieste per una pagina in Adobe Experience Manager.
exl-id: 3cd9374f-6f16-40fb-97cf-5f9a750b8dd2
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User,Admin,Architect,Developer
mini-toc-levels: 2
source-git-commit: d0515a6a3d08e181eada4a22e0d128305148e6ea
workflow-type: tm+mt
source-wordcount: '2477'
ht-degree: 37%

---


# Modifica delle proprietà di una pagina{#editing-page-properties}

Puoi impostare le proprietà richieste per una pagina. Queste possono variare a seconda del tipo di pagina. Ad esempio, alcune pagine potrebbero essere collegate a una Live Copy, mentre altre no, e le informazioni Live Copy diventano disponibili in base alle esigenze.

## Proprietà pagina {#page-properties}

Le proprietà sono distribuite su più schede.

### Base {#basic}

#### Titolo e tag {#tile}

* **Titolo** - Il titolo della pagina viene visualizzato in varie posizioni
   * Ad esempio, l&#39;elenco di schede **Siti Web** e le visualizzazioni **Siti** per schede/elenchi.
   * Questo campo è obbligatorio.
* **Tag** - Qui puoi aggiungere o rimuovere tag dalla pagina aggiornando l&#39;elenco nella casella di selezione.
   * Dopo aver selezionato un tag, questo viene elencato sotto la casella di selezione. È possibile rimuovere un tag dall’elenco utilizzando la x.
   * È possibile immettere un nuovo tag digitandone il nome in una casella di selezione vuota.
      * Il nuovo tag viene creato quando premi Invio.
      * Il nuovo tag viene visualizzato con una piccola stella sulla destra che indica che si tratta di un nuovo tag.
   * Con il menu a discesa, puoi selezionare tra i tag esistenti.
   * Quando passi il mouse su uno dei tag nella casella di selezione, viene visualizzata una x, che può essere utilizzata per rimuovere quel tag per quella pagina.
   * Per ulteriori informazioni sui tag, vedere [Utilizzo dei tag.](/help/sites-authoring/tags.md)
* **Nascondi in navigazione** - Indica se la pagina viene visualizzata o nascosta nella navigazione delle pagine del sito risultante

#### Branding {#branding}

Applica un’identità del brand coerente tra le pagine aggiungendo un marchio a ciascun titolo della pagina. Questa funzionalità richiede l’utilizzo del Componente Pagina dalla versione 2.14.0 o successiva di [Componenti Core.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=it)

* **Override**: selezionalo per definire il marchio su questa pagina.
   * Il valore viene ereditato da tutte le pagine secondarie a meno che non abbiano impostati anche i loro valori **Override**.
* **Valore di override** - Testo del marchio da aggiungere al titolo della pagina
   * Il valore viene aggiunto al titolo della pagina dopo un carattere barra verticale come `Cycling Tuscany | Always ready for the WKND`

#### Altri titoli e descrizioni {#more}

* **Titolo pagina** - Titolo da utilizzare nella pagina
   * Generalmente utilizzato dai componenti titolo
   * Se vuoto, il **Titolo** è utilizzato.
* **Titolo navigazione** - È possibile specificare un titolo separato da utilizzare nella navigazione (ad esempio, se si desidera un titolo più conciso).
   * Se vuoto, il **Titolo** è utilizzato.
* **Sottotitolo** - Sottotitolo da utilizzare nella pagina
* **Descrizione** - Descrizione della pagina, il suo scopo o altri dettagli da aggiungere

#### Ora di attivazione/disattivazione {#on-time}

L’ora di attivazione/disattivazione di una pagina è un modo comodo per nascondere temporaneamente il contenuto già pubblicato. Il contenuto rimane nell’istanza di pubblicazione quando è disattivato. La disattivazione di una pagina non annulla la pubblicazione del contenuto.

* **Ora di attivazione**: la data e l’ora in cui la pagina pubblicata viene resa visibile (renderizzata) nell’ambiente di pubblicazione. La pagina deve essere pubblicata, manualmente o tramite replica automatica preconfigurata.

   * Se [pubblicato,](/help/sites-authoring/publishing-pages.md) questa pagina è già disponibile nell&#39;istanza di pubblicazione, ma è rimasta inattiva (nascosta) fino al rendering all&#39;ora specificata.
   * Se non è pubblicata e [configurata per la replica automatica,](/help/sites-deploying/replication.md) la pagina viene pubblicata automaticamente e quindi sottoposta a rendering alla data e all&#39;ora specificate.
   * Se non è pubblicata e non è configurata per la replica automatica, la pagina non viene pubblicata automaticamente, quindi viene visualizzato un errore 404 quando si tenta di accedere alla pagina.

* **Ora di disattivazione**: simile e spesso utilizzata in combinazione con l’**Ora di attivazione**, definisce l’ora in cui la pagina pubblicata viene nascosta nell’ambiente di pubblicazione.

Lascia questi campi (**Ora di attivazione** e **Ora di disattivazione**) vuoti per le pagine da pubblicare e disponibili immediatamente e disponibili nell&#39;ambiente di pubblicazione fino a quando non vengono disattivate (lo scenario normale).

>[!NOTE]
>Se l’**Ora di attivazione** o l’**Ora di disattivazione** è nel passato e la replica automatica è configurata, l’azione pertinente verrà attivata immediatamente.

>[!TIP]
>
>I tempi di attivazione/disattivazione riguardano esclusivamente i contenuti già pubblicati (manualmente o tramite replica automatica). Per questo motivo, i flussi di lavoro di pubblicazione come quelli per l’approvazione del contenuto non vengono attivati da a orari di attivazione/disattivazione e da orari di attivazione/disattivazione non influiscono sullo stato di pubblicazione della pagina. Per questo motivo, i tempi di attivazione/disattivazione sono più appropriati per mostrare/nascondere temporaneamente il contenuto già approvato e pubblicato.
>
>Se desideri pubblicare nuovi contenuti con tutti i flussi di lavoro associati o rimuovere completamente (annullare la pubblicazione) dal sito, [gestisci la pubblicazione.](/help/sites-authoring/publishing-pages.md#manage-publication)

#### URL personalizzato {#vanity-url}

Immetti un URL personalizzato per questa pagina, che può consentire di avere un URL più breve e/o più espressivo.

Ad esempio, se l&#39;URL personalizzato è impostato su `welcome` per la pagina identificata dal percorso `/v1.0/startpage` per il sito Web `http://example.com,`, `http://example.com/welcome`sarà l&#39;URL personalizzato di `http://example.com/content/v1.0/startpage`

>[!CAUTION]
>
>Gli URL personalizzati:
>
>* Deve essere univoco.
>* non supportano le espressioni regolari;
>* non devono essere impostati su una pagina esistente.

Configura Dispatcher per abilitare l’accesso agli URL personalizzati. Vedi [Abilitazione dell&#39;accesso agli URL personalizzati](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=it#enabling-access-to-vanity-urls-vanity-urls) per ulteriori dettagli.

* **Aggiungi** - Tocca o fai clic per aggiungere un URL personalizzato.
* **Rimuovi** - Tocca o fai clic per rimuovere un URL personalizzato.
  **Reindirizza Vanity URL** - Indica se la pagina deve utilizzare il Vanity URL o reindirizzare all&#39;URL effettivo della pagina

### Avanzato {#advanced}

#### Impostazioni {#settings}

* **Lingua**: indica la lingua della pagina
* **Lingua root**: deve essere selezionato, se la pagina è la root di una copia in lingua
* **Reindirizza**: indica la pagina a cui deve essere automaticamente reindirizzata la pagina corrente
* **Progettazione** - Indica la [progettazione](/help/sites-developing/designer.md) da utilizzare per questa pagina.
* **Alias**: specifica un alias da utilizzare per la pagina
   * Ad esempio, se definisci un alias di `private` per la pagina`/content/wknd/us/en/magazine/members-only`, è possibile accedere a questa pagina tramite `/content/wknd/us/en/magazine/private`
   * La creazione di un alias imposta la proprietà `sling:alias` sul nodo della pagina, che influisce solo sulla risorsa, non sul percorso dell&#39;archivio.
   * Le pagine accessibili da alias nell’editor non possono essere pubblicate. Le [opzioni di pubblicazione](/help/sites-authoring/publishing-pages.md) nell’editor sono disponibili solo per le pagine accessibili tramite i relativi percorsi effettivi.
   * Per ulteriori dettagli, consulta [Nomi di pagina localizzati in Best practice per la gestione di SEO e URL](/help/managing/seo-and-url-management.md#localized-page-names).

#### Configurazione {#configuration}

* **Ereditato da &lt;*percorso*>** - Abilita/disabilita l&#39;ereditarietà della **configurazione cloud** per la pagina
* **Configurazione cloud**: il percorso della configurazione

#### Impostazioni modello {#templates}

* **Modelli permessi**: [definisce l’elenco di modelli che sono disponibili](/help/sites-authoring/templates.md#allowingatemplate) in questo ramo secondario

#### Autenticazione richiesta {#authentication}

* **Abilita** - Abilita (o disabilita) l&#39;utilizzo dell&#39;autenticazione per poter accedere alla pagina
* **Pagina di accesso**: indica la pagina da utilizzare per l’accesso

>[!NOTE]
>
>Nella scheda **[Autorizzazioni](/help/sites-authoring/editing-page-properties.md#permissions)** è possibile definire gruppi utenti chiusi per la pagina.

>[!CAUTION]
>
>La scheda **[Autorizzazioni](#permissions)** consente di modificare le configurazioni CUG in base alla presenza del mixin `granite:AuthenticationRequired`. Se le autorizzazioni di pagina sono configurate utilizzando configurazioni CUG obsolete, in base alla presenza della proprietà `cq:cugEnabled`, viene visualizzato un messaggio di avviso in **Requisiti di autenticazione** e l&#39;opzione non è modificabile, né le [Autorizzazioni](/help/sites-authoring/editing-page-properties.md#permissions) sono modificabili.
>
>
>In tal caso, le autorizzazioni CUG devono essere modificate nell&#39;[interfaccia utente classica](/help/sites-classic-ui-authoring/classic-page-author-edit-page-properties.md).

#### Esporta {#export}

* **Configurazione** - Specifica una configurazione di esportazione

#### SEO {#seo}

* **URL canonico** - Utilizzato per sovrascrivere l&#39;URL canonico della pagina
   * Se lasciato vuoto, l’URL della pagina corrisponde al suo URL canonico.
* **Tag robot** - Utilizzare il menu a discesa per selezionare i tag robot per controllare il comportamento dei crawler dei motori di ricerca
   * Alcune opzioni sono in conflitto tra loro, nel qual caso l’opzione più permissiva ha la precedenza.
* **Genera mappa del sito** - Se selezionata, viene generato un `sitemap.xml` per questa pagina e i relativi discendenti.

### Immagini {#images}

#### Immagine in primo piano {#featured-image}

Questa sezione viene utilizzata per selezionare e configurare l’immagine da visualizzare. Viene utilizzata nei componenti che fanno riferimento alla pagina; ad esempio teaser, elenchi di pagine e così via.

* **Immagine** - È possibile **Selezionare** una risorsa o cercare un file da caricare, quindi **Modificare** o **Cancellare** l&#39;immagine selezionata.
* **Testo alternativo** - Testo utilizzato per rappresentare il significato e/o la funzione dell&#39;immagine, comunemente utilizzato dagli assistenti vocali
* **Eredita - Valore tratto dalla risorsa DAM** - Se questa opzione è selezionata, nel testo alternativo viene inserito il valore dei metadati `dc:description` in DAM.

#### Miniatura  {#thumbnail}

Questa sezione viene utilizzata per selezionare e configurare la miniatura dell’immagine per la pagina. Viene utilizzata nei componenti che fanno riferimento alla pagina; ad esempio teaser, elenchi di pagine e così via.

* **Genera anteprima** - Genera un&#39;anteprima della pagina da utilizzare come miniatura
* **Carica immagine** - Carica un&#39;immagine da utilizzare come miniatura
* **Seleziona immagine** - Seleziona una risorsa esistente da usare come miniatura
* **Ripristina** - Questa opzione diventa disponibile dopo aver modificato la miniatura. Se non desideri mantenere la modifica, puoi annullarla prima di salvare.

### Servizi cloud {#cloud-services}

* **Configurazioni Cloud Service** - Definisce quale configurazione viene utilizzata per i servizi cloud per la pagina
* **Ereditato da** - Per le Live Copy e le copie per lingua, le configurazioni cloud vengono ereditate dalla blueprint per impostazione predefinita.
   * Deseleziona per ignorare l’ereditarietà

### Personalizzazione {#personalization}

#### Configurazioni ContextHub {#contexthub}

* **Ereditato da** - Per impostazione predefinita, le configurazioni ContextHub vengono ereditate dalla pagina padre.
   * Deseleziona questa opzione per ignorare l’ereditarietà.
* **Percorso ContextHub** - Seleziona la [configurazione ContextHub](/help/sites-developing/ch-configuring.md)
* **Percorso segmenti** - Seleziona il [Percorso segmenti](/help/sites-administering/segmentation.md).

#### Configurazione targeting {#targeting}

Seleziona un marchio [per specificare un ambito per il targeting.](/help/sites-authoring/target-adobe-campaign.md)

>[!NOTE]
>Questa opzione richiede che l’account utente appartenga al gruppo `Target Adminstrators`.

### Autorizzazioni  {#permissions}

Utilizzare la scheda **Autorizzazioni** per definire quali utenti, gruppi o [gruppi di utenti chiusi (CUG)](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/advanced/closed-user-groups.html?lang=it) possono accedere alla pagina e/o modificarla.

* [Aggiungere autorizzazioni](/help/sites-administering/user-group-ac-admin.md)
* [Modificare un gruppo utenti chiuso](/help/sites-administering/cug.md#applying-your-closed-user-group-to-content-pages)
* Visualizza le [autorizzazioni effettive](/help/sites-administering/user-group-ac-admin.md)

>[!CAUTION]
>
>La scheda **Autorizzazioni** consente di modificare le configurazioni CUG in base alla presenza del mixin `granite:AuthenticationRequired`. Se le autorizzazioni di pagina sono configurate utilizzando configurazioni CUG obsolete, in base alla presenza della proprietà `cq:cugEnabled`, viene visualizzato un messaggio di avviso e le autorizzazioni CUG non sono modificabili, né il requisito di autenticazione nella scheda [Avanzate](/help/sites-authoring/editing-page-properties.md#advanced) è modificabile.
>
>
>In tal caso, le autorizzazioni CUG devono essere modificate nell&#39;[interfaccia utente classica](/help/sites-classic-ui-authoring/classic-page-author-edit-page-properties.md).

>[!NOTE]
>
>La scheda Autorizzazioni non consente la creazione di gruppi CUG vuoti, che può essere utile come modo semplice per negare l’accesso a ogni utente. A questo scopo, è necessario utilizzare CRX Explorer. Per ulteriori informazioni, vedere il documento [Amministrazione diritti di accesso, utenti e gruppi](/help/sites-administering/user-group-ac-admin.md).

### Blueprint {#blueprint}

Questa scheda è visibile solo per le pagine che fungono da blueprint. Le blueprint fungono da base per le Live Copy e fanno parte della [Gestione multisito.](/help/sites-administering/msm.md)

* **Rollout** - Avvia il rollout del contenuto blueprint nelle Live Copy
* **Panoramica Live Copy** - Apre una finestra per sfogliare la struttura della pagina Live Copy
* **Live Copy correnti** - Elenco di pagine basate sulla pagina blueprint selezionata (ovvero Live Copy di)
* **Configurazione rollout** - Definisce la configurazione di rollout per la pagina

### Live Copy  {#live-copy}

Questa scheda è visibile solo per le pagine configurate come Live Copy. Come per [blueprint,](#blueprint) Live Copy fanno parte di [Gestione multisito.](/help/sites-administering/msm.md)

* **Sincronizza** - Sincronizza la Live Copy con la blueprint, mantenendo le modifiche locali
* **Ripristina** - Ripristina la Live Copy allo stato di blueprint, rimuovendo le modifiche locali
* **Sospendi** - Sospende la Live Copy da ulteriori modifiche di rollout
* **Scollega** - Scollega la Live Copy dalla blueprint

#### Sorgente {#source}

* Visualizza il percorso della blueprint per questa Live Copy

#### Stato {#status}

* Elenca lo stato attuale della Live Copy della pagina

#### Configurazione {#live-copy-config}

* **Ereditarietà Live Copy** - Se questa opzione è selezionata, la configurazione Live Copy ha effetto su tutti gli elementi figlio.
* **Eredita configurazioni di rollout dal padre** - Se selezionato, la configurazione di rollout viene ereditata dalla pagina padre.
* **Scegli configurazione di rollout**: definisce le circostanze in cui le modifiche vengono propagate dalla Blueprint e disponibili solo quando **Eredita configurazioni di rollout dall’elemento principale** non è selezionato
* **Elenco dei percorsi esclusi**

## Modifica delle proprietà di una pagina {#editing-page-properties-1}

Puoi definire le proprietà di pagina:

* Dalla console **Sites**:

   * [Creazione di una pagina](/help/sites-authoring/managing-pages.md#creating-a-new-page) (un sottoinsieme delle proprietà)

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

   ![schermata_shot_2018-03-22at095740](assets/screen_shot_2018-03-22at095740.png)

1. Seleziona **Apri proprietà** e viene visualizzata una finestra di dialogo che consente di modificare le proprietà, ordinate in base alla scheda appropriata. A destra della barra degli strumenti sono disponibili anche i seguenti pulsanti:

   * **Annulla**
   * **Salva e chiudi**

1. Usa il pulsante **Salva e chiudi** per salvare le modifiche.

### Dalla console Sites - Pagine multiple {#from-the-sites-console-multiple-pages}

Dalla console **Sites**, puoi selezionare più pagine e quindi utilizzare **Visualizza proprietà** per visualizzare e/o modificare le proprietà della pagina. Questa operazione viene definita bulk edit delle proprietà della pagina.

>[!NOTE]
>
>La modifica in blocco delle proprietà è disponibile anche per Assets. È simile, ma differisce in alcuni punti. Per ulteriori informazioni, vedere [Modifica delle proprietà di più Assets](/help/assets/metadata.md).
>
>È presente anche l&#39;[Bulk Editor](/help/sites-administering/bulk-editor.md). Questo editor consente di cercare contenuti da più pagine utilizzando GQL (Google Query Language), e quindi di modificarli direttamente utilizzando l’editor in blocco prima di salvare le modifiche apportate alle pagine originarie.

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
      * Quando il campo ha più valori (ad esempio Tag), questi vengono visualizzati solo se *tutti* sono comuni. Se solo alcune sono comuni, vengono visualizzate solo durante la modifica.

  Se non esiste nessuna proprietà con un valore comune, viene visualizzato un messaggio.

* **Modifica**

  Quando si modificano le proprietà di pagina per più pagine:

   * Puoi aggiornare i valori nei campi disponibili.

      * I nuovi valori vengono applicati a tutte le pagine selezionate quando selezioni **Fine**.
      * Quando il campo ha più valori (ad esempio Tag), puoi aggiungere un nuovo valore o rimuovere un valore comune.

   * I campi in comune, ma con valori diversi nelle varie pagine, sono indicati con un valore speciale, ad esempio il testo `<Mixed Entries>`.

>[!NOTE]
>
>Il componente Pagina può essere configurato in modo da specificare i campi disponibili per la modifica in serie. Consulta [Configurazione della pagina per la modifica in blocco delle proprietà di pagina](/help/sites-developing/bulk-editing.md).
