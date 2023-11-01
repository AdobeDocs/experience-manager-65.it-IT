---
title: "Gestione della corrispondenza: risoluzione dei problemi"
description: Scopri come gestire gli errori che si verificano durante il salvataggio di una lettera in un ambiente AEM Forms.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
feature: Correspondence Management
exl-id: cf06796b-bb8c-4a65-8f42-02fb0cfa3ebd
source-git-commit: 000c22028259eb05a61625d43526a2e8314a1d60
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 1%

---

# Gestione della corrispondenza: risoluzione dei problemi {#correspondence-management-troubleshooting}

## Errori durante il salvataggio di una lettera {#errors-when-saving-a-letter}

### Problema   {#issue}

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

### Problema   {#issue-1}

Durante l’anteprima di una lettera, l’errore &quot;Errore durante il caricamento della lettera: impossibile importare la risorsa dall’input XML&quot; viene visualizzato anche quando viene pubblicata una risorsa di testo non pubblicata in precedenza nella lettera.

### Soluzione alternativa {#workaround-1}

Reimposta la cache delle lettere sull’istanza di pubblicazione seguendo la procedura riportata di seguito, quindi prova a rivedere la lettera:

1. Vai a **`https://'[server]:[port]'/[contextPath]/system/console/configMgr`** e accedi come Amministratore.
1. Seleziona **Configurazioni gestione corrispondenza**.
1. In entrata **Configurazioni gestione corrispondenza**, disattiva **Abilita cache lettere** e quindi fare clic su **Salva.**
1. Verifica **Abilita cache lettere** e quindi fare clic su **Salva**.
1. Riprovare a visualizzare la lettera.
