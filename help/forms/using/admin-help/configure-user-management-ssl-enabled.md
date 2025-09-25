---
title: Configurare la gestione degli utenti per un server LDAP abilitato per SSL
description: Scopri come configurare la gestione degli utenti per un server LDAP abilitato per SSL per garantire il corretto funzionamento della sincronizzazione su LDAPS.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 606e84f2-6728-47a9-a439-dbe2e55100ad
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: ht
source-wordcount: '279'
ht-degree: 100%

---

# Configurare la gestione degli utenti per un server LDAP abilitato per SSL {#configure-user-management-for-an-ssl-enabled-ldap-server}

Affinché la sincronizzazione funzioni correttamente su LDAPS, i certificati LDAP emessi dall’autorità di certificazione (CA) devono essere presenti nell’ambiente di runtime Java (JRE) del server applicazioni. Importa il certificato nel file JRE cacerts del server applicazioni, che si trova in genere nella directory *[JAVA_HOME]*/jre/lib/security/cacerts.

1. Abilita SSL sul server delle directory. Per ulteriori informazioni, consulta la documentazione del fornitore della directory.
1. Esporta un certificato client dal server delle directory.
1. Utilizza il programma keytool per importare il file di certificato client nell’archivio certificati predefinito di Java Virtual Machine (JVM™) del server applicazioni AEM Forms. La procedura per questa attività varia a seconda della JVM e dei percorsi di installazione del client. Ad esempio, se utilizzi il server BEA WebLogic con JDK 1.5, digita il testo seguente nel prompt dei comandi:

   `keytool -import -alias`*alias* `-file certificatename -keystore C:\bea\jdk15_04\jre\lib\security\cacerts`

1. Quando viene richiesto, digita la password. Per Java, la password predefinita è `changeit`. Viene visualizzato un messaggio che informa che il certificato è stato importato correttamente.
1. Quando richiesto, digitare `Yes` per considerare affidabile il certificato.
1. Abilita SSL in Gestione degli utenti, quindi durante la configurazione delle impostazioni della directory, seleziona Sì per l’opzione SSL e modifica di conseguenza l’impostazione della porta. Il numero di porta predefinito è 636.

>[!NOTE]
>
>Se riscontri problemi durante l’utilizzo di SSL, utilizza un browser LDAP per verificare se è in grado di accedere al sistema LDAP quando utilizzi SSL. Se il browser LDAP non è in grado di accedere, il certificato o il server applicazioni non è configurato correttamente. Se il browser LDAP funziona correttamente e si verificano ancora problemi, la gestione degli utenti non è configurata correttamente.
