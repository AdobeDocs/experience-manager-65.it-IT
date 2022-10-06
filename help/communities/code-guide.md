---
title: Linee guida sulla codifica
seo-title: Coding Guidelines
description: Linee guida, suggerimenti e trucchi per gli sviluppatori di Communities
seo-description: Communities developer guidelines, tips, and tricks
uuid: 311ef4f7-7f2c-44c3-bcf2-f68713752623
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 244cd43c-a573-495d-b80c-b97ba9d19b75
exl-id: a23aab83-1dfa-4d91-9b6b-6246a2103896
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 1%

---

# Linee guida sulla codifica {#coding-guidelines}

## Linee guida, suggerimenti {#guidelines-tips-and-tricks}

L’utilizzo di AEM Communities si è evoluto, passando dall’essere fortemente dipendente dalle pagine Java Server alla flessibilità nella scelta di modelli di linguaggi di script in cui la logica di business, lo stile e il contenuto di pagina sono diversi l’uno dall’altro.

L&#39;ulteriore flessibilità nell&#39;utilizzo dei contenuti generati dagli utenti (UGC) è attraverso l&#39;API SocialResourceProvider, che elimina la necessità di esserne consapevoli [SRP](srp.md) opzione selezionata per la distribuzione.

Di seguito sono riportate diverse linee guida per la codifica e best practice per gli sviluppatori AEM Communities:

### Codice {#code}

* [Accesso a UGC con SRP](accessing-ugc-with-srp.md) - come evitare di scrivere un&#39;applicazione che funziona solo quando UGC è memorizzato in JCR (JSRP).
* [Refactoring di SocialUtils](socialutils.md) - metodi di utilità per SRP che sostituiscono SocialUtils.
* [Convenzioni di denominazione](naming-conventions.md) - convenzioni di denominazione per classi Java personalizzate.

### Script {#scripts}

* [Caricamento in parallelo dei componenti di Communities](sideloading.md) - come aggiungere dinamicamente un componente dopo il caricamento della pagina.
* [Nozioni di base sull’editor Rich Text](rte.md) - come personalizzare l’interfaccia RTF fornita ai membri per la pubblicazione dei contenuti.

### IDE {#ide}

* [Utilizzo di Maven per Communities](maven.md) - come includere il jar API di Communities.
* [Refactoring di SocialUtils](socialutils.md) - metodi di utilità per SRP che sostituiscono SocialUtils.
