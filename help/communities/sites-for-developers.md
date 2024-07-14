---
title: Nozioni di base sul sito community
description: Esportazione ed eliminazione di siti community e creazione di modelli di sito personalizzati
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 1dc568cd-315c-4944-9a3e-e5d7794e5dc0
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '488'
ht-degree: 1%

---

# Nozioni di base sul sito community {#community-site-essentials}

## Modello di sito personalizzato {#custom-site-template}

Un modello di sito personalizzato può essere specificato separatamente per ogni copia per lingua di un sito community.

Per eseguire questa operazione:

* Crea un modello personalizzato.
* Sovrapponi il percorso predefinito del modello del sito.
* Aggiungi il modello personalizzato al percorso di sovrapposizione.
* Specificare il modello personalizzato aggiungendo una proprietà `page-template` al nodo `configuration`.

**Modello predefinito**:

`/libs/social/console/components/hbs/sitepage/sitepage.hbs`

**Modello personalizzato nel percorso di sovrapposizione**:

`/apps/social/console/components/hbs/sitepage/template-name.hbs`

**Proprietà**: modello pagina

**Tipo**: Stringa

**Valore**: `template-name` (nessuna estensione)

**Nodo di configurazione**:

`/content/community site path/lang/configuration`

Esempio: `/content/sites/engage/en/configuration`

>[!NOTE]
>
>Tutti i nodi nel percorso sovrapposto devono essere solo di tipo `Folder`.

>[!CAUTION]
>
>Se al modello personalizzato viene assegnato il nome *sitepage.hbs*, verranno personalizzati tutti i siti della community.

### Esempio di modello di sito personalizzato {#custom-site-template-example}

Ad esempio, `vertical-sitepage.hbs` è un modello di sito che determina il posizionamento di collegamenti di menu in verticale lungo il lato sinistro della pagina, invece che in orizzontale sotto il banner.

[Ottieni file](assets/vertical-sitepage.hbs)
Posiziona il modello di sito personalizzato nella cartella di sovrapposizione:

`/apps/social/console/components/hbs/sitepage/vertical-sitepage.hbs`

Identificare il modello personalizzato aggiungendo una proprietà `page-template` al nodo di configurazione:

`/content/sites/sample/en/configuration`

![configurazione del sito crxde](assets/crxde-siteconfiguration.png)

Assicurarsi di **Salvare tutto** e replicare il codice personalizzato in tutte le istanze di Adobe Experience Manager (AEM). Il codice personalizzato non è incluso quando il contenuto del sito community viene pubblicato dalla console.

La procedura consigliata per la replica del codice personalizzato è [creare un pacchetto](../../help/sites-administering/package-manager.md#creating-a-new-package) e distribuirlo in tutte le istanze.

## Esportazione di un sito community {#exporting-a-community-site}

Una volta creato un sito community, è possibile esportarlo come pacchetto AEM memorizzato in Gestione pacchetti e disponibile per il download e il caricamento.

È disponibile dalla console [Siti community](sites-console.md#exporting-the-site).

UGC e codice personalizzato non sono inclusi nel pacchetto per il sito community.

Per esportare UGC, utilizza [AEM Communities UGC Migration Tool](https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration), uno strumento di migrazione open-source disponibile su GitHub.

## Eliminazione di un sito community {#deleting-a-community-site}

In AEM Communities 6.3 Service Pack 1, l&#39;icona Elimina sito viene visualizzata quando si passa il puntatore del mouse sul sito community dalla console **[!UICONTROL Communities]** > **[!UICONTROL Sites]**. Durante lo sviluppo, se si desidera eliminare un sito community e ricominciare da capo, è possibile utilizzare questa funzionalità. Quando si elimina un sito community, vengono rimossi i seguenti elementi associati a tale sito:

* [UGC](#user-generated-content)
* [Gruppi di utenti](#community-user-groups)
* [Record di database](#database-records)

### ID sito univoco community {#community-unique-site-id}

Per identificare l&#39;ID sito univoco associato al sito community, utilizzando CRXDE:

* Passare alla lingua root del sito, ad esempio `/content/sites/*<site name>*/en/rep:policy`.

* Trovare il nodo `allow<#>` con `rep:principalName` in questo formato `rep:principalName = *community-enable-nrh9h-members*`.

* L&#39;ID sito è il terzo componente di `rep:principalName`

  Ad esempio, se `rep:principalName = community-enable-nrh9h-members`

   * **nome sito** = *abilita*
   * **ID sito** = *nrh9h*
   * **ID sito univoco** = *enable-nrh9h*

### Contenuti generati dall&#39;utente {#user-generated-content}

Ottieni il progetto Communities-srp-tools da GitHub:

* [https://github.com/Adobe-Marketing-Cloud/aem-communities-srp-tools](https://github.com/Adobe-Marketing-Cloud/aem-communities-srp-tools)

Contiene un servlet per eliminare tutti i contenuti generati dagli utenti (UGC, User-Generated Content) da qualsiasi SRP.

Tutti i contenuti UGC possono essere rimossi o per un sito specifico, ad esempio:

* `path=/content/usergenerated/asi/mongo/content/sites/engage`

Questo rimuove solo i contenuti generati dall’utente (immessi al momento della pubblicazione) e non quelli creati (immessi al momento dell’authoring). Pertanto, [i nodi shadow](srp.md#shadownodes) non sono interessati.

### Gruppi di utenti community {#community-user-groups}

In tutte le istanze di authoring e pubblicazione, dalla [console di sicurezza](../../help/sites-administering/security.md), individuare e rimuovere i [gruppi di utenti](users.md):

* Con prefisso `community`
* Seguito da [id sito univoco](#community-unique-site-id)

Esempio: `community-engage-x0e11-members`.
