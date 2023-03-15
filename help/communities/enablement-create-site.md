---
title: Creare un nuovo sito community per l’abilitazione
seo-title: Author a New Community Site for Enablement
description: Creare un sito community per l’abilitazione
seo-description: Create a community site for enablement
uuid: a75fa566-a570-45fd-aabc-23651ef819cc
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
discoiquuid: b9333558-6af9-46b2-9f03-3722645c69a6
docset: aem65
exl-id: 812bbf7b-c49f-4c34-a47d-636b0468e0ba
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1715'
ht-degree: 3%

---

# Creare un nuovo sito community per l’abilitazione {#author-a-new-community-site-for-enablement}

## Crea sito community {#create-community-site}

[Creazione di siti community](/help/communities/sites-console.md) utilizza una procedura guidata che ti guida attraverso i passaggi necessari per creare un sito community. È possibile passare al `Next` passo o `Back` al passaggio precedente prima di impegnare il sito nel passaggio finale.

Per iniziare a creare un nuovo sito community:

Utilizzo della [istanza autore](https://localhost:4502/)

* Accedi con privilegi di amministratore e accedi a **[!UICONTROL Community]** > **[!UICONTROL Sites]**.

* Seleziona **Crea**.

### Passaggio 1 : Modello del sito {#step-site-template}

![modello di sito di abilitazione](assets/enablement-site-template.png)

Sulla **Modello del sito** , inserisci un titolo, una descrizione, il nome dell&#39;URL e seleziona un modello di sito community, ad esempio :

* **Titolo del sito community**: `Enablement Tutorial`.

* **Descrizione del sito community**: `A site for enabling the community to learn.`

* **Radice sito community**: (lasciare vuoto per la radice predefinita `/content/sites`)

* **Configurazioni cloud**: (lascia vuoto se non sono specificate configurazioni cloud) fornisci il percorso delle configurazioni cloud specificate.
* **Lingua di base del sito community**: (lasciare invariate le informazioni per una sola lingua: Inglese) utilizza il menu a discesa per sceglierne uno *o più* lingue di base delle lingue disponibili: tedesco, italiano, francese, giapponese, spagnolo, portoghese (Brasile), cinese (tradizionale) e cinese (semplificato). Verrà creato un sito community per ogni lingua aggiunta, che si troverà all’interno della stessa cartella del sito seguendo le best practice descritte in [Traduzione di contenuti per siti multilingue](/help/sites-administering/translation.md). La pagina principale di ciascun sito conterrà una pagina figlia denominata dal codice della lingua di una delle lingue selezionate, ad esempio &quot;en&quot; per l’inglese o &quot;fr&quot; per il francese.

* **Nome sito community**: `enable`

   * L’URL iniziale verrà visualizzato sotto il nome del sito community
   * Per un URL valido, aggiungi un codice della lingua di base + &quot;.html&quot;
      *Esempio*, https://localhost:4502/content/sites/ `enable/en.html`

* **Modello del sito di riferimento**: scegli `Reference Structured Learning Site Template`

Seleziona **Avanti**.

### Passaggio 2 : Progettazione {#step-design}

La fase Progettazione è presentata in due sezioni per selezionare il tema e il banner di branding:

#### TEMA DEL SITO COMUNITARIO {#community-site-theme}

Selezionare lo stile desiderato da applicare al modello. Se selezionato, il tema verrà sovrapposto con un segno di spunta.

#### MARCATURA DEL SITO COMMUNITY {#community-site-branding}

(Facoltativo) Carica un&#39;immagine banner da visualizzare nelle pagine del sito. Il banner viene fissato al bordo sinistro del browser, tra l&#39;intestazione del sito community e il menu (collegamenti di navigazione). L’altezza del banner viene ritagliata a 120 pixel. Il banner non viene ridimensionato in modo da adattarsi alla larghezza del browser e all’altezza di 120 pixel.

![site-branding1](assets/site-branding1.png)

![site-branding2](assets/site-branding2.png)

Seleziona **Avanti**.

### Passaggio 3 : Impostazioni {#step-settings}

Nel passaggio Impostazioni, prima di selezionare `Next`, noterai che esistono sette sezioni che forniscono accesso alle configurazioni che coinvolgono gestione utenti, assegnazione tag, ruoli, moderazione, analisi, traduzione e abilitazione.

#### GESTIONE UTENTE {#user-management}

Si consiglia di: [comunità di abilitazione](/help/communities/overview.md#enablement-community) sia privato.

Un sito community è privato quando ai visitatori anonimi viene negato l’accesso, non può registrarsi autonomamente e non può utilizzare l’accesso social.

Assicurati che la maggior parte delle caselle di controllo sia deselezionata per [Gestione utente](/help/communities/sites-console.md#user-management) :

* NON consentire ai visitatori del sito di registrarsi autonomamente.
* NON consentire ai visitatori anonimi del sito di visualizzare il sito.
* Facoltativo se consentire o meno la messaggistica tra i membri della community.
* NON consentire l&#39;accesso con Facebook.
* NON consentire l&#39;accesso con Twitter.

![user-mgmt](assets/user-mgmt.png)

#### TAG {#tagging}

I tag che possono essere applicati al contenuto della community vengono controllati selezionando AEM namespace definiti in precedenza tramite [Console assegnazione tag](/help/sites-administering/tags.md#tagging-console) (ad esempio [Spazio dei nomi tutorial](/help/communities/enablement-setup.md#create-tutorial-tags)).

Inoltre, selezionando Tag Namespace per il sito community , la selezione presentata viene limitata quando definisci cataloghi e risorse di abilitazione. Vedi [Risorse di abilitazione assegnazione tag](/help/communities/tag-resources.md) per informazioni importanti.

La ricerca di spazi dei nomi è semplice tramite la ricerca tipo-avanti. Ad esempio:

* Tipo `tut`
* Seleziona `Tutorial`

![assegnazione tag](assets/enablement-tagging.png)

### RUOLI {#roles}

[Ruoli dei membri della community](/help/communities/users.md) sono assegnate tramite le impostazioni nella sezione Ruoli .

Per consentire a un membro della comunità (o a un gruppo di membri) di utilizzare il sito come gestore della community, utilizza la ricerca tipo-avanti e seleziona il nome del membro o del gruppo dalle opzioni nel menu a discesa.

Ad esempio:

* Tipo `q`
* Seleziona [Quinn Harper](/help/communities/enablement-setup.md#publishcreateenablementmembers)

>[!NOTE]
>
>[Servizio tunnel](/help/communities/deploy-communities.md#tunnel-service-on-author) consente la selezione di membri e gruppi esistenti solo nell’ambiente di pubblicazione.

![ruoli di abilitazione](assets/site-admin.png)

#### MODERAZIONE {#moderation}

Accettare le impostazioni globali predefinite per [moderatore](/help/communities/sites-console.md#moderation) contenuto generato dall’utente (UGC).

![moderation1](assets/moderation1.png)

#### ANALYTICS {#analytics}

Dall’elenco a discesa , seleziona il framework del servizio cloud di Analytics configurato per questo sito community.

La selezione vista nello screenshot, `Communities`, è l&#39;esempio di framework dal [documentazione sulla configurazione.](/help/communities/analytics.md#aem-analytics-framework-configuration)

![analisi](assets/analytics.png)

#### TRADUZIONE {#translation}

La [Impostazioni di traduzione](/help/communities/sites-console.md#translation) specificare se l&#39;UGC può essere tradotto o meno e in quale lingua, in tal caso.

* Controlla **Consenti traduzione automatica**
* Usa le impostazioni predefinite

![traduzione](assets/translation.png)

#### ABILITARE {#enablement}

Per una comunità di abilitazione, è necessario identificare uno o più manager di abilitazione della community.

* **Manager di abilitazione**
(obbligatorio) Membri 
`Community Enablement Managers` sono disponibili per la gestione del sito community.

   * Tipo `s`
   * Seleziona `Sirius Nilson`

* **ID organizzazione Marketing Cloud**
(Facoltativo) L&#39;ID per un account Adobe Analytics necessario quando include [Video Heartbeat Analytics](/help/communities/analytics.md#video-heartbeat-analytics) nel rapporto di abilitazione.

![abilitazione](assets/enablement.png)

Seleziona **Avanti**.

### Passaggio 4 : Crea sito community {#step-create-community-site}

Seleziona **Crea.**

![anteprima](assets/preview.png)

Al termine del processo, la cartella del nuovo sito viene visualizzata nella console Community > Sites .

![enablementecreated](assets/enablementsitecreated.png)

### Pubblica il nuovo sito della community {#publish-the-new-community-site}

Il sito creato deve essere gestito dalla console Communities - Sites , la stessa console da cui è possibile creare nuovi siti.

Dopo aver selezionato la cartella del sito community, passa il puntatore sull’icona del sito in modo che vengano visualizzate quattro icone di azione:

![siteactionicone](assets/siteactionicons.png)

Quando si seleziona l’icona dei puntini di sospensione (icona Altre azioni), vengono visualizzate le opzioni Esporta sito ed Elimina sito .

![siteactionsnew](assets/siteactionsnew.png)

Da sinistra a destra sono:

* **Apri sito**

   Seleziona l’icona a forma di matita per aprire il sito community in modalità di modifica dell’autore e aggiungere e/o configurare i componenti della pagina.

* **Modifica sito**

   Seleziona l’icona delle proprietà per aprire il sito community e modificare le proprietà, ad esempio il titolo o il tema.

* **Pubblica sito**

   Seleziona l&#39;icona del mondo per pubblicare il sito della community (su localhost:4503 per impostazione predefinita).

* **Esporta sito**

   Seleziona l&#39;icona di esportazione per creare un pacchetto del sito della community memorizzato entrambi in [gestore di pacchetti](/help/sites-administering/package-manager.md) e scaricato.
UGC non è incluso nel pacchetto del sito.

* **Elimina sito**

   Per eliminare il sito community, seleziona l’icona Elimina sito visualizzata quando si passa il mouse sul sito nella console Sito di Communities. Questa azione rimuove tutti gli elementi associati al sito, come UGC, gruppi di utenti, risorse e record di database.

   ![enablesiteactions](assets/enablesiteactions.png)

#### Selezionate Pubblica {#select-publish}

Seleziona l&#39;icona del mondo per pubblicare il sito della community.

![sito di pubblicazione](assets/publish-site.png)

Ci sarà un&#39;indicazione che il sito è stato pubblicato.

![pubblicato sul sito](assets/site-published.png)

## Utenti e gruppi di utenti della community {#community-users-user-groups}

### Nuovi gruppi di utenti della community {#notice-new-community-user-groups}

Insieme al nuovo sito della community, vengono creati nuovi gruppi di utenti con le autorizzazioni appropriate impostate per diverse funzioni amministrative. Per maggiori dettagli, visita [Gruppi di utenti per siti della community](/help/communities/users.md#usergroupsforcommunitysites).

Per questo nuovo sito della community, dato il nome del sito &quot;enable&quot; nel passaggio 1, i nuovi gruppi di utenti esistenti nell’ambiente di pubblicazione possono essere visualizzati dal [Console Membri e gruppi delle community](/help/communities/members.md#groups-console):

![community_usergroup](assets/community_usergroup.png)

### Assegna membri a gruppo di membri di abilitazione community {#assign-members-to-community-enable-members-group}

Su autore, con il servizio tunnel abilitato, è possibile assegnare il [utenti creati durante la configurazione iniziale](/help/communities/enablement-setup.md#publishcreateenablementmembers) al gruppo dei membri della community per il sito della community appena creato.

Utilizzando la console Gruppi della community, i membri possono essere aggiunti singolarmente o tramite l’appartenenza a un gruppo.

In questo esempio, il gruppo `Community Ski Class` viene aggiunto come membro del gruppo `Community Enable Members` nonché membro `Quinn Harper`.

* Passa a **Community, gruppi** console
* Seleziona *Community Abilita membri* gruppo
* Inserisci &#39;ski&#39; nel **Aggiungi membri al gruppo** casella di ricerca
* Seleziona *Classe sciistica comunitaria* (gruppo di studenti)
* Inserisci &#39;quinn&#39; nella casella di ricerca
* Seleziona *Quinn Harper* (contatto risorse di abilitazione)

* Seleziona **Salva**

![edit-group-settings](assets/edit-group-settings.png)

## Configurazioni su pubblicazione {#configurations-on-publish}

`https://localhost:4503/content/sites/enable/en.html {#http-localhost-content-sites-enable-en-html}`

![enablement-login](assets/enablement-login.png)

### Configurazione per errore di autenticazione {#configure-for-authentication-error}

Una volta che un sito è stato configurato e inviato per la pubblicazione, [configurare la mappatura degli accessi](/help/communities/sites-console.md#configure-for-authentication-error) ( `Adobe Granite Login Selector Authentication Handler`) sull’istanza di pubblicazione. Il vantaggio è che quando le credenziali di accesso non vengono immesse correttamente, l&#39;errore di autenticazione rivisualizza la pagina di accesso del sito della community con un messaggio di errore.

Aggiungi un `Login Page Mapping` come:

* `/content/sites/enable/en/signin:/content/sites/enable/en`

### (Facoltativo) Modificare la home page predefinita {#optional-change-the-default-home-page}

Quando si lavora con il sito di pubblicazione a scopo dimostrativo, potrebbe essere utile modificare la home page predefinita nel nuovo sito.

A tal fine è necessario utilizzare [CRX|DE](https://localhost:4503/crx/de) Lite per modificare il [mappatura delle risorse](/help/sites-deploying/resource-mapping.md) tabella sulla pubblicazione.

Per iniziare:

1. Al momento della pubblicazione, accedi a CRXDE e accedi con privilegi di amministratore

   * Ad esempio, cerca [https://localhost:4503/crx/de](https://localhost:4503/crx/de) e accedi con `admin/admin`

1. Nel browser del progetto, espandi `/etc/map`
1. Seleziona la `http` nodo

   * Seleziona **Crea nodo**

      * **Nome** localhost.4503

         (do *not* utilizzare &#39;:&#39;)

      * **Tipo** [sling:Mapping](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)

1. Con la nuova creazione `localhost.4503` nodo selezionato

   * Aggiungi proprietà

      * **Nome** sling:match
      * **Tipo** Stringa
      * **Valore** localhost.4503/$

   (deve terminare con il carattere &#39;$&#39;)

   * Aggiungi proprietà

      * **Nome** sling:internalRedirect
      * **Tipo** Stringa
      * **Valore** /content/sites/enable/en.html


1. Seleziona **Salva tutto**
1. (Facoltativo) Elimina la cronologia di navigazione
1. Sfoglia https://localhost:4503/

   * Arriva a https://localhost:4503/content/sites/enable/en.html

>[!NOTE]
>
>Per disattivare, è sufficiente pre-pend il `sling:match` valore della proprietà con un valore &#39;x&#39; - `xlocalhost.4503/$` - e **Salva tutto**.

![change-default-homepage](assets/change-default-homepage.png)

#### Risoluzione dei problemi: Errore durante il salvataggio della mappa {#troubleshooting-error-saving-map}

Se non riesci a salvare le modifiche, assicurati che il nome del nodo sia `localhost.4503`, con un separatore &quot;punto&quot; e non `localhost:4503` con un separatore a due punti, come `localhost` non è un prefisso dello spazio dei nomi valido.

![mappa degli errori](assets/error-map.png)

#### Risoluzione dei problemi: Impossibile reindirizzare {#troubleshooting-fail-to-redirect}

Il **$**&quot; alla fine dell&#39;espressione regolare `sling:match` la stringa è cruciale, in modo che solo `https://localhost:4503/` è mappato, altrimenti il valore di reindirizzamento viene preceduto da qualsiasi percorso che potrebbe esistere dopo server:port nell&#39;URL. Pertanto, quando AEM tenta di reindirizzare alla pagina di accesso, non riesce.

## Modifica del sito della community {#modifying-the-community-site}

Dopo la creazione iniziale del sito, gli autori possono utilizzare il [Icona Apri sito](/help/communities/sites-console.md#authoring-site-content) per eseguire attività di authoring standard AEM.

Inoltre, gli amministratori possono utilizzare [Icona Modifica sito](/help/communities/sites-console.md#modifying-site-properties) per modificare le proprietà del sito, ad esempio il titolo.

Dopo qualsiasi modifica, ricorda di **Salva** e **Pubblica** il sito.

>[!NOTE]
>
>Se non hai familiarità con AEM, consulta la documentazione su [trattamento di base](/help/sites-authoring/basic-handling.md) e [guida rapida all’authoring delle pagine](/help/sites-authoring/qg-page-authoring.md).

### Aggiungere un catalogo {#add-a-catalog}

Il modello di sito community scelto per questo sito community deve contenere la funzione di catalogo.

In caso contrario, è possibile aggiungere facilmente la funzione di catalogo. In questo modo gli altri membri della community, non assegnati a risorse di abilitazione o a un percorso di apprendimento, potranno selezionare risorse di abilitazione da un catalogo.

Se la struttura del sito contiene già la funzione catalogo, è possibile modificare il relativo Titolo.

Per modificare la struttura del sito, passa a **[!UICONTROL Community]** > **[!UICONTROL Sites]** aprire la console `enable` e seleziona la **Modifica sito** per accedere alle proprietà di `Enablement Tutorial`.

Seleziona il pannello STRUTTURA per aggiungere un catalogo o modificare un catalogo esistente :

* **Titolo**: `Ski Catalog`

* **URL**: `catalog`

* **Seleziona tutti i namespace**: lascia come predefinito.

* Seleziona **Salva**.

![struttura-sito di modifica](assets/modify-site-structure.png)

Utilizzare l&#39;icona Posizione per spostare la funzione Catalogo nella seconda posizione, dopo Assegnazioni.

![move-catalog-func](assets/move-catalog-func.png)

Seleziona **Salva** nell&#39;angolo in alto a destra per salvare le modifiche al sito community.

Quindi ri-**Pubblica** il sito.
