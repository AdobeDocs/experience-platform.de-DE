---
title: Datenelementtypen in der Adobe Experience Platform Web SDK Extension
description: Erfahren Sie mehr über die verschiedenen Datenelementtypen, die von der Adobe Experience Platform Web SDK Extension in Adobe Experience Platform Launch bereitgestellt werden.
translation-type: tm+mt
source-git-commit: 2a0ae9541a8bb2bb985d43a402d0842e73b23c81
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 47%

---


# Datenelementtypen

Nachdem Sie die Aktionstypen [in der [Adobe Experience Platform Web SDK-Erweiterung](web-sdk-extension.md) für [Adobe Experience Platform Launch](https://experienceleague.adobe.com/docs/launch.html) festgelegt haben, konfigurieren Sie die Datenelementtypen.](action-types.md)

Auf dieser Seite werden die verfügbaren Datenelementtypen beschrieben.

## Zusammenführungs-ID eines Ereignisses

Dieses Datenelement stellt die Zusammenführungs-ID eines Ereignisses bereit, falls verwendet. Für dieses Datenelement ist keine Konfiguration erforderlich. Das bereitgestellte Datenelement bleibt unverändert, bis entweder der Besucher die Seite verlässt oder der Aktionstyp „Zusammenführungs-ID des Ereignisses zurücksetzen“ verwendet wird.

## Identitätszuordnung

Mit dem Datenelement „Identitätszuordnung“ können Sie Identitäten aus anderen Datenelementen oder anderen von Ihnen angegebenen Werten erstellen. Alle von Ihnen erstellten Identitäten müssen an einen entsprechenden Namensraum zurückgebunden werden. Dieses Datenelement bietet eine Dropdown-Liste mit allen Standardeinstellungen und allen von Ihnen erstellten Namensräumen.

![](./assets/identity-map-data-element.png)

## XDM-Objekt

Verwenden Sie das XDM-Format, um Daten an das Adobe Experience Platform Web SDK zu senden. Die Formatierung Ihrer Daten ist nämlich mit dem XDM-Objektdatenelement einfacher. Wenn Sie dieses Datenelement zum ersten Mal öffnen, wählen Sie die richtige Adobe Experience Platform-Sandbox und das richtige Schema aus. Nachdem Sie Ihr Schema ausgewählt haben, sehen Sie die Struktur Ihres Schemas, die Sie einfach ausfüllen können.

![](./assets/XDM-object.png)

Beachten Sie, dass beim Öffnen bestimmter Felder Ihres Schemas wie `web.webPageDetails.URL` einige Elemente automatisch erfasst werden. Obwohl mehrere Elemente automatisch erfasst werden, können Sie bei Bedarf alle Elemente überschreiben. Alle Werte können manuell oder mithilfe anderer Datenelemente ausgefüllt werden.

>[!NOTE]
>
>Füllen Sie nur die Informationen aus, die Sie sammeln möchten. Alles, was nicht ausgefüllt wird, wird weggelassen, wenn die Daten an die Lösungen gesendet werden.
