---
title: Configurare l’Assistente IA in AEM
description: Scopri come impostare e configurare l’Assistente IA utilizzando Admin Console in Adobe Experience Manager.
solution: Experience Manager
feature: Authoring, AI Assistant, AI Tools
role: Admin, Developer, User
exl-id: 06824b3d-f912-4922-8fb6-ee2ca04c6326
autotag-review: '2026-05-18T18:35:37.980Z'
TQID: 'https://experienceleague.adobe.com/5YTQUJbJPlJuxToS6AVhJww1KQ20tuOlRoCVquyfSng'
product_v2: id: e14eb250-3c22-4a07-9061-a78112b2b826id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
feature_v2: id: ac5ecfc1-cc78-4ecc-a90a-0362685062ce
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2: id: c7d04a2c-412a-4c9d-9d7a-4456eaa5adeb
source-git-commit: 9c96b6744c7af2f061b4dfbf403560047485f9b5
workflow-type: tm+mt
source-wordcount: 1202
ht-degree: 98%

---

# Configurare l’Assistente IA in AEM {#aem-ai-asst-admin-setup}

<!-- An Administrator must configure access, permissions, and settings before users in their organization can use the features in AI Assistant in AEM. -->

<!-- badge: label="Beta" type="Positive" -->

Per utilizzare l’Assistente IA in AEM (Adobe Experience Manager), devi disporre delle autorizzazioni necessarie per accedere alla knowledge del prodotto tramite l’Assistente IA. Questa autorizzazione è attivata per impostazione predefinita.

Se desideri controllare chi può accedere alla knowledge del prodotto, invia un’e-mail ad [aemaiassistant@adobe.com](mailto:aemaiassistant@adobe.com) dall’indirizzo e-mail associato al tuo Adobe ID. Adobe può abilitare il controllo degli accessi a livello di utente. Quando è abilitato, l’amministratore può concedere l’accesso a livello di utente seguendo i passaggi descritti di seguito.

Se hai richiesto il controllo degli accessi a livello di utente, la tua organizzazione deve dare il consenso tramite Adobe Admin Console. Un amministratore di prodotto crea (o seleziona) un gruppo di utenti e concede la nuova autorizzazione “Assistante IA”. Chiunque venga aggiunto a quel gruppo ottiene immediatamente l’accesso all’Assistante IA in tutto AEM. Se l’obiettivo è la disponibilità a livello aziendale, l’amministratore assegna semplicemente tutti gli utenti a quel gruppo.

Dal punto di vista di un dipendente, il processo è semplice: identifica l’amministratore del prodotto per Adobe Experience Manager nella tua organizzazione e richiedi di essere aggiunto al gruppo di utenti abilitato all’IA. Una volta presente in quel gruppo, l’icona dell’Assistente sarà visualizzata automaticamente al prossimo accesso.

Gli amministratori devono tenere presente la normale governance di Cloud Manager. È necessario disporre dei diritti di amministratore del prodotto in Admin Console per creare profili, gestire gruppi di utenti o modificare le autorizzazioni. Se gli utenti necessitano anche della funzione incorporata dell’Assistente **Crea ticket di supporto**, aggiungi il ruolo standard di **amministratore di supporto** (ruolo standard di Admin Console) alle stesse persone o allo stesso gruppo.

Il processo di configurazione dell’Assistente IA in AEM prevede i seguenti passaggi:

1. [Creazione di un nuovo profilo di prodotto in Adobe Admin Console](#create-profile).
1. [Abilitazione dell’autorizzazione alla knowledge del prodotto dell’Assistente IA](#enable-permission).
1. [Creazione di un nuovo gruppo di utenti (o utilizzo di un gruppo di utenti esistente)](#create-user-group).
1. [Aggiunta di utenti al gruppo di utenti](#add-users).
1. [Assegnazione del profilo di prodotto al gruppo di utenti](#assign-product-profile).

**Prerequisiti**

Prima di iniziare, assicurati di aver soddisfatto i seguenti prerequisiti:

* Devi disporre almeno dei diritti di amministratore di prodotto in Adobe Admin Console.
* Devi conoscere la struttura di gestione degli utenti della tua organizzazione.

**Considerazioni sulla configurazione**

* Tempo di elaborazione: le risorse create in Cloud Manager potrebbero richiedere fino a 2 minuti per essere visualizzate in Admin Console per la configurazione delle autorizzazioni.
* Profili multipli: gli utenti possono far parte di più profili e le autorizzazioni vengono combinate da tutti i profili assegnati.
* Ambito dell’organizzazione: alcune autorizzazioni possono essere applicate a livello di organizzazione in tutti i programmi.
* Profili predefiniti: non eliminare i profili di autorizzazione predefiniti da Admin Console.


## 1 - Creazione di un nuovo profilo di prodotto in Adobe Admin Console{#create-profile}

1. Segui le istruzioni dettagliate in [Creare un nuovo profilo di prodotto in Adobe Admin Console](https://experienceleague.adobe.com/it/docs/experience-platform/access-control/ui/create-profile) disponibili nella documentazione di Experience Platform.

1. Quando crei il nuovo profilo di prodotto, puoi utilizzare i seguenti valori suggeriti per l’Assistente IA.

   | Campo testo | Valore suggerito |
   | --- | --- |
   | Nome del profilo di prodotto | `AI Assistant in AEM` (o il tuo nome descrittivo preferito) |
   | Nome visualizzato (facoltativo) | `AI Assistant` |
   | Descrizione (facoltativa) | `Product profile for managing AI Assistant in AEM access` |
   | Notifica | Imposta la configurazione in base alle preferenze della tua organizzazione |


## 2 - Abilitazione dell’autorizzazione alla knowledge del prodotto dell’Assistente IA{#enable-permission}

La procedura per l’assegnazione di autorizzazioni personalizzate ai profili di prodotto segue il flusso di lavoro standard di Adobe Cloud Manager relativo alle autorizzazioni personalizzate.

Articolo di riferimento: [Assegnare autorizzazioni personalizzate al nuovo profilo di prodotto](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-manager/content/requirements/custom-permissions#assign-permissions)

1. In Admin Console, fai clic sul nome del nuovo profilo di prodotto appena creato (`AI Assistant in AEM`)

   ![Schermata](/help/assets/assets-ai/ai-assistant-console.png)

1. Per visualizzare l’elenco delle autorizzazioni modificabili, fai clic sulla scheda **Autorizzazioni**.

1. Nell’elenco della tabella, individua l’autorizzazione `AI Assistant Product Knowledge`.

   ![Scheda Autorizzazioni dell’Assistente IA in Admin Console](/help/assets/assets-ai/ai-assistant-permission.png)

1. A destra del nome dell’autorizzazione, fai clic su ![icona a forma di matita o per la modifica](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Edit_18_N.svg).

1. Nella pagina **Modifica autorizzazioni per Assistente IA**, attiva l’opzione **Knowledge del prodotto dell’Assistente IA**.

   ![Pagina Modifica autorizzazioni per l’Assistente IA, opzione di attivazione/disattivazione della knowledge del prodotto](/help/assets/assets-ai/ai-assistant-prod-knowledge.png)

1. Nell’angolo in basso a destra della pagina, fai clic su **Salva**.

   Per il tuo profilo di prodotto è ora abilitata l’autorizzazione alla knowledge del prodotto dell’Assistente IA.


## 3 - Creazione di un nuovo gruppo di utenti (o utilizzo di un gruppo di utenti esistente){#create-user-group}

1. Effettua una delle seguenti operazioni:

>[!BEGINTABS]

>[!TAB Crea un nuovo gruppo di utenti]

1. In Admin Console, fai clic su **Utenti** > **Gruppi di utenti**.

   ![Gruppi di utenti](/help/assets/assets-ai/ai-assistant-user-groups.png)

1. Nella pagina **Gruppi utenti**, fai clic su **Nuovo gruppo di utenti**.

   ![Pulsante Nuovo gruppo di utenti nella pagina Gruppi di utenti](/help/assets/assets-ai/ai-assistant-new-user-group.png)

1. Nella pagina **Crea un nuovo gruppo di utenti**, fornisci le seguenti informazioni:

   | Opzione | Valore suggerito |
   | --- | --- |
   | Nome del gruppo di utenti | `AI Assistant in AEM` (o il tuo nome preferito) |
   | Descrizione (facoltativa) | `User group for managing AI Assistant in AEM access` |

   ![Crea un nuovo gruppo di utenti](/help/assets/assets-ai/ai-assistant-create-new-user-group.png)

1. Nell’angolo in basso a destra della pagina, fai clic su **Salva**.

>[!TAB Utilizza un gruppo di utenti esistente]

Invece di creare un nuovo gruppo, puoi utilizzare un gruppo di utenti AEM esistente se soddisfa i requisiti di accesso dell’Assistente IA.

>[!ENDTABS]

## 4 - Aggiunta di utenti al gruppo di utenti{#add-users}

1. Effettua una delle seguenti operazioni:

>[!BEGINTABS]

>[!TAB Aggiungi singoli utenti]

1. Nella pagina **Gruppi di utenti** della tabella **Nome gruppo**, fai clic sul nome del gruppo utenti appena creato o sul nome di un gruppo di utenti esistente.

   ![Pagina Gruppi di utenti che mostra il nome del gruppo di utenti dell’Assistente IA nella tabella](/help/assets/assets-ai/ai-assistant-user-group-name-in-table.png)

1. Nella pagina **Gruppi di utenti** per l’**Assistente IA in AEM**, fai clic sulla scheda **Utenti**, quindi su **Aggiungi utenti**.

   ![Assistente AI nella pagina Gruppi di utenti di AEM, con la scheda Utenti e il pulsante Aggiungi utenti](/help/assets/assets-ai/ai-assistant-add-users.png)

1. Nella pagina **`Add users to this user group`**, cerca e seleziona gli utenti che hanno bisogno di accedere all’Assistente IA in AEM.

   ![Pagina per l’aggiunta di utenti a questo gruppo di utenti](/help/assets/assets-ai/ai-assistant-add-users-to-this-group.png)

1. Nell’angolo in basso a destra della pagina, fai clic su **Salva**.
1. Ora [assegna il profilo di prodotto al gruppo di utenti](#assign-product-profile).

>[!TAB Aggiungi utenti in blocco]

Puoi utilizzare la funzione di caricamento in blocco in Admin Console.

1. Prepara un file CSV con le informazioni degli utenti.
1. Utilizza l’opzione **`Add users by CSV`** per assicurare un’aggiunta in blocco efficiente.
1. Ora [assegna il profilo di prodotto al gruppo di utenti](#assign-product-profile).

>[!ENDTABS]


## 5 - Assegnazione del profilo di prodotto al gruppo di utenti{#assign-product-profile}

Questo passaggio segue il flusso di lavoro standard di Adobe Admin Console per l’assegnazione dei profili di prodotto ai gruppi di utenti.

Articolo di riferimento: [Gestione di profili di prodotto per utenti aziendali](https://helpx.adobe.com/it/enterprise/using/manage-product-profiles.html)

1. Rimanendo nel gruppo di utenti Assistente IA in AEM creato al passaggio [4 - Aggiunta di utenti al gruppo di utenti](#add-users), fai clic sulla scheda **Profili di prodotti assegnati**.
1. Fai clic su **Assegna profilo**.

   ![Pagina del gruppo di utenti dell’Assistente IA in AEM con la scheda Profili di prodotti assegnati selezionata](/help/assets/assets-ai/ai-assistant-assign-profile.png)

1. Nella finestra di dialogo **Seleziona profili di prodotto** della pagina **Assegna prodotti e profili**, cerca e seleziona il profilo di prodotto **Assistente IA**.

   ![Pagina “Assegna prodotti e profili” in cui sono visualizzati la finestra di dialogo “Seleziona profili di prodotto” e il profilo di prodotto “Assistente IA” selezionato](/help/assets/assets-ai/ai-assistant-select-product-profile.png)

1. Nell’angolo in basso a destra della finestra di dialogo, fai clic su **Applica**.
1. Nell’angolo in basso a destra della pagina **Assegna prodotti e profili**, fai clic su **Salva**.

   ![Visualizzazione del profilo di prodotto Assistente IA assegnato al gruppo di utenti dell’Assistente IA in AEM](/help/assets/assets-ai/ai-assistant-profile-assigned-to-user-group.png)


## Verifica della configurazione

* Verifica che il tuo profilo di prodotto mostri il numero corretto di gruppi di utenti assegnati.
* Verifica che il gruppo di utenti mostri il numero corretto di utenti.
* Conferma che l’autorizzazione alla knowledge del prodotto dell’Assistente IA sia abilitata e configurata correttamente.


## Test della configurazione

Chiedi a un utente del gruppo assegnato di eseguire le operazioni seguenti:

1. Accedi ad AEM.
2. Verificare che le funzioni dell’Assistente IA siano accessibili.
3. Verificare la funzionalità dell’Assistente IA per assicurare un’attivazione corretta.

## Consulta anche

* [Assistente IA in AEM](/help/ai-assistant-in-aem.md)
* [Controllo degli accessi in Adobe Experience Platform](https://experienceleague.adobe.com/it/docs/experience-platform/access-control/ui/overview)
<!-- * [Cloud Manager Custom Permissions](/help/implementing/cloud-manager/custom-permissions.md) -->
