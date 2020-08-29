---
title: Panoramica sulle comunicazioni interattive
seo-title: Panoramica sulle comunicazioni interattive
description: Questo articolo include una panoramica, esempi di casi di utilizzo, un flusso di lavoro per la creazione e le differenze tra le comunicazioni interattive e le lettere.
seo-description: Funzionalità chiave di comunicazione interattiva, esempi di casi di utilizzo, flusso di lavoro di creazione e differenze tra Comunicazione interattiva e Gestione della corrispondenza
uuid: a06b4ac7-ca20-4d6d-b2b7-87b21e2f5cf9
contentOwner: gtalwar
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: introduction
discoiquuid: 67b03098-c58d-4a57-90e0-e4ddd78e5d99
translation-type: tm+mt
source-git-commit: af326f2d2b278fe36df05afc8c172f74c99a064c
workflow-type: tm+mt
source-wordcount: '505'
ht-degree: 5%

---


# Panoramica sulle comunicazioni interattive {#interactive-communications-overview}

Questo articolo include una panoramica, esempi di casi di utilizzo, un flusso di lavoro per la creazione e le differenze tra le comunicazioni interattive e le lettere.

![](do-not-localize/correspondence-management.png)

Le comunicazioni interattive centralizzano e gestiscono la creazione, l&#39;assemblaggio e la distribuzione di corrispondenze sicure, personalizzate e interattive quali corrispondenza aziendale, documenti, dichiarazioni, note sui benefit, e-mail di marketing, fatture e kit di benvenuto.

## Funzionalità chiave {#key-capabilities}

Di seguito sono elencate le funzionalità chiave delle comunicazioni interattive:

* Integrazione standard con il modello dati del modulo per consentire un accesso semplice e semplificato ai database back-end e ad altri sistemi CRM, come MS® Dynamics
* Interfaccia di authoring integrata per canali Web e di stampa con la possibilità di generare automaticamente canali Web dal canale di stampa
* Grafici per presentare informazioni in formati visivi facilmente comprensibili per la stampa e il Web
* I frammenti di documento supportano l&#39;editor di regole e il modello di dati del modulo
* L&#39;interfaccia utente dell&#39;agente visualizza la stampa e l&#39;anteprima Web della comunicazione interattiva
* Trascinare i componenti per creare rapidamente canali di stampa e Web

## Interactive Communication creation  {#interactive-communication-creation}

![interactive_communication-01](assets/interactive_communication-01.jpg)

### Flusso di lavoro {#workflow}

Per creare una comunicazione interattiva, preparate gli [elementi](#buildingblocks) di base per la comunicazione interattiva e completate i seguenti passaggi:

1. Scegliete di [creare una comunicazione](/help/forms/using/create-interactive-communication.md)interattiva.

1. Specificare il modello [di dati del](/help/forms/using/data-integration.md)modulo, il servizio di precompilazione, nonché i modelli [per la](/help/forms/using/web-channel-print-channel.md)stampa e il canale Web. È possibile scegliere di generare un canale Web dal canale di stampa.

1. Utilizzando l&#39;interfaccia [di](/help/forms/using/introduction-interactive-communication-authoring.md)trascinamento, puoi aggiungere frammenti di documento, immagini, componenti per la stampa e il canale Web della comunicazione interattiva, a seconda delle necessità.
1. Configurare le proprietà dei componenti inseriti, ad esempio:

   1. [Immagini](/help/forms/using/create-interactive-communication.md#step2)
   1. [Tabelle](/help/forms/using/create-interactive-communication.md#tables) (Inclusi I Frammenti Di Layout)
   1. [Grafici](/help/forms/using/chart-component-interactive-communications.md)
   1. [Frammenti di documenti](/help/forms/using/create-interactive-communication.md#document-fragment-properties)

1. Visualizzate l&#39;anteprima dei canali di stampa e Web e, se necessario, modificate la comunicazione interattiva.
1. L’agente utilizza l’interfaccia utente dell’agente per [preparare la comunicazione](/help/forms/using/prepare-send-interactive-communication.md) interattiva da inviare al processo destinatario/post.

### Blocchi di generazione {#buildingblocks}

Di seguito sono riportati gli elementi costitutivi necessari per creare una comunicazione interattiva:

* [Modello dati modulo](/help/forms/using/data-integration.md)
* [Stampare e canalizzare i modelli](/help/forms/using/web-channel-print-channel.md)
* [Frammenti di documenti](/help/forms/using/document-fragments.md)
* Immagini
* [Temi](/help/forms/using/themes.md) per il canale Web

## Comunicazioni Interattive E Gestione Della Corrispondenza {#interactive-communications-vs-correspondence-management}

La comunicazione interattiva è l&#39;approccio predefinito e consigliato per creare comunicazioni con i clienti. Per continuare a utilizzare le lettere che creano in AEM 6.3 Forms e AEM 6.2 Forms, è necessario [installare un pacchetto](/help/forms/using/compatibility-package.md)di compatibilità. Di seguito è riportato un confronto tra le funzionalità di Comunicazione interattiva e lettera.

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
   <td>Editor regole</td>
   <td>
    <ul>
     <li>Editor di regole per il supporto del testo e delle condizioni per la creazione di condizioni in linea</li>
     <li>L'editor di comunicazione interattiva supporta l'applicazione di regole sui componenti del canale Web</li>
    </ul> </td>
   <td>Nessuna interfaccia utente per la creazione dell'espressione condizionale</td>
  </tr>
  <tr>
   <td>Authoring  </td>
   <td>Interfaccia di trascinamento per la creazione di canali Web e di stampa</td>
   <td>Nessun meccanismo di trascinamento </td>
  </tr>
  <tr>
   <td>Grafici</td>
   <td>Grafici supportati sia nella stampa che nel canale Web</td>
   <td>Non supportato</td>
  </tr>
  <tr>
   <td>Temi</td>
   <td>Utilizza i temi per definire lo stile del canale Web</td>
   <td>Non supporta i temi</td>
  </tr>
  <tr>
   <td>Controllo e controllo delle versioni</td>
   <td>Non supportato</td>
   <td>Supportato</td>
  </tr>
  <tr>
   <td>Bozze e gestione dell'istanza</td>
   <td>Non supportato</td>
   <td>Supportato</td>
  </tr>
  <tr>
   <td>Elaborazione batch</td>
   <td>Supportato </td>
   <td>Supportato</td>
  </tr>
  <tr>
   <td>Firma agente</td>
   <td>Non supportato</td>
   <td>Supportato</td>
  </tr>
  <tr>
   <td>Funzioni remote</td>
   <td>Non supportato</td>
   <td>Supportato</td>
  </tr>
 </tbody>
</table>

