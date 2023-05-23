---
title: Incorporazione di un componente collegamento in una pagina
seo-title: Embedding link component in a page
description: Puoi utilizzare il componente collegamento per collegare un documento adattivo o un modulo adattivo da qualsiasi pagina.
seo-description: You can use the link component to link an adaptive document or an adaptive form from any page.
uuid: 22f488fc-bb1a-40aa-a5f4-6d04d7250f29
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 9d63152d-41ca-4c7c-bb20-af16c7bdec13
docset: aem65
exl-id: eb45adf2-d0f3-4de6-92ac-fb146953e989
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 1%

---

# Incorporazione di un componente collegamento in una pagina{#embedding-link-component-in-a-page}

## Prerequisiti {#prerequisites}

Il componente Collegamento è un membro della categoria Servizi basati su documenti. Assicurati che la categoria Document Services sia visibile nel browser dei componenti AEM. Se la categoria non è elencata, segui i passaggi elencati in [Abilitazione dei componenti del portale Forms](/help/forms/using/enabling-forms-portal-components.md).

## Componente collegamento {#link-component}

Il componente Collegamento consente agli autori del portale dei moduli di creare un collegamento a un modulo adattivo da qualsiasi punto di una pagina. Il componente Collegamento è disponibile nella sezione Servizi documentali del browser componenti.

Per aggiungere un componente Collegamento alla pagina, effettua le seguenti operazioni:

1. Trascina **Collegamento** sulla pagina. Seleziona il componente e tocca ![cmppr](assets/cmppr.png). Viene visualizzata la finestra di dialogo Modifica componente collegamento.

   ![edit-link-component](assets/edit-link-component.png)

1. In **Visualizzazione** , specificare quanto segue:

   * **Didascalia collegamento**: testo di collegamento o didascalia del collegamento.
   * **Descrizione collegamento**: descrizione del collegamento.
   * **Modello di layout**: modello per il layout del componente Collegamento.

1. Apri **Info risorsa** e specifica il tipo di risorsa. Una risorsa può essere **modulo**. A seconda del tipo di risorsa selezionato, vengono visualizzate le opzioni elencate di seguito:

   * **Percorso risorsa**: percorso dell’archivio in cui è memorizzata la risorsa.

   * **Tipo di rendering**: formato di rendering, ovvero PDF, HTML o Auto. Il tipo di rendering automatico rileva l’ambiente utente e, di conseguenza, esegue il rendering del modulo come HTML o come PDF. Se, ad esempio, il modulo è accessibile da un dispositivo mobile, il tipo di rendering Automatico eseguirà il rendering del modulo in HTML.
   * **URL invio:**  URL del servlet in cui vengono inviati i dati del modulo.
   * **Profilo HTML**: profilo per il rendering del modulo come HTML.
   * **Profilo PDF**: profilo per il rendering del modulo come documento PDF.

1. Apri la scheda **Avanzate.** Potete specificare i parametri aggiuntivi nel formato coppia chiave-valore. Quando fai clic sul collegamento, questi parametri aggiuntivi vengono trasmessi insieme al modulo.

   Tocca **Fine** per salvare la configurazione.

## Best practice per l’utilizzo del componente Collegamento {#best-practices-for-using-link-component-br}

* Accertatevi di selezionare PDF come tipo di rendering se il percorso specificato in Percorso modulo punta a un documento il cui formato di rendering è PDF.
* È possibile specificare l&#39;URL di invio per un modulo in più posizioni e il relativo ordine di precedenza è il seguente:

   1. L’URL di invio incorporato nel modulo (nel pulsante di invio) ha la priorità più alta.
   1. L’URL di invio menzionato in Forms Manager ha la priorità media.
   1. L’URL di invio menzionato nel portale dei moduli ha la priorità più bassa.
