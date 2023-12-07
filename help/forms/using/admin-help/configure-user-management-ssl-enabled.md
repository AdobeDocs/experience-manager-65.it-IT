---
title: Configurare la gestione degli utenti per un server LDAP abilitato per SSL
description: Scopri come configurare User Management per un server LDAP abilitato per SSL in modo che la sincronizzazione funzioni correttamente su LDAPS.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 606e84f2-6728-47a9-a439-dbe2e55100ad
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 0%

---

# Configurare la gestione degli utenti per un server LDAP abilitato per SSL {#configure-user-management-for-an-ssl-enabled-ldap-server}

Affinché la sincronizzazione funzioni correttamente su LDAPS, i certificati LDAP emessi dall&#39;autorità di certificazione (CA) devono essere presenti nell&#39;ambiente di runtime Java (JRE) del server applicazioni. Importa il certificato nel file caert JRE del server applicazioni, in genere nel file *[JAVA_HOME]* directory /jre/lib/security/cacerts.

1. Abilitare SSL sul server delle directory. Per ulteriori informazioni, consultare la documentazione fornita dal fornitore dell&#39;elenco in linea.
1. Esporta un certificato client dal server delle directory.
1. Utilizza il programma keytool per importare il file di certificato client nell’archivio certificati predefinito della Java Virtual Machine (JVM™) del server applicazioni AEM Forms. La procedura per questa attività varia, a seconda della JVM e dei percorsi di installazione del client. Ad esempio, se si utilizza il server BEA WebLogic con JDK 1.5, dal prompt dei comandi digitare il testo seguente:

   `keytool -import -alias`*alias* `-file certificatename -keystore C:\bea\jdk15_04\jre\lib\security\cacerts`

1. Quando richiesto, digitare la password. Per Java, la password predefinita è `changeit`.) Viene visualizzato un messaggio che informa che il certificato è stato importato correttamente.
1. Quando richiesto, digita `Yes` per considerare attendibile il certificato.
1. Abilitare SSL in Gestione utente e, durante la configurazione delle impostazioni della directory, selezionare Sì per l&#39;opzione SSL e modificare di conseguenza l&#39;impostazione della porta. Il numero di porta predefinito è 636.

>[!NOTE]
>
>Se riscontri problemi durante l’utilizzo di SSL, utilizza un browser LDAP per verificare se è possibile accedere al sistema LDAP quando utilizzi SSL. Se il browser LDAP non è in grado di accedere, il certificato o il server applicazioni non è configurato correttamente. Se il browser LDAP funziona correttamente e si verificano ancora problemi, la gestione utente non viene configurata correttamente.
