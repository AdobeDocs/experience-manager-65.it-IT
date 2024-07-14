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
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 0%

---

# Avvio e arresto dei servizi {#starting-and-stopping-services}

Esistono due tipi di servizi che fanno parte delle forme AEM:

* Servizi che controllano il server applicazioni e il database AEM forms.
* Servizi che controllano i moduli per moduli AEM

## Avviare o arrestare i servizi associati ai moduli AEM Forms {#start-or-stop-the-services-associated-with-aem-forms-modules}

I moduli di moduli AEM (ad esempio, Forms, Rights Management, Output) funzionano come servizi. A volte, potrebbe essere necessario interrompere o avviare i servizi per questi moduli AEM Forms. Ad esempio, è necessario arrestare e quindi riavviare un servizio AEM forms dopo aver modificato un&#39;impostazione per il servizio.

>[!NOTE]
>
> Per riavviare l&#39;SDK, si consiglia di utilizzare il comando &#39;Ctrl + C&#39;. Il riavvio dell’SDK dell’AEM con metodi alternativi, ad esempio l’arresto dei processi Java, può causare incongruenze nell’ambiente di sviluppo dell’AEM.

1. Nella console di amministrazione, fare clic su **Servizi** > **Applicazioni e servizi** > **Gestione servizi**.
1. Nella pagina Gestione servizio selezionare la casella di controllo accanto al servizio da arrestare o avviare e fare clic su Arresta o Avvia.

## Avviare o arrestare i servizi per il server applicazioni e il database {#start-or-stop-services-for-the-application-server-and-database}

Un&#39;implementazione completa dei moduli AEM include un server applicazioni e servizi di database:

* *`[application server]`* per i moduli AEM
* *`[database]`* per i moduli AEM

In Windows, questi servizi sono accessibili tramite **Strumenti di amministrazione** > **Pannello servizi**. Ad esempio, se hai installato i moduli AEM su JBoss utilizzando il metodo chiavi in mano, sul sistema sono disponibili i seguenti servizi:

* JBoss per Adobe Experience Manager forms
* MySQL per Adobe Experience Manager forms

Avviare o arrestare questi servizi selezionandoli dall&#39;elenco nel pannello Servizi e quindi facendo clic sul pulsante di azione appropriato nel pannello.

In UNIX® o Linux, immettere il testo seguente da una riga di comando, dove *`[service name]`* è il nome del servizio che si sta verificando:

```java
     ps -A | grep [service name]
```
