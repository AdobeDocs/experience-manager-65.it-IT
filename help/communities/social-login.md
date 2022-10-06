---
title: Accesso social con Facebook e Twitter
seo-title: Social Login with Facebook and Twitter
description: L’accesso Social consente ai visitatori del sito di accedere con il loro account Facebook o Twitter.
seo-description: Social login lets site visitors to sign in with their Facebook or Twitter account.
uuid: f70e346e-0d8c-41a0-a100-206a420088dc
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: c0a71870-8f95-40c8-9ffd-b7af49723288
role: Admin
exl-id: aed9247c-eb81-470c-9fa4-a98c3df2dcaa
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '2783'
ht-degree: 1%

---

# Accesso social con Facebook e Twitter {#social-login-with-facebook-and-twitter}

L&#39;accesso per social network è la capacità di presentare a un visitatore del sito l&#39;opzione per accedere con il proprio account Facebook o Twitter. Pertanto, includendo i dati Facebook o Twitter consentiti nel profilo membro AEM.

![sociweretail](assets/socialloginweretail.png)

## Panoramica dell’accesso social network {#social-login-overview}

Per includere l&#39;accesso social, è *obbligatorio* per creare applicazioni Facebook e Twitter personalizzate.

Mentre l’esempio di we-retail fornisce app e servizi cloud di esempio per Facebook e Twitter, non sono disponibili su un [sito web di produzione](../../help/sites-administering/production-ready.md).

I passaggi necessari sono i seguenti:

