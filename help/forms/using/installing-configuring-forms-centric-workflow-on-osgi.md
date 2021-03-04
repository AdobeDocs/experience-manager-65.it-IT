---
title: Installazione e configurazione del flusso di lavoro incentrato su Forms su OSGi
seo-title: Installazione e configurazione del flusso di lavoro incentrato su Forms su OSGi
description: Installa e configura le comunicazioni interattive di AEM Forms per creare corrispondenze aziendali, documenti, dichiarazioni, note sui benefit, e-mail di marketing, fatture e kit di benvenuto.
seo-description: Installa e configura le comunicazioni interattive di AEM Forms per creare corrispondenze aziendali, documenti, dichiarazioni, note sui benefit, e-mail di marketing, fatture e kit di benvenuto.
uuid: 1ceae822-215a-4b83-a562-4609a09c3a54
topic-tags: installing
discoiquuid: de292a19-07db-4ed3-b13a-7a2f1cd9e0dd
docset: aem65
translation-type: tm+mt
source-git-commit: 3690d2d76ce13064bd3946f4f6fea1a2759cdf37
workflow-type: tm+mt
source-wordcount: '1642'
ht-degree: 5%

---


# Installazione e configurazione del flusso di lavoro incentrato su Forms su OSGi{#installing-and-configuring-forms-centric-workflow-on-osgi}

## Introduzione {#introduction}

Le aziende raccolgono ed elaborano dati da più moduli, sistemi back-end e altre origini dati. Il trattamento dei dati comporta procedure di revisione e approvazione, attività ripetitive e archiviazione dei dati. Ad esempio, la revisione di un modulo e la sua conversione in documento PDF. Quando viene eseguito manualmente, le attività ripetitive possono richiedere molto tempo e risorse.

È possibile utilizzare [Flusso di lavoro incentrato sui moduli su OSGi](../../forms/using/aem-forms-workflow.md) per creare rapidamente flussi di lavoro basati su moduli adattivi. Questi flussi di lavoro consentono di automatizzare i flussi di lavoro di revisione e approvazione, i flussi di lavoro dei processi aziendali e altre attività ripetitive. Questi flussi di lavoro consentono inoltre di elaborare i documenti (creare, assemblare, distribuire e archiviare documenti PDF, aggiungere firme digitali per limitare l’accesso ai documenti, decodificare moduli con codice a barre e altro ancora) e utilizzare il flusso di lavoro Firma di Adobe Sign con moduli e documenti.

Una volta configurati, questi flussi di lavoro possono essere attivati manualmente per completare un processo definito o eseguiti a livello di programmazione quando gli utenti inviano un modulo o una comunicazione interattiva. La funzionalità è inclusa nel pacchetto aggiuntivo di AEM Forms.

AEM Forms è una potente piattaforma di classe enterprise. Il flusso di lavoro incentrato sui moduli su OSGi è solo una delle funzionalità di AEM Forms. Per l&#39;elenco completo delle funzionalità, consulta [Introduzione ad AEM Forms](introduction-aem-forms.md).

>[!NOTE]
>
>Con il flusso di lavoro incentrato su Forms su OSGi, puoi creare e distribuire rapidamente flussi di lavoro per varie attività sullo stack OSGi, senza dover installare la funzionalità di gestione dei processi completa sullo stack JEE. Per scoprire la differenza e le similarità tra le funzionalità, consulta un [confronto](capabilities-osgi-jee-workflows.md) dei flussi di lavoro AEM incentrati su Forms su OSGi e la gestione dei processi su JEE.
>
>Dopo il confronto, se scegli di installare la funzionalità Process Management sullo stack JEE, consulta [Installare o aggiornare AEM Forms su JEE](/help/forms/home.md) per informazioni dettagliate sull’installazione e la configurazione dello stack JEE e delle funzionalità di Process Management.

## Topologia di distribuzione {#deployment-topology}

Il pacchetto aggiuntivo di AEM Forms è un’applicazione implementata su AEM. Per eseguire il flusso di lavoro incentrato su Forms sulla funzionalità OSGi, è necessario solo un minimo di un’istanza di AEM Author o Processing (autore di produzione). Un&#39;istanza di elaborazione è un&#39;istanza di AEM Author](/help/forms/using/hardening-securing-aem-forms-environment.md) rigida. [ Non eseguire operazioni di authoring effettive, ad esempio la creazione di flussi di lavoro o moduli adattivi, sull’autore di produzione.

