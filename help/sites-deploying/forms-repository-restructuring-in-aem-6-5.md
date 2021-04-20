---
title: Ristrutturazione dell'archivio Forms in AEM 6.5
seo-title: Ristrutturazione dell'archivio Forms in AEM 6.5
description: Scopri come apportare le modifiche necessarie per migrare alla nuova struttura dell’archivio in AEM 6.5 per Forms.
seo-description: Scopri come apportare le modifiche necessarie per migrare alla nuova struttura dell’archivio in AEM 6.5 per Forms.
uuid: e60830d4-23ca-4be9-941a-ee4abe4786a6
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
discoiquuid: 1ce9a622-5968-407f-a74b-d325a2bff669
feature: Upgrading
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '558'
ht-degree: 7%

---


# Ristrutturazione dell&#39;archivio Forms in AEM 6.5{#forms-repository-restructuring-in-aem}

Come descritto nella pagina padre [Ristrutturazione archivio AEM 6.5](/help/sites-deploying/repository-restructuring.md) , i clienti che eseguono l’aggiornamento a AEM 6.5 devono utilizzare questa pagina per valutare lo sforzo di lavoro associato alle modifiche dell’archivio che influiscono sulla soluzione AEM Forms. Alcune modifiche richiedono un lavoro durante il processo di aggiornamento di AEM 6.5, mentre altre possono essere differite fino a un aggiornamento futuro.

**Con aggiornamento alla versione 6.5**

