---
title: Adobe Experience Manager Mobili - Preparazione al RGPD
description: Scopri come Adobe Experience Manager è pronta ad aiutarti con gli obblighi di conformità ai requisiti RGPD.
contentOwner: trushton
exl-id: d06e675f-fb61-47da-85de-e0b50dd44153
solution: Experience Manager
feature: Mobile
role: User
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '683'
ht-degree: 0%

---

# AEM Mobile - Preparazione al RGPD {#aem-mobile-gdpr-readiness}

>[!IMPORTANT]
>
>Il RGPD è utilizzato come esempio nelle sezioni seguenti, ma i dettagli coperti sono applicabili a tutte le normative su privacy e protezione dei dati, come RGPD e CCPA.

{{ue-over-mobile}}

## Supporto per il RGPD di AEM Mobile {#aem-mobile-gdpr-support}

AEM Mobile è pronta ad assistere i clienti con i loro obblighi di conformità ai requisiti RGPD. In AEM Mobile non vengono memorizzati dati personali. Se hai effettuato il provisioning, puoi accedere a Adobe Experience Mobile con il tuo Adobe ID.

<!-- [https://aemmobile.adobe.com/signin/index.html](https://aemmobile.adobe.com/signin/index.html) -->

## Adobe Digital Publishing Suite {#adobe-digital-publishing-suite}

Il prodotto di pubblicazione digitale di Adobe (che precede AEM Mobile) supporta le iniziative di preparazione al RGPD di Adobe. Vedi [https://business.adobe.com/privacy/general-data-protection-regulation.html](https://business.adobe.com/privacy/general-data-protection-regulation.html). Di seguito sono riportate le specifiche sul supporto delle funzioni relative al RGPD nel prodotto di Digital Publishing Suite, incluso come utilizzare Adobe per avviare le richieste RGPD.

Per evitare di confondere AEM Mobile con il prodotto di Digital Publishing Suite precedente, puoi accedere al prodotto di Digital Publishing Suite facendo clic qui:

[https://acrobat.adobe.com/us/en/](https://acrobat.adobe.com/us/en/)

### Avvio di una richiesta RGPD {#initiating-a-gdpr-request}

Contatta l’Assistenza clienti di Adobe per avviare una richiesta RGPD per il Digital Publishing Suite.

Per individuare i dati dei clienti sono necessari i seguenti ID. Qualsiasi sottoinsieme ricevuto implica che gli altri ID non erano applicabili a questo utente.

Obbligatorio

* ID contratto del cliente: *dpsc-contractId*

Fornire almeno una delle seguenti informazioni:

* ID OAuth fornito dal cliente dell&#39;utente finale (l&#39;ID utilizzato nel sistema di adesione diretta del cliente): *dpsc-directEntitlementId*
* Per gli utenti dell&#39;app Windows, l&#39;ID App Store dell&#39;utente finale: *dpsc-windowsAppStoreId*
* Indirizzo e-mail utilizzato dall&#39;utente finale per interagire con l&#39;app DPS: *email*

### Domande frequenti {#frequently-asked-questions-faq}

**Adobe sta eliminando i miei acquisti App Store quando avvia una richiesta DELETE?**

Adobe elimina le informazioni di cui dispone sugli acquisti da app store (abbonamenti e così via), ma gli acquisti sono ancora registrati negli app store. Se l’app (utente finale) è registrata nell’App Store, le ricevute vengono prelevate nuovamente e inviate ad Adobe. Successivamente, questi vengono considerati come nuovi acquisti e vengono ripristinati dall’app, con accesso di nuovo.

**L&#39;Adobe elimina i diritti forniti dal cliente quando si avvia una richiesta DELETE?**

L&#39;Adobe elimina le informazioni di cui dispone in merito alle quote aggiuntive spettanti direttamente al cliente. Se l’app (utente finale) accede al meccanismo OAuth utilizzato dal cliente, invia informazioni ad Adobe e i servizi raccolgono nuovamente i diritti aggiuntivi.

**Cosa ci si aspetta dall&#39;utente finale?**

Poiché la chiave per assegnare i diritti all’app risiede sul dispositivo come parte del software del visualizzatore, l’utente finale deve disinstallare l’app. L’utente finale deve rendersi conto che se reinstalla l’app, gli acquisti esistenti (associati all’utente dell’app store) e le quote di adesione diretta (associate all’utente OAuth del cliente) vengono ancora ripristinati.

**Cosa succede quando un&#39;app viene condivisa tra persone su un dispositivo?**

Adobe dispone di informazioni minime che vengono associate direttamente a un utente specifico. Associa i dati utilizzando un UUID creato in modo casuale che viene conservato nei dati dell’app e trasmesso in ogni richiesta avviata dall’app. Ciò significa che gli utenti finali che condividono l’app sullo stesso dispositivo utilizzano lo stesso UUID e che tutti i dati sono considerati di proprietà della persona che effettua la richiesta RGPD. Per entrambe le richieste di accesso ed eliminazione, DPSC considera le persone che condividono un’app come un’unica persona.

**Quali dati personali vengono tracciati con Analytics?**

Nessuno. Sono presenti dati tracciati, ma si trovano a livello di app (non personali). Ciò include eventi come avvii, arresti anomali, chiusura, attività, acquisti o sovrapposizioni di folio. Le posizioni geografiche, i nomi, gli ID dispositivo o gli indirizzi IP non vengono tracciati.

**L&#39;utente finale ha fornito le informazioni, ma non è stato trovato nulla. Perché no?**

Con l’evoluzione del prodotto di Digital Publishing Suite, le implementazioni dei servizi sono state modificate e più dati sono stati offuscati. Se non sono stati trovati dati utilizzando i dati forniti dall’utente, significa che i dati dell’utente non possono essere tracciati per quella persona.

### Esempio {#example}

Contatta l’Assistenza clienti di Adobe per avviare una richiesta RGPD.

Di seguito è riportato un esempio degli input e degli output risultanti da una richiesta RGPD Digital Publishing Suite:

#### Input: {#inputs}

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
