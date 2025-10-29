---
title: Medallia-Verbindung
description: Aktivieren Sie Profile für gezielte Medallia-Umfragen und Feedback-Sammlungen, um die Bedürfnisse und Erwartungen der Kundinnen und Kunden besser zu verstehen.
exl-id: 2c2766eb-7be1-418c-bf17-d119d244de92
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '1098'
ht-degree: 29%

---

# Medallia-Verbindung

## Überblick {#overview}

Aktivieren Sie Profile für gezielte Medallia-Umfragen und Feedback-Sammlungen, um die Bedürfnisse und Erwartungen der Kundinnen und Kunden besser zu verstehen.

>[!IMPORTANT]
>
>Dieser Ziel-Connector und diese Dokumentationsseite werden vom Medallia-Team erstellt und gepflegt. Bei Fragen oder Aktualisierungsanfragen wenden Sie sich bitte direkt an adobe-integrations@medallia.com.

## Anwendungsfälle {#use-cases}

Damit Sie besser verstehen können, wie und wann Sie das Medallia-Ziel verwenden sollten, finden Sie hier einige Beispielanwendungsfälle, die Kundinnen und Kunden von Adobe Experience Platform mit diesem Ziel bewältigen können.

### Anwendungsfall #1

Eine B2B-Marke möchte ihr Onboarding-Programm bewerten und optimieren. Sie möchten personalisierte Umfragen in Echtzeit an Kunden senden, die gerade den Onboarding-Prozess abgeschlossen haben.

### Anwendungsfall #2

Ein retailer möchte die Kundenpräferenzen für die Bestellabwicklung besser verstehen. Sie möchten eine kurze SMS-Umfrage mit einer Frage an Kunden senden, die im letzten Monat Online- und In-Store-Käufe getätigt haben.

## Voraussetzungen {#prerequisites}

Zum Herstellen der Verbindung mit Medallia sind folgende Informationen erforderlich:

* **OAuth Token Endpoint URL**
* **Client ID** (Client-ID)
* **Client Secret** (Client-Geheimnis)
* **API-Gateway-URL**
* **API-Namen importieren**

Arbeiten Sie mit Ihrem Medallia-Versandteam zusammen, um diese Details zu erhalten.

## Unterstützte Identitäten {#supported-identities}

Medallia unterstützt die Aktivierung von Identitäten, die in der folgenden Tabelle beschrieben sind. Erhalten Sie weitere Informationen zu [Identitäten](/help/identity-service/features/namespaces.md).

| Ziel-Identität | Beschreibung | Zu beachten |
|---|---|---|
| email | E-Mail-Adresse | Wählen Sie die E-Mail-Zielidentität aus, wenn Sie E-Mail-Einladungs-Umfragen senden möchten. Wenn ein Profil mit mehreren E-Mail-Adressen verknüpft ist, versendet Medallia den Trigger nur an die erste E-Mail. |
| phone | Telefonnummern im E.164-Format gehasht | Wählen Sie die Zielidentität des Telefons aus, wenn Sie SMS-basierte Umfragen senden möchten. Die Telefonnummer muss im E.164-Format angegeben sein, das ein Pluszeichen (+), eine internationale Landesvorwahl, eine Ortsvorwahl und eine Telefonnummer enthält. Beispiel: (+)(Länder-Code)(Ortsvorwahl)(Telefonnummer). Wenn ein Profil mit mehreren Telefonnummern verknüpft ist, wird die Einladung von Medallia nur an die erste Telefonnummer Trigger. |

{style="table-layout:auto"}

