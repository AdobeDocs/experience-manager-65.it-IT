---
title: Ristrutturazione dell’archivio Forms nell’AEM 6.5
seo-title: Forms Repository Restructuring in AEM 6.5
description: Scopri come apportare le modifiche necessarie per migrare alla nuova struttura dell’archivio in AEM 6.5 per Forms.
seo-description: Learn how to make the necessary changes in order to migrate to the new repository structure in AEM 6.5 for Forms.
uuid: e60830d4-23ca-4be9-941a-ee4abe4786a6
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
discoiquuid: 1ce9a622-5968-407f-a74b-d325a2bff669
feature: Upgrading
exl-id: d555422e-dc97-4d45-9525-4299d22315e2
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '532'
ht-degree: 7%

---

# Ristrutturazione dell’archivio Forms nell’AEM 6.5{#forms-repository-restructuring-in-aem}

Come descritto sull’elemento padre [Ristrutturazione dell’archivio in AEM 6.5](/help/sites-deploying/repository-restructuring.md) pagina, i clienti che eseguono l’aggiornamento a AEM 6.5 devono utilizzare questa pagina per valutare l’impegno di lavoro associato alle modifiche dell’archivio che influiscono sulla soluzione AEM Forms. Alcune modifiche richiedono un impegno di lavoro durante il processo di aggiornamento AEM 6.5, mentre altre possono essere differite fino a un aggiornamento futuro.

**Con aggiornamento 6.5**

