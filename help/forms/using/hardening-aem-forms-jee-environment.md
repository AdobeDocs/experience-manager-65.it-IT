---
title: Come aumentare il livello di protezione del AEM Forms  in ambiente JEE
seo-title: Come aumentare il livello di protezione del AEM Forms  in ambiente JEE
description: Scopri una serie di impostazioni di protezione per migliorare la sicurezza di  AEM Forms su JEE in esecuzione in una Intranet aziendale.
seo-description: Scopri una serie di impostazioni di protezione per migliorare la sicurezza di  AEM Forms su JEE in esecuzione in una Intranet aziendale.
uuid: f6c63690-6376-4fe1-9df2-a14fbfd62aff
content-type: reference
topic-tags: Security
products: SG_EXPERIENCEMANAGER/6.4
discoiquuid: 6b380e92-f90d-4875-b7a2-f3958daf2364
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '7698'
ht-degree: 0%

---


# Come aumentare il livello di protezione  AEM Forms in ambiente JEE {#hardening-your-aem-forms-on-jee-environment}

Scopri una serie di impostazioni di protezione per migliorare la sicurezza di  AEM Forms su JEE in esecuzione in una Intranet aziendale.

L&#39;articolo descrive raccomandazioni e procedure ottimali per la protezione dei server che eseguono  AEM Forms su JEE. Non si tratta di un documento completo per l&#39;applicazione di protezione host per il sistema operativo e i server applicazioni in uso. Questo articolo descrive invece una serie di impostazioni di protezione che è necessario implementare per migliorare la sicurezza di  AEM Forms su JEE in esecuzione all&#39;interno di una rete Intranet aziendale. Per garantire che l&#39;AEM Forms  sui server applicazioni JEE rimanga sicuro, è tuttavia necessario implementare anche procedure di monitoraggio, rilevamento e risposta di sicurezza.

L&#39;articolo descrive le tecniche di indurimento che dovrebbero essere applicate nelle seguenti fasi durante il ciclo di vita dell&#39;installazione e della configurazione:

* **Pre-installazione:** utilizzate queste tecniche prima di installare  AEM Forms su JEE.
* **Installazione:** utilizzate queste tecniche durante il processo di installazione  AEM Forms su JEE.
* **Post-installazione:** Utilizzare queste tecniche dopo l&#39;installazione e periodicamente dopo.

 AEM Forms su JEE è altamente personalizzabile e può funzionare in molti ambienti diversi. Alcune delle raccomandazioni potrebbero non essere adatte alle esigenze della vostra organizzazione.

## Preinstallazione {#preinstallation}

Prima di installare  AEM Forms su JEE, potete applicare soluzioni di sicurezza al livello di rete e al sistema operativo. Questa sezione descrive alcuni problemi e formula raccomandazioni per ridurre le vulnerabilità di sicurezza in queste aree.

**Installazione e configurazione su UNIX e Linux**

Non installare o configurare  AEM Forms su JEE utilizzando una shell principale. Per impostazione predefinita, i file sono installati nella directory /opt, e l&#39;utente che esegue l&#39;installazione ha bisogno di tutte le autorizzazioni per i file in /opt. In alternativa, un&#39;installazione può essere eseguita nella directory /utente di un singolo utente, in cui dispongono già di tutte le autorizzazioni per i file.

**Installazione e configurazione in Windows**

È necessario eseguire l&#39;installazione in Windows come amministratore se si sta installando  AEM Forms su JEE su JBoss utilizzando il metodo chiavi in mano o se si sta installando PDF Generator. Inoltre, quando si installa PDF Generator in Windows con supporto dell&#39;applicazione nativa, è necessario eseguire l&#39;installazione come lo stesso utente Windows che ha installato Microsoft Office. Per ulteriori informazioni sui privilegi di installazione, consultare il documento relativo all&#39;installazione e alla distribuzione di  AEM Forms su JEE* per il server dell&#39;applicazione in uso.

### Protezione del livello di rete {#network-layer-security}

Le vulnerabilità di sicurezza della rete sono tra le prime minacce a qualsiasi server applicazioni rivolto a Internet o Intranet. Questa sezione descrive il processo di indurimento degli host sulla rete rispetto a tali vulnerabilità. Si occupa della segmentazione della rete, del protocollo di controllo della trasmissione/del protocollo Internet (TCP/IP) e dell&#39;uso di firewall per la protezione dell&#39;host.

Nella tabella seguente sono descritti i processi comuni che riducono le vulnerabilità di sicurezza della rete.

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
   <td><p>Implementare i server dei moduli all'interno di una zona demilitarizzata (DMZ). La segmentazione deve esistere in almeno due livelli con il server applicazione utilizzato per eseguire  AEM Forms su JEE posizionato dietro il firewall interno. Separare la rete esterna dalla rete perimetrale che contiene i server Web, che a sua volta deve essere separata dalla rete interna. Usate i firewall per implementare i livelli di separazione. Categorizzare e controllare il traffico che passa attraverso ciascun livello di rete per garantire che sia consentito solo il minimo assoluto di dati richiesti.</p> </td> 
  </tr> 
  <tr> 
   <td><p>Indirizzi IP privati</p> </td> 
   <td><p>Utilizzate Network Address Translation (NAT) con indirizzi IP privati RFC 1918  server dell'applicazione AEM Forms. Assegnate indirizzi IP privati (10.0.0.0/8, 172.16.0.0/12 e 192.168.0.0/16) per rendere più difficile per un utente malintenzionato indirizzare il traffico da e verso un host interno del NAT attraverso Internet.</p> </td> 
  </tr> 
  <tr> 
   <td><p>Firewall</p> </td> 
   <td><p>Utilizzate i seguenti criteri per selezionare una soluzione firewall:</p> 
    <ul> 
     <li><p>Implementate firewall che supportano server proxy e/o <em>ispezione dello stato</em> invece di semplici soluzioni di filtraggio dei pacchetti.</p> </li> 
     <li><p>Utilizzare un firewall che supporta un <em>negare tutti i servizi, ad eccezione di quelli consentiti esplicitamente</em> paradigmi di protezione.</p> </li> 
     <li><p>Implementate una soluzione firewall che sia a doppia casa o con più indirizzi. Questa architettura fornisce il massimo livello di protezione e aiuta a impedire che utenti non autorizzati scavalchino la protezione del firewall.</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>Porte database</p> </td> 
   <td><p>Non utilizzare porte di ascolto predefinite per i database (MySQL - 3306,  Oracle - 1521, MS SQL - 1433). Per informazioni sulla modifica delle porte del database, consultate la documentazione del database.</p> <p>L'utilizzo di una porta di database diversa influisce sull'intero  AEM Forms nella configurazione JEE. Se si modificano le porte predefinite, è necessario apportare le modifiche corrispondenti in altre aree di configurazione, come le origini dati per  AEM Forms su JEE.</p> <p>Per informazioni sulla configurazione delle origini dati in  AEM Forms su JEE, vedere Installare e aggiornare  AEM Forms su JEE o Eseguire l'aggiornamento a  AEM Forms su JEE per il server delle applicazioni in <a href="/help/forms/using/introduction-aem-forms.md" target="_blank"> Guida utente di AEM Forms</a>.</p> </td> 
  </tr> 
 </tbody> 
</table>

### Sicurezza del sistema operativo {#operating-system-security}

Nella tabella seguente sono descritti alcuni approcci potenziali per ridurre al minimo le vulnerabilità di sicurezza riscontrate nel sistema operativo.

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
   <td><p>Esiste un rischio maggiore che un utente non autorizzato possa accedere al server applicazione se le patch e gli aggiornamenti di sicurezza del fornitore non vengono applicati in modo tempestivo. Verificate le patch di protezione prima di applicarle ai server di produzione.</p><p>Inoltre, potete creare criteri e procedure per verificare e installare le patch su base regolare.</p></td> 
  </tr> 
  <tr> 
   <td><p>Software antivirus</p></td> 
   <td><p>Gli scanner antivirus possono identificare i file infetti digitalizzando una firma o guardando per un comportamento insolito. Gli scanner conservano le firme antivirus in un file, solitamente memorizzato sul disco rigido locale. Poiché i nuovi virus vengono spesso scoperti, è necessario aggiornare frequentemente questo file per lo scanner virus per identificare tutti i virus correnti.</p></td> 
  </tr> 
  <tr> 
   <td><p>Network Time Protocol (NTP)</p></td> 
   <td><p>Per l'analisi forense, tenere accurato il tempo sui server dei moduli. Utilizzate NTP per sincronizzare l'ora su tutti i sistemi che sono connessi direttamente a Internet.</p></td> 
  </tr> 
 </tbody> 
</table>

