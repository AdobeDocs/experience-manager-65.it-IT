---
title: Considerazioni generali sulla sicurezza per  AEM Forms su JEE
seo-title: Considerazioni generali sulla sicurezza per  AEM Forms su JEE
description: Scoprite come preparare l'applicazione dell' AEM Forms nell'ambiente JEE.
seo-description: Scoprite come preparare l'applicazione dell' AEM Forms nell'ambiente JEE.
uuid: 4d098731-fc8f-41d7-98b5-5c2e31211614
content-type: reference
topic-tags: Security
products: SG_EXPERIENCEMANAGER/6.4
discoiquuid: 64bc6018-2828-4634-9275-48f1d411452b
docset: aem65
translation-type: tm+mt
source-git-commit: 06335b9a85414b6b1141dd19c863dfaad0812503
workflow-type: tm+mt
source-wordcount: '1082'
ht-degree: 1%

---


# Considerazioni generali sulla sicurezza per  AEM Forms su JEE{#general-security-considerations-for-aem-forms-on-jee}

Questo articolo fornisce informazioni introduttive che aiutano a prepararsi a rendere più rigido l&#39;ambiente AEM Forms . Include informazioni preliminari su  AEM Forms su JEE, sistema operativo, server applicazioni e sicurezza del database. Rivedete queste informazioni prima di continuare a bloccare l&#39;ambiente.

## Informazioni di sicurezza specifiche per il fornitore {#vendor-specific-security-information}

Questa sezione contiene informazioni relative alla sicurezza su sistemi operativi, server applicazioni e database incorporati nella soluzione AEM Forms  su JEE.

Utilizzare i collegamenti in questa sezione per trovare informazioni di protezione specifiche per il fornitore per il sistema operativo, il database e il server applicazione in uso.

### Informazioni sulla sicurezza del sistema operativo {#operating-system-security-information}

Quando si protegge il sistema operativo, considerare attentamente l&#39;implementazione delle misure descritte dal fornitore del sistema operativo, tra cui:

* Definizione e controllo di utenti, ruoli e privilegi
* Monitoraggio dei registri e dei percorsi di controllo
* Rimozione di servizi e applicazioni non necessari
* Backup dei file

Per informazioni di sicurezza sui sistemi operativi supportati  AEM Forms su JEE, vedere le risorse nella tabella:

<table>
 <thead>
  <tr>
   <th><p>Sistema operativo</p> </th>
   <th><p>Risorsa di sicurezza</p> </th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>IBM® AIX® 7.2</p> </td>
   <td><p><a href="https://www.ibm.com/support/knowledgecenter/ssw_aix_72/com.ibm.aix.security/security-kickoff.htm" target="_blank">Vantaggi per la sicurezza di IBM AIX</a></p> </td>
  </tr>
  <tr>
   <td><p>Microsoft Windows Server® 2016 </p> </td>
   <td><p><a href="https://cloudblogs.microsoft.com/windowsserver/2017/08/22/now-available-windows-server-2016-security-guide/">Guida alla protezione di Windows Server 2016</a></p> </td>
  </tr>
  <tr>
   <td><p>Red Hat® Linux® AP o ES</p> </td>
   <td><p><a href="https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/pdf/security_guide/Red_Hat_Enterprise_Linux-7-Security_Guide-en-US.pdf" target="_blank">Guida alla sicurezza di Red Hat Enterprise Linux</a></p> </td>
  </tr>
  <tr>
   <td><p>Sun Solaris 11</p> </td>
   <td><p><a href="https://docs.oracle.com/cd/E53394_01/html/E54807/index.html" target="_blank">Linee guida per la sicurezza e l'indurimento</a></p> </td>
  </tr>
  <tr>
   <td> Oracle Linux® 7 Update 3</td>
   <td><a href="https://docs.oracle.com/cd/E52668_01/E54670/E54670.pdf" target="_blank">Guida alla sicurezza per la release 7</a><br /> </td>
  </tr>
  <tr>
   <td>CentOS 7<sup> </sup></td>
   <td><a href="https://wiki.centos.org/HowTos/OS_Protection" target="_blank">Documentazione di protezione</a></td>
  </tr>
 </tbody>
</table>

### Informazioni sulla protezione del server applicazioni {#application-server-security-information}

Durante la protezione del server applicazioni, considerare attentamente l&#39;implementazione delle misure descritte dal fornitore del server, tra cui:

