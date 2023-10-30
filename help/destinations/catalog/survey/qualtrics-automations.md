---
keywords: Streaming, Qualtrics-Ziel
title: Qualtrics Automation
description: Synchronisieren Sie Erlebnisse und operative Kundendaten, um die Personalisierung skaliert zu entsperren. Verwenden Sie die Aggregation mehrerer Quellen operativer Daten in Adobe Experience Platform als Input für Qualtrics Experience iD, um Ihre Kunden besser zu verstehen und zielgerichtete Kontakte zu ermöglichen, um die Lücke im Hinblick auf das Verständnis von Intent-, Emotions- und Erlebnistreibern zu schließen.
last-substantial-update: 2023-10-25T00:00:00Z
exl-id: 3289ed4c-8542-4e22-a574-e49cc6527a24
source-git-commit: 308d07cf0c3b4096ca934a9008a13bf425dc30b6
workflow-type: tm+mt
source-wordcount: '1149'
ht-degree: 32%

---

# Qualtrics Automation

## Übersicht {#overview}

Synchronisieren Sie Erlebnisse und operative Kundendaten, um die Personalisierung skaliert zu entsperren.

Verwenden Sie die Aggregation mehrerer Quellen operativer Daten in Adobe Experience Platform als Input für Qualtrics Experience iD, um Ihre Kunden besser zu verstehen und zielgerichtete Kontakte zu ermöglichen, um die Lücke im Hinblick auf das Verständnis von Intent-, Emotions- und Erlebnistreibern zu schließen.

