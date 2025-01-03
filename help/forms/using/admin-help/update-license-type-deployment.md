---
title: Aggiornare il tipo di licenza per la distribuzione
description: Aggiorna il tipo di licenza per la distribuzione utilizzando la pagina Modifica licenza nella console di amministrazione.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/get_started_with_administering_aem_forms_on_jee
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 6b975aa1-9270-4098-9af5-c5cc67cb7b5d
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 0%

---

# Aggiornare il tipo di licenza per la distribuzione {#update-the-license-type-for-the-deployment}

>[!NOTE]
> 
> Assicurati che l’utente disponga dei privilegi di amministratore per accedere alla console dell’amministratore.

Come parte del processo di installazione dei moduli AEM, hai utilizzato Configuration Manager per configurare e distribuire i moduli dei moduli AEM necessari. Per impostazione predefinita, tali moduli sono configurati con una licenza di valutazione di 60 giorni. Utilizzare la pagina Modifica licenza nella console di amministrazione per modificare il tipo di licenza per la distribuzione. I moduli attualmente distribuiti vengono visualizzati nella pagina Modifica licenza.

Nella pagina Modifica licenza vengono visualizzate le informazioni sulla licenza:

* Tipo di licenza corrente
* Data e ora dell&#39;ultimo aggiornamento della licenza
* Chi ha eseguito l’ultimo aggiornamento
* Stato corrente della licenza
* Data di installazione dei moduli AEM
* Data di scadenza della licenza corrente

>[!NOTE]
>
>La modifica della licenza si applica a tutti i moduli distribuiti. Prima di modificare il tipo di licenza, annullare la distribuzione dei moduli non concessi in licenza. Non selezionare il tipo di licenza Produzione se l’elenco dei moduli distribuiti contiene moduli diversi da quelli acquistati da Adobe.

## Aggiornare il tipo di licenza {#update-the-license-type}

1. Nella console di amministrazione, fare clic su Gestione licenze.
1. Leggere il contratto di licenza con l&#39;utente finale del modulo AEM, selezionare Accetto se si accettano i termini del contratto e quindi fare clic su Avanti.
1. Nella pagina Modifica licenza selezionare un tipo di licenza:

   * **EVAL:** licenza di valutazione di 60 giorni
   * **DEV:** Licenza di sviluppo permanente
   * **NFR:** licenza di valutazione biennale
   * **IDEV:** abbonamento di 1 anno al programma Adobe Developer
   * **Produzione:** licenza perpetua

1. Seleziona Sì, La Modifica Della Licenza È Valida Per Tutti I Moduli Distribuiti.
1. Fare clic su Conferma modifica licenza. Viene visualizzato un messaggio che informa che la licenza è stata aggiornata correttamente.
