---
title: Gestione dei frammenti di contenuto
description: Scopri come utilizzare la console Risorse per gestire i frammenti di contenuto AEM, alla base dei contenuti headless.
feature: Content Fragments
role: User
exl-id: 25c91a85-06ff-4666-a809-46778a689e25
source-git-commit: 20d46a7c37663dac36e6af9582d569a7f782eab7
workflow-type: tm+mt
source-wordcount: '1727'
ht-degree: 9%

---

# Gestione dei frammenti di contenuto {#managing-content-fragments}

Scopri come utilizzare la console Risorse per gestire i frammenti di contenuto AEM, alla base dei contenuti headless.

Dopo aver definito le [Modelli per frammenti di contenuto](#creating-a-content-model) è possibile utilizzare questi [creare i frammenti di contenuto](#creating-a-content-fragment).

La [Editor frammento di contenuto](#opening-the-fragment-editor) fornisce vari [modalità](#modes-in-the-content-fragment-editor) per abilitare:

* [Modificare il contenuto](#editing-the-content-of-your-fragment) e [gestione varianti](#creating-and-managing-variations-within-your-fragment)
* [Annotare il frammento](/help/assets/content-fragments/content-fragments-variations.md#annotating-a-content-fragment)
* [Associa contenuto al frammento](#associating-content-with-your-fragment)
* [Configurare i metadati](#viewing-and-editing-the-metadata-properties-of-your-fragment)
* [Visualizza albero struttura](/help/assets/content-fragments/content-fragments-structure-tree.md)
* [Anteprima della rappresentazione JSON](/help/assets/content-fragments/content-fragments-json-preview.md)


>[!NOTE]
>
>I frammenti di contenuto possono essere utilizzati:
>
>* quando si creano pagine; vedere [Authoring delle pagine con frammenti di contenuto](/help/sites-authoring/content-fragments.md).
>* per [Distribuzione di contenuti headless tramite frammenti di contenuto con GraphQL](/help/assets/content-fragments/content-fragments-graphql.md).


>[!NOTE]
>
>I frammenti di contenuto sono memorizzati come **Risorse**, così come vengono gestiti principalmente dal **Risorse** console.

## Creazione di frammenti di contenuto {#creating-content-fragments}

### Creazione di un modello di contenuto {#creating-a-content-model}

[Modelli per frammenti di contenuto](/help/assets/content-fragments/content-fragments-models.md) possono essere abilitate e create prima di creare frammenti di contenuto con contenuto strutturato.

### Creazione di un frammento di contenuto {#creating-a-content-fragment}

Il metodo di creazione di un frammento di contenuto è:

1. Passa alla cartella **Risorse** in cui desideri creare il frammento.
1. Per aprire la procedura guidata, seleziona **Crea**, quindi **Frammento di contenuto**.
1. Il primo passaggio della procedura guidata richiede di specificare la base del nuovo frammento.

   * [Modello](/help/assets/content-fragments/content-fragments-models.md) - utilizzato per creare un frammento che richiede contenuto strutturato; ad esempio **Avventura** model

      * Vengono visualizzati tutti i modelli disponibili.

   Dopo la selezione, utilizza **Successivo** per procedere.

   ![base del frammento](assets/cfm-managing-01.png)

1. Nel passaggio **Proprietà** specifica:

   * **Base**

      * **Titolo**

         Titolo del frammento.

         Obbligatorio.

      * **Descrizione**

      * **Tag**
   * **Avanzate**

      * **Nome**

         il nome; verrà utilizzato per formare l’URL.

         Obbligatorio; viene derivato automaticamente dal titolo, ma può essere aggiornato.


1. Seleziona **Crea** per completare l’azione, quindi **Apri** il frammento per la modifica oppure tornare alla console facendo clic su **Fine**.

   >[!NOTE]
   >In **Elenco** della console è possibile aggiornare la **Visualizza impostazioni** per abilitare **Modello per frammento di contenuto** colonna.

## Azioni per un frammento di contenuto nella console Risorse {#actions-for-a-content-fragment-assets-console}

In **Risorse** per i frammenti di contenuto sono disponibili diverse azioni:

* Dalla barra degli strumenti; dopo aver selezionato il frammento sono disponibili tutte le azioni appropriate.
* Come [azioni rapide](/help/sites-authoring/basic-handling.md#quick-actions); un sottoinsieme di azioni disponibili per le singole schede di frammento.

![azioni](assets/cfm-managing-02.png)

Seleziona il frammento per visualizzare la barra degli strumenti con le azioni applicabili:

* **Scarica**

   * Salvare il frammento come file ZIP; puoi definire se includere elementi, varianti, metadati.

* **Crea**
* **Pagamento**
* **Proprietà**

   * Consente di visualizzare e/o modificare i metadati del frammento.

* **Modifica**

   * Permette di [aprire il frammento per la modifica del contenuto](/help/assets/content-fragments/content-fragments-variations.md) insieme ai relativi elementi, varianti, contenuti associati e metadati.

* **Gestisci i tag**
* **Alla raccolta**
* **Copia** e **Incolla**)
* **Sposta**
* **Pubblicazione rapida**
* **Gestisci pubblicazione**
* **Elimina**

>[!NOTE]
>
>Molti di questi sono [azioni standard per Assets](/help/assets/manage-assets.md) e/o [app desktop AEM](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html?lang=it).

## Apertura dell’Editor frammento {#opening-the-fragment-editor}

Per aprire il frammento per la modifica:

>[!CAUTION]
>
>Per modificare un frammento di contenuto è necessario [le autorizzazioni appropriate](/help/sites-developing/customizing-content-fragments.md#asset-permissions). In caso di problemi, contatta l’amministratore di sistema.

>[!CAUTION]
>
>Per modificare un frammento di contenuto è necessario disporre delle autorizzazioni appropriate. In caso di problemi, contatta l’amministratore di sistema.

1. Utilizza la **Risorse** per passare alla posizione del frammento di contenuto.
1. Apri il frammento per la modifica:

   * Tocca o fai clic sul collegamento frammento o frammento (a seconda della vista della console).
   * Selezione del frammento, quindi **Modifica** dalla barra degli strumenti.

1. Viene aperto l’editor frammenti. Apporta le modifiche necessarie:

   ![editor frammenti](assets/cfm-managing-03.png)

1. Dopo aver apportato le modifiche, utilizza **Salva**, **Salva e chiudi** o **Chiudi** se necessario.

   >[!NOTE]
   >
   >**Salva e chiudi** è disponibile tramite **Salva** a discesa.

   >[!NOTE]
   >
   >Entrambi **Salva e chiudi** e **Chiudi** uscirà dall’editor; vedi [Salva, chiudi e versioni](#save-close-and-versions) per informazioni complete sul funzionamento delle varie opzioni per i frammenti di contenuto.

## Modalità e azioni nell’Editor frammento di contenuto {#modes-actions-content-fragment-editor}

Sono disponibili varie modalità e azioni dall’Editor frammento di contenuto.

### Modalità nell’Editor frammento di contenuto {#modes-in-the-content-fragment-editor}

Naviga tra le varie modalità utilizzando le icone nel pannello laterale:

* Variazioni: [Modifica del contenuto](#editing-the-content-of-your-fragment) e [Gestione delle varianti](#creating-and-managing-variations-within-your-fragment)

* [Annotazioni](/help/assets/content-fragments/content-fragments-variations.md#annotating-a-content-fragment)
* [Contenuto associato](#associating-content-with-your-fragment)
* [Metadati](#viewing-and-editing-the-metadata-properties-of-your-fragment)
* [Albero struttura](/help/assets/content-fragments/content-fragments-structure-tree.md)
* [Anteprima](/help/assets/content-fragments/content-fragments-json-preview.md)

![modalità](assets/cfm-managing-04.png)

### Azioni barra degli strumenti nell’Editor frammento di contenuto {#toolbar-actions-in-the-content-fragment-editor}

Alcune funzioni nella barra degli strumenti superiore sono disponibili in diverse modalità:

![modalità](assets/cfm-managing-top-toolbar.png)

* Se in una pagina di contenuto è già presente un riferimento al frammento, viene visualizzato un messaggio. È possibile **Chiudi** il messaggio.

* Il pannello laterale può essere nascosto o visualizzato utilizzando **Attiva/Disattiva pannello laterale** icona.

* Sotto il nome del frammento è possibile visualizzare il nome dell’ [Modello per frammento di contenuto](/help/assets/content-fragments/content-fragments-models.md) utilizzato per creare il frammento corrente:

   * Il nome è anche un collegamento che aprirà l&#39;editor modelli.

* Vedere lo stato del frammento; ad esempio, informazioni su quando è stato creato, modificato o pubblicato.

* **Salva** fornisce accesso al **Salva e chiudi** opzione .

* I tre punti (**...**) fornisce accesso alle azioni aggiuntive:
   * **Aggiorna i riferimenti pagina**
      * Questo aggiorna tutti i riferimenti di pagina.
   * **[Pubblicazione rapida](#publishing-and-referencing-a-fragment)**
   * **[Gestisci pubblicazione](#publishing-and-referencing-a-fragment)**

<!--
* See the status of the fragment; for example, information about when it was created, modified or published. The status is also color-coded:

  * **New**: grey
  * **Draft**: blue
  * **Published**: green
  * **Modified**: orange
  * **Deactivated**: red
-->

<!--
This updates any page references and ensures that the Dispatcher is flushed as required. 
-->

## Salva, chiudi e versioni {#save-close-and-versions}

>[!NOTE]
>
>Le versioni possono anche essere [creati, confrontati e ripristinati dalla timeline](/help/assets/content-fragments/content-fragments-managing.md#timeline-for-content-fragments).

L’editor dispone di diverse opzioni:

* **Salva** e **Salva e chiudi**

   * **Salva** salverà le modifiche più recenti e rimarrà nell’editor.
   * **Salva e chiudi** salverà le modifiche più recenti e chiuderà l’editor.

   >[!CAUTION]
   >
   >Per modificare un frammento di contenuto è necessario [le autorizzazioni appropriate](/help/sites-developing/customizing-content-fragments.md#asset-permissions). In caso di problemi, contatta l’amministratore di sistema.

   >[!NOTE]
   >
   >È possibile rimanere nell&#39;editor, apportando una serie di modifiche, prima di salvare.

   >[!CAUTION]
   >
   >Oltre a salvare semplicemente le modifiche, le azioni aggiornano anche i riferimenti e garantiscono che Dispatcher venga scaricato come necessario. L’elaborazione di queste modifiche può richiedere del tempo. Per questo motivo, può esserci un impatto sulle prestazioni su un sistema di grandi dimensioni/complesso/pesantemente caricato.
   >
   >Tieni presente questo aspetto quando utilizzi **Salva e chiudi** quindi è possibile reimmettere rapidamente l’editor frammenti per apportare e salvare ulteriori modifiche.

* **Chiudi**

   Uscirà dall’editor senza salvare le modifiche più recenti (ovvero apportate dall’ultimo **Salva**).

Durante la modifica del frammento di contenuto AEM crea automaticamente delle versioni per garantire che il contenuto precedente possa essere ripristinato se si annullano le modifiche (utilizzando **Chiudi** senza risparmio):

1. Quando un frammento di contenuto viene aperto per la modifica AEM verifica l’esistenza del token basato su cookie che indica se un *sessione di modifica* esiste:

   1. Se viene trovato il token, il frammento viene considerato parte della sessione di modifica esistente.
   2. Se il token è *not* disponibile e l’utente inizia a modificare il contenuto, viene creata una versione e viene inviato un token per questa nuova sessione di modifica al client, dove viene salvato in un cookie.

2. Mentre c&#39;è un *attivo* il contenuto in fase di modifica viene salvato automaticamente ogni 600 secondi (impostazione predefinita).

   >[!NOTE]
   >
   >L&#39;intervallo di salvataggio automatico è configurabile utilizzando `/conf` meccanismo.
   >
   >Valore predefinito, vedi:
   >  `/libs/settings/dam/cfm/jcr:content/autoSaveInterval`

3. Se l’utente annulla la modifica, la versione creata all’inizio della sessione di modifica viene ripristinata e il token viene rimosso per terminare la sessione di modifica.
4. Se l’utente seleziona **Salva** le modifiche, gli elementi/varianti aggiornati vengono mantenuti e il token viene rimosso per terminare la sessione di modifica.

## Modifica del contenuto del frammento {#editing-the-content-of-your-fragment}

Dopo aver aperto il frammento, è possibile utilizzare [Variazioni](/help/assets/content-fragments/content-fragments-variations.md) per creare i contenuti.

## Creazione e gestione di varianti all’interno del frammento {#creating-and-managing-variations-within-your-fragment}

Dopo aver creato il contenuto principale, puoi creare e gestire: [Variazioni](/help/assets/content-fragments/content-fragments-variations.md) di quel contenuto.

## Associazione di contenuto al frammento {#associating-content-with-your-fragment}

È inoltre possibile [associare il contenuto](/help/assets/content-fragments/content-fragments-assoc-content.md) con un frammento. Questa funzione consente di collegare in modo che le risorse (ad esempio le immagini) possano essere (facoltativamente) utilizzate con il frammento quando viene aggiunto a una pagina di contenuto.

## Visualizzazione e modifica dei metadati (proprietà) del frammento {#viewing-and-editing-the-metadata-properties-of-your-fragment}

È possibile visualizzare e modificare le proprietà di un frammento utilizzando [Metadati](/help/assets/content-fragments/content-fragments-metadata.md) scheda .

## Timeline per i frammenti di contenuto {#timeline-for-content-fragments}

Oltre alle opzioni standard, [Timeline](/help/assets/manage-assets.md#timeline) fornisce sia informazioni che azioni specifiche per i frammenti di contenuto:

* Visualizza informazioni su versioni, commenti e annotazioni
* Azioni per le versioni

   * **[Ripristina questa versione](#reverting-to-a-version)** (selezionare un frammento esistente, quindi una versione specifica)

   * **[Confronta con corrente](#comparing-fragment-versions)** (selezionare un frammento esistente, quindi una versione specifica)

   * Aggiungi un **Etichetta** e/o **Commento** (selezionare un frammento esistente, quindi una versione specifica)

   * **Salva come versione** (selezionare un frammento esistente, quindi la freccia su nella parte inferiore della timeline)

* Azioni per le annotazioni

   * **Elimina**

>[!NOTE]
I commenti sono:
* Funzionalità standard per tutte le risorse
* Made in Timeline
* Correlato alla risorsa frammento

Le annotazioni (per i frammenti di contenuto) sono:
* Inserito nell’editor frammenti
* Specifica per un segmento di testo selezionato all’interno del frammento


Esempio:

![timeline](assets/cfm-managing-05.png)

## Confronto delle versioni dei frammenti {#comparing-fragment-versions}

La **Confronta con corrente** è disponibile nella sezione [Timeline](/help/assets/content-fragments/content-fragments-managing.md#timeline-for-content-fragments) dopo aver selezionato una versione specifica.

Verrà aperto:

* la **Corrente** (ultima versione) (a sinistra)

* la versione selezionata **v&lt;*x.y*>** (a destra)

Vengono visualizzati affiancati, dove:

* Eventuali differenze sono evidenziate

   * Testo eliminato - rosso
   * Testo inserito - verde
   * Testo sostituito - blu

* L’icona a schermo intero consente di aprire una delle due versioni da sola; quindi torna alla vista parallela
* È possibile **Ripristina** alla versione specifica
* **Fine** tornerai alla console

>[!NOTE]
Non è possibile modificare il contenuto del frammento quando si confrontano i frammenti.

![confronto](assets/cfm-managing-06.png)

## Ripristino di una versione  {#reverting-to-a-version}

È possibile ripristinare una versione specifica del frammento:

* Direttamente dal [Timeline](/help/assets/content-fragments/content-fragments-managing.md#timeline-for-content-fragments).

   Seleziona la versione richiesta, quindi la **Ripristina questa versione** azione.

* Quando [confronto di una versione con la versione corrente](/help/assets/content-fragments/content-fragments-managing.md#comparing-fragment-versions) è possibile **Ripristina** alla versione selezionata.

## Pubblicazione e riferimento a un frammento {#publishing-and-referencing-a-fragment}

>[!CAUTION]
Se il frammento è basato su un modello, assicurati che la [modello pubblicato](/help/assets/content-fragments/content-fragments-models.md#publishing-a-content-fragment-model).
Se pubblichi un frammento di contenuto per il quale il modello non è ancora stato pubblicato, un elenco di selezione lo indicherà e il modello verrà pubblicato con il frammento.

I frammenti di contenuto devono essere pubblicati per l’utilizzo nell’ambiente di pubblicazione. Possono essere pubblicati:

* Dopo la creazione; utilizzo [azioni disponibili nella console Risorse](#actions-for-a-content-fragment-assets-console).
* Da [Editor frammento di contenuto](#toolbar-actions-in-the-content-fragment-editor).
* Quando [pubblicare una pagina che utilizza il frammento](/help/sites-authoring/content-fragments.md#publishing); il frammento viene elencato nei riferimenti di pagina.

>[!CAUTION]
Dopo la pubblicazione e/o il riferimento a un frammento, AEM un avviso quando un autore riapre il frammento per la modifica. In questo modo si avverte che le modifiche al frammento avranno effetto anche sulle pagine a cui si fa riferimento.

## Eliminazione di un frammento {#deleting-a-fragment}

Per eliminare un frammento:

1. In **Risorse** passa alla posizione del frammento di contenuto.
2. Selezionare il frammento.

   >[!NOTE]
   La **Elimina** azione non disponibile come azione rapida.

3. Seleziona **Elimina** dalla barra degli strumenti.
4. Conferma la **Elimina** azione.

   >[!CAUTION]
   Se in una pagina è già presente un riferimento al frammento, verrà visualizzato un messaggio di avviso e sarà necessario confermare che si desidera procedere con **Forza eliminazione**. Il frammento, insieme al relativo componente di frammento di contenuto, verrà eliminato da tutte le pagine di contenuto.
