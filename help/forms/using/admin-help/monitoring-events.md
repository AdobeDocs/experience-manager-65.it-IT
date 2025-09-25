---
title: Monitoraggio degli eventi
description: Quando la funzionalità di auditing è abilitata, la protezione dei documenti consente di monitorare determinati tipi di eventi. È possibile cercare e classificare facilmente l’elenco degli eventi utilizzando la protezione dei documenti.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: Document Security
exl-id: 078b9ad1-16e2-40f4-92dc-e4093c0bb6ac
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: ht
source-wordcount: '958'
ht-degree: 100%

---

# Monitoraggio degli eventi {#monitoring-events}

Quando la funzionalità di auditing è abilitata, la protezione dei documenti consente di monitorare determinati tipi di eventi. Gli eventi visualizzati dipendono dal ruolo:

**Utenti:** possono visualizzare eventi sottoposti ad audit per i documenti protetti tramite criteri e per tutti i documenti protetti ricevuti e utilizzati.

**Coordinatori set di criteri:** possono visualizzare eventi sottoposti ad audit, inclusi eventi relativi a documenti e criteri, per i documenti protetti da criteri dai relativi set di criteri.

**Amministratori:** possono visualizzare eventi controllati correlati a tutti i documenti e gli utenti protetti tramite criteri. Gli amministratori possono inoltre tenere traccia di altri tipi di eventi, tra cui eventi utente, documento, criteri e di sistema.

>[!NOTE]
>
>Anche gli eventi eseguiti su una copia di un documento protetto tramite criteri vengono tracciati come eventi nel documento protetto originale.

