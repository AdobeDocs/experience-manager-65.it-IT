---
title: Modifica dell’ordine di valutazione per l’autenticazione
description: È possibile modificare l'ordine in cui i moduli AEM valutano più provider di autenticazione.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 7e29c9d4-fb82-4308-aac7-0f5cb1f4aef2
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 0%

---

# Modifica dell’ordine di valutazione per l’autenticazione {#change-the-order-of-evaluation-for-authentication}

>[!NOTE]
> 
> Assicurati che l’utente disponga dei privilegi di amministratore per accedere alla console dell’amministratore.

Se sono stati configurati più provider di autenticazione, è possibile modificare l&#39;ordine di valutazione dei moduli AEM per l&#39;autenticazione. L&#39;ordine dei provider di autenticazione elencati nel file config.xml determina l&#39;ordine di valutazione per l&#39;autenticazione.

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utente > Configurazione > Importa ed esporta file di configurazione.
1. Per esportare l&#39;impostazione di configurazione corrente in un file, fare clic su Esporta e salvare il file di configurazione in un&#39;altra posizione.
1. Trova il seguente nodo nel file:

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

   In `<entry key="order" value="3" />`, modificare il valore di ogni nodo per impostare l&#39;ordine della valutazione dell&#39;autenticazione.

1. Per importare il file aggiornato, in Gestione utenti, fare clic su Configurazione > Importa ed esporta file di configurazione.
1. Fare clic su Sfoglia per trovare il file, su Importa e quindi su OK.
