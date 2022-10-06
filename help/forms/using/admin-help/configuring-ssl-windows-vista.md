---
title: Configurazione di SSL su Windows Vista
seo-title: Configuring SSL on Windows Vista
description: Scopri come configurare SSL in Windows Vista.
seo-description: Learn how to configure SSL on Windows Vista.
uuid: 20bfcefb-ec84-4c55-bceb-6af106d883d7
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_ssl
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 667645a0-53d0-4f9b-a0ba-cc7e366a23a1
exl-id: 36c4300d-7a44-41f4-b294-06f32bb01686
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 0%

---

# Configurazione di SSL su Windows Vista {#configuring-ssl-on-windows-vista}

Per configurare SSL su Windows Vista™, è necessario un certificato SSL con chiavi RSA per l&#39;autenticazione. Puoi usare il keytool Java per creare il certificato.

>[!NOTE]
>
>Windows Vista non funziona con le chiavi DSA.

È possibile eseguire keytool utilizzando un singolo comando che include tutte le informazioni necessarie per creare il certificato e il keystore.

**Creare un certificato SSL**

1. Al prompt dei comandi, passa a *`[JAVA HOME]`*/bin e digita il seguente comando per creare il certificato e il keystore:

   `keytool -genkey -keyalg RSA -dname "CN=`*Nome host* `, OU=`*Nome gruppo* `, O=`*Nome dell&#39;azienda* `,L=`*Nome della città* `, S=`*Stato* `, C=`*Codice paese* `" -alias`*&quot;LC Cert&quot;* `-keypass` `key`*_* *password* `-keystore`*nome chiave* `.keystore`

   >[!NOTE]
   >
   >Sostituisci *`[JAVA_HOME]`con la directory in cui è installato JDK e sostituisci il testo in corsivo con i valori corrispondenti al tuo ambiente.*

1. Tipo `changeit` come password. Questa password è l&#39;impostazione predefinita per un&#39;installazione Java e l&#39;amministratore di sistema potrebbe averla modificata.
