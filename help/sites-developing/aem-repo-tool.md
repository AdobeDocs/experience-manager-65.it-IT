---
title: Strumenti di reporting AEM
description: AEM Repo Tool è una soluzione semplice per trasferire contenuti JCR tra il file system locale e il server AEM tramite una riga di comando paragonabile all’FTP. AEM Repo Tool è simile allo strumento Jackrabbit FileVault, ma è più veloce, ha dipendenze minime ed è un semplice script di base.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
exl-id: c46c9f0c-b0d2-4f2f-b95c-90fd3ced32a9
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
source-wordcount: '287'
ht-degree: 2%
---
# Strumenti di reporting AEM{#aem-repo-tool}

AEM Repo Tool è una soluzione semplice per trasferire contenuti JCR tra il file system locale e il server AEM tramite la riga di comando, simile all’FTP. Lo strumento AEM Repo è simile allo strumento [Jackrabbit FileVault](/help/sites-developing/ht-vlttool.md), ma è più veloce, ha dipendenze minime ed è un semplice script di base.

Questo strumento semplifica il trasferimento dei file per lo sviluppatore e può anche essere integrato in IntelliJ ed Eclipse per rendere lo sviluppo ancora più efficiente.

## Panoramica {#overview}

Per un determinato percorso all&#39;interno di una struttura filevault `jcr_root` nel file system, AEM Repo Tool crea un pacchetto con un singolo filtro per l&#39;intera sottostruttura e lo invia al server (in modo simile all&#39;FTP `put`), lo recupera dal server ( `get`) o confronta le differenze ( `status` e `diff`).

Lo strumento non supporta più percorsi di filtro o `filter.xml` di FileVault.

>[!CAUTION]
>
>AEM Repo Tool sovrascrive sempre l’intero file o la directory specificata.

## Download e documentazione {#download-and-documentation}

Lo strumento [AEM Repo Tool è disponibile su GitHub tramite questo collegamento](https://github.com/Adobe-Marketing-Cloud/tools/tree/master/repo) insieme a istruzioni dettagliate di installazione e utilizzo.

Se desideri scaricare l’origine dello strumento AEM Repo Tool, consulta il progetto GitHub collegato di seguito.

CODICE SU GITHUB

Puoi trovare il codice di questa pagina su GitHub

* [Apri progetto strumenti su GitHub](https://github.com/Adobe-Marketing-Cloud/tools)
* Scarica il progetto come [file ZIP](https://github.com/Adobe-Marketing-Cloud/tools/archive/master.zip)
