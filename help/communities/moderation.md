---
title: Console di moderazione
seo-title: Console di moderazione
description: Come accedere alla console Moderazione
seo-description: Come accedere alla console Moderazione
uuid: d3b8a160-85b2-43f4-9891-5fafa8c48c5f
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 404582ab-bb4c-4775-9ae3-17356d376dca
docset: aem65
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '2110'
ht-degree: 4%

---


# Console di moderazione {#moderation-console}

In  AEM Communities, la moderazione [di contenuti della community ](/help/communities/moderate-ugc.md) è possibile sia dall&#39;ambiente di creazione che da quello di pubblicazione da parte di amministratori e moderatori della community (membri della community attendibili assegnati come moderatori).

Gli amministratori e i moderatori della community possono eseguire anche [moderazione contestuale](/help/communities/in-context.md) nell&#39;ambiente di pubblicazione.

Una funzione di tutti i [siti della community](/help/communities/sites-console.md) è una voce di menu `Administration` disponibile per gli utenti che accedono con privilegi amministrativi. Il collegamento `Administration` consente di accedere alla console Moderazione.

Dalla console Moderazione, gli amministratori e i moderatori della community avranno accesso a tutti i contenuti generati dagli utenti (UGC) per i quali dispongono dell’autorizzazione per moderare. Se è consentito moderare più siti, è possibile visualizzare i post in tutti i siti o filtrare in base a siti di comunità selezionate.

Per informazioni più dettagliate, visita [Gestione di utenti e gruppi di utenti](/help/communities/users.md).

La console Moderazione supporta:

* Esecuzione di attività di moderazione in massa.
* Ricerca UGC.
* Visualizzazione dei dettagli UGC.
* Visualizzazione dei dettagli dell’autore UGC.

È possibile eseguire le attività di moderazione solo quando si effettua l&#39;accesso come amministratore o un membro con ` [moderator permissions](/help/communities/in-context.md#identifyingtrustedmembers)`.

## Accesso all&#39;ambiente di pubblicazione {#publish-environment-access}

L&#39;accesso alla console Moderazione da un sito community pubblicato avviene tramite un collegamento Amministrazione che viene visualizzato al momento dell&#39;accesso di un moderatore della community.

![publishweretail](assets/publishweretail.png)

Selezionando il collegamento Amministrazione, viene visualizzata la console Moderazione:

![moderation-console-publish](assets/moderation-console-publish.png)

## Accesso all&#39;ambiente di authoring {#author-environment-access}

Nell’ambiente di authoring, per accedere alla console Moderazione

* Dalla navigazione globale, selezionare **[!UICONTROL Communities]** > **[!UICONTROL Moderazione]**.

È possibile eseguire le attività di moderazione solo quando si effettua l&#39;accesso come amministratore o come membro con [autorizzazioni del moderatore](/help/communities/in-context.md#identifyingtrustedmembers). L&#39;unico contenuto della community visualizzato è quello che il membro che ha effettuato l&#39;accesso può moderare.

>[!NOTE]
>
>L’UGC dell’ambiente di pubblicazione sarà visibile solo per gli autori se l’SRP scelto implementa uno store comune. Ad esempio, per impostazione predefinita l’archivio è JSRP, che non è uno store comune per l’autore e la pubblicazione. Vedere [Memorizzazione dei contenuti nella community](/help/communities/working-with-srp.md).

![moderationconsoleauthor](assets/moderationconsoleauthor.png)

## Interfaccia utente della console di moderazione {#moderation-console-ui}

Se si esclude la barra di navigazione a sinistra (che viene visualizzata sull’autore, ma non sulla pubblicazione), l’interfaccia utente di moderazione presenta le seguenti aree principali:

