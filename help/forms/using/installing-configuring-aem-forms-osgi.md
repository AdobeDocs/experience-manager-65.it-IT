---
title: Installare e configurare le funzionalità di acquisizione dati
seo-title: Installare e configurare le funzionalità di acquisizione dati
description: Installa e configura moduli adattivi, PDF forms e Forms HTML5. Configura Adobe Analytics e Adobe Target per i moduli adattivi per analizzare l’utilizzo dei moduli e indirizzare l’attività agli utenti in base al loro profilo.
seo-description: Installa e configura moduli adattivi, PDF forms e Forms HTML5. Configura Adobe Analytics e Adobe Target per i moduli adattivi per analizzare l’utilizzo dei moduli e indirizzare l’attività agli utenti in base al loro profilo.
uuid: 5d49032a-4dea-4f21-9dad-a7a30c5872ea
topic-tags: installing
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: dfc473eb-6091-4f5d-a5a0-789972c513a9
docset: aem65
role: Administrator
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1911'
ht-degree: 4%

---


# Installare e configurare le funzionalità di acquisizione dati{#install-and-configure-data-capture-capabilities}

## Introduzione {#introduction}

AEM Forms fornisce un set di moduli per ottenere i dati dall’utente finale: moduli adattivi, Forms HTML5 e PDF forms. Fornisce inoltre gli strumenti per elencare tutti i moduli disponibili su una pagina web, analizzare l’utilizzo dei moduli e indirizzare l’attività agli utenti in base al loro profilo. Queste funzionalità sono incluse nel pacchetto aggiuntivo di AEM Forms. Il pacchetto aggiuntivo viene distribuito su un’istanza di AEM Author o Publish di .

**Moduli adattivi:** questi moduli cambiano aspetto in base alle dimensioni dello schermo del dispositivo, sono interattivi e coinvolgenti. Adaptive Forms può anche integrarsi con Adobe Analytics, Adobe Sign e Adobe Target. Consente di fornire moduli personalizzati ed esperienze orientate ai processi agli utenti in base alla loro demografia e ad altre funzioni. È inoltre possibile integrare moduli adattivi con Adobe Sign.

**I** moduli PDF sono adatti per la stampa perfetta in pixel e l’acquisizione di informazioni digitali all’interno di un documento PDF. Nell’avatar digitale è possibile utilizzare Adobe Acrobat o Acrobat Reader per compilare i moduli. È possibile ospitare questi moduli sul sito Web o utilizzare il portale dei moduli per elencarli su un sito AEM. È inoltre possibile inviare questi moduli ad altri utenti tramite e-mail come allegati. Questi moduli sono particolarmente adatti per gli ambienti desktop.

**I moduli HTML5** sono versioni dei PDF forms compatibili con il browser. HTML5 Forms è adatto per ambienti che non supportano plug-in PDF. HTML5 Forms consente il rendering di moduli basati su XFA su dispositivi mobili e browser desktop su cui non è supportato il PDF basato su XFA. Questi moduli sono particolarmente adatti per tablet e ambienti desktop.

AEM Forms è una potente piattaforma di classe enterprise e l’acquisizione dei dati (moduli adattivi, PDF forms e HTML5 Forms) è solo una delle funzionalità di AEM Forms. Per l&#39;elenco completo delle funzionalità, consulta [Introduzione ad AEM Forms](/help/forms/using/introduction-aem-forms.md).

## Topologia di distribuzione {#deployment-topology}

Il pacchetto aggiuntivo di AEM Forms è un&#39;applicazione distribuita su AEM. Per eseguire le funzionalità di acquisizione dati di AEM Forms è necessaria solo un’istanza di AEM Author e AEM Publish . Per eseguire le funzionalità di acquisizione dati di AEM Forms AEM Forms, si consiglia la seguente topologia. Per informazioni dettagliate sulla topologia, consulta [Architettura e topologie di distribuzione per AEM Forms](/help/forms/using/aem-forms-architecture-deployment.md).

![topologia consigliata](assets/recommended-topology.png)

## Requisiti di sistema {#system-requirements}

Prima di iniziare a installare e configurare la funzionalità di acquisizione dati di AEM Forms, assicurati che:

* L&#39;infrastruttura hardware e software è in funzione. Per un elenco dettagliato dell&#39;hardware e del software supportati, vedere [requisiti tecnici](/help/sites-deploying/technical-requirements.md).

