---
title: Connettore SharePoint
seo-title: SharePoint Connector
description: Connettore Day JCR per Microsoft SharePoint 2010 e Microsoft SharePoint 2013, versione 4.0.
seo-description: Learn about the Sharepoint Connector in AEM.
uuid: df650476-4e2a-486f-a007-b5ac437ff99f
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 907316d1-3d23-4c46-bccb-bad6fe1bd1bb
docset: aem65
exl-id: 10ea7d2e-6e44-4d5c-a2b2-63c73b18f172
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '1562'
ht-degree: 3%

---

# Connettore SharePoint{#sharepoint-connector}

Questo articolo include informazioni dettagliate sul connettore JCR di Adobe per Microsoft SharePoint 2010 e Microsoft SharePoint 2013, versione 4.0.

Il connettore SharePoint supporta le seguenti funzionalità di base:

* Lettura di contenuti e metadati da SharePoint.
* Riconoscimento delle impostazioni di protezione di SharePoint per il contenuto a cui si accede applicando l&#39;autenticazione e l&#39;autorizzazione native di SharePoint
* Integrazione dei contenuti tramite Content Finder
* Utilizzo di componenti AEM, ad esempio risorse esterne, per visualizzare immagini e video SharePoint
* Sincronizzazione di SharePoint con AEM Assets

Tutte le funzionalità vengono implementate utilizzando i servizi web nativi di SharePoint come interfaccia per i contenuti e i servizi SharePoint.

>[!NOTE]
>
>Il connettore SharePoint è supportato anche con AEM 6.1 service pack 2. Il connettore non supporta più il montaggio dell’archivio virtuale e, pertanto, non può essere montato. Se desideri accedere all’archivio di Sharepoint utilizzando le API Java, utilizza l’implementazione dell’archivio JCR del connettore Sharepoint nel progetto.
>
>L&#39;installazione, la configurazione, la gestione e le operazioni IT del server SharePoint e della relativa infrastruttura IT non rientrano nell&#39;ambito del presente documento. Consulta la documentazione del fornitore su [SharePoint](https://www.microsoft.com/sharepoint) per informazioni su questi argomenti. Il connettore richiede che queste parti dell&#39;infrastruttura siano installate, configurate e gestite correttamente.

## Guida introduttiva {#getting-started}

Per iniziare a utilizzare il connettore, eseguire le operazioni seguenti:

* Verifica che sia installato almeno Java 7.
* Scarica il file di distribuzione del pacchetto del connettore da Software Distribution.
* Copia un valore valido *license.properties* nella directory che contiene *cq-quickstart-6.4.0.jar* file.

* Tocca o fai doppio clic sul file .jar per avviare AEM oppure avvialo dalla riga di comando.
* Installa il pacchetto del connettore da Gestione pacchetti.
* Configura le opzioni del connettore.

## Installazione del connettore SharePoint {#installing-sharepoint-connector}

Il connettore è un pacchetto di contenuti che facilita l&#39;installazione. Installa il pacchetto utilizzando Gestione pacchetti, quindi imposta l’URL del server SharePoint e altre opzioni di configurazione. Il contenuto SharePoint è disponibile nell’archivio AEM.

### Requisiti di installazione {#installation-requirements}

Il connettore richiede quanto segue:

* Java Runtime Environment 1.7 o versione successiva
* Servizi Web SharePoint disponibili tramite la rete
* URL del server SharePoint
* Credenziali utente e autorizzazioni per gli archivi CRX e SharePoint
* [Piattaforme supportate](#supported-platforms)

Il connettore SharePoint è disponibile per il download da [Distribuzione di software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/featurepack/cq-6.3.0-featurepack-17673).

### Piattaforme supportate {#supported-platforms}

Il connettore supporta quanto segue:

* Versioni AEM:

   * AEM 6.4, 6.3

* Versioni di Microsoft SharePoint:

   * Microsoft Office SharePoint Server (MOSS) 2010
   * Microsoft Office SharePoint Server (MOSS) 2013

* Se hai bisogno di supporto per le distribuzioni personalizzate del connettore (OEM, requisiti speciali, metodi di autenticazione personalizzati), contatta l’ufficio Adobe della tua regione.

>[!NOTE]
>
>Il connettore supporta solo configurazioni ufficialmente supportate da Microsoft. Consulta [MOSS 2010](https://technet.microsoft.com/en-us/library/cc262485(office.14).aspx) e [MOSS 2013](https://technet.microsoft.com/en-us/library/cc262485.aspx) requisiti di sistema.

### Installazione standard {#standard-installation}

La Distribuzione di software viene utilizzata per distribuire funzionalità, esempi e hotfix dei prodotti. Per ulteriori informazioni, vedere [Documentazione di Software Distribution](https://experienceleague.adobe.com/docs/experience-cloud/software-distribution/home.html#software-distribution).


#### Integrazione con l’AEM {#integrating-with-aem}

Per installare il pacchetto di contenuti del connettore.

1. Apri un ticket di supporto Adobe per richiedere il pacchetto di funzioni del connettore.
1. Scarica il pacchetto quando è disponibile e quindi apri Gestione pacchetti per l’istanza AEM.
1. Tocca o fai clic **Installa** dalla pagina di descrizione del pacchetto.
1. Dalla sezione **Installa pacchetto** , tocca o fai clic su **Installa**.

   **Nota**: accertati di aver effettuato l’accesso come amministratore.

1. Quando il pacchetto viene installato, tocca o fai clic su **Chiudi**.

## Configurazione del connettore SharePoint {#configuring-sharepoint-connector}

Dopo aver installato il connettore SharePoint, configurare l&#39;applicazione e i livelli SharePoint per il connettore.

Imposta l’URL del server SharePoint per rendere il tuo archivio SharePoint compatibile con JCR. Puoi impostare parametri aggiuntivi per configurare la connessione con il server SharePoint. Inoltre, configura l’autenticazione con il connettore SharePoint.

### Configurazione della connessione con il server SharePoint {#configuring-the-connection-with-the-sharepoint-server}

Per impostare l&#39;URL del server SharePoint e le opzioni avanzate, effettuare le seguenti operazioni:

1. Passa alla console di gestione OSGi: [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr).
1. Cerca **Connettore Day JCR per Microsoft Sharepoint** pacchetto.
1. Modifica i valori di configurazione.
1. Imposta l’URL del server SharePoint come valore di **Aree di lavoro**.
1. Tocca o fai clic **Salva**.

![chlimage_1-62](assets/chlimage_1-62.png)

Parametri &quot;Workspaces&quot; e &quot;Default Workspace Name&quot; (Nome area di lavoro predefinita):

Per impostazione predefinita, il connettore espone una singola area di lavoro JCR. Il server SharePoint esposto da questa area di lavoro viene impostato tramite il parametro di configurazione &quot;URL del server di SharePoint&quot;.

Il connettore può essere configurato anche per più aree di lavoro. In questo caso, ogni area di lavoro è associata all&#39;URL del relativo server SharePoint esposto tramite l&#39;area di lavoro. Per aggiungere un&#39;area di lavoro, aggiungete una definizione di area di lavoro al parametro Workspace. Una definizione di area di lavoro ha il seguente formato:
`<name>`= `<url>` dove
`<name>` è il nome dell’area di lavoro JCR e
`<url>` è l’URL del server SharePoint per tale area di lavoro.

In AEM, esegui un ulteriore passaggio oltre ai passaggi di configurazione precedenti. Elenco consentiti di &#39;**com.day.cq.dam.cq-dam-jcr-connectors** bundle &#39;.

Per elenco consentiti di bundle nell’AEM, effettua le seguenti operazioni:

1. Passa alla console di gestione OSGi: http://localhost:4502/system/console/configMgr.
1. Cerca il servizio &quot;Apache Sling Login Admin Whitelist&quot;.
1. Seleziona **Ignora la whitelist**.
1. Aggiungi `com.day.cq.dam.cq-dam-jcr-connectors` nei bundle della whitelist predefiniti
1. Fai clic su Salva.

![chlimage_1-82](assets/chlimage_1-82a.png)

>[!NOTE]
>
>Se configurate più aree di lavoro, specificate il nome dell&#39;area di lavoro predefinita nel parametro Nome area di lavoro predefinita.

Per ulteriori informazioni sui parametri relativi all’autenticazione, consulta [Autenticazione](/help/sites-administering/sharepoint-connector.md#configuring-authentication).

### Verifica dell&#39;impostazione di Sharepoint {#verifying-the-sharepoint-setup}

Dopo aver configurato il connettore, verifica quanto segue:

* Il server SharePoint viene eseguito e i servizi web sono accessibili all’istanza del connettore
* Le credenziali utente di SharePoint sono valide e l’utente dispone delle autorizzazioni SharePoint necessarie
* Il connettore è installato e configurato correttamente

### Configurazione della sincronizzazione DAM con il server SharePoint {#configuring-dam-sync-with-the-sharepoint-server}

Per sincronizzare SharePoint Assets con l’AEM, effettua le seguenti operazioni:

1. Passa alla console di gestione OSGi: [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr).
1. Cercare il servizio &quot;Default DAMAssetSynchronization&quot;.
1. Modifica i valori di configurazione.
1. Impostare il nome utente e la password corrispondente dell&#39;utente che ha accesso al sito SharePoint.
1. Fai clic su Salva.

Abilita il servizio di sincronizzazione DAM, che è disabilitato per impostazione predefinita:

1. Passa ai componenti della console Web OSGi: [http://localhost:4502/system/console/components](http://localhost:4502/system/console/components)
1. Cerca &quot;com.day.cq.dam.jcrconnectors.impl.AssetSynchronizationService&quot;.
1. Fai clic su Abilita.

In alternativa, è possibile configurare il ritardo di sincronizzazione tra diversi cicli di sincronizzazione:

1. Passa alla console di gestione OSGi: [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr)
1. Cerca &quot;DAY CQ DAM JCR Connector Asset Synchronization Service&quot;.
1. Modifica i valori di configurazione.
1. Imposta il valore del periodo di sincronizzazione (in secondi).
1. Fai clic su Salva.

### Configurazione dell’autenticazione {#configuring-authentication}

Sharepoint include i metodi di autenticazione Classic e Basata su attestazioni, che supportano entrambi i tipi di autenticazione seguenti:

* Base
* Basato su Forms

In particolare, sono disponibili i seguenti tipi di autenticazione:

* Classic-Basic
* Classic-basato su Forms
* Claims-Basic
* Basato su Forms per attestazioni

Il connettore JCR AEM per Microsoft SharePoint 2010 e Microsoft SharePoint 2013, versione 4.0. supporta l’autenticazione basata sulle attestazioni (suggerita da Microsoft), che funziona nelle seguenti modalità:

* **Autenticazione di base/NTLM**: il connettore tenta prima di connettersi utilizzando l’autenticazione di base. Se non disponibile, viene utilizzata l&#39;autenticazione basata su NTLM.
* **Autenticazione basata su Forms**: Sharepoint convalida gli utenti in base alle credenziali digitate dagli utenti in un modulo di accesso (in genere una pagina Web). Il sistema emette un token per le richieste autenticate che contiene una chiave per ristabilire l’identità per le richieste successive.

**Configurazione dell’autenticazione basata su Forms**

Vai a: [http://localhost:4502/system/console/bundles](http://localhost:4502/system/console/bundles)

1. Fai clic su OSGI -> Configurazione
1. Cerca &quot;Day JCR Connector for Microsoft Sharepoint&quot; (Connettore JCR diurno per Sharepoint)
1. Fai clic su &quot;Modifica i valori di configurazione&quot;
1. Impostare il valore di &quot;Sharepoint Connection Factory&quot; come &quot;com.day.crx.spi.sharepoint.security.FormsBasedAuthenticationConnectionFactory&quot;
1. Fai clic su **Salva**.

**Configurazione dell&#39;autenticazione di base (Windows)**

1. [Disabilita autenticazione token](#disable-token-authentication).
1. Vai a [http://localhost:4502/system/console/bundles](http://localhost:4502/system/console/bundles).
1. Fai clic su OSGI > Configurazione.
1. Cerca **Connettore Day JCR per Microsoft Sharepoint**.
1. Clic `Edit the configuration values`.
1. Impostare il valore di Connection Factory di Sharepoint su `com.day.crx.spi.sharepoint.security.WindowsAuthenticationConnectionFactory`.
1. Fai clic su **Salva**.

Solo un utente autenticato sia su AEM che su SharePoint può accedere al contenuto SharePoint tramite il connettore.

È inoltre possibile utilizzare l’estensione del connettore per l’autenticazione per creare un modulo di autenticazione personalizzato, che, ad esempio, mappa l’accesso degli utenti AEM a utenti SharePoint specifici. Crea utenti AEM corrispondenti agli utenti SharePoint (nome utente e password devono corrispondere) per poter visualizzare il contenuto SharePoint mappato all’istanza del connettore.

Per creare un utente in AEM:

1. Accedi a http://localhost:9502/with l’utente amministratore.
1. Fare clic su Strumenti.
1. Fare clic su Protezione.
1. Fai clic su Utenti.
1. Clic **Crea utente**.
1. Specifica l’ID utente (nome utente con accesso a SharePoint).
1. Immetti la password corrispondente.
1. Fai clic sul simbolo di spunta verde per creare l’utente.

Per aggiungere l’utente nel gruppo di amministrazione:

1. Passare ad Amministrazione gruppo.
1. Fai clic sul nodo &quot;a&quot;.
1. Fare clic su ‘amministratori’.
1. Digita l’ID utente creato sopra nella casella di testo prima di **Sfoglia** pulsante.
1. Fai clic sul simbolo di spunta verde per aggiungere l’utente al gruppo di amministrazione.

### Disabilita autenticazione token {#disable-token-authentication}

1. Scaricare e installare il pacchetto `basic auth`. `zip` da Software Distribution.

1. Chiudi Quickstart.
1. Apri il file *\crx-quickstart\repository\repository.xml*.
1. Trovare il tag `<LoginModule class="com.day.crx.core.CRXLoginModule"> ... </LoginModule>.`
1. Inserire il tag `<param name="disableTokenAuth" value="true"/>` all’interno del tag indicato al punto 4.
1. Salvare e chiudere il file xml.
1. Riavviare QuickStart e accedere con le credenziali.

#### Supporto di diversi metodi di autenticazione del server SharePoint {#supporting-different-authentication-methods-of-the-sharepoint-server}

Nella versione standard, il connettore supporta IIS standard **Windows** autenticazione di base e autenticazione basata su Forms (basata su token). Il [altri metodi di autenticazione](https://technet.microsoft.com/en-us/library/cc262350.aspx#section2) possono essere supportate tramite il meccanismo di estensibilità.

I passaggi seguenti forniscono indicazioni sull’estensione dell’autenticazione standard per supportare vari metodi di autenticazione del server SharePoint:

1. Implementare `com.day.crx.spi.sharepoint.security.SharepointConnectionFactory` per gestire il lato client del processo di autenticazione specifico.
1. Installare `SharepointConnectionFactory` implementazione come bundle di frammenti con host frammenti `com.day.crx.spi.crx2sharepoint-bundle`.

   Quando utilizzi Maven, adatta la seguente configurazione di `maven-bundle-plugin` in base alle esigenze del progetto:

   ```xml
              <plugin>
                  <groupId>org.apache.felix</groupId>
                  <artifactId>maven-bundle-plugin</artifactId>
                  <extensions>true</extensions>
                  <configuration>
                      <instructions>
                          <Export-Package />
                          <Private-Package>
                              <!-- your private package here -->
                          </Private-Package>
                          <Fragment-Host>
                              com.day.crx.spi.crx2sharepoint-bundle
                          </Fragment-Host>
                       </instructions>
                  </configuration>
              </plugin>
   ```

1. Registra il `SharepointConnectionFactory` implementazione nella configurazione del connettore. Nella finestra di configurazione del connettore, fai clic su **Opzioni avanzate**. Nel campo per **Connection Factory di Sharepoint** , specificare il nome dell&#39;implementazione `com.day.crx.spi.sharepoint.auth.CustomConnectionFactory`.

1. Riavviare il connettore.
