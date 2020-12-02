---
title: Creazione di un nuovo sito community
seo-title: Creazione di un nuovo sito community
description: 'Come creare un nuovo sito AEM Communities '
seo-description: 'Come creare un nuovo sito AEM Communities '
uuid: 4f609f5f-ef07-44fc-aeb3-1c616e120d46
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
discoiquuid: 8ae324ea-8b84-47a3-aabf-1fee2a3bd46d
docset: aem65
translation-type: tm+mt
source-git-commit: 2daf00f17058de8b901848fcf1128a5ee9770368
workflow-type: tm+mt
source-wordcount: '1661'
ht-degree: 2%

---


# Creazione di un nuovo sito community{#author-a-new-community-site}

## Creare un sito community {#create-a-community-site}

Utilizzate l&#39;istanza di creazione per creare un sito community. Nell&#39;istanza di AEM Author:

1. Effettuate l&#39;accesso con privilegi di amministratore.
1. Dalla navigazione globale, andate a **[!UICONTROL Communities]** > **[!UICONTROL Sites]**.

La console Siti community offre una procedura guidata che guida l’utente attraverso i passaggi necessari per creare un sito community. È possibile passare al passaggio `Next` o `Back` precedente prima di eseguire il commit del sito nel passaggio finale.

Per iniziare a creare un nuovo sito community:

* Selezionare il pulsante `Create`.

![createcommunitysite](assets/createcommunitysite.png)

### Passaggio 1: Modello del sito {#step-site-template}

![modello per la creazione del sito](assets/create-site.png)

