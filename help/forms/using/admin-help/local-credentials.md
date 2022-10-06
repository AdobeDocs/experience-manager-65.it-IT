---
title: Gestione delle credenziali locali
seo-title: Managing local credentials
description: Scopri come gestire le credenziali locali.
seo-description: Learn how to manage local credentials.
uuid: 3c4358e0-aaff-4e94-a6b2-04b463fca260
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_certificates_and_credentials
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 598a9a03-3773-4620-8867-1f754d8ca031
exl-id: c5905272-7d09-47e4-8b35-4cc25a148477
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '501'
ht-degree: 0%

---

# Gestione delle credenziali locali {#managing-local-credentials}

Le credenziali locali sono credenziali di chiave privata ospitate in Trust Store Management. A *credenziale locale* identifica la posizione in cui viene memorizzata la credenziale DES di un utente. Utilizzando Trust Store Management, è possibile importare e gestire le credenziali locali utilizzando, ad esempio, i file PFX esistenti in modo da importare, modificare ed eliminare le credenziali locali.

I moduli AEM supportano le credenziali RSA e DSA fino a 4096 bit nel formato standard PKCS12 (file .pfx e .p12).

È possibile importare ed esportare qualsiasi numero di credenziali. Se si desidera sostituire una credenziale scaduta utilizzando lo stesso alias, eliminare la credenziale e quindi importare la nuova credenziale con lo stesso alias.

Per informazioni e istruzioni relative alle estensioni Acrobat Reader DC, consulta [Configurazione delle credenziali per l’utilizzo con le estensioni Acrobat Reader DC](/help/forms/using/admin-help/configuring-credentials-acrobat-reader-dc.md#configuring-credentials-for-use-with-acrobat-reader-dc-extensions).

## Importare una credenziale {#import-a-credential}

1. Nella console di amministrazione, fare clic su Impostazioni > Gestione archivio attendibilità > Credenziali locali.
1. Fai clic su Importa. In Tipo archivio trust selezionare una delle seguenti opzioni:

   * **Credenziali firma documento:** Credenziale utilizzata per emettere una firma digitale su un documento.
   * **Credenziale delle estensioni Acrobat Reader DC:** Un certificato digitale specifico per le estensioni Acrobat Reader DC che consente di attivare i diritti di utilizzo di Adobe Reader nei documenti PDF prodotti.
   * **Predefinito:** Indica che si tratta della credenziale predefinita da utilizzare con le estensioni Acrobat Reader DC.

   Per informazioni su come ottenere una credenziale, consulta [Preparazione all’installazione AEM moduli](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_63).

1. Nella casella Alias digitare un identificatore per la credenziale. Questo identificatore viene utilizzato come nome visualizzato per la credenziale nelle estensioni Acrobat Reader DC e nel servizio Signature. Questo alias viene utilizzato anche per accedere alle credenziali a livello di programmazione utilizzando l’SDK per moduli AEM.

   >[!NOTE]
   >
   >Il nome alias viene automaticamente convertito in maiuscolo a scopo di visualizzazione. Il nome dell&#39;alias non fa distinzione tra maiuscole e minuscole quando vi si fa riferimento in un processo.

1. Fare clic su Sfoglia per individuare la credenziale, digitare la password della credenziale, quindi fare clic su OK.

   Se viene visualizzato il messaggio di errore &quot;Impossibile importare le credenziali a causa di un formato di file errato o di una password errata&quot;, verificare che la password sia valida.

## Esportare una credenziale {#export-a-credential}

Le credenziali vengono esportate come file P12 in formato PKCS#12.

1. Nella console di amministrazione, fare clic su Impostazioni > Gestione archivio attendibilità > Credenziali locali.
1. Fare clic sul nome dell&#39;alias della credenziale che si desidera esportare, quindi fare clic su Esporta.
1. Nella casella Password digitare la password. Questa password è nuova e viene utilizzata per crittografare la credenziale esportata.
1. Fare clic su Esporta, seguire le istruzioni per esportare le credenziali, quindi fare clic su OK.

## Modificare l’alias o il tipo di archivio delle credenziali {#edit-a-credential-s-alias-or-trust-store-type}

Dopo aver importato una credenziale, è possibile modificarne il nome alias e il tipo di archivio attendibili.

1. Nella console di amministrazione, fare clic su Impostazioni > Gestione archivio attendibilità > Credenziali locali.
1. Fare clic sul nome alias della credenziale che si desidera modificare.
1. Fare clic su Aggiorna credenziali.
1. Modificare il nome dell&#39;alias e il tipo di archivio attendibili come richiesto e fare clic su OK.

## Eliminare una credenziale {#delete-a-credential}

1. Nella console di amministrazione, fare clic su Impostazioni > Gestione archivio attendibilità > Credenziali locali.
1. Selezionare le caselle di controllo relative alle credenziali da eliminare.
1. Fare clic su Elimina, quindi su OK.
