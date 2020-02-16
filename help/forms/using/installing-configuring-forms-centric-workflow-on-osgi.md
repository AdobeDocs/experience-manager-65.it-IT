---
title: Installazione e configurazione di un flusso di lavoro incentrato sui moduli in OSGi
seo-title: Installazione e configurazione di un flusso di lavoro incentrato sui moduli in OSGi
description: Installate e configurate le comunicazioni interattive di AEM Forms per creare corrispondenze aziendali, documenti, dichiarazioni, note sui vantaggi, e-mail di marketing, fatture e kit di benvenuto.
seo-description: Installate e configurate le comunicazioni interattive di AEM Forms per creare corrispondenze aziendali, documenti, dichiarazioni, note sui vantaggi, e-mail di marketing, fatture e kit di benvenuto.
uuid: 1ceae822-215a-4b83-a562-4609a09c3a54
topic-tags: installing
discoiquuid: de292a19-07db-4ed3-b13a-7a2f1cd9e0dd
docset: aem65
translation-type: tm+mt
source-git-commit: 3226edb575de3d9f8bff53f5ca81e2957f37c544

---


# Installazione e configurazione di un flusso di lavoro incentrato sui moduli in OSGi{#installing-and-configuring-forms-centric-workflow-on-osgi}

## Introduzione {#introduction}

Le aziende raccolgono ed elaborano dati da più moduli, sistemi back-end e altre origini dati. L&#39;elaborazione dei dati comporta procedure di revisione e approvazione, attività ripetitive e archiviazione dei dati. Ad esempio, rivedere un modulo e convertirlo in documento PDF. Se eseguite manualmente, le attività ripetitive possono richiedere molto tempo e risorse.

