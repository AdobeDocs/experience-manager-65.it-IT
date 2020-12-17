---
title: Creazione di un nuovo sito community per l'abilitazione
seo-title: Creazione di un nuovo sito community per l'abilitazione
description: Creazione di un sito community per l'abilitazione
seo-description: Creazione di un sito community per l'abilitazione
uuid: a75fa566-a570-45fd-aabc-23651ef819cc
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
discoiquuid: b9333558-6af9-46b2-9f03-3722645c69a6
docset: aem65
translation-type: tm+mt
source-git-commit: e9d5a7acad04d841cbc7d62050163f3de998fab6
workflow-type: tm+mt
source-wordcount: '1728'
ht-degree: 3%

---


# Creazione di un nuovo sito community per l&#39;abilitazione {#author-a-new-community-site-for-enablement}

## Crea sito community {#create-community-site}

[Creazione ](/help/communities/sites-console.md) di siti community con una procedura guidata che illustra i passaggi necessari per creare un sito community. È possibile passare al passaggio `Next` o `Back` precedente prima di eseguire il commit del sito nel passaggio finale.

Per iniziare a creare un nuovo sito community:

Utilizzo dell&#39; [istanza di creazione](https://localhost:4502/)

* Accedete con i privilegi di amministratore e andate a **[!UICONTROL Communities]** > **[!UICONTROL Sites]**.

* Seleziona **Crea**.

### Passaggio 1: Modello del sito {#step-site-template}

![modello di sito di abilitazione](assets/enablement-site-template.png)

Nel passaggio **Modello del sito**, immettete un titolo, una descrizione, il nome dell&#39;URL e selezionate un modello di sito community, ad esempio:

* **Titolo del sito community**: `Enablement Tutorial`.

* **Descrizione del sito community**: `A site for enabling the community to learn.`

* **Radice** sito community: (lasciare vuoto per la radice predefinita  `/content/sites`)

* **Configurazioni** cloud: (lasciate vuoto se non sono specificate configurazioni cloud) fornite il percorso alle configurazioni cloud specificate.
* **Lingua** di base del sito community: (lasciare invariate le lingue per una sola: Inglese) utilizzare il menu a discesa per scegliere una  *o* più lingue tra quelle disponibili: tedesco, italiano, francese, giapponese, spagnolo, portoghese (Brasile), cinese tradizionale e cinese (semplificato). Verrà creato un sito community per ogni lingua aggiunta, all&#39;interno della stessa cartella del sito seguendo la procedura consigliata in [Translating Content for Multilingual Sites](/help/sites-administering/translation.md). La pagina principale di ciascun sito conterrà una pagina figlia denominata dal codice della lingua di una delle lingue selezionate, ad esempio &#39;en&#39; per l&#39;inglese o &#39;fr&#39; per il francese.

* **Nome sito community**: `enable`

   * L&#39;URL iniziale verrà visualizzato sotto il nome del sito community
   * Per un URL valido, aggiungete un codice della lingua di base + &quot;.html&quot;
      *Ad esempio*, https://localhost:4502/content/sites/  `enable/en.html`

* **Modello** del sito di riferimento: premuto per scegliere  `Reference Structured Learning Site Template`

Seleziona **Avanti**.

### Passaggio 2: Progettazione {#step-design}

Il passaggio Progettazione viene presentato in due sezioni per selezionare il tema e il banner di branding:

#### TEMA DEL SITO COMUNITARIO {#community-site-theme}

Selezionate lo stile da applicare al modello. Quando è selezionato, il tema sarà sovrapposto con un segno di spunta.

#### MARCHIO DEL SITO COMUNITARIO {#community-site-branding}

(Facoltativo) Caricate un&#39;immagine banner da visualizzare nelle pagine del sito. Il banner è fissato al bordo sinistro del browser, tra l&#39;intestazione del sito community e il menu (collegamenti di navigazione). L’altezza del banner viene ritagliata a 120 pixel. Il banner non può essere ridimensionato in modo da adattarlo alla larghezza del browser e all&#39;altezza di 120 pixel.

![site-branding1](assets/site-branding1.png)

![site-branding2](assets/site-branding2.png)

Seleziona **Avanti**.

### Passaggio 3: Impostazioni {#step-settings}

Nel passaggio Settings (Impostazioni), prima di selezionare `Next`, sono presenti sette sezioni che forniscono l&#39;accesso alle configurazioni che includono gestione utente, tag, ruoli, moderazione, analisi, traduzione e abilitazione.

#### GESTIONE UTENTE {#user-management}