Per ulteriori informazioni sulla sicurezza del sistema operativo in uso, vedere [&quot;Informazioni sulla sicurezza del sistema operativo&quot;](https://helpx.adobe.com/aem-forms/6-1/hardening-security/general-security-considerations.html#operating_system_security_information).

## Installazione {#installation}

Questa sezione descrive le tecniche che potete utilizzare durante il processo di installazione di  AEM Forms per ridurre le vulnerabilità di sicurezza. In alcuni casi, queste tecniche utilizzano opzioni che fanno parte del processo di installazione. Nella tabella seguente sono descritte queste tecniche.

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
   <td><p>Utilizzate il numero minimo di privilegi necessari per installare il software. Effettuate l'accesso al computer utilizzando un account non appartenente al gruppo Amministratori. In Windows, potete utilizzare il comando Esegui come per eseguire il programma di installazione  AEM Forms su JEE come utente amministrativo. Sui sistemi UNIX e Linux, utilizzare un comando come <code>sudo</code> per installare il software.</p> </td> 
  </tr> 
  <tr> 
   <td><p>Origine software</p> </td> 
   <td><p>Non scaricare o eseguire  AEM Forms su JEE da fonti non attendibili.</p> <p>I programmi dannosi possono contenere codice per violare la sicurezza in diversi modi, tra cui furto, modifica ed eliminazione di dati e negazione del servizio. Installate  AEM Forms su JEE dal DVD del Adobe  o solo da una fonte affidabile.</p> </td> 
  </tr> 
  <tr> 
   <td><p>Partizioni disco</p> </td> 
   <td><p>Posizionare  AEM Forms su JEE su una partizione dedicata del disco. La segmentazione del disco è un processo che mantiene dati specifici sul server su dischi fisici separati per una maggiore sicurezza. Disporre i dati in questo modo riduce il rischio di attacchi di traversata di directory. Pianificare la creazione di una partizione separata dalla partizione di sistema in cui è possibile installare l'AEM Forms  nella directory di contenuto JEE. (In Windows, la partizione di sistema contiene la directory system32, o partizione di avvio.)</p> </td> 
  </tr> 
  <tr> 
   <td><p>Componenti</p> </td> 
   <td><p>Valutare i servizi esistenti e disabilitare o disinstallare quelli non richiesti. Non installate componenti e servizi non necessari.</p> <p>L'installazione predefinita di un server applicazioni potrebbe includere servizi non necessari all'uso da parte dell'utente. Devi disattivare tutti i servizi non necessari prima della distribuzione per ridurre al minimo i punti di ingresso per un attacco. Ad esempio, in JBoss, potete inserire commenti sui servizi non necessari nel file descrittore META-INF/jboss-service.xml.</p> </td> 
  </tr> 
  <tr> 
   <td><p>File dei criteri tra domini</p> </td> 
   <td><p>La presenza di un file <code>crossdomain.xml</code> sul server potrebbe indebolire immediatamente tale server. È consigliabile rendere l'elenco dei domini il più restrittivo possibile. Non inserire in produzione il file <code>crossdomain.xml</code> utilizzato durante lo sviluppo quando si utilizzano le Guide <em>(obsoleto)</em>. Per una guida che utilizza i servizi Web, se il servizio si trova sullo stesso server che ha fornito la guida, non è necessario alcun file <code>crossdomain.xml</code>. Tuttavia, se il servizio si trova su un altro server o se sono coinvolti cluster, sarebbe necessaria la presenza di un file <code>crossdomain.xml</code>. Per ulteriori informazioni sul file crossdomain.xml, fare riferimento a <a href="https://kb2.adobe.com/cps/142/tn_14213.html">https://kb2.adobe.com/cps/142/tn_14213.html</a>.</p> </td> 
  </tr> 
  <tr> 
   <td><p>Impostazioni di protezione del sistema operativo</p> </td> 
   <td><p>Se è necessario utilizzare la crittografia XML a 192 bit o a 256 bit sulle piattaforme Solaris, assicurarsi di installare <code>pkcs11_softtoken_extra.so</code> invece di <code>pkcs11_softtoken.so</code>.</p> </td> 
  </tr> 
 </tbody> 
</table>

## Passaggi successivi all&#39;installazione {#post-installation-steps}

Dopo aver installato  AEM Forms su JEE, è importante mantenere periodicamente l&#39;ambiente dal punto di vista della sicurezza.

La sezione seguente descrive in dettaglio le diverse attività consigliate per proteggere il server dei moduli distribuito.

###  protezione AEM Forms {#aem-forms-security}

Le seguenti impostazioni consigliate si applicano all&#39;AEM Forms  sul server JEE esterno all&#39;applicazione Web amministrativa. Per ridurre i rischi di protezione per il server, applicate queste impostazioni subito dopo l&#39;installazione  AEM Forms su JEE.

**Patch di sicurezza**

Esiste un rischio maggiore che un utente non autorizzato possa accedere al server dell&#39;applicazione se le patch e gli aggiornamenti di sicurezza del fornitore non vengono applicati in modo tempestivo. Verificate le patch di sicurezza prima di applicarle ai server di produzione per garantire la compatibilità e la disponibilità delle applicazioni. Inoltre, potete creare criteri e procedure per verificare e installare le patch su base regolare.  gli aggiornamenti AEM Forms su JEE si trovano nel sito di download dei prodotti Enterprise.

**Account di servizio (chiavi in mano JBoss solo in Windows)**

 AEM Forms su JEE installa un servizio, per impostazione predefinita, utilizzando l&#39;account LocalSystem. L&#39;account utente LocalSystem integrato ha un livello elevato di accessibilità; fa parte del gruppo Amministratori. Se un&#39;identità di processo di lavoro viene eseguita come account utente LocalSystem, tale processo di lavoro dispone dell&#39;accesso completo all&#39;intero sistema.

Per eseguire il server applicazioni in cui  AEM Forms su JEE è distribuito, utilizzando un account non amministrativo specifico, attenersi alle istruzioni riportate di seguito:

1. In Microsoft Management Console (MMC), creare un utente locale che consenta al servizio server moduli di accedere come segue:

   * Selezionare **L&#39;utente non può cambiare la password**.
   * Nella scheda **Membro di**, assicurarsi che il gruppo **Utenti** sia elencato.

   >[!NOTE]
   >
   >Non è possibile modificare questa impostazione per PDF Generator.

1. Selezionare **Start** > **Settings** > **Administrative Tools** > **Services**.
1. Fate doppio clic su JBoss per  AEM Forms su JEE e arrestate il servizio.
1. Nella scheda **Accedi**, selezionare **Questo account**, individuare l&#39;account utente creato e immettere la password per l&#39;account.
1. In MMC, aprire **Impostazioni di protezione locali** e selezionare **Criteri locali** > **Assegnazione diritti utente**.
1. Assegnare i seguenti diritti all&#39;account utente in cui è in esecuzione il server moduli:

   * Rifiuta accesso tramite Servizi terminal
   * Rifiuta accesso localmente
   * Accedi come servizio (dovrebbe essere già impostato)

1. Assegnate al nuovo account utente autorizzazioni di modifica nelle seguenti directory:
   * **Directory** Global Document Storage (GDS): La posizione della directory GDS viene configurata manualmente durante il processo di installazione di AEM Forms . Se l&#39;impostazione della posizione rimane vuota durante l&#39;installazione, per impostazione predefinita la posizione corrisponde a una directory nell&#39;installazione del server applicazione in `[JBoss root]/server/[type]/svcnative/DocumentStorage`
   * **Directory** CRX-Repository: Il percorso predefinito è  `[AEM-Forms-installation-location]\crx-repository`
   * **directory** temporanee AEM Forms:
      * (Windows) Percorso TMP o TEMP impostato nelle variabili di ambiente
      * (AIX, Linux o Solaris) Directory principale dell&#39;utente registrato
Nei sistemi basati su UNIX, un utente non root può utilizzare la seguente directory come directory temporanea:
      * (Linux) /var/tmp o /usr/tmp
      * (AIX) /tmp o /usr/tmp
      * (Solaris) /var/tmp o /usr/tmp
1. Assegnate al nuovo account utente autorizzazioni di scrittura sulle seguenti directory:
   * [JBoss-directory]\standalone\deployment
   * [JBoss-directory]\standalone\
   * [JBoss-directory]\bin\

   >[!NOTE]
   >
   > Il percorso di installazione predefinito di JBoss Application Server:
   > * Windows: C:\Adobe\Adobe_Experience_Manager_Forms\jboss
   > * Linux: /opt/jboss/

1. Avviate il server applicazione.

**Disattivazione del servlet di avvio di Configuration Manager**

Configuration Manager ha utilizzato un servlet distribuito sul server applicazione per eseguire l&#39;avvio dell&#39;AEM Forms  nel database JEE. Poiché Configuration Manager accede a questo servlet prima del completamento della configurazione, l&#39;accesso a esso non è stato protetto per gli utenti autorizzati e deve essere disattivato dopo che Configuration Manager è stato utilizzato con successo per configurare  AEM Forms su JEE.

1. Decomprimete il file adobe-livecycle-[appserver].ear.
1. Aprite il file META-INF/application.xml.
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

1. Arrestate il server AEM Forms .
1. Aggiungete un commento alla directory adobe-bootstrapper.war e adobe-lcm-bootstrapper-redirectory. moduli di guerra come segue:

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

1. Salvate e chiudete il file META-INF/application.xml.
1. Zip il file EAR e ridistribuirlo nel server applicazione.
1. Avviate il server AEM Forms .
1. Digitate l&#39;URL seguente in un browser per verificare che la modifica non funzioni più.

   https://&lt;localhost>:&lt;porta>/adobe-bootstrapper/bootstrap

**Blocco dell&#39;accesso remoto all&#39;archivio attendibili**

Configuration Manager consente di caricare una credenziale di estensione Acrobat Reader DC nell&#39;AEM Forms  sull&#39;archivio di affidabilità JEE. Ciò significa che l&#39;accesso al servizio Credenziali archivio attendibili tramite protocolli remoti (SOAP ed EJB) è stato abilitato per impostazione predefinita. Questo accesso non è più necessario dopo aver caricato le credenziali dei diritti tramite Configuration Manager o se decidete di utilizzare la console di amministrazione in un secondo momento per gestire le credenziali.

È possibile disattivare l&#39;accesso remoto a tutti i servizi Store attendibili seguendo i passaggi descritti nella sezione [Disattivazione dell&#39;accesso remoto non essenziale ai servizi](https://helpx.adobe.com/aem-forms/6-1/hardening-security/configuring-secure-administration-settings-aem.html#disabling_non_essential_remote_access_to_services).

**Disattiva tutti gli accessi anonimi non essenziali**

Alcuni servizi server dei moduli dispongono di operazioni che possono essere richiamate da un chiamante anonimo. Se l&#39;accesso anonimo a questi servizi non è richiesto, disattivatelo seguendo la procedura indicata in [Disattivazione dell&#39;accesso anonimo non essenziale ai servizi](https://helpx.adobe.com/aem-forms/6-1/hardening-security/configuring-secure-administration-settings-aem.html#disabling_non_essential_anonymous_access_to_services).

#### Modificare la password amministratore predefinita {#change-the-default-administrator-password}

Quando  AEM Forms su JEE è installato, un singolo account utente predefinito è configurato per l&#39;utente Amministratore/Amministratore di login-id con una password predefinita *password*. È necessario modificare immediatamente la password utilizzando Gestione configurazione.

1. Digitate il seguente URL in un browser Web:

   ```java
   https://[host name]:[port]/adminui
   ```

   Il numero di porta predefinito è uno dei seguenti:

   **JBoss:** 8080

   **Server WebLogic:** 7001

   **WebSphere:** 9080.

1. Nel campo **Nome utente** digitare `administrator` e nel campo **Password** digitare `password`.
1. Fare clic su **Impostazioni** > **Gestione utente** > **Utenti e gruppi**.
1. Digitare `administrator` nel campo **Find**, quindi fare clic su **Find**.
1. Fare clic su **Super Administrator** dall&#39;elenco degli utenti.
1. Fare clic su **Modifica password** nella pagina Modifica utente.
1. Specificate la nuova password e fate clic su **Salva**.

Inoltre, si consiglia di modificare la password predefinita per l&#39;amministratore CRX eseguendo i seguenti passaggi:

1. Accedete a `https://[server]:[port]/lc/libs/granite/security/content/useradmin.html` utilizzando il nome utente/password predefinito.
1. Digitare Administrator nel campo di ricerca e fare clic su **Go**.
1. Selezionare **Administrator** dal risultato della ricerca e fare clic sull&#39;icona **Edit** in basso a destra dell&#39;interfaccia utente.
1. Specificare la nuova password nel campo **Nuova password** e la vecchia password nel campo **Password**.
1. Fate clic sull&#39;icona Salva in basso a destra dell&#39;interfaccia utente.

#### Disattiva generazione WSDL {#disable-wsdl-generation}

La generazione del linguaggio WSDL (Web Service Definition Language) deve essere abilitata solo per gli ambienti di sviluppo, dove la generazione WSDL viene utilizzata dagli sviluppatori per creare le applicazioni client. Potete scegliere di disabilitare la generazione WSDL in un ambiente di produzione per evitare di esporre i dettagli interni di un servizio.

1. Digitate il seguente URL in un browser Web:

   ```java
   https://[host name]:[port]/adminui
   ```

1. Fare clic su **Impostazioni > Impostazioni di sistema di base > Configurazioni**.
1. Deselezionare **Abilita WSDL** e fare clic su **OK**.

### Protezione del server applicazioni {#application-server-security}

Nella tabella seguente sono illustrate alcune tecniche per proteggere il server applicazione dopo l&#39;installazione dell&#39;applicazione  AEM Forms su JEE.

<table> 
 <thead> 
  <tr> 
   <th><p>Problema</p> </th> 
   <th><p>Descrizione</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>console di amministrazione del server applicazioni</p> </td> 
   <td><p>Dopo aver installato, configurato e implementato  AEM Forms su JEE nel server applicazione, è necessario disattivare l'accesso alle console di amministrazione del server applicazione. Per ulteriori informazioni, consultate la documentazione del server applicazione.</p> </td> 
  </tr> 
  <tr> 
   <td><p>Impostazioni cookie del server applicazioni</p> </td> 
   <td><p>I cookie dell'applicazione sono controllati dal server dell'applicazione. Quando distribuite l’applicazione, l’amministratore del server applicazione può specificare le preferenze relative ai cookie a livello di server o di applicazione. Per impostazione predefinita, le impostazioni del server hanno la preferenza.</p> <p>Tutti i cookie di sessione generati dal server applicazione devono includere l'attributo <code>HttpOnly</code>. Ad esempio, quando utilizzate il server applicazioni JBoss, potete modificare l'elemento SessionCookie in <code>httpOnly="true"</code> nel file <code>WEB-INF/web.xml</code>.</p> <p>È possibile limitare l'invio dei cookie solo tramite HTTPS. Di conseguenza, non vengono inviati non crittografati via HTTP. Gli amministratori del server applicazioni devono abilitare i cookie protetti per il server su base globale. Ad esempio, quando si utilizza JBoss Application Server, è possibile modificare l'elemento del connettore in <code>secure=true</code> nel file <code>server.xml</code>.</p> <p>Per ulteriori informazioni sulle impostazioni dei cookie, consultate la documentazione del server applicazione.</p> </td> 
  </tr> 
  <tr> 
   <td><p>Esplorazione directory</p> </td> 
   <td><p>Quando un utente richiede una pagina che non esiste o richiede il nome di un direttore (la stringa di richiesta termina con una barra (/))), il server applicazione non deve restituire il contenuto di tale directory. Per evitare questo problema, è possibile disattivare la navigazione nelle directory sul server dell'applicazione. È consigliabile eseguire questa operazione per l'applicazione della console di amministrazione e per altre applicazioni in esecuzione sul server.</p> <p>Per JBoss, impostare il valore del parametro di inizializzazione delle voci della proprietà <code>DefaultServlet</code> su <code>false</code> nel file web.xml, come illustrato nell'esempio seguente:</p> <p>&lt;servlet&gt;</p> <p>&lt;servlet-name&gt;default&lt;/servlet-name&gt;</p> <p>&lt;servlet-class&gt;</p> <p>org.apache.catalina.servlets.DefaultServlet</p> <p>&lt;/servlet-class&gt;</p> <p>&lt;init-param&gt;</p> <p>&lt;param-name&gt;inserzioni&lt;/param-name&gt;</p> <p>&lt;param-value&gt;false&lt;/param-value&gt;</p> <p>&lt;/init-param&gt;</p> <p>&lt;load-on-startup&gt;1&lt;/load-on-startup&gt;</p> <p>&lt;/servlet&gt;</p> <p>Per WebSphere, impostare la proprietà <code>directoryBrowsingEnabled</code> nel file ibm-web-ext.xmi su <code>false</code>.</p> <p>Per WebLogic, impostare le proprietà delle directory indice nel file weblogic.xml su <code>false</code>, come illustrato nell'esempio seguente:</p> <p>&lt;container-descriptor&gt;</p> <p>&lt;index-directory-enabled&gt;false</p> <p>&lt;/index-directory-enabled&gt;</p> <p>&lt;/container-descriptor&gt;</p> </td> 
  </tr> 
 </tbody> 
