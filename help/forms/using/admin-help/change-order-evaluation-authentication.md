---
title: Modificare l'ordine di valutazione per l'autenticazione
seo-title: Change the order of evaluation for authentication
description: È possibile modificare l’ordine in cui AEM moduli valuta più provider di autenticazione.
seo-description: You can change the order in which AEM forms evaluates multiple authentication providers.
uuid: c2693e5b-cf09-4bb8-815a-2b20ebf6eea0
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 5434df9c-ecf6-450a-aa7e-d9ab69b66fe6
exl-id: 7e29c9d4-fb82-4308-aac7-0f5cb1f4aef2
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 0%

---

# Modificare l&#39;ordine di valutazione per l&#39;autenticazione {#change-the-order-of-evaluation-for-authentication}

Se hai configurato più provider di autenticazione, puoi modificare l’ordine in cui AEM moduli li valuta per l’autenticazione. L&#39;ordine dei provider di autenticazione elencati nel file config.xml determina l&#39;ordine di valutazione per l&#39;autenticazione.

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utente > Configurazione > Importa ed esporta file di configurazione.
1. Per esportare l&#39;impostazione di configurazione corrente in un file, fare clic su Esporta e salvare il file di configurazione in un&#39;altra posizione.
1. Trova il seguente nodo nel file :

   ```xml
    <node name="AuthSchemes">
        <map />
            <node name="CertificateAuth">
                <map>
                    <entry key="order" value="3" />
                    <entry key="name" value="edc.server.auth.scheme.certificate" />
                </map>
        </node>
        <node name="Kerberos">
            <map>
                <entry key="kerberosSPN" value="defaultSPN" />
                <entry key="order" value="1" />
                <entry key="name" value="edc.server.auth.scheme.kerberos" />
            </map>
    </node>
   ```

   In `<entry key="order" value="3" />`, modifica il valore di ogni nodo per impostare l’ordine della valutazione dell’autenticazione.

1. Per importare il file aggiornato, in Gestione utente fare clic su Configurazione > Importa ed esporta file di configurazione.
1. Fare clic su Sfoglia per trovare il file, fare clic su Importa e quindi su OK.
