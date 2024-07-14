---
title: Configurare un account alias società Dynamic Medie
description: Scopri come configurare un account alias aziendale in Dynamic Medie.
contentOwner: Rick Brough
topic-tags: administering
content-type: reference
feature: Image Profiles
role: User,Admin
mini-toc-levels: 4
exl-id: 2ca7b8b2-573c-40e9-b8c3-f38736e819ef
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '671'
ht-degree: 0%

---

<!-- hide: yes
hidefromtoc: yes -->

# Informazioni sulla configurazione di un account alias società Dynamic Medie {#about-dm-alias-acct}

Gli URL di Dynamic Medie e il codice di incorporamento del visualizzatore contengono il nome dell&#39;account dell&#39;azienda. Questo nome account è stato creato al momento del provisioning di Dynamic Medie. Ci possono essere scenari in cui la tua azienda ha subito un&#39;acquisizione, o un rebranding, o semplicemente vuoi utilizzare un nome più memorabile. In questi scenari, non è facile aggiornare manualmente il nome dell’account aziendale in tutti gli URL e nel codice di incorporamento del visualizzatore fornito con la soluzione. Inoltre, esiste la possibilità che tu possa influire sull’archivio Dynamic Medie esistente o sui contenuti live. Per risolvere il problema, è possibile configurare un account alias società Dynamic Medie.

Un account alias società Dynamic Medie garantisce che tutti gli URL predefiniti di Dynamic Medie e il codice di incorporamento del visualizzatore nell’interfaccia utente riflettano eventuali aggiornamenti apportati al contesto aziendale, ad esempio il rebranding. Un account alias ha anche un impatto positivo sull’ottimizzazione SEO (Search Engine Optimization), in quanto gli URL di Dynamic Medie e il codice di incorporamento del visualizzatore riflettono il nuovo nome dell’account aziendale.

Quando configuri un account alias società Dynamic Medie, tieni presente quanto segue:

* Eventuali URL di Dynamic Medie esistenti o codice di incorporamento del visualizzatore nelle proprietà digitali di *live* devono essere aggiornati manualmente per riflettere il nuovo nome alias. Tuttavia, gli URL o i visualizzatori che incorporano il codice con il nome originale dell&#39;azienda Dynamic Medie continuano a funzionare per le risorse nuove o esistenti.
* La funzionalità dell’account alias della società Dynamic Medie è limitata alla modalità e alla consegna di Experience Manager Assets Authoring. Il nome alias della società non funziona con Experience Manager Sites. I componenti WCM (Web Content Management) non sono aggiornati per questa modifica. Tali componenti continuano a funzionare con il nome aziendale originale di Dynamic Medie per recuperare le risorse Dynamic Medie.
* È possibile impostare un solo account alias società nella pagina **[!UICONTROL Modifica configurazione Dynamic Medie]**. Tuttavia, puoi creare tutti gli account alias aziendali tramite un caso di supporto e riflettere manualmente il nome alias necessario negli URL di Dynamic Medie o nel codice di incorporamento del visualizzatore.
* La funzionalità predefinita [Annullamento della validità della cache](/help/assets/invalidate-cdn-cache-dynamic-media.md) di Dynamic Medie annulla la validità degli URL con gli account alias società e società configurati nella pagina Configurazione di Dynamic Medie in Cloud Service.
* Quando si configura un account alias società nella pagina **[!UICONTROL Modifica configurazione Dynamic Medie]**, affinché l&#39;annullamento della validità della cache venga eseguito correttamente, è necessario annullare la validità degli URL per *entrambi* l&#39;account **[!UICONTROL Società]** e l&#39;account **[!UICONTROL Alias società]**, contemporaneamente.

Vedi anche [Creare una configurazione Dynamic Medie in Cloud Service](/help/assets/config-dms7.md#configuring-dynamic-media-cloud-services)

## Configurare un account alias società Dynamic Medie {#configure-dm-alias-account}

Per iniziare a configurare un account alias della società Dynamic Medie, devi prima inviare un caso di supporto. Questo passaggio è obbligatorio.

1. [Utilizzare l&#39;Admin Console per creare un caso di supporto](https://helpx.adobe.com/it/enterprise/using/support-for-experience-cloud.html).
1. Fornisci le seguenti informazioni nel tuo caso di assistenza:

   * Nome alias società Dynamic Medie che si desidera utilizzare. Il nome deve contenere *solo* lettere (sono consentite maiuscole e minuscole miste), numeri, trattini e trattini bassi.
   * La tua regione.
   * Indica se in precedenza sono stati utilizzati [set di regole](/help/assets/using-rulesets-to-transform-urls.md) per ottenere la distribuzione del contenuto Dynamic Medie tramite un nome di account aziendale Dynamic Medie alternativo.

1. Dopo la creazione dell’account alias Dynamic Medie da parte del supporto, nell’istanza Experience Manager as a Cloud Service Experience Manager Author, seleziona il logo dell’as a Cloud Service per accedere alla console di navigazione globale.
1. Sulla sinistra della console, seleziona l&#39;icona Strumenti, quindi vai a **[!UICONTROL Cloud Service > Configurazione Dynamic Medie]**.
1. Nel riquadro sinistro della pagina Browser configurazioni Dynamic Medie selezionare **[!UICONTROL global]** (non selezionare l&#39;icona della cartella a sinistra di **[!UICONTROL global]**). Quindi seleziona **[!UICONTROL Modifica]**.

   ![Campo di testo Alias società Dynamic Medie](/help/assets/assets-dm/dm-company-alias.png)

1. Nella pagina **[!UICONTROL Modifica configurazione Dynamic Medie]**, nel campo di testo **[!UICONTROL Alias società]**, digitare il nome dell&#39;account alias Dynamic Medie specificato in precedenza nel caso di supporto.
1. In alto a destra, seleziona **[!UICONTROL Salva]**.
L’account alias società Dynamic Medie ora è salvato e abilitato; tutti gli URL e il codice di incorporamento del visualizzatore per le risorse nuove e esistenti ora riflettono il nuovo nome alias società.
