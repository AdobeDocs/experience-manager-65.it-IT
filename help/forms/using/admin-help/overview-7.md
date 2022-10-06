---
title: Nozioni di base sulla configurazione dei moduli
seo-title: Basics of configuring forms
description: Scopri i vari servizi forms che consentono di creare applicazioni interattive per l’acquisizione di dati.
seo-description: Learn about the various forms services that help you create interactive data capture applications.
uuid: f495c170-2d17-45b0-b09d-22cce101131e
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e87c7379-28ed-4fda-aef1-970d2b54f30d
exl-id: 169f3d94-ac00-41c7-853e-ecf0dbee559f
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---

# Nozioni di base sulla configurazione dei moduli {#basics-of-configuring-forms}

Il servizio Forms consente di creare applicazioni client di acquisizione dati interattive per la convalida, l’elaborazione, la trasformazione e la distribuzione dei moduli generalmente creati in Designer. Gli autori dei moduli sviluppano una singola struttura del modulo che il servizio Forms esegue in diversi formati:

* come PDF in Adobe Reader o in un browser
* come HTML in vari ambienti browser, incluso il rendering XHTML 1.0 conforme
* come guide dei moduli in vari ambienti del browser che supportano Adobe Flash Player.

Per ulteriori informazioni sul servizio Forms, consulta [Riferimento servizi](https://www.adobe.com/go/learn_aemforms_services_63).

Utilizzando la pagina Forms nella console di amministrazione, puoi configurare il comportamento del servizio Forms. Queste impostazioni si applicano a tutte le chiamate del servizio. Eventuali parametri inviati tramite l’SDK di moduli AEM sostituiscono le impostazioni impostate nella console di amministrazione; tuttavia, influenzano solo quella particolare invocazione.

Dopo aver modificato le impostazioni Forms nella console di amministrazione, fai clic su Salva. Non è necessario riavviare il server per rendere effettive le modifiche. Tuttavia, potrebbe essere necessario arrestare e riavviare il servizio Forms durante la configurazione delle impostazioni della modalità cache. (Vedi [Avvio e arresto dei servizi](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services).)
