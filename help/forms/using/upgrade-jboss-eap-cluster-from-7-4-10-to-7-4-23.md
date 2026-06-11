---
title: Aggiornamento del cluster EAP JBoss da 7.4.10 a 7.4.23 per AEM Forms su JEE
description: Passaggi aggiuntivi per aggiornare un cluster EAP JBoss da 7.4.10 a 7.4.23 per AEM Forms su JEE.
exl-id: 2c9e7f41-a8d6-4b03-8e5c-1a4f6d9e0b72
solution: Experience Manager, Experience Manager Forms
feature: AEM Forms on JEE
role: User, Developer
source-git-commit: dffa92539a8205387d21d3873ab9424508182f19
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 1%

---

# Aggiornamento del cluster EAP JBoss da 7.4.10 a 7.4.23 per AEM Forms su JEE {#upgrade-jboss-eap-cluster-from-7-4-10-to-7-4-23}

## Panoramica {#overview}

Quando si aggiorna un cluster EAP JBoss dalla versione 7.4.10 alla versione 7.4.23 per AEM Forms su JEE, è necessaria una configurazione aggiuntiva oltre i passaggi di aggiornamento autonomi. Nella nuova installazione di JBoss è necessario aggiornare le impostazioni specifiche del cluster, quali i localizzatori della cache, l&#39;autenticazione master-slave, le associazioni host e la configurazione del controller di dominio.

## Applicabile a {#applies-to}

Il presente articolo si applica a:

* AEM Forms su JEE in esecuzione su JBoss EAP 7.4.10 in un ambiente cluster
* Configurazioni EAP JBoss master-slave su Windows e Linux

## Prerequisiti {#prerequisites}

Completa tutti i passaggi in [Aggiornamento EAP JBoss da 7.4.10 a 7.4.23 per AEM Forms su JEE](/help/forms/using/upgrade-jboss-eap-from-7-4-10-to-7-4-23.md), inclusa la copia dell&#39;URL di connessione, del nome utente e della password dall&#39;installazione esistente nei nuovi file di configurazione.

## Passaggi {#steps}

Eseguire i seguenti passaggi aggiuntivi specifici per il cluster:

### Aggiorna domain.conf.bat {#update-domain-conf-bat}

1. In `domain.conf.bat`, aggiungi le informazioni sui localizzatori della configurazione esistente al nuovo file:

   ```text
   set "JAVA_OPTS=%JAVA_OPTS% -Doak.documentMK.maxServerTimeDiffMillis=-1"
   set "JAVA_OPTS=%JAVA_OPTS% -Dadobe.cache.cluster-locators=<ip-address-master>[22345],<ip-address-slave>[22345]"
   set "JAVA_OPTS=%JAVA_OPTS% -DentityExpansionLimit=10000"
   ```

### Configura autenticazione master-slave {#configure-master-slave-authentication}

1. Crea un nuovo utente per l&#39;autenticazione master-slave nel nodo master.
1. Nei nodi slave, aggiornare la password utente in `host.xml`:

   ```xml
   <server-identities>
       <secret value="Y2hhbmdlaXQ="/>
   </server-identities>
   ```

### Aggiornare gli indirizzi IP in host.xml {#update-ip-addresses-in-host-xml}

1. Aggiornare gli indirizzi IP per i nodi master e slave in `host.xml`:

   ```xml
   <interfaces>
       <interface name="management">
           <inet-address value="${jboss.bind.address.management:<ip-address>}"/>
       </interface>
       <interface name="public">
           <inet-address value="${jboss.bind.address:<ip-address>}"/>
       </interface>
   </interfaces>
   ```

### Rimuovi distribuzioni dalla configurazione del dominio {#remove-deployments-from-domain-configuration}

1. Verificare che nel nuovo file `domain_<db>.xml` non sia presente alcuna sezione `<deployments>`.
1. Non copiare il seguente blocco dalla configurazione esistente:

   ```xml
   <deployments>
       <deployment name="adobe-forms-ivs-jboss.ear" runtime-name="adobe-forms-ivs-jboss.ear"/>
       <deployment name="adobe-livecycle-cq-author.ear" runtime-name="adobe-livecycle-cq-author.ear"/>
       <deployment name="adobe-livecycle-jboss.ear" runtime-name="adobe-livecycle-jboss.ear"/>
       <deployment name="adobe-livecycle-native-jboss-x86_win32.ear" runtime-name="adobe-livecycle-native-jboss-x86_win32.ear"/>
       <deployment name="adobe-livecycle-native-jboss-x86_win64.ear" runtime-name="adobe-livecycle-native-jboss-x86_win64.ear"/>
       <deployment name="adobe-output-ivs-jboss.ear" runtime-name="adobe-output-ivs-jboss.ear"/>
       <deployment name="adobe-workspace-client.ear" runtime-name="adobe-workspace-client.ear"/>
   </deployments>
   ```

### Aggiorna classe driver nella configurazione del dominio {#update-driver-class-in-domain-configuration}

1. Aggiorna la sezione della classe driver in `domain_<db>.xml` in base al motore di database:

   **MSSQL:**

   ```xml
   <xa-datasource-class>com.microsoft.sqlserver.jdbc.SQLServerXADataSource</xa-datasource-class>
   ```

   **Oracle:**

   ```xml
   <xa-datasource-class>oracle.jdbc.xa.client.OracleXADataSource</xa-datasource-class>
   ```

### Aggiorna controller di dominio su nodi slave {#update-domain-controller-on-slave-nodes}

1. Aggiornare il blocco del controller di dominio nel nodo slave in `host.xml` con l&#39;indirizzo IP principale, la porta `9999`, il nome utente `slave1` e l&#39;area di autenticazione `ManagementRealm`:

   ```xml
   <remote host="<ip-address>" port="9999" username="slave1" realm="ManagementRealm"/>
   ```

### Aggiornare jboss-cli.xml {#update-jboss-cli-xml}

1. Aggiorna la voce `<host>` in `jboss-cli.xml` sia sui nodi master che su quelli slave.
