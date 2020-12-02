---
title: Strumenti di sviluppo
seo-title: Strumenti di sviluppo
description: Per sviluppare le applicazioni JCR, Apache Sling o AEM, sono disponibili diversi set di strumenti
seo-description: Per sviluppare le applicazioni JCR, Apache Sling o AEM, sono disponibili diversi set di strumenti
uuid: 1bee3a52-5d76-4b0c-a222-a02e12ff3a43
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: 76c570e5-46ed-46be-9864-4fe4a83f0caf
translation-type: tm+mt
source-git-commit: c13eabdf4938a47ddf64d55b00f845199591b835
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 2%

---


# Strumenti di sviluppo{#development-tools}

Per sviluppare le applicazioni JCR, Apache Sling o AEM, sono disponibili i seguenti set di strumenti:

* un set costituito da [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md) e WebDAV. CRXDE Lite è integrato in CRX/AEM e consente di eseguire attività di sviluppo standard nel browser. Con i CRXDE Lite, potete creare e modificare file (come .jsp e .java), cartelle, modelli, componenti, finestre di dialogo, nodi, proprietà e bundle durante la registrazione e l’integrazione con SVN.

   CRXDE Lite è consigliato quando non si dispone dell&#39;accesso diretto al server CRX/AEM, quando si sviluppa un&#39;applicazione estendendo o modificando i componenti out-of-the-box e i bundle Java o quando non è necessario un debugger dedicato, completamento del codice e evidenziazione della sintassi.

* un set costituito da un ambiente di sviluppo integrato (ad esempio: [Eclipse](/help/sites-developing/howto-projects-eclipse.md) o [IntelliJ](/help/sites-developing/ht-intellij.md)), uno strumento di compilazione (ad esempio: [Apache Maven](/help/sites-developing/ht-projects-maven.md)), FileVault sviluppato da  Adobe per mappare un repository su un file system, un sistema di controllo delle versioni (ad esempio: Subversion), un sistema di tracciamento dei bug (ad esempio: Jira), un sistema centrale di gestione delle dipendenze (ad esempio: Apache Archiva e un sistema di automazione di compilazione (ad esempio: Apache Continuum).

   Questa configurazione consente di integrare completamente l&#39;applicazione (contenuto, codice, configurazione) in qualsiasi ambiente e processo di sviluppo.Il collegamento tra i diversi elementi è la rappresentazione del file system del repository tramite FileVault, in quanto tutti i suddetti strumenti di sviluppo possono funzionare con i file.

## Estensioni per ambienti di sviluppo integrati {#extensions-for-integrated-development-environments}

 Adobe ha rilasciato le seguenti estensioni:

* [Estensione AEM Eclipse](/help/sites-developing/aem-eclipse.md)
* [Estensione AEM parentesi](/help/sites-developing/aem-brackets.md)
* [AEM estensione](https://github.com/headwirecom/aem-ide-tooling-4-intellij/blob/master/documenation/AEM%20Tooling%20Plugin%20for%20IntelliJ%20IDEA.pdf)  IntelliJ (da Headwire)

### Altri strumenti {#other-tools}

AEM navi con altri strumenti che agevolano lo sviluppo:

* [Editor finestre di dialogo](/help/sites-developing/dialog-editor.md)
* [Utilizzo di Translator per gestire i dizionari](/help/sites-developing/i18n-translator.md)
* [Gestione dei pacchetti con il cielo](/help/sites-developing/vlt-mavenplugin.md)
* [Come sviluppare AEM progetti con Eclipse](/help/sites-developing/howto-projects-eclipse.md)
* [Come creare AEM progetti con Apache Maven](/help/sites-developing/ht-projects-maven.md)
* [Come sviluppare progetti AEM utilizzando IntelliJ IDEA](/help/sites-developing/ht-intellij.md)
* [Come utilizzare lo strumento VLT](/help/sites-developing/ht-vlttool.md)
* [Come utilizzare lo strumento Proxy Server](/help/sites-developing/ht-proxy-server.md)
* [Strumento di conversione finestra di dialogo](/help/sites-developing/dialog-conversion.md)
* [AEM Repo Tool](/help/sites-developing/aem-repo-tool.md)

Strumenti che agevolano la creazione di nuovi progetti:

* [AEM Project Archetype](https://github.com/Adobe-Marketing-Cloud/aem-project-archetype)
* [Modelli AEM Lazybones](https://github.com/Adobe-Consulting-Services/lazybones-aem-templates)

>[!NOTE]
>
>L&#39;esercitazione seguente potrebbe interessare l&#39;avvio di un nuovo progetto AEM:
>[Guida introduttiva  AEM Sites Part 1 - Project Setup](https://helpx.adobe.com/experience-manager/kt/sites/using/getting-started-wknd-tutorial-develop/part1.html)

