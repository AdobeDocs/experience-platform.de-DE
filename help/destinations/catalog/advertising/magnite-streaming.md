---
title: Echtzeit-Zielverbindung Magnite
description: Verwenden Sie dieses Ziel, um Adobe-CDP-Zielgruppen in Echtzeit für die Magnite-Streaming-Plattform bereitzustellen.
last-substantial-update: 2024-11-18T00:00:00Z
exl-id: 4e08a14b-6800-41e1-95a5-826a6241144d
source-git-commit: da05db9376893bdbe8f0aa291f19a507e4a73d4f
workflow-type: tm+mt
source-wordcount: '1317'
ht-degree: 31%

---

# Magnitude: Echtzeit-Zielverbindung

## Übersicht {#overview}

Die [!DNL Magnite: Real-Time] und die Ziele [Magnite: Batch](/help/destinations/catalog/advertising/magnite-batch.md) in Adobe Experience Platform helfen Ihnen, Zielgruppen für das Targeting und die Aktivierung auf der Magnite-Streaming-Plattform zuzuordnen und zu exportieren.

Das Aktivieren von Zielgruppen für die [!DNL Magnite Streaming] ist ein zweistufiger Prozess, für den Sie sowohl die Ziele Magnite: Echtzeit als auch Magnite: Batch verwenden müssen.

Um Ihre Zielgruppen für die [!DNL Magnite Streaming] zu aktivieren, müssen Sie:

* Aktivieren Sie die Zielgruppen im [!DNL Magnite: Real-Time] Ziel, wie auf dieser Seite gezeigt.
* Aktivieren Sie dieselbe Zielgruppe auf dem Ziel Magnitude: Batch . Das [!DNL Magnite: Batch] ist eine obligatorische Komponente. Wenn Sie die Zielgruppe im [!DNL Magnite Streaming] Batch-Ziel nicht aktivieren, führt dies zu einer fehlgeschlagenen Integration, und Ihre Zielgruppen werden nicht aktiviert.

Hinweis: Bei Verwendung des Echtzeit-Ziels empfangen [!DNL Magnite Streaming] Zielgruppen in Echtzeit, aber Magnite kann Echtzeit-Zielgruppen nur vorübergehend auf seiner Plattform speichern und sie werden innerhalb weniger Tage aus dem System entfernt. Wenn Sie daher das Echtzeit-Ziel Magnite: verwenden möchten, müssen Sie *auch* das Ziel Magnite: Batch verwenden. Dabei handelt es sich um jede Zielgruppe, die Sie für das Echtzeit-Ziel aktivieren, außerdem müssen Sie für das Batch-Ziel aktivieren.

>[!IMPORTANT]
>
>Der Ziel-Connector und die Dokumentationsseite werden vom [!DNL Magnite]-Team erstellt und gepflegt. Bei Fragen oder Aktualisierungsanfragen wenden Sie sich bitte direkt an `adobe-tech@magnite.com`.

## Anwendungsfälle {#use-cases}

Damit Sie besser verstehen können, wie und wann Sie das [!DNL Magnite: Real-Time]-Ziel verwenden sollten, finden Sie hier ein Anwendungsbeispiel, das für Kundinnen und Kunden von Adobe Experience Platform mit diesem Ziel geeignet ist.

### Aktivierung und Zielgruppenbestimmung {#activation-and-targeting}

Durch diese Integration mit Magnite können Kunden ihre CDP-Zielgruppen von Adobe Experience Platform an Magnite für das Anzeigen-Targeting weiterleiten. Zielgruppen können in der Magnitude für positives Targeting sowie für negatives Targeting (Unterdrückung) ausgewählt werden.

## Voraussetzungen {#prerequisites}

