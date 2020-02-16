---
title: Esportazione di frammenti esperienza in Adobe Target
seo-title: Esportazione di frammenti esperienza in Adobe Target
description: Esportazione di frammenti esperienza in Adobe Target
seo-description: Esportazione di frammenti esperienza in Adobe Target
uuid: 2df0faab-5d5e-4fc1-93b3-28b7e6f3c306
contentOwner: carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: d4152b4d-531b-4b62-8807-a5bc5afe94c6
docset: aem65
translation-type: tm+mt
source-git-commit: 6723b12bebba2f239c0886e5f378f1dc70e5e247

---


# Esportazione di frammenti esperienza in Adobe Target{#exporting-experience-fragments-to-adobe-target}

>[!CAUTION]
>
>Alcune funzionalità presenti in questa pagina richiedono l’applicazione di AEM 6.5.3.0.
>
>6.5.3.0
>
>* **È ora possibile selezionare Domini** di esternalizzatore.
>
>
6.5.2.0:
>
>* I frammenti esperienza possono essere esportati in:
   >   * l&#39;area di lavoro predefinita.
   >   * un&#39;area di lavoro denominata, specificata in Configurazione cloud.
>* AEM deve essere [integrato con Adobe Target tramite Adobe I/O](/help/sites-administering/integration-ims-adobe-io.md).
>
>
AEM 6.5.0.0 e 6.5.1.0:
>
>* I frammenti esperienza AEM vengono esportati nell&#39;area di lavoro predefinita di Adobe Target.
>* AEM deve essere integrato con Adobe Target in base alle istruzioni in [Integrazione con Adobe Target](/help/sites-administering/target.md).


Puoi esportare frammenti [](/help/sites-authoring/experience-fragments.md)esperienza creati in Adobe Experience Manager (AEM) in Adobe Target (Target). Possono quindi essere utilizzati come offerte nelle attività Target, per sottoporre a test e personalizzare le esperienze su scala.

Per esportare un frammento esperienza in Adobe Target sono disponibili tre opzioni di formato:

* HTML (predefinito): Supporto per la distribuzione di contenuti Web e ibridi
* JSON: Supporto per la distribuzione headless dei contenuti
* HTML e JSON

I frammenti esperienza AEM possono essere esportati nell&#39;area di lavoro predefinita in Adobe Target, o in aree di lavoro definite dall&#39;utente per Adobe Target. Questo avviene tramite Adobe I/O, per il quale AEM deve essere [integrato con Adobe Target tramite Adobe I/O](/help/sites-administering/integration-ims-adobe-io.md).

>[!NOTE]
>
>Le aree di lavoro di Adobe Target non esistono proprio in Adobe Target. Vengono definiti e gestiti in Adobe IMS (Identity Management System), quindi selezionati per l&#39;utilizzo tra le soluzioni tramite integrazioni di I/O Adobe.

>[!NOTE]
>
>Le aree di lavoro di Adobe Target possono essere utilizzate per consentire ai membri di un&#39;organizzazione (gruppo) di creare e gestire offerte e attività solo per questa organizzazione; senza dare accesso ad altri utenti. Ad esempio, organizzazioni specifiche per paese all&#39;interno di una preoccupazione globale.

