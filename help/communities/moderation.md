---
title: Console di moderazione
description: Scopri come amministratori e moderatori della community possono utilizzare la console di moderazione per accedere a tutti i contenuti UGC per i quali dispongono dell’autorizzazione a moderare.
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
docset: aem65
role: Admin
exl-id: 829da16a-4083-43c1-857d-f2666b363bfc
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '2028'
ht-degree: 2%

---

# Console di moderazione {#moderation-console}

In AEM Communities, in blocco [moderazione di contenuti community](/help/communities/moderate-ugc.md) è possibile dagli ambienti Author e Publish sia per gli amministratori che per i moderatori della community (membri della community attendibili assegnati come moderatori).

Anche gli amministratori e i moderatori della community possono eseguire [moderazione nel contesto](/help/communities/in-context.md) nell’ambiente di pubblicazione.

Una caratteristica di tutti [siti community](/help/communities/sites-console.md) è un `Administration` voce di menu disponibile per gli utenti che accedono con privilegi amministrativi. Il `Administration` fornisce l&#39;accesso alla console di moderazione.

Dalla console di moderazione, gli amministratori e i moderatori della community hanno accesso a tutti i contenuti generati dagli utenti (UGC) per i quali dispongono dell’autorizzazione alla moderazione. Se si consente di moderare più siti, è possibile visualizzare i post in tutti i siti o filtrare per comunità selezionate siti.

Per maggiori informazioni, visitare il sito [Gestione di utenti e gruppi di utenti](/help/communities/users.md).

La console Moderazione supporta:

* Esecuzione in blocco di attività di moderazione.
* Ricerca UGC.
* Visualizzazione dei dettagli UGC.
* Visualizzazione dei dettagli dell’autore UGC.

Solo quando si esegue l&#39;accesso come amministratore o membro con ` [moderator permissions](/help/communities/in-context.md#identifyingtrustedmembers)`, possono essere eseguite attività di moderazione.

## Accesso all’ambiente di pubblicazione {#publish-environment-access}

L&#39;accesso alla console di moderazione da un sito community pubblicato avviene tramite un collegamento Amministrazione che viene visualizzato quando un moderatore della community ha effettuato l&#39;accesso.

![publishweretail](assets/publishweretail.png)

Selezionando il collegamento Amministrazione, viene visualizzata la console Moderazione:

![moderation-console-publish](assets/moderation-console-publish.png)

## Accesso all’ambiente di authoring {#author-environment-access}

Nell’ambiente di authoring, per raggiungere la console di moderazione

* Dalla navigazione globale, seleziona **[!UICONTROL Community]** > **[!UICONTROL Moderazione]**.

Solo quando si esegue l&#39;accesso come amministratore o come membro con [autorizzazioni moderatore](/help/communities/in-context.md#identifyingtrustedmembers), è possibile eseguire attività di moderazione. L&#39;unico contenuto della community visualizzato è quello che il membro connesso può moderare.

>[!NOTE]
>
>UGC dall’ambiente di pubblicazione è visibile nell’ambiente di authoring solo se l’SRP scelto implementa un archivio comune. Ad esempio, per impostazione predefinita l’archiviazione è JSRP, che non è un archivio comune per Author e Publish. Consulta [Archiviazione contenuti community](/help/communities/working-with-srp.md).

![moderationconsole author](assets/moderationconsoleauthor.png)

## Interfaccia utente console di moderazione {#moderation-console-ui}

