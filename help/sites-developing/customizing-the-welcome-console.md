---
title: Personalizzazione della console di benvenuto (interfaccia classica)
description: La console Benvenuti fornisce un elenco di collegamenti alle varie console e funzionalità dell’AEM
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
exl-id: 9e171b62-8efb-4143-a202-ba6555658d4b
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 6%

---

# Personalizzazione della console di benvenuto (interfaccia classica){#customizing-the-welcome-console-classic-ui}

>[!CAUTION]
>
>Questa pagina tratta l’interfaccia utente classica.
>
>Consulta [Personalizzazione delle console](/help/sites-developing/customizing-consoles-touch.md) per informazioni dettagliate sull’interfaccia utente standard touch.

La console di benvenuto fornisce un elenco di collegamenti alle varie console e funzionalità di AEM.

![cq_welcomescreen](assets/cq_welcomescreen.png)

È possibile configurare i collegamenti visibili. Questa può essere definita per utenti e/o gruppi specifici. Le azioni da intraprendere dipendono dal tipo di destinazione (che si collega alla sezione della console in cui si trovano):

* [Console principali](#links-in-main-console-left-pane) - Collegamenti nella console principale (riquadro a sinistra)
* [Risorse, documentazione e riferimenti, funzioni](#links-in-sidebar-right-pane) - Collegamenti nella barra laterale (riquadro destro)

## Collegamenti nella console principale (riquadro sinistro) {#links-in-main-console-left-pane}

Elenco delle principali console dell’AEM.

![cq_welcomescreenmainconsole](assets/cq_welcomescreenmainconsole.png)

### Configurazione della visibilità dei collegamenti della console principale {#configuring-whether-main-console-links-are-visible}

Le autorizzazioni a livello di nodo determinano se il collegamento può essere visualizzato o meno. I nodi in questione sono:

* **Siti Web:** `/libs/wcm/core/content/siteadmin`

* **Risorse digitali:** `/libs/wcm/core/content/damadmin`

* **Community:** `/libs/collab/core/content/admin`

* **Campagne:** `/libs/mcm/content/admin`

* **Casella in entrata:** `/libs/cq/workflow/content/inbox`

* **Utenti:** `/libs/cq/security/content/admin`

* **Strumenti:** `/libs/wcm/core/content/misc`

* **Assegnazione tag:** `/libs/cq/tagging/content/tagadmin`

Ad esempio:

* Per limitare l&#39;accesso a **Strumenti**, rimuovere l&#39;accesso in lettura da

  `/libs/wcm/core/content/misc`

Consulta la [Sezione Sicurezza](/help/sites-administering/security.md) per ulteriori informazioni su come impostare le autorizzazioni desiderate.

### Collegamenti nella barra laterale (riquadro destro) {#links-in-sidebar-right-pane}

![cq_welcomescreensidebar](assets/cq_welcomescreensidebar.png)

Questi collegamenti si basano sull&#39;esistenza di *e* accesso in lettura ai nodi nel seguente percorso:

`/libs/cq/core/content/welcome`

Per impostazione predefinita, sono disponibili tre sezioni (leggermente distanziate):

<table>
 <tbody>
  <tr>
   <td><strong>Riferimenti</strong></td>
   <td> </td>
  </tr>
  <tr>
   <td> Servizi cloud</td>
   <td><code>/libs/cq/core/content/welcome/resources/cloudservices</code></td>
  </tr>
  <tr>
   <td> Flussi di lavoro</td>
   <td><code>/libs/cq/core/content/welcome/resources/workflows</code></td>
  </tr>
  <tr>
   <td> Gestione attività</td>
   <td><code>/libs/cq/core/content/welcome/resources/taskmanager</code></td>
  </tr>
  <tr>
   <td> Replica</td>
   <td><code>/libs/cq/core/content/welcome/resources/replication</code></td>
  </tr>
  <tr>
   <td> Rapporti</td>
   <td><code>/libs/cq/core/content/welcome/resources/reports</code></td>
  </tr>
  <tr>
   <td> Pubblicazioni</td>
   <td><code>/libs/cq/core/content/welcome/resources/publishingadmin</code></td>
  </tr>
  <tr>
   <td> Manoscritti</td>
   <td><code>/libs/cq/core/content/welcome/resources/manuscriptsadmin</code></td>
  </tr>
  <tr>
   <td><strong>Documentazione e riferimenti</strong></td>
   <td> </td>
  </tr>
  <tr>
   <td> Documentazione</td>
   <td><code>/libs/cq/core/content/welcome/docs/docs</code></td>
  </tr>
  <tr>
   <td> Riferimenti per sviluppatori</td>
   <td><code>/libs/cq/core/content/welcome/docs/dev</code></td>
  </tr>
  <tr>
   <td><strong>Funzioni</strong></td>
   <td> </td>
  </tr>
  <tr>
   <td> CRXDE Lite</td>
   <td><code>/libs/cq/core/content/welcome/features/crxde</code></td>
  </tr>
  <tr>
   <td> Pacchetti</td>
   <td><code>/libs/cq/core/content/welcome/features/packages</code></td>
  </tr>
  <tr>
   <td> Condivisione pacchetti</td>
   <td><code>/libs/cq/core/content/welcome/features/share</code></td>
  </tr>
  <tr>
   <td> Clustering</td>
   <td><code>/libs/cq/core/content/welcome/features/cluster</code></td>
  </tr>
  <tr>
   <td> Backup</td>
   <td><code>/libs/cq/core/content/welcome/features/backup</code></td>
  </tr>
  <tr>
   <td> Console Web<br /> </td>
   <td><code>/libs/cq/core/content/welcome/features/config</code></td>
  </tr>
  <tr>
   <td> Immagine stato console Web<br /> </td>
   <td><code>/libs/cq/core/content/welcome/features/statusdump</code></td>
  </tr>
 </tbody>
</table>

#### Configurazione della visibilità dei collegamenti della barra laterale {#configuring-whether-sidebar-links-are-visible}

È possibile nascondere un collegamento a utenti o gruppi specifici rimuovendo l’accesso in lettura ai nodi che lo rappresentano.

* Risorse: rimuovi l’accesso a:

  `/libs/cq/core/content/welcome/resources/<link-target>`

* Docs - rimuovi accesso a:

  `/libs/cq/core/content/welcome/docs/<link-target>`

* Funzioni: rimuovi l’accesso a:

  `/libs/cq/core/content/welcome/features/<link-target>`

Ad esempio:

* Per rimuovere il collegamento a **Rapporti**, rimuovere l&#39;accesso in lettura da

  `/libs/cq/core/content/welcome/resources/reports`

* Per rimuovere il collegamento a **Pacchetti**, rimuovere l&#39;accesso in lettura da

  `/libs/cq/core/content/welcome/features/packages`

Consulta la [Sezione Sicurezza](/help/sites-administering/security.md) per ulteriori informazioni su come impostare le autorizzazioni desiderate.

### Meccanismo di selezione dei collegamenti {#link-selection-mechanism}

In entrata `/libs/cq/core/components/welcome/welcome.jsp` sia fatto di [ConsoleUtil](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/ConsoleUtil.html), che esegue una query sui nodi che dispongono della proprietà:

* `jcr:mixinTypes` con il valore: `cq:Console`

>[!NOTE]
>
>Esegui la seguente query per visualizzare l’elenco esistente:
>
>* `select * from cq:Console`
>

Quando un utente o un gruppo non dispone dell’autorizzazione di lettura per un nodo con il mixin `cq:Console`, tale nodo non viene recuperato da `ConsoleUtil` ricerca, pertanto non è elencato nella console.

### Aggiunta di un elemento personalizzato {#adding-a-custom-item}

Il [meccanismo di selezione dei collegamenti](#link-selection-mechanism) può essere utilizzato per aggiungere un elemento personalizzato all’elenco dei collegamenti.

Aggiungere l&#39;elemento personalizzato all&#39;elenco aggiungendo `cq:Console` mixin al widget o alla risorsa. A tale scopo, definisci la proprietà:

* `jcr:mixinTypes` con il valore: `cq:Console`
