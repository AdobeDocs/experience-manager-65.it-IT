---
title: Gestione delle credenziali locali
description: Scopri come gestire le credenziali locali utilizzando Gestione archivio fonti attendibili. I moduli AEM supportano le credenziali RSA e DSA nel modulo standard PKCS12.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_certificates_and_credentials
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: c5905272-7d09-47e4-8b35-4cc25a148477
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Security
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: tm+mt
source-wordcount: '533'
ht-degree: 0%

---

# Gestione delle credenziali locali {#managing-local-credentials}

>[!NOTE]
> 
> Assicurati che l’utente disponga dei privilegi di amministratore per accedere alla console dell’amministratore.

Le credenziali locali sono credenziali di chiave privata ospitate in Gestione archivio fonti attendibili. Una *credenziale locale* identifica la posizione in cui sono memorizzate le credenziali DES di un utente. Tramite Gestione archivio fonti attendibili è possibile importare e gestire le credenziali locali utilizzando, ad esempio, i file PFX esistenti, in modo da poter importare, modificare ed eliminare le credenziali locali.

I moduli AEM supportano le credenziali RSA e DSA fino a 4096 bit nel formato standard PKCS12 (file .pfx e .p12).

È possibile importare ed esportare un numero qualsiasi di credenziali. Se si desidera sostituire una credenziale scaduta utilizzando lo stesso alias, eliminare la credenziale e quindi importare la nuova credenziale con lo stesso alias.

Per informazioni e istruzioni relative alle estensioni Acrobat Reader DC, vedere [Configurazione delle credenziali per l&#39;utilizzo con le estensioni Acrobat Reader DC](/help/forms/using/admin-help/configuring-credentials-acrobat-reader-dc.md#configuring-credentials-for-use-with-acrobat-reader-dc-extensions).

## Importa credenziali {#import-a-credential}

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione archivio fonti attendibili > Credenziali locali.
1. Fai clic su Importa. In Tipo archivio fonti attendibili selezionare una delle opzioni seguenti:

   * **Credenziali firma documento:** Credenziali utilizzate per emettere una firma digitale su un documento.
   * **Credenziali estensioni Acrobat Reader DC:** un certificato digitale specifico delle estensioni Acrobat Reader DC che consente l&#39;attivazione dei diritti di utilizzo Adobe Reader nei documenti PDF prodotti.
   * **Predefinito:** indica che si tratta delle credenziali predefinite da utilizzare con le estensioni di Acrobat Reader DC.

   Per informazioni su come ottenere le credenziali, vedere [Preparazione all&#39;installazione dei moduli AEM](https://helpx.adobe.com/pdf/aem-forms/6-3/prepare-install-single-server.pdf).

1. Nella casella Alias digitare un identificatore per le credenziali. Questo identificatore viene utilizzato come nome visualizzato per le credenziali nelle estensioni di Acrobat Reader DC e nel servizio Signature. Questo alias viene utilizzato anche per accedere alle credenziali a livello di programmazione utilizzando l&#39;AEM form SDK.

   >[!NOTE]
   >
   >Il nome dell’alias viene automaticamente convertito in maiuscolo a scopo di visualizzazione. Il nome dell&#39;alias non fa distinzione tra maiuscole e minuscole quando vi si fa riferimento in un processo.

1. Fare clic su Sfoglia per individuare le credenziali, digitare la password delle credenziali e quindi fare clic su OK.

   Se viene visualizzato il messaggio di errore &quot;Impossibile importare le credenziali a causa di un formato di file errato o di una password errata&quot;, verificare che la password sia valida.

## Esportare le credenziali {#export-a-credential}

Le credenziali vengono esportate come file P12 in formato PKCS#12.

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione archivio fonti attendibili > Credenziali locali.
1. Fare clic sul nome alias delle credenziali che si desidera esportare e quindi su Esporta.
1. Nella casella Password digitare la password. Questa password è nuova e viene utilizzata per crittografare le credenziali esportate.
1. Fare clic su Esporta, seguire le istruzioni per esportare le credenziali, quindi fare clic su OK.

## Modificare l&#39;alias o il tipo di archivio fonti attendibili di una credenziale {#edit-a-credential-s-alias-or-trust-store-type}

Dopo l&#39;importazione di una credenziale, è possibile modificarne il nome alias e il tipo di archivio fonti attendibili.

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione archivio fonti attendibili > Credenziali locali.
1. Fare clic sul nome alias delle credenziali che si desidera modificare.
1. Fai clic su Aggiorna credenziali.
1. Modificare il nome alias e il tipo di archivio fonti attendibili, quindi fare clic su OK.

## Eliminare le credenziali {#delete-a-credential}

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione archivio fonti attendibili > Credenziali locali.
1. Selezionare le caselle di controllo relative alle credenziali da eliminare.
1. Fare clic su Elimina e quindi su OK.
