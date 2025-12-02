---
title: Konfigurationseinstellungen des Einverständnisses
description: Konfigurieren Sie die standardmäßigen Einverständnis- und Datenschutzeinstellungen für die Tag-Erweiterung.
source-git-commit: 46e5d007b27eaa67c9ee49e35a711424de383d68
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 1%

---

# Konfigurationseinstellungen des Einverständnisses

Im **[!UICONTROL Consent]** Abschnitt können Sie die Standardebene für das Einverständnis auswählen, von der ausgegangen wird, wenn keine andere explizite Einverständnisvoreinstellung angegeben wird. Die standardmäßige Einverständnisebene wird nicht in Benutzerprofilen gespeichert.

1. Melden Sie sich mit Ihren Adobe ID[Anmeldeinformationen bei ](https://experience.adobe.com)experience.adobe.com) an.
1. Navigieren Sie zu **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Wählen Sie die gewünschte Tag-Eigenschaft aus.
1. Navigieren Sie zu **[!UICONTROL Extensions]** und wählen Sie **[!UICONTROL Configure]** auf der [!UICONTROL Adobe Experience Platform Web SDK] aus.
1. Scrollen Sie nach unten zum Abschnitt **[!UICONTROL Consent]** .

![Bild mit den Datenschutzeinstellungen der Tag-Erweiterung „Web SDK&quot; in der Tags-Benutzeroberfläche](../assets/web-sdk-ext-privacy.png)

Dieser Abschnitt enthält einen einzigen Satz von Optionsfeldern, die die standardmäßige Einverständnisebene bestimmen:

* **[!UICONTROL In]**: Erfassen Sie Ereignisse, die auftreten, bevor die Benutzerin bzw. der Benutzer die Einverständnisvoreinstellungen angibt.
* **[!UICONTROL Out]**: Ereignisse ablegen, die auftreten, bevor die Benutzerin bzw. der Benutzer Einverständnisvoreinstellungen angibt.
* **[!UICONTROL Pending]**: Ereignisse in die Warteschlange stellen, die auftreten, bevor der Benutzer Einverständnisvoreinstellungen eingibt. Wenn das Einverständnis erteilt wird, werden Ereignisse in der Warteschlange an Adobe gesendet. Wenn das Einverständnis verweigert wird, werden Ereignisse in der Warteschlange verworfen.
* **[!UICONTROL Provide a data element]**: Wählen Sie ein Datenelement aus, das eine der oben genannten Konfigurationseinstellungen bestimmt. Gültige Werte sind die Zeichenfolgen `"in"`, `"out"` oder `"pending"`.

Wenn Ihr Unternehmen ein explizites Benutzereinverständnis zum Erfassen von Daten benötigt, empfiehlt Adobe, das standardmäßige Einverständnis entweder auf **[!UICONTROL Out]** oder auf **[!UICONTROL Pending]** festzulegen.
