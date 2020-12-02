---
title: Configurare la gestione utente per un server LDAP abilitato per SSL
seo-title: Configurare la gestione utente per un server LDAP abilitato per SSL
description: Scoprite come configurare Gestione utente per un server LDAP abilitato per SSL per consentire il corretto funzionamento della sincronizzazione su LDAPS.
seo-description: Scoprite come configurare Gestione utente per un server LDAP abilitato per SSL per consentire il corretto funzionamento della sincronizzazione su LDAPS.
uuid: 4b3f8ac7-fa38-4adf-a851-82d55fe431fe
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e6e7e2fa-579d-4b36-8598-6ced469a94b1
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 0%

---


# Configurare la gestione utente per un server LDAP abilitato per SSL {#configure-user-management-for-an-ssl-enabled-ldap-server}

Per il corretto funzionamento della sincronizzazione su LDAPS, i certificati LDAP rilasciati dall’autorità di certificazione (CA) devono essere presenti nell’ambiente JRE (Java Runtime Environment) del server dell’applicazione. Importare il certificato nel file dei cacerts del server applicazione, che in genere si trova nella directory *[JAVA_HOME]*/jre/lib/security/cacerts.

1. Abilitare SSL sul server di directory. Per informazioni dettagliate, consultate la documentazione fornita dal fornitore della directory.
1. Esportate un certificato client dal server di directory.
1. Utilizzare il programma keytool per importare il file del certificato client nell&#39;archivio certificati Java Virtual Machine (JVM™) predefinito del server applicazioni AEM moduli. La procedura per questa attività varia a seconda dei percorsi di installazione JVM e client. Ad esempio, se si utilizza BEA WebLogic Server con JDK 1.5, dal prompt dei comandi digitare il testo seguente:

   `keytool -import -alias`*alias* `-file certificatename -keystore C:\bea\jdk15_04\jre\lib\security\cacerts`

1. Quando richiesto, digitate la password. Per Java, la password predefinita è `changeit`. Viene visualizzato un messaggio che indica che il certificato è stato importato correttamente.
1. Quando richiesto, digitare `Yes` per rendere affidabile il certificato.
1. Attivate SSL in Gestione utente e, durante la configurazione delle impostazioni di directory, selezionate Sì per l’opzione SSL e modificate di conseguenza l’impostazione della porta. Il numero di porta predefinito è 636.

>[!NOTE]
>
>In caso di problemi durante l’utilizzo di SSL, usate un browser LDAP per verificare se può accedere al sistema LDAP quando usate SSL. Se il browser LDAP non riesce a ottenere l’accesso, il certificato o il server dell’applicazione non è configurato correttamente. Se il browser LDAP funziona correttamente e si verificano comunque dei problemi, Gestione utente non è configurata correttamente.

