---
title: Panoramica sulla configurazione di SSL
seo-title: Panoramica sulla configurazione di SSL
description: Scopri come migliorare la sicurezza delle comunicazioni configurando SSL.
seo-description: Scopri come migliorare la sicurezza delle comunicazioni configurando SSL.
uuid: 3e99d2bf-137b-45ba-8384-309624094623
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_ssl
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 8e107abb-861f-4063-b600-c87e34639019
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 0%

---


# Panoramica sulla configurazione di SSL {#overview-of-configuring-ssl}

Potete creare le credenziali SSL (Secure Sockets Layer) e configurare SSL sul server dell’applicazione per migliorare la sicurezza della comunicazione con il server dell’applicazione.

Come prodotto di sicurezza, il Rights Management richiede la configurazione di SSL. Quando configurate i certificati SSL, accertatevi di utilizzare solo le chiavi RSA. I certificati SSL con chiavi DSA non sono supportati.

Le informazioni fornite si applicano alle installazioni chiavi in mano, automatiche e manuali. Offre un esempio di metodo per la configurazione di SSL. È inoltre possibile utilizzare altri metodi più adatti alla rete o all&#39;organizzazione.

>[!NOTE]
>
>È consigliabile completare l&#39;installazione, la configurazione e la distribuzione dei moduli AEM e assicurarsi che i prodotti vengano eseguiti correttamente prima di configurare SSL sul server dell&#39;applicazione.

>[!NOTE]
>
>Quando create certificati di sicurezza SSL e le credenziali, utilizzate gli stessi privilegi dell&#39;account utente che avete usato per eseguire il server dell&#39;applicazione. Se il server applicazione viene eseguito utilizzando altri privilegi utente, il modulo potrebbe non essere visualizzato correttamente per le rappresentazioni PDFForm quando ContentRootURI punta a https.

Se disponete di un server LDAP abilitato per SSL, configurate Gestione utente per utilizzarlo. Consultate [Configurare la gestione utente per un server LDAP abilitato per SSL](/help/forms/using/admin-help/configure-user-management-ssl-enabled.md#configure-user-management-for-an-ssl-enabled-ldap-server).
