---
title: Creazione di una nuova schermata di login
seo-title: Creazione di una nuova schermata di login
description: Come modificare la pagina di login dei moduli di LiveCycle, ad esempio l’area di lavoro AEM Forms o Forms Manager.
seo-description: Come modificare la pagina di login dei moduli di LiveCycle, ad esempio l’area di lavoro AEM Forms o Forms Manager.
uuid: 2d4a72f4-cc9a-412d-856d-0fca75f1272b
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 35497785-263d-44b1-9ee4-85921997295b
docset: aem65
translation-type: tm+mt
source-git-commit: 9fcfd1c2c63d9a32f2d68f5b0c974bc5b5d22b40
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 5%

---


# Creazione di una nuova schermata di login{#creating-a-new-login-screen}

Potete modificare la schermata di login di tutti i moduli AEM Forms che utilizzano la schermata di login dei AEM Forms. Ad esempio, le modifiche influiscono sulla schermata di accesso dell’area di lavoro di Forms Manager e AEM Forms.

## Prerequisito {#prerequisite}

1. Effettuate l&#39;accesso `/lc/crx/de` con le autorizzazioni di amministratore.
1. Effettuare le seguenti operazioni:

   1. Replicare la struttura gerarchica: di `/libs/livecycle/core/content` a `/apps/livecycle/core/content`.

      Mantenere le stesse proprietà (nodo/cartella) e il controllo di accesso.

   1. Copiate la cartella del contenuto:

      da: `/libs/livecycle/core`

      a: `/apps/livecycle/core`.

   1. Eliminate il contenuto della `/apps/livecycle/core` cartella.

1. Effettuare le seguenti operazioni:

   1. Replicare la struttura gerarchica: di `/libs/livecycle/core/components/login` a `/apps/livecycle/core/components/login`. Mantenere le stesse proprietà (nodo/cartella) e il controllo di accesso.

   1. Copiate la cartella dei componenti: da `/libs/livecycle/core` a `/apps/livecycle/core`.

   1. Eliminate il contenuto della cartella: `/apps/livecycle/core/components/login`.

### Aggiunta di una nuova lingua {#adding-a-new-locale}

1. Copiate la `i18n` cartella:

   * da `/libs/livecycle/core/components/login`
   * a `/apps/livecycle/core/components/login`

1. Eliminate tutte le cartelle all&#39;interno `i18n` tranne una, ad esempio `en`.

1. Nella cartella `en`, effettuate le seguenti operazioni:

   1. Rinominare la cartella con il nome delle impostazioni internazionali da supportare. Esempio, `ar`.

   1. Modificate il valore della proprietà `jcr:language` in `ar`(per la `ar` cartella).
   >[!NOTE]
   >
   >Se l&#39;impostazione internazionale è una combinazione di codice paese lingua, ad esempio `ar-DZ`, modificare il nome della cartella e il valore della proprietà in `ar-DZ`.

1. Copia `login.jsp`:

   * da `/libs/livecycle/core/components/login`
   * a `/apps/livecycle/core/components/login`

1. Modificate il frammento di codice seguente per `/apps/livecycle/core/components/login/login.jsp`:

***Lingua è il codice della lingua***

```jsp
String browserLocale = "en";

    for(int i=0; i<locales.length; i++)
    {
        String prioperty = locales[i];
        if(prioperty.trim().startsWith("en")) {
            browserLocale = "en";
            break;
        }
        if(prioperty.trim().startsWith("de")){
            browserLocale = "de";
            break;
        }
        if(prioperty.trim().startsWith("ja")){
            browserLocale = "ja";
            break;
        }
        if(prioperty.trim().startsWith("fr")){
            browserLocale = "fr";
            break;
        }
    }
```

A

```jsp
String browserLocale = "en";
    for(int i=0; i<locales.length; i++)
    {
        String prioperty = locales[i];
        if(prioperty.trim().startsWith("ar")) {
            browserLocale = "ar";
            break;
        }
        if(prioperty.trim().startsWith("en")) {
            browserLocale = "en";
            break;
        }
        if(prioperty.trim().startsWith("de")){
            browserLocale = "de";
            break;
        }
        if(prioperty.trim().startsWith("ja")){
            browserLocale = "ja";
            break;
        }
        if(prioperty.trim().startsWith("fr")){
            browserLocale = "fr";
            break;
        }
    }
```

```jsp
String browserLocale = "en";

    for(int i=0; i<locales.length; i++)
    {
        String prioperty = locales[i];
        if(prioperty.trim().startsWith("en")) {
            browserLocale = "en";
            break;
        }
        if(prioperty.trim().startsWith("de")){
            browserLocale = "de";
            break;
        }
        if(prioperty.trim().startsWith("ja")){
            browserLocale = "ja";
            break;
        }
        if(prioperty.trim().startsWith("fr")){
            browserLocale = "fr";
            break;
        }
    }
```

A

```jsp
String browserLocale = "en";
    for(int i=0; i<locales.length; i++)
    {
        String prioperty = locales[i];
        if(prioperty.trim().equalsIgnoreCase("ar-DZ")) {
            browserLocale = "ar-DZ";
            break;
        }
        if(prioperty.trim().startsWith("en")) {
            browserLocale = "en";
            break;
        }
        if(prioperty.trim().startsWith("de")){
            browserLocale = "de";
            break;
        }
        if(prioperty.trim().startsWith("ja")){
            browserLocale = "ja";
            break;
        }
        if(prioperty.trim().startsWith("fr")){
            browserLocale = "fr";
            break;
        }
    }
```

