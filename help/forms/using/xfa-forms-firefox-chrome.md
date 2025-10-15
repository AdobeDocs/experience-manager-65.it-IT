---
title: Come aprire PDF forms basato su XFA su Firefox e Chrome
description: Come aprire PDF forms basato su XFA su Firefox e Chrome
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Security
geptopics: SG_AEMFORMS/categories/jee
role: Admin
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
source-git-commit: ebb61f2c5056a780e829e64031f8eba69a8ae25b
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 1%

---

# Come aprire PDF forms basato su XFA su Firefox e Chrome

## Problema  

Il visualizzatore PDF incorporato introdotto con Mozilla Firefox e Google Chrome non supporta PDF forms basato su XFA. Pertanto, i PDF forms basati su XFA non si aprono nelle versioni successive di Firefox e Chrome.

## Soluzione

Per utilizzare PDF forms basato su XFA su Firefox e Chrome, esegui i seguenti passaggi per configurare Firefox e Chrome per aprire PDF utilizzando Adobe Reader o Adobe Acrobat.

>[!NOTE]
> 
> Verifica che sul computer sia installato Adobe Reader o Adobe Acrobat.

### Configurare Firefox

1. In Firefox scegliere **Strumenti > Opzioni**.

1. Nella finestra di dialogo Opzioni, fai clic su **Applicazioni**.

1. Nella scheda Applicazioni digitare PDF nel campo di ricerca.

1. Per il tipo di contenuto PDF (Portable Document Format) nel risultato della ricerca, selezionare **Usa Adobe Acrobat (in Firefox)** dall&#39;elenco a discesa Azione.
   ![use-adobe-acrobat](/help/forms/using/assets/use-adobe-acrobat.png)
1. Fare clic su OK.

1. Riavvia Firefox.

### Configurare Chrome

1. In Chrome, vai su chrome://plugins/.

1. Fai clic su Disattiva in Visualizzatore PDF di Chrome, quindi su Abilita in Plug-in di Adobe PDF.
   ![chrome-pdf-viewer](/help/forms/using/assets/chrome-image.png)
Per ulteriori informazioni, consulta la documentazione del [plug-in Adobe PDF](https://support.google.com/chrome/?hl=en&visit_id=638803785294106945-2276548125&rd=4&topic=3421431#topic=7439538) di Google.

>[!NOTE]
> 
> LiveCycle ES4 fornisce il supporto per il rendering di moduli basati su XFA in HTML5 in modo che i moduli possano essere aperti in browser con supporto per HTML5, inclusi quelli in esecuzione su dispositivi mobili come iPad. La rappresentazione HTML5 dei moduli mantiene il layout della struttura del modulo e supporta la maggior parte delle logiche del modulo (come JavaScript, calcolo dei moduli e convalide dei moduli) incorporate nel modello di modulo XFA. In questo modo, gli investimenti tecnologici nei moduli XFA vengono facilmente trasferiti su dispositivi in cui non è possibile eseguire il plug-in Adobe Reader.
>Per ulteriori informazioni, consulta la [documentazione del prodotto LiveCycle](https://business.adobe.com/it/products/experience-manager/forms/aem-forms.html).

[Note legali](https://chl-author-preview.corp.adobe.com/content/help/en/legal/legal-notices.html)    |    [Informativa sulla privacy online](https://www.adobe.com/it/privacy.html)