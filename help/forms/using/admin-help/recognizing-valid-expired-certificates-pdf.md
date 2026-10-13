---
title: Riconoscimento di certificati validi e scaduti nei documenti PDF
description: Scopri come riconoscere i certificati validi e scaduti nei documenti di PDF.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: dfe2823a-3a0d-4e45-8765-f618529e22dd
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
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
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 8%
---
# Riconoscimento di certificati validi e scaduti nei documenti PDF {#recognizing-valid-and-expired-certificates-in-pdf-documents}

Quando un documento PDF con diritti di utilizzo applicati dalle estensioni Reader viene aperto in Adobe Reader, viene visualizzata una barra di stato che descrive i diritti di utilizzo specifici abilitati nel documento PDF.

Quando il certificato digitale che specifica i diritti di utilizzo per un documento PDF scade e il documento PDF viene aperto in Adobe Reader, una finestra di dialogo informa l&#39;utente che il documento PDF dispone di diritti di utilizzo, ma tali diritti sono disabilitati. Sebbene il messaggio indichi che il documento PDF è stato alterato o manomesso, ciò non avviene necessariamente. Adobe Reader visualizza questo messaggio quando un certificato scade o un documento viene modificato. In Adobe Reader 7.0.x o versione successiva, non è possibile determinare quale caso sia attualmente il problema.

Dopo aver chiuso la finestra di dialogo, Adobe Reader apre il documento PDF. I diritti di utilizzo applicati mediante le estensioni di Acrobat Reader DC non sono disponibili, come previsto. Se il documento di PDF è un modulo interattivo, i campi del modulo sono bloccati e l’utente non può modificare i dati del modulo.
