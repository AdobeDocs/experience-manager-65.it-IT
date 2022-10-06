---
title: Panoramica delle comunicazioni interattive
seo-title: Interactive Communications Overview
description: Questo articolo include una panoramica, esempi di casi d’uso, un flusso di lavoro di creazione e differenze tra le comunicazioni interattive e le lettere.
seo-description: Interactive Communication key capabilities, sample use cases, creation workflow, and differences between Interactive Communication and Correspondence Management
uuid: a06b4ac7-ca20-4d6d-b2b7-87b21e2f5cf9
contentOwner: gtalwar
topic-tags: interactive-communications, introduction
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 67b03098-c58d-4a57-90e0-e4ddd78e5d99
exl-id: 6cfbeec0-0be3-48b2-a4bb-fd19c69c92c7
source-git-commit: 415744ca5c46a1495fe90369c162158c7fc2f1d4
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 7%

---


# Panoramica delle comunicazioni interattive {#interactive-communications-overview}

Questo articolo include una panoramica, esempi di casi d’uso, un flusso di lavoro di creazione e differenze tra le comunicazioni interattive e le lettere.

![](do-not-localize/correspondence-management.png)

Le comunicazioni interattive centralizzano e gestiscono la creazione, l&#39;assemblaggio e la distribuzione di corrispondenze sicure, personalizzate e interattive quali corrispondenza aziendale, documenti, dichiarazioni, note sui benefit, e-mail di marketing, fatture e kit di benvenuto.

## Funzionalità principali {#key-capabilities}

Di seguito sono elencate le funzionalità principali delle comunicazioni interattive:

- Integrazione preconfigurata con il modello dati del modulo per consentire un accesso semplice e semplificato ai database back-end e ad altri sistemi CRM, come MS® Dynamics
- Interfaccia di authoring integrata per canali web e di stampa con la possibilità di generare automaticamente il canale web dal canale di stampa
- Grafici per presentare informazioni in formati visivi facilmente comprensibili in stampa e web
- I frammenti di documento supportano l’editor di regole e il modello di dati del modulo
- L&#39;interfaccia utente dell&#39;agente visualizza la stampa e l&#39;anteprima web della comunicazione interattiva
- Trascinare i componenti per creare rapidamente canali di stampa e web

## Creazione di comunicazioni interattive {#interactive-communication-creation}

![interattivo_comunicazione-01](assets/interactive_communication-01.jpg)

### Flusso di lavoro {#workflow}

Per creare una comunicazione interattiva, fai clic su [mattoni](#buildingblocks) per la comunicazione interattiva, esegui le seguenti operazioni:

1. Scegli [creare una comunicazione interattiva](/help/forms/using/create-interactive-communication.md).

1. Specifica la [modello dati modulo](/help/forms/using/data-integration.md), servizio di precompilazione e [modelli di canale web e di stampa](/help/forms/using/web-channel-print-channel.md). Puoi scegliere di generare un canale web dal canale di stampa.

1. Utilizzo della [interfaccia a trascinamento](/help/forms/using/introduction-interactive-communication-authoring.md), aggiungi frammenti di documento, immagini, componenti per la stampa e il canale web della comunicazione interattiva, a seconda delle esigenze.
1. Configura le proprietà dei componenti inseriti, ad esempio:

   1. [Immagini](/help/forms/using/create-interactive-communication.md#step2)
   1. [Tabelle](/help/forms/using/create-interactive-communication.md#tables) (Inclusi Frammenti Di Layout)
   1. [Grafici](/help/forms/using/chart-component-interactive-communications.md)
   1. [Frammenti di documento](/help/forms/using/create-interactive-communication.md#document-fragment-properties)

1. Visualizzare in anteprima i canali web e di stampa e, se necessario, modificare la comunicazione interattiva.
1. L’agente utilizza l’interfaccia utente dell’agente in [preparare la comunicazione interattiva](/help/forms/using/prepare-send-interactive-communication.md) per l’invio al processo destinatario/post.

### Blocchi di generazione {#buildingblocks}

Di seguito sono riportati i blocchi costitutivi necessari per la creazione di una comunicazione interattiva:

- [Modello dati modulo](/help/forms/using/data-integration.md)
- [Modelli di canale web e di stampa](/help/forms/using/web-channel-print-channel.md)
- [Frammenti di documento](/help/forms/using/document-fragments.md)
- Immagini
- [Temi](/help/forms/using/themes.md) per il canale Web

## Comunicazioni Interattive E Gestione Della Corrispondenza {#interactive-communications-vs-correspondence-management}

La comunicazione interattiva è l’approccio predefinito e consigliato per creare comunicazioni con i clienti. Per continuare a utilizzare le lettere create in AEM 6.3 Forms e AEM 6.2 Forms, è necessario [installare un pacchetto di compatibilità](/help/forms/using/compatibility-package.md). Di seguito è riportato un confronto tra le funzionalità di comunicazione interattiva e lettera.

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
   <td>Non supportato nel modello dati modulo</td>
   <td>Supportato nel dizionario dati</td>
  </tr>
  <tr>
   <td>Editor di regole</td>
   <td>
    <ul>
     <li>Editor di regole di supporto per testo e condizioni per la creazione di condizioni in linea</li>
     <li>L’editor delle comunicazioni interattive supporta l’applicazione di regole sui componenti del canale web</li>
    </ul> </td>
   <td>Nessuna interfaccia utente per la creazione dell’espressione condizionale</td>
  </tr>
  <tr>
   <td>Authoring  </td>
   <td>Interfaccia di trascinamento per la costruzione di canali web e di stampa</td>
   <td>Nessun meccanismo di trascinamento della selezione </td>
  </tr>
  <tr>
   <td>Grafici</td>
   <td>Grafici supportati sia nella stampa che nel canale web</td>
   <td>Non supportato</td>
  </tr>
  <tr>
   <td>Temi</td>
   <td>Utilizza i temi per personalizzare lo stile del canale web</td>
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
   <td>Firma dell'agente</td>
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
