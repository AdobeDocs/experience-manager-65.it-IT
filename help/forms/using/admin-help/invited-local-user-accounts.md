---
title: Gestione degli account utente invitati e locali
description: Document Security consente di cercare, visualizzare, modificare, bloccare, sbloccare ed eliminare gli account utente invitati e locali.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: Document Security
exl-id: 23f71b34-a0cb-4664-bb8b-a60f33dc70d8
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '1196'
ht-degree: 0%

---

# Gestione degli account utente invitati e locali {#managing-invited-and-local-user-accounts}

Utilizza la pagina Utenti invitati e locali per gestire gli utenti invitati e locali. Questa pagina viene visualizzata solo se sono soddisfatti i seguenti requisiti:

* Sei un amministratore a cui sono assegnati il ruolo di gestione della sicurezza dei documenti, Invitato e Utenti locali, e il ruolo Utente della console di amministrazione. (vedere [Creazione e configurazione di ruoli](/help/forms/using/admin-help/creating-configuring-roles.md#creating-and-configuring-roles).)
* La registrazione degli utenti invitati è abilitata. (vedere [Configurazione della registrazione degli utenti invitati](/help/forms/using/admin-help/configuring-client-server-options.md#configuring-invited-user-registration).)

La pagina Utenti invitati e locali contiene due schede che è possibile utilizzare per cercare, visualizzare, modificare, bloccare, sbloccare ed eliminare gli account utente invitati e locali.

Puoi anche inviare manualmente le e-mail di registrazione agli utenti invitati. Ad esempio, potrebbe essere utile eseguire questa operazione se il periodo di registrazione termina con l’e-mail autorizzata e l’utente non può utilizzare l’URL per la registrazione. In questo caso, puoi inviare nuovamente un’e-mail di registrazione all’utente invitato. Quando l’utente invitato registra e attiva l’account, diventa un utente locale.

>[!NOTE]
>
>Gli utenti invitati possono inoltre essere aggiunti direttamente tramite la directory LDAP a cui fa riferimento la sicurezza dei documenti oppure quando un utente o un amministratore invita un nuovo utente durante la creazione o la modifica di un criterio, avviando quindi un messaggio e-mail di invito alla registrazione. Gli utenti possono aggiungere nuovi utenti invitati ai criteri se si abilita l&#39;opzione Abilita registrazione utenti invitati nella pagina Registrazione utenti invitati.

## Aggiungi un utente invitato {#add-an-invited-user}

Puoi aggiungere alla protezione dei documenti uno o più account utente invitati alla volta. Per aggiungere un account utente invitato, devi disporre dell’indirizzo e-mail dell’utente. Quando aggiungi un utente, Document Security invia un’e-mail di registrazione invitandolo a registrarsi.

1. Nella console di amministrazione, fai clic su Servizi > Document Security > Utenti invitati e locali, quindi fai clic su Invita nuovo utente.
1. Digita gli indirizzi e-mail degli utenti che desideri invitare. Inserisci più indirizzi su una riga, separati da una virgola.

   Il messaggio creato quando si abilita la registrazione degli utenti invitati viene inviato agli utenti. (vedere [Configurazione della registrazione degli utenti invitati](/help/forms/using/admin-help/configuring-client-server-options.md#configuring-invited-user-registration).)

1. Fare clic su OK.

## Visualizzare informazioni su un utente locale {#view-information-about-a-local-user}

Puoi visualizzare informazioni sugli utenti locali, tra cui il nome, l’indirizzo e-mail, l’organizzazione, lo stato di registrazione e il dominio.

1. Nella console di amministrazione, fai clic su Servizi > Document Security > Utenti invitati e locali, quindi fai clic su Invita nuovo utente.
1. Fare clic sulla scheda Utenti locali e nella pagina Gestisci utenti locali fare clic sull&#39;indirizzo di posta elettronica dell&#39;utente che si desidera visualizzare.

   Vengono visualizzati i dettagli utente, è possibile reimpostare la password dell’utente e disattivare l’account.

## Inviare un messaggio e-mail a un utente esterno non registrato {#send-an-email-to-an-unregistered-external-user}

Quando aggiungi un utente invitato, document security invia automaticamente all’utente una richiesta e-mail di registrazione. Puoi anche generare manualmente un’e-mail di registrazione da inviare a un utente invitato che non si è ancora registrato. Ad esempio, potrebbe essere utile inviare un nuovo invito se l&#39;e-mail di registrazione dell&#39;utente invitato scade.

1. Nella console di amministrazione, fai clic su Servizi > Document Security > Utenti invitati e locali.
1. Nell&#39;elenco degli utenti selezionare la casella di controllo a cui inviare un messaggio di posta elettronica di registrazione e quindi fare clic su Invia di nuovo messaggio di invito.
1. Rivedere l&#39;elenco degli utenti selezionati e fare clic su OK.

## Reimpostare una password utente locale {#reset-a-local-user-password}

Puoi reimpostare le password per gli utenti invitati attivati che si sono registrati con document security ma hanno dimenticato la password. Quando si reimposta una password, viene generato un messaggio e-mail contenente una nuova password temporanea per l’utente.

Quando hai attivato il processo di registrazione degli utenti invitati, hai creato un messaggio e-mail che verrà inviato agli utenti chiedendo di reimpostare le password. (vedere [Configurazione della registrazione degli utenti invitati](/help/forms/using/admin-help/configuring-client-server-options.md#configuring-invited-user-registration).)

1. Nella console di amministrazione, fai clic su Servizi > Document Security > Utenti invitati e locali, quindi fai clic sulla scheda Utenti locali.
1. Nell’elenco degli utenti, seleziona l’utente appropriato.
1. Nella pagina Gestisci utente locale fare clic su Reimposta password e quindi su OK. All&#39;utente viene inviata un&#39;e-mail di reimpostazione della password contenente la nuova password.

## Attivare o disattivare un account utente {#enable-or-disable-a-user-account}

È possibile disattivare gli account utente locali per impedire temporaneamente a un utente di effettuare l’accesso a Document Security. Quando disattivi l’account, l’utente non può utilizzare documenti protetti tramite policy né creare o applicare policy.

È possibile abilitare un account utente locale attualmente disabilitato. Non è possibile abilitare un account utente invitato elencato come registrato. Lo stato di registrazione indica che l’utente invitato è registrato ma non ha ancora attivato l’account utilizzando il collegamento presente nell’e-mail di attivazione.

**Limitare un account utente**

1. In Administration Console, fai clic su Servizi > Document Security > Utenti invitati e locali, quindi fai clic sulla scheda Utenti locali.
1. Nell’elenco degli utenti, seleziona l’utente appropriato.
1. Nella pagina Dettagli utente locale fare clic su Disabilita account.

**Ripristinare un account utente**

1. Fare clic su Utenti invitati e utenti locali e quindi sulla scheda Utenti locali.
1. Nell’elenco degli utenti, seleziona l’utente appropriato.
1. Nella pagina Dettagli utente locale fare clic su Abilita account.

## Rimuovere un account utente invitato {#remove-an-invited-user-account}

Puoi eliminare gli account utente invitati da document security. Ad esempio, potrebbe essere utile eliminare un account quando un utente modifica le informazioni personali del proprio account di posta elettronica.

Se si elimina un account utente, solo l&#39;amministratore può ripristinarlo selezionando l&#39;opzione Aggiungi utente invitato nella pagina Utenti invitati. Gli utenti non possono aggiungere a un criterio l’account utente eliminato e tale metodo non può avviare alcun processo di invito.

>[!NOTE]
>
>Gli utenti invitati che sono stati eliminati tramite l’interfaccia per la gestione degli utenti dei moduli AEM non possono essere nuovamente invitati finché non sono stati nuovamente eliminati seguendo la procedura seguente.

1. Nella console di amministrazione, fai clic su Servizi > Document Security > Utenti invitati e locali, quindi fai clic sulla scheda Utenti invitati.
1. Selezionare la casella di controllo accanto a uno o più utenti, fare clic su Elimina e quindi su OK.

## Cerca un account utente invitato {#search-for-an-invited-user-account}

Puoi cercare gli account utente invitati utilizzando un indirizzo e-mail.

1. Nella console di amministrazione, fai clic su Servizi > Document Security > Utenti invitati e locali.
1. Nella casella Trova e-mail digitare l&#39;indirizzo e-mail dell&#39;utente e quindi fare clic su Trova.

## Cerca un account utente locale {#search-for-a-local-user-account}

Puoi cercare un utente locale utilizzando il suo indirizzo e-mail o nome e dominio.

1. Nella console di amministrazione, fai clic su Servizi > Document Security > Utenti invitati e locali, quindi fai clic sulla scheda Utenti locali.
1. Digitare i criteri di ricerca nella casella Trova, selezionare Nome o E-mail e quindi fare clic su Trova.

## Rimuovere un account utente locale {#remove-a-local-user-account}

È possibile eliminare gli account utente locali da document security. Ad esempio, potrebbe essere utile eliminare gli account quando gli utenti modificano le informazioni personali relative all’account di posta elettronica.

1. Nella console di amministrazione, fai clic su Servizi > Document Security > Utenti invitati e locali, quindi fai clic sulla scheda Utenti locali.
1. Selezionare la casella di controllo accanto a uno o più utenti, fare clic su Elimina e quindi su OK.

## Ordinare l’elenco degli utenti {#sort-the-user-list}

È possibile trovare gli utenti più facilmente ordinando l’elenco degli utenti per intestazione di colonna. Le icone triangolari accanto all’intestazione della colonna indicano quale colonna è attualmente utilizzata per ordinare:

* Un triangolo rivolto verso l&#39;alto indica l&#39;ordine crescente.
* Un triangolo rivolto verso il basso indica l&#39;ordine decrescente.

   1. Nella console di amministrazione, fai clic su Servizi > Document Security > Utenti invitati e locali.
   1. Per ordinare gli utenti invitati, fai clic sulla scheda Utenti invitati, quindi sull’intestazione di colonna appropriata.
   1. Per ordinare gli utenti locali, fare clic sulla scheda Utenti locali e quindi sull&#39;intestazione di colonna appropriata.
