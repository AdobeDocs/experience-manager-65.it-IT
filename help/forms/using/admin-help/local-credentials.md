---
title: Gestione delle credenziali locali
seo-title: Gestione delle credenziali locali
description: Scoprite come gestire le credenziali locali.
seo-description: Scoprite come gestire le credenziali locali.
uuid: 3c4358e0-aaff-4e94-a6b2-04b463fca260
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_certificates_and_credentials
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 598a9a03-3773-4620-8867-1f754d8ca031
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '510'
ht-degree: 0%

---


# Gestione delle credenziali locali {#managing-local-credentials}

Le credenziali locali sono credenziali di chiave privata ospitate in Trust Store Management. Una *credenziale locale* identifica la posizione di memorizzazione delle credenziali DES di un utente. Utilizzando Trust Store Management, è possibile importare e gestire le credenziali locali utilizzando, ad esempio, i file PFX esistenti in modo da importare, modificare ed eliminare le credenziali locali.

I moduli AEM supportano le credenziali RSA e DSA fino a 4096 bit nel formato PKCS12 standard (file .pfx e .p12).

Potete importare ed esportare qualsiasi numero di credenziali. Per sostituire una credenziale scaduta con lo stesso alias, eliminare la credenziale e importare la nuova credenziale con lo stesso alias.

Per informazioni e istruzioni relative alle estensioni Acrobat Reader DC, vedere [Configurazione delle credenziali per l&#39;uso con le estensioni Acrobat Reader DC](/help/forms/using/admin-help/configuring-credentials-acrobat-reader-dc.md#configuring-credentials-for-use-with-acrobat-reader-dc-extensions).

## Importa una credenziale {#import-a-credential}

1. Nella console di amministrazione, fate clic su Impostazioni > Gestione archivio attendibili > Credenziali locali.
1. Fai clic su Importa. In Tipo archivio attendibili, selezionare una delle seguenti opzioni:

   * **Credenziali firma documento:** credenziale utilizzata per emettere una firma digitale su un documento.
   * **Credenziali per estensioni Acrobat Reader DC:** Certificato digitale specifico per le estensioni Acrobat Reader DC che consente  diritti di utilizzo Adobe Reader di essere attivato nei documenti PDF prodotti.
   * **Valore predefinito:** indica che si tratta della credenziale predefinita da utilizzare con le estensioni Acrobat Reader DC.

   Per informazioni su come ottenere una credenziale, vedere [Preparazione all&#39;installazione di moduli AEM](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_63).

1. Nella casella Alias, digitare un identificatore per la credenziale. Questo identificatore viene utilizzato come nome visualizzato per la credenziale nelle estensioni Acrobat Reader DC e nel servizio Signature. Questo alias viene utilizzato anche per accedere alla credenziale a livello di programmazione tramite l&#39;SDK dei moduli AEM.

   >[!NOTE]
   >
   >Il nome alias viene automaticamente convertito in maiuscolo a scopo di visualizzazione. Il nome alias non fa distinzione tra maiuscole e minuscole se vi fate riferimento in un processo.

1. Fare clic su Sfoglia per individuare la credenziale, digitare la password della credenziale, quindi fare clic su OK.

   Se viene visualizzato il messaggio di errore &quot;Impossibile importare le credenziali a causa di un formato file errato o di una password non corretta&quot;, verificare che la password sia valida.

## Esportare una credenziale {#export-a-credential}

Le credenziali vengono esportate come file P12 in formato PKCS#12.

1. Nella console di amministrazione, fate clic su Impostazioni > Gestione archivio attendibili > Credenziali locali.
1. Fate clic sul nome alias della credenziale da esportare, quindi fate clic su Esporta.
1. Nella casella Password digitare la password. Questa password è nuova e viene utilizzata per crittografare le credenziali esportate.
1. Fate clic su Esporta, seguite le istruzioni per esportare le credenziali, quindi fate clic su OK.

## Modificare l&#39;alias o il tipo di archivio delle credenziali {#edit-a-credential-s-alias-or-trust-store-type}

Dopo l&#39;importazione di una credenziale, potete modificarne il nome alias e il tipo di archivio attendibili.

1. Nella console di amministrazione, fate clic su Impostazioni > Gestione archivio attendibili > Credenziali locali.
1. Fate clic sul nome alias della credenziale da modificare.
1. Fare clic su Aggiorna credenziali.
1. Modificate il nome alias e il tipo di archivio attendibili come richiesto e fate clic su OK.

## Eliminare una credenziale {#delete-a-credential}

1. Nella console di amministrazione, fate clic su Impostazioni > Gestione archivio attendibili > Credenziali locali.
1. Selezionare le caselle di controllo per le credenziali da eliminare.
1. Fate clic su Elimina, quindi su OK.

