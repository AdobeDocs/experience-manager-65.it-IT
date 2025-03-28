---
title: Ristrutturazione dell’archivio Forms nell’AEM 6.5
description: Scopri come apportare le modifiche necessarie per migrare alla nuova struttura dell’archivio in AEM 6.5 per Forms.
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
feature: Upgrading
exl-id: d555422e-dc97-4d45-9525-4299d22315e2
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '519'
ht-degree: 7%

---

# Ristrutturazione dell’archivio Forms nell’AEM 6.5{#forms-repository-restructuring-in-aem}

Come descritto nella pagina padre [Ristrutturazione dell’archivio in AEM 6.5](/help/sites-deploying/repository-restructuring.md), i clienti che eseguono l’aggiornamento a AEM 6.5 devono utilizzare questa pagina per valutare l’impegno di lavoro associato alle modifiche dell’archivio che influiscono sulla soluzione AEM Forms. Alcune modifiche richiedono un impegno di lavoro durante il processo di aggiornamento AEM 6.5, mentre altre possono essere differite fino a un aggiornamento futuro.

**Con Aggiornamento 6.5**

* [Varie](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md#misc)

**Prima dell&#39;aggiornamento futuro**

* [Configurazione Cloud Service Echosign](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md#echosign-cloud-service-configuration)
* [Configurazioni Cloud Service Recaptcha](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md#recaptcha-cloud-service-configurations)
* [Configurazioni del Cloud Service Typekit](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md#typekit-cloud-service-configurations)
* [Varie](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md#misc)

## Con aggiornamento 6.5 {#with-upgrade}

### Varie {#misc}

| **Percorso precedente** | `/etc/clientlibs/fd/fp` |
|---|---|
| **Nuova posizione** | `/libs/fd/fp/components` |
| **Linee guida per la ristrutturazione** | Eventuali riferimenti espliciti nel codice personalizzato alla posizione legacy devono essere aggiornati alla nuova posizione. |
| **Note** | Queste librerie client non devono essere modificate o estese. |

| **Percorso precedente** | `/etc/clientlibs/fd/rte` |
|---|---|
| **Nuova posizione** | `/libs/fd/rte` |
| **Linee guida per la ristrutturazione** | Per le risorse nelle librerie client a cui è possibile fare riferimento tramite percorsi assoluti, è necessario utilizzare percorsi più recenti nelle risorse nuove. |
| **Note** | N/D |

| **Percorso precedente** | `/etc/clientlibs/fd/af` |
|---|---|
| **Nuova posizione** | `/libs/fd/af/authoring/clientlibs` |
| **Linee guida per la ristrutturazione** | Per le risorse nelle librerie client a cui è possibile fare riferimento tramite percorsi assoluti, è necessario utilizzare percorsi più recenti nelle risorse nuove. |
| **Note** | N/D |

| **Percorso precedente** | `/etc/clientlibs/fd/xfaforms` |
|---|---|
| **Nuova posizione** | `/libs/fd/xfaforms/clientlibs/` |
| **Linee guida per la ristrutturazione** | Per le risorse nelle librerie client a cui è possibile fare riferimento tramite percorsi assoluti, è necessario utilizzare percorsi più recenti nelle risorse nuove. |
| **Note** | N/D |

| **Percorso precedente** | `/etc/clientlibs/fd/af` |
|---|---|
| **Nuova posizione** | `/libs/fd/af/runtime/clientlibs` |
| **Linee guida per la ristrutturazione** | Per le risorse nelle librerie client a cui è possibile fare riferimento tramite percorsi assoluti, è necessario utilizzare percorsi più recenti nelle risorse nuove. |
| **Note** | N/D |

| **Percorso precedente** | `/etc/clientlibs/fd/af` |
|---|---|
| **Nuova posizione** | `/libs/fd/af/runtime/clientlibs` |
| **Linee guida per la ristrutturazione** | Per le risorse nelle librerie client a cui è possibile fare riferimento tramite percorsi assoluti, è necessario utilizzare percorsi più recenti nelle risorse nuove. |
| **Note** | N/D |

| **Percorso precedente** | `/etc/clientlibs/fd/expeditor` |
|---|---|
| **Nuova posizione** | `/libs/fd/expeditor/clientlibs` |
| **Linee guida per la ristrutturazione** | Per le risorse nelle librerie client a cui è possibile fare riferimento tramite percorsi assoluti, è necessario utilizzare percorsi più recenti nelle risorse nuove. |
| **Note** | N/D |

| **Percorso precedente** | `/etc/clientlibs/fd/fmaddon` |
|---|---|
| **Nuova posizione** | `/libs/fd/fmaddon` |
| **Linee guida per la ristrutturazione** | La modifica di queste clientlibs non è mai stata consigliata né supportata. Se sono state apportate modifiche a queste clientlibs, è necessario eseguirne il rollback per utilizzare il codice fornito dall’AEM. |
| **Note** | N/D |

| **Percorso precedente** | `/etc/aep` |
|---|---|
| **Nuova posizione** | `/var/fd/content/annotations` |
| **Linee guida per la ristrutturazione** | La modifica di queste clientlibs non è mai stata consigliata né supportata. Se sono state apportate modifiche a queste clientlibs, è necessario eseguirne il rollback per utilizzare il codice fornito dall’AEM. |
| **Note** | N/D |

## Prima di aggiornamenti futuri {#prior-to-upgrade}

### Configurazione Cloud Service Echosign {#echosign-cloud-service-configuration}

| **Percorso precedente** | `/etc/cloudservices/echosign` |
|---|---|
| **Nuova posizione** | `/conf/<tenant>/settings/cloudconfigs/echosign` |
| **Linee guida per la ristrutturazione** | L&#39;utilità [Lazy Content Migration](/help/sites-deploying/lazy-content-migration.md) verrà attivata dall&#39;interfaccia utente di Forms Migration. |
| **Note** | N/D |

### Configurazioni Cloud Service Recaptcha {#recaptcha-cloud-service-configurations}

| **Percorso precedente** | `/etc/cloudservices/recaptcha` |
|---|---|
| **Nuova posizione** | `/conf/<tenant>/settings/cloudconfigs/recaptcha` |
| **Linee guida per la ristrutturazione** | L&#39;utilità [Lazy Content Migration](/help/sites-deploying/lazy-content-migration.md) verrà attivata dall&#39;interfaccia utente di Forms Migration. |
| **Note** | N/D |

### Configurazioni del Cloud Service Typekit {#typekit-cloud-service-configurations}

| **Percorso precedente** | `/etc/cloudservices/typekit` |
|---|---|
| **Nuova posizione** | `/conf/<tenant>/settings/cloudconfigs/typekit` |
| **Linee guida per la ristrutturazione** | L&#39;utilità [Lazy Content Migration](/help/sites-deploying/lazy-content-migration.md) verrà attivata dall&#39;interfaccia utente di Forms Migration. |
| **Note** | N/D |

### Varie {#misc-1}

| **Percorso precedente** | `/etc/cloudservices/fdm` |
|---|---|
| **Nuova posizione** | `/conf/<tenant>/settings/cloudconfigs/fdm` |
| **Linee guida per la ristrutturazione** | L&#39;utilità [Lazy Content Migration](/help/sites-deploying/lazy-content-migration.md) verrà attivata dall&#39;interfaccia utente di Forms Migration. |
| **Note** | N/D |

| **Percorso precedente** | `/etc/designs/fd/fp` |
|---|---|
| **Nuova posizione** | `/libs/fd/fp` |
| **Linee guida per la ristrutturazione** | Aggiorna eventuali riferimenti ai modelli /etc in modo che puntino alle corrispondenti `/libs`. |
| **Note** | N/D |
