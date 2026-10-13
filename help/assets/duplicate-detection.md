---
title: Abilita il rilevamento delle risorse duplicate
description: Scopri come abilitare il rilevamento delle risorse duplicate in Experience Manager.
contentOwner: AG
role: User, Admin
feature: Asset Management,Asset Reports
exl-id: a403d60e-2193-4835-8f37-4a40f2d01819
hide: true
solution: Experience Manager, Experience Manager Assets
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: d09181b5-a36a-43de-ba01-36641440bc43
    internal-label: Experience Manager Assets
feature_v2:
  - id: 7d2b2ec8-499c-5434-9ffd-9218cd71f683
    internal-label: Asset Management
  - id: ac365bec-0634-4744-9473-c42f47320593
    internal-label: Asset management and governance
subfeature_v2:
  - id: c29e3a96-cd2b-4e21-b382-a8279aa04553
    internal-label: Asset reports
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 0%
---
# Abilita il rilevamento delle risorse duplicate {#enable-detection-of-duplicate-assets}

Se si tenta di caricare una risorsa esistente in [!DNL Adobe Experience Manager Assets], la funzionalità di rilevamento duplicati la identifica come duplicata. Il rilevamento duplicati è disabilitato per impostazione predefinita. Per attivare la funzione, effettuare le seguenti operazioni:

1. Aprire la pagina di configurazione della console Web [!DNL Experience Manager] accedendo a `https://[aem_server]:[port]/system/console/configMgr`.
1. Modifica la configurazione per il servlet **[!UICONTROL Day CQ DAM Create Asset]**.
1. Seleziona l&#39;opzione **[!UICONTROL rileva duplicati]** e fai clic su **[!UICONTROL Salva]**.

   ![Selezionare l&#39;opzione di rilevamento duplicati nel servlet](assets/chlimage_1-377.png)

   *Figura: selezionare l&#39;opzione di rilevamento duplicati nel servlet.*

La funzionalità di rilevamento duplicati è ora abilitata in [!DNL Assets]. Quando un utente cerca di caricare una risorsa esistente in [!DNL Experience Manager], il sistema verifica la presenza di un conflitto e lo indica. Le risorse vengono identificate utilizzando l&#39;hash SHA-1 archiviato in `jcr:content/metadata/dam:sha1`, il che significa che le risorse duplicate vengono rilevate indipendentemente dai nomi dei file.

>[!MORELIKETHIS]
>
>* [Risorse duplicate nell&#39;archivio esistente (un&#39;esercitazione eseguita da un membro della community)](https://experience-aem.blogspot.com/2019/06/aem-65-find-duplicate-assets-binaries-in-existing-repository.html)
>* [Rileva risorse duplicate in AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/detect-duplicate-assets.html?lang=it)
