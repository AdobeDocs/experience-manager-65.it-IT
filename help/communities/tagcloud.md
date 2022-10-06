---
title: Utilizzo di Social Tag Cloud
seo-title: Using Social Tag Cloud
description: Aggiunta di un componente Social Tag Cloud a una pagina
seo-description: Adding a Social Tag Cloud component to a page
uuid: 8c400030-976c-457a-bb5f-e473909647a9
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 23a5a65e-774d-4789-9659-09e8be0c2bcd
exl-id: 56af5362-78de-4308-8958-63a45e8573cc
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '558'
ht-degree: 5%

---

# Utilizzo di Social Tag Cloud {#using-social-tag-cloud}

## Introduzione {#introduction}

La `Social Tag Cloud` Il componente evidenzia i tag applicati dai membri della community durante la pubblicazione dei contenuti. È un mezzo per identificare gli argomenti di tendenza e consentire ai visitatori del sito di individuare rapidamente i contenuti con tag.

Per un altro modo di identificare le tendenze attuali, visita [Tendenze delle attività](trends.md).

Questa pagina documenta la `Social Tag Cloud` impostazioni della finestra di dialogo dei componenti e descrive l’esperienza utente.

Per informazioni dettagliate per gli sviluppatori vedi [Nozioni di base sui tag](tag.md).

Vedi [Amministrazione dei tag](../../help/sites-administering/tags.md) per informazioni sulla creazione e la gestione dei tag e sui tag di contenuto applicati.

## Aggiunta di un cloud di tag social {#adding-a-social-tag-cloud}

Per aggiungere una `Social Tag Cloud` componente per una pagina in modalità di creazione, usate il browser componenti per individuare `Communities / Social Tag Cloud` e trascinalo nella posizione in una pagina in cui dovrebbe essere visualizzato il tag cloud.

Per le informazioni necessarie, visita [Nozioni di base sui componenti di Communities](basics.md).

Quando il [librerie lato client richieste](tag.md#essentials-for-client-side) sono inclusi, è così che `Social Tag Cloud` apparirà il componente:

![social-tag](assets/social-tag.png)

## Configurazione di Social Tag Cloud {#configuring-social-tag-cloud}

Seleziona il `Social Tag Cloud` per accedere e selezionare il `Configure` che apre la finestra di dialogo di modifica.

![configurare](assets/configure-new.png)

Sotto la **[!UICONTROL Social Tag Cloud]** , specifica i tag da visualizzare e, se i tag sono collegamenti attivi, il percorso della pagina per i risultati della ricerca:

![social-tag-cloud](assets/social-tag-cloud.png)

* **[!UICONTROL Tag per social network da visualizzare]**
Identifica i tag UGC da visualizzare. Le opzioni a discesa sono:

   * `From page and child pages`
   * `All tags`

   Il valore predefinito è `From page and child pages`, dove &quot;page&quot; fa riferimento al **Pagina** di seguito.

* **[!UICONTROL Pagina]**

   (Obbligatorio se non `All tags)` Percorso dell’UGC per una pagina. Il valore predefinito è la pagina corrente se lasciato vuoto.

* **[!UICONTROL Nessun collegamento sui tag]**

   Se questa opzione è selezionata, i tag vengono visualizzati nel tag cloud come testo normale. Se questa opzione è deselezionata, i tag vengono visualizzati come collegamenti attivi che consentono di eseguire ricerche in tutto il contenuto a cui è applicato il tag. Il valore predefinito è deselezionato e richiede l&#39;opzione **[!UICONTROL Percorso dei risultati di ricerca]** da impostare.

* **[!UICONTROL Percorso risultati ricerca]**

   Percorso di una pagina in cui è `Search Result` il componente è stato posizionato, configurato per fare riferimento a UGC che include il percorso UGC specificato da **Pagina** impostazione.

## Modifica visualizzazione di Social Tag Cloud {#change-display-of-social-tag-cloud}

Per modificare la visualizzazione del **Social Tag Cloud**, inserisci [Modalità Progettazione](../../help/sites-authoring/default-components-designmode.md) e fai doppio clic sul `Social Tag Cloud` per aprire una finestra di dialogo con una scheda aggiuntiva.

Utilizzo della **[!UICONTROL Social Tag Cloud (progettazione)]** Specifica la modalità di visualizzazione dei tag. Un tag può essere un tag semplice, una singola parola nello spazio dei nomi predefinito o una tassonomia gerarchica:

![social-tag-cloud-design](assets/social-tag-cloud-design.png)

* **[!UICONTROL Mostra percorsi titolo completi]**

   Se questa opzione è selezionata, mostra i titoli dei tag principali e lo spazio dei nomi per ciascun tag applicato.

   Esempio:

   * Selezionato: `Geometrixx Media: Gadgets / Cars`
   * Deselezionato: `Cars`

   Non c&#39;è differenza per un tag semplice.

   Il valore predefinito è deselezionato.

* **[!UICONTROL Mostra solo tag foglia]**

   Se questa opzione è selezionata, vengono visualizzati solo i tag applicati che non contengono altri tag.

   Ad esempio, in base al TagID di:

   `Geometrixx Media: Gadgets / Cars`

   È possibile applicare 3 tag:

   `Geometrixx Media (the namespace)`, `Gadgets`, e `Cars`

   * Selezionato: Solo `Cars` viene visualizzato, se applicato.
   * Deselezionato: `Geometrixx Media` e `Gadgets`nonché `Cars` viene visualizzato, se applicato.

   Un tag semplice è un tag foglia.

   Il valore predefinito è deselezionato.

* **[!UICONTROL Modello collegamento]**

   Un modello, diverso da quello predefinito, utilizzato per visualizzare i collegamenti in un tag cloud quando i collegamenti sono attivati tramite la finestra di dialogo di modifica del componente.

* **[!UICONTROL Stessa dimensione per tutti i tag]**

   Se questa opzione è selezionata, tutte le parole nel tag cloud vengono formattate nello stesso modo. Se questa opzione è deselezionata, le parole vengono formattate in modo diverso a seconda del loro utilizzo. Il valore predefinito è deselezionato.

## Informazioni aggiuntive {#additional-information}

Per ulteriori informazioni, consulta [Nozioni di base sui tag](tag.md) per sviluppatori.

Vedi [Assegnazione tag ai contenuti generati dagli utenti](tag-ugc.md) (UGC) per informazioni sulla creazione e la gestione dei tag.
