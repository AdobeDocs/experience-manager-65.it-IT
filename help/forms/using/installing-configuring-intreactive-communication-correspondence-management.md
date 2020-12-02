---
title: Installare e configurare le comunicazioni interattive
seo-title: Installare e configurare le comunicazioni interattive
description: Installate e configurate  AEM Forms Interactive Communications per creare corrispondenze aziendali, documenti, dichiarazioni, note sui vantaggi, e-mail di marketing, fatture e kit di benvenuto.
seo-description: Installate e configurate  AEM Forms Interactive Communications per creare corrispondenze aziendali, documenti, dichiarazioni, note sui vantaggi, e-mail di marketing, fatture e kit di benvenuto.
uuid: 8acb7f68-0b52-4acd-97e2-af31c9408e8d
topic-tags: installing
discoiquuid: 225f2bc1-6842-4c79-a66d-8024a29325c0
docset: aem65
translation-type: tm+mt
source-git-commit: 35b2c9c8c79b3cc3d81e0b92ea17cd7d599fa7ee
workflow-type: tm+mt
source-wordcount: '1411'
ht-degree: 1%

---


# Installazione e configurazione di Interactive Communications{#install-and-configure-interactive-communications}

## Introduzione {#introduction}

AEM Form è in grado di centralizzare la creazione, l&#39;assemblaggio, la gestione e la consegna di documenti sicuri e interattivi quali corrispondenze aziendali, documenti, dichiarazioni, note sui benefit, e-mail di marketing, fatture e kit di benvenuto. Questa funzionalità è nota come comunicazione interattiva. La funzionalità è inclusa  pacchetto aggiuntivo di AEM Forms. Il pacchetto del componente aggiuntivo viene distribuito su un’istanza di AEM Author o Publish.

È possibile utilizzare la capacità di comunicazione interattiva per produrre comunicazioni in più formati. Ad esempio, Web e PDF. È possibile integrare la comunicazione interattiva con AEM Workflow per elaborare e distribuire la comunicazione assemblata ai clienti sul canale desiderato. Ad esempio, l&#39;invio di una comunicazione all&#39;utente finale tramite e-mail.

Se state effettuando l&#39;aggiornamento da una versione precedente e avete già investito nella gestione della corrispondenza, potete installare il [pacchetto di compatibilità](../../forms/using/installing-configuring-intreactive-communication-correspondence-management.md#install-compatibility-package) per continuare a utilizzare la gestione della corrispondenza. Per informazioni sulle differenze tra la comunicazione interattiva e la gestione della corrispondenza, vedere [Interactive Communication Overview](/help/forms/using/interactive-communications-overview.md#interactive-communications-vs-correspondence-management).

 AEM Forms è una potente piattaforma di livello aziendale. La comunicazione interattiva è solo una delle capacità di  AEM Forms. Per l&#39;elenco completo delle funzionalità, vedere [Introduzione a  AEM Forms](../../forms/using/introduction-aem-forms.md).

## Topologia di distribuzione {#deployment-topology}

 pacchetto del componente aggiuntivo AEM Forms è un&#39;applicazione distribuita in AEM. Per eseguire la funzionalità di comunicazione interattiva è necessaria almeno un&#39;istanza di AEM Author and Processing. La topologia seguente è indicativa per l’esecuzione  AEM Forms Interactive Communications, Correspondence Management,  l’acquisizione dei dati AEM Forms e il flusso di lavoro Forms-Centric sulle funzionalità OSGi. Per informazioni dettagliate sulla topologia, vedere [Topologie di architettura e distribuzione per  AEM Forms](/help/forms/using/aem-forms-architecture-deployment.md).

![topologia consigliata](assets/recommended-topology.png)

 AEM Forms Interactive Communications esegue le interfacce utente admin, authoring e agent sulle istanze Author di  AEM Forms. Le istanze Pubblica ospitano la versione finale delle comunicazioni interattive pronte all’uso per gli utenti finali.

## Requisiti di sistema {#system-requirements}

Prima di iniziare a installare e configurare le funzionalità di comunicazione interattiva e gestione della corrispondenza di  AEM Forms, accertatevi che:

* L&#39;infrastruttura hardware e software è già in funzione. Per un elenco dettagliato di hardware e software supportati, vedere [requisiti tecnici](/help/sites-deploying/technical-requirements.md).

