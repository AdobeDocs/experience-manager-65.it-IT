---
title: Configurazione delle credenziali per l’utilizzo con le estensioni di Acrobat Reader DC
description: Scopri come configurare le credenziali per l’utilizzo con Estensioni di Acrobat Reader DC.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: e8015d59-7587-46dc-a672-e0f1108102ad
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: ht
source-wordcount: '558'
ht-degree: 100%

---

# Configurazione delle credenziali per l’utilizzo con le estensioni di Acrobat Reader DC{#configuring-credentials-for-use-with-acrobat-reader-dc-extensions}

Per applicare i diritti di utilizzo ai documenti PDF, configura AEM Forms con una credenziale valida per Estensioni di Acrobat Reader DC. È possibile che durante l’installazione di AEM Forms sia stata configurata una credenziale. Se non hai configurato le credenziali di Estensioni di Acrobat Reader DC durante l’esecuzione di Gestione configurazione o se hai necessità di importare una credenziale nuova o sostitutiva, puoi utilizzare le pagine Gestione archivio fonti attendibili.

Se utilizzi una credenziale di valutazione, sostituiscila con una di produzione durante il passaggio a questo ambiente. Per aggiornare una credenziale scaduta o di valutazione, elimina innanzitutto la credenziale precedente di Estensioni di Acrobat Reader DC.

Per informazioni su come ottenere le credenziali, consulta [Preparazione all’installazione di AEM Forms (server singolo)](https://helpx.adobe.com/pdf/aem-forms/6-3/prepare-install-single-server.pdf).

L’archivio certificati attendibili può contenere più di una credenziale di Estensioni di Acrobat Reader DC. Imposta una di queste credenziali come credenziale predefinita delle Estensioni di Reader. Le credenziali predefinite vengono utilizzate quando un utente di Workbench non è in grado di determinare quali utilizzare durante la creazione del processo. Queste regole si applicano alle credenziali predefinite:

* Se importi una credenziale di Estensioni di Acrobat Reader DC e l’archivio certificati attendibili non contiene altre credenziali di questa applicazione, quella importata verrà impostata come predefinita.
* Se importi una credenziale di Estensioni di Acrobat Reader DC con l’opzione Predefinita selezionata, il tipo predefinito viene rimosso da una credenziale predefinita esistente. La credenziale importata diventa predefinita.
* Non è possibile eliminare una credenziale predefinita di Estensioni di Acrobat Reader DC. Per eliminare le credenziali predefinite, imposta innanzitutto un’altra credenziale come predefinita. Si verifica un’eccezione a questa regola quando è presente una sola credenziale: in questo caso è possibile eliminarla anche se è quella predefinita.
* Non puoi aggiornare una credenziale predefinita di Estensioni di Acrobat Reader DC.

>[!NOTE]
>
>Puoi anche importare ed eliminare le credenziali a livello di programmazione. Consulta [Programmazione con AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=it).

## Importare una credenziale di Estensioni di Acrobat Reader DC {#import-a-acrobat-reader-dc-extensions-credential}

>[!NOTE]
> 
> Assicurati che l’utente disponga dei privilegi di amministratore per accedere alla console dell’amministratore.

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione archivio fonti attendibili > Credenziali locali.
1. Fai clic su Importa e in Tipo archivio fonti attendibili seleziona Credenziali estensioni di Acrobat Reader DC.
1. (Facoltativo) Per indicare che questa credenziale è quella predefinita da utilizzare con le estensioni di Acrobat Reader DC, seleziona Predefinita.
1. Nella casella Alias, digita un identificatore per le credenziali. Questo identificatore viene utilizzato come nome visualizzato per le credenziali nelle estensioni di Acrobat Reader DC. Questo alias viene utilizzato anche per accedere alle credenziali a livello di programmazione tramite l’SDK di AEM Forms.

   >[!NOTE]
   >
   >Il nome alias viene automaticamente convertito in maiuscolo a scopo di visualizzazione. Il nome alias non fa distinzione tra maiuscole e minuscole quando è utilizzato come riferimento in un processo.

1. Fai clic su Scegli file per individuare le credenziali, digita la password delle credenziali e, quindi, fai clic su OK.

   Se viene visualizzato il messaggio di errore “Impossibile importare le credenziali a causa di un formato di file errato o di una password errata”, verifica che la password sia valida.

## Rimozione delle credenziali di un’estensione di DC Acrobat Reader {#remove-a-acrobat-reader-dc-extensions-credential}

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione archivio fonti attendibili > Credenziali locali.
1. Seleziona la credenziale e fai clic su Elimina.

## Sostituzione di una credenziale delle estensioni di Acrobat Reader DC {#replace-a-acrobat-reader-dc-extensions-credential}

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione archivio fonti attendibili > Credenziali locali.
1. Prendi nota dell’alias della credenziale esistente, quindi selezionalo e fai clic su Elimina.
1. Importa la nuova credenziale utilizzando lo stesso alias.
