---
title: Configurazione di Commerce Multi-Store
description: Scopri come mappare più viste store da Magento a AEM. Questo consente ai progetti di supportare casi d’uso multi-tenant e multilingue.
sub-product: Commerce
doc-type: technical-video
activity: setup
audience: administrator
feature: Commerce Integration Framework
kt: 3046
thumbnail: 28952.jpg
translation-type: tm+mt
source-git-commit: da538dac17b4c6182b44801b4c79d6cdbf35f640
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 69%

---

# Configurazione multi-store di Commerce {#multi-store}

I componenti core CIF di AEM possono essere utilizzati su più strutture di siti AEM e l’implementazione client GraphQL sottostante può connettersi a diversi store o viste store di Magento. Ciò consente ai progetti di implementare complesse impostazioni per più store o siti.

Una procedura video dettagliata che illustra le opzioni di integrazione di più visualizzazioni store di Magento con Adobe Experience Manager Sites.

>[!VIDEO](https://video.tv.adobe.com/v/28952/?quality=12)

Le funzioni Live Copy e Copia per lingua di AEM per la gestione di più siti sono utilizzate insieme a Commerce Integration Framework (CIF) per gestire globalmente i siti per diverse aree geografiche e lingue.

Si consiglia di utilizzare una relazione 1:1 tra AEM Sites e la vista Store di Magento.

Per collegare un sito AEM e AEM componenti core CIF a una visualizzazione dedicata dello store, segui i passaggi seguenti:

## Configurazione {#configuration}

1. Configura più store e viste Store in base al pattern descritto in [Magento Websites, Stores &amp; Views](https://docs.magento.com/m2/ce/user_guide/stores/websites-stores-views.html) (Siti web, store e viste di Magento).

2. Assicurati che la connessione tra AEM e Magento funzioni.

3. Crea una configurazione figlio della configurazione di Cloud Service CIF:

   * In AEM vai a Strumenti -> Generale -> [Browser di configurazione](/help/sites-administering/configurations.md#using-configuration-browser)
   * Seleziona la configurazione di base creata.
   * Crea una nuova configurazione seguendo i passaggi descritti al punto 2 precedente.

   Questa nuova configurazione verrà creata come configurazione secondaria di quella di base. Ora passa a Strumenti > Generale > Browser di configurazione e crea le impostazioni di configurazione.

   >[!TIP]
   >
   > I cataloghi commerciali possono essere gestiti utilizzando ID o UID. Gli UID sono stati introdotti nel Magento 2.4.2. Abilitalo solo se il backend commerce supporta uno schema GraphQL della versione 2.4.2 o successiva.

4. Assegnare la configurazione figlio a un sito AEM

   * Passa alla console di AEM Sites.
   * Passa alla directory principale dell’area geografica o della lingua della struttura del sito, ad esempio /content/venia/us _o_ /content/venia/us/it per la pagina di esempio di Venia
   * Seleziona la pagina e apri le proprietà della pagina.
   * Seleziona la scheda Avanzate.
   * Nella sezione `Configuration`, seleziona la configurazione creata al passaggio

## Risorse aggiuntive

* [Magento Website, Stores e Views](https://docs.magento.com/m2/ce/user_guide/stores/websites-stores-views.html)
* [Componenti core CIF di AEM: configurazione di più store o siti](https://github.com/adobe/aem-core-cif-components/wiki/configuration#multi-store--site-configuration)
* [Utilizzo di Multi-Site Manager](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/translation/multi-site-manager-feature-video-use.html)
* [Riutilizzo del contenuto: Multi-Site Manager e Live Copy](/help/sites-administering/msm.md)