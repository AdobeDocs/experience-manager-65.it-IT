---
title: Aggiornamento a AEM 6.5 Forms su JEE
description: È possibile eseguire un aggiornamento diretto da Forms AEM 6.1, Forms AEM 6.2 e Forms LiveCycle ES4 SP1 a AEM 6.3.
uuid: 1435246a-9215-4d88-b52c-59a5c329bb77
content-type: reference
products: SG_EXPERIENCEMANAGER/6.3/FORMS
topic-tags: installing
geptopics: SG_AEMFORMS/categories/jee
discoiquuid: e745033f-8015-4fae-9d82-99d35802c0a6
role: Admin
exl-id: 722e75a0-bcb3-465e-bb74-ea94a3b99fd3
source-git-commit: e9f64722ba7df0a7f43aaf1005161483e04142f5
workflow-type: tm+mt
source-wordcount: '382'
ht-degree: 1%

---

# Aggiornamento a AEM 6.5 Forms su JEE {#upgrade-to-aem-forms-jee}

AEM 6.5.12.0 Forms su JEE fornisce due tipi di programmi di installazione: Programma di installazione completo e Programma di installazione patch.

**Installazione completa**: puoi utilizzare la [AEM 6.5.12.0 sul programma di installazione completo JEE](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html) per configurare nuove istanze di AEM Forms o eseguire aggiornamenti da AEM 6.3 Forms su JEE, AEM 6.4 su JEE e aggiornamento out-of-the-place da AEM 6.5.x.x Forms su JEE a AEM 6.5.12.0 Forms su JEE.

**Programma di installazione patch**: [AEM 6.5.12.0 sul programma di installazione patch JEE](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html) è per i clienti che già utilizzano le versioni 6.5.x.x di AEM. È possibile utilizzare il programma di installazione delle patch per eseguire l’aggiornamento alla versione più recente di AEM Forms.

Nella tabella seguente sono illustrati gli scenari per l&#39;utilizzo del programma di installazione completo e patch.

![Scenario del programma di installazione completo e patch](assets/full-and-patch-installer.png)

Eseguire la procedura seguente per utilizzare il programma di installazione completo per aggiornare il Forms AEM 6.3 esistente su JEE o il Forms AEM 6.4 su JEE al Forms AEM 6.5.12.0 su JEE:

1. Scarica il programma di installazione di Forms su JEE per AEM 6.5 da [Distribuzione di software](https://experience.adobe.com/#/downloads/content/software-distribution/it/aem.html). Per utilizzare il programma di installazione è necessario un contratto di manutenzione e supporto valido.
1. Consulta [Elenco di controllo per l&#39;aggiornamento e pianificazione](https://www.adobe.com/go/learn_aemforms_upgrade_checklist_65) per informazioni sui controlli da eseguire per garantire un aggiornamento corretto.
1. Consulta [Preparare l’aggiornamento ad AEM Forms](https://www.adobe.com/go/learn_aemforms_prepareupgrade_65) per scoprire ed eseguire le attività che garantiscono il corretto funzionamento dell&#39;aggiornamento con tempi di inattività minimi del server.
1. A seconda dell&#39;ambiente e del server applicazioni esistenti, scegliere uno dei seguenti documenti e seguire le istruzioni.

   * [Aggiornamento da Forms AEM 6.3 o AEM 6.4 a Forms AEM 6.5 per JBoss](https://www.adobe.com/go/learn_aemforms_upgradeJBoss_65)
   * [Aggiornamento da Forms AEM 6.3 o AEM 6.4 a Forms AEM 6.5 per WebSphere](https://www.adobe.com/go/learn_aemforms_upgradeWebSphere_65)
   * [Aggiornamento da Forms AEM 6.3 o AEM 6.4 a Forms AEM 6.5 per JBoss Turnkey](https://www.adobe.com/go/learn_aemforms_upgradeTurnkey_65)

Non è disponibile l’aggiornamento diretto dal LiveCycle ES2, dal LiveCycle ES3, dal Forms AEM 6.0, dal Forms AEM 6.1, dal Forms AEM 6.2 al AEM Forms 6.5. Puoi eseguire un aggiornamento intermedio a una o più versioni di LiveCycle o AEM Forms e quindi eseguire l’aggiornamento a AEM 6.5 Forms. Per un elenco delle versioni intermedie e delle istruzioni di aggiornamento corrispondenti, consulta [Scegli un percorso di aggiornamento](upgrade.md).