## Exporttyp und -häufigkeit {#export-type-frequency}

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| Element | Typ | Anmerkungen |
|---------|----------|---------|
| Exporttyp | **[!UICONTROL Profile-based]** | Sie exportieren alle neu qualifizierten Mitglieder eines Segments zusammen mit den gewünschten Schemafeldern (z. B. E-Mail-Adresse, Telefonnummer, Nachname), wie im Bildschirm „Profilattribute auswählen“ des Workflows [Zielaktivierung](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes) ausgewählt. |
| Exporthäufigkeit | **[!UICONTROL Streaming]** | Streaming-Ziele sind „immer verfügbare“ API-basierte Verbindungen. Sobald ein Profil in Experience Platform auf der Grundlage einer Zielgruppenauswertung aktualisiert wird, sendet der Connector das Update nachgelagert an die Zielplattform. Lesen Sie mehr über [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Herstellen einer Verbindung mit dem Ziel {#connect}

>[!IMPORTANT]
> 
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die **[!UICONTROL View Destinations]** und **[!UICONTROL Manage Destinations]** Zugriffssteuerungsberechtigungen[. ](/help/access-control/home.md#permissions) Lesen Sie die [Zugriffskontrolle – Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor. Füllen Sie im Workflow zum Konfigurieren des Ziels die Felder aus, die in den beiden folgenden Abschnitten aufgeführt sind.

### Beim Ziel authentifizieren {#authenticate}

Um sich beim Ziel zu authentifizieren, füllen Sie die erforderlichen Felder aus und wählen Sie **[!UICONTROL Connect to destination]** aus.

* **[!UICONTROL OAuth Token Endpoint URL]**: In der Regel ist dies https://instance.medallia.tld/oauth/tenant/token.
* **[!UICONTROL Client ID]**: Erhalten Sie von Ihrem Medallia-Versand-Team.
* **[!UICONTROL Client Secret]**: Erhalten Sie von Ihrem Medallia-Versand-Team.

![Bild mit dem Authentifizierungsbildschirm für dieses Ziel.](/help/destinations/assets/catalog/voice/medallia-destination-oauth.png)

### Ausfüllen der Zieldetails {#destination-details}

Füllen Sie die folgenden erforderlichen und optionalen Felder aus, um Details für das Ziel zu konfigurieren. Ein Sternchen neben einem Feld in der Benutzeroberfläche zeigt an, dass das Feld erforderlich ist.

* **[!UICONTROL Name]**: Ein Name, durch den Sie dieses Ziel in Zukunft erkennen können.
* **[!UICONTROL Description]**: Eine Beschreibung, die Ihnen hilft, dieses Ziel in Zukunft zu identifizieren.
* **[!UICONTROL API Gateway URL]**: Erhalten Sie von Ihrem Medallia-Versand-Team. In der Regel ist dies https://instance-tenant.apis.medallia.com.
* **[!UICONTROL Import API Name]**: Erhalten Sie von Ihrem Medallia-Versand-Team. Name der Medallia Import API (auch als Web-Feed bezeichnet), die in diesem Zusammenhang verwendet werden soll. Sie können verschiedene Zielgruppen aktivieren, um verschiedene Import-APIs zum Trigger verschiedener Umfrageprogramme zu importieren.

![Bild mit dem Bildschirm mit den Zieldetails für dieses Ziel.](/help/destinations/assets/catalog/voice/medallia-destination-details.png)

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie mit dem Eingeben der Details für Ihre Zielverbindung fertig sind, wählen Sie **[!UICONTROL Next]** aus.

## Aktivieren von Zielgruppen für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>* Zum Aktivieren von Daten benötigen Sie die **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** und **[!UICONTROL View Segments]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.
>* Zum Exportieren *Identitäten* benötigen Sie die **[!UICONTROL View Identity Graph]** Zugriffssteuerungsberechtigung[ ](/help/access-control/home.md#permissions). <br> ![Wählen Sie einen im Workflow hervorgehobenen Identity-Namespace aus, um Zielgruppen für Ziele zu aktivieren.](/help/destinations/assets/overview/export-identities-to-destination.png "Wählen Sie einen im Workflow hervorgehobenen Identity-Namespace aus, um Zielgruppen für Ziele zu aktivieren."){width="100" zoomable="yes"}

Anweisungen zum Aktivieren von Zielgruppen für dieses Ziel finden Sie unter [Aktivieren von Profilen und Zielgruppen für Streaming-Zielgruppen-Exportziele](/help/destinations/ui/activate-segment-streaming-destinations.md).

### Zuordnen von Attributen und Identitäten {#map}

Die folgenden Ziel-Identity-Namespaces müssen je nach Anwendungsfall zugeordnet werden:

* Bei E-Mail-basierten Umfragen muss **E-Mail** als Zielfeld mithilfe von **Zielfeld** > **Identity-Namespace auswählen** > **email zugeordnet werden**
* Bei SMS-basierten Umfragen muss **Telefon** als Zielfeld mithilfe von **Zielfeld** > **Identity-Namespace auswählen** > **Telefon** zugeordnet werden. Telefonnummern müssen im E.164-Format sein, das ein Pluszeichen (+), eine internationale Landesvorwahl, eine Ortsvorwahl und eine Telefonnummer enthält

Es wird dringend empfohlen, auch zusätzliche benutzerdefinierte Zielgruppenattribute zuzuordnen, um personalisierte Umfragen zu erstellen und zusätzliche Kundeninformationen an den Umfragedatensatz anzuhängen:

* Personalisierte Umfragen richten sich in der Regel an den Kunden nach Namen

   * Ordnen Sie den Vornamen des Kunden zu **Zielfeld** > **Benutzerdefinierte Attribute auswählen** > **Attributname** > **firstName**
   * Ordnen Sie den Nachnamen des Kunden zu **Zielfeld** > **Benutzerdefinierte Attribute auswählen** > **Attributname** > **lastName**

* Fügen Sie nach Bedarf Zuordnungen für beliebige andere benutzerdefinierte Zielattribute hinzu

![Bild mit einer Beispielzuordnung für Identitäten und Attribute.](/help/destinations/assets/catalog/voice/medallia-destination-mapping.png)

>[!IMPORTANT]
> 
> Geben Sie für Ihr Medallia-Versand-Team die genauen **Attributnamen** für jedes benutzerdefinierte Zielattribut frei, das Sie mithilfe von **Zielfeld** > **Benutzerdefinierte Attribute auswählen** > **Attributname**. Sie können einen Screenshot der Zuordnungsseite erstellen, um ihn direkt freizugeben.

## Exportierte Daten {#exported-data}

Nachdem Sie Ihr(e) Segment(e) für das Ziel aktiviert haben, informieren Sie Ihr Medallia-Versand-Team, das die exportierten Daten von Adobe Experience Platform nach Medallia überprüfen kann. Beachten Sie, dass Umfragen innerhalb von Medallia nur nach erfolgreicher Datenüberprüfung aktiviert werden können. Zuvor werden Daten nach Medallia exportiert, aber keine Umfragen an Kunden Trigger.

Nachfolgend finden Sie eine JSON-Beispieldatei der exportierten Daten, die die Beispielzuordnung aus dem obigen Screenshot im Abschnitt **Zuordnungsattribute und Identitäten** verwendet:

```json
[
    {
        "profile_raw_encoded": "eyJhdHRyaWJ1dGVzIjp7ImZpcnN",
        "email": "johnsmith@example.com",
        "aep_segments_new": ["c1c3edcc-07cb-4f66-b5dd-aff485148aba"],
        "aep_segments_existing": [],
        "aep_segments_removed": [],
        "firstname":  "John" ,
        "lastname":  "Smith",
        "contactId": "jsmith120002",
    }
]
```

## Datennutzung und -Governance {#data-usage-governance}

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Ausführliche Informationen darüber, wie [!DNL Adobe Experience Platform] Data Governance erzwingt, finden Sie unter [Data Governance – Übersicht](/help/data-governance/home.md).
