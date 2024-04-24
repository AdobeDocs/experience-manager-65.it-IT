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

Il codice di questo tutorial si basa sul fatto che il nome della cartella principale sia lo stesso per l’applicazione, la progettazione e il contenuto. Se scegli un altro nome per il sito web, sostituisci sempre `an-scf-sandbox` con il nome scelto.

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

1. Crea `/apps/an-scf-sandbox` cartella.

   Utilizzo di **[!UICONTROL CRXDE Liti]**, nel riquadro dell&#39;elenco delle cartelle

   1. Seleziona la `/apps` cartella.
   1. Clic con il pulsante destro **[!UICONTROL Crea]**... o tirare giù il **[!UICONTROL Crea...]** menu.
   1. Seleziona **[!UICONTROL Crea cartella...]**.
   1. In **[!UICONTROL Crea cartella]** finestra di dialogo, immetti `an-scf-sandbox`.
   1. Fai clic su **[!UICONTROL OK]**.

1. Crea **[!UICONTROL componenti]** sottocartella

   1. Seleziona la `/apps/an-scf-sandbox` cartella.
   1. Clic **[!UICONTROL Crea > Crea cartella]**.
   1. In **[!UICONTROL Crea cartella]** finestra di dialogo, immetti **[!UICONTROL componenti]**.
   1. Fai clic su **[!UICONTROL OK]**.

1. Crea **[!UICONTROL modelli]** sottocartella

   1. Seleziona la `/apps/an-scf-sandbox` cartella.
   1. Clic **[!UICONTROL Crea > Crea cartella]**.
   1. In **[!UICONTROL Crea cartella]** finestra di dialogo, immetti **[!UICONTROL modelli]**.
   1. Fai clic su **[!UICONTROL OK]**.
   1. Riseleziona `/apps/an-scf-sandbox`.
   1. Seleziona **[!UICONTROL Salva tutto]**.

   Come per qualsiasi processo di modifica, è consigliabile salvare spesso. In caso di problemi durante l&#39;immissione dei dati, è possibile che il login sia scaduto o che si debbano salvare le modifiche precedenti.

1. La struttura nel riquadro Esplora di CRXDE Liti dovrebbe ora essere simile alla seguente:

   ![crxde-template](assets/crxde-template.png)

## Impostare la directory di progettazione (/etc/designs) {#setup-the-design-directory-etc-designs}

La directory /etc/designs contiene le immagini, gli script e i fogli di stile da scaricare insieme al contenuto della pagina.

1. Per utilizzare lo strumento Designer nell’interfaccia classica, passa a [https://&lt;server>:&lt;port>/miscadmin](http://localhost:4502/miscadmin).

   Nota: se si utilizza CRXDE Liti per creare un nodo di tipo `cq:Page`, il controllo di accesso e la replica non vengono impostati sulle impostazioni predefinite di una pagina.

1. Nel riquadro dell&#39;elenco delle cartelle, selezionare **[!UICONTROL Progettazioni]** cartella e quindi fare clic su **[!UICONTROL Nuovo]** > **[!UICONTROL Nuova pagina]**.

   Inserisci:

   * Titolo: **[!UICONTROL Una sandbox SCF]**
   * Nome: **[!UICONTROL an-scf-sandbox]**
   * Seleziona **[!UICONTROL Progettare il modello di pagina]**

   Fai clic su **[!UICONTROL Crea]**.

   ![design-template](assets/design-template.png)

1. Aggiornare il riquadro dell&#39;elenco delle cartelle se non viene visualizzata la cartella &quot;Sandbox SCF&quot;.

1. Torna a CRXDE Liti (http:// localhost:4502/crx/de) ed espandi /etc/designs per visualizzare il nodo denominato &quot;an-scf-sandbox&quot;.

   Nel riquadro inferiore destro di CRXDE è possibile visualizzare la scheda Proprietà, la scheda Controllo di accesso e la scheda Replica per visualizzare ciò che è stato definito utilizzando il modello della pagina di progettazione.

   ![crxde-configure-template](assets/crxde-configure-template.png)

## Configurare la directory dei contenuti (/content) {#setup-the-content-directory-content}

La directory /content nel repository è dove risiede il contenuto del sito Web. I percorsi in /content comprendono i percorsi dell’URL per le richieste del browser.

*Dopo* il [modello pagina](initial-app.md#createthepagetemplate) viene creato come parte dell’applicazione iniziale, il contenuto della pagina iniziale può essere creato in base al modello.... [**⇒**](initial-app.md)
