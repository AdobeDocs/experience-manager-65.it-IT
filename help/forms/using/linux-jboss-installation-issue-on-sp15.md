---
title: Problema di installazione del service pack AEM Forms JEE 6.5.15.0 nell'ambiente JBoss® Linux®
description: Il service pack AEM Forms JEE 6.5.15.0 non è installato correttamente nell'ambiente JBoss® Linux®. Eventuali modifiche alle patch non vengono applicate al server dell'applicazione. Aggiungi il file 'RUP_BOM.xml' alla directory XML.
source-git-commit: 76a3a87408ceb13023737379c20fb44ce5fb180a
workflow-type: tm+mt
source-wordcount: '205'
ht-degree: 1%

---


# Problema di installazione di AEM Forms 6.5.15.0 JEE Service Pack nell’ambiente JBoss® {#aem-forms-installation-issue-environment}

## Problema   {#issue}

Il service pack AEM Forms JEE 6.5.15.0 non è installato correttamente nell&#39;ambiente JBoss® Linux®. In `PatchInstallerProcessing[1-9*].log` la voce di registro, `[AEM_Forms_JEE_DIR]/patch/AEMForms-6.5.0-0057/xml/RUP_BOM.xml not found! Assuming this component isn't in the installation. Skipping Processing`, viene registrato. Questa voce indica che l&#39;installazione del service pack AEM Forms JEE 6.5.15.0 non è riuscita.

## Si applica a {#applies-to}

Questa soluzione si applica a:
* Ambiente JBoss® Linux®

>[!NOTE]
>
> Assicurati che il service pack AEM Forms JEE 6.5.15.0 sia installato sul server dell&#39;applicazione almeno una volta prima di eseguire i passaggi di [aggiunta del file RUP_BOM.xml alla directory XML](#solution-solution).

## Soluzione {#solution}

Per risolvere il problema di installazione del service pack AEM Forms JEE 6.5.15.0, aggiungi la `RUP_BOM.xml` nella directory XML:
1. Passa alla cartella in cui è stata estratta la patch `AEMForms-6.5.0-0057_jboss_linux.tar.gz`.
1. Passa a `/CDROM_Installers/Linux/Disk1/InstData` posizione e posizione `Resource1.zip` file.
1. Copia il `Resource1.zip` in una posizione diversa all&#39;esterno della cartella estratta e decomprimere `Resource1.zip` file.
1. Passa a `/C_/builds/dev_releng/branches/rrt/aem6.5.0_rollup/tier1/install/patch/fileset_dir/xml` e copia il `RUP_BOM.xml` file.
1. Incolla il file RUP_BOM.xml in `[aem_forms_jee_installation_dir]/patch/AEMForms-6.5.0-0057/xml`.
1. Reinstalla [Service Pack di AEM Forms JEE 6.5.15.0](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html).