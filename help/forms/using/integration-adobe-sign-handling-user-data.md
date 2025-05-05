---
title: Integrazione con Adobe Sign | Gestione dei dati utente
description: Scopri l’integrazione di AEM Forms con Adobe Sign per le firme elettroniche nei moduli adattivi. Supporta più opzioni di firma per vari flussi di lavoro.
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: Acrobat Sign
role: Admin, User, Developer
exl-id: b43ed9b7-b1ef-4878-ae3b-643b558eed7b
solution: Experience Manager, Experience Manager Forms
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 0%

---

# Integrazione con Adobe Sign | Gestione dei dati utente {#integration-with-adobe-sign-handling-user-data}

[!DNL AEM Forms] si integra con [!DNL &#x200B; Adobe Sign] per abilitare i flussi di lavoro di firma elettronica nei moduli adattivi per elaborare moduli o accordi per flussi di lavoro legali, di vendita, di gestione delle retribuzioni e delle risorse umane. Consente la firma singola e multiutente, flussi di lavoro sequenziali e simultanei, la firma dei moduli come utente anonimo o connesso e diversi modi per autenticare gli utenti.

Quando uno o più firmatari firmano e inviano un modulo adattivo, viene generato un contratto [!DNL Adobe Sign] che include informazioni sui firmatari.

Per ulteriori informazioni sull&#39;integrazione di [!DNL AEM Forms] con [!DNL Adobe Sign], vedere [Utilizzo di Adobe Sign in un modulo adattivo](/help/forms/using/working-with-adobe-sign.md).

## Dati utente e archivi dati {#data}

Il modulo adattivo abilitato per [!DNL Adobe Sign] include informazioni sui firmatari e può includere altri dati utente raccolti dal modulo adattivo. Il servizio [!DNL Adobe Sign] salva i dati utente con la firma all&#39;interno dell&#39;accordo. Il contratto viene salvato su un server [!DNL Adobe Sign] configurato in [!DNL AEM Forms] servizi cloud. Inoltre, se il modulo adattivo è configurato per l’utilizzo dell’azione di invio Forms Portal, i dati dell’accordo vengono salvati nell’archivio dati di Forms Portal insieme ai dati del modulo.

## Accedere ed eliminare i dati utente {#access-and-delete-user-data}

I dati utente vengono raccolti all&#39;interno del contratto ma non vengono salvati in nessuna delle tabelle del servizio. [!DNL Adobe Sign] consente agli amministratori di effettuare le proprie scelte sulla gestione dei dati controllati nel servizio. Gli amministratori della privacy nel servizio [!DNL Adobe Sign] possono elencare o rimuovere accordi in base all&#39;indirizzo e-mail di un richiedente.

[!DNL Adobe Sign] offre un&#39;applicazione Web che consente la ricerca di accordi da parte dei partecipanti e, se necessario, la loro eliminazione. Per ulteriori informazioni, vedere [Adobe Sign - Funzionalità: Elimina informazioni utente](https://helpx.adobe.com/sign/help/adobesign_gdpr_user_deletion.html).

I dati dei contratti per i moduli adattivi configurati per l’utilizzo dell’azione di invio di Forms Portal vengono salvati anche nell’archivio dati di Forms Portal. Per accedere ed eliminare dati dall&#39;archivio dati di Forms Portal, vedere [Forms Portal | Gestione dei dati utente](/help/forms/using/forms-portal-handling-user-data.md).
