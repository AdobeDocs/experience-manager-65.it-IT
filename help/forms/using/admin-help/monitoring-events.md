---
title: Monitoraggio degli eventi
seo-title: Monitoraggio degli eventi
description: Quando la funzionalità di controllo è abilitata, la protezione dei documenti consente di monitorare determinati tipi di eventi. È possibile cercare e ordinare facilmente l'elenco degli eventi utilizzando la protezione del documento.
seo-description: Quando la funzionalità di controllo è abilitata, la protezione dei documenti consente di monitorare determinati tipi di eventi. È possibile cercare e ordinare facilmente l'elenco degli eventi utilizzando la protezione del documento.
uuid: 22add6ff-536d-4cb9-8eac-b72cad5c3ecf
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 379957bf-0634-4182-b269-1b010da4c90f
translation-type: tm+mt
source-git-commit: 2cf9dcf2e9cf71c54e19e2c6ee825c9a8f00a9b7
workflow-type: tm+mt
source-wordcount: '989'
ht-degree: 0%

---


# Eventi di monitoraggio {#monitoring-events}

Quando la funzionalità di controllo è abilitata, la protezione dei documenti consente di monitorare determinati tipi di eventi. Gli eventi visibili dipendono dal tuo ruolo:

**Utenti:** Può visualizzare gli eventi sottoposti a controllo per i documenti protetti tramite criterio e per tutti i documenti protetti che ricevono e utilizzano.

**Coordinatori set di criteri:** È possibile visualizzare gli eventi sottoposti a controllo, compresi gli eventi dei documenti e dei criteri, per i documenti protetti dai criteri dai relativi set di criteri.

**Amministratori:** può visualizzare gli eventi sottoposti a controllo correlati a tutti i documenti e gli utenti protetti tramite criterio. Gli amministratori possono inoltre tenere traccia di altri tipi di eventi, inclusi eventi utente, documenti, criteri ed eventi di sistema.

>[!NOTE]
>
>Gli eventi eseguiti su una copia di un documento protetto tramite criterio vengono inoltre tracciati come eventi nel documento protetto originale.

