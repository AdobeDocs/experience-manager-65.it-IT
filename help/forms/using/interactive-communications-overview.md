---
title: Panoramica delle comunicazioni interattive
description: Questo articolo include una panoramica, alcuni esempi di casi di utilizzo, un flusso di lavoro per la creazione e differenze tra comunicazione interattiva e lettera.
contentOwner: gtalwar
topic-tags: interactive-communications, introduction
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 6cfbeec0-0be3-48b2-a4bb-fd19c69c92c7
solution: Experience Manager, Experience Manager Forms
feature: Interactive Communication
role: Admin, User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '487'
ht-degree: 7%

---


# Panoramica delle comunicazioni interattive {#interactive-communications-overview}

Questo articolo include una panoramica, alcuni esempi di casi di utilizzo, un flusso di lavoro per la creazione e differenze tra comunicazione interattiva e lettera.

![immagine protagonista](do-not-localize/correspondence-management.png)

Le comunicazioni interattive centralizzano e gestiscono la creazione, l’assemblaggio e la distribuzione di corrispondenze sicure, personalizzate e interattive, quali corrispondenza aziendale, documenti, dichiarazioni, note sui benefit, e-mail di marketing, fatture e kit di benvenuto.

## Funzionalità principali {#key-capabilities}

Di seguito sono riportate le funzionalità principali delle comunicazioni interattive:

- Integrazione preconfigurata con il modello di dati del modulo per consentire un accesso semplice e semplificato ai database back-end e ad altri sistemi di gestione delle relazioni con i clienti, come MS® Dynamics
- Interfaccia di authoring integrata per canali di stampa e web, con la possibilità di generare automaticamente un canale web dal canale di stampa
- Grafici per presentare informazioni in formati visivi facilmente comprensibili su stampa e web
- I frammenti di documento supportano l’editor di regole e il modello di dati del modulo
- L&#39;interfaccia utente dell&#39;agente visualizza la stampa e l&#39;anteprima Web della comunicazione interattiva
- Trascinare i componenti per creare rapidamente canali di stampa e web

## Creazione di comunicazioni interattive {#interactive-communication-creation}

![comunicazione_interattiva-01](assets/interactive_communication-01.jpg)

### Flusso di lavoro {#workflow}

Per creare una comunicazione interattiva, prepara i [blocchi predefiniti](#buildingblocks) per la comunicazione interattiva, quindi completa i passaggi seguenti:

1. Scegli di [creare una comunicazione interattiva](/help/forms/using/create-interactive-communication.md).

1. Specifica il [modello dati modulo](/help/forms/using/data-integration.md), il servizio di precompilazione e [modelli di stampa e canale Web](/help/forms/using/web-channel-print-channel.md). Puoi scegliere di generare un canale web dal canale di stampa.

1. Utilizzando l&#39;interfaccia [trascinamento della selezione](/help/forms/using/introduction-interactive-communication-authoring.md), aggiungere frammenti di documento, immagini, componenti per la stampa e il canale Web della comunicazione interattiva, in base alle esigenze.
1. Configura le proprietà dei componenti inseriti, ad esempio:

   1. [Immagini](/help/forms/using/create-interactive-communication.md#step2)
   1. [Tabelle](/help/forms/using/create-interactive-communication.md#tables) (Inclusi I Frammenti Di Layout)
   1. [Grafici](/help/forms/using/chart-component-interactive-communications.md)
   1. [Frammenti di documenti](/help/forms/using/create-interactive-communication.md#document-fragment-properties)

1. Visualizzare l&#39;anteprima dei canali di stampa e web e, se necessario, modificare la comunicazione interattiva.
1. L&#39;agente utilizza l&#39;interfaccia utente dell&#39;agente per [preparare la comunicazione interattiva](/help/forms/using/prepare-send-interactive-communication.md) per inviarla al processo destinatario/post.

### Blocchi predefiniti {#buildingblocks}

Di seguito sono riportati gli elementi costitutivi necessari per la creazione di una comunicazione interattiva:

- [Modello dati modulo](/help/forms/using/data-integration.md)
- [Stampa e modelli di canale web](/help/forms/using/web-channel-print-channel.md)
- [Frammenti di documenti](/help/forms/using/document-fragments.md)
- Immagini
- [Temi](/help/forms/using/themes.md) per il canale Web

## Comunicazione Interattiva E Gestione Della Corrispondenza {#interactive-communications-vs-correspondence-management}

La comunicazione interattiva è l’approccio predefinito e consigliato per creare comunicazioni con i clienti. Per continuare a utilizzare le lettere create in Forms AEM 6.3 e AEM 6.2 Forms, è necessario [installare un pacchetto di compatibilità](/help/forms/using/compatibility-package.md). Di seguito è riportato un confronto tra le funzionalità di comunicazione interattiva e lettera.

<table>
 <tbody>
  <tr>
   <td><strong>Funzionalità</strong></td>
   <td><strong>Comunicazione interattiva</strong></td>
   <td><strong>Lettera</strong></td>
  </tr>
  <tr>
   <td>Output</td>
   <td>Stampa e Web</td>
   <td>Stampa</td>
  </tr>
  <tr>
   <td>Schema</td>
   <td>Modello dati modulo </td>
   <td>Dizionario dati </td>
  </tr>
  <tr>
   <td>Localizzazione</td>
   <td>Non supportato nel modello dati del modulo</td>
   <td>Supportato nel dizionario dati</td>
  </tr>
  <tr>
   <td>Editor regole</td>
   <td>
    <ul>
     <li>Editor di regole per il supporto di testo e condizioni per la creazione di condizioni in linea</li>
     <li>L’editor di comunicazione interattiva supporta l’applicazione di regole sui componenti del canale web</li>
    </ul> </td>
   <td>Nessuna interfaccia utente per la creazione di espressioni condizionali</td>
  </tr>
  <tr>
   <td>Authoring</td>
   <td>Interfaccia di trascinamento per la costruzione di canali di stampa e web</td>
   <td>Nessun meccanismo di trascinamento della selezione </td>
  </tr>
  <tr>
   <td>Grafici</td>
   <td>Grafici supportati nei canali di stampa e web</td>
   <td>Non supportato</td>
  </tr>
  <tr>
   <td>Temi</td>
   <td>Utilizza i temi per assegnare uno stile al canale web</td>
   <td>Non supporta i temi</td>
  </tr>
   <tr>
   <td>Bozze</td>
   <td>Supportato</td>
   <td>Supportato</td>
  </tr>
   <tr>
   <td>Invii</td>
   <td>Supportato</td>
   <td>Supportato</td>
  </tr>
  <tr>
  <tr>
   <td>Controllo</td>
   <td>Non supportato</td>
   <td>Funzione supportata</td>
  </tr>
   <tr>
   <td>Controllo delle versioni</td>
   <td>Non supportato</td>
   <td>Funzione supportata</td>
  </tr>
   <td>Elaborazione batch</td>
   <td>Supportato </td>
   <td>Supportato</td>
  </tr>
  <tr>
   <td>Firma agente</td>
   <td>Non supportato</td>
   <td>Funzione supportata</td>
  </tr>
  <tr>
   <td>Funzioni remote</td>
   <td>Non supportato</td>
   <td>Funzione supportata</td>
  </tr>
 </tbody>
</table>
