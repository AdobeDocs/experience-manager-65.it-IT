---
title: Connessione a Microsoft Translator
seo-title: Connessione a Microsoft Translator
description: Scopri come connettersi AEM a Microsoft Translator.
seo-description: Scopri come connettersi AEM a Microsoft Translator.
uuid: 5e3916ec-36a0-4d31-94ff-c340a462411a
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: a7958411-b509-428e-bbe2-42efe8fd1add
feature: Copia lingua
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '618'
ht-degree: 3%

---


# Connessione a Microsoft Translator{#connecting-to-microsoft-translator}

Crea una configurazione per il servizio cloud Microsoft Translator per utilizzare il tuo account Microsoft Translation per tradurre AEM contenuto di pagina, contenuto della community o risorse.

| Proprietà | Descrizione |
|---|---|
| Etichetta traduzione | Nome visualizzato del servizio di traduzione. |
| Attribuzione traduzione | (Facoltativo) Per i contenuti generati dall’utente, l’attribuzione che viene visualizzata accanto al testo tradotto, ad esempio `Translations by Microsoft`. |
| ID area di lavoro | (Facoltativo) L&#39;ID del motore Microsoft Translator personalizzato da utilizzare. |
| Chiave di sottoscrizione | Chiave di abbonamento Microsoft per Microsoft Translator. |

Dopo aver creato la configurazione, è necessario [attivarla](/help/sites-administering/tc-msconf.md#activating-the-translator-service-configurations).

La procedura seguente utilizza l’interfaccia touch per creare una configurazione di Microsoft Translator.

1. Nella barra, tocca o fai clic su Strumenti > Cloud Services.
1. Nell&#39;area Microsoft Translator, fare clic o toccare Mostra configurazioni.
1. Fai clic sul collegamento + accanto a Configurazioni disponibili.

   ![chlimage_1-382](assets/chlimage_1-382.png)

1. Digita un titolo per la configurazione. Il titolo identifica la configurazione sia nella console Cloud Services che negli elenchi a discesa delle proprietà della pagina. Il nome predefinito si basa sul titolo. Facoltativamente, digita un nome da utilizzare per il nodo del repository che memorizza la configurazione. Utilizzare il valore predefinito per la proprietà Configurazione padre che rappresenta il percorso del nodo del repository.
1. Fai clic su Crea.
1. Nella finestra di dialogo visualizzata, digitare i valori delle proprietà e quindi fare clic su OK.

## Esempi di configurazioni del Cloud Service Microsoft Translator {#sample-microsoft-translator-cloud-service-configurations}

Con gli esempi di Geometrixx vengono installate le seguenti configurazioni del servizio cloud di Microsoft Translator. Alcune configurazioni di esempio utilizzano un account di prova di Microsoft Translation che consente un massimo di 2 000 000 caratteri tradotti gratuiti al mese.

### Licenza di prova Microsoft Translator {#microsoft-translator-trial-license}

La configurazione di Microsoft Translator Trial License è una configurazione di esempio installata con il pacchetto di esempio Geometrixx Outdoors. Questa configurazione utilizza un account Microsoft Translator con un abbonamento gratuito che consente 2 000 000 caratteri tradotti al mese.

### Licenza di prova per traduttori Microsoft - Geometrixx all&#39;aperto {#microsoft-translator-trial-license-geometrixx-outdoors}

La configurazione Trial License di Microsoft Translator - Geometrixx-outdoors è un esempio di configurazione installata con Geometrixx Outdoors. Questa configurazione utilizza lo stesso account gratuito Microsoft Translator della configurazione Microsoft Translator Trial License. L&#39;account dispone di un abbonamento gratuito che consente 2 000 000 caratteri tradotti al mese.

Questa configurazione di Microsoft Translator è ottimizzata per l&#39;uso con il tipo di contenuto del sito di esempio di Geometrixx Outdoors.

### Aggiornamento della configurazione della licenza di prova di Microsoft Translator {#upgrading-the-microsoft-translator-trial-license-configuration}

Le pagine di configurazione di Microsoft Translation forniscono un comodo collegamento al sito Web Microsoft per ottenere un abbonamento a un account adeguato per i sistemi di produzione.

1. Nella barra, tocca o fai clic su Strumenti > Operazioni > Cloud > Cloud Services.
1. Nell&#39;area Microsoft Translator, fare clic o toccare Mostra configurazioni, quindi fare clic o toccare Microsoft Translator Trial License (Microsoft Translation Configuration).

   ![chlimage_1-383](assets/chlimage_1-383.png)

1. Nella pagina di configurazione, fai clic su Aggiorna sottoscrizione. Utilizzare la pagina Web Microsoft visualizzata per configurare l&#39;account.

   ![chlimage_1-384](assets/chlimage_1-384.png)

### Personalizzazione del motore di traduzione Microsoft {#customizing-your-microsoft-translator-engine}

Le pagine di configurazione di Microsoft Translation forniscono un comodo collegamento al sito Web Microsoft per personalizzare il motore Microsoft Translator. ([https://hub.microsofttranslator.com](https://hub.microsofttranslator.com/))

1. Nella barra, tocca o fai clic su Strumenti > Operazioni > Cloud > Cloud Services.
1. Nell&#39;area Microsoft Translator, fare clic o toccare Mostra configurazioni, quindi fare clic o toccare la configurazione che si desidera personalizzare.
1. Nella pagina di configurazione, fai clic su Personalizza traduttore. Utilizzare la pagina Web Microsoft visualizzata per personalizzare il servizio.

## Attivazione delle configurazioni del servizio di traduzione {#activating-the-translator-service-configurations}

Devi attivare le configurazioni del servizio cloud per supportare i contenuti tradotti replicati nell’istanza di pubblicazione. Utilizza il metodo di [attivazione di una sezione completa (tree)](/help/sites-authoring/publishing-pages.md#publishing-and-unpublishing-a-tree) per attivare i nodi del repository che memorizzano le configurazioni di Microsoft Translator o di servizi cloud di terze parti. I nodi si trovano sotto i seguenti nodi padre:

* Servizio di traduzione Microsoft: /libs/settings/cloudconfigs/translation/msft-translation
* Traduzione di terze parti: /etc/cloudservices/traduzione automatica

