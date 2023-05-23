---
title: Personalizzazione della console Siti web (interfaccia classica)
seo-title: Customizing the Websites Console (Classic UI)
description: La console di amministrazione dei siti Web può essere estesa per visualizzare colonne personalizzate
seo-description: The Websites Administration console can be extended to display custom columns
uuid: 9163fdff-5351-477d-b91c-8a74f8b41d34
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: aeb37103-541d-4235-8a78-980b78c8de66
docset: aem65
exl-id: 2b9b4857-821c-4f2f-9ed9-78a1c9f5ac67
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '781'
ht-degree: 0%

---

# Personalizzazione della console Siti web (interfaccia classica){#customizing-the-websites-console-classic-ui}

## Aggiunta di una colonna personalizzata alla console Siti Web (siteadmin) {#adding-a-custom-column-to-the-websites-siteadmin-console}

La console di amministrazione dei siti Web può essere estesa per visualizzare colonne personalizzate. La console è basata su un oggetto JSON che può essere esteso creando un servizio OSGI che implementa `ListInfoProvider` di rete. Tale servizio modifica l’oggetto JSON inviato al client per generare la console.

Questo tutorial dettagliato spiega come visualizzare una nuova colonna nella console di amministrazione dei siti web implementando `ListInfoProvider` di rete. È costituito dai seguenti passaggi:

1. [Creazione del servizio OSGI](#creating-the-osgi-service) e distribuire il bundle che lo contiene sul server AEM.
1. (facoltativo) [Test del nuovo servizio](#testing-the-new-service) eseguendo una chiamata JSON per richiedere l’oggetto JSON utilizzato per generare la console.
1. [Visualizzazione della nuova colonna](#displaying-the-new-column) estendendo la struttura dei nodi della console nell’archivio.

>[!NOTE]
>
>Questo tutorial può essere utilizzato anche per estendere le seguenti console di amministrazione:
>
>* la console Risorse digitali
>* la console Community
>


### Creazione del servizio OSGI {#creating-the-osgi-service}

Il `ListInfoProvider` L&#39;interfaccia definisce due metodi:

* `updateListGlobalInfo`, per aggiornare le proprietà globali dell&#39;elenco,
* `updateListItemInfo`, per aggiornare una singola voce di elenco.

Gli argomenti per entrambi i metodi sono:

* `request`, l’oggetto di richiesta HTTP Sling associato,
* `info`, l’oggetto JSON da aggiornare, che è rispettivamente l’elenco globale o la voce di elenco corrente,
* `resource`, una risorsa Sling.

Di seguito è riportato un esempio di implementazione:

* Aggiunge un *protagonista* per ogni elemento, che è `true` se il nome della pagina inizia con *e*, e `false` altrimenti.

* Aggiunge un *starredCount* , che è globale per l&#39;elenco e contiene il numero di voci dell&#39;elenco visualizzate.

Per creare il servizio OSGI:

1. In CRXDE Lite, [creare un bundle](/help/sites-developing/developing-with-crxde-lite.md#managing-a-bundle).
1. Aggiungi il codice di esempio seguente.
1. Crea il bundle.

Il nuovo servizio è operativo.

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
>* L’implementazione deve decidere, in base alla richiesta e/o alla risorsa fornite, se aggiungere o meno le informazioni all’oggetto JSON.
>* Se il `ListInfoProvider` L’implementazione definisce una proprietà già esistente nell’oggetto di risposta. Il relativo valore verrà sovrascritto da quello fornito.
>
>  È possibile utilizzare [classificazione dei servizi](https://www.osgi.org/javadoc/r2/org/osgi/framework/Constants.html#SERVICE_RANKING) per gestire l&#39;ordine di esecuzione di più `ListInfoProvider` implementazioni.

### Test del nuovo servizio {#testing-the-new-service}

Quando apri la console di amministrazione dei siti web e esplori il sito, il browser effettua una chiamata AJAX per ottenere l’oggetto JSON utilizzato per creare la console. Ad esempio, quando si passa al `/content/geometrixx` cartella, la seguente richiesta viene inviata al server AEM per creare la console:

[https://localhost:4502/content/geometrixx.pages.json?start=0&amp;limit=30&amp;predicate=siteadmin](https://localhost:4502/content/geometrixx.pages.json?start=0&amp;limit=30&amp;predicate=siteadmin)

Per assicurarti che il nuovo servizio sia in esecuzione dopo aver distribuito il bundle che lo contiene:

1. Puntare il browser al seguente URL:
   [https://localhost:4502/content/geometrixx.pages.json?start=0&amp;limit=30&amp;predicate=siteadmin](https://localhost:4502/content/geometrixx.pages.json?start=0&amp;limit=30&amp;predicate=siteadmin)

1. La risposta deve visualizzare le nuove proprietà come segue:

![screen_shot_2012-02-13at163046](assets/screen_shot_2012-02-13at163046.png)

### Visualizzazione della nuova colonna {#displaying-the-new-column}

Geometrixx L’ultimo passaggio consiste nell’adattare la struttura dei nodi della console di amministrazione dei siti web per visualizzare la nuova proprietà per tutte le pagine sovrapponendola `/libs/wcm/core/content/siteadmin`. Procedere come segue:

1. In CRXDE Lite, crea la struttura dei nodi `/apps/wcm/core/content` con nodi di tipo `sling:Folder` per riflettere la struttura `/libs/wcm/core/content`.

1. Copiare il nodo `/libs/wcm/core/content/siteadmin` e incollalo sotto `/apps/wcm/core/content`.

1. Copiare il nodo `/apps/wcm/core/content/siteadmin/grid/assets` a `/apps/wcm/core/content/siteadmin/grid/geometrixx` e ne modifica le proprietà:

   * Rimuovi **pageText**

   * Imposta **pathRegex** a `/content/geometrixx(/.*)?`
In questo modo la configurazione della griglia sarà attiva per tutti i siti web geometrixx.

   * Imposta **storeProxySuffix** a `.pages.json`

   * Modifica il **storeReaderFields** proprietà multivalore e aggiungi `starred` valore.

   * Per attivare la funzionalità MSM, aggiungi i seguenti parametri MSM alla proprietà multi-String **storeReaderFields**:

      * **msm:isSource**
      * **msm:isInBlueprint**
      * **msm:isLiveCopy**

1. Aggiungi un `starred` nodo (di tipo **nt:unstructured**) sotto `/apps/wcm/core/content/siteadmin/grid/geometrixx/columns` con le seguenti proprietà:

   * **dataIndex**: `starred` di tipo String

   * **intestazione**: `Starred` di tipo String

   * **xtype**: `gridcolumn` di tipo String

1. (facoltativo) Rilascia le colonne che non desideri visualizzare in corrispondenza di `/apps/wcm/core/content/siteadmin/grid/geometrixx/columns`

1. `/siteadmin` è un percorso personalizzato che, per impostazione predefinita, punta a `/libs/wcm/core/content/siteadmin`.
Per reindirizzarlo alla tua versione di siteadmin su `/apps/wcm/core/content/siteadmin` definire la proprietà `sling:vanityOrder` per avere un valore superiore a quello definito il `/libs/wcm/core/content/siteadmin`. Il valore predefinito è 300, quindi qualsiasi valore più alto è adatto.

1. Passa alla console di amministrazione dei siti Web e passa al Geometrixx:
   [https://localhost:4502/siteadmin#/content/geometrixx](https://localhost:4502/siteadmin#/content/geometrixx).

1. La nuova colonna denominata **Stellato** è disponibile, visualizzando le informazioni personalizzate nel modo seguente:

![screen_shot_2012-02-14at104602](assets/screen_shot_2012-02-14at104602.png)

>[!CAUTION]
>
>Se più configurazioni della griglia corrispondono al percorso richiesto definito da **pathRegex** , verrà utilizzata la prima, e non la più specifica, il che significa che l’ordine delle configurazioni è importante.

### Pacchetto di esempio {#sample-package}

Il risultato di questa esercitazione è disponibile nel [Personalizzazione della console di amministrazione dei siti Web](https://localhost:4502/crx/packageshare/index.html/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/helper/customizing-siteadmin) pacchetto in Condivisione pacchetti.