È consigliabile che [le comunità di abilitazione](/help/communities/overview.md#enablement-community) siano private.

Un sito community è privato quando ai visitatori anonimi viene negato l&#39;accesso, non può registrarsi autonomamente e non può utilizzare il login mediante social network.

Verificare che la maggior parte delle caselle di controllo siano deselezionate per [Gestione utente](/help/communities/sites-console.md#user-management):

* NON consentire ai visitatori del sito di registrarsi autonomamente.
* NON consentire ai visitatori anonimi del sito di visualizzare il sito.
* Facoltativo, sia che si desideri consentire o meno la messaggistica tra i membri della community.
* NON consentire l&#39;accesso con Facebook.
* NON consentire l&#39;accesso con Twitter.

![user-mgmt](assets/user-mgmt.png)

#### TAG {#tagging}

I tag che possono essere applicati al contenuto della community sono controllati selezionando gli spazi di nomi AEM definiti in precedenza tramite la [Console di assegnazione tag](/help/sites-administering/tags.md#tagging-console) (ad esempio [Spazio dei nomi delle esercitazioni](/help/communities/enablement-setup.md#create-tutorial-tags)).

Inoltre, selezionando Tag namespace per il sito della community, la selezione presentata nella definizione di cataloghi e risorse di abilitazione viene limitata. Per informazioni importanti, vedere [Risorse per l&#39;abilitazione dei tag](/help/communities/tag-resources.md).

La ricerca di spazi dei nomi è semplice tramite la ricerca tipo-avanti. Esempio,

* Tipo `tut`
* Seleziona `Tutorial`

![enablement-tagging](assets/enablement-tagging.png)

### RUOLI {#roles}

[I ](/help/communities/users.md) ruoli dei membri della community vengono assegnati tramite le impostazioni nella sezione Ruoli.

Per consentire a un membro della community (o a un gruppo di membri) di utilizzare il sito come manager della community, utilizzate la ricerca tipo avanti e selezionate il nome del membro o del gruppo dalle opzioni disponibili nel menu a discesa.

Esempio,

* Tipo `q`
* Selezionare [Quinn Harper](/help/communities/enablement-setup.md#publishcreateenablementmembers)

>[!NOTE]
>
>[Il ](/help/communities/deploy-communities.md#tunnel-service-on-author) servizio Tunnel consente la selezione di membri e gruppi esistenti solo nell’ambiente di pubblicazione.

![ruoli di abilitazione](assets/site-admin.png)

#### MODERAZIONE {#moderation}

Accettate le impostazioni globali predefinite per il contenuto generato dall&#39;utente [moderatore](/help/communities/sites-console.md#moderation) (UGC).

![moderazione1](assets/moderation1.png)

#### ANALYTICS {#analytics}

Dall&#39;elenco a discesa, seleziona il framework del servizio cloud di Analytics configurato per questo sito community.

La selezione vista nello screenshot, `Communities`, è l&#39;esempio di framework della [documentazione di configurazione.](/help/communities/analytics.md#aem-analytics-framework-configuration)

![analisi](assets/analytics.png)

#### TRADUZIONE {#translation}

Le [Impostazioni di traduzione](/help/communities/sites-console.md#translation) specificano se è possibile convertire o meno UGC e in quale lingua, se lo è.

* Selezionare **Consenti traduzione automatica**
* Utilizzare le impostazioni predefinite

![traduzione](assets/translation.png)

#### ABILITAZIONE {#enablement}

Per una comunità di abilitazione, è necessario identificare uno o più manager di abilitazione della community.

* **Manager**
 abilitazione (obbligatorio) Membri del gruppo 
`Community Enablement Managers` sono disponibili per essere selezionati per gestire questo sito community.

   * Tipo `s`
   * Seleziona `Sirius Nilson`

* **ID**
 organizzazione Marketing Cloud (facoltativo) ID per un account Adobe Analytics , necessario per l’inclusione di  [Video Heartbeat ](/help/communities/analytics.md#video-heartbeat-analytics) Analytics nella generazione dei rapporti di abilitazione.

![abilitazione](assets/enablement.png)

Seleziona **Avanti**.

### Passaggio 4: Crea sito community {#step-create-community-site}

Seleziona **Crea.**

![preview](assets/preview.png)

Al termine del processo, la cartella del nuovo sito viene visualizzata nella console Community > Siti.

![enablementecreated](assets/enablementsitecreated.png)

### Pubblicare il nuovo sito della community {#publish-the-new-community-site}

Il sito creato deve essere gestito dalla console Community - Siti, la stessa console da cui è possibile creare nuovi siti.

Dopo aver selezionato la cartella del sito della community, passate il puntatore sull&#39;icona del sito in modo che vengano visualizzate quattro icone di azione:

![siteactionicons](assets/siteactionicons.png)

Selezionando l&#39;icona delle ellissi (icona Altre azioni), vengono visualizzate le opzioni Esporta sito ed Elimina sito.

![siteactionsnew](assets/siteactionsnew.png)

Da sinistra a destra sono:

* **Apri sito**

   Selezionate l’icona matita per aprire il sito della community in modalità di modifica dell’autore e aggiungere e/o configurare i componenti della pagina.

* **Modifica sito**

   Selezionate l&#39;icona delle proprietà per aprire il sito della community e modificare le proprietà, ad esempio il titolo o il tema.

* **Pubblica sito**

   Selezionate l&#39;icona del mondo per pubblicare il sito della community (per impostazione predefinita, localhost:4503).

* **Esporta sito**

   Selezionate l&#39;icona di esportazione per creare un pacchetto del sito community che viene memorizzato e scaricato in [package manager](/help/sites-administering/package-manager.md).
UGC non è incluso nel pacchetto del sito.

* **Elimina sito**

   Per eliminare il sito community, selezionate l&#39;icona Elimina sito visualizzata quando si passa il mouse sul sito nella console del sito di Communities. Questa azione rimuove tutti gli elementi associati al sito, come UGC, gruppi di utenti, risorse e record del database.

   ![enablesiteazioni](assets/enablesiteactions.png)

#### Selezionate Pubblica {#select-publish}

Selezionate l&#39;icona del mondo per pubblicare il sito della community.

![sito di pubblicazione](assets/publish-site.png)

Ci sarà un&#39;indicazione che il sito è stato pubblicato.

![site-published](assets/site-published.png)

## Utenti e gruppi di utenti della community {#community-users-user-groups}

### Nuovi gruppi di utenti community {#notice-new-community-user-groups}

Insieme al nuovo sito della community, vengono creati nuovi gruppi di utenti che dispongono delle autorizzazioni appropriate impostate per diverse funzioni amministrative. Per informazioni dettagliate, vedere [Gruppi di utenti per siti community](/help/communities/users.md#usergroupsforcommunitysites).

Per questo nuovo sito della community, in base al nome del sito &quot;enable&quot; nel passaggio 1, i nuovi gruppi di utenti presenti nell&#39;ambiente di pubblicazione possono essere visualizzati nella console [Membri e gruppi della community](/help/communities/members.md#groups-console):

![community_usergroup](assets/community_usergroup.png)

### Assegna membri a community Enable Members Group {#assign-members-to-community-enable-members-group}

Per l&#39;autore, con il servizio tunnel abilitato, è possibile assegnare gli [utenti creati durante l&#39;impostazione iniziale](/help/communities/enablement-setup.md#publishcreateenablementmembers) al gruppo Membri della community per il nuovo sito community creato.

Utilizzando la console Gruppi community, i membri possono essere aggiunti singolarmente o tramite appartenenza a un gruppo.

In questo esempio, il gruppo `Community Ski Class` viene aggiunto come membro del gruppo `Community Enable Members` e come membro `Quinn Harper`.

* Passare alla console **Community, Groups**
* Selezionare il gruppo *Abilita membri community*
* Immettere &#39;ski&#39; nella casella di ricerca **Aggiungi membri a gruppo**
* Selezionare *Community Ski Class* (gruppo di studenti)
* Immettere &#39;quinn&#39; nella casella di ricerca
* Selezionare *Quinn Harper* (attivazione contatto risorse)

* Seleziona **Salva**

![edit-group-settings](assets/edit-group-settings.png)

## Configurazioni sulla pubblicazione {#configurations-on-publish}

`https://localhost:4503/content/sites/enable/en.html {#http-localhost-content-sites-enable-en-html}`

![enablement-login](assets/enablement-login.png)

### Configura per errore di autenticazione {#configure-for-authentication-error}

Dopo aver configurato e inviato un sito per la pubblicazione, [configurate la mappatura di accesso](/help/communities/sites-console.md#configure-for-authentication-error) ( `Adobe Granite Login Selector Authentication Handler`) nell&#39;istanza di pubblicazione. Il vantaggio è che, se le credenziali di accesso non vengono immesse correttamente, l&#39;errore di autenticazione rivisualizzerà la pagina di accesso del sito della community con un messaggio di errore.

Aggiungete un `Login Page Mapping` come:

* `/content/sites/enable/en/signin:/content/sites/enable/en`

### (Facoltativo) Modificare la home page predefinita {#optional-change-the-default-home-page}

Quando lavorate con il sito di pubblicazione a scopo dimostrativo, potrebbe essere utile modificare la pagina principale predefinita nel nuovo sito.

A tal fine è necessario utilizzare [CRX|DE](https://localhost:4503/crx/de) Lite per modificare la tabella [mapping delle risorse](/help/sites-deploying/resource-mapping.md) al momento della pubblicazione.

Per iniziare:

1. Al momento della pubblicazione, accedete a CRXDE ed effettuate l&#39;accesso con privilegi di amministratore

   * Ad esempio, individuare [https://localhost:4503/crx/de](https://localhost:4503/crx/de) ed effettuare l&#39;accesso con `admin/admin`

1. Nel browser del progetto, espandi `/etc/map`
1. Selezionare il nodo `http`

   * Selezionare **Crea nodo**

      * **** Namelocalhost.4503

         (fare *not* utilizzare &#39;:&#39;)

      * **** [Composizione:Mappatura](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)

1. Con il nodo `localhost.4503` appena creato selezionato

   * Aggiungi, proprietà

      * **** Namesling:match
      * **** TypeString
      * **** Valuelocalhost.4503/$

   (deve terminare con il carattere &#39;$&#39;)

   * Aggiungi, proprietà

      * **Nome:** internalRedirect
      * **** TypeString
      * **Valore**  /content/sites/enable/en.html


1. Selezionare **Salva tutto**
1. (Facoltativo) Eliminare la cronologia di navigazione
1. Passa a https://localhost:4503/

   * Arrivate a https://localhost:4503/content/sites/enable/en.html

>[!NOTE]
>
>Per disattivare, è sufficiente pre-inviare il valore della proprietà `sling:match` con un valore &#39;x&#39; - `xlocalhost.4503/$` - e **Save All**.

![change-default-homepage](assets/change-default-homepage.png)

#### Risoluzione dei problemi: Errore durante il salvataggio della mappa {#troubleshooting-error-saving-map}

Se non è possibile salvare le modifiche, assicurarsi che il nome del nodo sia `localhost.4503`, con un separatore &#39;punto&#39; e non `localhost:4503` con un separatore &#39;due punti&#39;, in quanto `localhost` non è un prefisso valido per lo spazio nomi.

![error-map](assets/error-map.png)

#### Risoluzione dei problemi: Impossibile eseguire il reindirizzamento {#troubleshooting-fail-to-redirect}

Il valore &#39;**$**&#39; alla fine della stringa di espressione regolare `sling:match` è cruciale, in modo che solo `https://localhost:4503/` sia mappato esattamente, altrimenti il valore di reindirizzamento viene anteposto a qualsiasi percorso che possa esistere dopo server:port nell&#39;URL. Pertanto, quando AEM tenta di reindirizzare alla pagina di accesso, non riesce.

## Modifica del sito community {#modifying-the-community-site}

Dopo la creazione iniziale del sito, gli autori possono utilizzare l&#39;icona [Apri sito](/help/communities/sites-console.md#authoring-site-content) per eseguire le attività di authoring AEM standard.

Inoltre, gli amministratori possono utilizzare l&#39;icona [Modifica sito](/help/communities/sites-console.md#modifying-site-properties) per modificare le proprietà del sito, ad esempio il titolo.

Dopo ogni modifica, ricordate di **Salvare** e di ri-**Pubblicare** il sito.

>[!NOTE]
>
>Se non avete familiarità con AEM, visualizzate la documentazione su [operazioni di base](/help/sites-authoring/basic-handling.md) e una [guida rapida all&#39;authoring delle pagine](/help/sites-authoring/qg-page-authoring.md).

### Aggiungere un catalogo {#add-a-catalog}

Il modello di sito community scelto per questo sito community deve contenere la funzione di catalogo.

In caso contrario, è possibile aggiungere facilmente la funzione catalogo. Ciò consentirebbe ad altri membri della comunità, non assegnati a risorse di abilitazione o a un percorso di apprendimento, di selezionare le risorse di abilitazione da un catalogo.

Se la struttura del sito contiene già la funzione catalogo, è possibile modificarne il Titolo.

Per modificare la struttura del sito, accedete alla console **[!UICONTROL Communities]** > **[!UICONTROL Sites]**, aprite la cartella `enable` e selezionate l&#39;icona **Edit Site** per accedere alle proprietà di `Enablement Tutorial`.

Selezionate il pannello STRUTTURA per aggiungere un catalogo o modificare un catalogo esistente:

* **Titolo**: `Ski Catalog`

* **URL**: `catalog`

* **Seleziona tutti gli spazi dei nomi**: lasciate come predefinito.

* Seleziona **Salva**.

![edit-site-structure](assets/modify-site-structure.png)

Utilizzate l&#39;icona Posizione per spostare la funzione Catalogo nella seconda posizione, dopo Assegnazioni.

![movecatalog-func](assets/move-catalog-func.png)

Selezionare **Salva** nell&#39;angolo in alto a destra per salvare le modifiche nel sito della community.

Quindi ri-**Pubblica** il sito.

