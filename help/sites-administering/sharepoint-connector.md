---
title: Connettore SharePoint
seo-title: Connettore SharePoint
description: Connettore Day JCR per Microsoft SharePoint 2010 e Microsoft SharePoint 2013, versione 4.0.
seo-description: Ulteriori informazioni sul connettore Sharepoint in AEM.
uuid: df650476-4e2a-486f-a007-b5ac437ff99f
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 907316d1-3d23-4c46-bccb-bad6fe1bd1bb
docset: aem65
translation-type: tm+mt
source-git-commit: cc3a2ce7cb3dc020f5466a4b65cf5a9714e7a344
workflow-type: tm+mt
source-wordcount: '1571'
ht-degree: 1%

---


# Connettore SharePoint{#sharepoint-connector}

Questo articolo include informazioni dettagliate sul connettore JCR  Adobe per Microsoft SharePoint 2010 e Microsoft SharePoint 2013, versione 4.0.

Il connettore di SharePoint supporta le seguenti funzionalità di base:

* Lettura di contenuti e metadati da SharePoint.
* Riconoscimento delle impostazioni di protezione di SharePoint per il contenuto a cui si accede tramite l&#39;applicazione dell&#39;autenticazione e dell&#39;autorizzazione nativa di SharePoint
* Integrazione dei contenuti tramite Content Finder
* Utilizzo di componenti AEM, come Risorse esterne per visualizzare immagini e video di SharePoint
* Sincronizzazione di SharePoint con  AEM Assets

Tutte le funzionalità sono implementate utilizzando i servizi Web di SharePoint nativi come interfaccia per il contenuto e i servizi di SharePoint.

>[!NOTE]
>
>Il connettore SharePoint è supportato anche con AEM 6.1 service pack 2. Il connettore non supporta più il montaggio dell&#39;archivio virtuale e, pertanto, non può essere montato. Se desiderate accedere all&#39;archivio di SharePoint utilizzando le API Java, utilizzate l&#39;implementazione dell&#39;archivio JCR del connettore di Sharepoint nel progetto.
>
>L&#39;installazione, la configurazione, la gestione e le operazioni IT del server SharePoint e dell&#39;infrastruttura IT correlata non rientrano nell&#39;ambito del presente documento. Per informazioni su questi argomenti, consultare la documentazione del fornitore in [SharePoint](https://www.microsoft.com/sharepoint). Il connettore richiede che queste parti dell&#39;infrastruttura siano installate, configurate e gestite correttamente.


## Guida introduttiva {#getting-started}

Per iniziare a utilizzare il connettore, effettuare le seguenti operazioni:

* Accertatevi che sia installato almeno Java 7.
* Scaricate il file di distribuzione del pacchetto di connettore da Distribuzione software.
* Copiate un file *license.properties* valido nella directory che contiene il file *cq-quickstart-6.4.0.jar*.

* Tocca o fai doppio clic sul file .jar per avviare AEM oppure avviarlo dalla riga di comando.
* Installate il pacchetto del connettore da Package Manager.
* Configurare le opzioni del connettore.

## Installazione del connettore SharePoint {#installing-sharepoint-connector}

Il connettore è un pacchetto di contenuti che semplifica l&#39;installazione. Installate il pacchetto utilizzando Package Manager, quindi impostate l&#39;URL del server di SharePoint
e altre opzioni di configurazione. Il contenuto di SharePoint è disponibile nell&#39;archivio AEM.

### Requisiti di installazione {#installation-requirements}

Il connettore richiede quanto segue:

* Java Runtime Environment 1.7 o versione successiva
* SharePoint Web Services disponibile nella rete
* URL server SharePoint
* Credenziali utente e autorizzazioni per repository CRX e SharePoint
* [Piattaforme supportate](#supported-platforms)

Il connettore SharePoint è disponibile per il download da [Distribuzione software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/featurepack/cq-6.3.0-featurepack-17673).

### Piattaforme supportate {#supported-platforms}

Il connettore supporta le seguenti funzionalità:

* Versioni AEM:

   * AEM 6.4, 6.3

* Versioni di Microsoft SharePoint:

   * Microsoft Office SharePoint Server (MOSS) 2010
   * Microsoft Office SharePoint Server (MOSS) 2013

* Se è necessario il supporto per le installazioni personalizzate del connettore (OEM, requisiti speciali, metodi di autenticazione personalizzati), contattare l&#39;ufficio del Adobe  della propria area geografica.

>[!NOTE]
>
>Il connettore supporta solo le configurazioni supportate ufficialmente da Microsoft. Vedere [MOSS 2010](https://technet.microsoft.com/en-us/library/cc262485(office.14).aspx) e [MOSS 2013](https://technet.microsoft.com/en-us/library/cc262485.aspx) requisiti di sistema.

### Installazione standard {#standard-installation}

Distribuzione software viene utilizzata per distribuire funzionalità, esempi e correzioni rapide del prodotto. Per informazioni dettagliate, consultate la [documentazione sulla distribuzione del software](https://experienceleague.adobe.com/docs/experience-cloud/software-distribution/home.html#software-distribution).


#### Integrazione con AEM {#integrating-with-aem}

Per installare il pacchetto di contenuto del connettore.

1. Aprite un ticket di assistenza  Adobe per richiedere la funzionalità del connettore.
1. Scaricate il pacchetto quando è disponibile e quindi aprite Package Manager per l&#39;istanza AEM.
1. Toccate/fate clic su **Installa** nella pagina di descrizione del pacchetto.
1. Dalla finestra di dialogo **Install Package**, toccate/fate clic su **Install**.

   **Nota**: Accertatevi di aver effettuato l’accesso come amministratore.

1. Quando il pacchetto è installato, toccate o fate clic su **Chiudi**.

## Configurazione del connettore SharePoint {#configuring-sharepoint-connector}

Dopo aver installato il connettore SharePoint, configurate l&#39;applicazione e i livelli SharePoint per il connettore.

Impostate l&#39;URL del server di SharePoint per rendere l&#39;archivio di SharePoint conforme a JCR. È possibile impostare parametri aggiuntivi per configurare la connessione con il server SharePoint. Inoltre, configurate l&#39;autenticazione con il connettore SharePoint.

### Configurazione della connessione con il server SharePoint {#configuring-the-connection-with-the-sharepoint-server}

Per impostare l&#39;URL del server SharePoint e le opzioni avanzate, procedere come segue:

1. Andate alla console di gestione OSGi: [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr).
1. Cercate il pacchetto **Day JCR Connector for Microsoft Sharepoint**.
1. Modificate i valori di configurazione.
1. Impostate l&#39;URL di SharePoint Server come valore di **Workspaces**.
1. Toccate/fate clic su **Salva**.

![chlimage_1-62](assets/chlimage_1-62.png)

Parametri &#39;Workspaces&#39; e &#39;Default Workspace Name&#39;:

Per impostazione predefinita, il connettore espone un&#39;unica area di lavoro JCR. Il server SharePoint esposto da questa area di lavoro viene impostato tramite il parametro di configurazione &#39;URL server SharePoint&#39;.

Il connettore può essere configurato anche per più aree di lavoro. In questo caso, ogni area di lavoro è associata all&#39;URL del rispettivo server SharePoint esposto attraverso l&#39;area di lavoro. Per aggiungere un’area di lavoro, aggiungete una definizione dell’area di lavoro al parametro Workspaces. Una definizione di area di lavoro ha il formato seguente:
`<name>`= `<url>` dove
`<name>` è il nome dell&#39;area di lavoro JCR e
`<url>` è l&#39;URL del server di SharePoint per tale area di lavoro.

In AEM, eseguite un altro passaggio oltre ai passaggi di configurazione indicati sopra.  Elenco consentiti il bundle &quot;**com.day.cq.dam.cq-dam-jcr-connector**&quot;.

Per  pacchetti di elenco consentiti in AEM, effettuate le seguenti operazioni:

1. Andate alla console di gestione OSGi: http://localhost:4502/system/console/configMgr.
1. Cercate il servizio &quot;Apache Sling Login Admin Whitelist&quot;.
1. Selezionare **Ignora la whitelist**.
1. Aggiungi `com.day.cq.dam.cq-dam-jcr-connectors` nei bundle della whitelist predefiniti
1. Fate clic su Salva.

![chlimage_1-82](assets/chlimage_1-82a.png)

>[!NOTE]
>
>Se configurate più aree di lavoro, specificate il nome dell’area di lavoro predefinita nel parametro Nome area di lavoro predefinito.

Per ulteriori informazioni sui parametri correlati all&#39;autenticazione, vedere [Authentication](/help/sites-administering/sharepoint-connector.md#configuring-authentication).

### Verifica della configurazione di Sharepoint {#verifying-the-sharepoint-setup}

Dopo aver configurato il connettore, verificare quanto segue:

* Il server SharePoint viene eseguito e i servizi Web sono accessibili all&#39;istanza di connettore
* Le credenziali utente di SharePoint sono valide e l&#39;utente dispone delle autorizzazioni SharePoint necessarie
* Il connettore è installato e configurato correttamente

### Configurazione della sincronizzazione DAM con il server SharePoint {#configuring-dam-sync-with-the-sharepoint-server}

Per sincronizzare le risorse di SharePoint con AEM, effettua le seguenti operazioni:

1. Andate alla console di gestione OSGi: [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr).
1. Cercate il servizio &quot;Default DAMAssetSynchronization&quot;.
1. Modificate i valori di configurazione.
1. Impostate il nome utente e la password corrispondente per l&#39;utente che ha accesso al sito di SharePoint.
1. Fate clic su Salva.

Abilita il servizio di sincronizzazione DAM, che è disabilitato per impostazione predefinita:

1. Passate ai componenti della console Web OSGi: [http://localhost:4502/system/console/components](http://localhost:4502/system/console/components)
1. Cercate &quot;com.day.cq.dam.jcrconnector.impl.AssetSynchronizationService&quot;.
1. Fate clic su Abilita.

Facoltativamente, potete configurare il ritardo di sincronizzazione tra i diversi cicli di sincronizzazione:

1. Andate alla console di gestione OSGi: [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr)
1. Cercate &quot;DAY CQ DAM JCR Connector Asset Synchronization Service&quot;.
1. Modificate i valori di configurazione.
1. Impostate il valore del periodo di sincronizzazione (in secondi).
1. Fate clic su Salva.

### Configurazione dell&#39;autenticazione {#configuring-authentication}

Sharepoint include i metodi di autenticazione Classic e Basato su attestazioni, che supportano entrambi i tipi di autenticazione seguenti:

* Base
* Basato su Forms

In particolare, sono disponibili i seguenti tipi di autenticazione:

* Classic-Basic
* Basato su Forms classico
* Claims-Basic
* Claims-based Forms

Il connettore JCR AEM per Microsoft SharePoint 2010 e Microsoft SharePoint 2013, versione 4.0. supporta l&#39;autenticazione basata sulle attestazioni (suggerita da Microsoft), che funziona nelle seguenti modalità:

* **Autenticazione** di base/NTLM: Il connettore tenta innanzitutto di connettersi utilizzando l&#39;autenticazione di base. Se non disponibile, passa all&#39;autenticazione basata su NTLM.
* **Autenticazione** basata su Forms: Sharepoint convalida gli utenti in base alle credenziali che gli utenti digitano in un modulo di login (in genere una pagina Web). Il sistema emette un token per le richieste autenticate che contiene una chiave per ripristinare l&#39;identità per le richieste successive.

**Configurazione dell&#39;autenticazione basata su Forms**

Vai a: [http://localhost:4502/system/console/bundles](http://localhost:4502/system/console/bundles)

1. Fare clic su OSGI -> Configurazione
1. Cerca &quot;Connettore JCR Day per Microsoft SharePoint&quot;
1. Fate clic su &quot;Edit the configuration values&quot; (Modifica i valori di configurazione)
1. Impostate il valore di ‘Sharepoint Connection Factory’ come ‘com.day.crx.spi.sharepoint.security.FormsBasedAuthenticationConnectionFactory’
1. Fai clic su **Salva**.

**Configurazione dell&#39;autenticazione di base (Windows)**

1. [Disattiva autenticazione](#disable-token-authentication) token.
1. Andate a [http://localhost:4502/system/console/bundles](http://localhost:4502/system/console/bundles).
1. Fate clic su OSGI > Configurazione.
1. Cercare **Connettore JCR giornaliero per Microsoft Sharepoint**.
1. Clic `Edit the configuration values`.
1. Impostate il valore di Sharepoint Connection Factory su `com.day.crx.spi.sharepoint.security.WindowsAuthenticationConnectionFactory`.
1. Fai clic su **Salva**.

Solo un utente autenticato sia su AEM che su SharePoint può accedere al contenuto SharePoint tramite il connettore.

È inoltre possibile utilizzare l&#39;estensione del connettore per l&#39;autenticazione per creare un modulo di autenticazione personalizzato, che, ad esempio, mappa l&#39;accesso degli utenti AEM a specifici utenti di SharePoint. Creare utenti AEM corrispondenti agli utenti di SharePoint (il nome utente e la password devono corrispondere) per poter visualizzare il contenuto di SharePoint mappato all&#39;istanza del connettore.

Per creare un utente in AEM:

1. Accedete a http://localhost:9502/with l&#39;utente amministratore.
1. Fare clic su Strumenti.
1. Fate clic su Protezione.
1. Fate clic su Utenti.
1. Fare clic su **Crea utente**.
1. Immettete l&#39;ID utente (il nome utente che ha accesso a SharePoint).
1. Immettete la password corrispondente.
1. Fate clic sul simbolo di spunta verde per creare l’utente.

Per aggiungere l&#39;utente nel gruppo di amministrazione:

1. Vai a Amministrazione gruppo.
1. Fare clic sul nodo &quot;a&quot;.
1. Fate clic su &quot;Administrators&quot;.
1. Digitate l&#39;ID utente creato sopra nella casella di testo prima del pulsante **Sfoglia**.
1. Fate clic sul simbolo di spunta verde per aggiungere l’utente al gruppo di amministrazione.

### Disattiva autenticazione token {#disable-token-authentication}

1. Scaricate e installate il pacchetto `basic auth`. `zip` da Distribuzione software.

1. Chiudi Avvio rapido.
1. Aprire il file *\crx-quickstart\repository\repository.xml*.
1. Trova il tag `<LoginModule class="com.day.crx.core.CRXLoginModule"> ... </LoginModule>.`
1. Inserite il tag `<param name="disableTokenAuth" value="true"/>` all&#39;interno del tag indicato al punto 4.
1. Salvate e chiudete il file xml.
1. Riavvia QuickStart ed effettua l’accesso con le tue credenziali.

#### Supporto di diversi metodi di autenticazione del server SharePoint {#supporting-different-authentication-methods-of-the-sharepoint-server}

Nella versione standard, il connettore supporta l&#39;autenticazione standard IIS **Windows** (Basic) e l&#39;autenticazione basata su Forms (token). Gli [altri metodi di autenticazione](https://technet.microsoft.com/en-us/library/cc262350.aspx#section2) possono essere supportati tramite il meccanismo di estensibilità.

I passaggi seguenti forniscono linee guida sull&#39;estensione dell&#39;autenticazione standard per supportare vari metodi di autenticazione del server SharePoint:

1. Implementate `com.day.crx.spi.sharepoint.security.SharepointConnectionFactory` per gestire il lato client del processo di autenticazione specifico.
1. Installare l&#39;implementazione `SharepointConnectionFactory` come pacchetto di frammenti con l&#39;host del frammento `com.day.crx.spi.crx2sharepoint-bundle`.

   Quando si utilizza Maven, adattare la seguente configurazione di `maven-bundle-plugin` ai requisiti del progetto:

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

1. Registra l&#39;implementazione `SharepointConnectionFactory` nella configurazione del connettore. Nella finestra di configurazione del connettore, fare clic su **Opzioni avanzate**. Nel campo relativo a **Sharepoint Connection Factory**, specificare il nome dell&#39;implementazione `com.day.crx.spi.sharepoint.auth.CustomConnectionFactory`.

1. Riavviare il connettore.

