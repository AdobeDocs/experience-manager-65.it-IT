---
title: Incorporazione di un componente collegamento in una pagina
seo-title: Incorporazione di un componente collegamento in una pagina
description: Potete utilizzare il componente Collegamento per collegare un documento adattivo o un modulo adattivo da qualsiasi pagina.
seo-description: Potete utilizzare il componente Collegamento per collegare un documento adattivo o un modulo adattivo da qualsiasi pagina.
uuid: 22f488fc-bb1a-40aa-a5f4-6d04d7250f29
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 9d63152d-41ca-4c7c-bb20-af16c7bdec13
docset: aem65
translation-type: tm+mt
source-git-commit: f9ed171c188a4dfb71f12ae9c98105a4c1895542
workflow-type: tm+mt
source-wordcount: '432'
ht-degree: 1%

---


# Incorporazione del componente collegamento in una pagina{#embedding-link-component-in-a-page}

## Prerequisiti {#prerequisites}

Il componente Collegamento è membro della categoria Document Services. Assicurarsi che la categoria Document Services sia visibile nel browser dei componenti AEM. Se la categoria non è elencata, seguire i passaggi elencati in [Abilitazione dei componenti del portale dei moduli](/help/forms/using/enabling-forms-portal-components.md).

## Componente collegamento {#link-component}

Il componente Collegamento consente agli autori di un portale moduli di creare un collegamento a un modulo adattivo da qualsiasi punto di una pagina. Il componente Collegamento è disponibile nella sezione Document Services del browser Componenti.

Per aggiungere un componente Collegamento alla pagina, effettuate le seguenti operazioni:

1. Trascinare il componente **Link** sulla pagina. Selezionate il componente e toccate ![cmppr](assets/cmppr.png). Viene visualizzata la finestra di dialogo Modifica componente collegamento.

   ![edit-link-component](assets/edit-link-component.png)

1. Nella scheda **Display**, specificare quanto segue:

   * **Didascalia** collegamento: Collega testo o didascalia per il collegamento.
   * **Descrizione collegamento**: Descrizione del collegamento.
   * **Modello** di layout: Modello per il layout del componente Collegamento.

1. Aprite la scheda **Informazioni risorsa** e specificate il tipo di risorsa. Una risorsa può essere un **modulo**. A seconda del tipo di risorsa selezionata, vengono visualizzate le opzioni elencate di seguito:

   * **Percorso** risorsa: Percorso del repository in cui è memorizzata la risorsa.

   * **Tipo** di rendering: Il formato di rendering: PDF, HTML o Auto. Il tipo di rendering automatico rileva l&#39;ambiente dell&#39;utente ed esegue di conseguenza il rendering del modulo come HTML o come PDF. Ad esempio, se si accede al modulo da un dispositivo mobile, il tipo di rendering automatico esegue il rendering del modulo in HTML.
   * **Invia URL:**  URL al servlet in cui vengono inviati i dati del modulo.
   * **Profilo** HTML: Profilo per il rendering del modulo come HTML.
   * **Profilo** PDF: Profilo per il rendering del modulo come documento PDF.

1. Apri la scheda **Avanzate.** Potete specificare i parametri aggiuntivi nel formato della coppia chiave-valore. Quando si fa clic sul collegamento, questi parametri aggiuntivi vengono passati insieme al modulo.

   Toccate **Fine** per salvare la configurazione.

## Procedure ottimali per l&#39;utilizzo del componente Collegamento {#best-practices-for-using-link-component-br}

* Assicurarsi di selezionare PDF come tipo di rendering se il percorso specificato in Percorso modulo punta a un documento con PDF come formato di rendering consentito.
* È possibile specificare l&#39;URL di invio di un modulo in più punti e il relativo ordine di precedenza è il seguente:

   1. L&#39;URL di invio incorporato nel modulo (nel pulsante di invio) ha la priorità più alta.
   1. L’URL di invio indicato in Forms Manager ha la priorità media.
   1. L&#39;URL di invio indicato nel portale dei moduli ha la priorità più bassa.
