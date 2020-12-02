---
title: Modelli per frammenti di contenuto
seo-title: Modelli per frammenti di contenuto
description: I modelli di frammenti di contenuto vengono utilizzati per creare frammenti di contenuto con contenuto strutturato.
seo-description: I modelli di frammenti di contenuto vengono utilizzati per creare frammenti di contenuto con contenuto strutturato.
uuid: 73e38629-37c6-4f68-97a9-62f9783cc3d4
content-type: reference
topic-tags: content-fragments
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
discoiquuid: 9da10294-2dc8-4e82-8d32-f034e6a5aeeb
docset: aem65
translation-type: tm+mt
source-git-commit: ce64b148ba96cc64670aaf96c1b201bafa282b98
workflow-type: tm+mt
source-wordcount: '745'
ht-degree: 22%

---


# Modelli per frammenti di contenuto{#content-fragment-models}

I modelli di frammenti di contenuto definiscono la struttura del contenuto per i [frammenti di contenuto](/help/assets/content-fragments/content-fragments.md).

## Abilita modelli di frammenti di contenuto {#enable-content-fragment-models}

>[!CAUTION]
>
>Se non si abilita l&#39;opzione **Modelli di frammenti di contenuto**, l&#39;opzione **Crea** non sarà disponibile per la creazione di nuovi modelli.

Per abilitare i modelli di frammenti di contenuto è necessario:

* Abilitare l&#39;utilizzo di modelli di frammento di contenuto nel [browser di configurazione](/help/sites-administering/configurations.md)
* Applica la configurazione alla cartella Risorse

### Abilita modelli di frammenti di contenuto in Configuration Manager {#enable-content-fragment-models-in-configuration-manager}

