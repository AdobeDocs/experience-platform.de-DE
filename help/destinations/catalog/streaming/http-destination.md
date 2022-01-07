---
keywords: Streaming;
title: HTTP-Verbindung
description: Mit dem HTTP-API-Ziel in Adobe Experience Platform können Sie Profildaten an HTTP-Endpunkte von Drittanbietern senden.
exl-id: 165a8085-c8e6-4c9f-8033-f203522bb288
source-git-commit: 8d2c5ef477d4707be4c0da43ba1f672fac797604
workflow-type: tm+mt
source-wordcount: '633'
ht-degree: 5%

---

# (Beta) [!DNL HTTP] API-Verbindung

>[!IMPORTANT]
>
>Die [!DNL HTTP] Das Ziel in Platform befindet sich derzeit in der Beta-Phase. Dokumentation und Funktionalität können sich ändern.

## Übersicht {#overview}

Die [!DNL HTTP] API-Ziel ist ein [!DNL Adobe Experience Platform] Streaming-Ziel, mit dem Sie Profildaten an Drittanbieter senden können [!DNL HTTP] -Endpunkte.

So senden Sie Profildaten an [!DNL HTTP] -Endpunkte müssen Sie zunächst eine Verbindung zum Ziel in [[!DNL Adobe Experience Platform]](#connect-destination).

## Anwendungsfälle {#use-cases}

Die [!DNL HTTP] Ziel ist auf Kunden ausgerichtet, die XDM-Profildaten und Zielgruppensegmente in generische exportieren müssen [!DNL HTTP] -Endpunkte.

[!DNL HTTP] Endpunkte können entweder die eigenen Systeme von Kunden oder Lösungen von Drittanbietern sein.

## Mit Ziel verbinden {#connect}

Gehen Sie wie im Abschnitt [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md).

### Verbindungsparameter {#parameters}

while [Einrichten](../../ui/connect-destination.md) An diesem Ziel müssen Sie die folgenden Informationen angeben:

* **[!UICONTROL httpEndpoint]**: die [!DNL URL] des HTTP-Endpunkts, an den Sie die Profildaten senden möchten.
   * Optional können Sie Abfrageparameter zum [!UICONTROL httpEndpoint] [!DNL URL].
* **[!UICONTROL authEndpoint]**: die [!DNL URL] des HTTP-Endpunkts, der für [!DNL OAuth2] Authentifizierung.
* **[!UICONTROL Client-ID]**: die [!DNL clientID] -Parameter, der in der [!DNL OAuth2] Client-Anmeldedaten.
* **[!UICONTROL Client Secret]**: die [!DNL clientSecret] -Parameter, der in der [!DNL OAuth2] Client-Anmeldedaten.

   >[!NOTE]
   >
   >Nur [!DNL OAuth2] Client-Anmeldeinformationen werden derzeit unterstützt.

* **[!UICONTROL Name]**: Geben Sie einen Namen ein, mit dem Sie dieses Ziel in Zukunft erkennen werden.
* **[!UICONTROL Beschreibung]**: Geben Sie eine Beschreibung ein, die Ihnen dabei hilft, dieses Ziel in der Zukunft zu identifizieren.
* **[!UICONTROL Benutzerdefinierte Kopfzeilen]**: Geben Sie alle benutzerdefinierten Header ein, die in die Zielaufrufe aufgenommen werden sollen, indem Sie folgendes Format verwenden: `header1:value1,header2:value2,...headerN:valueN`.

   >[!IMPORTANT]
   >
   >Für die aktuelle Implementierung ist mindestens eine benutzerdefinierte Kopfzeile erforderlich. Diese Einschränkung wird in einer zukünftigen Aktualisierung behoben.

## Aktivieren von Segmenten für dieses Ziel {#activate}

Siehe [Aktivieren von Zielgruppendaten für Streaming-Profil-Export-Ziele](../../ui/activate-streaming-profile-destinations.md) für Anweisungen zum Aktivieren von Zielgruppensegmenten für dieses Ziel.

### Zielattribute {#attributes}

Im [[!UICONTROL Attribute auswählen]](../../ui/activate-streaming-profile-destinations.md#select-attributes) in Adobe empfiehlt, eine eindeutige Kennung aus der [Vereinigungsschema](../../../profile/home.md#profile-fragments-and-union-schemas). Wählen Sie die eindeutige Kennung und alle anderen XDM-Felder aus, die Sie an das Ziel exportieren möchten.

## Profil-Exportverhalten {#profile-export-behavior}

Experience Platform optimiert das Profil-Exportverhalten für Ihr HTTP-API-Ziel, sodass nur Daten an Ihren API-Endpunkt exportiert werden, wenn relevante Profilaktualisierungen nach der Segmentqualifizierung oder anderen wichtigen Ereignissen durchgeführt wurden. Profile werden in den folgenden Situationen an Ihr Ziel exportiert:

* Das Profil-Update wurde durch eine Änderung der Segmentzugehörigkeit für mindestens eines der dem Ziel zugeordneten Segmente ausgelöst. Beispielsweise hat sich das Profil für eines der Segmente qualifiziert, die dem Ziel zugeordnet sind, oder eines der dem Ziel zugeordneten Segmente verlassen.
* Das Profil-Update wurde durch eine Änderung der [Identitätszuordnung](/help/xdm/field-groups/profile/identitymap.md). Beispielsweise wurde einem Profil, das sich bereits für eines der dem Ziel zugeordneten Segmente qualifiziert hatte, eine neue Identität im Identitätszuordnungsattribut hinzugefügt.
* Das Profil-Update wurde durch eine Änderung der Attribute für mindestens eines der dem Ziel zugeordneten Attribute ausgelöst. Beispielsweise wird eines der Attribute, die dem Ziel im Zuordnungsschritt zugeordnet sind, einem Profil hinzugefügt.

In allen oben beschriebenen Fällen werden nur die Profile exportiert, in denen relevante Aktualisierungen vorgenommen wurden. Wenn beispielsweise ein Segment, das dem Zielfluss zugeordnet ist, aus hundert Mitgliedern besteht und fünf neue Profile für das Segment qualifiziert sind, ist der Export in Ihr Ziel inkrementell und umfasst nur die fünf neuen Profile.

Beachten Sie, dass alle zugeordneten Attribute unabhängig vom Speicherort der Änderungen für ein Profil exportiert werden. Daher werden im Beispiel vor allem alle zugeordneten Attribute für diese fünf neuen Profile exportiert, selbst wenn sich die Attribute selbst nicht geändert haben.

## Exportierte Daten {#exported-data}

Ihr exportiert [!DNL Experience Platform] Daten landen in Ihrer [!DNL HTTP] Ziel im JSON-Format. Beispielsweise enthält das nachstehende Ereignis das E-Mail-Adressen-Profilattribut einer Zielgruppe, die sich für ein bestimmtes Segment qualifiziert und ein anderes Segment verlassen hat. Die Identitäten für diese Perspektive sind [!DNL ECID] und E-Mail.

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
