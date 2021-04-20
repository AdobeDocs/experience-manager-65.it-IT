---
title: Modelli per frammenti di contenuto
seo-title: Modelli per frammenti di contenuto
description: I modelli per frammenti di contenuto vengono utilizzati per creare frammenti di contenuto con contenuto strutturato.
seo-description: I modelli per frammenti di contenuto vengono utilizzati per creare frammenti di contenuto con contenuto strutturato.
uuid: 73e38629-37c6-4f68-97a9-62f9783cc3d4
content-type: reference
topic-tags: content-fragments
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
discoiquuid: 9da10294-2dc8-4e82-8d32-f034e6a5aeeb
docset: aem65
feature: Content Fragments
role: Business Practitioner, Administrator
translation-type: tm+mt
source-git-commit: aec4530fa93eacd151ca069c2da5d1bc92408e10
workflow-type: tm+mt
source-wordcount: '758'
ht-degree: 21%

---


# Modelli per frammenti di contenuto{#content-fragment-models}

I modelli per frammenti di contenuto definiscono la struttura del contenuto per i [frammenti di contenuto](/help/assets/content-fragments/content-fragments.md).

## Abilita modelli di frammenti di contenuto {#enable-content-fragment-models}

>[!CAUTION]
>
>Se non abiliti l’opzione **Modelli di frammento di contenuto** , l’opzione **Crea** non sarà disponibile per la creazione di nuovi modelli.

Per abilitare i modelli di frammento di contenuto è necessario:

* Abilitare l&#39;uso di modelli di frammenti di contenuto nel [Browser di configurazione](/help/sites-administering/configurations.md)
* Applica la configurazione alla cartella Assets

### Abilitare i modelli di frammenti di contenuto in Configuration Manager {#enable-content-fragment-models-in-configuration-manager}

