---
title: Riconoscimento di certificati validi e scaduti nei documenti PDF
seo-title: Riconoscimento di certificati validi e scaduti nei documenti PDF
description: Scoprite come riconoscere certificati validi e scaduti nei documenti PDF.
seo-description: Scoprite come riconoscere certificati validi e scaduti nei documenti PDF.
uuid: ceeff57a-586f-4f7b-852f-2a637f003d7e
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 4559218a-65ba-4577-ad26-7721e28971bc
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 0%

---


# Riconoscimento di certificati validi e scaduti nei documenti PDF {#recognizing-valid-and-expired-certificates-in-pdf-documents}

Quando in  Adobe Reader viene aperto un documento PDF con diritti di utilizzo applicati da Estensioni Reader, viene visualizzata una barra di stato che descrive i diritti di utilizzo specifici attivati nel documento PDF.

Quando il certificato digitale che specifica i diritti di utilizzo per un documento PDF scade e il documento PDF viene aperto in  Adobe Reader, viene visualizzata una finestra di dialogo in cui si informa l&#39;utente che il documento PDF dispone di diritti di utilizzo, ma tali diritti sono disattivati. Anche se il messaggio indica che il documento PDF è stato alterato o alterato, ciò non avviene necessariamente.  Adobe Reader visualizza questo messaggio alla scadenza di un certificato o alla modifica di un documento. In  Adobe Reader 7.0.x o versione successiva, non è possibile determinare quale caso è al momento il problema.

Dopo aver chiuso la finestra di dialogo,  Adobe Reader apre il documento PDF. I diritti di utilizzo applicati tramite le estensioni Acrobat Reader DC non sono disponibili, come previsto. Se il documento PDF è un modulo interattivo, i campi del modulo sono bloccati e l&#39;utente non può modificare i dati del modulo.
