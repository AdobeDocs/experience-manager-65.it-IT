---
title: Utilizzare i set di regole per trasformare gli URL
description: Puoi distribuire i set di regole in Dynamic Media per trasformare gli URL. I set di regole sono insiemi di istruzioni scritte in un linguaggio di script (ad esempio JavaScript) che valutano i dati XML e eseguono determinate azioni se tali dati soddisfano determinate condizioni.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
role: User, Admin,Developer
exl-id: b0ac587b-8592-4d37-9ce0-98a0859c367f
feature: Configuration,Rulesets
source-git-commit: 65af6e33ae3897519491952f4d3a6832700f77b2
workflow-type: tm+mt
source-wordcount: '760'
ht-degree: 0%

---

# Utilizzare i set di regole per trasformare gli URL {#using-rulesets-to-transform-urls}

Puoi distribuire i set di regole in Dynamic Media per trasformare gli URL. I set di regole sono insiemi di istruzioni scritte in un linguaggio di script (ad esempio JavaScript) che valutano i dati XML e eseguono determinate azioni se tali dati soddisfano determinate condizioni. Ogni regola consiste di almeno una condizione e almeno un&#39;azione. Una regola valuta i dati XML in base alle condizioni e, se una condizione viene soddisfatta, esegue l&#39;azione appropriata. Esempi di set di regole includono:

* Aggiunta di un suffisso di tipo MIME. Molti servizi e siti web richiedono suffissi di immagini, ad esempio l’aggiunta di `.jpg` a un URL.
* Creazione di un percorso di cartella per l’URL a scopo di ottimizzazione SEO (Search Engine Optimization).

   Consulta [Come Adobe Dynamic Media Classic supporta SEO](/help/assets/assets/s7_seo.pdf).

* Aggiunta di metadati all’URL per scopi SEO (Search Engine Optimization).

   Consulta [Come Adobe Dynamic Media Classic supporta SEO](/help/assets/assets/s7_seo.pdf).

* Impostazione della disposizione dei contenuti per attivare un download.
* Semplificare gli URL dei modelli di Image Server per la personalizzazione. Ad esempio, trasforma `rgb{XX,YY,ZZ}` in RTF-ready `\redXX\greenYY\blueZZ`

* Richiedi la codifica di alcuni caratteri, ad esempio `$`, `{` e `}`, e di alcuni caratteri da decodificare in ImageServer. Ad esempio, Facebook non funziona bene con gli URL contenenti caratteri speciali.

   Consulta [Rimuovere i caratteri speciali dagli URL](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/remove-special-characters-urls.html).

Nel contesto di Dynamic Media, i siti web che utilizzano un sistema basato su XML per gestire le informazioni sulle risorse possono caricare file XML in Dynamic Media. Puoi designare uno di questi file come file del set di regole di pre-elaborazione per il serving della risorsa Dynamic Media. Questo file ristruttura il formato del protocollo URL standard per soddisfare la logica di business dei sistemi che vengono integrati con Dynamic Media. È possibile specificare un file XML da utilizzare come percorso del file delle definizioni del set di regole.

>[!CAUTION]
>
>Prestare attenzione quando si utilizzano i set di regole; possono impedire la visualizzazione del contenuto Dynamic Media sul sito web.

Sono disponibili set di regole di esempio che possono essere utili per creare un set di regole personalizzato.
Consulta [Riferimento set di regole](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/rule-set-reference/c-rule-set-reference.html).

Come per la creazione di tutti i set di regole, assicurati che il file XML sia valido prima di caricarlo utilizzando un programma di convalida XML come xmlvalid.
Vedi anche [Risolvere i problemi relativi ai set di regole](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/scene7-ruleset-troubleshooting.html).

Inoltre, verifica prima il set di regole in un ambiente di staging che non influisce sull’ambiente di produzione live.
Gli ambienti di produzione e gli ambienti di staging in genere richiedono accessi diversi.

Per informazioni sull&#39;accesso, consulta l&#39; [applicazione desktop Adobe Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#sign-in-dmc-app).

<!-- OBSOLETE INFORMATION * **NA staging environment** login page: [https://s7sps1-staging.scene7.com/IpsWeb/](https://s7sps1-staging.scene7.com/IpsWeb/)
* **EMEA staging environment** login page: [https://s7sps3-staging.scene7.com/IpsWeb/](https://s7sps3-staging.scene7.com/IpsWeb/)
* **JAPAC staging environment** login page: [https://s7sps5-staging.scene7.com/IpsWeb/](https://s7sps5-staging.scene7.com/IpsWeb/) -->

Vedi anche [Usa immagine &#39;asset&#39; invece di &#39;is&#39; in un set di regole](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/ruleset-asset-instead-image.html).

**Per distribuire i set di regole XML:**

1. Accedi alla tua [applicazione desktop Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#sign-in-dmc-app).

   Le credenziali e i dettagli di accesso sono stati forniti da Adobe al momento del provisioning. Se non disponi di tali informazioni, contatta l’Assistenza clienti Adobe.

1. Carica il file del set di regole facendo quanto segue:

   * Nella barra di navigazione globale, seleziona **[!UICONTROL Carica]**.
   * Nella pagina **[!UICONTROL Carica]**, vicino all&#39;angolo superiore sinistro, seleziona **[!UICONTROL Sfoglia]**.
   * Nella finestra di dialogo **[!UICONTROL Apri]**, individua il file del set di regole (XML).
   * Selezionare il file, quindi selezionare **[!UICONTROL Apri]**.
   * Sul lato destro della pagina **[!UICONTROL Carica]**, seleziona una cartella di destinazione per il file del set di regole.
   * Vicino alla parte inferiore della pagina, accertati che sia selezionato **[!UICONTROL Pubblica dopo il caricamento]** .
   * Nell’angolo in basso a destra della pagina, seleziona **[!UICONTROL Invia caricamento]**.
   * Nella barra di navigazione globale, seleziona **[!UICONTROL Processi]** per controllare lo stato del processo di caricamento. Quando la colonna **[!UICONTROL Stato]** nella pagina **[!UICONTROL Processo]** indica Caricamento completato, continua con i passaggi successivi.

1. Nella barra di navigazione vicino alla parte superiore della pagina, seleziona **[!UICONTROL Configurazione]** > **[!UICONTROL Impostazione applicazione]** > **[!UICONTROL Impostazioni pubblicazione]** > **[!UICONTROL Server immagini]**.
1. Nella pagina **[!UICONTROL Pubblicazione su Image Server]**, nel gruppo **[!UICONTROL Gestione catalogo]**, individua **[!UICONTROL Percorso file definizione set regole]**, quindi seleziona **[!UICONTROL Seleziona]**.
1. Nella pagina **[!UICONTROL Seleziona file definizione set regole (XML)]** , individua il file del set di regole, quindi seleziona **[!UICONTROL Seleziona]** nell’angolo inferiore destro della pagina.
1. Nell&#39;angolo in basso a destra della pagina Configurazione, selezionare **[!UICONTROL Chiudi]**.
1. Esegui un processo di pubblicazione su Image Server.

   Le condizioni del set di regole vengono applicate alle richieste ai server di immagini Dynamic Media live.

   Se modifichi il file del set di regole, le modifiche vengono applicate immediatamente quando ricarichi e ripubblichi il file del set di regole aggiornato.
