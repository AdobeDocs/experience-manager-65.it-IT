---
title: Gestione degli account utente invitati e locali
seo-title: Gestione degli account utente invitati e locali
description: Mediante Document Security potete cercare, visualizzare, modificare, bloccare, sbloccare ed eliminare gli account utente invitati e locali.
seo-description: Mediante Document Security potete cercare, visualizzare, modificare, bloccare, sbloccare ed eliminare gli account utente invitati e locali.
uuid: 0d0c717a-6e6e-4e42-96eb-3a7166e215ab
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 65720eed-ab06-463f-9567-2fdc468b6219
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '1220'
ht-degree: 0%

---


# Gestione degli account utente invitati e locali {#managing-invited-and-local-user-accounts}

Utilizzate la pagina Utenti invitati e locali per gestire gli utenti invitati e locali. Questa pagina viene visualizzata solo se sono soddisfatti i seguenti requisiti:

* Siete un amministratore a cui vengono assegnati il ruolo Gestisci utenti invitati e locali per la protezione dei documenti e il ruolo Utente della console di amministrazione. (Vedere [Creazione e configurazione di ruoli](/help/forms/using/admin-help/creating-configuring-roles.md#creating-and-configuring-roles).)
* La registrazione degli utenti invitati è abilitata. Consultate [Configurazione della registrazione dell&#39;utente invitato](/help/forms/using/admin-help/configuring-client-server-options.md#configuring-invited-user-registration).

La pagina Utenti invitati e locali contiene due schede che potete utilizzare per cercare, visualizzare, modificare, bloccare, sbloccare ed eliminare gli account utente invitati e locali.

Potete inoltre inviare manualmente e-mail di registrazione agli utenti invitati. Potrebbe essere utile eseguire questa operazione, ad esempio, se il periodo di registrazione del messaggio e-mail autorizzato termina e l&#39;utente non può utilizzare l&#39;URL per la registrazione. In questo caso, potete inviare nuovamente un messaggio e-mail di registrazione all’utente invitato. Quando l&#39;utente invitato si registra e attiva l&#39;account, l&#39;utente diventa un utente locale.

>[!NOTE]
>
>Gli utenti invitati possono anche essere aggiunti direttamente tramite la directory LDAP che documenta i riferimenti alla sicurezza, oppure quando un utente o un amministratore invita un nuovo utente al momento della creazione o della modifica di un criterio, avviando quindi un messaggio e-mail di invito alla registrazione. Gli utenti possono aggiungere nuovi utenti invitati ai criteri se abilitate l&#39;opzione Abilita registrazione utente invitata nella pagina Registrazione utente invitata.

## Aggiunta di un utente invitato {#add-an-invited-user}

Potete aggiungere uno o più account utente invitati alla volta per la protezione dei documenti. Per aggiungere un account utente invitato, è necessario l’indirizzo e-mail dell’utente. Quando aggiungete un utente, Document Security invia un messaggio e-mail di registrazione che invita l&#39;utente a registrarsi.

1. Nella console di amministrazione, fate clic su Servizi > Document Security > Utenti invitati e locali, quindi fate clic su Invita nuovo utente.
1. Digitate gli indirizzi e-mail degli utenti che desiderate invitare. Inserite più indirizzi su una riga, separati da una virgola.

   Il messaggio creato quando si abilita la registrazione degli utenti invitati viene inviato agli utenti. Consultate [Configurazione della registrazione dell&#39;utente invitato](/help/forms/using/admin-help/configuring-client-server-options.md#configuring-invited-user-registration).

1. Fai clic su OK.

## Visualizza informazioni su un utente locale {#view-information-about-a-local-user}

Potete visualizzare informazioni sugli utenti locali, inclusi nome, indirizzo e-mail, organizzazione, stato di registrazione e dominio.

1. Nella console di amministrazione, fate clic su Servizi > Document Security > Utenti invitati e locali, quindi fate clic su Invita nuovo utente.
1. Fate clic sulla scheda Utenti locali e, nella pagina Gestisci utenti locali, fate clic sull’indirizzo e-mail dell’utente che desiderate visualizzare.

   I dettagli utente vengono visualizzati e potete ripristinare la password dell&#39;utente e disattivare l&#39;account.

## Invia un&#39;e-mail a un utente esterno non registrato {#send-an-email-to-an-unregistered-external-user}

Quando si aggiunge un utente invitato, Document Security invia automaticamente all&#39;utente una richiesta di posta elettronica di registrazione. Potete inoltre generare manualmente un messaggio e-mail di registrazione da inviare a un utente invitato che non si è ancora registrato. A questo scopo, ad esempio, potete inviare un nuovo invito se scade il messaggio e-mail di registrazione di un utente invitato.

1. Nella console di amministrazione, fate clic su Servizi > Document Security > Utenti invitati e locali.
1. Nell’elenco di utenti, selezionate la casella di controllo a cui ogni utente deve inviare un messaggio e-mail di registrazione, quindi fate clic su Invia di nuovo e-mail di invito.
1. Esaminate l’elenco degli utenti selezionati e fate clic su OK.

## Reimpostare una password utente locale {#reset-a-local-user-password}

Potete ripristinare le password per gli utenti invitati attivati che si sono registrati con Document Security ma hanno dimenticato la password. Quando reimpostate una password, viene generato un messaggio e-mail che contiene una nuova password temporanea per l’utente.

Quando avete attivato il processo di registrazione degli utenti invitati, avete creato un messaggio e-mail che verrà inviato agli utenti che chiedono loro di ripristinare le password. Consultate [Configurazione della registrazione dell&#39;utente invitato](/help/forms/using/admin-help/configuring-client-server-options.md#configuring-invited-user-registration).

1. Nella console di amministrazione, fate clic su Servizi > Document Security > Utenti invitati e locali e fate clic sulla scheda Utenti locali.
1. Nell’elenco di utenti, selezionate l’utente appropriato.
1. Nella pagina Gestisci utente locale, fate clic su Reimposta password e fate clic su OK. All’utente viene inviato un messaggio e-mail di reimpostazione della password contenente la nuova password.

## Attivare o disattivare un account utente {#enable-or-disable-a-user-account}

È possibile disattivare gli account utente locali per limitare temporaneamente l&#39;accesso di un utente alla protezione del documento. Quando disabilitate l&#39;account, l&#39;utente non può utilizzare documenti protetti tramite criterio né creare o applicare criteri.

È possibile abilitare un account utente locale che attualmente è disabilitato. Non potete abilitare un account utente invitato elencato come registrato. Lo stato registrato indica che l&#39;utente invitato è registrato ma non ha ancora attivato l&#39;account utilizzando il collegamento presente nel messaggio e-mail di attivazione.

**Limitare un account utente**

1. In Admin Console, fai clic su Servizi > Protezione documento > Utenti invitati e locali, quindi fai clic sulla scheda Utenti locali.
1. Nell’elenco di utenti, selezionate l’utente appropriato.
1. Nella pagina Dettagli utente locale, fate clic su Disattiva account.

**Ripristino di un account utente**

1. Fate clic su Invitati e su Utenti locali, quindi fate clic sulla scheda Utenti locali.
1. Nell’elenco di utenti, selezionate l’utente appropriato.
1. Nella pagina Dettagli utente locale, fate clic su Attiva account.

## Rimozione di un account utente invitato {#remove-an-invited-user-account}

Potete eliminare gli account utente invitati dalla protezione del documento. Potrebbe essere utile eliminare un account, ad esempio, quando un utente modifica le informazioni personali del proprio account e-mail.

Se eliminate un account utente, solo voi o un altro amministratore potete ripristinare l’account selezionando l’opzione Aggiungi utente invitato nella pagina Utenti invitati. Gli utenti non possono aggiungere l&#39;account utente eliminato a un criterio e tale metodo non consente di avviare alcun processo di invito.

>[!NOTE]
>
>Gli utenti invitati che sono stati eliminati tramite l&#39;interfaccia di gestione utenti dei moduli AEM non possono essere nuovamente invitati fino a quando non sono stati nuovamente eliminati utilizzando la procedura seguente.

1. Nella console di amministrazione, fate clic su Servizi > Document Security > Utenti invitati e locali e fate clic sulla scheda Utenti invitati.
1. Selezionate la casella di controllo accanto a uno o più utenti, fate clic su Elimina, quindi su OK.

## Cerca un account utente invitato {#search-for-an-invited-user-account}

Potete cercare gli account utente invitati utilizzando un indirizzo e-mail.

1. Nella console di amministrazione, fate clic su Servizi > Document Security > Utenti invitati e locali.
1. Nella casella Trova e-mail, digitate l’indirizzo e-mail dell’utente e fate clic su Trova.

## Cerca un account utente locale {#search-for-a-local-user-account}

Potete cercare un utente locale utilizzando l&#39;indirizzo e-mail o il nome e il dominio dell&#39;utente.

1. Nella console di amministrazione, fate clic su Servizi > Document Security > Utenti invitati e locali e fate clic sulla scheda Utenti locali.
1. Digitate i criteri di ricerca nella casella Trova, selezionate Nome o E-mail, quindi fate clic su Trova.

## Rimozione di un account utente locale {#remove-a-local-user-account}

È possibile eliminare gli account utente locali dalla protezione dei documenti. Potreste desiderare di eliminare account, ad esempio, quando gli utenti modificano le informazioni personali del loro account e-mail.

1. Nella console di amministrazione, fate clic su Servizi > Document Security > Utenti invitati e locali e fate clic sulla scheda Utenti locali.
1. Selezionate la casella di controllo accanto a uno o più utenti, fate clic su Elimina, quindi su OK.

## Ordinare l&#39;elenco di utenti {#sort-the-user-list}

Per trovare più facilmente gli utenti, ordinate l’elenco di utenti per intestazione di colonna. Le icone a triangolo accanto all’intestazione della colonna indicano quale colonna è attualmente utilizzata per ordinare:

* Un triangolo rivolto verso l’alto indica l’ordine crescente.
* Un triangolo rivolto verso il basso indica un ordine decrescente.

   1. Nella console di amministrazione, fate clic su Servizi > Document Security > Utenti invitati e locali.
   1. Per ordinare gli utenti invitati, fate clic sulla scheda Utenti invitati e fate clic sull’intestazione di colonna appropriata.
   1. Per ordinare gli utenti locali, fate clic sulla scheda Utenti locali e fate clic sull&#39;intestazione di colonna appropriata.

