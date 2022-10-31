---
title: Esportazione di frammenti di esperienza in Adobe Target
seo-title: Exporting Experience Fragments to Adobe Target
description: Esportazione di frammenti di esperienza in Adobe Target
seo-description: Exporting Experience Fragments to Adobe Target
uuid: 2df0faab-5d5e-4fc1-93b3-28b7e6f3c306
contentOwner: carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: d4152b4d-531b-4b62-8807-a5bc5afe94c6
docset: aem65
exl-id: f2921349-de8f-4bc1-afa2-aeace99cfc5c
source-git-commit: a5f3e33a6abe7ac1bbd610a8528fd599d1ffd2aa
workflow-type: tm+mt
source-wordcount: '1220'
ht-degree: 81%

---

# Esportazione di frammenti di esperienza in Adobe Target{#exporting-experience-fragments-to-adobe-target}

>[!CAUTION]
>
>Alcune funzionalità in questa pagina richiedono l’applicazione di AEM 6.5.3.0 (o versioni successive).
>
>6.5.3.0:
>
>* **Domini esternalizzatori** ora può essere selezionato.
   >  **Nota:** I domini esternalizzatori sono rilevanti solo per il contenuto del frammento esperienza inviato a Target e non per metadati come Visualizza contenuto offerta.
>
>6.5.2.0:
>
>* I frammenti esperienza possono essere esportati in:
   >
   >   * l&#39;area di lavoro predefinita.
   >   * un’area di lavoro denominata, specificata nella configurazione cloud.
   >   * **Nota:** L&#39;esportazione in aree di lavoro specifiche richiede Adobe Target Premium.
>
>* AEM [integrato con Adobe Target tramite IMS](/help/sites-administering/integration-target-ims.md).
>
>AEM 6.5.0.0 e 6.5.1.0:
>
>* I Frammenti di esperienza AEM vengono esportati nell’area di lavoro predefinita di Adobe Target.
>* AEM deve essere integrato con Adobe Target secondo le istruzioni contenute in [Integrazione con Adobe Target](/help/sites-administering/target.md).


Puoi esportare [Frammenti esperienza](/help/sites-authoring/experience-fragments.md), creato in Adobe Experience Manager (AEM), in Adobe Target (Target). Puoi quindi utilizzarli come offerte nelle attività di Target, per testare e personalizzare le esperienze su larga scala.

Sono disponibili tre opzioni di formato per esportare un frammento esperienza in Adobe Target:

* HTML (predefinito): supporto per la distribuzione di contenuti web e ibridi
* JSON: supporto per la distribuzione di contenuti headless
* HTML e JSON

AEM Frammenti esperienza possono essere esportati nell’area di lavoro predefinita in Adobe Target o in aree di lavoro definite dall’utente per Adobe Target. Questa operazione viene eseguita utilizzando la console Adobe Developer, per la quale AEM [integrato con Adobe Target tramite IMS](/help/sites-administering/integration-target-ims.md).

>[!NOTE]
>
>Le aree di lavoro di Adobe Target non sono già esistenti in Adobe Target. Vengono definiti e gestiti in Adobe IMS (Identity Management System), quindi selezionati per l’utilizzo tra le soluzioni tramite integrazioni dalla console Adobe Developer.

>[!NOTE]
>
>Le aree di lavoro di Adobe Target possono essere utilizzate per consentire ai membri di un’organizzazione (gruppo) di creare e gestire offerte e attività riservate all’organizzazione; senza dare accesso ad altri utenti. Ad esempio, organizzazioni specifiche per paese nell&#39;ambito di un’azienda globale.

