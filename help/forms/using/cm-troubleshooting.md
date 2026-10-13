---
title: 'Gestione della corrispondenza: risoluzione dei problemi'
description: Scopri come gestire gli errori che si verificano durante il salvataggio di una lettera in un ambiente AEM Forms.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
feature: Correspondence Management
exl-id: cf06796b-bb8c-4a65-8f42-02fb0cfa3ebd
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 3f00fc92-85ee-583e-abd1-3bc3d96de3a0
    internal-label: Correspondence Management
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 4%
---
# Gestione della corrispondenza: risoluzione dei problemi {#correspondence-management-troubleshooting}

## Errori durante il salvataggio di una lettera {#errors-when-saving-a-letter}

### Problema {#issue}

Durante il salvataggio di una lettera viene visualizzato uno dei seguenti errori:

* Associazione dati non presente per il modulo di testo
* Fornisci le informazioni sulla proprietà necessarie per:

### Motivo {#reason}

Questi errori possono verificarsi a causa di uno dei seguenti motivi:

* Un dizionario dati è associato alla lettera ma non è presente nel server.
* Un dizionario dati è associato alla lettera ma presenta un carattere di sottolineatura (_) nel nome.

### Soluzione alternativa {#workaround}

Verifica che il dizionario dati utilizzato nella lettera sia presente sul server e non contenga un carattere di sottolineatura (_) nel nome.

## Errore durante l’anteprima di una lettera {#error-when-previewing-a-letter}

### Problema {#issue-1}

Durante l’anteprima di una lettera, l’errore &quot;Errore durante il caricamento della lettera: impossibile importare la risorsa dall’input XML&quot; viene visualizzato anche quando viene pubblicata una risorsa di testo non pubblicata in precedenza nella lettera.

### Soluzione alternativa {#workaround-1}

Reimposta la cache delle lettere sull’istanza di pubblicazione seguendo la procedura riportata di seguito, quindi prova a rivedere la lettera:

1. Vai a **`https://'[server]:[port]'/[contextPath]/system/console/configMgr`** e accedi come Amministratore.
1. Seleziona **Configurazioni gestione corrispondenza**.
1. In **Configurazioni Gestione corrispondenza**, disabilitare **Abilita cache lettere** e quindi fare clic su **Salva.**
1. Selezionare **Abilita cache lettere**, quindi fare clic su **Salva**.
1. Riprovare a visualizzare la lettera.
