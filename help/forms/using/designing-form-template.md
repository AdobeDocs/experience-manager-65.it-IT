---
title: Progettazione di modelli di modulo per moduli HTML5
seo-title: Progettazione di modelli di modulo per moduli HTML5
description: AEM Forms offre il rendering del modello di modulo XFA in formato HTML5. I progettisti di moduli possono progettare i modelli di modulo utilizzando Designer e utilizzare la funzionalità di rappresentazione HTML5.
seo-description: AEM Forms offre il rendering del modello di modulo XFA in formato HTML5. I progettisti di moduli possono progettare i modelli di modulo utilizzando Designer e utilizzare la funzionalità di rappresentazione HTML5.
uuid: 4f6b7231-4479-400a-adcd-c68064f06b4e
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: f2e9dbe4-e210-41f3-8878-2fc4d166e63c
docset: aem65
translation-type: tm+mt
source-git-commit: f763359fb333ef6cc8a6748ccfa39ba9aee9ca48

---


# Progettazione di modelli di modulo per moduli HTML5{#designing-form-templates-for-html-forms}

Il componente Moduli HTML5 in AEM offre il rendering del modello di modulo XFA in formato HTML5. I progettisti di moduli possono progettare modelli di modulo utilizzando [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63) e utilizzare la funzionalità di rappresentazione HTML5. Questi modelli di modulo, insieme alle relative risorse, possono risiedere nell’archivio AEM, nel file system o essere esposti tramite http. Tuttavia, se si intende gestire i moduli utilizzando Forms Manager, i modelli e le risorse devono risiedere nell&#39;archivio di AEM.

Sebbene i moduli HTML5 corrispondano in larga misura al funzionamento dei moduli PDF, alcune funzioni di entrambi i formati non sono applicabili all&#39;altro formato. Ad esempio, il modo in cui i codici a barre vengono applicati a un modulo PDF in Adobe Reader varia a seconda del modulo Mobile o il modo in cui il modulo viene firmato digitalmente varia a seconda dei formati. Per ulteriori informazioni su tali variazioni, vedere Differenza tra le [funzioni dei moduli HTML5 e dei moduli](../../forms/using/feature-differentiation-html5-forms-pdf-forms.md)PDF.

Per le funzioni XFA comuni, vedere le procedure ottimali e le linee guida riportate di seguito per progettare un modulo che funzioni in entrambi i formati.

## Best practices {#best-practices}

La maggior parte dei passaggi necessari per progettare un modello di modulo, ad esempio i binding degli schemi o per scrivere la logica del modulo, sono gli stessi. Tuttavia, a causa delle differenze intrinseche tra il rendering e il motore di script di un client spesso come Adobe Reader e i moduli basati su browser, sono disponibili alcune raccomandazioni descritte nell&#39;articolo relativo alle [best practice](/help/forms/using/design-accessible-html5-forms.md) . Queste best practice consentono di progettare i modelli di modulo in modo che funzionino come previsto in entrambi i formati.

### Funzionalità di AEM Forms Designer per moduli HTML5 {#capabilities-in-aem-forms-designer-for-html-forms}

#### Anteprima HTML {#preview-html}

La scheda Anteprima HTML viene aggiunta nella modalità Progettazione per i progettisti di moduli per visualizzare in anteprima i moduli in formato HTML5 durante il processo di progettazione. Per ulteriori informazioni su come abilitare e configurare questa funzionalità in AEM Forms Designer, consultate [Anteprima HTML](../../forms/using/preview-xdp-forms-html.md).

#### Firma scarabocchio {#scribble-signature}

La destinazione chiave per i moduli HTML5 sono i dispositivi touch. In AEM Forms Designer, quindi, è stato aggiunto un nuovo controllo di firma con script. È possibile fare clic o trascinare e rilasciare il controllo firma script sul modello di modulo e configurarlo. Viene rappresentato come campo di script nella rappresentazione HTML5 e può essere utilizzato per creare script di firma sui dispositivi touch. Sui computer desktop, può essere utilizzato come campo di scripting utilizzando il controllo del mouse. Per ulteriori informazioni sull&#39;utilizzo di questa funzione, vedere Campo [di](../../forms/using/scribble-signature.md)scorrimento XFA.

![4](assets/4.png)

#### Rich text format {#rich-text-format}

È possibile convertire un campo di testo in un campo RTF. Aggiunge un elenco di opzioni di formattazione al campo di testo. Per convertire, aprire Forms Designer, toccare il campo di testo in visualizzazione **** Struttura. Nella scheda **[!UICONTROL Campo]** , selezionare **[!UICONTROL RTF]** dall&#39;elenco a discesa Formato **** campo. Ora, quando viene eseguito il rendering del modulo XFA come modulo HTML5, il campo viene rappresentato come un campo di testo RTF.

[Contattare il supporto](https://www.adobe.com/account/sign-in.supportportal.html)
