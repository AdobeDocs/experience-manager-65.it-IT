---
title: Ristrutturazione dell'archivio moduli in AEM 6.5
seo-title: Ristrutturazione dell'archivio moduli in AEM 6.5
description: Scopri come apportare le modifiche necessarie per eseguire la migrazione alla nuova struttura del repository in AEM 6.5 per Forms.
seo-description: Scopri come apportare le modifiche necessarie per eseguire la migrazione alla nuova struttura del repository in AEM 6.5 per Forms.
uuid: e60830d4-23ca-4be9-941a-ee4abe4786a6
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
discoiquuid: 1ce9a622-5968-407f-a74b-d325a2bff669
translation-type: tm+mt
source-git-commit: d20ddba254c965e1b0c0fc84a482b7e89d4df5cb

---


# Ristrutturazione dell&#39;archivio moduli in AEM 6.5{#forms-repository-restructuring-in-aem}

Come descritto nella pagina Ristrutturazione del [repository padre in AEM 6.5](/help/sites-deploying/repository-restructuring.md) , i clienti che effettuano l’aggiornamento ad AEM 6.5 devono utilizzare questa pagina per valutare lo sforzo di lavoro associato alle modifiche del repository che hanno un impatto sulla soluzione AEM Forms. Alcune modifiche richiedono sforzi durante il processo di aggiornamento di AEM 6.5, mentre altre possono essere posticipate fino a un aggiornamento futuro.

**Con aggiornamento 6.5**

