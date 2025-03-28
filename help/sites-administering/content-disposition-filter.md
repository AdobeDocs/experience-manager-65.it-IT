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
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 0%

---

# Filtro eliminazione contenuti {#content-disposition-filter}

Il filtro di disposizione del contenuto è una funzione di sicurezza contro gli attacchi XSS sui file SVG.

Una volta installato, il filtro blocca l’accesso a tutte le risorse. Non è possibile, ad esempio, visualizzare un PDF online. Questa sezione descrive come configurare il filtro in base alle tue esigenze.

## Configurare il filtro di eliminazione dei contenuti {#configure-content-disposition-filter}

Puoi visualizzare il filtro di disposizione dei contenuti [Apache Sling in GitHub](https://github.com/apache/sling-org-apache-sling-security/blob/master/src/main/java/org/apache/sling/security/impl/ContentDispositionFilterConfiguration.java).

Le opzioni del filtro di eliminazione del contenuto forniscono le seguenti funzionalità:

* **Percorsi di disposizione contenuto:** elenco di percorsi in cui viene applicato il filtro seguito da un elenco di tipi MIME da escludere nel percorso. Il percorso deve essere assoluto e può contenere un carattere jolly (`*`) alla fine, in modo che ogni percorso di risorsa corrisponda al prefisso del percorso specificato. Ad esempio: `/content/*:image/jpeg,image/svg+xml` applica il filtro a ogni nodo in `/content?` ad eccezione delle immagini JPG e SVG.

* **Percorsi risorse esclusi:** Elenco di risorse escluse. Ogni percorso di risorsa deve essere specificato come percorso assoluto e completo. I caratteri jolly/corrispondenti ai prefissi non sono supportati.

* **Abilita per tutti i percorsi delle risorse:** Questo flag controlla se abilitare il filtro per tutti i percorsi, ad eccezione dei percorsi esclusi definiti dai percorsi delle risorse esclusi. Se si imposta questo flag su &quot;true&quot;, i percorsi di disposizione del contenuto vengono ignorati. Indipendentemente dalla configurazione, vengono coperti solo i percorsi delle risorse che contengono una proprietà denominata `jcr:data` o `jcr:content/jcr:data`.
