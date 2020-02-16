---
title: Aggiornamento del tipo di licenza per la distribuzione
seo-title: Aggiornamento del tipo di licenza per la distribuzione
description: Aggiornate il tipo di licenza per la distribuzione utilizzando la pagina Modifica licenza nella console di amministrazione.
seo-description: Aggiornate il tipo di licenza per la distribuzione utilizzando la pagina Modifica licenza nella console di amministrazione.
uuid: 0152635e-2c00-4944-b9b6-64b368589a91
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/get_started_with_administering_aem_forms_on_jee
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e4f31377-ccc9-4986-a3bf-ef2e83d12448
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Aggiornamento del tipo di licenza per la distribuzione {#update-the-license-type-for-the-deployment}

Durante il processo di installazione dei moduli AEM, è stato utilizzato Configuration Manager per configurare e implementare i moduli AEM richiesti. Per impostazione predefinita, tali moduli sono configurati con una licenza di valutazione di 60 giorni. Utilizzate la pagina Modifica licenza nella console di amministrazione per modificare il tipo di licenza per la distribuzione. I moduli attualmente distribuiti vengono visualizzati nella pagina Modifica licenza.

Nella pagina Modifica licenza sono visualizzate le informazioni sulla licenza:

* Il tipo di licenza corrente
* Data e ora dell’ultimo aggiornamento della licenza
* Chi ha eseguito l&#39;ultimo aggiornamento
* Stato corrente della licenza
* Data di installazione dei moduli AEM
* Data di scadenza della licenza corrente

>[!NOTE]
>
>La modifica della licenza si applica a tutti i moduli distribuiti. Prima di modificare il tipo di licenza, è necessario annullare la distribuzione dei moduli che non dispongono di licenza. Non selezionate il tipo di licenza Produzione se l&#39;elenco dei moduli distribuiti contiene moduli diversi da quelli acquistati da Adobe.

## Aggiornare il tipo di licenza {#update-the-license-type}

1. Nella console di amministrazione, fate clic su Licenze.
1. Leggi il contratto di licenza con l’utente finale dei moduli AEM, seleziona Accetto se sei d’accordo con i termini del contratto, quindi fai clic su Avanti.
1. Nella pagina Modifica licenza, selezionate un tipo di licenza:

   * **** EVAL: Licenza di valutazione di 60 giorni
   * **** DEV: Licenza di sviluppo permanente
   * **** NFR: licenza di valutazione biennale
   * **** IDEV: Iscrizione di 1 anno al programma Adobe Developer
   * **** Produzione: Licenza perpetua

1. Selezionare Sì, La Modifica Della Licenza È Valida Per Tutti I Moduli Distribuiti.
1. Fate clic su Conferma modifica licenza. Viene visualizzato un messaggio che indica che la licenza è stata aggiornata correttamente.

