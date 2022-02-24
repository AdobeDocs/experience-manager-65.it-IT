---
title: Integrazione con Adobe Analytics tramite Adobe I/O
description: Scopri come integrare AEM con Adobe Analytics utilizzando Adobe I/O
source-git-commit: c2c7c3f745a5f1edc1a8d2a73922f86f0b952ff7
workflow-type: tm+mt
source-wordcount: '1081'
ht-degree: 1%

---

# Integrazione con Adobe Analytics tramite Adobe I/O {#integration-with-adobe-analytics-using-adobe-i-o}

L’integrazione di AEM con Adobe Analytics tramite l’API di Analytics Standard richiede la configurazione di Adobe IMS (Identity Management System) e di un Adobe I/O.

>[!NOTE]
>
>Il supporto per l’API Adobe Analytics Standard 2.0 è una novità di AEM 6.5.12.0. Questa versione dell’API supporta l’autenticazione IMS.
>
>L’utilizzo dell’API Adobe Analytics Classic 1.4 in AEM è ancora supportato per la compatibilità con le versioni precedenti. La [L’API di Analytics Classic utilizza l’autenticazione delle credenziali utente](/help/sites-administering/adobeanalytics-connect.md).
>
>La selezione API è guidata dal metodo di autenticazione utilizzato per l’integrazione AEM/Analytics.
>
>Ulteriori informazioni sono disponibili al seguente indirizzo: [Migrazione alle API 2.0](https://developer.adobe.com/analytics-apis/docs/2.0/guides/migration/).

## Prerequisiti {#prerequisites}

Prima di avviare questa procedura:

* [Supporto Adobe](https://helpx.adobe.com/it/contact/enterprise-support.ec.html) deve effettuare il provisioning del tuo account per:

   * Console Adobe
   * Adobe I/O
   * Adobe Analytics e
   * Adobe IMS (sistema Identity Management)

* L’amministratore di sistema della tua organizzazione deve utilizzare l’Admin Console per aggiungere gli sviluppatori necessari nella tua organizzazione ai profili di prodotto pertinenti.

   * Questo fornisce agli sviluppatori specifici le autorizzazioni per abilitare le integrazioni all’interno di Adobe I/O.
   * Per maggiori dettagli vedi [Gestire gli sviluppatori](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/manage-developers.ug.html).


## Configurazione di una configurazione IMS - Generazione di una chiave pubblica {#configuring-an-ims-configuration-generating-a-public-key}

La prima fase della configurazione consiste nel creare una configurazione IMS in AEM e generare la chiave pubblica.

1. AEM aprire **Strumenti** menu.
1. In **Sicurezza** selezione della sezione **Configurazioni Adobe IMS**.
1. Seleziona **Crea** per aprire **Configurazione dell’account tecnico Adobe IMS**.
1. Utilizzo del menu a discesa in **Configurazione cloud**, seleziona **Adobe Analytics**.
1. Attiva **Crea nuovo certificato** e immettere un nuovo alias.
1. Conferma con **Crea certificato**.

   ![](assets/integrate-analytics-io-01.png)

1. Seleziona **Scarica** o **Scarica chiave pubblica**) per scaricare il file sull&#39;unità locale, in modo che sia pronto per l&#39;uso quando [configurazione di Adobe I/O per l’integrazione di Adobe Analytics con AEM](#configuring-adobe-i-o-for-adobe-analytics-integration-with-aem).

   >[!CAUTION]
   >
   >Tieni aperta questa configurazione, sarà necessaria di nuovo quando [Completamento della configurazione IMS in AEM](#completing-the-ims-configuration-in-aem).

   ![](assets/integrate-analytics-io-02.png)

## Configurazione di Adobe I/O per l’integrazione di Adobe Analytics con AEM {#configuring-adobe-i-o-for-adobe-analytics-integration-with-aem}

Devi creare il progetto di Adobe I/O (integrazione) con Adobe Analytics che AEM utilizzare, quindi assegnare i privilegi richiesti.

### Creazione del progetto {#creating-the-project}

Apri la console Adobe I/O per creare un progetto I/O con Adobe Target che AEM utilizzare:

<!--
>[!NOTE]
>
>See also the [Adobe I/O tutorials](https://www.adobe.io/apis/experienceplatform/home/tutorials/alltutorials.html).
-->

1. Apri la console Adobe I/O per Progetti :

   [https://console.adobe.io/projects](https://console.adobe.io/projects)

1. Verranno visualizzati tutti i progetti che hai. Seleziona **Crea nuovo progetto** - la posizione e l’utilizzo dipenderanno da:

   * Se non hai ancora un progetto, **Crea nuovo progetto** sarà al centro, in basso.
      ![Crea nuovo progetto - Primo progetto](assets/integration-analytics-io-02.png)
   * Se disponi già di progetti esistenti, questi verranno elencati e **Crea nuovo progetto** sarà in alto a destra.
      ![Crea nuovo progetto - Più progetti](assets/integration-analytics-io-03.png)


1. Seleziona **Aggiungi a progetto** seguito da **API**:

   ![Guida introduttiva al nuovo progetto](assets/integration-analytics-io-10.png)

1. Seleziona **Adobe Analytics**, quindi **Successivo**:

   >[!NOTE]
   >
   >Se sei abbonato a Adobe Analytics ma non lo vedi nell’elenco, controlla la [Prerequisiti](#prerequisites).

   ![Aggiungere un’API](assets/integration-analytics-io-12.png)

1. Seleziona **Account di servizio (JWT)** come tipo di autenticazione, quindi continua con **Successivo**:

   ![Selezionare il tipo di autenticazione](assets/integration-analytics-io-12a.png)

1. **Carica la chiave pubblica** e, una volta completato, continua con **Successivo**:

   ![Carica la chiave pubblica](assets/integration-analytics-io-13.png)

1. Rivedi le credenziali e continua con **Successivo**:

   ![Verificare le credenziali](assets/integration-analytics-io-15.png)

1. Seleziona i profili di prodotto richiesti e continua con **Salva API configurata**:

   >[!NOTE]
   >
   >I profili di prodotto visualizzati con dipendono dall’esistenza o meno di:
   >
   >* Adobe Target Standard - Solo **Area di lavoro predefinita** è disponibile
   >* Adobe Target Premium : vengono elencate tutte le aree di lavoro disponibili, come illustrato di seguito


   ![Selezionare i profili di prodotto richiesti](assets/integration-analytics-io-16.png)

1. La configurazione verrà confermata.

<!--
1. The creation will be confirmed, you can now **Continue to integration details**; these are needed for [Completing the IMS Configuration in AEM](#completing-the-ims-configuration-in-aem).

   ![](assets/integrate-target-io-07.png)
-->

### Assegnazione di privilegi all&#39;integrazione {#assigning-privileges-to-the-integration}

Ora devi assegnare i privilegi richiesti all’integrazione:

1. Apri l’Adobe **Admin Console**:

   * [https://adminconsole.adobe.com](https://adminconsole.adobe.com/)

1. Passa a **Prodotti** (barra degli strumenti superiore), quindi seleziona **Adobe Analytics - &lt;*your-tenant-id*>** (dal pannello a sinistra).
1. Seleziona **Profili di prodotto**, quindi l’area di lavoro richiesta dall’elenco presentato. Ad esempio, Area di lavoro predefinita.
1. Seleziona **Credenziali API**, quindi la configurazione di integrazione richiesta.
1. Seleziona **Editor** come **Ruolo del prodotto**; anziché **Osservatore**.

## Dettagli memorizzati per il progetto di integrazione Adobe I/O {#details-stored-for-the-adobe-io-integration-project}

Dalla console Progetti di Adobe I/O è disponibile un elenco di tutti i progetti di integrazione:

* [https://console.adobe.io/projects](https://console.adobe.io/projects)

Seleziona una voce di progetto specifica per visualizzare ulteriori dettagli sulla configurazione. Comprendono:

* Panoramica del progetto
* Approfondimenti
* Credenziali
   * Account di servizio (JWT)
      * Dettagli delle credenziali
      * Genera JWT
* API
   * Ad esempio, Adobe Analytics

Alcune di queste sono necessarie per completare l’integrazione di Adobe I/O per Adobe Analytics in AEM.

## Completamento della configurazione IMS in AEM {#completing-the-ims-configuration-in-aem}

Di nuovo AEM puoi completare la configurazione IMS aggiungendo i valori richiesti dall’integrazione Adobe I/O per Target:

1. Torna a [Configurazione IMS aperta in AEM](#configuring-an-ims-configuration-generating-a-public-key).
1. Seleziona **Avanti**.

1. Qui puoi utilizzare la [dettagli della configurazione del progetto nell’Adobe I/O](#details-stored-for-the-adobe-io-integration-project):

   * **Titolo**: Testo.
   * **Server autorizzazioni**: Copia/incolla questo da `aud` della linea **Payload** sezione seguente, ad esempio `https://ims-na1.adobelogin.com` nell&#39;esempio seguente
   * **Chiave API**: Copia questo da **Credenziali** della sezione [Panoramica del progetto](#details-stored-for-the-adobe-io-integration-project)
   * **Segreto client**: Genera questo in [Scheda Segreto client della sezione Account servizio (JWT)](#details-stored-for-the-adobe-io-integration-project)e copia
   * **Payload**: Copia questo da [Scheda Genera JWT della sezione Account di servizio (JWT)](#details-stored-for-the-adobe-io-integration-project)

   ![Dettagli di configurazione di IMS AEM](assets/integrate-analytics-io-10.png)

1. Conferma con **Crea**.

1. La configurazione di Adobe Target verrà visualizzata nella console AEM.

   ![Configurazione IMS](assets/integrate-analytics-io-11.png)

## Conferma della configurazione IMS {#confirming-the-ims-configuration}

Per confermare che la configurazione funziona come previsto:

1. Apri:

   * `https://localhost<port>/libs/cq/adobeims-configuration/content/configurations.html`

   Esempio:

   * `https://localhost:4502/libs/cq/adobeims-configuration/content/configurations.html`


1. Seleziona la configurazione.
1. Seleziona **Verifica stato** dalla barra degli strumenti, seguita da **Controlla**.

   ![Configurazione IMS - Verifica stato](assets/integrate-analytics-io-12.png)

1. In caso di esito positivo, verrà visualizzato un messaggio di conferma.

   <!--
   ![](assets/integrate-target-io-13.png)
   -->

## Configurazione del servizio Adobe Analytics Cloud {#configuring-the-adobe-analytics-cloud-service}

È ora possibile fare riferimento alla configurazione affinché un Cloud Service utilizzi l’API di Analytics Standard:

1. Apri **Strumenti** menu. Quindi, all&#39;interno del **Cloud Services** sezione , seleziona **Cloud Services legacy**.
1. Scorri verso il basso fino a **Adobe Analytics** e seleziona **Configura ora**.

   La **Crea configurazione** si aprirà la finestra di dialogo .

1. Inserisci un **Titolo** e, se volete, un **Nome** (se lasciato vuoto, verrà generato dal titolo).

   È inoltre possibile selezionare il modello richiesto (se sono disponibili più modelli).

1. Conferma con **Crea**.

   La **Modifica componente** si aprirà la finestra di dialogo .

1. Immetti i dettagli nella **Impostazioni di Analytics** scheda:

   * **Autenticazione**: IMS

   * **Configurazione IMS**: seleziona il nome della configurazione IMS

1. Fai clic su **Connettersi ad Analytics** per inizializzare la connessione con Adobe Target.

   Se la connessione ha esito positivo, viene visualizzato il messaggio **Connessione riuscita** viene visualizzato.

1. Seleziona **OK** sul messaggio.

1. Se necessario, completa gli altri parametri seguiti da **OK** nella finestra di dialogo per confermare la configurazione.

1. Ora puoi procedere con [Aggiunta di un framework di Analytics](/help/sites-administering/adobeanalytics-connect.md) per configurare i parametri che verranno inviati ad Adobe Analytics.
