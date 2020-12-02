---
title: Guida ai componenti community
seo-title: Guida ai componenti community
description: Uno strumento di sviluppo interattivo per iniziare a usare il framework delle componenti social (SCF)
seo-description: Uno strumento di sviluppo interattivo per iniziare a usare il framework delle componenti social (SCF)
uuid: 120e56d1-b93c-4f92-bab4-6bb5e40e0ddf
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: a777a3f1-b39f-4d90-b9b6-02d3e321a86f
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '1203'
ht-degree: 2%

---


# Guida ai componenti community  {#community-components-guide}

La Guida ai componenti comunitari è uno strumento di sviluppo interattivo per il [social component framework (SCF)](scf.md). Fornisce un elenco dei componenti disponibili  AEM Communities o delle funzioni più complesse create da più componenti.

Oltre alle informazioni di base per ciascun componente, la guida consente di sperimentare il funzionamento dei componenti e delle funzioni SCF e le modalità di configurazione o personalizzazione.

Per informazioni sulle funzionalità di sviluppo di ciascun componente, vedere [Feature and Component Essentials](essentials.md) (Caratteristiche e componenti essenziali).

## Guida introduttiva {#getting-started}

La guida è destinata alle installazioni di sviluppo di istanze di creazione (localhost:4502) e pubblicazione (localhost:4503).

Per accedere al sito Community Components, consulta

