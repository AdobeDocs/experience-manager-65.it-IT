---
title: Configurare la password di binding LDAP
description: Scopri come configurare il campo password di binding prima di importare il file di configurazione in un altro sistema.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: c72794f5-8767-409e-a1df-91a8fdc54d18
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: ht
source-wordcount: '195'
ht-degree: 100%

---

# Configurare la password di binding LDAP{#configure-the-ldap-bind-password}

>[!NOTE]
> 
> Assicurati che l’utente disponga dei privilegi di amministratore per accedere alla console dell’amministratore.

Per evitare rischi di sicurezza, il campo password di binding nel file di configurazione esportato (config.xml) non è configurato. Prima di importare il file di configurazione in un altro sistema, verifica di aver configurato la password. Questa password sostituisce una password esistente memorizzata nel database. Una password nulla non sostituisce un valore esistente per una password non nulla.

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utenti > Configurazione > Importa ed esporta file di configurazione.
1. Per esportare l’impostazione di configurazione corrente in un file, fai clic su Esporta e salva il file di configurazione in un’altra posizione.
1. Nel file, individua il nodo `Domains` > *[Nome dominio]* > `DirectoryConfigs` > `LDAPGroupConfig`. Ecco un esempio:

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

1. Nel file, individua il nodo `Domains` > *[Nome dominio]* > `DirectoryConfigs` > `LDAPGroupConfig` > `LDAPUserConfig`. Ecco un esempio:

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

1. Per importare il file aggiornato, in Gestione utenti fai clic su Configurazione > Importa ed esporta file di configurazione.
1. Fai clic su Sfoglia per trovare il file, fai clic su Importa e quindi su OK.
