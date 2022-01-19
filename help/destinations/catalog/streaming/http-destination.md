---
keywords: streaming;
title: HTTP-API-Verbindung
description: The HTTP API destination in Adobe Experience Platform allows you to send profile data to third-party HTTP endpoints.
exl-id: 165a8085-c8e6-4c9f-8033-f203522bb288
source-git-commit: f098df9df2baa971db44a6746949f021e212ae3e
workflow-type: tm+mt
source-wordcount: '833'
ht-degree: 4%

---

# (Beta) HTTP API connection

>[!IMPORTANT]
>
>The HTTP API destination in Platform is currently in beta. Dokumentation und Funktionalität können sich ändern.

## Übersicht {#overview}

Das HTTP-API-Ziel ist ein [!DNL Adobe Experience Platform] Streaming-Ziel, mit dem Sie Profildaten an HTTP-Endpunkte von Drittanbietern senden können.

Um Profildaten an HTTP-Endpunkte zu senden, müssen Sie zunächst [Verbindung zum Ziel herstellen](#connect-destination) in [!DNL Adobe Experience Platform].

## Anwendungsfälle {#use-cases}

The HTTP destination is targeted towards customers who need to export XDM profile data and audience segments to generic HTTP endpoints.

HTTP-Endpunkte können entweder eigene Systeme von Kunden oder Lösungen von Drittanbietern sein.

## Voraussetzungen {#prerequisites}

>[!IMPORTANT]
>
>Contact your Adobe representatives or Adobe Customer Care if you would like to enable the HTTP API destination beta functionality for your company.

To use the HTTP API destination to export data out of Experience Platform, you must meet the following prerequisites:

* Sie müssen über einen HTTP-Endpunkt verfügen, der die REST-API unterstützt.
* Ihr HTTP-Endpunkt muss das Experience Platform-Profilschema unterstützen. No transformation to a 3rd-party payload schema is supported in the HTTP API destination. Siehe Abschnitt [exportierte Daten](#exported-data) ein Beispiel für das Ausgabeschema der Experience Platform.
* Ihr HTTP-Endpunkt muss Kopfzeilen unterstützen.
* Ihr HTTP-Endpunkt muss [OAuth 2.0-Client-Anmeldeinformationen](https://www.oauth.com/oauth2-servers/access-tokens/client-credentials/) Authentifizierung. This requirement is valid while the HTTP API destination is in the beta phase.
* Die Client-Anmeldedaten müssen in den Hauptteil der POST-Anfragen an Ihren -Endpunkt aufgenommen werden, wie im folgenden Beispiel gezeigt.

```shell
curl --location --request POST '<YOUR_API_ENDPOINT>' \
--header 'Content-Type: application/x-www-form-urlencoded' \
--data-urlencode 'grant_type=client_credentials' \
--data-urlencode 'client_id=<CLIENT_ID>' \
--data-urlencode 'client_secret=<CLIENT_SECRET>'
```


Sie können auch [Adobe Experience Platform Destination SDK](/help/destinations/destination-sdk/overview.md) , um eine Experience Platform einzurichten und Profildaten an einen HTTP-Endpunkt zu senden.

## Mit Ziel verbinden {#connect-destination}

Gehen Sie wie im Abschnitt [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md).

### Verbindungsparameter {#parameters}

while [Einrichten](../../ui/connect-destination.md) An diesem Ziel müssen Sie die folgenden Informationen angeben:

* **[!UICONTROL httpEndpoint]**: die [!DNL URL] des HTTP-Endpunkts, an den Sie die Profildaten senden möchten.
   * Optional können Sie Abfrageparameter zum [!UICONTROL httpEndpoint] [!DNL URL].
* **[!UICONTROL authEndpoint]**: die [!DNL URL] des HTTP-Endpunkts, der für [!DNL OAuth2] Authentifizierung.
* **[!UICONTROL Client-ID]**: die [!DNL clientID] -Parameter, der in der [!DNL OAuth2] Client-Anmeldedaten.
* **[!UICONTROL Client Secret]**: the [!DNL clientSecret] parameter used in the [!DNL OAuth2] client credentials.

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

Experience Platform optimizes the profile export behavior to your HTTP API destination, to only export data to your API endpoint when relevant updates to a profile have occurred following segment qualification or other significant events. Profile werden in den folgenden Situationen an Ihr Ziel exportiert:

* Das Profil-Update wurde durch eine Änderung der Segmentzugehörigkeit für mindestens eines der dem Ziel zugeordneten Segmente ausgelöst. Beispielsweise hat sich das Profil für eines der Segmente qualifiziert, die dem Ziel zugeordnet sind, oder eines der dem Ziel zugeordneten Segmente verlassen.
* Das Profil-Update wurde durch eine Änderung der [Identitätszuordnung](/help/xdm/field-groups/profile/identitymap.md). Beispielsweise wurde einem Profil, das sich bereits für eines der dem Ziel zugeordneten Segmente qualifiziert hatte, eine neue Identität im Identitätszuordnungsattribut hinzugefügt.
* Das Profil-Update wurde durch eine Änderung der Attribute für mindestens eines der dem Ziel zugeordneten Attribute ausgelöst. Beispielsweise wird eines der Attribute, die dem Ziel im Zuordnungsschritt zugeordnet sind, einem Profil hinzugefügt.

In all the cases described above, only the profiles where relevant updates have occurred are exported to your destination. Wenn beispielsweise ein Segment, das dem Zielfluss zugeordnet ist, aus hundert Mitgliedern besteht und fünf neue Profile für das Segment qualifiziert sind, ist der Export in Ihr Ziel inkrementell und umfasst nur die fünf neuen Profile.

Note that the all the mapped attributes are exported for a profile, no matter where the changes lie. Daher werden im Beispiel vor allem alle zugeordneten Attribute für diese fünf neuen Profile exportiert, selbst wenn sich die Attribute selbst nicht geändert haben.

## Exportierte Daten {#exported-data}

Your exported [!DNL Experience Platform] data lands in your [!DNL HTTP] destination in JSON format. Der folgende Export enthält beispielsweise ein Profil, das sich für ein bestimmtes Segment qualifiziert und ein anderes Segment verlassen hat, und das das Profilattribut mit Vorname, Nachname, Geburtsdatum und persönlicher E-Mail-Adresse enthält. The identities for this profile are ECID and email.

```json
{
  "person": {
    "birthDate": "YYYY-MM-DD",
    "name": {
      "firstName": "John",
      "lastName": "Doe"
    }
  },
  "personalEmail": {
    "address": "john.doe@acme.com"
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
