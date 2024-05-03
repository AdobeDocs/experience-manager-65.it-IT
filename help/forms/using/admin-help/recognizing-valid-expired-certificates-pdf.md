---
title: Riconoscimento di certificati validi e scaduti nei documenti di PDF
description: Scopri come riconoscere i certificati validi e scaduti nei documenti di PDF.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: dfe2823a-3a0d-4e45-8765-f618529e22dd
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 0%

---

# Riconoscimento di certificati validi e scaduti nei documenti di PDF {#recognizing-valid-and-expired-certificates-in-pdf-documents}

Quando un documento PDF con diritti di utilizzo applicati dalle estensioni di Reader viene aperto in Adobe Reader, viene visualizzata una barra di stato che descrive i diritti di utilizzo specifici abilitati nel documento PDF.

Quando il certificato digitale che specifica i diritti di utilizzo per un documento PDF scade e il documento PDF viene aperto in Adobe Reader, una finestra di dialogo informa l&#39;utente che il documento PDF dispone di diritti di utilizzo, ma tali diritti sono disabilitati. Sebbene il messaggio indichi che il documento PDF è stato alterato o manomesso, ciò non avviene necessariamente. Adobe Reader visualizza questo messaggio quando un certificato scade o un documento viene modificato. In Adobe Reader 7.0.x o versione successiva, non è possibile determinare quale caso sia attualmente il problema.

Dopo aver chiuso la finestra di dialogo, Adobe Reader apre il documento PDF. I diritti di utilizzo applicati utilizzando le estensioni di Acrobat Reader DC non sono disponibili, come previsto. Se il documento PDF è un modulo interattivo, i campi del modulo sono bloccati e l’utente non può modificare i dati del modulo.
