---
title: Installare e configurare le comunicazioni interattive
seo-title: Install and configure Interactive Communications
description: Installa e configura AEM Forms Interactive Communications per creare corrispondenze aziendali, documenti, dichiarazioni, note sui benefit, e-mail di marketing, fatture e kit di benvenuto.
seo-description: Install and configure AEM Forms Interactive Communications to create business correspondences, documents, statements, benefit notices, marketing mails, bills, and welcome kits.
uuid: 8acb7f68-0b52-4acd-97e2-af31c9408e8d
topic-tags: installing
discoiquuid: 225f2bc1-6842-4c79-a66d-8024a29325c0
docset: aem65
role: Admin
exl-id: 37fcfad9-2f84-4f0c-aed8-e4a5a3303a06
source-git-commit: 63f066013c34a5994e2c6a534d88db0c464cc905
workflow-type: tm+mt
source-wordcount: '1383'
ht-degree: 7%

---

# Installare e configurare le comunicazioni interattive{#install-and-configure-interactive-communications}

## Introduzione {#introduction}

AEM Form è in grado di centralizzare la creazione, l&#39;assemblaggio, la gestione e la consegna di documenti sicuri e interattivi quali corrispondenze aziendali, documenti, dichiarazioni, note sui benefit, e-mail di marketing, fatture e kit di benvenuto. Questa funzionalità è nota come comunicazione interattiva. La funzionalità è inclusa nel pacchetto aggiuntivo di AEM Forms. Il pacchetto aggiuntivo viene distribuito su un’istanza di AEM Author o Publish di .

È possibile utilizzare la funzionalità di comunicazione interattiva per produrre comunicazioni in più formati. Ad esempio, web e PDF. È possibile integrare la comunicazione interattiva con AEM Workflow per elaborare e distribuire la comunicazione assemblata ai clienti sul canale desiderato. Ad esempio, l’invio di una comunicazione all’utente finale tramite e-mail.

