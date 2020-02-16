---
title: Nozioni di base sulla gestione di certificati e credenziali
seo-title: Nozioni di base sulla gestione di certificati e credenziali
description: Informazioni sulle nozioni di base per la gestione di certificati e credenziali.
seo-description: Informazioni sulle nozioni di base per la gestione di certificati e credenziali.
uuid: f421e206-e7b5-416c-b9fb-974094f10a66
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_certificates_and_credentials
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 986d16fc-4c81-4785-b1f3-fe8bd7ff669e
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Nozioni di base sulla gestione di certificati e credenziali {#basics-of-managing-certificates-and-credentials}

Una *credenziale* contiene le informazioni di chiave privata necessarie per firmare o identificare i documenti. Un *certificato* è un&#39;informazione di chiave pubblica configurata per l&#39;attendibilità. I moduli AEM utilizzano certificati e credenziali per diversi scopi:

* Le estensioni Acrobat Reader DC utilizzano una credenziale per abilitare i diritti di utilizzo di Adobe Reader nei documenti PDF. (vedere [Configurazione delle credenziali per l’uso con le estensioni](/help/forms/using/admin-help/configuring-credentials-acrobat-reader-dc.md#configuring-credentials-for-use-with-acrobat-reader-dc-extensions)Acrobat Reader DC.)
* Potete configurare Rights Management per visualizzare le credenziali da utilizzare in Acrobat solo da emittenti attendibili. Consultate [Configurare le impostazioni](/help/forms/using/admin-help/configuring-client-server-options.md#configure-document-security-display-settings)di visualizzazione di Rights Management. Il nome comune (NC) deve essere presente nel certificato.
* Il servizio Signature accede a certificati e credenziali. Per informazioni dettagliate sul servizio Firma, vedere Riferimento [](https://www.adobe.com/go/learn_aemforms_services_63)servizi.

**Generazione di un tasto coppia**

I moduli AEM utilizzano il proprio archivio certificati per memorizzare e gestire certificati, credenziali ed elenchi di revoche di certificati (CRL). È inoltre possibile utilizzare un dispositivo HSM (Hardware Security Module) indipendente per memorizzare chiavi private.

I moduli AEM non forniscono alcuna opzione per generare una coppia di chiavi. Tuttavia, è possibile generarlo utilizzando strumenti quali Java keytool e importarlo nell&#39;archivio certificati moduli AEM. Per ulteriori informazioni su Java keytool, vedi:

[https://docs.oracle.com/javase/tutorial/security/toolsign/step3.html](https://docs.oracle.com/javase/tutorial/security/toolsign/step3.html)

[https://docs.oracle.com/cd/E19798-01/821-1841/gjrgy/index.html](https://docs.oracle.com/cd/E19798-01/821-1841/gjrgy/index.html)

[https://blogs.adobe.com/livecycle/2010/01/creating_ssl_keys_and_certific.html](https://blogs.adobe.com/livecycle/2010/01/creating_ssl_keys_and_certific.html)

I seguenti tipi di firma sono supportati e possono essere importati nei moduli AEM:

* Firma XML
* XMLTimeStampToken
* RFC 3161 TimeStampToken
* PKCS#7
* PKCS#1
* Firme DSA

**Gestione della chiave persa o compromessa**

Se sospetti che la tua chiave sia stata persa o compromessa, effettua le seguenti operazioni:

1. Informare l&#39;autorità di certificazione, in modo che aggiungano la chiave compromessa nell&#39;elenco di revoca del certificato per revocare la chiave.
1. Ottenere una nuova chiave e i relativi certificati dall&#39;autorità di certificazione.
1. Firmare nuovamente i documenti firmati utilizzando la chiave compromessa utilizzando la nuova chiave.

