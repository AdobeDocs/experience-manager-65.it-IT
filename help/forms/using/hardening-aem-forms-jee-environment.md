---
title: Hardening del tuo AEM Forms sull'ambiente JEE
seo-title: Hardening del tuo AEM Forms sull'ambiente JEE
description: Scopri diverse impostazioni di protezione per migliorare la sicurezza di AEM Forms su JEE in esecuzione in una Intranet aziendale.
seo-description: Scopri diverse impostazioni di protezione per migliorare la sicurezza di AEM Forms su JEE in esecuzione in una Intranet aziendale.
uuid: f6c63690-6376-4fe1-9df2-a14fbfd62aff
content-type: reference
topic-tags: Security
products: SG_EXPERIENCEMANAGER/6.4
discoiquuid: 6b380e92-f90d-4875-b7a2-f3958daf2364
role: Admin
exl-id: 6fb260f9-d0f8-431e-8d4e-535b451e4124
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '7696'
ht-degree: 1%

---

# Hardening del tuo AEM Forms sull&#39;ambiente JEE {#hardening-your-aem-forms-on-jee-environment}

Scopri diverse impostazioni di protezione per migliorare la sicurezza di AEM Forms su JEE in esecuzione in una Intranet aziendale.

L’articolo descrive raccomandazioni e best practice per la protezione dei server che eseguono AEM Forms su JEE. Non si tratta di un documento completo per l&#39;indurimento degli host per il sistema operativo e i server applicazioni. Questo articolo descrive invece una serie di impostazioni di protezione che devi implementare per migliorare la sicurezza di AEM Forms su JEE in esecuzione all&#39;interno di una Intranet aziendale. Tuttavia, per garantire la sicurezza di AEM Forms sui server applicazioni JEE, devi anche implementare procedure di monitoraggio, rilevamento e risposta della sicurezza.

L&#39;articolo descrive le tecniche di indurimento che devono essere applicate durante le seguenti fasi del ciclo di vita dell&#39;installazione e della configurazione:

* **Pre-installazione:** utilizza queste tecniche prima di installare AEM Forms su JEE.
* **Installazione:** utilizza queste tecniche durante il processo di installazione di AEM Forms on JEE.
* **Post-installazione:** utilizza queste tecniche dopo l’installazione e periodicamente dopo.

AEM Forms su JEE è altamente personalizzabile e può funzionare in molti ambienti diversi. Alcuni dei consigli potrebbero non essere adatti alle esigenze della tua organizzazione.

## Preinstallazione {#preinstallation}

Prima di installare AEM Forms su JEE , puoi applicare soluzioni di sicurezza al livello di rete e al sistema operativo. Questa sezione descrive alcuni problemi e formula raccomandazioni per ridurre le vulnerabilità di sicurezza in queste aree.

**Installazione e configurazione su UNIX e Linux**

Non installare o configurare AEM Forms su JEE utilizzando una shell principale. Per impostazione predefinita, i file sono installati nella directory /opt e l&#39;utente che esegue l&#39;installazione ha bisogno di tutte le autorizzazioni dei file in /opt. In alternativa, è possibile eseguire un’installazione sotto la directory /user di un singolo utente, in cui dispongono già di tutte le autorizzazioni per i file.

**Installazione e configurazione in Windows**

È necessario eseguire l&#39;installazione su Windows come amministratore se si sta installando AEM Forms su JEE su JBoss utilizzando il metodo chiavi in mano o se si sta installando PDF Generator. Inoltre, quando si installa PDF Generator su Windows con supporto dell&#39;applicazione nativa, è necessario eseguire l&#39;installazione come lo stesso utente Windows che ha installato Microsoft Office. Per ulteriori informazioni sui privilegi di installazione, consulta il documento* Installazione e distribuzione di AEM Forms su JEE* per il server delle applicazioni.

### Sicurezza a livello di rete {#network-layer-security}

Le vulnerabilità relative alla sicurezza della rete costituiscono una delle prime minacce per qualsiasi server applicativo rivolto a Internet o Intranet. Questa sezione descrive il processo di indurimento degli host sulla rete rispetto a queste vulnerabilità. Si occupa della segmentazione della rete, dell&#39;indurimento dello stack del protocollo di controllo della trasmissione/protocollo Internet (TCP/IP) e dell&#39;uso di firewall per la protezione dell&#39;host.

La tabella seguente descrive i processi comuni che riducono le vulnerabilità relative alla sicurezza della rete.

<table> 
 <thead> 
  <tr> 
   <th><p>Problema</p> </th> 
   <th><p>Descrizione</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>Zone demilitarizzate (DMZ)</p> </td> 
   <td><p>Distribuire server dei moduli all’interno di una zona demilitarizzata (DMZ). La segmentazione deve esistere in almeno due livelli con il server applicazioni utilizzato per eseguire AEM Forms su JEE posizionato dietro il firewall interno. Separare la rete esterna dalla rete DMZ che contiene i server web, che a loro volta devono essere separati dalla rete interna. Usa i firewall per implementare i livelli di separazione. Dividi in categorie e controlla il traffico che passa attraverso ciascun livello di rete per garantire che sia consentito solo il minimo assoluto di dati richiesti.</p> </td> 
  </tr> 
  <tr> 
   <td><p>Indirizzi IP privati</p> </td> 
   <td><p>Utilizza NAT (Network Address Translation) con indirizzi IP privati RFC 1918 sul server dell'applicazione AEM Forms. Assegna indirizzi IP privati (10.0.0.0/8, 172.16.0.0/12 e 192.168.0.0/16) per rendere più difficile per un aggressore indirizzare il traffico da e verso un host interno NAT attraverso Internet.</p> </td> 
  </tr> 
  <tr> 
   <td><p>Firewall</p> </td> 
   <td><p>Utilizza i seguenti criteri per selezionare una soluzione firewall:</p> 
    <ul> 
     <li><p>Implementa firewall che supportano server proxy e/o <em>ispezione dello stato</em> invece di semplici soluzioni di filtro dei pacchetti.</p> </li> 
     <li><p>Utilizzare un firewall che supporta <em>nega tutti i servizi, eccetto quelli consentiti in modo esplicito</em> paradigmi di sicurezza.</p> </li> 
     <li><p>Implementa una soluzione firewall con doppia home o multihomed. Questa architettura fornisce il massimo livello di sicurezza e aiuta a evitare che utenti non autorizzati bypassino la sicurezza del firewall.</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>Porte del database</p> </td> 
   <td><p>Non utilizzare le porte di ascolto predefinite per i database (MySQL - 3306, Oracle - 1521, MS SQL - 1433). Per informazioni sulla modifica delle porte del database, consultare la documentazione del database.</p> <p>L'utilizzo di una porta di database diversa influisce sulla configurazione complessiva di AEM Forms su JEE. Se modifichi le porte predefinite, devi apportare le modifiche corrispondenti in altre aree di configurazione, ad esempio le origini dati per AEM Forms su JEE.</p> <p>Per informazioni sulla configurazione delle origini dati in AEM Forms su JEE, consulta Installare e aggiornare AEM Forms su JEE o Aggiornare ad AEM Forms su JEE per il server delle applicazioni in <a href="/help/forms/using/introduction-aem-forms.md" target="_blank">Guida utente di AEM Forms</a>.</p> </td> 
  </tr> 
 </tbody> 
</table>

### Sicurezza del sistema operativo {#operating-system-security}

La tabella seguente descrive alcuni approcci potenziali per ridurre al minimo le vulnerabilità di sicurezza riscontrate nel sistema operativo.

<table> 
 <thead> 
  <tr> 
   <th><p>Problema</p></th> 
   <th><p>Descrizione</p></th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>Patch di sicurezza</p></td> 
   <td><p>Esiste un rischio maggiore che un utente non autorizzato possa accedere al server dell'applicazione se le patch e gli aggiornamenti di sicurezza del fornitore non vengono applicati in modo tempestivo. Verifica le patch di sicurezza prima di applicarle ai server di produzione.</p><p>Inoltre, crea criteri e procedure per verificare e installare le patch regolarmente.</p></td> 
  </tr> 
  <tr> 
   <td><p>Software di protezione contro i virus</p></td> 
   <td><p>Gli scanner di virus possono identificare i file infetti digitalizzando una firma o guardando per un comportamento insolito. Gli scanner conservano le firme dei virus in un file, che di solito è memorizzato sul disco rigido locale. Poiché i nuovi virus vengono spesso scoperti, è necessario aggiornare frequentemente questo file per lo scanner virus per identificare tutti i virus correnti.</p></td> 
  </tr> 
  <tr> 
   <td><p>Network Time Protocol (NTP)</p></td> 
   <td><p>Per l'analisi forense, mantenere un tempo preciso sui server dei moduli. Utilizzare NTP per sincronizzare il tempo su tutti i sistemi che sono connessi direttamente a Internet.</p></td> 
  </tr> 
 </tbody> 
</table>

