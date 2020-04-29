---
title: Login tramite social network con Facebook e Twitter
seo-title: Login tramite social network con Facebook e Twitter
description: Il login mediante profilo sociale consente ai visitatori del sito di accedere con il proprio account Facebook o Twitter.
seo-description: Il login mediante profilo sociale consente ai visitatori del sito di accedere con il proprio account Facebook o Twitter.
uuid: f70e346e-0d8c-41a0-a100-206a420088dc
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: c0a71870-8f95-40c8-9ffd-b7af49723288
translation-type: tm+mt
source-git-commit: 3296db289b2e2f4ca0d1981597ada6ca1310bd46

---


# Login tramite social network con Facebook e Twitter {#social-login-with-facebook-and-twitter}

Il login mediante profilo sociale è la capacità di presentare a un visitatore del sito l’opzione per accedere con il proprio account Facebook o Twitter. Pertanto, includendo i dati Facebook o Twitter consentiti nel profilo membro AEM.

![sociinweretail](assets/socialloginweretail.png)

## Panoramica di accesso tramite social network {#social-login-overview}

Per includere il login mediante social network, è *necessario* creare applicazioni Facebook e Twitter personalizzate.

L’esempio di vendita al dettaglio fornisce esempi di app Facebook e Twitter e servizi cloud, ma non sono disponibili in un sito Web [di](../../help/sites-administering/production-ready.md)produzione.

I passaggi necessari sono:

