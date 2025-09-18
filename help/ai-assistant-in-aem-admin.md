---
title: Configurare l’Assistente IA in AEM
description: Scopri come impostare e configurare l’Assistente AI utilizzando Admin Console in Adobe Experience Manager.
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
exl-id: 06824b3d-f912-4922-8fb6-ee2ca04c6326
source-git-commit: 1aa70fc14e41ce4dd76be206723e8a44856e8c09
workflow-type: tm+mt
source-wordcount: '1148'
ht-degree: 4%

---

# Configurare l’Assistente IA in AEM {#aem-ai-asst-admin-setup}

<!-- An Administrator must configure access, permissions, and settings before users in their organization can use the features in AI Assistant in AEM. -->

<!-- badge: label="Beta" type="Positive" -->

Per utilizzare l’Assistente all’intelligenza artificiale in AEM (Adobe Experience Manager), è necessario disporre dell’autorizzazione per accedere alla conoscenza del prodotto tramite l’Assistente all’intelligenza artificiale. Questa autorizzazione è attivata per impostazione predefinita.

Se desideri controllare chi può accedere alla conoscenza del prodotto, invia un&#39;e-mail a [aemaiassistant@adobe.com](mailto:aemaiassistant@adobe.com) dal tuo indirizzo e-mail associato al tuo Adobe ID. Adobe può abilitare il controllo degli accessi a livello di utente. Quando è abilitato, l’amministratore può concedere l’accesso a livello di utente seguendo i passaggi descritti di seguito.

Se hai richiesto il controllo degli accessi a livello di utente, la tua organizzazione deve dare il consenso tramite Adobe Admin Console. Un amministratore di prodotto crea (o sceglie) un gruppo di utenti e gli concede la nuova autorizzazione &quot;Assistente IA&quot;. Chiunque sia aggiunto a quel gruppo ha accesso istantaneamente all’Assistente all’intelligenza artificiale in AEM. Se l’obiettivo è la disponibilità a livello aziendale, l’amministratore assegna semplicemente tutti gli utenti a quel gruppo.

Dal punto di vista di un dipendente, il processo è semplice: identifica l’amministratore del prodotto per Adobe Experience Manager nella tua organizzazione e richiede di essere aggiunto al gruppo di utenti abilitato all’intelligenza artificiale. Una volta visualizzato in tale gruppo, l&#39;icona Assistente viene visualizzata automaticamente al successivo accesso.

Gli amministratori devono tenere presente la normale governance di Cloud Manager. In Admin Console, tieni i diritti di amministratore del prodotto per creare profili, gestire gruppi di utenti o modificare le autorizzazioni. Se gli utenti necessitano anche della funzionalità integrata **Crea ticket di supporto** dell&#39;Assistente, aggiungere il ruolo standard **Amministratore supporto** (ruolo standard di Admin Console) agli stessi utenti o gruppi.

Il processo di configurazione di AI Assistant in AEM consiste nei seguenti passaggi:

