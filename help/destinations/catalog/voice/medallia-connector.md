---
title: Medallia-Verbindung
description: Aktivieren Sie Profile für gezielte Medallia-Umfragen und Feedback-Sammlungen, um die Bedürfnisse und Erwartungen der Kundinnen und Kunden besser zu verstehen.
exl-id: 2c2766eb-7be1-418c-bf17-d119d244de92
source-git-commit: dd18350387aa6bdeb61612f0ccf9d8d2223a8a5d
workflow-type: tm+mt
source-wordcount: '1102'
ht-degree: 10%

---

# Medallia-Verbindung

## Übersicht {#overview}

Aktivieren Sie Profile für gezielte Medallia-Umfragen und Feedback-Sammlungen, um die Bedürfnisse und Erwartungen der Kundinnen und Kunden besser zu verstehen.

>[!IMPORTANT]
>
>Diese Dokumentationsseite wurde vom Medallia-Team erstellt. Bei Fragen oder Aktualisierungsanfragen wenden Sie sich bitte direkt an adobe-integrations@medallia.com.

## Anwendungsbeispiele {#use-cases}

Um Ihnen zu helfen, besser zu verstehen, wie und wann Sie das Medallia-Ziel verwenden sollten, finden Sie hier Beispielanwendungsfälle, die Adobe Experience Platform-Kunden mit diesem Ziel lösen können.

### Anwendungsfall 1

Eine B2B Marke möchte ihr Onboarding-Programm bewerten und optimieren. Sie möchten personalisierte Umfragen in Echtzeit an Kunden senden, die gerade das Onboarding abgeschlossen haben.

### Anwendungsfall 2

Ein Einzelhändler sucht nach einem besseren Verständnis der Kundenpräferenzen für die Erfüllung seiner Bestellung. Sie möchten Kunden, die im vergangenen Monat Online- und In-Store-Käufe getätigt haben, eine kurze SMS-Umfrage mit einer Frage senden.

## Voraussetzungen {#prerequisites}

Die folgenden Informationen sind erforderlich, um die Medallia-Verbindung herzustellen:
* **OAuth-Token-Endpunkt-URL**
* **Client-ID**
* **Client-Geheimnis**
* **API-Gateway-URL**
* **Import API Name**

Wenden Sie sich an Ihr Medallia-Versand-Team, um diese Details zu erhalten.

## Unterstützte Identitäten {#supported-identities}

Medallia unterstützt die Aktivierung von Identitäten, die in der folgenden Tabelle beschrieben sind. Weitere Informationen [identities](/help/identity-service/namespaces.md).

| Zielgruppenidentität | Beschreibung | Zu beachten |
|---|---|---|
| email | E-Mail Adresse | Wählen Sie die E-Mail-Zielidentität aus, wenn Sie Umfragen per E-Mail einladen möchten. Wenn ein Profil mit mehreren E-Mail-Adressen verknüpft ist, wird die Einladung nur an die erste E-Mail Trigger. |
| phone | Telefonnummern im Format E.164 gehasht | Wählen Sie die Telefonzielgruppenkennung aus, wenn Sie SMS-basierte Umfragen senden möchten. Die Telefonnummer muss im E.164-Format vorliegen, das ein Pluszeichen (+), eine internationale Telefonnummer, eine Ortsvorwahl und eine Telefonnummer enthält. Beispiel: (+)(Landesvorwahl)(Ortsvorwahl)(Telefonnummer). Wenn ein Profil mit mehreren Telefonnummern verknüpft ist, Trigger Medallia nur die Einladung zur ersten Telefonnummer. |

{style=&quot;table-layout:auto&quot;}

## Exportart und -frequenz {#export-type-frequency}

Informationen zum Zielexporttyp und zur Häufigkeit finden Sie in der unten stehenden Tabelle.

