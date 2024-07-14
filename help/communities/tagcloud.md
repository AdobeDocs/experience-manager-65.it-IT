---
title: Utilizzo di Tag cloud per social network
description: Scopri come aggiungere un componente Cloud di tag per social network a una pagina che consenta ai membri della community con accesso esterno di identificare rapidamente gli argomenti di tendenza e individuare i contenuti con tag.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
exl-id: 56af5362-78de-4308-8958-63a45e8573cc
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '569'
ht-degree: 1%

---

# Utilizzo di Tag cloud per social network {#using-social-tag-cloud}

## Introduzione {#introduction}

Il componente `Social Tag Cloud` evidenzia i tag applicati dai membri della community durante la pubblicazione del contenuto. È un mezzo per identificare gli argomenti di tendenza e consentire ai visitatori del sito di individuare rapidamente i contenuti con tag.

Per un altro mezzo per identificare le tendenze correnti, visita [Tendenze attività](trends.md).

Questa pagina documenta le impostazioni della finestra di dialogo del componente `Social Tag Cloud` e descrive l&#39;esperienza utente.

Per informazioni dettagliate per gli sviluppatori, consulta [Tag Essentials](tag.md).

Per informazioni sulla creazione e la gestione dei tag e sui tag di contenuto applicati, vedere [Amministrazione dei tag](../../help/sites-administering/tags.md).

## Aggiunta di un tag cloud per social network {#adding-a-social-tag-cloud}

Per aggiungere un componente `Social Tag Cloud` a una pagina in modalità di modifica, utilizzare il browser componenti per individuare `Communities / Social Tag Cloud` e trascinarlo in una pagina in cui dovrebbe apparire il tag cloud.

Per informazioni necessarie, visitare [Nozioni di base sui componenti delle community](basics.md).

Quando sono incluse le [librerie lato client richieste](tag.md#essentials-for-client-side), il componente `Social Tag Cloud` viene visualizzato in questo modo:

![tag social](assets/social-tag.png)

## Configurazione di Tag Cloud per social network {#configuring-social-tag-cloud}

Selezionare il componente `Social Tag Cloud` inserito in modo da poter accedere e selezionare l&#39;icona `Configure` che apre la finestra di dialogo per modifica.

![configura](assets/configure-new.png)

Nella scheda **[!UICONTROL Tag cloud per social network]**, specifica i tag da visualizzare e, se i tag sono collegamenti attivi, il percorso della pagina per i risultati della ricerca:

![social-tag-cloud](assets/social-tag-cloud.png)

* **[!UICONTROL Tag per social network da visualizzare]**
Identifica i tag UGC da visualizzare. Le opzioni di pull-down sono:

   * `From page and child pages`
   * `All tags`

  Il valore predefinito è `From page and child pages`, dove &quot;page&quot; fa riferimento all&#39;impostazione **Page** riportata di seguito.

* **[!UICONTROL Pagina]**

  (Obbligatorio se non `All tags)` Percorso dell&#39;UGC per una pagina. Se lasciata vuota, la pagina corrente è predefinita.

* **[!UICONTROL Nessun collegamento sui tag]**

  Se questa opzione è selezionata, i tag vengono visualizzati nell’area dei tag come testo normale. Se questa opzione è deselezionata, i tag vengono visualizzati come collegamenti attivi che eseguono ricerche su tutto il contenuto a cui è applicato il tag. L&#39;impostazione predefinita è deselezionata e richiede l&#39;impostazione del **[!UICONTROL percorso dei risultati di ricerca]**.

* **[!UICONTROL Percorso risultati ricerca]**

  Percorso di una pagina in cui è stato inserito un componente `Search Result`, configurato per fare riferimento a UGC che include il percorso UGC specificato dall&#39;impostazione **Page**.

## Cambia visualizzazione tag cloud per social network {#change-display-of-social-tag-cloud}

Per modificare la visualizzazione di **Tag Cloud per social network**, immetti [Modalità progettazione](../../help/sites-authoring/default-components-designmode.md) e fai doppio clic sul componente `Social Tag Cloud` inserito per aprire una finestra di dialogo con una scheda aggiuntiva.

Utilizzando la scheda **[!UICONTROL Tag Cloud per social network (Progettazione)]**, specifica come vengono visualizzati i tag. Un tag può essere un tag semplice, una singola parola nello spazio dei nomi predefinito o una tassonomia gerarchica:

![social-tag-cloud-design](assets/social-tag-cloud-design.png)

* **[!UICONTROL Mostra percorsi titolo completi]**

  Se questa opzione è selezionata, mostra i titoli dei tag padre e dello spazio dei nomi per ogni tag applicato.

  Ad esempio:

   * Selezionato: `Geometrixx Media: Gadgets / Cars`
   * Deselezionato: `Cars`

  Non c’è differenza per un tag semplice.

  L&#39;impostazione predefinita è deselezionata.

* **[!UICONTROL Mostra solo tag foglia]**

  Se questa opzione è selezionata, vengono visualizzati solo i tag applicati che non contengono altri tag.

  Ad esempio, dato il TagID di:

  `Geometrixx Media: Gadgets / Cars`

  È possibile applicare tre tag:

  `Geometrixx Media (the namespace)`, `Gadgets` e `Cars`

   * Spunta: vengono visualizzati solo `Cars`, se applicati.
   * Deselezionato: `Geometrixx Media`, `Gadgets` e `Cars` sono visualizzati, se applicati.

  Un tag semplice è un tag foglia.

  L&#39;impostazione predefinita è deselezionata.

* **[!UICONTROL Modello collegamento]**

  Modello, diverso da quello predefinito, utilizzato per visualizzare i collegamenti in un’area tag quando i collegamenti sono abilitati tramite la finestra di dialogo di modifica del componente.

* **[!UICONTROL Stessa dimensione per tutti i tag]**

  Se questa opzione è selezionata, a tutte le parole presenti nell’area dei tag viene applicato lo stesso stile. Se questa opzione è deselezionata, lo stile delle parole varia a seconda dell&#39;utilizzo. L&#39;impostazione predefinita è deselezionata.

## Informazioni aggiuntive {#additional-information}

Ulteriori informazioni sono disponibili nella pagina [Tag Essentials](tag.md) per sviluppatori.

Per informazioni sulla creazione e la gestione dei tag, vedere [Assegnazione di tag a contenuti generati dagli utenti](tag-ugc.md) (UGC).
