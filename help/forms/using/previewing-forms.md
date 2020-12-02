---
title: Anteprima di un modulo
seo-title: Anteprima di un modulo
description: È possibile visualizzare l'anteprima dei moduli prima di pubblicarli o attivarli per assicurarsi che soddisfino le aspettative. Le opzioni di anteprima possono variare a seconda dei tipi di modulo supportati.
seo-description: È possibile visualizzare l'anteprima dei moduli prima di pubblicarli o attivarli per assicurarsi che soddisfino le aspettative. Le opzioni di anteprima possono variare a seconda dei tipi di modulo supportati.
uuid: 9ec359ea-f518-441c-9c3d-e3c1ea07a532
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 377d804d-4a75-4c93-8125-d2660cf56418
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 2%

---


# Anteprima di un modulo {#previewing-a-form}

## Panoramica {#overview}

In  AEM Forms è possibile visualizzare l&#39;anteprima dei moduli e dei documenti presenti nella directory archivio. La funzione Anteprima consente di sapere esattamente l’aspetto e il funzionamento dei moduli quando vengono rilasciati agli utenti finali.

Durante la visualizzazione dell&#39;anteprima dei moduli, viene eseguito il rendering nell&#39;interfaccia interattiva e l&#39;utente può compilare i moduli con i dati. Durante l&#39;anteprima dei documenti, il rendering viene eseguito in modalità non interattiva e l&#39;utente può visualizzare solo il documento. Per i moduli è disponibile un&#39;ulteriore opzione di Anteprima personalizzata. Utilizzando questa opzione, è possibile visualizzare l&#39;anteprima del modulo utilizzando i dati provenienti da un file XML. I dati riempiono alcuni o tutti i campi del modulo di cui si sta visualizzando l&#39;anteprima.

Nella tabella seguente sono elencate le opzioni di anteprima disponibili per i diversi tipi di moduli supportati:

<table>
 <tbody>
  <tr>
   <td><strong>Tipo risorsa</strong><br /> </td>
   <td><strong>Opzioni di anteprima disponibili</strong><br /> </td>
  </tr>
  <tr>
   <td>Documento</td>
   <td>Anteprima PDF</td>
  </tr>
  <tr>
   <td>Modulo PDF</td>
   <td>Anteprima PDF con dati<br /> </td>
  </tr>
  <tr>
   <td>modulo adattivo</td>
   <td>Anteprima HTML e anteprima HTML con dati</td>
  </tr>
  <tr>
   <td>Modello modulo</td>
   <td>Anteprima PDF, anteprima PDF con dati, anteprima HTML, anteprima HTML con dati<br /> </td>
  </tr>
 </tbody>
</table>

## Anteprima di un modulo {#previewing-a-form-1}

1. Selezionate una risorsa da visualizzare in anteprima e fate clic su Anteprima ![aem6forms_preview](assets/aem6forms_preview.png) nella barra degli strumenti delle azioni.

   >[!NOTE]
   >
   >Per selezionare una risorsa, passate alla vista Elenco dalla vista scheda predefinita. Fare clic su ![aem6forms_viewlist](assets/aem6forms_viewlist.png) o ![aem6forms_viewcard](assets/aem6forms_viewcard.png) per cambiare visualizzazione.

1. Facendo clic su Anteprima vengono elencate le possibili opzioni di anteprima applicabili al tipo di risorsa selezionato. Fate clic sull’opzione desiderata per eseguire il rendering della risorsa selezionata in una nuova scheda.

   Le opzioni disponibili sono:

   * Anteprima come HTML
   * Anteprima con i dati
   * Anteprima come PDF (disponibile per i modelli di modulo)

## Anteprima con i dati {#preview-with-data}

Quando si seleziona **Anteprima con dati**, è possibile verificare l&#39;aspetto del modulo con i dati reali immessi. L’opzione Anteprima con dati consente di caricare un file XML contenente dati utente di esempio. I dati utente di esempio vengono utilizzati per compilare il modulo di anteprima nel formato scelto.

1. Selezionate una risorsa, fate clic su Anteprima ![aem6forms_preview](assets/aem6forms_preview.png), quindi selezionate **Anteprima con dati**.
1. Nella finestra di dialogo Anteprima modulo, specificare FormData come file XML. Fare clic su Anteprima per eseguire il rendering del modulo con i dati uniti da XML.

