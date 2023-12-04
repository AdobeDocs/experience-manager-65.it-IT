---
title: Miglioramenti alla traduzione
description: Miglioramenti e perfezionamenti incrementali delle funzionalità di gestione della traduzione AEM.
topic-tags: site-features
content-type: reference
feature: Language Copy
exl-id: 2011a976-d506-4c0b-9980-b8837bdcf5ad
source-git-commit: 10b370fd8f855f71c6d7d791c272137bb5e04d97
workflow-type: tm+mt
source-wordcount: '669'
ht-degree: 26%

---

# Miglioramenti alla traduzione{#translation-enhancements}

Questa pagina presenta miglioramenti e perfezionamenti incrementali delle funzionalità di gestione della traduzione AEM.

## Automazione progetto di traduzione {#translation-project-automation}

Sono state aggiunte opzioni per migliorare la produttività lavorando con progetti di traduzione, come la promozione e l’eliminazione automatica dei lanci di traduzione e la pianificazione dell’esecuzione ricorrente di un progetto di traduzione.

1. Nel progetto di traduzione, fai clic sui puntini di sospensione nella parte inferiore della sezione **Riepilogo traduzione** affiancare.

   ![screen_shot_2018-04-19at222622](assets/screen_shot_2018-04-19at222622.jpg)

1. Passa a **Avanzate** scheda. In basso puoi selezionare **Promuovi automaticamente i lanci di traduzione**.

   ![screen_shot_2018-04-19at223430](assets/screen_shot_2018-04-19at223430.jpg)

1. Facoltativamente, puoi scegliere se, dopo aver ricevuto il contenuto tradotto, i lanci di traduzione debbano essere promossi ed eliminati automaticamente.

   ![screen_shot_2018-04-19at224033](assets/screen_shot_2018-04-19at224033.jpg)

1. Per selezionare l’esecuzione ricorrente di un progetto di traduzione, seleziona la frequenza con il menu a discesa in **Ripeti traduzione**. L’esecuzione ricorrente di un progetto creerà ed eseguirà automaticamente i processi di traduzione negli intervalli specificati.

   ![screen_shot_2018-04-19at223820](assets/screen_shot_2018-04-19at223820.jpg)

## Progetti di traduzione multilingue {#multilingual-translation-projects}

È possibile configurare più lingue di destinazione in un progetto di traduzione, per ridurre il numero totale di progetti di traduzione creati.

1. Nel progetto di traduzione, fai clic sui punti nella parte inferiore della sezione **Riepilogo traduzione** affiancare.

   ![screen_shot_2018-04-19at222622](assets/screen_shot_2018-04-19at222622.jpg)

1. Passa a **Avanzate** scheda. È possibile aggiungere più lingue in **Lingua di destinazione**.

   ![screen_shot_2018-04-22at212601](assets/screen_shot_2018-04-22at212601.jpg)

1. In alternativa, se stai avviando la traduzione tramite la barra dei riferimenti in Sites, aggiungi le lingue e seleziona **Crea progetto di traduzione multilingue**.

   ![screen_shot_2018-04-22at212941](assets/screen_shot_2018-04-22at212941.jpg)

1. I processi di traduzione verranno creati nel progetto per ogni lingua di destinazione. Possono essere avviati uno alla volta all’interno del progetto oppure tutti insieme eseguendo il progetto a livello globale in Projects Admin (Amministrazione progetti).

   ![screen_shot_2018-04-22at213854](assets/screen_shot_2018-04-22at213854.jpg)

## Aggiornamenti alla memoria di traduzione {#translation-memory-updates}

Le modifiche manuali dei contenuti tradotti possono essere sincronizzate con il sistema di gestione della traduzione (TMS) per addestrare la memoria di traduzione.

1. Dalla console Sites, dopo aver aggiornato il contenuto di testo in una pagina tradotta, seleziona **Aggiorna memoria di traduzione**.

   ![screen_shot_2018-04-22at234430](assets/screen_shot_2018-04-22at234430.jpg)

1. Una vista a elenco mostra un confronto affiancato dell’originale e della traduzione per ogni componente di testo modificato. Seleziona gli aggiornamenti da sincronizzare con la memoria di traduzione e quindi fai clic su **Aggiorna memoria**.

   ![screen_shot_2018-04-22at235024](assets/screen_shot_2018-04-22at235024.jpg)

AEM aggiorna la traduzione delle stringhe esistenti nella memoria di traduzione del TMS configurato.

* L’azione aggiorna la traduzione delle stringhe esistenti nella memoria di traduzione del TMS configurato.
* Non crea nuovi processi di traduzione.
* Invia le traduzioni al TMS tramite l’API di traduzione di AEM (vedi sotto).

Per utilizzare questa funzione:

* deve essere configurato un TMS per l’utilizzo in AEM.
* Il connettore deve implementare il metodo [`storeTranslation`](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/adobe/granite/translation/api/TranslationService.html).
   * Il codice all’interno di questo metodo determina cosa accade alla richiesta di aggiornamento della memoria di traduzione.
   * Il framework di traduzione di AEM invia nuovamente le coppie di valori stringa (traduzione originale e aggiornata) al TMS tramite questa implementazione del metodo.

Nei casi in cui viene utilizzata una memoria di traduzione proprietaria, gli aggiornamenti della memoria di traduzione possono essere intercettati e inviati a una destinazione personalizzata.

## Copie per lingua su più livelli {#language-copies-on-multiple-levels}

Le directory principali della lingua possono ora essere raggruppate in nodi, ad esempio per regione, pur essendo ancora riconosciute come directory principali delle copie della lingua.

![screen_shot_2018-04-23at144012](assets/screen_shot_2018-04-23at144012.jpg)

>[!CAUTION]
>
>È consentito un solo livello. Ad esempio, i seguenti elementi non consentiranno alla pagina &quot;es&quot; di risolvere in una copia per lingua:
>
>* `/content/we-retail/language-masters/en`
>* `/content/we-retail/language-masters/americas/central-america/es`
>
>Questo `es` la copia per lingua non verrà rilevata poiché si trova a 2 livelli (america/america centrale) di distanza dal `en` nodo.

>[!NOTE]
>
>Le radici della lingua possono avere qualsiasi nome di pagina, anziché solo il codice ISO della lingua. L&#39;AEM controlla sempre il percorso e il nome, ma se il nome della pagina non identifica una lingua, l&#39;AEM controlla la proprietà cq:language della pagina per l&#39;identificazione della lingua.

## Reporting sullo stato della traduzione {#translation-status-reporting}

Ora è possibile selezionare una proprietà nella vista a elenco Sites che mostra se una pagina è stata tradotta, è in traduzione o non è ancora stata tradotta. Per visualizzarlo:

1. In Sites, passa a **Vista a elenco.**

   ![screen_shot_2018-04-23at130646](assets/screen_shot_2018-04-23at130646.jpg)

1. Clic **Impostazioni vista**.

   ![screen_shot_2018-04-23at130844](assets/screen_shot_2018-04-23at130844.jpg)

1. Verifica **Tradotto** casella di controllo in **Traduzione** e fai clic su **Aggiorna**.

   ![screen_shot_2018-04-23at130955](assets/screen_shot_2018-04-23at130955.jpg)

Ora puoi vedere un **Tradotto** che mostra lo stato di traduzione delle pagine.

![screen_shot_2018-04-23at133821](assets/screen_shot_2018-04-23at133821.jpg)
