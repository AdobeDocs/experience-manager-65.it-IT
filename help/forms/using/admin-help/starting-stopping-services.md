---
title: Avvio e arresto dei servizi
description: Scopri come avviare e arrestare i servizi associati ai moduli AEM Forms, al server applicazioni e al database.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_services
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 55bf5196-22c6-4286-8c92-ff44d81dde49
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
source-wordcount: '311'
ht-degree: 17%
---
# Avvio e arresto dei servizi {#starting-and-stopping-services}

>[!NOTE]
> 
> Assicurati che l’utente disponga dei privilegi di amministratore per accedere alla console dell’amministratore.

Esistono due tipi di servizi che fanno parte di AEM Forms:

* Servizi che controllano il server applicazioni e il database di AEM Form.
* Servizi che controllano i moduli di AEM Forms

## Avviare o arrestare i servizi associati ai moduli di AEM Forms {#start-or-stop-the-services-associated-with-aem-forms-modules}

I moduli di AEM Forms (ad esempio, Forms, Rights Management, Output) funzionano come servizi. A volte può essere necessario arrestare o avviare i servizi per questi moduli di AEM Forms. È ad esempio necessario arrestare e riavviare un servizio AEM Forms dopo aver modificato un&#39;impostazione per il servizio.

>[!NOTE]
>
> Si consiglia di utilizzare il comando “Ctrl + C” per riavviare SDK. Il riavvio di AEM SDK utilizzando metodi alternativi, ad esempio l’arresto dei processi Java, può causare incoerenze nell’ambiente di sviluppo AEM.

1. Nella console di amministrazione, fare clic su **Servizi** > **Applicazioni e servizi** > **Gestione servizi**.
1. Nella pagina Gestione servizio selezionare la casella di controllo accanto al servizio da arrestare o avviare e fare clic su Arresta o Avvia.

## Avviare o arrestare i servizi per il server applicazioni e il database {#start-or-stop-services-for-the-application-server-and-database}

Un&#39;implementazione completa di AEM Forms include un server applicazioni e servizi di database:

* *`[application server]`* per AEM Forms
* *`[database]`* per AEM Forms

In Windows, questi servizi sono accessibili tramite **Strumenti di amministrazione** > **Pannello servizi**. Ad esempio, se AEM Forms è stato installato su JBoss utilizzando il metodo chiavi in mano, nel sistema sono disponibili i seguenti servizi:

* JBoss per Adobe Experience Manager forms
* MySQL per Adobe Experience Manager forms

Avviare o arrestare questi servizi selezionandoli dall&#39;elenco nel pannello Servizi e quindi facendo clic sul pulsante di azione appropriato nel pannello.

In UNIX® o Linux, immettere il testo seguente da una riga di comando, dove *`[service name]`* è il nome del servizio che si sta verificando:

```java
     ps -A | grep [service name]
```
