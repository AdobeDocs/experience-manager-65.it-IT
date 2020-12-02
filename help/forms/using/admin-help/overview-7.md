---
title: Nozioni di base sulla configurazione dei moduli
seo-title: Nozioni di base sulla configurazione dei moduli
description: Scopri i diversi servizi dei moduli che consentono di creare applicazioni interattive per l'acquisizione dei dati.
seo-description: Scopri i diversi servizi dei moduli che consentono di creare applicazioni interattive per l'acquisizione dei dati.
uuid: f495c170-2d17-45b0-b09d-22cce101131e
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e87c7379-28ed-4fda-aef1-970d2b54f30d
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 0%

---


# Nozioni di base sulla configurazione dei moduli {#basics-of-configuring-forms}

Il servizio Forms consente di creare applicazioni client interattive per l&#39;acquisizione dei dati che convalidano, elaborano, trasformano e distribuiscono i moduli generalmente creati in Designer. Gli autori dei moduli sviluppano una singola struttura del modulo rappresentata dal servizio Forms in vari formati:

* come PDF in  Adobe Reader o in un browser
* come HTML in vari ambienti del browser, incluso il rendering XHTML 1.0 conforme
* come guide dei moduli in vari ambienti browser che supportano  Flash Player Adobe.

Per ulteriori informazioni sul servizio Forms, vedere [Guida di riferimento dei servizi](https://www.adobe.com/go/learn_aemforms_services_63).

Utilizzando la pagina Forms nella console di amministrazione, potete configurare il comportamento del servizio Forms. Queste impostazioni si applicano a tutte le chiamate del servizio. Eventuali parametri inviati tramite l’SDK AEM moduli sovrascrivono le impostazioni impostate nella console di amministrazione; tuttavia, influiscono solo su tale particolare chiamata.

Dopo aver modificato le impostazioni Forms nella console di amministrazione, fate clic su Salva. Non è necessario riavviare il server per rendere effettive le modifiche. Tuttavia, potrebbe essere necessario arrestare e riavviare il servizio Forms durante la configurazione delle impostazioni della modalità cache. (Vedere [Avvio e arresto dei servizi](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services).)