Lasciando da parte la barra di navigazione a sinistra (che appare nell&#39;ambiente di authoring ma non in quello di pubblicazione), l&#39;interfaccia utente di moderazione presenta le seguenti aree principali:

* **[Barra di navigazione superiore](#top-navigation-bar)**
* **[Barra degli strumenti](#toolbar)**
* **[Area contenuto](#content-area)**

### Barra di navigazione superiore {#top-navigation-bar}

La barra di navigazione superiore è costante per tutte le console. Per ulteriori informazioni, consulta [Operazioni di base](/help/sites-authoring/basic-handling.md).

### Barra degli strumenti {#toolbar}

La barra degli strumenti, situata sotto la barra di navigazione superiore, fornisce il seguente interruttore a sinistra:

* [Barra dei filtri](/help/communities/moderation.md#filterrail)
apre una barra che consente di scegliere le proprietà su cui filtrare il contenuto.

La barra degli strumenti, situata sotto la barra di navigazione superiore, fornisce il seguente interruttore a sinistra:

![interruttore](assets/toggleswitch.png)

[Barra dei filtri](/help/communities/moderation.md#filterrail)
apre una barra su selezione Ricerca, che consente di scegliere le proprietà su cui filtrare il contenuto.

![filterrail](assets/filterrail.png)

### Area contenuto {#content-area}

L’area del contenuto contiene informazioni per UGC pubblicati:

* UGC pubblicato
* Nome membro
* Avatar membro
* Posizione del posto
* Quando è stato pubblicato
* Numero di risposte al post
* [Sentimento](/help/communities/moderate-ugc.md#sentiment) associato al post
* Se approvata, viene visualizzato un segno di spunta
* Se è presente un allegato, viene visualizzata una graffetta

>[!NOTE]
> 
>L&#39;area dei contenuti include *scorrimento infinito*, il che significa che ti consente di continuare a scorrere fino a quando non raggiungi la fine del contenuto. La barra degli strumenti rimane in una posizione fissa visibile sopra l’area del contenuto anche durante lo scorrimento.

### Barra di filtro {#ootbfilters}

![open-filterrail](assets/open-filterrail.png)

L’icona del pannello laterale apre la barra del filtro. La barra dei filtri, visualizzata a sinistra dell’area del contenuto, fornisce diversi filtri, ciascuno dei quali ha un effetto immediato sull’UGC di riferimento visualizzato nell’area del contenuto.

I filtri all’interno di ogni categoria sono **OPPURE**&#39;d insieme, e i filtri in diverse categorie sono **E** Io andavo insieme.

Ad esempio, se selezioni entrambi **Domanda** e **Risposta**, è possibile visualizzare contenuti che possono essere **Domanda** *o* un **Risposta**.

Tuttavia, se selezioni **Domanda** e **In sospeso**, puoi visualizzare solo il contenuto che è un **Domanda** ed è **In sospeso**.

>[!NOTE]
>
>I moderatori della community possono applicare un segnalibro ai filtri predefiniti nell’interfaccia utente della console di moderazione. Poiché questi filtri vengono aggiunti alla fine dell’URL (come parametri della stringa di query), i moderatori possono tornare ai filtri con segnalibro in un secondo momento e condividere questi collegamenti.

![searchicon](assets/searchicon.png)

Quando la barra dei filtri è aperta, l’icona Ricerca attiva e disattiva la visualizzazione del pannello laterale. Tuttavia, per chiudere la barra dei filtri e visualizzare solo il contenuto generato dall’utente, fai clic sull’icona Ricerca e seleziona l’opzione Solo contenuto.

#### Percorso contenuto {#content-path}

Il Percorso contenuto limita il riferimento UGC visualizzato ai post presenti nell’archivio dei contenuti specificato.

![content-path](assets/content-path.png)

#### Ricerca di testo {#text-search}

La ricerca di testo limita l’UGC di riferimento visualizzato ai post che contengono il testo immesso.

![text-search](assets/text-search.png)

#### Sito {#site}

Il sito limita il contenuto UGC di riferimento visualizzato ai post per i siti community selezionati. Se non è selezionato alcun sito, vengono visualizzati tutti i riferimenti a UGC.

![site-panel](assets/site-panel.png)

>[!NOTE]
>
>Quando un amministratore accede alla console di moderazione in blocco, vengono visualizzati tutti i riferimenti a UGC, inclusi i siti non creati con [creazione guidata sito](/help/communities/sites-console.md), ad esempio i campioni di Geometrixx.
>
>Quando un membro attendibile della community accede alla console di moderazione in blocco al momento della pubblicazione, vengono visualizzati solo i riferimenti a contenuti generati dagli utenti per i siti della community che il membro è autorizzato a moderare. Inoltre, può essere filtrato con il filtro Sito.

#### Tipo di contenuto {#content-type}

Il tipo di contenuto limita il contenuto UGC di riferimento visualizzato ai post del tipo di risorsa selezionato. È possibile selezionare uno o più dei seguenti tipi. Se non è selezionata alcuna opzione, vengono visualizzati tutti i tipi.

* **Commento**
* **Argomento forum**
* **Risposta forum**
* **Domanda D/R**
* **Risposta D/R**
* **Articolo di blog**
* **Commento blog**
* **Evento calendario**
* **Commento calendario**
* **Cartella libreria file**
* **Documento libreria file**
* **Idea**
* **Commento ideazione**

![content-types](assets/content-types.png)

#### Tipi di contenuto aggiuntivi {#additional-content-types}

Per aggiungere altre risorse da filtrare:

* Accedi all’istanza di authoring come amministratore.
* Apri [Console web](https://localhost:4502/system/console/configMgr).
* Individua `AEM Communities Moderation Dashboard Filters`.
* Seleziona la configurazione per aprirla in modalità di modifica.
* Immettere il ResourceType di un componente su cui filtrare:

   * Ad esempio, per filtrare in base ai componenti di voto inclusi, immettere:

     `Voting=social/tally/components/hbs/voting`

  ![additional-contenttype](assets/additional-contenttype.png)

* Seleziona Salva.
* Aggiorna la console Community - Moderazione.

Il risultato è un nuovo filtro selezionabile per `Voting` sotto `Content Type` gruppo di filtri.

Quando questo filtro è selezionato, il contenuto del dashboard mostra contenuti generati dagli utenti (UGC, User-Generated Content) che corrispondono a qualsiasi tipo di ResourceTypes immesso.

#### Stato {#status}

Lo stato limita il UGC di riferimento visualizzato ai post dello stato selezionato, che possono essere uno o più dei seguenti: In sospeso, Approvato, Negato o Chiuso, Bozza o Pianificato per articoli di blog e Risposte o Non risposte per domande di controllo qualità. Se non è selezionato nessuno, vengono visualizzati tutti.

>[!NOTE]
>
>Se viene selezionato solo lo stato Senza risposta, il moderatore visualizza tutto il contenuto (per tutti i tipi di contenuto) tranne le domande a cui è stato risposto. È così perché la proprietà responsabile della domanda non esiste se ci sono domande senza risposta e altri contenuti come l&#39;argomento del forum, l&#39;articolo del blog o i commenti.

![stati](assets/statuses.png)

#### Segnalazione {#flagging}

I flag limitano il contenuto UGC di riferimento visualizzato ai post contrassegnati o nascosti.

Una volta contrassegnato, un contenuto rimane contrassegnato fino a quando non lo si scontra selezionando il **Contrassegno** ancora una volta. Non esistono livelli di segnalazione, ad esempio importante o di follow-up.

![segnalazione](assets/flagging.png)

#### Membri {#members}

I membri limitano l&#39;UGC di riferimento visualizzato all&#39;UGC pubblicato in base al nome membro immesso.

![membri](assets/members.png)

#### Pubblicato nell&#39;ultimo/a {#posted-in-the-last}

Pubblicato in L&#39;ultimo limita il UGC di riferimento visualizzato ai post effettuati nell&#39;ultima ora, giorno, settimana, mese o anno.

![postato-ultimo](assets/posted-last.png)

#### Sentimento {#sentiment}

[Sentimento](/help/communities/moderate-ugc.md#sentiment) limita il contenuto UGC di riferimento visualizzato ai post con un valore di valutazione positivo, negativo o neutro.

![sentiment](assets/sentiment.png)

## Filtri personalizzati {#custom-filters}

A parte i filtri predefiniti in [Barra di filtro](/help/communities/moderation.md#ootbfilters), è possibile aggiungere all&#39;interfaccia utente di moderazione ulteriori filtri personalizzati sui metadati. Gli sviluppatori possono utilizzare il codice di esempio in GitHub per estendere i filtri dell&#39;interfaccia utente di moderazione esistenti.

![custom-tag-filter](assets/custom-tag-filter.png)

Il [progetto di esempio](https://github.com/Adobe-Marketing-Cloud/aem-communities-extensions/tree/main/aem-communities-moderation-filter) su GitHub implementa il filtro Tag, per filtrare l’elenco UGC in base al fatto che i tag specifici vengano applicati o meno a contenuti generati dall’utente. Puoi seguire il codice di esempio e creare filtri analoghi per altri campi di metadati UGC simili.

Per installare l’esempio per il filtro Tag:

1. Apri Gestione pacchetti in AEM Author (`https://[aem-author]:4502/crx/packmgr/index.jsp`) e pubblicazione AEM (`https://[aem-publish]:4503/crx/packmgr/index.jsp`).
1. Creare il pacchetto `com.adobe.social.sample.moderation.filter.ui.apps-1.0-SNAPSHOT.zip` dal codice GitHub, e installarlo e abilitarlo.
1. Apri la console dei bundle in AEM Author ( `https://[aem-author]:4502/system/console/bundles`) e pubblicazione AEM ( `https://[aem-publish]:4503/system/console/bundles`).
1. Creare il pacchetto (`[com](https://sample-moderation-filter.com/).adobe.social.sample.moderation.filter.core-1.0-SNAPSHOT.jar`) da GitHub, e installarlo e abilitarlo.
1. Vai a **/apps/social/moderation/facets** node su AEM Author (`https://[aem-author]:4502/crx/de/index.jsp#/apps/social/moderation/facets`) e pubblicazione AEM (`https://[aem-publish]:4502/crx/de/index.jsp#/apps/social/moderation/facets`).
1. Aggiungere un utente tecnico **community-utility-reader** con `jcr:read` autorizzazioni.

Per esporre i filtri personalizzati sui siti community esistenti:

1. Modifica `Clientlibs` della pagina di moderazione esistente `/content/we-retail/us/en/community/moderation/shell3/jcr:content/head/clientlibs.`

   * Aggiungi nuova categoria `cq.social.hbs.moderation.v2.`

1. Vai a `/content/we-retail/us/en/community/moderation/shell3/jcr:content/rails/searchWell/items/filters.`

   * Imposta su nuovo componente `sling:resourceType = social/moderation/v2/filters.`

1. Passa a `/content/we-retail/us/en/community/moderation/shell3/jcr:content/views/content/items/modcontainer`.

   * Imposta su nuovo componente `sling:resourceType = social/moderation/v2/modcontainer`.

## Azioni di moderazione {#moderation-actions}

[Azioni di moderazione](/help/communities/moderate-ugc.md#moderation-actions) può essere eseguita su una o più selezioni effettuate nell’area del contenuto o durante la visualizzazione dei dettagli del contenuto.

Per moderare in blocco i post, nell’area del contenuto fai clic su Seleziona (![selettore](assets/selecticon.png)) su un post, che appare quando ci si passa sopra con il mouse (desktop) o premendo e tenendo premuto un dito sul post (mobile). In questo modo, si entra nella modalità di selezione multipla e ora è possibile selezionare i post successivi da moderare in blocco semplicemente facendo clic su di essi. Utilizza i pulsanti visualizzati nella barra degli strumenti per eseguire azioni di moderazione sui post selezionati. Tutte le azioni richiedono conferma.

Per moderare un singolo post nell’area dei contenuti, posiziona il cursore su di esso con il mouse (desktop) oppure tieni premuto un dito sul post (mobile) in modo che vengano visualizzati i pulsanti sul post. Quando si opera su un singolo dettaglio di contenuto, solo un’azione di eliminazione richiede una conferma.

### Moderazione di più post {#moderating-multiple-posts}

Entra nella modalità di selezione collettiva facendo clic sul pulsante `Select` icona in un post:

![select-icon](assets/select-icon.png)

Per uscire dalla modalità di selezione collettiva, seleziona l’icona Annulla (x) sulla barra degli strumenti:

Le azioni di moderazione che possono essere eseguite su più post sono:

* Rifiuta
* Eliminare
* Chiudi/riapri i post

Le icone che consentono queste azioni vengono visualizzate sulla barra degli strumenti solo quando sono selezionati più post.

![bulkmoderato](assets/bulkmoderate.png)

### Moderazione di un singolo post {#moderating-a-single-post}

Nella modalità di selezione singola, è possibile:

* Visualizzare i dettagli utente selezionando il nome dell&#39;utente.
* Visualizza il post nel contesto selezionando il collegamento al post.
* [Risposta](#reply)
* [Consenti](#allow)
* [Rifiuta](#deny)
* [Eliminare](#delete)
* [Chiudi](#close)
* Visualizza [Cronologia moderazione](#moderation-history)
* [Visualizza dettagli](#viewdetails)

Nella visualizzazione a schede, sopra le icone delle azioni di moderazione, è presente il testo del post e qui sotto sono riportati i dati che indicano:

* In caso di risposte, precedute dal numero di risposte
* Se è stato segnalato
* Se è stato approvato
* Quando è stato pubblicato l’UGC

![singleselectmode](assets/singleselectmode.png)

#### Risposta {#reply}

![rispondi](assets/reply.png)

Quando si lavora con un singolo post, viene visualizzata un’icona Rispondi se il tipo UGC supporta le risposte ed è configurato per consentire le risposte.

#### Consenti {#allow}

![allow](assets/allow.png)

Quando si lavora con un singolo post, l’icona Consenti viene visualizzata se il post è stato contrassegnato o negato. Se contrassegnato, selezionando Consenti tutti i contrassegni vengono cancellati.

#### Rifiuta {#deny}

![rifiuta](assets/deny.png)

Il **Rifiuta** l&#39;azione di moderazione è disponibile solo per il contenuto moderato e non viene visualizzato su contenuto non moderato, tranne che nella modalità di selezione multipla.

Il contenuto non moderato viene sempre approvato.

Il contenuto moderato entra inizialmente nello stato In sospeso e può essere modificato in un secondo momento per l&#39;approvazione o la negazione.

Il contenuto che lascia lo stato in sospeso non può mai tornare a uno stato in sospeso. Il contenuto contrassegnato come approvato o negato può essere modificato in un altro stato in qualsiasi momento.

#### Eliminare {#delete}

![eliminare](assets/delete.png)

In modalità di selezione singola o in modalità collettiva, è possibile selezionare gli elementi ed eliminarli. L’azione Elimina genera una finestra di dialogo di conferma. Una volta eliminati, gli elementi scompaiono immediatamente dall’area del contenuto. **Una volta eliminato, l’UGC viene rimosso definitivamente dall’archivio e non può essere recuperato in un secondo momento**.

#### Chiudi {#close}

![chiudi](assets/close.png)

Quando si lavora con un singolo post, viene visualizzata un’icona Chiudi se il tipo di UGC supporta la possibilità di impedire ulteriori post per tale risorsa.

#### Cronologia moderazione {#moderation-history}

![moderazione](assets/moderation.png)

Quando si lavora con un singolo post, viene visualizzata un&#39;icona Cronologia moderazione al passaggio del mouse su di esso. Selezionando l’icona viene visualizzato un riquadro contenente una cronologia delle azioni eseguite in relazione al post UGC.

Per tornare alla visualizzazione dell&#39;area del contenuto di più post UGC, seleziona la X nell&#39;angolo in alto a destra del riquadro dei dettagli della visualizzazione.

Ad esempio:

![moderation-history](assets/moderation-history.png)

#### Visualizza dettagli {#view-detail}

![visualizza](assets/view.png)

Quando si lavora con un singolo post, è possibile visualizzare più dettagli aprendo l’UGC in modalità dettaglio.

A questo scopo, passa il cursore del mouse sul post per visualizzare `View Detail` e selezionarla per visualizzare un pannello contenente ulteriori dettagli sul post.

Per tornare alla visualizzazione dell&#39;area del contenuto di più post UGC, seleziona la X nell&#39;angolo in alto a destra del riquadro dei dettagli della visualizzazione.

Ad esempio:

![view1](assets/view1.png)
