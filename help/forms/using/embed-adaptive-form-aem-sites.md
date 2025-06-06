---
title: Incorporare un modulo adattivo o una comunicazione interattiva nella pagina dei siti AEM
description: Puoi incorporare moduli adattivi nelle pagine dei siti AEM. Gli utenti possono compilare e inviare moduli senza uscire dalle pagine del sito.
contentOwner: vishgupt
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author, interactive-communications
feature: Adaptive Forms,Foundation Components
exl-id: 00ee7929-649f-4cbb-be79-ba13ac73a16d
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '1150'
ht-degree: 1%

---

# Incorporare un modulo adattivo o una comunicazione interattiva nella pagina dei siti AEM {#embed-an-adaptive-form-or-interactive-communication-in-aem-sites-page}

<span class="preview"> Adobe consiglia di utilizzare l&#39;acquisizione dati moderna ed estensibile [Componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=it) per [la creazione di un nuovo Forms adattivo](/help/forms/using/create-an-adaptive-form-core-components.md) o [l&#39;aggiunta di Forms adattivo alle pagine AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Questi componenti rappresentano un progresso significativo nella creazione di Forms adattivi, garantendo esperienze utente straordinarie. Questo articolo descrive un approccio precedente all’authoring di Forms adattivi utilizzando i componenti di base. </span>

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/services/embed-adaptive-form-aem-sites.html?lang=it) |
| AEM 6.5 | Questo articolo |


## Panoramica {#overview}

AEM Forms consente agli sviluppatori di moduli di incorporare facilmente moduli adattivi e comunicazioni interattive in una pagina AEM Sites o in una pagina web ospitata al di fuori dell’AEM. Il modulo adattivo incorporato e la comunicazione interattiva sono completamente funzionali e gli utenti possono compilare e inviare il modulo senza uscire dalla pagina. Consente all’utente di rimanere nel contesto di altri elementi della pagina web e interagire contemporaneamente con il modulo o la comunicazione interattiva.

Per informazioni sull&#39;incorporamento di un modulo adattivo in una pagina Web esterna, vedere [Incorporare un modulo adattivo in una pagina Web esterna](/help/forms/using/embed-adaptive-form-external-web-page.md).

Nella pagina di AEM Sites puoi aggiungere un modulo adattivo o una comunicazione interattiva utilizzando:

