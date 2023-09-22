---
title: Integrazione con Adobe Sign | Gestione dei dati utente
description: Integrazione con Adobe Sign | Gestione dei dati utente
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: Acrobat Sign
role: Admin
exl-id: b43ed9b7-b1ef-4878-ae3b-643b558eed7b
source-git-commit: f7b24617dec77c6907798b1615debdc2329c9d80
workflow-type: tm+mt
source-wordcount: '310'
ht-degree: 0%

---

# Integrazione con Adobe Sign | Gestione dei dati utente {#integration-with-adobe-sign-handling-user-data}

[!DNL AEM Forms] si integra con[!DNL  Adobe Sign] per consentire ai flussi di lavoro di firma elettronica nei moduli adattivi di elaborare moduli o accordi per flussi di lavoro legali, di vendita, di gestione delle retribuzioni e delle risorse umane. Consente la firma singola e multiutente, flussi di lavoro sequenziali e simultanei, la firma dei moduli come utente anonimo o connesso e diversi modi per autenticare gli utenti.

Quando uno o più firmatari firmano e inviano un modulo adattivo, un [!DNL Adobe Sign] viene generato un contratto che include informazioni sui firmatari.

Per ulteriori informazioni su [!DNL AEM Forms] integrazione con [!DNL Adobe Sign], vedi [Utilizzo di Adobe Sign in un modulo adattivo](/help/forms/using/working-with-adobe-sign.md).

## Dati utente e archivi dati {#data}

[!DNL Adobe Sign] il modulo adattivo abilitato include informazioni sui firmatari e può includere altri dati utente raccolti dal modulo adattivo. Il [!DNL Adobe Sign] Il servizio salva i dati utente con la firma all&#39;interno del contratto. Il contratto viene salvato su [!DNL Adobe Sign] server configurato in [!DNL AEM Forms] servizi cloud. Inoltre, se il modulo adattivo è configurato per l’utilizzo dell’azione di invio Forms Portal, i dati dell’accordo vengono salvati nell’archivio dati di Forms Portal insieme ai dati del modulo.

## Accedere ed eliminare i dati utente {#access-and-delete-user-data}

I dati utente vengono raccolti all&#39;interno del contratto ma non vengono salvati in nessuna delle tabelle del servizio. [!DNL Adobe Sign] consente agli amministratori di effettuare le proprie scelte in merito alla gestione dei dati che controllano nel servizio. Amministratori della privacy sulla [!DNL Adobe Sign] Il servizio può elencare o rimuovere contratti in base all&#39;indirizzo e-mail di un richiedente.

[!DNL Adobe Sign] offre un’applicazione web che consente di cercare gli accordi dei partecipanti e, se necessario, eliminarli. Per ulteriori informazioni, consulta [Adobe Sign - Funzionalità: Cancella Informazioni Utente](https://helpx.adobe.com/sign/help/adobesign_gdpr_user_deletion.html).

I dati dei contratti per i moduli adattivi configurati per l’utilizzo dell’azione di invio di Forms Portal vengono salvati anche nell’archivio dati di Forms Portal. Per accedere ed eliminare dati dall&#39;archivio dati di Forms Portal, vedere [Forms Portal | Gestione dei dati utente](/help/forms/using/forms-portal-handling-user-data.md).
