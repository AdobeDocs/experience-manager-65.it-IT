---
title: Impostazione dei valori di timeout per l'uso con le estensioni Acrobat Reader DC
seo-title: Impostazione dei valori di timeout per l'uso con le estensioni Acrobat Reader DC
description: Scoprite come impostare i valori di timeout per l'utilizzo con le estensioni Acrobat Reader DC.
seo-description: Scoprite come impostare i valori di timeout per l'utilizzo con le estensioni Acrobat Reader DC.
uuid: d6d072a0-0a30-417a-98b1-df8b4ff8f911
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a9aeeb89-45e9-4d5d-aa25-8145c89b64f2
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 0%

---


# Impostazione dei valori di timeout per l&#39;uso con le estensioni Acrobat Reader DC {#setting-timeout-values-for-use-with-acrobat-reader-dc-extensions}

Quando lavorate su molti file PDF con le estensioni Acrobat Reader DC, accertatevi che i seguenti valori di timeout siano impostati correttamente per evitare che i processi scadano e non funzionino correttamente:

**Timeout eliminazione documento**

Questo valore può essere impostato nella console di amministrazione. Fate clic su Impostazioni > Impostazioni di sistema di base > Configurazioni e specificate un valore per Timeout eliminazione documento predefinito.

**Timeout AEM moduli di User Manager:** questo valore può essere impostato modificando il file config.xml. Nella console di amministrazione, fate clic su Impostazioni > Gestione utente > Configurazione > Importa ed esporta file di configurazione, quindi fate clic su Esporta. Aprite il file config.xml esportato e modificate le righe seguenti:

&lt;entry key=&quot;assertionValidityInMinutes&quot; value=&quot;600&quot; />

&lt;entry key=&quot;SessionTimeout&quot; value=&quot;600&quot; />

Salvate e importate di nuovo il file config.xml nella console di amministrazione.

**Timeout sessione server applicazione:** questo valore può essere impostato sul server applicazione. Per ulteriori informazioni, consultate la documentazione fornita con il server applicazione.
