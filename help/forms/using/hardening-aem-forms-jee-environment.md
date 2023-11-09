---
title: Rafforzamento dell’ambiente AEM Forms su JEE
description: Scopri diverse impostazioni per rafforzare la sicurezza di AEM Forms su JEE in esecuzione in una Intranet aziendale.
content-type: reference
topic-tags: Security
products: SG_EXPERIENCEMANAGER/6.4
role: Admin
exl-id: 6fb260f9-d0f8-431e-8d4e-535b451e4124
source-git-commit: 451fb472e170a79f9854efadf9be1d4fe0628b94
workflow-type: tm+mt
source-wordcount: '7662'
ht-degree: 1%

---

# Rafforzamento dell’ambiente AEM Forms su JEE {#hardening-your-aem-forms-on-jee-environment}

Scopri diverse impostazioni per rafforzare la sicurezza di AEM Forms su JEE in esecuzione in una Intranet aziendale.

L’articolo descrive raccomandazioni e best practice per la protezione dei server che eseguono AEM Forms su JEE. Non si tratta di un documento completo di protezione avanzata dell&#39;host per il sistema operativo e i server delle applicazioni. In questo articolo vengono invece descritte diverse impostazioni che è necessario implementare per migliorare la sicurezza di AEM Forms su JEE in esecuzione in una Intranet aziendale. Tuttavia, per garantire la sicurezza dell’AEM Forms sui server applicazioni JEE, è necessario implementare anche procedure di monitoraggio, rilevamento e risposta di sicurezza.

L&#39;articolo descrive le tecniche di tempra da applicare durante le seguenti fasi del ciclo di vita dell&#39;installazione e della configurazione:

* **Pre-installazione:** Utilizza queste tecniche prima di installare AEM Forms su JEE.
* **Installazione:** Utilizza queste tecniche durante il processo di installazione di AEM Forms su JEE.
* **Post-installazione:** Utilizzare queste tecniche dopo l&#39;installazione e in seguito periodicamente.

AEM Forms su JEE è altamente personalizzabile e può funzionare in molti ambienti diversi. Alcuni consigli potrebbero non soddisfare le esigenze della tua organizzazione.

## Preinstallazione {#preinstallation}

Prima di installare AEM Forms su JEE , è possibile applicare soluzioni di sicurezza al livello di rete e al sistema operativo. Questa sezione descrive alcuni problemi e formula raccomandazioni per ridurre le vulnerabilità di sicurezza in queste aree.

**Installazione e configurazione su UNIX e Linux**

Non installare o configurare AEM Forms su JEE utilizzando una shell radice. Per impostazione predefinita, i file vengono installati nella directory /opt e l&#39;utente che esegue l&#39;installazione deve disporre di tutte le autorizzazioni per i file in /opt. In alternativa, è possibile eseguire un&#39;installazione nella directory /user di un singolo utente in cui sono già disponibili tutte le autorizzazioni per i file.

**Installazione e configurazione in Windows**

Se stai installando AEM Forms su JEE su JBoss utilizzando il metodo turnkey o se stai installando PDF Generator, è necessario eseguire l’installazione su Windows come amministratore. Inoltre, quando si installa PDF Generator su Windows con il supporto nativo dell&#39;applicazione, è necessario eseguire l&#39;installazione come lo stesso utente di Windows che ha installato Microsoft Office. Per ulteriori informazioni sui privilegi di installazione, consulta il documento Installazione e distribuzione di AEM Forms su JEE* per il server applicazioni.

### Protezione a livello di rete {#network-layer-security}

Le vulnerabilità relative alla sicurezza di rete sono tra le prime minacce per qualsiasi server applicazioni che si affaccia su Internet o su Intranet. Questa sezione descrive il processo di protezione degli host della rete da queste vulnerabilità. Affronta la segmentazione della rete, l&#39;irrigidimento dello stack TCP/IP (Transmission Control Protocol/Internet Protocol) e l&#39;uso di firewall per la protezione dell&#39;host.

Nella tabella seguente vengono descritti i processi comuni che riducono le vulnerabilità relative alla sicurezza della rete.

<table> 
 <thead> 
  <tr> 
   <th><p>Problema  </p> </th> 
   <th><p>Descrizione</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>Zone demilitarizzate (DMZ)</p> </td> 
   <td><p>Distribuire i server Forms all'interno di una zona demilitarizzata (DMZ). La segmentazione deve esistere in almeno due livelli con il server applicazioni utilizzato per eseguire AEM Forms su JEE posizionato dietro il firewall interno. Separare la rete esterna dalla DMZ che contiene i server web, che a sua volta deve essere separata dalla rete interna. Utilizzate i firewall per implementare i livelli di separazione. Categorizza e controlla il traffico che attraversa ogni livello di rete per garantire che sia consentito solo il minimo assoluto di dati richiesti.</p> </td> 
  </tr> 
  <tr> 
   <td><p>Indirizzi IP privati</p> </td> 
   <td><p>Utilizza Network Address Translation (NAT) con indirizzi IP privati RFC 1918 sul server applicazioni AEM Forms. Assegna indirizzi IP privati (10.0.0.0/8, 172.16.0.0/12 e 192.168.0.0/16) per rendere più difficile per un utente malintenzionato indirizzare il traffico da e verso un host interno NAT attraverso Internet.</p> </td> 
  </tr> 
  <tr> 
   <td><p>Firewall</p> </td> 
   <td><p>Utilizzare i criteri seguenti per selezionare una soluzione firewall:</p> 
    <ul> 
     <li><p>Implementare firewall che supportano server proxy e/o <em>ispezione di stato</em> anziché soluzioni semplici per il filtraggio dei pacchetti.</p> </li> 
     <li><p>Utilizzare un firewall che supporti <em>rifiuta tutti i servizi eccetto quelli esplicitamente consentiti</em> i paradigmi di sicurezza.</p> </li> 
     <li><p>Implementare una soluzione firewall con doppia o multihomed. Questa architettura offre il massimo livello di protezione e consente di evitare che utenti non autorizzati aggirino la protezione del firewall.</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>Porte del database</p> </td> 
   <td><p>Non utilizzare porte di ascolto predefinite per i database (MySQL - 3306, Oracle - 1521, MS SQL - 1433). Per informazioni sulla modifica delle porte del database, vedere la documentazione del database.</p> <p>L’utilizzo di una porta di database diversa influisce sulla configurazione complessiva di AEM Forms su JEE. Se modifichi le porte predefinite, devi apportare le modifiche corrispondenti in altre aree di configurazione, ad esempio le origini dati per AEM Forms su JEE.</p> <p>Per informazioni sulla configurazione delle origini dati in AEM Forms su JEE, consulta Installare e aggiornare AEM Forms su JEE o Aggiornare ad AEM Forms su JEE per il server applicazioni all’indirizzo <a href="/help/forms/using/introduction-aem-forms.md" target="_blank">Guida utente di AEM Forms</a>.</p> </td> 
  </tr> 
 </tbody> 
</table>

### Sicurezza del sistema operativo {#operating-system-security}

Nella tabella seguente vengono descritti alcuni approcci potenziali per ridurre al minimo le vulnerabilità di sicurezza rilevate nel sistema operativo.

<table> 
 <thead> 
  <tr> 
   <th><p>Problema  </p></th> 
   <th><p>Descrizione</p></th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>Patch di sicurezza</p></td> 
   <td><p>Esiste un rischio maggiore che un utente non autorizzato possa accedere all'Application Server se le patch e gli aggiornamenti di sicurezza del fornitore non vengono applicati in modo tempestivo. Verificare le patch di sicurezza prima di applicarle ai server di produzione.</p><p>È inoltre possibile creare criteri e procedure per verificare e installare regolarmente le patch.</p></td> 
  </tr> 
  <tr> 
   <td><p>Software antivirus</p></td> 
   <td><p>Gli scanner antivirus possono identificare i file infetti eseguendo la scansione alla ricerca di una firma o osservando un comportamento insolito. Gli scanner conservano le firme dei virus in un file, in genere memorizzato sul disco rigido locale. Poiché i nuovi virus vengono individuati spesso, è consigliabile aggiornare di frequente questo file per consentire al programma antivirus di identificare tutti i virus correnti.</p></td> 
  </tr> 
  <tr> 
   <td><p>NTP (Network Time Protocol)</p></td> 
   <td><p>Per l’analisi forense, assicurati di disporre di tempo preciso sui server dei moduli. Utilizzare NTP per sincronizzare l'ora su tutti i sistemi connessi direttamente a Internet.</p></td> 
  </tr> 
 </tbody> 
</table>

