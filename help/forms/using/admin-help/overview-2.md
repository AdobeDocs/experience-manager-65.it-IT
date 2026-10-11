---
title: Informazioni di base sulla gestione di certificati e credenziali
description: Scopri le nozioni di base sulla gestione di certificati e credenziali.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_certificates_and_credentials
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 74bf0e77-f47b-475a-b2a7-52cfb3baaa22
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '372'
ht-degree: 95%
---
# Informazioni di base sulla gestione di certificati e credenziali {#basics-of-managing-certificates-and-credentials}

Una *credenziale* contiene le informazioni sulla chiave privata che sono necessarie per firmare o identificare i documenti. Un *certificato* è un’informazione di chiave pubblica configurata per l’attendibilità. AEM Forms utilizza certificati e credenziali per diversi scopi:

* Le estensioni Acrobat Reader DC utilizzano una credenziale per abilitare i diritti di utilizzo di Adobe Reader nei documenti PDF. Vedere [Configurazione delle credenziali per l’utilizzo con le estensioni di Acrobat Reader DC](/help/forms/using/admin-help/configuring-credentials-acrobat-reader-dc.md#configuring-credentials-for-use-with-acrobat-reader-dc-extensions).
* È possibile configurare Rights Management in modo che visualizzi le credenziali da utilizzare in Acrobat solo da emittenti attendibili. (Vedi [Configurare le impostazioni di visualizzazione di Rights Management](/help/forms/using/admin-help/configuring-client-server-options.md#configure-document-security-display-settings).) Il certificato deve contenere il nome comune (CN).
* Il servizio di firma accede a certificati e credenziali. Per informazioni dettagliate sul servizio di firma, vedere [Riferimento ai servizi](https://www.adobe.com/go/learn_aemforms_services_65).

**Generazione di una coppia di chiavi**

AEM Forms utilizza il proprio archivio fonti attendibili per archiviare e gestire certificati, credenziali ed elenchi di revoche di certificati (CRL, Certificate Revocation List). È inoltre possibile utilizzare un dispositivo HSM (Hardware Security Module) indipendente per memorizzare le chiavi private.

AEM Forms non fornisce alcuna opzione per generare una coppia di chiavi. Tuttavia, è possibile generarlo utilizzando strumenti quali Java Keytool e importarlo nell’archivio fonti attendibili di AEM Forms. Per ulteriori informazioni su Java Keytool, vedere:

[https://docs.oracle.com/javase/tutorial/security/toolsign/step3.html](https://docs.oracle.com/javase/tutorial/security/toolsign/step3.html)

[https://docs.oracle.com/cd/E19798-01/821-1841/gjrgy/index.html](https://docs.oracle.com/cd/E19798-01/821-1841/gjrgy/index.html)

[https://helpcenter.gsx.com/hc/en-us/articles/115015960428-How-to-Generate-a-Self-Signed-Certificate-and-Private-Key-using-OpenSSL](https://helpcenter.gsx.com/hc/en-us/articles/115015960428-How-to-Generate-a-Self-Signed-Certificate-and-Private-Key-using-OpenSSL)

I seguenti tipi di firma sono supportati e possono essere importati in AEM Forms:

* Firma XML
* XMLTimeStampToken
* RFC 3161 TimeStampToken
* PKCS#7
* PKCS#1
* Firme DSA

**Gestione della chiave persa o compromessa**

Se si sopetta che la chiave sia stata persa o compromessa, effettuare le seguenti operazioni:

1. Informare l’autorità di certificazione, in modo che aggiunga la chiave compromessa nell’elenco di revoche di certificati per revocare la chiave.
1. Ottenere una nuova chiave e i relativi certificati dall’autorità di certificazione.
1. Utilizzare la nuova chiave per firmare di nuovo i documenti che erano stati già firmati tramite chiave compromessa.
