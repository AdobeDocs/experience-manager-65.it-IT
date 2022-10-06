---
title: Avvio e arresto dei servizi
seo-title: Starting and stopping services
description: Scopri come avviare e interrompere i servizi associati ai moduli AEM Forms e al server applicazioni e al database.
seo-description: Learn how to start and stop services associated with AEM Forms modules and the application server and database.
uuid: 8c831cb2-4165-4118-8a09-764cec4e5e05
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_services
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: b93060bd-c6e1-40d2-8acd-ccafb8ed56da
exl-id: 55bf5196-22c6-4286-8c92-ff44d81dde49
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 0%

---

# Avvio e arresto dei servizi {#starting-and-stopping-services}

Esistono due tipi di servizi che fanno parte dei moduli AEM:

* Servizi che controllano l’application server e il database di AEM forms.
* Servizi che controllano i moduli AEM

## Avviare o arrestare i servizi associati ai moduli AEM {#start-or-stop-the-services-associated-with-aem-forms-modules}

I moduli AEM (ad esempio, Forms, Rights Management, Output) funzionano come servizi. A volte, potrebbe essere necessario interrompere o avviare i servizi per questi moduli AEM. Ad esempio, è necessario arrestare e quindi riavviare un servizio AEM forms dopo aver modificato un&#39;impostazione per il servizio.

1. Nella console di amministrazione fai clic su **Servizi** > **Applicazioni e servizi** > **Gestione dei servizi**.
1. Nella pagina Gestione servizi selezionare la casella di controllo accanto al servizio da arrestare o avviare e fare clic su Interrompi o Avvia.

## Avvia o arresta i servizi per l&#39;application server e il database {#start-or-stop-services-for-the-application-server-and-database}

Un’implementazione completa di AEM moduli include un application server e servizi di database:

* *`[application server]`* per i moduli AEM
* *`[database]`* per i moduli AEM

In Windows, questi servizi sono accessibili tramite **Strumenti di amministrazione** > **Pannello Servizi**. Ad esempio, se hai installato AEM moduli su JBoss utilizzando il metodo chiavi in mano, nel sistema sono disponibili i seguenti servizi:

* JBoss per Adobe Experience Manager forms
* MySQL per i moduli Adobe Experience Manager

Avvia o interrompi questi servizi selezionandoli dall&#39;elenco nel pannello Servizi e facendo clic sul pulsante di azione appropriato nel pannello.

In UNIX® o Linux, immettere il seguente testo da una riga di comando, dove *`[service name]`* è il nome del servizio che stai verificando:

```java
     ps -A | grep [service name]
```
