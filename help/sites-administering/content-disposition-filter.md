---
title: Filtro eliminazione contenuti
description: Scopri come utilizzare il filtro di eliminazione dei contenuti per prevenire gli attacchi XSS.
contentOwner: trushton
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: Security
exl-id: 1c3d0d48-5c31-42a8-8698-922d7c2127e9
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 0%

---

# Filtro eliminazione contenuti {#content-disposition-filter}

Il filtro di disposizione del contenuto è una funzione di sicurezza contro gli attacchi XSS sui file SVG.

Una volta installato, il filtro blocca l’accesso a tutte le risorse. Non è possibile, ad esempio, visualizzare un PDF online. Questa sezione descrive come configurare il filtro in base alle tue esigenze.

## Configurare il filtro di eliminazione dei contenuti {#configure-content-disposition-filter}

È possibile visualizzare [Filtro di eliminazione dei contenuti Apache Sling in GitHub](https://github.com/apache/sling-org-apache-sling-security/blob/master/src/main/java/org/apache/sling/security/impl/ContentDispositionFilterConfiguration.java).

Le opzioni del filtro di eliminazione del contenuto forniscono le seguenti funzionalità:

* **Percorsi di disposizione contenuto:** Un elenco di percorsi in cui viene applicato il filtro seguito da un elenco di tipi mime da escludere su quel percorso. Il percorso deve essere assoluto e può contenere un carattere jolly (`*`) alla fine, per far corrispondere ogni percorso di risorsa con il prefisso del percorso specificato. Ad esempio: `/content/*:image/jpeg,image/svg+xml` applica il filtro a ogni nodo in `/content?` ad eccezione delle immagini JPG e SVG.

* **Percorsi risorse esclusi:** Un elenco delle risorse escluse; ogni percorso di risorsa deve essere fornito come percorso assoluto e completo. I caratteri jolly/corrispondenti ai prefissi non sono supportati.

* **Abilita per tutti i percorsi di risorse:** Questo flag controlla se abilitare questo filtro per tutti i percorsi, ad eccezione di quelli esclusi definiti da Percorsi di risorse esclusi. Se si imposta questo flag su &quot;true&quot;, i percorsi di disposizione del contenuto vengono ignorati. Indipendentemente dalla configurazione, vengono coperti solo i percorsi delle risorse che contengono una proprietà denominata `jcr:data` o `jcr:content/jcr:data`.
