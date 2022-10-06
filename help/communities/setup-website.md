---
title: Imposta struttura sito Web
seo-title: Setup Website Structure
description: Configurare le directory
seo-description: Set up directories
uuid: a31edcd5-dab8-4a42-953b-1d076c2182b2
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: d18c0ece-4c4f-499c-ac94-a9aaa7f883c4
exl-id: 1f60a0d4-a272-45e8-9742-4b706be8502e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '543'
ht-degree: 1%

---

# Imposta struttura sito Web {#setup-website-structure}

Per configurare il sito web, le istruzioni riportate di seguito descrivono le cartelle da creare nelle seguenti posizioni:

* `/apps/an-scf-sandbox`

   È qui che risiedono le applicazioni e i modelli personalizzati.

* `/etc/designs/an-scf-sandbox`

   Qui risiedono gli elementi di progettazione scaricabili.

* `/content/an-scf-sandbox`

   In questo punto risiedono le pagine web scaricabili.

Il codice di questa esercitazione si basa sul fatto che il nome della cartella principale sia lo stesso per l&#39;applicazione, la progettazione e il contenuto. Se scegli un altro nome per il tuo sito web, sostituisci sempre `an-scf-sandbox` con il nome scelto.

>[!NOTE]
>
>Informazioni sui nomi:
>
>* I nomi visualizzati in CRXDE sono nomi di nodo che formano il percorso del contenuto indirizzabile.
>* I nomi dei nodi possono contenere spazi, ma se utilizzati in un URI, lo spazio deve essere codificato come &#39;%20&#39; o &#39;+&#39;.
>* I nomi dei nodi possono contenere trattini e trattini bassi, ma devono essere codificati quando si fa riferimento come nome di pacchetto all&#39;interno di un file Java. Sia i trattini che i trattini di sottolineatura sono preceduti dal relativo valore unicode:
   >
   >   * il trattino diventa &#39;_002d&#39;
   >   * carattere di sottolineatura diventa &#39;_005f&#39;


## Impostare la directory dell&#39;applicazione (/apps) {#setup-the-application-directory-apps}

La directory /apps nell&#39;archivio contiene il codice con implementa il comportamento e il rendering delle pagine servite dalla directory /content.

La directory /apps è protetta e non accessibile al pubblico così come le directory /content e /etc/designs .

1. Crea `/apps/an-scf-sandbox` cartella.

   Utilizzo **[!UICONTROL CRXDE Lite]**, nel riquadro explorer

   1. Seleziona la `/apps` cartella.
   1. Fai clic con il pulsante destro del mouse **[!UICONTROL Crea]**... o tirare giù il **[!UICONTROL Crea...]** menu.
   1. Seleziona **[!UICONTROL Crea cartella...]**.
   1. In **[!UICONTROL Crea cartella]** finestra di dialogo, immettere `an-scf-sandbox`.
   1. Fai clic su **[!UICONTROL OK]**.

1. Crea **[!UICONTROL componenti]** sottocartella.

   1. Seleziona la `/apps/an-scf-sandbox` cartella.
   1. Fai clic su **[!UICONTROL Crea > Crea cartella]**.
   1. In **[!UICONTROL Crea cartella]** finestra di dialogo, immettere **[!UICONTROL componenti]**.
   1. Fai clic su **[!UICONTROL OK]**.

1. Crea **[!UICONTROL modelli]** sottocartella.

   1. Seleziona la `/apps/an-scf-sandbox` cartella.
   1. Fai clic su **[!UICONTROL Crea > Crea cartella]**.
   1. In **[!UICONTROL Crea cartella]** finestra di dialogo, immettere **[!UICONTROL modelli]**.
   1. Fai clic su **[!UICONTROL OK]**.
   1. Seleziona nuovamente `/apps/an-scf-sandbox`.
   1. Seleziona **[!UICONTROL Salva tutto]**.

   Come per qualsiasi processo di modifica, puoi salvare spesso. Se si verificano problemi durante l’immissione dei dati, potrebbe essere dovuto al timeout dell’accesso o al salvataggio delle modifiche precedenti.

1. La struttura nel riquadro Esplora risorse di CRXDE Lite dovrebbe ora avere un aspetto simile al seguente:

   ![crxde-template](assets/crxde-template.png)

## Impostare la directory di progettazione (/etc/designs) {#setup-the-design-directory-etc-designs}

La directory /etc/designs contiene le immagini, gli script e i fogli di stile da scaricare insieme al contenuto della pagina.

1. Per utilizzare lo strumento Designer nell’interfaccia classica, individuare [https://&lt;server>:&lt;port>/miscadmin](http://localhost:4502/miscadmin).

   Nota: Se si utilizza CRXDE Lite per creare un nodo di tipo `cq:Page`, Controllo di accesso e replica non verranno impostati sulle impostazioni predefinite per una pagina.

1. Nel riquadro Esplora risorse, seleziona la **[!UICONTROL Disegni]** e fai clic su **[!UICONTROL Nuovo]** > **[!UICONTROL Nuova pagina]**.

   Inserisci:

   * Titolo: **[!UICONTROL Sandbox SCF]**
   * Nome: **[!UICONTROL sandbox an-scf]**
   * Seleziona **[!UICONTROL Modello di pagina di progettazione]**

   Fai clic su **[!UICONTROL Crea]**.

   ![modello di progettazione](assets/design-template.png)

1. Aggiornare il riquadro di esplorazione se la cartella &quot;Una Sandbox SCF&quot; non viene visualizzata.

1. Torna a CRXDE Lite (http:// localhost:4502/crx/de) ed espandi /etc/designs per vedere il nodo chiamato &quot;an-scf-sandbox&quot;.

   Nel riquadro inferiore a destra di CRXDE, puoi visualizzare la scheda Proprietà, la scheda Controllo accessi e la scheda Replica per vedere cosa è stato definito utilizzando il modello di pagina di progettazione.

   ![crxde-configure-template](assets/crxde-configure-template.png)

## Impostare la directory dei contenuti (/content) {#setup-the-content-directory-content}

La directory /content nell&#39;archivio è la posizione in cui si trova il contenuto del sito web. I percorsi sotto /content comprendono i percorsi dell’URL per le richieste del browser.

*Dopo* la [modello di pagina](initial-app.md#createthepagetemplate) viene creato come parte dell&#39;applicazione iniziale, il contenuto della pagina iniziale può essere creato in base al modello.... [**⇒**](initial-app.md)
