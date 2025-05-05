---
title: Problemi di visualizzazione per PDF forms basato su XFA e documenti protetti tramite policy
description: Problemi di visualizzazione per PDF forms basato su XFA e documenti protetti tramite policy
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Security
geptopics: SG_AEMFORMS/categories/jee
role: Admin
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
source-git-commit: ebb61f2c5056a780e829e64031f8eba69a8ae25b
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 0%

---

# Problemi di visualizzazione per PDF forms basato su XFA e documenti protetti tramite policy

Se non riesci ad aprire un modulo PDF basato su XFA o un documento protetto tramite policy utilizzando Adobe LiveCycle Rights Management, verifica i seguenti motivi:

* I documenti PDF forms basati su XFA e protetti tramite policy richiedono Adobe® Acrobat® o Adobe® Reader®, versione 8 e successive. Consulta [Download di Adobe](https://www.adobe.com/downloads.html) per scaricare il Reader o Acrobat più recente.
* Browser come Mozilla Firefox e Google Chrome offrono un visualizzatore PDF integrato che non supporta PDF forms basato su XFA. Per visualizzare i PDF forms basati su XFA in questi browser, è necessario configurare per l’apertura di PDF con Acrobat o Reader. Per ulteriori informazioni, consulta PDF forms basato su XFA su Mozilla Firefox e Google Chrome.
* Acrobat e Reader, su Microsoft® Windows®, consentono di configurare per l’apertura di PDF in modalità Visualizzazione protetta, impedendo l’apertura di documenti PDF forms basati su XFA e protetti tramite policy. Assicurati che la modalità Visualizzazione protetta nell’Acrobat o nel Reader sia disabilitata. Per ulteriori informazioni, vedere [Visualizzazione protetta (solo Windows)](https://helpx.adobe.com/it/acrobat/kb/end-of-support-acrobat-x-reader-x.html).
* Se tenti di accedere a documenti PDF forms basati su XFA o protetti tramite policy sul tuo dispositivo mobile, considera quanto segue:

   * L’apertura di documenti protetti tramite policy su dispositivi mobili richiede Adobe Reader per dispositivi mobili. Per ulteriori informazioni, vedere [App mobile Adobe Reader](https://www.adobe.com/in/acrobat/mobile/acrobat-reader.html).
   * I dispositivi mobili e gli smartphone iOS, Android e Blackberry non supportano il plug-in Adobe Reader con moduli XFA. LiveCycle ES4 fornisce un servizio che esegue il targeting dei dispositivi mobili utilizzando HTML5; il creatore del modulo deve utilizzare tale servizio per consentire l&#39;utilizzo dei moduli su tali dispositivi.
   * Se utilizzi lo stile Metro su un dispositivo mobile Windows 8, passa alla visualizzazione classica o utilizza HTML5 con LiveCycle ES4.

>[!NOTE]
>
>LiveCycle ES4 fornisce il supporto per il rendering di moduli basati su XFA in HTML5 in modo che i moduli possano essere aperti in browser con supporto per HTML5, inclusi quelli in esecuzione su dispositivi mobili come iPad. La rappresentazione HTML5 dei moduli mantiene il layout della struttura del modulo e supporta la maggior parte delle logiche del modulo (come JavaScript, calcolo dei moduli e convalide dei moduli) incorporate nel modello di modulo XFA. In questo modo, gli investimenti tecnologici nei moduli XFA vengono facilmente trasferiti ai dispositivi in cui non è possibile eseguire il plug-in Adobe Reader.
>Per ulteriori informazioni, consulta Aggiornamento alla [documentazione del prodotto LiveCycle](https://business.adobe.com/products/experience-manager/forms/aem-forms.html).

[Note legali](https://chl-author-preview.corp.adobe.com/content/help/en/legal/legal-notices.html)    |    [Informativa sulla privacy online](https://www.adobe.com/it/privacy.html)