* Il percorso di installazione dell&#39;istanza AEM non contiene spazi bianchi.
* Un&#39;istanza AEM è attiva e in esecuzione. AEM terminologia, un&#39;istanza è una copia di AEM in esecuzione su un server in modalità di creazione o pubblicazione. Per eseguire  funzionalità di comunicazione interattiva e gestione della corrispondenza AEM Forms è necessario disporre di almeno un AEM istanze (Author o Processing):

   * **Autore**: Istanza AEM utilizzata per creare, caricare e modificare i contenuti e per amministrare il sito Web. Quando il contenuto è pronto per essere live, viene replicato nell’istanza di pubblicazione.
   * **Elaborazione:** Un&#39;istanza di elaborazione è un&#39; [istanza AEM ](/help/forms/using/hardening-securing-aem-forms-environment.md) Authoring indurita. Potete impostare un&#39;istanza Author e renderla più indurita dopo l&#39;installazione.

   * **Pubblica**: Un&#39;istanza AEM che trasmette il contenuto pubblicato al pubblico su Internet o su una rete interna.

* I requisiti di memoria sono soddisfatti.  pacchetto del componente aggiuntivo AEM Forms richiede:

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

## Installare  pacchetto aggiuntivo AEM Forms {#install-aem-forms-add-on-package}

 pacchetto del componente aggiuntivo AEM Forms è un&#39;applicazione distribuita in AEM. Il pacchetto contiene  comunicazione interattiva AEM Forms, gestione della corrispondenza e altre funzionalità. Effettuate le seguenti operazioni per installare il pacchetto del componente aggiuntivo:

1. Aprire [Distribuzione software](https://experience.adobe.com/downloads). È necessario un Adobe ID  per accedere a Distribuzione software.
1. Toccate **[!UICONTROL Adobe Experience Manager]** disponibile nel menu di intestazione.
1. Nella sezione **[!UICONTROL Filtri]**:
   1. Selezionare **[!UICONTROL Forms]** dall&#39;elenco a discesa **[!UICONTROL Soluzione]**.
   2. Selezionate la versione e digitate il tipo di pacchetto. Potete anche utilizzare l&#39;opzione **[!UICONTROL Download di ricerca]** per filtrare i risultati.
1. Toccate il nome del pacchetto applicabile al sistema operativo in uso, selezionate **[!UICONTROL Accetta termini EULA]**, quindi toccate **[!UICONTROL Scarica]**.
1. Aprite [Gestione pacchetti](https://docs.adobe.com/content/help/en/experience-manager-65/administering/contentmanagement/package-manager.html) e fate clic su **[!UICONTROL Carica pacchetto]** per caricare il pacchetto.
1. Selezionate il pacchetto e fate clic su **[!UICONTROL Installa]**.

   Potete anche scaricare il pacchetto tramite il collegamento diretto elencato nell&#39;articolo [ rilasci di AEM Forms](https://helpx.adobe.com/it/aem-forms/kb/aem-forms-releases.html).

1. Dopo l&#39;installazione del pacchetto, viene richiesto di riavviare l&#39;istanza AEM. **Non riavviare immediatamente il server.** Prima di arrestare il server AEM Forms , attendere che i messaggi ServiceEvent REGISTERED e ServiceEvent UNREGISTERED non vengano visualizzati nel file  [AEM-Installation-Directory]/crx-quickstart/logs/error.log e il registro sia stabile.
1. Ripetete i passaggi da 1 a 7 su tutte le istanze Author e Publish.

## Configurazioni post-installazione {#post-installation-configurations}

 AEM Forms dispone di alcune configurazioni obbligatorie e facoltative. Le configurazioni obbligatorie includono la configurazione delle librerie BouncyCastle e dell&#39;agente di serializzazione. Le configurazioni facoltative includono la configurazione del dispatcher e  Adobe Target.

### Configurazioni post-installazione obbligatorie {#mandatory-post-installation-configurations}

#### Configurare le librerie RSA e BouncyCastle {#configure-rsa-and-bouncycastle-libraries}

Per avviare la delega delle librerie, eseguite i seguenti passaggi su tutte le istanze Autore e Pubblica:

1. Arrestate l’istanza AEM sottostante.
1. Aprire il file [AEM directory di installazione]\crx-quickstart\conf\sling.properties per la modifica.

   Se avete utilizzato [AEM directory di installazione]\crx-quickstart\bin\start.bat per avviare AEM, modificate le proprietà sling.properties che si trovano in [AEM_root]\crx-quickstart\.

1. Aggiungete le seguenti proprietà al file sling.properties:

   ```shell
   sling.bootdelegation.class.com.rsa.jsafe.provider.JsafeJCE=com.rsa.*
   ```

1. Salvate e chiudete il file e avviate l&#39;istanza AEM.
1. Ripetete i passaggi da 1 a 4 su tutte le istanze Author e Publish.

#### Configurare l&#39;agente di serializzazione {#configure-the-serialization-agent}

Per aggiungere il pacchetto al inserire nell&#39;elenco Consentiti di , eseguite i seguenti passaggi su tutte le istanze Author e Publish:

1. Aprite AEM Configuration Manager in una finestra del browser. L&#39;URL predefinito è https://&#39;[server]:[porta]&#39;/system/console/configMgr.
1. Cerca e apri **Configurazione firewall di deserializzazione**.
1. Aggiungete il pacchetto **sun.util.Calendar** al campo **inserì nell&#39;elenco Consentiti**. Fate clic su Salva.
1. Ripetete i passaggi da 1 a 3 su tutte le istanze Author e Publish.

### Configurazioni di post-installazione facoltative {#optional-post-installation-configurations}

#### Installa pacchetto di compatibilità {#install-compatibility-package}

La comunicazione interattiva è l&#39;approccio predefinito e consigliato per creare comunicazioni con i clienti nell&#39;Forms AEM 6.5. Se avete effettuato l&#39;aggiornamento o la migrazione da una versione precedente e intendete continuare a utilizzare le lettere (Gestione corrispondenza), installate il [pacchetto di compatibilità AEMFD](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq640/fd/AEM-FORMS-6.4-COMPAT).

Il pacchetto di compatibilità AEMFD consente di utilizzare le seguenti risorse da Forms 6.4, Forms 6.3 AEM e Forms 6.2 AEM 6.2 su AEM 6.5 Forms:

* Frammenti di documenti
* Lettere
* Dizionari dati
* Moduli adattivi modelli e pagine obsoleti

#### Configura dispatcher {#configure-dispatcher}

Dispatcher è uno strumento di cache e/o bilanciamento del carico Adobe Experience Manager che può essere utilizzato insieme a un server Web di classe enterprise. Se si utilizza [Dispatcher](https://helpx.adobe.com/it/experience-manager/dispatcher/using/dispatcher-configuration.html), eseguire le seguenti configurazioni per  AEM Forms:

1. Configurare l&#39;accesso per  AEM Forms:

   Aprire il file dispatcher.any per la modifica. Andate alla sezione del filtro e aggiungete il seguente filtro alla sezione del filtro:

   `/0025 { /type "allow" /glob "* /bin/xfaforms/submitaction*" } # to enable AEM Forms submission`

   Salvate e chiudete il file. Per informazioni dettagliate sui filtri, consultare la [Documentazione del dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html).

1. Configurare il servizio filtro di riferimento:

   Accedete al gestore di configurazione Apache Felix come amministratore. L&#39;URL predefinito del gestore di configurazione è https://&#39;server&#39;:[port_number]/system/console/configMgr. Nel menu **Configurations**, selezionare l&#39;opzione **Apache Sling Referrer Filter**. Nel campo Consenti ospitanti, immettere il nome host del dispatcher per consentirlo come referente e fare clic su **Salva**. Il formato della voce è https://&#39;[server]:[porta]&#39;.

#### Integrare  Adobe Target {#integrate-adobe-target}

È probabile che i clienti abbandonino una comunicazione interattiva se l&#39;esperienza non è coinvolgente. Anche se è frustrante per i clienti, può anche aumentare il volume e i costi del supporto per la vostra organizzazione. È fondamentale e impegnativo identificare e fornire al cliente la giusta esperienza che aumenta il tasso di conversione. AEM moduli rappresenta la chiave di questo problema.

AEM moduli si integra con  Adobe Target, una soluzione Adobe Marketing Cloud, per offrire esperienze cliente personalizzate e coinvolgenti su più canali digitali. Per utilizzare  Adobe Target per personalizzare una comunicazione interattiva, [Integrare  Adobe Target con  AEM Forms](../../forms/using/ab-testing-adaptive-forms.md#setupandintegratetargetinaemforms).

#### Configurare la comunicazione SSL per il modello dati modulo {#configure-ssl-communcation-for-form-data-model}

È possibile abilitare la comunicazione SSL per il modello dati modulo. Per abilitare la comunicazione SSL per il modello dati modulo, prima di avviare un&#39;istanza  AEM Forms, aggiungere certificati a Java Trust Store per tutte le istanze. È possibile eseguire il comando seguente per aggiungere i certificati:

`keytool -import -alias <alias-name> -file <pathTo .cer certificate file> -keystore <<pathToJRE>\lib\security\cacerts>`

## Passaggi successivi {#next-steps}

Hai configurato un ambiente per l&#39;utilizzo delle funzionalità di comunicazione interattiva e gestione della corrispondenza. Ora, i passaggi per utilizzare la funzionalità sono:

* [Panoramica sulla gestione della corrispondenza](/help/forms/using/interactive-communications-overview.md)

* [Creazione di una comunicazione interattiva](../../forms/using/create-interactive-communication.md)

* [Creare una lettera di gestione della corrispondenza](../../forms/using/create-letter.md)

