---
title: Progettazione di modelli per moduli per moduli HTML5
description: AEM Forms può eseguire il rendering del modello di modulo XFA nel formato HTML5. I progettisti di moduli possono progettare modelli di modulo utilizzando Designer e utilizzare la funzionalità di rendering di HTML5.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
docset: aem65
feature: HTML5 Forms,Mobile Forms
exl-id: 7c8d501f-c953-495e-8bac-1f66fd99c783
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 97aafc4b-2598-52d6-9012-295a95969e38
    internal-label: HTML5 Forms
  - id: 59f95943-e802-56ac-990d-21ab923984c1
    internal-label: Mobile Forms
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '487'
ht-degree: 3%
---
# Progettazione di modelli per moduli per moduli HTML5{#designing-form-templates-for-html-forms}

Il componente HTML5 Forms in AEM può eseguire il rendering del modello di modulo XFA in formato HTML5. I progettisti di moduli possono progettare modelli di modulo utilizzando [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63) e utilizzare la funzionalità di rendering di HTML5. Questi modelli di modulo, insieme alle relative risorse, possono trovarsi nell’archivio di AEM, nel file system o essere esposti tramite http. Tuttavia, se prevedi di gestire i moduli con Forms Manager, i modelli e le risorse devono trovarsi nell’archivio di AEM.

Anche se i moduli HTML5 corrispondono in larga misura al comportamento di PDF forms, esistono alcune funzioni in entrambi i formati che non sono applicabili all’altro formato. Ad esempio, il modo in cui i codici a barre vengono applicati a un modulo PDF in Adobe Reader varia da un modulo Mobile, oppure il modo in cui un modulo è firmato digitalmente varia anche tra i formati. Per ulteriori informazioni su tali varianti, vedere [Differenziazione delle funzionalità tra HTML5 Forms e PDF forms](../../forms/using/feature-differentiation-html5-forms-pdf-forms.md).

Per le funzioni XFA più comuni, consulta le best practice e le linee guida seguenti per progettare un modulo che funzioni in entrambi i formati.

## Best practice {#best-practices}

La maggior parte dei passaggi per la progettazione di un modello di modulo, ad esempio le associazioni di schema o la scrittura della logica del modulo, sono gli stessi. Tuttavia, a causa delle differenze intrinseche tra il motore di rendering e di script di un client spesso come Adobe Reader e i moduli basati su browser, nell&#39;articolo [best practice](/help/forms/using/design-accessible-html5-forms.md) sono descritti alcuni consigli. Queste best practice consentono di progettare modelli di modulo in modo che funzionino come previsto in entrambi i formati.

### Funzionalità in AEM Forms Designer per HTML5 Forms {#capabilities-in-aem-forms-designer-for-html-forms}

#### Anteprima HTML {#preview-html}

La scheda Anteprima HTML viene aggiunta in modalità Progettazione per consentire ai progettisti di moduli di visualizzare in anteprima i moduli in formato HTML5 durante il processo di progettazione. Per ulteriori informazioni su come abilitare e configurare questa funzionalità in AEM Forms Designer, vedere [Anteprima HTML](../../forms/using/preview-xdp-forms-html.md).

#### Firma scarabocchio {#scribble-signature}

Il target principale per i moduli HTML5 sono i dispositivi touch. Pertanto, in AEM Forms Designer viene aggiunto un nuovo controllo della firma scarabocchio. È possibile fare clic o trascinare e rilasciare il controllo della firma scarabocchio sul modello di modulo e configurarlo. Viene visualizzato come campo scarabocchio nel rendering di HTML5 e può essere utilizzato per scrivere la firma sui dispositivi touch. Sui computer desktop, può essere utilizzato come campo scarabocchio utilizzando il controllo del mouse. Per ulteriori informazioni sull&#39;utilizzo di questa funzionalità, vedere [Campo a mano libera XFA](../../forms/using/scribble-signature.md).

![4](assets/4.png)

#### Formato RTF {#rich-text-format}

È possibile convertire un campo di testo in un campo RTF. Aggiunge un elenco di opzioni di formattazione al campo di testo. Per convertire, aprire Forms Designer, selezionare il campo di testo in **[!UICONTROL Visualizzazione Struttura]**. Nella scheda **[!UICONTROL Campo]**, seleziona **[!UICONTROL Testo formattato]** dall&#39;elenco a discesa **[!UICONTROL Formato campo]**. Ora, quando il modulo XFA viene renderizzato come modulo HTML5, il campo viene renderizzato come campo in formato Rich Text. Seleziona ![Ingrandisci](assets/maximize_icon.svg) per visualizzare altre opzioni di formattazione.
