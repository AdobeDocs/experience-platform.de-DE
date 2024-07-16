---
title: Medallia-Verbindung
description: Aktivieren Sie Profile für gezielte Medallia-Umfragen und Feedback-Sammlungen, um die Bedürfnisse und Erwartungen der Kundinnen und Kunden besser zu verstehen.
exl-id: 2c2766eb-7be1-418c-bf17-d119d244de92
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '1135'
ht-degree: 33%

---

# Medallia-Verbindung

## Übersicht {#overview}

Aktivieren Sie Profile für gezielte Medallia-Umfragen und Feedback-Sammlungen, um die Bedürfnisse und Erwartungen der Kundinnen und Kunden besser zu verstehen.

>[!IMPORTANT]
>
>Diese Ziel-Connector- und Dokumentationsseite werden vom Medallia-Team erstellt und gepflegt. Bei Fragen oder Aktualisierungsanfragen wenden Sie sich bitte direkt an adobe-integrations@medallia.com.

## Anwendungsfälle {#use-cases}

Um Ihnen zu helfen, besser zu verstehen, wie und wann Sie das Medallia-Ziel verwenden sollten, finden Sie hier Beispielanwendungsfälle, die Adobe Experience Platform-Kunden mit diesem Ziel lösen können.

### Anwendungsfall 1

Eine B2B Marke möchte ihr Onboarding-Programm bewerten und optimieren. Sie möchten personalisierte Umfragen in Echtzeit an Kunden senden, die gerade das Onboarding abgeschlossen haben.

### Anwendungsfall 2

Ein Einzelhändler sucht nach einem besseren Verständnis der Kundenpräferenzen für die Erfüllung seiner Bestellung. Sie möchten Kunden, die im vergangenen Monat Online- und In-Store-Käufe getätigt haben, eine kurze SMS-Umfrage mit einer Frage senden.

## Voraussetzungen {#prerequisites}

Die folgenden Informationen sind erforderlich, um die Medallia-Verbindung herzustellen:
* **OAuth-Token-Endpunkt-URL**
* **Client ID** (Client-ID)
* **Client Secret** (Client-Geheimnis)
* **API-Gateway-URL**
* **Import API Name**

Wenden Sie sich an Ihr Medallia-Versand-Team, um diese Details zu erhalten.

## Unterstützte Identitäten {#supported-identities}

Medallia unterstützt die Aktivierung von Identitäten, die in der folgenden Tabelle beschrieben sind. Erhalten Sie weitere Informationen zu [Identitäten](/help/identity-service/features/namespaces.md).

| Ziel-Identität | Beschreibung | Zu beachten |
|---|---|---|
| E-Mail | E-Mail-Adresse | Wählen Sie die E-Mail-Zielidentität aus, wenn Sie Umfragen per E-Mail einladen möchten. Wenn ein Profil mit mehreren E-Mail-Adressen verknüpft ist, wird die Einladung nur an die erste E-Mail Trigger. |
| phone | Telefonnummern im Format E.164 gehasht | Wählen Sie die Telefonzielgruppenkennung aus, wenn Sie SMS-basierte Umfragen senden möchten. Die Telefonnummer muss im E.164-Format vorliegen, das ein Pluszeichen (+), eine internationale Telefonnummer, eine Ortsvorwahl und eine Telefonnummer enthält. Beispiel: (+)(Ländercode)(Gebietscode)(Telefonnummer). Wenn ein Profil mit mehreren Telefonnummern verknüpft ist, Trigger Medallia nur die Einladung zur ersten Telefonnummer. |

{style="table-layout:auto"}

