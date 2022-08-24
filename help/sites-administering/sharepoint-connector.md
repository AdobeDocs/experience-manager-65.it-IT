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

Questo articolo include informazioni dettagliate sul connettore Adobe JCR per Microsoft SharePoint 2010 e Microsoft SharePoint 2013, versione 4.0.

Il connettore SharePoint supporta le seguenti funzionalità di base:

* Lettura di contenuti e metadati da SharePoint.
* Riconoscere le impostazioni di sicurezza SharePoint per il contenuto a cui si accede applicando l’autenticazione e l’autorizzazione native di SharePoint
* Integrazione dei contenuti tramite Content Finder
* Utilizzo di componenti AEM, ad esempio Risorse esterne per visualizzare immagini e video SharePoint
* Sincronizzazione di SharePoint con AEM Assets

Tutte le funzionalità vengono implementate utilizzando i servizi web nativi di SharePoint come interfaccia per i contenuti e i servizi SharePoint.

>[!NOTE]
>
>SharePoint Connector è supportato anche con AEM service pack 2 6.1. Il connettore non supporta più il montaggio dell&#39;archivio virtuale e, pertanto, non può essere montato. Se desideri accedere all’archivio Sharepoint utilizzando le API Java, utilizza l’implementazione dell’archivio JCR del connettore Sharepoint nel tuo progetto.
>
>L&#39;installazione, la configurazione, la gestione e le operazioni IT del server SharePoint e della relativa infrastruttura IT non rientrano nell&#39;ambito di applicazione di questo documento. Consulta la documentazione del fornitore su [SharePoint](https://www.microsoft.com/sharepoint) per informazioni su questi argomenti. Il connettore richiede che queste parti dell&#39;infrastruttura siano installate, configurate e gestite correttamente.

## Guida introduttiva {#getting-started}

Per iniziare a utilizzare il connettore, procedi come segue:

* Assicurati di avere installato almeno Java 7.
* Scarica il file di distribuzione del pacchetto del connettore da Distribuzione di software.
* Copia un valore valido *license.properties* alla directory che contiene il *cq-quickstart-6.4.0.jar* file.

* Tocca o fai doppio clic sul file .jar per avviare AEM o avviarlo dalla riga di comando.
* Installa il pacchetto del connettore da Gestione pacchetti.
* Configura le opzioni del connettore.

## Installazione del connettore SharePoint {#installing-sharepoint-connector}

Il connettore è un pacchetto di contenuti che facilita l&#39;installazione. Installa il pacchetto utilizzando Gestione pacchetti, quindi imposta l&#39;URL del server SharePoint e altre opzioni di configurazione. Il contenuto SharePoint è disponibile nell’archivio AEM.

### Requisiti di installazione {#installation-requirements}

Il connettore richiede quanto segue:

* Java Runtime Environment 1.7 o versione successiva
* Servizi Web SharePoint disponibili in rete
* URL del server SharePoint
* Credenziali utente e autorizzazioni per gli archivi CRX e SharePoint
* [Piattaforme supportate](#supported-platforms)

Il connettore SharePoint è disponibile per il download da [Distribuzione di software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/featurepack/cq-6.3.0-featurepack-17673).

### Piattaforme supportate {#supported-platforms}

Il connettore supporta le seguenti funzioni:

* Versioni AEM:

   * AEM 6.4, 6.3

* Versioni Microsoft SharePoint:

   * Microsoft Office SharePoint Server (MOSS) 2010
   * Microsoft Office SharePoint Server (MOSS) 2013

* Se hai bisogno di supporto per le distribuzioni personalizzate del connettore (OEM, requisiti speciali, metodi di autenticazione personalizzati), contatta l&#39;ufficio Adobe della tua area.

>[!NOTE]
>
>Il connettore supporta solo le configurazioni supportate ufficialmente da Microsoft. Vedi [MOSS 2010](https://technet.microsoft.com/en-us/library/cc262485(office.14).aspx) e [MOSS 2013](https://technet.microsoft.com/en-us/library/cc262485.aspx) requisiti di sistema.

### Installazione standard {#standard-installation}

La Distribuzione di software viene utilizzata per distribuire funzionalità di prodotto, esempi e hotfix. Per ulteriori informazioni, consulta la sezione [Documentazione sulla distribuzione del software](https://experienceleague.adobe.com/docs/experience-cloud/software-distribution/home.html#software-distribution).


#### Integrazione con AEM {#integrating-with-aem}

Per installare il pacchetto di contenuti del connettore.

1. Apri un ticket di supporto Adobe per richiedere il pacchetto di funzionalità del connettore.
1. Scarica il pacchetto quando è disponibile e quindi apri Gestione pacchetti per la tua istanza AEM.
1. Tocca o fai clic su **Installa** dalla pagina di descrizione del pacchetto.
1. Da **Installa pacchetto** finestra di dialogo, tocca/fai clic **Installa**.

   **Nota**: Assicurati di aver effettuato l&#39;accesso come amministratore.

1. Quando il pacchetto è installato, tocca o fai clic su **Chiudi**.

## Configurazione del connettore SharePoint {#configuring-sharepoint-connector}

Dopo aver installato il connettore SharePoint, configura l’applicazione e i livelli SharePoint per il connettore.

Imposta l&#39;URL del server SharePoint per rendere l&#39;archivio SharePoint compatibile con JCR. Puoi impostare parametri aggiuntivi per configurare la connessione con il server SharePoint. Inoltre, configura l’autenticazione con il connettore SharePoint.

### Configurazione della connessione con il server SharePoint {#configuring-the-connection-with-the-sharepoint-server}

Per impostare l’URL del server SharePoint e le opzioni avanzate, effettua le seguenti operazioni:

1. Passa alla console di gestione OSGi: [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr).
1. Cerca il **Connettore Day JCR per Microsoft Sharepoint** pacchetto.
1. Modifica i valori di configurazione.
1. Imposta l’URL del server SharePoint come valore di **Aree di lavoro**.
1. Tocca o fai clic su **Salva**.

![chlimage_1-62](assets/chlimage_1-62.png)

Parametri &quot;Workspace&quot; e &quot;Nome area di lavoro predefinito&quot;:

Per impostazione predefinita, il connettore espone una singola area di lavoro JCR. Il server SharePoint esposto da questa area di lavoro viene impostato tramite il parametro di configurazione &quot;URL server di SharePoint&quot;.

Il connettore può essere configurato anche per più aree di lavoro. In questo caso, ogni area di lavoro è associata all’URL del rispettivo server SharePoint esposto tramite l’area di lavoro. Per aggiungere un’area di lavoro, aggiungi una definizione dell’area di lavoro al parametro Workspace. Una definizione di area di lavoro ha il formato seguente:
`<name>`= `<url>` dove
`<name>` è il nome dell’area di lavoro JCR e
`<url>` è l&#39;URL del server SharePoint per quell&#39;area di lavoro.

In AEM, esegui un altro passaggio oltre ai passaggi di configurazione indicati sopra. Elenco consentiti di &quot;**com.day.cq.dam.cq-dam-jcr-connectors**&#39; bundle.

Per elenco consentiti dei bundle in AEM, esegui i seguenti passaggi:

1. Passa alla console di gestione OSGi: http://localhost:4502/system/console/configMgr.
1. Cerca il servizio &quot;Apache Sling Login Admin Whitelist&quot;.
1. Seleziona **Ignora la whitelist**.
1. Aggiungi `com.day.cq.dam.cq-dam-jcr-connectors` nei bundle della whitelist predefiniti
1. Fai clic su Salva.

![chlimage_1-82](assets/chlimage_1-82a.png)

>[!NOTE]
>
>Se si configurano più aree di lavoro, specificare il nome dell&#39;area di lavoro predefinita nel parametro Nome area di lavoro predefinito.

Per ulteriori informazioni sui parametri correlati all’autenticazione, consulta [Autenticazione](/help/sites-administering/sharepoint-connector.md#configuring-authentication).

### Verifica della configurazione di Sharepoint {#verifying-the-sharepoint-setup}

Dopo aver configurato il connettore, verifica quanto segue:

* Il server SharePoint viene eseguito e i servizi Web sono accessibili all’istanza del connettore
* Le credenziali utente di SharePoint sono valide e l&#39;utente dispone delle autorizzazioni SharePoint necessarie
* Il connettore viene installato e configurato correttamente

### Configurazione della sincronizzazione DAM con il server SharePoint {#configuring-dam-sync-with-the-sharepoint-server}

Per sincronizzare le risorse SharePoint con AEM, esegui le seguenti operazioni:

1. Passa alla console di gestione OSGi: [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr).
1. Cerca il servizio &quot;Default DAMAssetSynchronization&quot;.
1. Modifica i valori di configurazione.
1. Impostare il nome utente e la password corrispondente dell&#39;utente che ha accesso al sito SharePoint.
1. Fai clic su Salva.

Abilita il servizio di sincronizzazione DAM, disattivato per impostazione predefinita:

1. Passa ai componenti della console Web OSGi: [http://localhost:4502/system/console/components](http://localhost:4502/system/console/components)
1. Cerca &quot;com.day.cq.dam.jcrConnectors.impl.AssetSynchronizationService&quot;.
1. Fare clic su Abilita.

Facoltativamente, puoi configurare il ritardo di sincronizzazione tra diversi cicli di sincronizzazione:

1. Passa alla console di gestione OSGi: [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr)
1. Cerca &quot;DAY CQ DAM JCR Connector Asset Synchronization Service&quot;.
1. Modifica i valori di configurazione.
1. Imposta il valore del periodo di sincronizzazione (in secondi).
1. Fai clic su Salva.

### Configurazione dell’autenticazione {#configuring-authentication}

Sharepoint include i metodi di autenticazione basati su attestazioni e classici, che supportano entrambi i seguenti tipi di autenticazione:

* Base
* Basato su Forms

In particolare, sono disponibili i seguenti tipi di autenticazione:

* Classic-Basic
* Basato su Forms classico
* Claims-Basic
* Basato su Forms

Il connettore JCR AEM per Microsoft SharePoint 2010 e Microsoft SharePoint 2013, versione 4.0. supporta l’autenticazione basata sulle attestazioni (suggerita da Microsoft), che funziona nelle seguenti modalità:

* **Autenticazione di base/NTLM**: Il connettore tenta innanzitutto di connettersi utilizzando l’autenticazione di base. Se non disponibile, passa all’autenticazione basata su NTLM.
* **Autenticazione basata su Forms**: Sharepoint convalida gli utenti in base alle credenziali che gli utenti digitano in un modulo di accesso (in genere una pagina web). Il sistema invia un token per le richieste autenticate che contiene una chiave per ripristinare l’identità per le richieste successive.

**Configurazione dell’autenticazione basata su Forms**

Vai a: [http://localhost:4502/system/console/bundles](http://localhost:4502/system/console/bundles)

1. Fai clic su OSGI -> Configurazione
1. Cerca &quot;Connettore JCR Day per Microsoft Sharepoint&quot;
1. Fai clic su &quot;Modifica i valori di configurazione&quot;
1. Imposta il valore di &quot;Sharepoint Connection Factory&quot; come &quot;com.day.crx.spi.sharepoint.security.FormsBasedAuthenticationConnectionFactory&quot;
1. Fai clic su **Salva**.

**Configurazione dell&#39;autenticazione di base (Windows)**

1. [Disattiva autenticazione token](#disable-token-authentication).
1. Vai a [http://localhost:4502/system/console/bundles](http://localhost:4502/system/console/bundles).
1. Fai clic su OSGI > Configurazione.
1. Cerca **Connettore Day JCR per Microsoft Sharepoint**.
1. Clic `Edit the configuration values`.
1. Imposta il valore di Sharepoint Connection Factory su `com.day.crx.spi.sharepoint.security.WindowsAuthenticationConnectionFactory`.
1. Fai clic su **Salva**.

Solo un utente autenticato sia su AEM che su SharePoint può accedere al contenuto SharePoint tramite il connettore.

Puoi anche utilizzare l’estensione del connettore per l’autenticazione per creare un modulo di autenticazione personalizzato, che, ad esempio, mappa l’accesso degli utenti AEM a specifici utenti SharePoint. Crea utenti AEM corrispondenti agli utenti SharePoint (nome utente e password devono corrispondere) per poter vedere il contenuto SharePoint mappato all&#39;istanza del connettore.

Per creare un utente in AEM:

1. Accedi a http://localhost:9502/with l&#39;utente amministratore.
1. Fare clic su Strumenti.
1. Fare clic su Protezione.
1. Fai clic su Utenti.
1. Fai clic su **Crea utente**.
1. Fornisci l&#39;ID utente (nome utente con accesso su SharePoint).
1. Immetti la password corrispondente.
1. Fare clic sul simbolo di spunta verde per creare l&#39;utente.

Per aggiungere l&#39;utente nel gruppo di amministrazione:

1. Vai a Amministrazione gruppo.
1. Fai clic sul nodo &quot;a&quot;.
1. Fai clic su &quot;amministratori&quot;.
1. Digita l’ID utente creato sopra nella casella di testo prima di **Sfoglia** pulsante .
1. Fai clic sul simbolo di spunta verde per aggiungere l&#39;utente al gruppo di amministrazione.

### Disattiva autenticazione token {#disable-token-authentication}

1. Scarica e installa il pacchetto `basic auth`. `zip` da Distribuzione software.

1. Chiudi Quickstart.
1. Apri il file . *\crx-quickstart\repository\repository.xml*.
1. Trova il tag `<LoginModule class="com.day.crx.core.CRXLoginModule"> ... </LoginModule>.`
1. Inserire il tag `<param name="disableTokenAuth" value="true"/>` all’interno del tag menzionato al punto 4.
1. Salva e chiudi il file xml.
1. Riavvia QuickStart e accedi con le tue credenziali.

#### Supporto di diversi metodi di autenticazione del server SharePoint {#supporting-different-authentication-methods-of-the-sharepoint-server}

Nella versione standard, il connettore supporta IIS standard **Windows** autenticazione (di base) e autenticazione basata su Forms (basata su token). La [altri metodi di autenticazione](https://technet.microsoft.com/en-us/library/cc262350.aspx#section2) può essere supportato tramite il meccanismo di estensibilità.

I passaggi seguenti forniscono linee guida sull’estensione dell’autenticazione standard per supportare vari metodi di autenticazione del server SharePoint:

1. Implementare `com.day.crx.spi.sharepoint.security.SharepointConnectionFactory` per gestire il lato client del processo di autenticazione specifico.
1. Installa il `SharepointConnectionFactory` implementazione come bundle di frammenti con host frammento `com.day.crx.spi.crx2sharepoint-bundle`.

   Quando utilizzi Maven, adatta la seguente configurazione del `maven-bundle-plugin` ai requisiti del progetto:

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

1. Registrare `SharepointConnectionFactory` implementazione nella configurazione del connettore. Nella finestra di configurazione del connettore, fai clic su **Opzioni avanzate**. Nella sezione **Sharepoint Connection Factory** campo , specifica il nome dell’implementazione `com.day.crx.spi.sharepoint.auth.CustomConnectionFactory`.

1. Riavvia il connettore.
