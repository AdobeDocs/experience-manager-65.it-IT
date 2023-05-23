---
title: Guida ai componenti della community
seo-title: Community Components Guide
description: Strumento di sviluppo interattivo per iniziare a utilizzare il framework dei componenti social (SCF)
seo-description: An interactive development tool to get started with the social component framework (SCF)
uuid: 120e56d1-b93c-4f92-bab4-6bb5e40e0ddf
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: a777a3f1-b39f-4d90-b9b6-02d3e321a86f
exl-id: 12c0eae5-fd76-4480-a012-25d3312f3570
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1187'
ht-degree: 2%

---

# Guida ai componenti della community  {#community-components-guide}

La guida ai componenti community è uno strumento di sviluppo interattivo per [framework della componente social network (SCF)](scf.md). Fornisce un elenco dei componenti AEM Communities disponibili o delle funzioni più complesse create da più componenti.

Oltre alle informazioni di base per ciascun componente, la guida consente di sperimentare il funzionamento dei componenti e delle funzioni SCF e come configurarli o personalizzarli.

Per informazioni sulle nozioni di base di sviluppo relative a ciascun componente, consulta [Funzionalità e componenti essenziali](essentials.md).

## Guida introduttiva {#getting-started}

La guida deve essere utilizzata nelle installazioni di sviluppo di istanze di authoring (localhost:4502) e pubblicazione (localhost:4503).

Per accedere al sito Componenti community, vai a