## Exporttyp und -häufigkeit {#export-type-frequency}

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| Element | Typ | Anmerkungen |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Profilbasiert]** | Sie exportieren alle neu qualifizierten Mitglieder eines Segments zusammen mit den gewünschten Schemafeldern (z. B. E-Mail-Adresse, Telefonnummer, Nachname), wie im Bildschirm &quot;Profilattribute auswählen&quot;des [Zielaktivierungs-Workflows](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes) ausgewählt. |
| Exporthäufigkeit | **[!UICONTROL Streaming]** | Streaming-Ziele sind „immer verfügbare“ API-basierte Verbindungen. Sobald ein Profil in Experience Platform auf der Grundlage einer Zielgruppenauswertung aktualisiert wird, sendet der Connector das Update nachgelagert an die Zielplattform. Lesen Sie mehr über [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Herstellen einer Verbindung mit dem Ziel {#connect}

>[!IMPORTANT]
> 
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die Zugriffssteuerungsberechtigungen **[!UICONTROL Ziele anzeigen]** und **[!UICONTROL Ziele verwalten]** [. ](/help/access-control/home.md#permissions) Lesen Sie die [Zugriffskontrolle – Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor. Füllen Sie im Workflow zum Konfigurieren des Ziels die Felder aus, die in den beiden folgenden Abschnitten aufgeführt sind.

### Beim Ziel authentifizieren {#authenticate}

Um sich beim Ziel zu authentifizieren, füllen Sie die erforderlichen Felder aus und wählen Sie **[!UICONTROL Mit Ziel verbinden]** aus.

* **[!UICONTROL OAuth-Token-Endpunkt-URL]**: In der Regel wird https://instance.medallia.tld/oauth/tenant/token verwendet.
* **[!UICONTROL Client-ID]**: Rufen Sie sich von Ihrem Medallia-Bereitstellungsteam ab.
* **[!UICONTROL Client-Geheimnis]**: Besorgen Sie sich von Ihrem Medallia-Versandteam.

![Bild, das den Authentifizierungsbildschirm für dieses Ziel anzeigt.](/help/destinations/assets/catalog/voice/medallia-destination-oauth.png)

### Ausfüllen der Zieldetails {#destination-details}

Füllen Sie die folgenden erforderlichen und optionalen Felder aus, um Details für das Ziel zu konfigurieren. Ein Sternchen neben einem Feld in der Benutzeroberfläche zeigt an, dass das Feld erforderlich ist.

* **[!UICONTROL Name]**: Ein Name, durch den Sie dieses Ziel in Zukunft erkennen können.
* **[!UICONTROL Beschreibung]**: Eine Beschreibung, die Ihnen hilft, dieses Ziel in Zukunft zu identifizieren.
* **[!UICONTROL API-Gateway-URL]**: Rufen Sie sich von Ihrem Medallia-Versandteam ab. In der Regel hat das Format https://instance-tenant.apis.medallia.com.
* **[!UICONTROL Import API Name]**: Rufen Sie sich von Ihrem Medallia-Bereitstellungsteam ab. Name der Media Import-API (auch als Web-Feed bezeichnet), die in dieser Verbindung verwendet werden soll. Sie können verschiedene Zielgruppen für verschiedene Import-APIs aktivieren, um verschiedene Umfrageprogramme Trigger.

![Bild, das den Bildschirm mit den Zieldetails für dieses Ziel anzeigt.](/help/destinations/assets/catalog/voice/medallia-destination-details.png)

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie alle Details für Ihre Zielverbindung eingegeben haben, klicken Sie auf **[!UICONTROL Weiter]**.

## Aktivieren von Zielgruppen für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>* Um Daten zu aktivieren, benötigen Sie die Zugriffssteuerungsberechtigungen **[!UICONTROL Ziele anzeigen]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]** [. ](/help/access-control/home.md#permissions) Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.
>* Um *identities* zu exportieren, benötigen Sie die Zugriffssteuerungsberechtigung **[!UICONTROL Identitätsdiagramm anzeigen]** [ ](/help/access-control/home.md#permissions). <br> ![Wählen Sie den im Workflow hervorgehobenen Identitäts-Namespace aus, um Zielgruppen für Ziele zu aktivieren.](/help/destinations/assets/overview/export-identities-to-destination.png "Wählen Sie den im Workflow hervorgehobenen Identitäts-Namespace aus, um Zielgruppen für Ziele zu aktivieren."){width="100" zoomable="yes"}

Anweisungen zum Aktivieren von Zielgruppen für dieses Ziel finden Sie unter [Aktivieren von Profilen und Zielgruppen für Streaming-Zielgruppen-Exportziele](/help/destinations/ui/activate-segment-streaming-destinations.md).

### Zuordnen von Attributen und Identitäten {#map}

Die folgenden Ziel-Identitäts-Namespaces müssen je nach Anwendungsfall zugeordnet werden:
* Bei E-Mail-basierten Umfragen muss **E-Mail** als Zielfeld mithilfe von **Zielfeld** > **Identitäts-Namespace auswählen** > **E-Mail** zugeordnet werden.
* Bei SMS-basierten Umfragen muss **phone** als Zielfeld mithilfe von **Zielfeld** > **Identitäts-Namespace auswählen** > **phone** zugeordnet werden. Die Telefonnummern müssen im E.164-Format vorliegen, das ein Pluszeichen (+), ein internationales Rufzeichen, eine Ortsvorwahl und eine Telefonnummer enthält.

Es wird dringend empfohlen, zusätzliche benutzerdefinierte Zielattribute zuzuordnen, um personalisierte Umfragen zu erstellen und zusätzliche Informationen über den Kunden an den Umfragedatensatz anzuhängen:

* Personalisierte Umfragen richten sich in der Regel nach Name an den Kunden
   * Weisen Sie den Vornamen des Kunden **Zielfeld** > **Benutzerdefinierte Attribute auswählen** > **Attributname** > **Vorname** zu
   * Ordnen Sie den Nachnamen des Kunden **Zielfeld** > **Benutzerdefinierte Attribute auswählen** > **Attributname** > **lastname** zu
* Fügen Sie nach Bedarf Zuordnungen für andere benutzerdefinierte Zielattribute hinzu.

![Bild mit einer Beispielzuordnung für Identitäten und Attribute.](/help/destinations/assets/catalog/voice/medallia-destination-mapping.png)

>[!IMPORTANT]
> 
> Geben Sie für Ihr Medallia-Versandteam die exakten **Attributnamen** für jedes benutzerdefinierte Zielattribut frei, das Sie mit **Zielfeld** > **Benutzerdefinierte Attribute auswählen** > **Attributname** zuordnen. Sie können einen Screenshot der Zuordnungsseite erstellen, um sie direkt freizugeben.

## Exportierte Daten {#exported-data}

Nachdem Sie Ihre Segmente für das Ziel aktiviert haben, informieren Sie Ihr Medallia-Versandteam, das die exportierten Daten aus Adobe Experience Platform nach Medallia validieren kann. Beachten Sie, dass Umfragen nur nach erfolgreicher Datenüberprüfung in Medallia aktiviert werden können. Zuvor werden Daten nach Medallia exportiert, aber keine Umfragen an Kunden Trigger.

Nachfolgend finden Sie ein Beispiel-JSON der exportierten Daten, das die Beispielzuordnung aus dem obigen Screenshot im Abschnitt **Attribute und Identitäten zuordnen** verwendet:

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
