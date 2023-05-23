---
title: Connessione a Microsoft&reg; Translator
description: Scopri come collegare AEM a Microsoft&reg; Translator.
uuid: 5e3916ec-36a0-4d31-94ff-c340a462411a
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: a7958411-b509-428e-bbe2-42efe8fd1add
feature: Language Copy
exl-id: ca575a30-fc3e-4f38-9aa7-dbecbc089f87
source-git-commit: 95638b6dd9527c567b38d8cd9da14633bd4142b5
workflow-type: tm+mt
source-wordcount: '606'
ht-degree: 11%

---

# Connessione a Microsoft® Translator{#connecting-to-microsoft-translator}

Crea una configurazione per Microsoft® Translator Cloud Service per utilizzare il tuo account di traduzione Microsoft® per tradurre il contenuto di una pagina AEM, il contenuto della community o le risorse.

| Proprietà | Descrizione |
|---|---|
| Etichetta traduzione | Il nome visualizzato per il servizio di traduzione. |
| Attribuzione traduzione | (Facoltativo) Per i contenuti generati dall’utente, l’attribuzione visualizzata accanto al testo tradotto, ad esempio `Translations by Microsoft`. |
| ID area di lavoro | (Facoltativo) L’ID del motore di traduzione Microsoft® personalizzato da utilizzare. |
| Chiave di sottoscrizione | Chiave di sottoscrizione Microsoft® per Microsoft® Translator. |

Dopo aver creato la configurazione, devi [attivarla](/help/sites-administering/tc-msconf.md#activating-the-translator-service-configurations).

La procedura seguente utilizza l’interfaccia utente ottimizzata per il tocco per creare una configurazione di Microsoft® Translator.

1. Nella barra, tocca o fai clic su Strumenti > Cloud Services.
1. Nell’area Microsoft® Translator, seleziona Mostra configurazioni.
1. Fai clic sul collegamento + accanto a Configurazioni disponibili.

   ![chlimage_1-382](assets/chlimage_1-382.png)

1. Digita un titolo per la configurazione. Il titolo identifica la configurazione nella console Cloud Services e negli elenchi a discesa delle proprietà della pagina. Il nome predefinito è basato sul titolo. Facoltativamente, digita un nome da utilizzare per il nodo dell’archivio che memorizza la configurazione. Utilizza il valore predefinito per la proprietà Configurazione principale, che corrisponde al percorso del nodo dell’archivio.
1. Fai clic su Crea.
1. Nella finestra di dialogo visualizzata digitare i valori per le proprietà e quindi fare clic su OK.

## Esempio di configurazioni del Cloud Service Microsoft® Translator {#sample-microsoft-translator-cloud-service-configurations}

Con gli esempi di Geometrixx vengono installate le seguenti configurazioni del servizio cloud Microsoft® Translator. Alcune configurazioni di esempio utilizzano un account Microsoft® Translation di prova che consente un massimo di 2 000 000 caratteri tradotti gratuiti al mese.

### Licenza di prova Microsoft® Translator {#microsoft-translator-trial-license}

La configurazione della licenza di prova di Microsoft® Translator è una configurazione di esempio installata con il pacchetto di esempio Geometrixx Outdoors. Questa configurazione utilizza un account Microsoft® Translator con un abbonamento gratuito che consente di tradurre 2.000.000 caratteri al mese.

### Licenza di prova Microsoft® Translator - Geometrixx-Outdoors {#microsoft-translator-trial-license-geometrixx-outdoors}

La configurazione Microsoft® Translator Trial License - Geometrixx-outdoors è una configurazione di esempio installata con i Geometrixx Outdoors. Questa configurazione utilizza lo stesso account Microsoft® Translator gratuito della configurazione della licenza di prova di Microsoft® Translator. L&#39;account dispone di un abbonamento gratuito che consente di tradurre 2 000 000 caratteri al mese.

Questa configurazione di Microsoft® Translator è ottimizzata per l’utilizzo con il tipo di contenuto del sito di esempio dei Geometrixx Outdoors.

### Aggiornamento della configurazione della licenza di prova di Microsoft® Translator {#upgrading-the-microsoft-translator-trial-license-configuration}

Le pagine di configurazione di Microsoft® Translation forniscono un comodo collegamento al sito web Microsoft® per ottenere un abbonamento a un account adeguato per i sistemi di produzione.

1. Nella barra, tocca o fai clic su Strumenti > Operazioni > Cloud > Cloud Services.
1. Nell’area Microsoft® Translator, tocca o fai clic su Mostra configurazioni, quindi tocca o fai clic su Microsoft® Translator Trial License (Microsoft® Translation Configuration).

   ![chlimage_1-383](assets/chlimage_1-383.png)

1. Nella pagina di configurazione, fai clic su Aggiorna abbonamento. Utilizza la pagina web Microsoft® che si apre per configurare l’account.

   ![chlimage_1-384](assets/chlimage_1-384.png)

### Personalizzazione del motore di traduzione Microsoft® {#customizing-your-microsoft-translator-engine}

Le pagine di configurazione di Microsoft® Translation forniscono un comodo collegamento al sito web Microsoft® per personalizzare il motore di traduzione Microsoft®. ([https://www.microsoft.com/en-us/research/project/microsoft-translator-hub/](https://www.microsoft.com/en-us/research/project/microsoft-translator-hub/))

1. Nella barra, tocca o fai clic su Strumenti > Operazioni > Cloud > Cloud Services.
1. Nell’area Microsoft® Translator, tocca o fai clic su Mostra configurazioni, quindi tocca o fai clic sulla configurazione da personalizzare.
1. Nella pagina di configurazione, fai clic su Personalizza Translator. Utilizza la pagina web Microsoft® che si apre per personalizzare il tuo servizio.

## Attivazione delle configurazioni del servizio Translator {#activating-the-translator-service-configurations}

Per supportare i contenuti tradotti replicati nell’istanza Publish, attiva le configurazioni del servizio cloud. Per attivare i nodi dell’archivio che memorizzano le configurazioni di Microsoft® Translator o di un servizio cloud di terze parti, utilizza il metodo [attivazione di una sezione completa (albero)](/help/sites-authoring/publishing-pages.md#publishing-and-unpublishing-a-tree). I nodi si trovano sotto i seguenti nodi principali:

* Servizio di traduzione Microsoft®: /libs/settings/cloudconfigs/translation/msft-translation
* Traduzione di terze parti: /etc/cloudservices/machine-translation
