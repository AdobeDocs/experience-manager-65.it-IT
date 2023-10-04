---
title: Integrazione di AEM 6.5 con Adobe Campaign Standard
description: Scopri come integrare AEM 6.5 con Adobe Campaign Standard.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
exl-id: caa43d80-1f38-46fc-a8b9-9485c235c0ca
source-git-commit: 5bdf42d1ce7b2126bfb2670049deec4b6eaedba2
workflow-type: tm+mt
source-wordcount: '1833'
ht-degree: 18%

---


# Integrazione di AEM 6.5 con Adobe Campaign Standard {#integrating-with-adobe-campaign-standard}

Integrando AEM 6.5 con Adobe Campaign Standard (ACS), puoi gestire la consegna e-mail, il contenuto e i moduli direttamente nell’AEM. Per consentire la comunicazione bidirezionale tra le soluzioni sono necessari passaggi di configurazione sia in Adobe Campaign Standard che in AEM.

Questa integrazione consente di utilizzare AEM e Adobe Campaign Standard in modo indipendente. Gli addetti al marketing possono creare campagne e utilizzare il targeting in Adobe Campaign, mentre i creatori di contenuti possono lavorare contemporaneamente sulla progettazione del contenuto in AEM. Utilizzando l’integrazione, il contenuto e la progettazione della campagna creata in AEM possono essere mirati e consegnati da Adobe Campaign.

>[!INFO]
>
>Questo documento illustra come integrare Adobe Campaign Standard con AEM 6.5. Per altre integrazioni di Campaign consulta il documento [Integrazione di AEM 6.5 con Adobe Campaign.](campaign.md)

## Passaggi dell’integrazione {#integration-steps}

La configurazione dell’integrazione tra AEM e Adobe Campaign Standard richiede una serie di passaggi in entrambe le soluzioni.

