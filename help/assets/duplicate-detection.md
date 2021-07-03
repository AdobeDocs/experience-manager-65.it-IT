---
title: Abilita il rilevamento delle risorse duplicate
description: Scopri come abilitare il rilevamento delle risorse duplicate in Experience Manager.
contentOwner: AG
role: User, Admin
feature: Gestione delle risorse, rapporti sulle risorse
exl-id: a403d60e-2193-4835-8f37-4a40f2d01819
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 0%

---

# Abilita il rilevamento delle risorse duplicate {#enable-detection-of-duplicate-assets}

Se tenti di caricare una risorsa esistente in [!DNL Adobe Experience Manager Assets], la funzione di rilevamento duplicato la identifica come duplicato. Il rilevamento dei duplicati è disattivato per impostazione predefinita. Per abilitare la funzione, procedi come segue:

1. Apri la pagina di configurazione della [!DNL Experience Manager] Console web accedendo a `https://[aem_server]:[port]/system/console/configMgr`.
1. Modifica la configurazione del servlet **[!UICONTROL Day CQ DAM Create Asset]**.
1. Selezionare l&#39;opzione **[!UICONTROL Rileva duplicati]** e fare clic su **[!UICONTROL Salva]**.

   ![Seleziona l’opzione per rilevare i duplicati nel servlet](assets/chlimage_1-377.png)

   *Figura: Seleziona l’opzione per rilevare i duplicati nel servlet.*

La funzione di rilevamento duplicati è ora abilitata in [!DNL Assets]. Quando un utente tenta di caricare una risorsa esistente in [!DNL Experience Manager], il sistema controlla la presenza di conflitti e lo indica. Le risorse vengono identificate utilizzando l’hash SHA-1 memorizzato in `jcr:content/metadata/dam:sha1`, il che significa che le risorse duplicate vengono rilevate indipendentemente dai nomi dei file.

>[!MORELIKETHIS]
>
>* [Duplicare le risorse nell’archivio esistente (un tutorial tratto da un membro della community)](https://experience-aem.blogspot.com/2019/06/aem-65-find-duplicate-assets-binaries-in-existing-repository.html)

