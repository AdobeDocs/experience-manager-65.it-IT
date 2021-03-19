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
feature: Gestione della corrispondenza
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 6%

---


# Gestione della corrispondenza: Risoluzione dei problemi {#correspondence-management-troubleshooting}

## Errori durante il salvataggio di una lettera {#errors-when-saving-a-letter}

### Problema {#issue}

Durante il salvataggio di una lettera viene visualizzato uno dei seguenti errori:

* Binding dei dati non presente per il modulo di testo
* Fornisci informazioni sulla proprietà necessarie per

### Motivo {#reason}

Questi errori possono verificarsi a causa di uno dei seguenti elementi:

* Un dizionario dati è associato alla lettera ma non è presente sul server.
* Un dizionario dati è associato alla lettera ma il nome contiene un carattere di sottolineatura (_).

### Soluzione alternativa {#workaround}

Assicurati che il dizionario dati che stai utilizzando nella lettera sia presente sul server e non abbia un carattere di sottolineatura (_) nel suo nome.

## Errore durante l&#39;anteprima di una lettera {#error-when-previewing-a-letter}

### Problema {#issue-1}

Durante l&#39;anteprima di una lettera, l&#39;errore &quot;Errore nel caricamento della lettera: Impossibile importare la risorsa da un input XML&quot; viene visualizzato anche quando viene pubblicata una risorsa di testo non pubblicata in precedenza nella lettera.

### Soluzione alternativa {#workaround-1}

Reimposta la cache delle lettere sull&#39;istanza di pubblicazione seguendo i passaggi seguenti, quindi riprova a visualizzare la lettera:

1. Vai a **`https://'[server]:[port]'/[contextPath]/system/console/configMgr`** e accedi come amministratore.
1. Seleziona **Configurazioni di gestione della corrispondenza**.
1. In **Configurazioni gestione corrispondenza**, disattiva **Abilita cache lettere** e quindi fai clic su **Salva.**
1. Abilita **Abilita cache lettere**, quindi fai clic su **Salva**.
1. Riprova a visualizzare la lettera.

