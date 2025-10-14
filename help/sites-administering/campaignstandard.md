---
title: Integrazione di AEM 6.5 con Adobe Campaign Standard
description: Scopri come integrare AEM 6.5 con Adobe Campaign Standard.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
exl-id: caa43d80-1f38-46fc-a8b9-9485c235c0ca
solution: Experience Manager, Experience Manager Sites
feature: Integration
role: Admin
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '1787'
ht-degree: 12%

---


# Integrazione di AEM 6.5 con Adobe Campaign Standard {#integrating-with-adobe-campaign-standard}

Integrando AEM 6.5 con Adobe Campaign Standard (ACS), puoi gestire la consegna e-mail, il contenuto e i moduli direttamente nell’AEM. Per consentire la comunicazione bidirezionale tra le soluzioni sono necessari passaggi di configurazione sia in Adobe Campaign Standard che in AEM.

Questa integrazione consente di utilizzare AEM e Adobe Campaign Standard in modo indipendente. Gli addetti al marketing possono creare campagne e utilizzare il targeting in Adobe Campaign, mentre i creatori di contenuti possono lavorare contemporaneamente sulla progettazione dei contenuti nell’AEM. Utilizzando l’integrazione, il contenuto e la progettazione della campagna creata in AEM possono essere mirati e consegnati da Adobe Campaign.

>[!INFO]
>
>Questo documento illustra come integrare Adobe Campaign Standard con AEM 6.5. Per altre integrazioni di Campaign, consulta il documento [Integrazione di AEM 6.5 con Adobe Campaign.](campaign.md)

## Passaggi dell’integrazione {#integration-steps}

La configurazione dell’integrazione tra AEM e Adobe Campaign Standard richiede diversi passaggi in entrambe le soluzioni.

