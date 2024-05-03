---
title: Progettazione di modelli di modulo per moduli HTML5
description: AEM Forms può eseguire il rendering del modello di modulo XFA nel formato HTML5. I progettisti di moduli possono progettare modelli di moduli utilizzando Designer e utilizzare la funzionalità di rendering di HTML 5.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
docset: aem65
feature: HTML5 Forms
exl-id: 7c8d501f-c953-495e-8bac-1f66fd99c783
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '480'
ht-degree: 0%

---

# Progettazione di modelli di modulo per moduli HTML5{#designing-form-templates-for-html-forms}

Il componente HTML5 Forms nell’AEM può eseguire il rendering del modello di modulo XFA nel formato HTML5. I progettisti di moduli possono progettare modelli di modulo utilizzando [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63) e utilizza la funzionalità di rendering di HTML5. Questi modelli di modulo, insieme alle relative risorse, possono risiedere nell’archivio AEM, nel file system o essere esposti tramite http. Tuttavia, se prevedi di gestire i moduli con Forms Manager, i modelli e le risorse devono trovarsi nell’archivio AEM.

Anche se i moduli HTML5 corrispondono in larga misura al comportamento dei PDF forms, esistono alcune funzioni in entrambi i formati che non sono applicabili all’altro formato. Ad esempio, il modo in cui i codici a barre vengono applicati a un modulo PDF in Adobe Reader varia da un modulo Mobile, oppure il modo in cui un modulo è firmato digitalmente varia anche tra i formati. Per ulteriori informazioni su tali varianti, consulta [Differenziazione delle funzioni tra moduli di HTML5 e PDF forms](../../forms/using/feature-differentiation-html5-forms-pdf-forms.md).

Per le funzioni XFA più comuni, consulta le best practice e le linee guida seguenti per progettare un modulo che funzioni in entrambi i formati.

## Best practice {#best-practices}

La maggior parte dei passaggi per la progettazione di un modello di modulo, ad esempio le associazioni di schema o la scrittura della logica del modulo, sono gli stessi. Tuttavia, a causa delle differenze intrinseche tra il motore di rendering e di script di un client spesso come Adobe Reader e i moduli basati su browser, vi sono alcuni consigli descritti in [best practice](/help/forms/using/design-accessible-html5-forms.md) articolo. Queste best practice consentono di progettare modelli di modulo in modo che funzionino come previsto in entrambi i formati.

### Funzionalità di AEM Forms Designer per HTML5 Forms {#capabilities-in-aem-forms-designer-for-html-forms}

#### Anteprima HTML {#preview-html}

La scheda Anteprima HTML viene aggiunta in modalità Progettazione per consentire ai progettisti di moduli di visualizzare in anteprima i moduli in formato HTML5 durante il processo di progettazione. Per ulteriori informazioni su come abilitare e configurare questa funzionalità in AEM Forms Designer, consulta [Anteprima HTML](../../forms/using/preview-xdp-forms-html.md).

#### Firma scarabocchio {#scribble-signature}

Il target principale per i moduli HTML5 sono i dispositivi touch. Pertanto, in AEM Forms Designer viene aggiunto un nuovo controllo della firma scarabocchio. È possibile fare clic o trascinare e rilasciare il controllo della firma scarabocchio sul modello di modulo e configurarlo. Viene rappresentato come campo scarabocchio nella rappresentazione di HTML5 e può essere utilizzato per scrivere la firma sui dispositivi touch. Sui computer desktop, può essere utilizzato come campo scarabocchio utilizzando il controllo del mouse. Per ulteriori informazioni su come utilizzare questa funzione, consulta [Campo a mano libera XFA](../../forms/using/scribble-signature.md).

![4](assets/4.png)

#### Formato RTF {#rich-text-format}

È possibile convertire un campo di testo in un campo RTF. Aggiunge un elenco di opzioni di formattazione al campo di testo. Per convertire, apri Forms Designer, seleziona il campo di testo in **[!UICONTROL Visualizzazione Progettazione]**. In **[!UICONTROL Campo]** , seleziona **[!UICONTROL Rich Text]** dal **[!UICONTROL Formato campo]** elenco a discesa. Ora, quando il modulo XFA viene renderizzato come modulo HTML5, il campo viene renderizzato come campo in formato Rich Text. Seleziona ![Ingrandisci](assets/maximize_icon.svg) per visualizzare ulteriori opzioni di formattazione.
