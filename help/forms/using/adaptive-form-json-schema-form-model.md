---
title: Creazione di moduli adattivi con lo schema JSON
seo-title: Creazione di moduli adattivi con lo schema JSON
description: I moduli adattivi possono utilizzare lo schema JSON come modello di modulo, consentendo di sfruttare gli schemi JSON esistenti per creare moduli adattivi.
seo-description: I moduli adattivi possono utilizzare lo schema JSON come modello di modulo, consentendo di sfruttare gli schemi JSON esistenti per creare moduli adattivi.
uuid: bdeaeae8-65a3-4c46-b27d-fe68481e31f1
topic-tags: develop
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 375ba8fc-3152-4564-aec5-fcff2a95cf4c
docset: aem65
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '1469'
ht-degree: 5%

---


# Creazione di moduli adattivi con lo schema JSON{#creating-adaptive-forms-using-json-schema}

## Prerequisiti {#prerequisites}

Per creare un modulo adattivo utilizzando uno schema JSON come modello di modulo, è necessario conoscere a fondo lo schema JSON. Si consiglia di leggere il contenuto seguente prima di questo articolo.

* [Creazione di un modulo adattivo](../../forms/using/creating-adaptive-form.md)
* [Schema JSON](https://json-schema.org/)

## Utilizzo di uno schema JSON come modello di modulo  {#using-a-json-schema-as-form-model}

I AEM Forms supportano la creazione di un modulo adattivo utilizzando uno schema JSON esistente come modello di modulo. Questo schema JSON rappresenta la struttura in cui i dati vengono prodotti o utilizzati dal sistema back-end della tua organizzazione. Lo schema JSON utilizzato deve essere conforme alle specifiche [](https://json-schema.org/draft-04/schema)v4.

Le caratteristiche chiave dell&#39;utilizzo di uno schema JSON sono:

* La struttura del JSON viene visualizzata come struttura ad albero nella scheda Content Finder nella modalità di creazione per un modulo adattivo. Puoi trascinare e aggiungere elementi dalla gerarchia JSON al modulo adattivo.
* È possibile precompilare il modulo utilizzando JSON conforme allo schema associato.
* Al momento dell&#39;invio, i dati immessi dall&#39;utente vengono inviati come JSON che si allinea allo schema associato.

Uno schema JSON è costituito da tipi di elementi semplici e complessi. Gli elementi hanno attributi che aggiungono regole all&#39;elemento. Quando questi elementi e attributi vengono trascinati su un modulo adattivo, vengono mappati automaticamente sul componente modulo adattivo corrispondente.

La mappatura degli elementi JSON con componenti per moduli adattivi è la seguente:

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
   <th><strong>Elemento, proprietà o attributi JSON</strong></th>
   <th><strong>Componente modulo adattivo</strong></th>
  </tr>
  <tr>
   <td><p>Proprietà delle stringhe con vincolo enum e enumNames.</p> <p>Sintassi,</p> <p> <code>{</code></p> <p><code>"type" : "string",</code></p> <p><code>"enum" : ["M", "F"]</code></p> <p><code>"enumNames" : ["Male", "Female"]</code></p> <p><code>}</code></p> <p> </p> </td>
   <td><p>Componente a discesa:</p>
    <ul>
     <li>I valori elencati in enumNames vengono visualizzati nella casella di rilascio.</li>
     <li>I valori elencati nell'enum sono utilizzati per il calcolo.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Proprietà stringa con vincolo di formato. Ad esempio, e-mail e data.</p> <p>Sintassi,</p> <p><code>{</code></p> <p><code>"type" : "string",</code></p> <p><code>"format" : "email"</code></p> <p><code>}</code></p> <p> </p> </td>
   <td>
    <ul>
     <li>Il componente e-mail viene mappato quando il tipo è stringa e il formato è e-mail.</li>
     <li>Il componente Textbox con convalida viene mappato quando il tipo è stringa e il formato è nomehost.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>{</p> <p>"type" : "string",</p> <p>}</p> </td>
   <td><br /> <br /> Campo di testo<br /> <br /> <br /> </td>
  </tr>
  <tr>
   <td>number, proprietà<br /> </td>
   <td>Campo numerico con sottotipo impostato su Mobile<br /> </td>
  </tr>
  <tr>
   <td>integer, proprietà<br /> </td>
   <td>Campo numerico con sottotipo impostato su numero intero<br /> </td>
  </tr>
  <tr>
   <td>boolean, proprietà<br /> </td>
   <td>Scambia<br /> </td>
  </tr>
  <tr>
   <td>object property<br /> </td>
   <td>Pannello<br /> </td>
  </tr>
  <tr>
   <td>array, proprietà</td>
   <td>Pannello ripetibile con min e max uguali rispettivamente a minItems e maxItems. Sono supportati solo gli array omogenei. Pertanto, il vincolo elementi deve essere un oggetto e non un array.<br /> </td>
  </tr>
 </tbody>
</table>

### Proprietà comuni dello schema {#common-schema-properties}

Il modulo adattivo utilizza le informazioni disponibili nello schema JSON per mappare ciascun campo generato. In particolare:

* La proprietà title funge da etichetta per i componenti per modulo adattivo.
* La proprietà description è impostata come descrizione lunga per un componente modulo adattivo.
* La proprietà predefinita funge da valore iniziale di un campo modulo adattivo.
* La proprietà maxLength è impostata come attributo maxlength del componente Campo di testo.
* Per il componente Casella numerica vengono utilizzate le proprietà minima, massima, esclusivaMinimum ed esclusivaMaximum.
* Per supportare l&#39;intervallo per il componente DatePicker, vengono fornite ulteriori proprietà dello schema JSON: minDate e maxDate.
* Le proprietà minItems e maxItems vengono utilizzate per limitare il numero di elementi/campi che possono essere aggiunti o rimossi da un componente del pannello.
* La proprietà readOnly imposta l’attributo di sola lettura di un componente modulo adattivo.
* La proprietà richiesta contrassegna il campo modulo adattivo come obbligatorio, mentre nel caso del pannello (dove type è object), i dati JSON inviati finali hanno campi con un valore vuoto corrispondente a tale oggetto.
* La proprietà pattern è impostata come pattern di convalida (espressione regolare) in forma adattiva.
* L&#39;estensione del file di schema JSON deve essere mantenuta .schema.json. Ad esempio, &lt;nomefile>.schema.json.

## Schema JSON di esempio {#sample-json-schema}

Ecco un esempio di uno schema JSON.

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

### Definizioni dello schema riutilizzabili {#reusable-schema-definitions}

Le chiavi di definizione vengono utilizzate per identificare gli schemi riutilizzabili. Le definizioni dello schema riutilizzabili vengono utilizzate per creare i frammenti. È simile all&#39;identificazione di tipi complessi in XSD. Di seguito è riportato un esempio di schema JSON con definizioni:

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

L&#39;esempio precedente definisce un record cliente, in cui ogni cliente dispone sia di un indirizzo di spedizione che di un indirizzo di fatturazione. La struttura di entrambi gli indirizzi è la stessa (gli indirizzi hanno un indirizzo, una città e uno stato) quindi è una buona idea non duplicare gli indirizzi. Consente inoltre di aggiungere ed eliminare campi con facilità per qualsiasi modifica futura.

## Pre-configurazione dei campi nella definizione dello schema JSON {#pre-configuring-fields-in-json-schema-definition}

È possibile utilizzare la proprietà **aem:afProperties** per preconfigurare il campo Schema JSON in modo che venga associato a un componente modulo adattivo personalizzato. Di seguito è riportato un esempio:

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

JavaScript è il linguaggio di espressione dei moduli adattivi. Tutte le espressioni sono espressioni JavaScript valide e utilizzano API per modelli di script di moduli adattivi. È possibile preconfigurare gli oggetti modulo per [valutare un&#39;espressione](../../forms/using/adaptive-form-expressions.md) su un evento del modulo.

Utilizzare la proprietà aem:afproperties per preconfigurare le espressioni di modulo adattivo o gli script per i componenti modulo adattivi. Ad esempio, quando si attiva l&#39;evento initialize, il codice seguente imposta il valore del campo telefonico e stampa un valore nel registro:

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

È necessario essere membri del gruppo [](/help/forms/using/forms-groups-privileges-tasks.md) form-power-user per configurare script o espressioni per l&#39;oggetto modulo. Nella tabella seguente sono elencati tutti gli eventi di script supportati per un componente modulo adattivo.

<table>
 <tbody>
  <tr>
   <th><strong></strong>Componente \ Evento</th>
   <th>initialize <br /> </th>
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
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Campo numerico</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Stepper numerico</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Pulsante di scelta</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Telefono</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Scambia</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Pulsante</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
  </tr>
  <tr>
   <td>Casella di controllo</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
  </tr>
  <tr>
   <td>A Discesa</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
  </tr>
  <tr>
   <td>Scelta immagine</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
  </tr>
  <tr>
   <td>Campo immissione data</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Selettore data</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>E-mail</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Allegato file</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Immagine</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Draw</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Pannello</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
 </tbody>
</table>

Alcuni esempi dell&#39;utilizzo degli eventi in un JSON nascondono un campo in corrispondenza dell&#39;evento initialize e configurano il valore di un altro campo in corrispondenza dell&#39;evento value commit. Per informazioni dettagliate sulla creazione di espressioni per gli eventi di script, vedere Espressioni [modulo](../../forms/using/adaptive-form-expressions.md)adattive.

Di seguito è riportato il codice JSON di esempio per i suddetti esempi.

### Nascondere un campo durante l&#39;evento initialize {#hiding-a-field-on-initialize-event}

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

#### Configurare il valore di un altro campo in caso di evento commit del valore {#configure-value-of-another-field-on-value-commit-event}

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

## Limitare i valori accettabili per un componente modulo adattivo {#limit-acceptable-values-for-an-adaptive-form-component}

È possibile aggiungere le seguenti limitazioni agli elementi dello schema JSON per limitare i valori accettabili per un componente modulo adattivo:

<table>
 <tbody>
  <tr>
   <td><p><strong> Proprietà Schema</strong></p> </td>
   <td><p><strong>Tipo di dati</strong></p> </td>
   <td><p><strong>Descrizione</strong></p> </td>
   <td><p><strong>Componente</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>maximum</code></p> </td>
   <td><p>Stringa</p> </td>
   <td><p>Specifica il limite superiore per i valori numerici e le date. Per impostazione predefinita, è incluso il valore massimo.</p> </td>
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
   <td><p>Se true, il valore numerico o la data specificati nel componente del modulo devono essere inferiori al valore numerico o alla data specificati per la proprietà massima.</p> <p>Se è false, il valore numerico o la data specificati nel componente del modulo deve essere minore o uguale al valore numerico o alla data specificati per la proprietà massima.</p> </td>
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
   <td><p>Se true, il valore numerico o la data specificati nel componente del modulo devono essere maggiori del valore numerico o della data specificati per la proprietà minima.</p> <p>Se è false, il valore numerico o la data specificati nel componente del modulo deve essere maggiore o uguale al valore numerico o alla data specificati per la proprietà minima.</p> </td>
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
   <td><p>Specifica il numero minimo di caratteri consentiti in un componente. La lunghezza minima deve essere uguale o maggiore di zero.</p> </td>
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
   <td><p>Specifica la sequenza dei caratteri. Un componente accetta i caratteri se questi sono conformi al pattern specificato.</p> <p>La proprietà pattern viene mappata sul pattern di convalida del componente modulo adattivo corrispondente.</p> </td>
   <td>
    <ul>
     <li>Tutti i componenti di moduli adattivi mappati a uno schema XSD </li>
    </ul> </td>
  </tr>
  <tr>
   <td>maxItems</td>
   <td>Stringa</td>
   <td>Specifica il numero massimo di elementi in un array. Gli elementi massimi devono essere uguali o maggiori di zero.</td>
   <td> </td>
  </tr>
  <tr>
   <td>minItems</td>
   <td>Stringa</td>
   <td>Specifica il numero minimo di elementi in un array. Gli elementi minimi devono essere uguali o maggiori di zero.</td>
   <td> </td>
  </tr>
 </tbody>
</table>

## costrutti non supportati  {#non-supported-constructs}

I moduli adattivi non supportano i seguenti costrutti dello schema JSON:

* Tipo Null
* tipi di Unione, quali eventuali, e
* Uno, AnyOf, AllOf e NO
* Sono supportati solo gli array omogenei. Pertanto, il vincolo elementi deve essere un oggetto e non un array.

## Domande frequenti {#frequently-asked-questions}

**Perché non è possibile trascinare singoli elementi di un sottomodulo (struttura generata da qualsiasi tipo complesso) per sottomoduli ripetibili (i valori minOccours o maxOccurs sono maggiori di 1)?**

In un sottomodulo ripetibile, è necessario utilizzare il sottomodulo completo. Se desiderate solo campi selettivi, utilizzate l&#39;intera struttura ed eliminate quelli indesiderati.

**In Content Finder ho una struttura complessa molto lunga. Come posso trovare un elemento specifico?**

Sono disponibili due opzioni:

* Scorrere la struttura ad albero
* Utilizzare la casella di ricerca per trovare un elemento

**Quale dovrebbe essere l&#39;estensione del file di schema JSON?**

L&#39;estensione del file di schema JSON deve essere .schema.json. Ad esempio, &lt;nomefile>.schema.json.
