---
title: Considerazioni generali sulla sicurezza per AEM Forms su JEE
seo-title: General Security Considerations for AEM Forms on JEE
description: Scopri come prepararti a rendere più rigido il tuo AEM Forms nell’ambiente JEE.
seo-description: Learn how to prepare for hardening your AEM Forms on JEE environment.
uuid: 4d098731-fc8f-41d7-98b5-5c2e31211614
content-type: reference
topic-tags: Security
products: SG_EXPERIENCEMANAGER/6.4
discoiquuid: 64bc6018-2828-4634-9275-48f1d411452b
docset: aem65
role: Admin
exl-id: 3f150dd5-f486-4f16-9de9-035cde53b034
source-git-commit: d3923e5e693e7426ee57e81e203f31964a23af3a
workflow-type: tm+mt
source-wordcount: '1060'
ht-degree: 1%

---

# Considerazioni generali sulla sicurezza per AEM Forms su JEE{#general-security-considerations-for-aem-forms-on-jee}

Questo articolo fornisce informazioni introduttive che ti aiutano a prepararti a rendere più rigido il tuo ambiente AEM Forms. Include informazioni preliminari su AEM Forms su JEE, sistema operativo, server applicazioni e sicurezza del database. Rivedi queste informazioni prima di continuare a bloccare il tuo ambiente.

## Informazioni di sicurezza specifiche per il fornitore {#vendor-specific-security-information}

Questa sezione contiene informazioni relative alla sicurezza su sistemi operativi, server di applicazioni e database incorporati nella soluzione AEM Forms on JEE.

Utilizzare i collegamenti presenti in questa sezione per trovare informazioni di sicurezza specifiche per il sistema operativo, il database e il server applicazioni.

### Informazioni sulla sicurezza del sistema operativo {#operating-system-security-information}

Quando proteggi il sistema operativo, considera attentamente l&#39;implementazione delle misure descritte dal fornitore del sistema operativo, tra cui:

* Definizione e controllo di utenti, ruoli e privilegi
* Monitoraggio dei registri e dei percorsi di controllo
* Rimozione di servizi e applicazioni superflui
* Backup dei file

Per informazioni sulla sicurezza dei sistemi operativi supportati da AEM Forms su JEE, consulta la tabella seguente:

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
   <td><p><a href="https://www.ibm.com/support/knowledgecenter/ssw_aix_72/com.ibm.aix.security/security-kickoff.htm" target="_blank">Vantaggi per la sicurezza di IBM® AIX®</a></p> </td>
  </tr>
  <tr>
   <td><p>Microsoft® Windows Server® 2016 </p> </td>
   <td><p><a href="https://cloudblogs.microsoft.com/windowsserver/2017/08/22/now-available-windows-server-2016-security-guide/">Guida alla sicurezza di Windows Server 2016</a></p> </td>
  </tr>
  <tr>
   <td><p>Red Hat® Linux® AP o ES</p> </td>
   <td><p><a href="https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/pdf/security_guide/Red_Hat_Enterprise_Linux-7-Security_Guide-en-US.pdf" target="_blank">Guida alla sicurezza di Red Hat® Enterprise Linux®</a></p> </td>
  </tr>
  <tr>
   <td><p>Sun Solaris™ 11</p> </td>
   <td><p><a href="https://docs.oracle.com/cd/E53394_01/html/E54807/index.html" target="_blank">Linee guida per la sicurezza e l’indurimento</a></p> </td>
  </tr>
  <tr>
   <td>Oracle Linux® 7 Aggiornamento 3</td>
   <td><a href="https://docs.oracle.com/cd/E52668_01/E54670/E54670.pdf" target="_blank">Guida alla sicurezza per la versione 7</a><br /> </td>
  </tr>
  <tr>
   <td>CentOS 7<sup> </sup></td>
   <td><a href="https://wiki.centos.org/HowTos/OS_Protection" target="_blank">Documentazione sulla protezione</a></td>
  </tr>
 </tbody>
</table>

### Informazioni sulla sicurezza del server applicazioni {#application-server-security-information}

Quando proteggi il server applicazioni, considera attentamente l&#39;implementazione delle misure descritte dal fornitore del server, tra cui:

