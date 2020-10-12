---
keywords: streaming;
title: Das HTTP-Ziel ist ein Adobe Real-Time Customer Data Platform-Ziel, mit dem Sie Profil-Daten an HTTP-Endpunkte von Drittanbietern senden können.
seo-title: Das HTTP-Ziel ist ein Adobe Real-Time Customer Data Platform-Ziel, mit dem Sie Profil-Daten an HTTP-Endpunkte von Drittanbietern senden können.
description: Das HTTP-Ziel ist ein Adobe Real-Time Customer Data Platform-Ziel, mit dem Sie Profil-Daten an HTTP-Endpunkte von Drittanbietern senden können.
seo-description: Das HTTP-Ziel ist ein Adobe Real-Time Customer Data Platform-Ziel, mit dem Sie Profil-Daten an HTTP-Endpunkte von Drittanbietern senden können.
translation-type: tm+mt
source-git-commit: cf100e8df225a665eade5ee6ddab071707e93f8b
workflow-type: tm+mt
source-wordcount: '572'
ht-degree: 7%

---


# (Alpha) [!DNL HTTP] Ziel

>[!IMPORTANT]
>
>Das [!DNL HTTP] Ziel in Adobe Echtzeit-CDP befindet sich derzeit in Alpha. Dokumentation und Funktionalität können sich ändern.

## Übersicht {#overview}

Das [!DNL HTTP] Ziel ist ein [!DNL Adobe Real-Time Customer Data Platform] Streaming-Ziel, mit dem Sie Profil-Daten an [!DNL HTTP] Endpunkte von Drittanbietern senden können.

