---
title: Personalizzazione della console Siti Web (interfaccia classica)
seo-title: Personalizzazione della console Siti Web (interfaccia classica)
description: La console Amministrazione siti Web può essere estesa per visualizzare colonne personalizzate
seo-description: La console Amministrazione siti Web può essere estesa per visualizzare colonne personalizzate
uuid: 9163fdff-5351-477d-b91c-8a74f8b41d34
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: aeb37103-541d-4235-8a78-980b78c8de66
docset: aem65
translation-type: tm+mt
source-git-commit: ebf3f34af7da6b1a659ac8d8843152b97f30b652
workflow-type: tm+mt
source-wordcount: '798'
ht-degree: 0%

---


# Personalizzazione della console Siti Web (interfaccia classica){#customizing-the-websites-console-classic-ui}

## Aggiunta di una colonna personalizzata alla console Siti Web (siteadmin) {#adding-a-custom-column-to-the-websites-siteadmin-console}

La console Amministrazione siti Web può essere estesa per visualizzare colonne personalizzate. La console è basata su un oggetto JSON che può essere esteso creando un servizio OSGI che implementa l&#39;interfaccia `ListInfoProvider`. Tale servizio modifica l&#39;oggetto JSON inviato al client per creare la console.

Questa esercitazione dettagliata spiega come visualizzare una nuova colonna nella console Amministrazione siti Web implementando l&#39;interfaccia `ListInfoProvider`. Si compone dei seguenti passaggi:

