---
title: Abilita il rilevamento delle risorse duplicate
description: Scopri come abilitare il rilevamento delle risorse duplicate in Experience Manager.
contentOwner: AG
role: User, Admin
feature: Asset Management,Asset Reports
exl-id: a403d60e-2193-4835-8f37-4a40f2d01819
hide: true
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '165'
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