* [Varie](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md#misc)

**Prima di un aggiornamento futuro**

* [Configurazione Cloud Service Echosign](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md#echosign-cloud-service-configuration)
* [Configurazioni Cloud Service Recaptcha](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md#recaptcha-cloud-service-configurations)
* [Configurazioni del Cloud Service Typekit](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md#typekit-cloud-service-configurations)
* [Varie](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md#misc)

## Con aggiornamento 6.5 {#with-upgrade}

### Varie {#misc}

| **Posizione precedente** | `/etc/clientlibs/fd/fp` |
|---|---|
| **Nuove posizioni** | `/libs/fd/fp/components` |
| **Orientamenti per la ristrutturazione** | Eventuali riferimenti espliciti nel codice personalizzato alla posizione legacy devono essere aggiornati alla nuova posizione. |
| **Note** | Queste librerie client non devono essere modificate o estese. |

| **Posizione precedente** | `/etc/clientlibs/fd/rte` |
|---|---|
| **Nuove posizioni** | `/libs/fd/rte` |
| **Orientamenti per la ristrutturazione** | Per le risorse nelle librerie client a cui è possibile fare riferimento tramite percorsi assoluti, è necessario utilizzare percorsi più recenti nelle risorse nuove. |
| **Note** | N/D |

| **Posizione precedente** | `/etc/clientlibs/fd/af` |
|---|---|
| **Nuove posizioni** | `/libs/fd/af/authoring/clientlibs` |
| **Orientamenti per la ristrutturazione** | Per le risorse nelle librerie client a cui è possibile fare riferimento tramite percorsi assoluti, è necessario utilizzare percorsi più recenti nelle risorse nuove. |
| **Note** | N/D |

| **Posizione precedente** | `/etc/clientlibs/fd/xfaforms` |
|---|---|
| **Nuove posizioni** | `/libs/fd/xfaforms/clientlibs/` |
| **Orientamenti per la ristrutturazione** | Per le risorse nelle librerie client a cui è possibile fare riferimento tramite percorsi assoluti, è necessario utilizzare percorsi più recenti nelle risorse nuove. |
| **Note** | N/D |

| **Posizione precedente** | `/etc/clientlibs/fd/af` |
|---|---|
| **Nuove posizioni** | `/libs/fd/af/runtime/clientlibs` |
| **Orientamenti per la ristrutturazione** | Per le risorse nelle librerie client a cui è possibile fare riferimento tramite percorsi assoluti, è necessario utilizzare percorsi più recenti nelle risorse nuove. |
| **Note** | N/D |

| **Posizione precedente** | `/etc/clientlibs/fd/af` |
|---|---|
| **Nuove posizioni** | `/libs/fd/af/runtime/clientlibs` |
| **Orientamenti per la ristrutturazione** | Per le risorse nelle librerie client a cui è possibile fare riferimento tramite percorsi assoluti, è necessario utilizzare percorsi più recenti nelle risorse nuove. |
| **Note** | N/D |

| **Posizione precedente** | `/etc/clientlibs/fd/expeditor` |
|---|---|
| **Nuove posizioni** | `/libs/fd/expeditor/clientlibs` |
| **Orientamenti per la ristrutturazione** | Per le risorse nelle librerie client a cui è possibile fare riferimento tramite percorsi assoluti, è necessario utilizzare percorsi più recenti nelle risorse nuove. |
| **Note** | N/D |

| **Posizione precedente** | `/etc/clientlibs/fd/fmaddon` |
|---|---|
| **Nuove posizioni** | `/libs/fd/fmaddon` |
| **Orientamenti per la ristrutturazione** | La modifica di queste clientlibs non è mai stata consigliata né supportata. Se sono state apportate modifiche a queste clientlibs, è necessario eseguirne il rollback per utilizzare il codice fornito dall’AEM. |
| **Note** | N/D |

| **Posizione precedente** | `/etc/aep` |
|---|---|
| **Nuove posizioni** | `/var/fd/content/annotations` |
| **Orientamenti per la ristrutturazione** | La modifica di queste clientlibs non è mai stata consigliata né supportata. Se sono state apportate modifiche a queste clientlibs, è necessario eseguirne il rollback per utilizzare il codice fornito dall’AEM. |
| **Note** | N/D |

## Prima di un aggiornamento futuro {#prior-to-upgrade}

### Configurazione Cloud Service Echosign {#echosign-cloud-service-configuration}

| **Posizione precedente** | `/etc/cloudservices/echosign` |
|---|---|
| **Nuove posizioni** | `/conf/<tenant>/settings/cloudconfigs/echosign` |
| **Orientamenti per la ristrutturazione** | Il [Migrazione dei contenuti differita](/help/sites-deploying/lazy-content-migration.md) da attivare dall&#39;interfaccia utente di Forms Migration. |
| **Note** | N/D |

### Configurazioni Cloud Service Recaptcha {#recaptcha-cloud-service-configurations}

| **Posizione precedente** | `/etc/cloudservices/recaptcha` |
|---|---|
| **Nuove posizioni** | `/conf/<tenant>/settings/cloudconfigs/recaptcha` |
| **Orientamenti per la ristrutturazione** | Il [Migrazione dei contenuti differita](/help/sites-deploying/lazy-content-migration.md) da attivare dall&#39;interfaccia utente di Forms Migration. |
| **Note** | N/D |

### Configurazioni del Cloud Service Typekit {#typekit-cloud-service-configurations}

| **Posizione precedente** | `/etc/cloudservices/typekit` |
|---|---|
| **Nuove posizioni** | `/conf/<tenant>/settings/cloudconfigs/typekit` |
| **Orientamenti per la ristrutturazione** | Il [Migrazione dei contenuti differita](/help/sites-deploying/lazy-content-migration.md) da attivare dall&#39;interfaccia utente di Forms Migration. |
| **Note** | N/D |

### Varie {#misc-1}

| **Posizione precedente** | `/etc/cloudservices/fdm` |
|---|---|
| **Nuove posizioni** | `/conf/<tenant>/settings/cloudconfigs/fdm` |
| **Orientamenti per la ristrutturazione** | Il [Migrazione dei contenuti differita](/help/sites-deploying/lazy-content-migration.md) da attivare dall&#39;interfaccia utente di Forms Migration. |
| **Note** | N/D |

| **Posizione precedente** | `/etc/designs/fd/fp` |
|---|---|
| **Nuove posizioni** | `/libs/fd/fp` |
| **Orientamenti per la ristrutturazione** | Eventuali riferimenti ai modelli /etc devono essere aggiornati per puntare ai relativi `/libs` controparti. |
| **Note** | N/D |
