---
title: Filtro di disposizione dei contenuti
seo-title: Filtro di disposizione dei contenuti
description: Scopri come utilizzare il filtro di disposizione dei contenuti per evitare attacchi XSS.
seo-description: Scopri come utilizzare il filtro di disposizione dei contenuti per evitare attacchi XSS.
uuid: 145a88e0-9fa8-42db-b189-eda507c33049
contentOwner: trushton
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: Security
discoiquuid: badfaa18-472e-4777-a7dc-9c28441b38b7
exl-id: 1c3d0d48-5c31-42a8-8698-922d7c2127e9
translation-type: tm+mt
source-git-commit: cd895fcab5adce600ce230fb6867392e45963c16
workflow-type: tm+mt
source-wordcount: '255'
ht-degree: 0%

---

# Filtro di disposizione dei contenuti {#content-disposition-filter}

Il filtro di disposizione dei contenuti è una funzione di sicurezza contro gli attacchi XSS su file SVG.

Una volta installato, il filtro blocca l’accesso a tutte le risorse. Ad esempio, non è stato possibile visualizzare un PDF online. Questa sezione descrive come configurare il filtro in base alle tue esigenze.

## Configura il filtro di disposizione dei contenuti {#configure-content-disposition-filter}

Puoi visualizzare il [filtro di disposizione dei contenuti Sling Apache in GitHub](https://github.com/apache/sling-org-apache-sling-security/blob/master/src/main/java/org/apache/sling/security/impl/ContentDispositionFilterConfiguration.java).

Le opzioni Filtro disposizione contenuto forniscono le funzionalità seguenti:

* **Percorsi di disposizione del contenuto:** un elenco di percorsi in cui il filtro verrà applicato seguito da un elenco di mime-types da escludere su quel percorso. Questo percorso deve essere un percorso assoluto e può contenere un carattere jolly (`*`) alla fine, per far corrispondere ogni percorso di risorsa con il prefisso del percorso specificato. Ad esempio: `/content/*:image/jpeg,image/svg+xml` applicherà il filtro a ogni nodo in `/content? eccetto immagini jpg e svg

* **Percorsi risorsa esclusi:** un elenco di risorse escluse, ogni percorso di risorsa deve essere indicato come percorso assoluto e completo. I caratteri jolly/corrispondenti al prefisso non sono supportati.

* **Abilita per tutti i percorsi delle risorse:** questo flag controlla se abilitare questo filtro per tutti i percorsi, ad eccezione dei percorsi esclusi definiti dai percorsi delle risorse escluse. Impostando questo valore su &quot;true&quot; si ignorano i percorsi di disposizione del contenuto. Indipendentemente dalla configurazione, vengono coperti solo i percorsi delle risorse che contengono una proprietà denominata `jcr:data` o `jcr:content/jcr:data`.
