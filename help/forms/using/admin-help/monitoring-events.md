---
title: Monitoraggio degli eventi
description: Quando la funzionalità di controllo è abilitata, la protezione dei documenti consente di monitorare determinati tipi di eventi. Puoi cercare e ordinare facilmente l’elenco degli eventi utilizzando Document Security.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: Document Security
exl-id: 078b9ad1-16e2-40f4-92dc-e4093c0bb6ac
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '958'
ht-degree: 0%

---

# Monitoraggio degli eventi {#monitoring-events}

Quando la funzionalità di controllo è abilitata, la protezione dei documenti consente di monitorare determinati tipi di eventi. Gli eventi visibili dipendono dal ruolo:

**Utenti:** possono visualizzare eventi controllati per i documenti protetti tramite policy e per tutti i documenti protetti ricevuti e utilizzati.

**Coordinatori set di criteri:** possono visualizzare eventi controllati, inclusi eventi di documenti e criteri, per i documenti protetti da criteri dai relativi set di criteri.

**Amministratori:** possono visualizzare eventi controllati correlati a tutti i documenti e gli utenti protetti tramite policy. Gli amministratori possono inoltre tenere traccia di altri tipi di eventi, tra cui eventi utente, documento, criteri e di sistema.

>[!NOTE]
>
>Anche gli eventi eseguiti su una copia di un documento protetto tramite policy vengono tracciati come eventi nel documento protetto originale.

