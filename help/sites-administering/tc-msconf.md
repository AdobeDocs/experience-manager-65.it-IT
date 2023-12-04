---
title: Connetti a Microsoft Translator
description: Scopri come collegare AEM a Microsoft Translator predefinito per automatizzare il flusso di lavoro di traduzione.
feature: Language Copy
role: Admin
exl-id: ca575a30-fc3e-4f38-9aa7-dbecbc089f87
source-git-commit: 10b370fd8f855f71c6d7d791c272137bb5e04d97
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 80%

---

# Connetti a Microsoft Translator {#connecting-to-microsoft-translator}

Crea una configurazione per [Microsoft Translator](https://www.microsoft.com/it-it/translator/business/) Cloud Service per utilizzare il tuo account di traduzione Microsoft per tradurre il contenuto di una pagina o le risorse di AEM.

>[!NOTE]
>
>AEM fornisce un account di prova di Microsoft Translation che consente un massimo di 2 000 000 caratteri tradotti gratuiti al mese. Per ottenere un abbonamento a un account adeguato per i sistemi di produzione, consulta [Aggiornamento della configurazione della licenza di prova di Microsoft Translator](#upgrading-the-microsoft-translator-trial-license-configuration).

| Proprietà | Descrizione |
|---|---|
| Etichetta traduzione | Il nome visualizzato per il servizio di traduzione |
| Attribuzione traduzione | (Facoltativo) Per i contenuti generati dall’utente, l’attribuzione visualizzata accanto al testo tradotto, ad esempio, `Translations by Microsoft` |
| ID area di lavoro | (Facoltativo) L’ID del motore di Microsoft Translator personalizzato da utilizzare |
| Chiave di sottoscrizione | La chiave di abbonamento a Microsoft per Microsoft Translator |

Dopo aver creato la configurazione, devi [attivarla](#activating-the-translator-service-configurations).

La procedura seguente crea una configurazione di Microsoft Translator.

1. In [pannello di navigazione,](/help/sites-authoring/basic-handling.md#first-steps) click **Strumenti** > **Cloud Service** > **Cloud Service di traduzione**.
1. Passa alla posizione in cui desideri creare la configurazione. Normalmente si trova nel sito principale oppure può essere una configurazione globale predefinita.
1. Fai clic su **Crea** pulsante.
1. Definisci la configurazione.
   1. Seleziona **Microsoft Translator** nel menu a discesa.
   1. Digita un titolo per la configurazione. Il titolo identifica la configurazione sia nella console Cloud Services che negli elenchi a discesa delle proprietà della pagina.
   1. Facoltativamente, digita un nome da utilizzare per il nodo dell’archivio che memorizza la configurazione.

   ![Creare una configurazione di traduzione](assets/create-translation-config.png)

1. Fai clic su **Crea**.
1. Nella finestra **Modifica configurazione**, indica i valori per il servizio di traduzione descritto nella tabella precedente.

   ![Modificare la configurazione della traduzione](assets/edit-translation-config.png)

1. Clic **Connetti** per verificare la connessione.
1. Fai clic su **Salva e chiudi**.

## Aggiornamento della configurazione della licenza di prova di Microsoft Translator {#upgrading-the-microsoft-translator-trial-license-configuration}

Le pagine di configurazione di Microsoft Translation forniscono un comodo collegamento al sito web Microsoft per ottenere un abbonamento a un account adeguato per i sistemi di produzione.

1. In [pannello di navigazione,](/help/sites-authoring/basic-handling.md#first-steps) click **Strumenti** > **Cloud Service** > **Cloud Service di traduzione**.
1. Fai clic sulla configurazione di Microsoft Translator esistente.
1. Clic **Modifica**.
1. In **Modifica configurazione** finestra, fai clic su **Aggiorna abbonamento**. Si aprirà una pagina web Microsoft con ulteriori dettagli sul servizio.

## Personalizzazione del motore di traduzione Microsoft {#customizing-your-microsoft-translator-engine}

Le pagine di configurazione di Microsoft Translation forniscono un comodo collegamento al sito web Microsoft per personalizzare il motore di traduzione Microsoft.

1. In [pannello di navigazione,](/help/sites-authoring/basic-handling.md#first-steps) click **Strumenti** > **Cloud Service** > **Cloud Service di traduzione**.
1. Fai clic sulla configurazione di Microsoft Translator esistente.
1. Clic **Modifica**.
1. In **Modifica configurazione** finestra, fai clic su **Personalizza Translator**. Utilizza la pagina web Microsoft che si apre per personalizzare il tuo servizio.

## Attivazione delle configurazioni del servizio Translator {#activating-the-translator-service-configurations}

Devi attivare le configurazioni del servizio cloud per supportare i contenuti tradotti replicati nell’istanza di pubblicazione. Utilizza il metodo [pubblicazione di una struttura](/help/sites-authoring/publishing-pages.md#publishing-and-unpublishing-a-tree) per attivare i nodi dell’archivio che memorizzano le configurazioni di Microsoft Translator. I nodi si trovano sotto i seguenti nodi principali:

* `/libs/settings/cloudconfigs/translation/msft-translation`
