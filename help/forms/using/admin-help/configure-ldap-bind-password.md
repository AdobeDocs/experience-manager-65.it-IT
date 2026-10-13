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
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '196'
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