* Utilizzo di un nome utente amministratore non ovvio
* Disattivazione di servizi non necessari
* Protezione del console manager
* Abilitazione dei cookie protetti
* Chiusura delle porte non necessarie
* Limitazione dei client per indirizzi IP o domini
* Utilizzo di Java™ Security Manager per limitare programmaticamente i privilegi

Per informazioni sulla protezione dei server delle applicazioni che  AEM Forms su JEE supporta, vedere le risorse in questa tabella.

<table>
 <thead>
  <tr>
   <th><p>Application Server</p> </th>
   <th><p>Risorsa di sicurezza</p> </th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p> Oracle WebLogic®</p> </td>
   <td><p>Cercate informazioni sulla sicurezza WebLogic all'indirizzo <a href="https://download.oracle.com/docs/">https://download.oracle.com/docs/</a>.</p> </td>
  </tr>
  <tr>
   <td><p>IBM WebSphere®</p> </td>
   <td><p><a href="https://www.ibm.com/developerworks/websphere/zones/was/security/" target="_blank">Protezione delle applicazioni e del relativo ambiente</a></p> </td>
  </tr>
  <tr>
   <td><p>Red Hat® JBoss®</p> </td>
   <td><p><a href="https://docs.jboss.org/author/display/AS7/Security+subsystem+configuration">Configurazione del sottosistema di sicurezza</a></p> </td>
  </tr>
 </tbody>
</table>

### Informazioni sulla protezione del database {#database-security-information}

Quando proteggete il database, prendete in considerazione l&#39;implementazione delle misure descritte dal fornitore del database, tra cui:

* Limitazione delle operazioni con elenchi di controllo di accesso (ACL)
* Utilizzo di porte non standard
* Nascondere il database dietro un firewall
* Cifratura di dati sensibili prima di scriverli nel database (consultare la documentazione del produttore del database)

Per informazioni di protezione sui database supportati da AEM Forms su JEE, vedere le risorse in questa tabella.

<table>
 <thead>
  <tr>
   <th><p>Database</p> </th>
   <th><p>Risorsa di sicurezza</p> </th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>IBM DB2® 11.1</p> </td>
   <td><p><a href="https://www-01.ibm.com/software/data/db2/library/">Libreria della famiglia di prodotti DB2</a></p> </td>
  </tr>
  <tr>
   <td><p>Microsoft SQL Server 2016</p> </td>
   <td>Cercate nel Web "SQL Server 2016: Security"</td>
  </tr>
  <tr>
   <td><p>MySQL 5</p> </td>
   <td><p><a href="https://dev.mysql.com/doc/refman/5.0/en/security.html">Problemi generali di protezione di MySQL 5.0</a></p> <p><a href="https://dev.mysql.com/doc/refman/5.1/en/security.html">Problemi generali di protezione di MySQL 5.1</a></p> </td>
  </tr>
  <tr>
   <td><p> Oracle® 12c</p> </td>
   <td><p>Vedere il capitolo Sicurezza nella <a href="https://docs.oracle.com/database/121/TDPSG/GUID-6E2F4E53-5D87-4FCD-9C9C-6792217D7014.htm#TDPSG94426" target="_blank"> documentazione Oracle 12g</a></p> </td>
  </tr>
 </tbody>
</table>

La tabella seguente descrive le porte predefinite che devono essere aperte durante il processo di configurazione di AEM Forms  su JEE. Se vi connettete attraverso https, regolate di conseguenza le informazioni sulla porta e gli indirizzi IP. Per ulteriori informazioni sulla configurazione delle porte, vedere il documento *Installazione e distribuzione  AEM Forms su JEE* per il server applicazioni.

