---
title: Configurazione di SSL in Windows Vista
description: Scopri come configurare SSL in Windows Vista. Utilizza ed esegui Java Keytool per generare il certificato SSL con le chiavi RSA per l’autenticazione.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_ssl
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 36c4300d-7a44-41f4-b294-06f32bb01686
solution: Experience Manager, Experience Manager Forms
feature: Document Security
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 0%

---

# Configurazione di SSL in Windows Vista {#configuring-ssl-on-windows-vista}

Per configurare SSL in Windows Vista™, è necessario un certificato SSL con chiavi RSA per l&#39;autenticazione. Puoi utilizzare lo strumento chiave Java per creare il certificato.

>[!NOTE]
>
>Windows Vista non funzionerà con le chiavi DSA.

È possibile eseguire keytool utilizzando un singolo comando che include tutte le informazioni necessarie per creare il certificato e il keystore.

**Crea un certificato SSL**

1. Al prompt dei comandi passare a *`[JAVA HOME]`*/bin e digitare il comando seguente per creare il certificato e il keystore:

   `keytool -genkey -keyalg RSA -dname "CN=`*Nome host* `, OU=`*Nome gruppo* `, O=`*Nome società* `,L=`*Nome città* `, S=`*Stato* `, C=`*Codice paese* `" -alias`*&quot;Certificato LC&quot;* `-keypass` `key`*_* *password* `-keystore`*nomechiave* `.keystore`

   >[!NOTE]
   >
   >Sostituisci *`[JAVA_HOME]`con la directory in cui è installato JDK e sostituisci il testo in corsivo con i valori corrispondenti all&#39;ambiente.*

1. Digitare `changeit` come password. Questa password è l&#39;impostazione predefinita per un&#39;installazione Java e l&#39;amministratore di sistema potrebbe averla modificata.