È possibile utilizzare il flusso di lavoro basato su [Forms su OSGi](../../forms/using/aem-forms-workflow.md) per creare rapidamente flussi di lavoro basati su moduli adattivi. Questi flussi di lavoro possono aiutarti ad automatizzare flussi di lavoro di revisione e approvazione, flussi di lavoro dei processi aziendali e altre attività ripetitive. Questi flussi di lavoro consentono inoltre di elaborare documenti (creare, assemblare, distribuire e archiviare documenti PDF, aggiungere firme digitali per limitare l&#39;accesso ai documenti, decodificare moduli con codice a barre e altro ancora) e utilizzare il flusso di lavoro di firma Adobe Sign con moduli e documenti.

Una volta configurati, questi flussi di lavoro possono essere attivati manualmente per completare un processo definito o eseguiti a livello di programmazione quando gli utenti inviano un modulo o una comunicazione interattiva. Questa funzionalità è inclusa nel pacchetto del componente aggiuntivo AEM Forms.

AEM Forms è una potente piattaforma aziendale. Il flusso di lavoro incentrato sui moduli in OSGi è solo una delle funzionalità di AEM Forms. Per un elenco completo delle funzionalità, consultate [Introduzione ai moduli](../../forms/using/introduction-aem-forms.md)AEM.

>[!NOTE]
>
>Con il flusso di lavoro basato su Forms su OSGi, potete creare e implementare rapidamente flussi di lavoro per varie attività nello stack OSGi, senza dover installare la funzionalità di Process Management completa nello stack JEE. Per informazioni sulle differenze e le similarità tra le funzionalità, vedi un [confronto](../../forms/using/capabilities-osgi-jee-workflows.md) dei flussi di lavoro AEM incentrati sui moduli in OSGi e Gestione dei processi in JEE.
>
>Dopo il confronto, se scegliete di installare la funzionalità Process Management sullo stack JEE, consultate [Installare o aggiornare AEM Forms su JEE](/help/forms/home.md) per informazioni dettagliate sull&#39;installazione e la configurazione dello stack JEE e delle funzionalità di Process Management.

## Topologia di distribuzione {#deployment-topology}

Il pacchetto del componente aggiuntivo AEM Forms è un&#39;applicazione implementata in AEM. Per eseguire il flusso di lavoro incentrato sui moduli in base alla funzionalità OSGi, è necessario solo un&#39;istanza di AEM Author o Processing (autore di produzione).  Un&#39;istanza di elaborazione è un&#39;istanza AEM Author [protetta](/help/forms/using/hardening-securing-aem-forms-environment.md) . Non eseguite operazioni di authoring effettive, ad esempio la creazione di flussi di lavoro o moduli adattivi, sull’autore della produzione.

La topologia seguente è indicativa per eseguire le comunicazioni interattive di AEM Forms, la gestione della corrispondenza, l’acquisizione dei dati di AEM Forms e il flusso di lavoro incentrato sui moduli sulle funzionalità OSGi. Per informazioni dettagliate sulla topologia, consultate Topologie di [architettura e distribuzione per AEM Forms](/help/forms/using/aem-forms-architecture-deployment.md).

![topologia consigliata](assets/recommended-topology.png)

Il flusso di lavoro incentrato sui moduli AEM su OSGi esegue l’interfaccia utente per la creazione di inbox AEM e modelli di flussi di lavoro AEM sulle istanze Author di AEM Forms.

## Requisiti di sistema {#system-requirements}

>[!NOTE]
>
>Passate alla sezione Passaggi [](../../forms/using/installing-configuring-forms-centric-workflow-on-osgi.md#next-steps) successivi del documento, se avete già installato AEM Forms su OSGi come illustrato nell&#39;articolo [Installazione e configurazione delle funzionalità](../../forms/using/installing-configuring-aem-forms-osgi.md) di acquisizione dei dati.

Prima di iniziare a installare e configurare il flusso di lavoro incentrato su Forms in OSGi, assicurarsi che:

* L&#39;infrastruttura hardware e software è già in funzione. Per un elenco dettagliato di hardware e software supportati, consultate i requisiti [tecnici](/help/sites-deploying/technical-requirements.md).

* Il percorso di installazione dell’istanza AEM non contiene spazi bianchi.
* Un’istanza di AEM è attiva e in esecuzione. Nella terminologia di AEM, un’istanza è una copia di AEM in esecuzione su un server in modalità di creazione o pubblicazione. Per eseguire il flusso di lavoro incentrato sui moduli in OSGi è necessaria almeno un’istanza di AEM (Author o Processing):

   * **Autore**: Un’istanza di AEM utilizzata per creare, caricare e modificare i contenuti e per amministrare il sito Web. Quando il contenuto è pronto per essere live, viene replicato nell’istanza di pubblicazione.
   * **** Elaborazione: Un&#39;istanza di elaborazione è un&#39;istanza AEM Author [protetta](/help/forms/using/hardening-securing-aem-forms-environment.md) . Potete impostare un&#39;istanza Author e renderla più indurita dopo l&#39;installazione.

   * **Pubblica**: Un’istanza di AEM che trasmette il contenuto pubblicato al pubblico su Internet o su una rete interna.

* I requisiti di memoria sono soddisfatti. Il pacchetto del componente aggiuntivo AEM Forms richiede:

   * 15 GB di spazio temporaneo per le installazioni basate su Microsoft Windows.
   * 6 GB di spazio temporaneo per le installazioni basate su UNIX.

* Requisiti aggiuntivi per i sistemi basati su UNIX: Se si utilizza il sistema operativo basato su UNIX, installare i pacchetti seguenti dal supporto di installazione del sistema operativo corrispondente.

<table>
 <tbody>
  <tr>
   <td>espatriato</td>
   <td>libxcb</td>
   <td>freetype</td>
   <td>libXau</td>
  </tr>
  <tr>
   <td>libSM</td>
   <td>zlib</td>
   <td>libICE</td>
   <td>libuuid</td>
  </tr>
  <tr>
   <td>glibc</td>
   <td>libXext</td>
   <td><p>nss-softokn-freebl</p> </td>
   <td>fontconfig</td>
  </tr>
  <tr>
   <td>libX11</td>
   <td>libXrendering</td>
   <td>libXrandr</td>
   <td>libXinerama</td>
  </tr>
 </tbody>
</table>

## Install AEM Forms add-on package {#install-aem-forms-add-on-package}

Il pacchetto del componente aggiuntivo AEM Forms è un&#39;applicazione implementata in AEM. Il pacchetto contiene un flusso di lavoro incentrato su Forms su OSGi e altre funzionalità. Effettuate le seguenti operazioni per installare il pacchetto del componente aggiuntivo:

1. Accedete al server [](https://localhost:4502) AEM come amministratore e aprite la condivisione [dei](https://localhost:4502/crx/packageshare)pacchetti. È necessario un Adobe ID per accedere alla condivisione del pacchetto.
1. In [AEM Package Share](https://localhost:4502/crx/packageshare/login.html)(Condivisione **pacchetti AEM), cercate i pacchetti aggiuntivi** AEM 6.5 Forms **o gli** ultimi service pack **, fate clic sul pacchetto applicabile al sistema operativo in uso e fate clic su** Scarica. Leggere e accettare il contratto di licenza e fare clic su **OK**. Il download viene avviato. Una volta scaricata, accanto al pacchetto viene visualizzata la parola **Download** .

   Potete anche usare il numero di versione per cercare un pacchetto aggiuntivo. Per il numero di versione dell&#39;ultimo pacchetto, consultate l&#39;articolo sulle versioni [di](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) AEM Forms.

1. Al termine del download, fate clic su **Scaricato**. Viene reindirizzato a Gestione pacchetti. In Gestione pacchetti, eseguite una ricerca nel pacchetto scaricato e fate clic su **Installa**.

   Se scaricate manualmente il pacchetto tramite il collegamento diretto elencato nell&#39;articolo delle release [di](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) AEM Forms, accedete a Gestione pacchetti, fate clic su **Carica pacchetto**, selezionate il pacchetto scaricato e fate clic su Carica. Dopo aver caricato il pacchetto, fate clic sul nome del pacchetto e fate clic su **Installa.**

1. Dopo l&#39;installazione del pacchetto, viene richiesto di riavviare l&#39;istanza AEM. **Non riavviare immediatamente il server.** Prima di arrestare il server AEM Forms, attendete che i messaggi ServiceEvent REGISTERED e ServiceEvent UNREGISTERED non vengano più visualizzati nel file [AEM-Installation-Directory]/crx-quickstart/logs/error.log e il registro sia stabile.
1. Ripetete i passaggi da 1 a 4 su tutte le istanze Author e Publish.

## Configurazioni post-installazione {#post-installation-configurations}

In AEM Forms sono disponibili alcune configurazioni obbligatorie e facoltative. Le configurazioni obbligatorie includono la configurazione delle librerie BouncyCastle e dell&#39;agente di serializzazione. Le configurazioni facoltative includono la configurazione del dispatcher e di Adobe Target.

### Configurazioni post-installazione obbligatorie {#mandatory-post-installation-configurations}

#### Configurare le librerie RSA e BouncyCastle {#configure-rsa-and-bouncycastle-libraries}

Per avviare la delega delle librerie, eseguite i seguenti passaggi su tutte le istanze Autore e Pubblica:

1. Interrompi l’istanza AEM sottostante.
1. Aprite il file [\crx-quickstart\conf\sling.properties della directory]di installazione di AEM per la modifica.

   Se avete utilizzato la directory [di installazione di]AEM [\crx-quickstart\bin\start.bat per avviare AEM, modificate le proprietà sling.properties ubicate in]AEM_root\crx-quickstart\.

1. Aggiungete le seguenti proprietà al file sling.properties:

   ```
   sling.bootdelegation.class.com.rsa.jsafe.provider.JsafeJCE=com.rsa.*
   sling.bootdelegation.class.org.bouncycastle.jce.provider.BouncyCastleProvider=org.bouncycastle.*
   ```

1. Salvate e chiudete il file e avviate l’istanza di AEM.
1. Ripetete i passaggi da 1 a 4 su tutte le istanze Author e Publish.

#### Configurare l’agente di serializzazione {#configure-the-serialization-agent}

Per inserire nella whitelist il pacchetto, eseguite i seguenti passaggi su tutte le istanze Author e Publish:

1. Aprite AEM Configuration Manager in una finestra del browser. L’URL predefinito è https://[server]:[port]/system/console/configMgr.
1. Cerca e apri la configurazione **del firewall di** deserializzazione.
1. Aggiungete il pacchetto **sun.util.Calendar** al campo **whitelist** . Fate clic su Salva.
1. Ripetete i passaggi da 1 a 3 su tutte le istanze Author e Publish.

### Configurazioni di post-installazione facoltative {#optional-post-installation-configurations}

#### Configura dispatcher {#configure-dispatcher}

Dispatcher: strumento di caching e bilanciamento del carico per AEM. AEM Dispatcher aiuta anche a proteggere il server AEM dagli attacchi. Puoi aumentare la sicurezza dell’istanza AEM utilizzando il dispatcher insieme a un server Web di classe enterprise. Se utilizzate [Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html), eseguite le seguenti configurazioni per AEM Forms:

1. Configurare l&#39;accesso ai moduli AEM:

   Aprire il file dispatcher.any per la modifica. Andate alla sezione del filtro e aggiungete il seguente filtro alla sezione del filtro:

   `/0025 { /type "allow" /glob "* /bin/xfaforms/submitaction*" } # to enable AEM Forms submission`

   Salvate e chiudete il file. Per informazioni dettagliate sui filtri, consultate la documentazione [del](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html)dispatcher.

1. Configurare il servizio filtro di riferimento:

   Accedete al gestore di configurazione Apache Felix come amministratore. L’URL predefinito del gestore di configurazione è https://[server]:[port_number]/system/console/configMgr. Nel menu **Configurazioni** , selezionate l&#39;opzione Filtro **di riferimento** Apache Sling. Nel campo Consenti ospitanti, immettete il nome host del dispatcher per consentirlo come referente e fate clic su **Salva**. Il formato della voce è `https://[server]:[port]`.

#### Configura cache {#configure-cache}

La cache è un meccanismo per ridurre i tempi di accesso ai dati, ridurre la latenza e migliorare le velocità di ingresso/uscita (I/O). La cache dei moduli adattivi memorizza solo il contenuto HTML e la struttura JSON di un modulo adattivo senza salvare i dati precompilati. Consente di ridurre il tempo necessario per il rendering di un modulo adattivo.

* Utilizzando la cache dei moduli adattivi, utilizzate il dispatcher [AEM](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html) per memorizzare nella cache le librerie client (CSS e JavaScript) di un modulo adattivo.
* Durante lo sviluppo di componenti personalizzati, mantenere disattivata la cache dei moduli adattivi sul server utilizzato per lo sviluppo.

Per configurare la cache dei moduli adattivi, effettuate le seguenti operazioni:

1. Andate al gestore di configurazione della console Web AEM all&#39;indirizzo `https://[server]:[port]/system/console/configMgr`.
1. Fare clic su Servizio **configurazione modulo** adattivo per modificare i valori di configurazione. Nella finestra di dialogo Modifica valori di configurazione, specificare il numero massimo di moduli o documenti che un’istanza del server AEM Forms può memorizzare nella cache nel campo **Numero di moduli** adattivi. Il valore predefinito è 100. Fai clic su **Salva**.

   >[!NOTE]
   >
   >Per disabilitare la cache, impostare il valore nel campo Numero di moduli adattivi su **0**. La cache viene reimpostata e tutti i moduli e i documenti vengono rimossi dalla cache quando si disabilita o si modifica la configurazione della cache.

#### Configurare Adobe Sign {#configure-adobe-sign}

Adobe Sign consente flussi di lavoro di firma elettronica per i moduli adattivi. Le firme elettroniche migliorano i flussi di lavoro per l&#39;elaborazione di documenti per scopi legali, di vendita, di retribuzione, di gestione delle risorse umane e per molte altre aree.

In uno scenario OSGi con un flusso di lavoro tipico basato su Adobe Sign e Forms, un utente compila un modulo adattivo da **richiedere per un servizio**. Ad esempio, un&#39;applicazione con carta di credito e un benefit per i cittadini vengono modulo. Quando un utente compila, invia e firma il modulo di richiesta, viene avviato un flusso di lavoro di approvazione/rifiuto. Il provider di servizi controlla l’applicazione in AEM Inbox e utilizza Adobe Sign per firmare elettronicamente l’applicazione. Per abilitare flussi di lavoro di firma elettronica simili, è possibile integrare Adobe Sign con AEM Forms.

Per utilizzare Adobe Sign con AEM Forms, [integrare Adobe Sign con AEM Forms](../../forms/using/adobe-sign-integration-adaptive-forms.md).

## Passaggi successivi {#next-steps}

È stato configurato un ambiente per l’utilizzo di un flusso di lavoro incentrato su Forms sulle funzionalità OSGi. Ora, i passi verso l&#39;utilizzo della funzionalità sono:

* [Utilizzo di un flusso di lavoro basato su moduli in OSGi](../../forms/using/aem-forms-workflow.md)
* [Riferimento passo flusso di lavoro](/help/sites-developing/workflows-step-ref.md)
* [Post-elaborazione di lettere e comunicazioni interattive](../../forms/using/submit-letter-topostprocess.md)