* Il percorso di installazione dell&#39;istanza AEM non contiene spazi bianchi.
* Un&#39;istanza AEM è in esecuzione. Per gli utenti Windows, installa l&#39;istanza AEM in modalità elevata. Nella terminologia AEM, un&#39;istanza è una copia di AEM in esecuzione su un server in modalità di authoring o pubblicazione. Per eseguire le funzionalità di acquisizione dati di AEM Forms, è necessario disporre di almeno due istanze [AEM (un autore e una pubblicazione)](/help/sites-deploying/deploy.md):

   * **Autore**: Un’istanza AEM utilizzata per creare, caricare e modificare i contenuti e per amministrare il sito web. Quando il contenuto è pronto per essere live, viene replicato nell’istanza di pubblicazione.
   * **Pubblica**: Un&#39;istanza AEM che trasmette il contenuto pubblicato al pubblico tramite Internet o una rete interna.

* I requisiti di memoria sono soddisfatti. Il pacchetto aggiuntivo di AEM Forms richiede:

   * 15 GB di spazio temporaneo per le installazioni basate su Microsoft Windows.
   * 6 GB di spazio temporaneo per installazioni basate su UNIX.

* È impostata la replica e la replica inversa per le istanze di authoring e pubblicazione. Per ulteriori informazioni, vedere [Replica](/help/sites-deploying/replication.md).
* Per i sistemi basati su UNIX:

   * Installa i seguenti pacchetti a 32 bit dal supporto di installazione:

<table>
 <tbody>
  <tr>
   <td>espatriare</td>
   <td>fontconfig</td>
   <td>freetype</td>
   <td>glibc</td>
  </tr>
  <tr>
   <td>libcurl</td>
   <td>libICE</td>
   <td>libicu</td>
   <td>libSM</td>
  </tr>
  <tr>
   <td>libuuuid</td>
   <td>libX11</td>
   <td><p>libXau</p> </td>
   <td>libxcb</td>
  </tr>
  <tr>
   <td>libXext</td>
   <td>libXinerama</td>
   <td>libXrandr</td>
   <td>libXrender</td>
  </tr>
  <tr>
   <td>nss-softokn-freebl</td>
   <td>OpenSSL</td>
   <td>zlib</td>
   <td> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>* Se OpenSSL è già installato sul server, aggiornarlo alla versione più recente.
>* Crea i collegamenti simbolici libcurl.so, libcrypto.so e libssl.so che puntano rispettivamente alla versione più recente delle librerie libcurl, libcrypto e libssl.

>



* Installa il seguente pacchetto a 64 bit dal supporto di installazione:

   * libicu

## Installa il pacchetto aggiuntivo di AEM Forms {#install-aem-forms-add-on-package}

Il pacchetto aggiuntivo di AEM Forms è un&#39;applicazione distribuita su AEM. Il pacchetto contiene l’acquisizione di dati AEM Forms e altre funzionalità. Esegui i seguenti passaggi per installare il pacchetto aggiuntivo:

1. Apri [Software Distribution](https://experience.adobe.com/downloads). Per accedere a Software Distribution è necessario disporre di un Adobe ID.
1. Tocca **[!UICONTROL Adobe Experience Manager]** che si trova nel menu di intestazione.
1. Nella sezione **[!UICONTROL Filtri]** :
   1. Seleziona **[!UICONTROL Forms]** dall&#39;elenco a discesa **[!UICONTROL Soluzione]**.
   2. Seleziona la versione e digita il pacchetto. Puoi anche utilizzare l&#39;opzione **[!UICONTROL Download di ricerca]** per filtrare i risultati.
1. Tocca il nome del pacchetto applicabile al tuo sistema operativo, seleziona **[!UICONTROL Accetta termini EULA]** e tocca **[!UICONTROL Scarica]**.
1. Apri [Gestione pacchetti](https://docs.adobe.com/content/help/it/experience-manager-65/administering/contentmanagement/package-manager.html) e fai clic su **[!UICONTROL Carica pacchetto]** per caricarlo.
1. Seleziona il pacchetto e fai clic su **[!UICONTROL Installa]**.

   Puoi anche scaricare il pacchetto tramite il collegamento diretto elencato nell&#39;articolo [Versioni di AEM Forms](https://helpx.adobe.com/it/aem-forms/kb/aem-forms-releases.html) .
1. Una volta installato il pacchetto, viene richiesto di riavviare l&#39;istanza AEM. **Non riavviare immediatamente il server.** Prima di arrestare il server AEM Forms, attendere che i messaggi ServiceEvent REGISTERED e ServiceEvent UNREGISTERED smettano di apparire nel  `[AEM-Installation-Directory]/crx-quickstart/logs/error.log` file e il registro sia stabile.
1. Ripeti i passaggi da 1 a 7 su tutte le istanze Author e Publish.

### Installazione automatica dei componenti ridistribuibili di Visual Studio {#automatic-installation-visual-studio-redistributables}

Se si installa un&#39;istanza AEM in modalità elevata, i ridistribuibili di Visual Studio mancanti vengono installati automaticamente durante l&#39;installazione del pacchetto aggiuntivo AEM Forms.

Per valutare se i ridistribuibili di Visual Studio sono installati automaticamente, aprire il file `error.log` disponibile nella directory `/crx-repository/logs/`. I registri includono il seguente messaggio:

`Redist <service name> already installed on system, will not attempt re-installation`

Se l&#39;installazione dei file ridistribuibili non riesce, i registri includono il seguente messaggio:

`Current user does not have elevated privileges, aborting installation of redist <service name>`

Per risolvere il problema, riavviare il server AEM, installare AEM in modalità elevata, quindi installare il pacchetto aggiuntivo AEM Forms.

Se il controllo dei privilegi non riesce, i log includono il seguente messaggio:

`Privilege escalation check failed with error: <error message>`

## Configurazioni post-installazione {#post-installation-configurations}

AEM Forms dispone di alcune configurazioni obbligatorie e facoltative. Le configurazioni obbligatorie includono la configurazione delle librerie BouncyCastle e dell&#39;agente di serializzazione. Le configurazioni facoltative includono la configurazione di dispatcher, Forms portal, Adobe Sign, Adobe Analytics e Adobe Target.

### Configurazioni obbligatorie post-installazione {#mandatory-post-installation-configurations}

#### Configurare le librerie RSA e BouncyCastle {#configure-rsa-and-bouncycastle-libraries}

Esegui i seguenti passaggi su tutte le istanze Author e Publish per avviare la delega delle librerie:

1. Interrompi l&#39;istanza AEM sottostante.
1. Apri il file `[AEM installation directory]\crx-quickstart\conf\sling.properties` per la modifica.

   Se hai utilizzato `[AEM installation directory]\crx-quickstart\bin\start.bat` per avviare AEM, modifica le proprietà sling.properties che si trovano in `[AEM_root]\crx-quickstart\`.

1. Aggiungi le seguenti proprietà al file sling.properties :

   ```shell
   sling.bootdelegation.class.com.rsa.jsafe.provider.JsafeJCE=com.rsa.*  
   ```

1. Salva e chiudi il file e avvia l’istanza AEM.
1. Ripeti i passaggi 1-4 su tutte le istanze Author e Publish.

#### Configura l&#39;agente di serializzazione {#configure-the-serialization-agent}

Esegui i seguenti passaggi su tutte le istanze Author e Publish per aggiungere il pacchetto all’inserire nell&#39;elenco Consentiti:

1. Apri AEM Configuration Manager in una finestra del browser. L’URL predefinito è `https://'[server]:[port]'/system/console/configMgr`.
1. Cerca **com.adobe.cq.deserfw.impl.DeserializationFirewallImpl.name** e apri la configurazione.
1. Aggiungi il pacchetto **sun.util.calendar** al campo **inserire nell&#39;elenco Consentiti** . Fai clic su **Salva**.
1. Ripeti i passaggi 1-3 su tutte le istanze Author e Publish.

### Configurazioni opzionali post-installazione {#optional-post-installation-configurations}

#### Configurare il Dispatcher {#configure-dispatcher}

Dispatcher è uno strumento di caching e/o bilanciamento del carico Adobe Experience Manager che può essere utilizzato insieme a un server web di classe enterprise. Se utilizzi [Dispatcher](https://helpx.adobe.com/it/experience-manager/dispatcher/using/dispatcher-configuration.html), esegui le seguenti configurazioni per AEM Forms:

1. Configura l’accesso per AEM Forms:

   Apri il file dispatcher.any per la modifica. Passa alla sezione filtro e aggiungi il seguente filtro alla sezione filtro :

   `/0025 { /type "allow" /glob "* /bin/xfaforms/submitaction*" } # to enable AEM Forms submission`

   Salva e chiudi il file. Per informazioni dettagliate sui filtri, consulta la [documentazione del Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html).

1. Configura il servizio filtro referrer:

   Accedi al gestore di configurazione Apache Felix come amministratore. L&#39;URL predefinito del gestore di configurazione è `https://[server]:[port_number]/system/console/configMgr`. Nel menu **Configurazioni**, seleziona l&#39;opzione **Filtro di riferimento Apache Sling** . Nel campo Consenti host , immetti il nome host del dispatcher per consentirlo come referrer e fai clic su **Salva**. Il formato della voce è &#39;https://[server]:[port]&#39;.

#### Configura la cache {#configure-cache}

La memorizzazione in cache è un meccanismo per ridurre i tempi di accesso ai dati, ridurre la latenza e migliorare le velocità di ingresso/uscita (I/O). La cache dei moduli adattivi memorizza solo il contenuto HTML e la struttura JSON di un modulo adattivo senza salvare dati precompilati. Consente di ridurre il tempo necessario per eseguire il rendering di un modulo adattivo.

* Quando utilizzi la cache dei moduli adattivi, utilizza il [AEM Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html) per memorizzare nella cache le librerie client (CSS e JavaScript) di un modulo adattivo.
* Durante lo sviluppo di componenti personalizzati, mantieni la cache dei moduli adattivi disabilitata sul server utilizzato per lo sviluppo.

Esegui i seguenti passaggi per configurare la cache dei moduli adattivi:

1. Vai AEM gestione della configurazione della console Web all&#39;indirizzo https://&#39;[server]:[port]&#39;/system/console/configMgr.
1. Fai clic su **Configurazione canale web per moduli adattivi e comunicazioni interattive** per modificare i relativi valori di configurazione. Nella finestra di dialogo modifica valori di configurazione, specifica il numero massimo di moduli o documenti che un’istanza del server AEM Forms può memorizzare nella cache nel campo **Number of Adaptive Forms** . Il valore predefinito è 100. Fai clic su **Salva**.

   >[!NOTE]
   >
   >Per disabilitare la cache, imposta il valore nel campo Numero di Forms adattivo su **0**. La cache viene reimpostata e tutti i moduli e i documenti vengono rimossi dalla cache quando si disabilita o si modifica la configurazione della cache.

#### Configurare la comunicazione SSL per il modello dati modulo {#configure-ssl-communcation-for-form-data-model}

È possibile abilitare la comunicazione SSL per il modello dati modulo. Per abilitare la comunicazione SSL per il modello dati modulo, prima di avviare un’istanza AEM Forms, aggiungi i certificati a Java Trust Store di tutte le istanze. Puoi eseguire il comando seguente per aggiungere i certificati: &quot;

`keytool -import -alias <alias-name> -file <pathTo .cer certificate file> -keystore <<pathToJRE>\lib\security\cacerts>`

#### Configurare Adobe Sign {#configure-adobe-sign}

Adobe Sign abilita i flussi di lavoro di firma elettronica per i moduli adattivi. Le firme elettroniche migliorano i flussi di lavoro per elaborare documenti per scopi legali, di vendita, di retribuzione, di gestione delle risorse umane e molte altre aree.

In un tipico scenario di Adobe Sign e moduli adattivi, un utente compila un modulo adattivo per **richiedere un servizio**. Ad esempio, un&#39;applicazione con carta di credito e un modulo di benefit per i cittadini. Quando un utente compila, invia e firma il modulo di applicazione, il modulo viene inviato al provider di servizi per ulteriori azioni. Il fornitore di servizi esamina l&#39;applicazione e utilizza Adobe Sign per contrassegnare l&#39;applicazione approvata. Per abilitare flussi di lavoro con firma elettronica simili, è possibile integrare Adobe Sign con AEM Forms.

Per utilizzare Adobe Sign con AEM Forms, [Integra Adobe Sign con AEM Forms](/help/forms/using/adobe-sign-integration-adaptive-forms.md).

#### Configurare Adobe Analytics {#configure-adobe-analytics}

AEM Forms si integra con Adobe Analytics per acquisire e monitorare le metriche delle prestazioni dei moduli e dei documenti pubblicati. L’analisi di queste metriche ha lo scopo di prendere decisioni informate basate sui dati necessari per rendere i moduli o i documenti più utilizzabili.

Per utilizzare Adobe Analytics con AEM Forms, consulta [Configurazione di analisi e rapporti](/help/forms/using/configure-analytics-forms-documents.md).

#### Integrare Adobe Target {#integrate-adobe-target}

È probabile che i clienti abbandonino un modulo se l’esperienza che offre non è coinvolgente. Anche se è frustrante per i clienti, può anche aumentare il volume di supporto e i costi per la tua organizzazione. È fondamentale e impegnativo identificare e fornire al cliente la giusta esperienza che aumenti il tasso di conversione. AEM forms rappresenta la chiave di questo problema.

AEM forms si integra con Adobe Target, una soluzione Adobe Marketing Cloud, per fornire esperienze cliente personalizzate e coinvolgenti su più canali digitali. Per utilizzare Adobe Target per testare i moduli adattivi A/B, [Integrare Adobe Target con AEM Forms](/help/forms/using/ab-testing-adaptive-forms.md#setupandintegratetargetinaemforms).

## Passaggi successivi {#next-steps}

Hai configurato un ambiente per utilizzare le funzionalità di acquisizione dati di AEM Forms. Ora, i passaggi successivi per utilizzare la funzionalità sono:

* [Creare il primo modulo adattivo](/help/forms/using/create-your-first-adaptive-form.md)
* [Creare il primo modulo PDF](http://www.adobe.com/go/learn_aemforms_designer_quick_start_65)
* [Introduzione a HTML5 Forms](/help/forms/using/introduction.md)