1. [Abilita autenticazione OAuth](#adobe-granite-oauth-authentication-handler) su tutte AEM istanze di pubblicazione.

   Senza OAuth abilitato, i tentativi di accesso non riescono.

1. **Crea** un’app social e un servizio cloud.

   * Per supportare l’accesso con Facebook:

      * Crea un [app facebook](#create-a-facebook-app).
      * Creare e pubblicare un [Servizio cloud facebook Connect](#create-a-facebook-connect-cloud-service).
   * Per supportare l’accesso con Twitter:

      * Crea un [app twitter](#create-a-twitter-app).
      * Creare e pubblicare un [Servizio cloud twitter Connect](#create-a-twitter-connect-cloud-service).


1. [**Abilita** accesso social](#enable-social-login) per un sito della community.

Esistono due concetti fondamentali:

1. **Ambito** (autorizzazioni) specifica i dati che l&#39;app può richiedere.

   * Facebook e Twitter [Applicazione e provider OAuth di Adobe Granite](#adobe-granite-oauth-application-and-provider) Le istanze, per impostazione predefinita, includono le autorizzazioni dell&#39;app di base all&#39;interno del loro ambito.

1. **Campi** (params) specifica i dati effettivi richiesti utilizzando i parametri URL.

   * Questi campi sono specificati in [Provider OAuth di AEM Communities Facebook](#aem-communities-facebook-oauth-provider) e [Provider OAuth di AEM Communities Twitter](#aem-communities-twitter-oauth-provider).
   * I campi predefiniti sono sufficienti per la maggior parte dei casi d’uso ma possono essere modificati.

## Accesso facebook {#facebook-login}

### Versione API di facebook {#facebook-api-version}

L’accesso social network e l’esempio di Facebook per la vendita al dettaglio sono stati sviluppati quando l’API grafico Facebook era versione 1.0. A partire AEM 6.4 GA e AEM 6.3 SP1 l’accesso social era stato aggiornato per funzionare con la nuova versione di Facebook Graph API 2.5.

>[!NOTE]
>
>Per le versioni AEM precedenti, se si sta riscontrando un&#39;eccezione nei registri **Impossibile estrarre un token da questo**, effettua l’aggiornamento all’ultimo CFP per tale versione AEM.

Per informazioni sulla versione dell’API grafico di Facebook, consulta la sezione [changelog API di facebook](https://developers.facebook.com/docs/apps/changelog).

### Creare un’app Facebook {#create-a-facebook-app}

Per abilitare l&#39;accesso social a Facebook è necessaria un&#39;applicazione Facebook configurata correttamente.

Per creare un&#39;applicazione Facebook, segui le istruzioni Facebook disponibili all&#39;indirizzo [https://developers.facebook.com/apps/](https://developers.facebook.com/apps/). Le modifiche alle relative istruzioni non sono riportate nelle informazioni seguenti.

In generale, a partire dall’API Facebook v2.7:

* *Aggiungere una nuova app Facebook*
   * Per *Piattaforma*, scegli Sito Web:
      * Per *URL sito*, inserisci `  https://<server>:<port>.`
      * Per *Nome visualizzato*, inserisci un titolo da utilizzare come titolo del servizio di connessione Facebook.
      * Per *Categoria*, scelta consigliata *App per le pagine* Ma può essere qualsiasi cosa.
      * *Aggiungi prodotto: Accesso facebook*
      * Per *URI di reindirizzamento OAuth validi*, inserisci `  https://<server>:<port>.`

>[!NOTE]
>
>Per lo sviluppo, http://localhost:4503 funzionerà.

Una volta creata l&#39;applicazione, individua la **[!UICONTROL ID app]** e **[!UICONTROL Segreto app]** impostazioni. Queste informazioni sono necessarie per configurare il [Servizio cloud facebook](#createafacebookcloudservice).

### Creare un Cloud Service Facebook Connect {#create-a-facebook-connect-cloud-service}

La [Applicazione e provider OAuth di Adobe Granite](#adobe-granite-oauth-application-and-provider) istanza, creata mediante la creazione di una configurazione del servizio cloud, identifica l’applicazione Facebook e il gruppo o i gruppi di membri a cui vengono aggiunti i nuovi utenti.

1. Nell’istanza di authoring AEM, accedi con privilegi di amministratore.
1. Dalla navigazione globale, seleziona **[!UICONTROL Strumenti]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Configurazione dell&#39;accesso a facebook Social]**.
1. Seleziona la configurazione **[!UICONTROL percorso del contesto]**.

   **[!UICONTROL Percorso del contesto]** deve corrispondere al percorso di configurazione cloud selezionato durante la creazione/modifica di un sito community.

1. Controlla se il percorso contestuale è abilitato per creare servizi cloud sotto di esso.
1. Vai a **[!UICONTROL Strumenti]** > **[!UICONTROL Generale]** > **[!UICONTROL Browser di configurazione]**. Seleziona il tuo contesto e modifica le proprietà. Abilita le configurazioni cloud se non ancora abilitate.

   ![config-propertiespng](assets/config-propertiespng.png)

   * Consulta la sezione [Browser di configurazione](/help/sites-administering/configurations.md) documentazione per ulteriori informazioni.

1. **Crea/Modifica** Configurazione del servizio cloud facebook.

   ![fbsociloginconfigpng](assets/fbsocialloginconfigpng.png)

   * **[!UICONTROL Titolo]** (*Obbligatorio*) Immetti un titolo di visualizzazione che identifichi l’app Facebook. Si consiglia di utilizzare lo stesso nome immesso come *Nome visualizzato* per l’app Facebook.
   * **[!UICONTROL ID app/chiave API]** (*Obbligatorio*) Inserisci il ***ID app*** per l’app Facebook. In questo modo si identificano le [Applicazione e provider OAuth di Adobe Granite](https://helpx.adobe.com/experience-manager/6-3/communities/using/social-login.html#AdobeGraniteOAuthApplicationandProvider) istanza creata dalla finestra di dialogo.
   * **[!UICONTROL Segreto app]** (*Obbligatorio*) Inserisci il ***Segreto app*** per l’app Facebook.
   * **[!UICONTROL Creare utenti]** Se questa opzione è selezionata, l&#39;accesso con un account Facebook creerà una voce utente AEM e la aggiungerà come membro al gruppo o ai gruppi di utenti selezionati.  Il valore predefinito è selezionato (fortemente consigliato).
   * **[!UICONTROL Maschera ID utente]**: Lascia deselezionato .
   * **[!UICONTROL Ambito e-mail]**: l’id e-mail dell’utente deve essere recuperato da Facebook.
   * **[!UICONTROL Aggiungi a gruppi di utenti]** seleziona Aggiungi gruppo di utenti per scegliere uno o più [gruppi di membri](https://helpx.adobe.com/experience-manager/6-3/communities/using/users.html) per il sito community a cui verranno aggiunti gli utenti.

   >[!NOTE]
   >
   >I gruppi possono essere aggiunti o rimossi in qualsiasi momento. Ma le appartenenze degli utenti esistenti non saranno influenzate. L&#39;iscrizione automatica si applica solo ai nuovi utenti creati dopo l&#39;aggiornamento del campo. Per i siti in cui gli utenti anonimi sono disabilitati, scegliere di aggiungere utenti al gruppo corrispondente di membri della community destinato a quel sito community chiuso.

   * Seleziona **[!UICONTROL SALVA]**.
   * **[!UICONTROL Pubblicazione]**.


Il risultato è un [Applicazione e provider OAuth di Adobe Granite](https://helpx.adobe.com/experience-manager/6-3/communities/using/social-login.html#adobe-granite-oauth-application-and-provider) istanza che non richiede ulteriori modifiche a meno che non aggiunga ulteriore ambito (autorizzazioni). L’ambito predefinito è quello standard per l’accesso a Facebook. Se desideri un ambito aggiuntivo, è necessario modificare direttamente la configurazione OSGI. In caso di modifiche effettuate direttamente tramite sistema/console, evita di modificare le configurazioni del servizio cloud dall’interfaccia utente touch per evitare la sovrascrittura.

### Provider OAuth di AEM Communities Facebook {#aem-communities-facebook-oauth-provider}

Il provider AEM Communities estende la [Applicazione e provider OAuth di Adobe Granite](#adobe-granite-oauth-application-and-provider) istanza.

Questo provider richiederà la modifica per:

* Consenti aggiornamenti utente
* Aggiungi campi aggiuntivi [ambito](#adobe-granite-oauth-application-and-provider)

   * Per impostazione predefinita non tutti i campi consentiti per impostazione predefinita sono inclusi.

Se è necessaria la modifica, su ogni istanza di pubblicazione AEM:

1. Accedi con privilegi di amministratore.
1. Passa a [Console web](../../help/sites-deploying/configuring-osgi.md). Ad esempio, http://localhost:4503/system/console/configMgr.
1. Individua il provider OAuth di AEM Communities Facebook.
1. Seleziona l’icona a forma di matita da aprire per la modifica.

   ![fboauthprov_png](assets/fboauthprov_png.png)

   * **[!UICONTROL ID provider OAuth]**

      (*Obbligatorio*) Il valore predefinito è *soco-facebook*. Non modificare.

   * **[!UICONTROL Configurazione Cloud Service]**

      Il valore predefinito è `/etc/  cloudservices /  facebookconnect`. Non modificare.

   * **[!UICONTROL Configurazione del servizio del provider OAuth]**

      Il valore predefinito è `/apps/social/facebookprovider/config/`. Non modificare.

   * **[!UICONTROL Abilita tag]**

      Non modificare.

   * **[!UICONTROL Percorso utente]**

      Posizione nella directory archivio in cui sono archiviati i dati utente. Per un sito della community, per garantire ai membri le autorizzazioni necessarie per visualizzare il profilo degli altri, il percorso deve essere quello predefinito */home/users/community*.

   * **[!UICONTROL Abilita campi]**

      Se questa opzione è selezionata, i campi elencati vengono specificati nella richiesta ad Facebook per l’autenticazione e le informazioni dell’utente. Il valore predefinito è deselezionato.

   * **[!UICONTROL Campi]**

      Quando i campi sono abilitati, i campi seguenti sono inclusi quando si chiama l’API grafico di Facebook. I campi devono essere consentiti all’interno dell’ambito definito nella configurazione del servizio cloud. Per ulteriori campi potrebbe essere necessaria l’approvazione di Facebook. Consulta la sezione Autorizzazioni di accesso Facebook della documentazione Facebook . I campi predefiniti aggiunti come parametri sono:

      * id
      * name
      * nome_primo
      * cognome
      * Collegamento
      * locale
      * picture
      * fuso orario
      * update_time
      * verificato
      * e-mail

   Se viene aggiunto o modificato un campo, aggiorna la configurazione del gestore di sincronizzazione predefinita corrispondente per correggere la mappatura.

   * **[!UICONTROL Aggiorna utente]**

      Se questa opzione è selezionata, aggiorna i dati utente nell’archivio a ogni accesso per riflettere le modifiche del profilo o i dati aggiuntivi richiesti. Il valore predefinito è deselezionato.


#### Passaggi successivi {#next-steps}

I passaggi successivi sono gli stessi per Facebook e Twitter:

* [Pubblicare le configurazioni del servizio cloud](#publishcloudservices)
* [Abilita per un sito community](#enable-social-login)

## Accesso twitter {#twitter-login}

### Creare un’app Twitter {#create-a-twitter-app}

Per abilitare l’accesso social a Twitter è necessaria un’applicazione Twitter configurata.

Segui le istruzioni più recenti per creare una nuova applicazione Twitter all’indirizzo [https://apps.twitter.com](https://apps.twitter.com/).

In generale:

1. Inserisci un *Nome* in modo da identificare l’applicazione Twitter per gli utenti del sito web.
1. Inserire una *descrizione*.
1. Per *sito web* - enter `https://<server>`.
1. Per *URL di callback* - enter `https://server`.

   >[!NOTE]
   >
   >Non è necessario specificare la porta.
   >
   >Per lo sviluppo, https://127.0.0.1/ funzionerà.

1. Una volta creata l&#39;applicazione, individua la **[!UICONTROL Chiave consumer (API)]** e **[!UICONTROL Segreto consumer (API)]**. Queste informazioni saranno necessarie per configurare il [Servizio cloud twitter](#createatwittercloudservice).

#### Autorizzazioni {#permissions}

Nella sezione delle autorizzazioni di gestione dell&#39;applicazione Twitter:

* **[!UICONTROL Accesso]**: Seleziona `Read only`.

   * Altre opzioni non sono supportate

* **[!UICONTROL Autorizzazioni aggiuntive]**: Facoltativamente scegliere `Request email addresses from users`.

   * Se non è selezionato, il profilo utente in AEM non includerà il proprio indirizzo e-mail.
   * Le istruzioni di twitter indicano ulteriori passaggi da intraprendere.

L’unica richiesta REST effettuata per l’accesso social è di *[GET account/verifica credenziali](https://dev.twitter.com/rest/reference/get/account/verify_credentials)*.

### Creare un Cloud Service Twitter Connect {#create-a-twitter-connect-cloud-service}

La [Applicazione e provider OAuth di Adobe Granite](#adobe-granite-oauth-application-and-provider) istanza, creata mediante la creazione di una configurazione del servizio cloud, identifica l’applicazione Twitter e il gruppo o i gruppi di membri a cui vengono aggiunti i nuovi utenti.

1. Nell’istanza di authoring, accedi con privilegi di amministratore.
1. Dalla navigazione globale, seleziona **[!UICONTROL Strumenti]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Configurazione dell&#39;accesso a twitter Social]**.
1. Scegli la **[!UICONTROL percorso del contesto]** configurazione.

   Il percorso contestuale deve corrispondere al percorso di configurazione cloud selezionato durante la creazione/modifica di un sito della community.

1. Controlla se il percorso contestuale è abilitato per creare servizi cloud sotto di esso.
1. Vai a **[!UICONTROL Strumenti]** > **[!UICONTROL Generale]** > **[!UICONTROL Browser di configurazione]**. Seleziona il tuo contesto e modifica le proprietà. Abilita le configurazioni cloud se non ancora abilitate.

   ![twitterconfigpropping](assets/twitterconfigproppng.png)

   * Consulta la sezione [Browser di configurazione](/help/sites-administering/configurations.md) documentazione per ulteriori informazioni.

1. Creare/modificare la configurazione del servizio cloud Twitter.

   ![twittersociloginpng](assets/twittersocialloginpng.png)

   * **[!UICONTROL Titolo]**

      (*Obbligatorio*) Immetti un titolo di visualizzazione che identifichi l’app Twitter. Si consiglia di utilizzare lo stesso nome immesso come *Nome visualizzato* per l’app Twitter.

   * **[!UICONTROL Chiave consumer]**

      (*Obbligatorio*) Inserisci il **Chiave consumer (API)** per l’app Twitter. In questo modo si identificano le [Applicazione e provider OAuth di Adobe Granite](https://helpx.adobe.com/experience-manager/6-3/communities/using/social-login.html#AdobeGraniteOAuthApplicationandProvider) istanza creata dalla finestra di dialogo.

   * **[!UICONTROL Segreto consumer]**

      (*Obbligatorio*) Inserisci il ***Segreto consumer(API)*** per l’app Twitter.

   * **[!UICONTROL Crea utenti]**

      Se questa opzione è selezionata, l&#39;accesso con un account Twitter creerà una voce utente AEM e la aggiungerà come membro al gruppo o ai gruppi di utenti selezionati. Il valore predefinito è selezionato (fortemente consigliato).

   * **[!UICONTROL Maschera ID utenti]**

      Lascia deselezionato .

   * **[!UICONTROL Aggiungi a gruppo di utenti]**

      Selezionare Aggiungi gruppo di utenti per scegliere uno o più [gruppi di membri](https://helpx.adobe.com/experience-manager/6-3/communities/using/users.html) per il sito community a cui verranno aggiunti gli utenti.
   >[!NOTE]
   >
   >I gruppi possono essere aggiunti o rimossi in qualsiasi momento. Ma le appartenenze degli utenti esistenti non saranno influenzate. L&#39;iscrizione automatica si applica solo ai nuovi utenti creati dopo l&#39;aggiornamento del campo. Per i siti in cui gli utenti anonimi sono disabilitati, aggiungi gli utenti al gruppo di membri della community corrispondente destinato a quel sito community chiuso.

1. Seleziona **[!UICONTROL SALVA]** e **[!UICONTROL Pubblica]**.

Il risultato è un [Applicazione e provider OAuth di Adobe Granite](https://helpx.adobe.com/experience-manager/6-3/communities/using/social-login.html#adobe-granite-oauth-application-and-provider) istanza che non richiede ulteriori modifiche. L’ambito predefinito è quello standard per l’accesso a Twitter.

### Provider OAuth di AEM Communities Twitter {#aem-communities-twitter-oauth-provider}

La configurazione di AEM Communities estende [Applicazione e provider OAuth di Adobe Granite](#adobe-granite-oauth-application-and-provider) istanza. Questo provider richiederà modifiche per consentire gli aggiornamenti degli utenti.

Se è necessaria la modifica, su ogni istanza di pubblicazione AEM:

1. Accedi con privilegi di amministratore.
1. Passa a [Console web](../../help/sites-deploying/configuring-osgi.md).

   Ad esempio, http://localhost:4503/system/console/configMgr.

1. Individua il provider OAuth di AEM Communities Twitter.
1. Seleziona l’icona a forma di matita da aprire per la modifica.

   ![twitteroauth_png](assets/twitteroauth_png.png)

   * **[!UICONTROL ID provider OAuth]**

   (*Obbligatorio*) Il valore predefinito è *soco-twitter*. Non modificare.

   * **[!UICONTROL Configurazione Cloud Service]**

      Il valore predefinito è *conf.* Non modificare.

   * **[!UICONTROL Configurazione del servizio del provider OAuth]**

      Il valore predefinito è `/apps/social/twitterprovider/config/`. Non modificare.

   * **[!UICONTROL Percorso utente]**

      Posizione nella directory archivio in cui sono archiviati i dati utente. Per un sito della community, per garantire ai membri le autorizzazioni necessarie per visualizzare il profilo degli altri, il percorso deve essere quello predefinito `/home/users/community`.

   * **[!UICONTROL Abilita parametri]** non modificare
   * **[!UICONTROL Parametri URL]** non modificare
   * **[!UICONTROL Aggiorna utente]**

      Se questa opzione è selezionata, aggiorna i dati utente nell’archivio a ogni accesso per riflettere le modifiche del profilo o i dati aggiuntivi richiesti. Il valore predefinito è deselezionato.


#### Passaggi successivi {#next-steps-1}

I passaggi successivi sono gli stessi per Facebook e Twitter:

* [Pubblicare le configurazioni del servizio cloud](#publishcloudservices)
* [Abilita per un sito community](#enable-social-login)

## Abilita accesso social {#enable-social-login}

### Console AEM Communities Sites {#aem-communities-sites-console}

Una volta configurato, il servizio cloud può essere abilitato per l’impostazione di accesso social pertinente per un sito community utilizzando [Gestione utente](https://helpx.adobe.com/experience-manager/6-3/communities/using/sites-console.html#USERMANAGEMENT) Pannello secondario Impostazioni durante il sito community [creazione](https://helpx.adobe.com/experience-manager/6-3/communities/using/sites-console.html#SiteCreation) o [gestione](https://helpx.adobe.com/experience-manager/6-3/communities/using/sites-console.html#ModifyingSiteProperties).

1. Scegli il contesto di configurazione del sito in cui hai salvato le configurazioni di accesso social.

1. Nella scheda Generale, imposta le configurazioni cloud.

   ![managesites_png](assets/managesites_png.png)

1. Nella scheda Impostazioni , abilita **[!UICONTROL Accesso a Social]** e Salva.

   ![usermgmt_png](assets/usermgmt_png.png)

## Verifica accesso social {#test-social-login}

* Assicurati [Gestore autenticazione OAuth di Adobe Granite](#adobe-granite-oauth-authentication-handler) è stato abilitato su tutte le istanze di pubblicazione.
* Verifica che i servizi cloud siano stati pubblicati.
* Assicurati che il sito della community sia stato pubblicato.
* Avvia il sito pubblicato in un browser.
Ad esempio, http://localhost:4503/content/sites/engage/en.html
* Seleziona **[!UICONTROL Accesso]**.
* Seleziona o **[!UICONTROL Accesso con Facebook]** o **[!UICONTROL Accesso con Twitter]**.
* Se non hai già effettuato l&#39;accesso a Facebook o Twitter, accedi con le credenziali appropriate.
* Potrebbe essere necessario concedere l&#39;autorizzazione in base alla finestra di dialogo visualizzata dall&#39;app Facebook o Twitter.
* La barra degli strumenti nella parte superiore della pagina viene aggiornata per riflettere l’accesso eseguito correttamente.
* Seleziona **[!UICONTROL Profilo]**: nella pagina Profilo viene visualizzata l’immagine avatar dell’utente, il nome e il cognome. Inoltre, visualizza le informazioni dal profilo Facebook o Twitter in base ai campi/parametri consentiti.

## Configurazioni OAuth della piattaforma AEM {#aem-platform-oauth-configurations}

### Gestore autenticazione OAuth di Adobe Granite {#adobe-granite-oauth-authentication-handler}

La `Adobe Granite OAuth Authentication Handler` non è abilitato per impostazione predefinita e ***deve essere abilitata su tutte le istanze di pubblicazione AEM.***

Per abilitare il gestore di autenticazione al momento della pubblicazione, è sufficiente aprire la configurazione OSGi e salvarla:

* Accedi con privilegi di amministratore.
* Passa a [Console web](../../help/sites-deploying/configuring-osgi.md).
Ad esempio, http://localhost:4503/system/console/configMgr
* Individua `Adobe Granite OAuth Authentication Handler`.
* Seleziona per aprire la configurazione per la modifica.
* Seleziona **[!UICONTROL Salva]**.

![graniteoauth](assets/graniteoauth.png)

>[!CAUTION]
>
>Fai attenzione a non confondere il gestore di autenticazione con un&#39;istanza Facebook o Twitter di *Applicazione e provider OAuth di Adobe Granite*.

![graniteoauth1](assets/graniteoauth1.png)

### Applicazione e provider OAuth di Adobe Granite {#adobe-granite-oauth-application-and-provider}

Quando viene creato un servizio cloud per Facebook o Twitter, viene creata un&#39;istanza di `Adobe Granite OAuth Authentication Handler` viene creato.

Per individuare l&#39;istanza creata per un&#39;app Facebook o Twitter:

1. Accedi con privilegi di amministratore.
1. Passa a [Console web](../../help/sites-deploying/configuring-osgi.md).

   Ad esempio, http://localhost:4503/system/console/configMgr.

1. Individua l’applicazione e il provider OAuth di Adobe Granite.

   * Individua l’istanza in cui **[!UICONTROL ID client]** corrisponde a **[!UICONTROL ID app]**.

      ![graniteoauth2](assets/graniteoauth2.png)

      Ad eccezione delle seguenti proprietà, lasciare invariate le altre proprietà della configurazione:

   * **[!UICONTROL ID configurazione]**

      (*Obbligatorio*) Gli ID di configurazione OAuth devono essere univoci. Generazione automatica quando viene creato il servizio cloud.

   * **[!UICONTROL ID client]**

      (*Obbligatorio*) L&#39;ID applicazione fornito al momento della creazione del servizio cloud.

   * **[!UICONTROL Segreto client]**

      (*Obbligatorio*) Il segreto dell&#39;applicazione fornito al momento della creazione del servizio cloud.

   * **[!UICONTROL Ambito]**

      (*Facoltativo*) Il provider può richiedere un ulteriore ambito per ciò che è consentito. L&#39;ambito predefinito copre le autorizzazioni necessarie per fornire l&#39;autenticazione social e i dati di profilo.

   * **[!UICONTROL ID fornitore]**

      (*Obbligatorio*) L&#39;ID fornitore per AEM Communities viene impostato al momento della creazione del servizio cloud. Non modificare. Per Facebook Connect, il valore è *soco-facebook*. Per Twitter Connect, il valore è *soco-twitter*.

   * **[!UICONTROL Gruppi]**

      (*Consigliato*) Uno o più gruppi di membri a cui vengono aggiunti gli utenti creati. Per AEM Communities, si consiglia di elencare il gruppo di membri per il sito community.

   * **[!UICONTROL URL callback]**

      (*Facoltativo*) URL configurato con i provider OAuth per reindirizzare nuovamente il client. Utilizza un URL relativo per utilizzare l’host della richiesta originale. Lascia vuoto per utilizzare invece l’URL originariamente richiesto. Il suffisso &quot;/callback/j_security_check&quot; viene aggiunto automaticamente a questo url .
   >[!NOTE]
   >
   >Il dominio del callback deve essere registrato con il provider (Facebook o Twitter).

Per ogni configurazione del gestore di autenticazione OAuth, nell’istanza sono state create due configurazioni aggiuntive:

* Apache Jackrabbit Oak Default Sync Handler (org.apache.jackrabbit.oak.spi.security.authentication.external.impl.DefaultSyncHandler) - Non sono necessarie modifiche, ma puoi guardare le mappature dei campi utente in cui i campi Facebook sono mappati su un nodo di profilo utente CQ. Inoltre, &#39;Sync Handler Name&#39; corrisponde all&#39;ID di configurazione della configurazione del provider OAuth.
* Modulo di accesso esterno Apache Jackrabbit Oak (org.apache.jackrabbit.oak.spi.security.authentication.external.impl.ExternalLoginModuleFactory) - Non sono necessarie modifiche, ma si può notare che &#39;Nome provider identità&#39; e &#39;Nome gestore sincronizzazione&#39; sono uguali e puntano rispettivamente alle corrispondenti configurazioni OAuth e del gestore di sincronizzazione.

Per ulteriori informazioni, consulta [Autenticazione con modulo di accesso esterno Apache Oak](https://jackrabbit.apache.org/oak/docs/security/authentication/externalloginmodule.html).

## Prestazioni di trasferimento degli utenti OAuth {#oauth-user-traversal-performance}

Per i siti della community in cui centinaia di migliaia di utenti si registrano utilizzando il proprio accesso Facebook o Twitter, le prestazioni traverse della query eseguita quando un visitatore del sito utilizza il proprio accesso social possono essere migliorate aggiungendo il seguente indice Oak.

Se nei registri sono visualizzati avvisi traversal, è consigliabile aggiungere questo indice.

Su un&#39;istanza di authoring, connesso con privilegi amministrativi:

1. Dalla navigazione globale: select **Strumenti, [CRX/DE Lite](../../help/sites-developing/developing-with-crxde-lite.md).**
1. Crea un indice denominato ntBaseLucene-oauth da una copia di ntBaseLucene:

   * Sotto il nodo `/oak:index`
   * Seleziona nodo `ntBaseLucene`
   * Seleziona **[!UICONTROL Copia]**
   * Seleziona `/oak:index`
   * Seleziona **[!UICONTROL Incolla]**
   * Rinomina copia di ntBaseLucene in `ntBaseLucene-oauth`

1. Modifica le proprietà del nodo ntBaseLucene-oauth:

   * **[!UICONTROL indexPath]**: `/oak:index/ntBaseLucene-oauth`
   * **[!UICONTROL name]**: `oauthid-123****`
   * **[!UICONTROL reindicizzare]**: `true`
   * **[!UICONTROL reindexCount]**: `1`

1. Sotto il nodo /oak:index/ntBaseLucene-oauth/indexRules/nt:base/properties:

   * Elimina tutti i nodi figlio, ad eccezione di cqTags.
   * Rinomina cqTags in `oauthid-123****`
   * Modifica le proprietà del nodo `oauthid-123****`

      * **[!UICONTROL name]**: `oauthid-123****`
   * Seleziona **[!UICONTROL Salva tutto]**.


* Per **name** `oauthid-123`, sostituisci *123* con Facebook ***ID app*** o Twitter ***Chiave consumer (API)*** che è il valore del **ID client** in [Applicazione e provider OAuth di Adobe Granite](social-login.md#adobe-granite-oauth-application-and-provider) configurazione.

   ![graniteoauth-crxde](assets/graniteoauth-crxde.png)

Per ulteriori informazioni e strumenti, consulta [Query e indicizzazione Oak](../../help/sites-deploying/queries-and-indexing.md).

## Configurazione del Dispatcher {#dispatcher-configuration}

Vedi [Configurazione di Dispatcher per Communities](dispatcher.md).