La topologia seguente è indicativa per eseguire le comunicazioni interattive di AEM Forms, la gestione della corrispondenza, l’acquisizione di dati di AEM Forms e il flusso di lavoro incentrato su Forms sulle funzionalità OSGi. Per informazioni dettagliate sulla topologia, consulta [Architettura e topologie di distribuzione per AEM Forms](/help/forms/using/aem-forms-architecture-deployment.md).

![topologia consigliata](assets/recommended-topology.png)

Il flusso di lavoro incentrato su AEM Forms su OSGi esegue la Casella in entrata AEM e l’interfaccia utente per la creazione di modelli di flussi di lavoro AEM sulle istanze di authoring di AEM Forms.

## Requisiti di sistema {#system-requirements}

>[!NOTE]
>
>Vai alla sezione [Passaggi successivi](../../forms/using/installing-configuring-forms-centric-workflow-on-osgi.md#next-steps) del documento, se hai già installato AEM Forms su OSGi come spiegato nell&#39;articolo [installare e configurare le funzionalità di acquisizione dati](../../forms/using/installing-configuring-aem-forms-osgi.md) .

Prima di iniziare a installare e configurare il flusso di lavoro incentrato su Forms su OSGi, assicurati che:

* L&#39;infrastruttura hardware e software è in funzione. Per un elenco dettagliato dell&#39;hardware e del software supportati, vedere [requisiti tecnici](/help/sites-deploying/technical-requirements.md).

* Il percorso di installazione dell’istanza AEM non contiene spazi bianchi.
* Un’istanza AEM è in esecuzione. Nella terminologia di AEM, un’istanza è una copia di AEM in esecuzione su un server in modalità di authoring o pubblicazione. Per eseguire un flusso di lavoro incentrato su Forms su OSGi, è necessaria almeno un’istanza AEM (Author or or Processing):

   * **Autore**: Un’istanza AEM utilizzata per creare, caricare e modificare i contenuti e per amministrare il sito web. Quando il contenuto è pronto per essere live, viene replicato nell’istanza di pubblicazione.
   * **Elaborazione:** un&#39;istanza di elaborazione è un&#39;istanza AEM  [Authoring ](/help/forms/using/hardening-securing-aem-forms-environment.md) rigida. È possibile impostare un&#39;istanza Author e renderla più rigida dopo l&#39;esecuzione dell&#39;installazione.

   * **Pubblica**: Un’istanza AEM che trasmette il contenuto pubblicato al pubblico tramite Internet o una rete interna.

* I requisiti di memoria sono soddisfatti. Il pacchetto aggiuntivo di AEM Forms richiede:

   * 15 GB di spazio temporaneo per le installazioni basate su Microsoft Windows.
   * 6 GB di spazio temporaneo per installazioni basate su UNIX.

* Requisiti aggiuntivi per i sistemi basati su UNIX: Se si utilizza il sistema operativo basato su UNIX, installare i seguenti pacchetti dal supporto di installazione del rispettivo sistema operativo.

<table>
 <tbody>
  <tr>
   <td>espatriare</td>
   <td>libxcb</td>
   <td>freetype</td>
   <td>libXau</td>
  </tr>
  <tr>
   <td>libSM</td>
   <td>zlib</td>
   <td>libICE</td>
   <td>libuuuid</td>
  </tr>
  <tr>
   <td>glibc</td>
   <td>libXext</td>
   <td><p>nss-softokn-freebl</p> </td>
   <td>fontconfig</td>
  </tr>
  <tr>
   <td>libX11</td>
   <td>libXrender</td>
   <td>libXrandr</td>
   <td>libXinerama</td>
  </tr>
 </tbody>
</table>

## Installa il pacchetto aggiuntivo di AEM Forms {#install-aem-forms-add-on-package}

Il pacchetto aggiuntivo di AEM Forms è un’applicazione implementata su AEM. Il pacchetto contiene un flusso di lavoro incentrato su Forms su OSGi e altre funzionalità. Esegui i seguenti passaggi per installare il pacchetto aggiuntivo:

1. Apri [Software Distribution](https://experience.adobe.com/downloads). Per accedere a Software Distribution è necessario disporre di un Adobe ID.
1. Tocca **[!UICONTROL Adobe Experience Manager]** che si trova nel menu di intestazione.
1. Nella sezione **[!UICONTROL Filtri]** :
   1. Seleziona **[!UICONTROL Moduli]** dall&#39;elenco a discesa **[!UICONTROL Soluzione]**.
   2. Seleziona la versione e digita il pacchetto. Puoi anche utilizzare l&#39;opzione **[!UICONTROL Download di ricerca]** per filtrare i risultati.
1. Tocca il nome del pacchetto applicabile al tuo sistema operativo, seleziona **[!UICONTROL Accetta termini EULA]** e tocca **[!UICONTROL Scarica]**.
1. Apri [Gestione pacchetti](https://docs.adobe.com/content/help/it/experience-manager-65/administering/contentmanagement/package-manager.html) e fai clic su **[!UICONTROL Carica pacchetto]** per caricarlo.
1. Seleziona il pacchetto e fai clic su **[!UICONTROL Installa]**.

   Puoi anche scaricare il pacchetto tramite il collegamento diretto elencato nell&#39;articolo [Versioni di AEM Forms](https://helpx.adobe.com/it/aem-forms/kb/aem-forms-releases.html) .

1. Una volta installato il pacchetto, viene richiesto di riavviare l&#39;istanza AEM. **Non riavviare immediatamente il server.** Prima di arrestare il server AEM Forms, attendi che i messaggi ServiceEvent REGISTERED e ServiceEvent UNREGISTERED smettano di essere visualizzati nel file  [AEM-Installation-Directory]/crx-quickstart/logs/error.log e il registro sia stabile.
1. Ripeti i passaggi da 1 a 7 su tutte le istanze Author e Publish.

## Configurazioni post-installazione {#post-installation-configurations}

AEM Forms dispone di alcune configurazioni obbligatorie e facoltative. Le configurazioni obbligatorie includono la configurazione delle librerie BouncyCastle e dell&#39;agente di serializzazione. Le configurazioni facoltative includono la configurazione del dispatcher e di Adobe Target.

### Configurazioni obbligatorie post-installazione {#mandatory-post-installation-configurations}

#### Configurare le librerie RSA e BouncyCastle {#configure-rsa-and-bouncycastle-libraries}

Esegui i seguenti passaggi su tutte le istanze Author e Publish per avviare la delega delle librerie:

1. Arresta l’istanza AEM sottostante.
1. Apri il file [directory di installazione di AEM]\crx-quickstart\conf\sling.properties per la modifica.

   Se hai utilizzato [la directory di installazione di AEM]\crx-quickstart\bin\start.bat per avviare AEM, modifica le proprietà sling.properties che si trovano in [AEM_root]\crx-quickstart\.

1. Aggiungi le seguenti proprietà al file sling.properties :

   ```shell
   sling.bootdelegation.class.com.rsa.jsafe.provider.JsafeJCE=com.rsa.*  
   ```

1. Salva e chiudi il file e avvia l’istanza AEM.
1. Ripeti i passaggi 1-4 su tutte le istanze Author e Publish.

#### Configura l&#39;agente di serializzazione {#configure-the-serialization-agent}

Esegui i seguenti passaggi su tutte le istanze Autore e Pubblica per aggiungere il pacchetto all’elenco Consentiti:

1. Apri AEM Configuration Manager in una finestra del browser. L&#39;URL predefinito è https://&#39;[server]:[port]&#39;/system/console/configMgr.
1. Cerca e apri **Configurazione firewall di deserializzazione**.
1. Aggiungi il pacchetto **sun.util.calendar** al campo **allowlist** . Fai clic su Salva.
1. Ripeti i passaggi 1-3 su tutte le istanze Author e Publish.

### Configurazioni opzionali post-installazione {#optional-post-installation-configurations}

#### Configurare il Dispatcher {#configure-dispatcher}

Dispatcher è lo strumento di caching e bilanciamento del carico per AEM. AEM Dispatcher aiuta anche a proteggere il server AEM dagli attacchi. Puoi aumentare la sicurezza dell’istanza AEM utilizzando Dispatcher insieme a un server web di classe enterprise. Se utilizzi [Dispatcher](https://helpx.adobe.com/it/experience-manager/dispatcher/using/dispatcher-configuration.html), esegui le seguenti configurazioni per AEM Forms:

1. Configura l’accesso per AEM Forms:

   Apri il file dispatcher.any per la modifica. Passa alla sezione filtro e aggiungi il seguente filtro alla sezione filtro :

   `/0025 { /type "allow" /glob "* /bin/xfaforms/submitaction*" } # to enable AEM Forms submission`

   Salva e chiudi il file. Per informazioni dettagliate sui filtri, consulta la [documentazione del Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html).

1. Configura il servizio filtro referrer:

   Accedi al gestore di configurazione Apache Felix come amministratore. L&#39;URL predefinito del gestore di configurazione è https://&#39;server&#39;:[port_number]/system/console/configMgr. Nel menu **Configurazioni**, seleziona l&#39;opzione **Filtro di riferimento Apache Sling** . Nel campo Consenti host , immetti il nome host del dispatcher per consentirlo come referrer e fai clic su **Salva**. Il formato della voce è `https://'[server]:[port]'`.

#### Configura la cache {#configure-cache}

La memorizzazione in cache è un meccanismo per ridurre i tempi di accesso ai dati, ridurre la latenza e migliorare le velocità di ingresso/uscita (I/O). La cache dei moduli adattivi memorizza solo il contenuto HTML e la struttura JSON di un modulo adattivo senza salvare dati precompilati. Consente di ridurre il tempo necessario per eseguire il rendering di un modulo adattivo.

* Quando utilizzi la cache dei moduli adattivi, utilizza [AEM Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html) per memorizzare nella cache le librerie client (CSS e JavaScript) di un modulo adattivo.
* Durante lo sviluppo di componenti personalizzati, mantieni la cache dei moduli adattivi disabilitata sul server utilizzato per lo sviluppo.

Esegui i seguenti passaggi per configurare la cache dei moduli adattivi:

1. Vai al gestore di configurazione della console web AEM all&#39;indirizzo `https://'[server]:[port]'/system/console/configMgr`.
1. Fai clic su **[!UICONTROL Configurazione canale web per moduli adattivi e comunicazioni interattive]** per modificare i relativi valori di configurazione. Nella finestra di dialogo modifica i valori di configurazione , specifica il numero massimo di moduli o documenti che un’istanza del server AEM Forms può memorizzare nella cache nel campo **Number of Adaptive Forms** . Il valore predefinito è 100. Fai clic su **Salva**.

   >[!NOTE]
   >
   >Per disabilitare la cache, imposta il valore nel campo Numero di moduli adattivi su **0**. La cache viene reimpostata e tutti i moduli e i documenti vengono rimossi dalla cache quando si disabilita o si modifica la configurazione della cache.

#### Configurare Adobe Sign {#configure-adobe-sign}

Adobe Sign abilita i flussi di lavoro di firma elettronica per i moduli adattivi. Le firme elettroniche migliorano i flussi di lavoro per elaborare documenti per scopi legali, di vendita, di retribuzione, di gestione delle risorse umane e molte altre aree.

In un tipico flusso di lavoro incentrato su Adobe Sign e Forms in uno scenario OSGi, un utente compila un modulo adattivo per **richiedere un servizio**. Ad esempio, un&#39;applicazione con carta di credito e un modulo di benefit per i cittadini. Quando un utente compila, invia e firma il modulo di applicazione, viene avviato un flusso di lavoro di approvazione/rifiuto. Il fornitore di servizi controlla l’applicazione in AEM Inbox e utilizza Adobe Sign per firmare elettronicamente l’applicazione. Per abilitare flussi di lavoro con firma elettronica simili, è possibile integrare Adobe Sign con AEM Forms.

Per utilizzare Adobe Sign con AEM Forms, [Integrare Adobe Sign con AEM Forms](../../forms/using/adobe-sign-integration-adaptive-forms.md).

## Passaggi successivi {#next-steps}

Hai configurato un ambiente per utilizzare un flusso di lavoro incentrato su Forms sulle funzionalità OSGi. Ora, i passaggi per utilizzare la funzionalità sono:

* [Utilizzo del flusso di lavoro incentrato su Forms su OSGi](../../forms/using/aem-forms-workflow.md)
* [Guida di riferimento per i passaggi dei flussi di lavoro](/help/sites-developing/workflows-step-ref.md)
* [Post-elaborazione di lettere e comunicazioni interattive](../../forms/using/submit-letter-topostprocess.md)

