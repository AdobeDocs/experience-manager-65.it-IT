---
title: Impostazione dei valori di timeout per l’utilizzo con le estensioni Acrobat Reader DC
seo-title: Setting timeout values for use with Acrobat Reader DC extensions
description: Scopri come impostare i valori di timeout per l’utilizzo con le estensioni Acrobat Reader DC.
seo-description: Learn how to set timeout values for use with Acrobat Reader DC extensions.
uuid: d6d072a0-0a30-417a-98b1-df8b4ff8f911
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a9aeeb89-45e9-4d5d-aa25-8145c89b64f2
exl-id: 0a55aab3-14a3-41ad-8533-dc2cd116a848
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 0%

---

# Impostazione dei valori di timeout per l’utilizzo con le estensioni Acrobat Reader DC  {#setting-timeout-values-for-use-with-acrobat-reader-dc-extensions}

Quando lavori su molti file PDF nelle estensioni Acrobat Reader DC, accertati che i seguenti valori di timeout siano impostati in modo appropriato per evitare che i processi si interrompano per timeout o non riescano:

**Timeout eliminazione documento**

Questo valore può essere impostato nella console di amministrazione. Fai clic su Impostazioni > Impostazioni sistema core > Configurazioni e specifica un valore per Timeout eliminazione documento predefinito.

**Timeout moduli AEM di User Manager:** Questo valore può essere impostato modificando il file config.xml. Nella console di amministrazione, fare clic su Impostazioni > Gestione utente > Configurazione > Importa ed esporta file di configurazione, quindi fare clic su Esporta. Apri il file config.xml esportato e modifica le righe seguenti:

&lt;entry key=&quot;assertionValidityInMinutes&quot; value=&quot;600&quot;/>

&lt;entry key=&quot;SessionTimeout&quot; value=&quot;600&quot;/>

Salva e importa nuovamente il file config.xml nella console di amministrazione.

**Timeout sessione server applicazioni:** Questo valore può essere impostato sul server applicazioni. Per ulteriori informazioni, vedere la documentazione fornita con il server applicazioni.
