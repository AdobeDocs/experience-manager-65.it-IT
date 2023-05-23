---
title: Strumenti di sviluppo
seo-title: Development Tools
description: Per sviluppare applicazioni JCR, Apache Sling o AEM, sono disponibili diversi set di strumenti
seo-description: To develop your JCR, Apache Sling or AEM applications, a number of tool sets are available
uuid: 1bee3a52-5d76-4b0c-a222-a02e12ff3a43
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: 76c570e5-46ed-46be-9864-4fe4a83f0caf
exl-id: 97310ed5-f8fb-416c-8a66-68f652abeaa0
source-git-commit: 4967a6d9ad92272a1ff442456fe65de51cc46a73
workflow-type: tm+mt
source-wordcount: '373'
ht-degree: 3%

---

# Strumenti di sviluppo{#development-tools}

Per sviluppare applicazioni JCR, Apache Sling o AEM, sono disponibili i seguenti set di strumenti:

* un set costituito da [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md) e WebDAV. CRXDE Lite è incorporato in CRX/AEM e consente di eseguire attività di sviluppo standard nel browser. Con CRXDE Lite puoi creare e modificare file (come .jsp e .java), cartelle, modelli, componenti, finestre di dialogo, nodi, proprietà e bundle durante la registrazione e l’integrazione con SVN.

   CRXDE Lite è consigliato quando non hai accesso diretto al server CRX/AEM, quando sviluppi un’applicazione estendendo o modificando i componenti predefiniti e i bundle Java o quando non hai bisogno di un debugger dedicato, del completamento del codice e dell’evidenziazione della sintassi.

* un set costituito da un ambiente di sviluppo integrato (ad esempio: [Eclipse](/help/sites-developing/howto-projects-eclipse.md) o [IntelliJ](/help/sites-developing/ht-intellij.md)), uno strumento di generazione (ad esempio: [Apache Maven](/help/sites-developing/ht-projects-maven.md)), FileVault che è stato sviluppato da Adobe per mappare un archivio su un file system, un sistema di controllo della versione (ad esempio: Subversion), un sistema di tracciamento dei bug (ad esempio: Jira), un sistema di gestione delle dipendenze centrale (ad esempio: Apache Archiva) e un sistema di automazione della build (ad esempio: Apache Continuum).

   Questa configurazione consente di integrare completamente l&#39;applicazione (contenuto, codice, configurazione) in qualsiasi ambiente e processo di sviluppo.Il collegamento tra i diversi elementi è la rappresentazione del file system dell&#39;archivio tramite FileVault, in quanto tutti gli strumenti di sviluppo sopra menzionati possono funzionare con i file.

## Estensioni per ambienti di sviluppo integrati {#extensions-for-integrated-development-environments}

L’Adobe ha rilasciato le seguenti estensioni:

* [Estensione AEM Eclipse](/help/sites-developing/aem-eclipse.md)
* [Estensione parentesi AEM](/help/sites-developing/aem-brackets.md)

### Altri strumenti {#other-tools}

L&#39;AEM viene fornito con altri strumenti che facilitano lo sviluppo:

* [Editor finestre di dialogo](/help/sites-developing/dialog-editor.md)
* [Utilizzo di Translator per gestire i dizionari](/help/sites-developing/i18n-translator.md)
* [Gestione dei pacchetti tramite Maven](/help/sites-developing/vlt-mavenplugin.md)
* [Come sviluppare progetti AEM utilizzando Eclipse](/help/sites-developing/howto-projects-eclipse.md)
* [Come creare progetti AEM con Apache Maven](/help/sites-developing/ht-projects-maven.md)
* [Come sviluppare progetti AEM utilizzando IntelliJ IDEA](/help/sites-developing/ht-intellij.md)
* [Come utilizzare lo strumento VLT](/help/sites-developing/ht-vlttool.md)
* [Come utilizzare lo strumento Server proxy](/help/sites-developing/ht-proxy-server.md)
* [Strumenti AEM Modernization Tools](/help/sites-developing/modernization-tools.md)
* [AEM Repo Tool](/help/sites-developing/aem-repo-tool.md)

Strumenti che facilitano la creazione di nuovi progetti:

* [AEM Project Archetype](https://github.com/Adobe-Marketing-Cloud/aem-project-archetype)
* [Modelli Lazybones AEM](https://github.com/Adobe-Consulting-Services/lazybones-aem-templates)

>[!NOTE]
>
>Il seguente tutorial potrebbe essere utile per avviare un nuovo progetto AEM:
>[Guida introduttiva ad AEM Sites Parte 1 - Configurazione del progetto](https://helpx.adobe.com/experience-manager/kt/sites/using/getting-started-wknd-tutorial-develop/part1.html)
