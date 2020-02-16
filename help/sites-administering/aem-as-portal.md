---
title: Portali e portlet AEM
seo-title: Portali e portlet AEM
description: Portali e portali in AEM.
seo-description: Portali e portali in AEM.
uuid: 7f9e316d-277e-4a1e-b6f3-cd89addc897b
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 99528fda-5c8c-4034-bcbe-a4cea42f694b
docset: aem65
translation-type: tm+mt
source-git-commit: 684d2d5f73d571a15c8155e7870134c28dc892b7

---


# Portali e portlet AEM{#aem-portals-and-portlets}

Il presente documento descrive quanto segue:

* Architettura di AEM Portal
* Amministrazione e configurazione di AEM come portale
* Utilizzo di AEM come portale
* Installazione, configurazione e visualizzazione del contenuto AEM in un portlet (ad esempio, un server Web)

## Architettura AEM Portal {#aem-portal-architecture}

L&#39;architettura del portale AEM include definizioni di portali e portlet.

### Che cos&#39;è un portale? {#what-is-a-portal}

Un portale è un&#39;applicazione Web che offre personalizzazione, single sign-on, integrazione dei contenuti da origini diverse e ospita il livello di presentazione dei sistemi informativi.

In AEM è possibile eseguire portlet compatibili con JSR 286. Il componente portlet consente di incorporare un portlet nella pagina. Consultate [Amministrazione del portlet](#administeringthecqcontentportlet)di contenuti AEM.

### Che cos&#39;è una portlet? {#what-is-a-portlet}

I portlet sono componenti Web distribuiti all&#39;interno di un contenitore che genera contenuto dinamico. L&#39;interfaccia portlet è inclusa in un pacchetto e distribuita come file .war all&#39;interno di un contenitore portlet. Se AEM è in esecuzione come portale, per eseguire il portlet è necessario il file .war.

Per configurare il contenuto AEM in modo che venga visualizzato in un portale, consultate [Installazione, configurazione e utilizzo di AEM in un portlet](#installingconfiguringandusingcqinaportlet).

### AEM Portal Director {#aem-portal-director}

>[!CAUTION]
>
>AEM Portal Director è obsoleto a partire da AEM 6.4.Consultate Funzioni [obsolete e rimosse](https://helpx.adobe.com/experience-manager/6-4/release-notes/deprecated-removed-features.html).

## Amministrazione di AEM Content Portlet {#administering-the-aem-content-portlet}

Il portlet dei contenuti AEM consente di visualizzare il contenuto AEM in un portale. Il portlet è disponibile `/crx-quickstart/opt/portal`e può essere personalizzato in vari modi. Ad esempio, potete personalizzare la gestione SSO/Autenticazione implementando il vostro servizio di autenticazione che genera le informazioni di autenticazione richieste affinché AEM sovrascriva il comportamento predefinito. I plug-in utilizzano un&#39;API definita che consente di aggiungere funzionalità personalizzate creando il plug-in rispetto all&#39;API. Il plug-in può essere distribuito nella porta in esecuzione. Per funzionare correttamente, è necessario configurare l’istanza di creazione e pubblicazione di AEM insieme al percorso del contenuto da visualizzare all’avvio.

Alcune delle configurazioni possono essere modificate tramite le preferenze portlet e altre mediante le configurazioni di servizio OSGi. Potete modificare queste configurazioni utilizzando i file di **configurazione** o la console Web OSGi.

### Preferenze portlet {#portlet-preferences}

Le preferenze dei portlet possono essere configurate al momento della distribuzione nel server del portale o modificando il file **WEB-INF/portlet.xml** prima di distribuire l&#39;applicazione Web portlet. Il file portlet.xml viene visualizzato come segue per impostazione predefinita:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<portlet-app xmlns="https://java.sun.com/xml/ns/portlet/portlet-app_1_0.xsd"
             xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
             xsi:schemaLocation="https://java.sun.com/xml/ns/portlet/portlet-app_1_0.xsd /opt/SUNWps/dtd/portlet.xsd"
             version="1.0">
   <portlet>
      <portlet-name>RSSWeatherPortlet</portlet-name>
      <portlet-class>org.jboss.portlet.weather.WeatherPortlet</portlet-class>
      <init-param>
         <name>default_zipcode</name>
         <value>05673</value>
      </init-param>
      <init-param>
         <name>RSS_XSL</name>
         <value>/WEB-INF/Rss.xsl</value>
      </init-param>
      <init-param>
         <name>base_url</name>
         <value>https://xml.weather.yahoo.com/forecastrss?p=</value>
      </init-param>
      <expiration-cache>180</expiration-cache>
      <supports>
         <mime-type>text/html</mime-type>
         <portlet-mode>VIEW</portlet-mode>
         <portlet-mode>EDIT</portlet-mode>
      </supports>
      <portlet-info>
         <title>Weather Portlet</title>
      </portlet-info>
      <portlet-preferences>
         <preference>
            <name>expires</name>
            <value>180</value>
         </preference>
         <preference>
            <name>RssXml</name>
            <value>https://xml.weather.yahoo.com/forecastrss?p=33145</value>
            <read-only>false</read-only>
         </preference>
      </portlet-preferences>
   </portlet>
</portlet-app>
```

Il portlet può essere configurato con le seguenti preferenze:

<table>
 <tbody>
  <tr>
   <td>startPath</td>
   <td><p>Percorso iniziale del portlet: definisce il contenuto inizialmente visualizzato.</p> <p><strong>Importante</strong>: Se il portlet è configurato per connettersi alle istanze di creazione e pubblicazione di AEM in esecuzione su un percorso di contesto diverso da /<strong> , è necessario abilitare la forza</strong>CQUrlInfo <strong></strong> nella configurazione Html Library Manager di queste istanze AEM (ad esempio tramite Felix Webconsole) oppure la modifica non funzionerà e la finestra di dialogo delle preferenze non verrà visualizzata.</p> </td>
  </tr>
  <tr>
   <td>htmlSelector</td>
   <td>Selettore aggiunto a ogni URL. Per impostazione predefinita, questo è <strong>portlet</strong>, pertanto tutte le richieste alle pagine html utilizzano URL che terminano con <strong>.portlet.html.</strong> Questo consente l'utilizzo di script personalizzati in AEM per il rendering portlet.</td>
  </tr>
  <tr>
   <td>addCssToPortalHeader</td>
   <td><p>Per impostazione predefinita, i file css inclusi nella pagina HTML di AEM sono inclusi nel portlet. La disattivazione di questa opzione esclude i file css predefiniti.</p> <p>Se questa opzione è attivata, i file CSS vengono aggiunti all'intestazione della pagina html o incorporati nella pagina html a seconda del comportamento del portale.</p> </td>
  </tr>
  <tr>
   <td>includeToolbar</td>
   <td>Per impostazione predefinita, all’interno del portlet del contenuto viene eseguito il rendering di una barra degli strumenti per la funzionalità di gestione. Disattivando questa opzione, non viene eseguito il rendering di alcuna barra degli strumenti.</td>
  </tr>
  <tr>
   <td>urlParameterNames</td>
   <td><p>Elenco di nomi di parametri URL alternativi che potrebbero contenere il nuovo URL di contenuto da visualizzare per il portlet. L'elenco viene elaborato dall'alto verso il basso e viene utilizzato il primo parametro contenente un valore. Se non viene trovato alcun URL, viene utilizzato il parametro URL predefinito. L’URL fornito viene utilizzato, così come è, senza ulteriori modifiche.</p> <p>Questa impostazione è per portlet distribuito; inoltre, per configurare globalmente alcuni parametri URL nella configurazione OSGi per il "Day Portal Director Portlet Bridge", è necessario configurare anche alcuni parametri URL.</p> </td>
  </tr>
  <tr>
   <td>favoriteDialog</td>
   <td>Percorso della finestra di dialogo delle preferenze in AEM - se lasciato vuoto, verrà utilizzata la finestra di dialogo delle preferenze integrate. Per impostazione predefinita, è /libs/portal/content/prefs.html.</td>
  </tr>
  <tr>
   <td>initialRedirect</td>
   <td>Per impostazione predefinita, il portlet esegue un reindirizzamento javascript dell'intera pagina del portale alla prima chiamata. Questo per supportare lo scenario di trascinamento dei server portale moderni. Nella produzione questo reindirizzamento è raramente necessario e può quindi essere disattivato con questa preferenza impostata su <em>false</em>.</td>
  </tr>
 </tbody>
</table>

#### Console Web OSGi {#osgi-web-console}

Se il server portale viene eseguito su host localhost, porta 8080 e l’applicazione Web portlet AEM viene montata nel *portlet* contestuale dell’applicazione Web, l’URL per la console Web è `https://localhost:8080/cqportlet/cqbridge/system/console`. L&#39;utente e la password predefiniti sono **admin**.

Aprite la scheda **Configurazioni** e selezionate Configurazione **server CQ** Portal Directory. Qui si specifica l’URL di base per l’istanza di creazione e pubblicazione. Questa procedura è descritta in [Configurazione del portlet](#configuring-the-portlet).

>[!NOTE]
>
>La console Web OSGi può essere utilizzata solo per modificare le configurazioni durante lo sviluppo (o il test). Accertatevi di bloccare le richieste alla console per i sistemi di produzione.

### Configurazione {#providing-configurations}

Per supportare le distribuzioni automatizzate e il provisioning di configurazione, il portlet di contenuti AEM dispone di un supporto di configurazione integrato che tenta di leggere le configurazioni dal percorso di classe fornito all’applicazione portlet.

All&#39;avvio, la proprietà di sistema **com.day.cq.portet.config** viene letta per rilevare l&#39;ambiente corrente. Solitamente, il valore di questa proprietà è simile a **dev**, **prod**, **test** e così via. Se non è impostato alcun ambiente, non viene letta alcuna configurazione.

Se si imposta un ambiente, la ricerca di un file di configurazione viene eseguita nel percorso di classe in* ***com/day/cq/portlet/{env}.config** , dove **env** viene sostituito con il valore effettivo per l&#39;ambiente. Questo file deve elencare tutti i file di configurazione per questo ambiente. La ricerca di questi file viene effettuata in relazione alla posizione del file di configurazione. Ad esempio, se il file contiene una riga, `my.service.xml,` questo file viene letto dal percorso di classe `com/day/cq/portlet/my.service.config.` Il nome del file è costituito dall&#39;ID di persistenza del servizio, seguito da **.config**. Nell&#39;esempio precedente, l&#39;ID di persistenza è **my.service**. Il formato del file di configurazione è il formato utilizzato dal programma di installazione Apache Sling OSGi.

Ciò significa che, per ogni ambiente, è necessario aggiungere un file di configurazione corrispondente. Una configurazione che dovrebbe essere applicata a tutti gli ambienti deve essere inserita in tutti questi file - se è solo per un singolo ambiente, è solo inserita in quel file. Questo meccanismo assicura il controllo completo della configurazione in cui viene letto l&#39;ambiente.

È possibile utilizzare una proprietà di sistema diversa per rilevare l&#39;ambiente. Specificate la proprietà di sistema **com.day.cq.portet.configproperty** contenente il nome della proprietà di sistema da utilizzare invece di **com.day.cq.portet.config**.

#### Annullamento della memorizzazione nella cache {#caching-and-caching-invalidation}

Nella configurazione predefinita, il portlet memorizza nella cache le risposte ricevute da AEM WCM in una cache specifica dell’utente. Le cache devono essere annullate quando si verificano modifiche nel contenuto dell’istanza di pubblicazione. A tal fine, in AEM WCM un agente di replica deve essere configurato nell’istanza di creazione. La cache può anche essere scaricata manualmente. Questa sezione descrive entrambe le procedure.

Il portlet può essere configurato con una propria cache, in modo che il contenuto del portlet venga visualizzato senza che sia necessario accedere ad AEM. Il portale è disponibile come contenuto in /libs/Portal/director. Per accedere al contenuto, avviate un’istanza di AEM e scaricate il file da tale posizione utilizzando CRXDE Lite o WebDAV.

Potete distribuire questo bundle in fase di esecuzione o aggiungerlo all&#39;applicazione Web portlet `WEB-INF/lib/resources/bundles` prima della distribuzione.

Dopo la distribuzione della cache, il portlet memorizza nella cache il contenuto dall’istanza di pubblicazione. La cache del portlet può essere invalidata con lo scaricamento del dispatcher da AEM. Per configurare il portlet in modo che utilizzi la propria cache:

1. Configurare un agente di replica in autore che esegue la destinazione del server del portale.
1. Supponendo che il server portale venga eseguito su host **localhost**, **port 8080 **e che l&#39;applicazione Web portlet AEM sia montata nel **portlet** contestuale, l&#39;URL per cancellare la cache è `https://localhost:8080/cqportlet/cqbridge/cqpcache?Path=$(path)`. Utilizzate GET come metodo.
   **** Nota: Invece di usare un parametro di richiesta, potete inviare un’intestazione http denominata **Path**.

#### Cancellazione della cache tramite Replication Agent {#flushing-the-cache-via-replication-agent}

Come per la normale invalidazione del dispatcher, un agente di replica può essere configurato per la destinazione della cache portlet AEM del portale. Dopo aver configurato l’agente di replica, ogni normale attivazione della pagina scarica la cache del portale.

Se si gestiscono più nodi portale con il portlet AEM, è necessario creare un agente per ciascun nodo come descritto in questa procedura.

Per configurare un agente di replica per il portale:

1. Effettuate l’accesso all’istanza di creazione.
1. Nella scheda Siti Web fare clic sulla scheda *Strumenti* .
1. **** Fate clic su **Nuova pagina... in agenti di replica** Nuovo... menu.

   ![screen_shot_2012-02-15at40647pm](assets/screen_shot_2012-02-15at40647pm.png)

1. In *Modello*, selezionare Agente ** replica e immettere un nome per l&#39;agente. Fai clic su *Crea*. 

   ![screen_shot_2012-02-15at40817pm](assets/screen_shot_2012-02-15at40817pm.png)

1. Fare doppio clic sull&#39;agente di replica appena creato. Viene visualizzato come non valido in quanto non è ancora stato configurato.

   ![screen_shot_2012-02-15at41001pm](assets/screen_shot_2012-02-15at41001pm.png)

1. Fai clic su **Modifica.**
1. Nella scheda **Impostazioni** , selezionare la casella di controllo **Abilitato** , selezionare **Dispatcher Flush** come tipo di serializzazione e immettere un timeout per tentativi (ad esempio, 60000).

   ![screen_shot_2012-02-15at42101pm](assets/screen_shot_2012-02-15at42101pm.png)

1. Click the **Transport** tab.
1. Nel campo **URI** , immettete l’URI (URL) del portlet. L&#39;URI si trova nel seguente modulo:

   ```xml
   https://<wps-host>:<port>/<wps-context>/<cq5-portlet-context>/cqbridge/cqpcache
   ```

   ![screen_shot_2012-02-15at42322pm](assets/screen_shot_2012-02-15at42322pm.png)

1. Click the **Extended** tab.

   ![screen_shot_2012-02-15at42515pm](assets/screen_shot_2012-02-15at42515pm.png)

1. Nel campo Metodo **** HTTP digitare **GET**.
1. Nel campo Intestazioni **** HTTP, fare clic su **+** per aggiungere una nuova voce e digitare **Percorso: {path}**.
1. Se necessario, fate clic sulla scheda **Proxy** e immettete le informazioni sul proxy per l&#39;agente.
1. Click **OK** to save changes.
1. Per verificare la connessione, fate clic sul collegamento **Test connessione** . Viene visualizzato un messaggio di registro che indica se il test di replica è riuscito. Esempio:

   ![screen_shot_2012-02-15at42639pm](assets/screen_shot_2012-02-15at42639pm.png)

#### Eliminazione manuale della cache del portlet {#manually-flushing-the-portlet-cache}

Potete cancellare manualmente la cache del portlet accedendo allo stesso URL configurato per l&#39;agente di replica. Consultate [Scorrimento della cache](#flushing-the-cache-via-replication-agent) per il modulo dell’URL. Inoltre, l’URL deve essere esteso con un parametro URL Path=&lt;percorso> per indicare cosa cancellare.

Esempio:

`https://10.0.20.99:10040/wps/PA_CQ5_Portlet/cqbridge/cqpcache?Path=*` svuota la cache completa. `https://10.0.20.99:10040/wps/PA_CQ5_Portlet/cqbridge/cqpcache?Path=/content/mypage/xyz` scarica `/content/mypage/xyz` dalla cache.

### Portal Security {#portal-security}

Il portale è il meccanismo di autenticazione guida. Puoi accedere ad AEM con un utente tecnico, l’utente del portale, un gruppo e così via. Il portlet non dispone dell&#39;accesso alla password per l&#39;utente nel portale, pertanto se il portlet non conosce tutte le credenziali per l&#39;accesso corretto a un utente, è necessario utilizzare una soluzione SSO. In questo caso, il portlet AEM inoltra tutte le informazioni richieste ad AEM, che a sua volta le inoltra all’archivio AEM sottostante. Questo comportamento è collegabile e può essere personalizzato.

### Autenticazione su Pubblica {#authentication-on-publish}

Questa sezione descrive le modalità di autenticazione disponibili che il portlet può utilizzare per comunicare con le istanze WCM AEM sottostanti.

Per impostazione predefinita non vengono inviate informazioni utente all’istanza di pubblicazione di AEM; il contenuto viene sempre visualizzato come utente anonimo. Se le informazioni specifiche per l’utente devono essere fornite da AEM o se è richiesta l’autenticazione utente per la pubblicazione, questa deve essere attivata.

#### Accesso alla configurazione di autenticazione del portlet {#accessing-the-portlet-s-authentication-configuration}

Le opzioni di configurazione dell&#39;autenticazione che il portlet utilizza nelle istanze WCM di AEM sono disponibili nella console Web (configurazione OSGi).

>[!NOTE]
>
>Quando lavorate con AEM, esistono diversi metodi per gestire le impostazioni di configurazione per i servizi OSGi (nodi console o repository).
>
>Per informazioni dettagliate, consultate [Configurazione di OSGi](/help/sites-deploying/configuring-osgi.md) .

Per accedere alla configurazione di autenticazione del portlet:

1. Accedete alla console Web al seguente URL:

   `https://localhost:8080/cqportlet/cqbridge/system/console`

   Ad esempio, nella configurazione predefinita:

   `https://wps-host:10040/wps/PA_CQ5_Portlet/cqbridge/system/console`

1. Accedere alla console Web. Le credenziali predefinite sono `admin/admin`.
1. Nella console, selezionare **Configurazione**.
1. Nel menu **Configurazione** , selezionate un particolare servizio da configurare. I servizi sono forniti dal portlet nel framework OSGi.

   | Nome servizio | Descrizione |
   |---|---|
   | Day Portal Director Authenticator | Configurare la modalità di autenticazione utilizzata per le istanze WCM AEM. A seconda della modalità selezionata, è possibile specificare un utente tecnico o il nome del cookie SSO. Inoltre, è possibile abilitare l&#39;autenticazione per le istanze di pubblicazione AEM WCM. |
   | Cache dei file di Director del portale giornaliero | Configura i parametri di come il portlet memorizza nella cache le risposte ricevute dalle istanze WCM di AEM. |
   | Servizio client HTTP di Day Portal Director | Configurare la modalità di connessione del portlet tramite HTTP alle istanze WCM AEM sottostanti. Ad esempio, potete specificare un server proxy. |
   | Gestore impostazioni internazionali di Day Portal Director | Configurare le impostazioni internazionali supportate dal portlet. Le richieste alle istanze di AEM WCM si basano sulle impostazioni internazionali dell&#39;utente; ad esempio, lingua utente *Tedesco *richiederebbe `/content/geometrixx/de/`... . |
   | Day Portal Director Privilege Manager | Configurare se il portlet deve testare la scheda Siti Web in base all&#39;utente attualmente connesso. |
   | Modulo di rendering Day Portal Director Toolbar | Personalizzare il rendering della barra degli strumenti della portlet. |

1. È inoltre possibile configurare la console Web e il servizio di registrazione. Ad esempio, potete modificare le credenziali di amministratore per la console Web facendo clic sul collegamento della console di gestione Apache Felix OSGi.

#### Modalità utente tecnica {#technical-user-mode}

In modalità predefinita, tutte le richieste emesse dal portlet per l&#39;istanza di creazione di AEM WCM vengono autenticate utilizzando lo stesso utente tecnico, indipendentemente dall&#39;utente corrente del portale. La modalità Utente tecnico è attivata per impostazione predefinita. Questa modalità viene attivata o disattivata nella rispettiva schermata di configurazione nella console di gestione OSGi:

L&#39;utente tecnico specificato deve esistere nell&#39;istanza di creazione di AEM WCM e nell&#39;istanza di pubblicazione se **Authenticate on Publish **is enabled. Assicuratevi di concedere agli utenti i privilegi di accesso sufficienti per le operazioni di authoring.

#### SSO {#sso}

Il portlet supporta SSO con AEM out-of-the-box. Il servizio di autenticazione può essere configurato per utilizzare SSO e trasmettere l&#39;utente del portale corrente con il formato **Basic** come cookie denominato `cqpsso` in AEM. AEM deve essere configurato per utilizzare il gestore di autenticazione SSO per path /. Anche in questo caso è necessario configurare il nome del cookie.

L’archivio `crx-quickstart/repository/repository.xml` per AEM deve essere configurato di conseguenza:

```xml
<LoginModule class="com.day.crx.security.authentication.CRXLoginModule">
  ...
  <param name="trust_credentials_attribute" value="TrustedInfo"/>
  <param name="anonymous_principal" value="anonymous"/>
</LoginModule>
```

#### Modalità autenticazione SSO {#sso-authentication-mode}

La portlet può essere autenticata per AEM WCM utilizzando lo schema Single Sign On (SSO). In questa modalità, l&#39;utente che ha effettuato l&#39;accesso al portale viene inoltrato ad AEM WCM sotto forma di cookie SSO. Se viene utilizzata la modalità SSO, tutti gli utenti del portale con accesso al portlet AEM devono essere noti alle istanze WCM AEM sottostanti, più comunemente sotto forma di AEM WCM connesso a LDAP, o avendo creato manualmente gli utenti in anticipo. Inoltre, prima di abilitare SSO nel portlet, è necessario configurare l’istanza di creazione AEM WCM sottostante (e l’istanza di pubblicazione, se **l’opzione Autenticazione** è attivata) per accettare richieste basate su SSO.

Per configurare il portlet per l&#39;utilizzo della modalità di autenticazione SSO, completa i seguenti passaggi (descritti in dettaglio nelle sezioni seguenti):

* Abilita l&#39;archivio di AEM WCM per accettare credenziali attendibili.
* Abilitare l&#39;autenticazione SSO in AEM WCM.
* Abilita autenticazione SSO nel portlet AEM.

#### Abilitazione dell&#39;archivio di AEM WCM per accettare credenziali attendibili {#enabling-aem-wcm-s-repository-to-accept-trusted-credentials}

Prima di abilitare SSO per AEM WCM, è necessario configurare il repository sottostante per accettare le credenziali attendibili fornite da AEM WCM. A questo scopo, configurate il file repository.xml di AEM.

1. Nel file system in cui è installato AEM WCM, aprite il file seguente:

   `//crx-quickstart/repository/repository.xml`

1. Nel file XML, trovate la voce per **LoginModule** e aggiungete l&#39;attributo trust_Credits_attribute alla configurazione:

   ```xml
   <LoginModule class="com.day.crx.security.authentication.CRXLoginModule">
     ...
     <param name="trust_credentials_attribute" value="TrustedInfo"/>
     <param name="anonymous_principal" value="anonymous"/>
   </LoginModule>
   ```

1. Per rendere effettive le modifiche, riavviate AEM WCM.

#### Abilitazione dell&#39;autenticazione SSO in AEM WCM {#enabling-sso-authentication-in-the-aem-wcm}

Per abilitare SSO in AEM WCM, accedi alla voce di configurazione corrispondente nella console di gestione Web Apache Felix di AEM WCM (OSGi):

1. Accedete alla console tramite il relativo URI all&#39;indirizzo https://&lt;AEM-host>:&lt;porta>/system/console.
1. Nel menu Configurazione, selezionate Gestore autenticazione SSO. In questo esempio, il gestore SSO accetta richieste SSO per tutti i percorsi basati sul cookie fornito dal portlet AEM. La configurazione può variare.

   | Percorso | / | Abilita il gestore SSO per tutte le richieste |
   |---|---|---|
   | Nomi cookie | cqpsso | Nome del cookie fornito dal portlet come configurato nella console OSGi del portlet. |

1. Fate clic su **Salva** per abilitare SSO. SSO è ora lo schema di autenticazione principale.

Per ogni richiesta ricevuta da AEM WCM, viene tentata innanzitutto l’autenticazione basata su SSO. In caso di errore, viene eseguito un fallback allo schema di autenticazione di base usuale. Di conseguenza, restano possibili le normali connessioni ad AEM WCM senza SSO.

#### Abilitazione dell&#39;autenticazione SSO in un portlet AEM {#enabling-sso-authentication-in-a-aem-portlet}

Affinché l’istanza AEM WCM sottostante possa accettare richieste SSO, la modalità di autenticazione del portlet deve essere commutata da **Technical** a **SSO**.

Per abilitare l&#39;autenticazione SSO in un portlet AEM:

1. Accedete alla console tramite il relativo URI all&#39;indirizzo https://&lt;aem-host>:&lt;porta>/system/console.
1. Nel menu Configurazione, selezionate Day Portal Director Authenticator dall&#39;elenco delle configurazioni disponibili.
1. In Modalità, selezionare SSO. Lasciate gli altri parametri con i relativi valori predefiniti.

   ![chlimage_1-135](assets/chlimage_1-135.png)

1. Fate clic su Salva per abilitare SSO per il portlet.

   A scopo di test, accedete al portlet con l&#39;utente amministrativo del portale, dopo aver creato lo stesso utente in AEM WCM con privilegi di amministratore.

Dopo aver eseguito questa procedura, le richieste vengono autenticate tramite SSO. Un frammento tipico della comunicazione HTTP rivela la presenza delle seguenti intestazioni SSO e portlet specifiche:

```xml
C-12-#001898 -> [GET /mynet/en/_jcr_content/par/textimage/image.img.png HTTP/1.1 ]
C-12-#001963 -> [cq5:locale: en ]
C-12-#001979 -> [cq5:used-locale: en ]
C-12-#002000 -> [cq5:locales: en,en_US ]
C-12-#002023 -> [cqp:user: wpadmin ]
C-12-#002042 -> [cqp:portal: IBM WebSphere Portal/6.1 ]
C-12-#002080 -> [cqp:windowid: 7_CGAH47L000CE302V2KFNOG0084 ]
C-12-#002124 -> [cqp:windowstate: normal ]
C-12-#002149 -> [cqp:portletmode: view ]
C-12-#002172 -> [User-Agent: Jakarta Commons-HttpClient/3.1 ]
C-12-#002216 -> [Host: 10.0.0.68:4502 ]
C-12-#002238 -> [Cookie: $Version=0; cqpsso=Basic+d3BhZG1pbg%3D%3D ]
C-12-#002289 -> [ ]
```

### Abilitazione dell&#39;autenticazione PIN {#enabling-pin-authentication}

Se non utilizzate le funzioni di modifica in linea predefinite del portlet di contenuti AEM, ma desiderate che la parte di authoring e amministrazione del portlet all’esterno del portale sia direttamente nell’istanza di creazione di AEM, dovete abilitare l’autenticazione PIN. È inoltre necessario modificare la configurazione dei pulsanti di gestione.

Per aprire la pagina di amministrazione del sito Web o modificare una pagina dal portlet, il portlet del contenuto AEM utilizza la nuova autenticazione pin. Per impostazione predefinita, l’autenticazione pin è disattivata, pertanto in AEM è necessario apportare le seguenti modifiche alla configurazione:

1. Abilita l’autenticazione attendibile in AEM aggiungendo le informazioni attendibili nel file repository.xml:

   ```xml
   <LoginModule class="com.day.crx.security.authentication.CRXLoginModule">
     ...
     <param name="trust_credentials_attribute" value="TrustedInfo"/>
   </LoginModule>
   ```

1. Nella console di configurazione OSGi, per impostazione predefinita, all’indirizzo https://localhost:4502/system/console/configMgr, selezionate Gestore **autenticazione** CQ PIN dal menu a discesa.
1. Modificate il parametro **URL Root Path** in modo che contenga solo il singolo valore **/**.

### Privilegi {#privileges}

Alcune funzioni del portlet sono protette da privilegi. L&#39;utente corrente deve avere questo privilegio per poter accedere a questa funzione. Sono disponibili i seguenti privilegi predefiniti:

* &quot;toolbar&quot;: Si tratta del privilegio generale per visualizzare/utilizzare la barra degli strumenti nella portlet.
* &quot;prefs&quot; : Se l&#39;utente dispone di questo privilegio, può visualizzare/modificare le preferenze del portlet.
* &quot;cq-author:edit&quot; : Con questo privilegio, l&#39;utente può richiamare la visualizzazione di modifica del contenuto.
* &quot;cq-author:preview&quot; : Con questo privilegio, l&#39;utente può visualizzare l&#39;anteprima.
* &quot;cq-author:siteadmin&quot; : Con questo privilegio, l’utente può aprire l’amministratore del sito in AEM.

L&#39;approccio migliore per gestire i privilegi consiste nell&#39;utilizzare i ruoli del portale e assegnare ruoli a tali privilegi. Questo può essere fatto tramite una configurazione OSGi. È possibile configurare &quot;Day Portal Director Privilege Manager&quot; con un set di ruoli per ciascun privilegio. Se l&#39;utente dispone di uno dei ruoli, l&#39;utente dispone dei privilegi corrispondenti.

Inoltre, è possibile definire questo accesso basato su un ruolo in base a un&#39;istanza portlet. La finestra di dialogo delle preferenze del portlet contiene un campo di immissione per ciascuno dei privilegi di cui sopra. Per ciascun privilegio è possibile configurare un elenco di ruoli portlet separati da virgole. Se è configurato un valore, questo sostituisce la configurazione globale dal servizio &quot;Gestione privilegi di Day Portal Director&quot; e potrebbe essere necessario aggiungere gli stessi ruoli da questa impostazione globale, in quanto i ruoli non vengono uniti. Se non viene specificato alcun valore, viene utilizzata la configurazione globale.

### Personalizzazione dell’applicazione portlet AEM {#customizing-the-aem-portlet-application}

L’applicazione portlet AEM fornita avvia un contenitore OSGi all’interno dell’applicazione Web esattamente come fa AEM. Questa architettura consente di sfruttare tutti i vantaggi di OSGi:

* Facilità di aggiornamento ed estensione
* Fornisce aggiornamenti a caldo del portlet senza alcuna interazione del server portale
* Facile da personalizzare

### Pulsanti della barra degli strumenti {#toolbar-buttons}

La barra degli strumenti e i relativi pulsanti sono configurabili e possono essere personalizzati. È possibile aggiungere pulsanti personalizzati alla barra degli strumenti o definire quali pulsanti visualizzare in quale modalità. Ogni pulsante è un servizio OSGi configurabile tramite una configurazione OSGi.

Nella console Web OSGi sono elencate tutte le configurazioni dei pulsanti nella scheda **Configurazione** . Per ciascun pulsante, è possibile definire in quale modalità viene visualizzato questo pulsante. Questo consente di disattivare un pulsante rimuovendo, ad esempio, tutte le modalità.

Per impostazione predefinita, il portlet del contenuto AEM utilizza la funzionalità di modifica in linea. Tuttavia, se preferite passare all’istanza di creazione di AEM per la modifica, abilitate i pulsanti **** SiteAdmin e **ContentFinder**, ma disattivate il pulsante **** Modifica. In questo caso, accertatevi di configurare correttamente l’autenticazione PIN in AEM.

Il layout della barra degli strumenti del portlet può essere personalizzato installando un bundle tramite la console Web Felix del portlet, che contiene CSS/HTML personalizzato in una posizione predefinita.

#### Struttura del pacchetto {#bundle-structure}

Esempio di struttura del pacchetto:

```xml
$ jar tvf target/toolbarlayout-0.0.1-SNAPSHOT.jar | awk '{print $8}'
META-INF/
META-INF/MANIFEST.MF
/com/day/cq/portlet/toolbar/layout/
/com/day/cq/portlet/toolbar/layout/author.gif
/com/day/cq/portlet/toolbar/layout/back.gif
/com/day/cq/portlet/toolbar/layout/button.html
/com/day/cq/portlet/toolbar/layout/edit.gif
/com/day/cq/portlet/toolbar/layout/manage.html
/com/day/cq/portlet/toolbar/layout/publish.html
/com/day/cq/portlet/toolbar/layout/refresh.gif
/com/day/cq/portlet/toolbar/layout/siteadmin.gif
/com/day/cq/portlet/toolbar/layout/toolbar.css
```

La cartella META-INF contiene il file MANIFEST.MF richiesto da OSGi per identificarlo come pacchetto. Viene visualizzata come segue:

```xml
Manifest-Version: 1.0
Built-By: djaeggi
Created-By: Apache Maven Bundle Plugin
Import-Package: com.day.cq.portlet.toolbar.layout
Bnd-LastModified: 1234178347159
Export-Package: com.day.cq.portlet.toolbar.layout
Bundle-Version: 0.0.1.SNAPSHOT
Bundle-Name: Company CQ5 Portal Director Portlet Toolbar Layout
Bundle-Description: This bundle provides a custom layout for the CQ5 P
 ortal Director Portlet Toolbar.
Build-Jdk: 1.5.0_16
Bundle-ManifestVersion: 2
Bundle-SymbolicName: com.day.cq.portlet.company.toolbarlayout
Tool: Bnd-0.0.255
```

Il fatto che HTML/CSS/images si trovino nella cartella /com/day/cq/portlet/toolbar/layout è imposto dal portlet e non può essere modificato. Sulle stesse righe, le intestazioni Import-Package e Export-Package in MANIFEST.MF devono essere denominate /com/day/cq/portlet/toolbar/layout. Bundle-SymbolicName deve essere un nome di pacchetto univoco e completo.

Potete creare il file utilizzando uno strumento come il cielo o creare manualmente un file JAR con il set di intestazioni corrispondente come mostrato in questa sezione.

#### Visualizzazioni barra degli strumenti portlet {#portlet-toolbar-views}

La barra degli strumenti della portlet ha sostanzialmente due stati di visualizzazione. Ogni vista e i pulsanti associati possono essere personalizzati con un rispettivo file HTML.

#### Visualizzazione pubblicazione {#publish-view}

La visualizzazione di pubblicazione dispone di un solo pulsante che consente di passare alla visualizzazione Gestisci della barra degli strumenti. La visualizzazione di pubblicazione è rappresentata dal file publish.html nel pacchetto [precedente](/help/sites-deploying/configuring-osgi.md#bundles). Nell’HTML, potete utilizzare i seguenti segnaposto, che vengono sostituiti dal portlet con i rispettivi contenuti al momento del rendering:

#### Segnaposto vista pubblicazione {#publish-view-placeholders}

| Stringa Segnaposto | Descrizione |
|---|---|
| {buttonManage} | Il segnaposto è sostituito dal pulsante **Manage **che sposta lo stato del portlet nello stato di gestione. |

#### Gestisci vista {#manage-view}

La vista di gestione è dotata di quattro pulsanti: Modifica, scheda Siti Web, Aggiorna e Indietro. La vista di gestione è rappresentata dal file manage.html nel pacchetto [precedente](/help/sites-deploying/configuring-osgi.md#bundles). Nell’HTML, potete utilizzare i seguenti segnaposto, che vengono sostituiti dal portlet con i rispettivi contenuti al momento del rendering:

#### Gestisci segnaposto vista {#manage-view-placeholders}

| Stringa Segnaposto | Descrizione |
|---|---|
| {buttonEdit} | Il segnaposto viene sostituito dal pulsante** Modifica**, che apre una nuova finestra con la pagina corrente in modalità di modifica di AEM. |
| {buttonWebsites, scheda} | Segnaposto, sostituito da un pulsante che apre la scheda Siti Web di AEM WCM. |
| {buttonRefresh} | Aggiorna la visualizzazione corrente. |
| {buttonBack} | Consente di ripristinare la visualizzazione di pubblicazione del portlet. |

#### Pulsanti {#buttons}

I pulsanti, a prescindere dalla visualizzazione, utilizzano lo stesso HTML comune, definito in button.html.

Nell’HTML, potete utilizzare i seguenti segnaposto, che vengono sostituiti dal portlet con i rispettivi contenuti al momento del rendering:

#### Pulsanti di visualizzazione Gestisci e pubblica {#manage-and-publish-view-buttons}

| Stringa Segnaposto | Descrizione |
|---|---|
| {nome} | Nome del pulsante, ad esempio,** autore, back, refresh** e così via. |
| {id} | ID CSS del pulsante. |
| {url} | URL della destinazione del pulsante. |
| {testo} | Etichetta del pulsante. |
| {onclick} | Funzione **onclick** JavaScript (contiene {url}). |

Esempio di file button.html:

```xml
<div class="cqp_button">

 <a href="#" onclick="{onclick}">

 <img src="/wps/PA_CQ5_Portlet/cqbridge/static/{id}.gif" alt="{text}"
title="{text}"/>

 </a>
</div>
```

#### Installazione di un layout personalizzato {#installing-a-custom-layout}

Per installare un layout personalizzato, accedete alla sezione della console Web OSGI **Bundle **e caricate il bundle.

#### Pacchetti {#packages}

Per caricare o creare pacchetti per l’installazione, consulta Gestione pacchetti nella documentazione di AEM per istruzioni dettagliate.

### Gestione collegamenti {#link-handling}

Tutti i collegamenti vengono riscritti per funzionare nel contesto del portale. Per impostazione predefinita vengono utilizzati i collegamenti con i parametri di rendering. La funzione di riscrittura HTML di Portal Director può essere configurata per l&#39;utilizzo dei collegamenti delle azioni.

Potete anche definire parametri di richiesta aggiuntivi per i quali eseguire una query per visualizzare il percorso del contenuto. Questo è utile, ad esempio, se esiste un collegamento dall&#39;esterno a un contenuto specifico.

Inoltre, è possibile configurare la funzione di riscrittura HTML di Portal Director con un elenco di espressioni regolari definite per la riscrittura dei collegamenti. Se, ad esempio, si dispone di collegamenti relativi a sistemi esterni, è necessario aggiungerli a questo elenco di esclusione.

### Localizzazione {#localization}

Il portlet dei contenuti AEM dispone di una funzione di localizzazione integrata che garantisce che il contenuto di AEM sia nella lingua corretta.

Ciò avviene in due passaggi:

1. Il rilevatore delle impostazioni internazionali della directory portale rileva le impostazioni internazionali dell&#39;utente del portale ottenendo le impostazioni internazionali dal portale. Questo servizio deve essere configurato con l’elenco delle lingue disponibili in AEM.
1. Il gestore impostazioni internazionali di Portal Director gestisce la localizzazione della richiesta corrente. Prende il percorso del contenuto richiesto, ad esempio `/content/geometrixx/en/company.html`e, in base alla configurazione, riscrive l&#39; **en** con le impostazioni internazionali effettive dell&#39;utente.

Il gestore impostazioni internazionali di Portal Director può essere configurato con i percorsi per la verifica delle informazioni sulle impostazioni internazionali, in genere include tutto ciò che si trova sotto `/content` e con la posizione delle informazioni sulle impostazioni internazionali nel percorso. Per impostazione predefinita, il gestore di impostazioni internazionali segue la ricomposizione della strutturazione di siti in più lingue in AEM.

Se il sito non dispone di regole rigorose per la gestione delle informazioni sulle impostazioni internazionali all&#39;interno del percorso, è possibile sostituire il gestore di impostazioni internazionali con la propria implementazione.

### Servizi OSGi opzionali {#optional-osgi-services}

I servizi OSGi opzionali possono essere implementati per personalizzare diverse parti del portlet. Ogni servizio corrisponde a un&#39;interfaccia Java. Questa interfaccia può essere implementata e distribuita tramite un bundle nella portlet.

<table>
 <tbody>
  <tr>
   <td>RequestTracker</td>
   <td>Il tracciatore delle richieste riceve una notifica ogni volta che il contenuto viene visualizzato dal portlet. Questo consente di tenere traccia delle chiamate del portlet.</td>
  </tr>
  <tr>
   <td>InvocationContextListener</td>
   <td>Listener richiamato all'inizio e alla fine di ogni richiesta al portlet. Il listener può essere utilizzato per modificare o aggiungere informazioni per la richiesta corrente.<br /> </td>
  </tr>
  <tr>
   <td>ErrorHandler</td>
   <td>Gestore di errori personalizzato per gli errori durante la fase di rendering.</td>
  </tr>
  <tr>
   <td>HttpProcessor</td>
   <td>Questo servizio può essere utilizzato per aggiungere informazioni a ogni chiamata HTTP ad AEM.</td>
  </tr>
  <tr>
   <td>PortletAction</td>
   <td>Aggiungi una propria azione al portlet: questa azione può essere invocata tramite un collegamento di azione portlet.</td>
  </tr>
  <tr>
   <td>PortletDecoratorService</td>
   <td>Questo servizio può essere utilizzato per decorare il contenuto del portlet.</td>
  </tr>
  <tr>
   <td>ResourceProvider</td>
   <td>Aggiungete il vostro provider di risorse per distribuire alcune risorse tramite un collegamento di risorse portlet al client.</td>
  </tr>
  <tr>
   <td>TextMapper</td>
   <td>Consente di pubblicare i file HTML, CSS e JavaScript di elaborazione.</td>
  </tr>
  <tr>
   <td>ToolbarButton</td>
   <td>Aggiungere un pulsante personalizzato alla barra degli strumenti.</td>
  </tr>
  <tr>
   <td>UrlMapper</td>
   <td>Aggiungete un servizio per applicare una mappatura URL personalizzata o per riscrivere.</td>
  </tr>
  <tr>
   <td>UserInfoProvider</td>
   <td>Aggiungete le vostre informazioni sull'utente. Questo servizio può essere utilizzato per ottenere informazioni dal portale al portlet.</td>
  </tr>
 </tbody>
</table>

#### Sostituzione dei servizi predefiniti {#replacing-default-services}

I seguenti servizi hanno un&#39;implementazione predefinita nel portlet del contenuto (con un&#39;interfaccia Java corrispondente). Per personalizzare, è necessario distribuire nell’applicazione portlet un bundle contenente la nuova implementazione del servizio.

Quando implementate tale servizio, accertatevi di impostare la proprietà **service.ranking** del servizio su un valore positivo. L&#39;implementazione predefinita utilizza la classifica** 0** e il portlet utilizza il servizio con la classifica più alta.

| **Nome** | **Descrizione** | **Comportamento predefinito** |
|---|---|---|
| Autenticatore | Fornisce le informazioni di autenticazione ad AEM | Utilizza un utente tecnico configurabile per l’authoring e la pubblicazione. Oppure è possibile utilizzare SSO. |
| HTMLRewriter | Riscrive collegamenti, immagini e così via. | Riscrive i collegamenti AEM ai collegamenti del portale, che possono essere estesi tramite UrlMapper e TextMapper |
| HttpClientService | Gestisce tutte le connessioni HTTP | Implementazione standard |
| LocaleHandler | Gestisce le informazioni sulle impostazioni internazionali | Riscrive un collegamento al contenuto rispetto alle impostazioni internazionali. |
| LocaleDetector | Rileva le impostazioni internazionali dell&#39;utente. | Utilizza le impostazioni internazionali fornite dal portale. |
| PrivilegeManager | Controlla i diritti utente | Controlla l&#39;accesso all&#39;istanza di creazione se l&#39;utente può modificare i contenuti |
| ToolbarRenderer | Rendering della barra degli strumenti | Aggiunge una funzionalità della barra degli strumenti |

### Eventi Portlet {#portlet-events}

L&#39;API portlet (JSR-286) specifica gli eventi portlet. Il portlet dei contenuti AEM è dotato di un bridge integrato che distribuisce gli eventi portlet per il portlet AEM come eventi OSGi. In questo modo è possibile gestire gli eventi portlet tramite il pluggable.

Se si desidera gestire eventi specifici, dichiararli come eventi riceventi nel descrittore di distribuzione (o configurarli tramite il server del portale) e implementare un servizio OSGi che dichiara l&#39;interfaccia EventHandler (vedere la specifica OSGi EventAdmin).

Ogni volta che si verifica un evento portlet, viene inviato un evento OSGi specifico che richiama il gestore. Il gestore riceve tutte le informazioni contestuali e può aggiornare di conseguenza lo stato del portlet oppure inviare nuovi eventi. In sostanza, all&#39;interno del metodo handle è possibile utilizzare tutte le funzionalità della fase evento portlet.

## Utilizzo di AEM come portale {#using-aem-as-a-portal}

Utilizzate il componente Portlet per aggiungere le finestre portlet alle pagine AEM. Le librerie condivise installate nel server delle applicazioni consentono al componente Portlet di rilevare le applicazioni portlet distribuite.

Per utilizzare AEM come portale, effettua le seguenti operazioni:

1. Installate il componente Portlet e le librerie condivise.
1. Aggiungete il componente Portlet alla barra laterale.
1. Configurate e distribuite l’applicazione Web che contiene i portlet da visualizzare nel componente Portal.
1. Aggiungere il componente Portlet a una pagina e selezionare il portlet da visualizzare.

>[!NOTE]
>
>Potete usare il componente portlet solo quando AEM viene distribuito come applicazione Web. ([consultate Installazione di AEM con un server]applicazione (/content/docs/en/aem/6-3/deploy/installing.md#installing adobe experience manager with a application server).

### Installazione del componente portlet {#installing-the-portlet-component}

Il file AEM Quickstart JAR contiene i file dei componenti portlet. Per ottenere i file (cq-portlet-components.zip), potete eseguire il Quickstart o estrarre il contenuto.

1. Eseguite o estraete il contenuto del file JAR di Quickstart, quindi individuate il file cq-portlet-components.zip di conseguenza:

   * Esegui avvio rapido: crx-quickstart/opt/Portal
   * Estrai contenuti di Quickstart: static/opt/Portal

1. Aprite Package Manager dell’istanza di creazione CQ5 distribuita nel server dell’applicazione. (https://*appserverhost*:*port*/cq5author/crx/packmgr)

1. Usate Gestione pacchetti per [caricare e installare](/help/sites-administering/package-manager.md#uploading-packages-from-your-file-system) il pacchetto cq-portlets-components.zip.

   Il pacchetto installa cq-portlet-director-sharedlibs-x.x.x.jar nella cartella /libs/Portal/director nella directory archivio.

1. Copiare cq-portlet-director-sharedlibs-x.x.x.jar sul disco rigido. Utilizzare qualsiasi mezzo per ottenere il file, ad esempio FileVault o un client WebDAV.
1. Spostate il file cq-portlet-director-sharedlibs.x.x.x.jar nella cartella della libreria condivisa del server applicazione in modo che le classi siano disponibili per le applicazioni portlet distribuite.

### Aggiunta del componente Portlet alla barra laterale {#adding-the-portlet-component-to-sidekick}

Aggiungete il componente portlet al sistema paragrafo in modo che sia disponibile per gli autori.

1. Nella barra laterale fate clic sull’icona del righello per passare alla modalità Progettazione.
1. Accanto all’ `Design of par` intestazione sopra il primo paragrafo, fate clic su **Modifica**.

1. Nella categoria del componente **Generale** , selezionate la casella di controllo accanto al componente Portlet e fate clic su OK.

![chlimage_1-25](assets/chlimage_1-25.jpeg)

### Configurazione e implementazione delle applicazioni portlet {#configuring-and-deploying-your-portlet-applications}

Distribuite i portlet nel contenitore Web del server applicazione in modo che siano disponibili per il componente Portal. Prima di implementare l’applicazione portlet, è necessario configurare l’applicazione in modo che carichi il servlet contenitore del portale AEM. Questa configurazione consente al componente Portlet di accedere ai portlet.

1. Estrarre il contenuto del file WAR dell&#39;applicazione portlet.

   **** Suggerimento: Il comando jar xf *nameofapp*.war estrae i file.

1. Aprite il file web.xml in un editor di testo.
1. Aggiungi la seguente configurazione servlet all&#39;interno dell&#39;elemento web-app:

   ```xml
   <servlet>
           <servlet-name>slingportal</servlet-name>
           <servlet-class>org.apache.sling.portal.container.api.ContainerServlet</servlet-class>
           <load-on-startup>1</load-on-startup>
   </servlet>
   <servlet-mapping>
           <servlet-name>slingportal</servlet-name>
           <url-pattern>/SlingPortletInvoker</url-pattern>
   </servlet-mapping>
   ```

1. Salvate il file web.xml e ricompilate il file WAR.

   **** Suggerimento: Il `jar cvf nameofapp.war *` comando aggiunge il contenuto della directory corrente al file nameofapp.war.

1. Implementare l&#39;applicazione portlet nel server applicazione. Per ulteriori informazioni, consultate la documentazione del server applicazione.

### Aggiunta di portlet alla pagina AEM {#adding-portlets-to-your-aem-page}

Utilizzate il componente Portal per aggiungere una finestra portlet alla pagina Web. Utilizzate le proprietà del componente per specificare il portlet da visualizzare.

1. Sulla pagina Web, trascinare il componente **Portlet** dal gruppo Generale nella barra laterale alla pagina.

   >[!NOTE]
   >
   >Dopo aver trascinato il componente sulla pagina, ricaricate la pagina per assicurarvi che funzioni correttamente.

1. Fare doppio clic sul componente per aprire le proprietà Portlet.
1. Nel menu a discesa **Portlet Entity** , selezionate il portlet dall&#39;elenco.
1. Selezionare o deselezionare la casella di controllo **Nascondi barra del titolo **a seconda che si desideri visualizzare o meno la barra del titolo del portlet.
1. Nel campo Finestra **** portlet, immettete un ID univoco per la finestra Portlet, se lo desiderate.

   >[!NOTE]
   >
   >Se intendete utilizzare la stessa portlet più volte sulla stessa pagina, assegnate a ciascuna portlet un ID finestra diverso.

1. Fai clic su **OK**. Il portlet viene visualizzato sulla pagina AEM.

   ![chlimage_1-136](assets/chlimage_1-136.png)

## Installazione, configurazione e utilizzo di AEM in un portfolio {#installing-configuring-and-using-aem-in-a-portlet}

Per accedere al contenuto fornito da AEM WCM, il server portale deve essere dotato del portlet AEM Portal Director. A tal fine, è possibile installare, configurare e aggiungere il portlet alla pagina del portale utilizzando i passaggi forniti in questa sezione.

Per impostazione predefinita, il portlet si collega all’istanza di pubblicazione localhost:4503 e all’istanza di creazione in localhost:4502. Questi valori possono essere modificati durante la distribuzione del portlet. Il direttore del portale è disponibile come contenuto nella directory archivio in /libs/portale/directory. Sarà necessario scaricare il file di guerra dell&#39;applicazione prima di utilizzarlo.

### Download del file di guerra {#downloading-the-war-file}

1. Utilizzando WebDAV o CRXDE Lite, andate a /libs/portale/director.

1. Scarica *cq-portlet-webapp.war*.

>[!NOTE]
>
>Queste procedure utilizzano il portale WebSfera come esempio, anche se il più possibile generiche; le procedure variano per altri portali Web. Anche se i passaggi sono sostanzialmente identici per tutti i portali Web, è necessario riadattare i passaggi per un particolare portale Web.

#### Installazione del portlet {#installing-the-portlet}

Per installare il portlet:

1. Accedete al portale con privilegi di amministratore.
1. Passare alla sezione Gestione portlet del portale Web.
1. Fai clic su Installa e individua l’applicazione portlet AEM (cq-portlet-webapp.war) che hai scaricato e immetti altre informazioni importanti sul portlet.

   Per altre informazioni essenziali sul portlet, potete accettare le impostazioni predefinite o modificare i valori. Se accettate i valori predefiniti, il portlet è disponibile all’indirizzo https://&lt;wps-host>:&lt;port>/wps/PA_CQ5_Portlet. La console di amministrazione OSGi fornita dal portlet è disponibile all&#39;indirizzo https://&lt;wps-host>:&lt;port>/wps/ PA_CQ5_Portlet/cqbridge/system/console (il nome utente/password predefinito è admin/admin).

1. Verificare che l&#39;applicazione portlet venga avviata automaticamente selezionando tale opzione o casella di controllo e salvare le modifiche. Viene visualizzato un messaggio di errore relativo all&#39;installazione.

#### Configurazione del portlet {#configuring-the-portlet}

Dopo aver installato il portlet, dovete configurarlo in modo che conosca gli URL delle istanze AEM sottostanti (creazione e pubblicazione). Potete anche configurare altre opzioni.

Per configurare il portlet:

1. Nella finestra di amministrazione del portale del server app, andate alla gestione del portlet, in cui sono elencati tutti i portlet e selezionate il portlet AEM Portal Director.
1. Configura il portlet, a seconda delle necessità. Ad esempio, potrebbe essere necessario modificare l’URL per le istanze di creazione e pubblicazione e l’URL per il percorso iniziale. Le configurazioni predefinite sono descritte in Preferenze [](/help/sites-administering/aem-as-portal.md#portlet-preferences)portlet.

   >[!NOTE]
   >
   >Se il portlet è configurato per connettersi alle istanze di creazione e pubblicazione di AEM in esecuzione su un percorso di contesto diverso da** /***, è necessario abilitare la forza **CQUrlInfo** nella configurazione Html Library Manager di queste istanze AEM (ad esempio tramite Felix Webconsole), altrimenti la modifica non funzionerà e la finestra di dialogo delle preferenze non verrà visualizzata.

1. Salva le modifiche alla configurazione nel server app.

1. Passate alla console di amministrazione OSGI per il portlet. Il percorso predefinito è `https://<wps-host>:<port>/wps/PA_CQ5_Portlet/cqbridge/system/console/configMgr`. Il nome utente/password predefinito è **admin/admin**.

1. Selezionate la configurazione **Day Portal Director CQ Server Configuration** e modificate i seguenti valori:

   * **URL** base autore: L’URL di base per l’istanza di creazione di AEM.
   * **URL** base pubblicazione: L’URL di base per l’istanza di pubblicazione AEM.
   * **L’Autore Viene Utilizzato Come Pubblica**: L’istanza di autore è utilizzata come istanza pubblica (per lo sviluppo)?
   ![chlimage_1-137](assets/chlimage_1-137.png)

1. Fai clic su **Salva**. È ora possibile aggiungere il portlet alle pagine del portale e utilizzare il portale.

### URL contenuto {#content-urls}

Quando il contenuto viene richiesto da AEM, il portlet utilizza la modalità di visualizzazione corrente (pubblicazione o creazione) e il percorso corrente per assemblare un URL completo. Con i valori predefiniti, il primo URL è `https://localhost:4503/content/geometrixx/en.portlet.html`. Il valore dell’URL `htmlSelector` viene aggiunto automaticamente all’URL prima dell’estensione.

Se il portlet passa alla modalità help e l&#39; `appendHelpViewModeAsSelector` opzione è selezionata, viene aggiunto anche il `help` selettore, ad esempio `https://localhost:4503/content/geometrixx/en.portlet.html.help`. Se la finestra del portlet è ingrandita e `appendMaxWindowStateAsSelector` è selezionata, viene aggiunto anche il selettore, ad esempio `https://localhost:4503/content/geometrixx/en.portlet.max.help`.

I selettori possono essere valutati in AEM e per i diversi selettori è possibile utilizzare un modello diverso.

### Utilizzo di una mappa URL contenuto in AEM {#using-a-content-url-map-in-aem}

Solitamente il percorso iniziale punta direttamente al contenuto in AEM. Tuttavia, se desiderate mantenere i percorsi iniziali in AEM anziché nelle preferenze per i portlet, potete indirizzare il percorso iniziale a una mappa di contenuto in AEM, come `/var/portlets`. In questo caso, uno script in esecuzione in AEM può utilizzare le informazioni inviate dal portlet per decidere quale URL corrisponde all’URL iniziale. Dovrebbe eseguire un reindirizzamento all&#39;URL corretto.

#### Aggiunta del portlet alla pagina del portale {#adding-the-portlet-to-the-portal-page}

Per aggiungere il portlet alla pagina del portale:

1. Accertatevi di essere nella finestra di amministrazione del server app e andate al percorso in cui gestite le pagine. Ad esempio, in WebSphere 6.1, fare clic su **Gestisci pagine**.
1. Selezionate il nome del portlet, quindi selezionate una pagina esistente o create una nuova pagina.
1. Modificate il layout della pagina.
1. Selezionate il portlet e aggiungetelo a un contenitore.
1.  Salvare le modifiche.

#### Utilizzo del portlet {#using-the-portlet}

Per accedere alla pagina aggiunta alla portlet:

1. Nel menu di personalizzazione del portlet, configura il portlet come lo hai configurato nel portale.
1. Aprite la configurazione (il portlet visualizza l’URL di avvio pubblicazione configurato nella configurazione del portlet), apportate le modifiche necessarie, quindi salvateli.

