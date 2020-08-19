---
title: Configurare e configurare siti di riferimento self-service per We.Finance e Dipendenti
seo-title: Configurare e configurare siti di riferimento self-service per We.Finance e Dipendenti
description: ' siti di riferimento AEM Forms illustrano come utilizzare  AEM Forms per implementare un flusso di lavoro end-to-end in un’organizzazione.'
seo-description: ' siti di riferimento AEM Forms illustrano come utilizzare  AEM Forms per implementare un flusso di lavoro end-to-end in un’organizzazione.'
uuid: 199349b7-97bd-4eca-a2e7-19d6708fcbee
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: introduction
discoiquuid: 03886dd3-5873-4908-912b-fbbddb26c322
docset: aem65
translation-type: tm+mt
source-git-commit: b0e071cb3bf972ceaa2af3b70a7887557e6f10f9
workflow-type: tm+mt
source-wordcount: '2915'
ht-degree: 0%

---


# Configurare e configurare siti di riferimento self-service per We.Finance e Dipendenti{#set-up-and-configure-we-finance-and-employee-self-service-reference-sites}

 AEM Forms fornisce un&#39;implementazione del sito di riferimento per dimostrare come  AEM Forms aiuta le organizzazioni del settore e del governo dei servizi finanziari a trasformare le loro complesse transazioni in esperienze digitali semplici e coinvolgenti ovunque, in qualsiasi momento, su qualsiasi dispositivo.

Il sito di riferimento We.Finance raccoglie casi di utilizzo reali per interagire con clienti esistenti e potenziali, dal momento del primo tocco alla gestione delle corrispondenze e delle transazioni in modo personalizzato ed economico.