Per ulteriori informazioni sulla sicurezza del sistema operativo in uso, vedere [&quot;Informazioni sulla sicurezza del sistema operativo&quot;](https://helpx.adobe.com/aem-forms/6-1/hardening-security/general-security-considerations.html#operating_system_security_information).

## Installazione {#installation}

Questa sezione descrive le tecniche che puoi utilizzare durante il processo di installazione di AEM Forms per ridurre le vulnerabilità relative alla sicurezza. In alcuni casi, queste tecniche utilizzano le opzioni che fanno parte del processo di installazione. Nella tabella seguente vengono descritte queste tecniche.

<table> 
 <thead> 
  <tr> 
   <th><p>Problema  </p> </th> 
   <th><p>Descrizione</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>Privilegi</p> </td> 
   <td><p>Utilizzare il minor numero di privilegi necessari per installare il software. Accedere al computer utilizzando un account non incluso nel gruppo Administrators. In Windows è possibile utilizzare il comando Esegui come per eseguire il programma di installazione di AEM Forms su JEE come utente amministrativo. Nei sistemi UNIX e Linux, utilizzare un comando quale <code>sudo</code> per installare il software.</p> </td> 
  </tr> 
  <tr> 
   <td><p>Origine software</p> </td> 
   <td><p>Non scaricare o eseguire AEM Forms su JEE da origini non attendibili.</p> <p>I programmi dannosi possono contenere codice per violare la sicurezza in diversi modi, tra cui il furto di dati, la modifica e l'eliminazione e la negazione del servizio. Installa AEM Forms su JEE dal DVD di Adobe o solo da una fonte attendibile.</p> </td> 
  </tr> 
  <tr> 
   <td><p>Partizioni disco</p> </td> 
   <td><p>Posizionare AEM Forms su JEE in una partizione disco dedicata. La segmentazione del disco è un processo che mantiene dati specifici sul server su dischi fisici separati per una maggiore sicurezza. Questo tipo di disposizione dei dati riduce il rischio di attacchi di attraversamento delle directory. Pianifica la creazione di una partizione separata dalla partizione di sistema in cui è possibile installare la directory di contenuto AEM Forms su JEE. In Windows, la partizione di sistema contiene la directory system32 o la partizione di avvio.</p> </td> 
  </tr> 
  <tr> 
   <td><p>Componenti</p> </td> 
   <td><p>Valuta i servizi esistenti e disattiva o disinstalla quelli non necessari. Non installare componenti e servizi non necessari.</p> <p>L'installazione predefinita di un server applicazioni potrebbe includere servizi non necessari per l'utilizzo. Prima della distribuzione, è necessario disabilitare tutti i servizi non necessari per ridurre al minimo i punti di ingresso per un attacco. Ad esempio, in JBoss, puoi aggiungere un commento ai servizi non necessari nel file descrittore META-INF/jboss-service.xml.</p> </td> 
  </tr> 
  <tr> 
   <td><p>File di criteri tra domini</p> </td> 
   <td><p>La presenza di un <code>crossdomain.xml</code> sul server potrebbe indebolirlo immediatamente. È consigliabile creare l’elenco dei domini nel modo più restrittivo possibile. Non posizionare <code>crossdomain.xml</code> file utilizzato durante lo sviluppo in produzione durante l'utilizzo delle guide <em>(obsoleto)</em>. Per una guida che utilizza i servizi web, se il servizio si trova sullo stesso server su cui è stata distribuita la guida, viene visualizzata una <code>crossdomain.xml</code> non è necessario. Tuttavia, se il servizio si trova su un altro server o se sono coinvolti cluster, la presenza di un <code>crossdomain.xml</code> il file è necessario. Fai riferimento a <a href="https://kb2.adobe.com/cps/142/tn_14213.html">https://kb2.adobe.com/cps/142/tn_14213.html</a>, per ulteriori informazioni sul file crossdomain.xml.</p> </td> 
  </tr> 
  <tr> 
   <td><p>Impostazioni di protezione del sistema operativo</p> </td> 
   <td><p>Se è necessario utilizzare la crittografia XML a 192 bit o a 256 bit sulle piattaforme Solaris, assicurarsi di installare <code>pkcs11_softtoken_extra.so</code> invece di <code>pkcs11_softtoken.so</code>.</p> </td> 
  </tr> 
 </tbody> 
</table>

## Passaggi successivi all’installazione {#post-installation-steps}

Dopo aver installato correttamente AEM Forms su JEE, è importante mantenere periodicamente l’ambiente dal punto di vista della sicurezza.

Nella sezione seguente vengono descritte in dettaglio le diverse attività consigliate per proteggere il server Forms distribuito.

### Sicurezza di AEM Forms {#aem-forms-security}

Le seguenti impostazioni consigliate si applicano al server AEM Forms su JEE all’esterno dell’applicazione web amministrativa. Per ridurre i rischi per la sicurezza del server, applica queste impostazioni immediatamente dopo l’installazione di AEM Forms su JEE.

**Patch di sicurezza**

Esiste un rischio maggiore che un utente non autorizzato possa accedere all&#39;Application Server se le patch e gli aggiornamenti di sicurezza del fornitore non vengono applicati in modo tempestivo. Verificare le patch di sicurezza prima di applicarle ai server di produzione per garantire la compatibilità e la disponibilità delle applicazioni. È inoltre possibile creare criteri e procedure per verificare e installare regolarmente le patch. Gli aggiornamenti di AEM Forms su JEE sono disponibili sul sito di download dei prodotti Enterprise.

**Account di servizio (JBoss turnkey solo su Windows)**

Per impostazione predefinita, AEM Forms su JEE installa un servizio utilizzando l’account LocalSystem. L&#39;account utente LocalSystem incorporato dispone di un livello elevato di accessibilità e fa parte del gruppo Administrators. Se un&#39;identità del processo di lavoro viene eseguita come account utente LocalSystem, tale processo di lavoro dispone dell&#39;accesso completo all&#39;intero sistema.

Per eseguire l’application server in cui viene distribuito AEM Forms su JEE, utilizzando un account non amministrativo specifico, segui queste istruzioni:

1. In Microsoft Management Console (MMC), creare un utente locale per il servizio Forms Server per l&#39;accesso come:

   * Seleziona **L&#39;utente non può cambiare la password**.
   * Il giorno **Membro di** , assicurati che il **Utenti** è elencato.

   >[!NOTE]
   >
   >Non è possibile modificare questa impostazione per PDF Generator.

1. Seleziona **Inizio** > **Impostazioni** > **Strumenti di amministrazione** > **Servizi**.
1. Fai doppio clic su JBoss per AEM Forms su JEE e arresta il servizio.
1. Il giorno **Accedi** , seleziona **Questo account**, individua l&#39;account utente creato e immetti la password per l&#39;account.
1. In MMC aprire **Impostazioni di protezione locali** e seleziona **Criteri locali** > **Assegnazione diritti utente**.
1. Assegnare i seguenti diritti all&#39;account utente in cui è in esecuzione Forms Server:

   * Nega accesso tramite Servizi terminal
   * Nega accesso locale
   * Accedi come servizio (dovrebbe essere già impostato)

1. Concedi al nuovo account utente le autorizzazioni di modifica per le seguenti directory:
   * **Directory Global Document Storage (GDS)**: la posizione della directory GDS viene configurata manualmente durante il processo di installazione di AEM Forms. Se l&#39;impostazione relativa al percorso rimane vuota durante l&#39;installazione, per impostazione predefinita viene utilizzata una directory nell&#39;installazione del server applicazioni in `[JBoss root]/server/[type]/svcnative/DocumentStorage`
   * **Directory CRX-Repository**: la posizione predefinita è `[AEM-Forms-installation-location]\crx-repository`
   * **Directory temporanee di AEM Forms**:
      * (Windows) Percorso TMP o TEMP impostato nelle variabili di ambiente
      * (AIX, Linux o Solaris) Directory principale dell&#39;utente connesso Nei sistemi basati su UNIX, un utente non root può utilizzare la seguente directory come directory temporanea:
      * (Linux) /var/tmp o /usr/tmp
      * (AIX) /tmp o /usr/tmp
      * (Solaris) /var/tmp o /usr/tmp
1. Assegna al nuovo account utente le autorizzazioni di scrittura per le directory seguenti:
   * [JBoss-directory]\standalone\distribuzione
   * [JBoss-directory]\standalone\
   * [JBoss-directory]\bin\

   >[!NOTE]
   >
   >Percorso di installazione predefinito del server applicazioni JBoss:
   >
   >* Windows: C:\Adobe\Adobe_Experience_Manager_Forms\jboss
   >* Linux: /opt/jboss/

1. Avviare il server applicazioni.

**Disabilitazione del servlet di avvio di Configuration Manager**

Configuration Manager ha utilizzato un servlet distribuito sul server applicazioni per eseguire l’avvio automatico del database AEM Forms su JEE. Poiché Configuration Manager accede a questo servlet prima del completamento della configurazione, l’accesso non è stato protetto per gli utenti autorizzati e dovrebbe essere disattivato dopo che l’utente ha utilizzato Configuration Manager per configurare AEM Forms su JEE.

1. Decomprimi il ciclo di vita di adobe[appserver]file .ear.
1. Apri il file META-INF/application.xml.
1. Cerca la sezione adobe-bootstrapper.war:

   ```java
   <!-- bootstrapper start --> 
   <module id="WebApp_adobe_bootstrapper"> 
       <web> 
           <web-uri>adobe-bootstrapper.war</web-uri> 
           <context-root>/adobe-bootstrapper</context-root> 
       </web> 
   </module> 
   <module id="WebApp_adobe_lcm_bootstrapper_redirector"> 
       <web> 
           <web-uri>adobe-lcm-bootstrapper-redirector.war</web-uri> 
           <context-root>/adobe-lcm-bootstrapper</context-root> 
       </web> 
   </module> 
   <!-- bootstrapper end-->
   ```

1. Arresta il server AEM Forms.
1. Commenta adobe-bootstrapper.war e adobe-lcm-bootstrapper-redirectory. moduli guerra come segue:

   ```java
   <!-- bootstrapper start --> 
   <!-- 
   <module id="WebApp_adobe_bootstrapper"> 
       <web> 
           <web-uri>adobe-bootstrapper.war</web-uri> 
           <context-root>/adobe-bootstrapper</context-root> 
       </web> 
   </module> 
   <module id="WebApp_adobe_lcm_bootstrapper_redirector"> 
       <web> 
           <web-uri>adobe-lcm-bootstrapper-redirector.war</web-uri> 
           <context-root>/adobe-lcm-bootstrapper</context-root> 
       </web> 
   </module> 
   --> 
   <!-- bootstrapper end-->
   ```

1. Salvare e chiudere il file META-INF/application.xml.
1. Comprimere il file EAR e ridistribuirlo sul server applicazioni.
1. Avvia il server AEM Forms.
1. Digita l’URL seguente in un browser per verificare la modifica e assicurarti che non funzioni più.

   https://&lt;localhost>:&lt;port>/adobe-bootstrapper/bootstrap

**Blocca accesso remoto all&#39;archivio fonti attendibili**

Configuration Manager consente di caricare una credenziale di estensioni Acrobat Reader DC nell’archivio fonti attendibili di AEM Forms su JEE. L&#39;accesso al servizio credenziali dell&#39;archivio fonti attendibili tramite protocolli remoti (SOAP ed EJB) è stato abilitato per impostazione predefinita. Questo accesso non è più necessario dopo che hai caricato le credenziali dei diritti tramite Configuration Manager o se decidi di utilizzare la console di amministrazione in un secondo momento per gestire le credenziali.

Per disabilitare l&#39;accesso remoto a tutti i servizi dell&#39;archivio fonti attendibili, seguire la procedura descritta nella sezione [Disattivazione dell&#39;accesso remoto non essenziale ai servizi](https://helpx.adobe.com/aem-forms/6-1/hardening-security/configuring-secure-administration-settings-aem.html#disabling_non_essential_remote_access_to_services).

**Disattiva tutti gli accessi anonimi non essenziali**

Alcuni servizi di Forms Server dispongono di operazioni che possono essere richiamate da un chiamante anonimo. Se non è necessario l’accesso anonimo a questi servizi, disattivalo seguendo i passaggi descritti in [Disabilitazione dell’accesso anonimo non essenziale ai servizi](https://helpx.adobe.com/aem-forms/6-1/hardening-security/configuring-secure-administration-settings-aem.html#disabling_non_essential_anonymous_access_to_services).

#### Modificare la password predefinita dell&#39;amministratore {#change-the-default-administrator-password}

Quando si installa AEM Forms su JEE, per l’utente amministratore privilegiato/login-id viene configurato un singolo account utente predefinito con una password predefinita di *password*. È necessario modificare immediatamente la password utilizzando Configuration Manager.

1. Digita il seguente URL in un browser web:

   ```java
   https://[host name]:[port]/adminui
   ```

   Il numero di porta predefinito è uno dei seguenti:

   **JBoss:** 8080

   **Server WebLogic:** 7001

   **WebSphere:** 9080.

1. In **Nome utente** campo, tipo `administrator` e, nella **Password** campo, tipo `password`.
1. Clic **Impostazioni** > **Gestione utente** > **Utenti e gruppi**.
1. Tipo `administrator` nel **Trova** e fai clic su **Trova**.
1. Clic **Amministratore privilegiato** dall’elenco degli utenti.
1. Clic **Cambia password** nella pagina Modifica utente.
1. Specifica la nuova password e fai clic su **Salva**.

Inoltre, si consiglia di modificare la password predefinita per l’amministratore CRX eseguendo i seguenti passaggi:

1. Accedi a `https://[server]:[port]/lc/libs/granite/security/content/useradmin.html` utilizzando il nome utente/password predefinito.
1. Digitare Administrator nel campo di ricerca e fare clic su **Vai**.
1. Seleziona **Amministratore** dal risultato della ricerca e fare clic sul pulsante **Modifica** in basso a destra nell’interfaccia utente.
1. Specifica la nuova password in **Nuova password** e la vecchia password in **Password** campo.
1. Fai clic sull’icona Salva in basso a destra nell’interfaccia utente.

#### Disattiva generazione WSDL {#disable-wsdl-generation}

La generazione WSDL (Web Service Definition Language) deve essere abilitata solo per gli ambienti di sviluppo in cui la generazione WSDL viene utilizzata dagli sviluppatori per creare le applicazioni client. Puoi scegliere di disabilitare la generazione WSDL in un ambiente di produzione per evitare di esporre i dettagli interni di un servizio.

1. Digita il seguente URL in un browser web:

   ```java
   https://[host name]:[port]/adminui
   ```

1. Seleziona **Settings (Impostazioni) > Core System Settings (Impostazioni sistema core) > Configurations (Configurazioni)**.
1. Deseleziona **Abilita WSDL**, quindi seleziona **OK**.

### Protezione del server applicazioni {#application-server-security}

Nella tabella seguente vengono descritte alcune tecniche per proteggere il server applicazioni dopo l’installazione dell’applicazione AEM Forms su JEE.

<table> 
 <thead> 
  <tr> 
   <th><p>Problema  </p> </th> 
   <th><p>Descrizione</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>Console di amministrazione del server applicazioni</p> </td> 
   <td><p>Dopo aver installato, configurato e implementato AEM Forms su JEE nel server applicazioni, è necessario disabilitare l’accesso alle console di amministrazione del server applicazioni. Per informazioni dettagliate, consulta la documentazione del server applicazioni.</p> </td> 
  </tr> 
  <tr> 
   <td><p>Impostazioni dei cookie del server applicazioni</p> </td> 
   <td><p>I cookie dell’applicazione sono controllati dal server dell’applicazione. Durante la distribuzione dell'applicazione, l'amministratore del server applicazioni può specificare le preferenze dei cookie a livello di server o di applicazione. Per impostazione predefinita, le impostazioni del server hanno la precedenza.</p> <p>Tutti i cookie di sessione generati dal server applicazioni devono includere <code>HttpOnly</code> attributo. Ad esempio, quando si utilizza il server applicazioni JBoss, è possibile modificare l’elemento SessionCookie in <code>httpOnly="true"</code> nel <code>WEB-INF/web.xml</code> file.</p> <p>Puoi limitare l’invio dei cookie utilizzando solo HTTPS. Di conseguenza, non vengono inviate non crittografate tramite HTTP. Gli amministratori del server applicazioni devono abilitare i cookie protetti per il server su base globale. Ad esempio, quando si utilizza il server applicazioni JBoss, è possibile modificare l’elemento connettore in <code>secure=true</code> nel <code>server.xml</code> file.</p> <p>Per ulteriori informazioni sulle impostazioni dei cookie, consulta la documentazione del server applicazioni.</p> </td> 
  </tr> 
  <tr> 
   <td><p>Esplorazione directory</p> </td> 
   <td><p>Quando qualcuno richiede una pagina che non esiste o il nome di un director (la stringa di richiesta termina con una barra (/)), il server applicazioni non deve restituire il contenuto di quella directory. Per evitare questo problema, è possibile disabilitare la navigazione nelle directory sul server applicazioni. Questa operazione deve essere eseguita per l'applicazione console di amministrazione e per altre applicazioni in esecuzione sul server.</p> <p>Per JBoss, imposta il valore del parametro di inizializzazione delle inserzioni di <code>DefaultServlet</code> proprietà a <code>false</code> nel file web.xml, come illustrato in questo esempio:</p> <p>&lt;servlet&gt;</p> <p>&lt;servlet-name&gt;predefinito&lt;/servlet-name&gt;</p> <p>&lt;servlet-class&gt;</p> <p>org.apache.catalina.servlets.DefaultServlet</p> <p>&lt;/servlet-class&gt;</p> <p>&lt;init-param&gt;</p> <p>&lt;param-name&gt;inserzioni&lt;/param-name&gt;</p> <p>&lt;param-value&gt;false&lt;/param-value&gt;</p> <p>&lt;/init-param&gt;</p> <p>&lt;load-on-startup&gt;1&lt;/load-on-startup&gt;</p> <p>&lt;/servlet&gt;</p> <p>Per WebSphere, impostare <code>directoryBrowsingEnabled</code> nel file ibm-web-ext.xmi a <code>false</code>.</p> <p>Per WebLogic, impostare le proprietà delle directory indice nel file weblogic.xml su <code>false</code>, come mostrato in questo esempio:</p> <p>&lt;container-descriptor&gt;</p> <p>&lt;index-directory-enabled&gt;false</p> <p>&lt;/index-directory-enabled&gt;</p> <p>&lt;/container-descriptor&gt;</p> </td> 
  </tr> 
 </tbody> 
</table>

### Sicurezza del database {#database-security}

Quando si protegge il database, è necessario implementare le misure descritte dal fornitore del database. È necessario allocare un utente del database con le autorizzazioni minime richieste concesse per l’utilizzo da parte di AEM Forms su JEE. Ad esempio, non utilizzare un account con privilegi di amministratore del database.

Ad Oracle, l&#39;account di database utilizzato richiede solo i privilegi CONNECT, RESOURCE e CREATE VIEW. Per requisiti simili per altri database, vedere [Preparazione all’installazione di AEM Forms su JEE (server singolo)](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_64).

#### Configurazione della sicurezza integrata per SQL Server su Windows per JBoss {#configuring-integrated-security-for-sql-server-on-windows-for-jboss}

1. Modifica [JBOSS_HOME]\\standalone\configuration\lc_{datasource.xml} da aggiungere `integratedSecurity=true` all’URL di connessione, come illustrato in questo esempio:

   ```java
    jdbc:sqlserver://<serverhost>:<port>;databaseName=<dbname>;integratedSecurity=true
   ```

1. Aggiungere il file sqljdbc_auth.dll al percorso del sistema Windows nel computer che esegue il server applicazioni. Il file sqljdbc_auth.dll si trova con l&#39;installazione del driver Microsoft SQL JDBC 6.2.1.0.
1. Modificare la proprietà del servizio JBoss di Windows (JBoss for AEM Forms on JEE) per Accedi come dal sistema locale in un account di accesso con database AEM Forms e un set minimo di privilegi. Se si esegue JBoss dalla riga di comando anziché come servizio Windows, non è necessario eseguire questo passaggio.
1. Imposta protezione per SQL Server da **Misto** modalità a **Solo autenticazione di Windows**.

#### Configurazione della sicurezza integrata per SQL Server su Windows per WebLogic {#configuring-integrated-security-for-sql-server-on-windows-for-weblogic}

1. Avviare la console di amministrazione del server WebLogic digitando il seguente URL nella riga URL di un browser Web:

   ```java
   https://[host name]:7001/console
   ```

1. In Cambia centro fare clic su **Blocca e modifica**.
1. In Struttura dominio, fai clic su *[dominio_base]* > **Servizi** > **JDBC** > **Origini dati** e, nel riquadro di destra, fai clic su **IDP_DS**.
1. Nella schermata successiva, sul **Configurazione** , fare clic sulla scheda **Pool di connessioni** e, nella scheda **Proprietà** casella, digitare `integratedSecurity=true`.
1. In Struttura dominio, fai clic su **[dominio_base]** > **Servizi** > **JDBC** > **Origini dati** e, nel riquadro di destra, fai clic su **RM_DS**.
1. Nella schermata successiva, sul **Configurazione** , fare clic sulla scheda **Pool di connessioni** e, nella scheda **Proprietà** casella, digitare `integratedSecurity=true`.
1. Aggiungere il file sqljdbc_auth.dll al percorso del sistema Windows nel computer che esegue il server applicazioni. Il file sqljdbc_auth.dll si trova con l&#39;installazione del driver Microsoft SQL JDBC 6.2.1.0.
1. Imposta protezione per SQL Server da **Misto** modalità a **Solo autenticazione di Windows**.

#### Configurazione della sicurezza integrata per SQL Server su Windows per WebSphere {#configuring-integrated-security-for-sql-server-on-windows-for-websphere}

In WebSphere è possibile configurare la protezione integrata solo quando si utilizza un driver JDBC esterno di SQL Server e non il driver JDBC di SQL Server incorporato con WebSphere.

1. Accedere a WebSphere Administrative Console.
1. Nella struttura di navigazione, fai clic su **Risorse** > **JDBC** > **Origini dati** e, nel riquadro di destra, fai clic su **IDP_DS**.
1. Nel riquadro di destra, in Proprietà aggiuntive, fare clic su **Proprietà personalizzate** e quindi fare clic su **Nuovo**.
1. In **Nome** casella, digitare `integratedSecurity` e, nella **Valore** casella, digitare `true`.
1. Nella struttura di navigazione, fai clic su **Risorse** > **JDBC** > **Origini dati** e, nel riquadro di destra, fai clic su **RM_DS**.
1. Nel riquadro di destra, in Proprietà aggiuntive, fare clic su **Proprietà personalizzate** e quindi fare clic su **Nuovo**.
1. In **Nome** casella, digitare `integratedSecurity` e, nella **Valore** casella, digitare `true`.
1. Nel computer in cui è installato WebSphere, aggiungere il file sqljdbc_auth.dll al percorso del sistema Windows (C:\Windows). Il file sqljdbc_auth.dll si trova nella stessa posizione dell&#39;installazione del driver Microsoft SQL JDBC 1.2 (il valore predefinito è *[InstallDir]*/sqljdbc_1.2/enu/auth/x86).
1. Seleziona **Inizio** > **Pannello di controllo Campaign** > **Servizi**, fare clic con il pulsante destro del mouse sul servizio Windows per WebSphere (IBM WebSphere Application Server) &lt;version> - &lt;node>) e seleziona **Proprietà**.
1. Nella finestra di dialogo Proprietà fare clic su **Accedi** scheda.
1. Seleziona **Questo account** e fornire le informazioni necessarie per impostare l&#39;account di accesso che si desidera utilizzare.
1. Imposta protezione su SQL Server da **Misto** modalità a **Solo autenticazione di Windows**.

### Protezione dell&#39;accesso a contenuto riservato nel database {#protecting-access-to-sensitive-content-in-the-database}

Lo schema del database AEM Forms contiene informazioni riservate sulla configurazione del sistema e sui processi aziendali e deve essere nascosto dietro il firewall. Il database deve essere considerato all&#39;interno dello stesso limite di attendibilità del server Forms. Per evitare la divulgazione delle informazioni e il furto dei dati aziendali, il database deve essere configurato dall&#39;amministratore del database (DBA) in modo da consentire l&#39;accesso solo agli amministratori autorizzati.

Come ulteriore precauzione, è consigliabile utilizzare strumenti specifici del fornitore del database per crittografare le colonne nelle tabelle che contengono i dati seguenti:

* Chiavi documento Rights Management
* Chiave di crittografia PIN HSM dell&#39;archivio fonti attendibili
* Hash password utente locale

Per informazioni sugli strumenti specifici del fornitore, consulta [&quot;Informazioni sulla sicurezza del database&quot;](https://helpx.adobe.com/aem-forms/6-1/hardening-security/general-security-considerations.html#database_security_information).

### Protezione LDAP {#ldap-security}

Una directory LDAP (Lightweight Directory Access Protocol) viene in genere utilizzata da AEM Forms su JEE come origine per le informazioni di utenti e gruppi aziendali e come mezzo per eseguire l’autenticazione tramite password. È necessario verificare che la directory LDAP sia configurata per l’utilizzo di Secure Socket Layer (SSL) e che AEM Forms su JEE sia configurato per l’accesso alla directory LDAP tramite la relativa porta SSL.

#### Denial of Service LDAP {#ldap-denial-of-service}

Un attacco comune che utilizza LDAP implica che un utente malintenzionato non riesca deliberatamente ad autenticarsi più volte. In questo modo il server di elenchi in linea LDAP blocca un utente da tutti i servizi basati su LDAP.

Puoi impostare il numero di tentativi di errore e il successivo tempo di blocco implementato da AEM Forms quando un utente non riesce a eseguire ripetutamente l’autenticazione in AEM Forms. Nella console di amministrazione, scegli valori bassi. Quando si seleziona il numero di tentativi non riusciti, è importante comprendere che dopo tutti i tentativi, AEM Forms blocca l’utente prima che il server di elenchi in linea LDAP lo faccia.

#### Imposta blocco automatico account {#set-automatic-account-locking}

1. Accedere alla console di amministrazione.
1. Clic **Impostazioni** > **Gestione utente** > **Gestione del dominio**.
1. In Impostazioni blocco account automatico, impostare **Numero massimo di errori di autenticazione consecutivi** a un numero basso, ad esempio 3.
1. Fai clic su **Salva**.

### Controllo e registrazione {#auditing-and-logging}

L&#39;utilizzo corretto e sicuro del controllo e della registrazione delle applicazioni può contribuire a garantire che la sicurezza e altri eventi anomali vengano monitorati e rilevati il più rapidamente possibile. L&#39;utilizzo efficace del controllo e della registrazione all&#39;interno di un&#39;applicazione include elementi quali il tracciamento degli accessi riusciti e non riusciti e gli eventi chiave dell&#39;applicazione, ad esempio la creazione o l&#39;eliminazione di record chiave.

Puoi utilizzare il controllo per rilevare molti tipi di attacchi, tra cui:

* Attacchi brutali forzati con password
* Attacchi Denial of Service
* Iniezione di input ostili e classi correlate di attacchi di scripting

Questa tabella descrive le tecniche di controllo e registrazione che è possibile utilizzare per ridurre le vulnerabilità del server.

<table> 
 <thead> 
  <tr> 
   <th><p>Problema  </p> </th> 
   <th><p>Descrizione</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>ACL file di registro</p> </td> 
   <td><p>Imposta AEM Forms appropriato sugli elenchi di controllo di accesso (ACL) dei file di registro JEE.</p> <p>L'impostazione delle credenziali appropriate consente di impedire agli autori di attacchi di eliminare i file.</p> <p>Le autorizzazioni di protezione nella directory dei file di registro devono essere Controllo completo per gli amministratori e i gruppi SYSTEM. L’account utente di AEM Forms deve disporre solo delle autorizzazioni di lettura e scrittura.</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ridondanza dei file di registro</p> </td> 
   <td><p>Se le risorse lo consentono, inviare i registri a un altro server in tempo reale che non sia accessibile all'autore dell'attacco (solo scrittura) utilizzando Syslog, Tivoli, Microsoft Operations Manager (MOM) Server o un altro meccanismo.</p> <p>Proteggere i registri in questo modo aiuta a evitare manomissioni. Inoltre, l’archiviazione dei registri in un archivio centrale facilita la correlazione e il monitoraggio (ad esempio, se sono in uso più server forms e viene eseguito un attacco di ricerca delle password in più computer in cui viene richiesta una password a ciascun computer).</p> </td> 
  </tr> 
 </tbody> 
</table>

### Consenti a un utente non amministratore di eseguire PDF Generator

È possibile abilitare un utente non amministratore all&#39;utilizzo di PDF Generator. Normalmente, solo gli utenti con privilegi amministrativi possono utilizzare PDF Generator. Per consentire a un utente non amministratore di eseguire PDF Generator, effettuare le seguenti operazioni:

1. Creare una variabile di ambiente denominata PDFG_NON_ADMIN_ENABLED.

1. Imposta il valore della variabile su TRUE.

1. Riavvia l’istanza di AEM Forms.

## Configurazione di AEM Forms su JEE per l’accesso oltre i confini dell’azienda {#configuring-aem-forms-on-jee-for-access-beyond-the-enterprise}

Dopo aver installato correttamente AEM Forms su JEE, è importante mantenere periodicamente la sicurezza dell’ambiente. Questa sezione descrive le attività consigliate per mantenere la sicurezza dell’AEM Forms sul server di produzione JEE.

### Impostazione di un proxy inverso per l&#39;accesso Web {#setting-up-a-reverse-proxy-for-web-access}

A *proxy inverso* può essere utilizzato per garantire che un set di URL per le applicazioni web AEM Forms su JEE sia disponibile per gli utenti interni ed esterni. Questa configurazione è più sicura di quella che consente agli utenti di connettersi direttamente al server applicazioni su cui è in esecuzione AEM Forms on JEE. Il proxy inverso esegue tutte le richieste HTTP per il server applicazioni che esegue AEM Forms su JEE. Gli utenti dispongono solo dell&#39;accesso di rete al proxy inverso e possono solo tentare connessioni URL supportate dal proxy inverso.

**AEM Forms sugli URL principali di JEE da utilizzare con il server proxy inverso**

I seguenti URL principali dell’applicazione per ogni applicazione web AEM Forms su JEE. È consigliabile configurare il proxy inverso solo per esporre gli URL per la funzionalità dell&#39;applicazione Web che si desidera fornire agli utenti finali.

Alcuni URL sono evidenziati come applicazioni web rivolte all’utente finale. È consigliabile evitare di esporre altri URL per Configuration Manager per l’accesso agli utenti esterni tramite il proxy inverso.

<table> 
 <thead> 
  <tr> 
   <th><p>URL principale</p> </th> 
   <th><p>Finalità e/o applicazione web associata</p> </th> 
   <th><p>Interfaccia basata su Web</p> </th> 
   <th><p>Accesso utente finale</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>/ReaderExtensions/*</p> </td> 
   <td><p>Estensioni Acrobat Reader DC applicazione Web per l'utente finale per l'applicazione dei diritti di utilizzo ai documenti PDF</p> </td> 
   <td><p>Sì</p> </td> 
   <td><p>Sì</p> </td> 
  </tr> 
  <tr> 
   <td><p>/edc/</p> </td> 
   <td><p>applicazione web Rights Management per utenti finali</p> </td> 
   <td><p>Sì</p> </td> 
   <td><p>Sì</p> </td> 
  </tr> 
  <tr> 
   <td><p>/edcws/</p> </td> 
   <td><p>URL servizio Web per Rights Management</p> </td> 
   <td><p>No</p> </td> 
   <td><p>Sì</p> </td> 
  </tr> 
  <tr> 
   <td><p>/pdfgui/*</p> </td> 
   <td><p>applicazione web di amministrazione di PDF Generator</p> </td> 
   <td><p>Sì</p> </td> 
   <td><p>Sì</p> </td> 
  </tr> 
  <tr> 
   <td><p>/workspace/*</p> </td> 
   <td><p>Applicazione web per utenti finali di Workspace</p> </td> 
   <td><p>Sì</p> </td> 
   <td><p>Sì</p> </td> 
  </tr> 
  <tr> 
   <td><p>/workspace-server/*</p> </td> 
   <td><p>Servlet e servizi dati di Workspace richiesti dall’applicazione client Workspace</p> </td> 
   <td><p>Sì</p> </td> 
   <td><p>Sì</p> </td> 
  </tr> 
  <tr> 
   <td><p>/adobe-bootstrapper/*</p> </td> 
   <td><p>Servlet per l’avvio automatico dell’archivio AEM Forms su JEE</p> </td> 
   <td><p>No</p> </td> 
   <td><p>No</p> </td> 
  </tr> 
  <tr> 
   <td><p>/soap/*</p> </td> 
   <td><p>Pagina delle informazioni per i servizi Web di Forms Server</p> </td> 
   <td><p>No</p> </td> 
   <td><p>No</p> </td> 
  </tr> 
  <tr> 
   <td><p>/soap/services/*</p> </td> 
   <td><p>URL servizio Web per tutti i servizi di Forms Server</p> </td> 
   <td><p>No</p> </td> 
   <td><p>No</p> </td> 
  </tr> 
  <tr> 
   <td><p>/edc/admin/*</p> </td> 
   <td><p>applicazione web di amministrazione del Rights Management</p> </td> 
   <td><p>Sì</p> </td> 
   <td><p>No</p> </td> 
  </tr> 
  <tr> 
   <td><p>/adminui/*</p> </td> 
   <td><p>Home page di Administration Console</p> </td> 
   <td><p>Sì</p> </td> 
   <td><p>No</p> </td> 
  </tr> 
  <tr> 
   <td><p>/TruststoreComponent/</p> <p>protetto/*</p> </td> 
   <td><p>Pagine di amministrazione della gestione dell'archivio fonti attendibili</p> </td> 
   <td><p>Sì</p> </td> 
   <td><p>No</p> </td> 
  </tr> 
  <tr> 
   <td><p>/FormsIVS/*</p> </td> 
   <td><p>Applicazione Forms IVS per il test e il debug del rendering dei moduli</p> </td> 
   <td><p>Sì</p> </td> 
   <td><p>No</p> </td> 
  </tr> 
  <tr> 
   <td><p>/OutputIVS/*</p> </td> 
   <td><p>Applicazione IVS di output per il test e il debug del servizio di output</p> </td> 
   <td><p>Sì</p> </td> 
   <td><p>No</p> </td> 
  </tr> 
  <tr> 
   <td><p>/rmws/*</p> </td> 
   <td><p>URL REST per Rights Management</p> </td> 
   <td><p>No</p> </td> 
   <td><p>Sì</p> </td> 
  </tr> 
  <tr> 
   <td><p>/OutputAdmin/*</p> </td> 
   <td><p>Pagine di amministrazione dell’output</p> </td> 
   <td><p>Sì</p> </td> 
   <td><p>No</p> </td> 
  </tr> 
  <tr> 
   <td><p>/FormServer/*</p> </td> 
   <td><p>File dell’applicazione web Forms</p> </td> 
   <td><p>Sì</p> </td> 
   <td><p>No</p> </td> 
  </tr> 
  <tr> 
   <td><p>/FormServer/GetImage</p> <p>Servlet</p> </td> 
   <td><p>Utilizzato per recuperare JavaScript durante la trasformazione HTML</p> </td> 
   <td><p>No</p> </td> 
   <td><p>No</p> </td> 
  </tr> 
  <tr> 
   <td><p>/FormServerAdmin/*</p> </td> 
   <td><p>Pagine di amministrazione di Forms</p> </td> 
   <td><p>Sì</p> </td> 
   <td><p>No</p> </td> 
  </tr> 
  <tr> 
   <td><p>/repository/*</p> </td> 
   <td><p>URL per accesso a WebDAV (debug)</p> </td> 
   <td><p>Sì</p> </td> 
   <td><p>No</p> </td> 
  </tr> 
  <tr> 
   <td><p>/AACComponent/*</p> </td> 
   <td><p>Interfaccia utente di applicazioni e servizi</p> </td> 
   <td><p>Sì</p> </td> 
   <td><p>No</p> </td> 
  </tr> 
  <tr> 
   <td><p>/WorkspaceAdmin/*</p> </td> 
   <td><p>Pagine di amministrazione di Workspace</p> </td> 
   <td><p>Sì</p> </td> 
   <td><p>No</p> </td> 
  </tr> 
  <tr> 
   <td><p>/rest/*</p> </td> 
   <td><p>Pagine di supporto rimanenti</p> </td> 
   <td><p>Sì</p> </td> 
   <td><p>No</p> </td> 
  </tr> 
  <tr> 
   <td><p>/CoreSystemConfig/*</p> </td> 
   <td><p>Pagina delle impostazioni della configurazione di base di AEM Forms su JEE</p> </td> 
   <td><p>Sì</p> </td> 
   <td><p>No</p> </td> 
  </tr> 
  <tr> 
   <td><p>/um/</p> </td> 
   <td><p>Autenticazione di User Management</p> </td> 
   <td><p>No</p> </td> 
   <td><p>Sì</p> </td> 
  </tr> 
  <tr> 
   <td><p>/um/*</p> </td> 
   <td><p>Interfaccia di amministrazione della gestione utente</p> </td> 
   <td><p>Sì</p> </td> 
   <td><p>No</p> </td> 
  </tr> 
  <tr> 
   <td><p>/DocumentManager/*</p> </td> 
   <td><p>Caricamento e download di documenti da elaborare durante l’accesso agli endpoint remoti, agli endpoint WSDL SOAP e all’SDK Java sul trasporto SOAP o EJB con i documenti HTTP abilitati.</p> </td> 
   <td><p>Sì</p> </td> 
   <td><p>Sì</p> </td> 
  </tr> 
 </tbody> 
</table>

## Protezione da attacchi di tipo Cross-Site Request Forgery {#protecting-from-cross-site-request-forgery-attacks}

Un attacco Cross-Site Request Forgery (CSRF) sfrutta l’affidabilità di un sito web per l’utente, per trasmettere comandi non autorizzati e non voluti dall’utente. L’attacco viene configurato includendo un collegamento o uno script in una pagina web, o un URL in un messaggio e-mail, per accedere a un altro sito a cui l’utente è già stato autenticato.

Ad esempio, potresti aver effettuato l’accesso ad Administration Console mentre navighi simultaneamente in un altro sito web. Una delle pagine web può includere un tag immagine HTML con `src` attributo che esegue il targeting di uno script lato server sul sito web delle vittime. Utilizzando il meccanismo di autenticazione delle sessioni basato su cookie fornito dai browser web, il sito web attaccante può inviare richieste dannose a questo script lato server vittima, mascherato come l&#39;utente legittimo. Per ulteriori esempi, consulta [https://owasp.org/www-community/attacks/csrf#Examples](https://owasp.org/www-community/attacks/csrf#Examples).

Le seguenti caratteristiche sono comuni al CSRF:

* Coinvolgono siti che si basano sull’identità di un utente.
* Sfruttare l&#39;attendibilità del sito per tale identità.
* Impara il browser dell’utente a inviare richieste HTTP a un sito di destinazione.
* Richieste HTTP che hanno effetti collaterali.

AEM Forms su JEE utilizza la funzione Referrer Filter per bloccare gli attacchi CSRF. In questa sezione vengono utilizzati i seguenti termini per descrivere il meccanismo di filtro del referente:

* **Referente consentito:** Un Referrer è l&#39;indirizzo della pagina sorgente che invia una richiesta al server. Per le pagine o i moduli JSP, i Referenti sono in genere la pagina precedente nella cronologia di navigazione. I referrer per le immagini sono in genere le pagine su cui vengono visualizzate le immagini. Puoi identificare il Referrer a cui è consentito l’accesso alle risorse del server aggiungendole all’elenco Referrer consentiti.
* **Eccezioni referente consentite:** Puoi limitare l’ambito di accesso di un particolare Referrer nell’elenco dei Referrer consentiti. Per applicare questa restrizione, puoi aggiungere singoli percorsi di quel Referrer all’elenco Eccezioni referrer consentite. Le richieste provenienti da percorsi inclusi nell&#39;elenco Eccezioni referente consentite non possono richiamare alcuna risorsa sul server Forms. È possibile definire Eccezioni referente consentite per un&#39;applicazione specifica e utilizzare anche un elenco globale di eccezioni che si applicano a tutte le applicazioni.
* **URI consentiti:** Questo è un elenco di risorse che devono essere servite senza controllare l’intestazione Referrer. A questo elenco è possibile aggiungere risorse, ad esempio le pagine della guida, che non determinano modifiche dello stato sul server. Le risorse nell’elenco URI consentiti non vengono mai bloccate dal filtro Referrer, indipendentemente da chi sia il Referrer.
* **Referente nullo:** Una richiesta server che non è associata o non proviene da una pagina web padre viene considerata una richiesta di un referente nullo. Ad esempio, quando apri una nuova finestra del browser, digita un indirizzo e premi Invio, il Referente inviato al server è nullo. Un’applicazione desktop (.NET o SWING) che effettua una richiesta HTTP a un server web invia anche un referente Null al server.

### Filtro referrer {#referer-filtering}

Il processo di filtro Referrer può essere descritto come segue:

1. Forms Server controlla il metodo HTTP utilizzato per la chiamata:

   1. Se si tratta di POST, Forms Server esegue il controllo dell&#39;intestazione Referrer.
   1. Se è GET, il server Forms ignora il controllo Referrer, a meno che *CSRF_CHECK_GETS* è impostato su true, nel qual caso esegue il controllo dell’intestazione Referrer. *CSRF_CHECK_GETS* è specificato in *web.xml* per la tua applicazione.

1. Il server Forms verifica se l&#39;URI richiesto esiste nel inserisco nell&#39;elenco Consentiti di:

   1. Se l&#39;URI viene inserito nell&#39;elenco Consentiti, il server accetta la richiesta.
   1. Se l’URI richiesto non viene inserito nell&#39;elenco Consentiti, il server recupera il Referrer della richiesta.

1. Se nella richiesta è presente un Referrer, il server controlla se si tratta di un Referrer consentito. Se consentito, il server verifica la presenza di un&#39;eccezione Referrer:

   1. Se si tratta di un&#39;eccezione, la richiesta viene bloccata.
   1. Se non si tratta di un’eccezione, la richiesta viene passata.

1. Se nella richiesta non è presente alcun Referrer, il server controlla se è consentito un Referrer Nullo:

   1. Se è consentito un referente nullo, la richiesta viene passata.
   1. Se non è consentito un referente Null, il server controlla se l’URI richiesto è un’eccezione per il referente Null e gestisce la richiesta di conseguenza.

### Gestione del filtro del referente {#managing-referer-filtering}

AEM Forms su JEE fornisce un filtro Referrer per specificare il Referrer che può accedere alle risorse del server. Per impostazione predefinita, il filtro Referrer non filtra le richieste che utilizzano un metodo HTTP sicuro, ad esempio GET, a meno che *CSRF_CHECK_GETS* è impostato su true. Se il numero di porta per una voce Referrer consentito è impostato su 0, AEM Forms su JEE consentirà tutte le richieste con Referrer provenienti da tale host indipendentemente dal numero di porta. Se non viene specificato alcun numero di porta, sono consentite solo le richieste dalla porta predefinita 80 (HTTP) o dalla porta 443 (HTTPS). Il filtro Referrer è disattivato se tutte le voci nell&#39;elenco Referrer consentiti vengono eliminate.

Quando si installa Document Services per la prima volta, l’elenco Referenti consentiti viene aggiornato con l’indirizzo del server in cui è installato Document Services. Le voci per il server includono il nome del server, l&#39;indirizzo IPv4, l&#39;indirizzo IPv6 se IPv6 è abilitato, l&#39;indirizzo di loopback e una voce localhost. I nomi aggiunti all&#39;elenco Referenti consentiti vengono restituiti dal sistema operativo host. Ad esempio, un server con un indirizzo IP di 10.40.54.187 includerà le seguenti voci: `https://server-name:0, https://10.40.54.187:0, https://127.0.0.1:0, http://localhost:0`. Per tutti i nomi non qualificati restituiti dal sistema operativo host (nomi che non hanno indirizzo IPv4, indirizzo IPv6 o nome di dominio qualificato), il inserisco nell&#39;elenco Consentiti di non viene aggiornato. Modifica l’elenco dei Referenti consentiti in base all’ambiente aziendale. Non distribuire Forms Server nell’ambiente di produzione con l’elenco dei Destinatari autorizzati predefiniti. Dopo aver modificato uno dei Referrer consentiti, le Eccezioni referente o gli URI, assicurati di riavviare il server affinché le modifiche diventino effettive.

**Gestione dell’elenco dei referenti consentiti**

È possibile gestire l’elenco Referenti consentiti dall’interfaccia di gestione utente di Administration Console. L&#39;interfaccia User Management offre la funzionalità di creazione, modifica o eliminazione dell&#39;elenco. Consulta la sezione * [Prevenzione degli attacchi CSRF](/help/forms/using/admin-help/preventing-csrf-attacks.md)* sezione del *aiuto per l&#39;amministrazione* per ulteriori informazioni sull’utilizzo dell’elenco Referenti consentiti.

**Gestione degli elenchi delle eccezioni e degli URI consentiti ai referenti**

AEM Forms su JEE fornisce API per gestire l’elenco Eccezioni referenti consentite e l’elenco URI consentiti. Puoi utilizzare queste API per recuperare, creare, modificare o eliminare l’elenco. Di seguito è riportato un elenco delle API disponibili:

* createAllowedURIsList
* getAllowedURIsList
* updateAllowedURIsList
* deleteAllowedURIsList
* addAllowedRefererExceptions
* getAllowedRefererExceptions
* updateAllowedRefererExceptions
* deleteAllowedRefererExceptions

Per ulteriori informazioni sulle API, consulta la documentazione di riferimento* per AEM Forms su JEE API.

Utilizza il ***LC_GLOBAL_ALLOWED_REFERER_EXCEPTION*** elenco delle eccezioni Referente consentite a livello globale, per definire le eccezioni applicabili a tutte le applicazioni. Questo elenco contiene solo URI con un percorso assoluto (ad esempio, `/index.html`) o un percorso relativo (ad esempio, `/sample/`). Puoi anche aggiungere un’espressione regolare alla fine di un URI relativo, ad esempio: `/sample/(.)*`.

Il ***LC_GLOBAL_ALLOWED_REFERER_EXCEPTION*** l’ID elenco è definito come costante nella `UMConstants` classe del `com.adobe.idp.um.api` spazio dei nomi, trovato in `adobe-usermanager-client.jar`. Puoi utilizzare le API di AEM Forms per creare, modificare o modificare questo elenco. Ad esempio, per creare l’elenco Eccezioni referente consentite globali, utilizza:

```java
addAllowedRefererExceptions(UMConstants.LC_GLOBAL_ALLOWED_REFERER_EXCEPTION, Arrays.asList("/index.html", "/sample/(.)*"))
```

Utilizza il ***CSRF_ALLOWED_REFERER_EXCEPTIONS*** elenco di eccezioni specifiche per l&#39;applicazione.

**Disabilitazione del filtro Referrer**

Se il filtro Referrer blocca completamente l&#39;accesso a Forms Server e non è possibile modificare l&#39;elenco Referrer consentiti, è possibile aggiornare lo script di avvio del server e disattivare il filtro Referrer.

Includi `-Dlc.um.csrffilter.disabled=true` Argomento JAVA nello script di avvio e riavviare il server. Assicurati di eliminare l’argomento JAVA dopo aver riconfigurato in modo appropriato l’elenco dei Referenti consentiti.

**Filtro referrer per file WAR personalizzati**

È possibile che tu abbia creato file WAR personalizzati da utilizzare con AEM Forms su JEE per soddisfare i tuoi requisiti aziendali. Per abilitare il filtro Referrer per i file WAR personalizzati, includi ***adobe-usermanager-client.jar*** nel percorso di classe per WAR e includere una voce di filtro nel file* web.xml* con i seguenti parametri:

**CSRF_CHECK_GETS** controlla il controllo Referrer sulle richieste GET. Se questo parametro non è definito, il valore predefinito viene impostato su false. Includi questo parametro solo se desideri filtrare le richieste GET.

**CSRF_ALLOWED_REFERER_EXCEPTIONS** è l’ID dell’elenco Eccezioni referente consentite. Il filtro Referrer impedisce che le richieste provenienti da Referrer nell&#39;elenco identificato dall&#39;ID elenco richiamino qualsiasi risorsa sul server Forms.

**CSRF_ALLOWED_URIS_LIST_NAME** è l’ID dell’elenco degli URI consentiti. Il filtro Referrer non blocca le richieste per nessuna delle risorse nell’elenco identificate dall’ID elenco, indipendentemente dal valore dell’intestazione Referrer nella richiesta.

**CSRF_ALLOW_NULL_REFERER** controlla il comportamento del filtro Referrer quando il Referrer è nullo o non presente. Se questo parametro non è definito, il valore predefinito viene impostato su false. Includi questo parametro solo se desideri consentire l’uso di Riferimenti Null. L’autorizzazione di referenti null può consentire alcuni tipi di attacchi di tipo Cross Site Request Forgery.

**CSRF_NULL_REFERER_EXCEPTIONS** è un elenco degli URI per i quali non viene eseguito il controllo Referrer quando il Referrer è nullo. Questo parametro è abilitato solo quando *CSRF_ALLOW_NULL_REFERER* è impostato su false. Separa più URI nell’elenco con una virgola.

Di seguito è riportato un esempio della voce di filtro in *web.xml* file per un ***ESEMPIO*** File WAR:

```java
<filter> 
       <filter-name> filter-name </filter-name> 
       <filter-class> com.adobe.idp.um.auth.filter.RemoteCSRFFilter </filter-class> 
     <!-- default is false --> 
     <init-param> 
      <param-name> CSRF_ALLOW_NULL_REFERER </param-name> 
      <param-value> false </param-value> 
     </init-param> 
     <!-- default is false --> 
     <init-param> 
      <param-name> CSRF_CHECK_GETS </param-name> 
      <param-value> true </param-value> 
     </init-param> 
     <!-- Optional --> 
     <init-param> 
       <param-name> CSRF_NULL_REFERER_EXCEPTIONS </param-name> 
       <param-value> /SAMPLE/login, /SAMPLE/logout  </param-value> 
     </init-param> 
     <!-- Optional --> 
     <init-param> 
      <param-name> CSRF_ALLOWED_REFERER_EXCEPTIONS </param-name> 
      <param-value> SAMPLE_ALLOWED_REF_EXP_ID </param-value> 
     </init-param> 
     <!-- Optional --> 
     <init-param> 
      <param-name> CSRF_ALLOWED_URIS_LIST_NAME </param-name> 
      <param-value> SAMPLE_ALLOWED_URI_LIST_ID     </param-value> 
     </init-param> 
</filter> 
    ........ 
    <filter-mapping> 
      <filter-name> filter-name </filter-name> 
      <url-pattern>/*</url-pattern> 
    </filter-mapping>
```

**Risoluzione dei problemi**

Se le richieste di server legittime vengono bloccate dal filtro CSRF, eseguire una delle operazioni seguenti:

* Se la richiesta rifiutata ha un’intestazione Referrer, prova ad aggiungerla all’elenco Referrer consentiti. Aggiungi solo referrer considerato attendibile.
* Se la richiesta rifiutata non ha un’intestazione Referrer, modifica l’applicazione client per includere un’intestazione Referrer.
* Se il client può funzionare in un browser, provare il modello di distribuzione.
* In ultima istanza, puoi aggiungere la risorsa all’elenco degli URI consentiti. Questa impostazione non è consigliata.

## Configurazione di rete sicura {#secure-network-configuration}

Questa sezione descrive i protocolli e le porte richiesti da AEM Forms su JEE e fornisce consigli per la distribuzione di AEM Forms su JEE in una configurazione di rete sicura.

### Protocolli di rete utilizzati da AEM Forms su JEE {#network-protocols-used-by-aem-forms-on-jee}

Quando configuri un’architettura di rete sicura come descritto nella sezione precedente, per l’interazione tra AEM Forms su JEE e altri sistemi della rete aziendale sono necessari i seguenti protocolli di rete.

<table> 
 <thead> 
  <tr> 
   <th><p>Protocollo</p> </th> 
   <th><p>Utilizzare</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>HTTP</p> </td> 
   <td> 
    <ul> 
     <li><p>Il browser visualizza le applicazioni web di Configuration Manager e dell’utente finale</p> </li> 
     <li><p>Tutte le connessioni SOAP</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>SOAP</p> </td> 
   <td> 
    <ul> 
     <li><p>applicazioni client di servizi Web, ad esempio applicazioni .NET</p> </li> 
     <li><p>Adobe Reader® utilizza SOAP per AEM Forms sui servizi web del server JEE</p> </li> 
     <li><p>Adobe di applicazioni Flash® che utilizzano SOAP per i servizi Web di Forms Server</p> </li> 
     <li><p>Chiamate SDK di AEM Forms su JEE quando utilizzate in modalità SOAP</p> </li> 
     <li><p>Ambiente di progettazione di Workbench</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>RMI</p> </td> 
   <td><p>Chiamate SDK di AEM Forms su JEE quando utilizzato in modalità Enterprise JavaBeans (EJB)</p> </td> 
  </tr> 
  <tr> 
   <td><p>IMAP/POP3</p> </td> 
   <td> 
    <ul> 
     <li><p>Input basato su e-mail a un servizio (endpoint e-mail)</p> </li> 
     <li><p>Notifiche delle attività utente tramite e-mail</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>I/O file UNC</p> </td> 
   <td><p>Monitoraggio AEM Forms su JEE delle cartelle controllate per l’input in un servizio (endpoint cartella controllata)</p> </td> 
  </tr> 
  <tr> 
   <td><p>LDAP</p> </td> 
   <td> 
    <ul> 
     <li><p>Sincronizzazioni delle informazioni su utenti e gruppi dell’organizzazione in una directory</p> </li> 
     <li><p>Autenticazione LDAP per utenti interattivi</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>JDBC</p> </td> 
   <td> 
    <ul> 
     <li><p>Query e chiamate di routine effettuate a un database esterno durante l'esecuzione di un processo tramite il servizio JDBC</p> </li> 
     <li><p>Accesso interno all’archivio AEM Forms su JEE</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>WebDAV</p> </td> 
   <td><p>Consente la navigazione remota dell’archivio AEM Forms in fase di progettazione JEE (moduli, frammenti e così via) da parte di qualsiasi client WebDAV</p> </td> 
  </tr> 
  <tr> 
   <td><p>AMF</p> </td> 
   <td><p>Adobe di applicazioni di Flash, in cui i servizi server di AEM Forms su JEE sono configurati con un endpoint remoto</p> </td> 
  </tr> 
  <tr> 
   <td><p>JMX</p> </td> 
   <td><p>AEM Forms su JEE espone MBean per il monitoraggio tramite JMX</p> </td> 
  </tr> 
 </tbody> 
</table>

### Porte per server applicazioni {#ports-for-application-servers}

In questa sezione vengono descritte le porte predefinite (e gli intervalli di configurazione alternativi) per ogni tipo di server applicazioni supportato. Queste porte devono essere attivate o disattivate sul firewall interno, a seconda della funzionalità di rete che si desidera consentire ai client che si connettono al server applicazioni che esegue AEM Forms su JEE.

>[!NOTE]
>
>Per impostazione predefinita, il server espone diversi MBean JMX nello spazio dei nomi adobe.com. Vengono esposte solo le informazioni utili per il monitoraggio dello stato del server. Tuttavia, per evitare la divulgazione delle informazioni, è necessario impedire ai chiamanti di una rete non attendibile di cercare MBean JMX e di accedere alle metriche di integrità.

**Porte JBoss**

<table> 
 <thead> 
  <tr> 
   <th><p>Scopo</p> </th> 
   <th><p>Porta </p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>Accesso alle applicazioni web</p> </td> 
   <td><p>[JBOSS_Root]/standalone/configuration/lc_[database].xml</p> <p>Porta del connettore HTTP/1.1 8080</p> <p>AJP 1.3 Porta del connettore 8009</p> <p>Porta connettore SSL/TLS 8443</p> </td> 
  </tr> 
  <tr> 
   <td><p>Supporto per CORBA</p> </td> 
   <td><p>[Directory principale JBoss]/server/all/conf/jacorb.properties</p> <p>OAPort 3528</p> <p>OASSLPort 3529</p> </td> 
  </tr> 
 </tbody> 
</table>

**Porte WebLogic**

<table> 
 <thead> 
  <tr> 
   <th><p>Scopo</p> </th> 
   <th><p>Porta </p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>Accesso alle applicazioni web</p> </td> 
   <td> 
    <ul> 
     <li><p>Porta di ascolto di Admin Server: il valore predefinito è 7001</p> </li> 
     <li><p>Porta di ascolto SSL di Admin Server: il valore predefinito è 7002</p> </li> 
     <li><p>Porta configurata per il server gestito, ad esempio 8001</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>Porte di amministrazione WebLogic non necessarie per accedere a AEM Forms su JEE</p> </td> 
   <td> 
    <ul> 
     <li><p>Porta di ascolto del server gestito: configurabile da 1 a 65534</p> </li> 
     <li><p>Porta di ascolto SSL del server gestito: configurabile da 1 a 65534</p> </li> 
     <li><p>Porta di ascolto di Node Manager: il valore predefinito è 5556</p> </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>

**Porte WebSphere**

Per informazioni sulle porte WebSphere richieste da AEM Forms su JEE, passare all&#39;impostazione del numero di porta nell&#39;interfaccia utente di WebSphere Application Server.

### Configurazione di SSL {#configuring-ssl}

Con riferimento all’architettura fisica descritta nella sezione [Architettura fisica di AEM Forms su JEE](hardening-aem-forms-jee-environment.md#aem-forms-on-jee-physical-architecture), è necessario configurare SSL per tutte le connessioni che si intende utilizzare. In particolare, tutte le connessioni SOAP devono essere eseguite tramite SSL per evitare l&#39;esposizione delle credenziali utente in una rete.

Per istruzioni su come configurare SSL su JBoss, WebLogic e WebSphere, vedi &quot;Configurazione di SSL&quot; in [aiuto per l&#39;amministrazione](https://www.adobe.com/go/learn_aemforms_admin_64).

Per istruzioni su come importare certificati in JVM (Java Virtual Machine) configurata per un server AEM Forms, vedere la sezione Autenticazione reciproca in [Guida di AEM Forms Workbench](https://www.adobe.com/go/learn_aemforms_workbench_65).

### Configurazione del reindirizzamento SSL {#configuring-ssl-redirect}

Dopo aver configurato il server applicazioni per il supporto di SSL, è necessario assicurarsi che tutto il traffico HTTP verso applicazioni e servizi venga imposto per l&#39;utilizzo della porta SSL.

Per configurare il reindirizzamento SSL per WebSphere o WebLogic, consulta la documentazione del server applicazioni.

1. Apri il prompt dei comandi, passa alla directory /JBOSS_HOME/standalone/configuration ed esegui il comando seguente:

   `keytool -genkey -alias jboss7 -keyalg RSA -keystore server.keystore -validity 10950`

1. Apri il file JBOSS_HOME/standalone/configuration/standalone.xml per la modifica.

   Dopo il &lt;subsystem xmlns=&quot;urn&lt;span id=&quot; translate=&quot;no&quot; />dominio:web:1.1&quot; native=&quot;false&quot; default-virtual-server=&quot;default-host&quot;>, aggiungere i dettagli seguenti::jboss:

   &lt;connector name=&quot;https&quot; protocol=&quot;HTTP/1.1&quot; scheme=&quot;https&quot; socket-binding=&quot;https&quot; enabled=&quot;true&quot; secure=&quot;true&quot;/>

1. Aggiungi il seguente codice nell’elemento del connettore https:

   ```xml
   <connector name="https" protocol="HTTP/1.1" scheme="https" socket-binding="https" secure="true" enabled="true"> 
    <ssl name="jboss7_ssl" key-alias="jboss71" password="Tibco321" certificate-key-file="../standalone/configuration/server.keystore" protocol="TLSv1"/> 
    </connector>
   ```

   Salvare e chiudere il file standalone.xml.

## Consigli di protezione specifici per Windows {#windows-specific-security-recommendations}

Questa sezione contiene raccomandazioni sulla sicurezza specifiche per Windows quando viene utilizzato per eseguire AEM Forms su JEE.

### Account del servizio JBoss {#jboss-service-accounts}

Per impostazione predefinita, l’installazione chiavi in mano di AEM Forms su JEE imposta un account di servizio utilizzando l’account Sistema locale. L&#39;account utente del sistema locale incorporato dispone di un livello elevato di accessibilità e fa parte del gruppo Administrators. Se l&#39;identità di un processo di lavoro viene eseguita come account utente del sistema locale, tale processo di lavoro ha accesso completo all&#39;intero sistema.

#### Eseguire il server applicazioni utilizzando un account non amministrativo {#run-the-application-server-using-a-non-administrative-account}

1. In Microsoft Management Console (MMC), creare un utente locale per il servizio Forms Server per l&#39;accesso come:

   * Seleziona **L&#39;utente non può cambiare la password**.
   * Il giorno **Membro di** , verificare che sia elencato il gruppo Utenti.

1. Seleziona **Impostazioni** > **Strumenti di amministrazione** > **Servizi**.
1. Fare doppio clic sul servizio Application Server e arrestare il servizio.
1. Il giorno **Accedi** , seleziona **Questo account**, individua l&#39;account utente creato e immetti la password per l&#39;account.
1. Nella finestra Impostazioni di protezione locali, in Assegnazione diritti utente assegnare i seguenti diritti all&#39;account utente in cui è in esecuzione Forms Server:

   * Nega accesso tramite Servizi terminal
   * Nega accesso localyxx
   * Accedi come servizio (dovrebbe essere già impostato)

1. Concedi al nuovo account utente le autorizzazioni di modifica per le seguenti directory:
   * **Directory Global Document Storage (GDS)**: la posizione della directory GDS viene configurata manualmente durante il processo di installazione di AEM Forms. Se l&#39;impostazione relativa al percorso rimane vuota durante l&#39;installazione, per impostazione predefinita viene utilizzata una directory nell&#39;installazione del server applicazioni in `[JBoss root]/server/[type]/svcnative/DocumentStorage`
   * **Directory CRX-Repository**: la posizione predefinita è `[AEM-Forms-installation-location]\crx-repository`
   * **Directory temporanee di AEM Forms**:
      * (Windows) Percorso TMP o TEMP impostato nelle variabili di ambiente
      * (AIX, Linux o Solaris) Directory principale dell&#39;utente connesso Nei sistemi basati su UNIX, un utente non root può utilizzare la seguente directory come directory temporanea:
      * (Linux) /var/tmp o /usr/tmp
      * (AIX) /tmp o /usr/tmp
      * (Solaris) /var/tmp o /usr/tmp
1. Assegna al nuovo account utente le autorizzazioni di scrittura per le directory seguenti:
   * [JBoss-directory]\standalone\distribuzione
   * [JBoss-directory]\standalone\
   * [JBoss-directory]\bin\

   >[!NOTE]
   >
   >Percorso di installazione predefinito del server applicazioni JBoss:
   >
   >* Windows: C:\Adobe\Adobe_Experience_Manager_Forms\jboss
   >* Linux: /opt/jboss/.

1. Avviare il servizio server applicazioni.

### Protezione del file system {#file-system-security}

AEM Forms su JEE utilizza il file system nei seguenti modi:

* Memorizza i file temporanei utilizzati durante l&#39;elaborazione dell&#39;input e dell&#39;output del documento
* Memorizza i file nell&#39;archivio di archivio globale utilizzati per supportare i componenti della soluzione installati
* Nelle cartelle controllate vengono archiviati i file eliminati utilizzati come input in un servizio da una posizione della cartella del file system

Quando si utilizzano le cartelle controllate come metodo per inviare e ricevere documenti con un servizio Forms Server, adottare ulteriori precauzioni per la protezione del file system. Quando un utente rilascia del contenuto nella cartella controllata, tale contenuto viene esposto attraverso la cartella controllata. In questo caso, il servizio non autentica l’utente finale effettivo. Al contrario, si basa sulla sicurezza ACL e a livello di condivisione da impostare a livello di cartella per determinare chi può effettivamente richiamare il servizio.

## Raccomandazioni sulla sicurezza specifiche per JBoss {#jboss-specific-security-recommendations}

Questa sezione contiene i consigli di configurazione del server applicazioni specifici per JBoss 7.0.6 quando utilizzato per eseguire AEM Forms su JEE.

### Disabilita la console di gestione JBoss e la console JMX {#disable-jboss-management-console-and-jmx-console}

L’accesso a JBoss Management Console e JMX Console è già configurato (il monitoraggio JMX è disabilitato) quando si installa AEM Forms su JEE su JBoss utilizzando il metodo di installazione chiavi in mano. Se utilizzi un server applicazioni JBoss personalizzato, assicurati che l’accesso alla console di gestione JBoss e alla console di monitoraggio JMX sia protetto. L’accesso alla console di monitoraggio JMX è impostato nel file di configurazione JBoss denominato jmx-invoker-service.xml.

### Disattiva esplorazione directory {#disable-directory-browsing}

Dopo aver effettuato l’accesso ad Administration Console, è possibile sfogliare l’elenco delle directory della console modificando l’URL. Ad esempio, se modifichi l’URL in uno dei seguenti URL, potrebbe essere visualizzato un elenco di directory:

```java
https://<servername>:8080/adminui/secured/ 
https://<servername>:8080/um/
```

## Raccomandazioni sulla sicurezza specifiche per WebLogic {#weblogic-specific-security-recommendations}

Questa sezione contiene i suggerimenti per la configurazione del server applicazioni per la protezione di WebLogic 9.1 durante l&#39;esecuzione di AEM Forms su JEE.

### Disattiva esplorazione directory {#disable_directory_browsing-1}

Impostare le proprietà delle directory indice nel file weblogic.xml su `false`, come mostrato in questo esempio:

```xml
<container-descriptor> 
    <index-directory-enabled>false 
    </index-directory-enabled> 
</container-descriptor>
```

### Abilita porta SSL WebLogic {#enable-weblogic-ssl-port}

Per impostazione predefinita, WebLogic non abilita la porta di ascolto SSL predefinita, 7002. Abilitare questa porta nella console di amministrazione del server WebLogic prima di configurare SSL.

## Consigli sulla sicurezza specifici per WebSphere {#websphere-specific-security-recommendations}

Questa sezione contiene i suggerimenti per la configurazione del server applicazioni per la protezione di WebSphere che esegue AEM Forms su JEE.

### Disattiva esplorazione directory {#disable_directory_browsing-2}

Imposta il `directoryBrowsingEnabled` nel file ibm-web-ext.xml a `false`.

### Abilita protezione amministrativa WebSphere {#enable-websphere-administrative-security}

1. Accedere a WebSphere Administrative Console.
1. Nella struttura di navigazione, vai a **Sicurezza** > **Sicurezza globale**
1. Seleziona **Abilita sicurezza amministrativa**.
1. Deseleziona entrambi **Abilitare la sicurezza dell&#39;applicazione** e **Usa protezione Java 2**.
1. Clic **OK** o **Applica**.
1. In **Messaggi** , fare clic su **Salva direttamente nella configurazione principale**.
