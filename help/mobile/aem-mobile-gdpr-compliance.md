---
title: Adobe Experience Manager Mobile - Preparazione all’RGPD
description: Adobe Experience Manager Mobile - Preparazione all’RGPD
uuid: 817c434f-4b78-40f7-99d6-6efafdedb77e
contentOwner: trushton
discoiquuid: 9399dd3d-a485-4f53-a6f2-7b190da4235b
exl-id: d06e675f-fb61-47da-85de-e0b50dd44153
source-git-commit: 85d39e59b82fdfdcd310be61787a315668aebe38
workflow-type: tm+mt
source-wordcount: '691'
ht-degree: 1%

---

# AEM Mobile - Preparazione all’RGPD {#aem-mobile-gdpr-readiness}

>[!IMPORTANT]
>
>Il RGPD è utilizzato come esempio nelle sezioni seguenti, ma i dettagli trattati sono applicabili a tutte le normative sulla protezione dei dati e sulla privacy; come RGPD, CCPA, ecc.

## Supporto per il RGPD in AEM Mobile {#aem-mobile-gdpr-support}

AEM Mobile è pronta ad assistere i clienti negli obblighi di conformità ai requisiti RGPD. Nessun dato personale viene memorizzato in AEM Mobile. Se hai il provisioning, puoi accedere ad Adobe Experience Mobile con il tuo Adobe ID.

<!-- [https://aemmobile.adobe.com/signin/index.html](https://aemmobile.adobe.com/signin/index.html) -->

## Adobe Digital Publishing Suite {#adobe-digital-publishing-suite}

Il prodotto di pubblicazione digitale di Adobe (che precede AEM Mobile) supporta le iniziative di preparazione al RGPD di Adobe. Vedi [https://www.adobe.com/privacy/general-data-protection-regulation.html](https://www.adobe.com/privacy/general-data-protection-regulation.html). Di seguito sono fornite informazioni specifiche sul supporto per le funzioni correlate al RGPD nel prodotto Digital Publishing Suite, tra cui come lavorare con Adobe per avviare richieste RGPD.

Per evitare di confondere AEM Mobile con il vecchio prodotto Digital Publishing Suite, accedi al prodotto Digital Publishing Suite qui:

[https://acrobat.adobe.com/us/en/](https://acrobat.adobe.com/us/en/)

### Avvio di una richiesta RGPD {#initiating-a-gdpr-request}

Contatta l’Assistenza clienti Adobe per avviare una richiesta RGPD per Digital Publishing Suite.

Per individuare i dati dei clienti sono necessari i seguenti ID. Qualsiasi sottoinsieme ricevuto implica che gli altri ID non erano applicabili a questo utente.

Obbligatorio:

* ID contratto del cliente: *dpsc-contractId*

Fornire almeno 1 delle seguenti informazioni:

* Il cliente dell’utente finale ha fornito l’ID OAuth (l’ID utilizzato nel sistema di adesione diretta del cliente): *dpsc-directEntitlementId*
* Per gli utenti dell&#39;app Windows, l&#39;App Store ID dell&#39;utente finale: *dpsc-windowsAppStoreId*
* L&#39;indirizzo e-mail dell&#39;utente finale utilizzato per interagire con l&#39;app DPS: *email*

### Domande frequenti {#frequently-asked-questions-faq}

**L’Adobe eliminerà gli acquisti App Store all’avvio di una richiesta DELETE?**

Adobe eliminerà le informazioni di cui dispone sugli acquisti da app store (abbonamenti, ecc.) ma gli acquisti saranno ancora registrati negli App Store. Se l’app (utente finale) è connessa all’App Store, tali ricevute verranno prelevate di nuovo e inviate all’Adobe e, successivamente, saranno considerate nuovi acquisti e verranno ripristinate dall’App per avere nuovamente accesso.

**L’Adobe elimina le adesioni fornite dal cliente quando si avvia una richiesta di DELETE?**

L&#39;Adobe eliminerà le informazioni di cui dispone in merito alle quote aggiuntive di diritto diretto del cliente. Se l’app (utente finale) accede al meccanismo OAuth utilizzato dal cliente, invia informazioni ad Adobe e i servizi recupereranno nuovamente le adesioni aggiuntive.

**Cosa ci si aspetta dall’utente finale?**

Poiché la chiave di assegnazione delle adesioni all&#39;app risiede sul dispositivo come parte del software del visualizzatore, l&#39;utente finale dovrebbe disinstallare l&#39;app. L’utente finale deve rendersi conto che, se reinstalla l’app, gli acquisti esistenti (associati all’utente dell’App Store) e le quote di adesione dirette (associate all’utente OAuth del cliente) verranno ancora ripristinati.

**Cosa succede quando un&#39;app viene condivisa tra persone su un dispositivo?**

Adobe dispone di poche informazioni che vengono associate direttamente a un utente specifico. Associa i dati utilizzando un UUID creato in modo casuale che viene tenuto nei dati dell’app e trasmesso in ogni richiesta avviata dall’app. Ciò significa che gli utenti finali che condividono l’app sullo stesso dispositivo utilizzeranno lo stesso UUID e che tutti i dati saranno considerati di proprietà della persona che effettua la richiesta RGPD. Per le richieste di accesso e di cancellazione, DPSC considera le persone che condividono un’app come un’unica persona.

**Quali dati personali vengono tracciati con Analytics?**

Nessuno. I dati vengono tracciati, ma sono a livello di app (non personali). Questo include eventi come avvii, arresti anomali, chiusura, attività, acquisti o sovrapposizioni di folio. Le posizioni geografiche, i nomi, gli ID dispositivo o gli indirizzi IP non vengono tracciati.

**L&#39;utente finale ha fornito le proprie informazioni ma non è stato trovato nulla. Perché no?**

Con l’evoluzione del prodotto Digital Publishing Suite, le implementazioni dei servizi sono state modificate e più dati sono stati offuscati. Se non sono stati trovati dati utilizzando i dati forniti dall’utente, significa che i dati dell’utente non possono essere tracciati nuovamente per tale persona.

### Esempio {#example}

Contatta l’Assistenza clienti Adobe per avviare una richiesta RGPD.

Ecco un esempio degli input e degli output risultanti di una richiesta RGPD di Digital Publishing Suite:

#### Ingressi: {#inputs}

```
dpsc-contractId = "12345-1234-12416234" 
directEntitlementId = "1234-1234-1234" 
windowsAppStoreId = "testWinAppStoreId" 
email = "test@what.com"
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