(Vedi [Opzioni di controllo degli eventi](/help/forms/using/admin-help/configuring-client-server-options.md#event-auditing-options).)

Se un utente non autorizzato tenta di visualizzare un documento o di accedere utilizzando un nome utente o una password non corretti, viene registrato un evento di errore.

>[!NOTE]
>
>Gli eventi di accesso anonimo non riusciti per i documenti possono essere registrati se viene modificato un criterio per rimuovere l&#39;accesso anonimo. Quando un destinatario autorizzato tenta di accedere a un documento protetto dalla policy modificata, viene effettuato un tentativo di accesso anonimo, ma l’operazione non riesce.

Se una policy consente l’accesso anonimo ma l’amministratore disattiva successivamente tale accesso per la sicurezza dei documenti, l’accesso anonimo non riuscirà per i documenti protetti con la policy e l’evento non verrà registrato.

## Abilita controllo eventi {#enable-event-auditing}

Affinché il controllo degli eventi abbia luogo, è necessario soddisfare i seguenti requisiti di configurazione:

* Il sistema o l&#39;amministratore devono abilitare la funzionalità di controllo per il server.

  (Vedi [Configurazione del controllo degli eventi e delle impostazioni di privacy](/help/forms/using/admin-help/configuring-client-server-options.md#configuring-event-auditing-and-privacy-settings).)

* Il controllo deve essere abilitato per il criterio utilizzato per proteggere il documento. (Vedi [Creazione e modifica dei criteri](/help/forms/using/admin-help/creating-policies.md#creating-and-editing-policies).)

## Cercare un evento {#search-for-an-event}

Puoi cercare nell’elenco degli eventi e visualizzare descrizioni più dettagliate sugli eventi. Le descrizioni dettagliate includono informazioni quali l’ID evento, la descrizione, l’indirizzo IP, l’organizzazione, l’utente interessato, la data e l’ora in cui si è verificato l’evento, le attività negate ed eventi offline (quando gli utenti tentano di utilizzare un documento quando non sono connessi alla protezione dei documenti).

È possibile cercare gli eventi nella pagina Eventi utilizzando una combinazione di criteri di ricerca degli eventi e le date in cui si sono verificati. Gli eventi che puoi cercare dipendono dal tuo ruolo:

**Utenti:** possono visualizzare eventi controllati per i documenti protetti tramite policy e per tutti i documenti protetti ricevuti e utilizzati. Sono disponibili le seguenti opzioni di ricerca:

**Eventi correlati
per me:** Gli utenti possono trovare eventi per qualsiasi documento protetto tramite policy che hanno creato o ricevuto. Ad esempio, se un utente apre, visualizza o stampa un documento protetto da un’altra persona, vedrà solo questi eventi per quel documento.

**Eventi correlati ai miei documenti:** Gli utenti possono trovare tutti gli eventi correlati ai propri documenti protetti tramite policy. Gli utenti visualizzano gli eventi generati da ogni persona che ha gestito i propri documenti.

**Coordinatori set di criteri:** possono visualizzare eventi controllati, inclusi eventi di documenti e criteri, per i documenti protetti da criteri dai relativi set di criteri. Sono disponibili le seguenti opzioni:

**Eventi documento in cui
Sono un coordinatore di set di criteri:** I coordinatori di set di criteri che dispongono dell&#39;autorizzazione Visualizza evento possono trovare eventi correlati a documenti protetti dai propri set di criteri.

**Eventi dei criteri per i quali sono un coordinatore di set di criteri:** I coordinatori di set di criteri che dispongono dell&#39;autorizzazione di visualizzazione eventi possono trovare eventi correlati ai criteri dai propri set di criteri.

**Amministratori:** possono visualizzare eventi controllati correlati a tutti i documenti e gli utenti protetti tramite policy. Gli amministratori possono anche tenere traccia di altri tipi. Inoltre, gli amministratori possono suddividere ulteriormente le ricerche degli eventi in base al tipo di utente:

**Utenti noti:** Gli utenti si trovano nelle directory di origine o sono registrati come utenti esterni.

**Utenti anonimi:** Utenti sconosciuti che accedono a un documento protetto con un criterio che consente l&#39;accesso anonimo.

**Utenti di sistema:** eventi avviati dal server, ad esempio la sincronizzazione della directory.

1. Nella pagina Document Security, fai clic su Eventi.
1. Nell&#39;elenco Trova selezionare i criteri di ricerca che si desidera utilizzare. A seconda della selezione effettuata nell&#39;elenco Trova, viene visualizzato un secondo elenco che fornisce criteri di ricerca aggiuntivi. Se applicabile, nella casella di testo digitare i criteri di ricerca.

   Per ulteriori dettagli sui tipi di evento specifici, vedere [Opzioni di controllo eventi](/help/forms/using/admin-help/configuring-client-server-options.md#event-auditing-options).

1. Nell&#39;elenco Utente selezionare il tipo di utente che ha eseguito l&#39;evento:

   * Se si seleziona Utente noto, viene visualizzata una seconda casella di ricerca in cui è necessario digitare il nome utente o l&#39;indirizzo di posta elettronica dell&#39;utente.
   * Se non si conoscono questi valori, fare clic sull&#39;icona di ricerca della Rubrica per cercare l&#39;utente in base al nome utente o all&#39;indirizzo di posta elettronica.

1. Nell’elenco Data, seleziona un’opzione di intervallo di date. Se selezioni Date personalizzate, vengono visualizzate delle caselle in cui si digita la data nel formato aaaa/mm/gg oppure è possibile utilizzare il Selettore data per specificare l’intervallo di date:

   * Fai clic sul calendario per aprire il Selettore data.
   * Utilizzare le frecce per trovare un anno e un mese.
   * Fare clic su un giorno del mese nel calendario.
   * Fare clic su OK per chiudere il selettore data.

1. Nell&#39;elenco Visualizza selezionare il numero di risultati di ricerca da visualizzare per pagina.
1. Fai clic su Trova.

   Eventuali eventi non riusciti vengono evidenziati nell’elenco con un’icona Negato.

1. Per visualizzare i dettagli di un evento, fare clic sulla descrizione dell&#39;evento nell&#39;elenco.

## Ordinare l’elenco degli eventi {#sort-the-event-list}

Per trovare gli eventi in modo più semplice, puoi ordinare l’elenco degli eventi in base all’intestazione della colonna. Le icone triangolari accanto all’intestazione della colonna indicano la colonna attualmente utilizzata per l’ordinamento. Un triangolo rivolto verso l&#39;alto indica un ordine crescente, mentre un triangolo rivolto verso il basso indica un ordine decrescente.

1. Fare clic sull&#39;intestazione di colonna appropriata.
1. Per modificare l’ordinamento, fai di nuovo clic sull’intestazione della colonna.
