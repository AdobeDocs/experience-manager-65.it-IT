---
title: Amministrazione dei tag
seo-title: Administering Tags
description: Scopri come amministrare i tag in AEM.
seo-description: Learn how to administer Tags in AEM.
uuid: 77e1280a-feea-4edd-94b6-4fb825566c42
contentOwner: Chiradeep Majumdar
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: content
content-type: reference
discoiquuid: 69253ee9-8c28-436b-9331-6fb875f64cba
exl-id: ff041ef0-e566-4373-818e-76680ff668d8
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1760'
ht-degree: 7%

---

# Amministrazione dei tag {#administering-tags}

I tag sono un metodo semplice e veloce per classificare i contenuti di un sito web. Possono essere considerate come parole chiave o etichette (metadati) che consentono di trovare più rapidamente il contenuto a seguito di una ricerca.

In Adobe Experience Manager (AEM), un tag può essere una proprietà di

* un nodo di contenuto per una pagina (vedi [Utilizzo dei tag](/help/sites-authoring/tags.md))

* un nodo di metadati per una risorsa (consulta [Gestione dei metadati per le risorse digitali](/help/assets/metadata.md))

Oltre alle pagine e alle risorse, i tag vengono utilizzati per le funzioni di AEM Communities

* contenuto generato dall’utente (consulta [Assegnazione tag UGC)](/help/communities/tag-ugc.md)