Se esegui l’aggiornamento da una versione precedente e hai già investito nella gestione della corrispondenza, puoi installare la [pacchetto di compatibilità](../../forms/using/installing-configuring-intreactive-communication-correspondence-management.md#install-compatibility-package) per continuare a utilizzare la gestione della corrispondenza. Per informazioni sulle differenze tra comunicazione interattiva e gestione della corrispondenza, vedi [Panoramica della comunicazione interattiva](/help/forms/using/interactive-communications-overview.md#interactive-communications-vs-correspondence-management).

AEM Forms è una potente piattaforma di classe enterprise. La comunicazione interattiva è solo una delle funzionalità di AEM Forms. Per un elenco completo delle funzionalità, consulta [Introduzione ad AEM Forms](../../forms/using/introduction-aem-forms.md).

## Topologia di distribuzione {#deployment-topology}

Il pacchetto aggiuntivo di AEM Forms è un&#39;applicazione distribuita su AEM. Per eseguire la funzionalità di comunicazione interattiva è necessaria solo un’istanza di authoring ed elaborazione di AEM. La topologia seguente è indicativa per l’esecuzione di AEM Forms Interactive Communications, Gestione della corrispondenza, acquisizione dati AEM Forms e flusso di lavoro incentrato su Forms sulle funzionalità OSGi. Per informazioni dettagliate sulla topologia, consulta [Architettura e topologie di implementazione per AEM Forms](/help/forms/using/aem-forms-architecture-deployment.md).

![topologia consigliata](assets/recommended-topology.png)

AEM Forms Interactive Communications esegue le interfacce utente amministratore, authoring e agente sulle istanze Autore di AEM Forms. Le istanze di pubblicazione ospitano la versione finale delle comunicazioni interattive pronte all’uso per gli utenti finali.

## Requisiti di sistema {#system-requirements}

Prima di iniziare a installare e configurare le funzionalità di comunicazione interattiva e gestione della corrispondenza di AEM Forms, assicurati che:

* L&#39;infrastruttura hardware e software è in funzione. Per un elenco dettagliato dell&#39;hardware e del software supportati, consultare [requisiti tecnici](/help/sites-deploying/technical-requirements.md).

* Il percorso di installazione dell&#39;istanza AEM non contiene spazi bianchi.
* Un&#39;istanza AEM è in esecuzione. Nella terminologia AEM, un&#39;istanza è una copia di AEM in esecuzione su un server in modalità di authoring o pubblicazione. Per eseguire le funzionalità di comunicazione interattiva e di gestione della corrispondenza di AEM Forms, è necessaria almeno una AEM istanze (Author or or or Processing):

   * **Autore**: Un’istanza AEM utilizzata per creare, caricare e modificare i contenuti e per amministrare il sito web. Quando il contenuto è pronto per essere live, viene replicato nell’istanza di pubblicazione.
   * **Elaborazione:** Un&#39;istanza di elaborazione è [AEM Author indurito](/help/forms/using/hardening-securing-aem-forms-environment.md) istanza. È possibile impostare un&#39;istanza Author e renderla più rigida dopo l&#39;esecuzione dell&#39;installazione.

   * **Pubblica**: Un&#39;istanza AEM che trasmette il contenuto pubblicato al pubblico tramite Internet o una rete interna.

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

## Installare il pacchetto aggiuntivo di AEM Forms {#install-aem-forms-add-on-package}

Il pacchetto aggiuntivo di AEM Forms è un&#39;applicazione distribuita su AEM. Il pacchetto contiene comunicazioni interattive AEM Forms, gestione della corrispondenza e altre funzionalità. Esegui i seguenti passaggi per installare il pacchetto aggiuntivo:

1. Apri [Software Distribution](https://experience.adobe.com/downloads). Per accedere a Software Distribution è necessario disporre di un Adobe ID.
1. Tocca **[!UICONTROL Adobe Experience Manager]** che si trova nel menu di intestazione.
1. In **[!UICONTROL Filtri]** sezione:
   1. Seleziona **[!UICONTROL Forms]** dal **[!UICONTROL Soluzione]** elenco a discesa.
   2. Seleziona la versione e digita il pacchetto. È inoltre possibile utilizzare **[!UICONTROL Download di ricerca]** per filtrare i risultati.
1. Toccare il nome del pacchetto applicabile al sistema operativo in uso, selezionare **[!UICONTROL Accettare i termini dell&#39;EULA]**, e tocca **[!UICONTROL Scarica]**.
1. Apri [Gestione pacchetti](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=it) e fai clic su **[!UICONTROL Carica pacchetto]** per caricarlo.
1. Seleziona il pacchetto e fai clic su **[!UICONTROL Installa]**.

   Puoi anche scaricare il pacchetto tramite il collegamento diretto elencato in [Versioni di AEM Forms](https://helpx.adobe.com/it/aem-forms/kb/aem-forms-releases.html) articolo.

1. Una volta installato il pacchetto, viene richiesto di riavviare l&#39;istanza AEM. **Non riavviare immediatamente il server.** Prima di arrestare il server AEM Forms, attendi che i messaggi ServiceEvent REGISTERED e ServiceEvent UNREGISTERED non vengano più visualizzati nel [Directory AEM-Installazione]/crx-quickstart/logs/error.log e il registro è stabile.
1. Ripeti i passaggi da 1 a 7 su tutte le istanze Author e Publish.

## Configurazioni post-installazione {#post-installation-configurations}

AEM Forms dispone di alcune configurazioni obbligatorie e facoltative. Le configurazioni obbligatorie includono la configurazione delle librerie BouncyCastle e dell&#39;agente di serializzazione. Le configurazioni facoltative includono la configurazione del dispatcher e di Adobe Target.

### Configurazioni obbligatorie post-installazione {#mandatory-post-installation-configurations}

#### Configurare le librerie RSA e BouncyCastle  {#configure-rsa-and-bouncycastle-libraries}

Esegui i seguenti passaggi su tutte le istanze Author e Publish per avviare la delega delle librerie:

1. Interrompi l&#39;istanza AEM sottostante.
1. Apri [Directory di installazione AEM]\crx-quickstart\conf\sling.properties file per la modifica.

   Se hai utilizzato [Directory di installazione AEM]\crx-quickstart\bin\start.bat per iniziare AEM, quindi modifica le proprietà sling.properties che si trovano in [AEM_root]\crx-quickstart\.

1. Aggiungi le seguenti proprietà al file sling.properties :

   ```shell
   sling.bootdelegation.class.com.rsa.jsafe.provider.JsafeJCE=com.rsa.*
   ```

1. Salva e chiudi il file e avvia l’istanza AEM.
1. Ripeti i passaggi 1-4 su tutte le istanze Author e Publish.

#### Configura l’agente di serializzazione {#configure-the-serialization-agent}

Esegui i seguenti passaggi su tutte le istanze Author e Publish per aggiungere il pacchetto all’inserire nell&#39;elenco Consentiti:

1. Apri AEM Configuration Manager in una finestra del browser. L’URL predefinito è https://&#39;[server]:[porta]&#39;/system/console/configMgr.
1. Cerca e apri **Configurazione del firewall di deserializzazione**.
1. Aggiungi il **sun.util.calendar** il pacchetto **inserire nell&#39;elenco Consentiti** campo . Fai clic su Salva.
1. Ripeti i passaggi 1-3 su tutte le istanze Author e Publish.

### Configurazioni opzionali post-installazione {#optional-post-installation-configurations}

#### Installa il pacchetto di compatibilità {#install-compatibility-package}

La comunicazione interattiva è l’approccio predefinito e consigliato per creare comunicazioni con i clienti in Forms 6.5 AEM. Se hai effettuato l’aggiornamento o la migrazione da una versione precedente e intendi continuare a utilizzare le lettere (Gestione corrispondenza), installa la [Pacchetto di compatibilità AEMFD](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq640/fd/AEM-FORMS-6.4-COMPAT).

Il pacchetto di compatibilità AEMFD consente di utilizzare le seguenti risorse da Forms 6.4, Forms 6.3 AEM e Forms 6.2 su AEM 6.5 Forms:

* Frammenti di documento
* Lettere
* Dizionari dati
* Modelli e pagine obsolete per i moduli adattivi

#### Configurare Dispatcher {#configure-dispatcher}

Dispatcher è uno strumento di caching e/o bilanciamento del carico di Adobe Experience Manager che può essere utilizzato insieme a un server web di classe enterprise. Se utilizzi [Dispatcher](https://helpx.adobe.com/it/experience-manager/dispatcher/using/dispatcher-configuration.html), quindi esegui le seguenti configurazioni per AEM Forms:

1. Configura l’accesso per AEM Forms:

   Apri il file dispatcher.any per la modifica. Passa alla sezione filtro e aggiungi il seguente filtro alla sezione filtro :

   `/0025 { /type "allow" /glob "* /bin/xfaforms/submitaction*" } # to enable AEM Forms submission`

   Salva e chiudi il file. Per informazioni dettagliate sui filtri, vedi [Documentazione di Dispatcher](https://helpx.adobe.com/it/experience-manager/dispatcher/using/dispatcher-configuration.html).

1. Configura il servizio filtro referrer:

   Accedi al gestore di configurazione Apache Felix come amministratore. L&#39;URL predefinito del gestore di configurazione è https://&#39;server&#39;:[numero_porta]/system/console/configMgr. In **Configurazioni** seleziona il menu **Filtro di riferimento Apache Sling** opzione . Nel campo Consenti host , immetti il nome host del dispatcher per consentirlo come referrer e fai clic su **Salva**. Il formato della voce è https://&#39;[server]:[porta]&quot;.

#### Integrare Adobe Target {#integrate-adobe-target}

È probabile che i clienti abbandonino una comunicazione interattiva se l’esperienza che offre non è coinvolgente. Anche se è frustrante per i clienti, può anche aumentare il volume di supporto e i costi per la tua organizzazione. È fondamentale e impegnativo identificare e fornire al cliente la giusta esperienza che aumenti il tasso di conversione. AEM forms rappresenta la chiave di questo problema.

AEM forms si integra con Adobe Target, una soluzione Adobe Marketing Cloud, per fornire esperienze cliente personalizzate e coinvolgenti su più canali digitali. Per utilizzare Adobe Target per personalizzare una comunicazione interattiva, [Integrare Adobe Target con AEM Forms](../../forms/using/ab-testing-adaptive-forms.md#setupandintegratetargetinaemforms).

#### Configurare la comunicazione SSL per il modello dati del modulo  {#configure-ssl-communcation-for-form-data-model}

È possibile abilitare la comunicazione SSL per il modello dati modulo. Per abilitare la comunicazione SSL per il modello dati modulo, prima di avviare un’istanza AEM Forms, aggiungi i certificati a Java Trust Store di tutte le istanze. Puoi eseguire il comando seguente per aggiungere i certificati:

`keytool -import -alias <alias-name> -file <pathTo .cer certificate file> -keystore <<pathToJRE>\lib\security\cacerts>`

## Passaggi successivi {#next-steps}

Hai configurato un ambiente per utilizzare le funzionalità di comunicazione interattiva e gestione della corrispondenza. Ora, i passaggi per utilizzare la funzionalità sono:

* [Panoramica sulla gestione della corrispondenza](/help/forms/using/interactive-communications-overview.md)

* [Creare una comunicazione interattiva](../../forms/using/create-interactive-communication.md)

* [Creare una lettera di gestione della corrispondenza](../../forms/using/create-letter.md)