Per [creare un nuovo modello di frammento di contenuto](#creating-a-content-fragment-model) **è necessario** prima abilitarli utilizzando Gestione configurazione:

>[!CAUTION]
>
>Le sottoconfigurazioni (una configurazione nidificata all’interno di una configurazione) non sono supportate per l’uso con Frammenti di contenuto.

1. Accedi a **Strumenti**, **Generali**, quindi apri **Browser configurazioni**.

1. Utilizza **Crea** per aprire la finestra di dialogo in cui:

   1. Specifica un **titolo**.
   1. Seleziona **Modelli di frammento di contenuto** per attivarne l’uso.

   ![cfm-6420-09](assets/cfm-6420-09.png)

1. Seleziona **Crea** per salvare la definizione.

<!-- 1. Select the location appropriate to your website. -->

### Applica la configurazione alla cartella delle risorse {#apply-the-configuration-to-your-assets-folder}

Quando la configurazione **global** è abilitata per i modelli di frammento di contenuto, tutti i modelli creati dagli utenti possono essere utilizzati in qualsiasi cartella Assets.

Per utilizzare altre configurazioni con una cartella Risorse simile, ovvero escludendo il formato globale, è necessario definire la connessione. Questa operazione viene eseguita dalla voce **Configurazione** della scheda **Cloud Services** della finestra **Proprietà cartella** della cartella specifica.

## Creazione di un modello di frammento di contenuto {#creating-a-content-fragment-model}

1. Passa a **Strumenti**, **Risorse**, quindi apri **Modelli di frammento di contenuto**.
1. Passa alla cartella appropriata per la [configurazione](#enable-content-fragment-models).
1. Utilizza **Crea** per aprire la procedura guidata.

   >[!CAUTION]
   >
   >Se l&#39;utilizzo dei modelli di frammento di contenuto [non è stato abilitato](#enable-content-fragment-models), l&#39;opzione **Crea** non sarà disponibile.

1. Specifica il **Titolo modello**. Se necessario, puoi anche aggiungere una **Descrizione**.

   ![cfm-6420-10](assets/cfm-6420-10.png)

1. Utilizza **Crea** per salvare il modello vuoto. Un messaggio indica il successo dell’azione, puoi selezionare **Apri** per modificare immediatamente il modello oppure **Fine** per tornare alla console.

## Definizione del modello per frammenti di contenuto {#defining-your-content-fragment-model}

Il modello per frammenti di contenuto definisce in modo efficace la struttura dei frammenti di contenuto risultanti. Utilizzando l&#39;editor modelli è possibile aggiungere e configurare i campi richiesti:

>[!CAUTION]
>
>La modifica di un modello di frammento di contenuto esistente può avere un impatto sui frammenti dipendenti.

1. Passa a **Strumenti**, **Risorse**, quindi apri **Modelli di frammento di contenuto**.

1. Passa alla cartella contenente il modello di frammento di contenuto.
1. Apri il modello richiesto per **Modifica**; utilizza l’azione rapida oppure seleziona il modello e quindi l’azione dalla barra degli strumenti.

   Una volta aperto l&#39;editor modelli mostra:

   * sinistra: campi già definiti
   * A destra: **Tipi di dati** disponibili per la creazione di campi, oltre alle **Proprietà** da utilizzare dopo la creazione.

   >[!NOTE]
   >
   >Quando un campo è **obbligatorio**, l’**Etichetta** indicata nel riquadro a sinistra sarà contrassegnata con un asterisco (*****).

   ![cfm-6420-12](assets/cfm-6420-12.png)

1. **Aggiunta di un campo**

   * Trascina un tipo di dati obbligatorio nella posizione desiderata per un campo:

   ![cfm-6420-11](assets/cfm-6420-11.png)

   * Una volta aggiunto un campo al modello, il pannello di destra mostra le **Proprietà** che possono essere definite per quel particolare tipo di dati. Qui puoi definire ciò che è necessario per quel campo. Esempio:

   ![cfm-6420-13](assets/cfm-6420-13.png)

   >[!NOTE]
   Per il tipo di dati **Testo su più righe** è possibile definire il **Tipo predefinito** come:
   * **Formato RTF**

   * **Markdown**

   * **Testo normale**

   Se non viene specificato, per questo campo viene utilizzato il valore predefinito **Rich Text**.
   La modifica del **Tipo predefinito** in un modello per frammenti di contenuto avrà effetto solo su un frammento esistente correlato, una volta che il frammento è stato aperto nell’editor e successivamente salvato.

1. **Rimozione di un campo**

   Seleziona il campo richiesto, quindi tocca o fai clic sull’icona del cestino. Viene richiesto di confermare l’operazione.

   ![cf-32](assets/cf-32.png)

1. Dopo aver aggiunto tutti i campi obbligatori e definito le proprietà, utilizza **Salva** per mantenere la definizione. Esempio:

   ![cfm-6420-14](assets/cfm-6420-14.png)

## Eliminazione di un modello di frammento di contenuto {#deleting-a-content-fragment-model}

>[!CAUTION]
L’eliminazione di un modello di frammento di contenuto può avere un impatto sui frammenti dipendenti.

Per eliminare un modello di frammento di contenuto:

1. Passa a **Strumenti**, **Risorse**, quindi apri **Modelli di frammento di contenuto**.

1. Passa alla cartella contenente il modello di frammento di contenuto.
1. Seleziona il modello, seguito da **Elimina** dalla barra degli strumenti.

   >[!NOTE]
   Se si fa riferimento al modello, viene visualizzato un avviso. Agisci in modo appropriato.

## Pubblicazione di un modello di frammento di contenuto {#publishing-a-content-fragment-model}

I modelli di frammento di contenuto devono essere pubblicati quando/prima che vengano pubblicati eventuali frammenti di contenuto dipendenti.

Per pubblicare un modello di frammento di contenuto:

1. Passa a **Strumenti**, **Risorse**, quindi apri **Modelli di frammento di contenuto**.

1. Passa alla cartella contenente il modello di frammento di contenuto.
1. Seleziona il modello, seguito da **Pubblica** dalla barra degli strumenti.

   >[!NOTE]
   Se pubblichi un frammento di contenuto per il quale il modello non è ancora stato pubblicato, un elenco di selezione lo indicherà e il modello verrà pubblicato con il frammento.

