---
title: Utilizzo di Tag cloud per social network
description: Scopri come aggiungere un componente Cloud di tag per social network a una pagina che consenta ai membri della community con accesso esterno di identificare rapidamente gli argomenti di tendenza e individuare i contenuti con tag.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
exl-id: 56af5362-78de-4308-8958-63a45e8573cc
source-git-commit: 62d4a8b3af5031ccc539d78f7d06a8cd1fec7af1
workflow-type: tm+mt
source-wordcount: '569'
ht-degree: 5%

---

# Utilizzo di Tag cloud per social network {#using-social-tag-cloud}

## Introduzione {#introduction}

Il `Social Tag Cloud` Il componente evidenzia i tag applicati dai membri della community durante la pubblicazione del contenuto. È un mezzo per identificare gli argomenti di tendenza e consentire ai visitatori del sito di individuare rapidamente i contenuti con tag.

Per un altro modo di identificare le tendenze attuali, visita [Tendenze attività](trends.md).

Questa pagina documenta `Social Tag Cloud` impostazioni della finestra di dialogo del componente e descrive l’esperienza utente.

Per informazioni dettagliate per gli sviluppatori, consulta [Nozioni di base sui tag](tag.md).

Consulta [Amministrazione dei tag](../../help/sites-administering/tags.md) per informazioni sulla creazione e la gestione dei tag e sui tag di contenuto applicati.

## Aggiunta di un tag cloud per social network {#adding-a-social-tag-cloud}

Per aggiungere una `Social Tag Cloud` a una pagina in modalità di authoring, utilizza il browser Componenti per individuare `Communities / Social Tag Cloud` e trascinarlo in una pagina in cui dovrebbe apparire l’area dei tag.

Per informazioni necessarie, visitare il sito [Nozioni di base sui componenti community](basics.md).

Quando [librerie lato client richieste](tag.md#essentials-for-client-side) sono inclusi, è così che `Social Tag Cloud` viene visualizzato il componente:

![tag social](assets/social-tag.png)

## Configurazione di Tag Cloud per social network {#configuring-social-tag-cloud}

Seleziona la inserita `Social Tag Cloud` in modo da poter accedere e selezionare `Configure` che apre la finestra di dialogo per modifica.

![configura](assets/configure-new.png)

Sotto **[!UICONTROL Tag cloud social]** , specificare i tag da visualizzare e, se i tag sono collegamenti attivi, la posizione della pagina per i risultati di ricerca:

![social-tag-cloud](assets/social-tag-cloud.png)

* **[!UICONTROL Tag per social network da visualizzare]**
Identifica i tag UGC da visualizzare. Le opzioni di pull-down sono:

   * `From page and child pages`
   * `All tags`

  Il valore predefinito è `From page and child pages`, dove &quot;page&quot; si riferisce al **Pagina** di seguito.

* **[!UICONTROL Pagina]**

  (Obbligatorio se non `All tags)` Percorso dell’UGC per una pagina. Se lasciata vuota, la pagina corrente è predefinita.

* **[!UICONTROL Nessun collegamento sui tag]**

  Se questa opzione è selezionata, i tag vengono visualizzati nell’area dei tag come testo normale. Se questa opzione è deselezionata, i tag vengono visualizzati come collegamenti attivi che eseguono ricerche su tutto il contenuto a cui è applicato il tag. L&#39;impostazione predefinita è deselezionata e richiede **[!UICONTROL Percorso risultati di ricerca]** da impostare.

* **[!UICONTROL Percorso risultati ricerca]**

  Percorso di una pagina in cui è presente un `Search Result` il componente è stato inserito, configurato per fare riferimento a UGC che include il percorso UGC specificato da **Pagina** impostazione.

## Cambia visualizzazione tag cloud per social network {#change-display-of-social-tag-cloud}

Per modificare la visualizzazione di **Tag cloud social**, immetti [Modalità Progettazione](../../help/sites-authoring/default-components-designmode.md) e fare doppio clic sul `Social Tag Cloud` per aprire una finestra di dialogo con una scheda aggiuntiva.

Utilizzo di **[!UICONTROL Tag cloud per social network (progettazione)]** , specificare la modalità di visualizzazione dei tag. Un tag può essere un tag semplice, una singola parola nello spazio dei nomi predefinito o una tassonomia gerarchica:

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

  `Geometrixx Media (the namespace)`, `Gadgets`, e `Cars`

   * Selezionato: Solo `Cars` vengono visualizzati, se applicati.
   * Deselezionato: `Geometrixx Media`, `Gadgets`, e `Cars` sono visualizzati, se applicati.

  Un tag semplice è un tag foglia.

  L&#39;impostazione predefinita è deselezionata.

* **[!UICONTROL Modello collegamento]**

  Modello, diverso da quello predefinito, utilizzato per visualizzare i collegamenti in un’area tag quando i collegamenti sono abilitati tramite la finestra di dialogo di modifica del componente.

* **[!UICONTROL Stessa dimensione per tutti i tag]**

  Se questa opzione è selezionata, a tutte le parole presenti nell’area dei tag viene applicato lo stesso stile. Se questa opzione è deselezionata, lo stile delle parole varia a seconda dell&#39;utilizzo. L&#39;impostazione predefinita è deselezionata.

## Informazioni aggiuntive {#additional-information}

Ulteriori informazioni sono disponibili sul sito [Nozioni di base sui tag](tag.md) pagina per sviluppatori.

Consulta [Assegnazione di tag ai contenuti generati dagli utenti](tag-ugc.md) (UGC) per informazioni sulla creazione e la gestione dei tag.
