---
title: Implementazione di un valutatore del predicato personalizzato per Query Builder
description: Query Builder offre un modo semplice per eseguire query sull’archivio dei contenuti
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
docset: aem65
exl-id: 72cbe589-14a1-40f5-a7cb-8960f02e0ebb
solution: Experience Manager, Experience Manager Sites
feature: Developing,Search,Query Builder
role: Developer
source-git-commit: 305227eff3c0d6414a5ae74bcf3a74309dccdd13
workflow-type: tm+mt
source-wordcount: '664'
ht-degree: 0%

---

# Implementazione di un valutatore del predicato personalizzato per Query Builder{#implementing-a-custom-predicate-evaluator-for-the-query-builder}

Questa sezione descrive come estendere [Query Builder](/help/sites-developing/querybuilder-api.md) implementando un valutatore di predicati personalizzato.

## Panoramica {#overview}

[Query Builder](/help/sites-developing/querybuilder-api.md) offre un modo semplice per eseguire query nell&#39;archivio dei contenuti. CQ viene fornito con un set di valutatori di predicati che consente di gestire i dati.

Tuttavia, potrebbe essere utile semplificare le query implementando un valutatore di predicati personalizzato che nasconda una certa complessità e garantisca una semantica migliore.

Un predicato personalizzato potrebbe inoltre eseguire altre operazioni non direttamente possibili con XPath, ad esempio:

* ricerca di alcuni dati da un servizio
* filtro personalizzato basato su calcolo

>[!NOTE]
>
>Quando si implementa un predicato personalizzato, è necessario considerare i problemi di prestazioni.

>[!NOTE]
>
>Puoi trovare esempi di query nella sezione [Generatore di query](/help/sites-developing/querybuilder-api.md).

CODICE SU GITHUB

Puoi trovare il codice di questa pagina su GitHub.

