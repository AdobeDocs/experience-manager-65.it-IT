---
title: Imposta struttura sito Web
description: Scopri come impostare la struttura del sito web, incluse le cartelle da creare.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 1f60a0d4-a272-45e8-9742-4b706be8502e
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '555'
ht-degree: 1%

---

# Imposta struttura sito Web {#setup-website-structure}

Per configurare il sito Web, le istruzioni seguenti descrivono le cartelle da creare nelle posizioni seguenti:

* `/apps/an-scf-sandbox`

  Qui risiedono applicazioni e modelli personalizzati.

* `/etc/designs/an-scf-sandbox`

  Qui risiedono gli elementi di progettazione scaricabili.

* `/content/an-scf-sandbox`

  Qui risiedono le pagine web scaricabili.

Il codice di questo tutorial si basa sul fatto che il nome della cartella principale sia lo stesso per l’applicazione, la progettazione e il contenuto. Se si sceglie un altro nome per il sito Web, sostituire sempre `an-scf-sandbox` con il nome scelto.

>[!NOTE]
>
>Informazioni sui nomi:
>
>* I nomi visualizzati in CRXDE sono nomi di nodo che costituiscono il percorso del contenuto indirizzabile.
>* I nomi dei nodi possono contenere spazi, ma se utilizzati in un URI, devono essere codificati come &#39;%20&#39; o &#39;+&#39;.
>* I nomi dei nodi possono contenere trattini e trattini bassi, ma devono essere codificati quando vengono indicati come nomi di pacchetti all’interno di un file Java™. Sia i trattini che i caratteri di sottolineatura sono preceduti dal carattere di escape underscore seguito dal relativo valore Unicode:
>
>   * il trattino diventa &#39;_002d&#39;
>   * il carattere di sottolineatura diventa &#39;_005f&#39;

## Configurare la directory applicazioni (/apps) {#setup-the-application-directory-apps}

La directory /apps nell’archivio contiene il codice con implementa il comportamento e il rendering delle pagine fornite dalla directory /content.

La directory /apps è protetta e non è accessibile al pubblico, così come le directory /content e /etc/designs.

1. Crea la cartella `/apps/an-scf-sandbox`.

   Utilizzo di **[!UICONTROL CRXDE Liti]** nel riquadro dell&#39;elenco delle cartelle

   1. Selezionare la cartella `/apps`.
   1. Fare clic con il pulsante destro del mouse su **[!UICONTROL Crea]**... o trascinare il menu **[!UICONTROL Crea...]**.
   1. Seleziona **[!UICONTROL Crea cartella...]**.
   1. Nella finestra di dialogo **[!UICONTROL Crea cartella]** immettere `an-scf-sandbox`.
   1. Fai clic su **[!UICONTROL OK]**.

1. Crea la sottocartella **[!UICONTROL components]**.

   1. Selezionare la cartella `/apps/an-scf-sandbox`.
   1. Fare clic su **[!UICONTROL Crea > Crea cartella]**.
   1. Nella finestra di dialogo **[!UICONTROL Crea cartella]** immettere **[!UICONTROL componenti]**.
   1. Fai clic su **[!UICONTROL OK]**.

1. Crea la sottocartella **[!UICONTROL templates]**.

   1. Selezionare la cartella `/apps/an-scf-sandbox`.
   1. Fare clic su **[!UICONTROL Crea > Crea cartella]**.
   1. Nella finestra di dialogo **[!UICONTROL Crea cartella]** immettere **[!UICONTROL modelli]**.
   1. Fai clic su **[!UICONTROL OK]**.
   1. Riselezionare `/apps/an-scf-sandbox`.
   1. Seleziona **[!UICONTROL Salva tutto]**.

   Come per qualsiasi processo di modifica, è consigliabile salvare spesso. In caso di problemi durante l&#39;immissione dei dati, è possibile che il login sia scaduto o che si debbano salvare le modifiche precedenti.

1. La struttura nel riquadro Esplora di CRXDE Lite dovrebbe ora essere simile alla seguente:

   ![modello-crxde](assets/crxde-template.png)

## Impostare la directory di progettazione (/etc/designs) {#setup-the-design-directory-etc-designs}

La directory /etc/designs contiene le immagini, gli script e i fogli di stile da scaricare insieme al contenuto della pagina.

1. Per utilizzare lo strumento Designer nell&#39;interfaccia classica, passare a [https://&lt;server>:&lt;port>/miscadmin](http://localhost:4502/miscadmin).

   Nota: se si utilizza CRXDE Lite per creare un nodo di tipo `cq:Page`, il controllo di accesso e la replica non verranno impostati sulle impostazioni predefinite per una pagina.

1. Nel riquadro dell&#39;elenco delle cartelle selezionare la cartella **[!UICONTROL Designs]** e quindi fare clic su **[!UICONTROL New]** > **[!UICONTROL New Page]**.

   Inserisci:

   * Titolo: **[!UICONTROL Sandbox SCF]**
   * Nome: **[!UICONTROL an-scf-sandbox]**
   * Seleziona **[!UICONTROL Modello per pagina progettazione]**

   Fai clic su **[!UICONTROL Crea]**.

   ![modello-progettazione](assets/design-template.png)

1. Aggiornare il riquadro dell&#39;elenco delle cartelle se non viene visualizzata la cartella &quot;Sandbox SCF&quot;.

1. Torna a CRXDE Lite (http:// localhost:4502/crx/de) ed espandi /etc/designs per visualizzare il nodo denominato &quot;an-scf-sandbox&quot;.

   Nel riquadro inferiore destro di CRXDE è possibile visualizzare la scheda Proprietà, la scheda Controllo di accesso e la scheda Replica per visualizzare ciò che è stato definito utilizzando il modello della pagina di progettazione.

   ![crxde-configure-template](assets/crxde-configure-template.png)

## Configurare la directory dei contenuti (/content) {#setup-the-content-directory-content}

La directory /content nel repository è dove risiede il contenuto del sito Web. I percorsi in /content comprendono i percorsi dell’URL per le richieste del browser.

*Dopo* che il [modello di pagina](initial-app.md#createthepagetemplate) è stato creato come parte dell&#39;applicazione iniziale, è possibile creare il contenuto della pagina iniziale in base al modello.... [**⇒**](initial-app.md)
