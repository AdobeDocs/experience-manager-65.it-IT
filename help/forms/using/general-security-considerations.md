---
title: Considerazioni generali sulla sicurezza per AEM Forms su JEE
description: Scopri come prepararti per irrigidire l’ambiente AEM Forms su JEE.
content-type: reference
topic-tags: Security
products: SG_EXPERIENCEMANAGER/6.4
docset: aem65
role: Admin,User
exl-id: 3f150dd5-f486-4f16-9de9-035cde53b034
solution: Experience Manager, Experience Manager Forms
feature: Security, Adaptive Forms
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '1030'
ht-degree: 1%

---

# Considerazioni generali sulla sicurezza per AEM Forms su JEE{#general-security-considerations-for-aem-forms-on-jee}

Questo articolo fornisce informazioni introduttive utili per prepararti a rendere più solido l’ambiente AEM Forms. Include informazioni sui prerequisiti di AEM Forms per JEE, il sistema operativo, il server applicazioni e la sicurezza del database. Rivedi queste informazioni prima di continuare a bloccare l’ambiente.

## Informazioni di sicurezza specifiche del fornitore {#vendor-specific-security-information}

Questa sezione contiene informazioni relative alla sicurezza su sistemi operativi, server applicazioni e database incorporati nella soluzione AEM Forms on JEE.

Utilizzare i collegamenti presenti in questa sezione per trovare informazioni di protezione specifiche per il sistema operativo, il database e il server applicazioni.

### Informazioni sulla sicurezza del sistema operativo {#operating-system-security-information}

Quando si protegge il sistema operativo, valutare attentamente l&#39;implementazione delle misure descritte dal fornitore del sistema operativo, tra cui:

* Definizione e controllo di utenti, ruoli e privilegi
* Registri di monitoraggio e audit trail
* Rimozione di servizi e applicazioni non necessari
* Backup dei file

Per informazioni sulla sicurezza dei sistemi operativi supportati da AEM Forms su JEE, consulta le risorse nella tabella:

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
   <td><p><a href="https://www.ibm.com/support/knowledgecenter/ssw_aix_72/com.ibm.aix.security/security-kickoff.htm" target="_blank">Vantaggi della sicurezza di IBM® AIX®</a></p> </td>
  </tr>
  <tr>
   <td><p>Microsoft® Windows Server® 2016 </p> </td>
   <td><p><a href="https://cloudblogs.microsoft.com/windowsserver/2017/08/22/now-available-windows-server-2016-security-guide/">Guida alla protezione di Windows Server 2016</a></p> </td>
  </tr>
  <tr>
   <td><p>Red Hat® Linux® AP o ES</p> </td>
   <td><p><a href="https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/pdf/security_guide/Red_Hat_Enterprise_Linux-7-Security_Guide-en-US.pdf" target="_blank">Guida alla sicurezza di Red Hat® Enterprise Linux®</a></p> </td>
  </tr>
  <tr>
   <td><p>Sun Solaris™ 11</p> </td>
   <td><p><a href="https://docs.oracle.com/cd/E53394_01/html/E54807/index.html" target="_blank">Linee guida per la protezione e la protezione</a></p> </td>
  </tr>
  <tr>
   <td>Oracle Linux® 7 Aggiornamento 3</td>
   <td><a href="https://docs.oracle.com/en/operating-systems/oracle-linux/7/security/" target="_blank">Guida alla sicurezza per la versione 7</a><br /> </td>
  </tr>
  <tr>
   <td>CentOS 7<sup> </sup></td>
   <td><a href="https://wiki.centos.org/HowTos/OS_Protection" target="_blank">Documentazione sulla protezione</a></td>
  </tr>
 </tbody>
</table>

### Informazioni sulla sicurezza del server applicazioni {#application-server-security-information}

Quando si protegge il server applicazioni, è consigliabile implementare con attenzione le misure descritte dal fornitore del server, tra cui:

* Utilizzo di un nome utente amministratore non ovvio
* Disabilitazione dei servizi non necessari
* Protezione di Console Manager
* Abilitazione dei cookie protetti
* Chiusura delle porte non necessarie
* Limitazione dei client per indirizzi IP o domini
* Utilizzo di Java™ Security Manager per limitare i privilegi a livello di programmazione

Per informazioni sulla sicurezza dei server applicazioni supportati da AEM Forms su JEE, consulta le risorse in questa tabella.

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
   <td><p>Cerca informazioni sulla sicurezza di WebLogic all'indirizzo <a href="https://docs.oracle.com/">https://docs.oracle.com/</a>.</p> </td>
  </tr>
  <tr>
   <td><p>IBM® WebSphere®</p> </td>
   <td><p><a href="https://www.ibm.com/developerworks/websphere/zones/was/security/" target="_blank">Protezione delle applicazioni e del relativo ambiente</a></p> </td>
  </tr>
  <tr>
   <td><p>Red Hat® JBoss®</p> </td>
   <td><p><a href="https://docs.jboss.org/author/display/AS7/Security%20subsystem%20configuration.html">Configurazione del sottosistema di sicurezza</a></p> </td>
  </tr>
 </tbody>
</table>

### Informazioni sulla sicurezza del database {#database-security-information}

Quando si protegge il database, è consigliabile implementare le misure descritte dal fornitore del database, incluse le seguenti:

* Limitazione delle operazioni con elenchi di controllo di accesso (ACL)
* Utilizzo di porte non standard
* Nascondere il database dietro un firewall
* Crittografia dei dati sensibili prima di scriverli nel database (consultare la documentazione del produttore del database)

