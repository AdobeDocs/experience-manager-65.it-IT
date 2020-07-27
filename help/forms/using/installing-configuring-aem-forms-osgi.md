---
title: Installare e configurare le funzionalità di acquisizione dei dati
seo-title: Installare e configurare le funzionalità di acquisizione dei dati
description: Installare e configurare moduli adattivi, PDF forms e moduli HTML5. Configurare Adobe  Analytics e  Adobe Target per i moduli adattivi per analizzare l'uso dei moduli e indirizzare gli utenti in base al relativo profilo.
seo-description: Installare e configurare moduli adattivi, PDF forms e moduli HTML5. Configurare Adobe  Analytics e  Adobe Target per i moduli adattivi per analizzare l'uso dei moduli e indirizzare gli utenti in base al relativo profilo.
uuid: 5d49032a-4dea-4f21-9dad-a7a30c5872ea
topic-tags: installing
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: dfc473eb-6091-4f5d-a5a0-789972c513a9
docset: aem65
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '1817'
ht-degree: 1%

---


# Installare e configurare le funzionalità di acquisizione dei dati{#install-and-configure-data-capture-capabilities}

## Introduzione {#introduction}

I AEM Forms forniscono un set di moduli per ottenere i dati dall&#39;utente finale: moduli adattivi, moduli HTML5 e PDF forms. Fornisce inoltre strumenti per elencare tutti i moduli disponibili su una pagina Web, analizzare l’uso dei moduli e indirizzare gli utenti in base al relativo profilo. Queste funzionalità sono incluse nel pacchetto del componente aggiuntivo AEM Forms. Il pacchetto del componente aggiuntivo viene distribuito su un’istanza Author o Publish di AEM.

**Moduli adattivi:** Questi moduli modificano l&#39;aspetto in base alle dimensioni dello schermo del dispositivo, sono interattivi e coinvolgenti. I moduli adattivi possono essere integrati anche con Adobe  Analytics, Adobe Sign e  Adobe Target. Consentiva di distribuire moduli personalizzati ed esperienze orientate ai processi agli utenti in base alla loro demografia e ad altre funzioni. È inoltre possibile integrare moduli adattivi con Adobe Sign.

**I PDF forms** sono adatti per la stampa perfetta in pixel e l&#39;acquisizione di informazioni digitali all&#39;interno di un documento PDF. Nell&#39;avatar digitale è possibile utilizzare Adobe Acrobat o Acrobat Reader per compilare i moduli. È possibile ospitare tali moduli sul sito Web o utilizzare il portale dei moduli per elencarli in un sito AEM. È inoltre possibile inviare questi moduli ad altri come allegati. Questi moduli sono particolarmente adatti agli ambienti desktop.

**HTML5 Forms** è la versione semplice per il browser degli PDF forms. I moduli HTML5 sono adatti ad ambienti che non supportano i plug-in PDF. I moduli HTML5 consentono di eseguire il rendering dei moduli basati su XFA su dispositivi mobili e browser desktop sui quali non è supportato PDF basato su XFA. Questi moduli sono particolarmente adatti per tablet e ambienti desktop.

AEM Forms è una potente piattaforma di classe enterprise e l&#39;acquisizione dei dati (moduli adattivi, PDF forms e moduli HTML5) è solo una delle capacità dei AEM Forms. Per l&#39;elenco completo delle funzionalità, consultate [Introduzione ai AEM Forms](/help/forms/using/introduction-aem-forms.md).

## Topologia di distribuzione {#deployment-topology}

Il pacchetto aggiuntivo AEM Forms è un’applicazione distribuita in AEM. È necessario solo un minimo di un&#39;istanza AEM Author e AEM Publish per eseguire le funzionalità di acquisizione dei dati AEM Forms. Per eseguire le funzionalità di acquisizione dei dati dei AEM Forms AEM Forms, è consigliabile utilizzare la seguente topologia. Per informazioni dettagliate sulla topologia, consultate Topologie di [architettura e distribuzione per AEM Forms](/help/forms/using/aem-forms-architecture-deployment.md).

![topologia consigliata](assets/recommended-topology.png)

## Requisiti di sistema {#system-requirements}

Prima di iniziare a installare e configurare la funzionalità di acquisizione dei dati dei AEM Forms, accertati che:

* L&#39;infrastruttura hardware e software è già in funzione. Per un elenco dettagliato di hardware e software supportati, consultate i requisiti [tecnici](/help/sites-deploying/technical-requirements.md).

