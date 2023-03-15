---
title: Portali AEM e portlet
seo-title: AEM Portals and Portlets
description: Scopri Portals e Portles in AEM.
seo-description: Learn about Portals and Portles in AEM.
uuid: 7f9e316d-277e-4a1e-b6f3-cd89addc897b
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 99528fda-5c8c-4034-bcbe-a4cea42f694b
docset: aem65
exl-id: b5f3d3a6-39c0-4aa5-8562-3cc6fa2b9e46
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '6086'
ht-degree: 0%

---

# Portali AEM e portlet{#aem-portals-and-portlets}

Il presente documento descrive quanto segue:

* Architettura AEM Portal
* Amministrazione e configurazione di AEM come portale
* Utilizzo di AEM come portale
* Installazione, configurazione e visualizzazione AEM contenuto in un portlet (ad esempio, un server web)

## Architettura AEM Portal {#aem-portal-architecture}

AEM&#39;architettura del portale include definizioni di portali e portlet.

### Che cos&#39;è un portale? {#what-is-a-portal}

Un portale è un’applicazione web che offre personalizzazione, accesso singolo, integrazione dei contenuti da diverse sorgenti e ospita il livello di presentazione dei sistemi informativi.

È possibile eseguire portlet conformi a JSR 286 in AEM. Il componente portlet consente di incorporare un portlet nella pagina. Vedi [Amministrazione del AEM Content Portlet](#administeringthecqcontentportlet).

### Cos&#39;è un portlet? {#what-is-a-portlet}

I portlet sono componenti web distribuiti all’interno di un contenitore che genera contenuto dinamico. L’interfaccia portlet viene compilata e distribuita come file .war all’interno di un contenitore portlet. Se esegui AEM come portale, è necessario il file .war del portlet per eseguire il portlet.

Per configurare AEM contenuto da visualizzare in un portale, vedi [Installazione, configurazione e utilizzo di AEM in un portlet](#installingconfiguringandusingcqinaportlet).

### AEM Portal Director {#aem-portal-director}

>[!CAUTION]
>
>AEM Portal Director è obsoleto a partire da AEM 6.4. Vedi [Funzioni obsolete e rimosse](https://helpx.adobe.com/experience-manager/6-4/release-notes/deprecated-removed-features.html).

## Amministrazione del AEM Content Portlet {#administering-the-aem-content-portlet}

Il portlet del contenuto AEM consente di visualizzare AEM contenuto in un portale. Il portlet è disponibile all&#39;indirizzo `/crx-quickstart/opt/portal`e può essere personalizzato in vari modi. Ad esempio, è possibile personalizzare la gestione SSO/autenticazione distribuendo il proprio servizio di autenticazione generando le informazioni di autenticazione necessarie per AEM sovrascrivere il comportamento predefinito. I plug-in utilizzano un’API definita che ti consente di aggiungere funzionalità personalizzate creando il plug-in rispetto all’API. Il plug-in può essere distribuito nel portlet in esecuzione. Per funzionare correttamente, è necessaria una configurazione dell’istanza di authoring e pubblicazione AEM insieme al percorso del contenuto da visualizzare all’avvio.

Alcune delle configurazioni possono essere modificate tramite le preferenze del portlet e altre tramite le configurazioni del servizio OSGi. Queste configurazioni vengono modificate utilizzando **config** file o la console Web OSGi.

### Preferenze del portlet {#portlet-preferences}

È possibile configurare le preferenze del portlet in fase di distribuzione nel server del portale o modificando il **WEB-INF/portlet.xml** prima di distribuire l&#39;applicazione web portlet. Il file portlet.xml viene visualizzato come segue per impostazione predefinita:

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
   <td><p>Questo è il percorso iniziale del portlet: definisce il contenuto inizialmente visualizzato.</p> <p><strong>Importante</strong>: Se il portlet è configurato per connettersi a istanze di creazione e pubblicazione AEM che sono in esecuzione su un percorso contestuale diverso da<strong> /</strong>, è necessario abilitare la forza <strong>CQUrlInfo</strong> nella configurazione di Html Library Manager di queste istanze AEM (ad esempio tramite Felix Webconsole) o la modifica non funzionerà e la finestra di dialogo delle preferenze non verrà visualizzata.</p> </td>
  </tr>
  <tr>
   <td>htmlSelector</td>
   <td>Il selettore che viene aggiunto a ogni url. Per impostazione predefinita <strong>portlet</strong>, in modo che tutte le richieste alle pagine html utilizzino url che terminano in <strong>.portlet.html.</strong> Questo consente l’utilizzo di script personalizzati all’interno di AEM per il rendering del portlet.</td>
  </tr>
  <tr>
   <td>addCssToPortalHeader</td>
   <td><p>Per impostazione predefinita, i file css inclusi nella pagina HTML da AEM sono inclusi nel portlet. La disattivazione di questa opzione esclude i file css predefiniti.</p> <p>Se questa opzione è abilitata, i file CSS vengono aggiunti all’intestazione della pagina HTML o incorporati nella pagina html a seconda del comportamento del portale.</p> </td>
  </tr>
  <tr>
   <td>includeToolbar</td>
   <td>Per impostazione predefinita, all’interno del portlet dei contenuti viene eseguito il rendering di una barra degli strumenti per la funzionalità di gestione. Disattivando questa opzione, non viene eseguito il rendering di alcuna barra degli strumenti.</td>
  </tr>
  <tr>
   <td>urlParameterNames</td>
   <td><p>Elenco di nomi di parametri URL alternativi che potrebbero contenere il nuovo URL di contenuto da visualizzare per il portlet. L’elenco viene elaborato dall’alto verso il basso e viene utilizzato il primo parametro contenente un valore. Se non viene trovato alcun URL, viene utilizzato il parametro URL predefinito. L’URL fornito viene utilizzato così come è, senza ulteriori modifiche.</p> <p>Questa impostazione si basa su un portlet distribuito. È anche necessario configurare globalmente alcuni parametri url nella configurazione OSGi per il "Day Portal Director Portlet Bridge".</p> </td>
  </tr>
  <tr>
   <td>favoriteDialog</td>
   <td>Percorso della finestra di dialogo delle preferenze in AEM: se lasciato vuoto, verrà utilizzata la finestra di dialogo delle preferenze integrate. Il valore predefinito è /libs/portal/content/prefs.html.</td>
  </tr>
  <tr>
   <td>initialRedirect</td>
   <td>Per impostazione predefinita, il portlet esegue un reindirizzamento javascript dell’intera pagina del portale nella prima chiamata. Questo per supportare lo scenario di trascinamento dei server di portale moderni. Nella produzione questo reindirizzamento è raramente necessario e può quindi essere disattivato con questa preferenza impostata su <em>false</em>.</td>
  </tr>
 </tbody>
</table>

#### Console web OSGi {#osgi-web-console}

Supponendo che il server portale venga eseguito su host localhost, porta 8080 e che l&#39;applicazione Web AEM portlet sia montata nel contesto dell&#39;applicazione Web *cqportlet*, l’url di per la console web è `https://localhost:8080/cqportlet/cqbridge/system/console`. L&#39;utente e la password predefiniti sono **admin**.

Apri **Configurazioni** e seleziona **Configurazione del server CQ della directory portale**. Qui si specifica l’URL di base per l’istanza di authoring e di pubblicazione. Questa procedura è descritta in [Configurazione del portlet](#configuring-the-portlet).

>[!NOTE]
>
>La console web OSGi è destinata solo a modificare le configurazioni durante lo sviluppo (o il test). Assicurati di bloccare le richieste alla console per i sistemi di produzione.

### Configurazione {#providing-configurations}

Per supportare le distribuzioni automatizzate e il provisioning della configurazione, il portlet di contenuti AEM dispone di un supporto di configurazione integrato che cerca di leggere le configurazioni dal percorso di classe fornito all’applicazione portlet.

All&#39;avvio, la proprietà del sistema **com.day.cq.portet.config** viene letto per rilevare l&#39;ambiente corrente. Di solito, il valore di questa proprietà è simile a qualcosa **dev**, **prod**, **test** e così via. Se non è impostato alcun ambiente, non viene letta alcuna configurazione.

Se è impostato un ambiente, la ricerca in un file di configurazione si trova nel classpath in* ***com/day/cq/portlet/{env}.config** dove **env** viene sostituito con il valore effettivo per l’ambiente. Questo file deve elencare tutti i file di configurazione per questo ambiente. La ricerca di questi file viene eseguita in base alla posizione del file di configurazione. Ad esempio, se il file contiene una riga `my.service.xml,` questo file viene letto dal percorso di classe in `com/day/cq/portlet/my.service.config.` Il nome del file è costituito dall’ID di persistenza del servizio, seguito da **.config**. Nell’esempio precedente, l’ID di persistenza è **my.service**. Il formato del file di configurazione è il formato utilizzato dal programma di installazione di Apache Sling OSGi.

Ciò significa che, per ogni ambiente, è necessario aggiungere un file di configurazione corrispondente. Una configurazione che deve essere applicata a tutti gli ambienti deve essere inserita in tutti questi file - se si tratta solo di un singolo ambiente, viene inserita solo in quel file. Questo meccanismo assicura il pieno controllo sulla configurazione che viene letta in quale ambiente.

È possibile utilizzare una proprietà di sistema diversa per rilevare l&#39;ambiente. Specificare la proprietà di sistema **com.day.cq.portet.configproperty** contenente il nome della proprietà di sistema da utilizzare invece di **com.day.cq.portet.config**.

#### Annullamento della validità della memorizzazione nella cache e della memorizzazione nella cache {#caching-and-caching-invalidation}

Il portlet, nella configurazione predefinita, memorizza nella cache le risposte ricevute da AEM WCM in una cache specifica dell’utente. Le cache devono essere invalidate quando si verificano modifiche nel contenuto dell&#39;istanza di pubblicazione. A questo scopo, in AEM WCM deve essere configurato un agente di replica nell’istanza di authoring. La cache può anche essere scaricata manualmente. Questa sezione descrive entrambe le procedure.

Il portlet può essere configurato con la propria cache, in modo che il contenuto del portlet venga visualizzato senza richiedere l’accesso a AEM. Il portale è disponibile come contenuto in /libs/portal/director. Per accedere al contenuto, avvia un’istanza AEM e scarica, utilizzando CRXDE Lite o Webdav, il file da quella posizione.

Puoi distribuire questo bundle in fase di runtime o aggiungerlo all&#39;applicazione web portlet in `WEB-INF/lib/resources/bundles` prima della distribuzione.

Dopo la distribuzione della cache, il portlet memorizza in cache il contenuto dall&#39;istanza di pubblicazione. La cache del portlet può essere invalidata con uno scaricamento del dispatcher da AEM. Per configurare il portlet per l’utilizzo della propria cache:

1. Configura un agente di replica in autore che esegue il targeting del server portale.
1. Presupponendo che il server portale venga eseguito sull&#39;host **localhost**, **porta 8080 **e l&#39;applicazione Web AEM portlet è montata nel contesto **cqportlet**, l’url per lo scaricamento della cache è `https://localhost:8080/cqportlet/cqbridge/cqpcache?Path=$(path)`. Utilizza GET come metodo.
   **Nota:** Invece di utilizzare un parametro di richiesta, puoi inviare un’intestazione http denominata **Percorso**.

#### Scaricamento della cache tramite Replication Agent {#flushing-the-cache-via-replication-agent}

Proprio come la normale invalidazione del dispatcher, un agente di replica può essere configurato per eseguire il targeting della cache AEM portlet del portale. Dopo aver configurato l’agente di replica, ogni normale attivazione della pagina scarica la cache del portale.

Se si gestiscono più nodi portale che eseguono il portlet AEM, è necessario creare un agente per ogni nodo come descritto in questa procedura.

Per configurare un agente di replica per il portale:

1. Accedi all’istanza di authoring.
1. Nella scheda Siti Web fai clic su *Strumenti* scheda .
1. Fai clic su **Nuova pagina...** negli agenti di replica **Nuovo...** menu.

   ![screen_shot_2012-02-15at40647pm](assets/screen_shot_2012-02-15at40647pm.png)

1. In *Modello*, seleziona *Agente di replica*, quindi immetti un nome per l&#39;agente. Fai clic su *Crea*.

   ![screen_shot_2012-02-15at40817pm](assets/screen_shot_2012-02-15at40817pm.png)

1. Fare doppio clic sull&#39;agente di replica appena creato. Viene visualizzato come non valido in quanto non è ancora stato configurato.

   ![screen_shot_2012-02-15at41001pm](assets/screen_shot_2012-02-15at41001pm.png)

1. Fai clic su **Modifica.**
1. In **Impostazioni** seleziona la scheda **Abilitato** casella di controllo, seleziona **Flush del Dispatcher** come tipo di serializzazione e immetti un timeout per un nuovo tentativo (ad esempio, 60000).

   ![screen_shot_2012-02-15at42101pm](assets/screen_shot_2012-02-15at42101pm.png)

1. Fai clic sul pulsante **Trasporti** scheda .
1. In **URI** , immetti l’URI di scaricamento (URL) del portlet. L’URI si trova nella seguente forma:

   ```xml
   https://<wps-host>:<port>/<wps-context>/<cq5-portlet-context>/cqbridge/cqpcache
   ```

   ![screen_shot_2012-02-15at42322pm](assets/screen_shot_2012-02-15at42322pm.png)

1. Fai clic sul pulsante **Esteso** scheda .

   ![screen_shot_2012-02-15at42515pm](assets/screen_shot_2012-02-15at42515pm.png)

1. In **metodo HTTP** campo, tipo **GET**.
1. In **Intestazioni HTTP** campo, fai clic su **+** per aggiungere una nuova voce e un nuovo tipo **Percorso: {path}**.
1. Se necessario, fai clic sul pulsante **Proxy** e immetti le informazioni sul proxy all&#39;agente.
1. Fai clic su **OK** per salvare le modifiche.
1. Per verificare la connessione, fai clic sul pulsante **Prova connessione** link. Viene visualizzato un messaggio di log che indica se il test di replica è riuscito. Esempio:

   ![screen_shot_2012-02-15at42639pm](assets/screen_shot_2012-02-15at42639pm.png)

#### Scaricamento manuale della cache del portlet {#manually-flushing-the-portlet-cache}

Puoi scaricare manualmente la cache del portlet accedendo allo stesso URL configurato per l’agente di replica. Vedi [Scaricamento della cache](#flushing-the-cache-via-replication-agent) per il modulo dell’URL. Inoltre, l&#39;URL deve essere esteso con un parametro URL Path=&lt;path> per indicare cosa eseguire lo scaricamento.

Esempio:

`https://10.0.20.99:10040/wps/PA_CQ5_Portlet/cqbridge/cqpcache?Path=*` scarica la cache completa. `https://10.0.20.99:10040/wps/PA_CQ5_Portlet/cqbridge/cqpcache?Path=/content/mypage/xyz` vampate `/content/mypage/xyz` dalla cache.

### Sicurezza del portale {#portal-security}

Il portale è il meccanismo di autenticazione alla guida. Puoi accedere a AEM sia con un utente tecnico, l’utente del portale, un gruppo e così via. Il portlet non ha accesso alla password per l&#39;utente nel portale, quindi se il portlet non conosce tutte le credenziali per l&#39;accesso corretto a un utente, deve essere utilizzata una soluzione SSO. In questo caso, il portlet AEM inoltra tutte le informazioni necessarie a AEM, che a sua volta inoltrano tali informazioni all’archivio AEM sottostante. Questo comportamento è collegabile e può essere personalizzato.

### Autenticazione su Publish {#authentication-on-publish}

Questa sezione descrive le modalità di autenticazione disponibili che il portlet può utilizzare per comunicare con le istanze WCM AEM sottostanti.

Per impostazione predefinita non vengono inviate informazioni utente all’istanza di pubblicazione di AEM; il contenuto viene sempre visualizzato come utente anonimo. Se è necessario fornire informazioni specifiche per l’utente da AEM o se è richiesta l’autenticazione utente per la pubblicazione, è necessario attivarle.

#### Accesso alla configurazione di autenticazione del portlet {#accessing-the-portlet-s-authentication-configuration}

Le opzioni di configurazione dell&#39;autenticazione utilizzate dal portlet AEM istanze WCM sono disponibili nella console Web (configurazione OSGi).

>[!NOTE]
>
>Quando lavori con AEM esistono diversi metodi per gestire le impostazioni di configurazione per i servizi OSGi (nodi console o repository).
>
>Vedi [Configurazione di OSGi](/help/sites-deploying/configuring-osgi.md) per informazioni complete.

Per accedere alla configurazione di autenticazione del portlet:

1. Accedi alla console Web all’URL seguente:

   `https://localhost:8080/cqportlet/cqbridge/system/console`

   Ad esempio, nella configurazione predefinita:

   `https://wps-host:10040/wps/PA_CQ5_Portlet/cqbridge/system/console`

1. Accedi alla console Web. Le credenziali predefinite sono `admin/admin`.
1. Nella console, seleziona **Configurazione**.
1. In **Configurazione** seleziona un particolare servizio da configurare. I servizi sono forniti dal portlet nel framework OSGi.

   | Nome servizio | Descrizione |
   |---|---|
   | Autenticatore Day Portal Director | Configura quale modalità di autenticazione viene utilizzata per AEM istanze WCM. A seconda della modalità selezionata, è possibile specificare un utente tecnico o il nome del cookie SSO. Inoltre, è possibile abilitare l’autenticazione per AEM istanze di pubblicazione WCM. |
   | Cache dei file Director del portale giornaliero | Configura i parametri della modalità in cui il portlet memorizza nella cache le risposte ricevute dalle istanze WCM AEM. |
   | Servizio client HTTP Director Day Portal | Configura la modalità di connessione del portlet tramite HTTP alle istanze WCM sottostanti AEM. Ad esempio, puoi specificare un server proxy. |
   | Gestore di impostazioni internazionali Director Day Portal | Configura le impostazioni internazionali supportate dal portlet. Le richieste di AEM istanze WCM si basano sulle impostazioni internazionali dell’utente; ad esempio, la lingua utente *German *richiederebbe `/content/geometrixx/de/`.... |
   | Day Portal Director Privilege Manager | Configura se il portlet deve testare la scheda Siti web in base all&#39;utente attualmente connesso. |
   | Renderer della barra degli strumenti Director del portale giornaliero | Personalizza il rendering della barra degli strumenti del portlet. |

1. Inoltre, puoi configurare la console Web e il servizio di registrazione. Ad esempio, puoi modificare le credenziali di amministratore per la console Web facendo clic sul collegamento alla console di gestione Apache Felix OSGi.

#### Modalità utente tecnica {#technical-user-mode}

In modalità predefinita, tutte le richieste emesse dal portlet per l&#39;istanza di authoring AEM WCM vengono autenticate utilizzando lo stesso utente tecnico, indipendentemente dall&#39;utente del portale corrente. La modalità utente tecnico è attivata per impostazione predefinita. Attiva/disattiva questa modalità nella relativa schermata di configurazione nella console di gestione OSGi:

L&#39;utente tecnico specificato deve esistere nell&#39;istanza di authoring AEM WCM e nell&#39;istanza di pubblicazione se **Autentica su Pubblica** è abilitato. Assicurati di assegnare agli utenti i privilegi di accesso sufficienti per il lavoro di authoring.

#### SSO {#sso}

Il portlet supporta SSO con AEM preconfigurato. Il servizio di autenticazione può essere configurato per utilizzare SSO e trasmettere l&#39;utente del portale corrente con il formato **Base** come cookie denominato `cqpsso` AEM. AEM deve essere configurato per utilizzare il gestore di autenticazione SSO per il percorso /. Anche in questo caso è necessario configurare il nome del cookie.

La `crx-quickstart/repository/repository.xml` per AEM repository deve essere configurato di conseguenza:

```xml
<LoginModule class="com.day.crx.security.authentication.CRXLoginModule">
  ...
  <param name="trust_credentials_attribute" value="TrustedInfo"/>
  <param name="anonymous_principal" value="anonymous"/>
</LoginModule>
```

#### Modalità autenticazione SSO {#sso-authentication-mode}

Il portlet può eseguire l’autenticazione per AEM WCM utilizzando lo schema Single Sign On (SSO). In questa modalità, l&#39;utente che ha effettuato l&#39;accesso al portale viene inoltrato a AEM WCM sotto forma di cookie SSO. Se si utilizza la modalità SSO, tutti gli utenti del portale con accesso al portlet AEM devono essere noti alle istanze WCM AEM sottostanti, più comunemente sotto forma di AEM WCM collegato a LDAP, o avendo creato manualmente gli utenti in precedenza. Inoltre, prima di abilitare SSO nel portlet, l&#39;istanza di authoring AEM WCM sottostante (e l&#39;istanza di pubblicazione, se **Autentica su Pubblica** è abilitato) deve essere configurato per accettare richieste basate su SSO.

Per configurare il portlet per l&#39;utilizzo della modalità di autenticazione SSO, completa i seguenti passaggi (descritti in dettaglio nelle sezioni seguenti):

* Abilitare AEM archivio WCM per accettare credenziali affidabili.
* Abilitare l’autenticazione SSO in AEM WCM.
* Abilita l&#39;autenticazione SSO nel portlet AEM.

#### Abilitazione dell’archivio AEM WCM per accettare credenziali affidabili {#enabling-aem-wcm-s-repository-to-accept-trusted-credentials}

Prima di poter abilitare SSO per AEM WCM, l&#39;archivio sottostante deve essere configurato per accettare le credenziali affidabili fornite da AEM WCM. A questo scopo, è necessario configurare AEM repository.xml.

1. Nel file system in cui è installato AEM WCM, apri il file seguente:

   `//crx-quickstart/repository/repository.xml`

1. Nel file XML, trova la voce per **Modulo di accesso** e aggiungi l&#39;attributo trust_credentials_attribute alla relativa configurazione:

   ```xml
   <LoginModule class="com.day.crx.security.authentication.CRXLoginModule">
     ...
     <param name="trust_credentials_attribute" value="TrustedInfo"/>
     <param name="anonymous_principal" value="anonymous"/>
   </LoginModule>
   ```

1. Riavvia AEM WCM per rendere effettive le modifiche.

#### Abilitazione dell’autenticazione SSO in AEM WCM {#enabling-sso-authentication-in-the-aem-wcm}

Per abilitare SSO in AEM WCM, accedi alla voce di configurazione pertinente nella Console di gestione Web Apache Felix di AEM WCM (OSGi):

1. Accedi alla console tramite il suo URI all’indirizzo https://&lt;aem-host>:&lt;port>/system/console.
1. Nel menu Configurazione, selezionare Handler autenticazione SSO. In questo esempio, il gestore SSO accetta richieste SSO per tutti i percorsi in base al cookie fornito dal portlet AEM. La configurazione può variare.

   | Percorso | / | Abilita il gestore SSO per tutte le richieste |
   |---|---|---|
   | Nomi dei cookie | cqpsso | Nome del cookie fornito dal portlet configurato nella console OSGi del portlet. |

1. Fai clic su **Salva** per abilitare SSO. SSO è ora lo schema di autenticazione principale.

Per ogni richiesta AEM ricevuta da WCM, si tenta innanzitutto l&#39;autenticazione basata su SSO. In caso di errore, viene eseguito un fallback al normale schema di autenticazione di base. Come tale, le normali connessioni a AEM WCM senza SSO rimangono possibili.

#### Abilitazione dell&#39;autenticazione SSO in un portlet AEM {#enabling-sso-authentication-in-a-aem-portlet}

Affinché l’istanza WCM sottostante AEM possa accettare richieste SSO, la modalità di autenticazione del portlet deve essere commutata da **Tecnico** a **SSO**.

Per abilitare l&#39;autenticazione SSO in un portlet AEM:

1. Accedi alla console tramite il suo URI all’indirizzo https://&lt;aem-host>:&lt;port>/system/console.
1. Nel menu Configurazione, seleziona Day Portal Director Authenticator dall’elenco delle configurazioni disponibili.
1. In Modalità, selezionare SSO. Lascia gli altri parametri con i loro valori predefiniti.

   ![chlimage_1-135](assets/chlimage_1-135.png)

1. Fai clic su Salva per abilitare SSO per il portlet.

   A scopo di test, accedi al portlet con l’utente amministrativo del portale dopo aver creato lo stesso utente in AEM WCM con privilegi di amministratore.

Dopo aver eseguito questa procedura, le richieste vengono autenticate utilizzando SSO. Un frammento tipico della comunicazione HTTP rivela la presenza delle seguenti intestazioni specifiche SSO e Portlet:

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

### Abilitazione dell’autenticazione PIN {#enabling-pin-authentication}

Se non utilizzi le funzioni di modifica in linea predefinite del portlet di contenuti AEM, ma desideri che la parte di authoring e amministrazione del portlet all’esterno del portale direttamente nell’istanza di authoring AEM, devi abilitare l’autenticazione PIN. È inoltre necessario modificare la configurazione dei pulsanti di gestione.

Per aprire la pagina di amministrazione del sito web o modificare una pagina dal portlet, il portlet del contenuto AEM utilizza la nuova autenticazione pin. Per impostazione predefinita, l’autenticazione tramite pin è disabilitata, pertanto è necessario apportare le seguenti modifiche alla configurazione in AEM:

1. Abilita l&#39;autenticazione affidabile in AEM aggiungendo le informazioni attendibili nel file repository.xml:

   ```xml
   <LoginModule class="com.day.crx.security.authentication.CRXLoginModule">
     ...
     <param name="trust_credentials_attribute" value="TrustedInfo"/>
   </LoginModule>
   ```

1. Nella console di configurazione OSGi, per impostazione predefinita all’indirizzo https://localhost:4502/system/console/configMgr, seleziona **Gestore autenticazione PIN CQ** dal menu a discesa.
1. Modifica le **Percorso directory principale URL** per contenere solo il valore singolo **/**.

### Privilegi {#privileges}

Alcune funzioni del portlet sono protette da privilegi. L&#39;utente corrente deve disporre di questo privilegio per poter accedere a questa funzione. Sono disponibili i seguenti privilegi predefiniti:

* &quot;toolbar&quot; : Si tratta del privilegio generale per visualizzare/utilizzare la barra degli strumenti nel portlet.
* &quot;prefs&quot; : Se l’utente dispone di questo privilegio, può vedere/modificare le preferenze del portlet.
* &quot;cq-author:edit&quot; : Con questo privilegio, l’utente può richiamare la visualizzazione di modifica del contenuto.
* &quot;cq-author:preview&quot; : Con questo privilegio, l’utente può visualizzare l’anteprima.
* &quot;cq-author:siteadmin&quot; : Con questo privilegio, l&#39;utente è autorizzato ad aprire l&#39;amministratore del sito in AEM.

L’approccio migliore per gestire i privilegi consiste nell’utilizzare i ruoli del portale e assegnare ruoli a tali privilegi. Questo può essere fatto tramite una configurazione OSGi. Il &quot;Day Portal Director Privilege Manager&quot; può essere configurato con un set di ruoli per ogni privilegio. Se l’utente dispone di uno dei ruoli, l’utente dispone del privilegio corrispondente.

Inoltre è possibile definire questo accesso basato su un ruolo basato su una base di istanze di portlet per. La finestra di dialogo delle preferenze del portlet contiene un campo di input per ciascuno dei privilegi di cui sopra. Per ogni privilegio è possibile configurare un elenco di ruoli portlet separati da virgole. Se un valore è configurato, questo esclude la configurazione globale dal servizio &quot;Day Portal Director Privilege Manager&quot; e potrebbe essere necessario aggiungere gli stessi ruoli da questa impostazione globale, in quanto i ruoli non vengono uniti. Se non viene specificato alcun valore, viene utilizzata la configurazione globale.

### Personalizzazione dell&#39;applicazione AEM portlet {#customizing-the-aem-portlet-application}

L&#39;applicazione portlet AEM fornita avvia un contenitore OSGi all&#39;interno dell&#39;applicazione web proprio come AEM. Questa architettura consente di sfruttare tutti i vantaggi di OSGi:

* Facile da aggiornare ed estendere
* Fornisce aggiornamenti a caldo del portlet senza alcuna interazione del server portale
* Facile da personalizzare

### Pulsanti della barra degli strumenti {#toolbar-buttons}

La barra degli strumenti e i relativi pulsanti sono configurabili e personalizzabili. È possibile aggiungere pulsanti personalizzati alla barra degli strumenti o definire quali pulsanti visualizzare in quale modalità. Ogni pulsante è un servizio OSGi configurabile tramite una configurazione OSGi.

La console web OSGi elenca tutte le configurazioni dei pulsanti presenti nella **Configurazione** scheda . Per ogni pulsante, puoi definire in quale modalità viene visualizzato questo pulsante. Questo consente di disattivare un pulsante rimuovendo, ad esempio, tutte le modalità.

Per impostazione predefinita, il portlet di contenuti AEM utilizza la funzionalità di modifica in linea. Tuttavia, se preferisci passare all’istanza di authoring AEM per la modifica, abilita **Pulsante SiteAdmin** e **Pulsante ContentFinder**, ma disattiva il **Pulsante Modifica**. In questo caso, assicurati di configurare correttamente l’autenticazione PIN in AEM.

Il layout della barra degli strumenti del portlet può essere personalizzato installando un bundle attraverso la console Web Felix del portlet, che contiene CSS/HTML personalizzati in una posizione predefinita.

#### Struttura del bundle {#bundle-structure}

Di seguito è riportato un esempio di struttura del bundle:

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

La cartella META-INF contiene il file MANIFEST.MF richiesto da OSGi per identificarlo come bundle. Viene visualizzato come segue:

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

Il fatto che HTML/CSS/images si trovino all&#39;interno della cartella /com/day/cq/portlet/toolbar/layout è richiesto dal portlet e non può essere modificato. Sulle stesse linee, le intestazioni Import-Package ed Export-Package in MANIFEST.MF devono essere chiamate anche /com/day/cq/portlet/toolbar/layout. Bundle-SymbolicName deve essere un nome di pacchetto univoco e completo.

Puoi costruirlo utilizzando uno strumento come maven o creare manualmente un file jar di questo tipo con l’intestazione pertinente impostata come mostrato in questa sezione.

#### Viste della barra degli strumenti del portlet {#portlet-toolbar-views}

La barra degli strumenti della portlet ha sostanzialmente due stati di visualizzazione. È possibile personalizzare ciascuna visualizzazione e i pulsanti associati con un rispettivo file HTML.

#### Vista di pubblicazione {#publish-view}

Nella visualizzazione di pubblicazione è disponibile un solo pulsante che consente di passare alla visualizzazione Gestisci. La visualizzazione di pubblicazione è rappresentata dal file publish.html in [bundle precedente](/help/sites-deploying/configuring-osgi.md#bundles). In HTML è possibile utilizzare i seguenti segnaposto, sostituiti dal portlet con i rispettivi contenuti durante il rendering:

#### Pubblicare Segnaposto Vista {#publish-view-placeholders}

| Stringa segnaposto | Descrizione |
|---|---|
| {buttonManage} | Il segnaposto viene sostituito dal **Gestisci** che consente di passare lo stato del portlet allo stato di gestione. |

#### Gestisci vista {#manage-view}

La vista Gestisci presenta quattro pulsanti: Modifica, scheda Siti Web, Aggiorna e Indietro. La vista Gestisci è rappresentata dal file manage.html nel [bundle precedente](/help/sites-deploying/configuring-osgi.md#bundles). In HTML è possibile utilizzare i seguenti segnaposto, sostituiti dal portlet con i rispettivi contenuti durante il rendering:

#### Gestisci segnaposto visualizzazione {#manage-view-placeholders}

| Stringa segnaposto | Descrizione |
|---|---|
| {buttonEdit} | Il segnaposto viene sostituito dal **Modifica** che apre una nuova finestra con la pagina corrente in modalità di modifica AEM. |
| {scheda buttonWebsites} | Segnaposto, sostituito da un pulsante che apre la scheda Siti Web di AEM WCM. |
| {buttonRefresh} | Aggiorna la visualizzazione corrente. |
| {buttonBack} | Ripristina la visualizzazione di pubblicazione del portlet. |

#### Pulsanti {#buttons}

I pulsanti, a prescindere dalla visualizzazione, utilizzano lo stesso HTML comune, definito in button.html.

In HTML è possibile utilizzare i seguenti segnaposto, sostituiti dal portlet con i rispettivi contenuti durante il rendering:

#### Pulsanti di visualizzazione Gestisci e pubblica {#manage-and-publish-view-buttons}

| Stringa segnaposto | Descrizione |
|---|---|
| {name} | Nome del pulsante, ad esempio** author, back, refresh** e così via. |
| {id} | ID CSS del pulsante. |
| {url} | URL della destinazione del pulsante. |
| {text} | Etichetta del pulsante. |
| {onclick} | Javascript **onclick** (contiene {url}). |

Esempio di file button.html :

```xml
<div class="cqp_button">

 <a href="#" onclick="{onclick}">

 <img src="/wps/PA_CQ5_Portlet/cqbridge/static/{id}.gif" alt="{text}"
title="{text}"/>

 </a>
</div>
```

#### Installazione di un layout personalizzato {#installing-a-custom-layout}

Per installare un layout personalizzato, accedi alla sezione **Bundle **Bundle **del portlet e carica il bundle.

#### Pacchetti {#packages}

Per istruzioni dettagliate, consulta Gestione pacchetti nella documentazione AEM per caricare o creare pacchetti per l’installazione.

### Gestione dei collegamenti {#link-handling}

Tutti i collegamenti vengono riscritti in modo che funzionino nel contesto del portale. Per impostazione predefinita vengono utilizzati collegamenti con parametri di rendering. Il rewriter di Portal Director HTML può essere configurato in modo da utilizzare al suo posto i collegamenti delle azioni.

Puoi anche definire parametri di richiesta aggiuntivi da interrogare per il percorso di contenuto da visualizzare. Questa funzione è utile, ad esempio, se esiste un collegamento dall’esterno a un contenuto specifico.

Inoltre, è possibile configurare il rewriter di Portal Director HTML con un elenco di espressioni regolari definite esclusioni per la riscrittura dei collegamenti. Ad esempio, se disponi di collegamenti relativi a sistemi esterni, devi aggiungerli a questo elenco di esclusione.

### Localizzazione {#localization}

Il portlet di contenuti AEM dispone di una funzione di localizzazione integrata che garantisce che il contenuto di AEM sia nella lingua corretta.

Questo avviene in due passaggi:

1. Il rilevatore delle impostazioni internazionali della directory portale rileva le impostazioni internazionali dell&#39;utente del portale ottenendo le impostazioni internazionali dal portale. Questo servizio deve essere configurato con l&#39;elenco delle lingue disponibili in AEM.
1. Il gestore di impostazioni locali Director del portale gestisce la localizzazione della richiesta corrente. Prende il percorso del contenuto richiesto, ad esempio `/content/geometrixx/en/company.html`e in base alla configurazione, riscrive il **en** con le impostazioni internazionali effettive dell’utente.

Il gestore locale Director del portale può essere configurato con i percorsi per controllare le informazioni sulle impostazioni internazionali - di solito questo include tutto ciò che si trova sotto `/content` e con la posizione delle informazioni sulle impostazioni internazionali nel percorso. Per impostazione predefinita, il gestore di impostazioni internazionali segue la ridefinizione della strutturazione di siti multilingue in AEM.

Se il tuo sito non dispone di una regola restrittiva per la gestione delle informazioni sulle impostazioni internazionali all&#39;interno del percorso, è possibile sostituire il gestore impostazioni internazionali con la tua implementazione.

### Servizi OSGi opzionali {#optional-osgi-services}

I servizi OSGi opzionali possono essere implementati per personalizzare varie parti del portlet. Ogni servizio corrisponde a un&#39;interfaccia Java. Questa interfaccia può essere implementata e distribuita tramite un bundle nel portlet.

<table>
 <tbody>
  <tr>
   <td>RequestTracker</td>
   <td>Il tracciamento della richiesta viene notificato ogni volta che il contenuto viene visualizzato dal portlet. Questo consente di tenere traccia delle invocazioni del portlet.</td>
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
   <td>Processore Http</td>
   <td>Questo servizio può essere utilizzato per aggiungere informazioni a ogni chiamata http a AEM.</td>
  </tr>
  <tr>
   <td>PortletAction</td>
   <td>Aggiungi un’azione personalizzata al portlet: questa azione può essere richiamata tramite un collegamento di azione del portlet.</td>
  </tr>
  <tr>
   <td>PortletDecoratorService</td>
   <td>Questo servizio può essere utilizzato per decorare il contenuto del portlet.</td>
  </tr>
  <tr>
   <td>ResourceProvider</td>
   <td>Aggiungi il tuo provider di risorse per fornire al client una certa risorsa tramite un collegamento alla risorsa del portlet.</td>
  </tr>
  <tr>
   <td>TextMapper</td>
   <td>Consente di pubblicare file HTML, CSS e JavaScript di elaborazione.</td>
  </tr>
  <tr>
   <td>PulsanteBarraStrumenti</td>
   <td>Aggiungi un pulsante personalizzato alla barra degli strumenti.</td>
  </tr>
  <tr>
   <td>UrlMapper</td>
   <td>Aggiungi un servizio per applicare una mappatura URL personalizzata o riscrivere.</td>
  </tr>
  <tr>
   <td>UserInfoProvider</td>
   <td>Aggiungi le tue informazioni sull'utente. Questo servizio può essere utilizzato per ottenere informazioni dal portale al portlet.</td>
  </tr>
 </tbody>
</table>

#### Sostituzione dei servizi predefiniti {#replacing-default-services}

I seguenti servizi hanno un’implementazione predefinita nel portlet del contenuto (con un’interfaccia Java corrispondente). Per personalizzare, è necessario distribuire nell’applicazione portlet un bundle contenente la nuova implementazione del servizio.

Quando implementi tale servizio, assicurati di impostare la variabile **service.ranking** proprietà del servizio a un valore positivo. L’implementazione predefinita utilizza la classificazione** 0** e il portlet utilizza il servizio con la classificazione più alta.

| **Nome** | **Descrizione** | **Comportamento predefinito** |
|---|---|---|
| Autenticatore | Fornisce informazioni di autenticazione a AEM | Utilizza un utente tecnico configurabile sia per l’authoring che per la pubblicazione. O SSO può essere utilizzato. |
| HTMLRewriter | Consente di riscrivere collegamenti, immagini e così via. | Riscrive i collegamenti AEM ai collegamenti portale, possono essere estesi da un UrlMapper e da un TextMapper |
| HttpClientService | Gestisce tutte le connessioni http | Implementazione standard |
| LocaleHandler | Gestisce le informazioni sulle impostazioni internazionali | Consente di riscrivere un collegamento al contenuto rispetto alle impostazioni internazionali. |
| LocaleDetector | Rileva le impostazioni internazionali dell’utente. | Utilizza le impostazioni internazionali fornite dal portale. |
| PrivilegeManager | Verifica i diritti utente | Controlla l&#39;accesso all&#39;istanza di authoring se l&#39;utente è autorizzato a modificare il contenuto |
| ToolbarRenderer | Rendering della barra degli strumenti | Aggiunge una funzionalità della barra degli strumenti |

### Eventi Portlet {#portlet-events}

L&#39;API portlet (JSR-286) specifica gli eventi portlet. Il portlet dei contenuti AEM ha un ponte integrato, che distribuisce eventi portlet per il portlet AEM come eventi OSGi - questo rende la gestione degli eventi portlet collegabili.

Se desideri gestire eventi specifici, dichiarali come eventi riceventi nel descrittore di distribuzione (o configuralo tramite il server del portale) e implementa un servizio OSGi che dichiara l’interfaccia EventHandler (consulta le specifiche OSGi EventAdmin ).

Ogni volta che si verifica un evento portlet, viene inviato un evento OSGi specifico che richiama il tuo handler. Il gestore ottiene tutte le informazioni di contesto e può aggiornare di conseguenza lo stato del portlet o inviare nuovi eventi. In pratica, all&#39;interno del metodo handle è possibile utilizzare tutte le funzionalità della fase evento portlet.

## Utilizzo di AEM come portale {#using-aem-as-a-portal}

Utilizza il componente Portlet per aggiungere finestre di portlet alle pagine AEM. Le librerie condivise installate nel server applicazioni abilitano il componente Portlet per rilevare le applicazioni di portlet distribuite.

Per utilizzare AEM come portale, eseguire le operazioni seguenti:

1. Installa il componente Portlet e le librerie condivise.
1. Aggiungi il componente Portlet alla barra laterale.
1. Configura e distribuisci l’applicazione web che contiene i portlet che desideri visualizzare nel componente Portal.
1. Aggiungi il componente Portlet a una pagina e seleziona il portlet da visualizzare.

>[!NOTE]
>
>Puoi utilizzare il componente portlet solo quando AEM viene distribuito come applicazione web. ([Vedere Installazione di AEM con un server applicazioni](/help/sites-deploying/application-server-install.md).)

### Installazione del componente portlet {#installing-the-portlet-component}

Il file JAR AEM Quickstart contiene i file dei componenti portlet. Per ottenere i file (cq-portlet-components.zip), puoi eseguire il Quickstart o estrarre il contenuto.

1. Esegui o estrae il contenuto del file JAR Quickstart e individua di conseguenza il file cq-portlet-components.zip:

   * Esegui avvio rapido: crx-quickstart/opt/portal
   * Estrai contenuto di Quickstart: static/opt/portal

1. Apri Gestione pacchetti dell&#39;istanza di authoring CQ5 distribuita nel server applicazioni. (https://)*appserverhost*:*porta*/cq5author/crx/packmgr)

1. Utilizza Gestione pacchetti per [Carica e installa](/help/sites-administering/package-manager.md#uploading-packages-from-your-file-system) il pacchetto cq-portlets-components.zip.

   Il pacchetto installa il cq-portlet-director-sharedlibs-x.x.x.jar nella cartella /libs/portal/director nell&#39;archivio.

1. Copia cq-portlet-director-sharedlibs-x.x.x.jar sul tuo disco rigido. Utilizzare qualsiasi mezzo per ottenere il file, ad esempio FileVault o un client WebDAV.
1. Sposta il file cq-portlet-director-sharedlibs.x.x.x.jar nella cartella della libreria condivisa del server applicazioni in modo che le classi siano disponibili per le applicazioni portlet distribuite.

### Aggiunta del componente Portlet alla barra laterale {#adding-the-portlet-component-to-sidekick}

Aggiungi il componente portlet al sistema di paragrafi in modo che sia disponibile per gli autori.

1. Nella barra laterale fate clic sull’icona del righello per accedere alla modalità Progettazione.
1. Accanto al `Design of par` intestazione sopra il primo paragrafo, fai clic su **Modifica**.

1. In **Generale** categoria di componenti, selezionare la casella di controllo accanto al componente Portlet e fare clic su OK.

![chlimage_1-25](assets/chlimage_1-25.jpeg)

### Configurazione e distribuzione delle applicazioni portlet {#configuring-and-deploying-your-portlet-applications}

Distribuisci i portlet nel contenitore Web dell’applicazione server in modo che siano disponibili per il componente Portal. Prima di distribuire l&#39;applicazione portlet, è necessario configurare l&#39;applicazione in modo che carichi il servlet contenitore del portale AEM. Questa configurazione consente al componente Portlet di accedere ai portlet.

1. Estrarre il contenuto del file WAR dell&#39;applicazione portlet.

   **Suggerimento:** Il jar xf *nome app* Il comando .war estrae i file.

1. Apri il file web.xml in un editor di testo.
1. Aggiungi la seguente configurazione del servlet all&#39;interno dell&#39;elemento web-app:

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

1. Salva il file web.xml e riconfeziona il file WAR.

   **Suggerimento:** La `jar cvf nameofapp.war *` aggiunge il contenuto della directory corrente al file nameofapp.war.

1. Distribuire l&#39;applicazione portlet al server applicazioni. Per informazioni, consulta la documentazione relativa al server delle applicazioni.

### Aggiunta di portlet alla pagina AEM {#adding-portlets-to-your-aem-page}

Utilizza il componente Portale per aggiungere una finestra portlet alla pagina web. Utilizza le proprietà del componente per specificare il portlet da visualizzare.

1. Nella pagina web, trascina **Portlet** dal gruppo Generale nella barra laterale alla pagina.

   >[!NOTE]
   >
   >Dopo aver trascinato il componente sulla pagina, ricarica la pagina per assicurarti che funzioni correttamente.

1. Fai doppio clic sul componente per aprire le proprietà del portlet.
1. In **Entità portlet** dal menu a discesa, seleziona il portlet dall’elenco.
1. Seleziona o deseleziona la casella di controllo **Nascondi barra del titolo **a seconda che desideri visualizzare o meno la barra del titolo del portlet.
1. In **Finestra portlet** immetti un ID univoco della finestra Portlet, se lo desideri.

   >[!NOTE]
   >
   >Se prevedi di utilizzare lo stesso portlet più volte sulla stessa pagina, assegna a ogni portlet un ID finestra diverso.

1. Fai clic su **OK**. Il portlet viene visualizzato sulla pagina AEM.

   ![chlimage_1-136](assets/chlimage_1-136.png)

## Installazione, configurazione e utilizzo di AEM in un portlet {#installing-configuring-and-using-aem-in-a-portlet}

Per accedere al contenuto fornito da AEM WCM, il server portale deve essere dotato del Portlet Director del Portale AEM. A tale scopo, installa, configura e aggiungi il portlet alla pagina del portale utilizzando i passaggi descritti in questa sezione.

Per impostazione predefinita, il portlet si connette all&#39;istanza di pubblicazione su localhost:4503 e all&#39;istanza di authoring su localhost:4502. Questi valori possono essere modificati durante la distribuzione del portlet. Il direttore del portale è disponibile come contenuto nell&#39;archivio sotto /libs/portal/directory. Sarà necessario scaricare il file war dell&#39;applicazione prima di utilizzarlo.

### Download del file WAR {#downloading-the-war-file}

1. Utilizzando Webdav o CRXDE Lite, vai a /libs/portal/director.

1. Scarica *cq-portlet-webapp.war*.

>[!NOTE]
>
>Queste procedure utilizzano il portale Websphere come esempio, anche se sono il più generiche possibile; tieni presente che le procedure variano per gli altri portali web. Sebbene i passaggi siano sostanzialmente identici per tutti i portali web, è necessario riadattare i passaggi per un particolare portale web.

#### Installazione del portlet {#installing-the-portlet}

Per installare il portlet:

1. Accedi al portale con privilegi di amministratore.
1. Passa alla parte Gestione portlet del portale web.
1. Fai clic su Installa e individua l&#39;applicazione portlet AEM (cq-portlet-webapp.war) scaricata e immetti altre informazioni importanti sul portlet.

   Per altre informazioni essenziali sul portlet, è possibile accettare le impostazioni predefinite o modificare i valori. Se si accettano i valori predefiniti, il portlet è disponibile all’indirizzo https://&lt;wps-host>:&lt;port>/wps/PA_CQ5_Portlet. La console di amministrazione OSGi fornita dal portlet è disponibile all’indirizzo https://&lt;wps-host>:&lt;port>/wps/ PA_CQ5_Portlet/cqbridge/system/console (il nome utente/password predefinito è admin/admin).

1. Assicurati che l&#39;applicazione portlet si avvii automaticamente selezionando tale opzione o casella di controllo e salva le modifiche. Viene visualizzato un messaggio di errore durante l&#39;installazione.

#### Configurazione del portlet {#configuring-the-portlet}

Dopo aver installato il portlet, devi configurarlo in modo che conosca gli URL delle istanze AEM sottostanti (authoring e pubblicazione). Puoi anche configurare altre opzioni.

Per configurare il portlet:

1. Nella finestra di amministrazione del portale dell’app server, passa alla gestione del portlet, in cui sono elencati tutti i portlet e seleziona il portlet Director del portale AEM.
1. Configura il portlet, a seconda delle necessità. Ad esempio, potrebbe essere necessario modificare l’URL per le istanze di authoring e pubblicazione e l’URL per il percorso iniziale. Le configurazioni predefinite sono descritte in [Preferenze del portlet](/help/sites-administering/aem-as-portal.md#portlet-preferences).

   >[!NOTE]
   >
   >Se il portlet è configurato per connettersi a istanze di authoring e pubblicazione AEM che sono in esecuzione su un percorso contestuale diverso da** /**, devi abilitare la forza **CQUrlInfo** nella configurazione di Html Library Manager di queste istanze AEM (ad esempio tramite Felix Webconsole) o la modifica non funzionerà e la finestra di dialogo delle preferenze non verrà visualizzata.

1. Salva le modifiche di configurazione nel server app.

1. Passa alla console di amministrazione OSGI per il portlet. Il percorso predefinito è `https://<wps-host>:<port>/wps/PA_CQ5_Portlet/cqbridge/system/console/configMgr`. Il nome utente/password predefinito è **admin/admin**.

1. Seleziona la **Configurazione del server CQ Director del portale giornaliero** configura e modifica i seguenti valori:

   * **URL di base dell’autore**: L&#39;URL di base per l&#39;istanza di authoring AEM.
   * **URL di base della pubblicazione**: L&#39;URL di base per l&#39;istanza di pubblicazione AEM.
   * **Autore Utilizzato Come Pubblicazione**: L’istanza di authoring viene utilizzata come istanza di pubblicazione (per lo sviluppo)?

   ![chlimage_1-137](assets/chlimage_1-137.png)

1. Fai clic su **Salva**. È ora possibile aggiungere il portlet alle pagine del portale e utilizzare il portale.

### URL del contenuto {#content-urls}

Quando il contenuto viene richiesto da AEM, il portlet utilizza la modalità di visualizzazione corrente (pubblicazione o authoring) e il percorso corrente per assemblare un URL completo. Con i valori predefiniti, il primo url è `https://localhost:4503/content/geometrixx/en.portlet.html`. Il valore del `htmlSelector` viene aggiunto automaticamente all&#39;URL prima dell&#39;estensione .

Se il portlet passa alla modalità Aiuto e alla `appendHelpViewModeAsSelector` viene selezionato, quindi il `help` viene aggiunto anche il selettore , ad esempio `https://localhost:4503/content/geometrixx/en.portlet.html.help`. Se la finestra del portlet è ingrandita e la `appendMaxWindowStateAsSelector` viene selezionato, quindi viene aggiunto anche il selettore, ad esempio: `https://localhost:4503/content/geometrixx/en.portlet.max.help`.

I selettori possono essere valutati in AEM e un modello diverso può essere utilizzato per diversi selettori.

### Utilizzo di una mappa URL contenuto in AEM {#using-a-content-url-map-in-aem}

Di solito il percorso iniziale punta direttamente al contenuto in AEM. Tuttavia, se desideri mantenere i percorsi iniziali in AEM anziché nelle preferenze del portlet, puoi indirizzare il percorso iniziale a una mappa di contenuto in AEM, come `/var/portlets`. In questo caso, uno script in esecuzione in AEM può utilizzare le informazioni inviate dal portlet per decidere quale url è l’URL iniziale. Dovrebbe emettere un reindirizzamento all&#39;URL corretto.

#### Aggiunta del portlet alla pagina del portale {#adding-the-portlet-to-the-portal-page}

Per aggiungere il portlet alla pagina del portale:

1. Accertati di essere nella finestra di amministrazione dell’app server e passa alla posizione in cui gestisci le pagine. (ad esempio, in WebSphere 6.1, fai clic su **Gestire le pagine**).
1. Seleziona il nome del portlet, quindi seleziona una pagina esistente o creane una nuova.
1. Modifica il layout della pagina.
1. Seleziona il portlet e aggiungilo a un contenitore.
1. Salva le modifiche.

#### Utilizzo del portlet {#using-the-portlet}

Per accedere alla pagina aggiunta al portlet:

1. Nel menu di personalizzazione del portlet, configura il portlet come lo hai configurato nel portale.
1. Apri la configurazione (il portlet visualizza l’URL di inizio pubblicazione configurato nella configurazione del portlet) e apporta le modifiche necessarie, quindi salvalo.
