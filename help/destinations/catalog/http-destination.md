---
keywords: Streaming;
title: HTTP-Verbindung
description: Mit dem HTTP-Ziel in Adobe Experience Platform können Sie Profil-Daten an HTTP-Endpunkte von Drittanbietern senden.
translation-type: tm+mt
source-git-commit: 709908196bb5df665c7e7df10dc58ee9f3b0edbf
workflow-type: tm+mt
source-wordcount: '543'
ht-degree: 8%

---


# (Alpha) [!DNL HTTP]-Verbindung

>[!IMPORTANT]
>
>Das [!DNL HTTP]-Ziel in der Plattform befindet sich derzeit in Alpha. Die Dokumentation und Funktionalität können sich ändern.

## Übersicht {#overview}

Das [!DNL HTTP]-Ziel ist ein [!DNL Adobe Experience Platform]-Streaming-Ziel, mit dem Sie Profil-Daten an Drittanbieter-Endpunkte [!DNL HTTP] senden können.

Um Profil-Daten an [!DNL HTTP]-Endpunkte zu senden, müssen Sie zunächst eine Verbindung zum Ziel in [[!DNL Adobe Experience Platform]](#connect-destination) herstellen.

## Nutzungsszenarien {#use-cases}

Das [!DNL HTTP]-Ziel ist auf Kunden ausgerichtet, die XDM-Profil- und Audience-Segmente in generische [!DNL HTTP]-Endpunkte exportieren müssen.

[!DNL HTTP] Endpunkte können entweder eigene Systeme oder Lösungen von Drittanbietern sein.

## Verbindung mit Ziel {#connect-destination}

Wählen Sie unter **[!UICONTROL Verbindungen]** > **[!UICONTROL Ziele]** [!DNL HTTP API] aus und wählen Sie **[!UICONTROL Konfigurieren]**.

![HTTP-Ziel aktivieren](../assets/catalog/http/activate.png)

Wenn bereits eine Verbindung zu diesem Ziel besteht, wird auf der Zielkarte die Schaltfläche **[!UICONTROL Aktivieren]** angezeigt. Weitere Informationen zum Unterschied zwischen **[!UICONTROL Aktivieren]** und **[!UICONTROL Konfigurieren]** finden Sie im Abschnitt [Katalog](../ui/destinations-workspace.md#catalog) der Dokumentation zum Zielarbeitsbereich.

![HTTP-Ziel aktivieren](../assets/catalog/http/connect.png)

Im Schritt [!UICONTROL Konto] müssen Sie die HTTP-Endpunktverbindungsdetails definieren. Wählen Sie **[!UICONTROL Neues Konto]** und geben Sie die Verbindungsdetails für den HTTP-Endpunkt ein, mit dem Sie eine Verbindung herstellen möchten.
- **[!UICONTROL httpEndpoint]**: der vollständige  [!DNL URL] HTTP-Endpunkt, an den Sie die Profil-Daten senden möchten.
   - Optional können Sie dem [!UICONTROL httpEndpoint] [!DNL URL] Abfragen-Parameter hinzufügen.
- **[!UICONTROL authEndpoint]**: der vollständige  [!DNL URL] HTTP-Endpunkt, der für die  [!DNL OAuth2] Authentifizierung verwendet wird.
- **[!UICONTROL Client-ID]**: der in den  [!DNL clientID] Clientberechtigungen verwendete  [!DNL OAuth2] Parameter.
- **[!UICONTROL geheim]**: der in den  [!DNL clientSecret] Clientberechtigungen verwendete  [!DNL OAuth2] Parameter.

>[!NOTE]
>
>Derzeit werden nur die Clientberechtigungen [!DNL OAuth2] unterstützt.

![HTTP-Endpunktverbindung](../assets/catalog/http/connect.png)

Klicken Sie auf **[!UICONTROL Mit Ziel]** verbinden. Klicken Sie nach erfolgreicher Verbindung auf **[!UICONTROL Weiter]**.

Geben Sie im Schritt [!UICONTROL Authentifizierung] die Anmeldeinformationen für die Kontoauthentifizierung ein:
- **[!UICONTROL Name]**: Geben Sie einen Namen ein, unter dem Sie dieses Ziel in Zukunft erkennen werden.
- **[!UICONTROL Beschreibung]**: Geben Sie eine Beschreibung ein, mit der Sie dieses Ziel in Zukunft identifizieren können.
- **[!UICONTROL Benutzerdefinierte Kopfzeilen]**: Geben Sie alle benutzerdefinierten Kopfzeilen ein, die in die Zielaufrufe aufgenommen werden sollen, und befolgen Sie dabei das folgende Format:  `header1:value1,header2:value2,...headerN:valueN`.
- **[!UICONTROL Marketingaktionen]**: Marketingaktionen geben die Absicht an, für die Daten an das Ziel exportiert werden. Sie können aus von der Adobe definierten Marketingaktionen auswählen oder eine eigene Marketingaktion erstellen. Weitere Informationen zu Marketingaktionen finden Sie auf der Seite [Datenverwaltung in Adobe Experience Platform](/help/data-governance/policies/overview.md). Informationen zu den einzelnen, von der Adobe definierten Marketingaktionen finden Sie unter [Übersicht über Datenverwendungsrichtlinien](/help/data-governance/policies/overview.md).

>[!IMPORTANT]
>
>Für die aktuelle Implementierung ist mindestens ein benutzerdefinierter Header erforderlich. Diese Einschränkung wird in einem zukünftigen Update behoben.

![HTTP-Authentifizierung](../assets/catalog/http/authenticate.png)

**[!UICONTROL Marketingaktion]**: Marketingaktionen geben die Absicht an, für die Daten an das Ziel exportiert werden. Sie können aus von der Adobe definierten Marketingaktionen auswählen oder eine eigene Marketingaktion erstellen. Weitere Informationen zu Marketingaktionen finden Sie unter [Übersicht über Datenverwendungsrichtlinien](../../data-governance/policies/overview.md).

Klicken Sie auf **[!UICONTROL Ziel erstellen]**.

## Segmente aktivieren

Informationen zum Workflow für die Segmentaktivierung finden Sie unter [Profile und Segmente für ein Ziel aktivieren](../ui/activate-destinations.md#select-attributes).

## Zielattribute

Wenn Sie im Schritt [[!UICONTROL Attribute auswählen]](../ui/activate-destinations.md#select-attributes) und [segmente](../ui/activate-destinations.md) an ein [!DNL HTTP]-Ziel aktivieren, empfehlen wir Ihnen, einen eindeutigen Bezeichner aus Ihrem [Vereinigung-Schema](../../profile/home.md#profile-fragments-and-union-schemas) auszuwählen. Wählen Sie die eindeutige Kennung und alle anderen XDM-Felder aus, die Sie an das Ziel exportieren möchten.

## Exportierte Daten {#exported-data}

Ihre exportierten [!DNL Experience Platform]-Daten landen im JSON-Format im [!DNL HTTP]-Ziel. Das folgende Ereignis enthält beispielsweise das Segmentattribut &quot;E-Mail-Adresse&quot;einer Audience, die sich für ein bestimmtes Profil qualifiziert und ein anderes Segment verlassen hat. Die Identitäten für diesen Potenzieller Kunde sind [!DNL ECID] und email.

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
