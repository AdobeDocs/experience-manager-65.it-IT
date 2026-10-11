---
title: Filtro eliminazione contenuti
description: Scopri come utilizzare il filtro di eliminazione dei contenuti per prevenire gli attacchi XSS.
contentOwner: trushton
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: Security
exl-id: 1c3d0d48-5c31-42a8-8698-922d7c2127e9
solution: Experience Manager, Experience Manager Sites
feature: Security
role: Admin
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: b1210526-416b-4ef6-bcc0-1692e99f30e9
    internal-label: Administration and security
subfeature_v2:
  - id: c35bc059-fd80-4a01-91a6-e48da3c76758
    internal-label: Security practices
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 2%
---
# Filtro eliminazione contenuti {#content-disposition-filter}

Il filtro di eliminazione dei contenuti è una funzione di sicurezza contro gli attacchi XSS sui file SVG.

Una volta installato, il filtro blocca l’accesso a tutte le risorse. Ad esempio, non è possibile visualizzare un PDF online. Questa sezione descrive come configurare il filtro in base alle tue esigenze.

## Configurare il filtro di eliminazione dei contenuti {#configure-content-disposition-filter}

Puoi visualizzare il filtro di disposizione dei contenuti [Apache Sling in GitHub](https://github.com/apache/sling-org-apache-sling-security/blob/master/src/main/java/org/apache/sling/security/impl/ContentDispositionFilterConfiguration.java).

Le opzioni del filtro di eliminazione del contenuto forniscono le seguenti funzionalità:

* **Percorsi di disposizione contenuto:** elenco di percorsi in cui viene applicato il filtro seguito da un elenco di tipi MIME da escludere nel percorso. Il percorso deve essere assoluto e può contenere un carattere jolly (`*`) alla fine, in modo che ogni percorso di risorsa corrisponda al prefisso del percorso specificato. Ad esempio: `/content/*:image/jpeg,image/svg+xml` applica il filtro a ogni nodo in `/content?` ad eccezione delle immagini JPG e SVG.

* **Percorsi risorse esclusi:** Elenco di risorse escluse. Ogni percorso di risorsa deve essere specificato come percorso assoluto e completo. I caratteri jolly/corrispondenti ai prefissi non sono supportati.

* **Abilita per tutti i percorsi delle risorse:** Questo flag controlla se abilitare il filtro per tutti i percorsi, ad eccezione dei percorsi esclusi definiti dai percorsi delle risorse esclusi. Se si imposta questo flag su &quot;true&quot;, i percorsi di disposizione del contenuto vengono ignorati. Indipendentemente dalla configurazione, vengono coperti solo i percorsi delle risorse che contengono una proprietà denominata `jcr:data` o `jcr:content/jcr:data`.
