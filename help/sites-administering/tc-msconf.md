---
title: Collegamento a Microsoft&reg; Traduttore
description: Scopri come collegare AEM a Microsoft&reg; Traduttore.
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

Crea una configurazione per il servizio cloud Microsoft® Translator per utilizzare il tuo account Microsoft® Translation per tradurre AEM contenuto di pagina, contenuto della community o risorse.

| Proprietà | Descrizione |
|---|---|
| Etichetta traduzione | Il nome visualizzato per il servizio di traduzione. |
| Attribuzione traduzione | (Facoltativo) Per i contenuti generati dall’utente, l’attribuzione visualizzata accanto al testo tradotto, ad esempio `Translations by Microsoft`. |
| ID area di lavoro | (Facoltativo) L&#39;ID del motore di traduzione Microsoft® personalizzato da utilizzare. |
| Chiave di sottoscrizione | Chiave di abbonamento Microsoft® per traduttore Microsoft®. |

Dopo aver creato la configurazione, devi [attivare](/help/sites-administering/tc-msconf.md#activating-the-translator-service-configurations).

La procedura seguente utilizza l’interfaccia touch per creare una configurazione Microsoft® Translator.

1. Nella barra, tocca o fai clic su Strumenti > Cloud Services.
1. Nell&#39;area Microsoft® Translator, selezionare Mostra configurazioni.
1. Fai clic sul collegamento + accanto a Configurazioni disponibili.

   ![chlimage_1-382](assets/chlimage_1-382.png)

1. Digita un titolo per la configurazione. Il titolo identifica la configurazione negli elenchi a discesa della console Cloud Services e delle proprietà della pagina. Il nome predefinito si basa sul titolo. Facoltativamente, digita un nome da utilizzare per il nodo dell’archivio che memorizza la configurazione. Utilizzare il valore predefinito per la proprietà Configurazione padre che rappresenta il percorso del nodo del repository.
1. Fai clic su Crea.
1. Nella finestra di dialogo visualizzata, digitare i valori delle proprietà e quindi fare clic su OK.

## Esempi di configurazioni del Cloud Service Microsoft® Translator {#sample-microsoft-translator-cloud-service-configurations}

Con gli esempi di Geometrixx sono installate le seguenti configurazioni del servizio cloud Microsoft® Translator. Alcune configurazioni di esempio utilizzano un account Microsoft® Translation di prova che consente un massimo di 2 000 000 caratteri tradotti gratuiti al mese.

### Licenza di prova per traduttori Microsoft® {#microsoft-translator-trial-license}

La configurazione Microsoft® Translator Trial License è una configurazione di esempio installata con il pacchetto di esempio Geometrixx Outdoors. Questa configurazione utilizza un account Microsoft® Translator che dispone di un abbonamento gratuito che consente 2 000 000 caratteri tradotti al mese.

### Licenza di prova per traduttori Microsoft® - Geometrixx all&#39;aperto {#microsoft-translator-trial-license-geometrixx-outdoors}

La Microsoft® Translator Trial License - Geometrixx all&#39;aperto è una configurazione di esempio installata con Geometrixx Outdoors. Questa configurazione utilizza lo stesso account gratuito Microsoft® Translator della configurazione Microsoft® Translator Trial License. L&#39;account dispone di un abbonamento gratuito che consente 2 000 000 caratteri tradotti al mese.

Questa configurazione di Microsoft® Translator è ottimizzata per l&#39;uso con il tipo di contenuto del sito di esempio Geometrixx Outdoors.

### Aggiornamento della configurazione della licenza di prova per Microsoft® Translator {#upgrading-the-microsoft-translator-trial-license-configuration}

Le pagine di configurazione di Microsoft® Translation forniscono un comodo collegamento al sito web Microsoft® per ottenere un abbonamento a un account adeguato per i sistemi di produzione.

1. Nella barra, tocca o fai clic su Strumenti > Operazioni > Cloud > Cloud Services.
1. Nell&#39;area Microsoft® Translator, tocca o fai clic su Mostra configurazioni, quindi tocca o fai clic su Microsoft® Translator Trial License (Microsoft® Translation Configuration).

   ![chlimage_1-383](assets/chlimage_1-383.png)

1. Nella pagina di configurazione, fai clic su Aggiorna sottoscrizione. Utilizza la pagina web Microsoft® visualizzata per configurare il tuo account.

   ![chlimage_1-384](assets/chlimage_1-384.png)

### Personalizzazione del motore di traduzione Microsoft® {#customizing-your-microsoft-translator-engine}

Le pagine di configurazione di Microsoft® Translation forniscono un comodo collegamento al sito web Microsoft® per personalizzare il motore di traduzione Microsoft®. ([https://www.microsoft.com/en-us/research/project/microsoft-translator-hub/](https://www.microsoft.com/en-us/research/project/microsoft-translator-hub/))

1. Nella barra, tocca o fai clic su Strumenti > Operazioni > Cloud > Cloud Services.
1. Nell&#39;area Microsoft® Translator, tocca o fai clic su Mostra configurazioni, quindi tocca o fai clic sulla configurazione da personalizzare.
1. Nella pagina di configurazione, fai clic su Personalizza traduttore. Utilizzare la pagina Web Microsoft® visualizzata per personalizzare il servizio.

## Attivazione delle configurazioni del servizio Translator {#activating-the-translator-service-configurations}

Per supportare i contenuti tradotti replicati nell’istanza di pubblicazione, attiva le configurazioni del servizio cloud. Per attivare i nodi dell&#39;archivio che memorizzano le configurazioni di Microsoft® Translator o di servizi cloud di terze parti, utilizza il metodo di [attivazione di una sezione completa (struttura ad albero)](/help/sites-authoring/publishing-pages.md#publishing-and-unpublishing-a-tree). I nodi si trovano sotto i seguenti nodi principali:

* Servizio di traduzione Microsoft®: /libs/settings/cloudconfigs/translation/msft-translation
* Traduzione di terze parti: /etc/cloudservices/traduzione automatica
