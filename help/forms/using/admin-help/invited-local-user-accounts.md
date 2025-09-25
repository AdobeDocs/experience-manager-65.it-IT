---
title: Gestione degli account utente invitati e locali
description: La protezione dei documenti consente di ricercare, visualizzare, modificare, bloccare, sbloccare ed eliminare gli account utente invitati e locali.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: Document Security
exl-id: 23f71b34-a0cb-4664-bb8b-a60f33dc70d8
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: ht
source-wordcount: '1208'
ht-degree: 100%

---

# Gestione degli account utente invitati e locali {#managing-invited-and-local-user-accounts}

>[!NOTE]
> 
> Assicurati che l’utente disponga dei privilegi di amministratore per accedere alla console dell’amministratore.

Utilizza la pagina Utenti invitati e locali per gestire gli utenti invitati e locali. Questa pagina viene visualizzata solo se sono soddisfatti i seguenti requisiti:

* Sei un amministratore a cui è assegnato il ruolo di gestione della protezione dei documenti, il ruolo Utenti invitati e locali, e il ruolo utente della console di amministrazione. Consulta [Creazione e configurazione dei ruoli](/help/forms/using/admin-help/creating-configuring-roles.md#creating-and-configuring-roles).
* La registrazione degli utenti invitati è abilitata. Consulta [Configurazione della registrazione degli utenti invitati](/help/forms/using/admin-help/configuring-client-server-options.md#configuring-invited-user-registration).

La pagina Utenti invitati e locali contiene due schede che è possibile utilizzare per ricercare, visualizzare, modificare, bloccare, sbloccare ed eliminare gli account utente invitati e locali.

Puoi anche inviare manualmente le e-mail di registrazione agli utenti invitati. Ad esempio, potrebbe essere utile eseguire questa operazione se il periodo di registrazione autorizzato dall’e-mail termina e l’utente non può utilizzare l’URL per la registrazione. In questo caso, puoi inviare nuovamente un’e-mail di registrazione all’utente invitato. Quando l’utente invitato registra e attiva l’account, diventa un utente locale.

>[!NOTE]
>
>Gli utenti invitati possono inoltre essere aggiunti direttamente tramite la directory LDAP a cui fa riferimento la protezione dei documenti oppure quando un utente o un amministratore invita un nuovo utente durante la creazione o la modifica di un criterio, avviando quindi un’e-mail di invito alla registrazione. Gli utenti possono aggiungere nuovi utenti invitati ai criteri se abiliti l’opzione Abilita registrazione utenti invitati nella pagina Registrazione utenti invitati.

## Aggiungere un utente invitato {#add-an-invited-user}

Puoi aggiungere alla protezione dei documenti uno o più account utente invitati alla volta. Per aggiungere un account utente invitato, devi disporre dell’indirizzo e-mail dell’utente. Quando aggiungi un utente, la protezione dei documenti invia un’e-mail di registrazione invitandolo a registrarsi.

1. Nella console di amministrazione, fai clic su Servizi > Protezione dei documenti > Utenti invitati e locali, quindi fai clic su Invita nuovo utente.
1. Digita gli indirizzi e-mail degli utenti che desideri invitare. Inserisci più indirizzi su una riga, separati da una virgola.

   Il messaggio creato quando abiliti la registrazione degli utenti invitati viene inviato agli utenti. Consulta [Configurazione della registrazione degli utenti invitati](/help/forms/using/admin-help/configuring-client-server-options.md#configuring-invited-user-registration).

1. Fai clic su OK.

## Visualizzare informazioni su un utente locale {#view-information-about-a-local-user}

Puoi visualizzare informazioni sugli utenti locali, tra cui il nome, l’indirizzo e-mail, l’organizzazione, lo stato di registrazione e il dominio.

1. Nella console di amministrazione, fai clic su Servizi > Protezione dei documenti > Utenti invitati e locali, quindi fai clic su Invita nuovo utente.
1. Fai clic sulla scheda Utenti locali e nella pagina Gestisci utenti locali, fai clic sull’indirizzo e-mail dell’utente che desideri visualizzare.

   Vengono visualizzati i dettagli utente, puoi reimpostare la password dell’utente e disattivare l’account.

## Inviare un’e-mail a un utente esterno non registrato {#send-an-email-to-an-unregistered-external-user}

Quando aggiungi un utente invitato, la protezione dei documenti invia automaticamente all’utente una richiesta e-mail di registrazione. Puoi anche generare manualmente un’e-mail di registrazione da inviare a un utente invitato che non si è ancora registrato. Ad esempio, potrebbe essere utile inviare un nuovo invito se l’e-mail di registrazione dell’utente invitato scade.

1. Nella console di amministrazione, fai clic su Servizi > Protezione dei documenti > Utenti invitati e locali.
1. Nell’elenco degli utenti, seleziona la casella di controllo di ciascun utente a cui inviare un’e-mail di registrazione, quindi fai clic su Invia nuova e-mail di invito.
1. Rivedi l’elenco degli utenti selezionati e fai clic su OK.

## Reimpostare una password utente locale {#reset-a-local-user-password}

Puoi reimpostare le password per gli utenti invitati attivati che hanno eseguito la registrazione con protezione dei documenti ma hanno dimenticato la password. Quando reimposti una password, viene generata un’e-mail contenente una nuova password temporanea per l’utente.

Quando hai abilitato il processo di registrazione degli utenti invitati, hai creato un’e-mail che verrà inviata agli utenti chiedendo di reimpostare le password. Consulta [Configurazione della registrazione degli utenti invitati](/help/forms/using/admin-help/configuring-client-server-options.md#configuring-invited-user-registration).

1. Nella console di amministrazione, fai clic su Servizi > Protezione dei documenti > Utenti invitati e locali, quindi fai clic sulla scheda Utenti locali.
1. Nell’elenco degli utenti, seleziona l’utente appropriato.
1. Nella pagina Gestisci utente locale, fai clic su Reimposta password e su OK. All’utente viene inviata un’e-mail di reimpostazione della password contenente la nuova password.

## Abilitare o disabilitare un account utente {#enable-or-disable-a-user-account}

Puoi disabilitare gli account utente locali per impedire temporaneamente a un utente di effettuare l’accesso alla protezione dei documenti. Disabilitando l’account, l’utente non può utilizzare documenti protetti da criteri né creare o applicare criteri.

Puoi abilitare un account utente locale attualmente disabilitato. Non puoi abilitare un account utente invitato elencato come registrato. Lo stato di registrazione indica che l’utente invitato è registrato ma non ha ancora attivato l’account tramite il link presente nell’e-mail di attivazione.

**Limita un account utente**

1. Nella Console di amministrazione, fai clic su Servizi > Protezione dei documenti > Utenti invitati e locali, quindi fai clic sulla scheda Utenti locali.
1. Nell’elenco degli utenti, seleziona l’utente appropriato.
1. Nella pagina Dettagli utente locale fai clic su Disabilita account.

**Ripristina un account utente**

1. Fai clic su Utenti invitati e locali e quindi sulla scheda Utenti locali.
1. Nell’elenco degli utenti, seleziona l’utente appropriato.
1. Nella pagina Dettagli utente locale fai clic su Abilita account.

## Rimuovere un account utente invitato {#remove-an-invited-user-account}

Puoi eliminare gli account utente invitati dalla protezione dei documenti. Ad esempio, potrebbe essere utile eliminare un account quando un utente modifica le informazioni del proprio account personale di posta elettronica.

Se elimini un account utente, solo l’amministratore può ripristinarlo selezionando l’opzione Aggiungi utente invitato nella pagina Utenti invitati. Gli utenti non possono aggiungere l’account utente eliminato ai criteri e non è possibile avviare alcun processo di invito in questo modo.

>[!NOTE]
>
>Gli utenti invitati che sono stati eliminati tramite l’interfaccia di Gestione utente di AEM Forms non possono essere nuovamente invitati fino a quando non vengono eliminati di nuovo tramite la procedura seguente.

1. Nella console di amministrazione, fai clic su Servizi > Protezione dei documenti > Utenti invitati e locali, quindi fai clic sulla scheda Utenti invitati.
1. Seleziona la casella di controllo accanto a uno o più utenti, fai clic su Elimina e quindi su OK.

## Cercare un account utente invitato {#search-for-an-invited-user-account}

Puoi cercare gli account utente invitati utilizzando un indirizzo e-mail.

1. Nella console di amministrazione, fai clic su Servizi > Protezione dei documenti > Utenti invitati e locali.
1. Nella casella Trova e-mail digitare l’indirizzo e-mail dell’utente e quindi fare clic su Trova.

## Cercare un account utente locale {#search-for-a-local-user-account}

Puoi cercare un utente locale utilizzando il suo indirizzo e-mail oppure il suo nome e il suo dominio.

1. Nella console di amministrazione, fai clic su Servizi > Protezione dei documenti > Utenti invitati e locali, quindi fai clic sulla scheda Utenti locali.
1. Digita i criteri di ricerca nella casella Trova, seleziona Nome o E-mail e quindi fai clic su Trova.

## Rimuovere un account utente locale {#remove-a-local-user-account}

Puoi eliminare gli account utente locali dalla protezione dei documenti. Ad esempio, potrebbe essere utile eliminare gli account quando gli utenti modificano le informazioni del proprio account personale di posta elettronica.

1. Nella console di amministrazione, fai clic su Servizi > Protezione dei documenti > Utenti invitati e locali, quindi fai clic sulla scheda Utenti locali.
1. Seleziona la casella di controllo accanto a uno o più utenti, fai clic su Elimina e quindi su OK.

## Ordinare l’elenco degli utenti {#sort-the-user-list}

Puoi trovare gli utenti più facilmente ordinando l’elenco degli utenti per intestazione di colonna. Le icone triangolari accanto all’intestazione di colonna indicano quale colonna è attualmente utilizzata per ordinare gli utenti:

* Un triangolo rivolto verso l’alto indica l’ordine crescente.
* Un triangolo rivolto verso il basso indica l’ordine decrescente.

   1. Nella console di amministrazione, fai clic su Servizi > Protezione dei documenti > Utenti invitati e locali.
   1. Per ordinare gli utenti invitati, fai clic sulla scheda Utenti invitati, quindi sull’intestazione di colonna appropriata.
   1. Per ordinare gli utenti locali, fare clic sulla scheda Utenti locali e quindi sull’intestazione di colonna appropriata.