| Element | Typ | Anmerkungen |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Profilbasiert]** | Sie exportieren alle neu qualifizierten Mitglieder eines Segments zusammen mit den gewünschten Schemafeldern (z. B.: E-Mail-Adresse, Telefonnummer, Nachname), wie im Bildschirm Profilattribute im [Zielaktivierungs-Workflow](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Exporthäufigkeit | **[!UICONTROL Streaming]** | Streaming-Ziele sind &quot;immer auf&quot;-API-basierte Verbindungen. Sobald ein Profil in Experience Platform auf der Grundlage einer Segmentbewertung aktualisiert wird, sendet der Connector das Update nachgelagert an die Zielplattform. Mehr dazu [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## Herstellen einer Verbindung mit der Datenbank {#connect}

>[!IMPORTANT]
> 
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die **[!UICONTROL Ziele verwalten]** [Zugriffsberechtigung](/help/access-control/home.md#permissions). Lesen Sie die [Zugriffskontrolle - Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im Abschnitt [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor. Füllen Sie im Workflow zum Konfigurieren des Ziels die Felder aus, die in den beiden folgenden Abschnitten aufgeführt sind.

### An Ziel authentifizieren {#authenticate}

Um sich beim Ziel zu authentifizieren, füllen Sie die erforderlichen Felder aus und wählen Sie **[!UICONTROL Mit Ziel verbinden]**.

* **[!UICONTROL OAuth-Token-Endpunkt-URL]**: In der Regel hat das Format https://instance.medallia.tld/oauth/tenant/token.
* **[!UICONTROL Client-ID]**: Besorgen Sie sich bei Ihrem Medallia-Versand-Team.
* **[!UICONTROL Client Secret]**: Besorgen Sie sich bei Ihrem Medallia-Versand-Team.

![Bild, das den Authentifizierungsbildschirm für dieses Ziel anzeigt.](/help/destinations/assets/catalog/voice/medallia-destination-oauth.png)

### Zieldetails ausfüllen {#destination-details}

Füllen Sie die folgenden erforderlichen und optionalen Felder aus, um Details für das Ziel zu konfigurieren. Ein Sternchen neben einem Feld in der Benutzeroberfläche zeigt an, dass das Feld erforderlich ist.

* **[!UICONTROL Name]**: Ein Name, mit dem Sie dieses Ziel in der Zukunft erkennen werden.
* **[!UICONTROL Beschreibung]**: Eine Beschreibung, die Ihnen dabei hilft, dieses Ziel in der Zukunft zu identifizieren.
* **[!UICONTROL API-Gateway-URL]**: Besorgen Sie sich bei Ihrem Medallia-Versand-Team. In der Regel hat das Format https://instance-tenant.apis.medallia.com.
* **[!UICONTROL Import API Name]**: Besorgen Sie sich bei Ihrem Medallia-Versand-Team. Name der Media Import-API (auch als Web-Feed bezeichnet), die in dieser Verbindung verwendet werden soll. Sie können verschiedene Segmente für verschiedene Import-APIs aktivieren, um verschiedene Umfrageprogramme Trigger.

![Bild, das den Bildschirm mit den Zieldetails für dieses Ziel anzeigt.](/help/destinations/assets/catalog/voice/medallia-destination-details.png)

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen über den Status des Datenflusses an Ihr Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnungen finden Sie im Handbuch zu [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie alle Details für Ihre Zielverbindung angegeben haben, wählen Sie **[!UICONTROL Nächste]**.

## Aktivieren von Segmenten für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>Um Daten zu aktivieren, benötigen Sie die **[!UICONTROL Ziele verwalten]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Zugriffskontrolle - Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Lesen [Aktivieren von Profilen und Segmenten für Streaming-Segmentexportziele](/help/destinations/ui/activate-segment-streaming-destinations.md) für Anweisungen zum Aktivieren von Zielgruppensegmenten für dieses Ziel.

### Zuordnen von Attributen und Identitäten {#map}

Die folgenden Ziel-Identitäts-Namespaces müssen je nach Anwendungsfall zugeordnet werden:
* Bei E-Mail-basierten Umfragen: **email** muss als Zielfeld mit **Zielfeld** > **Identitäts-Namespace auswählen** > **email**
* Bei SMS-basierten Umfragen: **phone** muss als Zielfeld mit **Zielfeld** > **Identitäts-Namespace auswählen** > **phone**. Die Telefonnummern müssen im E.164-Format vorliegen, das ein Pluszeichen (+), ein internationales Rufzeichen, eine Ortsvorwahl und eine Telefonnummer enthält.

Es wird dringend empfohlen, zusätzliche benutzerdefinierte Zielattribute zuzuordnen, um personalisierte Umfragen zu erstellen und zusätzliche Informationen über den Kunden an den Umfragedatensatz anzuhängen:

* Personalisierte Umfragen richten sich in der Regel nach Name an den Kunden
   * Den Vornamen des Kunden zuordnen zu **Zielfeld** > **Benutzerdefinierte Attribute auswählen** > **Attributname** > **firstname**
   * Ordnen Sie den Nachnamen des Kunden zu **Zielfeld** > **Benutzerdefinierte Attribute auswählen** > **Attributname** > **lastname**
* Fügen Sie nach Bedarf Zuordnungen für andere benutzerdefinierte Zielattribute hinzu.

![Bild, das eine Beispielzuordnung für Identitäten und Attribute anzeigt.](/help/destinations/assets/catalog/voice/medallia-destination-mapping.png)

>[!IMPORTANT]
> 
> Geben Sie für Ihr Medallia-Versandteam die genaue **Attributnamen** für jedes benutzerdefinierte Zielattribut, das Sie zuordnen, **Zielfeld** > **Benutzerdefinierte Attribute auswählen** > **Attributname**. Sie können einen Screenshot der Zuordnungsseite erstellen, um sie direkt freizugeben.

## Exportierte Daten {#exported-data}

Nachdem Sie Ihre Segmente für das Ziel aktiviert haben, informieren Sie Ihr Medallia-Versandteam, das die exportierten Daten aus Adobe Experience Platform nach Medallia validieren kann. Beachten Sie, dass Umfragen nur nach erfolgreicher Datenüberprüfung in Medallia aktiviert werden können. zuvor werden Daten nach Medallia exportiert, aber keine Umfragen an Kunden Trigger.

Nachfolgend finden Sie ein Beispiel für eine JSON-Datei der exportierten Daten, die die Beispielzuordnung aus dem obigen Screenshot im Abschnitt **Zuordnen von Attributen und Identitäten** Abschnitt:

```json
[
    {
        "profile_raw_encoded": "eyJhdHRyaWJ1dGVzIjp7ImZpcnN",
        "email": "johnsmith@example.com",
        "aep_segments_new": ["c1c3edcc-07cb-4f66-b5dd-aff485148aba"],
        "aep_segments_existing": [],
        "aep_segments_removed": [],
        "firstname":  “John” ,
        "lastname":  “Smith”,
        "contactId": "jsmith120002",
    }
]
```

## Datennutzung und -Governance {#data-usage-governance}

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Detaillierte Informationen zur [!DNL Adobe Experience Platform] erzwingt Data Governance, siehe [Data Governance - Übersicht](/help/data-governance/home.md).
