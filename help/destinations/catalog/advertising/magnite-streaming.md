---
title: Magnite-Streaming-Echtzeit-Zielverbindung
description: Verwenden Sie dieses Ziel, um Adobe CDP-Zielgruppen in Echtzeit an die Magnite-Streaming-Plattform zu übermitteln.
badgeBeta: label="Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: c61907768f6d3cfdae3d07291bb25ff4a5229a89
workflow-type: tm+mt
source-wordcount: '1306'
ht-degree: 32%

---


# (Beta) Magnite Streaming: Echtzeit-Zielverbindung

## Übersicht {#overview}

Die [!DNL Magnite Streaming: Real-Time] und das Magnite-Streaming: Batch-Ziele in Adobe Experience Platform helfen Ihnen beim Zuordnen und Exportieren von Zielgruppen für Targeting und Aktivierung auf der Magnite-Streaming-Plattform.

Aktivieren von Zielgruppen für [!DNL Magnite Streaming] Plattform ist ein zweistufiger Prozess, bei dem Sie sowohl das Magnite-Streaming verwenden müssen: Echtzeit- als auch das Magnite-Streaming: Batch-Ziele.

So aktivieren Sie Ihre Zielgruppen in [!DNL Magnite Streaming]müssen Sie:

* Aktivieren Sie die Zielgruppen für die [!DNL Magnite Streaming: Real-Time] Ziel, wie auf dieser Seite gezeigt.
* Aktivieren Sie dieselbe Zielgruppe im Magnite-Streaming: Batch-Ziel. Die [!DNL Magnite Streaming: Batch] Ziel ist eine obligatorische Komponente. Aktivierung der Zielgruppe auf der [!DNL Magnite Streaming] Das Batch-Ziel führt zu einer fehlgeschlagenen Integration und Ihre Zielgruppen werden nicht aktiviert.

Hinweis: Bei Verwendung des Echtzeit-Ziels gilt Folgendes: [!DNL Magnite: Streaming] Zielgruppen werden in Echtzeit empfangen, aber wir können Echtzeit-Zielgruppen nur vorübergehend in unserer Plattform speichern und sie werden innerhalb weniger Tage aus unserem System entfernt. Wenn Sie daher das Ziel Magnite: Streaming in Echtzeit verwenden möchten, werden Sie *auch* Sie müssen das Magnite-Streaming: Batch-Ziel verwenden - jede Zielgruppe, die Sie für das Echtzeit-Ziel aktivieren, müssen Sie auch für das Batch-Ziel aktivieren.

>[!IMPORTANT]
>
>Dieser Ziel-Connector befindet sich in der Beta-Phase und steht nur ausgewählten Kunden zur Verfügung. Wenden Sie sich an Ihren Adobe-Support-Mitarbeiter, um Zugriff anzufordern.
>
>Der Ziel-Connector und die Dokumentationsseite werden vom [!DNL Magnite] Team. Bei Fragen oder Aktualisierungsanfragen wenden Sie sich bitte direkt an `adobe-tech@magnite.com`.

## Anwendungsfälle {#use-cases}

Damit Sie besser verstehen können, wie und wann Sie das [!DNL Magnite Streaming: Real-Time]-Ziel verwenden sollten, finden Sie hier ein Anwendungsbeispiel, das für Kundinnen und Kunden von Adobe Experience Platform mit diesem Ziel geeignet ist.

### Aktivierung und Zielgruppenbestimmung {#activation-and-targeting}

Durch diese Integration mit Magnite können Kunden ihre CDP-Zielgruppen von Adobe Experience Platform an Magnite für das Anzeigen-Targeting übergeben. Zielgruppen können in Magnite sowohl für positives Targeting als auch für negatives Targeting (Unterdrückung) ausgewählt werden.

## Voraussetzungen {#prerequisites}