Installate i pacchetti dei siti di riferimento We.Gov e We.Finance utilizzando la distribuzione [](https://docs.adobe.com/content/help/en/experience-cloud/software-distribution/home.html)software. Per ulteriori informazioni, consultate [Implementare pacchetti](#refsite)di siti di riferimento.

I siti di riferimento consentono di esplorare e presentare le seguenti funzionalità chiave di  AEM Forms.

* Esperienza di authoring semplificata con moduli adattivi coinvolgenti e reattivi e comunicazioni interattive.
* Comunicazioni interattive per creare comunicazioni interattive, personalizzate e reattive per i clienti che si adattano all&#39;impostazione e al layout del dispositivo.
* Integrazione dei dati per la connessione a origini dati diverse per la precompilazione e l&#39;invio dei dati del modulo tramite un modello dati del modulo.
* Flusso di lavoro Forms per automatizzare processi e flussi di lavoro aziendali.
* Funzionalità avanzate di gestione ed elaborazione dei dati utente.
* Integrazione con  Adobe Sign per firmare e inviare moduli adattivi in modo sicuro.
* Integrazione con  Adobe Target per distribuire raccomandazioni mirate e eseguire test A/B per ottimizzare il ROI da un modulo.
* Integrazione con  Adobe Analytics per misurare le prestazioni di un modulo o di una campagna e prendere decisioni informate.
* Esperienza di compilazione dei moduli migliorata.

I siti di riferimento forniscono risorse riutilizzabili che potete usare come modelli per creare risorse personalizzate.

* Integrazione con  Adobe Sign per firmare e inviare moduli adattivi in modo sicuro.

* Integrazione con  Adobe Sign per firmare e inviare moduli adattivi in modo sicuro.

## Prerequisiti e passaggi per configurare i siti di riferimento {#prerequisites-and-steps-to-set-up-reference-sites}

Prima di configurare il sito di riferimento, accertatevi di disporre dei seguenti elementi:

* **AEM essenziali** AEM QuickStart,  pacchetto aggiuntivo AEM Forms e pacchetti per siti di riferimento. Consultate [versioni](https://helpx.adobe.com/it/aem-forms/kb/aem-forms-releases.html) AEM Forms per i dettagli dei pacchetti di componenti aggiuntivi e di riferimento per siti Web.

* **Un servizio** SMTP È possibile utilizzare qualsiasi servizio SMTP.

* **account sviluppatore Adobe Sign e  applicazione** API Adobe Sign Per utilizzare le funzionalità di firma digitale, è necessario  account sviluppatore Adobe Sign. Consultate [Adobe Sign](https://acrobat.adobe.com/us/en/why-adobe/developer-form.html).

* Un&#39;istanza in esecuzione di Microsoft Dynamics 365 da integrare con  AEM Forms. Per eseguire il sito di riferimento, importare i dati di esempio nell&#39;istanza di Microsoft Dynamics per precompilare la comunicazione interattiva utilizzata nel sito di riferimento.
* Un&#39;istanza in esecuzione di AEM con il pacchetto del componente aggiuntivo Forms. Per ulteriori informazioni, consultate [Installazione e configurazione  AEM Forms](../../forms/using/installing-configuring-aem-forms-osgi.md).

Effettuate i seguenti passaggi nella sequenza consigliata per configurare e impostare i siti di riferimento.

<table>
 <tbody>
  <tr>
   <th><strong>Incremento</strong></th>
   <th><strong>Configura</strong></th>
   <th><strong>Note</strong></th>
  </tr>
  <tr>
   <td><a href="#installandconfigureaemform">Installare e configurare  AEM Forms</a></td>
   <td>Creazione e pubblicazione</td>
   <td>Installate e configurate  istanze di creazione e pubblicazione AEM Forms.</td>
  </tr>
  <tr>
   <td><a href="#ssl">Configurare SSL</a></td>
   <td>Author and Publish<br /> </td>
   <td>Abilita HTTP su SSL per comunicazioni sicure con  Adobe Sign.</td>
  </tr>
  <tr>
   <td><p><a href="#externalizer">Configurare la configurazione Day CQ Link Externalizer</a></p> </td>
   <td>Author and Publish<br /> </td>
   <td><p>Casi di utilizzo del sito di riferimento forniscono e-mail per diverse transazioni. Questa impostazione è necessaria per la consegna della newsletter tramite e-mail. Gli URL e le immagini puntano all’istanza di pubblicazione. </p> </td>
  </tr>
  <tr>
   <td><a href="#cqmail">Configura servizio di posta CQ Day</a></td>
   <td>Creazione e pubblicazione</td>
   <td>Obbligatorio per la comunicazione tramite e-mail.</td>
  </tr>
  <tr>
   <td><a href="#xss">Ignora configurazione XSS predefinita</a></td>
   <td>Pubblicazione</td>
   <td>Utilizzato per ignorare $, { e } caratteri bloccati dalla sicurezza xss.</td>
  </tr>
  <tr>
   <td><a href="#aemds">Configurare le impostazioni di AEM DS</a></td>
   <td>Autore</td>
   <td>Configurare AEM DS per l'invio del modulo nell'istanza di pubblicazione e per l'elaborazione dei flussi di lavoro nell'istanza di creazione.</td>
  </tr>
  <tr>
   <td><a href="#refsite">Distribuzione di pacchetti di siti di riferimento</a></td>
   <td>Autore</td>
   <td>Distribuire pacchetti per siti di riferimento ’istanza di creazione AEM Forms.</td>
  </tr>
  <tr>
   <td><a href="../../forms/using/setup-reference-sites.md#optional-import-sample-data-into-microsoft-dynamics">Importa dati di esempio in Microsoft Dynamics</a></td>
   <td>Creazione e pubblicazione</td>
   <td>Importazione di dati di esempio per l'applicazione di carte di credito, l'applicazione di ipoteca per la casa e l'applicazione di assicurazione per la casa dettagliata</td>
  </tr>
  <tr>
   <td><a href="../../forms/using/setup-reference-sites.md#configure-oauth-cloud-service-for-microsoft-dynamics">Configurare il servizio cloud OAuth per Microsoft Dynamics</a></td>
   <td>Creazione e pubblicazione</td>
   <td>Configurare il servizio cloud OAuth in  AEM Forms per abilitare la comunicazione tra  AEM Forms e Microsoft Dynamics. </td>
  </tr>
  <tr>
   <td><a href="#scheduler">Configurare  pianificazione Adobe Sign</a></td>
   <td>Author and Publish<br /> </td>
   <td>Modifica la configurazione del pianificatore per controllare lo stato ogni due minuti.</td>
  </tr>
  <tr>
   <td><a href="#sign-service">Configura sito di riferimento  Cloud Service Adobe Sign</a></td>
   <td>Author and Publish<br /> </td>
   <td>Una configurazione fornita con i siti di riferimento crea pacchetti e richiede la riconfigurazione con credenziali valide.</td>
  </tr>
  <tr>
   <td><a href="#anonymous">Configurare Forms Common Configuration Service per gli utenti anonimi</a></td>
   <td>Pubblicazione</td>
   <td>La configurazione consente l’invio, la firma e la generazione del documento di registrazione per gli utenti anonimi.</td>
  </tr>
  <tr>
   <td><a href="#fdm">Modifica file Swagger del servizio residuo per il modello dati del modulo</a></td>
   <td>Author and Publish<br /> </td>
   <td>Modificare il servizio per il proprio ambiente.</td>
  </tr>
 </tbody>
</table>

## Installare e configurare  AEM Forms {#installandconfigureaemform}

Installate e distribuite  AEM Forms come descritto in [Installazione e configurazione  AEM Forms su OSGi](../../forms/using/installing-configuring-aem-forms-osgi.md).

>[!NOTE]
>
>Configurate gli agenti di replica e replica inversa se esistono più istanze di pubblicazione o di creazione e pubblicazione su computer diversi.

## Configurare SSL {#ssl}

La configurazione SSL è necessaria per comunicare con  server Adobe Sign. Per i passaggi dettagliati, consultate [Abilitazione di HTTP su SSL](/help/sites-administering/ssl-by-default.md).

>[!CAUTION]
>
>Non configurate Forza SSL sulla `/etc/map` cartella.

## Configurare la configurazione Day CQ Link Externalizer {#externalizer}

In AEM, **Externalizer** è un servizio OSGI che consente di trasformare programmaticamente un percorso di risorse (ad es. /path/to/my/page) in un URL esterno e assoluto (ad esempio, https://www.mycompany.com/path/to/my/page) anteponendo il percorso a un DNS preconfigurato. Consultate [Esternalizzazione degli URL](/help/sites-developing/externalizer.md).

>[!CAUTION]
>
>Non esternalizzate con l’URL HTTPS se utilizzate un certificato autofirmato per SSL.
>
>Inoltre, utilizzate localhost invece del relativo nome host per il server locale.

Effettuate le seguenti operazioni sia sulle istanze di creazione che di pubblicazione:

1. Andate alla configurazione OSGi all&#39;indirizzo https://&lt;*hostname>*:&lt;*port>*/system/console/configMgr.
1. Individuate e toccate la configurazione **Day CQ Link Externalizer** .
Viene visualizzata la finestra di dialogo Day CQ Link Externalizer (Esternalizzatore collegamento CQ Day) per modificare la configurazione.
1. Nella finestra di dialogo Day CQ Link Externalizer, nel campo Domains (Domini):

   * Nell’istanza di creazione, specificate un URL di pubblicazione a cui potete accedere da un sistema esterno. Ad esempio, un nome host o un server Web di pubblicazione.
   * Nell’istanza di pubblicazione, specificate gli URL di creazione e pubblicazione.

1. Sia nelle istanze di creazione che di pubblicazione, accertatevi che l’URL del server locale sia specificato nel campo Domini.
1. Toccate **Salva**. Attendi il riavvio di tutti i servizi.

## Configura servizio di posta CQ Day {#cqmail}

L&#39;implementazione del sito di riferimento richiede l&#39;invio di e-mail agli utenti di esempio quando compilano e inviano i moduli. La configurazione di Day CQ Mail Service consente di fornire i dettagli del servizio SMTP per inviare e-mail automatizzate ai clienti. See [Configuring Email Notifications](/help/sites-administering/notification.md).

Per configurare il servizio di posta elettronica nell’istanza di pubblicazione, effettuate le seguenti operazioni:

1. Andate alla configurazione OSGi all&#39;indirizzo https://&lt;*hostname>*:&lt;*port>*/system/console/configMgr.
1. Tocca e trova il servizio **di posta** Day CQ Mail per aprirlo alla configurazione.
1. Specificare il nome host del server SMTP e i valori della porta.
1. Toccate **Salva.**

>[!NOTE]
>
>Potete utilizzare il vostro servizio SMTP aziendale o i servizi pubblici come Gmail. Per configurare il servizio SMTP, consulta la documentazione del servizio SMTP.

## Ignora configurazione XSS predefinita {#xss}

I modelli e-mail per il sito di riferimento We.Finance contengono collegamenti personalizzati nelle e-mail. Tali collegamenti hanno il segnaposto `${placeholder}`. Questi segnaposto vengono sostituiti dai valori effettivi prima dell&#39;invio delle e-mail. La configurazione di protezione XSS predefinita per AEM non consente le parentesi graffe (**{ }**) nell&#39;URL nel contenuto HTML. Tuttavia, potete ignorare la configurazione predefinita eseguendo i seguenti passaggi sull’istanza di pubblicazione:

1. Copia `/libs/cq/xssprotection/config.xml` in `/apps/cq/xssprotection/config.xml`.
1. Apri `/apps/cq/xssprotection/config.xml`.
1. Nella `common-regexps` sezione, modificate la `onsiteURL` voce come segue e salvate il file.

   `<regexp name="onsiteURL" value="([\p{L}\p{N}\\\.\#@\$\{\}%\+&;\-_~,\?=/!\*\(\)]*|\#(\w)+)"/>`

>[!NOTE]
>
>Le parentesi graffe (**{ }**) sono incluse come caratteri accettati nell&#39;URL nel contenuto HTML.

Dopo aver configurato il server SMTP, provare a compilare un modulo utilizzando il nome Sarah Rose e salvarlo come bozza. Quando salvate come bozza, potete ricevere la bozza tramite e-mail. Toccando il pulsante **Invia e-mail** , se ricevete un messaggio e-mail con un collegamento alla bozza dell&#39;applicazione, la configurazione dell&#39;e-mail avrà esito positivo. Assicurati di accedere utilizzando le credenziali di Sarah per vedere la bozza.

## Configurare le impostazioni di AEM DS {#aemds}

AEM le impostazioni del servizio DS sono richieste nell&#39;istanza Pubblica per le comunicazioni e-mail nei casi di utilizzo del sito di riferimento. Per i passaggi dettagliati per configurare AEM configurazione del servizio DS nell&#39;istanza Pubblica, vedi [Configurare AEM impostazioni](../../forms/using/configuring-the-processing-server-url-.md)DS.

Per  siti di riferimento AEM Forms, in AEM DS Settings Service, specificate l&#39;URL del server di pubblicazione invece dell&#39;URL del server di elaborazione.

>[!CAUTION]
>
>Non inserite `/lc` l’URL del server di elaborazione se lo state configurando per  AEM Forms OSGi.

## Distribuzione di pacchetti di siti di riferimento {#refsite}

Installate i pacchetti dei siti di riferimento utilizzando la distribuzione [](https://docs.adobe.com/content/help/en/experience-cloud/software-distribution/home.html)software.

* [AEM Forms FSI Reference Site Package](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffd%2FAEM-FORMS-6.5-FSI-REF-SITE)
* [pacchetto dimostrativo AEM Forms We.Gov](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?orderby=%40jcr%3Acontent%2Fjcr%3AlastModified&amp;orderby.sort=desc&amp;layout=list&amp;p.offset=0&amp;p.limit=168&amp;package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffeaturepack%2Fwe-gov-forms.pkg.all-2.0.2.zip)

Per ulteriori informazioni sull&#39;utilizzo dei pacchetti, vedere [Come utilizzare i pacchetti](/help/sites-administering/package-manager.md).

Dopo aver installato i pacchetti e avviato le istanze di creazione e pubblicazione, visitate i seguenti URL nel browser:

* `https://'[server]:[port]'/wegov`
* `https://'[server]:[port]'/wefinance`

Se l&#39;installazione ha esito positivo, potete accedere alle pagine di destinazione dei siti di riferimento e We.Finance.

## (Facoltativo) Importa dati di esempio in Microsoft Dynamics {#optional-import-sample-data-into-microsoft-dynamics}

I siti di riferimento dell&#39;applicazione ipoteca principale e dell&#39;applicazione di assicurazione automatica sono configurati per utilizzare i record di Microsoft Dynamics. Il pacchetto del sito di riferimento installa un&#39;entità personalizzata e record di esempio che è possibile importare in Microsoft Dynamics per eseguire il sito di riferimento. Effettuare le seguenti operazioni per migrare e impostare i dati di esempio:

Per importare l&#39;entità personalizzata per l&#39;applicazione di assicurazione automatica:

1. Scaricate il pacchetto della soluzione **WeFinanceAutoInsurance_1_0.zip** dall&#39;istanza di `https://'[server]:[port]'/content/aemforms-refsite-collaterals/we-finance/auto-insurance/ms-dynamics/WeFinanceAutoInsurance_1_0.zip` authoring AEM.
1. Nell’istanza di Microsoft Dynamics, accedete a **Impostazioni > Soluzioni** e fate clic su **Importa**. Selezionate e importate il pacchetto.

Per importare l&#39;entità personalizzata per l&#39;applicazione di assicurazione automatica:

1. Scaricate il pacchetto **AEMFormsFSIRefsite_1_0.zip** da `https://[author]:'port'/content/aemforms-refsite-collaterals/we-finance/home-mortgage/ms-dynamics/AEMFormsFSIRefsite_1_0.zip`. Selezionate e importate il pacchetto.

1. Nell’istanza di Microsoft Dynamics, accedete a **Impostazioni > Soluzioni** e fate clic su **Importa**. Selezionate e importate il pacchetto.

Per importare i record cliente e polizza assicurativa:

1. Scaricate i file di dati **We.Finance Customers.csv, We.Finance Auto Insurance Renewals.csv** e **home ipoteca** dalle seguenti posizioni nell&#39;istanza di autore AEM:

   * `https://'server':[port/content/aemforms-refsite-collaterals/we-finance/auto-insurance/ms-dynamics/We.Finance Customers.csv`
   * `https://'server':[port/content/aemforms-refsite-collaterals/we-finance/auto-insurance/ms-dynamics/We.Finance Auto Insurance Renewals.csv`
   * `https://'[server]:[port]'/content/aemforms-refsite-collaterals/we-finance/home-mortgage/ms-dynamics/Sarah%20Rose%20Contact.csv`

1. Nell’istanza di Microsoft Dynamics, effettuate le seguenti operazioni:

   * Vai a **Vendite** > Clienti **** We.Finance e fai clic su **Importa**.

   * Vai a **Vendite** > **We.Finance Auto Insurance** e fai clic su **Importa**.

   * Vai a **Vendite** > **We.Finance Home Mort** e fai clic su **Importa**.

## Configurare il servizio cloud OAuth per Microsoft Dynamics {#configure-oauth-cloud-service-for-microsoft-dynamics}

Configurare il servizio cloud OAuth in  AEM Forms per abilitare la comunicazione tra  AEM Forms e Microsoft Dynamics. Effettuate le seguenti operazioni per configurare l’Cloud Service OAuth sulle istanze di creazione e pubblicazione AEM:

1. AEM’istanza di creazione, andate a **Strumenti** > **Cloud Services** > Origini **** dati > **globale**. Tocca l&#39;icona **Refsite Dynamics Integration** e tocca Proprietà.
1. Accedere all&#39;account Microsoft Azure Active Directory. Aggiungete l&#39;URL di configurazione del servizio cloud copiato nell&#39;impostazione **Rispondi URL** per l&#39;applicazione registrata. Salva la configurazione.
1. Nella scheda Impostazioni autenticazione, specificate **Origine** servizio, ID **** client, Segreto **** cliente e URL **** risorsa per l&#39;istanza di Microsoft Dynamics. Fate clic su **Connetti a OAuth** per reindirizzare alla pagina di accesso di Microsoft Dynamics.
1. Immettete le credenziali di accesso. Una volta effettuato l&#39;accesso, verrete reindirizzati alla pagina di configurazione del servizio cloud  AEM Forms. Fai clic su **Salva e chiudi**. La configurazione del servizio cloud viene salvata.
1. Vai a **Forms** > Integrazioni **** dati > **We.Finance**. Selezionare Auto Insurance (Dynamics) e fare clic su Edit (Modifica). Le entità di Microsoft Dynamics sono elencate nella scheda Origini dati. Attendere che tutte le entità siano recuperate da Microsoft Dynamics ed elencate nella scheda origini dati.
1. Selezionare l&#39;entità **** AutoInsuranceRenewal e fare clic su **Test Model Object**. Nella sezione della richiesta di input, specificate il valore per l&#39;ID cliente come &quot;900001&quot; e fate clic su **Test**. Nella sezione Output vengono visualizzati i record recuperati da Microsoft Dynamics per ID cliente 900001.
1. Nella sezione della richiesta di input, specificate il valore per l&#39;ID cliente come &quot;900001&quot; e fate clic su **Test**. Nella sezione Output vengono visualizzati i record recuperati da Microsoft Dynamics per ID cliente 900001.
1. Ripetete i passaggi da 1 a 6 sull’istanza di pubblicazione.

## Configurare  pianificazione Adobe Sign {#scheduler}

Per le istanze di creazione e pubblicazione effettuate le seguenti operazioni:

1. Passate AEM console Configurazione Web all&#39;indirizzo `https://'[server]:[port]'system/console/configMgr`.
1. Individuate e toccate **[!UICONTROL servizio]** di configurazione Adobe Sign per aprirlo alla configurazione.
1. Configurare l&#39;espressione **[!UICONTROL del pianificatore di aggiornamento]** dello stato come **0 0/2 * * ?**.

   >[!NOTE]
   >
   >La configurazione del pianificatore di cui sopra verifica lo stato del servizio Adobe Sign  ogni due minuti.

1. Toccate **[!UICONTROL Salva]**.

## Configurare il sito di riferimento  servizio cloud Adobe Sign {#sign-service}

Per le istanze di creazione e pubblicazione effettuate le seguenti operazioni:

1. Vai a **Strumenti** > **Cloud Services** > **Adobe Sign** > **globale**. Selezionare **AEM Forms Reference Site Sign** e toccare Proprietà.

   >[!CAUTION]
   >
   >Accertatevi che l&#39; `https://[host]:[ssl_port]/mnt/overlay/adobesign/cloudservices/adobesign/properties.html` URL venga aggiunto all&#39;elenco URL di reindirizzamento della configurazione OAuth &#39;applicazione API Adobe Sign.

1. Specificate l&#39;ID client e il segreto della configurazione OAuth dell&#39;applicazione Adobe Sign .
1. (Facoltativo) Selezionate anche **[!UICONTROL l&#39;opzione]** Abilita  Adobe Sign per gli allegati e toccate **[!UICONTROL Connetti per  Adobe Sign]**. Aggiunge i file allegati a un modulo adattivo al documento Adobe Sign  corrispondente inviato per la firma.
1. Toccate **[!UICONTROL Connect per  Adobe Sign]** ed effettuate l&#39;accesso con le credenziali Adobe Sign .

## Configurare Forms Common Configuration Service {#anonymous}

Effettuate le seguenti operazioni nell’istanza di pubblicazione per consentire l’accesso agli utenti anonimi:

1. Passate AEM console Configurazione Web all&#39;indirizzo `https://'[server]:[port]'/system/console/configMgr`.
1. Individuate e toccate **[!UICONTROL Forms Common Configuration Service]** per aprirlo alla configurazione.
1. Configura il campo **[!UICONTROL Consenti]** per **[!UICONTROL tutti gli utenti]**.
1. Toccate **[!UICONTROL Salva]**.

## Modifica servizio di riposo per il modello dati del modulo {#fdm}

Per le istanze di creazione e pubblicazione effettuate le seguenti operazioni:

1. Vai a CRXDE a `https://'[server]:[port]'/crx/de/index.jsp`.
1. Andate a **/conf/global/settings/cloudconfigs/fdm/roi-rest/jcr:content/swaggerFile** e aprite il file swagger.
1. Aggiornate le impostazioni di host e porta in base all&#39;ambiente in uso.
1. Salvate le impostazioni.
1. (Solo **istanza** Author) Vai a **Strumenti** > **Cloud Services** > **Origini** dati > **globale**. Selezionate **roi-rest** e toccate **Properties**.Toccate Impostazioni **** autenticazione e impostate Tipo **** autenticazione su Autenticazione **** di base. Specificate `admin`/ `admin`come nome utente/password per accedere al servizio. Toccate **Salva e chiudi**.

## Integrazione con il Marketing Cloud {#integrate-with-marketing-cloud}

È possibile integrare il  AEM Forms con  Adobe Analytics e  Adobe Target.  Adobe Analytics consente di generare report e analizzare le prestazioni dei moduli adattivi, mentre  Adobe Target consente di distribuire esperienze personalizzate ed eseguire test A/B per i moduli adattivi.

Effettuate le seguenti operazioni per configurare  Adobe Analytics e  Adobe Target  AEM Forms.

### Configurare  Adobe Analytics {#configureanalytics}

&#39;integrazione AEM Forms con  Adobe Analytics consente di monitorare e analizzare in che modo i clienti interagiscono con moduli e documenti. Consente di identificare e risolvere le aree problematiche e di agire per aumentare il tasso di conversione.

Per provare questa funzionalità nel sito di riferimento, configura il tuo account Analytics come descritto in [Configurazione di analisi e rapporti](../../forms/using/configure-analytics-forms-documents.md).

Per generare un rapporto, i dati iniziali vengono raggruppati con i siti di riferimento. Prima di utilizzare i dati iniziali, effettuate le seguenti operazioni:

1. Verifica che le configurazioni di analisi We.Finance siano disponibili nei servizi AEM Cloud. Puoi trovare i servizi cloud in uno dei seguenti modi:

   * Accedete a **[!UICONTROL Strumenti>Cloud Services>Cloud Services]** legacy oppure selezionate https://&lt;host>:&lt;porta>/libs/cq/core/content/tools/cloudservices.html.
   * Nella pagina **[!UICONTROL Cloud Services]** , nella sezione **[!UICONTROL Adobe Analytics]** , fate clic su `Show Configurations`. Potete vedere le configurazioni We.Finance disponibili. Fate clic per aprire la configurazione. Nella pagina di configurazione, fate clic su **[!UICONTROL Modifica]**. Specifica società, nome utente, segreto condiviso (password) e centro dati validi e fai clic su **[!UICONTROL Connetti ad Analytics]**. Una volta visualizzata la finestra di dialogo Connessione, fate clic su **[!UICONTROL OK]** nella finestra di dialogo di configurazione. Configurate il framework nella configurazione di Analytics come descritto in [Configurazione di Analytics e Report](../../forms/using/configure-analytics-forms-documents.md).

1. Andate a https://&lt;*host*>:&lt;*porta*>/system/console/configMgr ed effettuate le seguenti operazioni:

   * Nella pagina Configurazione **[!UICONTROL console]** Web, individua e fai clic su **[!UICONTROL Configurazione]** AEM Forms Analytics.

   * Nel campo **[!UICONTROL Framework]** SiteCatalyst della finestra di dialogo Configurazione AEM Forms Analytics , selezionate we-finance(we-finance) o we-gov(we-gov).
   * Fate clic su **[!UICONTROL Salva]** e lasciate che la pagina venga aggiornata.

1. Passare a Forms Manager all&#39;indirizzo https://&lt;host>:&lt;porta>/aem/forms ed effettuare le seguenti operazioni:

   * Aprire la cartella We.Finance e selezionare il modulo per il quale si desidera visualizzare il rapporto.
   * Fate clic su Abilita analisi nella barra degli strumenti Azioni. Dopo aver attivato l&#39;analisi del modulo, fai clic su Rapporto analisi. Potete visualizzare un rapporto vuoto generato. Dopo la generazione di un report vuoto, devi fornire i dati iniziali forniti con il pacchetto refsite per generare report di analisi a scopo dimostrativo.

   I siti di riferimento forniscono report di analisi con dati iniziali per i casi di utilizzo di carte di credito, ipoteche per la casa e assistenza ai bambini.

### Configurare Target {#configure-target}

Il sito di riferimento mostra l&#39;integrazione di  AEM Forms con  Adobe Target che consente di includere contenuti mirati e personalizzati nei documenti adattivi. Consente inoltre di creare test A/B per i moduli adattivi.

Per provare l&#39;integrazione nel sito di riferimento, effettuate le seguenti operazioni per configurare Target in AEM:

1. Avviate l&#39;argomento jvm dell&#39;autore `-Dabtesting.enabled=true` per abilitare i test A/B sul server.

   >[!NOTE]
   >
   >Se l&#39;istanza AEM è in esecuzione su JBoss, che viene avviata come servizio dall&#39;installazione di Turnkey, aggiungere il `-Dabtesting.enabled=true` parametro nella seguente voce del `jboss\bin\standalone.conf.bat` file:
   `set "JAVA_OPTS=%JAVA_OPTS% -Dadobeidp.serverName=server1 -Dfile.encoding=utf8 -Djava.net.preferIPv4Stack=true -Dabtesting.enabled=true"`

1. Accesso `https://<hostname>:<port>/libs/cq/core/content/tools/cloudservices.html`.

1. Nella **[!UICONTROL sezione Adobe Target]** , fate clic su **[!UICONTROL Mostra configurazioni]**. È possibile visualizzare la configurazione di destinazione We.Finance disponibile. Fate clic per aprire la configurazione. Nella pagina di configurazione, fate clic su **[!UICONTROL Modifica]**. Viene visualizzata la finestra di dialogo **[!UICONTROL Modifica componente]** per la configurazione.

1. Specifica il codice cliente, l&#39;e-mail e la password associati all&#39;account Target. Selezionate il tipo di API **[!UICONTROL REST]**.
1. Click **[!UICONTROL Connect to Adobe target]**. Una volta configurato l&#39;account Target, fate clic su **[!UICONTROL OK]**. Potete vedere che la configurazione del pacchetto include un framework di Target.

1. Passa a `https://<hostname>:<port>/system/console/configMgr`.

1. Fate clic su **[!UICONTROL Configurazione]** AEM Forms Target.
1. Selezionate un framework Target.
1. Nel campo URL **** Target, specificate l&#39;URL per  AEM Forms. Esempio: `https://<hostname>:<port>/`.

1. Fai clic su **[!UICONTROL Salva]**.

I casi di utilizzo di applicazioni con carta di credito e applicazioni con ipoteche domestiche dimostrano come eseguire test A/B e presentare un rapporto a scopo dimostrativo. Per informazioni dettagliate, vedere la procedura dettagliata sul sito di riferimento [We.Finance](../../forms/using/finance-reference-site-walkthrough.md).

## Next step {#next-step}

Ora siete tutti impostati per esplorare il sito di riferimento. Per ulteriori informazioni sul flusso di lavoro e i passaggi del sito di riferimento, vedi:

* [Procedura dettagliata sul sito di riferimento We.Finance](../../forms/using/finance-reference-site-walkthrough.md)
* [Procedura dettagliata sul sito di riferimento self-service dei dipendenti](../../forms/using/employee-self-service-reference-site.md)