* Il percorso di installazione dell’istanza AEM non contiene spazi bianchi.
* Un’istanza di AEM è attiva e in esecuzione. Nella terminologia di AEM, per &quot;istanza&quot; si intende una copia di AEM in esecuzione su un server in modalità di creazione o pubblicazione. Per eseguire le funzionalità di acquisizione dei dati dei AEM Forms, sono necessarie almeno due istanze [AEM (Autore e Pubblicazione)](/help/sites-deploying/deploy.md) :

   * **Autore**: Un’istanza di AEM utilizzata per creare, caricare e modificare i contenuti e per amministrare il sito Web. Quando il contenuto è pronto per essere live, viene replicato nell’istanza di pubblicazione.
   * **Pubblica**: Un’istanza di AEM che trasmette il contenuto pubblicato al pubblico su Internet o su una rete interna.

* I requisiti di memoria sono soddisfatti. Il pacchetto del componente aggiuntivo AEM Forms richiede:

   * 15 GB di spazio temporaneo per le installazioni basate su Microsoft Windows.
   * 6 GB di spazio temporaneo per le installazioni basate su UNIX.

* È impostata la replica e la replica inversa per le istanze di creazione e pubblicazione. For details, see [Replication](/help/sites-deploying/replication.md).
* Per i sistemi basati su UNIX:

   * Installate i seguenti pacchetti a 32 bit dal supporto di installazione:

<table>
 <tbody>
  <tr>
   <td>espatriato</td>
   <td>fontconfig</td>
   <td>freetype</td>
   <td>glibc</td>
  </tr>
  <tr>
   <td>libricolo</td>
   <td>libICE</td>
   <td>libicu</td>
   <td>libSM</td>
  </tr>
  <tr>
   <td>libuuid</td>
   <td>libX11</td>
   <td><p>libXau</p> </td>
   <td>libxcb</td>
  </tr>
  <tr>
   <td>libXext</td>
   <td>libXinerama</td>
   <td>libXrandr</td>
   <td>libXrendering</td>
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
>* Create libcurl.so, libcrypto.so e libssl.so symlinks puntando rispettivamente alla versione più recente delle librerie libcurl, libcrypto e libssl.

>



* Installate il seguente pacchetto a 64 bit dal supporto di installazione:

   * libicu

## Install AEM Forms add-on package {#install-aem-forms-add-on-package}

Il pacchetto aggiuntivo AEM Forms è un’applicazione distribuita in AEM. Il pacchetto contiene l&#39;acquisizione dei dati AEM Forms e altre funzionalità. Effettuate le seguenti operazioni per installare il pacchetto del componente aggiuntivo:

