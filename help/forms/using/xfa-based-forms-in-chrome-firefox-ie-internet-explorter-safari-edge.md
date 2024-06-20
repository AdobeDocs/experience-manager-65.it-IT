---
title: Impossibile aprire PDF forms basati su XFA in Google Chrome, Firefox, Microsoft&reg; Edge, Microsoft&reg; Internet Explorer o Apple Safari
description: Impossibile aprire PDF forms basati su XFA in Google Chrome, Firefox, Microsoft&reg; Edge, Microsoft&reg; Internet Explorer o Apple Safari
feature: Adaptive Forms, Troubleshooting
exl-id: fdd15315-e0d6-4d80-acb4-2e0ecec716c4
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '341'
ht-degree: 0%

---

# Impossibile aprire PDF forms basati su XFA in Google Chrome, Firefox, Microsoft® Edge, Microsoft® Internet Explorer o Apple Safari{#unable-to-open-XFA-based-PDF-forms-in-Google-Chrome-Firefox-Microsoft-Edge-Microsoft-Internet-Explorer-or-Apple-Safari}

Molte versioni recenti del browser hanno incluso il proprio supporto limitato per i PDF forms basati su XFA. Anche se questi browser possono aprire PDF forms basati su XFA, le funzionalità fornite sono limitate. Se non riesci ad aprire o inviare un modulo PDF basato su XFA in un browser moderno, utilizza uno dei seguenti metodi:

* Utilizzare [Adobe ® Acrobat®](https://www.adobe.com/acrobat.html) o [Adobe ® Adobe ® Reader ®](https://get.adobe.com/reader/), versione 8 o successiva per aprire e inviare PDF forms basati su XFA.
* Acrobat e Reader, in Microsoft® Windows®, consentono di configurare per l&#39;apertura dei PDF in modalità Visualizzazione protetta, che impedisce l&#39;apertura dei PDF forms basati su XFA. Assicurati che la modalità Visualizzazione protetta nell’Acrobat o nel Reader sia disabilitata. Per ulteriori informazioni, consulta [Visualizzazione protetta (solo Windows)](https://helpx.adobe.com/in/reader/using/protected-mode-windows.html).
* (Per sviluppatori Forms) Adobe Experience Manager Forms fornisce anche supporto per:

   * [eseguire il rendering di moduli basati su XFA in HTML5 Forms](https://experienceleague.adobe.com/docs/experience-manager-65/forms/html5-forms/introduction.html?#key-capabilities-of-html-forms-br) in modo che i moduli possano essere aperti in browser che supportano HTML5, inclusi i browser in esecuzione su dispositivi mobili come iPad. La rappresentazione HTML5 dei moduli mantiene il layout della struttura del modulo e supporta la maggior parte delle logiche del modulo (ad esempio JavaScript, calcolo del modulo e convalide del modulo) incorporate nel modello di modulo XFA.
   * [convertire i moduli basati su XFA in Forms adattivo reattivo per dispositivi mobili](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/creating-adaptive-form.html?#create-an-adaptive-form-based-on-an-xfa-form-template). Questi moduli forniscono un layout dinamico, funzionalità di personalizzazione e si adattano dinamicamente alle risposte degli utenti aggiungendo o rimuovendo campi o sezioni secondo necessità. Forniscono inoltre connettori predefiniti per varie origini dati, funzionalità per documenti di record e una facile connessione ad Adobe Analytics per la valutazione delle prestazioni. Per ulteriori informazioni, consulta [Funzionalità e caratteristiche principali](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/forms-overview/home.html?lang=en)
In questo modo, gli investimenti tecnologici nei moduli XFA sono protetti e continuano a fornire un’esperienza ottimale agli utenti finali. Per ulteriori informazioni, consulta [Documentazione del prodotto Adobe Experience Manager Forms](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/forms-overview/home.html).
