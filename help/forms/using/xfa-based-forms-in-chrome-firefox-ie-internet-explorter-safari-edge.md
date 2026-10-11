---
title: Impossibile aprire PDF forms basato su XFA in Google Chrome, Firefox, Microsoft&reg; Edge, Microsoft&reg; Internet Explorer o Apple Safari
description: Impossibile aprire PDF forms basato su XFA in Google Chrome, Firefox, Microsoft&reg; Edge, Microsoft&reg; Internet Explorer o Apple Safari
feature: Adaptive Forms,Document Services
exl-id: fdd15315-e0d6-4d80-acb4-2e0ecec716c4
solution: Experience Manager, Experience Manager Forms
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
  - id: f19cff18-c8cc-4a4b-adad-85dd2fa3dbe2
    internal-label: Document Services
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 751e1826ed53df7522418e50a206f0fe622256a4
workflow-type: tm+mt
source-wordcount: '424'
ht-degree: 0%
---
# Impossibile aprire PDF forms basato su XFA in Google Chrome, Firefox, Microsoft® Edge, Microsoft® Internet Explorer o Apple Safari{#unable-to-open-XFA-based-PDF-forms-in-Google-Chrome-Firefox-Microsoft-Edge-Microsoft-Internet-Explorer-or-Apple-Safari}

Molte versioni recenti del browser hanno incluso il proprio supporto limitato per PDF forms basato su XFA. Anche se questi browser possono aprire PDF forms basato su XFA, le funzionalità fornite sono limitate. Se non riesci ad aprire o inviare un modulo PDF basato su XFA in un browser moderno, utilizza uno dei seguenti metodi:

* Utilizza [Adobe® Acrobat®](https://www.adobe.com/acrobat.html) o [Adobe® Adobe® Reader®](https://get.adobe.com/it/reader/), versione 8 o successiva per aprire e inviare PDF forms basato su XFA.
* Acrobat e Reader, su Microsoft® Windows®, consentono di configurare per aprire i PDF in modalità Visualizzazione protetta, che impedisce l’apertura di PDF forms basato su XFA. Assicurati che la modalità Visualizzazione protetta nell’Acrobat o nel Reader sia disabilitata. Per ulteriori informazioni, vedere [Visualizzazione protetta (solo Windows)](https://helpx.adobe.com/in/reader/using/protected-mode-windows.html).
* (Per sviluppatori Forms) Adobe Experience Manager Forms fornisce anche supporto per:

  * [esegui il rendering di moduli basati su XFA in HTML5 Forms](https://experienceleague.adobe.com/docs/experience-manager-65/forms/html5-forms/introduction.html?#key-capabilities-of-html-forms-br) in modo che i moduli possano essere aperti in browser con supporto HTML5, inclusi i browser in esecuzione su dispositivi mobili come iPad. La rappresentazione HTML5 dei moduli mantiene il layout della struttura del modulo e supporta la maggior parte delle logiche del modulo (come JavaScript, calcolo dei moduli e convalide dei moduli) incorporate nel modello di modulo XFA.
  * [convertire i moduli basati su XFA in Forms adattivo reattivo per dispositivi mobili](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/creating-adaptive-form.html?#create-an-adaptive-form-based-on-an-xfa-form-template). Questi moduli forniscono un layout dinamico, funzionalità di personalizzazione e si adattano dinamicamente alle risposte degli utenti aggiungendo o rimuovendo campi o sezioni secondo necessità. Forniscono inoltre connettori predefiniti per varie origini dati, funzionalità per documenti di record e una facile connessione ad Adobe Analytics per la valutazione delle prestazioni. Per ulteriori informazioni, vedere [Funzionalità e funzionalità principali](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/forms-overview/home.html?lang=en)
    In questo modo, gli investimenti tecnologici nei moduli XFA sono protetti e continuano a fornire un’esperienza ottimale agli utenti finali. Per ulteriori informazioni, consulta [Documentazione del prodotto Adobe Experience Manager Forms](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/forms-overview/home.html).
