---
title: Nozioni di base sulla configurazione dei moduli
description: Scopri i vari servizi di moduli che ti consentono di creare applicazioni di acquisizione dati interattive.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 169f3d94-ac00-41c7-853e-ecf0dbee559f
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
source-wordcount: '200'
ht-degree: 100%
---
# Nozioni di base sulla configurazione dei moduli {#basics-of-configuring-forms}

Il servizio Forms consente di creare applicazioni client di acquisizione dati interattive per la convalida, il processo, la trasformazione e la distribuzione di moduli generalmente creati in Designer. Gli autori dei moduli sviluppano una singola progettazione di moduli che il servizio Forms esegue in vari formati:

* come PDF in Adobe Reader o in un browser
* come HTML in vari ambienti di browser, tra cui un rendering XHTML 1.0 conforme
* come guide per moduli in vari ambienti del browser che supportano Adobe Flash Player.

Per ulteriori informazioni sul servizio Forms, consulta [Riferimento ai servizi](https://www.adobe.com/go/learn_aemforms_services_63).

Utilizzando la pagina Forms nella console di amministrazione, puoi configurare il comportamento del servizio Forms. Queste impostazioni si applicano a tutte le chiamate del servizio. Tutti i parametri inviati tramite l’SDK di AEM Forms sostituiscono le impostazioni configurate nella console di amministrazione; tuttavia, influiscono solo su tale chiamata particolare.

Dopo aver modificato le impostazioni di Forms nella console di amministrazione, fai clic su Salva. Non è necessario riavviare il server per rendere effettive le modifiche. Tuttavia, potrebbe essere necessario interrompere e riavviare il servizio Forms durante la configurazione delle impostazioni della modalità cache (consulta [Avvio e interruzione dei servizi](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services)).
