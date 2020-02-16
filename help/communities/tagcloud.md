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
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Utilizzo di Social Tag Cloud {#using-social-tag-cloud}

## Introduzione {#introduction}

Il `Social Tag Cloud` componente evidenzia i tag applicati dai membri della community durante la pubblicazione dei contenuti. È uno strumento per identificare gli argomenti di tendenza e consentire ai visitatori del sito di individuare rapidamente il contenuto con tag.

Per un altro mezzo per identificare le tendenze correnti, visita Tendenze [](trends.md)attività.

In questa pagina sono documentate le impostazioni della finestra di dialogo del `Social Tag Cloud` componente e viene descritta l’esperienza utente.

Per informazioni dettagliate per gli sviluppatori, consulta [Tag Essentials](tag.md).

See [Administering Tags](../../help/sites-administering/tags.md) for information about creating and managing tags, as well as to which content tags have been applied.

## Aggiunta di un social tag Cloud {#adding-a-social-tag-cloud}

Per aggiungere un `Social Tag Cloud` componente a una pagina in modalità di creazione, usate il browser Componenti per individuarlo `Communities / Social Tag Cloud` e trascinarlo nella posizione desiderata su una pagina in cui dovrebbe comparire il tag cloud.

Per le informazioni necessarie, visita [Community Components Basics](basics.md).

Quando sono incluse le librerie [lato client](tag.md#essentials-for-client-side) richieste, verrà visualizzato il `Social Tag Cloud` componente:

![chlimage_1-303](assets/chlimage_1-303.png)

## Configurazione di Social Tag Cloud {#configuring-social-tag-cloud}

Selezionate il `Social Tag Cloud` componente inserito a cui accedere e selezionate l’ `Configure` icona che apre la finestra di dialogo di modifica.

![chlimage_1-304](assets/chlimage_1-304.png)

Nella scheda **[!UICONTROL Social Tag Cloud]** , specificate i tag da visualizzare e, se i tag sono collegamenti attivi, la posizione della pagina per i risultati della ricerca.:

![chlimage_1-305](assets/chlimage_1-305.png)

* **[!UICONTROL Tag per social network per visualizzare]** Identificare i tag UGC da visualizzare. Le opzioni a discesa sono

   * `From page and child pages`
   * `All tags`
   Il valore predefinito è `From page and child pages`, dove &quot;page&quot; fa riferimento all’impostazione **Pagina** riportata di seguito.

* **[!UICONTROL Page]**(obbligatorio se non `All tags)` il percorso dell&#39;UGC per una pagina. Il valore predefinito è la pagina corrente se lasciato vuoto.

* **[!UICONTROL Nessun collegamento sui tag]** Se questa opzione è selezionata, i tag vengono visualizzati nel tag cloud come testo normale. Se questa opzione è deselezionata, i tag vengono visualizzati come collegamenti attivi per la ricerca di tutto il contenuto a cui è applicato il tag. Il valore predefinito è deselezionato e richiede l&#39;impostazione del percorso **[!UICONTROL dei risultati di]** ricerca.

* **[!UICONTROL Percorso]** risultato ricerca Il percorso di una pagina in cui è stato inserito un `Search Result` componente, configurato per fare riferimento a UGC che include il percorso UGC specificato dall’impostazione **Pagina** .

## Modifica visualizzazione di Social Tag Cloud {#change-display-of-social-tag-cloud}

Per modificare la visualizzazione di **Social Tag Cloud**, entrate in modalità [](../../help/sites-authoring/default-components-designmode.md) Progettazione e fate doppio clic sul `Social Tag Cloud` componente inserito per aprire una finestra di dialogo con una scheda aggiuntiva.

Utilizzando la scheda **[!UICONTROL Social Tag Cloud (Progettazione)]** , specificate il modo in cui i tag vengono visualizzati. Un tag può essere un tag semplice, una singola parola nello spazio dei nomi predefinito o una tassonomia gerarchica:

![chlimage_1-306](assets/chlimage_1-306.png)

* **[!UICONTROL Mostra percorsi]** del titolo completi Se questa opzione è selezionata, vengono visualizzati i titoli dei tag principali e lo spazio dei nomi per ciascun tag applicato.

   Esempio:

   * Selezionato: `Geometrixx Media: Gadgets / Cars`
   * Deselezionato: `Cars`
   Non c&#39;è differenza per un tag semplice.

   Il valore predefinito è deselezionato.

* **[!UICONTROL Mostra solo tag]** foglia Se questa opzione è selezionata, vengono visualizzati solo i tag applicati che non contengono altri tag.

   Ad esempio, dato il tagID di

   `Geometrixx Media: Gadgets / Cars`

   È possibile applicare 3 tag: `Geometrixx Media (the namespace)`, `Gadgets`e `Cars`

   * Selezionato: viene `Cars` visualizzato solo se applicato
   * Non selezionato: `Geometrixx Media` e `Gadgets`così come `Cars` verrà visualizzata, se applicata
   Un tag semplice è un tag foglia.

   Il valore predefinito è deselezionato.

* **[!UICONTROL Modello]** collegamento Un modello, diverso da un modello predefinito, utilizzato per visualizzare i collegamenti in un tag cloud quando i collegamenti sono attivati tramite la finestra di dialogo di modifica del componente.

* **[!UICONTROL Stessa dimensione per tutti i tag]** Se questa opzione è selezionata, tutte le parole nel tag cloud sono formattate allo stesso modo. Se questa opzione è deselezionata, le parole hanno uno stile diverso a seconda del loro utilizzo. Il valore predefinito è deselezionato.

## Informazioni aggiuntive {#additional-information}

Ulteriori informazioni sono disponibili nella pagina [Tag Essentials](tag.md) per gli sviluppatori.

Per informazioni sulla creazione e gestione dei tag, consultate [Assegnazione di tag ai contenuti](tag-ugc.md) generati dagli utenti (UGC, Tagging User Generated Content).
