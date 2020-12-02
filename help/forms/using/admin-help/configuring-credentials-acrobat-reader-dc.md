---
title: Configurazione delle credenziali per l'uso con le estensioni Acrobat Reader DC
seo-title: Configurazione delle credenziali per l'uso con le estensioni Acrobat Reader DC
description: Scoprite come configurare le credenziali per l'utilizzo con le estensioni Acrobat Reader DC.
seo-description: Scoprite come configurare le credenziali per l'utilizzo con le estensioni Acrobat Reader DC.
uuid: 9210e6c9-6f5c-402d-b355-b104cdffd5eb
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 5bb32fb1-4b6e-412f-aa16-f60db9dcaba1
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '576'
ht-degree: 0%

---


# Configurazione delle credenziali per l&#39;uso con le estensioni Acrobat Reader DC{#configuring-credentials-for-use-with-acrobat-reader-dc-extensions}

Per applicare diritti di utilizzo ai documenti PDF, configurare AEM moduli con una credenziale valida per le estensioni Acrobat Reader DC. È possibile che sia stata configurata una credenziale durante l&#39;installazione dei moduli AEM. Se non avete configurato la credenziale delle estensioni Acrobat Reader DC durante l&#39;esecuzione di Configuration Manager o se avete bisogno di importare una credenziale nuova o sostitutiva, potete farlo utilizzando le pagine Gestione store attendibile.

Se utilizzate una credenziale di valutazione, sostituitela con una credenziale di produzione quando vi spostate nell&#39;ambiente di produzione. Per aggiornare una credenziale scaduta o di valutazioni, eliminare prima la credenziale delle estensioni Acrobat Reader DC precedente.

Per informazioni su come ottenere una credenziale, vedere [Preparazione all&#39;installazione dei moduli AEM (Server singolo)](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_63).

L&#39;archivio attendibili può contenere più credenziali di estensione Acrobat Reader DC. È necessario specificare una di queste credenziali come credenziale di Reader predefinita Estensioni. La credenziale predefinita viene utilizzata quando un utente di Workbench non è in grado di determinare quale credenziale utilizzare durante la creazione del processo. Queste regole si applicano alle credenziali predefinite:

* Se importate una credenziale di estensione Acrobat Reader DC e l&#39;archivio attendibili non contiene altre credenziali di estensione Acrobat Reader DC, viene impostata come predefinita.
* Se si importa una credenziale di estensione Acrobat Reader DC con l&#39;opzione Predefinito selezionata, il tipo predefinito viene rimosso da una credenziale predefinita esistente. La credenziale importata diventa l&#39;impostazione predefinita.
* Non è possibile eliminare una credenziale di estensione Acrobat Reader DC predefinita. Per eliminare la credenziale predefinita, impostare prima un&#39;altra credenziale come predefinita. Un&#39;eccezione a questa regola è che se esiste una sola credenziale, è possibile eliminarla anche se è l&#39;impostazione predefinita.
* Non è possibile aggiornare una credenziale di estensione Acrobat Reader DC predefinita.

>[!NOTE]
>
>È inoltre possibile importare ed eliminare le credenziali a livello di programmazione. (Vedere [Programmazione con moduli AEM](https://www.adobe.com/go/learn_aemforms_programming_63).)

## Importare una credenziale di estensione Acrobat Reader DC {#import-a-acrobat-reader-dc-extensions-credential}

1. Nella console di amministrazione, fate clic su Impostazioni > Gestione archivio attendibili > Credenziali locali.
1. Fare clic su Importa e, in Tipo archivio attendibili, selezionare Credenziale estensioni Acrobat Reader DC.
1. (Facoltativo) Per indicare che questa credenziale è la credenziale predefinita da utilizzare con le estensioni Acrobat Reader DC, selezionare Predefinito.
1. Nella casella Alias, digitare un identificatore per la credenziale. Questo identificatore viene utilizzato come nome visualizzato per la credenziale nelle estensioni Acrobat Reader DC. Questo alias viene utilizzato anche per accedere alla credenziale a livello di programmazione tramite l&#39;SDK dei moduli AEM.

   >[!NOTE]
   >
   >Il nome alias viene automaticamente convertito in maiuscolo a scopo di visualizzazione. Il nome alias non fa distinzione tra maiuscole e minuscole se vi fate riferimento in un processo.

1. Fare clic su Scegli file per individuare la credenziale, digitare la password della credenziale, quindi fare clic su OK.

   Se viene visualizzato il messaggio di errore &quot;Impossibile importare le credenziali a causa di un formato file errato o di una password non corretta&quot;, verificare che la password sia valida.

## Rimuovere una credenziale di estensione Acrobat Reader DC {#remove-a-acrobat-reader-dc-extensions-credential}

1. Nella console di amministrazione, fate clic su Impostazioni > Gestione archivio attendibili > Credenziali locali.
1. Selezionate la credenziale e fate clic su Elimina.

## Sostituire una credenziale di estensione Acrobat Reader DC {#replace-a-acrobat-reader-dc-extensions-credential}

1. Nella console di amministrazione, fate clic su Impostazioni > Gestione archivio attendibili > Credenziali locali.
1. Prendete nota dell&#39;alias della credenziale esistente, selezionatelo e fate clic su Elimina.
1. Importa la nuova credenziale utilizzando esattamente lo stesso nome alias.

