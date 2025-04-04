---
title: Aktivieren von Zielgruppen für Exportziele von Streaming-Profilen
type: Tutorial
description: Erfahren Sie, wie Sie Ihre Zielgruppendaten in Adobe Experience Platform aktivieren, indem Sie Zielgruppen an Ziele senden, die auf Streaming-Profilen basieren.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: bc0f781e-60de-44a5-93cb-06b4a3148591
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '765'
ht-degree: 23%

---


# Aktivieren von Zielgruppen für Exportziele von Streaming-Profilen

>[!IMPORTANT]
> 
> * Um Daten zu aktivieren und den [Zuordnungsschritt](#mapping) des Workflows zu aktivieren, benötigen Sie die Berechtigungen **[!UICONTROL Ziele anzeigen]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **** Segmente anzeigen[Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions).
> * Um Daten zu aktivieren, ohne den [Zuordnungsschritt](#mapping) des Workflows zu durchlaufen, benötigen Sie die Berechtigungen **[!UICONTROL Ziele anzeigen]**, **[!UICONTROL Segment ohne Zuordnung aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions).
> 
> Lesen Sie die [Übersicht über die Zugriffskontrolle](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

## Übersicht {#overview}

In diesem Artikel wird der Workflow erläutert, der zum Aktivieren von Zielgruppendaten in Adobe Experience Platform für Streaming-profilbasierte Ziele (auch als [-Ziele bezeichnet](/help/destinations/destination-types.md#advanced-enterprise-destinations) erforderlich ist.

Dieser Artikel gilt für die folgenden drei Ziele:

* [Amazon Kinesis](/help/destinations/catalog/cloud-storage/amazon-kinesis.md)
* [Azure Event Hubs](/help/destinations/catalog/cloud-storage/azure-event-hubs.md)
* [HTTP-API-](/help/destinations/catalog/streaming/http-destination.md).

## Voraussetzungen {#prerequisites}

Um Daten für Ziele aktivieren zu können, müssen Sie eine erfolgreiche [Verbindung zu einem Ziel](./connect-destination.md) hergestellt haben. Wenn Sie das noch nicht getan haben, navigieren Sie zum [Zielkatalog](../catalog/overview.md), durchsuchen Sie die unterstützten Ziele und konfigurieren Sie das Ziel, das Sie verwenden möchten.

## Auswählen des Ziels {#select-destination}

1. Navigieren Sie zu **[!UICONTROL Verbindungen und Ziele]** und wählen Sie die Registerkarte **[!UICONTROL Katalog]**.

   ![Bild, das die Registerkarte „Zielkatalog“ zeigt.](../assets/ui/activate-streaming-profile-destinations/catalog-tab.png)

1. Wählen Sie **[!UICONTROL Zielgruppen aktivieren]** auf der Karte, die dem Zielort entspricht, an dem Sie Ihre Zielgruppen aktivieren möchten, wie in der Abbildung unten dargestellt.

   ![Abbildung mit hervorgehobenem Steuerelement „Zielgruppen aktivieren“ auf der Registerkarte „Zielkatalog“.](../assets/ui/activate-streaming-profile-destinations/activate-audiences-button.png)

1. Wählen Sie die Zielverbindung aus, die Sie zum Aktivieren Ihrer Zielgruppen verwenden möchten, und klicken Sie dann auf **[!UICONTROL Weiter]**.

   ![Bild mit einer Auswahl von zwei Zielen, mit denen Sie eine Verbindung herstellen können.](../assets/ui/activate-streaming-profile-destinations/select-destination.png)

1. Gehen Sie zum nächsten Abschnitt, um [Ihre Zielgruppen auswählen](#select-audiences).

## Audiences auswählen {#select-audiences}

Um die Zielgruppen auszuwählen, die Sie für das Ziel aktivieren möchten, aktivieren Sie die Kontrollkästchen links neben den Zielgruppennamen und klicken Sie dann auf **[!UICONTROL Weiter]**.

Je nach Herkunft können Sie aus verschiedenen Arten von Zielgruppen auswählen:

* **[!UICONTROL Segmentierungs-Service]**: Zielgruppen, die in Experience Platform vom Segmentierungs-Service generiert werden. Weitere Informationen finden [ in der ](../../segmentation/ui/audience-portal.md) zum Audience Portal .
* **[!UICONTROL Benutzerdefinierter Upload]**: Zielgruppen, die außerhalb von Experience Platform generiert und als CSV-Dateien in Experience Platform hochgeladen werden. Weitere Informationen zu externen Zielgruppen finden Sie in der Dokumentation unter [Importieren einer Zielgruppe](../../segmentation/ui/audience-portal.md#import-audience).
* Andere Arten von Zielgruppen, die aus anderen Adobe-Lösungen wie [!DNL Audience Manager] stammen.

![Abbildung mit hervorgehobenen Kontrollkästchen im Schritt „Zielgruppen auswählen“ des Aktivierungs-Workflows.](../assets/ui/activate-streaming-profile-destinations/select-audiences.png)

## Auswählen der Profilattribute {#select-attributes}

Wählen **[!UICONTROL im Schritt]** die Profilattribute aus, die Sie an das Ziel senden möchten.

1. Wählen Sie auf der Seite **[!UICONTROL Attribute auswählen]** die Option **[!UICONTROL Neues Feld hinzufügen]**.

   ![Abbildung mit hervorgehobener Option „Neues Feld hinzufügen“ im Zuordnungsschritt.](../assets/ui/activate-streaming-profile-destinations/add-new-field.png)

1. Wählen Sie den Pfeil rechts neben dem Eintrag **[!UICONTROL Schemafeld]**.

   ![Abbildung mit hervorgehobenen Informationen zur Auswahl eines Quellfelds im Zuordnungsschritt.](../assets/ui/activate-streaming-profile-destinations/select-schema-field.png)

1. Wählen Sie auf der Seite **[!UICONTROL Feld auswählen]** die XDM-Attribute aus, die Sie an das Ziel senden möchten, und klicken Sie dann auf **[!UICONTROL Auswählen]**.

   ![Bild mit einer Auswahl von XDM-Feldern, die Sie als Quellfelder auswählen können.](../assets/ui/activate-streaming-profile-destinations/target-field-page.png)

1. Um weitere Felder hinzuzufügen, wiederholen Sie die Schritte 1 bis 3 und klicken Sie dann auf **[!UICONTROL Weiter]**.

## Überprüfung {#review}

Auf der Seite **[!UICONTROL Überprüfen]** können Sie eine Zusammenfassung Ihrer Auswahl sehen. Wählen Sie **[!UICONTROL Abbrechen]**, um den Fluss abzubrechen, **[!UICONTROL Zurück]**, um die Einstellungen zu ändern, oder **[!UICONTROL Fertig stellen]**, um Ihre Auswahl zu bestätigen und mit dem Senden von Daten an das Ziel zu beginnen.

![Zusammenfassung der Auswahl im Überprüfungsschritt.](../assets/ui/activate-streaming-profile-destinations/review.png)

### Auswertung der Einverständnisrichtlinie {#consent-policy-evaluation}

[Bewertung der Einverständnisrichtlinie](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) wird derzeit nicht für Exporte an die drei Unternehmensziele unterstützt - Amazon Kinesis, Azure Event Hubs und HTTP-API.

Das bedeutet, dass Profile, die der Zielgruppenbestimmung nicht zugestimmt haben *in* Exporte an diese drei Ziele einbezogen werden.

<!--

If your organization purchased **Adobe Healthcare Shield** or **Adobe Privacy & Security Shield**, select **[!UICONTROL View applicable consent policies]** to see which consent policies are applied and how many profiles are included in the activation as a result of them. Read about [consent policy evaluation](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) for more information.

-->

### Prüfung der Datennutzungsrichtlinien {#data-usage-policy-checks}

Im Schritt **[!UICONTROL Überprüfen]** prüft Experience Platform auch, ob Verstöße gegen Datennutzungsrichtlinien vorliegen. Nachstehend ist ein Beispiel angegeben, bei dem eine Richtlinie verletzt wird. Sie können den Zielgruppenaktivierungs-Workflow erst abschließen, nachdem Sie den Verstoß behoben haben. Informationen zum Beheben von Richtlinienverletzungen finden Sie unter [Verstöße gegen Datennutzungsrichtlinien](/help/data-governance/enforcement/auto-enforcement.md#data-usage-violation) im Dokumentationsabschnitt zur Data Governance.

![Verletzung von Datenrichtlinien](../assets/common/data-policy-violation.png)

### Audiences filtern {#filter-audiences}

In diesem Schritt können Sie auch die auf der Seite verfügbaren Filter verwenden, um nur die Zielgruppen anzuzeigen, deren Zeitplan oder Zuordnung im Rahmen dieses Workflows aktualisiert wurde.

![Bildschirmaufzeichnung mit den verfügbaren Zielgruppenfiltern im Überprüfungsschritt.](../assets/ui/activate-streaming-profile-destinations/filter-audiences-review-step.gif)

Wenn Sie mit Ihrer Auswahl zufrieden sind und keine Richtlinienverletzungen festgestellt wurden, wählen Sie **[!UICONTROL Beenden]**, um Ihre Auswahl zu bestätigen und mit dem Senden von Daten an das Ziel zu beginnen.

## Zielgruppenaktivierung überprüfen {#verify}

Ihre exportierten [!DNL Experience Platform] landen in Ihrem Ziel im JSON-Format. Beispiel: Das nachstehende Ereignis enthält das E-Mail-Adressenattribut eines Profils, das sich für eine bestimmte Zielgruppe qualifiziert und eine andere Zielgruppe verlassen hat. Die Identitäten für diesen potenziellen Kunden sind `ECID` und `email_lc_sha256`.

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
        "status": "realized"
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
