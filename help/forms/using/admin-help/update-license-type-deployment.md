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
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 751e1826ed53df7522418e50a206f0fe622256a4
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 100%
---
# Aggiornare il tipo di licenza per la distribuzione {#update-the-license-type-for-the-deployment}

>[!NOTE]
> 
> Assicurati che l’utente disponga dei privilegi di amministratore per accedere alla console dell’amministratore.

Come parte del processo di installazione di AEM Forms, è stato utilizzato Configuration Manager per configurare e distribuire i moduli di AEM Forms richiesti. Per impostazione predefinita, tali moduli sono configurati con una licenza di valutazione di 60 giorni. Utilizza la pagina Modifica licenza nella console di amministrazione per modificare il tipo di licenza per la distribuzione. I moduli attualmente distribuiti vengono visualizzati nella pagina Modifica licenza.

Nella pagina Modifica licenza vengono visualizzate le informazioni sulla licenza:

* Il tipo di licenza corrente
* La data e l’ora dell’ultimo aggiornamento della licenza
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
