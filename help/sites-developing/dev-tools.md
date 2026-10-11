---
title: Strumenti di sviluppo
description: Per sviluppare applicazioni JCR, Apache Sling o Adobe Experience Manager, sono disponibili diversi set di strumenti.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
exl-id: 97310ed5-f8fb-416c-8a66-68f652abeaa0
solution: Experience Manager, Experience Manager Sites
feature: Developing,Developer Tools
role: Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: c5d917df-d8bd-5e97-a117-6dde1e9f7103
    internal-label: Developing
  - id: f2d27a5f-0d67-4d85-8a24-86a8d8a3574b
    internal-label: Developer tools
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '394'
ht-degree: 17%
---
# Strumenti di sviluppo{#development-tools}

Per sviluppare applicazioni JCR, Apache Sling o Adobe Experience Manager (AEM), sono disponibili i seguenti set di strumenti:

* un set composto da [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md) e WebDAV. CRXDE Lite è incorporato in CRX/AEM e consente di eseguire attività di sviluppo standard nel browser. Con CRXDE Lite, puoi creare e modificare file (come .jsp e .java), cartelle, modelli, componenti, finestre di dialogo, nodi, proprietà e bundle durante la registrazione e l’integrazione con SVN.

  CRXDE Lite è consigliato quando non hai accesso diretto al server CRX/AEM, quando sviluppi un’applicazione estendendo o modificando i componenti predefiniti e i bundle Java™ o quando non hai bisogno di un debugger dedicato, del completamento del codice e dell’evidenziazione della sintassi.

* un insieme costituito dai seguenti elementi:
  * Un ambiente di sviluppo integrato. [Eclipse](/help/sites-developing/howto-projects-eclipse.md) o [IntelliJ](/help/sites-developing/ht-intellij.md).
  * Uno strumento di generazione. Ad esempio, [Apache Maven](/help/sites-developing/ht-projects-maven.md).
  * FileVault che è stato sviluppato da Adobe per mappare un archivio su un file system, un sistema di controllo della versione. Ad esempio, Subversion.
  * Un sistema di tracciamento dei bug. Per esempio, Jira.
  * Un sistema centrale di gestione delle dipendenze. Ad esempio, Apache Archiva.
  * E un sistema di automazione della build. Ad esempio, Apache Continuum.

  Questa configurazione consente di integrare completamente l’applicazione (contenuto, codice, configurazione) in qualsiasi ambiente e processo di sviluppo. Il collegamento tra i diversi elementi è la rappresentazione del file system dell’archivio tramite FileVault, in quanto tutti gli strumenti di sviluppo precedentemente menzionati possono funzionare con i file.

## Estensioni per ambienti di sviluppo integrati {#extensions-for-integrated-development-environments}

Adobe ha rilasciato le seguenti estensioni:

* [Estensione AEM Eclipse](/help/sites-developing/aem-eclipse.md)
* [Estensione AEM Brackets](/help/sites-developing/aem-brackets.md)

### Altri strumenti {#other-tools}

AEM viene fornito con altri strumenti che facilitano lo sviluppo:

* [Editor delle finestre di dialogo](/help/sites-developing/dialog-editor.md)
* [Utilizzo di Translator per gestire i dizionari](/help/sites-developing/i18n-translator.md)
* [Gestire i pacchetti con Maven](/help/sites-developing/vlt-mavenplugin.md)
* [Sviluppare progetti AEM con Eclipse](/help/sites-developing/howto-projects-eclipse.md)
* [Creare progetti AEM con Apache Maven](/help/sites-developing/ht-projects-maven.md)
* [Sviluppare progetti AEM con IntelliJ IDEA](/help/sites-developing/ht-intellij.md)
* [Utilizzare lo strumento VLT](/help/sites-developing/ht-vlttool.md)
* [Utilizzare lo strumento Server proxy](/help/sites-developing/ht-proxy-server.md)
* [Strumenti di modernizzazione AEM](/help/sites-developing/modernization-tools.md)
* [Strumenti di reporting AEM](/help/sites-developing/aem-repo-tool.md)

Strumenti che facilitano la creazione di nuovi progetti:

* [Archetipo di progetto AEM](https://github.com/adobe/aem-project-archetype)
* [Modelli AEM Lazybones](https://github.com/Adobe-Consulting-Services/lazybones-aem-templates)

>[!NOTE]
>
>Il seguente tutorial potrebbe essere utile per avviare un nuovo progetto AEM:
>[Guida introduttiva ad AEM Sites Parte 1 - Configurazione del progetto](https://helpx.adobe.com/experience-manager/kt/sites/using/getting-started-wknd-tutorial-develop/part1.html)
