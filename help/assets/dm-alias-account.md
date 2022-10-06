---
title: Configurare un account alias società Dynamic Media
description: Scopri come configurare un account alias società in Dynamic Media.
contentOwner: Rick Brough
topic-tags: administering
content-type: reference
feature: Image Profiles
role: User,Admin
mini-toc-levels: 4
exl-id: 2ca7b8b2-573c-40e9-b8c3-f38736e819ef
source-git-commit: 787c0c25da2258f234d3c821038d62bf8ef68932
workflow-type: tm+mt
source-wordcount: '675'
ht-degree: 0%

---

<!-- hide: yes
hidefromtoc: yes -->

# Informazioni sulla configurazione di un account alias società Dynamic Media {#about-dm-alias-acct}

Gli URL Dynamic Media e il codice di incorporamento del visualizzatore contengono il nome dell&#39;account aziendale. Questo nome account è stato creato al momento del provisioning di Dynamic Media. Ci possono essere scenari in cui la tua azienda ha subito un&#39;acquisizione, o un rebranding, o semplicemente vuoi usare un nome più memorabile. In tali scenari, non è facile aggiornare manualmente il nome dell’account dell’azienda in tutti gli URL e il codice di incorporamento del visualizzatore che viene fuori dalla scatola. Inoltre, è possibile che tu possa avere un impatto sull’archivio Dynamic Media esistente o sui contenuti live. Per risolvere il problema, puoi configurare un account alias società Dynamic Media.

Un account alias di un’azienda Dynamic Media garantisce che tutti gli URL Dynamic Media predefiniti e il codice da incorporare del visualizzatore nell’interfaccia utente riflettano eventuali aggiornamenti apportati al contesto aziendale, ad esempio il rebranding. Un account alias ha anche un impatto positivo sul tuo SEO (Search Engine Optimization) perché gli URL di Dynamic Media e il codice di incorporamento del visualizzatore riflettono il nome del nuovo account aziendale.

Quando configuri un account alias società Dynamic Media, tieni presente quanto segue:

* Eventuali URL Dynamic Media o codice di incorporamento visualizzatore esistenti sul tuo *live* le proprietà digitali devono essere aggiornate manualmente per riflettere il nuovo nome di alias. Tuttavia, qualsiasi URL o codice da incorporare dei visualizzatori con il nome della società Dynamic Media originale continua a funzionare per le risorse esistenti o nuove.
* La funzionalità dell’account alias dell’azienda Dynamic Media è limitata alla modalità di authoring e di consegna Experience Manager Assets. Il nome alias della società non funziona con Experience Manager Sites. I componenti WCM (Web Content Management) non vengono aggiornati per questa modifica. Questi componenti continuano a funzionare con il nome originale dell’azienda Dynamic Media per recuperare le risorse Dynamic Media.
* È possibile impostare un solo account alias società nel **[!UICONTROL Modifica configurazione Dynamic Media]** pagina. Tuttavia, puoi creare un numero illimitato di account alias aziendali tramite un caso di supporto e riflettere manualmente il nome alias necessario negli URL Dynamic Media o nel codice di incorporamento del visualizzatore.
* Il prodotto pronto all&#39;uso [Annullamento della validità della cache](/help/assets/invalidate-cdn-cache-dynamic-media.md) La funzionalità di Dynamic Media invalida gli URL con account Alias società e società configurati nella pagina Configurazione Dynamic Media in Cloud Services.
* Quando configuri un account alias società nel **[!UICONTROL Modifica configurazione Dynamic Media]** per il corretto annullamento della validità della validità della cache, è necessario annullare la validità degli URL per *entrambi* la **[!UICONTROL Azienda]** e **[!UICONTROL Alias società]** account, simultaneamente.

Vedi anche [Creare una configurazione Dynamic Media nei Cloud Services](/help/assets/config-dms7.md#configuring-dynamic-media-cloud-services)

## Configurare un account alias società Dynamic Media {#configure-dm-alias-account}

Per iniziare a configurare un account alias società Dynamic Media, invia prima un caso di assistenza. Questo passaggio è obbligatorio.

1. [Utilizza l’Admin Console per creare un caso di supporto](https://helpx.adobe.com/it/enterprise/using/support-for-experience-cloud.html).
1. Fornisci le seguenti informazioni nel tuo caso di assistenza:

   * Il nome dell&#39;alias della società Dynamic Media che si desidera utilizzare. Il nome deve contenere *only* lettere (è consentita la combinazione di maiuscole e minuscole), numeri, trattini e caratteri di sottolineatura.
   * La tua regione.
   * Se necessario [set di regole](/help/assets/using-rulesets-to-transform-urls.md) vengono utilizzati in precedenza per ottenere la trasmissione di contenuti Dynamic Media tramite un nome account aziendale Dynamic Media alternativo.

1. Dopo che l&#39;account alias Dynamic Media è stato creato dal supporto, in Experience Manager istanza di authoring as a Cloud Service, seleziona il logo as a Cloud Service di Experience Manager per accedere alla console di navigazione globale.
1. Nella parte sinistra della console, seleziona l’icona Strumenti , quindi vai a **[!UICONTROL Cloud Services > Configurazione Dynamic Media]**.
1. Nella pagina Browser configurazione Dynamic Media, seleziona nel riquadro a sinistra **[!UICONTROL globale]** (non selezionare l’icona della cartella a sinistra di **[!UICONTROL globale]**). Quindi seleziona **[!UICONTROL Modifica]**.

   ![Campo di testo Alias società Dynamic Media](/help/assets/assets-dm/dm-company-alias.png)

1. Sulla **[!UICONTROL Modifica configurazione Dynamic Media]** nella pagina **[!UICONTROL Alias società]** campo di testo, digitare il nome dell&#39;account alias Dynamic Media specificato in precedenza nel caso di supporto.
1. In alto a destra della pagina, seleziona **[!UICONTROL Salva]**.
L’account alias dell’azienda Dynamic Media viene ora salvato e attivato; tutti gli URL e il codice di incorporamento del visualizzatore per le risorse nuove ed esistenti ora riflettono il nuovo nome alias società.
