---
title: Amministrazione dei tag
seo-title: Amministrazione dei tag
description: Scopri come amministrare i tag in AEM.
seo-description: Scopri come amministrare i tag in AEM.
uuid: 77e1280a-feea-4edd-94b6-4fb825566c42
contentOwner: Chiradeep Majumdar
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: content
content-type: reference
discoiquuid: 69253ee9-8c28-436b-9331-6fb875f64cba
translation-type: tm+mt
source-git-commit: 1c1ade947f2cbd26b35920cfd10b1666b132bcbd
workflow-type: tm+mt
source-wordcount: '1769'
ht-degree: 7%

---


# Amministrazione dei tag {#administering-tags}

I tag sono un metodo semplice e veloce per classificare i contenuti di un sito web. Possono essere considerati parole chiave o etichette (metadati) che consentono di trovare più rapidamente il contenuto a seguito di una ricerca.

In Adobe Experience Manager (AEM), un tag può essere una proprietà di

* un nodo di contenuto per una pagina (vedere [Utilizzo di tag](/help/sites-authoring/tags.md))

* un nodo di metadati per una risorsa (consultate [Gestione dei metadati per le risorse digitali](/help/assets/metadata.md))

Oltre alle pagine e alle risorse, i tag vengono utilizzati per  funzioni di AEM Communities

* contenuto generato dall&#39;utente (vedere [Tagging UGC)](/help/communities/tag-ugc.md)