1. [Configurare &#x200B;](#aemserver-user)
1. [Verificare la &#x200B;](#resource-type-filter)
1. [Creare un modello di consegna e-mail specifico per AEM in Campaign](#aem-email-delivery-template)
1. [Configurare l’integrazione di Campaign in AEM](#campaign-integration)
1. [Configurare la replica nell’istanza Publish dell’AEM](#replication)
1. [Configurare AEM Externalizer](#externalizer)
1. [Configurare &#x200B;](#campaign-remote-user)
1. [Configurare l’account esterno dell’AEM in Campaign](#acc-external-user)

Questo documento illustra in dettaglio ciascuno di questi passaggi.

## Prerequisiti {#prerequisites}

* Accesso amministratore ad Adobe Campaign Standard
   * Per ulteriori informazioni su come configurare Adobe Campaign Standard, consulta la [documentazione di Adobe Campaign Standard.](https://experienceleague.adobe.com/docs/campaign-standard/using/campaign-standard-home.html?lang=it)
* Accesso dell’amministratore all’AEM

## Configurare l’utente aemserver in Campaign {#aemserver-user}

Per impostazione predefinita, Adobe Campaign Standard viene fornito con un utente `aemserver` utilizzato dall&#39;AEM per connettersi ad Adobe Campaign. Assegnare un gruppo di sicurezza appropriato per l&#39;utente e impostarne la password.

1. Accedi ad Adobe Campaign come amministratore.

1. Fai clic sul logo Adobe Campaign in alto a sinistra nella barra dei menu per aprire la navigazione globale, quindi seleziona **Amministrazione** > **Utenti e sicurezza** > **Utenti** dal menu di navigazione.

1. Fare clic sull&#39;utente `aemserver` nella console degli utenti.

1. Assicurarsi che l&#39;utente `aemserver` sia assegnato almeno a un gruppo di sicurezza a cui è assegnato il ruolo `deliveryPrepare`. Per impostazione predefinita, il gruppo `Standard Users` ha questo ruolo.

   ![utente aemserver in Adobe Campaign](assets/acs-aemserver-user.png)

1. Fai clic su **Salva** per salvare le modifiche.

L&#39;utente `aemserver` dispone ora dei diritti necessari per consentire all&#39;AEM di utilizzarlo per comunicare con Adobe Campaign.

Tuttavia, prima che l&#39;AEM possa utilizzare l&#39;utente `aemserver`, è necessario impostarne la password. Questo non può essere fatto tramite Adobe Campaign. Deve essere eseguita da un tecnico del supporto Adobe. [Invia un ticket all&#39;Assistenza clienti Adobe](https://experienceleague.adobe.com/it?support-tab=home?lang=it#support) per richiedere la reimpostazione della password `aemserver`. Una volta ottenuta la password da Adobe Customer Care, conservala in un luogo sicuro.

## Verificare AEMResourceTypeFilter in Campaign {#resource-type-filter}

`AEMResourceTypeFilter` è un&#39;opzione in Adobe Campaign che viene utilizzata per filtrare le risorse AEM che possono essere utilizzate in Adobe Campaign. Poiché l’AEM contiene molto contenuto, questa opzione funge da filtro che consente ad Adobe Campaign di recuperare solo il contenuto AEM di tipi appositamente progettati per essere utilizzati in Adobe Campaign.

Questa opzione è preconfigurata. Tuttavia, potrebbe essere necessario aggiornarla se sono stati personalizzati i componenti di Campaign dell’AEM. Per verificare che l&#39;opzione `AEMResourceTypeFilter` sia configurata, eseguire la procedura seguente.

1. Accedi ad Adobe Campaign come amministratore.

1. Fai clic sul logo Adobe Campaign in alto a sinistra nella barra dei menu per aprire la navigazione globale, quindi seleziona **Amministrazione** > **Impostazioni applicazione** > **Opzioni** dal menu di navigazione.

1. Fare clic su `AEMResourceTypeFilter` nella console delle opzioni.

1. Confermare la configurazione di `AEMResourceTypeFilter`. I percorsi sono delimitati da virgole e per impostazione predefinita contengono:

   * `mcm/campaign/components/newsletter`
   * `mcm/campaign/components/campaign_newsletterpage`
   * `mcm/neolane/components/newsletter`

   ![AEMResourceTypeFilter](assets/acs-aem-resource-type-filter.png)

1. Fai clic su **Salva** per salvare le modifiche.

`AEMResourceTypeFilter` è ora configurato per recuperare il contenuto corretto dall&#39;AEM.

## Creare un modello di consegna e-mail specifico per AEM in Campaign {#aem-email-delivery-template}

Per impostazione predefinita, l’AEM non è abilitato nei modelli e-mail di Adobe Campaign. Configura un nuovo modello di consegna e-mail che può essere utilizzato per creare e-mail utilizzando contenuti AEM. Per creare un modello di consegna e-mail specifico per l’AEM, segui la procedura riportata di seguito.

1. Accedi ad Adobe Campaign come amministratore.

1. Fai clic sul logo Adobe Campaign in alto a sinistra nella barra dei menu per aprire la navigazione globale, quindi seleziona **Risorse** > **Modelli** > **Modelli di consegna** dal menu di navigazione.

1. Nella console dei modelli di consegna, individua il modello di e-mail predefinito **Invia tramite e-mail** e passa il puntatore del mouse sulla scheda (o riga) che lo rappresenta per visualizzare le opzioni. Fare clic su **Elemento duplicato**.

   ![Elemento duplicato](assets/acs-copy-template.png)

1. Nella finestra di dialogo **Conferma**, fai clic su **Conferma** per duplicare il modello.

   ![Finestra di conferma](assets/acs-confirmation.png)

1. Verrà aperto l&#39;editor modelli con la tua copia del modello **Invia tramite posta elettronica**. Fai clic sull&#39;icona **Modifica proprietà** in alto a destra nella finestra.

   ![Editor modelli](assets/acs-template-editor.png)

1. Nella finestra delle proprietà, modifica il campo **Etichetta** in modo che sia descrittivo del nuovo modello AEM.

1. Fai clic sull&#39;intestazione **Contenuto** per espanderla e selezionare **Adobe Experience Manager** nel menu a discesa **Origine contenuto**.

1. Viene visualizzato il campo **Account Adobe Experience Manager**. Utilizza il menu a discesa per selezionare l&#39;utente **istanza di Adobe Experience Manager (aemInstance)**. Questo è l’utente esterno predefinito per l’integrazione AEM.

![Configura proprietà modello](assets/acs-template-properties.png)

1. Fai clic su **Conferma** per salvare le modifiche apportate alle proprietà.

1. Nell&#39;editor modelli, fai clic su **Salva** per salvare la copia modificata del modello e-mail da utilizzare con AEM.

Ora disponi di un modello e-mail che può utilizzare contenuti AEM.

## Configurare l’integrazione di Campaign in AEM {#campaign-integration}

AEM comunica con Adobe Campaign utilizzando un&#39;integrazione incorporata e l&#39;utente `aemserver` configurato in Adobe Campaign. Per configurare questa integrazione, segui la procedura riportata di seguito.

1. Accedi alla tua istanza di authoring di AEM come amministratore.

1. Dalla barra laterale di navigazione globale, seleziona **Strumenti** > **Cloud Services** > **Cloud Services legacy** > **Adobe Campaign**, quindi fai clic su **Configura ora**.

   ![Configura Adobe Campaign](assets/configure-campaign-service.png)

1. Nella finestra di dialogo, crea una configurazione del servizio Campaign inserendo un **Titolo** e facendo clic su **Crea**.

   ![Finestra di dialogo Configura Campaing](assets/configure-campaign-dialog.png)

1. Viene visualizzata una nuova finestra di dialogo per modificare la configurazione. Fornisci le informazioni necessarie.

   * **Nome utente** - Questo è [l&#39;utente `aemserver` in Adobe Campaign configurato in un passaggio precedente.](#aemserver-user)Per impostazione predefinita, è `aemserver`.
   * **Password** - Questa è la password per [l&#39;utente `aemserver` in Adobe Campaign che hai richiesto all&#39;Assistenza clienti di Adobe in un passaggio precedente.](#aemserver-user)
   * **Endpoint API**: corrisponde all’URL dell’istanza di Adobe Campaign.

   ![Configura Adobe Campaign in AEM](assets/configure-campaign.png)

1. Seleziona **Connetti ad Adobe Campaign** per verificare la connessione, quindi fai clic su **OK**.

AEM adesso può comunicare con Adobe Campaign.

>[!NOTE]
>
>Assicurati che il server di Adobe Campaign sia raggiungibile tramite Internet. L&#39;AEM non può accedere alle reti private.

## Configurare la replica nell’istanza Publish dell’AEM {#replication}

Il contenuto della campagna viene creato dagli autori di contenuti nell’istanza di authoring AEM. In genere questa istanza è disponibile solo internamente all’interno dell’organizzazione. Affinché contenuti come immagini e risorse siano accessibili ai destinatari della campagna, devi pubblicare tali contenuti.

L’agente di replica è responsabile della pubblicazione dei contenuti dall’istanza di authoring AEM all’istanza di pubblicazione e deve essere configurato affinché l’integrazione funzioni correttamente. Questo passaggio è necessario anche per replicare alcune configurazioni di istanze di authoring nell’istanza di pubblicazione.

Per configurare la replica dall’istanza di authoring AEM all’istanza di pubblicazione:

1. Accedi alla tua istanza di authoring di AEM come amministratore.

1. Dalla barra laterale di navigazione globale, seleziona **Strumenti** > **Distribuzione** > **Replica** > **Agenti sull&#39;autore**, quindi fai clic su **Agente predefinito (pubblicazione)**.

   ![Configura agente di replica](assets/acc-replication-config.png)

1. Fai clic su **Modifica**, quindi seleziona la scheda **Trasporto**.

1. Configurare il campo **URI** sostituendo il valore `localhost` predefinito con l&#39;indirizzo IP dell&#39;istanza di pubblicazione AEM.

   ![Scheda Trasporto](assets/acc-transport-tab.png)

1. Fare clic su **OK** per salvare le modifiche alle impostazioni dell&#39;agente.

Hai configurato la replica nell’istanza di pubblicazione dell’AEM in modo che i destinatari della campagna possano accedere al contenuto.

>[!NOTE]
>
>Se non desideri utilizzare l’URL di replica ma l’URL pubblico, puoi impostarlo nella seguente impostazione di configurazione tramite OSGi
>
>Dalla barra laterale di navigazione globale, seleziona **Strumenti** > **Operazioni** > **Console Web** > **Configurazione OSGi** e cerca **Integrazione campagna AEM - Configurazione**. Modifica la configurazione e modifica il campo **URL pubblico** (`com.day.cq.mcm.campaign.impl.IntegrationConfigImpl#aem.mcm.campaign.publicUrl`).

## Configurare AEM Externalizer {#externalizer}

[Externalizer](/help/sites-developing/externalizer.md) è un servizio OSGi in AEM che trasforma un percorso di risorsa in un URL esterno e assoluto, necessario affinché l&#39;AEM possa distribuire il contenuto utilizzabile da Campaign. Configuralo in modo che l’integrazione di Campaign funzioni.

1. Accedi all’istanza di authoring di AEM come amministratore.
1. Dalla barra laterale di navigazione globale, seleziona **Strumenti** > **Operazioni** > **Console Web** > **Configurazione OSGi** e cerca **Day CQ Link Externalizer**.
1. Per impostazione predefinita, l&#39;ultima voce nel campo **Domini** è destinata all&#39;istanza di pubblicazione. Modifica l&#39;URL da `http://localhost:4503` predefinito all&#39;istanza di pubblicazione disponibile pubblicamente.

   ![Configurazione di Externalizer](assets/acc-externalizer-config.png)

1. Fai clic su **Salva**.

Dopo aver configurato Externalizer, Adobe Campaign può accedere al contenuto.

>[!NOTE]
>
>L’istanza di pubblicazione deve essere raggiungibile dal server Adobe Campaign. Se punta a `localhost:4503` o a un altro server che Adobe Campaign non è in grado di raggiungere, le immagini dell&#39;AEM non verranno visualizzate nella console Adobe Campaign.

## Configurare l’utente remoto di Campaign in AEM {#campaign-remote-user}

Proprio come hai bisogno di un utente in Adobe Campaign che l’AEM possa utilizzare per comunicare con Adobe Campaign, Adobe Campaign ha bisogno di un utente in AEM anche per comunicare con AEM. Per impostazione predefinita, l&#39;integrazione di Campaign crea l&#39;utente `campaign-remote` in AEM. Per configurare l’utente, segui la procedura riportata di seguito.

1. Accedi ad AEM come amministratore.
1. Nella console di navigazione principale, fai clic su **Strumenti** nella barra a sinistra.
1. Quindi fai clic su **Sicurezza** > **Utenti** per aprire la console di amministrazione utenti.
1. Individua l’utente `campaign-remote`.
1. Seleziona l’utente `campaign-remote` e fai clic su **Proprietà** per modificarlo.
1. Nella finestra **Modifica impostazioni utente**, fai clic su **Cambia password**.
1. Fornisci una nuova password per l’utente, annota la password e conservala in un luogo sicuro per utilizzarla in futuro.
1. Fai clic su **Salva** per salvare il cambiamento della password.
1. Fai clic su **Salva e chiudi** per salvare le modifiche apportate all’utente `campaign-remote`.

## Configurare l’account esterno dell’AEM in Campaign {#acc-external-user}

Quando [hai creato un modello di consegna e-mail specifico per AEM](#aem-email-delivery-template) hai specificato che il modello deve utilizzare l&#39;account esterno `aemInstance` per comunicare con AEM. Per abilitare la comunicazione bidirezionale tra entrambe le soluzioni, devi configurare questo account in Adobe Campaign.

1. Accedi ad Adobe Campaign come amministratore.

1. Fai clic sul logo Adobe Campaign in alto a sinistra nella barra dei menu per aprire la navigazione globale, quindi seleziona **Amministrazione** > **Impostazioni applicazione** > **Account esterni** dal menu di navigazione.

1. Fai clic sull&#39;utente **istanza di Adobe Experience Manager (aemInstance)** nella console degli utenti.

1. Verificare che l&#39;utente disponga di **Adobe Experience Manager** come **Type**.

1. Nella sezione **Connessione**, definisci i campi seguenti:

   1. Server: URL del server di authoring AEM. Non deve terminare con una barra.
   1. Account: questo è l&#39;utente `campaign-remote` [&#x200B; configurato in precedenza in AEM.](#campaign-remote-user)
   1. Password: questa è la password per l&#39;utente `campaign-remote` configurato in precedenza in AEM.[&#128279;](#campaign-remote-user)

   ![Modifica dell&#39;utente aemInstance](assets/acs-external-acount-editor.png)

1. Assicurati che la casella di controllo **Enabled** sia selezionata, quindi fai clic su **Salva** per salvare le modifiche.

Congratulazioni Hai completato l’integrazione tra AEM e Adobe Campaign Standard.

## Passaggi successivi {#next-steps}

Con Adobe Campaign Classic e AEM configurati, l’integrazione è ora completa.

Per scoprire come creare una newsletter in Adobe Experience Manager, prosegui con [il presente documento.](/help/sites-authoring/campaign.md)