* [Varie](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md#misc)

**Prima dell’aggiornamento futuro**

* [Configurazione Cloud Service Echosign](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md#echosign-cloud-service-configuration)
* [Configurazioni del Cloud Service Recaptcha](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md#recaptcha-cloud-service-configurations)
* [Configurazioni del Cloud Service Typekit](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md#typekit-cloud-service-configurations)
* [Varie](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md#misc)

## Aggiornamento 6.5 {#with-upgrade}

### Varie {#misc}

| **Posizione precedente** | `/etc/clientlibs/fd/fp` |
|---|---|
| **Nuove posizioni** | `/libs/fd/fp/components` |
| **Orientamento alla ristrutturazione** | Eventuali riferimenti espliciti nel codice personalizzato alla posizione legacy devono essere aggiornati nella nuova posizione. |
| **Note** | Queste librerie client non devono essere modificate o estese. |

| **Posizione precedente** | `/etc/clientlibs/fd/rte` |
|---|---|
| **Nuove posizioni** | `/libs/fd/rte` |
| **Orientamento alla ristrutturazione** | Per le risorse nelle librerie client a cui è possibile fare riferimento tramite percorsi assoluti, è necessario utilizzare percorsi più recenti nelle nuove risorse. |
| **Note** | N/D |

| **Posizione precedente** | `/etc/clientlibs/fd/af` |
|---|---|
| **Nuove posizioni** | `/libs/fd/af/authoring/clientlibs` |
| **Orientamento alla ristrutturazione** | Per le risorse nelle librerie client a cui è possibile fare riferimento tramite percorsi assoluti, è necessario utilizzare percorsi più recenti nelle nuove risorse. |
| **Note** | N/D |

| **Posizione precedente** | `/etc/clientlibs/fd/xfaforms` |
|---|---|
| **Nuove posizioni** | `/libs/fd/xfaforms/clientlibs/` |
| **Orientamento alla ristrutturazione** | Per le risorse nelle librerie client a cui è possibile fare riferimento tramite percorsi assoluti, è necessario utilizzare percorsi più recenti nelle nuove risorse. |
| **Note** | N/D |

| **Posizione precedente** | `/etc/clientlibs/fd/af` |
|---|---|
| **Nuove posizioni** | `/libs/fd/af/runtime/clientlibs` |
| **Orientamento alla ristrutturazione** | Per le risorse nelle librerie client a cui è possibile fare riferimento tramite percorsi assoluti, è necessario utilizzare percorsi più recenti nelle nuove risorse. |
| **Note** | N/D |

| **Posizione precedente** | `/etc/clientlibs/fd/af` |
|---|---|
| **Nuove posizioni** | `/libs/fd/af/runtime/clientlibs` |
| **Orientamento alla ristrutturazione** | Per le risorse nelle librerie client a cui è possibile fare riferimento tramite percorsi assoluti, è necessario utilizzare percorsi più recenti nelle nuove risorse. |
| **Note** | N/D |

| **Posizione precedente** | `/etc/clientlibs/fd/expeditor` |
|---|---|
| **Nuove posizioni** | `/libs/fd/expeditor/clientlibs` |
| **Orientamento alla ristrutturazione** | Per le risorse nelle librerie client a cui è possibile fare riferimento tramite percorsi assoluti, è necessario utilizzare percorsi più recenti nelle nuove risorse. |
| **Note** | N/D |

| **Posizione precedente** | `/etc/clientlibs/fd/fmaddon` |
|---|---|
| **Nuove posizioni** | `/libs/fd/fmaddon` |
| **Orientamento alla ristrutturazione** | La modifica di queste clientlib non è mai stata consigliata o supportata. Se sono state apportate modifiche a queste clientlibs, è necessario eseguirne il rollback per utilizzare il codice fornito da AEM. |
| **Note** | N/D |

| **Posizione precedente** | `/etc/aep` |
|---|---|
| **Nuove posizioni** | `/var/fd/content/annotations` |
| **Orientamento alla ristrutturazione** | La modifica di queste clientlib non è mai stata consigliata o supportata. Se sono state apportate modifiche a queste clientlibs, è necessario eseguirne il rollback per utilizzare il codice fornito da AEM. |
| **Note** | N/D |

## Aggiornamento precedente a {#prior-to-upgrade}

### Configurazione del Cloud Service Echosign {#echosign-cloud-service-configuration}

| **Posizione precedente** | `/etc/cloudservices/echosign` |
|---|---|
| **Nuove posizioni** | `/conf/<tenant>/settings/cloudconfigs/echosign` |
| **Orientamento alla ristrutturazione** | L&#39;utility [Lazy Content Migration](/help/sites-deploying/lazy-content-migration.md) da attivare dall&#39;interfaccia utente di migrazione Forms. |
| **Note** | N/D |

### Configurazioni di Cloud Service Recaptcha {#recaptcha-cloud-service-configurations}

| **Posizione precedente** | `/etc/cloudservices/recaptcha` |
|---|---|
| **Nuove posizioni** | `/conf/<tenant>/settings/cloudconfigs/recaptcha` |
| **Orientamento alla ristrutturazione** | L&#39;utility [Lazy Content Migration](/help/sites-deploying/lazy-content-migration.md) da attivare dall&#39;interfaccia utente di migrazione Forms. |
| **Note** | N/D |

### Configurazioni Cloud Service Typekit {#typekit-cloud-service-configurations}

| **Posizione precedente** | `/etc/cloudservices/typekit` |
|---|---|
| **Nuove posizioni** | `/conf/<tenant>/settings/cloudconfigs/typekit` |
| **Orientamento alla ristrutturazione** | L&#39;utility [Lazy Content Migration](/help/sites-deploying/lazy-content-migration.md) da attivare dall&#39;interfaccia utente di migrazione Forms. |
| **Note** | N/D |

### Varie {#misc-1}

| **Posizione precedente** | `/etc/cloudservices/fdm` |
|---|---|
| **Nuove posizioni** | `/conf/<tenant>/settings/cloudconfigs/fdm` |
| **Orientamento alla ristrutturazione** | L&#39;utility [Lazy Content Migration](/help/sites-deploying/lazy-content-migration.md) da attivare dall&#39;interfaccia utente di migrazione Forms. |
| **Note** | N/D |

| **Posizione precedente** | `/etc/designs/fd/fp` |
|---|---|
| **Nuove posizioni** | `/libs/fd/fp` |
| **Orientamento alla ristrutturazione** | Eventuali riferimenti ai modelli /etc devono essere aggiornati in modo da puntare alle loro controparti `/libs`. |
| **Note** | N/D |