* [Apri progetto aem-search-custom-predicate-valutator su GitHub](https://github.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator)
* Scarica il progetto come [file ZIP](https://github.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator/archive/master.zip)

### Predicate Evaluator in Detail {#predicate-evaluator-in-detail}

Un valutatore di predicati gestisce la valutazione di alcuni predicati, che sono i vincoli di definizione di una query.

Mappa un vincolo di ricerca di livello superiore (ad esempio &quot;larghezza > 200&quot;) a una query JCR specifica che si adatta al modello di contenuto effettivo (ad esempio, metadati/@width > 200). Oppure può filtrare manualmente i nodi e controllarne i vincoli.

>[!NOTE]
>
>Per ulteriori informazioni sul pacchetto `PredicateEvaluator` e `com.day.cq.search`, vedere la [documentazione Java™](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/index.html?com/day/cq/search/package-summary.html).

### Implementazione di un valutatore del predicato personalizzato per i metadati di replica {#implementing-a-custom-predicate-evaluator-for-replication-metadata}

Ad esempio, questa sezione descrive come creare un valutatore di predicati personalizzato che aiuti i dati basati sui metadati di replica:

* `cq:lastReplicated` che memorizza la data dell&#39;ultima azione di replica

* `cq:lastReplicatedBy` che memorizza l&#39;ID dell&#39;utente che ha attivato l&#39;ultima azione di replica

* `cq:lastReplicationAction` che memorizza l&#39;ultima azione di replica (ad esempio Attivazione, Disattivazione)

#### Query dei metadati di replica con i valutatori del predicato predefiniti {#querying-replication-metadata-with-default-predicate-evaluators}

La query seguente recupera l&#39;elenco dei nodi nel ramo `/content` attivati da `admin` dall&#39;inizio dell&#39;anno.

```xml
path=/content

1_property=cq:lastReplicatedBy
1_property.value=admin

2_property=cq:lastReplicationAction
2_property.value=Activate

daterange.property=cq:lastReplicated
daterange.lowerBound=2013-01-01T00:00:00.000+01:00
daterange.lowerOperation=>=
```

Questa query è valida ma di difficile lettura e non evidenzia la relazione tra le tre proprietà di replica. L’implementazione di un valutatore di predicati personalizzato riduce la complessità e migliora la semantica di questa query.

#### Obiettivi {#objectives}

L&#39;obiettivo di `ReplicationPredicateEvaluator` è quello di supportare la query precedente utilizzando la sintassi seguente.

```xml
path=/content

replic.by=admin
replic.since=2013-01-01T00:00:00.000+01:00
replic.action=Activate
```

Il raggruppamento dei predicati di replica con un valutatore di predicati personalizzato consente di creare una query significativa.

#### Aggiornamento delle dipendenze Maven {#updating-maven-dependencies}

>[!NOTE]
>
>La configurazione di nuovi progetti Adobe Experience Manager (AEM) tramite Maven è documentata da [Come creare progetti AEM utilizzando Apache Maven](/help/sites-developing/ht-projects-maven.md).

Innanzitutto, aggiorna le dipendenze Maven del progetto. `PredicateEvaluator` fa parte dell&#39;artefatto `cq-search`, pertanto deve essere aggiunto al file pom.xml Maven.

>[!NOTE]
>
>L&#39;ambito della dipendenza `cq-search` è impostato su `provided` perché `cq-search` è fornito dal contenitore `OSGi`.

pom.xml

Il frammento seguente mostra le differenze nel formato diff [unificato](https://en.wikipedia.org/wiki/Diff#Unified_format)

```
@@ -120,6 +120,12 @@
             <scope>provided</scope>
         <dependency>
+            <groupid>com.day.cq</groupid>
+            <artifactid>cq-search</artifactid>
+            <version>5.6.4</version>
+            <scope>provided</scope>
+        </dependency>
+        <dependency>
             <groupid>junit</groupid>
             <artifactid>junit</artifactid>
             <version>3.8.1</version></dependency>
```

[aem-search-custom-predicate-valuator](https://github.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator) - [pom.xml](https://raw.githubusercontent.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator/7aed6b35b4c8dd3655296e1b10cf40c0dd1eaa61/pom.xml)

#### Scrittura di ReplicationPredicateEvaluator {#writing-the-replicationpredicateevaluator}

Il progetto `cq-search` contiene la classe astratta `AbstractPredicateEvaluator`. Questa estensione può essere estesa con alcuni passaggi per implementare il proprio valutatore di predicati personalizzato `(PredicateEvaluator`).

>[!NOTE]
>
>Nella procedura seguente viene illustrato come generare un&#39;espressione `Xpath` per filtrare i dati. Un&#39;altra opzione consiste nell&#39;implementare il metodo `includes` che seleziona i dati in base alla riga. Per ulteriori informazioni, consulta la [documentazione Java™](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/search/eval/PredicateEvaluator.html#includes28comdaycqsearchpredicatejavaxjcrqueryrowcomdaycqsearchevalevaluationcontext29).

1. Crea una classe Java™ che estende `com.day.cq.search.eval.AbstractPredicateEvaluator`
1. Annota la classe con `@Component` come segue

   src/main/java/com/adobe/aem/docs/search/ReplicationPredicateEvaluator.java

   Il frammento seguente mostra le differenze nel formato diff [unificato](https://en.wikipedia.org/wiki/Diff#Unified_format)

```
@@ -19,8 +19,11 @@
  */
 package com.adobe.aem.docs.search;

+import org.apache.felix.scr.annotations.Component;
+
 import com.day.cq.search.eval.AbstractPredicateEvaluator;

+@Component(metatype = false, factory = "com.day.cq.search.eval.PredicateEvaluator/repli")
 public class ReplicationPredicateEvaluator extends AbstractPredicateEvaluator {

 }
```

[aem-search-custom-predicate-valuator](https://github.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator) - [src/main/java/com/adobe/aem/docs/search/ReplicationPredicateEvaluator.java](https://raw.githubusercontent.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator/ec70fac35fbd0d132e00c6066a204804e9cbe70f/src/main/java/com/adobe/aem/docs/search/ReplicationPredicateEvaluator.java)

>[!NOTE]
>
>`factory` deve essere una stringa univoca che inizia con `com.day.cq.search.eval.PredicateEvaluator/` e termina con il nome del `PredicateEvaluator` personalizzato.

>[!NOTE]
>
>Il nome di `PredicateEvaluator` è il nome del predicato utilizzato per la creazione delle query.

1. Sostituisci:

   ```java
   public String getXPathExpression(Predicate predicate, EvaluationContext context)
   ```

   Nel metodo override viene generata un&#39;espressione `Xpath` basata su `Predicate` specificata nell&#39;argomento.

### Esempio di un valutatore del predicato personalizzato per i metadati di replica {#example-of-a-custom-predicate-evalutor-for-replication-metadata}

L&#39;implementazione completa di `PredicateEvaluator` potrebbe essere simile alla classe seguente.

src/main/java/com/adobe/aem/docs/search/ReplicationPredicateEvaluator.java

```
/*
 * #%L
 * aem-docs-custom-predicate-evaluator
 * %%
 * Copyright (C) 2013 Adobe Research
 * %%
 * Licensed under the Apache License, Version 2.0 (the "License");
 * you may not use this file except in compliance with the License.
 * You may obtain a copy of the License at
 *
 *      https://www.apache.org/licenses/LICENSE-2.0
 *
 * Unless required by applicable law or agreed to in writing, software
 * distributed under the License is distributed on an "AS IS" BASIS,
 * WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
 * See the License for the specific language governing permissions and
 * limitations under the License.
 * #L%
 */

package com.adobe.aem.docs.search;

import org.apache.felix.scr.annotations.Component;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import com.day.cq.search.Predicate;
import com.day.cq.search.eval.AbstractPredicateEvaluator;
import com.day.cq.search.eval.EvaluationContext;

@Component(metatype = false, factory = "com.day.cq.search.eval.PredicateEvaluator/repli")

public class ReplicationPredicateEvaluator extends AbstractPredicateEvaluator {

    static final String PE_NAME = "replic";


    static final String PN_LAST_REPLICATED_BY = "cq:lastReplicatedBy";
    static final String PN_LAST_REPLICATED = "cq:lastReplicated";
    static final String PN_LAST_REPLICATED_ACTION = "cq:lastReplicationAction";

    static final String PREDICATE_BY = "by";
    static final String PREDICATE_SINCE = "since";
    static final String PREDICATE_SINCE_OP = " >= ";
    static final String PREDICATE_ACTION = "action";

    Logger log = LoggerFactory.getLogger(getClass());

    /**
     * Returns a XPath expression filtering by replication metadata.
     *
     * @see com.day.cq.search.eval.AbstractPredicateEvaluator#getXPathExpression(com.day.cq.search.Predicate,
     *      com.day.cq.search.eval.EvaluationContext)
     */

    @Override

    public String getXPathExpression(Predicate predicate,
            EvaluationContext context) {

        log.debug("predicate {}", predicate);

        String date = predicate.get(PREDICATE_SINCE);
        String user = predicate.get(PREDICATE_BY);
        String action = predicate.get(PREDICATE_ACTION);

        StringBuilder sb = new StringBuilder();

        if (date != null) {

            sb.append(PN_LAST_REPLICATED).append(PREDICATE_SINCE_OP);
            sb.append("xs:dateTime('").append(date).append("')");

        }

        if (user != null) {

            addAndOperator(sb);
            sb.append(PN_LAST_REPLICATED_BY);
            sb.append("='").append(user).append("'");

        }

        if (action != null) {

            addAndOperator(sb);
            sb.append(PN_LAST_REPLICATED_ACTION);
            sb.append("='").append(action).append("'");

        }

        String xpath = sb.toString();

        log.debug("xpath **{}**", xpath);

        return xpath;

    }

    /**
     * Add an and operator if the builder is not empty.
     *
     * @param sb a {@link StringBuilder} containing the query under construction
     */

    private void addAndOperator(StringBuilder sb) {

        if (sb.length() != 0) {

            sb.append(" and ");

        }

    }

}
```

[aem-search-custom-predicate-valuator](https://github.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator) - [src/main/java/com/adobe/aem/docs/search/ReplicationPredicateEvaluator.java](https://github.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator/blob/master/src/main/java/com/adobe/aem/docs/search/ReplicationPredicateEvaluator.java)
