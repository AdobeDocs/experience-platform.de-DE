---
keywords: Werbung; criteo;
title: Crito-Verbindung
description: Criteo ermöglicht vertrauenswürdige und wirkungsvolle Werbung, um jedem Verbraucher im offenen Internet reichhaltigere Erlebnisse zu bieten. Mit dem weltweit größten Commerce-Datensatz und einer erstklassigen KI stellt Criteo sicher, dass jeder Touchpoint über die Einkaufs-Journey personalisiert ist, um Kunden zur richtigen Zeit mit der richtigen Anzeige zu erreichen.
exl-id: e6f394b2-ab82-47bb-8521-1cf9d01a203b
source-git-commit: dd18350387aa6bdeb61612f0ccf9d8d2223a8a5d
workflow-type: tm+mt
source-wordcount: '1005'
ht-degree: 8%

---

# (Beta) Criteo-Verbindung

## Übersicht {#overview}

>[!IMPORTANT]
>
>Diese Dokumentationsseite wurde von Criteo erstellt. Dies ist derzeit ein Beta-Produkt und die Funktionalität kann sich ändern. Bei Fragen oder Aktualisierungsanfragen wenden Sie sich bitte direkt an Criteo [here](mailto:criteoTechnicalPartnerships@criteo.com).

Criteo ermöglicht vertrauenswürdige und wirkungsvolle Werbung, um jedem Verbraucher im offenen Internet reichhaltigere Erlebnisse zu bieten. Mit dem weltweit größten Commerce-Datensatz und einer erstklassigen KI stellt Criteo sicher, dass jeder Touchpoint über die Einkaufs-Journey personalisiert ist, um Kunden zur richtigen Zeit mit der richtigen Anzeige zu erreichen.

## Voraussetzungen {#prerequisites}

