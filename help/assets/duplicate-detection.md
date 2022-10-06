---
title: Abilita il rilevamento delle risorse duplicate
description: Scopri come abilitare il rilevamento delle risorse duplicate in Experience Manager.
contentOwner: AG
role: User, Admin
feature: Asset Management,Asset Reports
exl-id: a403d60e-2193-4835-8f37-4a40f2d01819
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '157'
ht-degree: 0%

---

# Abilita il rilevamento delle risorse duplicate {#enable-detection-of-duplicate-assets}

Se tenti di caricare una risorsa esistente in [!DNL Adobe Experience Manager Assets], la funzione di rilevamento duplicato lo identifica come duplicato. Il rilevamento dei duplicati è disattivato per impostazione predefinita. Per abilitare la funzione, procedi come segue:

1. Apri [!DNL Experience Manager] Pagina di configurazione della console Web tramite l’accesso `https://[aem_server]:[port]/system/console/configMgr`.
1. Modificare la configurazione del servlet **[!UICONTROL Crea risorsa Day CQ DAM]**.
1. Seleziona la **[!UICONTROL rilevare]** e fai clic su **[!UICONTROL Salva]**.

   ![Seleziona l’opzione per rilevare i duplicati nel servlet](assets/chlimage_1-377.png)

   *Figura: Seleziona l’opzione per rilevare i duplicati nel servlet.*

La funzione di rilevamento duplicati è ora abilitata in [!DNL Assets]. Quando un utente tenta di caricare una risorsa esistente in [!DNL Experience Manager], il sistema verifica la presenza di un conflitto e lo indica. Le risorse vengono identificate utilizzando l’hash SHA-1 memorizzato in `jcr:content/metadata/dam:sha1`, il che significa che le risorse duplicate vengono rilevate indipendentemente dai nomi dei file.

>[!MORELIKETHIS]
>
>* [Duplicare le risorse nell’archivio esistente (un tutorial tratto da un membro della community)](https://experience-aem.blogspot.com/2019/06/aem-65-find-duplicate-assets-binaries-in-existing-repository.html)

