---
title: Configurare un account alias aziendale Dynamic Media
description: Scopri come configurare un account alias aziendale in Dynamic Media.
contentOwner: Rick Brough
topic-tags: administering
content-type: reference
feature: Image Profiles
role: User,Admin
mini-toc-levels: 4
exl-id: 2ca7b8b2-573c-40e9-b8c3-f38736e819ef
solution: Experience Manager, Experience Manager Assets
source-git-commit: 63b9494700aaafaa503216d037e2ad6efc8c5eac
workflow-type: tm+mt
source-wordcount: '684'
ht-degree: 2%

---

<!--
hide: true
-->

# Informazioni sulla configurazione di un account alias società Dynamic Media {#about-dm-alias-acct}

Gli URL di Dynamic Media e il codice di incorporamento del visualizzatore contengono il nome dell&#39;account della tua azienda. Questo nome account è stato creato al momento del provisioning di Dynamic Media. Ci possono essere scenari in cui la tua azienda ha subito un&#39;acquisizione, o un rebranding, o semplicemente vuoi utilizzare un nome più memorabile. In questi scenari, non è facile aggiornare manualmente il nome dell’account aziendale in tutti gli URL e nel codice di incorporamento del visualizzatore fornito con la soluzione. Inoltre, esiste la possibilità che tu possa influire sull’archivio Dynamic Media esistente o sui contenuti live. Per risolvere questo problema, puoi configurare un account alias della società Dynamic Media.

Un account alias della società Dynamic Media garantisce che tutti gli URL predefiniti di Dynamic Media e il codice di incorporamento del visualizzatore nell’interfaccia utente riflettano eventuali aggiornamenti apportati al contesto aziendale, ad esempio il rebranding. Un account alias ha anche un impatto positivo sull’ottimizzazione SEO (Search Engine Optimization), in quanto gli URL di Dynamic Media e il codice di incorporamento del visualizzatore riflettono il nuovo nome dell’account aziendale.

Quando configuri un account alias società Dynamic Media, tieni presente quanto segue:

* Eventuali URL Dynamic Media esistenti o codice di incorporamento del visualizzatore nelle proprietà digitali di *live* devono essere aggiornati manualmente per riflettere il nuovo nome alias. Tuttavia, gli URL o i visualizzatori che incorporano il codice con il nome aziendale Dynamic Media originale continuano a funzionare per le risorse nuove o esistenti.
* La funzionalità dell’account alias della società Dynamic Media è limitata alla modalità di authoring e alla consegna di Experience Manager Assets. Il nome alias della società non funziona con Experience Manager Sites. I componenti WCM (Web Content Management) non sono aggiornati per questa modifica. Questi componenti continuano a funzionare con il nome aziendale originale di Dynamic Media per recuperare le risorse Dynamic Media.
* Nella pagina **[!UICONTROL Modifica configurazione Dynamic Media]** è possibile impostare un solo account alias società. Tuttavia, puoi creare tutti gli account alias aziendali tramite un caso di supporto e riflettere manualmente il nome alias necessario negli URL di Dynamic Media o nel codice di incorporamento del visualizzatore.
* La funzionalità predefinita [Annullamento della validità della cache](/help/assets/invalidate-cdn-cache-dynamic-media.md) di Dynamic Media annulla la validità degli URL con gli account alias della società e della società configurati nella pagina Configurazione di Dynamic Media in Cloud Services.
* Quando configuri un account alias società nella pagina **[!UICONTROL Modifica configurazione Dynamic Media]**, affinché l&#39;annullamento della validità della cache abbia esito positivo, devi annullare la validità degli URL per *entrambi* l&#39;account **[!UICONTROL Società]** e l&#39;account **[!UICONTROL Alias società]**, contemporaneamente.

Vedi anche [Creare una configurazione Dynamic Media in Cloud Services](/help/assets/config-dms7.md#configuring-dynamic-media-cloud-services)

## Configurare un account alias società Dynamic Media {#configure-dm-alias-account}

Per iniziare a configurare un account alias della società Dynamic Media, invia prima un caso di supporto. Questo passaggio è obbligatorio.

1. [Utilizzare Admin Console per creare un caso di supporto](https://helpx.adobe.com/it/enterprise/using/support-for-experience-cloud.html).
1. Fornisci le seguenti informazioni nel tuo caso di assistenza:

   * Il nome alias della società Dynamic Media che desideri utilizzare. Il nome deve contenere *solo* lettere (sono consentite maiuscole e minuscole miste), numeri, trattini e trattini bassi.
   * La tua regione.
   * Indica se in precedenza sono stati utilizzati [set di regole](/help/assets/using-rulesets-to-transform-urls.md) per ottenere la distribuzione del contenuto Dynamic Media tramite un nome di account aziendale Dynamic Media alternativo.

1. Dopo la creazione dell’account alias Dynamic Media da parte del supporto, nell’istanza Autore Experience Manager as a Cloud Service, seleziona il logo Experience Manager as a Cloud Service per accedere alla console di navigazione globale.
1. Sulla sinistra della console, seleziona l&#39;icona Strumenti, quindi vai a **[!UICONTROL Cloud Services > Configurazione elemento multimediale dinamico]**.
1. Nel riquadro sinistro della pagina Browser configurazioni Dynamic Media selezionare **[!UICONTROL global]** (non selezionare l&#39;icona della cartella a sinistra di **[!UICONTROL global]**). Quindi seleziona **[!UICONTROL Modifica]**.

   ![Campo di testo alias società Dynamic Media](/help/assets/assets-dm/dm-company-alias.png)

1. Nella pagina **[!UICONTROL Modifica configurazione Dynamic Media]**, digita nel campo di testo **[!UICONTROL Alias società]** il nome dell&#39;account alias Dynamic Media specificato in precedenza nel caso di supporto.
1. In alto a destra, seleziona **[!UICONTROL Salva]**.
L’account alias società Dynamic Media è ora salvato e abilitato; tutti gli URL e il codice di incorporamento del visualizzatore per le risorse nuove e esistenti ora riflettono il nuovo nome alias società.
