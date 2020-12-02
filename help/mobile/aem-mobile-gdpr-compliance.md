---
title: ' AEM Mobile - Preparazione GDPR'
seo-title: ' AEM Mobile - Preparazione GDPR'
description: 'null'
seo-description: 'null'
uuid: 817c434f-4b78-40f7-99d6-6efafdedb77e
contentOwner: trushton
discoiquuid: 9399dd3d-a485-4f53-a6f2-7b190da4235b
translation-type: tm+mt
source-git-commit: 85a3dac5db940b81da9e74902a6aa475ec8f1780
workflow-type: tm+mt
source-wordcount: '694'
ht-degree: 1%

---


#  AEM Mobile - Preparazione GDPR {#aem-mobile-gdpr-readiness}

>[!IMPORTANT]
>
>Il GDPR è utilizzato come esempio nelle sezioni seguenti, ma i dettagli trattati sono applicabili a tutte le normative sulla protezione dei dati e sulla privacy; come GDPR, CCPA ecc.

##  supporto AEM Mobile GDPR {#aem-mobile-gdpr-support}

 AEM Mobile è pronta ad assistere i clienti nei loro obblighi di conformità ai requisiti GDPR. Nessun dato personale è memorizzato in  AEM Mobile. Se hai effettuato il provisioning, puoi accedere ad Adobe Experience Mobile con il tuo Adobe ID .

