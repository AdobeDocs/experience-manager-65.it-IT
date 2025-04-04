---
title: Impostazione dei valori di timeout per l’utilizzo con le estensioni di Acrobat Reader DC
description: Scopri come impostare i valori di timeout per l’utilizzo con le estensioni Acrobat Reader DC.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 0a55aab3-14a3-41ad-8533-dc2cd116a848
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 0%

---

# Impostazione dei valori di timeout per l’utilizzo con le estensioni di Acrobat Reader DC  {#setting-timeout-values-for-use-with-acrobat-reader-dc-extensions}

>[!NOTE]
> 
> Assicurati che l’utente disponga dei privilegi di amministratore per accedere alla console dell’amministratore.

Quando lavori su molti file PDF nelle estensioni di Acrobat Reader DC, accertati che i seguenti valori di timeout siano impostati in modo appropriato per evitare che i processi si interrompano per timeout o si interrompano:

**Timeout eliminazione documento**

Questo valore può essere impostato nella console di amministrazione. Fai clic su Impostazioni > Impostazioni sistema core > Configurazioni e specifica un valore per Timeout eliminazione documento predefinito.

**Timeout moduli AEM di User Manager:** Questo valore può essere impostato modificando il file config.xml. Nella console di amministrazione, fai clic su Impostazioni > Gestione utente > Configurazione > Importa ed esporta file di configurazione, quindi fai clic su Esporta. Apri il file config.xml esportato e modifica le righe seguenti:

&lt;entry key=&quot;assertionValidityInMinutes&quot; value=&quot;600&quot;/>

&lt;entry key=&quot;SessionTimeout&quot; value=&quot;600&quot;/>

Salva e importa nuovamente il file config.xml nella console di amministrazione.

**Timeout sessione server applicazioni:** Questo valore può essere impostato sul server applicazioni. Per ulteriori informazioni, vedere la documentazione fornita con il server applicazioni.
