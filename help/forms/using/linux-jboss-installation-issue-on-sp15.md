---
title: Problema di installazione del service pack AEM Forms JEE 6.5.15.0 nell’ambiente JBoss® Linux®
description: AEM Forms JEE 6.5.15.0 Service Pack non è installato correttamente nell’ambiente JBoss® Linux®. Eventuali modifiche delle patch non vengono applicate al server applicazioni. Aggiungi il file "RUP_BOM.xml" alla directory XML.
SEO Description: AEM Forms JEE 6.5.15.0 service pack  is not installed properly on the JBoss Linux environment.
exl-id: 96ecbe58-a859-4432-a2d8-3d5dc0eaf989
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,AEM Forms on JEE
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 94663796-0ee7-58b9-84f4-b425ebb69e83
    internal-label: AEM Forms on JEE
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '212'
ht-degree: 1%
---
# Problema di installazione di AEM Forms 6.5.15.0 JEE Service Pack nell’ambiente JBoss® {#aem-forms-installation-issue-environment}

## Problema {#issue}

Il Service Pack di AEM Forms JEE 6.5.15.0 non è installato correttamente nell&#39;ambiente JBoss® Linux®. Nel file `PatchInstallerProcessing[1-9*].log` è registrata la voce di registro `[AEM_Forms_JEE_DIR]/patch/AEMForms-6.5.0-0057/xml/RUP_BOM.xml not found! Assuming this component is not in the installation. Skipping Processing`. Questa voce indica che l&#39;installazione del service pack 6.5.15.0 di AEM Forms JEE non è riuscita.

## Applicabile a {#applies-to}

Questa soluzione si applica a:
* Ambiente JBoss® Linux®

>[!NOTE]
>
> Verificare che il Service Pack di AEM Forms JEE 6.5.15.0 sia installato nel server applicazioni almeno una volta prima di eseguire la procedura di [aggiunta del file RUP_BOM.xml alla directory XML](#solution-solution).

## Soluzione {#solution}

Per risolvere il problema di installazione del service pack AEM Forms JEE 6.5.15.0, aggiungere il file `RUP_BOM.xml` alla directory XML:
1. Passare alla cartella in cui è stata estratta la patch `AEMForms-6.5.0-0057_jboss_linux.tar.gz`.
1. Passare alla posizione `/CDROM_Installers/Linux/Disk1/InstData` e individuare il file `Resource1.zip`.
1. Copiare il file `Resource1.zip` in una posizione diversa all&#39;esterno della cartella estratta e decomprimere il file `Resource1.zip`.
1. Passare a `/C_/builds/dev_releng/branches/rrt/aem6.5.0_rollup/tier1/install/patch/fileset_dir/xml` e copiare il file `RUP_BOM.xml`.
1. Incollare il file RUP_BOM.xml in `[aem_forms_jee_installation_dir]/patch/AEMForms-6.5.0-0057/xml`.
1. Reinstalla il [Service Pack &#x200B;](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html) di AEM Forms JEE 6.5.15.0.
