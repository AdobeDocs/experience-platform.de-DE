---
title: Schnellstart-Beginn
seo-title: Beginn zum Adobe Experience Platform Web SDK-Schnellstart
description: Kurzanleitung zum Einsatz der Experience Platform Web SDK-Erweiterung zur Datenerfassung
seo-description: Kurzanleitung zum Einsatz der Experience Platform Web SDK-Erweiterung zur Datenerfassung
translation-type: tm+mt
source-git-commit: 0cc6e233646134be073d20e2acd1702d345ff35f

---


# (Beta) Voraussetzungen

>[!IMPORTANT]
>
>Das Adobe Experience Platform Web SDK befindet sich derzeit in der Betaphase und steht nicht allen Benutzern zur Verfügung. Dokumentation und Funktionalität können sich ändern.

Das Adobe Experience Platform Web SDK unterstützt derzeit nur das Senden von Daten an Adobe Experience Platform mit XDM. Sie müssen die folgenden Voraussetzungen erfüllen.

- Lassen Sie eine [Erstanbieterdomäne (CNAME)](https://docs.adobe.com/content/help/en/core-services/interface/ec-cookies/cookies-first-party.html) aktiviert. Wenn Sie bereits über einen CNAME für Analytics verfügen, sollten Sie diesen verwenden.
- Berechtigung für Adobe Experience Platform
- Verwenden Sie die neueste Version des Besucher-ID-Diensts

## Plattform vorbereiten

Um Daten an Adobe Experience Platform senden zu können, müssen Sie ein XDM-Schema und ein Dataset erstellen, das dieses Schema verwendet.

- [Erstellen Sie ein Schema](https://www.adobe.io/apis/experienceplatform/home/tutorials/alltutorials.html#!api-specification/markdown/narrative/tutorials/schema_editor_tutorial/schema_editor_tutorial.md) mit den folgenden Mixins:
   - ExperienceEvent-Implementierungsdetails
   - Details zur ExperienceEvent-Umgebung
   - ExperienceEvent-Webdetails
- Hinzufügen der Adobe Experience Platform Web SDK-Mischung mit dem erstellten Schema
- [Erstellen Sie einen Datensatz](https://platform.adobe.com/dataset/overview) mit Ihrem Schema, in dem die Daten landen sollen

## Anfordern einer Konfigurations-ID

Sie müssen über eine Konfigurations-ID verfügen, um das SDK verwenden zu können. Die Konfigurations-ID stellt sicher, dass Ihre Daten an den richtigen Ort weitergeleitet werden. Sie können eine Konfigurations-ID entweder von Ihrem Berater oder über Client Care abrufen. Sie benötigen folgende Informationen:

- **Organisations-ID:** Sie können dies anhand der Anweisungen [hier finden](https://docs.adobe.com/content/help/en/core-services/interface/manage-users-and-products/organizations.html)
- **Datenbestand-ID:** Dies ist in der DataSet-Benutzeroberfläche verfügbar, wenn Sie auf einen Datensatz klicken
- **Schema-ID:** Dies ist in der URL des Bildschirms zur Erstellung des Schemas verfügbar
- **Freundlicher Name:** Dies ist der Anzeigename, der in zukünftigen Benutzeroberflächen für diese Konfiguration verwendet wird

## SDK beim Start installieren

Melden Sie sich bei Launch an und installieren Sie die `AEP Web SDK` Erweiterung. Während der Installation des SDK werden Sie aufgefordert, die Erweiterung zu konfigurieren. Geben Sie die oben angeforderte Konfigurations-ID ein. Die Erweiterung füllt Ihre Organisations-ID automatisch aus.

Weitere Informationen zu den verschiedenen Konfigurationsoptionen finden Sie unter SDK [konfigurieren](../fundamentals/configuring-the-sdk.md).

## Ereignis senden

Nachdem die Erweiterung installiert wurde, senden Beginn Ereignis, indem sie eine Aktion &quot;Beacon senden&quot;aus der AEP Web SDK-Erweiterung hinzufügen. Es wird empfohlen, mindestens ein Ereignis zu senden, wenn eine Seite geladen wird und die Option &quot;Tritt am Beginn einer Ansicht auf&quot;aktiviert ist.

Weitere Informationen zur Verfolgung von Ereignissen finden Sie unter [Ereignis](../fundamentals/tracking-events.md)verfolgen.

## Daten senden

Sie können Daten senden, die mit dem zuvor erstellten Schema und Ihren Ereignissen übereinstimmen. Wenn Sie beispielsweise eine Commerce-Site besitzen und das Commerce-Mixin Ihrem Schema hinzufügen, senden Sie die folgende Struktur, wenn jemand ein Produkt Ansicht.

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
