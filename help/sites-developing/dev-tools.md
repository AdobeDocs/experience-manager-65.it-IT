---
title: Strumenti di sviluppo
seo-title: Development Tools
description: Per sviluppare le applicazioni JCR, Apache Sling o AEM, sono disponibili diversi set di strumenti
seo-description: To develop your JCR, Apache Sling or AEM applications, a number of tool sets are available
uuid: 1bee3a52-5d76-4b0c-a222-a02e12ff3a43
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: 76c570e5-46ed-46be-9864-4fe4a83f0caf
exl-id: 97310ed5-f8fb-416c-8a66-68f652abeaa0
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 3%

---

# Strumenti di sviluppo{#development-tools}

Per sviluppare le applicazioni JCR, Apache Sling o AEM, sono disponibili i seguenti set di strumenti:

* un set costituito da [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md) e WebDAV. CRXDE Lite è incorporato in CRX/AEM e consente di eseguire attività di sviluppo standard nel browser. Con CRXDE Lite è possibile creare e modificare file (come .jsp e .java), cartelle, modelli, componenti, finestre di dialogo, nodi, proprietà e bundle durante la registrazione e l’integrazione con SVN.

   CRXDE Lite è consigliato quando non si dispone dell’accesso diretto al server CRX/AEM, quando si sviluppa un’applicazione estendendo o modificando i componenti predefiniti e i bundle Java o quando non è necessario un debugger dedicato, il completamento del codice e l’evidenziazione della sintassi.

* un insieme costituito da un ambiente di sviluppo integrato (ad esempio: [Eclipse](/help/sites-developing/howto-projects-eclipse.md) o [IntelliJ](/help/sites-developing/ht-intellij.md)), uno strumento di creazione (ad esempio: [Apache Maven](/help/sites-developing/ht-projects-maven.md)), FileVault che è stato sviluppato da Adobe per mappare un archivio su un file system, un sistema di controllo delle versioni (ad esempio: Subversion), un sistema di tracciamento dei bug (per esempio: Jira), un sistema centrale di gestione delle dipendenze (ad esempio: Apache Archiva) e un sistema di automazione per la creazione (ad esempio: Apache Continuum).

   Questa configurazione consente di integrare completamente l&#39;applicazione (contenuto, codice, configurazione) in qualsiasi ambiente e processo di sviluppo.Il collegamento tra i diversi elementi è la rappresentazione del file system dell&#39;archivio tramite FileVault, in quanto tutti i suddetti strumenti di sviluppo possono funzionare con i file.

## Estensioni per ambienti di sviluppo integrati {#extensions-for-integrated-development-environments}

Adobe rilasciato le seguenti estensioni:

* [Estensione AEM Eclipse](/help/sites-developing/aem-eclipse.md)
* [Estensione Bracket AEM](/help/sites-developing/aem-brackets.md)
* [Estensione AEM IntelliJ](https://github.com/headwirecom/aem-ide-tooling-4-intellij/blob/master/documenation/AEM%20Tooling%20Plugin%20for%20IntelliJ%20IDEA.pdf) (da Headwire)

### Altri strumenti {#other-tools}

AEM navi con altri strumenti che facilitano lo sviluppo:

* [Editor finestre di dialogo](/help/sites-developing/dialog-editor.md)
* [Utilizzo di Translator per gestire i dizionari](/help/sites-developing/i18n-translator.md)
* [Gestione dei pacchetti con Maven](/help/sites-developing/vlt-mavenplugin.md)
* [Come sviluppare progetti AEM utilizzando Eclipse](/help/sites-developing/howto-projects-eclipse.md)
* [Come creare progetti AEM utilizzando Apache Maven](/help/sites-developing/ht-projects-maven.md)
* [Come sviluppare progetti AEM utilizzando IntelliJ IDEA](/help/sites-developing/ht-intellij.md)
* [Come utilizzare lo strumento VLT](/help/sites-developing/ht-vlttool.md)
* [Come utilizzare lo strumento Proxy Server](/help/sites-developing/ht-proxy-server.md)
* [Strumenti AEM Modernization Tools](/help/sites-developing/modernization-tools.md)
* [AEM Repo Tool](/help/sites-developing/aem-repo-tool.md)

Strumenti che facilitano la creazione di nuovi progetti:

* [AEM Project Archetype](https://github.com/Adobe-Marketing-Cloud/aem-project-archetype)
* [Modelli AEM Lazybones](https://github.com/Adobe-Consulting-Services/lazybones-aem-templates)

>[!NOTE]
>
>L’esercitazione seguente potrebbe interessare l’avvio di un nuovo progetto AEM:
>[Guida introduttiva ad AEM Sites Parte 1 - Configurazione del progetto](https://helpx.adobe.com/experience-manager/kt/sites/using/getting-started-wknd-tutorial-develop/part1.html)
