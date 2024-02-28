---
title: Installare e configurare le comunicazioni interattive
description: Installa e configura AEM Forms Interactive Communications per creare corrispondenze aziendali, documenti, dichiarazioni, avvisi sui vantaggi, marketing mail, fatture e kit di benvenuto.
topic-tags: installing
docset: aem65
role: Admin
exl-id: 37fcfad9-2f84-4f0c-aed8-e4a5a3303a06
source-git-commit: d195ac80ee59439bab5b1219a2c1f16e93e3d22b
workflow-type: tm+mt
source-wordcount: '1383'
ht-degree: 1%

---

# Installare e configurare le comunicazioni interattive{#install-and-configure-interactive-communications}

## Introduzione {#introduction}

Il modulo AEM ha la capacità di centralizzare la creazione, l’assemblaggio, la gestione e la consegna di documenti sicuri e interattivi come corrispondenza aziendale, documenti, dichiarazioni, avvisi di benefit, e-mail di marketing, fatture e kit di benvenuto. Questa funzionalità è nota come comunicazione interattiva. Questa funzionalità è inclusa nel pacchetto del componente aggiuntivo AEM Forms. Il pacchetto del componente aggiuntivo viene distribuito su un’istanza Author o Publish di AEM.

È possibile utilizzare la funzionalità di comunicazione interattiva per produrre comunicazioni in più formati. Ad esempio, web e PDF. È possibile integrare la comunicazione interattiva con il flusso di lavoro AEM per elaborare e distribuire la comunicazione assemblata ai clienti sul canale desiderato. Ad esempio, inviando una comunicazione all’utente finale tramite e-mail.

