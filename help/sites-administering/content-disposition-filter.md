---
title: Filtro eliminazione contenuti
seo-title: Content Disposition Filter
description: Scopri come utilizzare il filtro di eliminazione dei contenuti per prevenire gli attacchi XSS.
seo-description: Learn how to use the Content Disposition Filter to prevent XSS attacks.
uuid: 145a88e0-9fa8-42db-b189-eda507c33049
contentOwner: trushton
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: Security
discoiquuid: badfaa18-472e-4777-a7dc-9c28441b38b7
exl-id: 1c3d0d48-5c31-42a8-8698-922d7c2127e9
source-git-commit: d1fc2ff44378276522c2ff3208f5b3bdc4484bba
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 0%

---

# Filtro eliminazione contenuti {#content-disposition-filter}

Il filtro di disposizione del contenuto è una funzione di sicurezza contro gli attacchi XSS sui file SVG.

Una volta installato, il filtro blocca l’accesso a tutte le risorse. Non è possibile, ad esempio, visualizzare un PDF online. Questa sezione descrive come configurare il filtro in base alle tue esigenze.

## Configurare il filtro di eliminazione dei contenuti {#configure-content-disposition-filter}

È possibile visualizzare [Filtro di eliminazione dei contenuti Apache Sling in GitHub](https://github.com/apache/sling-org-apache-sling-security/blob/master/src/main/java/org/apache/sling/security/impl/ContentDispositionFilterConfiguration.java).

Le opzioni del filtro di eliminazione del contenuto forniscono le seguenti funzionalità:

* **Percorsi di disposizione contenuto:** un elenco di percorsi in cui verrà applicato il filtro seguito da un elenco di tipi mime da escludere in quel percorso. Questo percorso deve essere assoluto e può contenere un carattere jolly (`*`) alla fine, per far corrispondere ogni percorso di risorsa con il prefisso del percorso specificato. Ad esempio: `/content/*:image/jpeg,image/svg+xml` applicherà il filtro a ogni nodo in `/content?` eccetto immagini jpg e svg

* **Percorsi risorse esclusi:** un elenco delle risorse escluse, ogni percorso di risorsa deve essere fornito come percorso assoluto e completo. I caratteri jolly/corrispondenti ai prefissi non sono supportati.

* **Abilita per tutti i percorsi di risorse:** questo flag controlla se abilitare questo filtro per tutti i percorsi, ad eccezione di quelli esclusi definiti da Percorsi di risorse esclusi. Se si imposta questa opzione su &quot;true&quot;, i percorsi di disposizione del contenuto vengono ignorati. Indipendentemente dalla configurazione, vengono coperti solo i percorsi delle risorse che contengono una proprietà denominata `jcr:data` o `jcr:content/jcr:data`.