(Consulta [Opzioni di auditing degli eventi](/help/forms/using/admin-help/configuring-client-server-options.md#event-auditing-options).)

Se un utente non autorizzato tenta di visualizzare un documento o di accedere utilizzando un nome utente o una password non corretti, viene registrato un evento di errore.

>[!NOTE]
>
>Gli eventi di accesso anonimo non riusciti per i documenti possono essere registrati se viene modificato un criterio per la rimozione dell’accesso anonimo. Quando un destinatario autorizzato tenta di accedere a un documento protetto dalla criterio modificato, viene effettuato un tentativo di accesso anonimo, ma l’operazione avrà esito negativo.

Se un criterio consente l’accesso anonimo ma l’amministratore disattiva successivamente tale accesso per la protezione dei documenti, l’accesso anonimo avrà esito negativo per i documenti protetti tramite criteri e l’evento non verrà registrato.

## Abilitare l’auditing degli eventi {#enable-event-auditing}

Affinché l’auditing degli eventi si verifichi, è necessario soddisfare i seguenti requisiti di configurazione:

* Il sistema o l’amministratore devono abilitare la funzionalità di auditing per il server.

  (Consulta [Configurazione dell’auditing degli eventi e delle impostazioni di privacy](/help/forms/using/admin-help/configuring-client-server-options.md#configuring-event-auditing-and-privacy-settings).)

* L’auditing deve essere abilitato per il criterio utilizzato per la protezione del documento. (Consulta [Creazione e modifica dei criteri](/help/forms/using/admin-help/creating-policies.md#creating-and-editing-policies).)

## Ricerca di un evento {#search-for-an-event}

È possibile cercare nell’elenco degli eventi e visualizzare descrizioni più dettagliate sugli stessi. Le descrizioni dettagliate includono informazioni quali l’ID evento, la descrizione, l’indirizzo IP, l’organizzazione, l’utente interessato, la data e l’ora in cui si è verificato l’evento, le attività negate ed eventi offline (quando gli utenti tentano di utilizzare un documento se non sono connessi alla protezione dei documenti).

È possibile cercare gli eventi nella pagina Eventi utilizzando una combinazione di criteri di ricerca degli eventi e le date in cui si sono verificati. Gli eventi che si possono cercare dipendono dal proprio ruolo:

**Utenti:** possono visualizzare eventi controllati per i documenti protetti tramite criteri e per tutti i documenti protetti ricevuti e utilizzati. Sono disponibili le seguenti opzioni di ricerca:

**Eventi correlati
a me:** gli utenti possono trovare eventi per qualsiasi documento protetto tramite criteri che hanno creato o ricevuto. Ad esempio, se un utente apre, visualizza o stampa un documento protetto da un’altra persona, visualizzerà solo questi eventi per quel documento.

**Eventi correlati ai miei documenti:** gli utenti possono trovare tutti gli eventi correlati ai propri documenti protetti tramite citeri. Gli utenti visualizzano gli eventi generati da ogni persona che ha gestito i propri documenti.

**Coordinatori set di criteri:** possono visualizzare eventi controllati, inclusi eventi relativi a documenti e criteri, per i documenti protetti da criteri dai relativi set di criteri. Sono disponibili le seguenti opzioni:

**Eventi documento in cui
Sono un coordinatore di set di criteri:** i coordinatori di set di criteri che dispongono dell’autorizzazione Visualizza evento possono trovare eventi correlati a documenti protetti dai propri set di criteri.

**Eventi dei criteri per i quali sono un coordinatore di set di criteri:** i coordinatori di set di criteri che dispongono dell’autorizzazione di visualizzazione eventi possono trovare eventi correlati ai criteri dai propri set di criteri.

**Amministratori:** possono visualizzare eventi controllati correlati a tutti i documenti e gli utenti protetti tramite criteri. Gli amministratori possono anche monitorare altre tipologie. Inoltre, gli amministratori possono suddividere ulteriormente le ricerche degli eventi in base al tipo di utente:

**Utenti noti:** gli utenti si trovano nelle directory di origine o sono registrati come utenti esterni.

**Utenti anonimi:** utenti sconosciuti che accedono a un documento protetto con un criterio che consente l’accesso anonimo.

**Utenti di sistema:** eventi avviati dal server, ad esempio la sincronizzazione della directory.

1. Nella pagina Protezione dei documenti, fai clic su Eventi.
1. Nell’elenco Trova, seleziona i criteri di ricerca da utilizzare. A seconda della selezione effettuata nell’elenco Trova, viene visualizzato un secondo elenco che fornisce criteri di ricerca aggiuntivi. Se applicabile, digita i criteri di ricerca nella casella di testo.

   Per ulteriori dettagli sui tipi di evento specifici, consulta [Opzioni di auditing degli eventi](/help/forms/using/admin-help/configuring-client-server-options.md#event-auditing-options).

1. Nell’elenco Utente seleziona il tipo di utente che ha eseguito l’evento:

   * Se selezioni Utente noto, viene visualizzata una seconda casella di ricerca in cui è necessario digitare il nome utente o l’indirizzo e-mail dell’utente.
   * Se non conosci questi valori, fai clic sull’icona di ricerca della Rubrica per cercare l’utente in base al nome utente o all’indirizzo di posta elettronica.

1. Nell’elenco Data, seleziona un’opzione di intervallo di date. Se selezioni Date personalizzate, vengono visualizzate delle caselle in cui digitare la data nel formato gg/mm/aaaa oppure puoi utilizzare il Selettore data per specificare l’intervallo di date:

   * Fai clic sul calendario per aprire il Selettore data.
   * Usa le frecce per trovare un anno e un mese.
   * Fai clic su un giorno del mese nel calendario.
   * Fai clic su OK per chiudere il Selettore data.

1. Nell’elenco Visualizza, seleziona il numero di risultati di ricerca da visualizzare per pagina.
1. Fai clic su Trova.

   Eventuali eventi non riusciti vengono evidenziati nell’elenco con un’icona barrata.

1. Per visualizzare i dettagli di un evento, fare clic sulla descrizione dell’evento nell’elenco.

## Ordinare l’elenco degli eventi {#sort-the-event-list}

Per trovare gli eventi in modo più semplice, puoi ordinare l’elenco degli eventi in base all’intestazione della colonna. Le icone triangolari accanto all’intestazione della colonna indicano la colonna attualmente utilizzata per l’ordinamento. Un triangolo rivolto verso l’alto indica un ordine crescente, mentre un triangolo rivolto verso il basso indica un ordine decrescente.

1. Fai clic sull’intestazione di colonna appropriata.
1. Per modificare l’ordinamento, fai di nuovo clic sull’intestazione della colonna.
