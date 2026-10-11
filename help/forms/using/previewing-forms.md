---
title: Anteprima di un modulo
description: Puoi visualizzare in anteprima i moduli prima di pubblicarli o attivarli per assicurarti che soddisfino le aspettative. Le opzioni di anteprima possono variare tra i tipi di modulo supportati.
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 377d804d-4a75-4c93-8125-d2660cf56418
feature: Adaptive Forms,Foundation Components
exl-id: aed5703e-4fe6-4839-9657-c660ac48521e
solution: Experience Manager, Experience Manager Forms
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 7da902b6-fe94-5180-8e7c-f6d1e38d01d5
    internal-label: Foundation Components
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '417'
ht-degree: 9%
---
# Anteprima di un modulo {#previewing-a-form}

<span class="preview"> Adobe consiglia di utilizzare l&#39;acquisizione dati moderna ed estensibile [Componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=it) per [la creazione di un nuovo Forms adattivo](/help/forms/using/create-an-adaptive-form-core-components.md) o [l&#39;aggiunta di Forms adattivo alle pagine AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Questi componenti rappresentano un progresso significativo nella creazione di Forms adattivi, garantendo esperienze utente straordinarie. Questo articolo descrive un approccio precedente all’authoring di Forms adattivi utilizzando i componenti di base. </span>

## Panoramica {#overview}

In AEM Forms puoi visualizzare in anteprima i moduli e i documenti presenti nell’archivio. L&#39;anteprima consente di conoscere esattamente l&#39;aspetto e il comportamento dei moduli quando vengono rilasciati agli utenti finali.

Quando si visualizza l’anteprima dei moduli, questi vengono riprodotti in un’interfaccia interattiva e l’utente può riempirli di dati. Quando si visualizza l’anteprima di un documento, questo viene riprodotto in modalità non interattiva e l’utente può solo visualizzarlo. Per i moduli è disponibile un’ulteriore opzione di Anteprima personalizzata. Questa opzione consente di visualizzare in anteprima il modulo utilizzando i dati di un file XML. I dati riempiono alcuni o tutti i campi del modulo visualizzato in anteprima.

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
   <td>Anteprima HTML e Anteprima HTML con dati</td>
  </tr>
  <tr>
   <td>Modello per moduli</td>
   <td>Anteprima PDF, Anteprima PDF con dati, Anteprima HTML, Anteprima HTML con dati<br /> </td>
  </tr>
 </tbody>
</table>

## Anteprima di un modulo {#previewing-a-form-1}

1. Seleziona una risorsa da visualizzare in anteprima e fai clic su Anteprima ![aem6forms_preview](assets/aem6forms_preview.png) nella barra degli strumenti delle azioni.

   >[!NOTE]
   >
   >Per selezionare una risorsa, passa alla vista a elenco dalla vista a schede predefinita. Fai clic su ![aem6forms_viewlist](assets/aem6forms_viewlist.png) o ![aem6forms_viewcard](assets/aem6forms_viewcard.png) per cambiare visualizzazione.

1. Facendo clic su Anteprima vengono elencate le possibili opzioni di anteprima applicabili al tipo di risorsa selezionato. Fai clic sull’opzione desiderata per eseguire il rendering della risorsa selezionata in una nuova scheda.

   Le opzioni disponibili sono:

   * Anteprima come HTML
   * Anteprima con i dati
   * Anteprima come PDF (disponibile per i modelli di modulo)

## Anteprima con i dati {#preview-with-data}

Quando si seleziona **Anteprima con dati**, è possibile visualizzare l&#39;aspetto del modulo con i dati effettivi immessi. L’opzione Anteprima con dati consente di caricare un XML che contiene dati utente di esempio. I dati utente di esempio vengono utilizzati per compilare il modulo di anteprima nel formato scelto.

1. Seleziona una risorsa, fai clic su Anteprima ![aem6forms_preview](assets/aem6forms_preview.png) e seleziona **Anteprima con dati**.
1. Nella finestra di dialogo Anteprima modulo, specificare FormData come file XML. Fare clic su Anteprima per eseguire il rendering del modulo con i dati uniti da XML.