* [https://&lt;server>:&lt;port>/content/community-components/en.html](http://localhost:4502/content/community-components/en.html)

Le interazioni con i componenti Community variano a seconda:

* Server (autore o pubblicazione).
* Indica se il visitatore del sito ha effettuato o meno l&#39;accesso.
* Se avete effettuato l’accesso, i privilegi assegnati al membro.
* Indica se l&#39;SRP predefinito [JSRP](jsrp.md) è in uso o meno.

All&#39;autore, per passare alla modalità di modifica, inserire `editor.html` o `cf#` come primo segmento di percorso dopo il nome del server:

* Interfaccia standard:

   [https://&lt;server>:&lt;port>/editor.html/content/community-components/en.html](http://localhost:4502/editor.html/content/community-components/en.html)

* Interfaccia classica:

   [https://&lt;server>:&lt;port>/cf#/content/community-components/en.html](http://localhost:4502/cf#/content/community-components/en.html)

>[!NOTE]
>
>In modalità Modifica, i collegamenti presenti su una pagina non sono attivi.
>
>Per passare alla pagina di un componente, seleziona innanzitutto la modalità Anteprima per attivare i collegamenti.
>
>Con la pagina del componente visualizzata nel browser, tornate alla modalità Modifica per aprire la finestra di dialogo di modifica del componente.
>
>Per informazioni generali sull&#39;authoring, consultare la [guida rapida all&#39;authoring delle pagine](../../help/sites-authoring/qg-page-authoring.md).
>
>Se non hai familiarità con AEM, consulta la documentazione su [operazioni di base](../../help/sites-authoring/basic-handling.md).

### Home page {#home-page}

La guida fornisce un elenco dei componenti SCF disponibili per l’anteprima e la creazione di prototipi lungo il lato sinistro della pagina.

Guida ai componenti visualizzata su un’istanza di creazione in modalità di modifica:

![community-component1](assets/community-component1.png)

## Pagine dei componenti {#component-pages}

Selezionate un componente dall’elenco sul lato sinistro della pagina.

![community-component-pages](assets/community-component2.png)

Il corpo principale della guida visualizza:

1. Titolo: Nome del componente selezionato
1. [Librerie](#client-side-libraries) lato client: Elenco di una o più categorie richieste
1. [Inclusi](scf.md#add-or-include-a-communities-component): Se il componente può essere incluso in modo dinamico, è possibile attivare o disattivare lo stato in modalità di modifica dell’autore:

   * Se aggiunto, il testo visualizzato è: &quot;Questo componente è incluso tramite il relativo nodo par.&quot;
   * Se incluso, il testo visualizzato è: &quot;Questo componente è incluso dinamicamente.&quot;
   * Se non incluso, non viene visualizzato alcun testo

1. Esempio di componente o funzione: un’istanza attiva del componente o della feature. Se un componente può essere modificato con modifiche apportate ai modelli, ai CSS e ai dati forniti nella sezione scheda.

>[!NOTE]
>
>Dopo aver effettuato una selezione dal lato sinistro, il componente compare sotto, invece che accanto, l’elenco dei componenti quando la finestra del browser è troppo stretta.

### Interazioni autore {#author-interactions}

Quando si utilizza la guida in un’istanza di authoring, è possibile configurare un componente aprendo la relativa finestra di dialogo. Le informazioni per gli sviluppatori sono fornite nella sezione [Componenti e funzionalità Essentials](essentials.md) della documentazione, mentre le impostazioni della finestra di dialogo sono descritte nella sezione [Componenti community](author-communities.md) per gli autori.

Per la guida Componenti comunità, alcune impostazioni della finestra di dialogo dei componenti sono sovrapposte allo stato [Inclusibile](scf.md#add-or-include-a-communities-component). Per alternare tra l’utilizzo della risorsa esistente o di una risorsa inclusa dinamicamente, in modalità di modifica selezionate sia il componente che il testo incluso, quindi fate doppio clic per aprire la finestra di dialogo di modifica:

![community-component3](assets/community-component3.png)

Nella scheda **Modelli**:

![community-component4](assets/community-component4.png)

* **Includi componente secondario con sling:include**

   Se questa opzione è deselezionata, la Guida ai componenti utilizzerà la risorsa esistente nell&#39;archivio (un nodo jcr secondario di un nodo par).

   * il testo visualizzato è: &quot;Questo componente è incluso tramite il relativo nodo par.&quot;

   Se questa opzione è selezionata, la Guida ai componenti utilizzerà la funzione sling per includere dinamicamente un componente del resourceType del nodo secondario (risorsa non esistente).

   * il testo visualizzato è: &quot;Questo componente è incluso dinamicamente.&quot;

   Il valore predefinito è deselezionato.

### Pubblicare le interazioni {#publish-interactions}

Quando si utilizza la guida in un’istanza pubblicata, è possibile utilizzare i componenti e le funzioni come visitatore del sito (non ha effettuato l’accesso) e come membri con diversi privilegi al momento dell’accesso.

>[!NOTE]
>
>Tenete presente che se l&#39;SRP viene lasciato impostato come predefinito su [JSRP](jsrp.md), l&#39;UGC immesso nell&#39;istanza di pubblicazione sarà visibile solo al momento della pubblicazione e *not* sarà visibile dalla console [moderazione](moderate-ugc.md) nell&#39;istanza di creazione.

## Librerie lato client {#client-side-libraries}

Le librerie lato client (clientlibs) elencate per ciascun componente sono quelle *obbligatorie* a cui viene fatto riferimento quando il componente viene inserito in una pagina. I clientlibs forniscono uno strumento per gestire e ottimizzare il download di JavaScript e CSS utilizzati per il rendering del componente nel browser.

Per ulteriori informazioni, vedere [Clientlibs for Communities Components](clientlibs.md).

## Impersonazione {#impersonation}

Nell&#39;istanza di creazione, in cui uno di questi ha spesso effettuato l&#39;accesso come amministratore o sviluppatore, per verificare che il componente abbia eseguito l&#39;accesso come un altro utente, utilizzate la casella di testo a sinistra del pulsante **[!UICONTROL Impersonate]** per digitare il nome utente o selezionate dall&#39;elenco a discesa, quindi fate clic sul pulsante. Fate clic su Ripristina per uscire e terminare la rappresentazione.

L’istanza di pubblicazione non deve essere rappresentata. È sufficiente utilizzare il collegamento Login/Logout per rappresentare vari utenti, ad esempio [utenti dimostrativi](tutorials.md#demo-users).

## Personalizzazione {#customization}

Quando attivato, ciascun componente SCF è disponibile per la creazione di prototipi di personalizzazioni possibili modificando temporaneamente il modello, i CSS e i dati del componente.

### Abilitazione di Customization {#enabling-customization}

>[!NOTE]
>
>**Questo strumento è di sola** lettura. Nessuna delle modifiche apportate a modelli, CSS o dati viene salvata nella directory archivio.

Per sperimentare rapidamente le personalizzazioni, la proprietà `scg:showIde`deve essere aggiunta al nodo JCR del contenuto della pagina del componente e impostata su true.

Utilizzando il componente commenti come esempio, nell’istanza di creazione o di pubblicazione, è stato effettuato l’accesso con privilegi di amministratore:

1. Passa a [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md)

   Ad esempio, [http://localhost:4503/crx/de](http://localhost:4503/crx/de)

1. Selezionare il nodo `jcr:content` del componente

   Esempio, `/content/community-components/en/comments/jcr:content`

1. Aggiunta di una proprietà

   * **Nome** `scg:showIde`
   * **Tipo** `String`
   * **Valore** `true`

1. Selezionare **[!UICONTROL Salva tutto]**
1. Ricaricare la pagina Commenti nella guida

   [http://localhost:4503/content/community-components/en/comments.html](http://localhost:4503/content/community-components/en/comments.html)

1. Ora sono disponibili 3 schede per Modelli, CSS e Dati.

![community-component5](assets/community-component5.png)

![community-component6](assets/community-component6.png)

### Scheda Modelli {#templates-tab}

Selezionate la scheda Modelli per visualizzare i modelli associati al componente.

L’Editor modelli consente di compilare e applicare le modifiche locali all’istanza del componente di esempio nella parte superiore della pagina, senza interferire con il componente presente nell’archivio.

L’esecuzione della compilazione sulle modifiche locali evidenzierà eventuali errori posizionando un punto nel rilegio e contrassegnando il testo in rosso.

### Scheda CSS {#css-tab}

Selezionate la scheda CSS per visualizzare il CSS associato al componente.

Se un componente è composto da più componenti, alcuni CSS possono essere elencati in uno degli altri componenti.

L’Editor CSS consente di modificare il CSS e applicarlo all’istanza del componente di esempio nella parte superiore della pagina.

È possibile selezionare una regola per evidenziare le parti del DOM che utilizzano tale regola facendo clic accanto alla regola nel rilegio.

### Scheda Dati {#data-tab}

Selezionate la scheda Dati per visualizzare i dati dell&#39;endpoint .social.json. Questi dati sono modificabili e applicati all’istanza del componente di esempio.

Gli errori di sintassi possono essere contrassegnati nel rilegio e evidenziati nell&#39;editor.
