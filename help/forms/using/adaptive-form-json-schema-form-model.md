---
title: Come si crea un Forms adattivo utilizzando lo schema JSON?
description: Scopri come creare moduli adattivi utilizzando lo schema JSON come modello di modulo. Puoi utilizzare gli schemi JSON esistenti per creare moduli adattivi. Approfondisci un esempio di schema JSON, preconfigura i campi nella definizione dello schema JSON, limita i valori accettabili per un componente modulo adattivo e scopri i costrutti non supportati.
feature: Adaptive Forms
role: User, Developer
level: Beginner, Intermediate
exl-id: 1b402aef-a319-4d32-8ada-cadc86f5c872
source-git-commit: e7a3558ae04cd6816ed73589c67b0297f05adce2
workflow-type: tm+mt
source-wordcount: '1798'
ht-degree: 5%

---

# Creazione di moduli adattivi tramite lo schema JSON {#creating-adaptive-forms-using-json-schema}

<span class="preview"> L’Adobe consiglia di utilizzare l’acquisizione dati moderna ed estensibile [Componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=it) per [creazione di un nuovo Forms adattivo](/help/forms/using/create-an-adaptive-form-core-components.md) o [aggiunta di Forms adattivo alle pagine AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Questi componenti rappresentano un progresso significativo nella creazione di Forms adattivi, garantendo esperienze utente straordinarie. Questo articolo descrive un approccio precedente all’authoring di Forms adattivi utilizzando i componenti di base. </span>

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/create-an-adaptive-form-on-forms-cs/adaptive-form-json-schema-form-model.html) |
| AEM 6.5 | Questo articolo |


## Prerequisiti {#prerequisites}

Per creare un modulo adattivo utilizzando uno schema JSON come modello di modulo è necessario conoscere a fondo lo schema JSON. Si consiglia di leggere attentamente il seguente contenuto prima di questo articolo.