* Utilizzo di un nome utente amministratore non ovvio
* Disattivazione dei servizi non necessari
* Protezione della console manager
* Abilitazione dei cookie sicuri
* Chiusura delle porte non necessarie
* Limitazione dei client per indirizzi IP o domini
* Utilizzo di Java™ Security Manager per limitare programmaticamente i privilegi

Per informazioni sulla sicurezza dei server applicazioni supportati da AEM Forms su JEE, consulta le risorse presenti in questa tabella.

<table>
 <thead>
  <tr>
   <th><p>Server applicazioni</p> </th>
   <th><p>Risorsa di sicurezza</p> </th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>Oracle WebLogic®</p> </td>
   <td><p>Cerca informazioni sulla sicurezza WebLogic in <a href="https://docs.oracle.com/">https://docs.oracle.com/</a>.</p> </td>
  </tr>
  <tr>
   <td><p>IBM® WebSphere®</p> </td>
   <td><p><a href="https://www.ibm.com/developerworks/websphere/zones/was/security/" target="_blank">Sicurezza delle applicazioni e del loro ambiente</a></p> </td>
  </tr>
  <tr>
   <td><p>Red Hat® JBoss®</p> </td>
   <td><p><a href="https://docs.jboss.org/author/display/AS7/Security%20subsystem%20configuration.html">Configurazione del sottosistema sicurezza</a></p> </td>
  </tr>
 </tbody>
</table>

### Informazioni sulla protezione del database {#database-security-information}

Durante la protezione del database, è consigliabile implementare le misure descritte dal fornitore del database, tra cui:

* Limitazione delle operazioni con elenchi di controllo accessi (ACL)
* Utilizzo di porte non standard
* Nascondere il database dietro un firewall
* Crittografia dei dati sensibili prima di scriverli nel database (consulta la documentazione del produttore del database)

Per informazioni sulla sicurezza dei database supportati da AEM Forms su JEE, consulta le risorse presenti in questa tabella.

<table>
 <thead>
  <tr>
   <th><p>Database</p> </th>
   <th><p>Risorsa di sicurezza</p> </th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>IBM® DB2® 11.1</p> </td>
   <td><p><a href="https://www-01.ibm.com/software/data/db2/library/">Libreria della famiglia di prodotti DB2®</a></p> </td>
  </tr>
  <tr>
   <td><p>Microsoft® SQL Server 2016</p> </td>
   <td>Cercare sul Web "SQL Server 2016: Sicurezza"</td>
  </tr>
  <tr>
   <td><p>MySQL 5</p> </td>
   <td><p><a href="https://dev.mysql.com/doc/refman/5.0/en/security.html">Problemi di sicurezza generali di MySQL 5.0</a></p> <p><a href="https://dev.mysql.com/doc/refman/5.1/en/security.html">Problemi di sicurezza generali di MySQL 5.1</a></p> </td>
  </tr>
  <tr>
   <td><p>Oracle® 12c</p> </td>
   <td><p>Vedi il capitolo Sicurezza in <a href="https://docs.oracle.com/database/121/TDPSG/GUID-6E2F4E53-5D87-4FCD-9C9C-6792217D7014.htm#TDPSG94426" target="_blank">Documentazione dell'Oracle 12 octies</a></p> </td>
  </tr>
 </tbody>
</table>

Questa tabella descrive le porte predefinite che devono essere aperte durante il processo di configurazione AEM Forms on JEE. Se ti connetti su https, regola di conseguenza le informazioni sulla porta e gli indirizzi IP. Per ulteriori informazioni sulla configurazione delle porte, consulta la sezione *Installazione e distribuzione di AEM Forms su JEE* documento per il server applicazioni.

