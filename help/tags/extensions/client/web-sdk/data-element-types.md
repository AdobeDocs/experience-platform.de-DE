---
title: Datenelementtypen in der Adobe Experience Platform Web SDK-Erweiterung
description: Erfahren Sie mehr über die verschiedenen Datenelementtypen, die von der Tag-Erweiterung "Adobe Experience Platform Web SDK" bereitgestellt werden.
exl-id: 3c2c257f-1fbc-4722-8040-61ad19aa533f
source-git-commit: e34a9ee5b1a09ff3391e5b0e981215fefbc157fc
workflow-type: tm+mt
source-wordcount: '653'
ht-degree: 5%

---


# Datenelementtypen

Nachdem Sie Ihre [Aktionstypen](action-types.md) in der Tag-Erweiterung [Adobe Experience Platform Web SDK](web-sdk-extension-configuration.md) festgelegt haben, müssen Sie Ihre Datenelementtypen konfigurieren. Auf dieser Seite werden die verfügbaren Datenelementtypen beschrieben.

## Identitätszuordnung {#identity-map}

Mit einer Identitätszuordnung können Sie Identitäten für den Besucher Ihrer Web-Seite festlegen. Eine Identitätszuordnung besteht aus Namespaces wie `CRMID`, `Phone` oder `Email`, wobei jeder Namespace eine oder mehrere IDs enthält. Wenn beispielsweise die Person auf Ihrer Website zwei Telefonnummern bereitgestellt hat, sollte Ihr Telefonnamespace zwei Kennungen enthalten.

Im Datenelement [!UICONTROL Identitätszuordnung] geben Sie die folgenden Informationen für jede Kennung an:

* **[!UICONTROL ID]**: Der Wert, der den Besucher identifiziert. Wenn die Kennung beispielsweise zum Namespace &quot;_&quot; gehört_ kann die [!UICONTROL ID] &quot;_55-555-5555“_. Dieser Wert wird normalerweise von einer JavaScript-Variablen oder einem anderen Datenelement auf Ihrer Seite abgeleitet. Daher ist es am besten, ein Datenelement zu erstellen, das auf die Seitendaten verweist und dann auf das Datenelement im [!UICONTROL ID]-Feld im Datenelement [!UICONTROL Identitätszuordnung] verweist. Wenn der ID-Wert bei der Ausführung auf Ihrer Seite alles andere als eine ausgefüllte Zeichenfolge ist, wird die Kennung automatisch aus der Identitätszuordnung entfernt.
* **[!UICONTROL Authentifizierter Status]**: Eine Auswahl, die angibt, ob der Besucher authentifiziert ist.
* **[!UICONTROL Primär]**: Eine Auswahl, die angibt, ob die Kennung als primäre Kennung für die Einzelperson verwendet werden soll. Wenn keine Kennung als primär markiert ist, wird die ECID als primäre Kennung verwendet.

![UI-Bild, das den Bildschirm Datenelement bearbeiten anzeigt.](assets/identity-map-data-element.png)

>[!TIP]
>
>Adobe empfiehlt, Identitäten zu senden, die eine Person darstellen, z. B. `Luma CRM Id` als primäre Identität.
>
>Wenn die Identitätszuordnung die Personenkennung enthält (z. B. `Luma CRM Id`), wird die Personenkennung zur primären Kennung. Andernfalls wird `ECID` zur primären Identität.

Beim Erstellen einer Identitätszuordnung sollten Sie keine [!DNL ECID] angeben. Bei Verwendung der SDK wird automatisch eine [!DNL ECID] auf dem Server generiert und in die Identitätszuordnung aufgenommen.

Das Identitätszuordnungs-Datenelement wird häufig zusammen mit dem [[!UICONTROL XDM-Objekt] Datenelementtyp ](#xdm-object) dem Aktionstyp [[!UICONTROL Einverständnis festlegen] verwendet](action-types.md#set-consent).

Lesen Sie mehr über [Adobe Experience Platform Identity Service](../../../../identity-service/home.md).

## XDM-Objekt {#xdm-object}

Das Formatieren Ihrer Daten in XDM ist mit dem XDM-Objektdatenelement einfacher. Wenn Sie dieses Datenelement zum ersten Mal öffnen, wählen Sie die richtige Adobe Experience Platform-Sandbox und das richtige Schema aus. Nachdem Sie Ihr Schema ausgewählt haben, sehen Sie die Struktur Ihres Schemas, die Sie einfach ausfüllen können.

![UI-Bild, das die XDM-Objektstruktur anzeigt.](assets/XDM-object.png)

Beachten Sie, dass beim Öffnen bestimmter Felder Ihres Schemas, z. B. `web.webPageDetails.URL`, einige Elemente automatisch erfasst werden. Obwohl mehrere Elemente automatisch erfasst werden, können Sie bei Bedarf alle überschreiben. Alle Werte können manuell oder mithilfe anderer Datenelemente ausgefüllt werden.

>[!NOTE]
>
>Füllen Sie nur die Informationen aus, die Sie sammeln möchten. Alles, was nicht ausgefüllt ist, wird weggelassen, wenn die Daten an die Lösungen gesendet werden.

## Variable {#variable}

Sie können Payload-Objekte mit dem Datenelement **[!UICONTROL Variable]** erstellen. Sowohl [!UICONTROL XDM]- als [!UICONTROL Data]-Objekte werden unterstützt.

* Wenn Sie [!UICONTROL XDM] auswählen, wählen Sie die gewünschte [!UICONTROL Sandbox] und [!UICONTROL Schema] aus.
* Wählen Sie bei [!UICONTROL  Option ] die gewünschten Lösungen aus. Zu den verfügbaren Lösungen gehören [!UICONTROL Adobe Analytics] und [!UICONTROL Adobe Target].

![Bild der Tags-Benutzeroberfläche mit den Datenelementoptionen.](assets/variable-data-element.png)

Nachdem Sie dieses Datenelement erstellt haben, können Sie die Aktion [Variable aktualisieren](./action-types.md#update-variable) verwenden, um es zu ändern. Wenn Sie bereit sind, können Sie dieses Datenelement in die Aktion [Ereignis senden](./action-types.md#send-event) einbeziehen, um Daten an einen Datenstrom zu senden.

## Medien: Erlebnisqualität {#quality-experience}

Ein **[!UICONTROL Quality of Experience]**-Datenelement ist beim Senden von Streaming-Medienereignissen an Adobe Experience Platform hilfreich. Sie können dieses Element beim Erstellen einer Mediensitzung hinzufügen. Die folgenden Medienereignisse enthalten aktualisierte Daten zur Erlebnisqualität.

![UI-Bild, das den Bildschirm Qualität des Experience-Datenelements erstellen zeigt.](assets/qoe-data-element.png)

## Nächste Schritte {#next-steps}

Erfahren Sie mehr über bestimmte Anwendungsfälle wie [Zugriff auf die ECID](accessing-the-ecid.md).
