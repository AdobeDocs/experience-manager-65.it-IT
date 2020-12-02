---
title: '"Gestione della corrispondenza: Risoluzione dei problemi"'
seo-title: Risoluzione dei problemi di gestione della corrispondenza
description: Risoluzione dei problemi di gestione della corrispondenza
seo-description: Risoluzione dei problemi di gestione della corrispondenza
uuid: 25828cdd-110e-4a84-8f31-d82cd610a54f
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: cc473808-e71a-4834-bb30-91e6df783e60
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f
workflow-type: tm+mt
source-wordcount: '205'
ht-degree: 5%

---


# Gestione corrispondenza: Risoluzione dei problemi {#correspondence-management-troubleshooting}

## Errori durante il salvataggio della lettera {#errors-when-saving-a-letter}

### Problema {#issue}

Durante il salvataggio di una lettera viene visualizzato uno dei seguenti errori:

* Binding dei dati non presente per il modulo di testo
* Fornisci informazioni sulla proprietà necessarie per

### Motivo {#reason}

Questi errori possono verificarsi a causa di uno dei seguenti elementi:

* Un dizionario dati è associato alla lettera ma non è presente sul server.
* Un dizionario dati è associato alla lettera ma ha un carattere di sottolineatura (_) nel nome.

### Soluzione {#workaround}

Assicurarsi che il dizionario dati utilizzato nella lettera sia presente sul server e che non contenga un carattere di sottolineatura (_).

## Errore durante l&#39;anteprima di una lettera {#error-when-previewing-a-letter}

### Problema {#issue-1}

Durante l&#39;anteprima di una lettera, l&#39;errore &quot;Errore durante il caricamento della lettera: Impossibile importare la risorsa da un input XML&quot; viene visualizzato anche quando viene pubblicata una risorsa di testo non pubblicata in precedenza nella lettera.

### Soluzione {#workaround-1}

Ripristinare la cache delle lettere nell’istanza di pubblicazione seguendo la procedura seguente, quindi riprovare a visualizzare la lettera:

1. Vai a **`https://'[server]:[port]'/[contextPath]/system/console/configMgr`** ed effettua l&#39;accesso come Amministratore.
1. Selezionare **Configurazioni di gestione della corrispondenza**.
1. In **Configurazioni di gestione della corrispondenza**, disabilitare **Abilita cache lettere** e quindi fare clic su **Salva.**
1. Attivare **Abilita cache lettere**, quindi fare clic su **Salva**.
1. Riprova a visualizzare la lettera.

