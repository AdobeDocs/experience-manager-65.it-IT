---
title: Problema di installazione del service pack AEM Forms JEE 6.5.15.0 nell’ambiente JBoss® Linux®
description: AEM Forms JEE 6.5.15.0 Service Pack non è installato correttamente nell’ambiente JBoss® Linux®. Eventuali modifiche delle patch non vengono applicate al server applicazioni. Aggiungi il file "RUP_BOM.xml" alla directory XML.
exl-id: 96ecbe58-a859-4432-a2d8-3d5dc0eaf989
source-git-commit: 9d497413d0ca72f22712581cf7eda1413eb8d643
workflow-type: tm+mt
source-wordcount: '204'
ht-degree: 1%

---

# Problema di installazione di AEM Forms 6.5.15.0 JEE Service Pack nell’ambiente JBoss® {#aem-forms-installation-issue-environment}

## Problema   {#issue}

AEM Forms JEE 6.5.15.0 Service Pack non è installato correttamente nell’ambiente JBoss® Linux®. In entrata `PatchInstallerProcessing[1-9*].log` archiviare la voce di registro, `[AEM_Forms_JEE_DIR]/patch/AEMForms-6.5.0-0057/xml/RUP_BOM.xml not found! Assuming this component is not in the installation. Skipping Processing`, è registrato. Questa voce indica che l’installazione del service pack di AEM Forms JEE 6.5.15.0 non è andata a buon fine.

## Applicabile a {#applies-to}

Questa soluzione si applica a:
* Ambiente JBoss® Linux®

>[!NOTE]
>
> Assicurati che AEM Forms JEE 6.5.15.0 Service Pack sia installato sul server applicazioni almeno una volta prima di eseguire i passaggi di [aggiunta del file RUP_BOM.xml alla directory XML](#solution-solution).

## Soluzione {#solution}

Per risolvere il problema di installazione di AEM Forms JEE 6.5.15.0 service pack, aggiungi `RUP_BOM.xml` nella directory XML:
1. Passare alla cartella in cui è stata estratta la patch `AEMForms-6.5.0-0057_jboss_linux.tar.gz`.
1. Accedi a `/CDROM_Installers/Linux/Disk1/InstData` e individuare il `Resource1.zip` file.
1. Copia il `Resource1.zip` file in una posizione diversa all&#39;esterno della cartella estratta e decomprimi `Resource1.zip` file.
1. Accedi a `/C_/builds/dev_releng/branches/rrt/aem6.5.0_rollup/tier1/install/patch/fileset_dir/xml` e copia `RUP_BOM.xml` file.
1. Incollare il file RUP_BOM.xml in `[aem_forms_jee_installation_dir]/patch/AEMForms-6.5.0-0057/xml`.
1. Reinstalla [Service Pack di AEM Forms JEE 6.5.15.0](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html).