Per ulteriori informazioni sulla sicurezza del sistema operativo, vedere [&quot;Informazioni sulla sicurezza del sistema operativo&quot;](https://helpx.adobe.com/aem-forms/6-1/hardening-security/general-security-considerations.html#operating_system_security_information).

## Installazione {#installation}

Questa sezione descrive le tecniche che puoi utilizzare durante il processo di installazione di AEM Forms per ridurre le vulnerabilità relative alla sicurezza. In alcuni casi, queste tecniche utilizzano opzioni che fanno parte del processo di installazione. Nella tabella seguente sono descritte queste tecniche.

<table> 
 <thead> 
  <tr> 
   <th><p>Problema</p> </th> 
   <th><p>Descrizione</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>Privilegi</p> </td> 
   <td><p>Utilizzare il numero minimo di privilegi necessari per installare il software. Accedere al computer utilizzando un account non appartenente al gruppo Administrators. In Windows, è possibile utilizzare il comando Esegui come per eseguire il programma di installazione di AEM Forms su JEE come utente amministrativo. Nei sistemi UNIX e Linux, utilizzare un comando come <code>sudo</code> per installare il software.</p> </td> 
  </tr> 
  <tr> 
   <td><p>Origine software</p> </td> 
   <td><p>Non scaricare o eseguire AEM Forms su JEE da fonti non attendibili.</p> <p>I programmi dannosi possono contenere codice per violare la sicurezza in diversi modi, tra cui furto, modifica e cancellazione dei dati e rifiuto del servizio. Installa AEM Forms su JEE dal DVD di Adobe o solo da una sorgente affidabile.</p> </td> 
  </tr> 
  <tr> 
   <td><p>Partizioni disco</p> </td> 
   <td><p>Posizionare AEM Forms su JEE in una partizione disco dedicata. La segmentazione del disco è un processo che mantiene dati specifici sul server su dischi fisici separati per una maggiore sicurezza. L'organizzazione dei dati in questo modo riduce il rischio di attacchi di tipo "directory traversal". Pianificare la creazione di una partizione separata dalla partizione di sistema in cui è possibile installare AEM Forms nella directory dei contenuti JEE. In Windows, la partizione di sistema contiene la directory di sistema32 o la partizione di avvio.</p> </td> 
  </tr> 
  <tr> 
   <td><p>Componenti</p> </td> 
   <td><p>Valuta i servizi esistenti e disabilita o disinstalla quelli non necessari. Non installare componenti e servizi non necessari.</p> <p>L'installazione predefinita di un server applicazioni potrebbe includere servizi non necessari per l'utilizzo. È necessario disattivare tutti i servizi non necessari prima della distribuzione per ridurre al minimo i punti di ingresso per un attacco. Ad esempio, su JBoss, puoi commentare i servizi non necessari nel file descrittore META-INF/jboss-service.xml .</p> </td> 
  </tr> 
  <tr> 
   <td><p>File dei criteri tra domini diversi</p> </td> 
   <td><p>La presenza di un file <code>crossdomain.xml</code> sul server può indebolire immediatamente tale server. Si consiglia di rendere l’elenco dei domini il più restrittivo possibile. Non inserire in produzione il file <code>crossdomain.xml</code> utilizzato durante lo sviluppo utilizzando Guide <em>(obsoleto)</em>. Per una guida che utilizza i servizi web, se il servizio si trova sullo stesso server che ha fornito la guida, non è necessario alcun file <code>crossdomain.xml</code>. Ma se il servizio si trova su un altro server o se sono coinvolti cluster, sarebbe necessaria la presenza di un file <code>crossdomain.xml</code> . Per ulteriori informazioni sul file crossdomain.xml, consulta <a href="https://kb2.adobe.com/cps/142/tn_14213.html">https://kb2.adobe.com/cps/142/tn_14213.html</a> .</p> </td> 
  </tr> 
  <tr> 
   <td><p>Impostazioni di sicurezza del sistema operativo</p> </td> 
   <td><p>Se è necessario utilizzare la crittografia XML a 192 bit o 256 bit sulle piattaforme Solaris, assicurarsi di installare <code>pkcs11_softtoken_extra.so</code> invece di <code>pkcs11_softtoken.so</code>.</p> </td> 
  </tr> 
 </tbody> 
</table>

## Passaggi successivi all’installazione {#post-installation-steps}

Dopo aver installato AEM Forms su JEE, è importante mantenere periodicamente l’ambiente dal punto di vista della sicurezza.

La sezione seguente descrive in dettaglio le diverse attività consigliate per proteggere il server dei moduli distribuiti.

### Sicurezza AEM Forms {#aem-forms-security}

Le seguenti impostazioni consigliate si applicano ad AEM Forms sul server JEE al di fuori dell’applicazione web amministrativa. Per ridurre i rischi per la sicurezza del server, applica queste impostazioni immediatamente dopo l’installazione di AEM Forms su JEE.

**Patch di sicurezza**

C&#39;è un rischio maggiore che un utente non autorizzato possa accedere al server dell&#39;applicazione se le patch e gli aggiornamenti di sicurezza del fornitore non vengono applicati in modo tempestivo. Verifica le patch di sicurezza prima di applicarle ai server di produzione per garantire la compatibilità e la disponibilità delle applicazioni. Inoltre, crea criteri e procedure per verificare e installare le patch regolarmente. Gli aggiornamenti AEM Forms su JEE si trovano nel sito di download dei prodotti Enterprise.

**Account di servizio (chiavi in mano JBoss solo su Windows)**

AEM Forms su JEE installa un servizio, per impostazione predefinita, utilizzando l&#39;account LocalSystem. L&#39;account utente di LocalSystem integrato ha un alto livello di accessibilità; fa parte del gruppo Administrators. Se un&#39;identità processo di lavoro viene eseguita come account utente di LocalSystem, il processo di lavoro dispone dell&#39;accesso completo all&#39;intero sistema.

Per eseguire l&#39;application server su cui viene distribuito AEM Forms su JEE, utilizzando un account non amministrativo specifico, segui queste istruzioni:

1. In Microsoft Management Console (MMC), creare un utente locale per il servizio server dei moduli con cui eseguire l’accesso:

   * Selezionare **L&#39;utente non può modificare la password**.
   * Nella scheda **Membro di** , accertati che sia elencato il gruppo **Utenti** .

   >[!NOTE]
   >
   >Non è possibile modificare questa impostazione per PDF Generator.

1. Seleziona **Start** > **Impostazioni** > **Strumenti di amministrazione** > **Servizi**.
1. Fai doppio clic su JBoss per AEM Forms su JEE e interrompi il servizio.
1. Nella scheda **Accedi**, seleziona **Questo account**, cerca l&#39;account utente creato e immetti la password dell&#39;account.
1. In MMC, aprire **Impostazioni protezione locale** e selezionare **Criteri locali** > **Assegnazione diritti utente**.
1. Assegna i seguenti diritti all’account utente in cui è in esecuzione il server dei moduli:

   * Nega accesso tramite Servizi terminal
   * Nega accesso locale
   * Accedi come servizio (dovrebbe essere già impostato)

1. Assegna al nuovo account utente le autorizzazioni di modifica per le seguenti directory:
   * **Directory** GDS (Global Document Storage): La posizione della directory GDS viene configurata manualmente durante il processo di installazione di AEM Forms. Se l&#39;impostazione della posizione rimane vuota durante l&#39;installazione, la posizione viene impostata automaticamente su una directory sotto l&#39;installazione dell&#39;application server in `[JBoss root]/server/[type]/svcnative/DocumentStorage`
   * **Directory** CRX-Repository: Il percorso predefinito è  `[AEM-Forms-installation-location]\crx-repository`
   * **Directory** temporanee AEM Forms:
      * (Windows) Percorso TMP o TEMP impostato nelle variabili di ambiente
      * (AIX, Linux o Solaris) Directory home dell&#39;utente registrato
Nei sistemi basati su UNIX, un utente non root può utilizzare la seguente directory come directory temporanea:
      * (Linux) /var/tmp o /usr/tmp
      * (AIX) /tmp o /usr/tmp
      * (Solaris) /var/tmp o /usr/tmp
1. Assegna al nuovo account utente autorizzazioni di scrittura sulle seguenti directory:
   * [JBoss-directory]\standalone\deployment
   * [JBoss-directory]\standalone\
   * [JBoss-directory]\bin\

   >[!NOTE]
   >
   > Percorso di installazione predefinito di JBoss Application Server:
   > * Windows: C:\Adobe\Adobe_Experience_Manager_Forms\jboss
   > * Linux: /opt/jboss/

1. Avvia l&#39;application server.

**Disabilitazione del servlet di avvio di Configuration Manager**

Configuration Manager ha utilizzato un servlet distribuito sul server dell&#39;applicazione per eseguire il bootstrap di AEM Forms sul database JEE. Poiché Configuration Manager accede a questo servlet prima del completamento della configurazione, l’accesso a esso non è stato protetto per gli utenti autorizzati e deve essere disabilitato dopo che Configuration Manager è stato utilizzato per configurare AEM Forms su JEE.

1. Decomprimi il file adobe-livecycle-[appserver].ear.
1. Apri il file META-INF/application.xml .
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
1. Aggiungi un commento a adobe-bootstrapper.war e alla directory adobe-lcm-bootstrapper-redirectory. moduli di guerra come segue:

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

1. Salva e chiudi il file META-INF/application.xml .
1. Zip il file EAR e ridistribuiscilo nel server dell&#39;applicazione.
1. Avvia il server AEM Forms.
1. Digita il seguente URL in un browser per testare la modifica e assicurarti che non funzioni più.

   https://&lt;localhost>:&lt;port>/adobe-bootstrapper/bootstrap

**Blocco dell&#39;accesso remoto all&#39;archivio fonti attendibili**

Configuration Manager consente di caricare una credenziale di estensioni Acrobat Reader DC in AEM Forms sull&#39;archivio di attendibilità JEE. Ciò significa che l&#39;accesso al servizio di credenziali dell&#39;archivio protezione tramite protocolli remoti (SOAP ed EJB) è stato abilitato per impostazione predefinita. Questo accesso non è più necessario dopo aver caricato la credenziale Diritti tramite Configuration Manager o se decidi di utilizzare la console di amministrazione in un secondo momento per gestire le credenziali.

È possibile disabilitare l&#39;accesso remoto a tutti i servizi dell&#39;archivio protezione seguendo i passaggi descritti nella sezione [Disabilitazione dell&#39;accesso remoto non essenziale ai servizi](https://helpx.adobe.com/aem-forms/6-1/hardening-security/configuring-secure-administration-settings-aem.html#disabling_non_essential_remote_access_to_services).

**Disattiva tutti gli accessi anonimi non essenziali**

Alcuni servizi server di forms dispongono di operazioni che possono essere richiamate da un chiamante anonimo. Se l&#39;accesso anonimo a questi servizi non è necessario, disabilitalo seguendo i passaggi descritti in [Disabilitazione dell&#39;accesso anonimo non essenziale ai servizi](https://helpx.adobe.com/aem-forms/6-1/hardening-security/configuring-secure-administration-settings-aem.html#disabling_non_essential_anonymous_access_to_services).

#### Modificare la password amministratore predefinita {#change-the-default-administrator-password}

Quando AEM Forms su JEE è installato, viene configurato un singolo account utente predefinito per l&#39;utente Amministratore avanzato/ login-id Administrator con una password predefinita di *password*. È necessario modificare immediatamente la password utilizzando Gestione configurazione.

1. Digita il seguente URL in un browser web:

   ```java
   https://[host name]:[port]/adminui
   ```

   Il numero di porta predefinito è uno dei seguenti:

   **JBoss:** 8080

   **Server WebLogic:** 7001

   **WebSphere:** 9080.

1. Nel campo **Nome utente**, digita `administrator` e, nel campo **Password**, digita `password`.
1. Fai clic su **Impostazioni** > **Gestione utente** > **Utenti e gruppi**.
1. Digita `administrator` nel campo **Trova** e fai clic su **Trova**.
1. Fai clic su **Amministratore avanzato** dall&#39;elenco degli utenti.
1. Fare clic su **Cambia password** nella pagina Modifica utente.
1. Specifica la nuova password e fai clic su **Salva**.

Inoltre, si consiglia di cambiare la password predefinita per l&#39;amministratore CRX eseguendo i seguenti passaggi:

1. Accedi a `https://[server]:[port]/lc/libs/granite/security/content/useradmin.html` utilizzando il nome utente/password predefinito.
1. Digitare Amministratore nel campo di ricerca e fare clic su **Vai**.
1. Seleziona **Amministratore** dal risultato della ricerca e fai clic sull&#39;icona **Modifica** in basso a destra dell&#39;interfaccia utente.
1. Specifica la nuova password nel campo **Nuova password** e la vecchia password nel campo **Password** .
1. Fai clic sull’icona Salva in basso a destra dell’interfaccia utente.

#### Disattiva generazione WSDL {#disable-wsdl-generation}

La generazione WSDL (Web Service Definition Language) deve essere abilitata solo per gli ambienti di sviluppo in cui la generazione WSDL viene utilizzata dagli sviluppatori per creare le applicazioni client. È possibile disattivare la generazione WSDL in un ambiente di produzione per evitare di esporre i dettagli interni di un servizio.

1. Digita il seguente URL in un browser web:

   ```java
   https://[host name]:[port]/adminui
   ```

1. Fai clic su **Impostazioni > Impostazioni sistema di base > Configurazioni**.
1. Deselezionare **Abilita WSDL** e fare clic su **OK**.

### Protezione del server applicazioni {#application-server-security}

La tabella seguente descrive alcune tecniche per proteggere l&#39;application server dopo l&#39;installazione dell&#39;applicazione AEM Forms on JEE.

<table> 
 <thead> 
  <tr> 
   <th><p>Problema</p> </th> 
   <th><p>Descrizione</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>Console di amministrazione del server applicazioni</p> </td> 
   <td><p>Dopo aver installato, configurato e distribuito AEM Forms su JEE nel server delle applicazioni, devi disattivare l’accesso alle console di amministrazione del server delle applicazioni. Per ulteriori informazioni, consulta la documentazione dell’applicazione server .</p> </td> 
  </tr> 
  <tr> 
   <td><p>Impostazioni dei cookie del server applicazioni</p> </td> 
   <td><p>I cookie dell'applicazione sono controllati dal server dell'applicazione. Durante la distribuzione dell'applicazione, l'amministratore dell'application server può specificare le preferenze relative ai cookie a livello di server o di applicazione. Per impostazione predefinita, le impostazioni del server hanno le preferenze.</p> <p>Tutti i cookie di sessione generati dal server applicazioni devono includere l'attributo <code>HttpOnly</code> . Ad esempio, quando utilizzi JBoss Application Server, puoi modificare l’elemento SessionCookie in <code>httpOnly="true"</code> nel file <code>WEB-INF/web.xml</code>.</p> <p>È possibile limitare l’invio dei cookie tramite solo HTTPS. Di conseguenza, non vengono inviati non crittografati tramite HTTP. Gli amministratori del server applicazioni devono abilitare i cookie sicuri per il server su base globale. Ad esempio, quando utilizzi JBoss Application Server, puoi modificare l’elemento del connettore in <code>secure=true</code> nel file <code>server.xml</code>.</p> <p>Per ulteriori informazioni sulle impostazioni dei cookie, consulta la documentazione del server applicazioni .</p> </td> 
  </tr> 
  <tr> 
   <td><p>Esplorazione delle directory</p> </td> 
   <td><p>Quando un utente richiede una pagina che non esiste o richiede il nome di un regista (la stringa di richiesta termina con una barra (/))), il server applicazioni non deve restituire il contenuto di tale directory. Per evitare questo problema, è possibile disabilitare la navigazione delle directory sul server dell'applicazione. È necessario eseguire questa operazione per l'applicazione della console di amministrazione e per altre applicazioni in esecuzione sul server.</p> <p>Per JBoss, imposta il valore del parametro di inizializzazione degli elenchi della proprietà <code>DefaultServlet</code> su <code>false</code> nel file web.xml, come mostrato in questo esempio:</p> <p>&lt;servlet&gt;</p> <p>&lt;servlet-name&gt;default&lt;/servlet-name&gt;</p> <p>&lt;servlet-class&gt;</p> <p>org.apache.catalina.servlets.DefaultServlet</p> <p>&lt;/servlet-class&gt;</p> <p>&lt;init-param&gt;</p> <p>&lt;param-name&gt;elenchi&lt;/param-name&gt;</p> <p>&lt;param-value&gt;false&lt;/param-value&gt;</p> <p>&lt;/init-param&gt;</p> <p>&lt;load-on-startup&gt;1&lt;/load-on-startup&gt;</p> <p>&lt;/servlet&gt;</p> <p>Per WebSphere, imposta la proprietà <code>directoryBrowsingEnabled</code> nel file ibm-web-ext.xmi su <code>false</code>.</p> <p>Per WebLogic, imposta le proprietà delle directory degli indici nel file weblogic.xml su <code>false</code>, come mostrato in questo esempio:</p> <p>&lt;container-descriptor&gt;</p> <p>&lt;index-directory-enabled&gt;false</p> <p>&lt;/index-directory-enabled&gt;</p> <p>&lt;/container-descriptor&gt;</p> </td> 
  </tr> 
 </tbody> 