</table>

### Protezione del database {#database-security}

Durante la protezione del database, è necessario implementare le misure descritte dal fornitore del database. È necessario allocare un utente di database con le autorizzazioni minime richieste per il database concesse per l&#39;utilizzo da parte di  AEM Forms su JEE. Ad esempio, non utilizzate un account con privilegi di amministratore del database.

In  Oracle, l&#39;account del database utilizzato richiede solo i privilegi CONNECT, RISORSA e CREA VISUALIZZAZIONE. Per requisiti simili su altri database, vedere [Preparazione all&#39;installazione  AEM Forms su JEE (Single Server)](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_64).

#### Configurazione della protezione integrata per SQL Server in Windows per JBoss {#configuring-integrated-security-for-sql-server-on-windows-for-jboss}

1. Modificate [JBOSS_HOME]\\standalone\configuration\lc_{datasource.xml} per aggiungere `integratedSecurity=true` all&#39;URL della connessione, come illustrato in questo esempio:

   ```java
    jdbc:sqlserver://<serverhost>:<port>;databaseName=<dbname>;integratedSecurity=true
   ```

1. Aggiungete il file sqljdbc_auth.dll al percorso del sistema Windows sul computer su cui è in esecuzione il server dell&#39;applicazione. Il file sqljdbc_auth.dll si trova con l&#39;installazione del driver Microsoft SQL JDBC 6.2.1.0.
1. Modificate la proprietà del servizio Windows JBoss (JBoss per  AEM Forms su JEE) per Accesso come da sistema locale a un account di login che ha  database AEM Forms e un insieme minimo di privilegi. Se si esegue JBoss dalla riga di comando invece che come servizio Windows, non è necessario eseguire questo passaggio.
1. Impostare la protezione per SQL Server dalla modalità **Mixed** su **Solo autenticazione Windows**.

