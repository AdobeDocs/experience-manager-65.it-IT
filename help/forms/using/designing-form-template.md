---
title: Progettazione di modelli di modulo per moduli HTML5
seo-title: Designing form templates for HTML5 forms
description: AEM Forms offre il rendering del modello di modulo XFA in formato HTML5. I progettisti di moduli possono progettare modelli di moduli utilizzando Designer e utilizzare la funzionalità di rendering di HTML 5.
seo-description: AEM Forms offers rendering XFA form template to HTML5 format. Form designers can design form templates using Designer and use the HTML5 rendition capability.
uuid: 4f6b7231-4479-400a-adcd-c68064f06b4e
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: f2e9dbe4-e210-41f3-8878-2fc4d166e63c
docset: aem65
feature: Mobile Forms
exl-id: 7c8d501f-c953-495e-8bac-1f66fd99c783
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 1%

---

# Progettazione di modelli di modulo per moduli HTML5{#designing-form-templates-for-html-forms}

Il componente HTML5 Forms nell’AEM offre il rendering del modello di modulo XFA in formato HTML5. I progettisti di moduli possono progettare modelli di modulo utilizzando [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63_it) e utilizza la funzionalità di rendering di HTML5. Questi modelli di modulo, insieme alle relative risorse, possono risiedere nell’archivio AEM, nel file system o essere esposti tramite http. Tuttavia, se prevedi di gestire i moduli con Forms Manager, i modelli e le risorse devono trovarsi nell’archivio AEM.

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

È possibile convertire un campo di testo in un campo RTF. Aggiunge un elenco di opzioni di formattazione al campo di testo. Per convertire, apri Forms Designer, tocca il campo di testo in **[!UICONTROL Visualizzazione Progettazione]**. In **[!UICONTROL Campo]** , seleziona **[!UICONTROL Rich Text]** dal **[!UICONTROL Formato campo]** elenco a discesa. Ora, quando il modulo XFA viene renderizzato come modulo HTML5, il campo viene renderizzato come campo in formato Rich Text. Tocca ![Ingrandisci](assets/maximize_icon.svg) per visualizzare ulteriori opzioni di formattazione.