* [https://&lt;server>:&lt;port>/content/community-components/en.html](http://localhost:4502/content/community-components/en.html)

Le interazioni con i componenti Community variano a seconda di:

* Il server (di authoring o pubblicazione).
* Indica se il visitatore del sito ha eseguito o meno l&#39;accesso.
* Se l&#39;accesso è stato eseguito, i privilegi assegnati al membro.
* Indica se l&#39;SRP predefinito è o meno [JSRP](jsrp.md), è in uso.

Per accedere alla modalità di modifica, inserisci `editor.html` o `cf#` come primo segmento di percorso dopo il nome del server:

* Interfaccia standard:

   [https://&lt;server>:&lt;port>/editor.html/content/community-components/en.html](http://localhost:4502/editor.html/content/community-components/en.html)

* Interfaccia classica:

   [https://&lt;server>:&lt;port>/cf#/content/community-components/en.html](http://localhost:4502/cf#/content/community-components/en.html)

>[!NOTE]
>
>Quando si esegue l’authoring in modalità Modifica, i collegamenti presenti in una pagina non sono attivi.
>
>Per passare a una pagina di un componente, seleziona innanzitutto la modalità Anteprima per attivare i collegamenti.
>
>Con la pagina del componente visualizzata nel browser, torna alla modalità Modifica per aprire la finestra di dialogo di modifica del componente.
>
>Per informazioni generali sull&#39;authoring, vedere [guida rapida all’authoring delle pagine](../../help/sites-authoring/qg-page-authoring.md).
>
>Se non conosci l’AEM, consulta la documentazione su [operazioni di base](../../help/sites-authoring/basic-handling.md).

### Home page {#home-page}

La guida fornisce un elenco dei componenti SCF disponibili per l’anteprima e la prototipazione lungo il lato sinistro della pagina.

Guida ai componenti visualizzata in un’istanza Autore in modalità Modifica:

![community-component1](assets/community-component1.png)

## Pagine dei componenti {#component-pages}

Seleziona un componente dall’elenco lungo il lato sinistro della pagina.

![community-component-pages](assets/community-component2.png)

Il corpo principale della guida mostra:

1. Titolo: nome del componente selezionato
1. [Librerie lato client](#client-side-libraries): elenco di una o più categorie richieste
1. [Inclusi](scf.md#add-or-include-a-communities-component): se il componente può essere incluso in modo dinamico, lo stato può essere attivato nella modalità di modifica dell’autore:

   * Se aggiunto, il testo visualizzato è: &quot;Questo componente è incluso tramite il suo nodo par&quot;.
   * Se incluso, il testo visualizzato è: &quot;Questo componente è incluso in modo dinamico&quot;.
   * Se non è disponibile, non viene visualizzato alcun testo

1. Componente o feature di esempio: un&#39;istanza attiva del componente o della feature. Se un componente viene modificato, può essere modificato con modifiche apportate ai modelli, agli stili CSS e ai dati forniti nella sezione Scheda.

>[!NOTE]
>
>Dopo aver effettuato una selezione dal lato sinistro, il componente viene visualizzato sotto l’elenco dei componenti, anziché accanto, quando la finestra del browser è troppo stretta.

### Interazioni autore {#author-interactions}

Quando utilizzi la guida su un’istanza dell’autore, puoi provare a configurare un componente aprendo la relativa finestra di dialogo. Le informazioni per gli sviluppatori sono fornite nel [Nozioni di base su componenti e funzionalità](essentials.md) della documentazione, mentre le impostazioni della finestra di dialogo sono descritte in [Componenti community](author-communities.md) sezione per autori.

Nella guida Componenti community, alcune impostazioni della finestra di dialogo dei componenti sono sovrapposte al [Inclusi](scf.md#add-or-include-a-communities-component) attivare/disattivare lo stato. Per passare dall’utilizzo della risorsa esistente all’utilizzo di una risorsa inclusa dinamicamente, in modalità di modifica seleziona sia il componente che il testo da includere e fai doppio clic per aprire la finestra di dialogo di modifica:

![community-component3](assets/community-component3.png)

Sotto **Modelli** scheda:

![community-component4](assets/community-component4.png)

* **Includi componente secondario con sling:include**

   Se questa opzione è deselezionata, la Guida dei componenti utilizzerà la risorsa esistente nell’archivio (un nodo jcr che è figlio di un nodo par).

   * il testo visualizzato è: &quot;Questo componente è incluso tramite il suo nodo par&quot;.

   Se questa opzione è selezionata, nella Guida dei componenti verrà utilizzato sling per includere in modo dinamico un componente del resourceType del nodo figlio (risorsa non esistente).

   * il testo visualizzato è: &quot;Questo componente è incluso in modo dinamico&quot;.

   L&#39;impostazione predefinita è deselezionata.

### Pubblica interazioni {#publish-interactions}

Quando si utilizza la guida in un’istanza di pubblicazione, è possibile provare i componenti e le funzionalità come visitatore del sito (non connesso) e come membri con vari privilegi quando si è connessi.

>[!NOTE]
>
>Tieni presente che se l’SRP viene lasciato impostato come predefinito [JSRP](jsrp.md), quindi l’UGC immesso nell’istanza di pubblicazione sarà visibile solo al momento della pubblicazione e *non* essere visibile dall&#39; [moderazione](moderate-ugc.md) nell’istanza di authoring.

## Librerie lato client {#client-side-libraries}

Le librerie lato client (clientlibs) elencate per ciascun componente sono quelle *obbligatorio* da utilizzare quando il componente viene inserito in una pagina. Le clientlibs consentono di gestire e ottimizzare il download di JavaScript e CSS utilizzati per il rendering del componente nel browser.

Per ulteriori informazioni, visita [Clientlibs per i componenti Communities](clientlibs.md).

## Impersonazione {#impersonation}

Nell’istanza di authoring, in cui si è spesso connessi come amministratore o sviluppatore, per avere un’idea del componente connesso come un altro utente, utilizza la casella di testo a sinistra del **[!UICONTROL Impersona]** per digitare il nome utente o selezionarlo dall&#39;elenco a discesa, quindi fare clic sul pulsante. Fai clic su Ripristina per disconnettersi e terminare la rappresentazione.

Non è necessario che l’istanza Publish sia rappresentata. È sufficiente utilizzare il collegamento Login/Logout per rappresentare vari utenti, ad esempio [utenti demo](tutorials.md#demo-users).

## Personalizzazione {#customization}

Quando è abilitato, ogni componente SCF è disponibile per la creazione di prototipi di possibili personalizzazioni modificando temporaneamente il modello, i CSS e i dati del componente.

### Abilitazione della personalizzazione {#enabling-customization}

>[!NOTE]
>
>**Questo strumento è di sola lettura**. Nessuna delle modifiche apportate a modelli, CSS o dati viene salvata nell’archivio.

Per sperimentare rapidamente le personalizzazioni, `scg:showIde`deve essere aggiunta al nodo JCR del contenuto della pagina del componente e impostata su true.

Utilizzando il componente commenti come esempio, nell’istanza di authoring o di pubblicazione è stato effettuato l’accesso con privilegi di amministratore:

1. Sfoglia per [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md)

   Ad esempio: [http://localhost:4503/crx/de](http://localhost:4503/crx/de)

1. Seleziona il `jcr:content` nodo

   Ad esempio `/content/community-components/en/comments/jcr:content`

1. Aggiungi una proprietà

   * **Nome** `scg:showIde`
   * **Tipo** `String`
   * **Valore** `true`

1. Seleziona **[!UICONTROL Salva tutto]**
1. Ricarica la pagina Commenti nella guida

   [http://localhost:4503/content/community-components/en/comments.html](http://localhost:4503/content/community-components/en/comments.html)

1. Ora sono disponibili 3 schede per Modelli, CSS e Dati.

![community-component5](assets/community-component5.png)

![community-component6](assets/community-component6.png)

### Scheda Modelli {#templates-tab}

Seleziona la scheda modelli per visualizzare i modelli associati al componente.

L’Editor modelli consente di compilare e applicare modifiche locali all’istanza del componente di esempio nella parte superiore della pagina senza influire sul componente nell’archivio.

L&#39;esecuzione della compilazione su modifiche locali evidenzia gli eventuali errori posizionando un punto nella rilegatura e contrassegnando il testo in rosso.

### Scheda CSS {#css-tab}

Seleziona la scheda CSS per visualizzare il CSS associato al componente.

Se un componente è un composito di più componenti, alcuni CSS possono essere elencati in uno degli altri componenti.

L’editor CSS consente di modificare il CSS e applicarlo all’istanza del componente di esempio nella parte superiore della pagina.

È possibile selezionare una regola per evidenziare le parti del DOM che utilizzano tale regola facendo clic su accanto alla regola nella griglia.

### Scheda Dati {#data-tab}

Seleziona la scheda Dati per visualizzare i dati dell’endpoint .social.json. Questi dati sono modificabili e vengono applicati all’istanza del componente di esempio.

Gli errori di sintassi possono essere contrassegnati nel contagocce ed evidenziati nell’editor.