#### Configurazione della protezione integrata per SQL Server in Windows per WebLogic {#configuring-integrated-security-for-sql-server-on-windows-for-weblogic}

1. Avviate la console di amministrazione del server WebLogic digitando il seguente URL nella riga URL di un browser Web:

   ```java
   https://[host name]:7001/console
   ```

1. In Centro modifiche fare clic su **Blocca e modifica**.
1. In Struttura dominio, fare clic su *[base_domain]* > **Services** > **JDBC** > **Origini dati** e, nel riquadro di destra, fare clic su **IDP_DS**.
1. Nella schermata successiva, nella scheda **Configurazione**, fare clic sulla scheda **Pool di connessioni** e digitare `integratedSecurity=true` nella casella **Proprietà**.
1. In Struttura dominio, fare clic su **[base_domain]** > **Services** > **JDBC** > **Origini dati** e, nel riquadro di destra, fare clic su **RM_DS**.
1. Nella schermata successiva, nella scheda **Configurazione**, fare clic sulla scheda **Pool di connessioni** e digitare `integratedSecurity=true` nella casella **Proprietà**.
1. Aggiungete il file sqljdbc_auth.dll al percorso del sistema Windows sul computer su cui è in esecuzione il server dell&#39;applicazione. Il file sqljdbc_auth.dll si trova con l&#39;installazione del driver Microsoft SQL JDBC 6.2.1.0.
1. Impostare la protezione per SQL Server dalla modalità **Mixed** su **Solo autenticazione Windows**.

#### Configurazione della protezione integrata per SQL Server in Windows per WebSphere {#configuring-integrated-security-for-sql-server-on-windows-for-websphere}

In WebSphere è possibile configurare la protezione integrata solo quando si utilizza un driver JDBC SQL Server esterno, non il driver JDBC di SQL Server incorporato con WebSphere.

1. Accedete alla console di amministrazione di WebSphere.
1. Nella struttura di navigazione, fare clic su **Risorse** > **JDBC** > **Origini dati** e, nel riquadro a destra, fare clic su **IDP_DS**.
1. Nel riquadro a destra, in Proprietà aggiuntive, fare clic su **Proprietà personalizzate**, quindi fare clic su **Nuovo**.
1. Nella casella **Nome** digitare `integratedSecurity` e, nella casella **Valore**, digitare `true`.
1. Nella struttura di navigazione, fare clic su **Risorse** > **JDBC** > **Origini dati** e, nel riquadro a destra, fare clic su **RM_DS**.
1. Nel riquadro a destra, in Proprietà aggiuntive, fare clic su **Proprietà personalizzate**, quindi fare clic su **Nuovo**.
1. Nella casella **Nome** digitare `integratedSecurity` e, nella casella **Valore**, digitare `true`.
1. Nel computer in cui è installato WebSphere, aggiungere il file sqljdbc_auth.dll al percorso dei sistemi Windows (C:\Windows). Il file sqljdbc_auth.dll si trova nello stesso percorso dell&#39;installazione del driver Microsoft SQL JDBC 1.2 (il valore predefinito è *[InstallDir]*/sqljdbc_1.2/enu/auth/x86).
1. Selezionare **Start** > **Pannello di controllo Campaign** > **Services**, fare clic con il pulsante destro del mouse sul servizio Windows per WebSphere (IBM WebSphere Application Server &lt;version> - &lt;node>) e selezionare **Properties**.
1. Nella finestra di dialogo Proprietà, fare clic sulla scheda **Accedi**.
1. Selezionare **This Account** e fornire le informazioni necessarie per impostare l&#39;account di accesso che si desidera utilizzare.
1. Impostare la protezione su SQL Server dalla modalità **Mixed** su **Solo autenticazione Windows**.

### Protezione dell&#39;accesso a contenuti sensibili nel database {#protecting-access-to-sensitive-content-in-the-database}

Lo schema  database AEM Forms contiene informazioni riservate sulla configurazione del sistema e sui processi aziendali e deve essere nascosto dietro il firewall. Il database deve essere considerato all&#39;interno dello stesso limite di attendibilità del server dei moduli. Per evitare la divulgazione di informazioni e il furto di dati aziendali, il database deve essere configurato dall&#39;amministratore del database (DBA) per consentire l&#39;accesso solo agli amministratori autorizzati.

Come precauzione aggiuntiva, è consigliabile utilizzare gli strumenti specifici del fornitore del database per cifrare le colonne nelle tabelle contenenti i dati seguenti:

* Rights Management chiavi documento
* Chiave di crittografia PIN HSM Store Trust
* Hash password utente locale

Per informazioni sugli strumenti specifici del fornitore, vedere [&quot;Database security information&quot;](https://helpx.adobe.com/aem-forms/6-1/hardening-security/general-security-considerations.html#database_security_information).

### Protezione LDAP {#ldap-security}

Una directory LDAP (Lightweight Directory Access Protocol) viene in genere utilizzata da  AEM Forms su JEE come origine per le informazioni di utenti e gruppi aziendali e come mezzo per eseguire l&#39;autenticazione tramite password. Accertatevi che la directory LDAP sia configurata per l’utilizzo di Secure Socket Layer (SSL) e che  AEM Forms su JEE sia configurato per l’accesso alla directory LDAP utilizzando la porta SSL.

#### Negazione del servizio LDAP {#ldap-denial-of-service}

Un attacco comune che utilizza LDAP coinvolge un aggressore che intenzionalmente non riesce ad autenticarsi più volte. In questo modo il server di directory LDAP blocca un utente da tutti i servizi basati su LDAP.

Potete impostare il numero di tentativi di errore e il successivo tempo di blocco che  AEM Forms implementa quando un utente ripetutamente non riesce ad autenticarsi  AEM Forms. In Admin Console, scegli valori bassi. Quando si seleziona il numero di tentativi di errore, è importante comprendere che dopo tutti i tentativi,  AEM Forms blocca l&#39;utente prima che il server di directory LDAP lo faccia.

#### Impostazione del blocco automatico dell&#39;account {#set-automatic-account-locking}

1. Accedi alla console di amministrazione.
1. Fare clic su **Impostazioni** > **Gestione utente** > **Gestione dominio**.
1. In Impostazioni di blocco account automatico, impostare **Numero massimo di errori di autenticazione consecutivi** su un numero basso, ad esempio 3.
1. Fai clic su **Salva**.

### Controllo e registrazione {#auditing-and-logging}

L&#39;utilizzo corretto e sicuro del controllo e della registrazione delle applicazioni può contribuire a garantire che la sicurezza e altri eventi anomali siano tracciati e rilevati il più rapidamente possibile. L&#39;utilizzo efficace del controllo e della registrazione all&#39;interno di un&#39;applicazione include elementi quali il monitoraggio degli accessi riusciti e non riusciti, nonché eventi applicativi chiave come la creazione o l&#39;eliminazione di record chiave.

Potete utilizzare il controllo per rilevare molti tipi di attacchi, tra cui:

* Attacchi di password di forza bruta
* Negazione degli attacchi di servizio
* Iniezione di input ostili e classi correlate di attacchi di script

Nella tabella seguente sono descritte le tecniche di auditing e registrazione utilizzabili per ridurre le vulnerabilità del server.

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
   <td><p>Impostare  AEM Forms appropriato sugli elenchi di controllo di accesso ai file di registro JEE (ACL).</p> <p>L'impostazione delle credenziali appropriate consente di impedire agli aggressori di eliminare i file.</p> <p>Le autorizzazioni di protezione nella directory del file di registro devono essere Controllo completo per gli amministratori e i gruppi SYSTEM. L'account utente  AEM Forms deve avere autorizzazioni di sola lettura e scrittura.</p> </td> 
  </tr> 
  <tr> 
   <td><p>ridondanza dei file di registro</p> </td> 
   <td><p>Se le risorse lo consentono, inviate i file di registro a un altro server in tempo reale non accessibile dall’utente malintenzionato (solo in scrittura) utilizzando Syslog, Tivoli, Microsoft Operations Manager (MOM) Server o un altro meccanismo.</p> <p>La protezione dei file di registro in questo modo consente di evitare manomissioni. Inoltre, l'archiviazione dei registri in un archivio centrale facilita la correlazione e il monitoraggio (ad esempio, se sono in uso più server di moduli e si verifica un attacco per l'identificazione della password in più computer, dove ogni computer viene interrogato per ottenere una password).</p> </td> 
  </tr> 
 </tbody> 
