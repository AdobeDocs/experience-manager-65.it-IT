---
title: Integrazione di AEM 6.5 con Adobe Campaign Classic
description: Scopri come integrare AEM 6.5 con Adobe Campaign Classic
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
exl-id: a7281ca0-461f-4762-a631-6bb539596200
solution: Experience Manager, Experience Manager Sites
feature: Integration
role: Admin
source-git-commit: 6fb844ea428c15adab71503dde6138e46eabf0a3
workflow-type: tm+mt
source-wordcount: '1564'
ht-degree: 52%

---


# Integrazione di AEM 6.5 con Adobe Campaign Classic {#integrating-campaign-classic}

Integrando l’AEM con Adobe Campaign Classic (ACC), puoi gestire la consegna e-mail, il contenuto e i moduli direttamente nell’AEM. Per consentire la comunicazione bidirezionale tra le soluzioni sono necessari passaggi di configurazione sia in Adobe Campaign Classic che in AEM.

Questa integrazione consente di utilizzare AEM e Adobe Campaign Classic in modo indipendente. Gli addetti al marketing possono creare campagne e utilizzare il targeting in Adobe Campaign, mentre i creatori di contenuti possono lavorare contemporaneamente sulla progettazione dei contenuti nell’AEM. Utilizzando l’integrazione, il contenuto e la progettazione della campagna creata in AEM possono essere mirati e consegnati da Adobe Campaign.

>[!INFO]
>
>Questo documento illustra come integrare Adobe Campaign Classic con AEM 6.5. Per altre integrazioni di Campaign consulta il documento [Integrazione di AEM 6.5 con Adobe Campaign.](campaign.md)

## Passaggi dell’integrazione {#integration-steps}

L’integrazione tra AEM e Campaign richiede diversi passaggi in entrambe le soluzioni.

