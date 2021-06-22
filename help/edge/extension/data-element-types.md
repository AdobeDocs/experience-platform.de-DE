---
title: Datenelementtypen in der Adobe Experience Platform Web SDK-Erweiterung
description: Erfahren Sie mehr über die verschiedenen Datenelementtypen, die von der Adobe Experience Platform Web SDK-Erweiterung in Adobe Experience Platform Launch bereitgestellt werden.
exl-id: 3c2c257f-1fbc-4722-8040-61ad19aa533f
source-git-commit: 5a295a1f6e64c33ac4a48e1d74253d0527f495f9
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 47%

---

# Datenelementtypen

Nachdem Sie die [Aktionstypen](action-types.md) in der [Adobe Experience Platform Web SDK-Erweiterung](web-sdk-extension-configuration.md) für [Adobe Experience Platform Launch](https://experienceleague.adobe.com/docs/launch.html) festgelegt haben, konfigurieren Sie Ihre Datenelementtypen.

Auf dieser Seite werden die verfügbaren Datenelementtypen beschrieben.

## Zusammenführungs-ID eines Ereignisses

Dieses Datenelement stellt die Zusammenführungs-ID eines Ereignisses bereit, falls verwendet. Für dieses Datenelement ist keine Konfiguration erforderlich. Das bereitgestellte Datenelement bleibt unverändert, bis entweder der Besucher die Seite verlässt oder der Aktionstyp „Zusammenführungs-ID des Ereignisses zurücksetzen“ verwendet wird.

## Identitätszuordnung

Mit dem Datenelement „Identitätszuordnung“ können Sie Identitäten aus anderen Datenelementen oder anderen von Ihnen angegebenen Werten erstellen. Alle von Ihnen erstellten Identitäten müssen an einen entsprechenden Namensraum zurückgebunden werden. Dieses Datenelement bietet eine Dropdown-Liste, die alle standardmäßigen Namespaces und alle von Ihnen erstellten Namespaces anzeigt.

![](./assets/identity-map-data-element.png)

## XDM-Objekt {#xdm-object}

Verwenden Sie das XDM-Format, um Daten an das Adobe Experience Platform Web SDK zu senden. Die Formatierung Ihrer Daten ist nämlich mit dem XDM-Objektdatenelement einfacher. Wenn Sie dieses Datenelement zum ersten Mal öffnen, wählen Sie die richtige Adobe Experience Platform-Sandbox und das richtige Schema aus. Nachdem Sie Ihr Schema ausgewählt haben, sehen Sie die Struktur Ihres Schemas, die Sie einfach ausfüllen können.

![](./assets/XDM-object.png)

Beachten Sie, dass beim Öffnen bestimmter Felder Ihres Schemas wie `web.webPageDetails.URL` einige Elemente automatisch erfasst werden. Obwohl mehrere Elemente automatisch erfasst werden, können Sie bei Bedarf alle Elemente überschreiben. Alle Werte können manuell oder mithilfe anderer Datenelemente ausgefüllt werden.

>[!NOTE]
>
>Füllen Sie nur die Informationen aus, die Sie sammeln möchten. Alles, was nicht ausgefüllt wird, wird beim Senden der Daten an die Lösungen weggelassen.
