---
title: Strategia di backup per il connettore per gli utenti di EMC Documentum&reg;
description: Verificare come creare una strategia di backup per Connector per gli utenti di EMC Documentum&reg;.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: b759b936-5907-4311-a5cc-60f321476368
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 0%

---

# Strategia di backup per il connettore per gli utenti di EMC Documentum® {#backup-strategy-for-connector-for-emc-documentum-users}

Se è installato il connettore per EMC Documentum®, oltre alle istruzioni riportate in questo capitolo, la strategia di backup e ripristino deve includere il backup (o il ripristino) del computer su cui è installato il sistema ECM. Consultare la documentazione di ECM Documentum®.

Eseguire il backup dell’ambiente dei moduli AEM utilizzando l’archivio ECM ed eseguendo le seguenti attività:

* Eseguire il backup dei moduli AEM seguendo le istruzioni descritte in questo documento.
* Eseguire il backup del sistema ECM Documentum® seguendo le istruzioni riportate in [Backup di EMC Documentum® Content Server](/help/forms/using/admin-help/backing-recovering-emc-documentum-repository.md#back-up-the-emc-documentum-content-server).

Ripristinare l’ambiente dei moduli AEM utilizzando l’archivio ECM ed eseguendo le seguenti attività:

* Ripristinare il rispettivo sistema ECM seguendo le istruzioni riportate in [Ripristino di EMC Documentum® Content Server](/help/forms/using/admin-help/backing-recovering-emc-documentum-repository.md#restore-the-emc-documentum-content-server).
* Ripristinare i moduli AEM seguendo le istruzioni descritte in questo documento.
