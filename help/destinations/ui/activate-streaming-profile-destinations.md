---
keywords: Profil-Ziele aktivieren; Ziele aktivieren; Daten aktivieren; E-Mail-Marketingziele aktivieren; Cloud-Datenspeicherung-Ziele aktivieren
title: Audience-Daten in Streaming-Profil-Exportziele aktivieren
type: Tutorial
seo-title: Activate audience data to streaming profile export destinations
description: Erfahren Sie, wie Sie die Audience in Adobe Experience Platform aktivieren, indem Sie Segmente an Streaming-Profil-basierte Ziele senden.
seo-description: Learn how to activate the audience data you have in Adobe Experience Platform by sending segments to streaming profile-based destinations.
exl-id: bc0f781e-60de-44a5-93cb-06b4a3148591
source-git-commit: 2b1cde9fc913be4d3bea71e7d56e0e5fe265a6be
workflow-type: tm+mt
source-wordcount: '524'
ht-degree: 7%

---

# Audience-Daten in Streaming-Profil-Exportziele aktivieren

## Übersicht {#overview}

In diesem Artikel wird der Arbeitsablauf erläutert, der zur Aktivierung von Audience-Daten in Adobe Experience Platform-Streaming-Profilen wie Amazon Kinesis erforderlich ist.

## Voraussetzungen {#prerequisites}

Um Daten in Ziele zu aktivieren, müssen Sie erfolgreich [mit einem Ziel verbunden](./connect-destination.md). Wenn Sie das noch nicht getan haben, gehen Sie zu [Zielkatalog](../catalog/overview.md), durchsuchen Sie die unterstützten Ziele und konfigurieren Sie das Ziel, das Sie verwenden möchten.

## Ziel auswählen {#select-destination}

1. Gehe zu **[!UICONTROL Verbindungen > Ziele]**, und wählen Sie **[!UICONTROL Katalog]** Tabulator.

   ![Registerkarte &quot;Zielkatalog&quot;](../assets/ui/activate-streaming-profile-destinations/catalog-tab.png)

1. Auswählen **[!UICONTROL Segmente aktivieren]** auf der Karte, die dem Ziel entspricht, an dem Sie Ihre Segmente aktivieren möchten, wie in der Abbildung unten dargestellt.

   ![Schaltfläche &quot;Segmente aktivieren&quot;](../assets/ui/activate-streaming-profile-destinations/activate-segments-button.png)

1. Wählen Sie die Zielverbindung aus, die Sie zum Aktivieren der Segmente verwenden möchten, und wählen Sie dann **[!UICONTROL Weiter]**.

   ![Ziel auswählen](../assets/ui/activate-streaming-profile-destinations/select-destination.png)

1. Zum nächsten Abschnitt verschieben nach [Ihre Segmente auswählen](#select-segments).

## Segmente auswählen {#select-segments}

Verwenden Sie die Kontrollkästchen links neben den Segmentnamen, um die Segmente auszuwählen, die Sie am Ziel aktivieren möchten, und wählen Sie dann **[!UICONTROL Weiter]**.

![Segmente auswählen](../assets/ui/activate-streaming-profile-destinations/select-segments.png)

## Profil-Attribute auswählen {#select-attributes}

Wählen Sie die Profil-Attribute aus, die an das Ziel der Zielgruppe gesendet werden sollen.

>[!NOTE]
>
> Adobe Experience Platform erfüllt Ihre Auswahl mit vier empfohlenen, häufig verwendeten Attributen aus Ihrem Schema: `person.name.firstName`, `person.name.lastName`, `personalEmail.address`, `segmentMembership.status`.

Der Dateiexport variiert auf folgende Weise, je nachdem, ob `segmentMembership.status` ist ausgewählt:
* Wenn `segmentMembership.status` Feld ausgewählt, exportierte Dateien enthalten **[!UICONTROL Aktiv]** Mitglieder im ursprünglichen vollständigen Schnappschuss und **[!UICONTROL Aktiv]** und **[!UICONTROL Abgelaufen]** Mitglieder in späteren inkrementellen Exporten.
* Wenn `segmentMembership.status` Feld nicht ausgewählt, exportierte Dateien enthalten nur **[!UICONTROL Aktiv]** -Member im ursprünglichen vollständigen Schnappschuss und in nachfolgenden inkrementellen Exporten.

![empfohlene Attribute](../assets/ui/activate-streaming-profile-destinations/attributes-default.png)

1. In **[!UICONTROL Attribute auswählen]** Seite, auswählen **[!UICONTROL Neues Feld Hinzufügen]**.

   ![Neue Zuordnung Hinzufügen](../assets/ui/activate-streaming-profile-destinations/add-new-field.png)

1. Wählen Sie den Pfeil rechts neben dem **[!UICONTROL Schema]** Eintrag.

   ![Quellfeld auswählen](../assets/ui/activate-streaming-profile-destinations/select-schema-field.png)

1. In **[!UICONTROL Feld auswählen]** Seite, wählen Sie die XDM-Attribute aus, die an das Ziel gesendet werden sollen, und wählen Sie dann **[!UICONTROL Auswählen]**.

   ![Quellfeldseite auswählen](../assets/ui/activate-streaming-profile-destinations/target-field-page.png)


1. Um weitere Zuordnungen hinzuzufügen, wiederholen Sie die Schritte 1 bis 3 und wählen Sie dann **[!UICONTROL Weiter]**.

## Überprüfung {#review}

Auf der Seite **[!UICONTROL Überprüfen]** können Sie eine Zusammenfassung Ihrer Auswahl sehen. Wählen Sie **[!UICONTROL Abbrechen]**, um den Fluss abzubrechen, **[!UICONTROL Zurück]**, um die Einstellungen zu ändern, oder **[!UICONTROL Fertig stellen]**, um Ihre Auswahl zu bestätigen und mit dem Senden von Daten an das Ziel zu beginnen.

>[!IMPORTANT]
>
>In diesem Schritt prüft Adobe Experience Platform auf Verstöße gegen die Datenschutzrichtlinien. Im Folgenden finden Sie ein Beispiel für Verstöße gegen eine Richtlinie. Sie können den Segmentarbeitsablauf erst abschließen, wenn Sie die Verletzung behoben haben. Informationen zur Behebung von Verstößen gegen die Politik finden Sie unter [Durchsetzung der Rechtsvorschriften](../../rtcdp/privacy/data-governance-overview.md#enforcement) in der Dokumentation zur Datenverwaltung.

![Datenrichtlinienverletzung](../assets/common/data-policy-violation.png)

Wenn keine Richtlinienverletzungen festgestellt wurden, wählen Sie **[!UICONTROL Fertigstellen]** um Ihre Auswahl zu bestätigen und den Beginn zu informieren, der Daten an das Ziel sendet.

![Überprüfung](../assets/ui/activate-streaming-profile-destinations/review.png)

## Aktivierung des Segments überprüfen {#verify}

Ihr exportiert [!DNL Experience Platform] Daten landen im JSON-Format am Ziel Ihrer Zielgruppe. Das folgende Ereignis enthält beispielsweise das E-Mail-Adressattribut einer Audience, die sich für ein bestimmtes Profil qualifiziert und ein anderes Segment verlassen hat. Die Identitäten für diesen Potenzieller Kunde sind ECID und E-Mail.

```json
{
  "person": {
    "email": "yourstruly@adobe.com"
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
