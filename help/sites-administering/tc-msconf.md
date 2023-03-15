---
title: Connetti a Microsoft Translator
seo-title: Connecting to Microsoft Translator
description: Scopri come collegarti AEM a Microsoft Translator.
seo-description: Learn how to connect AEM to Microsoft Translator.
uuid: 5e3916ec-36a0-4d31-94ff-c340a462411a
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: a7958411-b509-428e-bbe2-42efe8fd1add
feature: Language Copy
exl-id: ca575a30-fc3e-4f38-9aa7-dbecbc089f87
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '604'
ht-degree: 35%

---

# Connetti a Microsoft Translator{#connecting-to-microsoft-translator}

Crea una configurazione per il servizio cloud Microsoft Translator per utilizzare il tuo account di traduzione Microsoft per tradurre AEM contenuto di pagina, contenuto della community o risorse.

| Proprietà | Descrizione |
|---|---|
| Etichetta traduzione | Il nome visualizzato per il servizio di traduzione. |
| Attribuzione traduzione | (Facoltativo) Per i contenuti generati dall’utente, l’attribuzione visualizzata accanto al testo tradotto, ad esempio `Translations by Microsoft`. |
| ID area di lavoro | (Facoltativo) L’ID del motore di Microsoft Translator personalizzato da utilizzare. |
| Chiave di sottoscrizione | La chiave di abbonamento a Microsoft per Microsoft Translator. |

Dopo aver creato la configurazione, devi [attivarla](/help/sites-administering/tc-msconf.md#activating-the-translator-service-configurations).

La procedura seguente utilizza l’interfaccia touch per creare una configurazione Microsoft Translator.

1. Nella barra, tocca o fai clic su Strumenti > Cloud Services.
1. Nell’area Microsoft Translator, tocca o fai clic su Mostra configurazioni.
1. Fai clic sul collegamento + accanto a Configurazioni disponibili.

   ![chlimage_1-382](assets/chlimage_1-382.png)

1. Digita un titolo per la configurazione. Il titolo identifica la configurazione sia nella console Servizi cloud che negli elenchi a discesa delle proprietà della pagina. Il nome predefinito si basa sul titolo. Facoltativamente, digita un nome da utilizzare per il nodo dell’archivio che memorizza la configurazione. Utilizzare il valore predefinito per la proprietà Configurazione padre che rappresenta il percorso del nodo del repository.
1. Fai clic su Crea.
1. Nella finestra di dialogo visualizzata, digitare i valori delle proprietà e quindi fare clic su OK.

## Configurazioni di Cloud Service Microsoft Translator di esempio {#sample-microsoft-translator-cloud-service-configurations}

Con gli esempi di Geometrixx sono installate le seguenti configurazioni del servizio cloud di Microsoft Translator. Alcune configurazioni di esempio utilizzano un account di traduzione Microsoft di prova che consente un massimo di 2 000 000 caratteri tradotti gratuiti al mese.

### Licenza di prova Microsoft Translator {#microsoft-translator-trial-license}

La configurazione Microsoft Translator Trial License è una configurazione di esempio installata con il pacchetto di esempio Geometrixx Outdoors. Questa configurazione utilizza un account Microsoft Translator con un abbonamento gratuito che consente 2 000 000 caratteri tradotti al mese.

### Licenza di prova per traduttori Microsoft - Geometrixx all&#39;aperto {#microsoft-translator-trial-license-geometrixx-outdoors}

La configurazione Geometrixx-outdoors della licenza di prova di Microsoft Translator è un esempio di configurazione installata con Geometrixx Outdoors. Questa configurazione utilizza lo stesso account gratuito Microsoft Translator della configurazione Microsoft Translator Trial License. L&#39;account dispone di un abbonamento gratuito che consente 2 000 000 caratteri tradotti al mese.

Questa configurazione di Microsoft Translator è ottimizzata per l’uso con il tipo di contenuto del sito di esempio Geometrixx Outdoors.

### Aggiornamento della configurazione della licenza di prova di Microsoft Translator {#upgrading-the-microsoft-translator-trial-license-configuration}

Le pagine di configurazione di Microsoft Translation forniscono un comodo collegamento al sito web Microsoft per ottenere un abbonamento a un account adeguato per i sistemi di produzione.

1. Nella barra, tocca o fai clic su Strumenti > Operazioni > Cloud > Cloud Services.
1. Nell’area Microsoft Translator, tocca o fai clic su Show Configurations (Mostra configurazioni), quindi tocca o fai clic su Microsoft Translator Trial License (Configurazione traduzione Microsoft).

   ![chlimage_1-383](assets/chlimage_1-383.png)

1. Nella pagina di configurazione, fai clic su Aggiorna sottoscrizione. Utilizza la pagina web Microsoft che si apre per configurare il tuo account.

   ![chlimage_1-384](assets/chlimage_1-384.png)

### Personalizzazione del motore di traduzione Microsoft {#customizing-your-microsoft-translator-engine}

Le pagine di configurazione di Microsoft Translation forniscono un comodo collegamento al sito web Microsoft per personalizzare il motore di traduzione Microsoft. ([https://hub.microsofttranslator.com](https://hub.microsofttranslator.com/))

1. Nella barra, tocca o fai clic su Strumenti > Operazioni > Cloud > Cloud Services.
1. Nell’area Microsoft Translator, tocca o fai clic su Mostra configurazioni , quindi tocca o fai clic sulla configurazione da personalizzare.
1. Nella pagina di configurazione, fai clic su Personalizza traduttore. Utilizza la pagina web Microsoft che si apre per personalizzare il tuo servizio.

## Attivazione delle configurazioni del servizio Translator {#activating-the-translator-service-configurations}

Devi attivare le configurazioni del servizio cloud per supportare i contenuti tradotti replicati nell’istanza di pubblicazione. Utilizzare il metodo [attivazione di una sezione completa (struttura ad albero)](/help/sites-authoring/publishing-pages.md#publishing-and-unpublishing-a-tree) per attivare i nodi dell’archivio che memorizzano le configurazioni di Microsoft Translator o di cloud service di terze parti. I nodi si trovano sotto i seguenti nodi principali:

* Servizio di traduzione Microsoft: /libs/settings/cloudconfigs/translation/msft-translation
* Traduzione di terze parti: /etc/cloudservices/traduzione automatica
