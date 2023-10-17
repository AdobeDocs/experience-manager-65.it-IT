---
title: Configurazione dell’e-mail
description: Scopri come configurare le notifiche e-mail e gli abbonamenti per le community Adobe Experience Manager.
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
pagetitle: Configuring Email
role: Admin
exl-id: bf97d388-f8ca-4e37-88e2-0c536834311e
source-git-commit: 0a4aca939c564720f63f055e9522e56942eaa128
workflow-type: tm+mt
source-wordcount: '824'
ht-degree: 3%

---

# Configurazione dell’e-mail {#configuring-email}

AEM Communities utilizza le e-mail per:

* [Notifiche community](notifications.md)
* [Iscrizioni alle community](subscriptions.md)

Per impostazione predefinita, la funzione e-mail non funziona in quanto richiede la specifica di un server SMTP e di un utente SMTP.

>[!CAUTION]
>
>Le e-mail per le notifiche e gli abbonamenti devono essere configurate solo sul [editore principale](deploy-communities.md#primary-publisher).

## Configurazione predefinita servizio di posta {#default-mail-service-configuration}

Il servizio di posta predefinito è richiesto sia per le notifiche che per gli abbonamenti.

* Accedi all’editore principale con privilegi di amministratore e accedi a [Console web](../../help/sites-deploying/configuring-osgi.md):

   * Ad esempio: [http://localhost:4503/system/console/configMgr](http://localhost:4503/system/console/configMgr)

* Individua il `Day CQ Mail Service`.
* Seleziona l’icona Modifica.

Si basa sulla documentazione di [Configurazione delle notifiche e-mail](../../help/sites-administering/notification.md), ma con una differenza nel campo `"From" address` è *non* obbligatorio e deve essere lasciato vuoto.

Ad esempio (compilato con valori solo a scopo illustrativo):

![email-config](assets/email-config.png)

* **[!UICONTROL Nome host del server SMTP]**

  *(Obbligatorio)* Server SMTP da utilizzare.

* **[!UICONTROL Porta del server SMTP]**

  *(Obbligatorio)* La porta del server SMTP deve essere uguale o superiore a 25.

* **[!UICONTROL Utente SMTP]**

  *(Obbligatorio)* Utente SMTP.

* **[!UICONTROL Password SMTP]**

  *(Obbligatorio)* Password dell&#39;utente SMTP.

* **[!UICONTROL Indirizzo &quot;Da&quot;]**

  Lascia vuoto
* **[!UICONTROL SMTP usa SSL]**

  Se questa opzione è selezionata, viene inviata un’e-mail protetta. Verificare che la porta sia impostata su 465 o come richiesto per un server SMTP.
* **[!UICONTROL Debug e-mail]**

  Se questa opzione è selezionata, viene attivata la registrazione delle interazioni del server SMTP.

## Configurazione e-mail AEM Communities {#aem-communities-email-configuration}

Una volta [servizio e-mail predefinito](#default-mail-service-configuration) è configurato, le due istanze esistenti di `AEM Communities Email Reply Configuration` La configurazione OSGi, inclusa nella versione, diventa funzionale.

Quando si consente la risposta per e-mail, è necessario configurare ulteriormente solo l’istanza per gli abbonamenti.

1. [E-mail](#configuration-for-notifications) istanza:

   Per le notifiche, che non supportano l’e-mail di risposta e che non devono essere modificate.

1. [Subscriptions-email](#configuration-for-subscriptions) istanza:

   Richiede la configurazione per abilitare completamente la creazione di post dall’e-mail di risposta.

Per raggiungere le istanze di configurazione e-mail Communities:

* Accedi all’editore principale con privilegi di amministratore e accedi a [Console web](../../help/sites-deploying/configuring-osgi.md)

   * Ad esempio: [http://localhost:4503/system/console/configMgr](http://localhost:4503/system/console/configMgr)

* Individua `AEM Communities Email Reply Configuration`.

![email-reply-config](assets/email-reply-config.png)

### Configurazione per le notifiche {#configuration-for-notifications}

L’istanza di `AEM Communities Email Reply Configuration` La configurazione OSGi con il Nome e-mail è senza notifiche. Questa funzione non include la risposta e-mail.

Non modificare questa configurazione.

* Individua il `AEM Communities Email Reply Configuration`.
* Seleziona l’icona Modifica.
* Verificare che **Nome** è `email`.

* Verifica che **Crea post da e-mail di risposta** è `unchecked`.

![configure-email-reply](assets/configure-email-reply.png)

### Configurazione per le sottoscrizioni {#configuration-for-subscriptions}

Per gli abbonamenti alle community, è possibile abilitare o disabilitare la possibilità per un membro di pubblicare contenuti rispondendo a un messaggio e-mail.

* Individua il `AEM Communities Email Reply Configuration`.
* Seleziona l’icona Modifica.
* Verificare che **Nome** è `subscriptions-email`.

  ![configure-email-subscription](assets/configure-email-subscriptions.png)

* **[!UICONTROL Nome]**

  *(Obbligatorio)* `subscriptions-email`. Non modificare.

* **[!UICONTROL Crea post da e-mail di risposta]**

  Se questa opzione è selezionata, il destinatario di un’e-mail di abbonamento può pubblicare contenuti inviando una risposta. Il valore predefinito è selezionato.
* **[!UICONTROL Aggiungi ID tracciato all&#39;intestazione]**

  Il valore predefinito è `Reply-To`.

* **[!UICONTROL Lunghezza massima oggetto]**

  Se l’ID di tracciamento viene aggiunto alla riga dell’oggetto, si tratta della lunghezza massima dell’oggetto, escluso l’ID tracciato, dopo la quale viene tagliato. Deve essere il più piccolo possibile per evitare che le informazioni ID tracciate vadano perse. Il valore predefinito è 200.

* **[!UICONTROL Indirizzo e-mail di risposta]**

  Indirizzo utilizzato come indirizzo e-mail di risposta. Il valore predefinito è `no-reply@example.com`.

* **[!UICONTROL Rispondi al delimitatore]**

  Se l’ID di tracciamento viene aggiunto all’intestazione Risposta, viene utilizzato questo delimitatore. Il valore predefinito è `+` (segno più).

* **[!UICONTROL Prefisso ID tracciatore nell’oggetto]**

  Se l’ID di tracciamento viene aggiunto alla riga dell’oggetto, viene utilizzato questo prefisso. Il valore predefinito è `post#`.

* **[!UICONTROL Prefisso ID tracciamento nel corpo del messaggio]**

  Se l’ID di tracciamento viene aggiunto al corpo del messaggio, viene utilizzato questo prefisso. Il valore predefinito è `Please do not remove this:`.

* **[!UICONTROL Invia e-mail come HTML]**: se questa opzione è selezionata, Content-Type dell’e-mail viene impostato come `"text/html;charset=utf-8"`. Il valore predefinito è selezionato.

* **[!UICONTROL Nome utente predefinito]**

  Questo nome viene utilizzato per gli utenti senza nome. Il valore predefinito è `no-reply@example.com`.

* **[!UICONTROL Percorso directory principale modelli]**

  L’e-mail viene creata utilizzando un modello memorizzato in questo percorso principale. Il valore predefinito è `/etc/community/templates/subscriptions-email`.

## Configurare Importazione polling {#configure-polling-importer}

Affinché l’e-mail possa essere introdotta nell’archivio, è necessario configurare manualmente un’importazione polling e le relative proprietà nell’archivio.

### Aggiungi nuova importazione polling {#add-new-polling-importer}

* Accedi all’editore principale con privilegi di amministratore e passa alla console Importazione polling:

  Ad esempio: [http://localhost:4503/etc/importers/polling.html](http://localhost:4503/etc/importers/polling.html)

* Seleziona **[!UICONTROL Aggiungi]**

  ![importazione polling](assets/polling-importer.png)

* **[!UICONTROL Tipo]**

  *(Obbligatorio)* Tirare verso il basso per selezionare `POP3 (over SSL)`.

* **[!UICONTROL URL]**

  *(Obbligatorio)* Il server della posta in uscita. Esempio: `pop.gmail.com:995/INBOX?username=community-emailgmail.com&password=****`.

* **[!UICONTROL Importa nel percorso]**&amp;ast;

  *(Obbligatorio)* Imposta su `/content/usergenerated/mailFolder/postEmails`
esplorando la `postEmails`cartella e seleziona **OK**.

* **[!UICONTROL Intervallo di aggiornamento in secondi]**

  *(Facoltativo)* Il server di posta configurato per il servizio di posta predefinito può avere requisiti relativi al valore dell&#39;intervallo di aggiornamento. Ad esempio, Gmail potrebbe richiedere un intervallo di `300`.

* **[!UICONTROL Accesso]**

  *(Facoltativo)*

* **[!UICONTROL Password]**

  *(Facoltativo)*

* Seleziona **[!UICONTROL OK]**.

### Regola protocollo per nuova importazione polling {#adjust-protocol-for-new-polling-importer}

Una volta salvata la nuova configurazione di polling, è necessario modificare ulteriormente le proprietà dell’importazione e-mail dell’abbonamento per modificare il protocollo da `POP3` a `emailreply`.

Utilizzo di [CRXDE Liti](../../help/sites-developing/developing-with-crxde-lite.md):

* Accedi all’editore principale con privilegi di amministratore e passa a [https://&lt;server>:&lt;port>/crx/de/index.jsp#/etc/importer/polling](http://localhost:4503/crx/de/index.jsp#/etc/importers/polling).
* Seleziona la configurazione appena creata e modifica le seguenti proprietà:

   * **feedType**: Sostituisci `pop3s` con **`emailreply`**
   * **sorgente**: Sostituisci il protocollo della sorgente `pop3s://` con **`emailreply://`**

![polling-protocol](assets/polling-protocol.png)

I triangoli rossi indicano le proprietà modificate. Assicurati di salvare le modifiche:

* Seleziona **[!UICONTROL Salva tutto]**.
