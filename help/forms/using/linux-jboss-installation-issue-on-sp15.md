---
title: Problema di installazione del service pack AEM Forms JEE 6.5.15.0 nell’ambiente JBoss® Linux®
description: AEM Forms JEE 6.5.15.0 Service Pack non è installato correttamente nell’ambiente JBoss® Linux®. Eventuali modifiche delle patch non vengono applicate al server applicazioni. Aggiungi il file "RUP_BOM.xml" alla directory XML.
exl-id: 96ecbe58-a859-4432-a2d8-3d5dc0eaf989
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,AEM Forms on JEE
role: User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '204'
ht-degree: 1%

---

# Problema di installazione di AEM Forms 6.5.15.0 JEE Service Pack nell’ambiente JBoss® {#aem-forms-installation-issue-environment}

## Problema   {#issue}

AEM Forms JEE 6.5.15.0 Service Pack non è installato correttamente nell’ambiente JBoss® Linux®. Nel file `PatchInstallerProcessing[1-9*].log` è registrata la voce di registro `[AEM_Forms_JEE_DIR]/patch/AEMForms-6.5.0-0057/xml/RUP_BOM.xml not found! Assuming this component is not in the installation. Skipping Processing`. Questa voce indica che l’installazione del service pack di AEM Forms JEE 6.5.15.0 non è andata a buon fine.

## Applicabile a {#applies-to}

Questa soluzione si applica a:
* Ambiente JBoss® Linux®

>[!NOTE]
>
> Verificare che il Service Pack di AEM Forms JEE 6.5.15.0 sia installato almeno una volta nel server applicazioni prima di eseguire la procedura di [aggiunta del file RUP_BOM.xml alla directory XML](#solution-solution).

## Soluzione {#solution}

Per risolvere il problema di installazione di AEM Forms JEE 6.5.15.0 service pack, aggiungere il file `RUP_BOM.xml` alla directory XML:
1. Passare alla cartella in cui è stata estratta la patch `AEMForms-6.5.0-0057_jboss_linux.tar.gz`.
1. Passare alla posizione `/CDROM_Installers/Linux/Disk1/InstData` e individuare il file `Resource1.zip`.
1. Copiare il file `Resource1.zip` in una posizione diversa all&#39;esterno della cartella estratta e decomprimere il file `Resource1.zip`.
1. Passare a `/C_/builds/dev_releng/branches/rrt/aem6.5.0_rollup/tier1/install/patch/fileset_dir/xml` e copiare il file `RUP_BOM.xml`.
1. Incollare il file RUP_BOM.xml in `[aem_forms_jee_installation_dir]/patch/AEMForms-6.5.0-0057/xml`.
1. Reinstalla [AEM Forms JEE 6.5.15.0 service pack](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=it).