>[!NOTE]
>
>Per ulteriori informazioni, consulta anche:
>
>* [Sviluppo di Adobe Target](https://www.adobe.io/apis/experiencecloud/target.html)
>* [Componenti di base - Frammenti esperienza](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/experience-fragment.html)
>



## Prerequisiti {#prerequisites}

>[!CAUTION]
>
>Alcune funzionalità presenti in questa pagina richiedono l’applicazione di AEM 6.5.3.0.

Sono necessarie diverse azioni:

1. Devi [integrare AEM con Adobe Target utilizzando Adobe I/O](/help/sites-administering/integration-ims-adobe-io.md).
2. I frammenti esperienza vengono esportati dall’istanza di creazione di AEM, pertanto devi [configurare AEM Link Externalizer](/help/sites-administering/target-requirements.md#configuring-the-aem-link-externalizer) sull’istanza di creazione per garantire che eventuali riferimenti all’interno del frammento esperienza siano esternalizzati per la distribuzione Web.

   >[!NOTE]
   >
   >Per la riscrittura dei collegamenti non coperta dall’impostazione predefinita, è disponibile il provider [di riscrittura dei collegamenti dei frammenti](/help/sites-developing/experience-fragments.md#the-experience-fragment-link-rewriter-provider-html) esperienza. Con questo, è possibile sviluppare regole personalizzate per la vostra istanza.

## Aggiungi configurazione cloud {#add-the-cloud-configuration}

Prima di esportare un frammento è necessario aggiungere la configurazione **** Cloud per **Adobe Target** al frammento o alla cartella. Questo consente anche di:

* specificare le opzioni di formato da utilizzare per l&#39;esportazione
* selezionate un&#39;area di lavoro Target come destinazione
* selezionate un dominio esternalizzatore per riscrivere i riferimenti nel frammento esperienza (facoltativo)

Le opzioni richieste possono essere selezionate in Proprietà **** pagina della cartella e/o del frammento richiesti; la specifica verrà ereditata in base alle esigenze.

1. Andate alla console **Frammenti** esperienza.

1. Aprire Proprietà **** pagina per la cartella o il frammento appropriato.

   >[!NOTE]
   >
   >Se aggiungi la configurazione cloud alla cartella padre del frammento esperienza, la configurazione viene ereditata da tutti gli elementi figlio.
   >
   >
   >Se aggiungi la configurazione cloud allo stesso frammento esperienza, la configurazione viene ereditata da tutte le varianti.

1. Selezionate la scheda Servizi **** cloud.

1. In Configurazione **servizio** Cloud, seleziona **Adobe Target** dall&#39;elenco a discesa.

1. 
   >[!NOTE]
   >
   >È possibile personalizzare il formato JSON di un&#39;offerta di frammenti esperienza. A tal fine, definite un componente Frammento esperienza cliente e annotatene le proprietà nel modello Sling del componente.
   >
   >Vedere il componente di base:
   >
   >[Componenti di base - Frammenti esperienza](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/experience-fragment.html)

   In **Adobe Target** selezionate:

   * la configurazione appropriata
   * l&#39;opzione di formato richiesta
   * un&#39;area di lavoro Adobe Target
   * se necessario - il dominio esternalizzatore
   >[!CAUTION]
   >
   >Il dominio esternalizzatore è facoltativo. Un esternalizzatore AEM è configurato quando desiderate che il contenuto esportato faccia riferimento a un dominio di *pubblicazione* specifico. Per ulteriori dettagli, consultate [Configurazione di AEM Link Externalizer](/help/sites-administering/target-requirements.md#configuring-the-aem-link-externalizer).

   Ad esempio, per una cartella:

   ![Cartella -](assets/xf-target-integration-01.png "Servizi cloud - Servizi cloud")

1. **Salva e chiudi**.

## Esportazione di un frammento esperienza in Adobe Target {#exporting-an-experience-fragment-to-adobe-target}

>[!CAUTION]
>
>Per le risorse multimediali, come le immagini, viene esportato solo un riferimento a Target. La risorsa stessa rimane memorizzata in Risorse AEM e viene distribuita dall’istanza di pubblicazione AEM.
>
>Per questo motivo, il frammento esperienza, con tutte le risorse correlate, deve essere pubblicato prima di esportare in Target.

Per esportare un frammento esperienza da AEM a Target (dopo aver specificato la configurazione cloud):

1. Passate alla console Frammenti esperienza.
1. Selezionate il frammento esperienza da esportare come destinazione.

   >[!NOTE]
   >
   >Deve essere una variante Web del frammento esperienza.

1. Toccate o fate clic su **Esporta in Adobe Target**.

   >[!NOTE]
   >
   >Se il frammento esperienza è già stato esportato, selezionate **Aggiorna in Adobe Target**.

1. Toccate/fate clic su **Esporta senza pubblicare** o **pubblicare** come necessario.

   >[!NOTE]
   >
   >Se selezionate **Pubblica** , il frammento esperienza viene subito pubblicato e inviato a Target.

1. Toccate o fate clic su **OK** nella finestra di dialogo di conferma.

   Il frammento esperienza deve ora essere in Target.

   >[!NOTE]
   >
   >[Vari dettagli](/help/sites-authoring/experience-fragments.md#details-of-your-experience-fragment) dell’esportazione sono disponibili nella vista **a** elenco della console e nelle **proprietà**.

   >[!NOTE]
   >
   >Quando si visualizza un frammento esperienza in Adobe Target, la data dell&#39; *ultima modifica* visualizzata è la data dell&#39;ultima modifica del frammento in AEM, non la data dell&#39;ultima esportazione del frammento in Adobe Target.

>[!NOTE]
>
>In alternativa, potete eseguire l’esportazione dall’editor pagina utilizzando comandi comparabili nel menu Informazioni [](/help/sites-authoring/author-environment-tools.md#page-information) pagina.

## Utilizzo dei frammenti esperienza in Adobe Target {#using-your-experience-fragments-in-adobe-target}

Dopo aver eseguito le attività precedenti, il frammento esperienza viene visualizzato nella pagina Offerte in Target. Consulta la documentazione [](https://experiencecloud.adobe.com/resources/help/en_US/target/target/aem-experience-fragments.html) specifica di Target per saperne di più sui risultati ottenuti.

>[!NOTE]
>
>Quando si visualizza un frammento esperienza in Adobe Target, la data dell&#39; *ultima modifica* visualizzata è la data dell&#39;ultima modifica del frammento in AEM, non la data dell&#39;ultima esportazione del frammento in Adobe Target.

## Eliminazione di un frammento esperienza già esportato in Adobe Target {#deleting-an-experience-fragment-already-exported-to-adobe-target}

L&#39;eliminazione di un frammento esperienza già esportato in Target potrebbe causare problemi se il frammento è già utilizzato in un&#39;offerta in Target. L’eliminazione del frammento renderebbe l’offerta inutilizzabile mentre il contenuto del frammento viene distribuito da AEM.

Per evitare tali situazioni:

* Se il frammento esperienza non è attualmente utilizzato in un&#39;attività, AEM consente all&#39;utente di eliminare il frammento senza ricevere un messaggio di avviso.
* Se il frammento esperienza è attualmente utilizzato da un&#39;attività in Target, un messaggio di errore avvisa l&#39;utente AEM delle possibili conseguenze che l&#39;eliminazione del frammento avrà sull&#39;attività.

   Il messaggio di errore in AEM non impedisce all’utente di (forzare-)eliminare il frammento esperienza. Se il frammento esperienza viene eliminato:

   * L&#39;offerta Target con il frammento esperienza AEM può mostrare un comportamento indesiderato

      * Il rendering dell&#39;offerta continuerà probabilmente, in quanto l&#39;HTML del frammento esperienza è stato inviato a Target
      * Eventuali riferimenti nel frammento esperienza potrebbero non funzionare correttamente se anche le risorse di riferimento venivano eliminate in AEM.
   * Ovviamente, non è possibile apportare ulteriori modifiche al frammento esperienza, in quanto il frammento esperienza non esiste più in AEM.