1. [Installazione del pacchetto di integrazione di AEM in Campaign.](#install-package)
1. [Creare un operatore di AEM in Campaign](#create-operator)
1. [Configurare l’integrazione di Campaign in AEM](#campaign-integration)
1. [Configurare AEM Externalizer](#externalizer)
1. [Configurare l’utente remoto di Campaing in AEM](#configure-user)
1. [Configurare l’account esterno di AEM in Campaign](#acc-setup)

Questo documento illustra in dettaglio ciascuno di questi passaggi.

## Prerequisiti {#prerequisites}

* Accesso amministratore ad Adobe Campaign Classic
   * Per eseguire l’integrazione, è necessaria un&#39;istanza Adobe Campaign Classic funzionante, incluso un database configurato.
   * Per ulteriori informazioni su come impostare e configurare Adobe Campaign Classic, vedere [documentazione di Adobe Campaign Classic,](https://experienceleague.adobe.com/docs/campaign-classic/using/campaign-classic-home.html?lang=it) in particolare la guida all&#39;installazione e alla configurazione.
* Accesso dell’amministratore all’AEM

## Installare il pacchetto di integrazione dell’AEM in Campaign {#install-package}

Il **Integrazione AEM** Il pacchetto in Adobe Campaign include diverse configurazioni standard necessarie per connettersi all’AEM.

1. In qualità di amministratore, accedi all’istanza di Adobe Campaign utilizzando la console client.

1. Seleziona **Strumenti** > **Avanzate** > **Importa pacchetto..**.

   ![Importa pacchetto](assets/import-package.png)

1. Fai clic su **Installa un pacchetto standard** e quindi su **Successivo**.

1. Verifica il pacchetto di **Integrazione di AEM**.

   ![Installa un pacchetto standard](assets/select-package.png)

1. Fai clic su **Successivo** e quindi su **Avvia** per avviare l’installazione.

   ![Avanzamento dell’installazione](assets/installation.png)

1. Al completamento dell’installazione, fai clic su **Chiudi**.

Il pacchetto di integrazione adesso è installato.

## Creare l’operatore per l’AEM in Campaign {#create-operator}

Il pacchetto di integrazione crea automaticamente l’operatore `aemserver` che AEM utilizza per connettersi ad Adobe Campaign. Definisci un’area di sicurezza per questo operatore e impostane la password.

1. Accedi ad Adobe Campaign come amministratore utilizzando la console client.

1. Seleziona **Strumenti** > **Esplora** dalla barra dei menu.

1. In Esplora, passa al nodo **Amministrazione** > **Gestione degli accessi** > **Operatori**.

1. Seleziona l’operatore `aemserver`.

1. Nella scheda **Modifica** dell’operatore, seleziona la sotto-scheda **Diritti di accesso** e quindi fai clic sul link **Modifica i parametri di accesso...**.

   ![Imposta l’area di sicurezza](assets/access-rights.png)

1. Seleziona l’area di sicurezza appropriata e definisci la maschera IP attendibile in base alle esigenze.

   >[!CAUTION]
   >
   >L’area di sicurezza da configurare è **Rete aziendale privata (VPN+LAN)**.

1. Fai clic su **Salva**.

1. Esci dal client di Adobe Campaign.

1. Nel file system del server di Adobe Campaign, accedi al percorso di installazione di Campaign e modifica il `serverConf.xml` file come amministratore. Generalmente questo file si trova in:
   * `C:\Program Files\Adobe\Adobe Campaign Classic v7\conf` in Windows.
   * `/usr/local/neolane/nl6/conf/eng` in Linux.

1. Cerca `securityZone` e assicurati che i seguenti parametri siano impostati per l’area di sicurezza dell’operatore AEM.

   * `allowHTTP="true"`
   * `sessionTokenOnly="true"`
   * `allowUserPassword="true"`.

1. Salva il file.

1. Assicurati che l’area di sicurezza non venga sovrascritta dalle rispettive impostazioni nel `config-<server name>.xml` file.

   * Se il file di configurazione contiene un’impostazione separata per l’area di sicurezza, modifica l’attributo `allowUserPassword` in `true`.

1. Se desideri modificare la porta del server Adobe Campaign Classic, sostituisci `8080` con la porta desiderata.

   >[!CAUTION]
   >
   >Per impostazione predefinita, per l’operatore non è configurata alcuna area di sicurezza. Affinché AEM possa connettersi ad Adobe Campaign, devi selezionare un’area come descritto nei passaggi precedenti.
   >
   >Per evitare problemi di sicurezza, Adobe consiglia vivamente di creare un’area di sicurezza dedicata ad AEM. Per ulteriori informazioni su questo argomento, consulta [Documentazione di Adobe Campaign Classic.](https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/additional-configurations/security-zones.html?lang=it)

1. Nel client Campaign, torna all’operatore `aemserver` e seleziona la scheda **Generale**.

1. Fai clic sul link **Reimpostare la password..**.

1. Specifica una password e conservala in luogo sicuro per utilizzarla in futuro.

1. Fai clic su **OK** per salvare la password per l’operatore `aemserver`.

## Configurare l’integrazione di Campaign in AEM {#campaign-integration}

L’AEM utilizza [l’operatore che hai già configurato in Campaign](#create-operator) per comunicare con Campaign

1. Accedi alla tua istanza di authoring di AEM come amministratore.

1. Dalla barra laterale di navigazione globale, seleziona **Strumenti** > **Cloud Services** > **Cloud Services legacy** > **Adobe Campaign**, quindi fai clic su **Configura ora**.

   ![Configura Adobe Campaign](assets/configure-campaign-service.png)

1. Nella finestra di dialogo, crea una configurazione del servizio Campaign inserendo un **Titolo** e facendo clic su **Crea**.

   ![Finestra di dialogo Configura Campaing](assets/configure-campaign-dialog.png)

1. Viene visualizzata una nuova finestra di dialogo per modificare la configurazione. Fornisci le informazioni necessarie.

   * **Nome utente**: corrisponde [all’operatore del pacchetto di integrazione di AEM in Adobe Campaign creato nel passaggio precedente.](#create-operator)Per impostazione predefinita, è `aemserver`.
   * **Password**: corrisponde alla password per l’[operatore del pacchetto di integrazione di AEM in Adobe Campaign creato nel passaggio precedente.](#create-operator)
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

1. Dalla barra laterale di navigazione globale, seleziona **Strumenti** > **Distribuzione** > **Replica** > **Agenti per creazione**, quindi fai clic su **Agente predefinito (pubblicazione)**.

   ![Configurare l’agente di replica](assets/acc-replication-config.png)

1. Clic **Modifica** quindi seleziona la **Trasporto** scheda.

1. Configurare **URI** sostituendo il campo predefinito `localhost` valore con l’indirizzo IP dell’istanza di pubblicazione AEM.

   ![Scheda Trasporto](assets/acc-transport-tab.png)

1. Clic **OK** per salvare le modifiche apportate alle impostazioni dell&#39;agente.

Hai configurato la replica nell’istanza di pubblicazione dell’AEM in modo che i destinatari della campagna possano accedere al contenuto.

>[!NOTE]
>
>Se non desideri utilizzare l’URL di replica ma l’URL pubblico, puoi impostarlo nella seguente impostazione di configurazione tramite OSGi
>
>Dalla barra laterale di navigazione globale, seleziona **Strumenti** > **Operazioni** > **Console web** > **Configurazione OSGi** e cerca **Integrazione AEM Campaign - Configurazione**. Modifica la configurazione e cambia il campo **URL pubblico** (`com.day.cq.mcm.campaign.impl.IntegrationConfigImpl#aem.mcm.campaign.publicUrl`).

## Configurare AEM Externalizer {#externalizer}

[Esternalizzatore](/help/sites-developing/externalizer.md) è un servizio OSGi in AEM che trasforma un percorso di risorsa in un URL esterno e assoluto, necessario affinché l’AEM possa distribuire i contenuti utilizzabili da Campaign. Configuralo in modo che l’integrazione di Campaign funzioni.

1. Accedi all’istanza di authoring di AEM come amministratore.
1. Dalla barra laterale di navigazione globale, seleziona **Strumenti** > **Operazioni** > **Console web** > **Configurazione OSGi** e cerca **Day CQ link Externalizer**.
1. Per impostazione predefinita, l’ultima voce nella **Domini** è destinato all’istanza Publish. Modifica l’URL dal valore predefinito `http://localhost:4503` nell’istanza Publish pubblicamente disponibile.

   ![Configurazione di Externalizer](assets/acc-externalizer-config.png)

1. Fai clic su **Salva**.

Dopo aver configurato Externalizer, Adobe Campaign può accedere al contenuto.

>[!NOTE]
>
L’istanza di pubblicazione deve essere raggiungibile dal server Adobe Campaign. Se punta a `localhost:4503` oppure in un altro server che Adobe Campaign non è in grado di raggiungere, le immagini provenienti dall’AEM non vengono visualizzate nella console Adobe Campaign.

## Configurare l’utente remoto di Campaign in AEM {#configure-user}

Per consentire a Campaign di comunicare con AEM, devi impostare una password per l’utente `campaign-remote` in AEM.

1. Accedi ad AEM come amministratore.
1. Nella console di navigazione principale, fai clic su **Strumenti** nella barra a sinistra.
1. Quindi fai clic su **Sicurezza** > **Utenti** per aprire la console di amministrazione degli utenti.
1. Individua l’utente `campaign-remote`.
1. Seleziona l’utente `campaign-remote` e fai clic su **Proprietà** per modificarlo.
1. Nella finestra **Modifica impostazioni utente**, fai clic su **Cambia password**.
1. Fornisci una nuova password per l’utente, annota la password e conservala in un luogo sicuro per utilizzarla in futuro.
1. Fai clic su **Salva** per salvare il cambiamento della password.
1. Fai clic su **Salva e chiudi** per salvare le modifiche apportate all’utente `campaign-remote`.

## Configurare l’account esterno dell’AEM in Campaign {#acc-setup}

Durante l’[installazione del pacchetto di **Integrazione di AEM** in Campaign,](#install-package) viene creato un account esterno per AEM. Configurando questo account esterno, Adobe Campaign può connettersi all’AEM, abilitando la comunicazione bidirezionale tra le soluzioni.

1. Accedi ad Adobe Campaign come amministratore utilizzando la console client.

1. Seleziona **Strumenti** > **Esplora** dalla barra dei menu.

1. In Esplora, passa al nodo **Amministrazione** > **Piattaforma** > **Account esterni**.

   ![Account esterni](assets/external-accounts.png)

1. Individua l’account di AEM esterno. Per impostazione predefinita, tale account ha i seguenti valori:

   * **Tipo** - `AEM`
   * **Etichetta** - `AEM Instance`
   * **Nome interno** - `aemInstance`

1. Nella scheda **Generale** di questo account, inserisci le informazioni utente definite nel passaggio [Imposta password utente remoto di Campaign](#set-campaign-remote-password).

   * **Server**: l’indirizzo server di authoring di AEM
      * Il server di authoring di AEM deve essere raggiungibile dall’stanza del server di Adobe Campaign Classic.
      * Verificare che l’indirizzo del server **non** termini con una barra finale.
   * **Account**: per impostazione predefinita, rappresenta  l’utente `campaign-remote` che hai impostato in AEM nel passaggio [Imposta password utente remoto di Campaign](#set-campaign-remote-password).
   * **Password**: questa password è la stessa `campaign-remote` dell’utente che hai impostato in AEM nel passaggio [Imposta password utente remoto di Campaign](#set-campaign-remote-password).

1. Seleziona la casella di controllo **Abilitato**.

1. Fai clic su **Salva**.

Adobe Campaign adesso può comunicare con AEM.

## Passaggi successivi {#next-steps}

Con Adobe Campaign Classic e AEM configurati, l’integrazione è ora completa.

Per scoprire come creare una newsletter in Adobe Experience Manager, prosegui con [il presente documento.](/help/sites-authoring/campaign.md)
