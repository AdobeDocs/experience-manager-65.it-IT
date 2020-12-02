---
title: Integrazione con  Adobe Target tramite  Adobe I/O
seo-title: Integrazione con  Adobe Target tramite  Adobe I/O
description: Scopri come integrare AEM con  Adobe Target utilizzando  Adobe I/O
seo-description: Scopri come integrare AEM con  Adobe Target utilizzando  Adobe I/O
uuid: dd4ed638-e182-4d7e-9c98-282431812467
contentOwner: aheimoz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: integration
discoiquuid: 3b9285db-8fba-4d12-8f52-41daa50a5403
docset: aem65
translation-type: tm+mt
source-git-commit: 26efba567985dcb89b2610935cab18943b7034b3
workflow-type: tm+mt
source-wordcount: '1335'
ht-degree: 1%

---


# Integrazione con  Adobe Target utilizzando  Adobe I/O{#integration-with-adobe-target-using-adobe-i-o}

L&#39;integrazione di AEM con  Adobe Target tramite l&#39;API di Target Standard richiede la configurazione di  Adobe IMS ( Identity Management System) e  Adobe I/O.

>[!NOTE]
>
>Il supporto per  Adobe Target Standard API è stato introdotto nella AEM 6.5. L&#39;API di Target Standard utilizza l&#39;autenticazione IMS.
>
>L&#39;utilizzo dell&#39;API Adobe Target Classic  in AEM è ancora supportato per la compatibilità con le versioni precedenti. L&#39; [API di Target Classic utilizza l&#39;autenticazione delle credenziali utente](/help/sites-administering/target-configuring.md#manually-integrating-with-adobe-target).
>
>La selezione API è guidata dal metodo di autenticazione utilizzato per l&#39;integrazione AEM/Target.

## Prerequisiti {#prerequisites}

Prima di avviare la procedura:

* [ Adobe ](https://helpx.adobe.com/it/contact/enterprise-support.ec.html) Support deve fornire il proprio account per:

   * Console Adobe 
   *  Adobe I/O
   *  Adobe Target e
   *  Adobe IMS ( Identity Management System)

* L&#39;amministratore di sistema della tua organizzazione deve utilizzare il Admin Console  per aggiungere gli sviluppatori richiesti nella tua organizzazione ai profili di prodotto pertinenti.

   * Questo fornisce agli sviluppatori specifici le autorizzazioni per abilitare le integrazioni all&#39;interno  Adobe I/O.
   * Per ulteriori dettagli, vedere [Gestione degli sviluppatori](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/manage-developers.ug.html).


## Configurazione di una configurazione IMS - Generazione di una chiave pubblica {#configuring-an-ims-configuration-generating-a-public-key}

La prima fase della configurazione consiste nel creare una configurazione IMS in AEM e generare la chiave pubblica.

1. AEM aprire il menu **Strumenti**.
1. Nella sezione **Sicurezza** selezionare **Configurazioni IMS  Adobe**.
1. Selezionare **Crea** per aprire il **Adobe IMS Technical Account Configuration**.
1. Nell&#39;elenco a discesa in **Configurazione cloud**, selezionare **Adobe Target**.
1. Attivate **Create un nuovo certificato** e immettete un nuovo alias.
1. Confermare con **Crea certificato**.

   ![](assets/integrate-target-io-01.png)

1. Selezionare **Scarica** (o **Scarica chiave pubblica**) per scaricare il file nell&#39;unità locale, in modo che sia pronto per essere utilizzato quando si configura  Adobe I/O per &#39;integrazione Adobe Target con AEM](#configuring-adobe-i-o-for-adobe-target-integration-with-aem).[

   >[!CAUTION]
   >
   >Tenere aperta questa configurazione, sarà necessario di nuovo quando [Completamento della configurazione IMS in AEM](#completing-the-ims-configuration-in-aem).

   ![](assets/integrate-target-io-02.png)

## Configurazione  Adobe I/O per  integrazione Adobe Target con AEM {#configuring-adobe-i-o-for-adobe-target-integration-with-aem}

È necessario creare il progetto Adobe I/O  (integrazione) con  Adobe Target che AEM utilizzare, quindi assegnare i privilegi richiesti.

### Creazione del progetto {#creating-the-project}

Aprite la console  Adobe I/O per creare un progetto I/O con  Adobe Target che AEM utilizzare:

>[!NOTE]
>
>Vedere anche le [ esercitazioni Adobe I/O](https://www.adobe.io/apis/experienceplatform/home/tutorials/alltutorials.html).

1. Aprite la  console Adobe I/O per Progetti:

   [https://console.adobe.io/projects](https://console.adobe.io/projects)

1. Vengono visualizzati tutti i progetti che avete. Selezionare **Crea nuovo progetto**: la posizione e l&#39;utilizzo dipenderanno da:

   * Se non hai ancora un progetto, **Crea nuovo progetto** sarà al centro, in basso.
      ![Crea nuovo progetto - Primo progetto](assets/integration-target-io-02.png)
   * Se hai già dei progetti esistenti, questi saranno elencati e **Crea nuovo progetto** sarà in alto a destra.
      ![Crea nuovo progetto - Più progetti](assets/integration-target-io-03.png)


1. Selezionare **Aggiungi a progetto** seguito da **API**:

   ![](assets/integration-target-io-10.png)

1. Selezionare **Adobe Target**, quindi **Next**:

   >[!NOTE]
   >
   >Se si è iscritti  Adobe Target, ma non lo si vede nell&#39;elenco, è necessario controllare i [Prequistes](#prerequisites).

   ![](assets/integration-target-io-12.png)

1. **Carica la tua chiave** pubblica e, al termine, continua con  **Avanti**:

   ![](assets/integration-target-io-13.png)

1. Rivedete le credenziali e continuate con **Next**:

   ![](assets/integration-target-io-15.png)

1. Selezionate i profili di prodotto richiesti e continuate con **Salva API configurata**:

   >[!NOTE]
   >
   >I profili di prodotto visualizzati dipendono dal fatto che:
   >
   >*  Adobe Target Standard - è disponibile solo **Area di lavoro predefinita**
   >*  Adobe Target Premium: vengono elencate tutte le aree di lavoro disponibili, come mostrato di seguito


   ![](assets/integration-target-io-16.png)

1. La creazione verrà confermata.

<!--
1. The creation will be confirmed, you can now **Continue to integration details**; these are needed for [Completing the IMS Configuration in AEM](#completing-the-ims-configuration-in-aem).

   ![](assets/integrate-target-io-07.png)
-->

### Assegnazione di privilegi all&#39;integrazione {#assigning-privileges-to-the-integration}

È ora necessario assegnare i privilegi richiesti all&#39;integrazione:

1. Aprire l&#39;Adobe  **Admin Console**:

   * [https://adminconsole.adobe.com](https://adminconsole.adobe.com/)

1. Andate a **Products** (barra degli strumenti superiore), quindi selezionate **Adobe Target - &lt;*your-tenant-id*>** (dal pannello a sinistra).
1. Selezionare **Profili di prodotto**, quindi l&#39;area di lavoro desiderata dall&#39;elenco. Ad esempio, Area di lavoro predefinita.
1. Selezionare **Integrations**, quindi la configurazione di integrazione richiesta.
1. Selezionare **Editor** come **ruolo prodotto**; anziché **Observer**.

## Dettagli memorizzati per  progetto di integrazione Adobe I/O {#details-stored-for-the-adobe-io-integration-project}

Dalla  console Progetti Adobe I/O potete visualizzare un elenco di tutti i progetti di integrazione:

* [https://console.adobe.io/projects](https://console.adobe.io/projects)

Selezionare **Visualizza** (a destra di una voce specifica del progetto) per visualizzare ulteriori dettagli sulla configurazione. Comprendono:

* Panoramica del progetto
* Approfondimenti
* Credenziali
   * Account di servizio (JWT)
      * Dettagli credenziali
      * Genera JWT
* APIS
   * Ad esempio,  Adobe Target

Alcuni di questi sono necessari per completare l&#39;integrazione Adobe I/O  per Target in AEM.

## Completamento della configurazione IMS in AEM {#completing-the-ims-configuration-in-aem}

Per AEM potete completare la configurazione IMS aggiungendo i valori richiesti dall&#39;integrazione Adobe I/O  per Target:

1. Tornate alla [configurazione IMS aperta in AEM](#configuring-an-ims-configuration-generating-a-public-key).
1. Seleziona **Avanti**.

1. Qui è possibile utilizzare i [dettagli da  Adobe I/O](#details-stored-for-the-adobe-io-integration-project):

   * **Titolo**: Testo.
   * **Server** autorizzazioni: Copiare/incollare questo dalla  `"aud"` riga della sezione  **** Payloadsection seguente, ad esempio  `"https://ims-na1.adobelogin.com"` nell&#39;esempio seguente
   * **Chiave** API: Copiatela dalla sezione  [](#details-stored-for-the-adobe-io-integration-project) Panoramica dell&#39;integrazione Adobe I/O  per Target
   * **Segreto** cliente: Generate questo nella sezione  [](#details-stored-for-the-adobe-io-integration-project) Panoramica dell&#39;integrazione Adobe I/O  per Target, e copiate
   * **Payload**: Copiatela dalla  [sezione ](#details-stored-for-the-adobe-io-integration-project) Genera JWT dell&#39;integrazione Adobe I/O  per Target

   ![](assets/integrate-target-io-10.png)

1. Confermare con **Create**.

1. La configurazione  Adobe Target verrà visualizzata nella console AEM.

   ![](assets/integrate-target-io-11.png)

## Conferma della configurazione IMS {#confirming-the-ims-configuration}

Per confermare che la configurazione funziona come previsto:

1. Apri:

   * `https://localhost<port>/libs/cq/adobeims-configuration/content/configurations.html`

   Esempio:

   * `https://localhost:4502/libs/cq/adobeims-configuration/content/configurations.html`


1. Selezionate la configurazione.
1. Selezionare **Controlla stato** dalla barra degli strumenti, seguita da **Controlla**.

   ![](assets/integrate-target-io-12.png)

1. In caso di esito positivo, verrà visualizzato il messaggio:

   ![](assets/integrate-target-io-13.png)

## Configurazione del Cloud Service Adobe Target  {#configuring-the-adobe-target-cloud-service}

Ora è possibile fare riferimento alla configurazione per un Cloud Service per utilizzare l&#39;API di Target Standard:

1. Aprire il menu **Strumenti**. Quindi, nella sezione **Cloud Services**, selezionare **Cloud Services precedenti**.
1. Scorri verso il basso fino a **Adobe Target** e seleziona **Configura ora**.

   Viene aperta la finestra di dialogo **Crea configurazione**.

1. Immettere un **Titolo** e, se lo si desidera, un **Nome** (se lasciato vuoto, questo verrà generato dal titolo).

   Potete anche selezionare il modello richiesto (se sono disponibili più modelli).

1. Confermare con **Create**.

   Viene aperta la finestra di dialogo **Modifica componente**.

1. Immettere i dettagli nella scheda **Adobe Target Settings**:

   * **Autenticazione**: IMS
   * **ID** tenant: l&#39;ID tenant IMS del Adobe

      >[!NOTE]
      >
      >Per IMS questo valore deve essere recuperato direttamente da Target. Potete accedere a Target ed estrarre l&#39;ID tenant dall&#39;URL.
      >
      >Ad esempio, se l’URL è:
      >
      >`https://experience.adobe.com/#/@yourtenantid/target/activities`
      >
      >Quindi si utilizza `yourtenantid`.

   * **Configurazione** IMS: selezionate il nome della configurazione IMS
   * **Tipo** API: REST
   * **Configurazione** A4T  Analytics Cloud: Seleziona la configurazione cloud di Analytics utilizzata per gli obiettivi e le metriche dell&#39;attività di destinazione. Questo è necessario se utilizzate  Adobe Analytics come origine di reporting quando eseguite il targeting del contenuto. Se non visualizzate la configurazione cloud, consultate la nota in [Configurazione A4T  configurazione Analytics Cloud](/help/sites-administering/target-configuring.md#configuring-a-t-analytics-cloud-configuration).
   * **Utilizzate targeting** accurato: Per impostazione predefinita questa casella di controllo è selezionata. Se selezionata, la configurazione del servizio cloud attende il caricamento del contesto prima di caricare il contenuto. Vedere la nota che segue.
   * **Sincronizzare i segmenti da  Adobe Target**: Selezionate questa opzione per scaricare i segmenti definiti in Target per utilizzarli in AEM. Devi selezionare questa opzione quando la proprietà Tipo API è REST, perché i segmenti in linea non sono supportati e devi sempre utilizzare i segmenti da Target. Il termine AEM &quot;segmento&quot; è equivalente al termine &quot;audience&quot; di Target.
   * **Libreria** client: Selezionate se la libreria client AT.js deve essere obsoleta oppure mbox.js.
   * **Utilizzate Tag Management System per distribuire la libreria** client: Usa DTM (obsoleto), Lancio  Adobe o qualsiasi altro sistema di gestione tag.
   * **AT.js** personalizzato: Lasciate vuoto se avete selezionato la casella Gestione tag o per utilizzare il file AT.js predefinito. In alternativa, caricate il vostro AT.js personalizzato. Viene visualizzato solo se avete selezionato AT.js.

   >[!NOTE]
   >
   >[La configurazione di un Cloud Service per l&#39;utilizzo dell&#39;](/help/sites-administering/target-configuring.md#manually-integrating-with-adobe-target) API di Target Classic è obsoleta (utilizza la scheda  Impostazioni Adobe Recommendations).

   Esempio:

   ![](assets/integrate-target-io-14.png)

1. Fate clic su **Connetti a Target** per inizializzare la connessione con  Adobe Target.

   Se la connessione ha esito positivo, viene visualizzato il messaggio **Connessione riuscita**.

1. Selezionare **OK** sul messaggio, seguito da **OK** nella finestra di dialogo per confermare la configurazione.
1. Ora potete procedere all&#39;aggiunta di [un framework di Target](/help/sites-administering/target-configuring.md#adding-a-target-framework) per configurare i parametri ContextHub o di ClientContext che verranno inviati a Target. Questo potrebbe non essere necessario per esportare AEM frammenti esperienza in Target.