* **[Componente contenitore AEM Forms](/help/forms/using/embed-adaptive-form-aem-sites.md#af-component)**
AEM Forms fornisce un componente che puoi aggiungere alle pagine del sito. Il componente Contenitore di AEM Forms consente di incorporare un modulo adattivo e una comunicazione interattiva.

* **[Browser risorse](/help/forms/using/embed-adaptive-form-aem-sites.md#asset-browser)**
Tutti i moduli e le comunicazioni interattive creati sono disponibili in Assets. Puoi trascinare il modulo come risorsa sulla pagina.

## Prerequisiti {#prerequisites}

Per incorporare un modulo adattivo o una comunicazione interattiva in una pagina dei siti AEM che utilizza un modello modificabile, accertati che il componente Modulo AEM sia configurato come componente consentito nel modello associato. Per ulteriori informazioni, vedere la sezione **Criteri e proprietà (contenitore di layout)** in [Creazione di modelli di pagina](/help/sites-authoring/templates.md).

Se è presente una pagina Sites che utilizza un modello statico, è necessario configurarla nel sistema paragrafo della pagina del sito. Per ulteriori informazioni, vedere [Configurazione dei componenti in modalità progettazione](/help/sites-authoring/default-components-designmode.md).

## Incorporazione di un modulo adattivo o di una comunicazione interattiva {#af-component}

Per incorporare un modulo adattivo o una comunicazione interattiva utilizzando il componente Contenitore di AEM Forms:

1. Apri la pagina dei siti AEM, in modalità di modifica, in cui desideri incorporare un modulo adattivo o una comunicazione interattiva.
1. Dal pannello del browser Componenti, trascina il componente Contenitore AEM Forms nella pagina.

   In alternativa, puoi cercare un modulo adattivo o una comunicazione interattiva nel browser Assets e trascinarlo sulla pagina Sites. Incorpora il modulo in un contenitore AEM Forms.

   >[!NOTE]
   >
   >Non sono supportati più componenti Contenitore di AEM Forms in una pagina.

1. Seleziona il componente Contenitore AEM Forms incorporato nella pagina Sites, quindi seleziona ![settings_icon](assets/settings_icon.png) nella barra delle azioni. Viene visualizzata la finestra di dialogo **[!UICONTROL Modifica contenitore AEM Forms]**.
1. Nella finestra di dialogo Modifica contenitore AEM Forms, specifica quanto segue.

   * **Tipo risorsa:** Seleziona il tipo di risorsa da incorporare. Le opzioni sono modulo adattivo e comunicazione interattiva
   * **Percorso risorsa**: sfoglia e seleziona il modulo adattivo o la comunicazione interattiva da incorporare. Viene compilato automaticamente se viene rilasciato dal browser Assets.
   * (Solo per moduli adattivi) **Invio Post**: seleziona l&#39;azione da attivare all&#39;invio del modulo. Puoi scegliere di visualizzare un messaggio di ringraziamento o una pagina di ringraziamento.

      * **Messaggio di ringraziamento**: scrivi un messaggio utilizzando l&#39;editor Rich Text per visualizzarlo all&#39;invio del modulo. Questa opzione è disponibile solo quando si sceglie di visualizzare un messaggio di ringraziamento.
      * **Pagina di ringraziamento**: sfoglia e seleziona la pagina da visualizzare all&#39;invio del modulo. Questa opzione è disponibile solo quando si sceglie di visualizzare una pagina di ringraziamento.
      * **Aggiorna pagina all&#39;invio**: abilita in modo da poter aggiornare la pagina contenente il modulo adattivo incorporato per visualizzare la pagina di ringraziamento. In caso contrario, la pagina di ringraziamento sostituisce il modulo adattivo nel contenitore AEM Forms, senza aggiornare la pagina. Questa opzione è disponibile solo quando si sceglie di visualizzare una pagina di ringraziamento.

   * **Tema**: seleziona un tema che definisca lo stile dei componenti del modulo adattivo o della comunicazione interattiva. Lo stile include proprietà di aspetto quali lo stile del carattere, il colore di sfondo, le dimensioni e l&#39;allineamento.
   * **Altezza**: specificare l&#39;altezza del contenitore. Lascia vuoto questo campo per ridimensionare automaticamente il contenitore.
   * **Libreria client CSS**: specificare il percorso di una libreria client CSS.

1. Salva le impostazioni. Il modulo adattivo o la comunicazione interattiva sono ora incorporati nella pagina.

## Pubblicazione di moduli adattivi incorporati e comunicazione interattiva {#publishing-embedded-adaptive-form-and-interactive-communication}

Prendiamo in considerazione i seguenti scenari per la pubblicazione di una risorsa incorporata (modulo adattivo o comunicazione interattiva) nella pagina dei siti AEM:

* Se pubblichi la pagina dei siti AEM per la prima volta e include un modulo adattivo incorporato o una comunicazione interattiva, pubblica la pagina dei siti e la risorsa incorporata.
* Se hai modificato solo il modulo adattivo incorporato o la comunicazione interattiva in una pagina del sito pubblicata, pubblica la risorsa originale e le modifiche si riflettono nella pagina del sito pubblicata. La pagina del sito pubblicata include un riferimento alla risorsa e non richiede la ripubblicazione della pagina.
* Se hai modificato la pagina Sites e il modulo adattivo incorporato o la comunicazione interattiva, ripubblica la pagina Sites e la risorsa incorporata.

## Modifica del modulo adattivo incorporato e della comunicazione interattiva {#modifying-embedded-adaptive-form-and-interactive-communication}

La pagina dei siti AEM mantiene un riferimento al modulo adattivo e alla comunicazione interattiva nel Contenitore AEM Forms. Pertanto, tutte le configurazioni e le proprietà, come il tema, gli stili e l’azione di invio, configurate nel modulo adattivo originale e nella comunicazione interattiva vengono mantenute nel modulo adattivo incorporato e nella comunicazione interattiva.

Per modificare la configurazione o la proprietà del modulo adattivo incorporato e della comunicazione interattiva, effettua una delle seguenti operazioni.

* Apri il modulo originale nei moduli adattivi o nella comunicazione interattiva nei rispettivi editor e modificali.
* Selezionare il modulo adattivo o la comunicazione interattiva dalla pagina del sito in modalità di modifica, quindi selezionare **[!UICONTROL Modifica in una nuova finestra]**. Il modulo originale viene aperto in modalità di modifica modificabile.

>[!NOTE]
>
>Le modifiche apportate al modulo adattivo originale o alla comunicazione interattiva si riflettono automaticamente nel modulo incorporato. Tuttavia, ripubblica il modulo adattivo, la comunicazione interattiva o la pagina del sito per riflettere le modifiche nella pagina pubblicata.

## Considerazioni e best practice {#considerations-and-best-practices}

Quando incorpori moduli adattivi nelle pagine dei siti AEM, considera gli aspetti seguenti:

* Intestazione e piè di pagina nel modulo originale non sono inclusi nel modulo incorporato.
* Le bozze utente e gli invii di moduli incorporati sono supportati e visibili nelle schede Bozze e Forms inviate nel portale dei moduli.
* L’azione di invio configurata nel modulo originale viene mantenuta nel modulo incorporato.
* Il targeting delle esperienze e i test A/B configurati nel modulo originale non funzionano nel modulo incorporato. Tuttavia, puoi utilizzare il targeting dell’esperienza sulla pagina Sites per presentare diversi moduli in base ai profili utente.
* Se hai configurato Adobe Analytics per il modulo originale, i dati di analisi del modulo incorporato vengono acquisiti in Adobe Analytics. Tuttavia, non è disponibile nel rapporto di analisi di Forms.
