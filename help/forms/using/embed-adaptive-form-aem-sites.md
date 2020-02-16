---
title: Incorporare un modulo adattivo o una comunicazione interattiva nella pagina Siti AEM
seo-title: Incorporare un modulo adattivo o una comunicazione interattiva nella pagina Siti AEM
description: È possibile incorporare moduli adattivi nelle pagine dei siti AEM. Gli utenti possono compilare e inviare i moduli senza uscire dalle pagine del sito.
seo-description: È possibile incorporare moduli adattivi nelle pagine dei siti AEM. Gli utenti possono compilare e inviare i moduli senza uscire dalle pagine del sito.
uuid: 59b49e2f-6d95-42e5-b31e-fc40936c42d2
contentOwner: vishgupt
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: interactive-communications
discoiquuid: 43362643-69cd-4006-a613-f998c79eeddc
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Incorporare un modulo adattivo o una comunicazione interattiva nella pagina Siti AEM {#embed-an-adaptive-form-or-interactive-communication-in-aem-sites-page}

## Panoramica {#overview}

AEM Forms consente agli sviluppatori di moduli di incorporare facilmente moduli adattivi e comunicazioni interattive in una pagina AEM Sites o in una pagina Web ospitata al di fuori di AEM. Il modulo adattivo incorporato e la comunicazione interattiva sono completamente funzionanti e gli utenti possono compilare e inviare il modulo senza uscire dalla pagina. Consente agli utenti di restare nel contesto di altri elementi della pagina Web e di interagire contemporaneamente con il modulo o la comunicazione interattiva.

Per informazioni sull&#39;incorporazione di un modulo adattivo in una pagina Web esterna, vedere [Incorporare un modulo adattivo in una pagina](/help/forms/using/embed-adaptive-form-external-web-page.md)Web esterna.

Nella pagina Siti AEM è possibile aggiungere un modulo adattivo o una comunicazione interattiva utilizzando:

* **[AEM Forms Container Component](/help/forms/using/embed-adaptive-form-aem-sites.md#af-component)**AEM Forms fornisce un componente che può essere aggiunto alle pagine del sito. Il componente Contenitore di AEM Forms consente di incorporare un modulo adattivo e una comunicazione interattiva.

* **[Browser](/help/forms/using/embed-adaptive-form-aem-sites.md#asset-browser)**risorse Tutti i moduli e le comunicazioni interattive creati sono disponibili in Risorse. È possibile trascinare il modulo come risorsa sulla pagina.

## Prerequisiti {#prerequisites}

Per incorporare un modulo adattivo o una comunicazione interattiva in una pagina siti AEM che utilizza un modello modificabile, accertati che il componente Modulo AEM sia configurato come componente consentito nel modello associato. Per ulteriori informazioni, vedere la sezione **Criteri e proprietà (Contenitore di layout)** in [Creazione di modelli](/help/sites-authoring/templates.md)di pagina.

Nel caso di una pagina Siti che utilizza un modello statico, è necessario configurarla nel sistema paragrafo della pagina del sito. Per ulteriori informazioni, consulta [Configurazione dei componenti in modalità Progettazione](/help/sites-authoring/default-components-designmode.md).

## Incorporazione di un modulo adattivo o comunicazione interattiva {#af-component}

Per incorporare un modulo adattivo o una comunicazione interattiva mediante il componente Contenitore di AEM Forms:

1. Aprite la pagina Siti AEM, in modalità di modifica, in cui desiderate incorporare un modulo adattivo o una comunicazione interattiva.
1. Dal browser Componenti, trascina sulla pagina il componente Contenitore di AEM Forms.

   In alternativa, potete cercare un modulo adattivo o una comunicazione interattiva nel browser Risorse e trascinarlo nella pagina Siti. Incorpora il modulo in un contenitore AEM Forms.

   >[!NOTE]
   >
   >Più componenti Contenitore di AEM Forms su una pagina non sono supportati.

1. Toccate il componente Contenitore di AEM Forms incorporato nella pagina dei siti, quindi toccate ![settings_icon](assets/settings_icon.png) nella barra delle azioni. Viene visualizzata la finestra di dialogo **[!UICONTROL Modifica contenitore]** AEM Forms.
1. Nella finestra di dialogo Modifica contenitore moduli AEM, specificate quanto segue.

   * **** Tipo risorsa: Selezionate il tipo di risorsa da incorporare. Le opzioni sono moduli adattivi e comunicazione interattiva
   * **Percorso** risorsa: Individuate e selezionate il modulo adattivo o la comunicazione interattiva da incorporare. Viene compilata automaticamente se viene rilasciata dal browser Risorse.
   * (Solo modulo adattivo) **Post-invio**: Selezionare l&#39;azione da attivare all&#39;invio del modulo. Potete scegliere di visualizzare un messaggio di ringraziamento o una pagina di ringraziamento.

      * **Messaggio** Di Ringraziamento: Scrivere un messaggio utilizzando l&#39;editor Rich Text da visualizzare durante l&#39;invio del modulo. Questa opzione è disponibile solo quando scegliete di mostrare un messaggio di ringraziamento.
      * **Pagina** di ringraziamento: Individuare e selezionare la pagina da visualizzare durante l&#39;invio del modulo. Questa opzione è disponibile solo quando scegliete di mostrare una pagina di ringraziamento.
      * **Aggiorna pagina all&#39;invio**: Consente di aggiornare la pagina contenente il modulo adattivo incorporato per visualizzare la pagina di ringraziamento. In caso contrario, la pagina di ringraziamento sostituisce il modulo adattivo nel contenitore AEM Forms senza aggiornare la pagina. Questa opzione è disponibile solo quando scegliete di mostrare una pagina di ringraziamento.
   * **Tema**: Selezionate un tema che definisca lo stile dei componenti del modulo adattivo o della comunicazione interattiva. Lo stile include proprietà di aspetto quali stile del font, colore di sfondo, dimensioni e allineamento.
   * **Altezza**: Specificate l&#39;altezza del contenitore. Lasciate vuoto per ridimensionare automaticamente il contenitore.
   * **Libreria** client CSS: Specificate il percorso di una libreria client CSS.


1. Salvate le impostazioni. Il modulo adattivo o la comunicazione interattiva ora è incorporato nella pagina.

## Pubblicazione di moduli adattivi incorporati e comunicazione interattiva {#publishing-embedded-adaptive-form-and-interactive-communication}

Esaminiamo i seguenti scenari per pubblicare una risorsa incorporata (modulo adattivo o comunicazione interattiva) nella pagina dei siti AEM:

* Se pubblicate per la prima volta la pagina dei siti AEM e include un modulo adattivo incorporato o una comunicazione interattiva, pubblicate la pagina dei siti e la risorsa incorporata.
* Se avete modificato solo il modulo adattivo incorporato o la comunicazione interattiva in una pagina del sito pubblicata, pubblicate la risorsa originale e le modifiche si riflettono nella pagina del sito pubblicato. La pagina del sito pubblicata include un riferimento alla risorsa e non richiede la ripubblicazione della pagina.
* Se avete modificato la pagina dei siti e il modulo adattivo incorporato o la comunicazione interattiva, ripubblicate la pagina dei siti e la risorsa incorporata.

## Modifica di moduli adattivi incorporati e comunicazione interattiva {#modifying-embedded-adaptive-form-and-interactive-communication}

Nella pagina dei siti AEM viene mantenuto un riferimento al modulo adattivo e alla comunicazione interattiva nel contenitore AEM Forms. Pertanto, tutte le configurazioni e proprietà, come il tema, gli stili e l&#39;azione Invia, configurate nel modulo adattivo originale e la comunicazione interattiva vengono mantenute nel modulo adattivo incorporato e nella comunicazione interattiva.

Per modificare qualsiasi configurazione o proprietà del modulo adattivo incorporato e della comunicazione interattiva, effettuare una delle seguenti operazioni.

* Aprire il modulo originale in moduli adattivi o nelle comunicazioni interattive nei rispettivi editor e modificarlo.
* Toccate il modulo adattivo o la comunicazione interattiva dalla pagina del sito in modalità di modifica, quindi toccate **[!UICONTROL Modifica in una nuova finestra]**. Il modulo originale viene aperto in modalità di modifica, modificabile dall&#39;utente.

>[!NOTE]
>
>Le modifiche apportate al modulo adattivo originale o alla comunicazione interattiva si riflettono automaticamente nel modulo incorporato. Tuttavia, ripubblicate il modulo adattivo, la comunicazione interattiva o la pagina del sito per riflettere le modifiche apportate alla pagina pubblicata.

## Considerazioni e procedure ottimali {#considerations-and-best-practices}

Quando incorporate moduli adattivi nelle pagine dei siti AEM, tenete presente quanto segue:

* L&#39;intestazione e il piè di pagina del modulo originale non sono inclusi nel modulo incorporato.
* Le bozze degli utenti e gli invii dei moduli incorporati sono supportati e visibili nelle schede Bozze e Moduli inviati nel portale dei moduli.
* L&#39;azione di invio configurata sul modulo originale viene mantenuta nel modulo incorporato.
* Il targeting delle esperienze e i test A/B configurati sul modulo originale non funzionano nel modulo incorporato. Tuttavia, è possibile utilizzare il targeting delle esperienze sulla pagina dei siti per presentare moduli diversi basati sui profili utente.
* Se Adobe Analytics è stato configurato per il modulo originale, i dati di analisi del modulo incorporato vengono acquisiti in Adobe Analytics. Tuttavia, non è disponibile nel report di analisi dei moduli.

