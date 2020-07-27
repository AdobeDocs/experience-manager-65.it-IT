---
title: Avvio e arresto dei servizi
seo-title: Avvio e arresto dei servizi
description: Scoprite come avviare e arrestare i servizi associati ai moduli AEM Forms e al server applicazione e al database.
seo-description: Scoprite come avviare e arrestare i servizi associati ai moduli AEM Forms e al server applicazione e al database.
uuid: 8c831cb2-4165-4118-8a09-764cec4e5e05
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_services
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: b93060bd-c6e1-40d2-8acd-ccafb8ed56da
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 0%

---


# Avvio e arresto dei servizi {#starting-and-stopping-services}

Esistono due tipi di servizi che fanno parte dei moduli AEM:

* Servizi che controllano il server applicazioni e il database AEM Forms.
* Servizi che controllano i moduli AEM

## Avviare o arrestare i servizi associati ai moduli AEM {#start-or-stop-the-services-associated-with-aem-forms-modules}

I moduli AEM (ad esempio, Forms, Rights Management, Output) funzionano come servizi. A volte può essere necessario arrestare o avviare i servizi per questi moduli AEM. Ad esempio, dopo aver modificato un&#39;impostazione per il servizio è necessario arrestare e riavviare un servizio moduli AEM.

1. Nella console di amministrazione, fai clic su **Servizi** > **Applicazioni e servizi** > Gestione **dei** servizi.
1. Nella pagina Gestione dei servizi, selezionate la casella di controllo accanto al servizio da arrestare o avviare e fate clic su Interrompi o Avvia.

## Avviare o arrestare i servizi per il server applicazioni e il database {#start-or-stop-services-for-the-application-server-and-database}

Un’implementazione completa dei moduli AEM include un server applicazioni e servizi di database:

* *`[application server]`* per i moduli AEM
* *`[database]`* per i moduli AEM

In Windows, questi servizi sono accessibili tramite il pannello **Strumenti** di amministrazione > **Servizi**. Ad esempio, se hai installato moduli AEM su JBoss utilizzando il metodo chiavi in mano, nel sistema sono disponibili i seguenti servizi:

* JBoss per  moduli di Adobe Experience Manager
* MySQL per  moduli di Adobe Experience Manager

Per avviare o arrestare questi servizi, selezionateli dall’elenco nel pannello Servizi e fate clic sul pulsante di azione appropriato nel pannello.

In UNIX® o Linux, immettete il testo seguente da una riga di comando, dove *`[service name]`* corrisponde al nome del servizio che state verificando:

```java
     ps -A | grep [service name]
```

