---
title: AEM Repo Tool
seo-title: AEM Repo Tool
description: AEM Repo Tool è una soluzione semplice per trasferire il contenuto JCR tra il filesystem locale e il server AEM tramite la riga di comando paragonabile a FTP. Lo AEM Repo Tool è simile allo strumento Jackrabbit FileVault, ma è più veloce, ha dipendenze minime ed è un semplice script bash.
seo-description: The AEM Repo Tool is a simple solution to transfer JCR content between your local filesystem and the AEM server via the command line comparable to FTP. The AEM Repo Tool is similar to the Jackrabbit FileVault tool, but is faster, has minimal dependencies, and is a simple bash script.
uuid: 6c4a3504-e8e8-46c0-83cb-c18d9791f93e
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: 7de7b2f9-770e-4af3-8a31-c7b4de64fd43
exl-id: c46c9f0c-b0d2-4f2f-b95c-90fd3ced32a9
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 2%

---

# Strumento AEM repository{#aem-repo-tool}

AEM Repo Tool è una soluzione semplice per trasferire il contenuto JCR tra il filesystem locale e il server AEM tramite la riga di comando paragonabile a FTP. Lo strumento Repo AEM è simile al [Strumento Jackrabbit FileVault](/help/sites-developing/ht-vlttool.md), ma è più veloce, ha dipendenze minime ed è un semplice script bash.

Questo strumento semplifica il trasferimento di file per lo sviluppatore e può anche essere integrato in IntelliJ ed Eclipse per rendere lo sviluppo ancora più efficiente.

## Panoramica {#overview}

Per un determinato percorso all&#39;interno di un `jcr_root` struttura filevault sul filesystem, AEM Repo Tool crea un pacchetto con un singolo filtro per l&#39;intero sottoalbero e lo invia al server (simile a FTP `put`), lo recupera dal server ( `get`) o confronta le differenze ( `status` e `diff`).

Lo strumento non supporta più percorsi di filtro o FileVault `filter.xml`.

>[!CAUTION]
>
>Tieni presente che lo AEM Repo Tool sovrascrive sempre l’intero file o directory specificato.

## Download e documentazione {#download-and-documentation}

La [AEM Repo Tool è disponibile su GitHub tramite questo collegamento](https://github.com/Adobe-Marketing-Cloud/tools/tree/master/repo) oltre a istruzioni dettagliate sull&#39;installazione e sull&#39;utilizzo.

Per scaricare l’origine dello strumento Repo AEM, fai riferimento al progetto GitHub collegato di seguito.

CODICE SU GITHUB

Puoi trovare il codice di questa pagina su GitHub

* [Progetto Open tools su GitHub](https://github.com/Adobe-Marketing-Cloud/tools)
* Scarica il progetto come [un file ZIP](https://github.com/Adobe-Marketing-Cloud/tools/archive/master.zip)
