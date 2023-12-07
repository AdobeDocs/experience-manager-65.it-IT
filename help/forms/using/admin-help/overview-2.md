---
title: Nozioni di base sulla gestione di certificati e credenziali
description: Scopri le nozioni di base sulla gestione di certificati e credenziali.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_certificates_and_credentials
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 74bf0e77-f47b-475a-b2a7-52cfb3baaa22
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 0%

---

# Nozioni di base sulla gestione di certificati e credenziali {#basics-of-managing-certificates-and-credentials}

A *credenziali* contiene le informazioni sulla chiave privata necessarie per la firma o l&#39;identificazione dei documenti. A *certificato* sono informazioni sulla chiave pubblica configurate per l&#39;attendibilità. I moduli AEM utilizzano certificati e credenziali per diversi scopi:

* Le estensioni Acrobat Reader DC utilizzano una credenziale per abilitare i diritti di utilizzo di Adobe Reader nei documenti PDF. (vedere [Configurazione delle credenziali per l’utilizzo con le estensioni Acrobat Reader DC](/help/forms/using/admin-help/configuring-credentials-acrobat-reader-dc.md#configuring-credentials-for-use-with-acrobat-reader-dc-extensions).)
* Puoi configurare il Rights Management in modo che visualizzi le credenziali da utilizzare in Acrobat solo da emittenti attendibili. (vedere [Configura impostazioni di visualizzazione Rights Management](/help/forms/using/admin-help/configuring-client-server-options.md#configure-document-security-display-settings).) Il certificato deve contenere il nome comune (CN).
* Il servizio di firma accede a certificati e credenziali. Per maggiori informazioni sul servizio di firma, vedere [Riferimento servizi](https://www.adobe.com/go/learn_aemforms_services_65).

**Generazione di una chiave di coppia**

I moduli AEM utilizzano il relativo archivio fonti attendibili per archiviare e gestire certificati, credenziali ed elenchi di revoche di certificati (CRL). È inoltre possibile utilizzare un dispositivo HSM (Hardware Security Module) indipendente per memorizzare le chiavi private.

I moduli AEM non forniscono alcuna opzione per generare una coppia di chiavi. Tuttavia, puoi generarlo utilizzando strumenti come Java Keytool e importarlo nell’archivio fonti attendibili dei moduli AEM. Per ulteriori informazioni su Java keytool, vedi:

[https://docs.oracle.com/javase/tutorial/security/toolsign/step3.html](https://docs.oracle.com/javase/tutorial/security/toolsign/step3.html)

[https://docs.oracle.com/cd/E19798-01/821-1841/gjrgy/index.html](https://docs.oracle.com/cd/E19798-01/821-1841/gjrgy/index.html)

[https://helpcenter.gsx.com/hc/en-us/articles/115015960428-How-to-Generate-a-Self-Signed-Certificate-and-Private-Key-using-OpenSSL](https://helpcenter.gsx.com/hc/en-us/articles/115015960428-How-to-Generate-a-Self-Signed-Certificate-and-Private-Key-using-OpenSSL)

I seguenti tipi di firma sono supportati e possono essere importati nei moduli AEM:

* Firma XML
* XMLTimeStampToken
* TimeStampToken RFC 3161
* PKCS#7
* PKCS#1
* Firme DSA

**Gestione della chiave persa o compromessa**

Se sospetti che la chiave sia stata persa o compromessa, effettua le seguenti operazioni:

1. Informare l&#39;autorità di certificazione, in modo che aggiunga la chiave compromessa nell&#39;elenco di revoche di certificati per revocare la chiave.
1. Ottieni una nuova chiave e i relativi certificati dall’autorità di certificazione.
1. Firma di nuovo i documenti firmati utilizzando la chiave compromessa utilizzando la nuova chiave.