</table>

### Abilitare un utente non amministratore a eseguire PDF Generator

È possibile consentire a un utente non amministratore di utilizzare PDF Generator. Normalmente, solo gli utenti con privilegi amministrativi possono utilizzare PDF Generator. Per consentire a un utente non amministratore di eseguire PDF Generator, effettuare le operazioni seguenti:

1. Create un nome di variabile di ambiente PDFG_NON_ADMIN_ENABLED.

1. Impostate il valore della variabile su TRUE.

1. Riavviate l&#39;istanza  AEM Forms.

## Configurazione  AEM Forms su JEE per l&#39;accesso oltre l&#39;azienda {#configuring-aem-forms-on-jee-for-access-beyond-the-enterprise}

Dopo aver installato  AEM Forms su JEE, è importante mantenere periodicamente la sicurezza dell&#39;ambiente. In questa sezione vengono descritte le attività consigliate per mantenere la sicurezza dell&#39;AEM Forms  sul server di produzione JEE.

### Configurazione di un proxy inverso per l&#39;accesso Web {#setting-up-a-reverse-proxy-for-web-access}

È possibile utilizzare un *proxy inverso* per garantire che un set di URL per  AEM Forms sulle applicazioni Web JEE sia disponibile per gli utenti esterni che per quelli interni. Questa configurazione è più sicura che consentire agli utenti di connettersi direttamente al server dell&#39;applicazione su cui è in esecuzione  AEM Forms su JEE. Il proxy inverso esegue tutte le richieste HTTP per il server applicazione in esecuzione  AEM Forms su JEE. Gli utenti dispongono solo dell&#39;accesso di rete al proxy inverso e possono tentare solo connessioni URL supportate dal proxy inverso.

**AEM Forms sugli URL principali JEE da utilizzare con il server proxy inverso**

I seguenti URL principali dell&#39;applicazione per ciascun AEM Forms  sull&#39;applicazione Web JEE. Configurate il proxy inverso solo per esporre gli URL per la funzionalità dell&#39;applicazione Web che desiderate fornire agli utenti finali.

Alcuni URL vengono evidenziati come applicazioni Web rivolte all’utente finale. Evitare di esporre altri URL per Configuration Manager per l&#39;accesso agli utenti esterni tramite il proxy inverso.

