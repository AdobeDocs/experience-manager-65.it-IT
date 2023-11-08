---
title: AEM Repo Tool
description: AEM Repo Tool è una soluzione semplice per trasferire contenuti JCR tra il file system locale e il server AEM tramite una riga di comando paragonabile all’FTP. Lo strumento AEM Repo è simile allo strumento Jackrabbit FileVault, ma è più veloce, ha dipendenze minime ed è un semplice script di base.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
exl-id: c46c9f0c-b0d2-4f2f-b95c-90fd3ced32a9
source-git-commit: 38f0496d9340fbcf383a2d39dba8efcbdcd20c6f
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 2%

---

# AEM Repo Tool{#aem-repo-tool}

AEM Repo Tool è una soluzione semplice per trasferire contenuti JCR tra il file system locale e il server AEM tramite la riga di comando, simile all’FTP. Lo strumento AEM Repo è simile al [Strumento FileVault Jackrabbit](/help/sites-developing/ht-vlttool.md), ma è più veloce, ha dipendenze minime ed è un semplice script di base.

Questo strumento semplifica il trasferimento dei file per lo sviluppatore e può anche essere integrato in IntelliJ ed Eclipse per rendere lo sviluppo ancora più efficiente.

## Panoramica {#overview}

Per un determinato percorso all’interno di un `jcr_root` struttura filevault sul filesystem, AEM Repo Tool crea un pacchetto con un singolo filtro per l’intera sottostruttura e lo invia al server (simile a FTP `put`), lo recupera dal server ( `get`) o confronta le differenze ( `status` e `diff`).

Lo strumento non supporta più percorsi di filtro o i `filter.xml`.

>[!CAUTION]
>
>Lo strumento AEM Repo Tool sovrascrive sempre l’intero file o la directory specificata.

## Download e documentazione {#download-and-documentation}

Il [Lo strumento AEM Repo è disponibile su GitHub tramite questo collegamento](https://github.com/Adobe-Marketing-Cloud/tools/tree/master/repo) insieme a istruzioni dettagliate per l&#39;installazione e l&#39;utilizzo.

Se desideri scaricare l’origine dello strumento AEM Repo Tool, consulta il progetto GitHub collegato di seguito.

CODICE SU GITHUB

Puoi trovare il codice di questa pagina su GitHub

* [Apri progetto strumenti su GitHub](https://github.com/Adobe-Marketing-Cloud/tools)
* Scarica il progetto come [un file ZIP](https://github.com/Adobe-Marketing-Cloud/tools/archive/master.zip)
