---
title: Utilizzo di set di regole per la trasformazione degli URL
description: Puoi distribuire i set di regole in Dynamic Medie per trasformare gli URL. I set di regole sono insiemi di istruzioni scritte in un linguaggio di script (ad esempio JavaScript) che valutano i dati XML e eseguono determinate azioni se tali dati soddisfano determinate condizioni.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
role: User, Admin,Developer
exl-id: b0ac587b-8592-4d37-9ce0-98a0859c367f
feature: Configuration,Rulesets
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '714'
ht-degree: 0%

---

# Utilizzare i set di regole per trasformare gli URL {#using-rulesets-to-transform-urls}

Puoi distribuire i set di regole in Dynamic Medie per trasformare gli URL. I set di regole sono insiemi di istruzioni scritte in un linguaggio di script (ad esempio JavaScript) che valutano i dati XML e eseguono determinate azioni se tali dati soddisfano determinate condizioni. Ogni regola è costituita da almeno una condizione e da almeno un&#39;azione. Una regola valuta i dati XML in base alle condizioni e, se una condizione viene soddisfatta, intraprende l&#39;azione appropriata. Di seguito sono riportati alcuni esempi di set di regole:

* Aggiunta di un suffisso di tipo MIME. Molti servizi e siti Web richiedono suffissi immagine, ad esempio l&#39;aggiunta di `.jpg` a un URL.
* Creazione di un percorso di cartella dell’URL a scopo di SEO (Search Engine Optimization).

  Consulta [Come Adobe Dynamic Media Classic supporta l’ottimizzazione SEO](/help/assets/assets/s7_seo.pdf).

* Aggiunta di metadati all’URL a scopo di SEO (Search Engine Optimization).

  Consulta [Come Adobe Dynamic Media Classic supporta l’ottimizzazione SEO](/help/assets/assets/s7_seo.pdf).

* Impostazione della disposizione del contenuto per attivare un download.
* Semplifica gli URL di modelli di Image Server per la personalizzazione. Ad esempio, girare `rgb{XX,YY,ZZ}` nell&#39;RTF-ready `\redXX\greenYY\blueZZ`

* Richiedi la codifica di alcuni caratteri, ad esempio `$`, `{`, e `}`e alcuni caratteri da decodificare in ImageServer. Ad esempio, Facebook non funziona bene con gli URL contenenti caratteri speciali.

  Consulta [Rimuovi caratteri speciali dagli URL](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/remove-special-characters-urls.html).

Nel contesto di Dynamic Medie, i siti Web che utilizzano un sistema basato su XML per gestire le informazioni sulle risorse possono caricare file XML in Dynamic Medie. Puoi designare uno di questi file come file del set di regole di pre-elaborazione per la gestione delle risorse Dynamic Medie. Questo file ristruttura il formato standard del protocollo URL per soddisfare la logica di business dei sistemi integrati con Dynamic Medie. Specificare un file XML da utilizzare come percorso del file delle definizioni del set di regole.

>[!CAUTION]
>
>Presta attenzione quando utilizzi i set di regole; possono impedire la visualizzazione del contenuto Dynamic Medie sul sito web.

Sono disponibili set di regole di esempio che consentono di creare set di regole personalizzati.
Consulta [Riferimento set di regole](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/rule-set-reference/c-rule-set-reference.html).

Come per la creazione di tutti i set di regole, prima di caricarli utilizzando un programma di convalida XML, ad esempio xmlvalid, accertarsi che il file XML sia valido.
Vedi anche [Risoluzione dei problemi dei set di regole](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/scene7-ruleset-troubleshooting.html).

Inoltre, assicurati di eseguire il test del set di regole in un ambiente di staging che non influisce sull’ambiente di produzione live.
In genere, gli ambienti di produzione e quelli di staging richiedono accessi diversi.

Consulta la [applicazione desktop Adobe Dynamic Media Classic per informazioni di accesso](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#sign-in-dmc-app).

<!-- OBSOLETE INFORMATION * **NA staging environment** login page: [https://s7sps1-staging.scene7.com/IpsWeb/](https://s7sps1-staging.scene7.com/IpsWeb/)
* **EMEA staging environment** login page: [https://s7sps3-staging.scene7.com/IpsWeb/](https://s7sps3-staging.scene7.com/IpsWeb/)
* **JAPAC staging environment** login page: [https://s7sps5-staging.scene7.com/IpsWeb/](https://s7sps5-staging.scene7.com/IpsWeb/) -->

Vedi anche [Utilizzare l’immagine &quot;asset&quot; invece di &quot;is&quot; in un set di regole](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/ruleset-asset-instead-image.html).

**Per distribuire i set di regole XML:**

1. Accedi al tuo [applicazione desktop Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#sign-in-dmc-app).

   Le credenziali e i dettagli di accesso sono stati forniti da Adobe al momento del provisioning. Se non disponi di queste informazioni, contatta l’Assistenza clienti Adobe.

1. Carica il file del set di regole effettuando le seguenti operazioni:

   * Sulla barra di navigazione globale, seleziona **[!UICONTROL Carica]**.
   * Il giorno **[!UICONTROL Carica]** nell&#39;angolo superiore sinistro, selezionare **[!UICONTROL Sfoglia]**.
   * In **[!UICONTROL Apri]** , passare al file del set di regole (XML).
   * Seleziona il file, quindi seleziona **[!UICONTROL Apri]**.
   * Sul lato destro del **[!UICONTROL Carica]** , selezionare una cartella di destinazione per il file del set di regole.
   * Nella parte inferiore della pagina, assicurati che **[!UICONTROL Pubblica dopo il caricamento]** è selezionato.
   * Nell’angolo inferiore destro della pagina, seleziona **[!UICONTROL Invia caricamento]**.
   * Sulla barra di navigazione globale, seleziona **[!UICONTROL Processi]** per controllare lo stato del processo di caricamento. Quando **[!UICONTROL Stato]** colonna sulla **[!UICONTROL Processo]** pagina indica Caricamento completato, continua con i passaggi successivi.

1. Nella barra di spostamento nella parte superiore della pagina, seleziona **[!UICONTROL Configurazione]** > **[!UICONTROL Impostazione applicazione]** > **[!UICONTROL Impostazione pubblicazione]** > **[!UICONTROL Server immagini]**.
1. Il giorno **[!UICONTROL Pubblicazione server immagini]** pagina, sotto **[!UICONTROL Gestione catalogo]** gruppo, individua **[!UICONTROL Percorso file definizione set regole]**, quindi seleziona **[!UICONTROL Seleziona]**.
1. Il giorno **[!UICONTROL Seleziona file definizione set regole (XML)]** , individua il file del set di regole e, nell’angolo inferiore destro della pagina, seleziona **[!UICONTROL Seleziona]**.
1. Nell’angolo inferiore destro della pagina Setup, seleziona **[!UICONTROL Chiudi]**.
1. Esegui un processo di pubblicazione su Image Server.

   Le condizioni del set di regole vengono applicate alle richieste ai server immagini Dynamic Medie live.

   Se modifichi il file del set di regole, le modifiche vengono immediatamente applicate quando ricarichi e ripubblichi il file del set di regole aggiornato.