1. Apri distribuzione [](https://experience.adobe.com/downloads)software. È necessario un Adobe ID  per accedere a Distribuzione software.
1. Toccate **[!UICONTROL Adobe Experience Manager]** disponibile nel menu dell&#39;intestazione.
1. Nella sezione **[!UICONTROL Filtri]** :
   1. Selezionare **[!UICONTROL Forms]** dall&#39;elenco a discesa **[!UICONTROL Soluzione]** .
   2. Selezionate la versione e digitate il tipo di pacchetto. Potete anche utilizzare l&#39;opzione Download **[!UICONTROL di]** ricerca per filtrare i risultati.
1. Toccate il nome del pacchetto applicabile al sistema operativo in uso, selezionate **[!UICONTROL Accetta termini]** EULA e toccate **[!UICONTROL Scarica]**.
1. Aprite [Package Manager](https://docs.adobe.com/content/help/en/experience-manager-65/administering/contentmanagement/package-manager.html) e fate clic su **[!UICONTROL Carica pacchetto]** per caricare il pacchetto.
1. Select the package and click **[!UICONTROL Install]**.

   Potete anche scaricare il pacchetto tramite il collegamento diretto elencato nell&#39;articolo delle release [](https://helpx.adobe.com/it/aem-forms/kb/aem-forms-releases.html) AEM Forms.
1. Dopo l&#39;installazione del pacchetto, viene richiesto di riavviare l&#39;istanza di AEM. **Non riavviare immediatamente il server.** Prima di arrestare il server AEM Forms, attendere che i messaggi ServiceEvent REGISTERED e ServiceEvent UNREGISTERED non vengano visualizzati nel `[AEM-Installation-Directory]/crx-quickstart/logs/error.log` file e il registro sia stabile.
1. Ripetete i passaggi da 1 a 7 su tutte le istanze Author e Publish.

## Configurazioni post-installazione {#post-installation-configurations}

I AEM Forms hanno alcune configurazioni obbligatorie e facoltative. Le configurazioni obbligatorie includono la configurazione delle librerie BouncyCastle e dell&#39;agente di serializzazione. Le configurazioni facoltative includono il dispatcher di configurazione, il portale Forms, Adobe Sign, Adobe  Analytics e  Adobe Target.

### Configurazioni post-installazione obbligatorie {#mandatory-post-installation-configurations}

#### Configurare le librerie RSA e BouncyCastle  {#configure-rsa-and-bouncycastle-libraries}

Per avviare la delega delle librerie, eseguite i seguenti passaggi su tutte le istanze Autore e Pubblica:

1. Interrompi l’istanza AEM sottostante.
1. Open the `[AEM installation directory]\crx-quickstart\conf\sling.properties` file for editing.

   Se avete iniziato `[AEM installation directory]\crx-quickstart\bin\start.bat` AEM, modificate le proprietà sling.properties che si trovano in `[AEM_root]\crx-quickstart\`.

1. Aggiungete le seguenti proprietà al file sling.properties:

   ```shell
   sling.bootdelegation.class.com.rsa.jsafe.provider.JsafeJCE=com.rsa.*
   sling.bootdelegation.class.org.bouncycastle.jce.provider.BouncyCastleProvider=org.bouncycastle.*
   ```

1. Salvate e chiudete il file e avviate l’istanza di AEM.
1. Ripetete i passaggi da 1 a 4 su tutte le istanze Author e Publish.

#### Configurare l’agente di serializzazione {#configure-the-serialization-agent}

Per aggiungere il pacchetto al inserire nell&#39;elenco Consentiti di , eseguite i seguenti passaggi su tutte le istanze Author e Publish:

1. Aprite AEM Configuration Manager in una finestra del browser. L’URL predefinito è `https://'[server]:[port]'/system/console/configMgr`.
1. Cercate **com.adobe.cq.deserfw.impl.DeserializationFirewallImpl.name** e aprite la configurazione.
1. Aggiungete il pacchetto **sun.util.Calendar** al campo di **inserire nell&#39;elenco Consentiti** . Fai clic su **Salva**.
1. Ripetete i passaggi da 1 a 3 su tutte le istanze Author e Publish.

### Configurazioni di post-installazione facoltative {#optional-post-installation-configurations}

#### Configurare Dispatcher {#configure-dispatcher}

Dispatcher è uno strumento per il caching e il bilanciamento del carico per AEM. AEM Dispatcher aiuta anche a proteggere il server AEM dagli attacchi. Puoi aumentare la sicurezza dell’istanza AEM utilizzando Dispatcher insieme a un server Web di classe enterprise. Se utilizzate [Dispatcher](https://helpx.adobe.com/it/experience-manager/dispatcher/using/dispatcher-configuration.html), eseguite le seguenti configurazioni per i AEM Forms:

1. Configurare l&#39;accesso per i AEM Forms:

   Aprire il file dispatcher.any per la modifica. Andate alla sezione del filtro e aggiungete il seguente filtro alla sezione del filtro:

   `/0025 { /type "allow" /glob "* /bin/xfaforms/submitaction*" } # to enable AEM Forms submission`

   Salvate e chiudete il file. Per informazioni dettagliate sui filtri, consultate la documentazione [](https://helpx.adobe.com/it/experience-manager/dispatcher/using/dispatcher-configuration.html)Dispatcher.

1. Configurare il servizio filtro di riferimento:

   Accedete al gestore di configurazione Apache Felix come amministratore. L&#39;URL predefinito del gestore di configurazione è `https://[server]:[port_number]/system/console/configMgr`. Nel menu **Configurazioni** , selezionate l&#39;opzione Filtro **di riferimento** Apache Sling. Nel campo Consenti ospitanti, immettete il nome host del dispatcher per consentirlo come referente e fate clic su **Salva**. Il formato della voce è `https://[server]:[port]&#39;.

#### Configura cache {#configure-cache}

La cache è un meccanismo per ridurre i tempi di accesso ai dati, ridurre la latenza e migliorare le velocità di ingresso/uscita (I/O). La cache dei moduli adattivi memorizza solo il contenuto HTML e la struttura JSON di un modulo adattivo senza salvare i dati precompilati. Consente di ridurre il tempo necessario per eseguire il rendering di un modulo adattivo.

* Utilizzando la cache dei moduli adattivi, utilizzare [AEM Dispatcher](https://helpx.adobe.com/it/experience-manager/dispatcher/using/dispatcher-configuration.html) per memorizzare nella cache le librerie client (CSS e JavaScript) di un modulo adattivo.
* Durante lo sviluppo di componenti personalizzati, mantenere disattivata la cache dei moduli adattivi sul server utilizzato per lo sviluppo.

Per configurare la cache dei moduli adattivi, effettuate le seguenti operazioni:

1. Andate al gestore di configurazione della console Web AEM all&#39;indirizzo https://&#39;[server]:[port]&#39;/system/console/configMgr.
1. Fate clic su Configurazione **canale Web per moduli** adattivi e comunicazioni interattive per modificarne i valori di configurazione. Nella finestra di dialogo Modifica valori di configurazione, specificare il numero massimo di moduli o documenti che un’istanza del server AEM Forms può memorizzare nella cache nel campo **Numero di moduli** adattivi. Il valore predefinito è 100. Fai clic su **Salva**.

   >[!NOTE]
   >
   >Per disabilitare la cache, impostare il valore nel campo Numero di moduli adattivi su **0**. La cache viene reimpostata e tutti i moduli e i documenti vengono rimossi dalla cache quando si disabilita o si modifica la configurazione della cache.

#### Configurare la comunicazione SSL per il modello dati del modulo {#configure-ssl-communcation-for-form-data-model}

È possibile abilitare la comunicazione SSL per il modello dati modulo. Per abilitare la comunicazione SSL per il modello dati del modulo, prima di avviare un&#39;istanza AEM Forms, aggiungere certificati a Java Trust Store per tutte le istanze. È possibile eseguire il comando seguente per aggiungere i certificati: &quot;

`keytool -import -alias <alias-name> -file <pathTo .cer certificate file> -keystore <<pathToJRE>\lib\security\cacerts>`

#### Configurare Adobe Sign {#configure-adobe-sign}

Adobe Sign consente flussi di lavoro di firma elettronica per i moduli adattivi. Le firme elettroniche migliorano i flussi di lavoro per l&#39;elaborazione di documenti per scopi legali, di vendita, di retribuzione, di gestione delle risorse umane e per molte altre aree.

In uno scenario di moduli adattivi e Adobe Sign tipico, l&#39;utente compila un modulo adattivo da **richiedere per un servizio**. Ad esempio, un&#39;applicazione con carta di credito e un benefit per i cittadini vengono modulo. Quando un utente compila, invia e firma il modulo di domanda, il modulo viene inviato al provider di servizi per ulteriori azioni. Il fornitore di servizi controlla l’applicazione e utilizza Adobe Sign per contrassegnare l’applicazione approvata. Per abilitare flussi di lavoro di firma elettronica simili, è possibile integrare Adobe Sign con i AEM Forms.

Per utilizzare Adobe Sign con i AEM Forms, [integrare Adobe Sign con i AEM Forms](/help/forms/using/adobe-sign-integration-adaptive-forms.md).

#### Configurare Adobe  Analytics {#configure-adobe-analytics}

AEM Forms si integra con Adobe  Analytics che consente di acquisire e tenere traccia delle metriche delle prestazioni per i moduli e i documenti pubblicati. L&#39;obiettivo dell&#39;analisi di queste metriche è di rendere più utilizzabili moduli o documenti con decisioni informate basate sui dati richiesti.

Per utilizzare Adobe  Analytics con AEM Forms, consultate [Configurazione di analisi e rapporti](/help/forms/using/configure-analytics-forms-documents.md).

#### Integrare  Adobe Target {#integrate-adobe-target}

È probabile che i clienti abbandonino un modulo se l&#39;esperienza non è coinvolgente. Anche se è frustrante per i clienti, può anche aumentare il volume e i costi del supporto per la vostra organizzazione. È fondamentale e difficile identificare e fornire al cliente la giusta esperienza che aumenta il tasso di conversione. I moduli AEM rappresentano la chiave di questo problema.

I moduli AEM si integrano con  Adobe Target, una soluzione di Adobe Marketing Cloud , per offrire esperienze cliente personalizzate e coinvolgenti su più canali digitali. Per utilizzare  Adobe Target per sottoporre a test i moduli adattivi A/B, [integrare  Adobe Target con AEM Forms](/help/forms/using/ab-testing-adaptive-forms.md#setupandintegratetargetinaemforms).

## Passaggi successivi {#next-steps}

Hai configurato un ambiente per l&#39;utilizzo delle funzionalità di acquisizione dei dati AEM Forms. Ora, i passaggi successivi per utilizzare la funzionalità sono:

* [Creare il primo modulo adattivo](/help/forms/using/create-your-first-adaptive-form.md)
* [Creare il primo modulo PDF](http://www.adobe.com/go/learn_aemforms_designer_quick_start_65)
* [Introduzione ai moduli HTML5](/help/forms/using/introduction.md)

