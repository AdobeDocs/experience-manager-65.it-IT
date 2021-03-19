---
title: Gestione degli account utente invitati e locali
seo-title: Gestione degli account utente invitati e locali
description: Utilizzando la protezione dei documenti, puoi cercare, visualizzare, modificare, bloccare, sbloccare ed eliminare gli account utente invitati e locali.
seo-description: Utilizzando la protezione dei documenti, puoi cercare, visualizzare, modificare, bloccare, sbloccare ed eliminare gli account utente invitati e locali.
uuid: 0d0c717a-6e6e-4e42-96eb-3a7166e215ab
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 65720eed-ab06-463f-9567-2fdc468b6219
feature: Sicurezza dei documenti
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1222'
ht-degree: 0%

---


# Gestione degli account utente invitati e locali {#managing-invited-and-local-user-accounts}

Utilizza la pagina Utenti invitati e locali per gestire gli utenti invitati e locali. Questa pagina viene visualizzata solo se sono soddisfatti i seguenti requisiti:

* L’utente è un amministratore a cui vengono assegnati il ruolo Gestione utenti invitati e locali e il ruolo Utente della console di amministrazione. (Consulta [Creazione e configurazione di ruoli](/help/forms/using/admin-help/creating-configuring-roles.md#creating-and-configuring-roles).)
* La registrazione degli utenti invitati è abilitata. (Consulta [Configurazione della registrazione utente invitata](/help/forms/using/admin-help/configuring-client-server-options.md#configuring-invited-user-registration).)

La pagina Utenti invitati e locali contiene due schede che è possibile utilizzare per cercare, visualizzare, modificare, bloccare, sbloccare ed eliminare gli account utente invitati e locali.

Puoi anche inviare manualmente le e-mail di registrazione agli utenti invitati. Puoi eseguire questa operazione, ad esempio, se il periodo di registrazione che l’e-mail autorizzata termina e l’utente non può utilizzare l’URL per la registrazione. In questo caso, puoi inviare nuovamente un’e-mail di registrazione all’utente invitato. Quando l&#39;utente invitato registra e attiva l&#39;account, l&#39;utente diventa un utente locale.

>[!NOTE]
>
>Gli utenti invitati possono anche essere aggiunti direttamente tramite la directory LDAP che documenta i riferimenti alla sicurezza, o quando un utente o un amministratore invita un nuovo utente durante la creazione o la modifica di un criterio, avviando quindi un&#39;e-mail di invito alla registrazione. Gli utenti possono aggiungere nuovi utenti invitati ai criteri se si abilita l&#39;opzione Abilita registrazione utenti invitati nella pagina Registrazione utenti invitati .

## Aggiungi un utente invitato {#add-an-invited-user}

È possibile aggiungere uno o più account utente invitati per la protezione dei documenti alla volta. Per aggiungere un account utente invitato, è necessario l’indirizzo e-mail dell’utente. Quando si aggiunge un utente, la sicurezza dei documenti invia un messaggio e-mail di registrazione che invita l’utente a registrarsi.

1. Nella console di amministrazione, fai clic su Servizi > Sicurezza documenti > Utenti invitati e locali, quindi fai clic su Invita nuovo utente.
1. Digita gli indirizzi e-mail degli utenti che desideri invitare. Inserisci più indirizzi su una riga, separati da una virgola.

   Il messaggio creato quando si abilita la registrazione utente invitata viene inviato agli utenti. (Consulta [Configurazione della registrazione utente invitata](/help/forms/using/admin-help/configuring-client-server-options.md#configuring-invited-user-registration).)

1. Fai clic su OK.

## Visualizza informazioni su un utente locale {#view-information-about-a-local-user}

Puoi visualizzare informazioni sugli utenti locali, tra cui nome, indirizzo e-mail, organizzazione, stato di registrazione e dominio.

1. Nella console di amministrazione, fai clic su Servizi > Sicurezza documenti > Utenti invitati e locali, quindi fai clic su Invita nuovo utente.
1. Fare clic sulla scheda Utenti locali e, nella pagina Gestione utenti locali, fare clic sull&#39;indirizzo e-mail dell&#39;utente che si desidera visualizzare.

   Vengono visualizzati i dettagli utente ed è possibile reimpostare la password dell’utente e disattivare l’account.

## Invia un&#39;e-mail a un utente esterno non registrato {#send-an-email-to-an-unregistered-external-user}

Quando si aggiunge un utente invitato, la sicurezza dei documenti invia automaticamente all&#39;utente una richiesta di posta elettronica di registrazione. Puoi anche generare manualmente un messaggio e-mail di registrazione da inviare a un utente invitato che non si è ancora registrato. Puoi eseguire questa operazione, ad esempio, per inviare un nuovo invito se l’e-mail di registrazione di un utente invitato scade.

1. Nella console di amministrazione, fai clic su Servizi > Sicurezza documenti > Utenti invitati e locali.
1. Nell’elenco degli utenti, seleziona la casella di controllo a cui ogni utente deve inviare un messaggio e-mail di registrazione, quindi fai clic su Invia di nuovo e-mail di invito.
1. Esaminare l&#39;elenco degli utenti selezionati e fare clic su OK.

## Reimpostare una password utente locale {#reset-a-local-user-password}

È possibile reimpostare le password per gli utenti invitati che si sono registrati con la sicurezza dei documenti ma hanno dimenticato la password. Quando reattivi una password, viene generato un messaggio e-mail che contiene una nuova password temporanea per l’utente.

Quando hai attivato il processo di registrazione dell’utente invitato, hai creato un messaggio e-mail che verrà inviato agli utenti e richiesto loro di reimpostare le password. (Consulta [Configurazione della registrazione utente invitata](/help/forms/using/admin-help/configuring-client-server-options.md#configuring-invited-user-registration).)

1. Nella console di amministrazione, fai clic su Servizi > Sicurezza documenti > Utenti invitati e locali e fai clic sulla scheda Utenti locali .
1. Nell’elenco utenti, seleziona l’utente appropriato.
1. Nella pagina Gestisci utente locale fare clic su Ripristina password e quindi su OK. All’utente viene inviato un messaggio e-mail di reimpostazione della password contenente la nuova password.

## Attivare o disattivare un account utente {#enable-or-disable-a-user-account}

È possibile disattivare gli account utente locali per limitare temporaneamente l&#39;accesso di un utente alla protezione dei documenti. Quando si disabilita l&#39;account, l&#39;utente non può utilizzare documenti protetti da policy o creare o applicare criteri.

È possibile abilitare un account utente locale attualmente disabilitato. Non è possibile abilitare un account utente invitato elencato come registrato. Lo stato registrato indica che l’utente invitato è registrato ma non ha ancora attivato l’account utilizzando il collegamento presente nell’e-mail di attivazione.

**Limitare un account utente**

1. In Console di amministrazione, fai clic su Servizi > Protezione dei documenti > Utenti invitati e locali e fai clic sulla scheda Utenti locali .
1. Nell’elenco utenti, seleziona l’utente appropriato.
1. Nella pagina Dettagli utente locale fare clic su Disattiva account.

**Ripristino di un account utente**

1. Fare clic su Utenti invitati e locali, quindi fare clic sulla scheda Utenti locali.
1. Nell’elenco utenti, seleziona l’utente appropriato.
1. Nella pagina Dettagli utente locale fare clic su Attiva account.

## Rimuovere un account utente invitato {#remove-an-invited-user-account}

È possibile eliminare gli account utente invitati dalla protezione dei documenti. Ad esempio, puoi eliminare un account quando un utente modifica le informazioni sul proprio account e-mail personale.

Se elimini un account utente, solo l’utente o un altro amministratore può reinstallare l’account selezionando l’opzione Aggiungi utente invitato nella pagina Utenti invitati . Gli utenti non possono aggiungere l&#39;account utente eliminato a un criterio e tale metodo non consente di avviare alcun processo di invito.

>[!NOTE]
>
>Gli utenti invitati che sono stati eliminati tramite l’interfaccia di gestione utenti dei moduli AEM non possono essere nuovamente invitati finché non sono stati nuovamente eliminati utilizzando la seguente procedura.

1. Nella console di amministrazione, fai clic su Servizi > Sicurezza documenti > Utenti invitati e locali e fai clic sulla scheda Utenti invitati .
1. Selezionare la casella di controllo accanto a uno o più utenti, fare clic su Elimina e quindi su OK.

## Cerca un account utente invitato {#search-for-an-invited-user-account}

Puoi cercare gli account utente invitati utilizzando un indirizzo e-mail.

1. Nella console di amministrazione, fai clic su Servizi > Sicurezza documenti > Utenti invitati e locali.
1. Nella casella Trova e-mail digitare l’indirizzo e-mail dell’utente e quindi fare clic su Trova.

## Cerca un account utente locale {#search-for-a-local-user-account}

Puoi cercare un utente locale utilizzando l’indirizzo e-mail o il nome e il dominio dell’utente.

1. Nella console di amministrazione, fai clic su Servizi > Sicurezza documenti > Utenti invitati e locali e fai clic sulla scheda Utenti locali .
1. Digitare i criteri di ricerca nella casella Trova, selezionare Nome o E-mail, quindi fare clic su Trova.

## Rimuovere un account utente locale {#remove-a-local-user-account}

È possibile eliminare gli account utente locali dalla protezione dei documenti. Ad esempio, puoi eliminare gli account quando gli utenti modificano le informazioni sul loro account e-mail personale.

1. Nella console di amministrazione, fai clic su Servizi > Sicurezza documenti > Utenti invitati e locali e fai clic sulla scheda Utenti locali .
1. Selezionare la casella di controllo accanto a uno o più utenti, fare clic su Elimina e quindi su OK.

## Ordina l&#39;elenco di utenti {#sort-the-user-list}

Per trovare più facilmente gli utenti, ordinate l’elenco di utenti in base all’intestazione della colonna. Le icone a triangolo accanto all’intestazione della colonna indicano quale colonna è attualmente utilizzata per ordinare:

* Un triangolo rivolto verso l&#39;alto indica l&#39;ordine crescente.
* Un triangolo rivolto verso il basso indica un ordine decrescente.

   1. Nella console di amministrazione, fai clic su Servizi > Sicurezza documenti > Utenti invitati e locali.
   1. Per ordinare gli utenti invitati, fai clic sulla scheda Utenti invitati e fai clic sull’intestazione di colonna appropriata.
   1. Per ordinare gli utenti locali, fare clic sulla scheda Utenti locali e quindi sull’intestazione di colonna appropriata.

