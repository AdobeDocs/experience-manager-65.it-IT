---
title: Connessione a Microsoft Translator
seo-title: Connessione a Microsoft Translator
description: Scoprite come collegare AEM a Microsoft Translator.
seo-description: Scoprite come collegare AEM a Microsoft Translator.
uuid: 5e3916ec-36a0-4d31-94ff-c340a462411a
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: a7958411-b509-428e-bbe2-42efe8fd1add
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Connessione a Microsoft Translator{#connecting-to-microsoft-translator}

Create una configurazione per il servizio cloud Microsoft Translator per utilizzare il vostro account Microsoft Translation per tradurre il contenuto delle pagine AEM, il contenuto della community o le risorse.

| Proprietà | Descrizione |
|---|---|
| Etichetta traduzione | Nome visualizzato per il servizio di traduzione. |
| Attribuzione traduzione | (Facoltativo) Per il contenuto generato dall&#39;utente, l&#39;attribuzione che viene visualizzata accanto al testo convertito, ad esempio `Translations by Microsoft`. |
| ID area di lavoro | (Facoltativo) L&#39;ID del motore di Microsoft Translator personalizzato da utilizzare. |
| Chiave di sottoscrizione | La chiave di iscrizione Microsoft per Microsoft Translator. |

Dopo aver creato la configurazione, è necessario [attivarla](/help/sites-administering/tc-msconf.md#activating-the-translator-service-configurations).

La procedura seguente utilizza l’interfaccia touch per creare una configurazione Microsoft Translator.

1. Nella barra laterale, fate clic o toccate Strumenti > Servizi cloud.
1. Nell&#39;area Microsoft Translator, fare clic o toccare Mostra configurazioni.
1. Fate clic sul collegamento + accanto a Configurazioni disponibili.

   ![chlimage_1-382](assets/chlimage_1-382.png)

1. Digitare un titolo per la configurazione. Il titolo identifica la configurazione sia nella console Servizi cloud che negli elenchi a discesa delle proprietà della pagina. Il nome predefinito si basa sul titolo. Facoltativamente, digitare un nome da utilizzare per il nodo del repository che memorizza la configurazione. È consigliabile utilizzare il valore predefinito per la proprietà Configurazione padre che rappresenta il percorso del nodo del repository.
1. Fate clic su Crea.
1. Nella finestra di dialogo visualizzata, digitate i valori per le proprietà e fate clic su OK.

## Configurazioni di servizio Microsoft Translator Cloud di esempio {#sample-microsoft-translator-cloud-service-configurations}

Con gli esempi Geometrixx sono installate le seguenti configurazioni del servizio cloud Microsoft Translator. Alcune configurazioni di esempio utilizzano un account di prova Microsoft Translation che consente di tradurre al massimo 2 000 000 caratteri al mese.

### Licenza di prova Microsoft Translator {#microsoft-translator-trial-license}

La configurazione della licenza di prova di Microsoft Translator è un esempio di configurazione installata con il pacchetto di esempio Geometrixx Outdoors. Questa configurazione utilizza un account Microsoft Translator con un abbonamento gratuito che consente 2 000 000 caratteri tradotti al mese.

### Microsoft Translator Trial License - Geometrixx-outdoors {#microsoft-translator-trial-license-geometrixx-outdoors}

La Microsoft Translator Trial License - Geometrixx-outdoors è una configurazione di esempio installata con Geometrixx Outdoors. Questa configurazione utilizza lo stesso account gratuito Microsoft Translator della configurazione Microsoft Translator Trial License. L&#39;account dispone di un&#39;iscrizione gratuita che consente 2 000 000 caratteri tradotti al mese.

Questa configurazione di Microsoft Translator è ottimizzata per l&#39;utilizzo con il tipo di contenuto del sito di esempio Geometrixx Outdoors.

### Aggiornamento della configurazione della licenza di prova di Microsoft Translator {#upgrading-the-microsoft-translator-trial-license-configuration}

Le pagine di configurazione di Microsoft Translation forniscono un comodo collegamento al sito Web Microsoft per ottenere un abbonamento a un account adeguato per i sistemi di produzione.

1. Nella barra laterale, fai clic su Strumenti > Operazioni > Cloud > Servizi cloud.
1. Nell&#39;area Microsoft Translator, fare clic o toccare Mostra configurazioni, quindi fare clic o toccare Microsoft Translator Trial License (Microsoft Translation Configuration).

   ![chlimage_1-383](assets/chlimage_1-383.png)

1. Nella pagina di configurazione, fate clic su Aggiorna iscrizione. Utilizzate la pagina Web Microsoft che si apre per configurare il vostro account.

   ![chlimage_1-384](assets/chlimage_1-384.png)

### Personalizzazione del motore di traduzione Microsoft {#customizing-your-microsoft-translator-engine}

Le pagine di configurazione di Microsoft Translation forniscono un comodo collegamento al sito Web Microsoft per la personalizzazione del motore Microsoft Translator. ([https://hub.microsofttranslator.com](https://hub.microsofttranslator.com/))

1. Nella barra laterale, fai clic su Strumenti > Operazioni > Cloud > Servizi cloud.
1. Nell&#39;area Microsoft Translator, fare clic o toccare Mostra configurazioni, quindi fare clic o toccare la configurazione da personalizzare.
1. Nella pagina di configurazione, fai clic su Personalizza traduttore. Utilizzare la pagina Web Microsoft che si apre per personalizzare il servizio.

## Attivazione delle configurazioni del servizio di traduzione {#activating-the-translator-service-configurations}

È necessario attivare le configurazioni del servizio cloud per supportare il contenuto convertito replicato nell’istanza di pubblicazione. Utilizzare il metodo di [attivazione di una sezione completa (struttura ad albero)](/help/sites-authoring/publishing-pages.md#publishing-and-unpublishing-a-tree) per attivare i nodi del repository in cui sono memorizzate le configurazioni del servizio cloud Microsoft Translator o di terze parti. I nodi si trovano sotto i seguenti nodi padre:

* Servizio di traduzione Microsoft: /etc/cloudservices/msft-Translation
* Traduzione di terze parti: /etc/cloudservices/traduzione automatica

