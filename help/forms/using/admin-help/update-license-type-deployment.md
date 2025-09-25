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
workflow-type: ht
source-wordcount: '282'
ht-degree: 100%

---

# Aggiornare il tipo di licenza per la distribuzione {#update-the-license-type-for-the-deployment}

>[!NOTE]
> 
> Assicurati che l’utente disponga dei privilegi di amministratore per accedere alla console dell’amministratore.

Come parte del processo di installazione di AEM Forms, è stato utilizzato Configuration Manager per configurare e distribuire i moduli di AEM Forms richiesti. Per impostazione predefinita, tali moduli sono configurati con una licenza di valutazione di 60 giorni. Utilizza la pagina Modifica licenza nella console di amministrazione per modificare il tipo di licenza per la distribuzione. I moduli attualmente distribuiti vengono visualizzati nella pagina Modifica licenza.

Nella pagina Modifica licenza vengono visualizzate le informazioni sulla licenza:

* Il tipo di licenza corrente
* La data e l’ora dell’ultima modifica apportata alla licenza
* Chi ha eseguito l’ultimo aggiornamento
* Lo stato corrente della licenza
* La data di installazione di AEM Forms
* La data di scadenza della licenza corrente

>[!NOTE]
>
>La modifica della licenza si applica a tutti i moduli distribuiti. Prima di modificare il tipo di licenza, annulla la distribuzione dei moduli non concessi in licenza. Non selezionare il tipo di licenza Produzione se l’elenco dei moduli distribuiti contiene moduli diversi da quelli acquistati da Adobe.

## Aggiornare il tipo di licenza {#update-the-license-type}

1. Nella console di amministrazione, fai clic su Concessione di licenza.
1. Leggi il contratto di licenza con l’utente finale di AEM Forms, seleziona Accetto se accetti i termini del contratto e quindi fai clic su Avanti.
1. Nella pagina Modifica licenza, seleziona un tipo di licenza:

   * **EVAL:** licenza di valutazione di 60 giorni
   * **DEV:** licenza di sviluppo permanente
   * **NFR:** licenza di valutazione biennale
   * **IDEV:** abbonamento di 1 anno ad Adobe Developer Program
   * **Produzione:** licenza perpetua

1. Seleziona Sì, la modifica della licenza è valida per tutti i moduli distribuiti.
1. Fai clic su Conferma modifica licenza. Viene visualizzato un messaggio che informa che la licenza è stata aggiornata correttamente.
