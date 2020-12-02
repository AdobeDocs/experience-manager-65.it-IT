---
title: Abilita rilevamento delle risorse duplicate
description: Scoprite come attivare il rilevamento di risorse duplicate nel Experience Manager .
contentOwner: AG
translation-type: tm+mt
source-git-commit: 9fc1201db83ae0d3bb902d4dc3ab6d78cc1dc251
workflow-type: tm+mt
source-wordcount: '157'
ht-degree: 0%

---


# Abilita il rilevamento delle risorse duplicate {#enable-detection-of-duplicate-assets}

Se tentate di caricare una risorsa esistente in [!DNL Adobe Experience Manager Assets], la funzione di rilevamento duplicato la identifica come duplicato. Per impostazione predefinita, il rilevamento di duplicati è disabilitato. Per attivare la funzione, effettuare le seguenti operazioni:

1. Aprite la [!DNL Experience Manager] pagina di configurazione della console Web accedendo a `https://[aem_server]:[port]/system/console/configMgr`.
1. Modificate la configurazione per il servlet **[!UICONTROL Day CQ DAM Create Asset]**.
1. Selezionare l&#39;opzione **[!UICONTROL Rileva duplicato]**, quindi fare clic su **[!UICONTROL Salva]**.

   ![Selezionate l’opzione Rileva duplicato nel servlet](assets/chlimage_1-377.png)

   *Figura: Selezionate l’opzione Rileva duplicato nel servlet.*

La funzione Rileva duplicato è ora abilitata in [!DNL Assets]. Quando un utente tenta di caricare una risorsa esistente in [!DNL Experience Manager], il sistema verifica la presenza di conflitti e la segnala. Le risorse vengono identificate tramite hash SHA-1 memorizzato in `jcr:content/metadata/dam:sha1`, il che significa che le risorse duplicate vengono rilevate indipendentemente dal nome del file.

>[!MORELIKETHIS]
>
>* [Duplicare le risorse presenti nell&#39;archivio esistente (esercitazione di un membro della community)](https://experience-aem.blogspot.com/2019/06/aem-65-find-duplicate-assets-binaries-in-existing-repository.html)