1. [Creazione del ](#creating-the-osgi-service) servizio OSGI e distribuzione del bundle che lo contiene nel server AEM.
1. (facoltativo) [Verifica del nuovo servizio](#testing-the-new-service) mediante una chiamata JSON per richiedere l&#39;oggetto JSON utilizzato per creare la console.
1. [Visualizzazione della nuova ](#displaying-the-new-column) colonna estendendo la struttura dei nodi della console nella directory archivio.

>[!NOTE]
>
>Questa esercitazione può essere utilizzata anche per estendere le seguenti console di amministrazione:
>
>* la console Risorse digitali
>* la console Community

>



### Creazione del servizio OSGI {#creating-the-osgi-service}

L&#39;interfaccia `ListInfoProvider` definisce due metodi:

* `updateListGlobalInfo`, per aggiornare le proprietà globali dell&#39;elenco,
* `updateListItemInfo`, per aggiornare una singola voce di elenco.

Gli argomenti di entrambi i metodi sono:

* `request`, l&#39;oggetto di richiesta Sling HTTP associato,
* `info`, l&#39;oggetto JSON da aggiornare, che è rispettivamente l&#39;elenco globale o la voce di elenco corrente,
* `resource`, una risorsa Sling.

Esempio di implementazione:

* Aggiunge una proprietà *starred* per ogni elemento, che è `true` se il nome della pagina inizia con un *e*, altrimenti `false`.

* Aggiunge una proprietà *starredCount*, che è globale per l&#39;elenco e contiene il numero di voci dell&#39;elenco di destinazione.

Per creare il servizio OSGI:

1. In CRXDE Lite, [creare un bundle](/help/sites-developing/developing-with-crxde-lite.md#managing-a-bundle).
1. Aggiungete il codice di esempio riportato di seguito.
1. Create il bundle.

Il nuovo servizio è attivo e funzionante.

```java
package com.test;

import com.day.cq.commons.ListInfoProvider;
import com.day.cq.i18n.I18n;
import com.day.cq.wcm.api.Page;
import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Service;
import org.apache.sling.api.SlingHttpServletRequest;
import org.apache.sling.api.resource.Resource;
import org.apache.sling.commons.json.JSONException;
import org.apache.sling.commons.json.JSONObject;

@Component(metatype = false)
@Service(value = ListInfoProvider.class)
public class StarredListInfoProvider implements ListInfoProvider {

    private int count = 0;

    public void updateListGlobalInfo(SlingHttpServletRequest request, JSONObject info, Resource resource) throws JSONException {
        info.put("starredCount", count);
        count = 0; // reset for next execution
    }

    public void updateListItemInfo(SlingHttpServletRequest request, JSONObject info, Resource resource) throws JSONException {
        Page page = resource.adaptTo(Page.class);
        if (page != null) {
            // Consider starred if page name starts with 'e'
            boolean starred = page.getName().startsWith("e");
            if (starred) {
                count++;
            }
            I18n i18n = new I18n(request);
            info.put("starred", starred ? i18n.get("Yes") : i18n.get("No"));
        }
    }

}
```

>[!CAUTION]
>
>* In base alla richiesta e/o alla risorsa fornita, l&#39;implementazione deve decidere se aggiungere o meno le informazioni all&#39;oggetto JSON.
>* Se l&#39;implementazione `ListInfoProvider` definisce una proprietà già esistente nell&#39;oggetto response, il suo valore verrà sovrascritto da quello fornito.

>
>  
È possibile utilizzare la classificazione [del servizio](https://www.osgi.org/javadoc/r2/org/osgi/framework/Constants.html#SERVICE_RANKING) per gestire l&#39;ordine di esecuzione di più implementazioni `ListInfoProvider`.

### Verifica del nuovo servizio {#testing-the-new-service}

Quando aprite la console di amministrazione dei siti Web e sfogliate il sito, il browser esegue una chiamata ajax per ottenere l’oggetto JSON utilizzato per creare la console. Ad esempio, quando individuate la cartella `/content/geometrixx`, la seguente richiesta viene inviata al server AEM per creare la console:

[https://localhost:4502/content/geometrixx.pages.json?start=0&amp;limit=30&amp;predicate=siteadmin](https://localhost:4502/content/geometrixx.pages.json?start=0&amp;limit=30&amp;predicate=siteadmin)

Per essere certi che il nuovo servizio sia in esecuzione dopo aver distribuito il pacchetto che lo contiene:

1. Impostate il browser sul seguente URL:
   [https://localhost:4502/content/geometrixx.pages.json?start=0&amp;limit=30&amp;predicate=siteadmin](https://localhost:4502/content/geometrixx.pages.json?start=0&amp;limit=30&amp;predicate=siteadmin)

1. La risposta deve visualizzare le nuove proprietà come segue:

![screen_shot_2012-02-13at163046](assets/screen_shot_2012-02-13at163046.png)

### Visualizzazione della nuova colonna {#displaying-the-new-column}

L&#39;ultimo passaggio consiste nell&#39;adattare la struttura dei nodi della console Amministrazione siti Web per visualizzare la nuova proprietà per tutte le pagine di Geometrixx sovrapponendo `/libs/wcm/core/content/siteadmin`. Procedere come segue:

1. In CRXDE Lite, creare la struttura dei nodi `/apps/wcm/core/content` con nodi di tipo `sling:Folder` per riflettere la struttura `/libs/wcm/core/content`.

1. Copiare il nodo `/libs/wcm/core/content/siteadmin` e incollarlo sotto `/apps/wcm/core/content`.

1. Copiare il nodo `/apps/wcm/core/content/siteadmin/grid/assets` in `/apps/wcm/core/content/siteadmin/grid/geometrixx` e modificarne le proprietà:

   * Rimuovi **pageText**

   * Impostare **pathRegex** su `/content/geometrixx(/.*)?`
In questo modo la configurazione della griglia sarà attiva per tutti i siti Web geometrixx.

   * Impostare **storeProxySuffix** su `.pages.json`

   * Modificare la proprietà multivalore **storeReaderFields** e aggiungere il valore `starred`.

   * Per attivare la funzionalità MSM, aggiungere i seguenti parametri MSM alla proprietà multi-stringa **storeReaderFields**:

      * **msm:isSource**
      * **msm:isInBlueprint**
      * **msm:isLiveCopy**

1. Aggiungete un nodo `starred` (di tipo **nt:unstructure**) sotto `/apps/wcm/core/content/siteadmin/grid/geometrixx/columns` con le seguenti proprietà:

   * **dataIndex**:  `starred` di tipo String

   * **intestazione**:  `Starred` di tipo String

   * **xtype**:  `gridcolumn` di tipo String

1. (facoltativo) Rilasciare le colonne che non si desidera visualizzare in `/apps/wcm/core/content/siteadmin/grid/geometrixx/columns`

1. `/siteadmin` è un percorso personalizzato che, come impostazione predefinita, punta a  `/libs/wcm/core/content/siteadmin`.
Per reindirizzare l&#39;utente alla versione dell&#39;amministratore del sito in `/apps/wcm/core/content/siteadmin`, definire la proprietà `sling:vanityOrder` in modo che abbia un valore superiore a quello definito in `/libs/wcm/core/content/siteadmin`. Il valore predefinito è 300, quindi è adatto qualsiasi valore superiore.

1. Passate alla console di amministrazione dei siti Web e individuate il sito di Geometrixx:
   [https://localhost:4502/siteadmin#/content/geometrixx](https://localhost:4502/siteadmin#/content/geometrixx).

1. È disponibile la nuova colonna denominata **Starred**, con le seguenti informazioni personalizzate:

![screen_shot_2012-02-14at104602](assets/screen_shot_2012-02-14at104602.png)

>[!CAUTION]
>
>Se più configurazioni della griglia corrispondono al percorso richiesto definito dalla proprietà **pathRegex**, verrà utilizzato il primo, e non il percorso più specifico, il che significa che l&#39;ordine delle configurazioni è importante.

### Pacchetto di esempio {#sample-package}

Il risultato di questa esercitazione è disponibile nel pacchetto [Customizing the Websites Administration Console](https://localhost:4502/crx/packageshare/index.html/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/helper/customizing-siteadmin) on Package Share (Personalizzazione della console di amministrazione dei siti Web).