Nel [passo Modello del sito](/help/communities/sites-console.md#step2013asitetemplate), immettete un titolo, una descrizione, il nome dell&#39;URL e selezionate un modello di sito community, ad esempio:

* **Titolo del sito community**: `Getting Started Tutorial`
* **Descrizione del sito community**: `A site for engaging with the community.`
* **Radice** sito community: (lasciare vuoto per la radice predefinita  `/content/sites`)
* **Configurazioni** cloud: (lasciate vuoto se non sono specificate configurazioni cloud) fornite il percorso alle configurazioni cloud specificate.
* **Lingua** di base del sito community: (lasciare invariate le lingue per una sola: Inglese) utilizzare l&#39;elenco a discesa per scegliere una  *o* più lingue tra quelle disponibili: tedesco, italiano, francese, giapponese, spagnolo, portoghese (Brasile), cinese tradizionale e cinese (semplificato). Verrà creato un sito community per ogni lingua aggiunta, all&#39;interno della stessa cartella del sito seguendo la procedura consigliata in [Translating Content for Multilingual Sites](/help/sites-administering/translation.md). La pagina principale di ciascun sito conterrà una pagina figlia denominata dal codice della lingua di una delle lingue selezionate, ad esempio &#39;en&#39; per l&#39;inglese o &#39;fr&#39; per il francese.

* **Nome** sito community: coinvolgimento

   * Ricontrolla il nome perché non viene facilmente modificato dopo la creazione del sito
   * L&#39;URL iniziale verrà visualizzato sotto il nome del sito community
   * Per un URL valido, aggiungete un codice della lingua di base + &quot;.html&quot;
   * *Ad esempio*, https://localhost:4502/content/sites/  `engage/en.html`

* **Modello**: premuto per scegliere  `Reference Site`

* Seleziona **Avanti**.

### Passaggio 2: Progettazione {#step-design}

Il passaggio Progettazione viene presentato in due sezioni per selezionare il tema e il banner di branding:

#### TEMA DEL SITO COMUNITARIO {#community-site-theme}

Selezionate lo stile da applicare al modello. Quando viene selezionato, al tema verrà sovrapposto un segno di spunta.

#### MARCHIO DEL SITO COMUNITARIO {#community-site-branding}

(Facoltativo) Caricate un&#39;immagine banner da visualizzare nelle pagine del sito. Il banner è fissato al bordo sinistro del browser, tra l&#39;intestazione del sito community e i collegamenti di navigazione. L’altezza del banner viene ritagliata a 120 pixel. Il banner non può essere ridimensionato in modo da adattarlo alla larghezza del browser e all&#39;altezza di 120 pixel.

![marchio comunitario](assets/community-site-branding.png)

![upload-image-site](assets/upload-image-site.png)

Seleziona **Avanti**.

### Passaggio 3: Impostazioni {#step-settings}

Nella fase Settings (Impostazioni), prima di selezionare `Next`, tenete presente che sono presenti sette sezioni che forniscono l&#39;accesso alle configurazioni che includono gestione utente, tag, moderazione, gestione dei gruppi, analisi, traduzione e abilitazione.

Per provare a utilizzare le funzioni di abilitazione, visita l&#39;esercitazione [Guida introduttiva  AEM Communities per l&#39;abilitazione](/help/communities/getting-started-enablement.md).

#### User Management {#user-management}

Selezionare tutte le caselle di controllo per [Gestione utente](/help/communities/sites-console.md#user-management)

* Per consentire ai visitatori del sito di registrarsi autonomamente
* Per consentire ai visitatori del sito di visualizzare il sito senza effettuare l&#39;accesso
* Per consentire ai membri di inviare e ricevere messaggi da altri membri della community
* Per consentire l&#39;accesso a Facebook invece di registrare e creare un profilo
* Per consentire l&#39;accesso con Twitter invece di registrare e creare un profilo

>[!NOTE]
>
>Per un ambiente di produzione, è necessario creare applicazioni Facebook e Twitter personalizzate. Consultate [Accesso tramite social network con Facebook e Twitter](/help/communities/social-login.md).

![impostazioni del sito community](assets/site-settings.png)

#### TAG {#tagging}

I tag che possono essere applicati al contenuto della community sono controllati selezionando gli spazi di nomi AEM definiti in precedenza tramite la [Console di assegnazione tag](/help/sites-administering/tags.md#tagging-console) (ad esempio [Spazio dei nomi delle esercitazioni](/help/communities/setup.md#create-tutorial-tags)).

La ricerca di spazi dei nomi è semplice tramite la ricerca tipo-avanti. Esempio,

* Tipo `tut`
* Seleziona `Tutorial`

![assegnazione](assets/tagging.png)

#### RUOLI {#roles}

[I ](/help/communities/users.md) ruoli dei membri della community vengono assegnati tramite le impostazioni nella sezione Ruoli.

Per consentire a un membro della community (o a un gruppo di membri) di utilizzare il sito come manager della community, utilizzate la ricerca tipo avanti e selezionate il nome del membro o del gruppo dalle opzioni disponibili nel menu a discesa.

Esempio,

* Tipo `q`
* Selezionare [Quinn Harper](/help/communities/enablement-setup.md#publishcreateenablementmembers)

>[!NOTE]
>
>[Il ](https://helpx.adobe.com/experience-manager/6-3/help/communities/deploy-communities.html#tunnel-service-on-author) servizio Tunnel consente la selezione di membri e gruppi esistenti solo nell’ambiente di pubblicazione.

![ruoli utente nel nuovo sito](assets/site-admin-1.png)

#### MODERAZIONE {#moderation}

Accettate le impostazioni globali predefinite per il contenuto generato dall&#39;utente (UGC) [moderatore](/help/communities/sites-console.md#moderation).

![moderazione](assets/moderation1.png)

#### ANALYTICS {#analytics}

Se  Adobe Analytics è concesso in licenza e è stato configurato un servizio e un framework cloud di Analytics, è possibile abilitare Analytics e selezionare il framework.

Consultate [Analytics Configuration for Communities Features](/help/communities/analytics.md).

![analisi](assets/analytics.png)

#### TRADUZIONE {#translation}

Le [Impostazioni di traduzione](/help/communities/sites-console.md#translation) specificano la lingua di base del sito, nonché se è possibile convertire o meno UGC e in quale lingua, in tal caso.

* Selezionare **Consenti traduzione automatica**
* Lasciare le lingue predefinite selezionate per la traduzione dal servizio di traduzione automatica predefinito
* Lascia il provider di traduzione predefinito e la configurazione
* Non c&#39;è bisogno di uno store globale perché non ci sono copie in lingua
* Selezionare **Traduci tutta la pagina**
* Opzione Mantieni persistenza predefinita

![impostazioni di traduzione](assets/translation-settings.png)

#### ABILITAZIONE {#enablement}

Lasciate vuoto quando create una community di coinvolgimento.

Per un&#39;esercitazione simile per creare rapidamente una [community di abilitazione](/help/communities/overview.md#enablement-community), vedere [Guida introduttiva a  AEM Communities per l&#39;abilitazione](/help/communities/getting-started-enablement.md).

Seleziona **Avanti**.

![abilitazione](assets/enablement.png)

### Passaggio 4: Crea sito community {#step-create-communities-site}

Seleziona **Crea.**

![create-site](assets/create-site2.png)

Al termine del processo, la cartella del nuovo sito viene visualizzata nella console Community - Siti.

![community_console](assets/communitiessitesconsole.png)

## Pubblicare il sito community {#publish-the-community-site}

Il sito creato deve essere gestito dalla console Community - Siti, la stessa console da cui è possibile creare nuovi siti.

Dopo aver selezionato la cartella del sito della community per aprirla, posizionate il puntatore sull&#39;icona del sito in modo che vengano visualizzate quattro icone di azione:

![siteactionicons-1](assets/siteactionicons-1.png)

Selezionando la quarta icona di ellissi (Altre azioni), vengono visualizzate le opzioni Esporta sito ed Elimina sito.

![siteactionsnew-1](assets/siteactionsnew-1.png)

Da sinistra a destra sono:

* **Apri sito**

   Selezionate l’icona matita per aprire il sito della community in modalità di modifica dell’autore, per aggiungere e/o configurare i componenti della pagina

* **Modifica sito**

   Selezionate l&#39;icona delle proprietà per aprire il sito della community e modificare le proprietà, ad esempio il titolo o il tema

* **Pubblica sito**

   Selezionate l&#39;icona del mondo per pubblicare il sito della community (ad esempio, se il server di pubblicazione è in esecuzione nel computer locale, per impostazione predefinita localhost:4503)

* **Esporta sito**

   Selezionate l&#39;icona di esportazione per creare un pacchetto del sito community che viene memorizzato e scaricato in [package manager](/help/sites-administering/package-manager.md).
UGC non è incluso nel pacchetto del sito.

* **Elimina sito**

   Selezionate l&#39;icona di eliminazione per eliminare il sito community dalla console **[!UICONTROL Community > Siti]**. Questa azione rimuove tutti gli elementi associati al sito, come UGC, gruppi di utenti, risorse e record del database.

![siteazioni](assets/siteactions.png)

>[!NOTE]
>
>Se non utilizzate la porta predefinita 4503 per l&#39;istanza di pubblicazione, modificate l&#39;agente di replica predefinito per impostare il numero di porta sul valore corretto.
>
>Nell’istanza di creazione, dal menu principale:
>
>1. Passare al menu **[!UICONTROL Strumenti]** > **[!UICONTROL Operazioni]** > **[!UICONTROL Replica]**.
>1. Selezionare **[!UICONTROL Agenti sull&#39;autore]**.
>1. Selezionare **[!UICONTROL Agente predefinito (pubblicazione)]**.
>1. Accanto a **[!UICONTROL Impostazioni]**, selezionare **[!UICONTROL Modifica]**.
>1. Nella finestra di dialogo a comparsa per Impostazioni agente, selezionare la scheda **[!UICONTROL Trasporto]**.
>1. In URI, modificate il numero di porta 4503 in base al numero di porta desiderato. Ad esempio, per utilizzare la porta 6103: https://localhost:6103/bin/receive?sling:authRequestLogin=1
>1. Selezionare **[!UICONTROL OK]**.
>1. (Facoltativo) Selezionare **[!UICONTROL Cancella]** o **[!UICONTROL Forza tentativo]** per ripristinare la coda di replica.


### Selezionate Pubblica {#select-publish}

Dopo aver verificato che il server di pubblicazione sia in esecuzione, selezionate l&#39;icona del mondo per pubblicare il sito della community.

![sito di pubblicazione](assets/publish-site.png)

Quando il sito della community è stato pubblicato correttamente, viene visualizzato brevemente il messaggio &quot;Sito pubblicato&quot;.

### Nuovi gruppi di utenti della community {#new-community-user-groups}

Insieme al nuovo sito della community, vengono creati nuovi gruppi di utenti che dispongono delle autorizzazioni appropriate impostate per diverse funzioni amministrative. Per informazioni dettagliate, vedere [Gruppi di utenti per siti community](/help/communities/users.md#usergroupsforcommunitysites).

Per questo nuovo sito community, dato il nome del sito &quot;coinvolgimento&quot; nel passaggio 1, i quattro nuovi gruppi di utenti possono essere visualizzati dalla console [Gruppi](/help/communities/members.md) (navigazione globale: Community, Gruppi):

* Manager Community Engagement
* Amministratori gruppo di coinvolgimento community
* Membri di coinvolgimento della community
* Moderatori di coinvolgimento community
* Partecipazione community con membri privilegiati
* Community Engagement Site Content Manager

Tenere presente che [Aaron McDonald](/help/communities/tutorials.md#demo-users) è un membro di

* Manager Community Engagement
* Moderatori di coinvolgimento community
* Partecipazione community (indirettamente come membro del gruppo Moderatori)

![user-group](assets/user-group.png)

#### https://localhost:4503/content/sites/engage/en.html {#http-localhost-content-sites-engage-en-html}

![coinvolgimento](assets/engage.png)

## Configura per errore di autenticazione {#configure-for-authentication-error}

Dopo aver configurato e inviato un sito per la pubblicazione, [configurate la mappatura di accesso](/help/communities/sites-console.md#configure-for-authentication-error) ( `Adobe Granite Login Selector Authentication Handler`) nell&#39;istanza di pubblicazione. Il vantaggio è che, se le credenziali di accesso non vengono immesse correttamente, l&#39;errore di autenticazione rivisualizzerà la pagina di accesso del sito della community con un messaggio di errore.

Aggiungi `Login Page Mapping` come

* `/content/sites/engage/en/signin:/content/sites/engage/en`

## Passaggi opzionali {#optional-steps}

### Modificare la home page predefinita {#change-the-default-home-page}

Quando lavorate con il sito di pubblicazione a scopo dimostrativo, potrebbe essere utile modificare la pagina principale predefinita nel nuovo sito.

A tal fine è necessario utilizzare [CRXDE](https://localhost:4503/crx/de) Lite per modificare la tabella [resource-mapping](/help/sites-deploying/resource-mapping.md) al momento della pubblicazione.

Per iniziare:

1. Nell’istanza di pubblicazione, effettuate l’accesso con privilegi di amministratore.
1. Individuate [https://localhost:4503/crx/de](https://localhost:4503/crx/de).
1. Nel browser del progetto, espandi `/etc/map.`
1. Selezionare il nodo `http`:

   * Selezionare **Crea nodo:**

      * **** Namelocalhost.4503 ( ** non utilizzare &#39;:&#39;)

      * **** [Composizione:Mappatura](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)

1. Con il nodo `localhost.4503` appena creato selezionato:

   * Aggiungi proprietà:

   * **** Namesling:match
      * **** TypeString
      * **** Valuelocalhost.4503/$ (deve terminare con il carattere &#39;$&#39;)
   * Aggiungi proprietà:

      * **Nome:** internalRedirect
      * **** TypeString
      * **Valore**  /content/sites/engage/en.html


1. Selezionare **Salva tutto.**
1. (Facoltativo) Eliminare la cronologia di navigazione.
1. Andate a https://localhost:4503/.

   * Arrivate a https://localhost:4503/content/sites/engage/en.html

>[!NOTE]
>
>Per disattivare, è sufficiente preimpostare il valore della proprietà `sling:match` con un prefisso &#39;x&#39; - `xlocalhost.4503/$` - e **Save All**.

![optional-step](assets/optional-steps.png)

#### Risoluzione dei problemi: Errore durante il salvataggio della mappa {#troubleshooting-error-saving-map}

Se non è possibile salvare le modifiche, assicurarsi che il nome del nodo sia `localhost.4503`, con un separatore &#39;punto&#39; e non `localhost:4503` con un separatore &#39;due punti&#39;, in quanto `localhost`non è un prefisso dello spazio nomi valido.

![error-message](assets/error-message.png)

#### Risoluzione dei problemi: Impossibile eseguire il reindirizzamento {#troubleshooting-fail-to-redirect}

La stringa &quot;**$**&quot; alla fine dell&#39;espressione regolare `sling:match`è fondamentale, in modo che solo `https://localhost:4503/` sia mappato esattamente, altrimenti il valore di reindirizzamento viene preceduto da qualsiasi percorso che potrebbe esistere dopo server:port nell&#39;URL. Pertanto, quando AEM tenta di reindirizzare alla pagina di accesso, non riesce.

### Modificare il sito {#modify-the-site}

Dopo la creazione iniziale del sito, gli autori possono utilizzare l&#39;icona [Apri sito](/help/communities/sites-console.md#authoring-site-content) per eseguire le attività di authoring AEM standard.

Inoltre, gli amministratori possono utilizzare l&#39;icona [Modifica sito](/help/communities/sites-console.md#modifying-site-properties) per modificare le proprietà del sito, ad esempio il titolo.

Dopo ogni modifica, ricordate di **Salvare** e di ri-**Pubblicare** il sito.

>[!NOTE]
>
>Se non avete familiarità con AEM, visualizzate la documentazione su [operazioni di base](/help/sites-authoring/basic-handling.md) e una [guida rapida all&#39;authoring delle pagine](/help/sites-authoring/qg-page-authoring.md).