<table>
 <thead>
  <tr>
   <th><p>Prodotto o servizio</p> </th>
   <th><p>Numero porta</p> </th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>JBoss</p> </td>
   <td><p>8080</p> </td>
  </tr>
  <tr>
   <td><p>WebLogic</p> </td>
   <td><p>7001</p> </td>
  </tr>
  <tr>
   <td>&gt;<p>Server gestito WebLogic</p> </td>
   <td><p>Impostato dall'amministratore durante la configurazione</p> </td>
  </tr>
  <tr>
   <td>&gt;<p>WebSphere</p> </td>
   <td><p>9060, se Global Security è abilitato, il valore predefinito della porta SSL è 9043.</p> <p>9080</p> </td>
  </tr>
  <tr>
   <td>&gt;<p>Server BAM</p> </td>
   <td><p>7001</p> </td>
  </tr>
  <tr>
   <td>&gt;<p>SOAP</p> </td>
   <td><p>8880</p> </td>
  </tr>
  <tr>
   <td>&gt;<p>MySQL</p> </td>
   <td><p>3306</p> </td>
  </tr>
  <tr>
   <td>&gt;<p> Oracle</p> </td>
   <td><p>1521</p> </td>
  </tr>
  <tr>
   <td>&gt;<p>DB2</p> </td>
   <td><p>50000</p> </td>
  </tr>
  <tr>
   <td>&gt;<p>SQL Server</p> </td>
   <td><p>1433</p> </td>
  </tr>
  <tr>
   <td>&gt;<p>LDAP</p> </td>
   <td><p>La porta su cui è in esecuzione il server LDAP. La porta predefinita è in genere 389. Tuttavia, se selezionate l’opzione SSL, la porta predefinita è in genere 636. Verificate con l’amministratore LDAP la porta da specificare.</p> </td>
  </tr>
 </tbody>
</table>

### Configurazione di JBoss per utilizzare una porta HTTP non predefinita {#configuring-jboss-to-use-a-non-default-http-port}

Application Server JBoss utilizza 8080 come porta HTTP predefinita. JBoss dispone anche di porte preconfigurate 8180, 8280 e 8380, che vengono commentate nel file jboss-service.xml. Se nel computer è già presente un&#39;applicazione che utilizza questa porta, modificare la porta utilizzata da AEM Forms su JEE seguendo la procedura seguente:

1. Aprite il file seguente per la modifica:

   Installazione su un solo server: [Radice JBoss]/standalone/configuration/standalone.xml

   Installazioni cluster: [Radice JBoss]/domain/configuration/domain.xml

1. Modificate il valore dell&#39;attributo **port** nel tag **&lt;socket-binding>** su un numero di porta personalizzato. Ad esempio, i seguenti utilizzano la porta 8090:

   &lt;socket-binding name=&quot;http&quot; port=&quot;8090&quot; />

1. Salvate e chiudete il file.
1. Riavviare il server applicazione JBoss.

##  AEM Forms su considerazioni di sicurezza JEE {#aem-forms-on-jee-security-considerations}

In questa sezione vengono descritti alcuni  di AEM Forms relativi a problemi di sicurezza specifici per JEE che dovrebbero essere noti.

### Credenziali e-mail non crittografate nel database {#email-credentials-not-encrypted-in-database}

Le credenziali e-mail archiviate dalle applicazioni non vengono crittografate prima di essere memorizzate nel  AEM Forms nel database JEE. Quando configurate un endpoint di servizio per l&#39;utilizzo dell&#39;e-mail, tutte le informazioni sulla password utilizzate come parte della configurazione dell&#39;endpoint non vengono crittografate quando vengono memorizzate nel database.

### Contenuto sensibile ad Rights Management nel database {#sensitive-content-for-rights-management-in-the-database}

 AEM Forms su JEE utilizza l&#39;AEM Forms  nel database JEE per memorizzare informazioni sensibili relative alle chiavi del documento e altro materiale crittografico utilizzato per i documenti dei criteri. Proteggere il database dall&#39;intrusione aiuta a proteggere queste informazioni sensibili.

### Password nel modulo di testo trasparente {#password-in-clear-text-format-in-adobe-ds-xml}

Il server applicazione utilizzato per eseguire  AEM Forms su JEE richiede una propria configurazione per poter accedere al database tramite un&#39;origine dati configurata sul server dell&#39;applicazione. Assicurarsi che il server applicazioni non esponga la password del database in testo libero nel file di configurazione dell&#39;origine dati.

Il file lc_[database].xml non deve contenere password in formato testo chiaro. Per informazioni su come crittografare queste password per il server applicazioni, consultare il fornitore del server applicazioni.

>[!NOTE]
>
>Il programma di installazione della chiave di  AEM Forms su JEE JBoss crittografa la password del database.

Per impostazione predefinita, IBM WebSphere Application Server e  Oracle WebLogic Server possono crittografare le password delle origini dati. Tuttavia, verificate con la documentazione del server applicazione che ciò si verifichi.

### Protezione della chiave privata memorizzata nell&#39;archivio certificati {#protecting-the-private-key-stored-in-trust-store}

Le chiavi private o le credenziali importate in Trust Store sono memorizzate in  AEM Forms nel database JEE. Prendere le dovute precauzioni per proteggere il database e limitare l&#39;accesso solo agli amministratori designati.
