---
title: Configurare la password di binding LDAP
seo-title: Configure the LDAP bind password
description: Scopri come configurare il campo bind password (password di associazione) prima di importare il file di configurazione in un altro sistema.
seo-description: Learn how to configure the bind password field before you import the configuration file into another system.
uuid: 1ab1907c-8b55-4b6f-bd5b-49f22d78b8a8
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 165b3950-b03f-4848-8361-ffb0a26d2658
exl-id: c72794f5-8767-409e-a1df-91a8fdc54d18
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '183'
ht-degree: 0%

---

# Configurare la password di binding LDAP{#configure-the-ldap-bind-password}

Per evitare rischi di sicurezza, il campo bind password (password di associazione) nel file di configurazione esportato (config.xml) non è configurato. Prima di importare il file di configurazione in un altro sistema, verificare di aver configurato la password. Questa password sostituisce una password esistente memorizzata nel database. Una password Null non sostituisce un valore esistente per una password non Null.

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utente > Configurazione > Importa ed esporta file di configurazione.
1. Per esportare l&#39;impostazione di configurazione corrente in un file, fare clic su Esporta e salvare il file di configurazione in un&#39;altra posizione.
1. Nel file, individua `Domains` > *[Nome dominio]* > `DirectoryConfigs` > `LDAPGroupConfig` nodo. Ecco un esempio:

   ```xml
    <node name="LDAPGroupConfig">
        <map>
            <entry key="bindanonymously" value="false" />
            <entry key="basedn" value="dc=corp,dc=adobe,dc=com" />
            <entry key="batchSize" value="200" />
            <entry key="binduser" value="cn=Directory Manager" />
            <entry key="bindpassword" value="" />
        </map>
   ```

   Digita un valore per `bindpassword` e salvare le modifiche.

1. Nel file, individua `Domains` > *[Nome dominio]* > `DirectoryConfigs` > `LDAPGroupConfig` > `LDAPUserConfig` nodo. Ecco un esempio:

   ```xml
    <node name="LDAPUserConfig">
        <map>
            <entry key="bindanonymously" value="false" />
            <entry key="batchSize" value="200" />
            <entry key="basedn" value="dc=corp,dc=adobe,dc=com" />
            <entry key="bindpassword" value="" />
            <entry key="binduser" value="cn=Directory Manager" />
        </map>
   ```

   Digita un valore per `bindpassword` e salvare le modifiche.

1. Per importare il file aggiornato, in Gestione utenti, fare clic su Configurazione > Importa ed esporta file di configurazione.
1. Fare clic su Sfoglia per trovare il file, su Importa e quindi su OK.
