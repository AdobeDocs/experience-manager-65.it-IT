---
title: Configurazione e-mail
seo-title: Configurazione e-mail
description: Configurazione e-mail per Communities
seo-description: Configurazione e-mail per Communities
uuid: e8422cc2-1594-43b0-b587-82825636cec1
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: b4d38e45-eaa0-4ace-a885-a2e84fdfd5a1
pagetitle: Configuring Email
translation-type: tm+mt
source-git-commit: 58fa0f05bae7ab5ba51491be3171b5c6ffbe870d

---


# Configurazione e-mail {#configuring-email}

AEM Communities utilizza l&#39;e-mail per

* [Notifiche community](notifications.md)
* [Iscrizioni community](subscriptions.md)

Per impostazione predefinita, la funzione e-mail non funziona perché richiede la specifica di un server SMTP e di un utente SMTP.

>[!CAUTION]
>
>Le e-mail per le notifiche e le iscrizioni devono essere configurate solo sull&#39;editore [](deploy-communities.md#primary-publisher)principale.

## Configurazione servizio di posta elettronica predefinita {#default-mail-service-configuration}

Il servizio e-mail predefinito è richiesto sia per le notifiche che per le iscrizioni.

* Nell&#39;editore principale
* Accesso con privilegi di amministratore
* Accesso alla console [Web](../../help/sites-deploying/configuring-osgi.md)

   * Ad esempio, [http://localhost:4503/system/console/configMgr](http://localhost:4503/system/console/configMgr)

* Individua il `Day CQ Mail Service`
* Selezionate l’icona di modifica

Questo si basa sulla documentazione per la [configurazione delle notifiche](../../help/sites-administering/notification.md)e-mail, ma con una differenza in quanto il campo `"From" address`*non* è obbligatorio e deve essere lasciato vuoto.

Ad esempio (con valori solo a scopo illustrativo):

![chlimage_1-98](assets/chlimage_1-98.png)

* **[!UICONTROL Nome]** host del server SMTP: *(obbligatorio)* Il server SMTP da utilizzare.

* **[!UICONTROL Porta]** del server SMTP *(richiesta)* La porta del server SMTP deve essere 25 o superiore.

* **[!UICONTROL Utente]** SMTP: *(obbligatorio)* L&#39;utente SMTP.

* **[!UICONTROL Password]** SMTP: *(obbligatorio)* La password dell&#39;utente SMTP.

* **[!UICONTROL Indirizzo]**&quot;Da&quot;: Lascia vuoto
* **[!UICONTROL SMTP usa SSL]**: Se questa opzione è selezionata, verrà inviata un&#39;e-mail protetta. Verificare che la porta sia impostata su 465 o come richiesto per il server SMTP.
* **[!UICONTROL Esegui debug e-mail]**: Se questa opzione è selezionata, consente la registrazione delle interazioni del server SMTP.

## Configurazione e-mail AEM Communities {#aem-communities-email-configuration}

Una volta configurato il servizio [di posta](#default-mail-service-configuration) predefinito, le due istanze esistenti della configurazione `AEM Communities Email Reply Configuration` OSGi, incluse nella release, diventano operative.

Per consentire la risposta tramite e-mail, è necessario configurare ulteriormente solo l’istanza per le iscrizioni.

1. ` [email](#configuration-for-notifications)` instance

   per le notifiche, che non supportano le e-mail di risposta e non devono essere modificate

1. ` [subscriptions-email](#configuration-for-subscriptions)` instance

   richiede la configurazione per abilitare completamente la creazione di post dal messaggio e-mail di risposta

Per raggiungere le istanze di configurazione e-mail di Communities:

* Nell&#39;editore principale
* Accesso con privilegi di amministratore
* Accesso alla console [Web](../../help/sites-deploying/configuring-osgi.md)

   * Ad esempio, [http://localhost:4503/system/console/configMgr](http://localhost:4503/system/console/configMgr)

* Individua `AEM Communities Email Reply Configuration`

![chlimage_1-99](assets/chlimage_1-99.png)

### Configurazione per le notifiche {#configuration-for-notifications}

L’istanza della configurazione `AEM Communities Email Reply Configuration` OSGi con l’e-mail Nome è una funzionalità di notifica. Questa funzione non include la risposta tramite e-mail.

Questa configurazione non deve essere modificata.

* Individua il `AEM Communities Email Reply Configuration`
* Selezionate l’icona di modifica
* Verifica che il **nome** sia `email`

* Verifica **Crea post dal messaggio e-mail** di risposta `unchecked`

![chlimage_1-100](assets/chlimage_1-100.png)

### Configurazione per le iscrizioni {#configuration-for-subscriptions}

Per le iscrizioni Community, è possibile abilitare o disabilitare la possibilità per un membro di pubblicare contenuto rispondendo a un&#39;e-mail.

* Individua il `AEM Communities Email Reply Configuration`
* Selezionate l’icona di modifica
* Verifica che il **nome** sia `subscriptions-email`

![chlimage_1-101](assets/chlimage_1-101.png)

* **[!UICONTROL Nome]** : *(obbligatorio)* `subscriptions-email`. Non Modificate.

* **[!UICONTROL Crea post dal messaggio e-mail]** di risposta: Se questa opzione è attivata, il destinatario dell&#39;e-mail di iscrizione può inviare contenuti inviando una risposta. Il valore predefinito è selezionato.
* **[!UICONTROL Aggiungi ID tracciato all’intestazione]**:Il valore predefinito è `Reply-To`.

* **[!UICONTROL Lunghezza massima del soggetto]**: Se l’ID tracciatore viene aggiunto all’oggetto, si tratta della lunghezza massima dell’oggetto, escluso l’ID tracciato, dopo di che verrà tagliato. Tieni presente che questo deve essere il più piccolo possibile per evitare che le informazioni ID tracciate vadano perdute. Il valore predefinito è 200.
* **[!UICONTROL Indirizzo]**&quot;Da&quot; e-mail: *(obbligatorio)* Indirizzo da cui verrà inviato il messaggio e-mail di notifica. Probabilmente lo stesso utente **** SMTP specificato per il servizio [di posta](#configuredefaultmailservice)predefinito. Default is `no-reply@example.com`.

* **[!UICONTROL Risposta al carattere di delimitazione]**: Se viene aggiunto l’ID tracciatore all’intestazione Rispondi a, verrà utilizzato questo delimitatore. Il valore predefinito è `+` (segno più).

* **[!UICONTROL Prefisso ID tracciatore nell’oggetto]**: Se alla riga dell’oggetto viene aggiunto l’ID tracciatore, verrà utilizzato questo prefisso. Default is `post#`.

* **[!UICONTROL Prefisso ID tracciatore nel corpo]** del messaggio: Se viene aggiunto l’ID tracciatore al corpo del messaggio, verrà utilizzato questo prefisso. Default is `Please do not remove this:`.

* **[!UICONTROL E-mail come HTML]**: Se questa opzione è selezionata, il tipo di contenuto dell’e-mail verrà impostato come `"text/html;charset=utf-8"`. Il valore predefinito è selezionato.

* **[!UICONTROL Nome]** utente predefinito: Questo nome verrà utilizzato per gli utenti senza nome. Default is `no-reply@example.com`.

* **[!UICONTROL Percorso]** principale dei modelli: L&#39;e-mail viene creata utilizzando il modello memorizzato in questo percorso principale. Default is `/etc/community/templates/subscriptions-email`.

## Configurare Importazione polling {#configure-polling-importer}

Affinché l’e-mail possa essere inserita nella directory archivio, è necessario configurare manualmente un modulo di importazione polling e configurarne le proprietà nella directory archivio.

### Aggiungi nuovo importatore di polling {#add-new-polling-importer}

* Nell&#39;editore principale
* Accesso con privilegi di amministratore
* Passare alla console di importazione pollingAd esempio, [http://localhost:4503/etc/importers/polling.html](http://localhost:4503/etc/importers/polling.html)
* Seleziona **[!UICONTROL Aggiungi]**

![chlimage_1-102](assets/chlimage_1-102.png)

* **[!UICONTROL Tipo]**: *(richiesto)* Per selezionare `POP3 (over SSL).`

* **[!UICONTROL URL]**: *(obbligatorio)* Il server di posta in uscita. Esempio, `pop.gmail.com:995/INBOX?username=community-emailgmail.com&password=****`

* **[!UICONTROL Importa in percorso]**&amp;ast;: *(richiesto)* Impostate su `/content/usergenerated/mailFolder/postEmails`visitando la `postEmails`cartella e selezionando **OK**

* **[!UICONTROL Intervallo di aggiornamento in secondi]**: *(facoltativo)* Il server di posta configurato per il servizio di posta elettronica predefinito può presentare requisiti relativi al valore dell&#39;intervallo di aggiornamento. Ad esempio, Gmail potrebbe richiedere un intervallo di `300`.

* **[!UICONTROL Login]**: *(facoltativo)*

* **[!UICONTROL Password]**: *(facoltativo)*

* Selezionare **[!UICONTROL OK]**

### Regola protocollo per il nuovo importatore di polling {#adjust-protocol-for-new-polling-importer}

Una volta salvata la nuova configurazione di polling, è necessario modificare ulteriormente le proprietà di Subscription Email Importer per cambiare il protocollo da `POP3` a `emailreply`

Utilizzo di [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md):

* Nell&#39;editore principale
* Accesso con privilegi di amministratore
* Individuate [https://&lt;server>:&lt;porta>/crx/de/index.jsp#/etc/importer/polling](http://localhost:4503/crx/de/index.jsp#/etc/importers/polling)
* Seleziona la configurazione appena creata
* Modificare le seguenti proprietà

   * **feedType**: sostituire `pop3s` con **`emailreply`**
   * **source**: sostituire il protocollo di origine `pop3s://` con **`emailreply://`**

![chlimage_1-103](assets/chlimage_1-103.png)

I triangoli rossi indicano le proprietà modificate. Salvare le modifiche:

* Seleziona **[!UICONTROL Salva tutto]**

