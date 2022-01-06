---
title: Scopri come creare modelli di frammenti di contenuto in AEM
description: Scopri i concetti e la meccanica della modellazione dei contenuti per i CMS headless utilizzando Modelli per frammenti di contenuto.
source-git-commit: 38525b6cc14e9f6025564c060b8cfb4f9e0ea473
workflow-type: tm+mt
source-wordcount: '690'
ht-degree: 2%

---

# Scopri come creare modelli di frammenti di contenuto in AEM {#architect-headless-content-fragment-models}

## La storia finora {#story-so-far}

All&#39;inizio del [AEM Percorso di authoring dei contenuti headless](overview.md) la [Nozioni di base sulla modellazione dei contenuti per headless con AEM](basics.md) ha trattato i concetti e la terminologia di base relativi all&#39;authoring per headless.

Questo articolo si basa su questi elementi per comprendere come creare modelli di frammenti di contenuto personalizzati per il progetto AEM headless.

## Obiettivo {#objective}

* **Pubblico**: Principiante
* **Obiettivo**: i concetti e la meccanica di modellazione dei contenuti per i CMS headless utilizzando Modelli per frammenti di contenuto.

<!-- which persona does this? -->
<!-- and who allows the configuration on the folders? -->

<!--
## Enabling Content Fragment Models {#enabling-content-fragment-models}

At the very start you need to enable Content Fragment Models for your site, this is done in the Configuration Browser; under Tools -> General -> Configuration Browser. You can either select to configure the global entry, or create a new configuration. For example:

![Define configuration](/help/assets/content-fragments/assets/cfm-conf-01.png)

>[!NOTE]
>
>See Additional Resources - Content Fragments in the Configuration Browser
-->

## Creazione di modelli di frammenti di contenuto {#creating-content-fragment-models}

È quindi possibile creare modelli di frammenti di contenuto e definire la struttura. Questa operazione può essere eseguita in Strumenti -> Risorse -> Modelli per frammenti di contenuto.

![Modelli per frammenti di contenuto negli strumenti](assets/cfm-tools.png)

Dopo aver selezionato questa opzione, si passa alla posizione del modello e si seleziona **Crea**. Qui puoi inserire vari dettagli chiave.

Opzione **Abilita modello** è attivato per impostazione predefinita. Ciò significa che il modello sarà disponibile per l’uso (nella creazione di frammenti di contenuto) non appena lo avrai salvato. Se lo desideri, puoi disattivarlo; in seguito potrai abilitare (o disabilitare) un modello esistente.

![Crea modello di frammento di contenuto](/help/assets/content-fragments/assets/cfm-models-02.png)

Conferma con **Crea** e potete **Apri** il modello per iniziare a definire la struttura.

## Definizione dei modelli di frammenti di contenuto {#defining-content-fragment-models}

La prima volta che apri un nuovo modello viene visualizzato un grande spazio vuoto a sinistra e un lungo elenco di **Tipi di dati** a destra:

![Modello vuoto](/help/assets/content-fragments/assets/cfm-models-03.png)

Quindi - cosa fare?

Puoi trascinare le istanze della **Tipi di dati** nello spazio a sinistra - state già definendo il vostro modello!

![Definizione dei campi](/help/assets/content-fragments/assets/cfm-models-04.png)

Dopo aver aggiunto un tipo di dati, dovrai definire le **Proprietà** per quel campo. Dipendono dal tipo utilizzato. Esempio:

![Proprietà dati](/help/assets/content-fragments/assets/cfm-models-05.png)

È possibile aggiungere tutti i campi necessari. Esempio:

![Modello per frammenti di contenuto](/help/assets/content-fragments/assets/cfm-models-07.png)

### Autori dei contenuti {#your-content-authors}

