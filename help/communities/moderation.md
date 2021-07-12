---
title: Console di moderazione
seo-title: Console di moderazione
description: Accesso alla console Moderazione
seo-description: Accesso alla console Moderazione
uuid: d3b8a160-85b2-43f4-9891-5fafa8c48c5f
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 404582ab-bb4c-4775-9ae3-17356d376dca
docset: aem65
role: Admin
exl-id: 829da16a-4083-43c1-857d-f2666b363bfc
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '2110'
ht-degree: 4%

---

# Console di moderazione {#moderation-console}

In AEM Communities, la moderazione [bulk dei contenuti della community](/help/communities/moderate-ugc.md) è possibile sia dall&#39;ambiente di authoring che da quello di pubblicazione da parte di amministratori e moderatori della community (membri affidabili della community assegnati come moderatori).

Gli amministratori e i moderatori della community possono anche eseguire [la moderazione nel contesto](/help/communities/in-context.md) nell&#39;ambiente di pubblicazione.

Una funzione di tutti i [siti della community](/help/communities/sites-console.md) è una voce di menu `Administration` disponibile per gli utenti che accedono con privilegi amministrativi. Il collegamento `Administration` consente di accedere alla console Moderazione .

Dalla console Moderazione, gli amministratori e i moderatori della community avranno accesso a tutti i contenuti generati dagli utenti (UGC) per i quali dispongono dell’autorizzazione per moderare. Se è consentito moderare più siti, è possibile visualizzare i post in tutti i siti o filtrare in base a siti di comunità selezionati.

Per informazioni più dettagliate, visita [Gestione di utenti e gruppi di utenti](/help/communities/users.md).

La console Moderazione supporta:

* Esecuzione in blocco di attività di moderazione.
* Ricerca in UGC.
* Visualizzazione dei dettagli UGC.
* Visualizzazione dei dettagli dell’autore UGC.

È possibile eseguire attività di moderazione solo quando si effettua l’accesso come amministratore o come membro con ` [moderator permissions](/help/communities/in-context.md#identifyingtrustedmembers)`.

## Accesso all&#39;ambiente di pubblicazione {#publish-environment-access}

L&#39;accesso alla console di moderazione da un sito community pubblicato avviene tramite un collegamento Amministrazione visualizzato all&#39;accesso di un moderatore della community.

![publishweretail](assets/publishweretail.png)

Selezionando il collegamento Amministrazione, viene visualizzata la console Moderazione :

![moderation-console-publish](assets/moderation-console-publish.png)

## Accesso all’ambiente di authoring {#author-environment-access}

Nell’ambiente di authoring, per raggiungere la console Moderazione

* Dalla navigazione globale, seleziona **[!UICONTROL Communities]** > **[!UICONTROL Moderazione]**.

Solo quando si effettua l&#39;accesso come amministratore o come membro con [autorizzazioni del moderatore](/help/communities/in-context.md#identifyingtrustedmembers), è possibile eseguire attività di moderazione. L&#39;unico contenuto della community visualizzato è quello che il membro connesso può moderare.

>[!NOTE]
>
>L’UGC dell’ambiente di pubblicazione sarà visibile sull’autore solo se l’SRP scelto implementa un archivio comune. Ad esempio, per impostazione predefinita l’archiviazione è JSRP, che non è un negozio comune per l’authoring e la pubblicazione. Consulta [Archiviazione dei contenuti della community](/help/communities/working-with-srp.md).

![moderationconsoleauthor](assets/moderationconsoleauthor.png)

## Interfaccia utente della console di moderazione {#moderation-console-ui}

Se si imposta la barra di navigazione a sinistra (che viene visualizzata sull’autore ma non sulla pubblicazione), l’interfaccia utente di moderazione presenta le seguenti aree principali:

* **[Barra di navigazione superiore](#top-navigation-bar)**
* **[Barra degli strumenti](#toolbar)**
* **[Area di contenuto](#content-area)**

### Barra di navigazione superiore {#top-navigation-bar}

La barra di navigazione superiore è costante per tutte le console. Per ulteriori informazioni, vedere [Operazioni di base](/help/sites-authoring/basic-handling.md).

### Barra degli strumenti {#toolbar}

La barra degli strumenti, situata sotto la barra di navigazione superiore, fornisce il seguente interruttore a sinistra:

* [La barra ](/help/communities/moderation.md#filterrail)
Filtro apre una barra che consente di scegliere le proprietà su cui filtrare il contenuto.

La barra degli strumenti, situata sotto la barra di navigazione superiore, fornisce il seguente interruttore a sinistra:

![toggleswitch](assets/toggleswitch.png)

[Filtro apre una barra ](/help/communities/moderation.md#filterrail)
a sinistra, selezionando Ricerca , che consente di scegliere le proprietà su cui filtrare il contenuto.

![filatoio](assets/filterrail.png)

### Area contenuto {#content-area}

L&#39;area contenuto contiene informazioni per gli UGC pubblicati:

* UGC pubblicato
* Nome membro
* Avatar membro
* Posizione del post.
* Quando è stato pubblicato.
* Numero di risposte al post.
* [](/help/communities/moderate-ugc.md#sentiment) Sentimentale associato al post
* Se approvato, viene visualizzato un segno di spunta.
* Se è presente un allegato, viene visualizzato un fermacarte.

>[!NOTE]
> 
>L’area contenuto presenta un *scorrimento infinito*, che consente di continuare lo scorrimento fino alla fine del contenuto. La barra degli strumenti rimane in una posizione fissa e visibile sopra l’area contenuto anche durante lo scorrimento.

### Barra Filtro {#ootbfilters}

![binario aperto](assets/open-filterrail.png)

L’icona del pannello laterale apre la barra del filtro. La barra del filtro, visualizzata a sinistra dell’area contenuto, fornisce filtri diversi, ciascuno dei quali ha un effetto immediato sull’UGC di riferimento visualizzato nell’area contenuto.

I filtri all’interno di ciascuna categoria sono **OR**’d insieme e i filtri di diverse categorie sono **AND** insieme.

Ad esempio, se controlli sia **Domanda** che **Risposta**, vedrai il contenuto che è un **Domanda** *o* un **Risposta**.

Tuttavia, se controlli **Domanda** e **In sospeso**, vedrai solo il contenuto che è una **Domanda** ed è **In sospeso**.

>[!NOTE]
>
>I moderatori della community possono aggiungere ai segnalibri i filtri predefiniti nell’interfaccia utente della console di moderazione. Man mano che questi filtri vengono aggiunti alla fine dell&#39;URL (come parametri della stringa di query), i moderatori possono tornare ai filtri con segnalibro in un secondo momento e anche condividere questi collegamenti.

![searchicon](assets/searchicon.png)

Quando la barra del filtro è aperta, l’icona Ricerca disattiva il pannello laterale chiuso. Tuttavia, per chiudere la barra del filtro e visualizzare solo il contenuto generato dall’utente, fai clic sull’icona Ricerca e seleziona l’opzione Solo contenuto .

#### Percorso contenuto {#content-path}

Percorso contenuto limita l’UGC di riferimento visualizzato ai post inseriti nell’archivio dei contenuti specificato.

![content-path](assets/content-path.png)

#### Ricerca di testo {#text-search}

La ricerca del testo limita l’UGC di riferimento visualizzato ai post contenenti il testo inserito.

![ricerca di testo](assets/text-search.png)

#### Sito {#site}

Il sito limita l&#39;UGC di riferimento visualizzato ai post a siti della community selezionati. Se non è selezionato alcun sito, vengono visualizzati tutti i riferimenti a UGC.

![pannello del sito](assets/site-panel.png)

>[!NOTE]
>
>Quando un amministratore accede alla console di moderazione in blocco, vengono visualizzati tutti i riferimenti a UGC, inclusi i siti non creati con la [procedura guidata di creazione del sito](/help/communities/sites-console.md), ad esempio gli esempi di Geometrixx.
>
>Quando si accede alla console di moderazione di massa al momento della pubblicazione da parte di un membro di una community fidato, vengono visualizzati solo i riferimenti a UGC creati per i siti della community in cui il membro è autorizzato a moderare e possono essere filtrati con il filtro Sito.

#### Tipo di contenuto {#content-type}

Il tipo di contenuto limita l’UGC a cui si fa riferimento ai post del tipo di risorsa selezionato. È possibile selezionare uno o più dei seguenti tipi. Se non è selezionata alcuna opzione, vengono visualizzati tutti i tipi.

* **Commento**
* **Topic forum**
* **Risposta forum**
* **Domanda d/r**
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

Per aggiungere ulteriori risorse su cui filtrare:

* Accedi all’istanza di authoring come amministratore.
* Apri [Console web](https://localhost:4502/system/console/configMgr).
* Individua `AEM Communities Moderation Dashboard Filters`.
* Seleziona la configurazione da aprire in modalità di modifica.
* Immettere il ResourceType di un componente su cui filtrare:

   * Ad esempio, per filtrare i componenti inclusi per la votazione, immetti:

      `Voting=social/tally/components/hbs/voting`
   ![tipo di contenuto aggiuntivo](assets/additional-contenttype.png)

* Seleziona Salva.
* Aggiorna la console Community - Moderazione .

Il risultato è un nuovo filtro selezionabile per `Voting` nel gruppo di filtri `Content Type`.

Quando quel filtro è selezionato, il contenuto del dashboard mostrerà UGC che corrisponde a uno qualsiasi dei Tipi di risorse inseriti.

#### Stato {#status}

Lo stato limita l&#39;UGC di riferimento visualizzato ai post dello stato selezionato, che può essere uno o più di In sospeso, Approvato, Rifiutato o Chiuso, nonché Bozza o Pianificato per gli articoli di blog, e ha risposto o meno alle domande di QnA. Se non è selezionato nessuno, vengono visualizzati tutti.

>[!NOTE]
>
>Se è selezionato solo lo stato Non risposto, il moderatore visualizzerà tutti i contenuti (per tutti i tipi di contenuto) tranne le domande ricevute. Questo perché la proprietà responsabile della domanda con risposta non esiste nel caso di domande senza risposta e altri contenuti come l&#39;argomento del forum, l&#39;articolo del blog o i commenti.

![stati](assets/statuses.png)

#### Segnalazione {#flagging}

L’evidenziazione limita l’UGC a cui si fa riferimento ai post contrassegnati o nascosti.

Una volta che un contenuto è stato contrassegnato, rimane contrassegnato finché non si annulla l’flag di quel singolo contenuto selezionando nuovamente il pulsante **Flag**. Non esistono livelli di contrassegno, ad esempio importanti o di follow-up.

![contrazione](assets/flagging.png)

#### Membri {#members}

I membri limitano l&#39;UGC di riferimento visualizzato a UGC pubblicato dal nome membro inserito.

![membri](assets/members.png)

#### Pubblicato nell&#39;ultimo/a {#posted-in-the-last}

Posted In the Last limita l’UGC a cui si fa riferimento ai post effettuati nell’ultima ora, giorno, settimana, mese o anno.

![postlast](assets/posted-last.png)

#### Sentimento {#sentiment}

[](/help/communities/moderate-ugc.md#sentiment) Sentimentals limita l&#39;UGC a cui si fa riferimento ai post con un valore del sentiment che è positivo, negativo o neutro.

![sentimento](assets/sentiment.png)

## Filtri personalizzati {#custom-filters}

Oltre ai filtri preconfigurati in [Barra dei filtri](/help/communities/moderation.md#ootbfilters), è possibile aggiungere altri filtri personalizzati sui metadati all&#39;interfaccia utente di moderazione. Gli sviluppatori possono utilizzare il codice di esempio in Github per estendere i filtri esistenti dell’interfaccia utente di moderazione.

![custom-tag-filter](assets/custom-tag-filter.png)

Il [progetto di esempio](https://github.com/Adobe-Marketing-Cloud/aem-communities-extensions/tree/main/aem-communities-moderation-filter) su Github implementa il filtro tag, per filtrare l’elenco UGC in base al fatto che i tag specifici siano applicati o meno al contenuto generato dall’utente. Puoi seguire il codice di esempio e creare filtri analoghi per altri campi di metadati UGC simili.

Per installare l’esempio per il filtro Tag:

1. Apri il gestore dei pacchetti sull&#39;istanza di AEM Author ([https://[aem-author]:4502/crx/packmgr/index.jsp](https://aem65-communities-demo.corp.adobe.com:4502/crx/packmgr/index.jsp)) e di AEM Publish ([https://[aem-publish]:4503/crx/packmgr/index.jsp](https://aem65-communities-demo.corp.adobe.com:4502/crx/packmgr/index.jsp)).
1. Crea il pacchetto `com.adobe.social.sample.moderation.filter.ui.apps-1.0-SNAPSHOT.zip` dal codice Github, quindi installa e abilita lo stesso.
1. Apri la console dei bundle sull’istanza di AEM Author ( `https://[aem-author]:4502/system/console/bundles`) e l’istanza di AEM Publish ( `https://[aem-publish]:4503/system/console/bundles`).
1. Crea il pacchetto ` [com](https://sample-moderation-filter.com/).adobe.social.sample.moderation.filter.core-1.0-SNAPSHOT.jar` da Github, quindi installa e abilita lo stesso.
1. Vai al nodo **/apps/social/moderation/facets** su AEM Author ([https://[aem-author]:4502/crx/de/index.jsp#/apps/social/moderation/facets](https://aem65-communities-demo.corp.adobe.com:4502/crx/de/index.jsp#/apps/social/moderation/facets)) e AEM Publish ([https://[aem-publish]:4502/crx/de/index.jsp#/apps/social/moderation/facets](https://aem65-communities-demo.corp.adobe.com:4502/crx/de/index.jsp#/apps/social/moderation/facets)).
1. Aggiungi un utente tecnico **communities-utility-reader** con le autorizzazioni `jcr:read`.

Per esporre i filtri personalizzati sui siti community esistenti:

1. Modifica `Clientlibs` della pagina di moderazione esistente `/content/we-retail/us/en/community/moderation/shell3/jcr:content/head/clientlibs.`

   * Aggiungi nuova categoria `cq.social.hbs.moderation.v2.`

1. Passa a `/content/we-retail/us/en/community/moderation/shell3/jcr:content/rails/searchWell/items/filters.`

   * Imposta sul nuovo componente `sling:resourceType = social/moderation/v2/filters.`

1. Passa a `/content/we-retail/us/en/community/moderation/shell3/jcr:content/views/content/items/modcontainer`.

   * Imposta sul nuovo componente `sling:resourceType = social/moderation/v2/modcontainer`.

## Azioni di moderazione {#moderation-actions}

[Le ](/help/communities/moderate-ugc.md#moderation-actions) azioni di moderazione possono essere eseguite su una o più selezioni effettuate nell’area contenuto o durante la visualizzazione dei dettagli del contenuto.

Per moderare in massa i post, nell&#39;area del contenuto fai clic sull&#39;icona Seleziona (![selezione](assets/selecticon.png)) su un post, che compare quando passi il mouse su di esso (desktop) o premi e tieni premuto un dito sul post (mobile). A questo scopo, accedi alla modalità di selezione multipla e ora puoi selezionare i post successivi da moderare in massa semplicemente facendo clic su di essi. Utilizzare i pulsanti visualizzati sulla barra degli strumenti per eseguire azioni di moderazione sui post selezionati. Tutte le azioni richiederanno una conferma.

Per moderare un singolo post nell’area contenuto, posiziona il cursore del mouse su di esso (desktop) o tieni premuto un dito sulla postazione (mobile) in modo che i pulsanti vengano visualizzati sulla postazione. Quando si utilizza un singolo dettaglio di contenuto, viene richiesta la conferma solo per un’azione di eliminazione.

### Moderazione di più post {#moderating-multiple-posts}

Attiva la modalità di selezione collettiva facendo clic sull&#39;icona `Select` su un post:

![select-icon](assets/select-icon.png)

Per uscire dalla modalità di selezione in blocco, seleziona l’icona Annulla (x) sulla barra degli strumenti:

Le azioni di moderazione che possono essere eseguite su più post sono:

* Rifiuta
* Elimina
* Chiudi/riapri i post

Le icone che consentono di eseguire queste operazioni vengono visualizzate sulla barra degli strumenti solo se sono selezionati più post.

![bulkmoderato](assets/bulkmoderate.png)

### Moderazione di un singolo post {#moderating-a-single-post}

In modalità di selezione singola è possibile:

* Visualizzare i dettagli utente selezionando il nome dell’utente.
* Per visualizzare il post nel contesto, seleziona il collegamento al post.
* [Risposta](#reply)
* [Consenti](#allow)
* [Rifiuta](#deny)
* [Elimina](#delete)
* [Chiudi](#close)
* Visualizza [Cronologia moderazione](#moderation-history)
* [Visualizza dettagli](#viewdetails)

Nella vista a schede sopra le icone delle azioni di moderazione è presente il testo del post e sotto sono riportati i dati che indicano:

* In caso di risposta e in caso affermativo, preceduta dal numero di risposte.
* Se è stato contrassegnato.
* Se è stato approvato.
* Quando è stato pubblicato l&#39;UGC.

![modalità singleselectmode](assets/singleselectmode.png)

#### Risposta {#reply}

![rispondere](assets/reply.png)

Quando si lavora con un singolo post, viene visualizzata un’icona Risposta se il tipo UGC supporta le risposte e è configurato per consentire le risposte.

#### Consenti {#allow}

![consenti](assets/allow.png)

Quando si lavora con un singolo post, l&#39;icona Consenti viene visualizzata quando il post è stato contrassegnato o negato. Se contrassegnato, selezionando Consenti verranno cancellati tutti i flag.

#### Rifiuta {#deny}

![rifiuta](assets/deny.png)

L’azione di moderazione **Rifiuta** è disponibile solo per i contenuti sottoposti a moderazione e non viene visualizzata su contenuti non moderati, tranne in modalità di selezione multipla.

Il contenuto non moderato viene sempre approvato.

Il contenuto moderato inizialmente entra in uno stato In sospeso e può essere successivamente modificato per essere approvato o negato.

Il contenuto che lascia lo stato in sospeso non può mai tornare a uno stato in sospeso. I contenuti contrassegnati come approvati o negati possono essere modificati in uno stato diverso in qualsiasi momento.

#### Elimina {#delete}

![delete](assets/delete.png)

In modalità di selezione singola o in modalità collettiva, puoi selezionare gli elementi ed eliminarli. L’azione di eliminazione si traduce in una finestra di dialogo di conferma. Una volta eliminati, tali elementi scompaiono immediatamente dall’area contenuto. **Una volta eliminato, l’UGC viene rimosso definitivamente dall’archivio e non può essere recuperato** in un secondo momento.

#### Chiudi {#close}

![chiudi](assets/close.png)

Quando si lavora con un singolo post, viene visualizzata un’icona Chiudi se il tipo UGC supporta la capacità di impedire ulteriori post per quella risorsa.

#### Cronologia moderazione {#moderation-history}

![moderazione](assets/moderation.png)

Quando si lavora con un singolo post, quando si passa il mouse su di esso viene visualizzata un’icona Cronologia moderazioni . Quando si seleziona l’icona, viene visualizzato un riquadro contenente una cronologia delle azioni eseguite relative al post UGC.

Per tornare alla visualizzazione dell’area contenuto di più post UGC, seleziona la X nell’angolo in alto a destra del riquadro dei dettagli della visualizzazione.

Esempio:

![moderazione](assets/moderation-history.png)

#### Visualizza dettagli {#view-detail}

![visualizzare](assets/view.png)

Quando si lavora con un singolo post, è possibile visualizzare più dettagli aprendo l&#39;UGC in modalità dettagliata.

A questo scopo, passa il cursore del mouse sul post per visualizzare l&#39;icona `View Detail` e selezionala per visualizzare un pannello contenente ulteriori dettagli sul post.

Per tornare alla visualizzazione dell’area contenuto di più post UGC, seleziona la X nell’angolo in alto a destra del riquadro dei dettagli della visualizzazione.

Esempio:

![view1](assets/view1.png)