<table>
 <thead>
  <tr>
   <th><p>Prodotto o servizio</p> </th>
   <th><p>Numero di porta</p> </th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>JBoss®</p> </td>
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
   <td>&gt;<p>WebSphere®</p> </td>
   <td><p>9060, se Global Security è abilitato, il valore di porta SSL predefinito è 9043.</p> <p>9080</p> </td>
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
   <td>&gt;<p>Oracle</p> </td>
   <td><p>1521</p> </td>
  </tr>
  <tr>
   <td>&gt;<p>DB2®</p> </td>
   <td><p>50000</p> </td>
  </tr>
  <tr>
   <td>&gt;<p>SQL Server</p> </td>
   <td><p>1433</p> </td>
  </tr>
  <tr>
   <td>&gt;<p>LDAP</p> </td>
   <td><p>La porta su cui è in esecuzione il server LDAP. La porta predefinita è in genere 389. Tuttavia, se selezioni l’opzione SSL, la porta predefinita è in genere 636. Conferma con il tuo amministratore LDAP quale porta specificare.</p> </td>
  </tr>
 </tbody>
</table>

### Configurazione di JBoss® per utilizzare una porta HTTP non predefinita {#configuring-jboss-to-use-a-non-default-http-port}

JBoss® Application Server utilizza 8080 come porta HTTP predefinita. JBoss® dispone anche di porte preconfigurate 8180, 8280 e 8380, che sono commentate nel file jboss-service.xml. Se nel computer è già presente un&#39;applicazione che utilizza questa porta, modificare la porta utilizzata da AEM Forms su JEE seguendo questi passaggi:

1. Apri il file seguente per la modifica:

   Installazione di un singolo server: [Radice JBoss®]/standalone/configuration/standalone.xml

   Installazioni cluster: [Radice JBoss®]/domain/configuration/domain.xml

1. Modifica il valore di **porta** nella **&lt;socket-binding>** a un numero di porta personalizzato. Ad esempio, la porta 8090 viene utilizzata come segue:

   &lt;socket-binding name=&quot;http&quot; port=&quot;8090&quot;/>

1. Salva e chiudi il file 
1. Riavvia il server dell&#39;applicazione JBoss®.

## Considerazioni sulla sicurezza JEE per AEM Forms {#aem-forms-on-jee-security-considerations}

Questa sezione descrive alcuni problemi di sicurezza specifici di JEE che dovresti conoscere.

### Credenziali e-mail non crittografate nel database {#email-credentials-not-encrypted-in-database}

Le credenziali e-mail archiviate dalle applicazioni non vengono crittografate prima di essere memorizzate nel database AEM Forms su JEE. Quando si configura un endpoint di servizio per l&#39;utilizzo dell&#39;e-mail, tutte le informazioni sulla password utilizzate come parte della configurazione dell&#39;endpoint non vengono crittografate quando vengono memorizzate nel database.

### Contenuto sensibile per Rights Management nel database {#sensitive-content-for-rights-management-in-the-database}

AEM Forms su JEE utilizza il database AEM Forms su JEE per memorizzare informazioni sensibili sulle chiavi dei documenti e altro materiale di crittografia utilizzato per i documenti di policy. Proteggere il database dall&#39;intrusione aiuta a proteggere queste informazioni sensibili.

### Password in formato testo trasparente {#password-in-clear-text-format-in-adobe-ds-xml}

Il server applicazioni utilizzato per eseguire AEM Forms su JEE richiede una propria configurazione per l&#39;accesso al database tramite un&#39;origine dati configurata sul server applicazioni. Assicurati che il server applicazioni non esponga la password del database in testo libero nel file di configurazione dell&#39;origine dati.

Lc_[database]Il file .xml non deve contenere password in formato testo libero. Consultare il fornitore dell&#39;application server su come crittografare queste password per l&#39;application server.

>[!NOTE]
>
>Il programma di installazione chiavi in mano di AEM Forms su JEE JBoss® crittografa la password del database.

Per impostazione predefinita, IBM® WebSphere® Application Server e Oracle WebLogic Server possono crittografare le password delle origini dati. Tuttavia, conferma con la documentazione del server dell&#39;applicazione per assicurarti che ciò si verifichi.

### Protezione della chiave privata archiviata nell&#39;archivio fonti attendibili {#protecting-the-private-key-stored-in-trust-store}

Le chiavi private o le credenziali importate in Trust Store sono memorizzate in AEM Forms nel database JEE. Prendere le dovute precauzioni per proteggere il database e limitare l&#39;accesso solo agli amministratori designati.