1. [Configurare ](#aemserver-user)
1. [Verificare la ](#resource-type-filter)
1. [Creare un modello di consegna e-mail specifico per AEM in Campaign](#aem-email-delivery-template)
1. [Configurare l’integrazione di Campaign in AEM](#campaign-integration)
1. [Configurare la replica nell’istanza di pubblicazione AEM](#replication)
1. [Configurare AEM Externalizer](#externalizer)
1. [Configurare ](#campaign-remote-user)
1. [Configurare l’account esterno dell’AEM in Campaign](#acc-external-user)

Il presente documento fornisce una guida dettagliata per superare ognuno di questi passaggi.

## Prerequisiti {#prerequisites}

* Accesso amministratore ad Adobe Campaign Standard
   * Per ulteriori informazioni su come impostare e configurare Adobe Campaign Standard, consulta [Documentazione di Adobe Campaign Standard.](https://experienceleague.adobe.com/docs/campaign-standard/using/campaign-standard-home.html)
* Accesso dell’amministratore all’AEM

## Configurare l’utente aemserver in Campaign {#aemserver-user}

Per impostazione predefinita, Adobe Campaign Standard viene fornito con `aemserver` utente che l’AEM utilizza per connettersi ad Adobe Campaign. È necessario assegnare un gruppo di sicurezza appropriato per l&#39;utente e impostarne la password.

1. Accedi ad Adobe Campaign come amministratore.

1. Tocca o fai clic sul Logo Adobe Campaign in alto a sinistra nella barra dei menu per aprire la navigazione globale, quindi seleziona **Amministrazione** > **Utenti e sicurezza** > **Utenti** dal menu di navigazione.

1. Tocca o fai clic su `aemserver` utente nella console utenti.

1. Assicurati che `aemserver` l&#39;utente viene assegnato come minimo a un gruppo di sicurezza con il ruolo `deliveryPrepare` ad essa assegnati. Per impostazione predefinita, il gruppo `Standard Users` ha questo ruolo.

   ![utente aemserver in Adobe Campaign](assets/acs-aemserver-user.png)

1. Per salvare le modifiche, tocca o fai clic su **Salva**.

Il tuo `aemserver` L’utente dispone ora dei diritti necessari per consentire all’AEM di utilizzarli per comunicare con Adobe Campaign.

Tuttavia, prima che l’AEM possa usare `aemserver` utente, è necessario impostarne la password. Questo non può essere fatto tramite Adobe Campaign. Deve essere eseguita da un tecnico del supporto Adobe. [Crea un ticket presso l’Assistenza clienti Adobe](https://experienceleague.adobe.com/?support-tab=home&amp;lang=it#support) per richiedere la reimpostazione del `aemserver` password. Una volta ottenuta la password da Adobe Customer Care, conservala in un luogo sicuro.

## Verificare AEMResourceTypeFilter in Campaign {#resource-type-filter}

Il `AEMResourceTypeFilter` è un’opzione di Adobe Campaign che viene utilizzata per filtrare le risorse AEM che possono essere utilizzate in Adobe Campaign. Poiché l’AEM contiene molti contenuti, questa opzione funge da filtro che consente ad Adobe Campaign di recuperare solo i contenuti AEM di tipi progettati specificamente per essere utilizzati in Adobe Campaign.

Questa opzione è preconfigurata. Tuttavia, potrebbe essere necessario aggiornarla se sono stati personalizzati i componenti di Campaign dell’AEM. Per verificare che `AEMResourceTypeFilter` è configurata, segui la procedura riportata di seguito.

1. Accedi ad Adobe Campaign come amministratore.

1. Tocca o fai clic sul Logo Adobe Campaign in alto a sinistra nella barra dei menu per aprire la navigazione globale, quindi seleziona **Amministrazione** > **Impostazioni applicazione** > **Opzioni** dal menu di navigazione.

1. Tocca o fai clic su `AEMResourceTypeFilter` nella console delle opzioni.

1. Conferma la configurazione di `AEMResourceTypeFilter`. I percorsi sono delimitati da virgole e per impostazione predefinita contengono:

   * `mcm/campaign/components/newsletter`
   * `mcm/campaign/components/campaign_newsletterpage`
   * `mcm/neolane/components/newsletter`

   ![AEMResourceTypeFilter](assets/acs-aem-resource-type-filter.png)

1. Per salvare le modifiche, tocca o fai clic su **Salva**.

Il tuo `AEMResourceTypeFilter` è ora configurato per recuperare il contenuto corretto dall’AEM.

## Creare un modello di consegna e-mail specifico per AEM in Campaign {#aem-email-delivery-template}

Per impostazione predefinita, l’AEM non è abilitato nei modelli e-mail di Adobe Campaign. Devi configurare un nuovo modello di consegna e-mail che possa essere utilizzato per creare e-mail utilizzando contenuti AEM. Per creare un modello di consegna e-mail specifico per l’AEM, segui la procedura riportata di seguito.

1. Accedi ad Adobe Campaign come amministratore.

1. Tocca o fai clic sul Logo Adobe Campaign in alto a sinistra nella barra dei menu per aprire la navigazione globale, quindi seleziona **Risorse** > **Modelli** > **Modelli di consegna** dal menu di navigazione.

1. Nella console dei modelli di consegna, individua il modello e-mail predefinito **Invia tramite e-mail** e passa il mouse sulla scheda (o riga) che la rappresenta per visualizzare le opzioni. Clic **Elemento duplicato**.

   ![Elemento duplicato](assets/acs-copy-template.png)

1. In **Conferma** , fai clic su **Conferma** per duplicare il modello.

   ![Finestra di dialogo di conferma](assets/acs-confirmation.png)

1. Viene aperto l’editor modelli con la tua copia del **Invia tramite e-mail** modello. Fai clic su **Modifica proprietà** in alto a destra nella finestra.

   ![Editor modelli](assets/acs-template-editor.png)

1. Nella finestra delle proprietà, modifica **Etichetta** per essere descrittivo del nuovo modello AEM.

1. Fai clic su **Contenuto** intestazione per espanderlo e selezionare **Adobe Experience Manager** nel **Origine contenuto** a discesa.

1. Questo rivela **Account Adobe Experience Manager** campo. Utilizza il menu a discesa per selezionare **Istanza di Adobe Experience Manager (aemInstance)** utente. Questo è l’utente esterno predefinito per l’integrazione AEM.

![Configurare le proprietà del modello](assets/acs-template-properties.png)

1. Clic **Conferma** per salvare le modifiche apportate alle proprietà.

1. Nell’editor modelli, fai clic su **Salva** per salvare la copia modificata del modello e-mail da utilizzare con AEM.

Ora disponi di un modello e-mail che può utilizzare contenuti AEM.

## Configurare l’integrazione di Campaign in AEM {#campaign-integration}

L’AEM comunica con Adobe Campaign utilizzando un’integrazione integrata e `aemserver` configurata in Adobe Campaign. Per configurare questa integrazione, segui la procedura riportata di seguito.

1. Accedi alla tua istanza di authoring di AEM come amministratore.

1. Dalla barra laterale di navigazione globale, seleziona **Strumenti** > **Cloud Services** > **Cloud Services legacy** > **Adobe Campaign**, quindi fai clic su **Configura ora**.

   ![Configura Adobe Campaign](assets/configure-campaign-service.png)

1. Nella finestra di dialogo, crea una configurazione del servizio Campaign inserendo un **Titolo** e facendo clic su **Crea**.

   ![Finestra di dialogo Configura Campaing](assets/configure-campaign-dialog.png)

1. Viene visualizzata una nuova finestra di dialogo per modificare la configurazione. Fornisci le informazioni necessarie.

   * **Nome utente** - Questo è [il `aemserver` utente in Adobe Campaign configurato in un passaggio precedente.](#aemserver-user)Per impostazione predefinita, è `aemserver`.
   * **Password** - Password per [il `aemserver` utente in Adobe Campaign che hai richiesto all’Assistenza clienti di Adobe in un passaggio precedente.](#aemserver-user)
   * **Endpoint API**: corrisponde all’URL dell’istanza di Adobe Campaign.

   ![Configura Adobe Campaign in AEM](assets/configure-campaign.png)

1. Seleziona **Connetti ad Adobe Campaign** per verificare la connessione, quindi fai clic su **OK**.

AEM adesso può comunicare con Adobe Campaign.

>[!NOTE]
>
>Assicurati che il server di Adobe Campaign sia raggiungibile tramite Internet. L&#39;AEM non può accedere alle reti private.

## Configurare la replica nell’istanza di pubblicazione AEM {#replication}

Il contenuto della campagna viene creato dagli autori di contenuti nell’istanza di authoring AEM. In genere questa istanza è disponibile solo internamente all’interno dell’organizzazione. Affinché contenuti come immagini e risorse siano accessibili ai destinatari della campagna, devi pubblicare tali contenuti.

L’agente di replica è responsabile della pubblicazione dei contenuti dall’istanza di authoring AEM all’istanza di pubblicazione e deve essere configurato affinché l’integrazione funzioni correttamente. Questo passaggio è necessario anche per replicare alcune configurazioni di istanze di authoring nell’istanza di pubblicazione.

Per configurare la replica dall’istanza di authoring AEM all’istanza di pubblicazione:

1. Accedi alla tua istanza di authoring di AEM come amministratore.

1. Dalla barra laterale di navigazione globale, seleziona **Strumenti** > **Distribuzione** > **Replica** > **Agenti per creazione**, quindi tocca o fai clic su **Agente predefinito (pubblicazione)**.

   ![Configurare l’agente di replica](assets/acc-replication-config.png)

1. Tocca o fai clic su **Modifica** quindi seleziona la **Trasporto** scheda.

1. Configurare **URI** sostituendo il campo predefinito `localhost` valore con l’indirizzo IP dell’istanza di pubblicazione AEM.

   ![Scheda Trasporto](assets/acc-transport-tab.png)

1. Tocca o fai clic su **OK** per salvare le modifiche apportate alle impostazioni dell&#39;agente.

Hai configurato la replica nell’istanza di pubblicazione dell’AEM in modo che i destinatari della campagna possano accedere al contenuto.

>[!NOTE]
>
>Se non desideri utilizzare l’URL di replica ma l’URL pubblico, puoi impostarlo nella seguente impostazione di configurazione tramite OSGi
>
>Dalla barra laterale di navigazione globale, seleziona **Strumenti** > **Operazioni** > **Console web** > **Configurazione OSGi** e cerca **Integrazione AEM Campaign - Configurazione**. Modifica la configurazione e cambia il campo **URL pubblico** (`com.day.cq.mcm.campaign.impl.IntegrationConfigImpl#aem.mcm.campaign.publicUrl`).

## Configurare AEM Externalizer {#externalizer}

[Externalizer è un servizio OSGi di AEM che trasforma un percorso di risorsa in un URL esterno e assoluto, necessario perché AEM possa distribuire i contenuti utilizzabili da Campaign. ](/help/sites-developing/externalizer.md) Devi configurarlo affinché l’integrazione di Campaign funzioni.

1. Accedi all’istanza di authoring di AEM come amministratore.
1. Dalla barra laterale di navigazione globale, seleziona **Strumenti** > **Operazioni** > **Console web** > **Configurazione OSGi** e cerca **Day CQ link Externalizer**.
1. Per impostazione predefinita, l’ultima voce nella **Domini** è destinato all’istanza Publish. Modifica l’URL dal valore predefinito `http://localhost:4503` nell’istanza Publish pubblicamente disponibile.

   ![Configurazione di Externalizer](assets/acc-externalizer-config.png)

1. Tocca o fai clic su **Salva**.

Dopo aver configurato Externalizer, Adobe Campaign può accedere al contenuto.

>[!NOTE]
>
L’stanza di pubblicazione deve essere raggiungibile dal server di Adobe Campaign. Se punta a `localhost:4503` oppure in un altro server che Adobe Campaign non è in grado di raggiungere, le immagini provenienti dall’AEM non vengono visualizzate nella console Adobe Campaign.

## Configurare l’utente remoto di Campaign in AEM {#campaign-remote-user}

Proprio come hai bisogno di un utente in Adobe Campaign che l’AEM possa utilizzare per comunicare con Adobe Campaign, Adobe Campaign ha bisogno di un utente in AEM anche per comunicare con AEM. Per impostazione predefinita, l’integrazione di Campaign crea `campaign-remote` dell&#39;AEM. Per configurare l’utente, segui la procedura riportata di seguito.

1. Accedi ad AEM come amministratore.
1. Nella console di navigazione principale, fai clic su **Strumenti** nella barra a sinistra.
1. Quindi fai clic su **Sicurezza** > **Utenti** per aprire la console di amministrazione degli utenti.
1. Individua l’utente `campaign-remote`.
1. Seleziona l’utente `campaign-remote` e fai clic su **Proprietà** per modificarlo.
1. Nella finestra **Modifica impostazioni utente**, fai clic su **Cambia password**.
1. Fornisci una nuova password per l’utente, annota la password e conservala in un luogo sicuro per utilizzarla in futuro.
1. Fai clic su **Salva** per salvare il cambiamento della password.
1. Fai clic su **Salva e chiudi** per salvare le modifiche apportate all’utente `campaign-remote`.

## Configurare l’account esterno dell’AEM in Campaign {#acc-external-user}

Quando [ha creato un modello di consegna e-mail specifico per l’AEM,](#aem-email-delivery-template) hai specificato che il modello deve utilizzare `aemInstance` conto esterno per comunicare con l’AEM. Per abilitare la comunicazione bidirezionale tra entrambe le soluzioni, devi configurare questo account in Adobe Campaign.

1. Accedi ad Adobe Campaign come amministratore.

1. Tocca o fai clic sul Logo Adobe Campaign in alto a sinistra nella barra dei menu per aprire la navigazione globale, quindi seleziona **Amministrazione** > **Impostazioni applicazione** > **Account esterni** dal menu di navigazione.

1. Tocca o fai clic su **Istanza di Adobe Experience Manager (aemInstance)** utente nella console utenti.

1. Assicurati che l’utente abbia **Adobe Experience Manager** come **Tipo**.

1. In **Connessione** , definisci i campi seguenti:

   1. Server: URL del server di authoring AEM. Non deve terminare con una barra.
   1. Account: questo è il `campaign-remote` utente tu [precedentemente configurato nell’AEM.](#campaign-remote-user)
   1. Password: password per il `campaign-remote`utente tu [precedentemente configurato nell’AEM.](#campaign-remote-user)

   ![Modifica dell’utente aemInstance](assets/acs-external-acount-editor.png)

1. Assicurati che **Abilitato** è selezionata, quindi fai clic su **Salva** per salvare le modifiche.

Congratulazioni. Hai completato l’integrazione tra AEM e Adobe Campaign Standard.

## Passaggi successivi {#next-steps}

Con Adobe Campaign Classic e AEM configurati, l’integrazione è ora completa.

Per scoprire come creare una newsletter in Adobe Experience Manager, prosegui con [il presente documento.](/help/sites-authoring/campaign.md)
