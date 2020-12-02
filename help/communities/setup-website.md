---
title: Imposta struttura sito Web
seo-title: Imposta struttura sito Web
description: Configurare le directory
seo-description: Configurare le directory
uuid: a31edcd5-dab8-4a42-953b-1d076c2182b2
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: d18c0ece-4c4f-499c-ac94-a9aaa7f883c4
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 1%

---


# Imposta struttura sito Web {#setup-website-structure}

Per impostare il sito Web, le istruzioni riportate di seguito descrivono le cartelle da creare nei seguenti percorsi:

* `/apps/an-scf-sandbox`

   Qui risiedono le applicazioni e i modelli personalizzati.

* `/etc/designs/an-scf-sandbox`

   Qui risiedono gli elementi di progettazione scaricabili.

* `/content/an-scf-sandbox`

   Qui risiedono le pagine Web scaricabili.

Il codice riportato in questa esercitazione si basa sul fatto che il nome della cartella principale sia lo stesso per l’applicazione, la progettazione e il contenuto. Se scegliete un altro nome per il sito Web, sostituite sempre `an-scf-sandbox` con il nome scelto.

>[!NOTE]
>
>Informazioni sui nomi:
>
>* I nomi visualizzati in CRXDE sono nomi di nodi che costituiscono il percorso al contenuto indirizzabile.
>* I nomi dei nodi possono contenere spazi, ma se utilizzati in un URI, lo spazio deve essere codificato come &#39;%20&#39; o &#39;+&#39;.
>* I nomi dei nodi possono contenere trattini e caratteri di sottolineatura, ma devono essere codificati se vi viene fatto riferimento come nome di pacchetto all&#39;interno di un file Java. Sia i trattini che i caratteri di sottolineatura sono preceduti dal relativo valore Unicode:

   >
   >   
   * hyphen diventa &#39;_002d&#39;
   >   * carattere di sottolineatura diventa &#39;_005f&#39;


## Configurare la directory applicazione (/apps) {#setup-the-application-directory-apps}

La directory /apps nell&#39;archivio contiene il codice con implementa il comportamento e il rendering delle pagine servite dalla directory /content.

La directory /apps è protetta e non accessibile al pubblico così come le directory /content e /etc/designs.

1. Creare la cartella `/apps/an-scf-sandbox`.

   Utilizzo di **[!UICONTROL CRXDE Lite]** nel riquadro di esplorazione

   1. Selezionare la cartella `/apps`.
   1. Fare clic con il pulsante destro del mouse su **[!UICONTROL Crea]**... oppure premere il tasto **[!UICONTROL Crea...]**.
   1. Selezionare **[!UICONTROL Crea cartella...]**.
   1. Nella finestra di dialogo **[!UICONTROL Crea cartella]**, immettere `an-scf-sandbox`.
   1. Fai clic su **[!UICONTROL OK]**.

1. Creare la sottocartella **[!UICONTROL components]**.

   1. Selezionare la cartella `/apps/an-scf-sandbox`.
   1. Fare clic su **[!UICONTROL Crea > Crea cartella]**.
   1. Nella finestra di dialogo **[!UICONTROL Crea cartella]**, immettere **[!UICONTROL components]**.
   1. Fai clic su **[!UICONTROL OK]**.

1. Creare la sottocartella **[!UICONTROL templates]**.

   1. Selezionare la cartella `/apps/an-scf-sandbox`.
   1. Fare clic su **[!UICONTROL Crea > Crea cartella]**.
   1. Nella finestra di dialogo **[!UICONTROL Crea cartella]**, immettere **[!UICONTROL templates]**.
   1. Fai clic su **[!UICONTROL OK]**.
   1. Selezionare nuovamente `/apps/an-scf-sandbox`.
   1. Selezionare **[!UICONTROL Salva tutto]**.

   Come per qualsiasi processo di modifica, salvate spesso. Se si verificano problemi durante l’immissione dei dati, è possibile che l’accesso sia scaduto o che sia necessario salvare le modifiche precedenti.

1. La struttura nel riquadro di esplorazione del CRXDE Lite deve ora essere simile alla seguente:

   ![crxde-template](assets/crxde-template.png)

## Configurare la directory di progettazione (/etc/designs) {#setup-the-design-directory-etc-designs}

La directory /etc/designs contiene le immagini, gli script e i fogli di stile da scaricare insieme al contenuto della pagina.

1. Per utilizzare lo strumento Designer nell&#39;interfaccia classica, individuare [https://&lt;server>:&lt;porta>/miscadmin](http://localhost:4502/miscadmin).

   Nota: Se si utilizza CRXDE Lite per creare un nodo di tipo `cq:Page`, il controllo di accesso e la replica non verranno impostati sulle impostazioni predefinite per una pagina.

1. Nel riquadro Esplora risorse, selezionare la cartella **[!UICONTROL Progettazione]**, quindi fare clic su **[!UICONTROL Nuova]** > **[!UICONTROL Nuova pagina]**.

   Invio:

   * Titolo: **[!UICONTROL Un sandbox SCF]**
   * Nome: **[!UICONTROL an-scf-sandbox]**
   * Selezionare **[!UICONTROL Modello pagina di progettazione]**

   Fai clic su **[!UICONTROL Crea]**.

   ![design-template](assets/design-template.png)

1. Aggiornate il riquadro di esplorazione se la cartella &quot;Una sandbox SCF&quot; non viene visualizzata.

1. Tornate al CRXDE Lite (http:// localhost:4502/crx/de) ed espandete /etc/designs per visualizzare il nodo denominato &quot;an-scf-sandbox&quot;.

   Nel riquadro inferiore destro di CRXDE, è possibile visualizzare la scheda Proprietà, la scheda Controllo accesso e la scheda Replica per vedere cosa è stato definito utilizzando il modello di pagina di progettazione.

   ![crxde-configure-template](assets/crxde-configure-template.png)

## Configurare la directory dei contenuti (/content) {#setup-the-content-directory-content}

La directory /content nel repository è la posizione in cui risiede il contenuto del sito Web. I percorsi in /content comprendono i percorsi dell&#39;URL per le richieste del browser.

*Dopo la* creazione dei  [modelli di ](initial-app.md#createthepagetemplate) pagina come parte dell’applicazione iniziale, il contenuto della pagina iniziale può essere creato in base al modello....  [**⇒**](initial-app.md)