Per informazioni sulla sicurezza dei database supportati da AEM Forms su JEE, consulta le risorse in questa tabella.

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
   <td><p><a href="https://www-01.ibm.com/software/data/db2/library/">Libreria famiglia di prodotti DB2®</a></p> </td>
  </tr>
  <tr>
   <td><p>Microsoft® SQL Server 2016</p> </td>
   <td>Cerca sul Web "SQL Server 2016: Security"</td>
  </tr>
  <tr>
   <td><p>MySQL 5</p> </td>
   <td><p><a href="https://dev.mysql.com/doc/refman/5.0/en/security.html">Problemi generali di sicurezza di MySQL 5.0</a></p> <p><a href="https://dev.mysql.com/doc/refman/5.1/en/security.html">Problemi generali di sicurezza di MySQL 5.1</a></p> </td>
  </tr>
  <tr>
   <td><p>Oracle ® 12 quater</p> </td>
   <td><p>Vedere il capitolo Sicurezza in <a href="https://docs.oracle.com/database/121/TDPSG/GUID-6E2F4E53-5D87-4FCD-9C9C-6792217D7014.htm#TDPSG94426" target="_blank">Oracle 12 octies documentazione</a></p> </td>
  </tr>
 </tbody>
</table>

Questa tabella descrive le porte predefinite che devono essere aperte durante il processo di configurazione di AEM Forms su JEE. Se ti connetti tramite https, regola di conseguenza le informazioni sulla porta e gli indirizzi IP. Per ulteriori informazioni sulla configurazione delle porte, vedere *Installazione e distribuzione di AEM Forms su JEE* per il server applicazioni.

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
   <td><p>Impostato dall’amministratore durante la configurazione</p> </td>
  </tr>
  <tr>
   <td>&gt;<p>WebSphere®</p> </td>
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
   <td><p>La porta su cui è in esecuzione il server LDAP. La porta predefinita è in genere 389. Tuttavia, se selezioni l’opzione SSL, la porta predefinita è in genere 636. Verificare con l'amministratore LDAP la porta da specificare.</p> </td>
  </tr>
 </tbody>
</table>

### Configurazione di JBoss® per utilizzare una porta HTTP non predefinita {#configuring-jboss-to-use-a-non-default-http-port}

JBoss® Application Server utilizza 8080 come porta HTTP predefinita. JBoss® dispone anche di porte preconfigurate 8180, 8280 e 8380, che vengono commentate nel file jboss-service.xml. Se nel computer è presente un’applicazione che utilizza già questa porta, modifica la porta utilizzata da AEM Forms su JEE come segue:

1. Apri il seguente file per la modifica:

   Installazione su server singolo: [Directory principale JBoss®]/standalone/configuration/standalone.xml

   Installazioni cluster: [Directory principale JBoss®]/domain/configuration/domain.xml

1. Modifica il valore di **porta** attributo in **&lt;socket-binding>** su un numero di porta personalizzato. Ad esempio, il seguente utilizza la porta 8090:

   &lt;socket-binding name=&quot;http&quot; port=&quot;8090&quot;/>

1. Salva e chiudi il file.
1. Riavvia il server applicazioni JBoss®.

>[!NOTE]
>
> Per riavviare l&#39;SDK, si consiglia di utilizzare il comando &#39;Ctrl + C&#39;. Il riavvio dell’SDK dell’AEM con metodi alternativi, ad esempio l’arresto dei processi Java, può causare incongruenze nell’ambiente di sviluppo dell’AEM.

## Considerazioni sulla sicurezza di AEM Forms su JEE {#aem-forms-on-jee-security-considerations}

Questa sezione descrive alcune AEM Forms sui problemi di sicurezza specifici di JEE che dovresti conoscere.

### Credenziali e-mail non crittografate nel database {#email-credentials-not-encrypted-in-database}

Le credenziali e-mail archiviate dalle applicazioni non vengono crittografate prima di essere memorizzate nel database AEM Forms su JEE. Quando si configura un endpoint di servizio per l&#39;utilizzo di posta elettronica, tutte le informazioni sulla password utilizzate come parte della configurazione dell&#39;endpoint non vengono crittografate quando vengono memorizzate nel database.

### Contenuto riservato per il Rights Management nel database {#sensitive-content-for-rights-management-in-the-database}

AEM Forms su JEE utilizza il database AEM Forms su JEE per memorizzare le informazioni sensibili relative alle chiavi di documenti e altro materiale crittografico utilizzato per i documenti relativi alle policy. Proteggere il database dalle intrusioni è utile per proteggere le informazioni riservate.

### Password in formato testo non crittografato {#password-in-clear-text-format-in-adobe-ds-xml}

Il server applicazioni utilizzato per eseguire AEM Forms su JEE richiede una propria configurazione per accedere al database tramite un’origine dati configurata sul server applicazioni. Verificare che il server applicazioni in uso non esponga la password del database in testo non crittografato nel file di configurazione dell&#39;origine dati.

Il valore lc_[database]Il file xml non deve contenere password in formato testo non crittografato. Rivolgersi al fornitore del server applicazioni per informazioni su come crittografare le password per il server applicazioni.

>[!NOTE]
>
>Il programma di installazione chiavi in mano di AEM Forms su JEE JBoss® crittografa la password del database.

IBM® WebSphere® Application Server e Oracle WebLogic Server possono crittografare le password dell&#39;origine dati per impostazione predefinita. Tuttavia, è necessario confermare con la documentazione del server applicazioni per assicurarsi che ciò avvenga.

### Protezione della chiave privata archiviata nell&#39;archivio fonti attendibili {#protecting-the-private-key-stored-in-trust-store}

Le chiavi private o le credenziali importate nell’archivio fonti attendibili sono memorizzate in AEM Forms nel database JEE. Per proteggere il database e limitare l&#39;accesso solo agli amministratori designati, adottare le precauzioni appropriate.