Gli autori dei contenuti non visualizzano i tipi di dati e le proprietà effettivamente utilizzati per creare i modelli. Ciò significa che potrebbe essere necessario fornire aiuto e informazioni su come completare campi specifici. Per informazioni di base è possibile utilizzare Etichetta campo e Valore predefinito, ma in casi più complessi potrebbe essere necessario prendere in considerazione la documentazione specifica del progetto.

>[!NOTE]
>
>Consulta Risorse aggiuntive - Modelli per frammenti di contenuto.

## Gestione dei modelli di frammenti di contenuto {#managing-content-fragment-models}

<!-- needs more details -->

La gestione dei modelli di frammenti di contenuto comporta:

* Abilitarli (o disattivarli), per renderli disponibili agli autori al momento della creazione dei frammenti di contenuto.
* Eliminazione: è sempre necessario eliminare, ma è necessario tenere presente che si elimina un modello già utilizzato per i frammenti di contenuto, in particolare i frammenti già pubblicati.

## Pubblicazione {#publishing}

<!-- needs more details -->

I modelli di frammento di contenuto devono essere pubblicati quando/prima che vengano pubblicati eventuali frammenti di contenuto dipendenti.

>[!NOTE]
>
>Se un autore tenta di pubblicare un frammento di contenuto per il quale il modello non è ancora stato pubblicato, un elenco di selezione lo indicherà e il modello verrà pubblicato con il frammento.

Non appena un modello viene pubblicato, viene *bloccato* in modalità READ-ONLY sull&#39;autore. Questo obiettivo è quello di evitare modifiche che potrebbero causare errori agli schemi e alle query GraphQL esistenti, soprattutto nell’ambiente di pubblicazione. È indicato nella console da **Bloccato**.

Quando il modello è **Bloccato** (in modalità DI SOLA LETTURA), è possibile visualizzare il contenuto e la struttura dei modelli, ma non è possibile modificarli direttamente; anche se puoi gestire **Bloccato** modelli dalla console o dall’editor modelli.

## Novità {#whats-next}

Dopo aver appreso le nozioni di base, il passaggio successivo consiste nell’iniziare a creare modelli di frammenti di contenuto personalizzati.

## Risorse aggiuntive {#additional-resources}

* [Concetti relativi all’authoring](/help/sites-authoring/author.md)

* [Operazioni di base](/help/sites-authoring/basic-handling.md) - questa pagina si basa principalmente sul **Sites** console, ma molte delle funzioni sono utili anche per navigare verso e intervenire su di esse, **Modelli per frammenti di contenuto** in **Risorse** console.

* [Utilizzo di frammenti di contenuto](/help/assets/content-fragments/content-fragments.md)

   * [Modelli per frammenti di contenuto](/help/assets/content-fragments/content-fragments-models.md)

      * [Definizione del modello per frammenti di contenuto](/help/assets/content-fragments/content-fragments-models.md#defining-your-content-fragment-model)

      * [Abilitazione o disabilitazione di un modello di frammento di contenuto](/help/assets/content-fragments/content-fragments-models.md#enabling-disabling-a-content-fragment-model)

      * [Consentire modelli di frammenti di contenuto nella cartella delle risorse](/help/assets/content-fragments/content-fragments-models.md#allowing-content-fragment-models-assets-folder)

      * [Eliminazione di un modello di frammento di contenuto](/help/assets/content-fragments/content-fragments-models.md#deleting-a-content-fragment-model)

      * [Pubblicazione di un modello di frammento di contenuto](/help/assets/content-fragments/content-fragments-models.md#publishing-a-content-fragment-model)

      * [Annullamento della pubblicazione di un modello di frammento di contenuto](/help/assets/content-fragments/content-fragments-models.md#unpublishing-a-content-fragment-model)

      * [Modelli per frammenti di contenuto bloccati (pubblicati)](/help/assets/content-fragments/content-fragments-models.md#locked-published-content-fragment-models)

* Guide introduttive

   * [Guida rapida alla creazione di modelli di frammenti di contenuto headless](/help/sites-developing/headless/getting-started/create-content-model.md)
