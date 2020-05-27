---
title: Abilita rilevamento delle risorse duplicate
description: Scoprite come abilitare il rilevamento di risorse duplicate in Experience Manager.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 566add37d6dd7efe22a99fc234ca42878f050aee
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 0%

---


# Abilita rilevamento delle risorse duplicate {#enable-detection-of-duplicate-assets}

Se tenti di caricare una risorsa esistente in Risorse Adobe Experience Manager, la funzione di rilevamento duplicato la identifica come duplicato. Per impostazione predefinita, il rilevamento di duplicati è disabilitato. Per attivare la funzione, effettuare le seguenti operazioni:

1. Aprite la pagina Configurazione console Web di Experience Manager accedendo `https://[aem_server]:[port]/system/console/configMgr`.
1. Modificate la configurazione per il servlet **[!UICONTROL Day CQ DAM Create Asset]**.
1. Selezionate l’opzione **[!UICONTROL Rileva duplicati]** e fate clic su **[!UICONTROL Salva]**.

   ![Selezionate l’opzione Rileva duplicato nel servlet](assets/chlimage_1-377.png)

   *Figura: Selezionate l’opzione Rileva duplicato nel servlet*

La funzione Rileva duplicato è ora abilitata in Risorse. Quando un utente tenta di caricare una risorsa esistente in Experience Manager, il sistema verifica la presenza di conflitti e la segnala. Le risorse vengono identificate tramite hash SHA-1 memorizzato in `jcr:content/metadata/dam:sha1`, il che significa che le risorse duplicate vengono rilevate indipendentemente dal nome del file.

>[!MORELIKETHIS]
>
>* [Duplicare le risorse presenti nell&#39;archivio esistente (esercitazione di un membro della community)](https://experience-aem.blogspot.com/2019/06/aem-65-find-duplicate-assets-binaries-in-existing-repository.html)

