---
keywords: Streaming;
title: HTTP-API-Verbindung
description: Mit dem HTTP-API-Ziel in Adobe Experience Platform können Sie Profildaten an HTTP-Endpunkte von Drittanbietern senden.
exl-id: 165a8085-c8e6-4c9f-8033-f203522bb288
source-git-commit: 7acacc4a5ddd10f47da59837ad7dab2615d41789
workflow-type: tm+mt
source-wordcount: '1384'
ht-degree: 3%

---

# (Beta) HTTP-API-Verbindung

>[!IMPORTANT]
>
>Das HTTP-API-Ziel in Platform befindet sich derzeit in der Betaphase. Dokumentation und Funktionalität können sich ändern.

## Übersicht {#overview}

Das HTTP-API-Ziel ist ein [!DNL Adobe Experience Platform] Streaming-Ziel, mit dem Sie Profildaten an HTTP-Endpunkte von Drittanbietern senden können.

Um Profildaten an HTTP-Endpunkte zu senden, müssen Sie zunächst [Verbindung zum Ziel herstellen](#connect-destination) in [!DNL Adobe Experience Platform].

## Anwendungsfälle {#use-cases}

Das HTTP-Ziel richtet sich an Kunden, die XDM-Profildaten und Zielgruppensegmente in allgemeine HTTP-Endpunkte exportieren müssen.

HTTP-Endpunkte können entweder eigene Systeme von Kunden oder Lösungen von Drittanbietern sein.

## Exportart und -frequenz {#export-type-frequency}

Informationen zum Zielexporttyp und zur Häufigkeit finden Sie in der unten stehenden Tabelle.

| Element | Typ | Anmerkungen |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Profilbasiert]** | Sie exportieren alle Mitglieder eines Segments zusammen mit den gewünschten Schemafeldern (z. B.: E-Mail-Adresse, Telefonnummer, Nachname), wie im Bildschirm Profilattribute im [Zielaktivierungs-Workflow](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| Exporthäufigkeit | **[!UICONTROL Streaming]** | Streaming-Ziele sind &quot;immer auf&quot;-API-basierte Verbindungen. Sobald ein Profil in Experience Platform auf der Grundlage einer Segmentbewertung aktualisiert wird, sendet der Connector das Update nachgelagert an die Zielplattform. Mehr dazu [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## Voraussetzungen {#prerequisites}

>[!IMPORTANT]
>
>Wenden Sie sich an Ihren Kundenbetreuer oder die Adobe-Kundenunterstützung, wenn Sie die HTTP-API-Ziel-Beta-Funktion für Ihr Unternehmen aktivieren möchten.

Um Daten aus Experience Platform mithilfe des HTTP-API-Ziels zu exportieren, müssen folgende Voraussetzungen erfüllt sein:

* Sie müssen über einen HTTP-Endpunkt verfügen, der die REST-API unterstützt.
* Ihr HTTP-Endpunkt muss das Experience Platform-Profilschema unterstützen. Im HTTP-API-Ziel wird keine Umwandlung in ein Drittanbieter-Payload-Schema unterstützt. Siehe Abschnitt [exportierte Daten](#exported-data) ein Beispiel für das Ausgabeschema der Experience Platform.
* Ihr HTTP-Endpunkt muss Kopfzeilen unterstützen.
* Ihr HTTP-Endpunkt muss [OAuth 2.0-Client-Anmeldeinformationen](https://www.oauth.com/oauth2-servers/access-tokens/client-credentials/) Authentifizierung. Diese Anforderung ist gültig, während sich das HTTP-API-Ziel in der Beta-Phase befindet.
* Die Client-Anmeldedaten müssen in den Hauptteil der POST-Anfragen an Ihren -Endpunkt aufgenommen werden, wie im folgenden Beispiel gezeigt.

```shell
curl --location --request POST '<YOUR_API_ENDPOINT>' \
--header 'Content-Type: application/x-www-form-urlencoded' \
--data-urlencode 'grant_type=client_credentials' \
--data-urlencode 'client_id=<CLIENT_ID>' \
--data-urlencode 'client_secret=<CLIENT_SECRET>'
```

Sie können auch [Adobe Experience Platform Destination SDK](/help/destinations/destination-sdk/overview.md) , um eine Experience Platform einzurichten und Profildaten an einen HTTP-Endpunkt zu senden.

## IP-Adressen-Zulassungsliste {#ip-address-allowlist}

Um die Sicherheits- und Compliance-Anforderungen von Kunden zu erfüllen, stellt Experience Platform eine Liste mit statischen IPs bereit, die Sie für das HTTP-API-Ziel auf die Zulassungsliste gesetzt haben. Siehe [IP-Adressen-Zulassungsliste für Streaming-Ziele](/help/destinations/catalog/streaming/ip-address-allow-list.md) für die vollständige Liste der IP-Adressen in Zulassungsliste.

## Mit Ziel verbinden {#connect-destination}

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

* Die Aktualisierung des Profils wurde durch eine Änderung der Segmentzugehörigkeit für mindestens eines der dem Ziel zugeordneten Segmente bestimmt. Beispielsweise hat sich das Profil für eines der Segmente qualifiziert, die dem Ziel zugeordnet sind, oder eines der dem Ziel zugeordneten Segmente verlassen.
* Die Aktualisierung des Profils wurde durch eine Änderung der [Identitätszuordnung](/help/xdm/field-groups/profile/identitymap.md). Beispielsweise wurde einem Profil, das sich bereits für eines der dem Ziel zugeordneten Segmente qualifiziert hatte, eine neue Identität im Identitätszuordnungsattribut hinzugefügt.
* Die Aktualisierung des Profils wurde durch eine Änderung der Attribute für mindestens eines der dem Ziel zugeordneten Attribute bestimmt. Beispielsweise wird eines der Attribute, die dem Ziel im Zuordnungsschritt zugeordnet sind, einem Profil hinzugefügt.

In allen oben beschriebenen Fällen werden nur die Profile exportiert, in denen relevante Aktualisierungen vorgenommen wurden. Wenn beispielsweise ein Segment, das dem Zielfluss zugeordnet ist, aus hundert Mitgliedern besteht und fünf neue Profile für das Segment qualifiziert sind, ist der Export in Ihr Ziel inkrementell und umfasst nur die fünf neuen Profile.

Beachten Sie, dass alle zugeordneten Attribute unabhängig vom Speicherort der Änderungen für ein Profil exportiert werden. Daher werden im Beispiel vor allem alle zugeordneten Attribute für diese fünf neuen Profile exportiert, selbst wenn sich die Attribute selbst nicht geändert haben.

### Was bestimmt einen Datenexport und was ist im Export enthalten? {#what-determines-export-what-is-included}

Für die Daten, die für ein bestimmtes Profil exportiert werden, ist es wichtig, die beiden verschiedenen Konzepte von *was den Datenexport an Ihr HTTP-API-Ziel bestimmt* und *welche Daten im Export enthalten sind*.

| Was bestimmt den Zielexport? | Im Zielexport enthaltene Informationen |
|---------|----------|
| <ul><li>Zugeordnete Attribute und Segmente dienen als Hinweis für einen Zielexport. Das bedeutet, dass ein Zielexport gestartet wird, wenn zugeordnete Segmente den Status ändern (von null zu realisiert oder von realisiert/existiert zu ausstieg) oder alle zugeordneten Attribute aktualisiert werden.</li><li>Da Identitäten derzeit nicht HTTP-API-Zielen zugeordnet werden können, bestimmen Änderungen an der Identität eines bestimmten Profils auch die Zielexporte.</li><li>Eine Änderung für ein Attribut wird als jede Aktualisierung des Attributs definiert, unabhängig davon, ob es sich um denselben Wert handelt oder nicht. Das bedeutet, dass eine Überschreiben eines Attributs als Änderung gilt, selbst wenn sich der Wert selbst nicht geändert hat.</li></ul> | <ul><li>Alle Segmente (mit dem aktuellen Mitgliedschaftsstatus), unabhängig davon, ob sie im Datenfluss zugeordnet sind oder nicht, werden im `segmentMembership` -Objekt.</li><li>Alle Identitäten in der `identityMap` -Objekt ebenfalls enthalten (Experience Platform unterstützt derzeit keine Identitätszuordnung im HTTP-API-Ziel).</li><li>Nur die zugeordneten Attribute werden in den Zielexport einbezogen.</li></ul> |

{style=&quot;table-layout:fixed&quot;}

Betrachten Sie beispielsweise diesen Datenfluss an ein HTTP-Ziel, bei dem drei Segmente im Datenfluss ausgewählt und dem Ziel vier Attribute zugeordnet sind.

![HTTP-API-Ziel-Datenfluss](/help/destinations/assets/catalog/http/profile-export-example-dataflow.png)

Ein Profilexport an das Ziel kann durch ein Profil bestimmt werden, das für eines der *drei zugeordnete Segmente*. Im Datenexport jedoch wird im `segmentMembership` -Objekt (siehe [Exportierte Daten](#exported-data) unten), können weitere nicht zugeordnete Segmente angezeigt werden, wenn dieses bestimmte Profil Mitglied ist. Wenn ein Profil für den Kunden mit dem Segment &quot;DeLorean Cars&quot;qualifiziert ist, aber auch Mitglied der Segmente &quot;Zurück zur Zukunft&quot;für Film- und Science Fiction-Fans ist, sind diese beiden anderen Segmente auch in den Segmenten `segmentMembership` -Objekt des Datenexports, auch wenn diese nicht im Datenfluss zugeordnet sind.

Aus Sicht der Profilattribute bestimmen alle Änderungen an den vier oben zugeordneten Attributen einen Zielexport und eines der vier im Profil vorhandenen zugeordneten Attribute wird im Datenexport vorhanden sein.

## Exportierte Daten {#exported-data}

Ihr exportiert [!DNL Experience Platform] Daten landen in Ihrer [!DNL HTTP] Ziel im JSON-Format. Beispielsweise enthält der unten stehende Export ein Profil, das sich für ein bestimmtes Segment qualifiziert hat, Mitglied weiterer zwei Segmente ist und ein weiteres Segment verlassen hat. Der Export umfasst auch das Profilattribut mit Vorname, Nachname, Geburtsdatum und persönlicher E-Mail-Adresse. Die Identitäten für dieses Profil sind ECID und E-Mail.

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
   "ups":{
      "7841ba61-23c1-4bb3-a495-00d3g5fe1e93":{
         "lastQualificationTime":"2022-01-11T21:24:39Z",
         "status":"exited"
      },
      "59bd2fkd-3c48-4b18-bf56-4f5c5e6967ae":{
         "lastQualificationTime":"2022-01-02T23:37:33Z",
         "status":"existing"
      },
      "947c1c46-008d-40b0-92ec-3af86eaf41c1":{
         "lastQualificationTime":"2021-08-25T23:37:33Z",
         "status":"existing"
      },
      "5114d758-ce71-43ba-b53e-e2a91d67b67f":{
         "lastQualificationTime":"2022-01-11T23:37:33Z",
         "status":"realized"
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