Se stai effettuando l’aggiornamento da una versione precedente e hai già investito nella gestione della corrispondenza, puoi installare [pacchetto di compatibilità](../../forms/using/installing-configuring-intreactive-communication-correspondence-management.md#install-compatibility-package) per continuare a utilizzare la gestione della corrispondenza. Per informazioni sulle differenze tra comunicazione interattiva e gestione della corrispondenza, consulta [Panoramica della comunicazione interattiva](/help/forms/using/interactive-communications-overview.md#interactive-communications-vs-correspondence-management).

AEM Forms è una potente piattaforma di classe enterprise. La comunicazione interattiva è solo una delle funzionalità di AEM Forms. Per l’elenco completo delle funzionalità, consulta [Introduzione ad AEM Forms](../../forms/using/introduction-aem-forms.md).

## Topologia di distribuzione {#deployment-topology}

Il pacchetto del componente aggiuntivo AEM Forms è un’applicazione implementata nell’AEM. Per eseguire la funzionalità di comunicazione interattiva sono necessarie almeno un&#39;istanza di elaborazione e creazione AEM. La topologia riportata di seguito è indicativa per l’esecuzione di comunicazioni interattive AEM Forms, gestione della corrispondenza, acquisizione dati AEM Forms e flusso di lavoro incentrato su Forms sulle funzionalità OSGi. Per informazioni dettagliate sulla topologia, vedere [Architettura e topologie di implementazione per AEM Forms](/help/forms/using/aem-forms-architecture-deployment.md).

![recommended-topology](assets/recommended-topology.png)

Le comunicazioni interattive di AEM Forms eseguono le interfacce utente di amministrazione, authoring e agente sulle istanze di authoring di AEM Forms. Le istanze Publish ospitano la versione finale delle comunicazioni interattive pronte per essere utilizzate dagli utenti finali.

## Requisiti di sistema {#system-requirements}

Prima di iniziare a installare e configurare le funzionalità di comunicazione interattiva e di gestione della corrispondenza di AEM Forms, assicurati che:

* Infrastruttura hardware e software già esistente. Per un elenco dettagliato dell&#39;hardware e del software supportati, vedere [requisiti tecnici](/help/sites-deploying/technical-requirements.md).

* Il percorso di installazione dell’istanza AEM non contiene spazi vuoti.
* Un’istanza AEM è operativa. Nella terminologia AEM, per &quot;istanza&quot; si intende una copia dell’AEM in esecuzione su un server in modalità di authoring o pubblicazione. Per eseguire le funzionalità di comunicazione interattiva e di gestione della corrispondenza di AEM Forms è necessaria almeno un’istanza AEM (di authoring o elaborazione):

   * **Autore**: istanza AEM utilizzata per creare, caricare e modificare i contenuti e amministrare il sito web. Quando il contenuto è pronto per essere pubblicato, viene replicato nell’istanza di pubblicazione.
   * **Elaborazione:** Un’istanza di elaborazione è un [Autore AEM incallito](/help/forms/using/hardening-securing-aem-forms-environment.md) dell&#39;istanza. Puoi impostare un’istanza Autore e irrigidirla dopo aver eseguito l’installazione.

   * **Pubblica**: istanza dell’AEM che fornisce il contenuto pubblicato al pubblico tramite Internet o una rete interna.

* I requisiti di memoria sono soddisfatti. AEM Forms pacchetto aggiuntivo richiede:

   * 15 GB di spazio temporaneo per le installazioni basate su Microsoft® Windows.
   * 6 GB di spazio temporaneo per installazioni basate su UNIX.

* Requisiti aggiuntivi per i sistemi basati su UNIX: se si utilizza il sistema operativo basato su UNIX, installare i pacchetti seguenti dal supporto di installazione del rispettivo sistema operativo.

<table>
 <tbody>
  <tr>
   <td>expat</td>
   <td>libxcb</td>
   <td>freetype</td>
   <td>libXau</td>
  </tr>
  <tr>
   <td>libSM</td>
   <td>zlib</td>
   <td>libICE</td>
   <td>libuuide</td>
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

## Installare il pacchetto del componente aggiuntivo AEM Forms {#install-aem-forms-add-on-package}

Il pacchetto del componente aggiuntivo AEM Forms è un’applicazione implementata nell’AEM. Il pacchetto contiene la comunicazione interattiva di AEM Forms, la gestione della corrispondenza e altre funzionalità. Per installare il pacchetto aggiuntivo, effettua le seguenti operazioni:

1. Apri [Software Distribution](https://experience.adobe.com/downloads). Per accedere a Software Distribution è necessario disporre di un Adobe ID.
1. Seleziona **[!UICONTROL Adobe Experience Manager]** disponibili nel menu dell&#39;intestazione.
1. **[!UICONTROL Nella sezione Filtri]**:
   1. Seleziona **[!UICONTROL Forms]** dall&#39;elenco a **[!UICONTROL discesa Soluzione]** .
   2. Seleziona la versione e il tipo per il pacchetto. È inoltre possibile utilizzare l&#39;opzione **[!UICONTROL Search Download]** per filtrare i risultati.
1. Selezionare il nome del pacchetto applicabile al sistema operativo in uso, quindi selezionare **[!UICONTROL Accetta termini EULA]**, e seleziona **[!UICONTROL Scarica]**.
1. Apri [Gestione pacchetti](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html)  e fai clic su **[!UICONTROL Carica pacchetto per caricare il pacchetto]** .
1. Seleziona il pacchetto e fai clic su **[!UICONTROL Installa]**.

   Puoi anche scaricare il pacchetto tramite la collegare diretta elencata nell&#39;articolo sulle [versioni](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=en) AEM Forms.

1. Dopo aver installato il pacchetto, viene chiesto di riavviare il AEM istanza. **Non riavviare immediatamente il server.** Prima di arrestare il server AEM Forms, attendere che i [messaggi ServiceEvent REGISTERED e ServiceEvent UNREGISTERED smettano di apparire nel file AEM-Installation-Directory]/crx-quickstart/logs/error.log e che il registro sia stabile.

   >[!NOTE]
   >
   > Per riavviare l&#39;SDK, si consiglia di utilizzare il comando &#39;Ctrl + C&#39;. Il riavvio dell’SDK dell’AEM con metodi alternativi, ad esempio l’arresto dei processi Java, può causare incongruenze nell’ambiente di sviluppo dell’AEM.

1. Ripeti i passaggi da 1 a 7 su tutte le istanze Author e Publish.

## Configurazioni post-installazione {#post-installation-configurations}

AEM Forms dispone di alcune configurazioni obbligatorie e opzionali. Le configurazioni obbligatorie includono la configurazione delle librerie BouncyCastle e dell’agente di serializzazione. Le configurazioni opzionali includono la configurazione di Dispatcher e Adobe Target.

### Configurazioni post-installazione obbligatorie {#mandatory-post-installation-configurations}

#### Configurare le librerie RSA e BouncyCastle  {#configure-rsa-and-bouncycastle-libraries}

Per avviare le librerie, esegui i seguenti passaggi su tutte le istanze Author e Publish:

1. Arresta l’istanza AEM sottostante.
1. Apri [Directory di installazione AEM]File \crx-quickstart\conf\sling.properties per la modifica.

   Se ha usato [Directory di installazione AEM]\crx-quickstart\bin\start.bat per avviare l’AEM, quindi modifica sling.properties in [AEM_root]\crx-quickstart\.

1. Aggiungi le seguenti proprietà al file sling.properties:

   ```shell
   sling.bootdelegation.class.com.rsa.jsafe.provider.JsafeJCE=com.rsa.*
   ```

1. Salva e chiudi il file e avvia l’istanza AEM.
1. Ripeti i passaggi da 1 a 4 su tutte le istanze Author e Publish.

#### Configurare l’agente di serializzazione {#configure-the-serialization-agent}

Per aggiungere il pacchetto al inserisco nell&#39;elenco Consentiti di creazione, effettua le seguenti operazioni su tutte le istanze Author e Publish:

1. Apri Gestione configurazione AEM in una finestra del browser. L’URL predefinito è https://&#39;[server]:[porta]&#39;/system/console/configMgr.
1. Cerca e apri **Configurazione firewall deserializzazione**.
1. Aggiungi il **sun.util.calendar** pacchetto per **INSERISCO NELL&#39;ELENCO CONSENTITI DI** campo. Fai clic su Salva.
1. Ripeti i passaggi 1-3 su tutte le istanze Author e Publish.

### Configurazioni opzionali post-installazione {#optional-post-installation-configurations}

#### Installa pacchetto di compatibilità {#install-compatibility-package}

La comunicazione interattiva è l’approccio predefinito e consigliato per la creazione di comunicazioni con i clienti in Forms AEM 6.5. Se hai effettuato l’aggiornamento o la migrazione da una versione precedente e prevedi di continuare a utilizzare le lettere (Gestione corrispondenza), installa [Pacchetto di compatibilità per AEMFD](https://experienceleague.adobe.com/docs/experience-manager-65/forms/upgrade-aem-forms/aem-forms-osgi-upgrade/compatibility-package.html?lang=en).

Il pacchetto Compatibilità AEMFD consente di utilizzare le seguenti risorse da AEM 6.4 Forms, AEM 6.3 Forms e AEM 6.2 Forms su AEM 6.5 Forms:

* Frammenti di documento
* Lettere
* Dizionari dati
* Moduli adattivi: modelli e pagine obsoleti

#### Configurare Dispatcher {#configure-dispatcher}

Dispatcher è uno strumento di caching e bilanciamento del carico di Adobe Experience Manager utilizzato con un server web di classe enterprise. Se usa [Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=it), quindi esegui le seguenti configurazioni per AEM Forms:

1. Configurare l’accesso per AEM Forms:

   Apri il file dispatcher.any per la modifica. Passa alla sezione del filtro e aggiungi il seguente filtro alla sezione del filtro:

   `/0025 { /type "allow" /glob "* /bin/xfaforms/submitaction*" } # to enable AEM Forms submission`

   Salvare e chiudere il file. Per informazioni dettagliate sui filtri, consulta [Documentazione di Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=it).

1. Configura il servizio filtro referenti:

   Accedi al gestore della configurazione Apache Felix come amministratore. L’URL predefinito del gestore di configurazione è https://&#39;server&#39;:[port_number]/system/console/configMgr. In **Configurazioni** , selezionare il **Filtro referrer Apache Sling** opzione. Nel campo Consenti host, immetti il nome host del Dispatcher per consentirlo come referrer e fai clic su **Salva**. Il formato della voce è https://&#39;[server]:[porta]&quot;.

#### Integrare Adobe Target {#integrate-adobe-target}

È probabile che i clienti abbandonino una comunicazione interattiva se l&#39;esperienza che offre non è coinvolgente. Se da un lato è frustrante per i clienti, dall&#39;altro aumenta il volume e i costi di supporto per la tua organizzazione. Identificare e fornire la giusta esperienza del cliente che aumenti il tasso di conversione è fondamentale e impegnativo. I moduli AEM sono la chiave di questo problema.

I moduli AEM si integrano con Adobe Target, una soluzione Adobe Experience Cloud, per offrire esperienze cliente personalizzate e coinvolgenti su più canali digitali. Per personalizzare una comunicazione interattiva con Adobe Target: [Integrare Adobe Target con AEM Forms](../../forms/using/ab-testing-adaptive-forms.md#setupandintegratetargetinaemforms).

#### Configurare la comunicazione SSL per il modello dati modulo  {#configure-ssl-communcation-for-form-data-model}

Puoi abilitare la comunicazione SSL per il modello dati modulo. Per abilitare la comunicazione SSL per il modello dati del modulo, prima di avviare qualsiasi istanza di AEM Forms, aggiungi i certificati all’archivio fonti attendibili Java™ di tutte le istanze. Puoi eseguire il comando seguente per aggiungere i certificati:

`keytool -import -alias <alias-name> -file <pathTo .cer certificate file> -keystore <<pathToJRE>\lib\security\cacerts>`

## Passaggi successivi {#next-steps}

È stato configurato un ambiente per l&#39;utilizzo delle funzionalità di comunicazione interattiva e gestione della corrispondenza. Ora, i passaggi per l&#39;utilizzo di questa funzionalità sono:

* [Panoramica sulla gestione della corrispondenza](/help/forms/using/interactive-communications-overview.md)

* [Crea una comunicazione interattiva](../../forms/using/create-interactive-communication.md)

* [Crea una lettera di gestione della corrispondenza](../../forms/using/create-letter.md)