[https://aemmobile.adobe.com/signin/index.html](https://aemmobile.adobe.com/signin/index.html)

## Adobe Digital Publishing Suite {#adobe-digital-publishing-suite}

 prodotto Digital Publishing del Adobe (che precede  AEM Mobile) supporta  iniziative di preparazione del GDPR del Adobe. Vedere [https://www.adobe.com/privacy/general-data-protection-regulation.html](https://www.adobe.com/privacy/general-data-protection-regulation.html). Di seguito verranno fornite informazioni specifiche sul supporto per le funzioni GDPR pertinenti nel prodotto Digital Publishing Suite, tra cui come lavorare con  Adobe per avviare richieste GDPR.

Per evitare di confondere  AEM Mobile con il precedente prodotto Digital Publishing Suite, potete accedere al prodotto Digital Publishing Suite qui:

[https://digitalpublishing.acrobat.com/welcome.html](https://digitalpublishing.acrobat.com/welcome.html)

### Avvio di una richiesta GDPR {#initiating-a-gdpr-request}

Per avviare una richiesta GDPR per Digital Publishing Suite, contattate &#39;Assistenza clienti di Adobe.

Per individuare i dati dei clienti sono necessari i seguenti ID. Eventuali sottoinsiemi ricevuti implicheranno che gli altri ID non fossero applicabili a questo utente.

Obbligatorio:

* ID contratto del cliente: *dpsc-ContractId*

Fornire almeno 1 delle seguenti informazioni:

* Il cliente dell&#39;utente finale ha fornito l&#39;ID OAuth (l&#39;ID utilizzato nel sistema di adesione diretta del cliente): *dpsc-directEntitlementId*
* Per gli utenti delle app Windows, l&#39;ID App Store dell&#39;utente finale: *dpsc-windowsAppStoreId*
* L&#39;indirizzo e-mail usato dall&#39;utente finale per interagire con l&#39;app DPS: *email*

### Domande frequenti {#frequently-asked-questions-faq}

**Adobe eliminare gli acquisti da App Store quando viene avviata una richiesta di DELETE?**

 Adobe eliminerà le informazioni di acquisto dell&#39;App Store (iscrizioni, ecc.) ma gli acquisti saranno ancora registrati negli App Store. Se l&#39;app (utente finale) ha eseguito l&#39;accesso all&#39;App Store, tali ricevute verranno prelevate di nuovo e inviate  Adobe, e successivamente verranno considerate come nuovi acquisti e verranno ripristinate dall&#39;App per avere nuovamente accesso.

**Adobe eliminare le adesioni fornite dal cliente quando si avvia una richiesta di DELETE?**

 Adobe eliminerà le informazioni di cui dispone sulle ulteriori quote di adesione diretta del cliente. Se l&#39;app (utente finale) effettua l&#39;accesso al meccanismo OAuth utilizzato dal cliente, invierà informazioni al Adobe  e i servizi recupereranno nuovamente le adesioni aggiuntive.

**Cosa ci si aspetta dall&#39;utente finale?**

Poiché la chiave per assegnare le adesioni all&#39;app risiede sul dispositivo come parte del software del visualizzatore, l&#39;utente finale deve disinstallare l&#39;app. L&#39;utente finale deve rendersi conto che se reinstalla l&#39;app, gli acquisti esistenti (associati all&#39;utente dell&#39;App Store) e le quote di adesione diretta (associate all&#39;utente OAuth del cliente) saranno ancora ripristinati.

**Cosa succede quando un&#39;app viene condivisa tra persone su un dispositivo?**

 Adobe dispone di poche informazioni che consentono di tornare direttamente a un utente specifico. Associa i dati utilizzando un UUID creato in modo casuale che viene memorizzato nei dati dell&#39;app e trasmesso in ogni richiesta avviata dall&#39;app. Ciò significa che gli utenti finali che condividono l&#39;app sullo stesso dispositivo utilizzeranno lo stesso UUID e che tutti i dati saranno considerati di proprietà della persona che effettua la richiesta GDPR. Per entrambe le richieste di accesso ed eliminazione, DPSC considererà le persone che condividono un&#39;app come un&#39;unica persona.

**Quali dati personali vengono tracciati con Analytics?**

Nessuno. I dati vengono tracciati, ma si trovano a livello di app (non a livello personale). Questo include eventi come avvii, arresti anomali, chiudi, attività, acquisti o sovrapposizioni di folio. Le posizioni geografiche, i nomi, gli ID dispositivo o gli indirizzi IP non vengono tracciati.

**L&#39;utente finale ha fornito le proprie informazioni, ma non è stato trovato nulla. Perché no?**

Con l&#39;evoluzione del prodotto Digital Publishing Suite, le implementazioni dei servizi sono state modificate e più dati sono stati oscurati. Se non sono stati trovati dati utilizzando i dati forniti dall&#39;utente, significa che i dati dell&#39;utente non possono essere tracciati a tale persona.

### Esempio {#example}

Contatta  Assistenza clienti di Adobe per avviare una richiesta GDPR.

Di seguito è riportato un esempio degli input e degli output risultanti da una richiesta GDPR di Digital Publishing Suite:

#### Ingressi: {#inputs}

```
dpsc-contractId = “12345-1234-12416234” 
directEntitlementId = “1234-1234-1234” 
windowsAppStoreId = “testWinAppStoreId” 
email = “test@what.com”
```

#### Uscite {#outputs}

```
{

    "jobId": "test-1524750204384",

    "product": "DPSC",

    "action": "access",

    "userIDS": [

        {

        "namespace": "email",

        "value": "test@what.com"

        },

        {

        "namespace": "windowsAppStoreId",

        "value": "testWinAppStoreId"

        },

        {

        "namespace": "directEntitlementId",

        "value": "1234-1234-1234"

        }

    ],

    "receiptData": {

    "recordsFound": 6,

    "recordsAffected": 0,

    "tablesModified": 0,

    "subscriptionsFound": 24,

    "entitlementsFound": 24

    },

    "records": {

        "DPS_Stage_EntitlementUserDevices": [

        {

            "user_id": "testc685-c9ca-4c1e-a11b-07d10ec724cf",

            "device_id": "appleStore:test1b16-f032-4d9c-9200-0d19999405c4",

            "account_id": "test@what.com"

        },

        {

            "user_id": "test967d-5179-4dc6-958c-facd9d94da38",

            "device_id": "appleStore:test3f07-d5aa-4b32-8fac-b2b690b7ccd7",

            "account_id": "test@what.com"

        },

        {

            "user_id": "test1838-6494-4e74-912c-1edf61581d0e",

            "device_id": "appleStore:test3813-f8cc-49ce-b021-50eb0814a3bb",

            "account_id": "1234-1234-1234"

        },

        {

            "user_id": "test5468-1a11-4e4c-be43-274181a9ef81",

            "device_id": "appleStore:testf082-2783-498d-ab62-b1b2e3eb67ae",

            "account_id": "1234-1234-1234"

        }

        ],

            "DPS_Stage_EntitlementUsers": [

        {

            "id": "store:test04a7-33a3-4b90-863d-79981ead0f19:appleStore",

            "part_id": "0",

            "alias_user_id": "testWinAppStoreId"

        },

        {

            "id": "internal:testd2da-0606-4444-87ef-0d5a1d4a121d:adobe",

            "part_id": "0",

            "user_id": "test@what.com"

        }

        ],

            "DPS_Stage_Subscriptions": [

        {

            "id": "appleStore:testc685-c9ca-4c1e-a11b-07d10ec724cf",

            "account_id": "test3531-a209-4391-beb9-951c7822244e",

            "overflow": "test4e59-86a8-4b75-b699-77e980c287ab",

            "entitlement_count": "12"

        },

        {

            "id": "appleStore:test5468-1a11-4e4c-be43-274181a9ef81",

            "account_id": "test491b-379e-4d24-96ef-e481bf8d3062",

            "overflow": "test931b-7422-485d-85a5-134828187b6c",

            "entitlement_count": "12"

        }

        ],

            "DPS_Stage_Entitlements": [

        {

            "id": "samsungStore:testc685-c9ca-4c1e-a11b-07d10ec724cf",

            "account_id": "test7332-60a0-42b8-a508-474668d83d2e",

            "overflow": "test9bc3-94d0-43cf-b132-0629868f7d9d",

            "entitlement_count": "12"

        },

        {

            "id": "appleStore:test5468-1a11-4e4c-be43-274181a9ef81",

            "account_id": "testf766-102a-460d-8f5a-42f7bb9d68b7",

            "overflow": "test4d96-2197-45a8-9caf-2aa2846b770c",

            "entitlement_count": "12"

        }

        ],

            "s3Buckets": {

            "name": "DPS-Entitlements-Overflow",

            "folder": "stage/",

            "overflows": {

            "subscriptions": [

            "test4e59-86a8-4b75-b699-77e980c287ab",

            "test931b-7422-485d-85a5-134828187b6c"

        ],

            "entitlements": [

            "test9bc3-94d0-43cf-b132-0629868f7d9d",

            "test4d96-2197-45a8-9caf-2aa2846b770c"

                ]

            }

        }

    }

}
```