***Per modificare le impostazioni internazionali predefinite***

```jsp
   String browserLocale = "en";
   for(int i=0; i<locales.length; i++)

   To

   String browserLocale = "ar";
   for(int i=0; i<locales.length; i++)
```

### Aggiunta di nuovo testo o modifica di testo esistente {#adding-new-text-or-modifying-existing-text}

1. Copia `i18n` cartella:

   * da `/libs/livecycle/core/components/login`
   * a `/apps/livecycle/core/components/login`

1. A questo punto, modificate il valore della proprietà `sling:message` del nodo (nella cartella del codice lingua desiderata) per il quale desiderate modificare il testo. La conversione viene eseguita tramite la chiave indicata nel valore della `sling:key` proprietà del nodo.

1. Per aggiungere una nuova coppia chiave-valore, effettuare le seguenti operazioni. Controllate un esempio nello screenshot che segue.

   1. Creare un nodo di tipo `sling:MessageEntry`, o copiare un nodo esistente e rinominarlo, in tutte le cartelle delle impostazioni internazionali.
   1. Copia `login.jsp` :

      * da `/libs/livecycle/core/components/login`

      * a `/apps/livecycle/core/components/login`
   1. Modificate `/apps/livecycle/core/components/login/login.jsp` per incorporare il testo appena aggiunto.

   ![Aggiungi nuova coppia chiave-valore](assets/capture_new.png)

   ```jsp
   div class="loginContent">
   
                       <span class="loginFlow"></code>
                       <span class="loginVersion"><%= i18n.get("Version: 11.0.0") %></code>
                       <span class="loginTitle"><%= i18n.get("Login") %></code>
                       <% if (loginFailed) {%>
   ```

   A

   ```jsp
   div class="loginContent">
   
                       <span class="loginFlow"></code>
                       <span class="loginVersion"><%= i18n.get("My Welcome Message") %></code>
                       <span class="loginVersion"><%= i18n.get("Version: 11.0.0") %></code>
                       <span class="loginTitle"><%= i18n.get("Login") %></code>
                       <% if (loginFailed) {%>
   ```

### Aggiunta di nuovo stile o modifica di uno stile esistente {#adding-new-style-or-modifying-existing-style}

1. Copy `login` node:

   * da `/libs/livecycle/core/content`
   * a `/apps/livecycle/core/content`

1. Eliminare file `login.js` e `jquery-1.8.0.min.js`, dal nodo `/apps/livecycle/core/content/login.`
1. Modificate gli stili nel file CSS.
1. Per aggiungere nuovi stili:

   1. Aggiungi nuovi stili a `/apps/livecycle/core/content/login/login.css`
   1. Copia `login.jsp`

      * da `/libs/livecycle/core/components/login`

      * a `/apps/livecycle/core/components/login`
   1. Modificate `/apps/livecycle/core/components/login/login.jsp` per incorporare i nuovi stili aggiunti.



Ad esempio:

* Aggiungi quanto segue a `/apps/livecycle/core/content/login/login.css`.

```
css.newLoginContentArea {
    width: 700px;
    padding: 100px 0px 0px 100px;
   }
```

* Modificate quanto segue in `/apps/livecycle/core/components/login.jsp`.


   ```jsp
   <div class="loginContentArea">
   ```

   A

   ```jsp
   <div class="newLoginContentArea">
   ```

>[!NOTE]
>
>Se le immagini esistenti in `/apps/livecycle/core/content/login` (copiate da `/libs/livecycle/core/content/login`) vengono rimosse, rimuovete i riferimenti corrispondenti in CSS.

### Aggiungere nuove immagini {#add-new-images}

1. Seguire i passaggi per aggiungere nuovo stile o modificare lo stile esistente (documentato sopra).
1. Aggiungere nuove immagini in `/apps/livecycle/core/content/login`. Per aggiungere un&#39;immagine:

   1. Installare il client WebDAV.
   1. Andate alla `/apps/livecycle/core/content/login` cartella, utilizzando il client webDAV. Per ulteriori informazioni, vedi: [https://dev.day.com/docs/en/crx/current/how_to/webdav_access.html](https://docs.adobe.com/docs/en/crx/current/how_to/webdav_access.html).

   1. Aggiungete nuove immagini.

1. Aggiungete nuovi stili in `/apps/livecycle/core/content/login/login.css,` base alle nuove immagini aggiunte in `/apps/livecycle/core/content/login`.
1. Utilizzate i nuovi stili in `login.jsp` in `/apps/livecycle/core/components`.

Ad Esempio:


```css
.newLoginContainerBkg {

 background-image: url(my_Bg.gif);
 background-repeat: no-repeat;
 background-position: left top;
 width: 727px;
}
```


    * Modificate quanto segue in /apps/livecycle/core/components/login.jsp.

```jsp
<div class="loginContainerBkg">
```

A

```jsp
<div class="newLginContainerBkg">
```