* [Creazione di un modulo adattivo](creating-adaptive-form.md)
* [Schema JSON](https://json-schema.org/)

## Utilizzo di uno schema JSON come modello di modulo  {#using-a-json-schema-as-form-model}

[!DNL Adobe Experience Manager Forms] supporta la creazione di un modulo adattivo utilizzando uno schema JSON esistente come modello di modulo. Questo schema JSON rappresenta la struttura in cui i dati vengono prodotti o utilizzati dal sistema back-end dell’organizzazione. Lo schema JSON utilizzato deve essere conforme a [specifiche v4](https://json-schema.org/draft-04/schema).

Le funzioni chiave dell’utilizzo di uno schema JSON sono:

* La struttura del JSON viene visualizzata come una struttura nella scheda Content Finder nella modalità di authoring di un modulo adattivo. Puoi trascinare e aggiungere un elemento dalla gerarchia JSON al modulo adattivo.
* Puoi precompilare il modulo utilizzando un JSON conforme allo schema associato.
* All’invio, i dati immessi dall’utente vengono inviati come JSON, in linea con lo schema associato.

Uno schema JSON è costituito da tipi di elementi semplici e complessi. Gli elementi dispongono di attributi che aggiungono regole all’elemento. Quando questi elementi e attributi vengono trascinati in un modulo adattivo, vengono mappati automaticamente al corrispondente componente del modulo adattivo.

La mappatura degli elementi JSON con i componenti dei moduli adattivi è la seguente:

```json
"birthDate": {
              "type": "string",
              "format": "date",
              "pattern": "date{DD MMMM, YYYY}",
              "aem:affKeyword": [
                "DOB",
                "Date of Birth"
              ],
              "description": "Date of birth in DD MMMM, YYYY",
              "aem:afProperties": {
                "displayPictureClause": "date{DD MMMM, YYYY}",
                "displayPatternType": "date{DD MMMM, YYYY}",
                "validationPatternType": "date{DD MMMM, YYYY}",
                "validatePictureClause": "date{DD MMMM, YYYY}",
                "validatePictureClauseMessage": "Date must be in DD MMMM, YYYY format."
              }
```

<table>
 <tbody>
  <tr>
   <th><strong>Elemento JSON, proprietà o attributi</strong></th>
   <th><strong>Componente modulo adattivo</strong></th>
  </tr>
  <tr>
   <td><p>Proprietà stringa con vincolo enum ed enumNames.</p> <p>Sintassi,</p> <p> <code>{</code></p> <p><code>"type" : "string",</code></p> <p><code>"enum" : ["M", "F"]</code></p> <p><code>"enumNames" : ["Male", "Female"]</code></p> <p><code>}</code></p> <p> </p> </td>
   <td><p>Componente a discesa:</p>
    <ul>
     <li>I valori elencati in enumNames vengono visualizzati nella casella di riepilogo.</li>
     <li>I valori elencati nell'enum vengono utilizzati per il calcolo.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Proprietà stringa con vincolo di formato. Ad esempio e-mail e data.</p> <p>Sintassi,</p> <p><code>{</code></p> <p><code>"type" : "string",</code></p> <p><code>"format" : "email"</code></p> <p><code>}</code></p> <p> </p> </td>
   <td>
    <ul>
     <li>Il componente E-mail viene mappato quando il tipo è stringa e il formato è e-mail.</li>
     <li>Il componente Textbox con convalida viene mappato quando il tipo è string (stringa) e il formato è hostname (nome host).</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>{</code></p> <p><code>"type" : "string",</code></p> <p><code>}</code></p> </td>
   <td><br /> <br /> Campo di testo<br /> <br /> <br /> </td>
  </tr>
  <tr>
   <td>proprietà number<br /> </td>
   <td>Campo numerico con sottotipo impostato su float<br /> </td>
  </tr>
  <tr>
   <td>proprietà integer<br /> </td>
   <td>Campo numerico con sottotipo impostato su integer<br /> </td>
  </tr>
  <tr>
   <td>proprietà booleana<br /> </td>
   <td>Interruttore<br /> </td>
  </tr>
  <tr>
   <td>proprietà oggetto<br /> </td>
   <td>Pannello<br /> </td>
  </tr>
  <tr>
   <td>proprietà array</td>
   <td>Pannello ripetibile con min e max uguali rispettivamente a minItems e maxItems. Sono supportati solo array omogenei. Pertanto, il vincolo items deve essere un oggetto e non un array.<br /> </td>
  </tr>
 </tbody>
</table>

### Proprietà comuni dello schema {#common-schema-properties}

Il modulo adattivo utilizza le informazioni disponibili nello schema JSON per mappare ogni campo generato. In particolare:

* Il `title` funge da etichetta per i componenti del modulo adattivo.
* Il `description` viene impostata come descrizione lunga per un componente modulo adattivo.
* Il `default` funge da valore iniziale di un campo modulo adattivo.
* Il `maxLength` la proprietà è impostata come `maxlength` attributo del componente campo di testo.
* Il `minimum`, `maximum`, `exclusiveMinimum`, e `exclusiveMaximum` Le proprietà vengono utilizzate per il componente Casella numerica.
* Per supportare l&#39;intervallo per `DatePicker component` proprietà aggiuntive dello schema JSON `minDate` e `maxDate` vengono fornite.
* Il `minItems` e `maxItems` Le proprietà vengono utilizzate per limitare il numero di elementi/campi che possono essere aggiunti o rimossi da un componente del pannello.
* Il `readOnly` imposta la proprietà `readonly` di un componente modulo adattivo.
* Il `required` La proprietà contrassegna il campo modulo adattivo come obbligatorio, mentre in panel (dove tipo è oggetto), i dati JSON finali inviati hanno campi con valore vuoto corrispondente a tale oggetto.
* Il `pattern` viene impostata come pattern di convalida (espressione regolare) in un modulo adattivo.
* L’estensione del file di schema JSON deve essere mantenuta .schema.json. Ad esempio: &lt;filename>.schema.json.

## Schema JSON di esempio {#sample-json-schema}

Di seguito è riportato un esempio di schema JSON.

```json
{
 "$schema": "https://json-schema.org/draft-04/schema#",
 "definitions": {
  "employee": {
   "type": "object",
   "properties": {
    "userName": {
     "type": "string"
    },
    "dateOfBirth": {
     "type": "string",
     "format": "date"
    },
    "email": {
     "type": "string",
     "format": "email"
    },
    "language": {
     "type": "string"
    },
    "personalDetails": {
     "$ref": "#/definitions/personalDetails"
    },
    "projectDetails": {
     "$ref": "#/definitions/projectDetails"
    }
   },
   "required": [
    "userName",
    "dateOfBirth",
    "language"
   ]
  },
  "personalDetails": {
   "type": "object",
   "properties": {
    "GeneralDetails": {
     "$ref": "#/definitions/GeneralDetails"
    },
    "Family": {
     "$ref": "#/definitions/Family"
    },
    "Income": {
     "$ref": "#/definitions/Income"
    }
   }
  },
  "projectDetails": {
   "type": "array",
   "items": {
    "properties": {
     "name": {
      "type": "string"
     },
     "age": {
      "type": "number"
     },
     "projects": {
      "$ref": "#/definitions/projects"
     }
    }
   },
   "minItems": 1,
   "maxItems": 4
  },
  "projects": {
   "type": "array",
   "items": {
    "properties": {
     "name": {
      "type": "string"
     },
     "age": {
      "type": "number"
     },
     "projectsAdditional": {
      "$ref": "#/definitions/projectsAdditional"
     }
    }
   },
   "minItems": 1,
   "maxItems": 4
  },
  "projectsAdditional": {
   "type": "array",
   "items": {
    "properties": {
     "Additional_name": {
      "type": "string"
     },
     "Additional_areacode": {
      "type": "number"
     }
    }
   },
   "minItems": 1,
   "maxItems": 4
  },
  "GeneralDetails": {
   "type": "object",
   "properties": {
    "age": {
     "type": "number"
    },
    "married": {
     "type": "boolean"
    },
    "phone": {
     "type": "number",
     "aem:afProperties": {
      "sling:resourceType": "/libs/fd/af/components/guidetelephone",
      "guideNodeClass": "guideTelephone"
     }
    },
    "address": {
     "type": "string"
    }
   }
  },
  "Family": {
   "type": "object",
   "properties": {
    "spouse": {
     "$ref": "#/definitions/spouse"
    },
    "kids": {
     "$ref": "#/definitions/kids"
    }
   }
  },
  "Income": {
   "type": "object",
   "properties": {
    "monthly": {
     "type": "number"
    },
    "yearly": {
     "type": "number"
    }
   }
  },
  "spouse": {
   "type": "object",
   "properties": {
    "name": {
     "type": "string"
    },
    "Income": {
     "$ref": "#/definitions/Income"
    }
   }
  },
  "kids": {
   "type": "array",
   "items": {
    "properties": {
     "name": {
      "type": "string"
     },
     "age": {
      "type": "number"
     }
    }
   },
   "minItems": 1,
   "maxItems": 4
  }
 },
 "type": "object",
 "properties": {
  "employee": {
   "$ref": "#/definitions/employee"
  }
 }
}
```

### Definizioni di schema riutilizzabili {#reusable-schema-definitions}

Le chiavi di definizione vengono utilizzate per identificare gli schemi riutilizzabili. Per creare frammenti vengono utilizzate le definizioni di schema riutilizzabili. È simile all&#39;identificazione di tipi complessi in XSD. Di seguito è riportato un esempio di schema JSON con definizioni:

```json
{
  "$schema": "https://json-schema.org/draft-04/schema#",

  "definitions": {
    "address": {
      "type": "object",
      "properties": {
        "street_address": { "type": "string" },
        "city":           { "type": "string" },
        "state":          { "type": "string" }
      },
      "required": ["street_address", "city", "state"]
    }
  },

  "type": "object",

  "properties": {
    "billing_address": { "$ref": "#/definitions/address" },
    "shipping_address": { "$ref": "#/definitions/address" }
  }
}
```

L&#39;esempio precedente definisce un record cliente, in cui ogni cliente ha sia un indirizzo di spedizione che un indirizzo di fatturazione. La struttura di entrambi gli indirizzi è la stessa: gli indirizzi hanno un indirizzo stradale, una città e uno stato, quindi è consigliabile non duplicare gli indirizzi. Inoltre, agevola l’aggiunta e l’eliminazione dei campi per eventuali modifiche future.

## Preconfigurazione dei campi nella definizione dello schema JSON {#pre-configuring-fields-in-json-schema-definition}

È possibile utilizzare **aem:afProperties** per preconfigurare il campo Schema JSON da mappare a un componente modulo adattivo personalizzato. Di seguito è riportato un esempio:

```json
{
    "properties": {
        "sizeInMB": {
            "type": "integer",
            "minimum": 16,
            "maximum": 512,
            "aem:afProperties" : {
                 "sling:resourceType" : "/apps/fd/af/components/guideTextBox",
                 "guideNodeClass" : "guideTextBox"
             }
        }
    },
    "required": [ "sizeInMB" ],
    "additionalProperties": false
}
```

## Configurare script o espressioni per gli oggetti modulo  {#configure-scripts-or-expressions-for-form-objects}

JavaScript è il linguaggio di espressione dei moduli adattivi. Tutte le espressioni sono espressioni JavaScript valide e utilizzano API di modelli di script per moduli adattivi. È possibile preconfigurare gli oggetti modulo in [valutare un’espressione](adaptive-form-expressions.md) in un evento modulo.

Utilizza la proprietà aem:afproperties per preconfigurare espressioni o script di moduli adattivi per i componenti dei moduli adattivi. Ad esempio, quando si attiva l&#39;evento di inizializzazione, il codice seguente imposta il valore del campo telefono e stampa un valore nel registro:

```json
"telephone": {
  "type": "string",
  "pattern": "/\\d{10}/",
  "aem:affKeyword": ["phone", "telephone","mobile phone", "work phone", "home phone", "telephone number", "telephone no", "phone number"],
  "description": "Telephone Number",
  "aem:afProperties" : {
    "sling:resourceType" : "fd/af/components/guidetelephone",
    "guideNodeClass" : "guideTelephone",
    "events": {
      "Initialize" : "this.value = \"1234567890\"; console.log(\"ef:gh\") "
    }
  }
}
```

Devi essere membro di [forms-power-user group](forms-groups-privileges-tasks.md) per configurare script o espressioni per l&#39;oggetto modulo. La tabella seguente elenca tutti gli eventi script supportati per un componente modulo adattivo.

<table>
 <tbody>
  <tr>
   <th><strong></strong>Componente \ Evento</th>
   <th>inizializzare <br /> </th>
   <td>Calcola</td>
   <td>Visibilità</td>
   <td>Convalida</td>
   <td>Abilitato</td>
   <td>Conferma valore</td>
   <td>Clic </td>
   <td>Opzioni</td>
  </tr>
  <tr>
   <td>Campo testo</td>
   <td><img alt="Icona di spunta Sì" src="assets/yes_tick.png" /></td>
   <td><img alt="Icona di spunta Sì" src="assets/yes_tick.png" /></td>
   <td><img alt="Icona di spunta Sì" src="assets/yes_tick.png" /></td>
   <td><img alt="Icona di spunta Sì" src="assets/yes_tick.png" /></td>
   <td><img alt="Icona di spunta Sì" src="assets/yes_tick.png" /></td>
   <td><img alt="Icona di spunta Sì" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Campo numerico</td>
   <td><img alt="Icona di spunta Sì" src="assets/yes_tick.png" /></td>
   <td><img alt="Icona di spunta Sì" src="assets/yes_tick.png" /></td>
   <td><img alt="Icona di spunta Sì" src="assets/yes_tick.png" /></td>
   <td><img alt="Icona di spunta Sì" src="assets/yes_tick.png" /></td>
   <td><img alt="Icona di spunta Sì" src="assets/yes_tick.png" /></td>
   <td><img alt="Icona di spunta Sì" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Stepper numerico</td>
   <td><img alt="Icona di spunta Sì" src="assets/yes_tick.png" /></td>
   <td><img alt="Icona di spunta Sì" src="assets/yes_tick.png" /></td>
   <td><img alt="Icona di spunta Sì" src="assets/yes_tick.png" /></td>
   <td><img alt="Icona di spunta Sì" src="assets/yes_tick.png" /></td>
   <td><img alt="Icona di spunta Sì" src="assets/yes_tick.png" /></td>
   <td><img alt="Icona di spunta Sì" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Pulsante di scelta</td>
   <td><img alt="Icona di spunta Sì" src="assets/yes_tick.png" /></td>
   <td><img alt="Icona di spunta Sì" src="assets/yes_tick.png" /></td>
   <td><img alt="Icona di spunta Sì" src="assets/yes_tick.png" /></td>
   <td><img alt="Icona di spunta Sì" src="assets/yes_tick.png" /></td>
   <td><img alt="Icona di spunta Sì" src="assets/yes_tick.png" /></td>
   <td><img alt="Icona di spunta Sì" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Telefono</td>
   <td><img alt="Icona di spunta Sì" src="assets/yes_tick.png" /></td>
   <td><img alt="Icona di spunta Sì" src="assets/yes_tick.png" /></td>
   <td><img alt="Icona di spunta Sì" src="assets/yes_tick.png" /></td>
   <td><img alt="Icona di spunta Sì" src="assets/yes_tick.png" /></td>
   <td><img alt="Icona di spunta Sì" src="assets/yes_tick.png" /></td>
   <td><img alt="Icona di spunta Sì" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Interruttore</td>
   <td><img alt="Icona di spunta Sì" src="assets/yes_tick.png" /></td>
   <td><img alt="Icona di spunta Sì" src="assets/yes_tick.png" /></td>
   <td><img alt="Icona di spunta Sì" src="assets/yes_tick.png" /></td>
   <td><img alt="Icona di spunta Sì" src="assets/yes_tick.png" /></td>
   <td><img alt="Icona di spunta Sì" src="assets/yes_tick.png" /></td>
   <td><img alt="Icona di spunta Sì" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Pulsante</td>
   <td><img alt="Icona di spunta Sì" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="Icona di spunta Sì" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="Icona di spunta Sì" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="Icona di spunta Sì" src="assets/yes_tick.png" /></td>
   <td> </td>
  </tr>
  <tr>
   <td>Casella di controllo</td>
   <td><img alt="Icona di spunta Sì" src="assets/yes_tick.png" /></td>
   <td><img alt="Icona di spunta Sì" src="assets/yes_tick.png" /></td>
   <td><img alt="Icona di spunta Sì" src="assets/yes_tick.png" /></td>
   <td><img alt="Icona di spunta Sì" src="assets/yes_tick.png" /></td>
   <td><img alt="Icona di spunta Sì" src="assets/yes_tick.png" /></td>
   <td><img alt="Icona di spunta Sì" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="Icona di spunta Sì" src="assets/yes_tick.png" /></td>
  </tr>
  <tr>
   <td>Elenchi a discesa</td>
   <td><img alt="Icona di spunta Sì" src="assets/yes_tick.png" /></td>
   <td><img alt="Icona di spunta Sì" src="assets/yes_tick.png" /></td>
   <td><img alt="Icona di spunta Sì" src="assets/yes_tick.png" /></td>
   <td><img alt="Icona di spunta Sì" src="assets/yes_tick.png" /></td>
   <td><img alt="Icona di spunta Sì" src="assets/yes_tick.png" /></td>
   <td><img alt="Icona di spunta Sì" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="Icona di spunta Sì" src="assets/yes_tick.png" /></td>
  </tr>
  <tr>
   <td>Scelta dell'immagine</td>
   <td><img alt="Icona di spunta Sì" src="assets/yes_tick.png" /></td>
   <td><img alt="Icona di spunta Sì" src="assets/yes_tick.png" /></td>
   <td><img alt="Icona di spunta Sì" src="assets/yes_tick.png" /></td>
   <td><img alt="Icona di spunta Sì" src="assets/yes_tick.png" /></td>
   <td><img alt="Icona di spunta Sì" src="assets/yes_tick.png" /></td>
   <td><img alt="Icona di spunta Sì" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="Icona di spunta Sì" src="assets/yes_tick.png" /></td>
  </tr>
  <tr>
   <td>Campo immissione data</td>
   <td><img alt="Icona di spunta Sì" src="assets/yes_tick.png" /></td>
   <td><img alt="Icona di spunta Sì" src="assets/yes_tick.png" /></td>
   <td><img alt="Icona di spunta Sì" src="assets/yes_tick.png" /></td>
   <td><img alt="Icona di spunta Sì" src="assets/yes_tick.png" /></td>
   <td><img alt="Icona di spunta Sì" src="assets/yes_tick.png" /></td>
   <td><img alt="Icona di spunta Sì" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Selettore data</td>
   <td><img alt="Icona di spunta Sì" src="assets/yes_tick.png" /></td>
   <td><img alt="Icona di spunta Sì" src="assets/yes_tick.png" /></td>
   <td><img alt="Icona di spunta Sì" src="assets/yes_tick.png" /></td>
   <td><img alt="Icona di spunta Sì" src="assets/yes_tick.png" /></td>
   <td><img alt="Icona di spunta Sì" src="assets/yes_tick.png" /></td>
   <td><img alt="Icona di spunta Sì" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>E-mail</td>
   <td><img alt="Icona di spunta Sì" src="assets/yes_tick.png" /></td>
   <td><img alt="Icona di spunta Sì" src="assets/yes_tick.png" /></td>
   <td><img alt="Icona di spunta Sì" src="assets/yes_tick.png" /></td>
   <td><img alt="Icona di spunta Sì" src="assets/yes_tick.png" /></td>
   <td><img alt="Icona di spunta Sì" src="assets/yes_tick.png" /></td>
   <td><img alt="Icona di spunta Sì" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Allegato file</td>
   <td><img alt="Icona di spunta Sì" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="Icona di spunta Sì" src="assets/yes_tick.png" /></td>
   <td><img alt="Icona di spunta Sì" src="assets/yes_tick.png" /></td>
   <td><img alt="Icona di spunta Sì" src="assets/yes_tick.png" /></td>
   <td><img alt="Icona di spunta Sì" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Immagine</td>
   <td><img alt="Icona di spunta Sì" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="Icona di spunta Sì" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Draw</td>
   <td><img alt="Icona di spunta Sì" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="Icona di spunta Sì" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Pannello</td>
   <td><img alt="Icona di spunta Sì" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="Icona di spunta Sì" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
 </tbody>
</table>

Alcuni esempi di utilizzo degli eventi in un JSON nascondono un campo sull’evento di inizializzazione e configurano il valore di un altro campo sull’evento di commit del valore. Per informazioni dettagliate sulla creazione di espressioni per gli eventi script, vedi [Espressioni modulo adattivo](adaptive-form-expressions.md).

Di seguito è riportato un codice JSON di esempio per gli esempi precedentemente menzionati.

### Nascondere un campo durante l’evento di inizializzazione {#hiding-a-field-on-initialize-event}

```json
"name": {
    "type": "string",
    "aem:afProperties": {
        "events" : {
            "Initialize" : "this.visible = false;"
        }
    }
}
```

#### Configura il valore di un altro campo nell’evento di commit del valore {#configure-value-of-another-field-on-value-commit-event}

```json
"Income": {
    "type": "object",
    "properties": {
        "monthly": {
            "type": "number",
            "aem:afProperties": {
                "events" : {
                    "Value Commit" : "IncomeYearly.value = this.value * 12;"
                }
            }
        },
        "yearly": {
            "type": "number",
            "aem:afProperties": {
                "name": "IncomeYearly"
            }
        }
    }
}
```

## Limitare valori accettabili per un componente modulo adattivo {#limit-acceptable-values-for-an-adaptive-form-component}

Per limitare i valori accettabili per un componente modulo adattivo, puoi aggiungere le seguenti restrizioni agli elementi dello schema JSON:

<table>
 <tbody>
  <tr>
   <td><p><strong> Proprietà schema</strong></p> </td>
   <td><p><strong>Tipo di dati</strong></p> </td>
   <td><p><strong>Descrizione</strong></p> </td>
   <td><p><strong>Componente</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>maximum</code></p> </td>
   <td><p>Stringa</p> </td>
   <td><p>Specifica il limite superiore per valori numerici e date. Per impostazione predefinita, il valore massimo è incluso.</p> </td>
   <td>
    <ul>
     <li>Casella numerica</li>
     <li>Stepper numerico<br /> </li>
     <li>Selettore data</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>minimum</code></p> </td>
   <td><p>Stringa</p> </td>
   <td><p>Specifica il limite inferiore per i valori numerici e le date. Per impostazione predefinita, è incluso il valore minimo.</p> </td>
   <td>
    <ul>
     <li>Casella numerica</li>
     <li>Stepper numerico</li>
     <li>Selettore data</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>exclusiveMaximum</code></p> </td>
   <td><p>Booleano</p> </td>
   <td><p>Se true, il valore numerico o la data specificati nel componente del modulo devono essere inferiori al valore numerico o alla data specificati per la proprietà maximum.</p> <p>Se false, il valore numerico o la data specificati nel componente del modulo deve essere minore o uguale al valore numerico o alla data specificati per la proprietà maximum.</p> </td>
   <td>
    <ul>
     <li>Casella numerica</li>
     <li>Stepper numerico</li>
     <li>Selettore data</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>exclusiveMinimum</code></p> </td>
   <td><p>Booleano</p> </td>
   <td><p>Se true, il valore numerico o la data specificati nel componente del modulo devono essere maggiori del valore numerico o della data specificati per la proprietà minimum.</p> <p>Se false, il valore numerico o la data specificati nel componente del modulo devono essere maggiori o uguali al valore numerico o alla data specificati per la proprietà minimum.</p> </td>
   <td>
    <ul>
     <li>Casella numerica</li>
     <li>Stepper numerico</li>
     <li>Selettore data</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>minLength</code></p> </td>
   <td><p>Stringa</p> </td>
   <td><p>Specifica il numero minimo di caratteri consentito in un componente. La lunghezza minima deve essere uguale o maggiore di zero.</p> </td>
   <td>
    <ul>
     <li>Casella di testo</li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>maxLength</code></td>
   <td>Stringa</td>
   <td>Specifica il numero massimo di caratteri consentiti in un componente. La lunghezza massima deve essere uguale o maggiore di zero.</td>
   <td>
    <ul>
     <li>Casella di testo</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>pattern</code></p> </td>
   <td><p>Stringa</p> </td>
   <td><p>Specifica la sequenza dei caratteri. Un componente accetta i caratteri se questi sono conformi al modello specificato.</p> <p>La proprietà pattern viene mappata sul pattern di convalida del componente del modulo adattivo corrispondente.</p> </td>
   <td>
    <ul>
     <li>Tutti i componenti di moduli adattivi mappati su uno schema XSD </li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>maxItems</code></td>
   <td>Stringa</td>
   <td>Specifica il numero massimo di elementi in un array. Il numero massimo di elementi deve essere uguale o maggiore di zero.</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>minItems</code></td>
   <td>Stringa</td>
   <td>Specifica il numero minimo di elementi in un array. Gli elementi minimi devono essere uguali o maggiori di zero.</td>
   <td> </td>
  </tr>
 </tbody>
</table>

## Costrutti non supportati  {#non-supported-constructs}

I moduli adattivi non supportano i seguenti costrutti dello schema JSON:

* Tipo nullo
* tipi di unione, come eventuali, e
* Uno di, uno di, tutti e NON
* Sono supportati solo array omogenei. Pertanto, il vincolo items deve essere un oggetto e non un array.

## Domande frequenti {#frequently-asked-questions}

**Perché non è possibile trascinare singoli elementi di una sottomaschera (struttura generata da qualsiasi tipo complesso) per sottomaschere ripetibili (i valori minOccours o maxOccurs sono maggiori di 1)?**

In una sottomaschera ripetibile, è necessario utilizzare la sottomaschera completa. Se desideri solo campi selettivi, utilizza l’intera struttura ed elimina quelli indesiderati.

**In Content Finder ho una struttura lunga e complessa. Come posso trovare un elemento specifico?**

Sono disponibili due opzioni:

* Scorri nella struttura ad albero
* Utilizzare la casella di ricerca per trovare un elemento

**Quale deve essere l’estensione del file di schema JSON?**

L’estensione del file dello schema JSON deve essere .schema.json. Ad esempio: &lt;filename>.schema.json.