(Vedere [Opzioni di controllo degli eventi](/help/forms/using/admin-help/configuring-client-server-options.md#event-auditing-options).)

Un evento non riuscito viene registrato se un utente non autorizzato tenta di visualizzare un documento o tenta di accedere utilizzando un nome utente o una password non corretti.

>[!NOTE]
>
>Se un criterio viene modificato per rimuovere l&#39;accesso anonimo, è possibile registrare eventi di accesso anonimo non riusciti per i documenti. Quando un destinatario autorizzato tenta di accedere a un documento protetto dai criteri modificati, viene comunque tentato di accedere in modo anonimo ma non sarà possibile.

Se un criterio consente l&#39;accesso anonimo degli utenti, ma successivamente l&#39;amministratore disattiva l&#39;accesso anonimo per la protezione dei documenti, l&#39;accesso anonimo non riuscirà per i documenti protetti tramite il criterio e l&#39;evento non verrà registrato.

## Abilita controllo eventi {#enable-event-auditing}

Per eseguire il controllo degli eventi, è necessario soddisfare i seguenti requisiti di configurazione:

* Il sistema o l&#39;amministratore deve abilitare la funzionalità di controllo per il server.

   (Vedere [Configurazione del controllo degli eventi e delle impostazioni di privacy](/help/forms/using/admin-help/configuring-client-server-options.md#configuring-event-auditing-and-privacy-settings).)

* Il criterio utilizzato per proteggere il documento deve avere il controllo abilitato. (Vedere [Creazione e modifica di criteri](/help/forms/using/admin-help/creating-policies.md#creating-and-editing-policies).)

## Cerca un evento {#search-for-an-event}

È possibile ricercare l&#39;elenco degli eventi e visualizzare descrizioni più dettagliate degli eventi. Le descrizioni dettagliate includono informazioni quali l&#39;ID dell&#39;evento, la descrizione, l&#39;indirizzo IP, l&#39;organizzazione, la data e l&#39;ora in cui si è verificato l&#39;evento, le attività negate e gli eventi offline (quando gli utenti tentano di utilizzare un documento quando non sono connessi alla protezione del documento).

Potete cercare gli eventi nella pagina Eventi utilizzando una combinazione di criteri di ricerca degli eventi e delle date in cui si sono verificati. Gli eventi che potete cercare dipendono dal vostro ruolo:

**Utenti:** Può visualizzare gli eventi sottoposti a controllo per i documenti protetti tramite criterio e per tutti i documenti protetti che ricevono e utilizzano. Sono disponibili le seguenti opzioni di ricerca:

**Eventi correlati a me:** Gli utenti possono trovare eventi per qualsiasi documento protetto tramite criterio creato o ricevuto. Ad esempio, se un utente apre, visualizza o stampa un documento protetto da un&#39;altra persona, l&#39;utente visualizza solo questi eventi per tale documento.

**Eventi relativi ai documenti:** gli utenti possono trovare tutti gli eventi correlati ai propri documenti protetti tramite criterio. Gli utenti visualizzano gli eventi generati da ogni persona che ha gestito i propri documenti.

**Coordinatori set di criteri:** È possibile visualizzare gli eventi sottoposti a controllo, compresi gli eventi dei documenti e dei criteri, per i documenti protetti dai criteri dai relativi set di criteri. Le opzioni disponibili sono:

**Eventi del documento in cui sono un coordinatore del set di criteri:i coordinatori dei set di** criteri che dispongono dell&#39;autorizzazione per l&#39;evento di visualizzazione possono trovare eventi correlati a documenti protetti dai relativi set di criteri.

**Eventi dei criteri in cui sono un coordinatore dei set di criteri:i coordinatori dei set di** criteri che dispongono dell&#39;autorizzazione per gli eventi di visualizzazione possono trovare gli eventi correlati ai criteri dai rispettivi set di criteri.

**Amministratori:** può visualizzare gli eventi sottoposti a controllo correlati a tutti i documenti e gli utenti protetti tramite criterio. Gli amministratori possono anche tenere traccia di altri tipi. Inoltre, gli amministratori possono suddividere ulteriormente le ricerche degli eventi in base al tipo di utente:

**Utenti noti:** gli utenti si trovano nelle directory di origine o sono registrati come utenti esterni.

**Utenti anonimi:utenti** sconosciuti che accedono a un documento protetto da un criterio che consente l&#39;accesso anonimo.

**Utenti del sistema:eventi generati dal** server, ad esempio la sincronizzazione di una directory.

1. Nella pagina di protezione del documento, fare clic su Eventi.
1. Nell’elenco Trova, selezionare i criteri di ricerca da utilizzare. A seconda della selezione nell’elenco Trova, viene visualizzato un secondo elenco che fornisce criteri di ricerca aggiuntivi. Se applicabile, nella casella di testo digitare i criteri di ricerca.

   Per ulteriori dettagli sui tipi di evento specifici, vedere [Opzioni di controllo degli eventi](/help/forms/using/admin-help/configuring-client-server-options.md#event-auditing-options).

1. Nell’elenco Utente, selezionate il tipo di utente che ha eseguito l’evento:

   * Se selezionate Utente noto, viene visualizzata una seconda casella di ricerca in cui è necessario digitare il nome utente o l&#39;indirizzo e-mail dell&#39;utente.
   * Se non si conoscono questi valori, fare clic sull’icona di ricerca Rubrica per cercare l’utente in base al nome utente o all’indirizzo e-mail.

1. Nell&#39;elenco Data, selezionare un&#39;opzione relativa all&#39;intervallo di date. Se si seleziona Data personalizzata, vengono visualizzate delle caselle in cui è possibile digitare la data nel formato aaaa/mm/gg, oppure è possibile utilizzare il selettore data per specificare l&#39;intervallo di date:

   * Fate clic sul calendario per aprire il selettore data.
   * Usate le frecce per trovare un anno e un mese.
   * Fare clic su un giorno del mese nel calendario.
   * Fate clic su OK per chiudere il selettore data.

1. Nell&#39;elenco Visualizza, selezionare il numero di risultati di ricerca da visualizzare per pagina.
1. Fate clic su Trova.

   Tutti gli eventi con errore vengono evidenziati nell&#39;elenco con un&#39;icona rifiutata.

1. Per visualizzare i dettagli relativi a un evento, fate clic sulla descrizione dell&#39;evento nell&#39;elenco.

## Ordinare l&#39;elenco eventi {#sort-the-event-list}

Potete ordinare l’elenco degli eventi per intestazione di colonna per individuare più facilmente gli eventi. Le icone a triangolo accanto all’intestazione della colonna indicano quale colonna è attualmente utilizzata per l’ordinamento. Un triangolo rivolto verso l’alto indica l’ordine crescente, mentre un triangolo rivolto verso il basso indica l’ordine decrescente.

1. Fare clic sull&#39;intestazione di colonna appropriata.
1. Per modificare l’ordinamento, fate di nuovo clic sull’intestazione della colonna.