Per [creare un nuovo modello di frammento di contenuto](#creating-a-content-fragment-model) **è necessario** prima attivarlo utilizzando Gestione configurazione:

1. Accedi a **Strumenti**, **Generali**, quindi apri **Browser configurazioni**.
1. Selezionate la posizione appropriata per il sito Web.
1. Utilizzate **Create** per aprire la finestra di dialogo in cui:

   1. Specificare un **Titolo**.
   1. Selezionare **Modelli di frammenti di contenuto** per attivarne l&#39;uso.

   ![cfm-6420-09](assets/cfm-6420-09.png)

1. Selezionare **Crea** per salvare la definizione.

### Applica la configurazione alla cartella delle risorse {#apply-the-configuration-to-your-assets-folder}

Quando la configurazione **global** è abilitata per i modelli di frammenti di contenuto, tutti i modelli creati dagli utenti possono essere utilizzati in qualsiasi cartella Risorse.

Per utilizzare altre configurazioni con una cartella Risorse simile, ovvero escludendo il formato globale, è necessario definire la connessione. Questa operazione viene eseguita dalla voce **Configurazione** della scheda **Cloud Services** della finestra **Proprietà cartella** della cartella specifica.

## Creazione di un modello di frammento di contenuto {#creating-a-content-fragment-model}

1. Andate a **Strumenti**, **Risorse**, quindi aprite **Modelli di frammenti di contenuto**.
1. Andate alla cartella appropriata per la [configurazione](#enable-content-fragment-models).
1. Utilizzare **Create** per aprire la procedura guidata.

   >[!CAUTION]
   >
   >Se l&#39;utilizzo di [modelli di frammento di contenuto non è stato abilitato](#enable-content-fragment-models), l&#39;opzione **Crea** non sarà disponibile.

1. Specifica il **Titolo modello**. Se necessario, puoi anche aggiungere una **Descrizione**.

   ![cfm-6420-10](assets/cfm-6420-10.png)

1. Utilizzare **Create** per salvare il modello vuoto. Un messaggio indica l&#39;esito positivo dell&#39;azione, è possibile selezionare **Apri** per modificare immediatamente il modello, oppure **Fine** per tornare alla console.

## Definizione del modello di frammento di contenuto {#defining-your-content-fragment-model}

Il modello di frammento di contenuto definisce in modo efficace la struttura dei frammenti di contenuto risultanti. Utilizzando l’editor modelli potete aggiungere e configurare i campi richiesti:

>[!CAUTION]
>
>La modifica di un modello di frammento di contenuto esistente può avere un impatto sui frammenti dipendenti.

1. Andate a **Strumenti**, **Risorse**, quindi aprite **Modelli di frammenti di contenuto**.

1. Individuate la cartella che contiene il modello di frammento di contenuto.
1. Aprire il modello richiesto per **Edit**; utilizzare l&#39;azione rapida oppure selezionare il modello e quindi l&#39;azione dalla barra degli strumenti.

   Una volta aperto l&#39;editor modelli mostra:

   * left: campi già definiti
   * A destra: **Tipi di dati** disponibili per la creazione di campi, oltre alle **Proprietà** da utilizzare dopo la creazione.

   >[!NOTE]
   >
   >Quando un campo è **obbligatorio**, l’**Etichetta** indicata nel riquadro a sinistra sarà contrassegnata con un asterisco (*****).

   ![cfm-6420-12](assets/cfm-6420-12.png)

1. **Aggiunta di un campo**

   * Trascinare un tipo di dati richiesto nella posizione desiderata per un campo:

   ![cfm-6420-11](assets/cfm-6420-11.png)

   * Una volta aggiunto un campo al modello, il pannello a destra mostrerà le **Proprietà** che possono essere definite per quel particolare tipo di dati. Qui è possibile definire i requisiti necessari per tale campo. Esempio:

   ![cfm-6420-13](assets/cfm-6420-13.png)

   >[!NOTE]
   Per il tipo di dati **Testo su più righe** è possibile definire il **Tipo predefinito** come:
   * **Formato RTF**

   * **Markdown**

   * **Testo normale**

   Se non viene specificato, per questo campo viene utilizzato il valore predefinito **Rich Text**.
   La modifica del **Tipo predefinito** in un modello per frammenti di contenuto avrà effetto solo su un frammento esistente correlato, una volta che il frammento è stato aperto nell’editor e successivamente salvato.

1. **Rimozione di un campo**

   Selezionate il campo desiderato, quindi toccate o fate clic sull&#39;icona del cestino. Viene richiesto di confermare l’operazione.

   ![cf-32](assets/cf-32.png)

1. Dopo aver aggiunto tutti i campi obbligatori e definito le proprietà, utilizzare **Save** per mantenere la definizione. Esempio:

   ![cfm-6420-14](assets/cfm-6420-14.png)

## Eliminazione di un modello di frammento di contenuto {#deleting-a-content-fragment-model}

>[!CAUTION]
L&#39;eliminazione di un modello di frammento di contenuto può avere un impatto sui frammenti dipendenti.

Per eliminare un modello di frammento di contenuto:

1. Andate a **Strumenti**, **Risorse**, quindi aprite **Modelli di frammenti di contenuto**.

1. Individuate la cartella che contiene il modello di frammento di contenuto.
1. Selezionare il modello, seguito da **Elimina** dalla barra degli strumenti.

   >[!NOTE]
   Se al modello viene fatto riferimento, verrà visualizzato un avviso. Adottare le misure appropriate.

## Pubblicazione di un modello di frammento di contenuto {#publishing-a-content-fragment-model}

I modelli di frammenti di contenuto devono essere pubblicati quando/prima che vengano pubblicati eventuali frammenti di contenuto dipendenti.

Per pubblicare un modello di frammento di contenuto:

1. Andate a **Strumenti**, **Risorse**, quindi aprite **Modelli di frammenti di contenuto**.

1. Individuate la cartella che contiene il modello di frammento di contenuto.
1. Selezionate il modello, seguito da **Pubblica** dalla barra degli strumenti.

   >[!NOTE]
   Se si pubblica un frammento di contenuto per il quale il modello non è ancora stato pubblicato, verrà visualizzato un elenco di selezione e il modello verrà pubblicato insieme al frammento.

