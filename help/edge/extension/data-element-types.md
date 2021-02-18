---
title: Datenelementtypen in der Adobe Experience Platform Web SDK Extension
description: Erfahren Sie mehr über die verschiedenen Datenelementtypen, die von der Adobe Experience Platform Web SDK Extension in Adobe Experience Platform Launch bereitgestellt werden.
translation-type: tm+mt
source-git-commit: 69f2e6069546cd8b913db453dd9e4bc3f99dd3d9
workflow-type: tm+mt
source-wordcount: '318'
ht-degree: 78%

---


# Datenelementtypen

Nachdem Sie die Aktionstypen [in der [Adobe Experience Platform Web SDK-Erweiterung](web-sdk-extension.md) für [Adobe Experience Platform Launch](https://experienceleague.adobe.com/docs/launch.html) festgelegt haben, konfigurieren Sie die Datenelementtypen.](action-types.md)

Auf dieser Seite werden die verfügbaren Datenelementtypen beschrieben.

## Zusammenführungs-ID eines Ereignisses

Dieses Datenelement stellt die Zusammenführungs-ID eines Ereignisses bereit, falls verwendet. Für dieses Datenelement ist keine Konfiguration erforderlich. Das bereitgestellte Datenelement bleibt unverändert, bis entweder der Besucher die Seite verlässt oder der Aktionstyp „Zusammenführungs-ID des Ereignisses zurücksetzen“ verwendet wird.

## Identitätszuordnung

Mit dem Datenelement „Identitätszuordnung“ können Sie Identitäten aus anderen Datenelementen oder anderen von Ihnen angegebenen Werten erstellen. Alle von Ihnen erstellten Identitäten müssen an einen entsprechenden Namensraum zurückgebunden werden. Dieses Datenelement bietet eine Dropdown-Liste, die alle standardmäßigen Namensräume sowie alle von Ihnen erstellten Namensräume anzeigt.

![](./assets/identity-map-data-element.png)

## XDM-Objekt

Alle Daten, die Sie an das Adobe Experience Platform Web SDK senden, sollten im XDM-Format vorliegen. Die Formatierung Ihrer Daten ist nämlich mit dem XDM-Objektdatenelement einfacher. Wenn Sie dieses Datenelement zum ersten Mal öffnen, wählen Sie die richtige Adobe Experience Platform-Sandbox und das richtige Schema aus. Nachdem Sie Ihr Schema ausgewählt haben, sehen Sie dessen Struktur, die Sie einfach ausfüllen können.

![](./assets/XDM-object.png)

Beachten Sie, dass beim Öffnen bestimmter Felder Ihres Schemas wie `web.webPageDetails.URL` einige Elemente automatisch erfasst werden. Auch wenn mehrere Elemente automatisch erfasst werden, haben Sie die Möglichkeit, bei Bedarf alle Elemente zu überschreiben. Alle Werte können manuell oder mithilfe anderer Datenelemente ausgefüllt werden.

>[!NOTE]
>
>Sie brauchen nur die Informationen einzutragen, die Sie sammeln möchten. Alles, was nicht ausgefüllt ist, wird ausgelassen, wenn die Daten an die Lösungen gesendet werden.
