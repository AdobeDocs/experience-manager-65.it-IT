---
title: Filtro eliminazione contenuto
seo-title: Filtro eliminazione contenuto
description: Scoprite come utilizzare il filtro di disposizione dei contenuti per prevenire gli attacchi XSS.
seo-description: Scoprite come utilizzare il filtro di disposizione dei contenuti per prevenire gli attacchi XSS.
uuid: 145a88e0-9fa8-42db-b189-eda507c33049
contentOwner: trushton
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: Security
discoiquuid: badfaa18-472e-4777-a7dc-9c28441b38b7
translation-type: tm+mt
source-git-commit: 741ba6f6ef3270414c0ddabb1a1d02d5c436b7d9
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 0%

---


# Filtro eliminazione contenuto{#content-disposition-filter}

Il filtro di disposizione dei contenuti è una funzione di sicurezza contro gli attacchi XSS ai file SVG.

Una volta installato, il filtro blocca l’accesso a tutte le risorse. Ad esempio, non è stato possibile visualizzare un PDF online. Questa sezione descrive come configurare il filtro in base alle proprie esigenze.

## Configurare il filtro di disposizione dei contenuti {#configure-content-disposition-filter}

È possibile visualizzare il filtro di disposizione dei contenuti [Apache Sling in GitHub](https://github.com/apache/sling-org-apache-sling-security/blob/master/src/main/java/org/apache/sling/security/impl/ContentDispositionFilterConfiguration.java).

Le opzioni Filtro disposizione contenuto forniscono le seguenti funzionalità:

* Percorsi di disposizione dei contenuti: un elenco di percorsi in cui il filtro verrà applicato seguito da un elenco di mime-type da escludere su quel percorso. Questo percorso deve essere un percorso assoluto e può contenere un carattere jolly (&#39;&amp;ast;&#39;) alla fine, per corrispondere a ogni percorso di risorsa con il prefisso del percorso specificato. Ad esempio: /content/&amp;ast;:image/jpeg,image/svg+xml &quot; applicherà il filtro a tutti i nodi in /content eccetto immagini jpg e svg

* Percorsi risorsa esclusi: un elenco di risorse escluse, ogni percorso di risorsa deve essere specificato come percorso assoluto e completo. La corrispondenza del prefisso/i caratteri jolly non sono supportati.

* Abilita Per Tutti I Percorsi Delle Risorse: questo flag controlla se abilitare questo filtro per tutti i percorsi, fatta eccezione per i percorsi di risorse esclusi definiti da Percorsi risorsa esclusi. Impostando questo valore su &quot;true&quot; si ignorano i percorsi di disposizione dei contenuti. Indipendentemente dalla configurazione sono coperti solo i percorsi delle risorse che contengono una proprietà denominata &#39;jcr:data&#39; o &#39;jcr:content jcr:data&#39;.

