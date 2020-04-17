---
title: Schnellstart mit Launch
seo-title: Adobe Experience Platform Web SDK – Schnellstart mit Launch
description: Kurzanleitung zum Einsatz der Experience Platform Web SDK-Erweiterung zur Datenerfassung
seo-description: Kurzanleitung zum Einsatz der Experience Platform Web SDK-Erweiterung zur Datenerfassung
translation-type: tm+mt
source-git-commit: a1161630c8edae107b784f32ee20af225f9f8c46

---


# (Beta) Voraussetzungen

>[!IMPORTANT]
>
>Das Adobe Experience Platform Web SDK befindet sich derzeit in der Betaphase und steht nicht allen Nutzern zur Verfügung. Dokumentation und Funktionalität können sich ändern.

Das Adobe Experience Platform Web SDK unterstützt derzeit nur das Senden von Daten an Adobe Experience Platform mit XDM. Sie müssen die folgenden Voraussetzungen erfüllen.

- Sie benötigen eine aktivierte [Erstanbieter-Domäne (CNAME)](https://docs.adobe.com/content/help/de-DE/core-services/interface/ec-cookies/cookies-first-party.html). Wenn Sie bereits über eine CNAME für Analytics verfügen, sollten Sie diese verwenden.
- Berechtigung für Adobe Experience Platform
- Verwenden Sie die neueste Version des Besucher-ID-Diensts

## Plattform vorbereiten

Um Daten an Adobe Experience Platform senden zu können, müssen Sie ein XDM-Schema und einen Datensatz erstellen, die dieses Schema verwenden.

- [Erstellen Sie ein Schema](../../xdm/tutorials/create-schema-ui.md) mit den folgenden Mixins:
   - ExperienceEvent-Implementierungsdetails
   - ExperienceEvent-Umgebungsdetails
   - ExperienceEvent-Web-Details
- Fügen Sie dem erstellten Schema das Adobe Experience Platform Web SDK-Mixin hinzu
- [Erstellen Sie einen Datensatz](https://platform.adobe.com/dataset/overview) mit Ihrem Schema, in dem die Daten landen sollen

## Anfordern einer Konfigurations-ID

Sie müssen über eine Konfigurations-ID verfügen, um das SDK verwenden zu können. Die Konfigurations-ID stellt sicher, dass Ihre Daten an den richtigen Ort weitergeleitet werden. Sie können eine Konfigurations-ID entweder von Ihrem Berater oder über Client Care abrufen. Sie benötigen folgende Informationen:

- **Organisations-ID:** Sie können diese anhand der Anweisungen [hier](https://docs.adobe.com/content/help/de-DE/core-services/interface/manage-users-and-products/organizations.html) finden.
- **Datensatz-ID:** Diese ist in der Datensatz-Benutzeroberfläche verfügbar, wenn Sie auf einen Datensatz klicken.
- **Schema-ID:** Diese ist in der URL des Bildschirms zur Schema-Erstellung verfügbar.
- **Anzeigename:** Dies ist der Anzeigename, der in zukünftigen Benutzeroberflächen für diese Konfiguration verwendet wird.

## SDK in Launch installieren

Melden Sie sich bei Launch an und installieren Sie die `AEP Web SDK`-Erweiterung. Während der Installation des SDK werden Sie aufgefordert, die Erweiterung zu konfigurieren. Geben Sie die oben angeforderte Konfigurations-ID ein. Die Erweiterung füllt Ihre Organisations-ID automatisch aus.

Weitere Informationen zu den verschiedenen Konfigurationsoptionen finden Sie unter [Konfigurieren des SDK](../fundamentals/configuring-the-sdk.md).

## Ereignis senden

Nachdem die Erweiterung installiert wurde, beginnen Sie mit dem Senden von Ereignissen, indem Sie eine Aktion „Beacon senden“ aus der AEP Web SDK-Erweiterung hinzufügen. Es wird empfohlen, jedes Mal, wenn eine Seite geladen wird, mindestens ein Ereignis zu senden, bei dem die Option „Tritt am Beginn einer Ansicht auf“ aktiviert ist.

Weitere Informationen zur Verfolgung von Ereignissen finden Sie unter [Verfolgen von Ereignissen](../fundamentals/tracking-events.md).

## Daten senden

Sie können Daten senden, die mit dem zuvor erstellten Schema und Ihren Ereignissen übereinstimmen. Wenn Sie beispielsweise eine Commerce-Site besitzen und Ihrem Schema das Commerce-Mixin hinzufügen, senden Sie die folgende Struktur, wenn jemand ein Produkt anzeigt.

```javascript
{
  "commerce": {
    "productListAdds": {
        "value":1
    }
  },
  "productListItems":{
      "name":"Floppy Green Hat",
      "SKU":"HATFLP123",
      "product":"1234567",
      "quantity":2
  }
}
```
