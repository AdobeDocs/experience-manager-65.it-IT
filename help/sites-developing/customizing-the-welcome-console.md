---
title: Personalizzazione della console di benvenuto (interfaccia classica)
seo-title: Personalizzazione della console di benvenuto (interfaccia classica)
description: La console di benvenuto contiene un elenco di collegamenti alle varie console e funzionalità presenti in AEM
seo-description: La console di benvenuto contiene un elenco di collegamenti alle varie console e funzionalità presenti in AEM
uuid: 4ef20cef-2d7a-417d-b36b-ed4fa56cd511
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 2e408acb-3802-4837-8619-688cfc3abfa7
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 9%

---


# Personalizzazione della console di benvenuto (interfaccia classica){#customizing-the-welcome-console-classic-ui}

>[!CAUTION]
>
>Questa pagina fa riferimento all’interfaccia utente classica.
>
>Per informazioni dettagliate sull&#39;interfaccia touch standard, consultate [Personalizzazione delle console](/help/sites-developing/customizing-consoles-touch.md).

La console Benvenuto contiene un elenco di collegamenti alle varie console e funzionalità presenti in AEM.

![cq_welcomescreen](assets/cq_welcomescreen.png)

È possibile configurare i collegamenti visibili. Questo può essere definito per utenti e/o gruppi specifici. Le azioni da eseguire dipendono dal tipo di destinazione (correlato alla sezione della console in cui si trovano):

* [Console](#links-in-main-console-left-pane)  principali - Collegamenti nella console principale (riquadro a sinistra)
* [Risorse, documentazione e riferimenti, funzioni](#links-in-sidebar-right-pane)  - Collegamenti nella barra laterale (riquadro a destra)

## Collegamenti nella console principale (riquadro a sinistra) {#links-in-main-console-left-pane}

Vengono elencate le console principali di AEM.

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

Esempio:

* Per limitare l&#39;accesso a **Strumenti**, rimuovere l&#39;accesso in lettura da

   `/libs/wcm/core/content/misc`

Per ulteriori informazioni sull&#39;impostazione delle autorizzazioni desiderate, vedere la sezione [Protezione](/help/sites-administering/security.md).

### Collegamenti nella barra laterale (riquadro a destra) {#links-in-sidebar-right-pane}

![cq_welcomescreensidebar](assets/cq_welcomescreensidebar.png)

Questi collegamenti si basano sull&#39;esistenza di *e* accesso in lettura ai nodi nel percorso seguente:

`/libs/cq/core/content/welcome`

Per impostazione predefinita sono disponibili tre sezioni (distanziate leggermente):

<table>
 <tbody>
  <tr>
   <td><strong>Riferimenti</strong></td>
   <td> </td>
  </tr>
  <tr>
   <td> Cloud Services</td>
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
   <td><strong>Documentazione e riferimento</strong></td>
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

#### Configurazione dei collegamenti della barra laterale visibili {#configuring-whether-sidebar-links-are-visible}

È possibile nascondere un collegamento da utenti o gruppi specifici rimuovendo l&#39;accesso in lettura ai nodi che rappresentano il collegamento.

* Risorse - rimuovere l&#39;accesso a:

   `/libs/cq/core/content/welcome/resources/<link-target>`

* Documenti - rimuovere l&#39;accesso a:

   `/libs/cq/core/content/welcome/docs/<link-target>`

* Funzionalità: rimozione dell&#39;accesso a:

   `/libs/cq/core/content/welcome/features/<link-target>`

Esempio:

* Per rimuovere il collegamento a **Reports**, rimuovere l&#39;accesso in lettura da

   `/libs/cq/core/content/welcome/resources/reports`

* Per rimuovere il collegamento a **Packages**, rimuovere l&#39;accesso in lettura da

   `/libs/cq/core/content/welcome/features/packages`

Per ulteriori informazioni sull&#39;impostazione delle autorizzazioni desiderate, vedere la sezione [Protezione](/help/sites-administering/security.md).

### Meccanismo di selezione del collegamento {#link-selection-mechanism}

In `/libs/cq/core/components/welcome/welcome.jsp` viene utilizzato [ConsoleUtil](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/ConsoleUtil.html), che esegue una query sui nodi che hanno la proprietà:

* `jcr:mixinTypes` con il valore:  `cq:Console`

>[!NOTE]
>
>Esegui la seguente query per visualizzare l&#39;elenco esistente:
>
>* `select * from cq:Console`

>



Se un utente o un gruppo non dispone dell&#39;autorizzazione di lettura su un nodo con il mixin `cq:Console`, tale nodo non viene recuperato dalla ricerca `ConsoleUtil`, pertanto non viene elencato nella console.

### Aggiunta di un elemento personalizzato {#adding-a-custom-item}

Il [meccanismo di selezione dei collegamenti](#link-selection-mechanism) può essere utilizzato per aggiungere un elemento personalizzato all&#39;elenco dei collegamenti.

Aggiungi l&#39;elemento personalizzato all&#39;elenco aggiungendo il mixin `cq:Console` al widget o alla risorsa. Questa operazione viene eseguita definendo la proprietà:

* `jcr:mixinTypes` con il valore:  `cq:Console`