* Risorse di abilitazione (consulta [Risorse di abilitazione assegnazione tag](/help/communities/functions.md#catalog-function))

## Funzioni tag {#tag-features}

Alcune delle funzioni dei tag in AEM includono:

* I tag possono essere raggruppati in vari namespace. Tali gerarchie consentono di creare tassonomie Queste tassonomie sono globali in tutta AEM.
* La restrizione principale per i tag appena creati è che devono essere univoci all’interno di uno specifico spazio dei nomi.
* Il titolo di un tag non deve includere caratteri di separazione del percorso del tag (né saranno visualizzati se presenti)

   * colon `:` - delimita il tag namespace
   * barra `/` - delimita i tag secondari

* I tag possono essere applicati da autori e visitatori del sito. A prescindere dalla modalità di creazione, tutti i tipi di tag possono essere selezionati sia per essere assegnati a una pagina, sia per operazioni di ricerca.
* I tag possono essere creati e la loro tassonomia può essere modificata dai membri del gruppo &quot;tag-administrators&quot; e dai membri che dispongono dei diritti di modifica per `/content/cq:tags`.

   * Un tag contenente tag secondari è denominato tag contenitore
   * Un tag che non è un tag contenitore è denominato tag foglia
   * Un tag namespace è un tag foglia o contenitore

* I tag vengono utilizzati dal [Componente di ricerca](https://helpx.adobe.com/experience-manager/core-components/using/quick-search.html) per facilitare la ricerca del contenuto.
* I tag vengono utilizzati dal [Componente teaser](https://helpx.adobe.com/experience-manager/core-components/using/teaser.html), che controlla il tag cloud di un utente per fornire contenuti mirati.
* Assegnazione di tag a un aspetto importante del contenuto

   * assicurati di creare pacchetti di tag con le pagine che li utilizzano
   * assicurati [autorizzazioni tag](#setting-tag-permissions) abilita accesso in lettura

## Console assegnazione tag {#tagging-console}

La console Assegnazione tag consente di creare e gestire i tag e le relative tassonomie. Un obiettivo è quello di evitare di avere molti tag simili che si riferiscono sostanzialmente alla stessa cosa : ad esempio, pagina e pagine o calzature e scarpe.

I tag vengono gestiti raggruppandoli in spazi dei nomi, esaminando l’utilizzo dei tag esistenti prima di crearne di nuovi e riorganizzandoli senza scollegare il tag dal contenuto attualmente a cui si fa riferimento.

Per accedere alla console Tagging :

* sull&#39;autore
* accesso con privilegi amministrativi
* dalla navigazione globale

   * select **`Tools`**
   * select **`General`**
   * select **`Tagging`**

![managing_tags_usingthetagasministrationconsole](assets/managing_tags_usingthetagasministrationconsolea.png)

### Creazione di un namespace {#creating-a-namespace}

Per creare un nuovo spazio dei nomi, seleziona la **`Create Namespace`** icona.

Lo spazio dei nomi è di per sé un tag e non deve contenere tag secondari. Tuttavia, per continuare a creare una tassonomia, [creare tag secondari](#creating-tags), che a sua volta possono essere tag foglia o contenitore .

![chlimage_1-183](assets/chlimage_1-183a.png) ![creazione_tags_andnamespaces](assets/creating_tags_andnamespacesa.png)

* **Titolo**

   *(obbligatorio)* Titolo da visualizzare per lo spazio dei nomi.

* **Nome**
   *(facoltativo)* Nome dello spazio dei nomi. Se non viene specificato, dal Titolo viene creato un nome di nodo valido. Vedi [TagID](/help/sites-developing/framework.md#tagid).

* **Descrizione**

   *(facoltativo)* Una descrizione dello spazio dei nomi.

Una volta inserite le informazioni richieste

* select **Crea**

### Operazioni sui tag {#operations-on-tags}

Quando si seleziona uno spazio dei nomi o un altro tag, sono disponibili le seguenti operazioni:

* [Visualizza proprietà](#viewing-tag-properties)
* [Riferimenti](#showing-tag-references)
* [Crea tag](#creating-tags)
* [Modifica](#editing-tags)
* [Spostare](#moving-tags)
* [Unisci](#merging-tags)
* [Pubblicazione](#publishing-tags)
* [Annulla pubblicazione](#unpublishing-tags)
* [Elimina](#deleting-tags)

![chlimage_1-184](assets/chlimage_1-184.png)

Quando la finestra del browser non è sufficientemente ampia da visualizzare tutte le icone, le icone più a destra sono raggruppate sotto una **`... More`** icona , che visualizza un elenco a discesa delle icone delle operazioni nascoste quando selezionate.

![chlimage_1-185](assets/chlimage_1-185.png)

### Selezione di un tag dello spazio dei nomi {#selecting-a-namespace-tag}

Quando è selezionata per la prima volta, se lo spazio dei nomi non contiene tag, le proprietà vengono visualizzate a destra, altrimenti vengono visualizzati i tag secondari. Ogni tag selezionato visualizzerà i tag in esso contenuti o le relative proprietà, se non dispone di tag secondari.

Per selezionare il tag per le operazioni e per effettuare una selezione multipla, seleziona solo l’icona accanto al titolo. Quando si seleziona il titolo, vengono visualizzate solo le proprietà o il tag viene aperto per visualizzarne il contenuto.

![chlimage_1-186](assets/chlimage_1-186.png) ![chlimage_1-187](assets/chlimage_1-187.png)

### Visualizzazione delle proprietà dei tag {#viewing-tag-properties}

![chlimage_1-188](assets/chlimage_1-188.png)

Quando selezioni uno spazio dei nomi o un altro tag, seleziona **`View Properties`** l&#39;icona restituisce la visualizzazione delle informazioni relative al `name`, ora dell’ultima modifica e numero di riferimenti. Se pubblicata, viene visualizzata l’ora dell’ultima pubblicazione e l’ID dell’editore. Queste informazioni vengono visualizzate in una colonna a sinistra delle colonne del tag.

![chlimage_1-189](assets/chlimage_1-189.png)

### Visualizzazione dei riferimenti ai tag {#showing-tag-references}

![chlimage_1-190](assets/chlimage_1-190.png)

Quando selezioni uno spazio dei nomi o un altro tag, seleziona **Riferimenti** identifica il contenuto a cui è stato applicato il tag.

La visualizzazione iniziale è un conteggio dei tag applicati.

![chlimage_1-191](assets/chlimage_1-191.png)

Selezionando la freccia a destra del conteggio, vengono elencati i nomi di riferimento.

Il percorso del riferimento viene visualizzato come una descrizione comandi quando si passa il mouse su un riferimento.

![chlimage_1-192](assets/chlimage_1-192.png)

### Creazione di tag {#creating-tags}

![chlimage_1-193](assets/chlimage_1-193.png)

Quando selezioni uno spazio dei nomi o un altro tag (selezionando l’icona accanto al titolo), puoi creare un tag secondario per il tag corrente selezionando la **`Create Tag`** icona.

![chlimage_1-194](assets/chlimage_1-194.png)

* **Titolo**
*(obbligatorio) *Un titolo di visualizzazione per il tag.

* **Nome**
*(facoltativo) *Un nome per il tag. Se non viene specificato, dal Titolo viene creato un nome di nodo valido. Vedi [TagID](/help/sites-developing/framework.md#tagid).

* **Descrizione**
*(facoltativo) *Una descrizione del tag.

Una volta inserite le informazioni richieste

* select **Crea**

### Modifica dei tag {#editing-tags}

![chlimage_1-195](assets/chlimage_1-195.png)

Quando è selezionato uno spazio dei nomi o un altro tag, è possibile modificare il Titolo, la Descrizione e fornire le localizzazioni del Titolo selezionando il valore **`Edit`**icona.

Dopo aver apportato le modifiche, seleziona **Salva**.

Per informazioni dettagliate sull’aggiunta di traduzioni in lingua, consulta la sezione su [Gestione dei tag in diverse lingue](#managing-tags-in-different-languages).

![chlimage_1-196](assets/chlimage_1-196.png)

### Spostamento dei tag {#moving-tags}

![chlimage_1-197](assets/chlimage_1-197.png)

Quando selezioni uno spazio dei nomi o un altro tag, seleziona **`Move`** Gli amministratori di tag e gli sviluppatori possono pulire la tassonomia spostando il tag in una nuova posizione o rinominandolo. Quando il tag selezionato è un tag contenitore, lo spostamento del tag comporta anche lo spostamento di tutti i tag secondari.

>[!NOTE]
>
>È consigliabile che gli autori siano autorizzati solo a [modifica](#editing-tags) del tag `title`, per non spostare o rinominare i tag.

![chlimage_1-198](assets/chlimage_1-198.png)

* **Percorso**

   *(sola lettura)* Percorso corrente del tag selezionato.

* **Sposta a**
Individua il nuovo percorso in cui spostare il tag.

* **Rinomina in**
Visualizza inizialmente il valore corrente 
`name`del tag . Nuovo `name`possono essere inseriti.

* select **Salva**

### Unione dei tag {#merging-tags}

![chlimage_1-199](assets/chlimage_1-199.png)

Se una tassonomia include duplicati, è possibile unire i tag. Quando il tag A viene unito al tag B, tutte le pagine contrassegnate con il tag A vengono contrassegnate con il tag B e il tag A non è più disponibile per gli autori.

Quando selezioni uno spazio dei nomi o un altro tag, seleziona **Unisci** apre un pannello in cui è possibile selezionare il percorso in cui unire.

![chlimage_1-200](assets/chlimage_1-200.png)

* **Percorso**

   *(sola lettura)* Percorso del tag selezionato da unire in un altro tag.

* **Unisci in**
Sfoglia per selezionare il percorso del tag in cui eseguire l&#39;unione.

>[!NOTE]
>
>Dopo l&#39;unione, la **Percorso** l&#39;opzione selezionata originariamente (virtualmente) non esiste più.
>
>Quando un tag di riferimento viene spostato o unito, il tag non viene fisicamente eliminato in modo da poter mantenere i riferimenti.

### Pubblicazione dei tag {#publishing-tags}

![chlimage_1-201](assets/chlimage_1-201.png)

Quando selezioni uno spazio dei nomi o un altro tag, seleziona **Pubblica** per attivare il tag nell’ambiente di pubblicazione. Simile al contenuto della pagina, viene pubblicato solo il tag selezionato, indipendentemente dal fatto che si tratti di un tag contenitore o meno.

Per pubblicare una tassonomia (uno spazio dei nomi e dei tag secondari), si consiglia di creare una [pacchetto](/help/sites-administering/package-manager.md) dello spazio dei nomi (vedi [Nodo principale tassonomia](/help/sites-developing/framework.md#taxonomy-root-node)). Assicurati di [applica autorizzazioni](#setting-tag-permissions) allo spazio dei nomi prima di creare il pacchetto.

### Annullamento della pubblicazione dei tag {#unpublishing-tags}

![chlimage_1-202](assets/chlimage_1-202.png)

Quando selezioni uno spazio dei nomi o un altro tag, seleziona **Annulla pubblicazione** Il tag viene disattivato nell’ambiente di authoring e rimosso dall’ambiente di pubblicazione. Simile al `Delete`se il tag selezionato è un tag contenitore, tutti i relativi tag figlio verranno disattivati nell’ambiente di authoring e rimossi dall’ambiente di pubblicazione.

### Eliminazione dei tag {#deleting-tags}

![chlimage_1-203](assets/chlimage_1-203.png)

Quando selezioni uno spazio dei nomi o un altro tag, seleziona **Elimina** l’icona rimuoverà definitivamente il tag dall’ambiente di authoring. Se il tag è stato pubblicato, viene rimosso anche dall’ambiente di pubblicazione. Se il tag selezionato è un tag contenitore, verranno rimossi anche tutti i tag secondari corrispondenti.

## Impostazione delle autorizzazioni dei tag {#setting-tag-permissions}

Le autorizzazioni dei tag sono [&#39;secure (by default)&#39;](/help/sites-administering/production-ready.md); una best practice per l’ambiente di pubblicazione che richiede l’autorizzazione di lettura per consentire esplicitamente i tag. Basciamente, questo viene fatto creando un pacchetto dello spazio dei nomi dei tag dopo che le autorizzazioni sono state impostate sull&#39;autore e installando il pacchetto su tutte le istanze di pubblicazione.

* sull’istanza dell’autore

   * accesso con privilegi amministrativi
   * accedere al [Console di sicurezza](/help/sites-administering/security.md#accessing-user-administration-with-the-security-console),

      * ad esempio, cerca http://localhost:4502/useradmin
   * nel riquadro a sinistra, seleziona il gruppo (o l’utente) per il quale [autorizzazione lettura](/help/sites-administering/security.md#permissions) è concesso
   * nel riquadro a destra, individua il **Path **to the Tag Namespace

      * ad esempio, `/content/cq:tags/mycommunity`
   * seleziona la `checkbox`in **Leggi** column
   * select **Salva**



![chlimage_1-204](assets/chlimage_1-204.png)

* assicurati che tutte le istanze di pubblicazione abbiano le stesse autorizzazioni

   * un approccio è [creare un pacchetto](/help/sites-administering/package-manager.md#package-manager) dello spazio dei nomi sull’autore

      * su `Advanced` scheda `AC Handling` select `Overwrite`
   * replicare il pacchetto

      * scegli `Replicate` da package manager


## Gestione dei tag in diverse lingue {#managing-tags-in-different-languages}

La `title`La proprietà di un tag può essere tradotta in più lingue. Una volta tradotto, il tag appropriato `title`possono essere visualizzati in base alla lingua dell’utente o alla lingua della pagina.

### Definizione dei titoli dei tag in diverse lingue {#defining-tag-titles-in-multiple-languages}

Di seguito viene descritto come tradurre il `title`del tag **Animali** dall&#39;inglese al tedesco e al francese.

Inizia selezionando il tag sotto il tag **Fotografia Stock** namespace e selezione del **`Edit`**icona (vedi [Modifica dei tag](#editing-tags) sezione).

Il pannello Modifica tag consente di scegliere le lingue in cui il titolo del tag deve essere localizzato.

Quando si seleziona ogni lingua, viene visualizzata una casella di immissione testo in cui è possibile inserire il titolo tradotto.

Una volta inserite tutte le traduzioni, seleziona **Salva** per uscire dalla modalità di modifica.

![chlimage_1-205](assets/chlimage_1-205.png)

In generale, la lingua scelta per il tag viene presa dalla lingua della pagina, se disponibile. Quando si utilizza il widget [`tag` in altre situazioni (ad esempio nei moduli o nelle finestre di dialogo) la lingua del tag dipende dal contesto.](/help/sites-developing/building.md#tagging-on-the-client-side)

Invece di usare l’impostazione per la lingua della pagina, nella console Assegnazione tag vengono utilizzate le impostazioni per la lingua utente. Nella console Tagging, per il tag &quot;Animals&quot; viene visualizzato &quot;Animaux&quot; per un utente che imposta la lingua in francese nelle relative proprietà utente.

Per aggiungere una nuova lingua alla finestra di dialogo, vedi [Aggiunta di una nuova lingua alla finestra di dialogo Modifica tag](/help/sites-developing/building.md#adding-a-new-language-to-the-edit-tag-dialog).

>[!NOTE]
>
>Il tag cloud e le parole chiave meta nel componente pagina standard utilizzano il tag localizzato `titles`in base alla lingua della pagina, se disponibile.

## Riferimenti {#resources}

* [Assegnazione tag per sviluppatori](/help/sites-developing/tags.md)

   Informazioni sul framework dei tag, nonché sull’estensione e l’inclusione di tag nelle applicazioni personalizzate.

* [Console per assegnazione tag dell’interfaccia classica](/help/sites-administering/classic-console.md)