Um Profil-Daten an [!DNL HTTP] Endpunkte zu senden, müssen Sie zunächst eine Verbindung zum Ziel im [!DNL Adobe Real-Time Customer Data Platform](#connect-destination)Knoten herstellen.

## Nutzungsszenarien {#use-cases}

Das [!DNL HTTP] Ziel richtet sich an Kunden, die XDM-Profil- und Audience-Segmente in allgemeine [!DNL HTTP] Endpunkte exportieren müssen.

[!DNL HTTP] Endpunkte können entweder eigene Systeme oder Lösungen von Drittanbietern sein.

## Connect to Destination {#connect-destination}

1. Wählen Sie unter **[!UICONTROL Verbindungen]** > **[!UICONTROL Ziele]** die Option [!DNL  HTTP API]und wählen Sie **[!UICONTROL Konfigurieren]**.

   ![HTTP-Ziel aktivieren](assets/activate-http-destination.png)

   >[!NOTE]
   >
   >Wenn bereits eine Verbindung zu diesem Ziel besteht, wird auf der Zielkarte die Schaltfläche &quot; **[!UICONTROL Aktivieren]** &quot;angezeigt. Weitere Informationen zum Unterschied zwischen **[!UICONTROL Aktivieren]** und **[!UICONTROL Konfigurieren]** finden Sie im Abschnitt &quot; [Katalog](../destinations/destinations-workspace.md#catalog) &quot;der Dokumentation zum Zielarbeitsbereich.
   ![HTTP-Ziel aktivieren](assets/connect-http-destination.png)

2. Im Schritt &quot; [!UICONTROL Konto] &quot;müssen Sie die Verbindungsdetails des HTTP-Endpunkts definieren. Wählen Sie &quot; **[!UICONTROL Neues Konto]** &quot;und geben Sie die Verbindungsdetails für den HTTP-Endpunkt ein, mit dem Sie eine Verbindung herstellen möchten.
   * **[!UICONTROL httpEndpoint]**: der vollständige HTTP-Endpunkt, an [!DNL URL] den Sie die Profil-Daten senden möchten.
      * Optional können Sie dem [!UICONTROL httpEndpunkt] Abfragen-Parameter hinzufügen [!DNL URL].
   * **[!UICONTROL authEndpoint]**: der vollständige [!DNL URL] HTTP-Endpunkt, der für die [!DNL OAuth2] Authentifizierung verwendet wird.
   * **[!UICONTROL Client-ID]**: der in den [!DNL clientID] Clientberechtigungen verwendete [!DNL OAuth2] Parameter.
   * **[!UICONTROL geheim]**: der in den [!DNL clientSecret] Clientberechtigungen verwendete [!DNL OAuth2] Parameter.

   >[!NOTE]
   >
   >Derzeit werden nur [!DNL OAuth2] Clientberechtigungen unterstützt.

   ![HTTP-Endpunktverbindung](assets/connect-http-endpoint.png)
3. Click **[!UICONTROL Connect to destination]**.
4. Klicken Sie nach erfolgreicher Verbindung auf **[!UICONTROL Weiter]**.
5. Geben Sie im Schritt [!UICONTROL Authentifizierung] die Anmeldeinformationen für die Kontoauthentifizierung ein:
   * **[!UICONTROL Name]**: Geben Sie einen Namen ein, unter dem Sie dieses Ziel in Zukunft erkennen werden.
   * **[!UICONTROL Beschreibung]**: Geben Sie eine Beschreibung ein, mit der Sie dieses Ziel in Zukunft identifizieren können.
   * **[!UICONTROL Benutzerdefinierte Kopfzeilen]**: Geben Sie alle benutzerdefinierten Kopfzeilen ein, die in die Zielaufrufe aufgenommen werden sollen, und befolgen Sie dabei das folgende Format: `header1:value1,header2:value2,...headerN:valueN`.

      >[!IMPORTANT]
      >
      >Für die aktuelle Implementierung ist mindestens ein benutzerdefinierter Header erforderlich. Diese Einschränkung wird in einem zukünftigen Update behoben.
   ![HTTP-Authentifizierung](assets/authentication-http-connection.png)

6. **[!UICONTROL Anwendungsfall]** für das Marketing: Anwendungsfälle für das Marketing geben die Absicht an, für die Daten an das Ziel exportiert werden. Sie können aus von der Adobe definierten Anwendungsfällen für das Marketing auswählen oder einen eigenen Anwendungsfall für das Marketing erstellen. Weitere Informationen zu Anwendungsfällen für das Marketing finden Sie auf der Seite [Datenverwaltung in Echtzeit-CDP](../privacy/data-governance-overview.md#destinations) . Informationen zu den einzelnen Anwendungsfällen für Marketingzwecke, die von der Adobe definiert wurden, finden Sie in der Übersicht über [Datenverwendungsrichtlinien](../../data-governance/policies/overview.md#core-actions).
7. Klicken Sie auf Ziel **[!UICONTROL erstellen]**.

## Segmente aktivieren

Informationen zum Workflow für die Segmentaktivierung finden Sie unter [Profile und Segmente für ein Ziel aktivieren](activate-destinations.md#select-attributes).

## Zielattribute

Beim [[!UICONTROL Auswählen von Attributen]](activate-destinations.md#select-attributes) wird empfohlen, beim [Aktivieren von Segmenten](activate-destinations.md) an einem [!DNL HTTP] Ziel eine eindeutige Kennung aus Ihrem [Vereinigungen-Schema](../../profile/home.md#profile-fragments-and-union-schemas)auszuwählen. Wählen Sie die eindeutige Kennung und alle anderen XDM-Felder aus, die Sie an das Ziel exportieren möchten.

## Exportierte Daten {#exported-data}

Ihre exportierten [!DNL Experience Platform] Daten landen im JSON-Format an Ihrem [!DNL HTTP] Ziel. Das folgende Ereignis enthält beispielsweise das Segmentattribut &quot;E-Mail-Adresse&quot;einer Audience, die sich für ein bestimmtes Profil qualifiziert und ein anderes Segment verlassen hat. Die Identitäten für diesen Potenzieller Kunde sind [!DNL ECID] und E-Mail.

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
