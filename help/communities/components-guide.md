---
title: Guida ai componenti della community
description: Strumento di sviluppo interattivo per iniziare a utilizzare il framework dei componenti social (SCF)
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 12c0eae5-fd76-4480-a012-25d3312f3570
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1153'
ht-degree: 0%

---

# Guida ai componenti della community  {#community-components-guide}

La guida dei componenti community è uno strumento di sviluppo interattivo per il [framework dei componenti social (SCF)](scf.md). Fornisce un elenco dei componenti disponibili di Adobe Experience Manager (AEM) Communities o delle funzioni più complesse create da più componenti.

Oltre alle informazioni di base per ciascun componente, la guida consente di sperimentare il funzionamento dei componenti e delle funzioni SCF e come configurarli o personalizzarli.

Per informazioni sulle nozioni di base di sviluppo relative a ciascun componente, vedi [Nozioni di base sulle funzionalità e sui componenti](essentials.md).

## Guida introduttiva {#getting-started}

La guida deve essere utilizzata nelle installazioni di sviluppo di istanze di authoring (localhost:4502) e di pubblicazione (localhost:4503).

Per accedere al sito Componenti community, vai a

* [https://&lt;server>:&lt;porta>/content/community-components/en.html](http://localhost:4502/content/community-components/en.html)

Le interazioni con i componenti Community variano a seconda di:

* Il server (di authoring o pubblicazione).
* Indica se il visitatore del sito ha effettuato o meno l&#39;accesso.
* Se l&#39;accesso è stato eseguito, i privilegi assegnati al membro.
* Indica se l&#39;SRP predefinito, [JSRP](jsrp.md), è in uso.

Per attivare la modalità di modifica, inserire `editor.html` o `cf#` come primo segmento di percorso dopo il nome del server:

* Interfaccia utente standard:

  [https://&lt;server>:&lt;porta>/editor.html/content/community-components/en.html](http://localhost:4502/editor.html/content/community-components/en.html)

* Interfaccia classica:

  [https://&lt;server>:&lt;porta>/cf#/content/community-components/en.html](http://localhost:4502/cf#/content/community-components/en.html)

>[!NOTE]
>
>Quando si esegue l’authoring in modalità Modifica, i collegamenti presenti in una pagina non sono attivi.
>
>Per passare a una pagina di un componente, seleziona innanzitutto la modalità Anteprima per attivare i collegamenti.
>
>Con la pagina del componente visualizzata nel browser, torna alla modalità Modifica per aprire la finestra di dialogo per modifica del componente.
>
>Per informazioni generali sull&#39;authoring, consulta la [guida rapida all&#39;authoring delle pagine](../../help/sites-authoring/qg-page-authoring.md).
>
>Se non conosci l&#39;AEM, consulta la documentazione sulle [operazioni di base](../../help/sites-authoring/basic-handling.md).

### Pagina home {#home-page}

La guida fornisce un elenco dei componenti SCF disponibili per l’anteprima e la prototipazione lungo il lato sinistro della pagina.

Guida ai componenti visualizzata in un’istanza Autore in modalità Modifica:

![componente-community1](assets/community-component1.png)

## Pagine dei componenti {#component-pages}

Seleziona un componente dall’elenco lungo il lato sinistro della pagina.

![pagine-componenti-community](assets/community-component2.png)

Il corpo principale della guida mostra:

1. Titolo: nome del componente selezionato
1. [Librerie lato client](#client-side-libraries): elenco di una o più categorie richieste
1. [Inclusivo](scf.md#add-or-include-a-communities-component): se il componente può essere incluso in modo dinamico, lo stato può essere attivato nella modalità di modifica dell&#39;autore:

   * Se aggiunto, il testo visualizzato è: &quot;Questo componente è incluso tramite il suo nodo par&quot;.
   * Se incluso, il testo visualizzato è: &quot;Questo componente è incluso in modo dinamico&quot;.
   * Se non è disponibile, non viene visualizzato alcun testo

1. Componente o feature di esempio: un&#39;istanza attiva del componente o della feature. Se un componente viene modificato, può essere modificato con modifiche apportate ai modelli, CSS e dati forniti nella sezione Scheda.

>[!NOTE]
>
>Dopo aver effettuato una selezione dal lato sinistro, il componente viene visualizzato sotto l’elenco dei componenti, anziché accanto, quando la finestra del browser è troppo stretta.

### Interazioni autore {#author-interactions}

Quando utilizzi la guida su un’istanza dell’autore, puoi provare a configurare un componente aprendo la relativa finestra di dialogo. Le informazioni per gli sviluppatori sono fornite nella sezione [Component and Feature Essentials](essentials.md) della documentazione, mentre le impostazioni della finestra di dialogo sono descritte nella sezione [Communities Components](author-communities.md) per gli autori.

Nella guida dei componenti della community, alcune impostazioni della finestra di dialogo dei componenti sono sovrapposte con lo stato di attivazione/disattivazione [Includable](scf.md#add-or-include-a-communities-component). Per passare dall’utilizzo della risorsa esistente all’utilizzo di una risorsa inclusa dinamicamente, in modalità di modifica seleziona sia il componente che il testo da includere e fai doppio clic per aprire la finestra di dialogo di modifica:

![componente community3](assets/community-component3.png)

Nella scheda **Modelli**:

![componente-community4](assets/community-component4.png)

* **Includi il componente secondario con sling:include**

  Se questa opzione è deselezionata, la Guida dei componenti utilizza la risorsa esistente nell’archivio (un nodo jcr che è figlio di un nodo par).

   * il testo visualizzato è: &quot;Questo componente è incluso tramite il suo nodo par&quot;.

  Se questa opzione è selezionata, nella Guida dei componenti viene utilizzato sling per includere in modo dinamico un componente del resourceType del nodo figlio (risorsa non esistente).

   * il testo visualizzato è: &quot;Questo componente è incluso in modo dinamico&quot;.

  L&#39;impostazione predefinita è deselezionata.

### Interazioni Publish {#publish-interactions}

Quando si utilizza la guida in un’istanza di pubblicazione, è possibile provare i componenti e le funzionalità come visitatore del sito (non connesso) e come membri con vari privilegi quando si è connessi.

>[!NOTE]
>
>Tieni presente che se l&#39;SRP viene lasciato impostato come predefinito su [JSRP](jsrp.md), l&#39;UGC immesso nell&#39;istanza di pubblicazione sarà visibile solo al momento della pubblicazione e *non* sarà visibile dalla console [moderazione](moderate-ugc.md) nell&#39;istanza di authoring.

## Librerie lato client {#client-side-libraries}

Le librerie lato client (clientlibs) elencate per ogni componente sono quelle *obbligatorie* a cui fare riferimento quando il componente viene inserito in una pagina. Le clientlibs consentono di gestire e ottimizzare il download del JavaScript e dei CSS utilizzati per il rendering del componente nel browser.

Per ulteriori informazioni, visitare [Clientlibs for Communities Components](clientlibs.md).

## Impersonazione {#impersonation}

Nell&#39;istanza di authoring, in cui si è spesso connessi come amministratore o sviluppatore, per visualizzare il componente connesso come altro utente, utilizzare la casella di testo a sinistra del pulsante **[!UICONTROL Impersona]** per digitare il nome utente o selezionarlo dall&#39;elenco a discesa, quindi fare clic sul pulsante. Fai clic su Ripristina per uscire e terminare la rappresentazione.

Non è necessario che l’istanza Publish sia rappresentata. È sufficiente utilizzare il collegamento Login/Logout per rappresentare vari utenti, ad esempio [utenti demo](tutorials.md#demo-users).

## Personalizzazione {#customization}

Quando è abilitato, ogni componente SCF è disponibile per la creazione di prototipi di possibili personalizzazioni modificando temporaneamente il modello, i CSS e i dati del componente.

### Abilitazione della personalizzazione {#enabling-customization}

>[!NOTE]
>
>**Strumento di sola lettura**. Nessuna delle modifiche apportate a modelli, CSS o dati viene salvata nell’archivio.

Per sperimentare rapidamente le personalizzazioni, la proprietà `scg:showIde` deve essere aggiunta al nodo JCR del contenuto della pagina del componente e impostata su true.

Utilizzando il componente commenti come esempio, nell’istanza di authoring o di pubblicazione è stato effettuato l’accesso con privilegi di amministratore:

1. Passa a [CRXDE Liti](../../help/sites-developing/developing-with-crxde-lite.md)

   Ad esempio, [http://localhost:4503/crx/de](http://localhost:4503/crx/de)

1. Seleziona il nodo `jcr:content` del componente

   Ad esempio `/content/community-components/en/comments/jcr:content`

1. Aggiungi una proprietà

   * **Nome** `scg:showIde`
   * **Tipo** `String`
   * **Valore** `true`

1. Seleziona **[!UICONTROL Salva tutto]**
1. Ricarica la pagina Commenti nella guida

   [http://localhost:4503/content/community-components/en/comments.html](http://localhost:4503/content/community-components/en/comments.html)

1. Da notare che ora sono disponibili tre schede per Modelli, CSS e Dati.

![componente-community5](assets/community-component5.png)

![componente-community6](assets/community-component6.png)

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