* **[Barra di navigazione superiore](#top-navigation-bar)**
* **[Barra degli strumenti](#toolbar)**
* **[Area di contenuto](#content-area)**

### Barra di navigazione superiore {#top-navigation-bar}

La barra di navigazione superiore è costante per tutte le console. Per ulteriori informazioni, vedere [Operazioni di base](/help/sites-authoring/basic-handling.md).

### Barra degli strumenti {#toolbar}

La barra degli strumenti, situata sotto la barra di navigazione superiore, fornisce il seguente interruttore di attivazione/disattivazione sul lato sinistro:

* [Filtra ](/help/communities/moderation.md#filterrail)
barra laterale consente di scegliere le proprietà su cui filtrare il contenuto.

La barra degli strumenti, situata sotto la barra di navigazione superiore, fornisce il seguente interruttore di attivazione/disattivazione sul lato sinistro:

![toggleswitch](assets/toggleswitch.png)

[Filtra ](/help/communities/moderation.md#filterrail)
barra laterale apre una barra laterale, selezionando Cerca, che consente di scegliere le proprietà su cui filtrare il contenuto.

![filterroide](assets/filterrail.png)

### Area contenuto {#content-area}

L&#39;area contenuto contiene informazioni per gli UGC inviati:

* UGC pubblicato
* Nome membro
* avatar membro
* Posizione del post.
* Quando è stato pubblicato.
* Numero di risposte al post.
* [](/help/communities/moderate-ugc.md#sentiment) Sentimentale associato al post
* Se approvato, viene visualizzato un segno di spunta.
* Se è presente un allegato, viene visualizzata una clip.

>[!NOTE]
> 
>L&#39;area contenuto presenta un *scorrimento infinito* che consente di continuare lo scorrimento fino alla fine del contenuto. La barra degli strumenti rimane in una posizione fissa e visibile sopra l&#39;area contenuto anche durante lo scorrimento.

### Barra dei filtri {#ootbfilters}

![open-filterrail](assets/open-filterrail.png)

L’icona del pannello laterale apre la barra laterale del filtro. La barra laterale del filtro, visualizzata a sinistra dell&#39;area contenuto, fornisce diversi filtri, ciascuno dei quali ha un effetto immediato sull&#39;UGC di riferimento visualizzato nell&#39;area contenuto.

I filtri all&#39;interno di ciascuna categoria sono **OR**&#39;d insieme, e i filtri di diverse categorie sono **AND** insieme.

Ad esempio, se selezionate sia **Domanda** che **Risposta**, il contenuto visualizzato sarà un **Domanda** *o* un **Risposta**.

Tuttavia, se si seleziona **Domanda** e **In sospeso**, verrà visualizzato solo il contenuto che è una **Domanda** ed è **In sospeso**.

>[!NOTE]
>
>I moderatori della community possono aggiungere segnalibri ai filtri predefiniti nell’interfaccia utente della console di moderazione. Poiché questi filtri vengono aggiunti alla fine dell’URL (come parametri della stringa di query), i moderatori possono tornare ai filtri con segnalibro in un secondo momento e condividere anche questi collegamenti.

![search icon](assets/searchicon.png)

Quando la barra laterale del filtro è aperta, l’icona Ricerca attiva/disattiva la chiusura del pannello laterale. Tuttavia, per chiudere la barra laterale del filtro e visualizzare solo il contenuto generato dall&#39;utente, fate clic sull&#39;icona Cerca e selezionate l&#39;opzione Solo contenuto.

#### Percorso contenuto {#content-path}

Percorso contenuto limita l&#39;UGC di riferimento visualizzato ai post inseriti nell&#39;archivio del contenuto specificato.

![content-path](assets/content-path.png)

#### Ricerca di testo {#text-search}

La ricerca del testo limita l’UGC di riferimento visualizzato ai post che contengono il testo immesso.

![text-search](assets/text-search.png)

#### Sito {#site}

Il sito limita l&#39;UGC di riferimento visualizzato ai post a siti community selezionati. Se non sono selezionati siti, vengono visualizzati tutti i riferimenti a UGC.

![site-panel](assets/site-panel.png)

>[!NOTE]
>
>Quando un amministratore accede alla console di moderazione in blocco, vengono visualizzati tutti i riferimenti a UGC, compresi i siti non creati con la [procedura guidata di creazione del sito](/help/communities/sites-console.md), ad esempio gli esempi di Geometrixx.
>
>Quando l&#39;accesso alla console di moderazione in blocco viene eseguito in seguito alla pubblicazione da parte di un membro della community affidabile, vengono visualizzati solo i riferimenti a UGC creati per i siti della community in cui il membro è autorizzato a moderare e possono essere filtrati con il filtro Sito.

#### Tipo di contenuto {#content-type}

Tipo di contenuto limita l&#39;UGC di riferimento visualizzato ai post del tipo di risorsa selezionato. È possibile selezionare uno o più dei seguenti tipi. Se non è selezionata alcuna opzione, vengono visualizzati tutti i tipi.

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

Per aggiungere ulteriori risorse da filtrare:

* Accedete all’istanza di creazione come amministratore.
* Apri [Console Web](https://localhost:4502/system/console/configMgr).
* Individuare `AEM Communities Moderation Dashboard Filters`.
* Selezionate la configurazione da aprire in modalità di modifica.
* Immettere ResourceType di un componente su cui filtrare:

   * Ad esempio, per filtrare i componenti per il voto inclusi, immettere:

      `Voting=social/tally/components/hbs/voting`
   ![tipo di contenuto aggiuntivo](assets/additional-contenttype.png)

* Seleziona Salva.
* Aggiornare la console Community - Moderazione.

Il risultato è un nuovo filtro selezionabile per `Voting` nel gruppo di filtri `Content Type`.

Quando il filtro viene selezionato, il contenuto del dashboard mostrerà UGC che corrisponde a qualsiasi tipo di risorsa immesso.

#### Stato {#status}

Lo stato limita l&#39;UGC di riferimento visualizzato ai post dello stato selezionato, che possono essere uno o più dei messaggi in sospeso, approvati, rifiutati o chiusi, nonché bozza o pianificati per gli articoli del blog e risposte o non fornite per le domande di QnA. Se non è selezionata alcuna opzione, vengono visualizzati tutti gli elementi.

>[!NOTE]
>
>Se è selezionato solo lo stato Non risposto, il moderatore visualizzerà tutto il contenuto (per tutti i tipi di contenuto) tranne le domande cui è stato risposto. Questo perché la proprietà responsabile della domanda cui è stata fornita la risposta non esiste nel caso di domande senza risposta e altri contenuti quali l&#39;argomento del forum, l&#39;articolo del blog o i commenti.

![stati](assets/statuses.png)

#### Segnalazione {#flagging}

Contrassegno limita l’UGC di riferimento visualizzato ai post contrassegnati o nascosti.

Una volta che un contenuto viene contrassegnato, rimane contrassegnato fino a quando non si annulla l&#39;contrassegno di tale singolo contenuto, selezionando nuovamente il pulsante **Flag**. Tenete presente che non esistono livelli di contrassegno, ad esempio importanti o successivi.

![contraddittorio](assets/flagging.png)

#### Membri {#members}

I membri limitano l&#39;UGC di riferimento visualizzato a UGC pubblicato dal nome membro immesso.

![membri](assets/members.png)

#### Pubblicato nell&#39;ultimo/a {#posted-in-the-last}

Pubblicato nell’ultimo limita la visualizzazione dell’UGC di riferimento ai post effettuati nell’ultima ora, giorno, settimana, mese o anno.

![postlast](assets/posted-last.png)

#### Sentimento {#sentiment}

[](/help/communities/moderate-ugc.md#sentiment) Sentimenticati limita l&#39;UGC di riferimento visualizzato ai post con un valore sentimentale positivo, negativo o neutro.

![sentimento](assets/sentiment.png)

## Filtri personalizzati {#custom-filters}

Oltre ai filtri integrati in [Barra dei filtri](/help/communities/moderation.md#ootbfilters), è possibile aggiungere altri filtri personalizzati sui metadati all&#39;interfaccia utente di moderazione. Gli sviluppatori possono utilizzare il codice di esempio in Github per estendere i filtri esistenti per l&#39;interfaccia utente di moderazione.

![custom-tag-filter](assets/custom-tag-filter.png)

Il [progetto di esempio](https://github.com/Adobe-Marketing-Cloud/aem-communities-extensions/tree/main/aem-communities-moderation-filter) su Github implementa il filtro di tag, per filtrare l&#39;elenco UGC in base al fatto che i tag specifici siano applicati o meno al contenuto generato dall&#39;utente. Potete seguire il codice di esempio e creare filtri analoghi per altri campi di metadati UGC simili.

Per installare l’esempio per il filtro Tag:

1. Aprite il gestore pacchetti nell&#39;istanza di AEM Author ([https://[aem-author]:4502/crx/packmgr/index.jsp](https://aem65-communities-demo.corp.adobe.com:4502/crx/packmgr/index.jsp)) e AEM Publish ([https://[aem-publish]:4503/crx/packmgr/index.jsp](https://aem65-communities-demo.corp.adobe.com:4502/crx/packmgr/index.jsp)).
1. Create il pacchetto `com.adobe.social.sample.moderation.filter.ui.apps-1.0-SNAPSHOT.zip` dal codice Github, quindi installate e abilitate lo stesso.
1. Aprite la console dei bundle nell&#39;istanza di AEM Author ( `https://[aem-author]:4502/system/console/bundles`) e nell&#39;istanza di AEM Publish ( `https://[aem-publish]:4503/system/console/bundles`).
1. Create il pacchetto ` [com](https://sample-moderation-filter.com/).adobe.social.sample.moderation.filter.core-1.0-SNAPSHOT.jar` da Github, quindi installate e abilitate lo stesso.
1. Andate al nodo **/apps/social/moderation/facets** su AEM Author ([https://[aem-author]:4502/crx/de/index.jsp#/apps/social/moderation/facets](https://aem65-communities-demo.corp.adobe.com:4502/crx/de/index.jsp#/apps/social/moderation/facets)) e AEM Publish ([https://[aem-publish]:4502/crx/de/index.jsp#/apps/social/moderation/facets](https://aem65-communities-demo.corp.adobe.com:4502/crx/de/index.jsp#/apps/social/moderation/facets)).
1. Aggiungi un utente tecnico **community-utility-reader** con autorizzazioni `jcr:read`.

Per esporre i filtri personalizzati sui siti comunitari esistenti:

1. Modifica `Clientlibs` della pagina di moderazione esistente `/content/we-retail/us/en/community/moderation/shell3/jcr:content/head/clientlibs.`

   * Aggiungi nuova categoria `cq.social.hbs.moderation.v2.`

1. Passa a `/content/we-retail/us/en/community/moderation/shell3/jcr:content/rails/searchWell/items/filters.`

   * Imposta su nuovo componente `sling:resourceType = social/moderation/v2/filters.`

1. Passa a `/content/we-retail/us/en/community/moderation/shell3/jcr:content/views/content/items/modcontainer`.

   * Impostare su nuovo componente `sling:resourceType = social/moderation/v2/modcontainer`.

## Azioni di moderazione {#moderation-actions}

[Le ](/help/communities/moderate-ugc.md#moderation-actions) azioni di moderazione possono essere eseguite su una o più selezioni effettuate nell&#39;area contenuto o durante la visualizzazione dei dettagli del contenuto.

Per moderare in massa i post, nell&#39;area del contenuto fare clic sull&#39;icona Seleziona (![seletz](assets/selecticon.png)) su un post, che viene visualizzata quando si passa il mouse (desktop) o si preme e si tiene premuto un dito sul post (mobile). A questo scopo, potete passare alla modalità multi-selezione e ora selezionare i post successivi da moderare in massa semplicemente facendo clic su di essi. Utilizzare i pulsanti visualizzati sulla barra degli strumenti per eseguire azioni di moderazione sui post selezionati. Tutte le azioni richiederanno la conferma.

Per moderare un singolo post nell&#39;area contenuto, posizionate il puntatore del mouse (desktop) o tenete premuto un dito sul post (mobile) in modo che sul post figurino dei pulsanti. Quando si utilizza un singolo dettaglio di contenuto, viene richiesta la conferma solo per un&#39;azione di eliminazione.

### Moderazione di più post {#moderating-multiple-posts}

Per passare alla modalità di selezione collettiva, fai clic sull&#39;icona `Select` in un post:

![select-icon](assets/select-icon.png)

Per uscire dalla modalità di selezione in blocco, selezionate l’icona Annulla (x) sulla barra degli strumenti:

Le azioni di moderazione che possono essere eseguite su più post sono:

* Rifiuta
* Elimina
* Chiudi/riapri i post

Le icone che consentono di eseguire queste azioni vengono visualizzate sulla barra degli strumenti solo se sono selezionati più post.

![bulkmoderato](assets/bulkmoderate.png)

### Moderazione di un singolo post {#moderating-a-single-post}

In modalità di selezione singola, è possibile:

* Visualizzate i dettagli utente selezionando il nome dell&#39;utente.
* Visualizzare il post nel contesto selezionando il collegamento al post.
* [Risposta](#reply)
* [Consenti](#allow)
* [Rifiuta](#deny)
* [Elimina](#delete)
* [Chiudi](#close)
* Visualizza [Cronologia moderazione](#moderation-history)
* [Visualizza dettagli](#viewdetails)

Presente nella vista a schede sopra le icone delle azioni di moderazione, il testo del post e sotto i dati che indicano:

* Se le risposte sono già state fornite e, in tal caso, precedute dal numero di risposte.
* Se è stato contrassegnato.
* Se approvato.
* Quando è stato pubblicato l&#39;UGC.

![singleselectmode](assets/singleselectmode.png)

#### Risposta {#reply}

![response](assets/reply.png)

Quando si lavora con un singolo post, viene visualizzata un&#39;icona Rispondi se il tipo UGC supporta le risposte ed è configurato per consentire le risposte.

#### Consenti {#allow}

![consenti](assets/allow.png)

Quando si utilizza un singolo post, l&#39;icona Consenti viene visualizzata quando il post è stato contrassegnato o rifiutato. Se questa opzione è contrassegnata, quando si seleziona Consenti verranno cancellati tutti i flag.

#### Rifiuta {#deny}

![rifiuta](assets/deny.png)

L&#39;azione di moderazione **Rifiuta** è disponibile solo per il contenuto moderato e non viene visualizzata su contenuto non moderato, tranne che in modalità di selezione multipla.

Il contenuto non moderato viene sempre approvato.

Il contenuto moderato inizialmente entra in uno stato In sospeso e può essere successivamente modificato per essere approvato o rifiutato.

Il contenuto che lascia lo stato in sospeso non può mai tornare a uno stato in sospeso. Il contenuto contrassegnato come approvato o rifiutato può essere modificato in un altro stato in qualsiasi momento.

#### Elimina {#delete}

![delete](assets/delete.png)

In modalità di selezione singola o in blocco, potete selezionare gli elementi ed eliminarli. L’azione di eliminazione crea una finestra di dialogo di conferma. Una volta eliminati, tali elementi scompaiono immediatamente dall&#39;area contenuto. **Una volta eliminato, l’UGC viene rimosso in modo permanente dall’archivio e non può essere recuperato** in un secondo momento.

#### Chiudi {#close}

![chiudi](assets/close.png)

Quando si lavora con un singolo post, viene visualizzata un&#39;icona Chiudi se il tipo UGC supporta la capacità di impedire ulteriori post per tale risorsa.

#### Cronologia moderazione {#moderation-history}

![moderazione](assets/moderation.png)

Quando si lavora con un singolo post, quando si passa il puntatore sopra di esso viene visualizzata un&#39;icona Cronologia moderazione. Quando si seleziona l’icona, viene visualizzato un riquadro contenente una cronologia delle azioni eseguite rispetto al post UGC.

Per tornare alla visualizzazione dell&#39;area contenuto di più post UGC, selezionate la X nell&#39;angolo superiore destro del riquadro dei dettagli di visualizzazione.

Esempio:

![moderazione](assets/moderation-history.png)

#### Visualizza dettagli {#view-detail}

![view](assets/view.png)

Quando si lavora con un singolo post, è possibile visualizzare ulteriori dettagli aprendo l&#39;UGC in modalità dettaglio.

A questo scopo, passate il mouse sul post per visualizzare l&#39;icona `View Detail` e selezionatelo per visualizzare un pannello contenente ulteriori dettagli sul post.

Per tornare alla visualizzazione dell&#39;area contenuto di più post UGC, selezionate la X nell&#39;angolo superiore destro del riquadro dei dettagli di visualizzazione.

Esempio:

![view1](assets/view1.png)