>[!IMPORTANT]
>
>Der Ziel-Connector und die Dokumentationsseite werden vom Qualtrics-Team erstellt und gepflegt. Bei Fragen oder Aktualisierungsanfragen kontaktieren Sie diese bitte direkt, indem Sie sich bei der [Customer Success Hub](https://support-portal.qualtrics.com/).

## Anwendungsfälle {#use-cases}

Um Ihnen zu helfen, besser zu verstehen, wie und wann Sie die *Qualtrics Automation* Ziel, hier finden Sie Beispielanwendungsfälle, die Adobe Experience Platform-Kunden mit diesem Ziel lösen können.

### Anwendungsfall 1 {#use-case-1}

**Szenario**: Ein Unternehmen möchte die Kundenzufriedenheit über verschiedene digitale Touchpoints hinweg messen, z. B. über seine Website und mobile App. Sie verwenden Adobe Experience Platform zum Trigger von Qualtrics-Umfragen auf der Grundlage von Benutzerinteraktionen, z. B. zum Abschluss eines Kaufs oder zum Besuch einer bestimmten Webseite.

**Ergebnis**: Durch die Erfassung von Echtzeit-Feedback kann das Unternehmen datenbasierte Verbesserungen an seinem Kundenerlebnis vornehmen und so die Zufriedenheit und Loyalität steigern.

### Anwendungsfall 2 {#use-case-2}

**Szenario**: Eine Organisation zielt darauf ab, den Onboarding-Prozess für ihre Mitarbeiter zu verbessern. Sie nutzen Adobe Experience Platform, um durch Qualtrics-Umfragen Feedback von neuen Mitarbeitern zu sammeln. Umfragen werden nach einer vordefinierten Einstiegsphase automatisch ausgelöst.

**Ergebnis**: Kontinuierliches Feedback ermöglicht es der Organisation, den Onboarding-Prozess anzupassen und zu verbessern, was zu einer besseren Interaktion und Produktivität neuer Mitarbeiter führt.

## Voraussetzungen

Bevor Sie das Qualtrics-Ziel in Adobe Experience Platform einrichten, stellen Sie sicher, dass die folgenden Voraussetzungen erfüllt sind:

* Sie haben ein Qualtrics-Konto.
* Sie haben das erforderliche API-Token von Qualtrics erhalten.

### Abrufen eines API-Tokens

Im Folgenden finden Sie die erforderlichen Schritte zum Abrufen eines API-Tokens von Qualtrics.

1. Melden Sie sich bei Ihrem Qualtrics-Konto an.
2. Navigieren Sie zu **Kontoeinstellungen**.
3. Auswählen **Qualtrics-IDs**.
4. Suchen Sie auf dieser Seite nach der **API** -Abschnitt enthält, enthält es eine **Token** -Feld. Dies ist das API-Token und wird während der Zieleinrichtung erforderlich sein.

## Unterstützte Identitäten {#supported-identities}

*Qualtrics Automation* unterstützt die Aktivierung der in der folgenden Tabelle beschriebenen Identitäten. Erhalten Sie weitere Informationen zu [Identitäten](/help/identity-service/namespaces.md).

| Ziel-Identität | Beschreibung | Zu beachten |
|---|---|---|
| E-Mail | E-Mail-Adressen in Textform | Qualtrics unterstützt nur E-Mail-Adressen mit normalem Text. |
| external_id | Benutzerdefinierte Benutzer-IDs | Wählen Sie diese Zielidentität aus, wenn Ihre Quellidentität ein benutzerdefinierter Namespace ist. |

{style="table-layout:auto"}

## Exporttyp und -häufigkeit {#export-type-frequency}

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| Element | Typ | Anmerkungen |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Segmentexport]** | Sie exportieren alle Mitglieder eines Segments (Zielgruppe) mit den IDs (Name, Telefonnummer oder andere), die im *Qualtrics Automation* Ziel. |
| Exporthäufigkeit | **[!UICONTROL Streaming]** | Streaming-Ziele sind „immer verfügbare“ API-basierte Verbindungen. Sobald ein Profil in Experience Platform auf der Grundlage einer Segmentauswertung aktualisiert wird, sendet der Connector das Update nachgelagert an die Zielplattform. Lesen Sie mehr über [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Herstellen einer Verbindung mit dem Ziel {#connect}

>[!IMPORTANT]
> 
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die [Zugriffsberechtigung](/help/access-control/home.md#permissions) **[!UICONTROL Ziele verwalten]**. Lesen Sie die [Zugriffskontrolle – Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor. Füllen Sie im Workflow zum Konfigurieren des Ziels die Felder aus, die in den beiden folgenden Abschnitten aufgeführt sind.

### Beim Ziel authentifizieren {#authenticate}

Als Teil der Authentifizierung müssen Sie eine **Benutzername** und **Passwort**. Der Benutzername ist Ihr Qualtrics-Benutzername und das Kennwort ist das API-Token Ihres Qualtrics-Kontos. Befolgen Sie die Anweisungen aus dem Abschnitt **Voraussetzungen** Abschnitt weiter oben.

![Authentifizierung](/help/destinations/assets/catalog/survey/qualtrics/authentication.png)

### Ausfüllen der Zieldetails {#destination-details}

Füllen Sie die folgenden erforderlichen und optionalen Felder aus, um Details für das Ziel zu konfigurieren. Ein Sternchen neben einem Feld in der Benutzeroberfläche zeigt an, dass das Feld erforderlich ist.

* **[!UICONTROL Name]**: Ein Name, durch den Sie dieses Ziel in Zukunft erkennen können.
* **[!UICONTROL Beschreibung]**: Eine Beschreibung, die Ihnen hilft, dieses Ziel in Zukunft zu identifizieren.
* **[!UICONTROL URL]**: Die URL, die im [JSON-Ereignis](https://www.qualtrics.com/support/survey-platform/actions-module/json-events/#About) dass Ihre [Workflow in Qualtrics](https://www.qualtrics.com/support/survey-platform/actions-module/setting-up-actions/#About). Ein Beispiel finden Sie im folgenden Screenshot.

![URL](/help/destinations/assets/catalog/survey/qualtrics/json-event-url.png)

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie alle Details für Ihre Zielverbindung eingegeben haben, klicken Sie auf **[!UICONTROL Weiter]**.

## Aktivieren von Zielgruppen für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>Um Daten zu aktivieren, benötigen Sie die [Zugriffskontrollberechtigungen](/help/access-control/home.md#permissions) **[!UICONTROL Ziele verwalten]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]**. Lesen Sie die [Zugriffssteuerung – Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Anweisungen zum Aktivieren von Zielgruppensegmenten für dieses Ziel finden Sie unter [Aktivieren von Profilen und Segmenten für Streaming-Segmentexportziele](/help/destinations/ui/activate-segment-streaming-destinations.md).

### Zuordnen von Attributen und Identitäten {#map}

Dieses Ziel verfügt über ein geöffnetes Schema, sodass Sie alle Eigenschaften an Qualtrics senden können.

#### Zuordnungsattribute

Um Ihrer Zuordnung ein Attribut hinzuzufügen, wählen Sie einfach **benutzerdefinierte Attribute** beim Hinzufügen einer neuen Zuordnung. Sie können einen beliebigen Namen für Ihr Attribut eingeben. Qualtrics fördert die *camelCase* Namenskonvention für Attributnamen (ein Beispiel finden Sie im folgenden Screenshot).

![Benutzerdefiniertes Attribut](/help/destinations/assets/catalog/survey/qualtrics/custom-attribute.png)

Im folgenden Screenshot finden Sie ein Beispiel für mögliche Attribut-Mappings.

![Beispielzuordnungen](/help/destinations/assets/catalog/survey/qualtrics/example-mappings.png)

#### Zuordnen von Identitäten

Es ist erforderlich, einen Identitäts-Namespace für dieses Ziel auszuwählen. Die beiden möglichen Quellfelder für Zielfeld-Zuordnungen sind:

| Quellfeld | Zielfeld |
|--------------------|-----------------------|
| IdentityMap: Email | Identität: email |
| IdentityMap: ECID | Identität: external_id |

Ein Beispiel finden Sie im folgenden Screenshot.

![Identity-Namespace](/help/destinations/assets/catalog/survey/qualtrics/identity-namespace.png)

## Exportierte Daten/Datenexport validieren {#exported-data}

Wie bereits erwähnt, verwendet dieses Ziel ein offenes Schema, sodass alle Eigenschaften an Qualtrics gesendet werden können. Die an Qualtrics gesendeten Daten folgen jedoch der folgenden Struktur:

```json
{
  "person": {
    "name": {
      "firstName": "Dave"
    }
  },
  "mobilePhone": {
    "number": "0123456789"
  },
  "identityMap": {
    "Email": [
      {
        "id": "Email-2Sf6C"
      }
    ]
  },
  "segmentMembership": {
    "ups": {
      "046456e3b-18e1-48a6-9bda-d68547861283": {
        "lastQualificationTime": "2023-09-05T10:43:55.602687Z",
        "status": "realized"
      },
      "007844dd1-9e5d-4531-a4ee-05470doe759dd": {
        "lastQualificationTime": "2023-09-05T10:43:55.602689Z",
        "status": "realized"
      }
    }
  }
}
```

Um sicherzustellen, dass Daten in Qualtrics erfasst wurden, gehen Sie zum Workflow, der Ihre **JSON-Ereignis** von dort aus zu **Verlauf ausführen** wo die Ausführungen Ihres Workflows angezeigt werden sollen. Jeder Workflow hat den Status **Erfolgreich** oder **Fehlgeschlagen**. Wenn Sie eine bestimmte Ausführung auswählen, werden Ihnen weitere Informationen angezeigt, damit Sie bei Problemen eine Fehlerbehebung durchführen können.

Wenn keine Ausführungen in **Verlauf ausführen** bedeutet dies, dass der Workflow noch nicht ausgelöst wurde, was darauf hinweist, dass möglicherweise ein Problem vorliegt. Stellen Sie sicher, dass der Workflow aktiviert ist und dass die **URL** im Ziel in Adobe Experience Platform korrekt ist. Workflow-Ausführungen sind nicht unmittelbar, daher müssen Sie möglicherweise kurz warten, bis sie abgeschlossen sind.

## Datennutzung und -Governance {#data-usage-governance}

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Ausführliche Informationen darüber, wie [!DNL Adobe Experience Platform] Data Governance erzwingt, finden Sie unter [Data Governance - Übersicht](/help/data-governance/home.md).
