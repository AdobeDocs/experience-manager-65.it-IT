---
title: Community Site Essentials
seo-title: Community Site Essentials
description: Esportazione ed eliminazione di siti community e creazione di modelli di sito personalizzati
seo-description: Esportazione ed eliminazione di siti community e creazione di modelli di sito personalizzati
uuid: f0ec0e71-64e9-415a-b14a-939a9b1611c1
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: dc7a085e-d6de-4bc8-bd7e-6b43f8d172d2
translation-type: tm+mt
source-git-commit: e49acbc042d84ae970058b4e99ab6f980866db5a
workflow-type: tm+mt
source-wordcount: '574'
ht-degree: 1%

---


# Community Site Essentials {#community-site-essentials}

## Modello del sito personalizzato {#custom-site-template}

Un modello di sito personalizzato può essere specificato separatamente per ogni copia in lingua di un sito community.

A questo scopo:

* Creare un modello personalizzato.
* Sovrapponete il percorso predefinito del modello di sito.
* Aggiungete il modello personalizzato al percorso della sovrapposizione.
* Specificare il modello personalizzato aggiungendo una `page-template` proprietà al `configuration` nodo.

**Modello** predefinito:

`/libs/social/console/components/hbs/sitepage/sitepage.hbs`

**Modello personalizzato nel percorso** della sovrapposizione:

`/apps/social/console/components/hbs/sitepage/template-name.hbs`

**Proprietà**: page-template

**Tipo**: Stringa

**Valore**: `template-name` (nessuna estensione)

**Nodo** di configurazione:

`/content/community site path/lang/configuration`

Esempio: `/content/sites/engage/en/configuration`

>[!NOTE]
>
>Tutti i nodi del percorso sovrapposto devono essere solo di tipo `Folder`.


>[!CAUTION]
>
>Se al modello personalizzato viene assegnato il nome *sitepage.hbs*, tutti i siti della community verranno personalizzati.


### Esempio di modello di sito personalizzato {#custom-site-template-example}

Ad esempio, `vertical-sitepage.hbs` è un modello di sito che consente di posizionare verticalmente i collegamenti dei menu verso il basso a sinistra della pagina, anziché in orizzontale sotto il banner.

[Ottieni file](assets/vertical-sitepage.hbs)Inserite il modello di sito personalizzato nella cartella delle sovrapposizioni:

`/apps/social/console/components/hbs/sitepage/vertical-sitepage.hbs`

Identificare il modello personalizzato aggiungendo una `page-template` proprietà al nodo di configurazione:

`/content/sites/sample/en/configuration`

![crxde-siteconfigurazione](assets/crxde-siteconfiguration.png)

Accertatevi di **salvare tutto** e replicare il codice personalizzato a tutte le istanze AEM (il codice personalizzato non è incluso quando il contenuto del sito community viene pubblicato dalla console).

La procedura consigliata per la replica del codice personalizzato consiste nel [creare un pacchetto](../../help/sites-administering/package-manager.md#creating-a-new-package) e distribuirlo in tutte le istanze.

## Esportazione di un sito community {#exporting-a-community-site}

Una volta creato un sito community, è possibile esportare il sito come pacchetto AEM memorizzato in package manager e disponibile per il download e il caricamento.

È disponibile dalla console [Siti](sites-console.md#exporting-the-site)community.

Si noti che UGC e codice personalizzato non sono inclusi nel pacchetto del sito community.

Per esportare UGC, utilizzate [AEM Communities UGC Migration Tool](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration), uno strumento di migrazione open source disponibile su GitHub.

## Eliminazione di un sito community {#deleting-a-community-site}

A partire  AEM Communities 6.3 Service Pack 1, l&#39;icona Elimina sito viene visualizzata quando si passa il puntatore del mouse sul sito della community dalla console **[!UICONTROL Community]** > **[!UICONTROL Siti]** . Durante lo sviluppo, se si desidera eliminare un sito community e iniziare a utilizzarne uno nuovo, è possibile utilizzare questa funzionalità. Eliminando un sito community, vengono rimossi i seguenti elementi associati a tale sito:

* [UGC](#user-generated-content)
* [Gruppi di utenti](#community-user-groups)
* [Assets](#enablement-assets)
* [Record del database](#database-records)

### ID sito univoco community {#community-unique-site-id}

Per identificare l&#39;ID univoco del sito associato al sito community, utilizzando CRXDE:

* Andate alla directory principale della lingua del sito, ad esempio `/content/sites/*<site name>*/en/rep:policy`.

* Trova il `allow<#>` nodo con un `rep:principalName` in questo formato `rep:principalName = *community-enable-nrh9h-members*`.

* L’ID sito è il terzo componente di `rep:principalName`

   Ad esempio, se `rep:principalName = community-enable-nrh9h-members`

   * **nome** sito = *enable*
   * **ID** sito = *nrh9h*
   * **ID** univoco del sito = *enable-nrh9h*

### Contenuto generato dall&#39;utente {#user-generated-content}

Ottenete il progetto community-srp-tools da Github:

* [https://github.com/Adobe-Marketing-Cloud/communities-srp-tools](https://github.com/Adobe-Marketing-Cloud/communities-srp-tools)

Contiene un servlet per eliminare tutti gli UGC da qualsiasi SRP.

Tutti gli UGC possono essere rimossi o per un sito specifico, ad esempio:

* `path=/content/usergenerated/asi/mongo/content/sites/engage`

Questo rimuove solo il contenuto generato dall’utente (immesso al momento della pubblicazione) e non il contenuto generato (immesso all’autore). Pertanto, i nodi [](srp.md#shadownodes) ombra non vengono modificati.

### Gruppi utenti community {#community-user-groups}

Per tutte le istanze di creazione e pubblicazione, dalla console [di](../../help/sites-administering/security.md)sicurezza individuate e rimuovete i gruppi [di](users.md) utenti che sono:

* Prefisso con `community`
* Seguito da un ID sito [univoco](#community-unique-site-id)

Esempio, `community-engage-x0e11-members`.

### Risorse di abilitazione {#enablement-assets}

Dalla console principale:

* Select **[!UICONTROL Assets]**.
* Accedete alla modalità **[!UICONTROL Seleziona]** .
* Selezionate una cartella denominata con l&#39;ID [sito](#community-unique-site-id)univoco.
* Selezionate **[!UICONTROL Elimina]** (potrebbe essere necessario selezionare **[!UICONTROL Altro...]**).

### Record del database {#database-records}

Non esiste uno strumento per eliminare selettivamente le voci del database per un sito community di abilitazione specifico.

Quando tutti i siti community vengono eliminati, eliminare enablementdb e scormenginedb utilizzando MySQL Workbench.