>[!NOTE]
>
>Per ulteriori informazioni, consulta:
>
>* [Sviluppo Adobe Target](https://www.adobe.io/apis/experiencecloud/target.html)
>* [Componenti core: Frammenti di esperienza](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/experience-fragment.html)
>


## Prerequisiti {#prerequisites}

>[!CAUTION]
>
>Alcune funzionalità in questa pagina richiedono l’applicazione di AEM 6.5.3.0.

Sono necessarie diverse azioni:

1. Devi [integrare AEM con Adobe Target utilizzando IMS](/help/sites-administering/integration-target-ims.md).
2. I Frammenti di esperienza vengono esportati dall’istanza di authoring AEM, per cui devi [Configurare AEM Link Externalizer](/help/sites-administering/target-requirements.md#configuring-the-aem-link-externalizer) nell’istanza di authoring, per garantire che tutti i riferimenti all’interno del Frammento di esperienza siano esternalizzati per la distribuzione web.

   >[!NOTE]
   >
   >Per la riscrittura di collegamenti non coperti dall’impostazione predefinita, è disponibile il [provider del rewriter di collegamento di Frammento esperienza](/help/sites-developing/experience-fragments.md#the-experience-fragment-link-rewriter-provider-html). Con questo, è possibile sviluppare regole personalizzate per la tua istanza.

## Aggiungere la configurazione cloud {#add-the-cloud-configuration}

Prima di esportare un frammento è necessario aggiungere la **Configurazione cloud** di **Adobe Target** al frammento o alla cartella. Questo consente anche di:

* specificare le opzioni di formato da utilizzare per l’esportazione
* selezionare un’area di lavoro di Target come destinazione
* selezionare un dominio esternalizzatore per riscrivere i riferimenti nel Frammento di esperienza (facoltativo)

Le opzioni richieste possono essere selezionate in **Proprietà pagina** della cartella e/o del frammento richiesti; la specifica viene ereditata in base alle necessità.

1. Passa alla console **Frammenti di esperienza**.

1. Apri **Proprietà pagina** per la cartella o il frammento appropriato.

   >[!NOTE]
   >
   >Se aggiungi la configurazione cloud alla cartella principale Frammento di esperienza, questa viene ereditata da tutti gli elementi secondari.
   >
   >
   >Se aggiungi la configurazione cloud al Frammento di esperienza stesso, questa viene ereditata da tutte le varianti.

1. Seleziona la scheda **Servizi cloud**.

1. Sotto **Configurazione servizio cloud**, seleziona **Adobe Target** dall’elenco a discesa.

   >[!NOTE]
   >
   >È possibile personalizzare il formato JSON di un’offerta Frammento di esperienza. A questo scopo, definisci un componente Frammento di esperienza cliente e poi annota come esportare le sue proprietà nel modello Sling del componente.
   >
   >Consulta il componente core :
   >
   >[Componenti core: Frammenti di esperienza](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/experience-fragment.html)

   Sotto **Adobe Target** seleziona:

   * la configurazione appropriata
   * l’opzione di formato richiesta
   * un’area di lavoro Adobe Target
   * se necessario, il dominio esternalizzatore

   >[!CAUTION]
   >
   >Il dominio esternalizzatore è facoltativo.
   >
   >Un esternalizzatore AEM è configurato quando desideri che il contenuto esportato punti a uno specifico dominio di *pubblicazione*. Per ulteriori dettagli vedi [Configurazione di AEM Link Externalizer](/help/sites-administering/target-requirements.md#configuring-the-aem-link-externalizer).
   >
   >Inoltre, i domini esternalizzatori sono rilevanti solo per il contenuto del Frammento di esperienza inviato a Target, e non per i metadati come Visualizza contenuto offerta.

   Ad esempio, per una cartella:

   ![Cartella - Servizi cloud](assets/xf-target-integration-01.png "Cartella - Servizi cloud")

1. **Salva e chiudi**.

## Esportazione di un frammento di esperienza in Adobe Target {#exporting-an-experience-fragment-to-adobe-target}

>[!CAUTION]
>
>Per le risorse multimediali, come le immagini, viene esportato solo un riferimento in Target. La risorsa stessa rimane memorizzata in AEM Assets e viene distribuita dall’istanza di pubblicazione AEM.
>
>Per questo motivo è necessario pubblicare il frammento di esperienza con tutte le relative risorse prima di esportarlo in Target.

Per esportare un frammento di esperienza da AEM a Target (dopo aver specificato la configurazione cloud):

1. Passa alla console Frammenti di esperienza.
1. Seleziona il frammento di esperienza da esportare in Target.

   >[!NOTE]
   >
   >Deve essere una variante Web del frammento di esperienza.

1. Tocca o fai clic su **Esporta in Adobe Target**.

   >[!NOTE]
   >
   >Se il frammento di esperienza è già stato esportato, seleziona **Aggiorna in Adobe Target**.

1. Tocca o fai clic su **Esporta senza pubblicare** o **Pubblica** se necessario.

   >[!NOTE]
   >
   >Selezionando **Pubblica** pubblicherà immediatamente il frammento di esperienza e lo invierà in Target.

1. Nella finestra di conferma tocca o fai clic su **OK**.

   Il frammento di esperienza deve ora essere in Target.

   >[!NOTE]
   >
   >[Vari dettagli](/help/sites-authoring/experience-fragments.md#details-of-your-experience-fragment) dell&#39;esportazione sono visibili in **Vista a elenco** della console e **Proprietà**.

   >[!NOTE]
   >
   >Quando visualizzi un frammento di esperienza in Adobe Target, la data dell&#39;*ultima modifica* visualizzata è la data dell’ultima modifica apportata al frammento in AEM, non la data dell’ultima esportazione del frammento in Adobe Target.

>[!NOTE]
>
>In alternativa, è possibile eseguire l’esportazione dall’editor di pagine utilizzando comandi comparabili nel menu [Informazioni pagina](/help/sites-authoring/author-environment-tools.md#page-information).

## Utilizzo dei frammenti di esperienza in Adobe Target {#using-your-experience-fragments-in-adobe-target}

Dopo aver eseguito le attività precedenti, il frammento di esperienza viene visualizzato nella pagina Offerte di Target. Dai un&#39;occhiata alla [documentazione specifica di Target](https://experiencecloud.adobe.com/resources/help/it_IT/target/target/aem-experience-fragments.html) per scoprire cosa puoi ottenere.

>[!NOTE]
>
>Quando visualizzi un frammento di esperienza in Adobe Target, la data dell&#39;*ultima modifica* visualizzata è la data dell’ultima modifica apportata al frammento in AEM, non la data dell’ultima esportazione del frammento in Adobe Target.

## Eliminazione di un frammento di esperienza già esportato in Adobe Target {#deleting-an-experience-fragment-already-exported-to-adobe-target}

L’eliminazione di un frammento di esperienza già esportato in Target potrebbe causare problemi se il frammento è già utilizzato in un’offerta in Target. L’eliminazione del frammento renderebbe l’offerta inutilizzabile mentre il contenuto del frammento è distribuito da AEM.

Per evitare tali situazioni:

* Se il frammento di esperienza non è attualmente utilizzato in un’attività, AEM consente all’utente di eliminarlo senza un messaggio di avviso.
* Se il frammento di esperienza è attualmente utilizzato da un’attività in Target, un messaggio di errore avvisa l’utente AEM delle possibili conseguenze che l’eliminazione del frammento avrà sull’attività.

   Il messaggio di errore in AEM non impedisce all’utente di (forzare) eliminare il frammento di esperienza. Se il frammento di esperienza viene eliminato:

   * L’offerta Target con il frammento di esperienza AEM può mostrare un comportamento indesiderato

      * L&#39;offerta sarà probabilmente ancora visualizzata, poiché l&#39;HTML del frammento di esperienza è stato inviato su Target
      * Eventuali riferimenti nel frammento di esperienza potrebbero non funzionare correttamente se le risorse di riferimento sono state eliminate anche in AEM.
   * Naturalmente, eventuali ulteriori modifiche al frammento di esperienza sono impossibili in quanto questo non esiste più in AEM.