* Risorse di abilitazione (vedere [Risorse per l&#39;abilitazione dei tag](/help/communities/functions.md#catalog-function))

## Funzioni tag {#tag-features}

Alcune delle funzioni dei tag all&#39;interno AEM includono:

* I tag possono essere raggruppati in vari spazi dei nomi. Tali gerarchie consentono di creare tassonomie Queste tassonomie sono globali in tutta AEM.
* La limitazione principale per i nuovi tag creati è che devono essere univoci all&#39;interno di uno specifico namespace.
* Il titolo di un tag non deve includere caratteri di separazione dei percorsi dei tag (né saranno visualizzati se presenti)

   * due punti `:` - delimita il tag namespace
   * barra avanti `/` - delimita i tag secondari

* I tag possono essere applicati dagli autori e dai visitatori del sito. A prescindere dalla modalità di creazione, tutti i tipi di tag possono essere selezionati sia per essere assegnati a una pagina, sia per operazioni di ricerca.
* I tag possono essere creati e la loro tassonomia può essere modificata dai membri del gruppo &quot;tag-administrators&quot; e dai membri che dispongono dei diritti di modifica su `/content/cq:tags`.

   * Un tag che contiene tag secondari viene definito tag contenitore
   * Un tag che non è un tag contenitore è definito tag foglia
   * Uno spazio dei nomi tag è un tag foglia o contenitore

* I tag vengono utilizzati dal componente [Ricerca](https://helpx.adobe.com/experience-manager/core-components/using/quick-search.html) per facilitare la ricerca del contenuto.
* I tag vengono utilizzati dal componente [Teaser](https://helpx.adobe.com/experience-manager/core-components/using/teaser.html), che controlla il tag cloud di un utente per fornire contenuti mirati.
* Se l’assegnazione di tag è un aspetto importante del contenuto

   * creare pacchetti di tag con le pagine che li utilizzano
   * assicurarsi che [autorizzazioni dei tag](#setting-tag-permissions) sia abilitata l&#39;accesso in lettura

## Console di assegnazione tag {#tagging-console}

La console Tagging consente di creare e gestire i tag e le rispettive tassonomie. Un obiettivo è quello di evitare di avere molti tag simili relativi sostanzialmente la stessa cosa: ad esempio, pagina e pagine o calzature e scarpe.

I tag vengono gestiti raggruppandoli in spazi di nomi, controllando l’utilizzo dei tag esistenti prima di crearne di nuovi e riorganizzandoli senza scollegare il tag dal contenuto attualmente a cui si fa riferimento.

Per accedere alla console Tagging:

* sull&#39;autore
* accesso con privilegi amministrativi
* dalla navigazione globale

   * select **`Tools`**
   * select **`General`**
   * select **`Tagging`**

![managing_tags_using_thetagasministrationconsole](assets/managing_tags_usingthetagasministrationconsolea.png)

### Creazione di uno spazio dei nomi {#creating-a-namespace}

Per creare un nuovo spazio nomi, selezionate l&#39;icona **`Create Namespace`**.

Lo spazio nomi è di per sé un tag e non deve contenere tag secondari. Tuttavia, per continuare a creare una tassonomia, [creare tag secondari](#creating-tags), che a loro volta possono essere tag foglia o contenitore.

![chlimage_1-183](assets/chlimage_1-183a.png) ![creating_tags_andnamespaces](assets/creating_tags_andnamespacesa.png)

* **Titolo**

   *(obbligatorio)* Titolo visualizzato per lo spazio dei nomi.

* **Nome**
   *(facoltativo)* Un nome per lo spazio dei nomi. Se non viene specificato, dal Titolo viene creato un nome di nodo valido. Vedere [TagID](/help/sites-developing/framework.md#tagid).

* **Descrizione**

   *(facoltativo)* Una descrizione dello spazio dei nomi.

Una volta inserite le informazioni richieste

* selezionare **Crea**

### Operazioni sui tag {#operations-on-tags}

Quando si seleziona uno spazio nomi o un altro tag, sono disponibili le operazioni seguenti:

* [Visualizza proprietà](#viewing-tag-properties)
* [Riferimenti](#showing-tag-references)
* [Crea tag](#creating-tags)
* [Modifica](#editing-tags)
* [Sposta](#moving-tags)
* [Unisci](#merging-tags)
* [Pubblicazione](#publishing-tags)
* [Annulla pubblicazione](#unpublishing-tags)
* [Elimina](#deleting-tags)

![chlimage_1-184](assets/chlimage_1-184.png)

Quando la finestra del browser non è abbastanza ampia per visualizzare tutte le icone, le icone più a destra sono raggruppate sotto un&#39;icona **`... More`**, che mostrerà un elenco a discesa delle icone delle operazioni nascoste quando è selezionata.

![chlimage_1-185](assets/chlimage_1-185.png)

### Selezione di un tag spazio nomi {#selecting-a-namespace-tag}

Quando è selezionata la prima volta, se lo spazio nomi non contiene tag, le proprietà vengono visualizzate a destra, altrimenti i tag secondari vengono visualizzati. Ogni tag selezionato visualizzerà i tag che contiene o le relative proprietà, se non dispone di tag secondari.

Per selezionare il tag per le operazioni e per selezionare più volte, selezionate solo l&#39;icona accanto al titolo. Selezionando il titolo verranno visualizzate solo le proprietà o si aprirà il tag per visualizzarne il contenuto.

![chlimage_1-186](assets/chlimage_1-186.png) ![chlimage_1-187](assets/chlimage_1-187.png)

### Visualizzazione delle proprietà dei tag {#viewing-tag-properties}

![chlimage_1-188](assets/chlimage_1-188.png)

Quando si seleziona uno spazio dei nomi o un altro tag, quando si seleziona l&#39;icona **`View Properties`** vengono visualizzate le informazioni relative a `name`, ora dell&#39;ultima modifica e numero di riferimenti. Se pubblicato, vengono visualizzati l’ora dell’ultima pubblicazione e l’ID dell’editore. Queste informazioni verranno visualizzate in una colonna a sinistra delle colonne del tag.

![chlimage_1-189](assets/chlimage_1-189.png)

### Visualizzazione dei riferimenti di tag {#showing-tag-references}

![chlimage_1-190](assets/chlimage_1-190.png)

Quando è selezionato uno spazio dei nomi o un altro tag, selezionando l&#39;icona **References** si identificherà il contenuto a cui è stato applicato il tag.

La visualizzazione iniziale è un numero totale di tag applicati.

![chlimage_1-191](assets/chlimage_1-191.png)

Selezionando la freccia a destra del conteggio, vengono elencati i nomi di riferimento.

Il percorso del riferimento viene visualizzato come una descrizione quando si passa il puntatore del mouse su un riferimento.

![chlimage_1-192](assets/chlimage_1-192.png)

### Creazione di tag {#creating-tags}

![chlimage_1-193](assets/chlimage_1-193.png)

Quando si seleziona uno spazio dei nomi o un altro tag (selezionando l&#39;icona accanto al titolo), è possibile creare un tag secondario per il tag corrente selezionando l&#39;icona **`Create Tag`**.

![chlimage_1-194](assets/chlimage_1-194.png)

* **Titolo**
* (richiesto) *Titolo visualizzato per il tag.

* **Nome**
* (facoltativo) *Un nome per il tag. Se non viene specificato, dal Titolo viene creato un nome di nodo valido. Vedere [TagID](/help/sites-developing/framework.md#tagid).

* **Descrizione**
* (facoltativo) *Una descrizione del tag.

Una volta inserite le informazioni richieste

* selezionare **Crea**

### Modifica dei tag {#editing-tags}

![chlimage_1-195](assets/chlimage_1-195.png)

Quando è selezionato uno spazio dei nomi o un altro tag, è possibile modificare il Titolo, la Descrizione e fornire le localizzazioni del Titolo selezionando l&#39;icona **`Edit`**.

Dopo aver apportato le modifiche, selezionare **Salva**.

Per informazioni dettagliate sull&#39;aggiunta di traduzioni in lingua, vedere la sezione relativa alla [Gestione dei tag in lingue diverse](#managing-tags-in-different-languages).

![chlimage_1-196](assets/chlimage_1-196.png)

### Spostamento dei tag {#moving-tags}

![chlimage_1-197](assets/chlimage_1-197.png)

Quando è selezionato uno spazio dei nomi o un altro tag, selezionando l&#39;icona **`Move`** gli amministratori e gli sviluppatori di tag potranno ripulire la tassonomia spostando il tag in una nuova posizione o rinominandolo. Quando il tag selezionato è un tag contenitore, lo spostamento del tag determina anche lo spostamento di tutti i tag secondari.

>[!NOTE]
>
>È consigliabile che gli autori possano solo [modificare](#editing-tags) il tag `title`, non spostare o rinominare i tag.

![chlimage_1-198](assets/chlimage_1-198.png)

* **Percorso**

   *(sola lettura)* Percorso corrente del tag selezionato.

* **Passa**
a: consente di individuare il nuovo percorso in cui spostare il tag.

* **Rinomina**
inInizialmente visualizza la variabile corrente 
`name`del tag . È possibile inserire un nuovo elemento `name`.

* selezionare **Save**

### Unione dei tag {#merging-tags}

![chlimage_1-199](assets/chlimage_1-199.png)

Se una tassonomia include duplicati, è possibile unire i tag. Quando il tag A viene unito al tag B, tutte le pagine contrassegnate con il tag A vengono contrassegnate con il tag B e il tag A non è più disponibile per gli autori.

Quando è selezionato uno spazio dei nomi o un altro tag, selezionando l&#39;icona **Merge** si aprirà un pannello in cui è possibile selezionare il percorso in cui unire.

![chlimage_1-200](assets/chlimage_1-200.png)

* **Percorso**

   *(sola lettura)* Percorso del tag selezionato per l&#39;unione in un altro tag.

* **Unisci**
in Sfoglia per selezionare il percorso del tag in cui unire.

>[!NOTE]
>
>Dopo l&#39;unione, il **Percorso** selezionato originariamente (virtualmente) non esisterà più.
>
>Quando un tag di riferimento viene spostato o unito, il tag non viene eliminato fisicamente in modo da poter mantenere i riferimenti.

### Pubblicazione dei tag {#publishing-tags}

![chlimage_1-201](assets/chlimage_1-201.png)

Quando è selezionato uno spazio dei nomi o un altro tag, selezionate l&#39;icona **Pubblica** per attivare il tag nell&#39;ambiente di pubblicazione. Analogamente al contenuto della pagina, viene pubblicato solo il tag selezionato, a prescindere dal fatto che si tratti o meno di un tag contenitore.

Per pubblicare una tassonomia (uno spazio dei nomi e dei tag secondari), è consigliabile creare un [pacchetto](/help/sites-administering/package-manager.md) dello spazio dei nomi (vedere [Nodo radice tassonomia](/help/sites-developing/framework.md#taxonomy-root-node)). Prima di creare il pacchetto, assicuratevi di [applicare le autorizzazioni](#setting-tag-permissions) allo spazio dei nomi.

### Annullamento della pubblicazione dei tag {#unpublishing-tags}

![chlimage_1-202](assets/chlimage_1-202.png)

Quando è selezionato uno spazio dei nomi o un altro tag, selezionando l&#39;icona **Annulla pubblicazione** il tag viene disattivato nell&#39;ambiente di creazione e rimosso dall&#39;ambiente di pubblicazione. Analogamente all&#39;operazione `Delete`se il tag selezionato è un tag contenitore, tutti i relativi tag secondari saranno disattivati nell&#39;ambiente di authoring e rimossi dall&#39;ambiente di pubblicazione.

### Eliminazione dei tag {#deleting-tags}

![chlimage_1-203](assets/chlimage_1-203.png)

Quando è selezionato uno spazio dei nomi o un altro tag, selezionando l&#39;icona **Elimina** il tag viene rimosso definitivamente dall&#39;ambiente di authoring. Se il tag è stato pubblicato, viene rimosso anche dall’ambiente di pubblicazione. Se il tag selezionato è un tag contenitore, verranno rimossi anche tutti i tag secondari corrispondenti.

## Impostazione delle autorizzazioni per i tag {#setting-tag-permissions}

Le autorizzazioni dei tag sono [&#39;secure (per impostazione predefinita)&#39;](/help/sites-administering/production-ready.md); una procedura ottimale per l’ambiente di pubblicazione che richiede l’autorizzazione di lettura per i tag. Per impostazione di base, questo viene fatto creando un pacchetto dello spazio dei nomi dei tag dopo che le autorizzazioni sono state impostate sull’autore e installando il pacchetto su tutte le istanze di pubblicazione.

* sull’istanza di creazione

   * accesso con privilegi amministrativi
   * accedere alla [console di sicurezza](/help/sites-administering/security.md#accessing-user-administration-with-the-security-console),

      * ad esempio, individuare http://localhost:4502/useradmin
   * nel riquadro a sinistra, selezionare il gruppo (o l&#39;utente) per il quale [read permissions](/help/sites-administering/security.md#permissions) deve essere concesso
   * nel riquadro di destra, individuare il **Path **to Tag Namespace

      * ad esempio, `/content/cq:tags/mycommunity`
   * selezionare il simbolo `checkbox`nella colonna **Leggi**
   * selezionare **Save**



![chlimage_1-204](assets/chlimage_1-204.png)

* verifica che tutte le istanze di pubblicazione abbiano le stesse autorizzazioni

   * un approccio consiste nel [creare un pacchetto](/help/sites-administering/package-manager.md#package-manager) dello spazio dei nomi sull&#39;autore

      * nella scheda `Advanced`, per `AC Handling` selezionare `Overwrite`
   * replicare il pacchetto

      * scegliete `Replicate` da Gestione pacchetti


## Gestione dei tag in diverse lingue {#managing-tags-in-different-languages}

La proprietà `title`di un tag può essere tradotta in più lingue. Una volta tradotto, il tag appropriato `title`può essere visualizzato in base alla lingua dell&#39;utente o alla lingua della pagina.

### Definizione dei titoli dei tag in diverse lingue {#defining-tag-titles-in-multiple-languages}

Di seguito viene descritto come tradurre il `title`del tag **Animals** dall&#39;inglese al tedesco e al francese.

Per iniziare, seleziona il tag sotto lo spazio dei nomi **Stock Photography** e seleziona l&#39;icona **`Edit`**(vedi [Editing Tags](#editing-tags)).

Il pannello Modifica tag consente di scegliere le lingue in cui il titolo del tag deve essere localizzato.

Quando viene selezionata ogni lingua, viene visualizzata una casella di immissione testo in cui è possibile inserire il titolo tradotto.

Una volta immesse tutte le traduzioni, selezionare **Salva** per uscire dalla modalità di modifica.

![chlimage_1-205](assets/chlimage_1-205.png)

In generale, la lingua scelta per il tag viene presa dalla lingua della pagina, se disponibile. Quando si utilizza il widget [`tag` in altre situazioni (ad esempio nei moduli o nelle finestre di dialogo) la lingua del tag dipende dal contesto.](/help/sites-developing/building.md#tagging-on-the-client-side)

Anziché utilizzare l’impostazione della lingua della pagina, nella console Tag viene utilizzata l’impostazione della lingua utente. Nella console Tagging, per il tag &quot;Animals&quot; viene visualizzato &quot;Animaux&quot; per un utente che imposta la lingua in francese nelle relative proprietà utente.

Per aggiungere una nuova lingua alla finestra di dialogo, vedere [Aggiunta di una nuova lingua alla finestra di dialogo Modifica tag](/help/sites-developing/building.md#adding-a-new-language-to-the-edit-tag-dialog).

>[!NOTE]
>
>Il tag cloud e le parole chiave meta nel componente di pagina standard utilizzano il tag localizzato `titles`in base alla lingua della pagina, se disponibile.

## Riferimenti {#resources}

* [Assegnazione di tag agli sviluppatori](/help/sites-developing/tags.md)

   Informazioni sul framework di tag, nonché sull’estensione e l’inclusione di tag nelle applicazioni personalizzate.

* [Console per tag dell’interfaccia classica](/help/sites-administering/classic-console.md)

