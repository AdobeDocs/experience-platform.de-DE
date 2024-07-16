---
keywords: Werbung; Kriterien;
title: Crito-Verbindung
description: Criteo ermöglicht vertrauenswürdige und wirkungsvolle Werbung, um jedem Verbraucher im offenen Internet reichhaltigere Erlebnisse zu bieten. Mit dem weltweit größten Commerce-Datensatz und einer erstklassigen KI stellt Criteo sicher, dass jeder Touchpoint über die Einkaufs-Journey personalisiert ist, um Kunden zur richtigen Zeit mit der richtigen Anzeige zu erreichen.
exl-id: e6f394b2-ab82-47bb-8521-1cf9d01a203b
source-git-commit: c3ef732ee82f6c0d56e89e421da0efc4fbea2c17
workflow-type: tm+mt
source-wordcount: '1029'
ht-degree: 25%

---

# (Beta) Criteo-Verbindung

## Übersicht {#overview}

>[!IMPORTANT]
>
>Diese Ziel-Connector- und Dokumentationsseite werden von Criteo erstellt und gepflegt. Dies ist derzeit ein Beta-Produkt, und die Funktionalität kann sich ändern. Bei Fragen oder Aktualisierungsanfragen wenden Sie sich bitte direkt an Criteo [hier](mailto:criteoTechnicalPartnerships@criteo.com).

Criteo ermöglicht vertrauenswürdige und wirkungsvolle Werbung, um jedem Verbraucher im offenen Internet reichhaltigere Erlebnisse zu bieten. Mit dem weltweit größten Commerce-Datensatz und einer erstklassigen KI stellt Criteo sicher, dass jeder Touchpoint über die Einkaufs-Journey personalisiert ist, um Kunden zur richtigen Zeit mit der richtigen Anzeige zu erreichen.

## Voraussetzungen {#prerequisites}

