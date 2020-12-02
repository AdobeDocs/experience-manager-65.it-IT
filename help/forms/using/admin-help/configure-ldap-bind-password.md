---
title: Configurare la password per il binding LDAP
seo-title: Configurare la password per il binding LDAP
description: Come configurare il campo password di binding prima di importare il file di configurazione in un altro sistema.
seo-description: Come configurare il campo password di binding prima di importare il file di configurazione in un altro sistema.
uuid: 1ab1907c-8b55-4b6f-bd5b-49f22d78b8a8
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 165b3950-b03f-4848-8361-ffb0a26d2658
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '205'
ht-degree: 3%

---


# Configurare la password per il binding LDAP{#configure-the-ldap-bind-password}

Per evitare rischi di protezione, il campo password di binding nel file di configurazione esportato (config.xml) non è configurato. Prima di importare il file di configurazione in un altro sistema, accertatevi di configurare questa password. Questa password sostituisce una password esistente memorizzata nel database. Una password null non sostituisce un valore di password esistente non nullo.

1. Nella console di amministrazione, fate clic su Impostazioni > Gestione utente > Configurazione > Importa ed esporta file di configurazione.
1. Per esportare l’impostazione di configurazione corrente in un file, fate clic su Esporta e salvate il file di configurazione in un’altra posizione.
1. Nel file, individuare il nodo `Domains` > *[Nome del dominio]* > `DirectoryConfigs` > `LDAPGroupConfig`. Di seguito è riportato un esempio:

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

   Digitare un valore per `bindpassword` e salvare le modifiche.

1. Nel file, individuare il nodo `Domains` > *[Nome del dominio]* > `DirectoryConfigs` > `LDAPGroupConfig` > `LDAPUserConfig`. Di seguito è riportato un esempio:

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

   Digitare un valore per `bindpassword` e salvare le modifiche.

1. Per importare il file aggiornato, in Gestione utente fate clic su Configurazione > Importa ed esporta file di configurazione.
1. Fate clic su Sfoglia per trovare il file, fate clic su Importa, quindi fate clic su OK.