So verwenden Sie die [!DNL Magnite] Ziele in Adobe Experience Platform müssen Sie zunächst über eine [!DNL Magnite Streaming] -Konto. Wenn Sie [!DNL Magnite Streaming] -Konto, wenden Sie sich bitte an Ihre [!DNL Magnite] Kundenbetreuer, um Anmeldeinformationen für den Zugriff bereitzustellen [!DNL Magnite's] Ziele.
Wenn Sie keine [!DNL Magnite Streaming] -Konto, wenden Sie sich bitte an adobe-tech@magnite.com

## Unterstützte Identitäten {#supported-identities}

Die [!DNL Magnite Streaming: Real-Time] Das Ziel unterstützt die Aktivierung von Identitäten, die in der folgenden Tabelle beschrieben sind. Erhalten Sie weitere Informationen zu [Identitäten](/help/identity-service/features/namespaces.md).

| Ziel-Identität | Beschreibung | Zu beachten |
|-------------------|--------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------|
| device_id | Eine eindeutige Kennung für ein Gerät oder eine Identität. Wir akzeptieren jede Geräte-ID und Erstanbieter-ID unabhängig vom Typ. | Zu den von uns unterstützten Identitätstypen gehören u. a. PPUID, GAID, IDFA und TV-Geräte-IDs. |

{style="table-layout:auto"}

## Unterstützte Zielgruppen {#supported-audiences}

In diesem Abschnitt wird beschrieben, welche Zielgruppentypen Sie an dieses Ziel exportieren können.

| Audience Origin | Unterstützt | Beschreibung |
|-----------------------------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Über die Experience Platform generierte Zielgruppen [Segmentierungsdienst](../../../segmentation/home.md). |
| Benutzerdefinierte Uploads | ✓ | Zielgruppen, die aus CSV-Dateien in Experience Platform [importiert](../../../segmentation/ui/overview.md#import-audience) werden. |

{style="table-layout:auto"}

## Exporttyp und -häufigkeit {#export-type-frequency}

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| Element | Typ | Anmerkungen |
|------------------|---------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Exporttyp | **[!UICONTROL Segmentexport]** | Sie exportieren alle Mitglieder eines Segments (Zielgruppe) mit den IDs (Name, Telefonnummer oder sonstiges), die im [!DNL Magnite Streaming: Real-Time]-Ziel verwendet werden. |
| Exporthäufigkeit | **[!UICONTROL Streaming]** | Streaming-Ziele sind „immer verfügbare“ API-basierte Verbindungen. Sobald ein Profil in Experience Platform auf der Grundlage einer Segmentauswertung aktualisiert wird, sendet der Connector das Update nachgelagert an die Zielplattform. Lesen Sie mehr über [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Herstellen einer Verbindung mit dem Ziel {#connect}

>[!IMPORTANT]
>
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die **[!UICONTROL Ziele anzeigen]** und **[!UICONTROL Ziele verwalten]** [Zugriffsberechtigung](/help/access-control/home.md#permissions). Lesen Sie die [Zugriffskontrolle – Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor. Füllen Sie im Workflow zum Konfigurieren des Ziels die Felder aus, die in den beiden folgenden Abschnitten aufgeführt sind.

### Beim Ziel authentifizieren {#authenticate}

Um sich beim Ziel zu authentifizieren, füllen Sie die erforderlichen Felder aus und wählen Sie **[!UICONTROL Mit Ziel verbinden]** aus.

![Zielkonfigurationsautorfelder nicht ausgefüllt](../../assets/catalog/advertising/magnite/destination-realtime-config-auth-unfilled.png)

* **[!UICONTROL Benutzername]**: Der Benutzername, den Sie von [!DNL Magnite].
* **[!UICONTROL Passwort]**: Das von [!DNL Magnite].

### Ausfüllen der Zieldetails {#destination-details}

Füllen Sie die folgenden erforderlichen und optionalen Felder aus, um Details für das Ziel zu konfigurieren. Ein Sternchen neben einem Feld in der Benutzeroberfläche zeigt an, dass das Feld erforderlich ist.

* **[!UICONTROL Name]**: Ein Name, durch den Sie dieses Ziel in Zukunft erkennen können.
* **[!UICONTROL Beschreibung]**: Eine Beschreibung, die Ihnen hilft, dieses Ziel in Zukunft zu identifizieren.
* **[!UICONTROL Name Ihres Quell-Partners]**: Name Ihres Kunden/Unternehmens. Nur unterstützt [!DNL Magnite Streaming] -Clients stehen zur Auswahl zur Verfügung.

![Felder für Zielkonfiguration ausgefüllt](../../assets/catalog/advertising/magnite/destination-realtime-config-auth-filled.png)

Wählen Sie anschließend die **[!UICONTROL Erstellen]** Schaltfläche.

![Optionale Governance-Politik und Durchsetzungsmaßnahmen](../../assets/catalog/advertising/magnite/destination-realtime-config-grouping-policy.png)

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie mit dem Eingeben der Details für Ihre Zielverbindung fertig sind, klicken Sie auf **[!UICONTROL Weiter]**.

## Aktivieren von Segmenten für dieses Ziel {#activate}

>[!IMPORTANT]
>
>* Um Daten zu aktivieren, benötigen Sie die **[!UICONTROL Ziele anzeigen]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Anzeigen von Profilen]**, und **[!UICONTROL Segmente anzeigen]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.
>* Export *identities*, benötigen Sie die **[!UICONTROL Identitätsdiagramm anzeigen]** [Zugriffsberechtigung](/help/access-control/home.md#permissions). <br> ![Wählen Sie im Workflow hervorgehobenen Identitäts-Namespace aus, um Zielgruppen für Ziele zu aktivieren.](/help/destinations/assets/overview/export-identities-to-destination.png "Wählen Sie im Workflow hervorgehobenen Identitäts-Namespace aus, um Zielgruppen für Ziele zu aktivieren."){width="100" zoomable="yes"}

Anweisungen zum Aktivieren von Zielgruppensegmenten für dieses Ziel finden Sie unter [Aktivieren von Profilen und Segmenten für Streaming-Segmentexportziele](/help/destinations/ui/activate-segment-streaming-destinations.md).

Nachdem die Zielverbindung erstellt wurde, können Sie mit dem Aktivierungsfluss für die Zielgruppe fortfahren. Im folgenden Abschnitt wird erläutert, wie Sie Zielgruppen mithilfe des Echtzeit-Ziels aktivieren können.

### Zuordnen von Attributen und Identitäten {#map}

Der nächste Schritt besteht in der Zuordnung der Quell-IDs zur Magnite-Geräte-ID.

* Sie können so viele Zuordnungen wie nötig hinzufügen, indem Sie **[!UICONTROL Neues Mapping hinzufügen]**.

In diesem Beispiel, das das Echtzeit-Ziel verwendet, wird eine Zeile angezeigt, die eine generische deviceId-Quellkennung enthält, die dem Zielfeld Magnite device_id zugeordnet ist. Wenn Sie mit den Zuordnungen arbeiten, wählen Sie [!UICONTROL Nächste].

![Ordnen Sie die gewünschten Datenfelder dem Feld device_ID zu.](../../assets/catalog/advertising/magnite/destination-realtime-active-audience-field-mapping.png)

Stellen Sie sicher, dass die Zuordnungs-IDs für alle aktivierten Zielgruppen festgelegt sind, oder legen Sie KEINE fest, wenn keine Zuordnungs-ID vorhanden ist.

![Stellen Sie sicher, dass die Zuordnungs-IDs für alle aktivierten Zielgruppen festgelegt sind, oder legen Sie KEINE fest, wenn keine Zuordnungs-ID vorhanden ist.](../../assets/catalog/advertising/magnite/destination-realtime-active-audience-mappingid.png)

Jetzt müssen Sie für jede Zielgruppe ein Startdatum (obligatorisch), ein Enddatum (optional) und eine Zuordnungs-ID konfigurieren.

**Zuordnungs-ID**

* Verwenden Sie die **[!UICONTROL Zuordnungs-ID]** -Feld, wenn eine Zielgruppe über eine bereits vorhandene Segment-ID verfügt, die Magnite zuvor bekannt war.

* So fügen Sie eine **[!UICONTROL Zuordnungs-ID]** für eine Zielgruppe festzulegen, wählen Sie jede einzelne Zielgruppenzeile aus und geben Sie Daten in die rechte Spalte ein (siehe Bild oben). Wenn Sie keine Zuordnungs-ID hinzufügen möchten, geben Sie KEINE in das Feld Zuordnungs-ID ein.

Auswählen **[!UICONTROL Nächste]** und den Aktivierungsfluss abschließen.

![Wählen Sie Weiter aus und schließen Sie den Aktivierungsfluss ab.](../../assets/catalog/advertising/magnite/destination-realtime-active-audience-review.png)

## Exportierte Daten/Datenexport validieren {#exported-data}

Nach dem Hochladen Ihrer Zielgruppen können Sie mit den folgenden Schritten überprüfen, ob Ihre Zielgruppen korrekt erstellt und hochgeladen wurden:

<!--

* In 95% of cases, audiences will be delivered to Magnite Streaming in under 10 minutes. The actual receipt and processing of the events within Magnite Streaming depends on the shared data volume.

-->

* Post-Erfassung werden Zielgruppen voraussichtlich in [!DNL Magnite Streaming] innerhalb weniger Minuten und kann auf einen Deal angewendet werden. Sie können dies bestätigen, indem Sie nach der Segment-ID suchen, die während der Aktivierungsschritte in der Adobe Experience Platform freigegeben wurde.

## Aktivieren Sie dieselben Zielgruppen über die [!DNL Magnite Streaming: Batch]Ziel

Für freigegebene Zielgruppen [!DNL Magnite Streaming] Die Verwendung des Echtzeit-Ziels muss auch über das Magnite Streaming: Batch-Ziel freigegeben werden. Wenn die Segmentnamen richtig konfiguriert sind, finden Sie im [!DNL Magnite Streaming] Die Benutzeroberfläche wird aktualisiert, um die in der täglichen Adobe Experience Platform-Aktualisierung verwendeten zu widerspiegeln.

Wenn für Ihre Integration kein Batch-Ziel konfiguriert wurde, richten Sie es jetzt über das Dokument Magnite Streaming: Batch-Ziel ein.

## Datennutzung und -Governance {#data-usage-governance}

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Ausführliche Informationen darüber, wie [!DNL Adobe Experience Platform] Data Governance erzwingt, finden Sie unter [Data Governance - Übersicht](/help/data-governance/home.md).

## Zusätzliche Ressourcen {#additional-resources}

Weitere Hilfedokumentation finden Sie im Abschnitt [Magnite Help Center](https://help.magnite.com/help).