1. [Crea un nuovo profilo di prodotto in Adobe Admin Console](#create-profile).
1. [Abilitare l&#39;autorizzazione alla conoscenza del prodotto dell&#39;Assistente all&#39;intelligenza artificiale](#enable-permission).
1. [Creare un nuovo gruppo utenti (o utilizzare un gruppo utenti esistente)](#create-user-group).
1. [Aggiungi utenti al gruppo di utenti](#add-users).
1. [Assegna il profilo di prodotto al gruppo di utenti](#assign-product-profile).

**Prerequisiti**

Prima di iniziare, assicurati di aver soddisfatto i seguenti prerequisiti:

* Devi disporre almeno dei diritti di amministratore del prodotto in Adobe Admin Console.
* Conosci la struttura di gestione degli utenti della tua organizzazione.

**Considerazioni sulla configurazione**

* Tempo di elaborazione: le risorse create in Cloud Manager potrebbero richiedere fino a 2 minuti per essere visualizzate in Admin Console per la configurazione delle autorizzazioni.
* Più profili: gli utenti possono far parte di più profili e le autorizzazioni sono combinate da tutti i profili assegnati.
* Ambito organizzazione: alcune autorizzazioni possono essere applicate a livello di organizzazione in tutti i programmi.
* Profili predefiniti: non eliminare i profili di autorizzazione predefiniti da Admin Console.


## 1 - Creare un nuovo profilo di prodotto in Adobe Admin Console{#create-profile}

1. Segui le istruzioni dettagliate in [Creare un nuovo profilo di prodotto in Adobe Admin Console](https://experienceleague.adobe.com/it/docs/experience-platform/access-control/ui/create-profile), reperibile nella documentazione di Experience Platform.

1. Quando crei il nuovo profilo di prodotto, puoi utilizzare i seguenti valori consigliati per l’Assistente IA.

   | Campo testo | Valore suggerito |
   | --- | --- |
   | Nome del profilo di prodotto | `AI Assistant in AEM` (o il tuo nome descrittivo preferito) |
   | Nome visualizzato (facoltativo) | `AI Assistant` |
   | Descrizione (facoltativo) | `Product profile for managing AI Assistant in AEM access` |
   | Notifica | Configura in base alle preferenze della tua organizzazione |


## 2 - Abilitare l’autorizzazione alla conoscenza del prodotto di AI Assistant{#enable-permission}

Il processo di assegnazione di autorizzazioni personalizzate ai profili di prodotto segue il flusso di lavoro standard delle autorizzazioni personalizzate di Adobe Cloud Manager.

Articolo di riferimento: [Assegnare autorizzazioni personalizzate al nuovo profilo di prodotto](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-manager/content/requirements/custom-permissions#assign-permissions)

1. In Admin Console, fai clic sul nome del nuovo profilo di prodotto creato (`AI Assistant in AEM`)

   ![Schermata](/help/assets/assets-ai/ai-assistant-console.png)

1. Per visualizzare l&#39;elenco delle autorizzazioni modificabili, fare clic sulla scheda **Autorizzazioni**.

1. Nell&#39;elenco della tabella individuare l&#39;autorizzazione `AI Assistant Product Knowledge`.

   ![Scheda Autorizzazioni Assistente AI in Admin Console](/help/assets/assets-ai/ai-assistant-permission.png)

1. A destra del nome dell&#39;autorizzazione, fare clic sull&#39;icona ![Matita o Modifica](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Edit_18_N.svg).

1. Nella pagina **Modifica autorizzazioni per Assistente IA**, attiva l&#39;opzione **Informazioni sul prodotto Assistente IA**.

   ![Modifica la pagina delle autorizzazioni per l&#39;opzione di attivazione/disattivazione della conoscenza del prodotto di AI Assistant](/help/assets/assets-ai/ai-assistant-prod-knowledge.png)

1. Nell&#39;angolo inferiore destro della pagina fare clic su **Salva**.

   Il tuo profilo di prodotto ora dispone dell’autorizzazione alla conoscenza del prodotto di AI Assistant abilitata.


## 3 - Creare un nuovo gruppo di utenti (o utilizzare un gruppo di utenti esistente){#create-user-group}

1. Effettua una delle seguenti operazioni:

>[!BEGINTABS]

>[!TAB Crea un nuovo gruppo di utenti]

1. In Admin Console, fai clic su **Utenti** > **Gruppi di utenti**.

   ![Gruppi di utenti](/help/assets/assets-ai/ai-assistant-user-groups.png)

1. Nella pagina **Gruppi utenti**, fare clic su **Nuovo gruppo utenti**.

   ![Pulsante Nuovo gruppo utenti nella pagina Gruppi utenti](/help/assets/assets-ai/ai-assistant-new-user-group.png)

1. Nella pagina **Crea un nuovo gruppo utenti**, fornisci le seguenti informazioni:

   | Opzione | Valore suggerito |
   | --- | --- |
   | Nome gruppo di utenti | `AI Assistant in AEM` (o il tuo nome preferito) |
   | Descrizione (facoltativo) | `User group for managing AI Assistant in AEM access` |

   ![Crea una nuova pagina gruppo utenti](/help/assets/assets-ai/ai-assistant-create-new-user-group.png)

1. Nell&#39;angolo inferiore destro della pagina fare clic su **Salva**.

>[!TAB Utilizza un gruppo di utenti esistente]

Invece di creare un nuovo gruppo, puoi utilizzare un gruppo di utenti AEM esistente se soddisfa i requisiti di accesso all’Assistente IA.

>[!ENDTABS]

## 4 - Aggiungere utenti al gruppo{#add-users}

1. Effettua una delle seguenti operazioni:

>[!BEGINTABS]

>[!TAB Aggiungi singoli utenti]

1. Nella tabella **Nome gruppo** della pagina **Gruppi utenti** fare clic sul nome del gruppo utenti appena creato o su un nome di gruppo utenti esistente.

   ![Pagina Gruppi di utenti che mostra l&#39;Assistente AI nel nome del gruppo di utenti AEM nella tabella](/help/assets/assets-ai/ai-assistant-user-group-name-in-table.png)

1. Nella pagina **Gruppi di utenti** per l&#39;Assistente di **IA in AEM**, fai clic sulla scheda **Utenti**, quindi fai clic su **Aggiungi utenti**.

   ![Assistente AI nella pagina Gruppi di utenti di AEM, con la scheda Utenti e il pulsante Aggiungi utenti](/help/assets/assets-ai/ai-assistant-add-users.png)

1. Nella pagina **`Add users to this user group`**, cerca e seleziona gli utenti che hanno bisogno di accedere all&#39;Assistente all&#39;intelligenza artificiale in AEM.

   ![Aggiungi utenti a questa pagina gruppo utenti](/help/assets/assets-ai/ai-assistant-add-users-to-this-group.png)

1. Nell&#39;angolo inferiore destro della pagina fare clic su **Salva**.
1. Ora [assegna il profilo di prodotto al gruppo di utenti](#assign-product-profile).

>[!TAB Aggiungere utenti in blocco]

Puoi utilizzare la funzione di caricamento in blocco in Admin Console.

1. Prepara un file CSV con le informazioni utente.
1. Utilizza l&#39;opzione **`Add users by CSV`** per un&#39;aggiunta in blocco efficiente.
1. Ora [assegna il profilo di prodotto al gruppo di utenti](#assign-product-profile).

>[!ENDTABS]


## 5 - Assegnare il profilo di prodotto al gruppo di utenti{#assign-product-profile}

Questo passaggio segue il flusso di lavoro standard di Adobe Admin Console per l’assegnazione di profili di prodotto ai gruppi di utenti.

Articolo di riferimento: [Gestire i profili di prodotto per gli utenti aziendali](https://helpx.adobe.com/it/enterprise/using/manage-product-profiles.html)

1. Mentre sei ancora nell&#39;Assistente all&#39;intelligenza artificiale nel gruppo di utenti di AEM da [4 - Aggiungi utenti al gruppo di utenti](#add-users), fai clic sulla scheda **Profili di prodotto assegnati**.
1. Fare clic su **Assegna profilo**.

   ![Assistente IA nella pagina gruppo di utenti di AEM con scheda Profili di prodotto assegnati selezionata](/help/assets/assets-ai/ai-assistant-assign-profile.png)

1. Nella pagina **Assegna prodotti e profili**, nella finestra di dialogo **Seleziona profili di prodotto**, cerca e seleziona il profilo di prodotto **Assistente AI**.

   ![Pagina &quot;Assegna prodotti e profili&quot;, con la finestra di dialogo &quot;Seleziona profili di prodotto&quot; e il profilo di prodotto &quot;Assistente AI&quot; selezionato](/help/assets/assets-ai/ai-assistant-select-product-profile.png)

1. Fai clic su **Applica** nell&#39;angolo inferiore destro della finestra di dialogo.
1. Fai clic su **Salva** nell&#39;angolo inferiore destro della pagina **Assegna prodotti e profili**.

   ![Profilo di prodotto Assistente IA visualizzato assegnato all&#39;Assistente IA nel gruppo di utenti di AEM](/help/assets/assets-ai/ai-assistant-profile-assigned-to-user-group.png)


## Verifica la configurazione

* Verifica che il tuo profilo di prodotto mostri il numero corretto di gruppi di utenti assegnati.
* Verifica che il gruppo di utenti mostri il numero corretto di utenti.
* Conferma che l’autorizzazione Knowledge base del prodotto di AI Assistant sia abilitata e configurata correttamente.


## Verifica la configurazione

Chiedi a un utente del gruppo assegnato di effettuare le seguenti operazioni:

1. Accedi ad AEM.
2. Verifica che le funzioni dell’Assistente AI siano accessibili.
3. Verifica la funzionalità di AI Assistant per assicurarti che venga attivata correttamente.

## Consulta anche

* [Assistente IA in AEM](/help/ai-assistant-in-aem.md)
* [Controllo dell&#39;accesso a Adobe Experience Platform](https://experienceleague.adobe.com/it/docs/experience-platform/access-control/ui/overview)
<!-- * [Cloud Manager Custom Permissions](/help/implementing/cloud-manager/custom-permissions.md) -->