Um die [!DNL Magnite] Ziele in Adobe Experience Platform verwenden zu können, müssen Sie zunächst über ein [!DNL Magnite Streaming] verfügen. Wenn Sie über ein [!DNL Magnite Streaming]-Konto verfügen, wenden Sie sich an Ihren [!DNL Magnite] Account Manager, um Anmeldeinformationen für den Zugriff auf [!DNL Magnite's] Ziele zu erhalten.
Wenn Sie noch kein [!DNL Magnite Streaming]-Konto haben, wenden Sie sich bitte an adobe-tech@magnite.com

## Unterstützte Identitäten {#supported-identities}

Das [!DNL Magnite: Real-Time]-Ziel unterstützt die Aktivierung von Identitäten, die in der folgenden Tabelle beschrieben sind. Erhalten Sie weitere Informationen zu [Identitäten](/help/identity-service/features/namespaces.md).

| Ziel-Identität | Beschreibung | Zu beachten |
|-------------------|--------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------|
| device_id | Eine eindeutige Kennung für ein Gerät oder eine Identität. Wir akzeptieren alle Geräte-IDs und Erstanbieter-IDs unabhängig vom Typ. | Zu den von Magnite unterstützten Identitätstypen gehören u. a. PPUID-, GAID-, IDFA- und TV-Geräte-IDs. |

{style="table-layout:auto"}

## Unterstützte Zielgruppen {#supported-audiences}

In diesem Abschnitt wird beschrieben, welche Art von Zielgruppen Sie an dieses Ziel exportieren können.

| Zielgruppenherkunft | Unterstützt | Beschreibung |
|-----------------------------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Zielgruppen, die über den Experience Platform ([-Service) generiert &#x200B;](../../../segmentation/home.md). |
| Benutzerdefinierte Uploads | ✓ | Zielgruppen, die aus CSV-Dateien in Experience Platform [importiert](../../../segmentation/ui/audience-portal.md#import-audience) werden. |

{style="table-layout:auto"}

## Exporttyp und -häufigkeit {#export-type-frequency}

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| Element | Typ | Anmerkungen |
|------------------|---------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Exporttyp | **[!UICONTROL Segmentexport]** | Sie exportieren alle Mitglieder eines Segments (Zielgruppe) mit den IDs (Name, Telefonnummer oder sonstiges), die im [!DNL Magnite: Real-Time]-Ziel verwendet werden. |
| Exporthäufigkeit | **[!UICONTROL Streaming]** | Streaming-Ziele sind „immer verfügbare“ API-basierte Verbindungen. Sobald ein Profil in Experience Platform auf der Grundlage einer Segmentauswertung aktualisiert wird, sendet der Connector das Update nachgelagert an die Zielplattform. Lesen Sie mehr über [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Herstellen einer Verbindung mit dem Ziel {#connect}

>[!IMPORTANT]
>
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die Berechtigungen **[!UICONTROL Ziele anzeigen]** und **[!UICONTROL Ziele verwalten]** [Zugriffssteuerung](/help/access-control/home.md#permissions). Lesen Sie die [Zugriffskontrolle – Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor. Füllen Sie im Workflow zum Konfigurieren des Ziels die Felder aus, die in den beiden folgenden Abschnitten aufgeführt sind.

### Beim Ziel authentifizieren {#authenticate}

Um sich beim Ziel zu authentifizieren, füllen Sie die erforderlichen Felder aus und wählen Sie **[!UICONTROL Mit Ziel verbinden]** aus.

![Nicht ausgefüllte Authentifizierungsfelder der Zielkonfiguration](../../assets/catalog/advertising/magnite/destination-realtime-config-auth-unfilled.png)

* **[!UICONTROL Benutzername]**: Der von [!DNL Magnite] bereitgestellte Benutzername.
* **[!UICONTROL Kennwort]**: Das Kennwort, das Sie von [!DNL Magnite] erhalten haben.

### Ausfüllen der Zieldetails {#destination-details}

Füllen Sie die folgenden erforderlichen und optionalen Felder aus, um Details für das Ziel zu konfigurieren. Ein Sternchen neben einem Feld in der Benutzeroberfläche zeigt an, dass das Feld erforderlich ist.

* **[!UICONTROL Name]**: Ein Name, durch den Sie dieses Ziel in Zukunft erkennen können.
* **[!UICONTROL Beschreibung]**: Eine Beschreibung, die Ihnen hilft, dieses Ziel in Zukunft zu identifizieren.
* **[!UICONTROL Ihr Firmenname]**: Ihr Kunden-/Firmenname. Es stehen nur unterstützte [!DNL Magnite Streaming]-Clients zur Auswahl.

>[!NOTE]
>
>Der Firmenname muss eine Zeichenfolge sein, die mit dem Namen des Amazon S3-Bereitstellungs-Buckets übereinstimmt, den Sie mit Magnite konfiguriert und im Schritt [Authentifizieren bei Ziel](#authenticate) eingerichtet haben. Zu den unterstützten Zeichen gehören „a-z“, „A-Z“, „0-9“, &quot;-„(Bindestrich) oder „_„(Unterstrich).

![Authentifizierungsfelder für die Zielkonfiguration ausgefüllt](../../assets/catalog/advertising/magnite/destination-realtime-config-auth-filled.png)

Klicken Sie abschließend auf die Schaltfläche **[!UICONTROL Erstellen]**.

![Optionale Governance-Richtlinie und Durchsetzungsmaßnahmen](../../assets/catalog/advertising/magnite/destination-realtime-config-grouping-policy.png)

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie mit dem Eingeben der Details für Ihre Zielverbindung fertig sind, klicken Sie auf **[!UICONTROL Weiter]**.

## Aktivieren von Segmenten für dieses Ziel {#activate}

>[!IMPORTANT]
>
>* Zum Aktivieren von Daten benötigen Sie die Berechtigungen **[!UICONTROL Ziele anzeigen]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]**&#x200B;[Zugriffssteuerung](/help/access-control/home.md#permissions). Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.
>* Zum Exportieren *Identitäten* benötigen Sie die Berechtigung **[!UICONTROL Identitätsdiagramm anzeigen]** [Zugriffssteuerung](/help/access-control/home.md#permissions). <br> ![Wählen Sie einen im Workflow hervorgehobenen Identity-Namespace aus, um Zielgruppen für Ziele zu aktivieren.](/help/destinations/assets/overview/export-identities-to-destination.png "Wählen Sie einen im Workflow hervorgehobenen Identity-Namespace aus, um Zielgruppen für Ziele zu aktivieren."){width="100" zoomable="yes"}

Anweisungen zum Aktivieren von Zielgruppensegmenten für dieses Ziel finden Sie unter [Aktivieren von Profilen und Segmenten für Streaming-Segmentexportziele](/help/destinations/ui/activate-segment-streaming-destinations.md).

Nachdem die Zielverbindung erstellt wurde, können Sie mit dem Aktivierungsfluss für die Zielgruppe fortfahren. Im folgenden Abschnitt wird erläutert, wie Sie Zielgruppen mithilfe des Echtzeit-Ziels aktivieren.

### Zuordnen von Attributen und Identitäten {#map}

Der nächste Schritt besteht darin, Quellkennungen der ID „Magnite device_id“ zuzuordnen.

* Sie können beliebig viele Zuordnungen hinzufügen, indem Sie **[!UICONTROL Neue Zuordnung hinzufügen]** auswählen.

Dieses Beispiel zeigt unter Verwendung des Echtzeit-Ziels eine Zeile, die eine generische deviceId-Quellkennung enthält, die dem Zielfeld Magnite device_id zugeordnet ist. Wenn Sie mit den Zuordnungen fertig sind, klicken Sie auf [!UICONTROL Weiter].

![Ordnen Sie dem Feld device_id die gewünschten Datenfelder zu](../../assets/catalog/advertising/magnite/destination-realtime-active-audience-field-mapping.png)

Stellen Sie sicher, dass Sie die Zuordnungs-IDs auf alle aktivierten Zielgruppen festlegen oder auf KEINE setzen, wenn keine Zuordnungs-ID vorhanden ist.

![Stellen Sie sicher, dass Sie die Zuordnungs-IDs für alle aktivierten Zielgruppen festlegen oder KEINE festlegen, wenn keine Zuordnungs-ID vorhanden ist](../../assets/catalog/advertising/magnite/destination-realtime-active-audience-mappingid.png)

Jetzt müssen Sie für jede Zielgruppe ein Startdatum (obligatorisch), ein Enddatum (optional) und eine Zuordnungs-ID konfigurieren.

**Zuordnungs-ID**

* Verwenden Sie das **[!UICONTROL Zuordnungs-ID]**-Feld, wenn eine Zielgruppe eine bereits vorhandene Segment-ID hat, die Magnite zuvor bekannt war.

* Um einer Zielgruppe eine **[!UICONTROL Zuordnungs]** ID) hinzuzufügen, wählen Sie jede Zielgruppenzeile einzeln aus und geben Sie Daten in der rechten Spalte ein (siehe Abbildung oben). Wenn Sie keine Zuordnungs-ID hinzufügen möchten, geben Sie KEINE in das Feld Zuordnungs-ID ein.

Wählen Sie **[!UICONTROL Weiter]** und schließen Sie den Aktivierungsfluss ab.

![Wählen Sie Weiter aus und schließen Sie den Aktivierungsfluss ab.](../../assets/catalog/advertising/magnite/destination-realtime-active-audience-review.png)

## Exportierte Daten/Datenexport validieren {#exported-data}

Nach dem Hochladen Ihrer Zielgruppen können Sie mithilfe der folgenden Schritte überprüfen, ob Ihre Zielgruppen korrekt erstellt und hochgeladen wurden:

<!--

* In 95% of cases, audiences will be delivered to Magnite Streaming in under 10 minutes. The actual receipt and processing of the events within Magnite Streaming depends on the shared data volume.

-->

* Nach der Aufnahme werden Zielgruppen voraussichtlich innerhalb weniger Minuten in [!DNL Magnite Streaming] angezeigt und können auf ein Angebot angewendet werden. Sie können dies bestätigen, indem Sie die Segment-ID nachschlagen, die während der Aktivierungsschritte in der Adobe Experience Platform freigegeben wurde.

## Aktivieren derselben Zielgruppen über das [!DNL Magnite: Batch]Ziel

Audiences, die für [!DNL Magnite Streaming] über das Echtzeit-Ziel freigegeben wurden, müssen auch über das Ziel Magnite: Batch freigegeben werden. Wenn die Segmentnamen in der [!DNL Magnite Streaming]-Benutzeroberfläche korrekt konfiguriert sind, werden sie entsprechend den Segmentnamen aktualisiert, die in der posttäglichen Aktualisierung von Adobe Experience Platform verwendet werden.

Wenn für Ihre Integration kein Batch-Ziel konfiguriert wurde, richten Sie es jetzt über das Dokument Magnite: Batch-Ziel ein.

## Datennutzung und -Governance {#data-usage-governance}

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Ausführliche Informationen darüber, wie [!DNL Adobe Experience Platform] Data Governance erzwingt, finden Sie unter [Data Governance - Übersicht](/help/data-governance/home.md).

## Zusätzliche Ressourcen {#additional-resources}

Weitere Hilfedokumentation finden Sie im [Magnite Help Center](https://help.magnite.com/help).
