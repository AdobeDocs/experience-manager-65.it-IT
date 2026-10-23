---
title: Creare un indice personalizzato per i riferimenti dei moduli adattivi
description: Scopri come creare un indice Lucene con tag per le query di riferimento per moduli adattivi in AEM Forms per evitare query trasversali durante la pubblicazione dei frammenti di esperienza.
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: Admin, Developer
source-git-commit: 9240de61985dc32f17593f416e5d054cadb8a392
workflow-type: tm+mt
source-wordcount: '668'
ht-degree: 1%
---

# Creare un indice personalizzato per i riferimenti ai moduli adattivi {#create-custom-index-for-adaptive-forms-references}

Crea un indice Lucene con tag per evitare query trasversali quando Adobe Experience Manager (AEM) Forms risolve i riferimenti ai moduli adattivi. Senza un indice appropriato, la pubblicazione di un frammento di esperienza contenente un riferimento a un modulo adattivo può produrre un avviso `Traversal query (query without index)` nei registri.

In AEM Forms 6.5.24.0 e versioni successive, la query di riferimento utilizza il tag di indice `aemformsAFReferences`. Queste versioni includono la modifica della query, ma è necessario creare un indice personalizzato con tale tag. Questo articolo mostra come definire e distribuire l’indice.

Per AEM Forms 6.5 LTS, consulta [Creare un indice personalizzato per i riferimenti ai moduli adattivi in AEM Forms 6.5 LTS](https://experienceleague.adobe.com/en/docs/experience-manager-65-lts/content/forms/install-aem-forms/configure-aem-forms/create-custom-index-for-adaptive-forms-references).

## Prerequisiti {#prerequisites}

Prima di iniziare, assicurati di avere:

* AEM Forms 6.5.24.0 o versione successiva, con il componente aggiuntivo Forms corrispondente installato.
* Accesso per creare un indice in `/oak:index` nell&#39;istanza di authoring.
* Un progetto AEM con un modulo `ui.apps` se distribuisci l&#39;indice tramite un pacchetto di contenuti o accedi a CRXDE Lite per l&#39;alternativa di sviluppo.

Verifica l’indice in un ambiente di sviluppo o di staging prima di distribuirlo in produzione. [La creazione di un indice può richiedere tempo in un repository di grandi dimensioni](/help/sites-deploying/queries-and-indexing.md#configuring-the-indexes).

## Definire l’indice personalizzato {#define-the-custom-index}

Creare l&#39;indice in `/oak:index/customAFReferenceLuceneIndex-1`. È possibile scegliere un nome di nodo di indice diverso, ma mantenere il tag `aemformsAFReferences` invariato in modo che la query di riferimento Forms possa selezionare l&#39;indice.

Utilizza la seguente definizione. Indica `sling:resourceType` nei nodi `nt:unstructured` in `/content`.

```json
{
  "jcr:primaryType": "oak:QueryIndexDefinition",
  "selectionPolicy": "tag",
  "compatVersion": 2,
  "includedPaths": ["/content"],
  "queryPaths": ["/content"],
  "tags": ["aemformsAFReferences"],
  "type": "lucene",
  "async": ["async"],
  "evaluatePathRestrictions": true,
  "reindex": false,
  "indexRules": {
    "jcr:primaryType": "nt:unstructured",
    "nt:unstructured": {
      "jcr:primaryType": "nt:unstructured",
      "properties": {
        "jcr:primaryType": "nt:unstructured",
        "resourceType": {
          "jcr:primaryType": "nt:unstructured",
          "propertyIndex": true,
          "name": "sling:resourceType"
        }
      }
    }
  }
}
```

Non aggiungere `analyzed=true`. La query di riferimento utilizza restrizioni di proprietà anziché una condizione `contains` full-text, pertanto l&#39;impostazione non è necessaria.

## Distribuire l’indice con un pacchetto di contenuti {#deploy-the-index-with-a-content-package}

Utilizza un pacchetto di contenuti per le distribuzioni di produzione.

1. Nel modulo `ui.apps` del progetto AEM, crea `ui.apps/src/main/content/jcr_root/_oak_index/customAFReferenceLuceneIndex-1/`.
1. Crea `.content.xml` nella directory con la seguente definizione:

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:oak="http://jackrabbit.apache.org/oak/ns/1.0"
             xmlns:jcr="http://www.jcp.org/jcr/1.0"
             xmlns:nt="http://www.jcp.org/jcr/nt/1.0"
             jcr:primaryType="oak:QueryIndexDefinition"
             async="[async]"
             compatVersion="{Long}2"
             evaluatePathRestrictions="{Boolean}true"
             includedPaths="[/content]"
             queryPaths="[/content]"
             reindex="{Boolean}false"
             selectionPolicy="tag"
             tags="[aemformsAFReferences]"
             type="lucene">
       <indexRules jcr:primaryType="nt:unstructured">
           <nt:unstructured jcr:primaryType="nt:unstructured">
               <properties jcr:primaryType="nt:unstructured">
                   <resourceType jcr:primaryType="nt:unstructured"
                                 name="sling:resourceType"
                                 propertyIndex="{Boolean}true"/>
               </properties>
           </nt:unstructured>
       </indexRules>
   </jcr:root>
   ```

1. Aggiungere il seguente filtro all&#39;interno dell&#39;elemento `workspaceFilter` esistente in `ui.apps/src/main/content/META-INF/vault/filter.xml`. Mantenere invariati gli altri filtri del progetto.

   ```xml
   <filter root="/oak:index/customAFReferenceLuceneIndex-1"/>
   ```

1. Crea il progetto utilizzando la configurazione di build esistente e installa il pacchetto di contenuti risultante sull’istanza di authoring. Per le istruzioni di caricamento e installazione del pacchetto, vedere [Gestione pacchetti](/help/sites-administering/package-manager.md#uploading-packages-from-your-file-system).
1. Verificare che `/oak:index/customAFReferenceLuceneIndex-1` esista. Consenti il completamento dell&#39;indicizzazione asincrona prima di controllare il piano di query.

Se hai scelto un nome di indice diverso, utilizza tale nome in modo coerente nella directory, nel filtro e nel percorso dell’archivio.

## Creare l’indice con CRXDE Lite {#create-the-index-with-crxde-lite}

Utilizza questa alternativa in un ambiente di sviluppo invece del metodo del pacchetto di contenuti.

Utilizza le seguenti proprietà quando crei il nodo di indice:

| Proprietà | Tipo | Valore |
| --- | --- | --- |
| `selectionPolicy` | Stringa | `tag` |
| `compatVersion` | Lungo | `2` |
| `includedPaths` | `String[]` | `/content` |
| `queryPaths` | `String[]` | `/content` |
| `tags` | `String[]` | `aemformsAFReferences` |
| `type` | Stringa | `lucene` |
| `async` | `String[]` | `async` |
| `evaluatePathRestrictions` | Booleano | `true` |
| `reindex` | Booleano | `false` |

`String[]` indica una proprietà String con più valori, anche se contiene un solo valore.

1. Apri `http://localhost:4502/crx/de/index.jsp`. Sostituisci l’host e la porta con quelli dell’istanza di authoring.
1. Accedi a `/oak:index`. Fare clic con il pulsante destro del mouse sul nodo e selezionare [!UICONTROL Crea] > [!UICONTROL Crea nodo].
1. Crea `customAFReferenceLuceneIndex-1` con tipo `oak:QueryIndexDefinition`.
1. Aggiungi le proprietà dalla tabella precedente al nodo dell’indice.
1. Nel nodo indice, crea la seguente gerarchia di nodi figlio. Imposta il tipo di ogni nodo figlio su `nt:unstructured`:

   ```text
   indexRules
       nt:unstructured
           properties
               resourceType
   ```

1. In `resourceType`, aggiungere `name` (stringa) con valore `sling:resourceType` e `propertyIndex` (booleano) con valore `true`.
1. Seleziona [!UICONTROL Salva tutto] e consenti il completamento dell&#39;indicizzazione asincrona.

## Verificare che la query utilizzi l&#39;indice {#verify-that-the-query-uses-the-index}

Controllare il piano di query per verificare che la query di riferimento selezioni l&#39;indice personalizzato.

1. Verificare che l&#39;indicizzazione asincrona sia stata completata. Utilizza [Gestione indici](/help/sites-administering/operations-dashboard.md#the-index-manager) per controllare lo stato dell&#39;indice.
1. Apri [!UICONTROL Strumenti] > [!UICONTROL Operazioni] > [!UICONTROL Diagnosi] > [!UICONTROL Prestazioni query] e seleziona [!UICONTROL Spiega query]. Selezionare la lingua di query XPath e immettere:

   ```text
   /jcr:root/content//element(*, nt:unstructured)[
     (@sling:resourceType = 'fd/af/components/aemform'
     or jcr:like(@sling:resourceType, '%components/aemformscontainer%')
     or jcr:like(@sling:resourceType, '%components/adaptiveForm/fragment%'))]
   option (index tag aemformsAFReferences)
   ```

1. Selezionare [!UICONTROL Spiega]. Verificare che il piano utilizzi `lucene:customAFReferenceLuceneIndex-1` e `/oak:index/customAFReferenceLuceneIndex-1` o il nome di indice scelto per i rami della query anziché un piano di attraversamento. Per ulteriori dettagli, vedere [Spiega query](/help/sites-administering/operations-dashboard.md#explain-query).
1. Ripeti l’operazione di pubblicazione del frammento di esperienza che ha generato l’avviso. Verificare la presenza di nuovi avvisi di attraversamento da `com.adobe.aem.formsndocuments.publish.AssetReferenceProvider.resolvePathsToFindReferences` in `error.log`.

Se il piano non seleziona l&#39;indice personalizzato, controllare il tag, la gerarchia `indexRules` e la definizione della proprietà `sling:resourceType` rispetto agli esempi precedenti. Per ulteriori diagnosi, vedere [Risoluzione dei problemi relativi agli indici Oak](/help/sites-deploying/troubleshooting-oak-indexes.md).

## Attività correlate {#related-tasks}

Per ulteriori informazioni sulle prestazioni delle query e sulla configurazione degli indici, consulta:

* [Query e indicizzazione Oak](/help/sites-deploying/queries-and-indexing.md)
* [Best practice per query e indicizzazione](/help/sites-deploying/best-practices-for-queries-and-indexing.md)
* [Risoluzione dei problemi relativi a query lente](/help/sites-developing/troubleshooting-slow-queries.md)