* [Misc](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md#misc)

**Prima dell&#39;aggiornamento futuro**

* [Configurazione del servizio Echosign Cloud](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md#echosign-cloud-service-configuration)
* [Configurazioni dei servizi Recaptcha Cloud](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md#recaptcha-cloud-service-configurations)
* [Configurazioni del servizio Typekit Cloud](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md#typekit-cloud-service-configurations)
* [Misc](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md#misc)

## Con aggiornamento 6.5 {#with-upgrade}

### Misc {#misc}

| **Posizione precedente** | `/etc/clientlibs/fd/fp` |
|---|---|
| **Nuove posizioni** | `/libs/fd/fp/components` |
| **Orientamenti per la ristrutturazione** | Eventuali riferimenti espliciti nel codice personalizzato alla posizione Legacy devono essere aggiornati alla nuova posizione. |
| **Note** | Queste librerie client non devono essere modificate o estese. |

| **Posizione precedente** | `/etc/clientlibs/fd/rte` |
|---|---|
| **Nuove posizioni** | `/libs/fd/rte` |
| **Orientamenti per la ristrutturazione** | Per le risorse nelle librerie client cui è possibile fare riferimento in percorsi assoluti, è necessario utilizzare percorsi più recenti per le risorse nuove. |
| **Note** | N/D |

| **Posizione precedente** | `/etc/clientlibs/fd/af` |
|---|---|
| **Nuove posizioni** | `/libs/fd/af/authoring/clientlibs` |
| **Orientamenti per la ristrutturazione** | Per le risorse nelle librerie client cui è possibile fare riferimento in percorsi assoluti, è necessario utilizzare percorsi più recenti per le risorse nuove. |
| **Note** | N/D |

| **Posizione precedente** | `/etc/clientlibs/fd/xfaforms` |
|---|---|
| **Nuove posizioni** | `/libs/fd/xfaforms/clientlibs/` |
| **Orientamenti per la ristrutturazione** | Per le risorse nelle librerie client cui è possibile fare riferimento in percorsi assoluti, è necessario utilizzare percorsi più recenti per le risorse nuove. |
| **Note** | N/D |

| **Posizione precedente** | `/etc/clientlibs/fd/af` |
|---|---|
| **Nuove posizioni** | `/libs/fd/af/runtime/clientlibs` |
| **Orientamenti per la ristrutturazione** | Per le risorse nelle librerie client cui è possibile fare riferimento in percorsi assoluti, è necessario utilizzare percorsi più recenti per le risorse nuove. |
| **Note** | N/D |

| **Posizione precedente** | `/etc/clientlibs/fd/af` |
|---|---|
| **Nuove posizioni** | `/libs/fd/af/runtime/clientlibs` |
| **Orientamenti per la ristrutturazione** | Per le risorse nelle librerie client cui è possibile fare riferimento in percorsi assoluti, è necessario utilizzare percorsi più recenti per le risorse nuove. |
| **Note** | N/D |

| **Posizione precedente** | `/etc/clientlibs/fd/expeditor` |
|---|---|
| **Nuove posizioni** | `/libs/fd/expeditor/clientlibs` |
| **Orientamenti per la ristrutturazione** | Per le risorse nelle librerie client cui è possibile fare riferimento in percorsi assoluti, è necessario utilizzare percorsi più recenti per le risorse nuove. |
| **Note** | N/D |

| **Posizione precedente** | `/etc/clientlibs/fd/fmaddon` |
|---|---|
| **Nuove posizioni** | `/libs/fd/fmaddon` |
| **Orientamenti per la ristrutturazione** | La modifica di questi clientlibs non è mai stata consigliata o supportata. Se sono state apportate modifiche a questi clientlibs, è necessario ripristinarli per utilizzare il codice fornito da AEM. |
| **Note** | N/D |

| **Posizione precedente** | `/etc/aep` |
|---|---|
| **Nuove posizioni** | `/var/fd/content/annotations` |
| **Orientamenti per la ristrutturazione** | La modifica di questi clientlibs non è mai stata consigliata o supportata. Se sono state apportate modifiche a questi clientlibs, è necessario ripristinarli per utilizzare il codice fornito da AEM. |
| **Note** | N/D |

## Prima dell&#39;aggiornamento futuro {#prior-to-upgrade}

### Configurazione del servizio Echosign Cloud {#echosign-cloud-service-configuration}

| **Posizione precedente** | `/etc/cloudservices/echosign` |
|---|---|
| **Nuove posizioni** | `/conf/<tenant>/settings/cloudconfigs/echosign` |
| **Orientamenti per la ristrutturazione** | L’utility di migrazione dei contenuti [pigri](/help/sites-deploying/lazy-content-migration.md) da attivare dall’interfaccia utente di migrazione di Forms. |
| **Note** | N/D |

### Configurazioni dei servizi Recaptcha Cloud {#recaptcha-cloud-service-configurations}

| **Posizione precedente** | `/etc/cloudservices/recaptcha` |
|---|---|
| **Nuove posizioni** | `/conf/<tenant>/settings/cloudconfigs/recaptcha` |
| **Orientamenti per la ristrutturazione** | L’utility di migrazione dei contenuti [pigri](/help/sites-deploying/lazy-content-migration.md) da attivare dall’interfaccia utente di migrazione di Forms. |
| **Note** | N/D |

### Configurazioni del servizio Typekit Cloud {#typekit-cloud-service-configurations}

| **Posizione precedente** | `/etc/cloudservices/typekit` |
|---|---|
| **Nuove posizioni** | `/conf/<tenant>/settings/cloudconfigs/typekit` |
| **Orientamenti per la ristrutturazione** | L’utility di migrazione dei contenuti [pigri](/help/sites-deploying/lazy-content-migration.md) da attivare dall’interfaccia utente di migrazione di Forms. |
| **Note** | N/D |

### Misc {#misc-1}

| **Posizione precedente** | `/etc/cloudservices/fdm` |
|---|---|
| **Nuove posizioni** | `/conf/<tenant>/settings/cloudconfigs/fdm` |
| **Orientamenti per la ristrutturazione** | L’utility di migrazione dei contenuti [pigri](/help/sites-deploying/lazy-content-migration.md) da attivare dall’interfaccia utente di migrazione di Forms. |
| **Note** | N/D |

| **Posizione precedente** | `/etc/designs/fd/fp` |
|---|---|
| **Nuove posizioni** | `/libs/fd/fp` |
| **Orientamenti per la ristrutturazione** | Eventuali riferimenti ai modelli /etc dovrebbero essere aggiornati in modo da indicare le `/libs` controparti. |
| **Note** | N/D |