</table>

### Protezione del database {#database-security}

Quando si protegge il database, è necessario implementare le misure descritte dal fornitore del database. È necessario allocare un utente del database con le autorizzazioni minime richieste al database concesse per l&#39;utilizzo da AEM Forms su JEE. Ad esempio, non utilizzare un account con privilegi di amministratore del database.

Ad Oracle, l&#39;account di database utilizzato richiede solo i privilegi CONNECT, RESOURCE e CREATE VIEW. Per requisiti simili per altri database, consulta [Preparazione all’installazione di AEM Forms su JEE (Single Server)](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_64).

#### Configurazione della protezione integrata per SQL Server su Windows per JBoss {#configuring-integrated-security-for-sql-server-on-windows-for-jboss}

1. Modifica [JBOSS_HOME]\\standalone\configuration\lc_{datasource.xml} per aggiungere `integratedSecurity=true` all&#39;URL di connessione, come mostrato in questo esempio:

   ```java
    jdbc:sqlserver://<serverhost>:<port>;databaseName=<dbname>;integratedSecurity=true
   ```

1. Aggiungere il file sqljdbc_auth.dll al percorso del sistema Windows sul computer che esegue l&#39;application server. Il file sqljdbc_auth.dll si trova con l&#39;installazione del driver Microsoft SQL JDBC 6.2.1.0.
1. Modifica la proprietà del servizio Windows JBoss (JBoss for AEM Forms on JEE) per Log On As from Local System su un account di accesso con database AEM Forms e un insieme minimo di privilegi. Se si esegue JBoss dalla riga di comando invece che come servizio Windows, non è necessario eseguire questo passaggio.
1. Impostare la protezione per SQL Server dalla modalità **Mixed** a **Solo autenticazione Windows**.

