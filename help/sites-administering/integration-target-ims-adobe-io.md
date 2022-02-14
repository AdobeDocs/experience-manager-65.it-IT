---
title: Integrazione con Adobe Target tramite Adobe I/O
seo-title: Integration with Adobe Target using Adobe I/O
description: Scopri come integrare AEM con Adobe Target utilizzando Adobe I/O
seo-description: Learn about integrating AEM with Adobe Target using Adobe I/O
uuid: dd4ed638-e182-4d7e-9c98-282431812467
contentOwner: aheimoz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: integration
discoiquuid: 3b9285db-8fba-4d12-8f52-41daa50a5403
docset: aem65
source-git-commit: e6f4f3cf31c39853b45450e0c925694fc45f7aec
workflow-type: tm+mt
source-wordcount: '1539'
ht-degree: 1%

---

# Integrazione con Adobe Target tramite Adobe I/O{#integration-with-adobe-target-using-adobe-i-o}

L’integrazione di AEM con Adobe Target tramite l’API di Target Standard richiede la configurazione di Adobe IMS (Identity Management System) e di Adobe I/O.

>[!NOTE]
>
>Il supporto per l’API Adobe Target Standard è stato introdotto nella AEM 6.5. L’API di Target Standard utilizza l’autenticazione IMS.
>
>L’utilizzo dell’API Adobe Target Classic in AEM è ancora supportato per la compatibilità con le versioni precedenti. La [L’API di Target Classic utilizza l’autenticazione delle credenziali utente](/help/sites-administering/target-configuring.md#manually-integrating-with-adobe-target).
>
>La selezione API è guidata dal metodo di autenticazione utilizzato per l’integrazione AEM/Target.
>Vedi anche [ID tenant e codice client](#tenant-client) sezione .

## Prerequisiti {#prerequisites}

Prima di avviare questa procedura:

* [Supporto Adobe](https://helpx.adobe.com/it/contact/enterprise-support.ec.html) deve effettuare il provisioning del tuo account per:

   * Console Adobe
   * Adobe I/O
   * Adobe Target e
   * Adobe IMS (sistema Identity Management)

* L’amministratore di sistema della tua organizzazione deve utilizzare l’Admin Console per aggiungere gli sviluppatori necessari nella tua organizzazione ai profili di prodotto pertinenti.

   * Questo fornisce agli sviluppatori specifici le autorizzazioni per abilitare le integrazioni all’interno di Adobe I/O.
   * Per maggiori dettagli vedi [Gestire gli sviluppatori](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/manage-developers.ug.html).


## Configurazione di una configurazione IMS - Generazione di una chiave pubblica {#configuring-an-ims-configuration-generating-a-public-key}

La prima fase della configurazione consiste nel creare una configurazione IMS in AEM e generare la chiave pubblica.

1. AEM aprire **Strumenti** menu.
1. In **Sicurezza** selezione della sezione **Configurazioni Adobe IMS**.
1. Seleziona **Crea** per aprire **Configurazione dell’account tecnico Adobe IMS**.
1. Utilizzo del menu a discesa in **Configurazione cloud**, seleziona **Adobe Target**.
1. Attiva **Crea nuovo certificato** e immettere un nuovo alias.
1. Conferma con **Crea certificato**.

   ![](assets/integrate-target-io-01.png)

1. Seleziona **Scarica** o **Scarica chiave pubblica**) per scaricare il file sull&#39;unità locale, in modo che sia pronto per l&#39;uso quando [configurazione di Adobe I/O per l’integrazione di Adobe Target con AEM](#configuring-adobe-i-o-for-adobe-target-integration-with-aem).

   >[!CAUTION]
   >
   >Tieni aperta questa configurazione, sarà necessaria di nuovo quando [Completamento della configurazione IMS in AEM](#completing-the-ims-configuration-in-aem).

   ![](assets/integrate-target-io-02.png)

## Configurazione di Adobe I/O per l’integrazione di Adobe Target con AEM {#configuring-adobe-i-o-for-adobe-target-integration-with-aem}

Devi creare il progetto di Adobe I/O (integrazione) con Adobe Target che AEM utilizzare, quindi assegnare i privilegi richiesti.

### Creazione del progetto {#creating-the-project}

Apri la console Adobe I/O per creare un progetto I/O con Adobe Target che AEM utilizzare:

>[!NOTE]
>
>Vedi anche [Esercitazioni di Adobe I/O](https://www.adobe.io/apis/experienceplatform/home/tutorials/alltutorials.html).

1. Apri la console Adobe I/O per Progetti :

   [https://console.adobe.io/projects](https://console.adobe.io/projects)

1. Verranno visualizzati tutti i progetti che hai. Seleziona **Crea nuovo progetto** - la posizione e l’utilizzo dipenderanno da:

   * Se non hai ancora un progetto, **Crea nuovo progetto** sarà al centro, in basso.
      ![Crea nuovo progetto - Primo progetto](assets/integration-target-io-02.png)
   * Se disponi già di progetti esistenti, questi verranno elencati e **Crea nuovo progetto** sarà in alto a destra.
      ![Crea nuovo progetto - Più progetti](assets/integration-target-io-03.png)


1. Seleziona **Aggiungi a progetto** seguito da **API**:

   ![](assets/integration-target-io-10.png)

1. Seleziona **Adobe Target**, quindi **Successivo**:

   >[!NOTE]
   >
   >Se sei abbonato a Adobe Target ma non lo vedi nell’elenco, controlla la [Prerequisiti](#prerequisites).

   ![](assets/integration-target-io-12.png)

1. **Carica la chiave pubblica** e, una volta completato, continua con **Successivo**:

   ![](assets/integration-target-io-13.png)

1. Rivedi le credenziali e continua con **Successivo**:

   ![](assets/integration-target-io-15.png)

1. Seleziona i profili di prodotto richiesti e continua con **Salva API configurata**:

   >[!NOTE]
   >
   >I profili di prodotto visualizzati con dipendono dall’esistenza o meno di:
   >
   >* Adobe Target Standard - Solo **Area di lavoro predefinita** è disponibile
   >* Adobe Target Premium : vengono elencate tutte le aree di lavoro disponibili, come illustrato di seguito


   ![](assets/integration-target-io-16.png)

1. La creazione verrà confermata.

<!--
1. The creation will be confirmed, you can now **Continue to integration details**; these are needed for [Completing the IMS Configuration in AEM](#completing-the-ims-configuration-in-aem).

   ![](assets/integrate-target-io-07.png)
-->

### Assegnazione di privilegi all&#39;integrazione {#assigning-privileges-to-the-integration}

Ora devi assegnare i privilegi richiesti all’integrazione:

1. Apri l’Adobe **Admin Console**:

   * [https://adminconsole.adobe.com](https://adminconsole.adobe.com/)

1. Passa a **Prodotti** (barra degli strumenti superiore), quindi seleziona **Adobe Target - &lt;*your-tenant-id*>** (dal pannello a sinistra).
1. Seleziona **Profili di prodotto**, quindi l’area di lavoro richiesta dall’elenco presentato. Ad esempio, Area di lavoro predefinita.
1. Seleziona **Credenziali API**, quindi la configurazione di integrazione richiesta.
1. Seleziona **Editor** come **Ruolo del prodotto**; anziché **Osservatore**.

## Dettagli memorizzati per il progetto di integrazione Adobe I/O {#details-stored-for-the-adobe-io-integration-project}

Dalla console Progetti di Adobe I/O è disponibile un elenco di tutti i progetti di integrazione:

* [https://console.adobe.io/projects](https://console.adobe.io/projects)

Seleziona **Visualizza** (a destra di una voce specifica del progetto) per visualizzare ulteriori dettagli sulla configurazione. Comprendono:

* Panoramica del progetto
* Approfondimenti
* Credenziali
   * Account di servizio (JWT)
      * Dettagli delle credenziali
      * Genera JWT
* API
   * Ad esempio, Adobe Target

Alcuni di questi sono necessari per completare l’integrazione di Adobe I/O per Target in AEM.

## Completamento della configurazione IMS in AEM {#completing-the-ims-configuration-in-aem}

Di nuovo AEM puoi completare la configurazione IMS aggiungendo i valori richiesti dall’integrazione Adobe I/O per Target:

1. Torna a [Configurazione IMS aperta in AEM](#configuring-an-ims-configuration-generating-a-public-key).
1. Seleziona **Avanti**.

1. Qui puoi utilizzare la [dettagli dell&#39;Adobe I/O](#details-stored-for-the-adobe-io-integration-project):

   * **Titolo**: Testo.
   * **Server autorizzazioni**: Copia/incolla questo da `aud` della linea **Payload** sezione seguente, ad esempio `https://ims-na1.adobelogin.com` nell&#39;esempio seguente
   * **Chiave API**: Copia questo da [Panoramica](#details-stored-for-the-adobe-io-integration-project) sezione dell’integrazione di Adobe I/O per Target
   * **Segreto client**: Genera questo in [Panoramica](#details-stored-for-the-adobe-io-integration-project) sezione dell’integrazione Adobe I/O per Target e copia
   * **Payload**: Copia questo da [Genera JWT](#details-stored-for-the-adobe-io-integration-project) sezione dell’integrazione di Adobe I/O per Target

   ![](assets/integrate-target-io-10.png)

1. Conferma con **Crea**.

1. La configurazione di Adobe Target verrà visualizzata nella console AEM.

   ![](assets/integrate-target-io-11.png)

## Conferma della configurazione IMS {#confirming-the-ims-configuration}

Per confermare che la configurazione funziona come previsto:

1. Apri:

   * `https://localhost<port>/libs/cq/adobeims-configuration/content/configurations.html`

   Esempio:

   * `https://localhost:4502/libs/cq/adobeims-configuration/content/configurations.html`


1. Seleziona la configurazione.
1. Seleziona **Verifica stato** dalla barra degli strumenti, seguita da **Controlla**.

   ![](assets/integrate-target-io-12.png)

1. In caso di esito positivo, verrà visualizzato il messaggio:

   ![](assets/integrate-target-io-13.png)

## Configurazione dell’Cloud Service Adobe Target {#configuring-the-adobe-target-cloud-service}

È ora possibile fare riferimento alla configurazione affinché un Cloud Service utilizzi l’API di Target Standard:

1. Apri **Strumenti** menu. Quindi, all&#39;interno del **Cloud Services** sezione , seleziona **Cloud Services legacy**.
1. Scorri verso il basso fino a **Adobe Target** e seleziona **Configura ora**.

   La **Crea configurazione** si aprirà la finestra di dialogo .

1. Inserisci un **Titolo** e, se volete, un **Nome** (se lasciato vuoto, verrà generato dal titolo).

   È inoltre possibile selezionare il modello richiesto (se sono disponibili più modelli).

1. Conferma con **Crea**.

   La **Modifica componente** si aprirà la finestra di dialogo .

1. Immetti i dettagli nella **Impostazioni di Adobe Target** scheda:

   * **Autenticazione**: IMS

   * **ID tenant**: l’ID tenant di Adobe IMS. Vedi anche [ID tenant e codice client](#tenant-client) sezione .

      >[!NOTE]
      >
      >Per IMS questo valore deve essere tratto da Target stesso. Puoi accedere a Target ed estrarre l’ID tenant dall’URL.
      >
      >Ad esempio, se l’URL è:
      >
      >`https://experience.adobe.com/#/@yourtenantid/target/activities`
      >
      >Poi userebbe `yourtenantid`.

   * **Codice client**: Consulta la sezione [ID tenant e codice client](#tenant-client) sezione .

   * **Configurazione IMS**: seleziona il nome della configurazione IMS

   * **Tipo di API**: REST

   * **Configurazione di A4T Analytics Cloud**: Seleziona la configurazione cloud di Analytics utilizzata per gli obiettivi e le metriche delle attività di destinazione. È necessario se utilizzi Adobe Analytics come origine per la generazione di rapporti durante il targeting del contenuto. Se la configurazione cloud non viene visualizzata, consulta la nota in [Configurazione della configurazione di A4T Analytics Cloud](/help/sites-administering/target-configuring.md#configuring-a-t-analytics-cloud-configuration).

   * **Utilizzare targeting accurato**: Per impostazione predefinita questa casella di controllo è selezionata. Se questa opzione è selezionata, la configurazione del servizio cloud attenderà il caricamento del contesto prima di caricare il contenuto. Vedi la nota che segue.

   * **Sincronizzare segmenti da Adobe Target**: Seleziona questa opzione per scaricare i segmenti definiti in Target e utilizzarli in AEM. Devi selezionare questa opzione quando la proprietà Tipo API è REST, perché i segmenti in linea non sono supportati e devi sempre utilizzare i segmenti da Target. Il termine AEM &quot;segmento&quot; è equivalente al &quot;pubblico&quot; di Target.

   * **Libreria client**: Seleziona se desideri la libreria client AT.js o mbox.js (obsoleto).

   * **Utilizza Tag Management System per distribuire la libreria client**: Utilizza DTM (obsoleto), Adobe Launch o qualsiasi altro sistema di gestione dei tag.

   * **AT.js personalizzato**: Lascia vuoto se hai selezionato la casella Gestione tag o per utilizzare il file AT.js predefinito. In alternativa, carica il tuo AT.js personalizzato. Viene visualizzato solo se è stato selezionato AT.js.
   >[!NOTE]
   >
   >[Configurazione di un Cloud Service per l’utilizzo dell’API di Target Classic](/help/sites-administering/target-configuring.md#manually-integrating-with-adobe-target) è stato dichiarato obsoleto (utilizza la scheda Impostazioni di Adobe Recommendations ).

1. Fai clic su **Connettersi a Target** per inizializzare la connessione con Adobe Target.

   Se la connessione ha esito positivo, viene visualizzato il messaggio **Connessione riuscita** viene visualizzato.

1. Seleziona **OK** sul messaggio, seguito da **OK** nella finestra di dialogo per confermare la configurazione.

1. Ora puoi procedere con [Aggiunta di un framework di Target](/help/sites-administering/target-configuring.md#adding-a-target-framework) per configurare i parametri ContextHub o di ClientContext che verranno inviati a Target. Questo potrebbe non essere necessario per esportare AEM frammenti esperienza in Target.

### ID tenant e codice client {#tenant-client}

Con [Adobe Experience Manager 6.5.8.0](/help/release-notes/release-notes.md), il campo Codice client è stato aggiunto alla finestra di configurazione di Target.

Durante la configurazione dei campi ID tenant e Codice client, tieni presente quanto segue:

1. Per la maggior parte dei clienti, l’ID tenant e il codice client sono gli stessi. Ciò significa che entrambi i campi contengono le stesse informazioni e sono identici. Assicurati di inserire l’ID tenant in entrambi i campi.
2. Per scopi precedenti, puoi anche immettere valori diversi nei campi ID tenant e Codice client .

In entrambi i casi, tieni presente che:

* Per impostazione predefinita, anche il codice client (se aggiunto per primo) viene copiato automaticamente nel campo ID tenant.
* Hai la possibilità di modificare il set di ID tenant predefinito.
* Di conseguenza, le chiamate di backend a Target saranno basate sull’ID tenant e le chiamate lato client a Target saranno basate sul codice client.

Come indicato in precedenza, il primo caso è il più comune per AEM 6.5. In entrambi i casi, assicurati **entrambi** i campi contengono le informazioni corrette a seconda dei requisiti.

>[!NOTE]
>
> Per modificare una configurazione di destinazione esistente:
>
> 1. Immetti nuovamente l&#39;ID tenant.
> 2. Riconnettersi a Target.
> 3. Salva la configurazione.