1. [Abilita autenticazione](#adobe-granite-oauth-authentication-handler) OAuth su tutte le istanze di pubblicazione AEM.

   Senza OAuth abilitato, i tentativi di accesso non riescono.

1. **Create** un&#39;app social e un servizio cloud.

   * Per supportare l’accesso con Facebook:

      * Create un&#39;app [](#create-a-facebook-app)Facebook.
      * Create e pubblicate un servizio [cloud di](#create-a-facebook-connect-cloud-service)Facebook Connect.
   * Per supportare l&#39;accesso con Twitter:

      * Create un&#39;app [](#create-a-twitter-app)Twitter.
      * Create e pubblicate un servizio [cloud di](#create-a-twitter-connect-cloud-service)Twitter Connect.


1. [**Abilitate **il login](#enable-social-login)mediante profilo sociale per un sito della community.

Esistono due concetti fondamentali:

1. **Ambito** (autorizzazioni) specifica i dati che l&#39;app può richiedere.

   * Per impostazione predefinita, le istanze di Facebook e Twitter [Adobe Granite OAuth Application e Provider](#adobe-granite-oauth-application-and-provider) includono le autorizzazioni di base dell&#39;app all&#39;interno del loro ambito.

1. **Campi** (params) specifica i dati effettivi richiesti utilizzando i parametri URL.

   * Questi campi sono specificati in [AEM Communities Facebook OAuth Provider](#aem-communities-facebook-oauth-provider) e [AEM Communities OAuth Provider](#aem-communities-twitter-oauth-provider)di Twitter.
   * I campi predefiniti sono sufficienti per la maggior parte dei casi di utilizzo ma possono essere modificati.

## Login Facebook {#facebook-login}

### Versione API Facebook {#facebook-api-version}

L&#39;accesso ai social network e l&#39;esempio di Facebook per la vendita al dettaglio sono stati sviluppati quando l&#39;API Facebook Graph era versione 1.0.
A partire da AEM 6.4 GA e AEM 6.3 SP1 l’accesso ai social network è stato aggiornato per funzionare con la nuova versione di Facebook Graph API 2.5.

>[!NOTE]
>
>Per le versioni precedenti di AEM, se si riscontra un’eccezione nei registri **Non è possibile estrarre un token da questo**, eseguire l’aggiornamento all’ultimo CFP per la versione di AEM.


Per informazioni sulla versione dell&#39;API di Facebook Graph, consultate la finestra di dialogo della modifica dell&#39;API di [Facebook](https://developers.facebook.com/docs/apps/changelog).

### Creare un&#39;app Facebook {#create-a-facebook-app}

Per abilitare l&#39;accesso ai social network di Facebook è necessaria un&#39;applicazione Facebook configurata correttamente.

Per creare un’applicazione Facebook, seguite le istruzioni di Facebook all’indirizzo [https://developers.facebook.com/apps/](https://developers.facebook.com/apps/). Le modifiche apportate alle relative istruzioni non sono riportate nelle seguenti informazioni.

In generale, a partire dall&#39;API Facebook v2.7:

* *Aggiungere una nuova app Facebook*
   * Per *Piattaforma*, scegliete Sito Web:
      * Per URL ** sito, immettete `  https://<server>:<port>.`
      * Per Nome ** visualizzato, immettete un titolo da usare come Titolo del servizio di connessione di Facebook.
      * Per *Categoria*, si consiglia di scegliere *App per Pagine*, ma può essere qualsiasi cosa.
      * *Aggiungi prodotto:  Login Facebook*
      * Per gli URI di reindirizzamento OAuth *validi*, immettere `  https://<server>:<port>.`

>[!NOTE]
>
>Per lo sviluppo, http://localhost:4503 funzionerà.


Una volta creata l&#39;applicazione, individua le impostazioni ID **** app e Segreto **** app. Queste informazioni sono necessarie per configurare il servizio [cloud di](#createafacebookcloudservice)Facebook.

### Creare un servizio Facebook Connect Cloud {#create-a-facebook-connect-cloud-service}

L&#39;istanza di [Adobe Granite OAuth Application and Provider](https://chl-author.corp.adobe.com/content/help/en/experience-manager/6-4/communities/using/social-login.html#AdobeGraniteOAuthApplicationandProvider) , creata mediante la creazione di una configurazione di servizio cloud, identifica l&#39;applicazione Facebook e i gruppi membri ai quali vengono aggiunti i nuovi utenti.

1. Nell’istanza di creazione di AEM, effettuate l’accesso con privilegi di amministratore.
1. Dalla navigazione globale, selezionate **[!UICONTROL Strumenti]** > Servizi **** cloud > Configurazione **[!UICONTROL accesso]** Facebook Social.
1. Selezionare il percorso **[!UICONTROL del]** contesto di configurazione.

   **[!UICONTROL Il percorso]** di contesto deve corrispondere al percorso di configurazione cloud selezionato durante la creazione o la modifica di un sito community.

1. Controlla se il percorso contestuale è abilitato per creare servizi cloud al di sotto di esso.
1. Scegliere **[!UICONTROL Strumenti]** > **[!UICONTROL Generale]** > **[!UICONTROL Browser]** di configurazione. Seleziona il contesto e modifica le proprietà. Abilita configurazioni cloud se non ancora abilitata.

   ![config-properties](assets/config-propertiespng.png)

1. **Creare/modificare** la configurazione del servizio cloud di Facebook.

   ![fbsociloginconfigpng](assets/fbsocialloginconfigpng.png)

   * **[!UICONTROL Titolo]** (*obbligatorio*) Immettete un titolo di visualizzazione che identifichi l’app Facebook. Si consiglia di utilizzare lo stesso nome immesso come Nome ** visualizzato per l&#39;app Facebook.
   * **[!UICONTROL ID]** app/ChiaveAPI (*richiesta*) Immettere l&#39;ID ****** app per l&#39;app Facebook. Questo identifica l&#39;istanza di applicazione e provider [OAuth](https://helpx.adobe.com/experience-manager/6-3/communities/using/social-login.html#AdobeGraniteOAuthApplicationandProvider) Adobe Granite creata dalla finestra di dialogo.
   * **[!UICONTROL Segreto]** app (*obbligatorio*) Immetti il Segreto ****** app per l&#39;app Facebook.
   * **[!UICONTROL Crea utenti]** Se questa opzione è attivata, l&#39;accesso con un account Facebook creerà una voce utente AEM e la aggiungerà come membro al gruppo o ai gruppi di utenti selezionati.  Il valore predefinito è selezionato (fortemente consigliato).
   * **[!UICONTROL Mascherare gli ID]** utente: Lascia deselezionato.
   * **[!UICONTROL E-mail]** ambito: l’ID e-mail dell’utente deve essere recuperato da Facebook.
   * **[!UICONTROL Aggiungi a gruppi]** di utenti selezionate Aggiungi gruppo di utenti per scegliere uno o più gruppi [di](https://helpx.adobe.com/experience-manager/6-3/communities/using/users.html) membri per il sito della community a cui verranno aggiunti gli utenti.
   >[!NOTE]
   >
   >I gruppi possono essere aggiunti o rimossi in qualsiasi momento. Ma le appartenenze degli utenti esistenti non ne saranno influenzate. L&#39;iscrizione automatica si applica solo ai nuovi utenti che vengono creati dopo l&#39;aggiornamento di questo campo. Per i siti in cui gli utenti anonimi sono disabilitati, scegliere di aggiungere utenti al gruppo di membri della community corrispondente destinato a tale sito community chiuso.

   * Select **[!UICONTROL SAVE]**.
   * **[!UICONTROL Pubblicazione]**.




Il risultato è un&#39;istanza [Adobe Granite OAuth Application e Provider](https://helpx.adobe.com/experience-manager/6-3/communities/using/social-login.html#adobe-granite-oauth-application-and-provider) che non richiede ulteriori modifiche a meno che non venga aggiunto ulteriore ambito (autorizzazioni). L’ambito predefinito è quello standard per l’accesso a Facebook. Se si desidera un ulteriore ambito, è necessario modificare direttamente la configurazione OSGI. In caso di modifiche effettuate direttamente tramite il sistema o la console, evitate di modificare le configurazioni del servizio cloud dall’interfaccia touch per evitare la sovrascrittura.

### Provider OAuth Facebook di AEM Communities {#aem-communities-facebook-oauth-provider}

Il provider AEM Communities estende l’istanza di [Adobe Granite OAuth Application e Provider](#adobe-granite-oauth-application-and-provider) .

Questo provider richiederà la modifica per:

* Consenti aggiornamenti utente
* Aggiunta di campi aggiuntivi [all&#39;interno dell&#39;ambito](#adobe-granite-oauth-application-and-provider)

   * Per impostazione predefinita, non tutti i campi consentiti per impostazione predefinita sono inclusi.

Se la modifica è necessaria, in ogni istanza di pubblicazione AEM:

1. Effettuate l&#39;accesso con privilegi di amministratore.
1. Passate alla console [](../../help/sites-deploying/configuring-osgi.md)Web. Ad esempio, http://localhost:4503/system/console/configMgr.
1. Individua il provider OAuth di Facebook di AEM Communities.
1. Selezionate l’icona matita da aprire per la modifica.

   ![fboauthprov_png](assets/fboauthprov_png.png)

   * **[!UICONTROL ID provider OAuth]**

      (*Obbligatorio*) Il valore predefinito è *soco-facebook*. Non modificare.

   * **[!UICONTROL Configurazione servizio cloud]**

      Il valore predefinito è `/etc/  cloudservices /  facebookconnect`. Non modificare.

   * **[!UICONTROL Configurazione servizio provider OAuth]**

      Il valore predefinito è `/apps/social/facebookprovider/config/`. Non modificare.

   * **[!UICONTROL Abilita tag]**

      Non modificare.

   * **[!UICONTROL Percorso utente]**

      Posizione nella directory archivio in cui sono memorizzati i dati utente. Per un sito community, per garantire ai membri le autorizzazioni necessarie per visualizzare il profilo dell&#39;altro, il percorso deve essere quello predefinito */home/users/community*.

   * **[!UICONTROL Abilita campi]**

      Se questa opzione è selezionata, i campi elencati vengono specificati nella richiesta a Facebook per l’autenticazione dell’utente e le informazioni. Il valore predefinito è deselezionato.

   * **[!UICONTROL espandibili]**

      Quando i campi sono attivati, quando si chiama l&#39;API di Facebook Graph vengono inclusi i campi seguenti. I campi devono essere consentiti all&#39;interno dell&#39;ambito definito nella configurazione del servizio cloud. Altri campi potrebbero richiedere l’approvazione di Facebook. Fate riferimento alla sezione Autorizzazioni di accesso a Facebook della documentazione di Facebook. I campi predefiniti aggiunti come parametri sono:

      * id
      * nome
      * first_name
      * last_name
      * Collegamento
      * locale
      * picture
      * timezone
      * update_time
      * verificato
      * e-mail
   Se viene aggiunto o modificato un campo, aggiornate la configurazione del gestore di sincronizzazione predefinito corrispondente per correggere il mapping.

   * **[!UICONTROL Aggiorna utente]**

      Se questa opzione è attivata, aggiorna i dati utente presenti nella directory archivio su ogni login in modo che riflettano le modifiche del profilo o i dati aggiuntivi richiesti. Il valore predefinito è deselezionato.


#### Passaggi successivi {#next-steps}

I passaggi successivi sono gli stessi sia per Facebook che per Twitter:

* [Pubblicare le configurazioni del servizio cloud](#publishcloudservices)
* [Abilita per un sito community](#enable-social-login)

## Login Twitter {#twitter-login}

### Creare un&#39;app Twitter {#create-a-twitter-app}

Per abilitare l&#39;accesso ai social network per Twitter è necessaria un&#39;applicazione Twitter configurata.

Seguite le istruzioni più recenti per creare una nuova applicazione Twitter all&#39;indirizzo [https://apps.twitter.com](https://apps.twitter.com/).

In generale:

1. Immettete un *nome* per identificare l’applicazione Twitter per gli utenti del sito Web.
1. Inserire una *descrizione*.
1. Per *sito* Web - immettere `https://<server>`.
1. Per URL ** callback - immettere `https://server`.

   >[!NOTE]
   >
   >Non è necessario specificare la porta.
   >
   >Per lo sviluppo, https://127.0.0.1/ funzionerà.

1. Una volta creata l&#39;applicazione, individua la chiave **[!UICONTROL Consumer (API) Key]** and **[!UICONTROL Consumer (API) Secret]**(Segreto API). Queste informazioni saranno necessarie per configurare il servizio [cloud](#createatwittercloudservice)Twitter.

#### Autorizzazioni  {#permissions}

Nella sezione delle autorizzazioni della gestione dell&#39;applicazione Twitter:

* **[!UICONTROL Accesso]**: Selezionare `Read only`.

   * Altre opzioni non sono supportate

* **[!UICONTROL Autorizzazioni]** aggiuntive: Facoltativamente, scegliete `Request email addresses from users`.

   * Se non è selezionato, il profilo utente in AEM non includerà il proprio indirizzo e-mail.
   * Le istruzioni di Twitter indicano ulteriori passi da compiere.

L&#39;unica richiesta REST fatta per l&#39;accesso tramite social network è di *[GET account/credenziali](https://dev.twitter.com/rest/reference/get/account/verify_credentials)*di verifica.

### Creare un servizio Twitter Connect Cloud {#create-a-twitter-connect-cloud-service}

L&#39;istanza di [Adobe Granite OAuth Application and Provider](#adobe-granite-oauth-application-and-provider) , creata mediante la creazione di una configurazione di servizio cloud, identifica l&#39;applicazione Twitter e i gruppi membri ai quali vengono aggiunti i nuovi utenti.

1. Nell’istanza di creazione, effettuate l’accesso con privilegi di amministratore.
1. Dalla navigazione globale, selezionate **[!UICONTROL Strumenti]** > Servizi **** cloud > Configurazione **[!UICONTROL accesso]** Twitter Social.
1. Scegliete la configurazione del percorso **** contestuale.

   Il percorso di contesto deve corrispondere al percorso di configurazione cloud selezionato durante la creazione o la modifica di un sito community.

1. Controlla se il percorso contestuale è abilitato per creare servizi cloud al di sotto di esso.
1. Scegliere **[!UICONTROL Strumenti]** > **[!UICONTROL Generale]** > **[!UICONTROL Browser]** di configurazione. Seleziona il contesto e modifica le proprietà. Abilita configurazioni cloud se non ancora abilitata.

   ![twitterconfigpropping](assets/twitterconfigproppng.png)

1. Creare/modificare la configurazione del servizio cloud di Twitter.

   ![twittersociloginping](assets/twittersocialloginpng.png)

   * **[!UICONTROL Titolo]**

      (*Obbligatorio*) Immettete un titolo di visualizzazione che identifichi l&#39;app Twitter. Si consiglia di utilizzare lo stesso nome immesso come Nome ** visualizzato per l&#39;app Twitter.

   * **[!UICONTROL Chiave consumer]**

      (*Obbligatorio*) Immettete la chiave **** consumer (API) per l&#39;app Twitter. Questo identifica l&#39;istanza di applicazione e provider [OAuth](https://helpx.adobe.com/experience-manager/6-3/communities/using/social-login.html#AdobeGraniteOAuthApplicationandProvider) Adobe Granite creata dalla finestra di dialogo.

   * **[!UICONTROL Segreto consumer]**

      (*Obbligatorio*) Immetti il segreto ***Consumer(API)*** per l&#39;app Twitter.

   * **[!UICONTROL Crea utenti]**

      Se questa opzione è attivata, l&#39;accesso con un account Twitter creerà una voce utente AEM e la aggiungerà come membro al gruppo o ai gruppi di utenti selezionati. Il valore predefinito è selezionato (fortemente consigliato).

   * **[!UICONTROL Maschera ID utenti]**

      Lascia deselezionato.

   * **[!UICONTROL Aggiungi a gruppo di utenti]**

      Selezionate Aggiungi gruppo di utenti per scegliere uno o più gruppi [di](https://helpx.adobe.com/experience-manager/6-3/communities/using/users.html) membri per il sito della community a cui verranno aggiunti gli utenti.
   >[!NOTE]
   >
   >I gruppi possono essere aggiunti o rimossi in qualsiasi momento. Ma le appartenenze degli utenti esistenti non ne saranno influenzate. L&#39;iscrizione automatica si applica solo ai nuovi utenti che vengono creati dopo l&#39;aggiornamento di questo campo. Per i siti in cui gli utenti anonimi sono disabilitati, aggiungete utenti al gruppo di membri della comunità corrispondente destinato a tale sito della comunità chiuso.

1. Selezionate **[!UICONTROL SALVA]** e **[!UICONTROL Pubblica]**.

Il risultato è un&#39;istanza [Adobe Granite OAuth Application e Provider](https://helpx.adobe.com/experience-manager/6-3/communities/using/social-login.html#adobe-granite-oauth-application-and-provider) che non richiede ulteriori modifiche. L’ambito predefinito è quello standard per le autorizzazioni di accesso a Twitter.

### Provider OAuth Twitter di AEM Communities {#aem-communities-twitter-oauth-provider}

La configurazione di AEM Communities estende l’istanza di [Adobe Granite OAuth Application e Provider](#adobe-granite-oauth-application-and-provider) . Per consentire gli aggiornamenti degli utenti, questo provider richiederà la modifica.

Se la modifica è necessaria, in ogni istanza di pubblicazione AEM:

1. Effettuate l&#39;accesso con privilegi di amministratore.
1. Passate alla console [](../../help/sites-deploying/configuring-osgi.md)Web.

   Ad esempio, http://localhost:4503/system/console/configMgr.

1. Individua provider OAuth Twitter di AEM Communities.
1. Selezionate l’icona matita da aprire per la modifica.

   ![twitteroauth_png](assets/twitteroauth_png.png)

   * **[!UICONTROL ID provider OAuth]**
   (*Obbligatorio*) Il valore predefinito è *soco-twitter*. Non modificare.

   * **[!UICONTROL Configurazione servizio cloud]**

      The default value is *conf.* Non modificare.

   * **[!UICONTROL Configurazione servizio provider OAuth]**

      Il valore predefinito è `/apps/social/twitterprovider/config/`. Non modificare.

   * **[!UICONTROL Percorso utente]**

      Posizione nella directory archivio in cui sono memorizzati i dati utente. Per un sito community, per garantire ai membri le autorizzazioni necessarie per visualizzare il profilo dell&#39;altro, il percorso deve essere quello predefinito `/home/users/community`.

   * **[!UICONTROL Abilita parametri]** non modificati
   * **[!UICONTROL I parametri]** URL non vengono modificati
   * **[!UICONTROL Aggiorna utente]**

      Se questa opzione è attivata, aggiorna i dati utente presenti nella directory archivio su ogni login in modo che riflettano le modifiche del profilo o i dati aggiuntivi richiesti. Il valore predefinito è deselezionato.


#### Passaggi successivi {#next-steps-1}

I passaggi successivi sono gli stessi sia per Facebook che per Twitter:

* [Pubblicare le configurazioni del servizio cloud](#publishcloudservices)
* [Abilita per un sito community](#enable-social-login)

## Abilita login per social network {#enable-social-login}

### Console Siti di AEM Communities {#aem-communities-sites-console}

Una volta configurato, il servizio cloud potrebbe essere abilitato per l&#39;impostazione di accesso tramite social network pertinente per un sito community tramite il sottopannello Impostazioni di gestione [](https://helpx.adobe.com/experience-manager/6-3/communities/using/sites-console.html#USERMANAGEMENT) utente durante la [creazione](https://helpx.adobe.com/experience-manager/6-3/communities/using/sites-console.html#SiteCreation) o la [gestione](https://helpx.adobe.com/experience-manager/6-3/communities/using/sites-console.html#ModifyingSiteProperties)di un sito community.

1. Scegliete il contesto di configurazione del sito in cui avete salvato le configurazioni di accesso mediante social network.

1. Nella scheda Generale, impostate le configurazioni cloud.

   ![managesites_png](assets/managesites_png.png)

1. Nella scheda Settings (Impostazioni), abilita **[!UICONTROL Social Logins (Accesso social network)]** e Salva.

   ![usermgmt_png](assets/usermgmt_png.png)

## Test login Social {#test-social-login}

* Assicurarsi che [Adobe Granite OAuth Authentication Handler](#adobe-granite-oauth-authentication-handler) sia stato abilitato su tutte le istanze di pubblicazione.
* Verifica che i servizi cloud siano stati pubblicati.
* Assicurati che il sito della community sia stato pubblicato.
* Avviate il sito pubblicato in un browser.
Ad esempio, http://localhost:4503/content/sites/engage/en.html
* Selezionate **[!UICONTROL Accesso]**.
* Selezionate **[!UICONTROL Accedi con Facebook]** o **[!UICONTROL Accedi con Twitter]**.
* Se non avete già eseguito l&#39;accesso a Facebook o Twitter, effettuate l&#39;accesso con le credenziali appropriate.
* Potrebbe essere necessario concedere l&#39;autorizzazione in base alla finestra di dialogo visualizzata dall&#39;app Facebook o Twitter.
* La barra degli strumenti nella parte superiore della pagina viene aggiornata per riflettere l’accesso effettuato correttamente.
* Seleziona **[!UICONTROL profilo]**: nella pagina Profilo vengono visualizzati l’immagine avatar dell’utente, il nome e il cognome. Vengono inoltre visualizzate le informazioni del profilo Facebook o Twitter in base ai campi/param consentiti.

## Configurazioni OAuth della piattaforma AEM {#aem-platform-oauth-configurations}

### Gestore autenticazione OAuth di Adobe Granite {#adobe-granite-oauth-authentication-handler}

Per impostazione predefinita `Adobe Granite OAuth Authentication Handler` non è attivato e ***deve essere attivato su tutte le istanze di pubblicazione AEM.***

Per attivare il gestore di autenticazione al momento della pubblicazione, è sufficiente aprire la configurazione OSGi e salvarla:

* Effettuate l&#39;accesso con privilegi di amministratore.
* Passate alla console [](../../help/sites-deploying/configuring-osgi.md)Web.
Ad esempio, http://localhost:4503/system/console/configMgr
* Individua `Adobe Granite OAuth Authentication Handler`.
* Selezionate per aprire la configurazione per la modifica.
* Seleziona **[!UICONTROL Salva]**.

![chlimage_1-489](assets/chlimage_1-489.png)

>[!CAUTION]
>
>Fare attenzione a non confondere il gestore di autenticazione con un&#39;istanza Facebook o Twitter di *Adobe Granite OAuth Application and Provider*.


![chlimage_1-490](assets/chlimage_1-490.png)

### Applicazione e provider OAuth di Adobe Granite {#adobe-granite-oauth-application-and-provider}

Quando viene creato un servizio cloud per Facebook o Twitter, `Adobe Granite OAuth Authentication Handler` viene creata un’istanza di

Per individuare l&#39;istanza creata per un&#39;app Facebook o Twitter:

1. Effettuate l&#39;accesso con privilegi di amministratore.
1. Passate alla console [](../../help/sites-deploying/configuring-osgi.md)Web.

   Ad esempio, http://localhost:4503/system/console/configMgr.

1. Individuate l&#39;applicazione e il provider OAuth di Adobe Granite.

   * Individuate l&#39;istanza in cui l&#39;ID **** client corrisponde all&#39;ID **** app.

      ![chlimage_1-491](assets/chlimage_1-491.png)

      Ad eccezione delle seguenti proprietà, lasciare invariate le altre proprietà della configurazione:

   * **[!UICONTROL ID configurazione]**

      (*Obbligatorio*) Gli ID di configurazione OAuth devono essere univoci. Generazione automatica quando viene creato il servizio cloud.

   * **[!UICONTROL ID client]**

      (*Obbligatorio*) L&#39;ID applicazione fornito al momento della creazione del servizio cloud.

   * **[!UICONTROL Segreto client]**

      (*Obbligatorio*) Il segreto dell&#39;applicazione fornito al momento della creazione del servizio cloud.

   * **[!UICONTROL Ambito]**

      (*Facoltativo*) È possibile richiedere al provider un ambito aggiuntivo per quanto consentito. L&#39;ambito predefinito copre le autorizzazioni necessarie per fornire l&#39;autenticazione social e i dati del profilo.

   * **[!UICONTROL ID fornitore]**

      (*Obbligatorio*) L&#39;ID fornitore per AEM Communities viene impostato al momento della creazione del servizio cloud. Non modificare. Per Facebook Connect, il valore è *Facebook*. Per Twitter Connect, il valore è *soco-twitter*.

   * **[!UICONTROL Gruppi]**

      (*consigliato*) Uno o più gruppi di membri a cui vengono aggiunti gli utenti creati. Per AEM Communities, si consiglia di elencare il gruppo di membri per il sito community.

   * **[!UICONTROL URL callback]**

      (*Facoltativo*) URL configurato con i provider OAuth per reindirizzare il client. Utilizzate un URL relativo per utilizzare l&#39;host della richiesta originale. Lasciate vuoto per usare l’URL originariamente richiesto. Il suffisso &quot;/callback/j_security_check&quot; viene aggiunto automaticamente a questo URL.
   >[!NOTE]
   >
   >Il dominio per il callback deve essere registrato con il provider (Facebook o Twitter).

Per ogni configurazione del gestore di autenticazione OAuth, nell&#39;istanza sono state create due configurazioni aggiuntive:

* Gestore di sincronizzazione predefinito Apache Jackrabbit Oak (org.apache.jackrabbit.oak.security.authentication.external.impl.DefaultSyncHandler) - Non sono necessarie modifiche, ma è possibile esaminare le mappature dei campi utente in modo che i campi Facebook siano mappati a un nodo di profilo utente CQ. Inoltre, &#39;Sync Handler Name&#39; corrisponde all&#39;ID di configurazione del provider OAuth.
* Modulo di accesso esterno Apache Jackrabbit Oak (org.apache.jackrabbit.oak.spi.security.authentication.external.impl.ExternalLoginModuleFactory) - Non sono necessarie modifiche, ma potete notare che &#39;Nome provider identità&#39; e &#39;Nome gestore sincronizzazione&#39; sono uguali e puntare rispettivamente alle corrispondenti configurazioni OAuth e del gestore di sincronizzazione.

Per ulteriori informazioni, consultate [Autenticazione con modulo](https://jackrabbit.apache.org/oak/docs/security/authentication/externalloginmodule.html)di login esterno Apache Oak.

## Prestazioni delle transizioni utente OAuth {#oauth-user-traversal-performance}

Per i siti della community che visualizzano centinaia di migliaia di utenti registrati con il proprio login Facebook o Twitter, le prestazioni traverse della query eseguite quando un visitatore del sito utilizza il proprio profilo sociale possono essere migliorate aggiungendo il seguente indice Oak.

Se nei registri sono visibili avvisi di attraversamento, è consigliabile aggiungere questo indice.

Per un’istanza di authoring, effettuate l’accesso con privilegi amministrativi:

1. Dalla navigazione globale: selezionare **Strumenti,[CRX/DE Lite](../../help/sites-developing/developing-with-crxde-lite.md).**
1. Create un indice denominato ntBaseLucene-oauth da una copia di ntBaseLucene:

   * Sotto il nodo `/oak:index`
   * Seleziona nodo `ntBaseLucene`
   * Seleziona **[!UICONTROL copia]**
   * Seleziona `/oak:index`
   * Seleziona **[!UICONTROL Incolla]**
   * Rinomina copia di ntBaseLucene in `ntBaseLucene-oauth`

1. Modificare le proprietà del nodo ntBaseLucene-oauth:

   * **[!UICONTROL indexPath]**: `/oak:index/ntBaseLucene-oauth`
   * **[!UICONTROL name]**: `oauthid-123****`
   * **[!UICONTROL reindex]**: `true`
   * **[!UICONTROL reindexCount]**: `1`

1. Sotto il nodo /oak:index/ntBaseLucene-oauth/indexRules/nt:base/properties:

   * Eliminate tutti i nodi secondari, ad eccezione di cqTags.
   * Rinomina i tag cq in `oauthid-123****`
   * Modifica delle proprietà del nodo `oauthid-123****`

      * **[!UICONTROL name]**: `oauthid-123****`
   * Selezionate **[!UICONTROL Salva tutto]**.


* Per il **nome** `oauthid-123`, sostituite *123* con l&#39;ID ****** app Facebook o la chiave ***Twitter*** Consumer (API) che è il valore dell&#39;ID **** [](social-login.md#adobe-granite-oauth-application-and-provider) client nella configurazione dell&#39;applicazione e del provider OAuth di Granite.

   ![chlimage_1-492](assets/chlimage_1-492.png)

Per ulteriori informazioni e strumenti, consultate Query [quercia e indicizzazione](../../help/sites-deploying/queries-and-indexing.md).

## Dispatcher Configuration {#dispatcher-configuration}

Consultate [Configurazione del dispatcher per Communities](dispatcher.md).