#### Configurazione della sicurezza integrata per SQL Server su Windows per WebLogic {#configuring-integrated-security-for-sql-server-on-windows-for-weblogic}

1. Avvia la console di amministrazione del server WebLogic digitando il seguente URL nella riga URL di un browser Web:

   ```java
   https://[host name]:7001/console
   ```

1. In Cambia centro fare clic su **Blocca e modifica**.
1. In Struttura del dominio, fai clic su *[dominio_base]* > **Servizi** > **JDBC** > **Origini dati** e, nel riquadro di destra, fai clic su **IDP_DS**.
1. Nella schermata successiva, nella scheda **Configurazione** fare clic sulla scheda **Pool di connessioni** e digitare `integratedSecurity=true` nella casella **Proprietà**.
1. In Struttura del dominio, fai clic su **[dominio_base]** > **Servizi** > **JDBC** > **Origini dati** e, nel riquadro di destra, fai clic su **RM_DS**.
1. Nella schermata successiva, nella scheda **Configurazione** fare clic sulla scheda **Pool di connessioni** e digitare `integratedSecurity=true` nella casella **Proprietà**.
1. Aggiungere il file sqljdbc_auth.dll al percorso del sistema Windows sul computer che esegue l&#39;application server. Il file sqljdbc_auth.dll si trova con l&#39;installazione del driver Microsoft SQL JDBC 6.2.1.0.
1. Impostare la protezione per SQL Server dalla modalità **Mixed** a **Solo autenticazione Windows**.

#### Configurazione della protezione integrata per SQL Server su Windows per WebSphere {#configuring-integrated-security-for-sql-server-on-windows-for-websphere}

In WebSphere è possibile configurare la protezione integrata solo quando si utilizza un driver JDBC di SQL Server esterno, non il driver JDBC di SQL Server incorporato con WebSphere.

1. Accedi alla console amministrativa WebSphere.
1. Nella struttura di navigazione, fai clic su **Risorse** > **JDBC** > **Origini dati** e, nel riquadro di destra, fai clic su **IDP_DS**.
1. Nel riquadro a destra, in Proprietà aggiuntive, fare clic su **Proprietà personalizzate**, quindi fare clic su **Nuovo**.
1. Nella casella **Nome**, digitare `integratedSecurity` e digitare **Valore** nella casella `true`.
1. Nella struttura di navigazione, fai clic su **Risorse** > **JDBC** > **Origini dati** e, nel riquadro di destra, fai clic su **RM_DS**.
1. Nel riquadro a destra, in Proprietà aggiuntive, fare clic su **Proprietà personalizzate**, quindi fare clic su **Nuovo**.
1. Nella casella **Nome**, digitare `integratedSecurity` e digitare **Valore** nella casella `true`.
1. Nel computer in cui è installato WebSphere, aggiungere il file sqljdbc_auth.dll al percorso del sistema Windows (C:\Windows). Il file sqljdbc_auth.dll si trova nella stessa posizione dell&#39;installazione del driver Microsoft SQL JDBC 1.2 (il valore predefinito è *[InstallDir]*/sqljdbc_1.2/enu/auth/x86).
1. Seleziona **Start** > **Pannello di controllo Campaign** > **Servizi**, fai clic con il pulsante destro del mouse sul servizio Windows per WebSphere (IBM WebSphere Application Server &lt;version> - &lt;node>) e seleziona **Proprietà**.
1. Nella finestra di dialogo Proprietà fare clic sulla scheda **Accedi** .
1. Seleziona **Questo account** e fornisci le informazioni necessarie per impostare l&#39;account di accesso che desideri utilizzare.
1. Impostare la protezione su SQL Server dalla modalità **Mixed** a **Solo autenticazione di Windows**.

### Protezione dell’accesso a contenuti sensibili nel database {#protecting-access-to-sensitive-content-in-the-database}

Lo schema del database AEM Forms contiene informazioni riservate sulla configurazione del sistema e sui processi aziendali e deve essere nascosto dietro il firewall. Il database deve essere considerato all’interno dello stesso limite di attendibilità del server dei moduli. Per evitare la divulgazione di informazioni e il furto di dati aziendali, il database deve essere configurato dall&#39;amministratore del database (DBA) per consentire l&#39;accesso solo agli amministratori autorizzati.

Come precauzione aggiuntiva, è consigliabile utilizzare strumenti specifici del fornitore del database per crittografare le colonne nelle tabelle contenenti i dati seguenti:

* Chiavi documento Rights Management
* Chiave di crittografia PIN HSM Store attendibile
* Hash password utente locale

