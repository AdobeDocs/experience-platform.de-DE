---
keywords: Streaming;
title: HTTP-Verbindung
description: Das HTTP-Ziel in Adobe Experience Platform ermöglicht das Senden von Profil-Daten an HTTP-Endpunkte von Drittanbietern.
exl-id: 165a8085-c8e6-4c9f-8033-f203522bb288
source-git-commit: 2b1cde9fc913be4d3bea71e7d56e0e5fe265a6be
workflow-type: tm+mt
source-wordcount: '357'
ht-degree: 9%

---

# (Alpha) [!DNL HTTP] Verbindung

>[!IMPORTANT]
>
>Die [!DNL HTTP] Ziel in Platform befindet sich derzeit in Alpha. Dokumentation und Funktionalität können sich ändern.

## Übersicht {#overview}

Die [!DNL HTTP] Ziel ist ein [!DNL Adobe Experience Platform] Streaming-Ziel, mit dem Sie Profil-Daten an Dritte senden können [!DNL HTTP] Endpunkte.

So senden Sie Profil-Daten an [!DNL HTTP] Endpunkte müssen Sie zunächst eine Verbindung zum Ziel herstellen in [[!DNL Adobe Experience Platform]](#connect-destination).

## Anwendungsfälle {#use-cases}

Die [!DNL HTTP] Ziel ist auf Kunden ausgerichtet, die XDM-Profil-Daten und -Audiencen in generische Segmente exportieren müssen [!DNL HTTP] Endpunkte.

[!DNL HTTP] Endpunkte können entweder eigene Systeme oder Lösungen von Drittanbietern sein.

## Mit Ziel verbinden {#connect}

Um eine Verbindung zu diesem Ziel herzustellen, führen Sie die Schritte aus, die in der [Übungen zur Zielkonfiguration](../ui/connect-destination.md).

### Verbindungsparameter {#parameters}

Während [einrichten](../ui/connect-destination.md) an diesem Ziel angeben, müssen Sie die folgenden Informationen angeben:

* **[!UICONTROL httpEndpoint]**: die [!DNL URL] des HTTP-Endpunkts, an den Sie die Profil-Daten senden möchten.
   * Optional können Sie Abfragen-Parameter zu den [!UICONTROL httpEndpoint] [!DNL URL].
* **[!UICONTROL authEndpoint]**: die [!DNL URL] des HTTP-Endpunkts, der für [!DNL OAuth2] Authentifizierung.
* **[!UICONTROL Client-ID]**: die [!DNL clientID] Parameter, der in [!DNL OAuth2] Client-Anmeldedaten.
* **[!UICONTROL Kundengeheimnis]**: die [!DNL clientSecret] Parameter, der in [!DNL OAuth2] Client-Anmeldedaten.

   >[!NOTE]
   >
   >Nur [!DNL OAuth2] Clientberechtigungen werden derzeit unterstützt.

* **[!UICONTROL Name]**: Geben Sie einen Namen ein, unter dem Sie dieses Ziel in der Zukunft erkennen.
* **[!UICONTROL Beschreibung]**: Geben Sie eine Beschreibung ein, die Ihnen hilft, dieses Ziel in der Zukunft zu identifizieren.
* **[!UICONTROL Benutzerdefinierte Überschriften]**: Geben Sie benutzerdefinierte Kopfzeilen ein, die in die Zielaufrufe aufgenommen werden sollen, und verwenden Sie folgendes Format: `header1:value1,header2:value2,...headerN:valueN`.

   >[!IMPORTANT]
   >
   >Für die aktuelle Implementierung ist mindestens ein benutzerdefinierter Header erforderlich. Diese Einschränkung wird in einer zukünftigen Aktualisierung behoben.

## Segmente zu diesem Ziel aktivieren {#activate}

Siehe [Audience-Daten in Streaming-Profil-Exportziele aktivieren](../ui/activate-streaming-profile-destinations.md) für Anweisungen zum Aktivieren von Audiencen-Segmenten für dieses Ziel.

### Zielattribute {#attributes}

In [[!UICONTROL Attribute auswählen]](../ui/activate-streaming-profile-destinations.md#select-attributes) Adobe empfiehlt, dass Sie eine eindeutige Kennung aus Ihrem [Vereinigung Schema](../../profile/home.md#profile-fragments-and-union-schemas). Wählen Sie die eindeutige Kennung und alle anderen XDM-Felder aus, die Sie an das Ziel exportieren möchten.

## Exportierte Daten {#exported-data}

Ihr exportiert [!DNL Experience Platform] Daten landen in Ihrer [!DNL HTTP] Ziel im JSON-Format. Das folgende Ereignis enthält beispielsweise das E-Mail-Adressattribut einer Audience, die sich für ein bestimmtes Profil qualifiziert und ein anderes Segment verlassen hat. Die Identitäten für diesen Potenzieller Kunde sind [!DNL ECID] und E-Mail.

```json
{
  "person": {
    "email": "yourstruly@adobe.com"
  },
  "segmentMembership": {
    "ups": {
      "7841ba61-23c1-4bb3-a495-00d3g5fe1e93": {
        "lastQualificationTime": "2020-05-25T21:24:39Z",
        "status": "exited"
      },
      "59bd2fkd-3c48-4b18-bf56-4f5c5e6967ae": {
        "lastQualificationTime": "2020-05-25T23:37:33Z",
        "status": "existing"
      }
    }
  },
  "identityMap": {
    "ecid": [
      {
        "id": "14575006536349286404619648085736425115"
      },
      {
        "id": "66478888669296734530114754794777368480"
      }
    ],
    "email_lc_sha256": [
      {
        "id": "655332b5fa2aea4498bf7a290cff017cb4"
      },
      {
        "id": "66baf76ef9de8b42df8903f00e0e3dc0b7"
      }
    ]
  }
}
```
