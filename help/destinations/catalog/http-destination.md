---
keywords: Streaming;
title: HTTP-Verbindung
description: Mit dem HTTP-Ziel in Adobe Experience Platform können Sie Profildaten an HTTP-Endpunkte von Drittanbietern senden.
exl-id: 165a8085-c8e6-4c9f-8033-f203522bb288
source-git-commit: 3aac1e7c7fe838201368379da8504efc8e316e1c
workflow-type: tm+mt
source-wordcount: '357'
ht-degree: 9%

---

# (Alpha) [!DNL HTTP] Verbindung

>[!IMPORTANT]
>
>Das [!DNL HTTP]-Ziel in Platform befindet sich derzeit in der Alpha-Phase. Dokumentation und Funktionalität können sich ändern.

## Übersicht {#overview}

Das [!DNL HTTP]-Ziel ist ein [!DNL Adobe Experience Platform]-Streaming-Ziel, mit dem Sie Profildaten an [!DNL HTTP]-Endpunkte von Drittanbietern senden können.

Um Profildaten an [!DNL HTTP]-Endpunkte zu senden, müssen Sie zunächst in [[!DNL Adobe Experience Platform]](#connect-destination) eine Verbindung zum Ziel herstellen.

## Anwendungsbeispiele {#use-cases}

Das [!DNL HTTP]-Ziel richtet sich an Kunden, die XDM-Profildaten und Zielgruppensegmente in allgemeine [!DNL HTTP]-Endpunkte exportieren müssen.

[!DNL HTTP] Endpunkte können entweder die eigenen Systeme von Kunden oder Lösungen von Drittanbietern sein.

## Mit Ziel verbinden {#connect}

Um eine Verbindung zu diesem Ziel herzustellen, führen Sie die Schritte aus, die im Tutorial [Zielkonfiguration](../ui/connect-destination.md) beschrieben sind.

### Verbindungsparameter {#parameters}

Während [Einrichten](../ui/connect-destination.md) dieses Ziels müssen Sie die folgenden Informationen angeben:

* **[!UICONTROL httpEndpoint]**: die  [!DNL URL] des HTTP-Endpunkts, an den Sie die Profildaten senden möchten.
   * Optional können Sie Abfrageparameter zum [!UICONTROL httpEndpoint] [!DNL URL] hinzufügen.
* **[!UICONTROL authEndpoint]**: die  [!DNL URL] des für die  [!DNL OAuth2] Authentifizierung verwendeten HTTP-Endpunkts.
* **[!UICONTROL Client-ID]**: den  [!DNL clientID] Parameter, der in den  [!DNL OAuth2] Client-Anmeldeinformationen verwendet wird.
* **[!UICONTROL Client Secret]**: den  [!DNL clientSecret] Parameter, der in den  [!DNL OAuth2] Client-Anmeldeinformationen verwendet wird.

   >[!NOTE]
   >
   >Derzeit werden nur Client-Anmeldedaten von [!DNL OAuth2] unterstützt.

* **[!UICONTROL Name]**: Geben Sie einen Namen ein, mit dem Sie dieses Ziel in Zukunft erkennen werden.
* **[!UICONTROL Beschreibung]**: Geben Sie eine Beschreibung ein, die Ihnen dabei hilft, dieses Ziel in der Zukunft zu identifizieren.
* **[!UICONTROL Benutzerdefinierte Kopfzeilen]**: Geben Sie alle benutzerdefinierten Header ein, die in die Zielaufrufe aufgenommen werden sollen, indem Sie folgendes Format verwenden:  `header1:value1,header2:value2,...headerN:valueN`.

   >[!IMPORTANT]
   >
   >Für die aktuelle Implementierung ist mindestens eine benutzerdefinierte Kopfzeile erforderlich. Diese Einschränkung wird in einer zukünftigen Aktualisierung behoben.

## Aktivieren von Segmenten für dieses Ziel {#activate}

Anweisungen zum Aktivieren von Zielgruppensegmenten für dieses Ziel finden Sie unter [Aktivieren von Zielgruppendaten für Streaming-Profilexport-Ziele](../ui/activate-streaming-profile-destinations.md) .

### Zielattribute {#attributes}

Im Schritt [[!UICONTROL Attribute]](../ui/activate-streaming-profile-destinations.md#select-attributes) auswählen empfiehlt Adobe, eine eindeutige Kennung aus Ihrem [Vereinigungsschema](../../profile/home.md#profile-fragments-and-union-schemas) auszuwählen. Wählen Sie die eindeutige Kennung und alle anderen XDM-Felder aus, die Sie an das Ziel exportieren möchten.

## Exportierte Daten {#exported-data}

Ihre exportierten [!DNL Experience Platform]-Daten landen im JSON-Format in Ihrem [!DNL HTTP]-Ziel. Beispielsweise enthält das nachstehende Ereignis das E-Mail-Adressen-Profilattribut einer Zielgruppe, die sich für ein bestimmtes Segment qualifiziert und ein anderes Segment verlassen hat. Die Identitäten für diesen Interessenten sind [!DNL ECID] und E-Mail.

```json
{
  "person": {
    "email": "yourstruly@adobe.con"
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