* Sie benötigen ein Administratorbenutzerkonto im [Kriterienverwaltungszentrum](https://marketing.criteo.com).
* Sie benötigen Ihre Criteo Advertiser ID (fragen Sie Ihren Criteo-Kontakt, wenn Sie diese ID nicht haben).
* Sie müssen [!DNL GUM caller ID] angeben, falls Sie [!DNL GUM ID] als Kennung verwenden möchten.

## Einschränkungen {#limitations}

* Criteo akzeptiert nur [!DNL SHA-256]-Hash- und Nur-Text-E-Mails (die vor dem Senden in [!DNL SHA-256] umgewandelt werden sollen). Bitte senden Sie keine personenbezogenen Daten (personenbezogene Daten, wie z.B. die Namen von Einzelpersonen oder Telefonnummern).
* Criteo benötigt mindestens eine Kennung, die vom Client bereitgestellt werden muss. [!DNL GUM ID] wird als Kennung priorisiert gegenüber Hash-E-Mail, da dies zu einer besseren Übereinstimmungsrate beiträgt.

![Voraussetzungen](../../assets/catalog/advertising/criteo/prerequisites.png)

## Unterstützte Identitäten {#supported-identities}

Criteo unterstützt die Aktivierung von Identitäten, die in der folgenden Tabelle beschrieben sind. Erhalten Sie weitere Informationen zu [Identitäten](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html#getting-started).

| Ziel-Identität | Beschreibung | Zu beachten |
| --- | --- | --- |
| `email_sha256` | Mit dem SHA-256-Algorithmus gehashte E-Mail-Adressen | Adobe Experience Platform unterstützt sowohl einfache als auch SHA-256-Hash-E-Mail-Adressen. Wenn Ihr Quellfeld ungehashte Attribute enthält, aktivieren Sie die Option [!UICONTROL Transformation anwenden] , damit Platform die Daten bei Aktivierung automatisch hasst. |
| `gum_id` | Cookie-Kennung von Criteo [!DNL GUM] | Mit [!DNL GUM IDs] können Kunden eine Korrespondenz zwischen ihrem Benutzeridentifizierungssystem und der Benutzerkennung von Criteo ([!DNL UID]) pflegen. Wenn der Kennungstyp `gum_id` ist, muss auch ein zusätzlicher Parameter, der [!DNL GUM Caller ID], einbezogen werden. Wenden Sie sich an Ihr Criteo-Account-Team, um den entsprechenden [!DNL GUM Caller ID] zu erhalten oder bei Bedarf weitere Informationen zu dieser [!DNL GUM ID]-Synchronisation zu erhalten. |

## Exporttyp und -häufigkeit {#export-type-frequency}

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| Element | Typ | Anmerkungen |
| --- | --- | --- |
| Exporttyp | Zielgruppenexport | Sie exportieren alle Mitglieder einer Zielgruppe mit den IDs (Name, Telefonnummer oder sonstiges), die im [!DNL Criteo]-Ziel verwendet werden. |
| Exporthäufigkeit | Streaming | Streaming-Ziele sind „immer verfügbare“ API-basierte Verbindungen. Sobald ein Profil in Experience Platform auf der Grundlage einer Zielgruppenauswertung aktualisiert wird, sendet der Connector das Update nachgelagert an die Zielplattform. Lesen Sie mehr über [Streaming-Ziele](../../destination-types.md#streaming-destinations). |

## Anwendungsfälle {#use-cases}

Um Ihnen ein besseres Verständnis der Verwendung des [!DNL Criteo]-Ziels zu vermitteln, finden Sie hier einige Ziele, die Adobe Experience Platform-Kunden mit [!DNL Criteo] erreichen können:

### Anwendungsfall 1: Traffic abrufen

Präsentieren Sie Ihr Unternehmen mit relevanten Produktangeboten und flexiblen Kreativen. Mit intelligenten Produktempfehlungen stellen Ihre Anzeigen automatisch die Produkte dar, die am ehesten Trigger zu Besuchen und Interaktionen sind. Flexibles Targeting ermöglicht Ihnen das Erstellen von Zielgruppen aus dem Commerce-Datensatz von Criteo oder aus Ihren eigenen Interessenslisten und Adobe-CDP-Segmenten.

### Anwendungsfall 2: Website-Konversionen erhöhen

Wenn Besucher Ihre Website verlassen, erinnern Sie sie daran, was ihnen bei Retargeting-Anzeigen fehlt, die Konversionen steigern, indem sie spezielle Angebote und hyperrelevante Angebote anzeigen, egal wohin sie als Nächstes gehen. Verbinden Sie Ihre Adobe-CDP-Zielgruppe, um Bestandskunden oder Kunden ähnlich Ihren treuesten Käufern erneut anzusprechen.

## Verbinden mit Criteo {#connect}

>[!IMPORTANT]
> 
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die Zugriffssteuerungsberechtigungen **[!UICONTROL Ziele anzeigen]** und **[!UICONTROL Ziele verwalten]** [. ](/help/access-control/home.md#permissions) Lesen Sie die [Übersicht über die Zugriffskontrolle](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im Abschnitt [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor.

### Bei Criteo authentifizieren

Die Schritte zum Verbinden lauten wie folgt:

1. Melden Sie sich bei Adobe Experience Platform an und verbinden Sie sich mit dem Criteo-Ziel.

   ![Anmelden](../../assets/catalog/advertising/criteo/connect-destination.png)

1. Sie werden zu Criteo umgeleitet, um die Verbindung zu autorisieren. Möglicherweise müssen Sie sich zunächst mit Ihren Criteo-Anmeldedaten anmelden:

   ![Bedingte Anmeldung](../../assets/catalog/advertising/criteo/log-in-1.png)

   ![Bedingte Anmeldung](../../assets/catalog/advertising/criteo/log-in-2.png)

   ![Bedingte Anmeldung](../../assets/catalog/advertising/criteo/log-in-3.png)


### Verbindungsparameter {#connection-parameters}

Geben Sie nach der Authentifizierung beim Ziel die folgenden Verbindungsparameter ein.

![Verbindungsparameter](../../assets/catalog/advertising/criteo/connection-parameters.png)

| Feld | Beschreibung | Erforderlich |
| --- | --- | --- |
| Name | Ein Name, der Ihnen dabei hilft, dieses Ziel in der Zukunft zu erkennen. Der Name, den Sie hier wählen, ist der Name &quot;[!DNL Audience]&quot;im Criteo Management Center und kann später nicht mehr geändert werden. | Ja |
| Beschreibung | Eine Beschreibung, mit der Sie dieses Ziel in der Zukunft identifizieren können. | Nein |
| Advertiser-ID | Criteo Advertiser ID Ihres Unternehmens. Wenden Sie sich an Ihren Criteo-Kundenbetreuer, um diese Informationen zu erhalten. | Ja |
| Criteo [!DNL GUM caller ID] | [!DNL GUM Caller ID] Ihres Unternehmens. Wenden Sie sich an Ihr Criteo-Account-Team, um den entsprechenden [!DNL GUM Caller ID] zu erhalten oder bei Bedarf weitere Informationen zu dieser [!DNL GUM]-Synchronisation zu erhalten. | Ja, wann immer [!DNL GUM ID] als Bezeichner bereitgestellt wird |

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie alle Details für Ihre Zielverbindung eingegeben haben, klicken Sie auf **[!UICONTROL Weiter]**.

## Aktivieren von Zielgruppen für dieses Ziel {#activate-segments}

>[!IMPORTANT]
> 
>* Um Daten zu aktivieren, benötigen Sie die Zugriffssteuerungsberechtigungen **[!UICONTROL Ziele anzeigen]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]** [. ](/help/access-control/home.md#permissions) Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.
>* Um *identities* zu exportieren, benötigen Sie die Zugriffssteuerungsberechtigung **[!UICONTROL Identitätsdiagramm anzeigen]** [ ](/help/access-control/home.md#permissions). <br> ![Wählen Sie den im Workflow hervorgehobenen Identitäts-Namespace aus, um Zielgruppen für Ziele zu aktivieren.](/help/destinations/assets/overview/export-identities-to-destination.png "Wählen Sie den im Workflow hervorgehobenen Identitäts-Namespace aus, um Zielgruppen für Ziele zu aktivieren."){width="100" zoomable="yes"}

Anweisungen zum Aktivieren von Zielgruppen für dieses Ziel finden Sie unter [Aktivieren von Profilen und Zielgruppen für Streaming-Zielgruppen-Exportziele](../../ui/activate-segment-streaming-destinations.md).

## Exportierte Daten {#exported-data}

Sie können die exportierten Zielgruppen im [Kriterienverwaltungszentrum](https://marketing.criteo.com/audience-manager/dashboard) sehen.

Der Anforderungstext zum Hinzufügen eines Benutzerprofils, das von der [!DNL Criteo] -Verbindung empfangen wird, sieht in etwa so aus:

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

Der Anforderungstext zum Entfernen des Benutzerprofils, das von der [!DNL Criteo]-Verbindung empfangen wurde, sieht in etwa so aus:

```json
{
  "data": {
    "type": "ContactlistWithUserAttributesAmendment",
    "attributes": {
      "operation": "remove",
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

Alle Adobe Experience Platform-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Detaillierte Informationen dazu, wie Adobe Experience Platform Data Governance durchsetzt, finden Sie in der [Übersicht zu Data Governance](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=de).

## Zusätzliche Ressourcen

* [Criteo Help Center](https://help.criteo.com/kb/en)
* [Criteo Developer Portal](https://developers.criteo.com)
