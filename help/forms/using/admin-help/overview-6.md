---
title: Panoramica sulla configurazione di SSL
description: Scopri come migliorare la sicurezza delle comunicazioni configurando SSL.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_ssl
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: fbe1487e-c830-4be8-9841-6022e6a98ae7
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 0%

---

# Panoramica sulla configurazione di SSL {#overview-of-configuring-ssl}

È possibile creare credenziali SSL (Secure Sockets Layer) e configurare SSL sul server applicazioni per migliorare la sicurezza delle comunicazioni con il server applicazioni.

Come prodotto per la sicurezza, il Rights Management richiede la configurazione di SSL. Durante la configurazione dei certificati SSL, accertati di utilizzare solo le chiavi RSA. I certificati SSL con chiavi DSA non sono supportati.

Le informazioni fornite si applicano alle installazioni chiavi in mano, automatiche e manuali. Offre un esempio di metodo per configurare SSL. È inoltre possibile utilizzare altri metodi più appropriati per la rete o l&#39;organizzazione.

>[!NOTE]
>
>Prima di configurare SSL sul server applicazioni, è consigliabile completare l&#39;installazione, la configurazione e la distribuzione dei moduli AEM e verificare che i prodotti funzionino correttamente.

>[!NOTE]
>
>Quando si creano certificati e credenziali di protezione SSL, utilizzare gli stessi privilegi dell&#39;account utente utilizzati per eseguire il server applicazioni. Se il server applicazioni viene eseguito utilizzando altri privilegi utente, è possibile che il modulo non venga eseguito correttamente per le rappresentazioni di PDForm quando ContentRootURI punta a https.

Se si dispone di un server LDAP abilitato per SSL, configurare User Management per utilizzarlo. (vedere [Configurare la gestione degli utenti per un server LDAP abilitato per SSL](/help/forms/using/admin-help/configure-user-management-ssl-enabled.md#configure-user-management-for-an-ssl-enabled-ldap-server).)