* Sie benötigen ein Administratorbenutzerkonto für [Criteo Management Center](https://marketing.criteo.com).
* Sie benötigen Ihre Criteo Advertiser ID (fragen Sie Ihren Criteo-Kontakt, wenn Sie diese ID nicht haben).
* Sie müssen [!DNL GUM caller ID], falls Sie [!DNL GUM ID] als Kennung.

## Einschränkungen {#limitations}

* Criteo unterstützt derzeit nicht das Entfernen von Benutzern aus Zielgruppen.
* Criteo akzeptiert nur [!DNL SHA-256]-Hash- und Text-E-Mails (zu konvertieren in [!DNL SHA-256] vor dem Senden). Bitte senden Sie keine personenbezogenen Daten (personenbezogene Daten, wie z.B. die Namen von Einzelpersonen oder Telefonnummern).
* Criteo benötigt mindestens eine Kennung, die vom Client bereitgestellt werden muss. Prioritäten [!DNL GUM ID] als Kennung anstelle von Hash-E-Mail, da sie zu einer besseren Übereinstimmungsrate beiträgt.

![Voraussetzungen](../../assets/catalog/advertising/criteo/prerequisites.png)

## Unterstützte Identitäten {#supported-identities}

Criteo unterstützt die Aktivierung von Identitäten, die in der folgenden Tabelle beschrieben sind. Weitere Informationen [identities](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=de#getting-started).

| Zielgruppenidentität | Beschreibung | Zu beachten |
| --- | --- | --- |
| `email_sha256` | Mit dem SHA-256-Algorithmus gehashte E-Mail-Adressen | Adobe Experience Platform unterstützt sowohl einfache als auch SHA-256-Hash-E-Mail-Adressen. Wenn Ihr Quellfeld ungehashte Attribute enthält, überprüfen Sie die [!UICONTROL Umwandlung anwenden] , damit Platform die Daten bei der Aktivierung automatisch hasst. |
| `gum_id` | Criteo [!DNL GUM] Cookie-Kennung | [!DNL GUM IDs] Kunden die Möglichkeit geben, eine Korrespondenz zwischen ihrem Benutzeridentifizierungssystem und der Benutzeridentifizierung von Criteo zu pflegen ([!DNL UID]). Wenn der Kennungstyp `GUM`, einen zusätzlichen Parameter, die [!DNL GUM Caller ID], muss ebenfalls einbezogen werden. Wenden Sie sich an Ihr Criteo-Account-Team, um Informationen zu den entsprechenden [!DNL GUM Caller ID] oder weitere Informationen dazu zu erhalten `GUM` bei Bedarf synchronisieren. |

## Exportart und -frequenz {#export-type-frequency}

Informationen zum Zielexporttyp und zur Häufigkeit finden Sie in der unten stehenden Tabelle.

| Element | Typ | Anmerkungen |
| --- | --- | --- |
| Exporttyp | Segmentexport | Sie exportieren alle Mitglieder eines Segments (Zielgruppe) mit den IDs (Name, Telefonnummer oder andere), die im [!DNL Criteo] Ziel. |
| Exporthäufigkeit | Streaming | Streaming-Ziele sind &quot;immer auf&quot;-API-basierte Verbindungen. Sobald ein Profil in Experience Platform auf der Grundlage einer Segmentbewertung aktualisiert wird, sendet der Connector das Update nachgelagert an die Zielplattform. Mehr dazu [Streaming-Ziele](../../destination-types.md#streaming-destinations). |

## Anwendungsfälle {#use-cases}

Damit Sie besser verstehen können, wie Sie die [!DNL Criteo] Ziel finden Sie hier einige Ziele, die Adobe Experience Platform-Kunden mit erreichen können. [!DNL Criteo]:

### Anwendungsfall 1: Traffic abrufen

Präsentieren Sie Ihr Unternehmen mit relevanten Produktangeboten und flexiblen Kreativen. Mit intelligenten Produktempfehlungen stellen Ihre Anzeigen automatisch die Produkte dar, die am ehesten Trigger zu Besuchen und Interaktionen sind. Flexibles Targeting ermöglicht Ihnen das Erstellen von Zielgruppen aus dem Commerce-Datensatz von Criteo oder aus Ihren eigenen Interessenten-Listen und Adobe-CDP-Segmenten.

### Anwendungsfall 2: Website-Konversionen erhöhen

Wenn Besucher Ihre Website verlassen, erinnern Sie sie daran, was ihnen bei Retargeting-Anzeigen fehlt, die Konversionen steigern, indem sie spezielle Angebote und hyperrelevante Angebote anzeigen, egal wohin sie als Nächstes gehen. Verbinden Sie Ihr Adobe-CDP-Segment, um Bestandskunden oder Kunden ähnlich Ihren treuesten Käufern erneut anzusprechen.

## Verbinden mit Criteo {#connect}

>[!IMPORTANT]
> 
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die **[!UICONTROL Ziele verwalten]** [Zugriffsberechtigung](/help/access-control/home.md#permissions). Lesen Sie die [Zugriffskontrolle - Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im Abschnitt [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor.

### Bei Criteo authentifizieren

Die Schritte zum Verbinden lauten wie folgt:

1. Melden Sie sich bei Adobe Experience Platform an und verbinden Sie sich mit dem Criteo-Ziel.

   ![Anmelden](../../assets/catalog/advertising/criteo/connect-destination.png)

1. Sie werden zu Criteo umgeleitet, um die Verbindung zu autorisieren. Möglicherweise müssen Sie sich zunächst mit Ihren Criteo-Anmeldedaten anmelden:

   ![Criteo-Anmeldung](../../assets/catalog/advertising/criteo/log-in-1.png)

   ![Criteo-Anmeldung](../../assets/catalog/advertising/criteo/log-in-2.png)

   ![Criteo-Anmeldung](../../assets/catalog/advertising/criteo/log-in-3.png)


### Verbindungsparameter {#connection-parameters}

Geben Sie nach der Authentifizierung beim Ziel die folgenden Verbindungsparameter ein.

![Verbindungsparameter](../../assets/catalog/advertising/criteo/connection-parameters.png)

| Feld | Beschreibung | Erforderlich |
| --- | --- | --- |
| Name | Ein Name, der Ihnen dabei hilft, dieses Ziel in der Zukunft zu erkennen. Der Name, den Sie hier auswählen, ist der [!DNL Audience] Name in Criteo Management Center und kann zu einem späteren Zeitpunkt nicht geändert werden. | Ja |
| Beschreibung | Eine Beschreibung, die Ihnen dabei hilft, dieses Ziel in der Zukunft zu identifizieren. | Nein |
| API-Version | API-Version von Criteo. Wählen Sie Vorschau aus. | Ja |
| Advertiser-ID | Criteo Advertiser ID Ihres Unternehmens. Wenden Sie sich an Ihren Criteo-Kundenbetreuer, um diese Informationen zu erhalten. | Ja |
| Criteo [!DNL GUM caller ID] | [!DNL GUM Caller ID] Ihrer Organisation. Wenden Sie sich an Ihr Criteo-Account-Team, um Informationen zu den entsprechenden [!DNL GUM Caller ID] oder weitere Informationen dazu zu erhalten [!DNL GUM] bei Bedarf synchronisieren. | Ja, wann immer [!DNL GUM ID] wird als Kennung bereitgestellt |

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen über den Status des Datenflusses an Ihr Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnungen finden Sie im Handbuch zu [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie alle Details für Ihre Zielverbindung angegeben haben, wählen Sie **[!UICONTROL Nächste]**.

## Aktivieren von Segmenten für dieses Ziel {#activate-segments}

>[!IMPORTANT]
> 
>Um Daten zu aktivieren, benötigen Sie die **[!UICONTROL Ziele verwalten]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Zugriffskontrolle - Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Lesen [Aktivieren von Profilen und Segmenten für Streaming-Segmentexportziele](../../ui/activate-segment-streaming-destinations.md) für Anweisungen zum Aktivieren von Zielgruppensegmenten für dieses Ziel.

## Exportierte Daten {#exported-data}

Sie können die exportierten Segmente im [Zentrum für die Verwaltung von Kriterien](https://marketing.criteo.com/audience-manager/dashboard).

Die bei der [!DNL Criteo] -Verbindung sieht in etwa wie folgt aus:

```json
{
  "data": {
    "type": "ContactlistWithUserAttributesAmendment",
    "attributes": {
      "operation": "add",
      "identifierType": "gum",
      "gumCallerId": "123",
      "identifiers": [
        {
          "identifier": "456",
          "attributes": [
            { "key": "ctoid_GumCaller", "value": "123" },
            { "key": "ctoid_Gum", "value": "456" },
            {
              "key": "ctoid_HashedEmail",
              "value": "98833030dc03751f2b2c1a0017078975fdae951aa6908668b3ec422040f2d4be"
            }
          ]
        }
      ]
    }
  }
}
```

## Datennutzung und -Governance {#data-usage}

Alle Adobe Experience Platform-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Detaillierte Informationen dazu, wie Adobe Experience Platform Data Governance durchsetzt, finden Sie im Abschnitt [Data Governance - Übersicht](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=en).

## Weitere Ressourcen

* [Criteo Help Center](https://help.criteo.com/kb/en)
* [Criteo Developer Portal](https://developers.criteo.com)
