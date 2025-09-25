---
title: Gestione delle credenziali locali
description: Scopri come gestire le credenziali locali utilizzando la Gestione archivio fonti attendibili. I moduli AEM supportano le credenziali RSA e DSA nel modulo standard PKCS12.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_certificates_and_credentials
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: c5905272-7d09-47e4-8b35-4cc25a148477
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Security
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: ht
source-wordcount: '533'
ht-degree: 100%

---

# Gestione delle credenziali locali {#managing-local-credentials}

>[!NOTE]
> 
> Assicurati che l’utente disponga dei privilegi di amministratore per accedere alla console dell’amministratore.

Le credenziali locali sono credenziali di chiave privata ospitate in Gestione archivio fonti attendibili. Una *credenziale locale* identifica la posizione in cui sono memorizzate le credenziali DES di un utente. Tramite Gestione archivio fonti attendibili è possibile importare e gestire le credenziali locali utilizzando, ad esempio, i file PFX esistenti, in modo da poter importare, modificare ed eliminare le credenziali locali.

I moduli AEM supportano credenziali RSA e DSA fino a 4096 bit in formato PKCS12 standard (file con estensione pfx e p12).

È possibile importare ed esportare qualsiasi numero di credenziali. Se si desidera sostituire una credenziale scaduta utilizzando lo stesso alias, eliminare la credenziale e quindi importare la nuova credenziale con lo stesso alias.

Per informazioni e istruzioni relative alle estensioni di Adobe Reader DC, vedere [Configurazione delle credenziali per l’utilizzo con le estensioni di Adobe Reader DC](/help/forms/using/admin-help/configuring-credentials-acrobat-reader-dc.md#configuring-credentials-for-use-with-acrobat-reader-dc-extensions).

## Importare una credenziale {#import-a-credential}

1. Nella console di amministrazione, fare clic su Impostazioni > Gestione archivio fonti attendibili > Credenziali locali.
1. Fai clic su Importa. In Tipo archivio fonti attendibili, selezionare una delle opzioni seguenti:

   * **Credenziali firma documento:** credenziali utilizzate per emettere una firma digitale su un documento.
   * **Credenziali estensioni DC di Acrobat Reader:** un certificato digitale specifico per le estensioni di Acrobat Reader DC che consente l’attivazione dei diritti di utilizzo di Adobe Reader nei documenti PDF prodotti.
   * **Predefinite:** indica che si tratta delle credenziali predefinite da utilizzare con le estensioni di Acrobat Reader DC.

   Per informazioni su come ottenere le credenziali, consulta [Preparazione all’installazione di AEM Forms](https://helpx.adobe.com/pdf/aem-forms/6-3/prepare-install-single-server.pdf).

1. Nella casella Alias, digita un identificatore per le credenziali. Questo identificatore viene utilizzato come nome visualizzato per le credenziali nelle estensioni di Acrobat Reader DC e nel servizio di firma. Questo alias viene utilizzato anche per accedere alle credenziali a livello di programmazione tramite l’SDK di AEM Forms.

   >[!NOTE]
   >
   >Il nome alias viene automaticamente convertito in maiuscolo a scopo di visualizzazione. Il nome alias non fa distinzione tra maiuscole e minuscole quando è utilizzato come riferimento in un processo.

1. Fai clic su Sfoglia per individuare le credenziali, digita la password delle credenziali, quindi fai clic su OK.

   Se viene visualizzato il messaggio di errore “Impossibile importare le credenziali a causa di un formato di file errato o di una password errata”, verifica che la password sia valida.

## Esportare una credenziale {#export-a-credential}

Le credenziali vengono esportate come file P12 in formato PKCS#12.

1. Nella console di amministrazione, fare clic su Impostazioni > Gestione archivio fonti attendibili > Credenziali locali.
1. Fai clic sul nome alias della credenziale che desideri esportare, quindi fai clic su Esporta.
1. Nella casella Password, digita la password. Questa password è nuova e viene utilizzata per crittografare la credenziale esportata.
1. Fai clic su Esporta, segui le istruzioni per esportare la credenziale, quindi fai clic su OK.

## Modificare l’alias o il tipo di archivio fonti attendibili di una credenziale {#edit-a-credential-s-alias-or-trust-store-type}

Dopo l’importazione di una credenziale, puoi modificarne il nome alias e il tipo di archivio fonti attendibili.

1. Nella console di amministrazione, fare clic su Impostazioni > Gestione archivio fonti attendibili > Credenziali locali.
1. Fai clic sul nome alias della credenziale da modificare.
1. Fai clic su Aggiorna credenziale.
1. Modifica il nome alias e il tipo di archivio fonti attendibili, quindi fai clic su OK.

## Eliminare una credenziale {#delete-a-credential}

1. Nella console di amministrazione, fare clic su Impostazioni > Gestione archivio fonti attendibili > Credenziali locali.
1. Seleziona le caselle di controllo relative alle credenziali da eliminare.
1. Fai clic su Elimina e quindi su OK.
