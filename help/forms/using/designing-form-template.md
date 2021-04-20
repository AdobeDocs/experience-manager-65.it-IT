---
title: Progettazione di modelli di modulo per i moduli HTML5
seo-title: Progettazione di modelli di modulo per i moduli HTML5
description: AEM Forms offre il rendering del modello di modulo XFA in formato HTML5. I progettisti di moduli possono progettare modelli di modulo utilizzando Designer e utilizzare la funzionalità di rendering HTML5.
seo-description: AEM Forms offre il rendering del modello di modulo XFA in formato HTML5. I progettisti di moduli possono progettare modelli di modulo utilizzando Designer e utilizzare la funzionalità di rendering HTML5.
uuid: 4f6b7231-4479-400a-adcd-c68064f06b4e
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: f2e9dbe4-e210-41f3-8878-2fc4d166e63c
docset: aem65
feature: Mobile Forms
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '517'
ht-degree: 0%

---


# Progettazione di modelli di modulo per i moduli HTML5{#designing-form-templates-for-html-forms}

Il componente Moduli HTML5 in AEM offre il rendering del modello di modulo XFA in formato HTML5. I progettisti di moduli possono progettare modelli di modulo utilizzando [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63) e utilizzare la funzionalità di rendering HTML5. Questi modelli di modulo, insieme alle relative risorse, possono risiedere AEM archivio, nel file system o essere esposti tramite http. Tuttavia, se si intende gestire i moduli utilizzando Forms Manager, i modelli e le risorse devono trovarsi nell’archivio AEM.

Sebbene i moduli HTML5 corrispondano in larga misura al comportamento dei PDF forms, vi sono alcune funzioni in entrambi i formati che non sono applicabili all’altro formato. Ad esempio, il modo in cui i codici a barre vengono applicati a un modulo PDF in Adobe Reader varia a seconda del modulo mobile o del modo in cui un modulo viene firmato digitalmente. Per ulteriori informazioni su tali varianti, vedere [Differenziazione delle funzioni tra i moduli HTML5 e i PDF forms](../../forms/using/feature-differentiation-html5-forms-pdf-forms.md).

Per informazioni sulle funzioni XFA comuni, vedere le best practice e le linee guida seguenti per progettare un modulo che funzioni in entrambi i formati.

## Best practice {#best-practices}

La maggior parte dei passaggi necessari per progettare un modello di modulo, ad esempio binding di schema o scrittura di logica del modulo, sono gli stessi. Tuttavia, a causa delle differenze intrinseche tra il rendering e il motore di script di un client spesso come Adobe Reader e i moduli basati su browser, esistono alcuni consigli descritti nell&#39;articolo [best practice](/help/forms/using/design-accessible-html5-forms.md) . Queste best practice consentono di progettare modelli di modulo che funzionino come previsto in entrambi i formati.

### Funzionalità di AEM Forms Designer per Forms HTML5 {#capabilities-in-aem-forms-designer-for-html-forms}

#### Anteprima HTML {#preview-html}

La scheda Anteprima HTML viene aggiunta in modalità Progettazione per consentire ai progettisti di visualizzare in anteprima i moduli in formato HTML5 durante il processo di progettazione. Per ulteriori informazioni su come abilitare e configurare questa funzionalità in AEM Forms Designer, consulta [Anteprima HTML](../../forms/using/preview-xdp-forms-html.md).

#### Firma scarabocchio {#scribble-signature}

Il target chiave dei moduli HTML5 è rappresentato dai dispositivi touch. Pertanto, in AEM Forms Designer viene aggiunto un nuovo controllo firma scarabocchio. È possibile fare clic o trascinare e rilasciare il controllo firma a mano libera sul modello di modulo e configurarlo. Viene rappresentato come un campo scarabocchio nel rendering HTML5 e può essere utilizzato per scarabocchiare la firma sui dispositivi touch. Sui computer desktop, può essere utilizzato come campo scarabocchio utilizzando il controllo del mouse. Per ulteriori informazioni su come utilizzare questa funzione, consulta [Campo di distribuzione XFA](../../forms/using/scribble-signature.md).

![4](assets/4.png)

#### Formato RTF {#rich-text-format}

È possibile convertire un campo di testo in un campo di testo RTF. Aggiunge un elenco di opzioni di formattazione al campo di testo. Per convertire, aprire Forms Designer, toccare il campo di testo in **[!UICONTROL Visualizzazione struttura]**. Nella scheda **[!UICONTROL Campo]** , seleziona **[!UICONTROL Rich Text]** dall’elenco a discesa **[!UICONTROL Formato campo]** . Ora, quando si esegue il rendering del modulo XFA come modulo HTML5, il campo viene rappresentato come un campo di testo RTF. Tocca ![Ingrandisci](assets/maximize_icon.svg) per visualizzare altre opzioni di formattazione.
