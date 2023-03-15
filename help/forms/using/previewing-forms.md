---
title: Anteprima di un modulo
seo-title: Previewing a form
description: È possibile visualizzare l’anteprima dei moduli prima di pubblicarli o attivarli per assicurarsi che soddisfino le aspettative. Le opzioni di anteprima possono variare in base ai tipi di modulo supportati.
seo-description: You can preview your forms before publishing or activating to ensure it meets the expectations. Preview options may vary across the supported form types.
uuid: 9ec359ea-f518-441c-9c3d-e3c1ea07a532
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 377d804d-4a75-4c93-8125-d2660cf56418
feature: Adaptive Forms
exl-id: aed5703e-4fe6-4839-9657-c660ac48521e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '365'
ht-degree: 3%

---

# Anteprima di un modulo {#previewing-a-form}

## Panoramica {#overview}

In AEM Forms è possibile visualizzare in anteprima i moduli e i documenti presenti nella directory archivio. L’anteprima consente di sapere esattamente come si presentano e si comportano i moduli quando vengono rilasciati agli utenti finali.

Durante la visualizzazione dell’anteprima dei moduli, viene eseguito il rendering in un’interfaccia interattiva e l’utente può compilare i moduli con i relativi dati. Durante l&#39;anteprima dei documenti, il rendering viene eseguito in modalità non interattiva e l&#39;utente può visualizzare solo il documento. Per i moduli è disponibile un’opzione aggiuntiva Anteprima personalizzata. Utilizzando questa opzione, è possibile visualizzare in anteprima il modulo utilizzando i dati di un file XML. I dati compilano alcuni o tutti i campi del modulo visualizzati in anteprima.

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
   <td>Anteprima e anteprima di PDF con dati<br /> </td>
  </tr>
  <tr>
   <td>modulo adattivo</td>
   <td>Anteprima HTML e anteprima HTML con dati</td>
  </tr>
  <tr>
   <td>Modello di modulo</td>
   <td>Anteprima PDF, anteprima PDF con dati, anteprima HTML, anteprima HTML con dati<br /> </td>
  </tr>
 </tbody>
</table>

## Anteprima di un modulo {#previewing-a-form-1}

1. Seleziona una risorsa da visualizzare in anteprima e fai clic su Anteprima ![aem6forms_preview](assets/aem6forms_preview.png) nella barra degli strumenti azioni.

   >[!NOTE]
   >
   >Per selezionare una risorsa, passa alla vista Elenco dalla vista Scheda predefinita. Fai clic su ![aem6forms_viewlist](assets/aem6forms_viewlist.png) o ![aem6forms_viewcard](assets/aem6forms_viewcard.png) per cambiare visualizzazione.

1. Facendo clic su Anteprima sono elencate le opzioni di anteprima applicabili al tipo di risorsa selezionato. Fai clic sull’opzione desiderata per eseguire il rendering della risorsa selezionata in una nuova scheda.

   Le opzioni disponibili sono:

   * Anteprima come HTML
   * Anteprima con i dati
   * Anteprima come PDF (disponibile per i modelli di modulo)

## Anteprima con i dati {#preview-with-data}

Quando selezioni **Anteprima con dati**, è possibile visualizzare l’aspetto del modulo con i dati reali immessi al suo interno. L’opzione Anteprima con dati consente di caricare un file XML contenente dati utente di esempio. I dati utente di esempio vengono utilizzati per compilare il modulo di anteprima nel formato scelto.

1. Seleziona una risorsa e fai clic su Anteprima ![aem6forms_preview](assets/aem6forms_preview.png), quindi seleziona **Anteprima con dati**.
1. Nella finestra di dialogo Anteprima modulo, specificare FormData come file XML. Fare clic su Anteprima per eseguire il rendering del modulo con i dati uniti da XML.
