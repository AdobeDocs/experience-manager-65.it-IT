---
title: AEM Repo Tool
seo-title: AEM Repo Tool
description: AEM Repo Tool è una soluzione semplice per trasferire il contenuto JCR tra il file system locale e il server AEM tramite la riga di comando paragonabile a FTP. AEM Repo Tool è simile allo strumento Jackrabbit FileVault, ma è più veloce, ha dipendenze minime ed è un semplice script Bash.
seo-description: AEM Repo Tool è una soluzione semplice per trasferire il contenuto JCR tra il file system locale e il server AEM tramite la riga di comando paragonabile a FTP. AEM Repo Tool è simile allo strumento Jackrabbit FileVault, ma è più veloce, ha dipendenze minime ed è un semplice script Bash.
uuid: 6c4a3504-e8e8-46c0-83cb-c18d9791f93e
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: 7de7b2f9-770e-4af3-8a31-c7b4de64fd43
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# AEM Repo Tool{#aem-repo-tool}

AEM Repo Tool è una soluzione semplice per trasferire il contenuto JCR tra il file system locale e il server AEM tramite la riga di comando paragonabile a FTP. AEM Repo Tool è simile allo strumento [](/help/sites-developing/ht-vlttool.md)Jackrabbit FileVault, ma è più veloce, ha dipendenze minime ed è un semplice script Bash.

Questo strumento semplifica il trasferimento di file per lo sviluppatore e può essere integrato in IntelliJ ed Eclipse per rendere lo sviluppo ancora più efficiente.

## Panoramica {#overview}

Per un determinato percorso all&#39;interno di una struttura di `jcr_root` file system del file system, AEM Repo Tool crea un pacchetto con un singolo filtro per l&#39;intero sottoalbero e lo invia al server (simile all&#39;FTP `put`), lo recupera dal server ( `get`) o confronta le differenze ( `status` e `diff`).

Lo strumento non supporta più percorsi di filtro o FileVault `filter.xml`.

>[!CAUTION]
>
>Lo strumento AEM Repo sovrascriverà sempre l&#39;intero file o directory specificato.

## Download e documentazione {#download-and-documentation}

Lo strumento [AEM Repo Tool è disponibile su GitHub tramite questo collegamento](https://github.com/Adobe-Marketing-Cloud/tools/tree/master/repo) , oltre a istruzioni dettagliate sull&#39;installazione e l&#39;utilizzo.

Se desiderate scaricare l’origine di AEM Repo Tool, fate riferimento al progetto GitHub collegato di seguito.

CODICE SU GITHUB

Puoi trovare il codice di questa pagina su GitHub

* [Open tools project on GitHub](https://github.com/Adobe-Marketing-Cloud/tools)
* Scarica il progetto come [file ZIP](https://github.com/Adobe-Marketing-Cloud/tools/archive/master.zip)

