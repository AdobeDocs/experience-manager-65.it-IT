---
title: Integrazione con Adobe Sign | Gestione dei dati utente
seo-title: Integrazione con Adobe Sign | Gestione dei dati utente
description: Integrazione con Adobe Sign | Gestione dei dati utente
uuid: cb3a455d-2e33-44c8-8f71-3a7ecd939cd8
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e9e0d8fb-955e-4021-9e9a-9c95c6ffe88d
feature: Adobe Sign
role: Admin
exl-id: b43ed9b7-b1ef-4878-ae3b-643b558eed7b
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 0%

---

# Integrazione con Adobe Sign | Gestione dei dati utente {#integration-with-adobe-sign-handling-user-data}

[!DNL AEM Forms] si integra [!DNL  Adobe Sign] con per abilitare i flussi di lavoro di firma elettronica in moduli adattivi per elaborare moduli o accordi per flussi di lavoro legali, di vendita, di retribuzione, di gestione delle risorse umane. Consente la firma di utenti singoli e multipli, flussi di lavoro di firma sequenziali e simultanei, la firma di moduli come utente anonimo o connesso e diversi modi per autenticare gli utenti.

Quando un firmatario o più firmatari firmano e inviano un modulo adattivo, viene generato un accordo [!DNL Adobe Sign] che include informazioni sui firmatari.

Per ulteriori informazioni sull&#39; [!DNL AEM Forms] integrazione con [!DNL Adobe Sign], consulta [Utilizzo di Adobe Sign in un modulo adattivo](/help/forms/using/working-with-adobe-sign.md).

## Archiviazione dati e dati utente {#data}

[!DNL Adobe Sign] il modulo adattivo abilitato include informazioni sui firmatari e può includere altri dati utente raccolti dal modulo adattivo. Il servizio [!DNL Adobe Sign] salva i dati utente con la firma all’interno del contratto. Il contratto viene salvato sul server [!DNL Adobe Sign] configurato in [!DNL AEM Forms] cloud services. Inoltre, se il modulo adattivo è configurato per utilizzare l’azione di invio di Forms Portal, i dati del contratto vengono salvati nell’archivio dati del portale dei moduli insieme ai dati del modulo.

## Accedere ed eliminare i dati utente {#access-and-delete-user-data}

I dati utente vengono raccolti all&#39;interno del contratto ma non vengono salvati in nessuna delle tabelle del servizio. [!DNL Adobe Sign] consente agli amministratori di effettuare le proprie scelte sulla gestione dei dati che controllano nel servizio. Gli amministratori della privacy sul servizio [!DNL Adobe Sign] possono elencare o rimuovere gli accordi in base all&#39;indirizzo e-mail di un richiedente.

[!DNL Adobe Sign] offre un&#39;applicazione web che consente la ricerca di accordi da parte dei partecipanti e, se necessario, l&#39;eliminazione. Per ulteriori informazioni, consulta [Adobe Sign - Funzionalità: Elimina informazioni utente](https://helpx.adobe.com/sign/help/adobesign_gdpr_user_deletion.html).

I dati dei contratti per i moduli adattivi configurati per utilizzare l’azione di invio del portale Forms vengono salvati anche nell’archivio dati del portale dei moduli. Per accedere e eliminare i dati dall’archivio dati del portale dei moduli, vedere [Portale Forms | Gestione dei dati utente](/help/forms/using/forms-portal-handling-user-data.md).
