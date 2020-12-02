---
title: Utilizzo di Social Tag Cloud
seo-title: Utilizzo di Social Tag Cloud
description: Aggiunta di un componente Social Tag Cloud a una pagina
seo-description: Aggiunta di un componente Social Tag Cloud a una pagina
uuid: 8c400030-976c-457a-bb5f-e473909647a9
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 23a5a65e-774d-4789-9659-09e8be0c2bcd
translation-type: tm+mt
source-git-commit: 2fcd87cd1def7fc265ba40c83b50db86618f3b70
workflow-type: tm+mt
source-wordcount: '571'
ht-degree: 5%

---


# Utilizzo di Social Tag Cloud {#using-social-tag-cloud}

## Introduzione {#introduction}

Il componente `Social Tag Cloud` evidenzia i tag applicati dai membri della community durante la pubblicazione di contenuti. È uno strumento per identificare gli argomenti di tendenza e consentire ai visitatori del sito di individuare rapidamente il contenuto con tag.

Per identificare le tendenze correnti, visitare [Tendenze attività](trends.md).

Questa pagina documenta le impostazioni della finestra di dialogo del componente `Social Tag Cloud` e descrive l&#39;esperienza utente.

Per informazioni dettagliate per gli sviluppatori, consultate [Tag Essentials](tag.md).

Per informazioni sulla creazione e la gestione dei tag, nonché sui tag di contenuto applicati, consultate [Amministrazione dei tag](../../help/sites-administering/tags.md).

## Aggiunta di un social tag cloud {#adding-a-social-tag-cloud}

Per aggiungere un componente `Social Tag Cloud` a una pagina in modalità di creazione, usate il browser componenti per individuare `Communities / Social Tag Cloud` e trascinatelo nella posizione in una pagina in cui dovrebbe comparire il tag cloud.

Per le informazioni necessarie, visitare [Community Components Basics](basics.md).

Quando vengono incluse le [librerie lato client ](tag.md#essentials-for-client-side), viene visualizzato il componente `Social Tag Cloud`:

![social-tag](assets/social-tag.png)

## Configurazione di Social Tag Cloud {#configuring-social-tag-cloud}

Selezionare il componente `Social Tag Cloud` inserito a cui accedere e selezionare l&#39;icona `Configure` che apre la finestra di dialogo di modifica.

![configure](assets/configure-new.png)

Nella scheda **[!UICONTROL Social Tag Cloud]**, specificate i tag da visualizzare e, se i tag sono collegamenti attivi, la posizione della pagina per i risultati della ricerca:

![social-tag-cloud](assets/social-tag-cloud.png)

* **[!UICONTROL Tag per social network da]**
visualizzare: identificate i tag UGC da visualizzare. Le opzioni a discesa sono:

   * `From page and child pages`
   * `All tags`

   Il valore predefinito è `From page and child pages`, dove &quot;page&quot; fa riferimento all&#39;impostazione **Page** riportata di seguito.

* **[!UICONTROL Pagina]**

   (Obbligatorio se non `All tags)` Il percorso dell&#39;UGC per una pagina. Il valore predefinito è la pagina corrente, se lasciato vuoto.

* **[!UICONTROL Nessun collegamento sui tag]**

   Se questa opzione è selezionata, i tag vengono visualizzati nel tag cloud come testo normale. Se questa opzione è deselezionata, i tag vengono visualizzati come collegamenti attivi per la ricerca di tutto il contenuto a cui è applicato il tag. Il valore predefinito è deselezionato e richiede l&#39;impostazione di **[!UICONTROL Percorso risultato ricerca]**.

* **[!UICONTROL Percorso risultati ricerca]**

   Percorso di una pagina in cui è stato inserito un componente `Search Result`, configurato per fare riferimento a UGC che include il percorso UGC specificato dall&#39;impostazione **Page**.

## Modifica visualizzazione di Social Tag Cloud {#change-display-of-social-tag-cloud}

Per modificare la visualizzazione di **Social Tag Cloud**, immettere [Design Mode](../../help/sites-authoring/default-components-designmode.md) e fare doppio clic sul componente `Social Tag Cloud` inserito per aprire una finestra di dialogo con una scheda aggiuntiva.

Utilizzando la scheda **[!UICONTROL Social Tag Cloud (Design)]**, specificate in che modo vengono visualizzati i tag. Un tag può essere un tag semplice, una singola parola nello spazio dei nomi predefinito o una tassonomia gerarchica:

![social-tag-cloud-design](assets/social-tag-cloud-design.png)

* **[!UICONTROL Mostra percorsi titolo completi]**

   Se questa opzione è selezionata, mostra i titoli per i tag principali e lo spazio dei nomi per ciascun tag applicato.

   Esempio:

   * Selezionato: `Geometrixx Media: Gadgets / Cars`
   * Deselezionato: `Cars`

   Non c&#39;è differenza per un tag semplice.

   Il valore predefinito è deselezionato.

* **[!UICONTROL Mostra solo tag foglia]**

   Se questa opzione è selezionata, vengono visualizzati solo i tag applicati che non contengono altri tag.

   Ad esempio, dato il TagID di:

   `Geometrixx Media: Gadgets / Cars`

   È possibile applicare 3 tag:

   `Geometrixx Media (the namespace)`,  `Gadgets`e  `Cars`

   * Selezionato: Se applicato, verrà visualizzato solo `Cars`.
   * Non selezionato: Se applicati, vengono visualizzati `Geometrixx Media` e `Gadgets`nonché `Cars`.

   Un tag semplice è un tag foglia.

   Il valore predefinito è deselezionato.

* **[!UICONTROL Modello collegamento]**

   Modello, diverso da quello predefinito, utilizzato per visualizzare i collegamenti in un tag cloud quando i collegamenti sono attivati tramite la finestra di dialogo di modifica del componente.

* **[!UICONTROL Stessa dimensione per tutti i tag]**

   Se questa opzione è selezionata, tutte le parole nel tag cloud sono formattate allo stesso modo. Se questa opzione è deselezionata, le parole hanno uno stile diverso a seconda del loro utilizzo. Il valore predefinito è deselezionato.

## Informazioni aggiuntive {#additional-information}

Ulteriori informazioni sono disponibili nella pagina [Tag Essentials](tag.md) per gli sviluppatori.

Per informazioni sulla creazione e gestione dei tag, consultate [Assegnazione di tag a contenuti generati dall&#39;utente](tag-ugc.md) (UGC).
