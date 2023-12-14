---
title: Abilita il rilevamento delle risorse duplicate
description: Scopri come abilitare il rilevamento delle risorse duplicate in Experience Manager.
contentOwner: AG
role: User, Admin
feature: Asset Management,Asset Reports
exl-id: a403d60e-2193-4835-8f37-4a40f2d01819
hide: true
source-git-commit: 477c62b857ab98d8617c7bd8ba226019d42d330d
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 0%

---

# Abilita il rilevamento delle risorse duplicate {#enable-detection-of-duplicate-assets}

Se tenti di caricare una risorsa esistente in [!DNL Adobe Experience Manager Assets], la funzione di rilevamento dei duplicati lo identifica come duplicato. Il rilevamento duplicati è disabilitato per impostazione predefinita. Per attivare la funzione, effettuare le seguenti operazioni:

1. Apri [!DNL Experience Manager] pagina di configurazione della console web accedendo a `https://[aem_server]:[port]/system/console/configMgr`.
1. Modificare la configurazione del servlet **[!UICONTROL Crea risorsa Day CQ DAM]**.
1. Seleziona la **[!UICONTROL rilevare duplicati]** e fai clic su **[!UICONTROL Salva]**.

   ![Seleziona l’opzione di rilevamento duplicati nel servlet](assets/chlimage_1-377.png)

   *Figura: Selezionare l’opzione di rilevamento duplicati nel servlet.*

La funzione di rilevamento duplicati è ora abilitata in [!DNL Assets]. Quando un utente cerca di caricare una risorsa esistente in [!DNL Experience Manager], il sistema verifica la presenza di un conflitto e lo indica. Le risorse vengono identificate utilizzando l’hash SHA-1 memorizzato in `jcr:content/metadata/dam:sha1`: le risorse duplicate vengono rilevate indipendentemente dai nomi dei file.

>[!MORELIKETHIS]
>
>* [Risorse duplicate nell’archivio esistente (un tutorial da un membro della community)](https://experience-aem.blogspot.com/2019/06/aem-65-find-duplicate-assets-binaries-in-existing-repository.html)
>* [Rilevare risorse duplicate in AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/detect-duplicate-assets.html)