Per informazioni sugli strumenti specifici del fornitore, vedere [&quot;Informazioni sulla sicurezza del database&quot;](https://helpx.adobe.com/aem-forms/6-1/hardening-security/general-security-considerations.html#database_security_information).

### Sicurezza LDAP {#ldap-security}

Una directory LDAP (Lightweight Directory Access Protocol) viene generalmente utilizzata da AEM Forms su JEE come origine per le informazioni di utenti e gruppi aziendali e come mezzo per eseguire l&#39;autenticazione tramite password. Assicurati che la tua directory LDAP sia configurata per utilizzare Secure Socket Layer (SSL) e che AEM Forms on JEE sia configurato per accedere alla tua directory LDAP utilizzando la sua porta SSL.

#### Rifiuto del servizio LDAP {#ldap-denial-of-service}

Un attacco comune che utilizza LDAP coinvolge un aggressore che deliberatamente non riesce ad autenticarsi più volte. Questo costringe LDAP Directory Server a bloccare un utente da tutti i servizi relativi a LDAP.

È possibile impostare il numero di tentativi di errore e il successivo tempo di blocco che AEM Forms implementa quando un utente ripetutamente non riesce ad autenticarsi in AEM Forms. In Console di amministrazione, scegli valori bassi. Quando si seleziona il numero di tentativi non riusciti, è importante comprendere che dopo tutti i tentativi eseguiti, AEM Forms blocca l&#39;utente prima che il server di directory LDAP lo faccia.

#### Imposta blocco account automatico {#set-automatic-account-locking}

1. Accedi alla console di amministrazione.
1. Fai clic su **Impostazioni** > **Gestione utente** > **Gestione dominio**.
1. In Impostazioni di blocco account automatico, impostare **Numero massimo di errori di autenticazione consecutivi** su un numero basso, ad esempio 3.
1. Fai clic su **Salva**.

### Controllo e registrazione {#auditing-and-logging}

L’utilizzo corretto e sicuro del controllo e della registrazione delle applicazioni può garantire che la sicurezza e altri eventi anomali vengano tracciati e rilevati il più rapidamente possibile. L&#39;utilizzo efficace del controllo e della registrazione all&#39;interno di un&#39;applicazione include elementi come il tracciamento degli accessi riusciti e non riusciti, nonché eventi applicativi chiave come la creazione o l&#39;eliminazione di record chiave.

Puoi utilizzare il controllo per rilevare molti tipi di attacchi, tra cui:

* Attacchi di password con forza bruta
* Negazione di attacchi di servizio
* Iniezione di input ostili e classi correlate di attacchi di script

Questa tabella descrive le tecniche di controllo e registrazione che è possibile utilizzare per ridurre le vulnerabilità del server.

<table> 
 <thead> 
  <tr> 
   <th><p>Problema</p> </th> 
   <th><p>Descrizione</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>ACL del file di registro</p> </td> 
   <td><p>Imposta l'AEM Forms appropriato sugli elenchi di controllo dell'accesso ai file di registro JEE (ACL).</p> <p>L'impostazione delle credenziali appropriate aiuta a impedire agli aggressori di eliminare i file.</p> <p>Le autorizzazioni di sicurezza nella directory dei file di registro devono essere Controllo completo per gli amministratori e i gruppi SYSTEM. L'account utente AEM Forms deve disporre solo delle autorizzazioni di lettura e scrittura.</p> </td> 
  </tr> 
  <tr> 
   <td><p>ridondanza dei file di registro</p> </td> 
   <td><p>Se le risorse lo consentono, inviare i registri a un altro server in tempo reale che non è accessibile dall'autore dell'attacco (solo scrittura) utilizzando Syslog, Tivoli, Microsoft Operations Manager (MOM) Server o un altro meccanismo.</p> <p>La protezione dei log in questo modo aiuta a prevenire manomissioni. Inoltre, l'archiviazione dei registri in un archivio centrale facilita la correlazione e il monitoraggio (ad esempio, se sono in uso più server di moduli e si verifica un attacco di impostazione della password in più computer in cui ogni computer viene interrogato per una password).</p> </td> 
  </tr> 
 </tbody> 
</table>

### Abilitare un utente non amministratore all&#39;esecuzione di PDF Generator

È possibile abilitare un utente non amministratore all’utilizzo di PDF Generator. Normalmente, solo gli utenti con privilegi amministrativi possono utilizzare PDF Generator. Esegui i seguenti passaggi per abilitare un utente non amministratore all’esecuzione di PDF Generator:

1. Crea un nome di variabile di ambiente PDFG_NON_ADMIN_ENABLED.

1. Imposta il valore della variabile su TRUE.

1. Riavvia l&#39;istanza AEM Forms.

## Configurazione di AEM Forms su JEE per l’accesso oltre l’azienda {#configuring-aem-forms-on-jee-for-access-beyond-the-enterprise}

Dopo aver installato AEM Forms su JEE, è importante mantenere periodicamente la sicurezza dell’ambiente. Questa sezione descrive le attività consigliate per mantenere la sicurezza di AEM Forms sul server di produzione JEE.

### Configurazione di un proxy inverso per l&#39;accesso al web {#setting-up-a-reverse-proxy-for-web-access}

È possibile utilizzare un *proxy inverso* per garantire che un set di URL per AEM Forms sulle applicazioni web JEE sia disponibile per gli utenti esterni che interni. Questa configurazione è più sicura che consente agli utenti di connettersi direttamente al server applicativo su cui AEM Forms on JEE è in esecuzione. Il proxy inverso esegue tutte le richieste HTTP per l&#39;application server che esegue AEM Forms su JEE. Gli utenti hanno solo accesso di rete al proxy inverso e possono solo tentare connessioni URL supportate dal proxy inverso.

**AEM Forms sugli URL principali JEE da utilizzare con il server reverse proxy**

I seguenti URL radice dell&#39;applicazione per ogni applicazione Web AEM Forms su JEE. È necessario configurare il proxy inverso solo per esporre gli URL per la funzionalità dell&#39;applicazione web che si desidera fornire agli utenti finali.

Alcuni URL vengono evidenziati come applicazioni web rivolte all’utente finale. Evita di esporre altri URL per Configuration Manager per l&#39;accesso a utenti esterni tramite il proxy inverso.

<table> 
 <thead> 
  <tr> 
   <th><p>URL principale</p> </th> 
   <th><p>Finalità e/o applicazione Web associata</p> </th> 
   <th><p>Interfaccia basata sul web</p> </th> 
   <th><p>Accesso dell'utente finale</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>/ReaderExtensions/*</p> </td> 
   <td><p>Acrobat Reader DC estende l’applicazione Web per l’utente finale per l’applicazione dei diritti di utilizzo ai documenti PDF</p> </td> 
   <td><p>Sì</p> </td> 
   <td><p>Sì</p> </td> 
  </tr> 
  <tr> 
   <td><p>/edc/*</p> </td> 
   <td><p>applicazione Web per l'utente finale del Rights Management</p> </td> 
   <td><p>Sì</p> </td> 
   <td><p>Sì</p> </td> 
  </tr> 
  <tr> 
   <td><p>/edcws/*</p> </td> 
   <td><p>URL del servizio Web per Rights Management</p> </td> 
   <td><p>No</p> </td> 
   <td><p>Sì</p> </td> 
  </tr> 
  <tr> 
   <td><p>/pdfgui/*</p> </td> 
   <td><p>applicazione Web di amministrazione PDF Generator</p> </td> 
   <td><p>Sì</p> </td> 
   <td><p>Sì</p> </td> 
  </tr> 
  <tr> 
   <td><p>/Workspace/*</p> </td> 
   <td><p>Applicazione web per l’utente finale di Workspace</p> </td> 
   <td><p>Sì</p> </td> 
   <td><p>Sì</p> </td> 
  </tr> 
  <tr> 
   <td><p>/workspace-server/*</p> </td> 
   <td><p>Servlet di Workspace e servizi dati richiesti dall’applicazione client di Workspace</p> </td> 
   <td><p>Sì</p> </td> 
   <td><p>Sì</p> </td> 
  </tr> 
  <tr> 
   <td><p>/adobe-bootstrapper/*</p> </td> 
   <td><p>Servlet per avviare l’AEM Forms sull’archivio JEE</p> </td> 
   <td><p>No</p> </td> 
   <td><p>No</p> </td> 
  </tr> 
  <tr> 
   <td><p>/soap/*</p> </td> 
   <td><p>Pagina delle informazioni per i servizi Web del server dei moduli</p> </td> 
   <td><p>No</p> </td> 
   <td><p>No</p> </td> 
  </tr> 
  <tr> 
   <td><p>/soap/services/*</p> </td> 
   <td><p>URL del servizio Web per tutti i servizi server dei moduli</p> </td> 
   <td><p>No</p> </td> 
   <td><p>No</p> </td> 
  </tr> 
  <tr> 
   <td><p>/edc/admin/*</p> </td> 
   <td><p>applicazione Web amministrazione Rights Management</p> </td> 
   <td><p>Sì</p> </td> 
   <td><p>No</p> </td> 
  </tr> 
  <tr> 
   <td><p>/adminui/*</p> </td> 
   <td><p>Pagina principale della console di amministrazione</p> </td> 
   <td><p>Sì</p> </td> 
   <td><p>No</p> </td> 
  </tr> 
  <tr> 
   <td><p>/TruststoreComponent/</p> <p>protetto/*</p> </td> 
   <td><p>Pagine di amministrazione di Trust Store</p> </td> 
   <td><p>Sì</p> </td> 
   <td><p>No</p> </td> 
  </tr> 
  <tr> 
   <td><p>/FormsIVS/*</p> </td> 
   <td><p>Applicazione Forms IVS per la verifica e il debug del rendering del modulo</p> </td> 
   <td><p>Sì</p> </td> 
   <td><p>No</p> </td> 
  </tr> 
  <tr> 
   <td><p>/OutputIVS/*</p> </td> 
   <td><p>Applicazione IVS di output per la verifica e il debug del servizio di output</p> </td> 
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
   <td><p>Pagine di amministrazione di output</p> </td> 
   <td><p>Sì</p> </td> 
   <td><p>No</p> </td> 
  </tr> 
  <tr> 
   <td><p>/FormServer/*</p> </td> 
   <td><p>File delle applicazioni web Forms</p> </td> 
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
   <td><p>Pagine di amministrazione Forms</p> </td> 
   <td><p>Sì</p> </td> 
   <td><p>No</p> </td> 
  </tr> 
  <tr> 
   <td><p>/repository/*</p> </td> 
   <td><p>URL per l'accesso a WebDAV (debugging)</p> </td> 
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
   <td><p>Pagine di supporto per il resto</p> </td> 
   <td><p>Sì</p> </td> 
   <td><p>No</p> </td> 
  </tr> 
  <tr> 
   <td><p>/CoreSystemConfig/*</p> </td> 
   <td><p>Pagina delle impostazioni di configurazione di base di AEM Forms su JEE</p> </td> 
   <td><p>Sì</p> </td> 
   <td><p>No</p> </td> 
  </tr> 
  <tr> 
   <td><p>/um/</p> </td> 
   <td><p>Autenticazione della gestione utenti</p> </td> 
   <td><p>No</p> </td> 
   <td><p>Sì</p> </td> 
  </tr> 
  <tr> 
   <td><p>/um/*</p> </td> 
   <td><p>Interfaccia di amministrazione di User Management</p> </td> 
   <td><p>Sì</p> </td> 
   <td><p>No</p> </td> 
  </tr> 
  <tr> 
   <td><p>/DocumentManager/*</p> </td> 
   <td><p>Caricamento e download di documenti da elaborare per l’accesso agli endpoint remoti, agli endpoint WSDL SOAP e all’SDK Java tramite trasporto SOAP o EJB con documenti HTTP abilitati.</p> </td> 
   <td><p>Sì</p> </td> 
   <td><p>Sì</p> </td> 
  </tr> 
 </tbody> 
</table>

## Protezione da attacchi di falsificazione di richieste intersito {#protecting-from-cross-site-request-forgery-attacks}

Un attacco CSRF (Cross-Site Request Forgery) sfrutta la fiducia che un sito web ha per l&#39;utente, per trasmettere comandi non autorizzati e non intenzionali da parte dell&#39;utente. L&#39;attacco è configurato includendo un collegamento o uno script in una pagina web, o un URL in un messaggio e-mail, per accedere a un altro sito a cui l&#39;utente è già stato autenticato.

Ad esempio, puoi aver effettuato l’accesso ad Admin Console mentre navighi su un altro sito web. Una delle pagine web può includere un tag immagine HTML con un attributo `src` che esegue il targeting di uno script lato server sul sito web della vittima. Sfruttando il meccanismo di autenticazione della sessione basato su cookie fornito dai browser web, il sito web attaccante può inviare richieste dannose a questo script lato server vittima, mascherato come utente legittimo. Per ulteriori esempi, consulta [https://www.owasp.org/index.php/Cross-Site_Request_Forgery_(CSRF)#Examples](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_(CSRF)#Examples).

Le seguenti caratteristiche sono comuni al CSRF:

* Coinvolgere siti che si basano sull&#39;identità di un utente.
* Sfruttare la fiducia del sito in quell&#39;identità.
* Associa il browser dell’utente all’invio di richieste HTTP a un sito di destinazione.
* Richiedi HTTP con effetti collaterali.

AEM Forms su JEE utilizza la funzione Filtro referente per bloccare gli attacchi CSRF. In questa sezione vengono utilizzati i seguenti termini per descrivere il meccanismo di filtraggio dei referenti:

* **Referente autorizzato:** un referente è l’indirizzo della pagina sorgente che invia una richiesta al server. Per le pagine o i moduli JSP, i referenti sono in genere la pagina precedente della cronologia di navigazione. Per riferimento per le immagini si intendono in genere le pagine sulle quali vengono visualizzate le immagini. Puoi identificare il referente a cui è consentito l’accesso alle risorse del server aggiungendo tali risorse all’elenco Riferimenti consentiti .
* **Eccezioni referente consentite:** puoi limitare l’ambito di accesso per un particolare referente nel tuo elenco Riferimenti consentiti. Per applicare questa restrizione è possibile aggiungere singoli percorsi di quel referente all&#39;elenco Eccezioni referente consentite. Le richieste provenienti da percorsi nell’elenco Eccezioni referente consentite non possono richiamare alcuna risorsa sul server dei moduli. È possibile definire eccezioni referente consentite per un&#39;applicazione specifica e utilizzare un elenco globale di eccezioni applicabili a tutte le applicazioni.
* **URI consentiti:** si tratta di un elenco di risorse da distribuire senza controllare l’intestazione del referente. È possibile aggiungere a questo elenco le risorse, ad esempio le pagine della guida, che non determinano modifiche allo stato del server. Le risorse nell’elenco URI consentiti non vengono mai bloccate dal filtro referente indipendentemente da chi sia il referente.
* **Referente Null:** una richiesta server che non è associata o non proviene da una pagina web padre viene considerata come una richiesta da un Referrer Null. Ad esempio, quando apri una nuova finestra del browser, digita un indirizzo e premi invio, il referente inviato al server è nullo. Anche un&#39;applicazione desktop (.NET o SWING) che effettua una richiesta HTTP a un server Web invia un Referrer Null al server.

### Filtro referente {#referer-filtering}

Il processo di filtraggio referente può essere descritto come segue:

1. Il server dei moduli controlla il metodo HTTP utilizzato per la chiamata:

   1. Se si tratta di POST, il server dei moduli esegue il controllo di intestazione Referrer.
   1. Se è GET, il server dei moduli ignora il controllo Referrer, a meno che *CSRF_CHECK_GETS* non sia impostato su true, nel qual caso esegue il controllo di intestazione Referrer. *CSRF_CHECK_* GETSè specificato nel file  *web.* xmlper la tua applicazione.

1. Il server dei moduli controlla se l’URI richiesto esiste inserire nell&#39;elenco Consentiti:

   1. Se l’URI viene inserito nell&#39;elenco Consentiti, il server accetta la richiesta.
   1. Se l’URI richiesto non viene inserito nell&#39;elenco Consentiti, il server recupera il referente della richiesta.

1. Se nella richiesta è presente un referente, il server controlla se si tratta di un referente consentito. Se consentito, il server verifica la presenza di un&#39;eccezione referente:

   1. Se si tratta di un&#39;eccezione, la richiesta viene bloccata.
   1. Se non si tratta di un’eccezione, la richiesta viene passata.

1. Se nella richiesta non è presente alcun referente, il server controlla se è consentito un referente Null:

   1. Se è consentito un Referente Null, la richiesta viene trasmessa.
   1. Se non è consentito un referente Null, il server controlla se l’URI richiesto è un’eccezione per il referente Null e gestisce la richiesta di conseguenza.

### Gestione del filtro referente {#managing-referer-filtering}

AEM Forms su JEE fornisce un filtro referente per specificare referente che può accedere alle risorse del server. Per impostazione predefinita, il filtro Referrer non filtra le richieste che utilizzano un metodo HTTP sicuro, ad esempio, a meno che *CSRF_CHECK_GETS* non sia impostato su true. Se il numero di porta per una voce Referente consentito è impostato su 0, AEM Forms su JEE consentirà tutte le richieste con Referrer da tale host, indipendentemente dal numero di porta. Se non viene specificato alcun numero di porta, sono consentite solo richieste dalla porta predefinita 80 (HTTP) o dalla porta 443 (HTTPS). Filtro referente è disabilitato se tutte le voci nell’elenco Riferimenti consentiti vengono eliminate.

Quando si installa Document Services per la prima volta, l&#39;elenco Riferimenti consentiti viene aggiornato con l&#39;indirizzo del server in cui è installato Document Services. Le voci per il server includono il nome del server, l&#39;indirizzo IPv4, l&#39;indirizzo IPv6 se IPv6 è abilitato, l&#39;indirizzo di loopback e una voce localhost. I nomi aggiunti all’elenco Riferimenti consentiti vengono restituiti dal sistema operativo Host. Ad esempio, un server con indirizzo IP 10.40.54.187 includerà le seguenti voci: `https://server-name:0, https://10.40.54.187:0, https://127.0.0.1:0, http://localhost:0`. Per qualsiasi nome non qualificato restituito dal sistema operativo host (nomi che non hanno indirizzo IPv4, indirizzo IPv6 o nome di dominio qualificato) inserì nell&#39;elenco Consentiti non viene aggiornato. Modificare l&#39;elenco Riferimenti consentiti in base all&#39;ambiente aziendale. Non distribuire il server dei moduli nell’ambiente di produzione con l’elenco Riferimenti consentiti predefinito. Dopo aver modificato uno qualsiasi degli URI, eccezioni di riferimento o riferimenti consentiti, assicurati di riavviare il server per rendere effettive le modifiche.

**Gestione dell’elenco dei referenti consentiti**

Puoi gestire l’elenco Riferimenti consentiti dall’interfaccia di gestione utenti di Admin Console. L’interfaccia User Management (Interfaccia di gestione utente) offre le funzionalità necessarie per creare, modificare o eliminare l’elenco. Per ulteriori informazioni sull’utilizzo dell’elenco Riferimenti consentiti, consulta la sezione * [Prevenzione degli attacchi CSRF](/help/forms/using/admin-help/preventing-csrf-attacks.md)* della *guida di amministrazione* .

**Gestione dell’eccezione di riferimento consentita e degli elenchi di URI consentiti**

AEM Forms su JEE fornisce API per gestire l’elenco di eccezioni referente consentite e l’elenco di URI consentiti. Puoi utilizzare queste API per recuperare, creare, modificare o eliminare l’elenco. Di seguito è riportato un elenco delle API disponibili:

* createAllowedURIsList
* getAllowedURIsList
* updateAllowedURIsList
* deleteAllowedURIsList
* addAllowedRefererExceptions
* getAllowedRefererExceptions
* updateAllowedRefererExceptions
* deleteAllowedRefererExceptions

Per ulteriori informazioni sulle API, consulta la documentazione di riferimento per le API di AEM Forms on JEE* .

Utilizzare l&#39;elenco ***LC_GLOBAL_ALLOWED_REFERER_EXCEPTION*** per Eccezioni referente consentite a livello globale, cioè per definire le eccezioni applicabili a tutte le applicazioni. Questo elenco contiene solo URI con un percorso assoluto (ad es. `/index.html`) o un percorso relativo (ad esempio `/sample/`). Puoi anche aggiungere un’espressione regolare alla fine di un URI relativo, ad esempio `/sample/(.)*`.

L&#39;ID elenco ***LC_GLOBAL_ALLOWED_REFERER_EXCEPTION*** è definito come una costante nella classe `UMConstants` dello spazio dei nomi `com.adobe.idp.um.api`, disponibile in `adobe-usermanager-client.jar`. Puoi utilizzare le API di AEM Forms per creare, modificare o modificare questo elenco. Ad esempio, per creare l’elenco Eccezioni referente globale consentite utilizza:

```java
addAllowedRefererExceptions(UMConstants.LC_GLOBAL_ALLOWED_REFERER_EXCEPTION, Arrays.asList("/index.html", "/sample/(.)*"))
```

Utilizzare l&#39;elenco ***CSRF_ALLOWED_REFERER_EXCEPTIONS*** per le eccezioni specifiche dell&#39;applicazione.

**Disattivazione del filtro referente**

Nel caso in cui il filtro referente blocchi completamente l’accesso al server dei moduli e non sia possibile modificare l’elenco Riferimenti consentiti, è possibile aggiornare lo script di avvio del server e disattivare Filtro referente.

Includi l&#39;argomento `-Dlc.um.csrffilter.disabled=true` JAVA nello script di avvio e riavvia il server. Assicurati di eliminare l’argomento JAVA dopo aver riconfigurato in modo appropriato l’elenco Riferimenti consentiti .

**Filtro referente per file WAR personalizzati**

Potresti aver creato file WAR personalizzati da utilizzare con AEM Forms su JEE per soddisfare i tuoi requisiti aziendali. Per abilitare il filtro referente per i file WAR personalizzati, includi ***adobe-usermanager-client.jar*** nel percorso classe per WAR e includi una voce di filtro nel file* web.xml* con i seguenti parametri:

**CSRF_CHECK_** GETScontrolla il controllo Referrer sulle richieste GET. Se questo parametro non è definito, il valore predefinito è impostato su false. Includi questo parametro solo se desideri filtrare le richieste GET.

**CSRF_ALLOWED_REFERER_** EXCEPTIONSè l&#39;ID dell&#39;elenco Eccezioni referente consentite. Il filtro referente impedisce che le richieste provenienti da referenti nell’elenco identificato dall’ID elenco richiamino qualsiasi risorsa sul server dei moduli.

**CSRF_ALLOWED_URIS_LIST_** NAMEè l’ID dell’elenco URI consentiti. Il filtro referente non blocca le richieste per nessuna delle risorse nell’elenco identificate dall’ID elenco, indipendentemente dal valore dell’intestazione Referrer nella richiesta.

**CSRF_ALLOW_NULL_** REFERERcontrolla il comportamento del filtro referente quando il referente è nullo o non presente. Se questo parametro non è definito, il valore predefinito è impostato su false. Includere questo parametro solo se si desidera consentire referenti Null. Consentire ai referrer nulli di consentire alcuni tipi di attacchi Cross Site Request Forgery.

**CSRF_NULL_REFERER_** EXCEPTIONSè un elenco degli URI per i quali non viene eseguito un controllo Referrer quando il Referrer è nullo. Questo parametro è abilitato solo quando *CSRF_ALLOW_NULL_REFERER* è impostato su false. Separa più URI nell’elenco con una virgola.

Di seguito è riportato un esempio della voce di filtro nel file *web.xml* per un file ***SAMPLE*** WAR:

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

Se le richieste server legittime sono bloccate dal filtro CSRF, prova una delle seguenti operazioni:

* Se la richiesta rifiutata dispone di un’intestazione Referrer, considera attentamente l’aggiunta di tale intestazione all’elenco Riferimenti consentiti. Aggiungi solo referente di cui sei fidato.
* Se la richiesta rifiutata non dispone di un&#39;intestazione Referrer, modifica l&#39;applicazione client per includere un&#39;intestazione Referrer.
* Se il client può funzionare in un browser, prova quel modello di distribuzione.
* Come ultima risorsa, puoi aggiungere la risorsa all’elenco URI consentiti . Questa impostazione non è consigliata.

## Configurazione sicura della rete {#secure-network-configuration}

Questa sezione descrive i protocolli e le porte richiesti da AEM Forms su JEE e fornisce raccomandazioni per la distribuzione di AEM Forms su JEE in una configurazione di rete sicura.

### Protocolli di rete utilizzati da AEM Forms su JEE {#network-protocols-used-by-aem-forms-on-jee}

Quando si configura un&#39;architettura di rete sicura come descritto nella sezione precedente, per l&#39;interazione tra AEM Forms su JEE e altri sistemi nella rete aziendale sono necessari i seguenti protocolli di rete.

<table> 
 <thead> 
  <tr> 
   <th><p>Protocollo</p> </th> 
   <th><p>Utilizzo</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>HTTP</p> </td> 
   <td> 
    <ul> 
     <li><p>Nel browser vengono visualizzate le applicazioni Web di Configuration Manager e dell'utente finale</p> </li> 
     <li><p>Tutte le connessioni SOAP</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>SOAP</p> </td> 
   <td> 
    <ul> 
     <li><p>Applicazioni client di servizi Web, ad esempio applicazioni .NET</p> </li> 
     <li><p>Adobe Reader® utilizza SOAP per AEM Forms sui servizi Web del server JEE</p> </li> 
     <li><p>Le applicazioni Adobe Flash® utilizzano SOAP per i servizi Web per server forms</p> </li> 
     <li><p>Chiamate AEM Forms on JEE SDK quando utilizzate in modalità SOAP</p> </li> 
     <li><p>Ambiente di progettazione di Workbench</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>RMI</p> </td> 
   <td><p>Chiamate AEM Forms on JEE SDK quando utilizzate in modalità Enterprise JavaBeans (EJB)</p> </td> 
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
   <td><p>File UNC IO</p> </td> 
   <td><p>AEM Forms sul monitoraggio JEE delle cartelle controllate per l'input a un servizio (endpoint cartelle controllate)</p> </td> 
  </tr> 
  <tr> 
   <td><p>LDAP</p> </td> 
   <td> 
    <ul> 
     <li><p>Sincronizzazione delle informazioni organizzative relative a utenti e gruppi in una directory</p> </li> 
     <li><p>Autenticazione LDAP per gli utenti interattivi</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>JDBC</p> </td> 
   <td> 
    <ul> 
     <li><p>Query e chiamate di procedura effettuate a un database esterno durante l'esecuzione di un processo utilizzando il servizio JDBC</p> </li> 
     <li><p>Accesso interno AEM Forms sull’archivio JEE</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>WebDAV</p> </td> 
   <td><p>Consente la navigazione remota dell'archivio AEM Forms in fase di progettazione JEE (moduli, frammenti e così via) da parte di qualsiasi client WebDAV</p> </td> 
  </tr> 
  <tr> 
   <td><p>AMF</p> </td> 
   <td><p>Adobe di applicazioni di Flash, in cui AEM Forms sui servizi server JEE è configurato con un endpoint remoto</p> </td> 
  </tr> 
  <tr> 
   <td><p>JMX</p> </td> 
   <td><p>AEM Forms su JEE espone MBeans per il monitoraggio utilizzando JMX</p> </td> 
  </tr> 
 </tbody> 
</table>

### Porte per server applicazioni {#ports-for-application-servers}

Questa sezione descrive le porte predefinite (e gli intervalli di configurazione alternativi) per ogni tipo di server applicazioni supportato. Queste porte devono essere abilitate o disabilitate nel firewall interno, a seconda della funzionalità di rete che si desidera consentire ai client che si connettono al server applicazioni che esegue AEM Forms su JEE.

>[!NOTE]
>
>Per impostazione predefinita, il server espone diversi MBeans JMX nello spazio dei nomi adobe.com. Vengono esposte solo le informazioni utili per il monitoraggio dello stato del server. Tuttavia, per evitare la divulgazione delle informazioni, è necessario impedire ai chiamanti in una rete non attendibile di cercare MBeans JMX e di accedere alle metriche di integrità.

**Porte JBoss**

<table> 
 <thead> 
  <tr> 
   <th><p>Scopo</p> </th> 
   <th><p>Porta</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>Accesso alle applicazioni web</p> </td> 
   <td><p>[JBOSS_Root]/standalone/configuration/lc_[database].xml</p> <p>Porta connettore HTTP/1.1 8080</p> <p>Porta connettore AJP 1.3 8009</p> <p>Porta del connettore SSL/TLS 8443</p> </td> 
  </tr> 
  <tr> 
   <td><p>Supporto CORBA</p> </td> 
   <td><p>[radice JBoss]/server/all/conf/jacorb.properties</p> <p>OAPort 3528</p> <p>OASSLPort 3529</p> </td> 
  </tr> 
 </tbody> 
</table>

**Porte WebLogic**

<table> 
 <thead> 
  <tr> 
   <th><p>Scopo</p> </th> 
   <th><p>Porta</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>Accesso alle applicazioni web</p> </td> 
   <td> 
    <ul> 
     <li><p>Porta di ascolto di Admin Server: Il valore predefinito è 7001</p> </li> 
     <li><p>Porta di ascolto SSL di Admin Server: Il valore predefinito è 7002</p> </li> 
     <li><p>Porta configurata per Managed Server, ad esempio 8001</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>Le porte di amministrazione WebLogic non sono necessarie per accedere ad AEM Forms su JEE</p> </td> 
   <td> 
    <ul> 
     <li><p>Porta di ascolto del server gestito: Configurabile da 1 a 65534</p> </li> 
     <li><p>Porta di ascolto SSL del server gestito: Configurabile da 1 a 65534</p> </li> 
     <li><p>Porta di ascolto di Node Manager: Il valore predefinito è 5556</p> </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>

**Porte WebSphere**

Per informazioni sulle porte WebSphere richieste da AEM Forms su JEE, passare all&#39;impostazione del numero di porta nell&#39;interfaccia utente di WebSphere Application Server.

### Configurazione di SSL {#configuring-ssl}

Facendo riferimento all&#39;architettura fisica descritta nella sezione [AEM Forms sull&#39;architettura fisica JEE](hardening-aem-forms-jee-environment.md#aem-forms-on-jee-physical-architecture), è necessario configurare SSL per tutte le connessioni che si intende utilizzare. In particolare, tutte le connessioni SOAP devono essere eseguite su SSL per impedire l’esposizione delle credenziali utente su una rete.

Per istruzioni su come configurare SSL su JBoss, WebLogic e WebSphere, consulta &quot;Configurazione di SSL&quot; nella [guida di amministrazione](https://www.adobe.com/go/learn_aemforms_admin_64).

Per istruzioni su come importare certificati in JVM (Java Virtual Machine) configurato per un server AEM Forms, consulta la sezione Autenticazione reciproca in [Guida di AEM Forms Workbench](http://www.adobe.com/go/learn_aemforms_workbench_65).

### Configurazione del reindirizzamento SSL {#configuring-ssl-redirect}

Dopo aver configurato l’application server per supportare SSL, è necessario assicurarsi che tutto il traffico HTTP verso le applicazioni e i servizi sia applicato per utilizzare la porta SSL.

Per configurare il reindirizzamento SSL per WebSphere o WebLogic, consulta la documentazione del server applicazioni.

1. Apri il prompt dei comandi, accedi alla directory /JBOSS_HOME/standalone/configuration ed esegui il seguente comando:

   `keytool -genkey -alias jboss7 -keyalg RSA -keystore server.keystore -validity 10950`

1. Apri il file JBOSS_HOME/standalone/configuration/standalone.xml per la modifica.

   Dopo l&#39;elemento &lt;sottosistema xmlns=&quot;urn:jboss:domain:web:1.1&quot; native=&quot;false&quot; default-virtual-server=&quot;default-host&quot;> , aggiungi i seguenti dettagli:

   &lt;connector name=&quot;https&quot; protocol=&quot;HTTP/1.1&quot; scheme=&quot;https&quot; socket-binding=&quot;https&quot; enabled=&quot;true&quot; secure=&quot;true&quot; />

1. Aggiungi il seguente codice nell’elemento del connettore https:

   ```xml
   <connector name="https" protocol="HTTP/1.1" scheme="https" socket-binding="https" secure="true" enabled="true"> 
    <ssl name="jboss7_ssl" key-alias="jboss71" password="Tibco321" certificate-key-file="../standalone/configuration/server.keystore" protocol="TLSv1"/> 
    </connector>
   ```

   Salvare e chiudere il file standalone.xml.

## Raccomandazioni per la protezione specifiche per Windows {#windows-specific-security-recommendations}

Questa sezione contiene consigli di sicurezza specifici per Windows quando viene utilizzato per eseguire AEM Forms su JEE.

### Account di servizio JBoss {#jboss-service-accounts}

L&#39;installazione chiavi in mano di AEM Forms su JEE imposta un account di servizio, per impostazione predefinita, utilizzando l&#39;account di sistema locale. L&#39;account utente del sistema locale integrato dispone di un livello elevato di accessibilità; fa parte del gruppo Administrators. Se l&#39;identità di un processo di lavoro viene eseguita come account utente del sistema locale, tale processo di lavoro dispone dell&#39;accesso completo all&#39;intero sistema.

#### Eseguire l&#39;application server utilizzando un account non amministrativo {#run-the-application-server-using-a-non-administrative-account}

1. In Microsoft Management Console (MMC), creare un utente locale per il servizio server dei moduli con cui eseguire l’accesso:

   * Selezionare **L&#39;utente non può modificare la password**.
   * Nella scheda **Membro di** , assicurati che il gruppo Utenti sia elencato.

1. Seleziona **Impostazioni** > **Strumenti di amministrazione** > **Servizi**.
1. Fare doppio clic sul servizio server applicazioni e arrestare il servizio.
1. Nella scheda **Accedi**, seleziona **Questo account**, cerca l&#39;account utente creato e immetti la password dell&#39;account.
1. Nella finestra Impostazioni protezione locale, in Assegnazione diritti utente, assegnare i seguenti diritti all&#39;account utente in cui è in esecuzione il server dei moduli:

   * Nega accesso tramite Servizi terminal
   * Nega accesso a locallyxx
   * Accedi come servizio (dovrebbe essere già impostato)

1. Assegna al nuovo account utente le autorizzazioni di modifica per le seguenti directory:
   * **Directory** GDS (Global Document Storage): La posizione della directory GDS viene configurata manualmente durante il processo di installazione di AEM Forms. Se l&#39;impostazione della posizione rimane vuota durante l&#39;installazione, la posizione viene impostata automaticamente su una directory sotto l&#39;installazione dell&#39;application server in `[JBoss root]/server/[type]/svcnative/DocumentStorage`
   * **Directory** CRX-Repository: Il percorso predefinito è  `[AEM-Forms-installation-location]\crx-repository`
   * **Directory** temporanee AEM Forms:
      * (Windows) Percorso TMP o TEMP impostato nelle variabili di ambiente
      * (AIX, Linux o Solaris) Directory home dell&#39;utente registrato
Nei sistemi basati su UNIX, un utente non root può utilizzare la seguente directory come directory temporanea:
      * (Linux) /var/tmp o /usr/tmp
      * (AIX) /tmp o /usr/tmp
      * (Solaris) /var/tmp o /usr/tmp
1. Assegna al nuovo account utente autorizzazioni di scrittura sulle seguenti directory:
   * [JBoss-directory]\standalone\deployment
   * [JBoss-directory]\standalone\
   * [JBoss-directory]\bin\

   >[!NOTE]
   >
   > Percorso di installazione predefinito di JBoss Application Server:
   > * Windows: C:\Adobe\Adobe_Experience_Manager_Forms\jboss
   > * Linux: /opt/jboss/.


1. Avviare il servizio server applicazioni.

### Sicurezza del file system {#file-system-security}

AEM Forms su JEE utilizza il file system nei seguenti modi:

* Memorizza i file temporanei utilizzati durante l&#39;elaborazione dell&#39;input e dell&#39;output del documento
* Memorizza i file nell&#39;archivio globale utilizzati per supportare i componenti della soluzione installati
* Le cartelle controllate memorizzano i file eliminati utilizzati come input per un servizio da un percorso di cartella di un file system

Quando si utilizzano cartelle controllate come modo per inviare e ricevere documenti con un servizio server forms, prendere precauzioni extra con la sicurezza del file system. Quando un utente rilascia del contenuto nella cartella controllata, questo viene esposto attraverso la cartella controllata. In questo caso, il servizio non autentica l&#39;utente finale effettivo. Al contrario, si basa sulla sicurezza a livello di ACL e Share per essere impostato a livello di cartella per determinare chi può richiamare efficacemente il servizio.

## Raccomandazioni per la sicurezza specifiche per JBoss {#jboss-specific-security-recommendations}

Questa sezione contiene raccomandazioni di configurazione dell&#39;application server specifiche per JBoss 7.0.6 quando utilizzato per eseguire AEM Forms su JEE.

### Disattiva la console di gestione JBoss e la console JMX {#disable-jboss-management-console-and-jmx-console}

L’accesso alla console di gestione JBoss e alla console JMX è già configurato (il monitoraggio JMX è disabilitato) quando installi AEM Forms su JEE su JBoss utilizzando il metodo di installazione chiavi in mano. Se utilizzi un server applicazioni JBoss personalizzato, assicurati che l’accesso alla console di gestione JBoss e alla console di monitoraggio JMX sia protetto. L&#39;accesso alla console di monitoraggio JMX è impostato nel file di configurazione JBoss denominato jmx-invoker-service.xml.

### Disattiva la navigazione nelle directory {#disable-directory-browsing}

Dopo aver effettuato l’accesso alla console di amministrazione, è possibile sfogliare l’elenco delle directory della console modificando l’URL. Ad esempio, se modifichi l’URL in uno dei seguenti URL, potrebbe comparire un elenco di directory:

```java
https://<servername>:8080/adminui/secured/ 
https://<servername>:8080/um/
```

## Raccomandazioni per la sicurezza specifiche per WebLogic {#weblogic-specific-security-recommendations}

Questa sezione contiene raccomandazioni sulla configurazione del server applicazioni per la protezione di WebLogic 9.1 durante l&#39;esecuzione di AEM Forms su JEE.

### Disattiva la navigazione nelle directory {#disable_directory_browsing-1}

Imposta le proprietà delle directory indice nel file weblogic.xml su `false`, come mostrato in questo esempio:

```xml
<container-descriptor> 
    <index-directory-enabled>false 
    </index-directory-enabled> 
</container-descriptor>
```

### Abilita porta SSL WebLogic {#enable-weblogic-ssl-port}

Per impostazione predefinita, WebLogic non abilita la porta di ascolto SSL predefinita, 7002. Abilita questa porta nella console di amministrazione del server WebLogic prima di configurare SSL.

## Raccomandazioni per la sicurezza specifiche per WebSphere {#websphere-specific-security-recommendations}

Questa sezione contiene raccomandazioni di configurazione dell&#39;applicazione server per la protezione di WebSphere che esegue AEM Forms su JEE.

### Disattiva la navigazione nelle directory {#disable_directory_browsing-2}

Imposta la proprietà `directoryBrowsingEnabled` nel file ibm-web-ext.xml su `false`.

### Abilita protezione amministrativa WebSphere {#enable-websphere-administrative-security}

1. Accedi alla console amministrativa WebSphere.
1. Nella struttura di navigazione, vai a **Sicurezza** > **Sicurezza globale**
1. Selezionare **Abilita protezione amministrativa**.
1. Deseleziona sia **Abilita protezione applicazione** che **Usa sicurezza Java 2**.
1. Fare clic su **OK** o **Applica**.
1. Nella casella **Messaggi**, fai clic su **Salva direttamente nella configurazione master**.