<table> 
 <thead> 
  <tr> 
   <th><p>URL principale</p> </th> 
   <th><p>Finalità e/o applicazione Web associata</p> </th> 
   <th><p>Interfaccia basata sul Web</p> </th> 
   <th><p>Accesso dell'utente finale</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>/ReaderExtensions/*</p> </td> 
   <td><p>Acrobat Reader DC estende l'applicazione Web per l'utente finale per l'applicazione dei diritti di utilizzo ai documenti PDF</p> </td> 
   <td><p>Sì</p> </td> 
   <td><p>Sì</p> </td> 
  </tr> 
  <tr> 
   <td><p>/edc/*</p> </td> 
   <td><p>Rights Management applicazione Web utente finale</p> </td> 
   <td><p>Sì</p> </td> 
   <td><p>Sì</p> </td> 
  </tr> 
  <tr> 
   <td><p>/edcws/*</p> </td> 
   <td><p>URL servizio Web per Rights Management</p> </td> 
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
   <td><p>Applicazione Web per l’utente finale di Workspace</p> </td> 
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
   <td><p>Servlet per avviare l'AEM Forms  nell'archivio JEE</p> </td> 
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
   <td><p>URL del servizio Web per tutti i servizi server per moduli</p> </td> 
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
   <td><p>/TruststoreComponent/</p> <p>secure/*</p> </td> 
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
   <td><p>Pagine di amministrazione di output</p> </td> 
   <td><p>Sì</p> </td> 
   <td><p>No</p> </td> 
  </tr> 
  <tr> 
   <td><p>/FormServer/*</p> </td> 
   <td><p>File di applicazioni Web Forms</p> </td> 
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
   <td><p>URL per accesso WebDAV (debug)</p> </td> 
   <td><p>Sì</p> </td> 
   <td><p>No</p> </td> 
  </tr> 
  <tr> 
   <td><p>/AACComponent/*</p> </td> 
   <td><p>Interfaccia utente Applicazioni e servizi</p> </td> 
   <td><p>Sì</p> </td> 
   <td><p>No</p> </td> 
  </tr> 
  <tr> 
   <td><p>/WorkspaceAdmin/*</p> </td> 
   <td><p>Pagine di amministrazione Workspace</p> </td> 
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
   <td><p> AEM Forms nella pagina delle impostazioni di configurazione JEE Core</p> </td> 
   <td><p>Sì</p> </td> 
   <td><p>No</p> </td> 
  </tr> 
  <tr> 
   <td><p>/um/</p> </td> 
   <td><p>Autenticazione Gestione utenti</p> </td> 
   <td><p>No</p> </td> 
   <td><p>Sì</p> </td> 
  </tr> 
  <tr> 
   <td><p>/um/*</p> </td> 
   <td><p>Interfaccia di amministrazione di Gestione utenti</p> </td> 
   <td><p>Sì</p> </td> 
   <td><p>No</p> </td> 
  </tr> 
  <tr> 
   <td><p>/DoumentManager/*</p> </td> 
   <td><p>Caricamento e scaricamento di documenti da elaborare per l'accesso agli endpoint remoti, agli endpoint WSDL SOAP e all'SDK Java attraverso il trasporto SOAP o il trasporto EJB con documenti HTTP abilitati.</p> </td> 
   <td><p>Sì</p> </td> 
   <td><p>Sì</p> </td> 
  </tr> 
 </tbody> 
</table>

## Protezione dagli attacchi di contraffazione delle richieste tra siti {#protecting-from-cross-site-request-forgery-attacks}

Un attacco CSRF (Cross-Site Request Forgery) sfrutta l&#39;affidabilità di un sito Web per l&#39;utente, per trasmettere comandi non autorizzati e non voluti dall&#39;utente. L&#39;attacco è configurato includendo un collegamento o uno script in una pagina Web, o un URL in un messaggio e-mail, per accedere a un altro sito al quale l&#39;utente è già stato autenticato.

Ad esempio, puoi aver effettuato l’accesso ad Admin Console mentre sfoglii contemporaneamente un altro sito Web. Una delle pagine Web può includere un tag immagine HTML con un attributo `src` che esegue il targeting di uno script lato server sul sito Web della vittima. Sfruttando il meccanismo di autenticazione della sessione basato su cookie fornito dai browser Web, il sito web attaccante può inviare richieste dannose a questo script lato server vittima, mascherato come utente legittimo. Per ulteriori esempi, vedere [https://www.owasp.org/index.php/Cross-Site_Request_Forgery_(CSRF)#Examples](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_(CSRF)#Examples).

Le seguenti caratteristiche sono comuni al CSRF:

* Coinvolgere i siti che si basano sull&#39;identità di un utente.
* Sfruttate la fiducia del sito in tale identità.
* Personalizzate il browser dell&#39;utente per inviare richieste HTTP a un sito di destinazione.
* Richiedi richieste HTTP con effetti collaterali.

 AEM Forms su JEE utilizza la funzione Filtro referente per bloccare gli attacchi CSRF. In questa sezione vengono utilizzati i termini seguenti per descrivere il meccanismo di filtro dei referenti:

* **Referente consentito:** Un Referente è l&#39;indirizzo della pagina di origine che invia una richiesta al server. Per le pagine o i moduli JSP, i Referenti sono in genere la pagina precedente della cronologia di navigazione. Per riferimento per le immagini si intendono in genere le pagine sulle quali vengono visualizzate le immagini. È possibile identificare il Referente a cui è consentito l&#39;accesso alle risorse del server aggiungendoli all&#39;elenco Referente autorizzato.
* **Eccezioni referente consentite:** potresti voler limitare l&#39;ambito di accesso di un particolare Referente nell&#39;elenco Referente autorizzato. Per applicare questa limitazione è possibile aggiungere singoli percorsi di tale referente all&#39;elenco Eccezioni referente consentite. Le richieste provenienti dai percorsi nell&#39;elenco Eccezioni referente consentite non possono richiamare alcuna risorsa sul server dei moduli. È possibile definire le eccezioni consentite per un&#39;applicazione specifica e utilizzare un elenco globale di eccezioni valide per tutte le applicazioni.
* **URI consentiti:** elenco di risorse da distribuire senza controllare l&#39;intestazione del referente. È possibile aggiungere a questo elenco risorse, ad esempio, pagine della guida che non comportano modifiche allo stato del server. Le risorse nell&#39;elenco URI consentiti non vengono mai bloccate dal filtro di riferimento, a prescindere da chi sia il referente.
* **Referente nullo:** Una richiesta server che non è associata o non proviene da una pagina Web padre è considerata una richiesta da un Referente Null. Ad esempio, quando si apre una nuova finestra del browser, digitare un indirizzo e premere Invio, il Referente inviato al server è nullo. Un&#39;applicazione desktop (.NET o SWING) che effettua una richiesta HTTP a un server Web, invia anche un Referente Null al server.

### Filtro referente {#referer-filtering}

Il processo di filtro referente può essere descritto come segue:

1. Il server dei moduli verifica il metodo HTTP utilizzato per la chiamata:

   1. Se si tratta di un POST, il server dei moduli esegue il controllo dell&#39;intestazione del referente.
   1. Se è GET, il server dei moduli ignora il controllo Referrer, a meno che *CSRF_CHECK_GETS* non sia impostato su true, nel qual caso esegue il controllo dell&#39;intestazione Referrer. *CSRF_CHECK_* GETSè specificato nel file  *web.* xmldell&#39;applicazione.

1. Il server dei moduli controlla se l&#39;URI richiesto esiste  :

   1. Se l’URI viene inserito nell&#39;elenco Consentiti, il server accetta la richiesta.
   1. Se l’URI richiesto non viene inserito nell&#39;elenco Consentiti, il server recupera il Referente della richiesta.

1. Se nella richiesta è presente un Referente, il server verifica se si tratta di un Referente Consentito. Se consentita, il server verifica la presenza di un&#39;eccezione di riferimento:

   1. Se si tratta di un&#39;eccezione, la richiesta viene bloccata.
   1. Se non si tratta di un&#39;eccezione, la richiesta viene passata.

1. Se nella richiesta non è presente alcun referente, il server verifica se è consentito un Referente Null:

   1. Se è consentito un Referente Null, la richiesta viene passata.
   1. Se non è consentito un Referente Null, il server verifica se l&#39;URI richiesto è un&#39;eccezione per il Referente Null e gestisce la richiesta di conseguenza.

### Gestione del filtro del referente {#managing-referer-filtering}

 AEM Forms su JEE fornisce un filtro di riferimento per specificare il referente che può accedere alle risorse del server. Per impostazione predefinita, il filtro Referente non filtra le richieste che utilizzano un metodo HTTP sicuro, ad GET, a meno che *CSRF_CHECK_GETS* non sia impostato su true. Se il numero di porta per una voce Referente consentito è impostato su 0,  AEM Forms su JEE consentirà tutte le richieste con Referente da tale host, indipendentemente dal numero di porta. Se non viene specificato alcun numero di porta, sono consentite solo le richieste dalla porta predefinita 80 (HTTP) o dalla porta 443 (HTTPS). Il filtro del referente è disabilitato se tutte le voci nell&#39;elenco Referente consentito vengono eliminate.

La prima volta che si installa Document Services, l&#39;elenco Referente consentito viene aggiornato con l&#39;indirizzo del server in cui è installato Document Services. Le voci per il server includono il nome del server, l&#39;indirizzo IPv4, l&#39;indirizzo IPv6 se IPv6 è abilitato, l&#39;indirizzo di loopback e una voce localhost. I nomi aggiunti all&#39;elenco Referente consentito vengono restituiti dal sistema operativo host. Ad esempio, un server con indirizzo IP pari a 10.40.54.187 includerà le seguenti voci: `https://server-name:0, https://10.40.54.187:0, https://127.0.0.1:0, http://localhost:0`. Per qualsiasi nome non qualificato restituito dal sistema operativo host (nomi che non hanno indirizzo IPv4, indirizzo IPv6 o nome di dominio qualificato)  inserì nell&#39;elenco Consentiti non viene aggiornato. Modificare l&#39;elenco Referente consentito in base all&#39;ambiente aziendale. Non distribuire il server moduli nell&#39;ambiente di produzione con l&#39;elenco Referente consentito predefinito. Dopo aver modificato uno qualsiasi degli URI, delle eccezioni di riferimento o di riferimento consentiti, assicurarsi di riavviare il server affinché le modifiche abbiano effetto.

**Gestione dell&#39;elenco di riferimenti consentiti**

Puoi gestire l’elenco Referente consentito dall’interfaccia di gestione utente della console di amministrazione. L&#39;interfaccia di gestione utente fornisce le funzionalità per creare, modificare o eliminare l&#39;elenco. Fare riferimento alla sezione * [Prevenzione degli attacchi CSRF](/help/forms/using/admin-help/preventing-csrf-attacks.md)* della *guida di amministrazione* per ulteriori informazioni sull&#39;utilizzo dell&#39;elenco di riferimenti consentiti.

**Gestione delle eccezioni di riferimento consentite e degli elenchi URI consentiti**

 AEM Forms su JEE fornisce API per gestire l&#39;elenco Eccezione referente consentita e l&#39;elenco URI consentito. Potete utilizzare queste API per recuperare, creare, modificare o eliminare l&#39;elenco. Segue un elenco di API disponibili:

* createAllowedURIsList
* getAllowedURIsList
* updateAllowedURIsList
* deleteAllowedURIsList
* addAllowedRefererExceptions
* getAllowedRefererExceptions
* updateAllowedRefererExceptions
* deleteAllowedRefererExceptions

Per ulteriori informazioni sulle API, fare riferimento alla sezione*  AEM Forms su JEE API Reference*.

Utilizzare l&#39;elenco ***LC_GLOBAL_ALLOWED_REFERER_EXCEPTION*** per Eccezioni referente consentite a livello globale, ad esempio per definire le eccezioni applicabili a tutte le applicazioni. Questo elenco contiene solo URI con percorso assoluto (ad es. `/index.html`) o un percorso relativo (ad esempio `/sample/`). Potete anche aggiungere un&#39;espressione regolare alla fine di un URI relativo, ad esempio `/sample/(.)*`.

L&#39;ID elenco ***LC_GLOBAL_ALLOWED_REFERER_EXCEPTION*** è definito come una costante nella classe `UMConstants` dello spazio dei nomi `com.adobe.idp.um.api`, trovata in `adobe-usermanager-client.jar`. Potete utilizzare le  API AEM Forms per creare, modificare o modificare questo elenco. Ad esempio, per creare l&#39;elenco Eccezioni referente Global Allowed utilizzare:

```java
addAllowedRefererExceptions(UMConstants.LC_GLOBAL_ALLOWED_REFERER_EXCEPTION, Arrays.asList("/index.html", "/sample/(.)*"))
```

Utilizzare l&#39;elenco ***CSRF_ALLOWED_REFERER_EXCEPTIONS*** per le eccezioni specifiche dell&#39;applicazione.

**Disattivazione del filtro di riferimento**

Se il filtro di riferimento blocca completamente l&#39;accesso al server dei moduli e non è possibile modificare l&#39;elenco di riferimento consentiti, è possibile aggiornare lo script di avvio del server e disabilitare il filtro di riferimento.

Includete l&#39;argomento JAVA `-Dlc.um.csrffilter.disabled=true` nello script di avvio e riavviate il server. Assicurarsi di eliminare l&#39;argomento JAVA dopo aver riconfigurato l&#39;elenco Referente consentito.

**Applicazione di filtri per file WAR personalizzati**

Potreste aver creato file WAR personalizzati da utilizzare con  AEM Forms su JEE per soddisfare i vostri requisiti aziendali. Per abilitare il filtro referente per i file WAR personalizzati, includi ***adobe-usermanager-client.jar*** nel percorso di classe per WAR e includi una voce di filtro nel file* web.xml* con i seguenti parametri:

**CSRF_CHECK_** GETScontrolla il controllo Referente sulle richieste di GET. Se questo parametro non è definito, il valore predefinito è false. Includete questo parametro solo se desiderate filtrare le richieste di GET.

**CSRF_ALLOWED_REFERER_** EXCEPTIONS è l&#39;ID dell&#39;elenco Eccezioni referente consentite. Il filtro Referente impedisce alle richieste provenienti da Referenti nell&#39;elenco identificato dall&#39;ID elenco di richiamare risorse sul server dei moduli.

**CSRF_ALLOWED_URIS_LIST_** NAME è l&#39;ID dell&#39;elenco URI consentiti. Il filtro referente non blocca le richieste per nessuna delle risorse nell&#39;elenco identificato dall&#39;ID elenco, indipendentemente dal valore dell&#39;intestazione Referente nella richiesta.

**CSRF_ALLOW_NULL_** REFERERcontrolla il comportamento del filtro referente quando il referente è nullo o non è presente. Se questo parametro non è definito, il valore predefinito è false. Includete questo parametro solo se desiderate consentire Referenti Null. Consentendo ai referenti nulli è possibile che alcuni tipi di attacchi Cross Site Request Forgery.

**CSRF_NULL_REFERER_** EXCEPTIONS è un elenco degli URI per i quali non viene eseguito un controllo Referrer quando il Referente è nullo. Questo parametro è attivato solo quando *CSRF_ALLOW_NULL_REFERER* è impostato su false. Separate più URI nell&#39;elenco con una virgola.

Di seguito è riportato un esempio della voce del filtro nel file *web.xml* per un file ***SAMPLE*** WAR:

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

Se le richieste server legittime vengono bloccate dal filtro CSRF, provate una delle seguenti operazioni:

* Se la richiesta rifiutata dispone di un&#39;intestazione Referente, è consigliabile aggiungerla all&#39;elenco Referente consentito. Aggiungi solo referente affidabile.
* Se la richiesta rifiutata non dispone di un&#39;intestazione Referente, modificate l&#39;applicazione client per includere un&#39;intestazione Referente.
* Se il client può funzionare in un browser, provate a utilizzare tale modello di distribuzione.
* Come ultima risorsa è possibile aggiungere la risorsa all&#39;elenco URI consentiti. Questa impostazione non è consigliata.

## Configurazione della rete protetta {#secure-network-configuration}

In questa sezione vengono descritti i protocolli e le porte richiesti da  AEM Forms su JEE e vengono fornite raccomandazioni per la distribuzione  AEM Forms su JEE in una configurazione di rete protetta.

### Protocolli di rete utilizzati da  AEM Forms su JEE {#network-protocols-used-by-aem-forms-on-jee}

Quando si configura un&#39;architettura di rete protetta come descritto nella sezione precedente, i seguenti protocolli di rete sono necessari per l&#39;interazione tra  AEM Forms su JEE e altri sistemi nella rete aziendale.

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
     <li><p> Adobe Reader® utilizza SOAP per  AEM Forms sui servizi Web del server JEE</p> </li> 
     <li><p> Adobe applicazioni di Flash® utilizzano SOAP per i servizi Web del server dei moduli</p> </li> 
     <li><p> le chiamate AEM Forms su SDK JEE quando utilizzate in modalità SOAP</p> </li> 
     <li><p>Ambiente di progettazione di Workbench</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>RMI</p> </td> 
   <td><p> le chiamate AEM Forms su SDK JEE quando utilizzate in modalità Enterprise JavaBeans (EJB)</p> </td> 
  </tr> 
  <tr> 
   <td><p>IMAP/POP3</p> </td> 
   <td> 
    <ul> 
     <li><p>Ingresso basato su e-mail a un servizio (endpoint e-mail)</p> </li> 
     <li><p>Notifiche attività utente tramite e-mail</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>IO file UNC</p> </td> 
   <td><p> AEM Forms sul monitoraggio JEE delle cartelle esaminate per l'input a un servizio (endpoint cartella controllato)</p> </td> 
  </tr> 
  <tr> 
   <td><p>LDAP</p> </td> 
   <td> 
    <ul> 
     <li><p>Sincronizzazione delle informazioni dell’utente e del gruppo organizzativo in una directory</p> </li> 
     <li><p>Autenticazione LDAP per utenti interattivi</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>JDBC</p> </td> 
   <td> 
    <ul> 
     <li><p>Richieste di query e procedure effettuate a un database esterno durante l'esecuzione di un processo utilizzando il servizio JDBC</p> </li> 
     <li><p>Accesso interno  AEM Forms nell'archivio JEE</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>WebDAV</p> </td> 
   <td><p>Consente la navigazione remota dell'AEM Forms  nell'archivio di progettazione JEE (moduli, frammenti e così via) da parte di qualsiasi client WebDAV</p> </td> 
  </tr> 
  <tr> 
   <td><p>AMF</p> </td> 
   <td><p> applicazioni di Flash di Adobe, in cui  AEM Forms sui servizi server JEE sono configurati con un endpoint remoto</p> </td> 
  </tr> 
  <tr> 
   <td><p>JMX</p> </td> 
   <td><p> AEM Forms su JEE espone MBeans per il monitoraggio utilizzando JMX</p> </td> 
  </tr> 
 </tbody> 
</table>

### Porte per i server applicazione {#ports-for-application-servers}

Questa sezione descrive le porte predefinite (e gli intervalli di configurazione alternativi) per ciascun tipo di server applicazioni supportato. Queste porte devono essere abilitate o disattivate sul firewall interno, a seconda della funzionalità di rete che si desidera consentire ai client che si connettono al server applicazioni in esecuzione  AEM Forms su JEE.

>[!NOTE]
>
>Per impostazione predefinita, il server espone diversi MBeans JMX nello spazio dei nomi adobe.com. Vengono esposte solo le informazioni utili per il monitoraggio dello stato del server. Tuttavia, per impedire la divulgazione delle informazioni, è necessario impedire ai chiamanti in una rete non affidabile di ricercare MBeans JMX e di accedere alle metriche di integrità.

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
   <td><p>Accesso alle applicazioni Web</p> </td> 
   <td><p>[JBOSS_Root]/standalone/configuration/lc_[database].xml</p> <p>Porta del connettore HTTP/1.1 8080</p> <p>Porta connettore AJP 1.3 8009</p> <p>Porta connettore SSL/TLS 8443</p> </td> 
  </tr> 
  <tr> 
   <td><p>Supporto CORBA</p> </td> 
   <td><p>[Radice JBoss]/server/all/conf/jacorb.properties</p> <p>OAPort 3528</p> <p>OASSLPort 3529</p> </td> 
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
   <td><p>Accesso alle applicazioni Web</p> </td> 
   <td> 
    <ul> 
     <li><p>Porta di ascolto di Admin Server: il valore predefinito è 7001</p> </li> 
     <li><p>Porta di ascolto SSL di Admin Server: il valore predefinito è 7002</p> </li> 
     <li><p>Porta configurata per il server gestito, ad esempio 8001</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>Porte di amministrazione WebLogic non necessarie per l'accesso a  AEM Forms su JEE</p> </td> 
   <td> 
    <ul> 
     <li><p>Porta di ascolto del server gestito: Configurabile da 1 a 65534</p> </li> 
     <li><p>Porta di ascolto SSL del server gestito: Configurabile da 1 a 65534</p> </li> 
     <li><p>Porta di ascolto di Node Manager: il valore predefinito è 5556</p> </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>

**Porte WebSphere**

Per informazioni sulle porte WebSphere che  AEM Forms su JEE richiede, passare all&#39;impostazione del numero di porta nell&#39;interfaccia utente del server applicazioni WebSphere.

### Configurazione di SSL {#configuring-ssl}

Facendo riferimento all&#39;architettura fisica descritta nella sezione [ AEM Forms sull&#39;architettura fisica JEE](hardening-aem-forms-jee-environment.md#aem-forms-on-jee-physical-architecture), è necessario configurare SSL per tutte le connessioni che si intende utilizzare. Nello specifico, tutte le connessioni SOAP devono essere eseguite su SSL per impedire l&#39;esposizione delle credenziali utente in una rete.

Per istruzioni su come configurare SSL su JBoss, WebLogic e WebSphere, vedere &quot;Configuring SSL&quot; nella [guida di amministrazione](https://www.adobe.com/go/learn_aemforms_admin_64).

Per istruzioni su come importare certificati in JVM (Java Virtual Machine) configurati per un server AEM Forms , vedere la sezione Autenticazione reciproca nella [ Guida di AEM Forms Workbench](http://www.adobe.com/go/learn_aemforms_workbench_65).

### Configurazione del reindirizzamento SSL {#configuring-ssl-redirect}

Dopo aver configurato il server applicazione per supportare SSL, è necessario assicurarsi che tutto il traffico HTTP verso le applicazioni e i servizi venga imposto per utilizzare la porta SSL.

Per configurare il reindirizzamento SSL per WebSphere o WebLogic, consulta la documentazione del server applicazione.

1. Aprite il prompt dei comandi, accedete alla directory /JBOSS_HOME/standalone/configuration ed eseguite il comando seguente:

   `keytool -genkey -alias jboss7 -keyalg RSA -keystore server.keystore -validity 10950`

1. Aprite il file JBOSS_HOME/standalone/configuration/standalone.xml per la modifica.

   Dopo l’elemento &lt;sottosistema xmlns=&quot;urn:jboss:domain:web:1.1&quot; native=&quot;false&quot; default-virtual-server=&quot;default-host&quot;>, aggiungete i seguenti dettagli:

   &lt;connector name=&quot;https&quot; protocol=&quot;HTTP/1.1&quot; scheme=&quot;https&quot; socket-binding=&quot;https&quot; enabled=&quot;true&quot; secure=&quot;true&quot; />

1. Aggiungete il codice seguente nell&#39;elemento https Connector:

   ```xml
   <connector name="https" protocol="HTTP/1.1" scheme="https" socket-binding="https" secure="true" enabled="true"> 
    <ssl name="jboss7_ssl" key-alias="jboss71" password="Tibco321" certificate-key-file="../standalone/configuration/server.keystore" protocol="TLSv1"/> 
    </connector>
   ```

   Salvate e chiudete il file standalone.xml.

## Raccomandazioni di protezione specifiche per Windows {#windows-specific-security-recommendations}

Questa sezione contiene raccomandazioni di protezione specifiche per Windows, se utilizzate per eseguire  AEM Forms su JEE.

### Account di servizio JBoss {#jboss-service-accounts}

L&#39;installazione  AEM Forms su chiavi in mano JEE imposta un account di servizio, per impostazione predefinita, utilizzando l&#39;account di sistema locale. L&#39;account utente del sistema locale integrato dispone di un elevato livello di accessibilità; fa parte del gruppo Amministratori. Se l&#39;identità di un processo di lavoro viene eseguita come account utente del sistema locale, tale processo di lavoro dispone dell&#39;accesso completo all&#39;intero sistema.

#### Eseguire il server applicazione utilizzando un account non amministrativo {#run-the-application-server-using-a-non-administrative-account}

1. In Microsoft Management Console (MMC), creare un utente locale che consenta al servizio server moduli di accedere come segue:

   * Selezionare **L&#39;utente non può cambiare la password**.
   * Nella scheda **Membro di**, assicurarsi che il gruppo Utenti sia elencato.

1. Selezionare **Settings** > **Administrative Tools** > **Services**.
1. Fare doppio clic sul servizio del server applicazioni e arrestare il servizio.
1. Nella scheda **Accedi**, selezionare **Questo account**, individuare l&#39;account utente creato e immettere la password per l&#39;account.
1. Nella finestra Impostazioni protezione locale, in Assegnazione diritti utente, assegnare i seguenti diritti all&#39;account utente in cui è in esecuzione il server moduli:

   * Rifiuta accesso tramite Servizi terminal
   * Rifiuta accesso in locale
   * Accedi come servizio (dovrebbe essere già impostato)

1. Assegnate al nuovo account utente autorizzazioni di modifica nelle seguenti directory:
   * **Directory** Global Document Storage (GDS): La posizione della directory GDS viene configurata manualmente durante il processo di installazione di AEM Forms . Se l&#39;impostazione della posizione rimane vuota durante l&#39;installazione, per impostazione predefinita la posizione corrisponde a una directory nell&#39;installazione del server applicazione in `[JBoss root]/server/[type]/svcnative/DocumentStorage`
   * **Directory** CRX-Repository: Il percorso predefinito è  `[AEM-Forms-installation-location]\crx-repository`
   * **directory** temporanee AEM Forms:
      * (Windows) Percorso TMP o TEMP impostato nelle variabili di ambiente
      * (AIX, Linux o Solaris) Directory principale dell&#39;utente registrato
Nei sistemi basati su UNIX, un utente non root può utilizzare la seguente directory come directory temporanea:
      * (Linux) /var/tmp o /usr/tmp
      * (AIX) /tmp o /usr/tmp
      * (Solaris) /var/tmp o /usr/tmp
1. Assegnate al nuovo account utente autorizzazioni di scrittura sulle seguenti directory:
   * [JBoss-directory]\standalone\deployment
   * [JBoss-directory]\standalone\
   * [JBoss-directory]\bin\

   >[!NOTE]
   >
   > Il percorso di installazione predefinito di JBoss Application Server:
   > * Windows: C:\Adobe\Adobe_Experience_Manager_Forms\jboss
   > * Linux: /opt/jboss/.


1. Avviate il servizio server applicazione.

### Protezione del file system {#file-system-security}

 AEM Forms su JEE utilizza il file system nei seguenti modi:

* Memorizza i file temporanei utilizzati durante l&#39;elaborazione dell&#39;input e dell&#39;output del documento
* Memorizza i file nell&#39;archivio globale utilizzati per supportare i componenti della soluzione installati
* Le cartelle esaminate archiviano i file rilasciati che vengono utilizzati come input per un servizio da un percorso di cartella del file system

Quando si utilizzano le cartelle esaminate per inviare e ricevere documenti con un servizio server moduli, prendere ulteriori precauzioni con la protezione del file system. Quando un utente rilascia del contenuto nella cartella esaminata, tale contenuto viene esposto attraverso la cartella esaminata. In questo caso, il servizio non autentica l&#39;utente finale effettivo. Al contrario, si basa sulla protezione di livello ACL e Condivisione per essere impostata a livello di cartella per determinare chi può richiamare efficacemente il servizio.

## Raccomandazioni di protezione specifiche per JBoss {#jboss-specific-security-recommendations}

Questa sezione contiene raccomandazioni di configurazione del server applicazione specifiche per JBoss 7.0.6, se utilizzate per eseguire  AEM Forms su JEE.

### Disattiva console di gestione JBoss e console JMX {#disable-jboss-management-console-and-jmx-console}

L’accesso alla console di gestione JBoss e alla console JMX è già configurato (il monitoraggio JMX è disabilitato) quando si installa  AEM Forms su JEE su JBoss utilizzando il metodo di installazione chiavi in mano. Se utilizzate un server applicazioni JBoss personalizzato, accertatevi che l’accesso alla console di gestione JBoss e alla console di monitoraggio JMX sia protetto. L&#39;accesso alla console di monitoraggio JMX è impostato nel file di configurazione JBoss denominato jmx-invoker-service.xml.

### Disabilita esplorazione directory {#disable-directory-browsing}

Dopo aver effettuato l’accesso alla console di amministrazione, è possibile sfogliare l’elenco di directory della console modificando l’URL. Ad esempio, se modificate l’URL in uno dei seguenti URL, potrebbe comparire un elenco di directory:

```java
https://<servername>:8080/adminui/secured/ 
https://<servername>:8080/um/
```

## Raccomandazioni per la protezione specifiche di WebLogic {#weblogic-specific-security-recommendations}

Questa sezione contiene le raccomandazioni di configurazione del server applicazione per proteggere WebLogic 9.1 quando si esegue  AEM Forms su JEE.

### Disabilita esplorazione directory {#disable_directory_browsing-1}

Impostate le proprietà index-directory nel file weblogic.xml su `false`, come illustrato nell&#39;esempio seguente:

```xml
<container-descriptor> 
    <index-directory-enabled>false 
    </index-directory-enabled> 
</container-descriptor>
```

### Abilita porta SSL WebLogic {#enable-weblogic-ssl-port}

Per impostazione predefinita, WebLogic non abilita la porta di ascolto SSL predefinita, 7002. Abilita questa porta nella console di amministrazione del server WebLogic prima di configurare SSL.

## Raccomandazioni di protezione specifiche per WebSphere {#websphere-specific-security-recommendations}

Questa sezione contiene le raccomandazioni di configurazione del server applicazione per proteggere WebSphere in esecuzione  AEM Forms su JEE.

### Disabilita esplorazione directory {#disable_directory_browsing-2}

Impostate la proprietà `directoryBrowsingEnabled` nel file ibm-web-ext.xml su `false`.

### Abilita protezione amministrativa di WebSphere {#enable-websphere-administrative-security}

1. Accedete alla console di amministrazione di WebSphere.
1. Nella struttura di navigazione, passare a **Sicurezza** > **Sicurezza globale**
1. Selezionare **Abilita protezione amministrativa**.
1. Deselezionare sia **Abilita protezione applicazione** che **Usa protezione Java 2**.
1. Fare clic su **OK** o su **Applica**.
1. Nella casella **Messaggi**, fare clic su **Salva direttamente nella configurazione principale**.