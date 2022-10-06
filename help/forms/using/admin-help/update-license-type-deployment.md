---
title: Aggiornare il tipo di licenza per la distribuzione
seo-title: Update the license type for the deployment
description: Aggiorna il tipo di licenza per la distribuzione utilizzando la pagina Cambia licenza nella console di amministrazione.
seo-description: Update the license type for the deployment by using the Change License page in administration console.
uuid: 0152635e-2c00-4944-b9b6-64b368589a91
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/get_started_with_administering_aem_forms_on_jee
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e4f31377-ccc9-4986-a3bf-ef2e83d12448
exl-id: 6b975aa1-9270-4098-9af5-c5cc67cb7b5d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 0%

---

# Aggiornare il tipo di licenza per la distribuzione {#update-the-license-type-for-the-deployment}

Come parte del processo di installazione dei moduli di AEM, è stato utilizzato Configuration Manager per configurare e distribuire i moduli di moduli di AEM richiesti. Per impostazione predefinita, tali moduli sono configurati con una licenza di valutazione di 60 giorni. Utilizzare la pagina Modifica licenza nella console di amministrazione per modificare il tipo di licenza per la distribuzione. I moduli attualmente distribuiti vengono visualizzati nella pagina Modifica licenza .

Nella pagina Modifica licenza sono visualizzate le informazioni sulla licenza:

* Tipo di licenza corrente
* Data e ora dell’ultimo aggiornamento della licenza
* Chi ha eseguito l’ultimo aggiornamento
* Stato attuale della licenza
* Data di installazione AEM moduli
* Data di scadenza della licenza corrente

>[!NOTE]
>
>La modifica della licenza si applica a tutti i moduli distribuiti. Prima di modificare il tipo di licenza, annullare la distribuzione dei moduli privi di licenza. Non selezionare il tipo di licenza Produzione se l’elenco dei moduli distribuiti contiene moduli diversi da quelli acquistati da Adobe.

## Aggiornare il tipo di licenza {#update-the-license-type}

1. Nella console di amministrazione, fare clic su Licenze.
1. Leggere il contratto di licenza per gli utenti finali dei moduli di AEM, selezionare Accetto se si accettano i termini del contratto, quindi fare clic su Avanti.
1. Nella pagina Modifica licenza selezionare un tipo di licenza:

   * **EVAL:** Licenza di valutazione di 60 giorni
   * **DEV:** Licenza di sviluppo permanente
   * **NFR:** Licenza di valutazione biennale
   * **IDEV:** abbonamento di 1 anno al programma Adobe Developer
   * **Produzione:** Licenza perpetua

1. Selezionare Sì, la modifica della licenza è valida per tutti i moduli distribuiti.
1. Fare clic su Conferma modifica licenza. Viene visualizzato un messaggio che indica che la licenza è stata aggiornata correttamente.
