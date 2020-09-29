---
keywords: Experience Platform;home;popular topics;Real-time Customer Profile;Identity Service;
solution: Experience Platform
title: Tutorials zum Echtzeit-Kundenprofil
topic: tutorial
type: Tutorial
description: In diesem Dokument werden die erforderlichen Schritte beschrieben und Links zu Tutorials für die einzelnen Workflows bereitgestellt.
translation-type: tm+mt
source-git-commit: 844ef4a0131e41d3a7a3da319ccf7f8d5cf1f40d
workflow-type: tm+mt
source-wordcount: '1001'
ht-degree: 25%

---


# Konfigurieren [!DNL Real-time Customer Profile] und [!DNL Identity Service]

In order to configure [!DNL Real-time Customer Profile] for your organization, you are required to complete multiple separate workflows. In diesem Dokument werden die erforderlichen Schritte beschrieben und Links zu Tutorials für die einzelnen Workflows bereitgestellt.

To learn more about [!DNL Real-time Customer Profile], begin by reading the [Profile overview](../profile/home.md).

## Übersicht über das Echtzeit-Profil

Das Echtzeit-Kundenprofil erstellt eine ganzheitliche Sicht Ihrer einzelnen Kunden und fasst Daten aus mehreren Kanälen (einschließlich Online-, Offline-, CRM- und Drittanbieter-Daten) zusammen.

**Dieses Handbuch hilft Ihnen:**
- Machen Sie sich mit der Benutzeroberfläche der [!UICONTROL Profil] und den verfügbaren Funktionen vertraut.
- Ansicht und Verwaltung Ihrer Profil-Daten.

Weitere Informationen finden Sie im Benutzerhandbuch für das [Echtzeit-Profil.](../profile/ui/user-guide.md)

## Echtzeit-Kundenprofil-API

Die Echtzeit-Client-Profil-API enthält mehrere Endpunkte. Mit Profil können Sie heterogene Kundendaten aus verschiedenen Kanälen, z. B. Online-, Offline-, CRM- und Drittanbieter-Daten, in einer einheitlichen Ansicht zusammenfassen, die eine verwertbare Auflistung mit Zeitstempel für jede Kundeninteraktion bietet. Weitere Informationen zu den einzelnen Endpunkten und Anwendungsfällen finden Sie in der Übersicht [zur](../profile/api/overview.md) Echtzeit-Kunden-Profil-API.

**Die folgenden API-Entwicklerhandbücher stehen zur Verfügung:**
- [Berechnete Attribute (Alpha) ](../profile/api/computed-attributes.md) - Erfahren Sie mehr über Anwendungsfälle für berechnete Attribute sowie darüber, wie ein berechnetes Attribut konfiguriert, aufgerufen, aktualisiert und gelöscht werden kann.
- [Edge-Projektionen](../profile/api/edge-projections.md) - Erfahren Sie, wie Sie Ziele für die Projektion, Ansicht, Aktualisierung, Löschen und Liste erstellen, aktualisieren und löschen. Außerdem enthält dieses Dokument Informationen zur Auflistung und Erstellung von Projektionskonfigurationen und Beispiele zur Verwendung von Selektoren.
- [Entitäten (Profil-Zugriff)](../profile/api/entities.md) - Erfahren Sie, wie Sie auf Profil-Daten durch Identitäten oder eine Liste von Identitäten zugreifen können. Erfahren Sie außerdem, wie Sie mithilfe von Identitäten, einem einzelnen Profil nach Identität und dem Zugriff auf mehrere Schema-Entitäten auf Zeitreihen-Ereignis für mehrere Profil zugreifen können.
- [Exportaufträge (Profil-Export)](../profile/api/export-jobs.md) - Erfahren Sie, wie Sie Exportaufträge erstellen, Ansicht, überwachen und abbrechen.
- [Richtlinien](../profile/api/merge-policies.md) zusammenführen - Erfahren Sie mehr über die Komponenten von Zusammenführungsrichtlinien und wie Sie auf eine Zusammenführungsrichtlinie zugreifen, diese erstellen, aktualisieren und löschen.
- [Beispielstatus der Vorschau (Profil-Vorschau)](../profile/api/preview-sample-status.md) - Erfahren Sie, wie Sie Ihren letzten Beispielstatus, die Verteilung des Liste-Profils nach Datensatz und die Verteilung des Liste-Profils nach Namensraum Ansicht festlegen.
- [Profil-Systemaufträge (Anforderungen löschen)](../profile/api/profile-system-jobs.md) - Erfahren Sie, wie Sie eine Anforderung zum Löschen eines Datensatzes oder Stapels im Profil Store Ansicht, erstellen und entfernen.

Weitere Informationen und die erforderlichen Werte für die Ausführung von CRUD-Operationen mit der Echtzeit-Client-Profil-API finden Sie im Handbuch [Erste Schritte](../profile/api/getting-started.md).

## Schema für [!DNL Profile] und [!DNL Identity] Dienst aktivieren

Before data can be ingested into Adobe Experience Platform and used in the creation of [!DNL Real-time Customer Profiles], a schema must be created to provide the structure for the data that will be ingested and that schema must be enabled for use in [!DNL Profile] and Adobe Experience Platform [!DNL Identity Service].

**Dieses Handbuch hilft Ihnen:**
- Durchsuchen Sie vorhandene Schema.
- Erstellen und Benennen eines Schemas.
- hinzufügen und definieren Sie XDM-Mixins.
- Legen Sie Ihre Schema-Felder als Identitätsfelder fest.
- Aktivieren Sie Profil für Ihr Schema.

For step-by-step instructions on creating a schema that is enabled for both [!DNL Profile] and [!DNL Identity Service], please refer to the tutorials for [creating a schema using the Schema Registry API](../xdm/tutorials/create-schema-api.md) or [creating a schema using the Schema Builder UI](../xdm/tutorials/create-schema-ui.md).

## Konfigurieren eines Datensatzes für [!DNL Profile] und [!DNL Identity]

To begin ingesting data into [!DNL Profile], you must have a dataset that has been properly configured for use with [!DNL Real-time Customer Profile] and [!DNL Identity Service].

**Dieses Handbuch hilft Ihnen:**
- Erstellen Sie einen zum Profil aktivierten Datensatz.
- Konfigurieren Sie vorhandene Datensätze.
- Daten in den Datensatz aufnehmen.
- Vergewissern Sie sich, dass Ihr Datensatz für Profil aktiviert ist und verwenden Sie den Identitätsdienst.

Beginnen Sie mit dem API-Lernprogramm zum [Konfigurieren eines Datensatzes für Profil und Identität](../profile/tutorials/dataset-configuration.md).

## Konfigurieren von Zusammenführungsrichtlinien

Mit Adobe Experience Platform können Sie Daten aus verschiedenen Quellen zusammenführen und kombinieren, damit Sie sich einen kompletten Überblick über einzelne Kunden verschaffen können. When bringing this data together, merge policies are the rules that [!DNL Platform] uses to determine how data will be prioritized and what data will be combined to create that unified view.

**Dieses Handbuch hilft Ihnen:**
- Erstellen Sie neue Zusammenführungsrichtlinien.
- Verwalten Sie vorhandene Zusammenführungsrichtlinien.
- Legen Sie eine standardmäßige Mergerichtlinie für Ihr Unternehmen fest.
- Verstehen Sie die Verstöße gegen die Fusionsrichtlinie.

To work with merge policies in the [!DNL Platform] UI, visit the [merge policies user guide](../profile/ui/merge-policies.md). Informationen zum Arbeiten mit Zusammenführungsrichtlinien mithilfe der Echtzeit-Kundenprofil-API finden Sie im [Entwicklerhandbuch für Zusammenführungsrichtlinien](../profile/api/merge-policies.md).

## Konfigurieren von Edge-Projektionen

Um koordinierte, konsistente und personalisierte Erlebnisse für Ihre Kunden über mehrere Kanäle hinweg in Echtzeit umsetzen zu können, müssen die richtigen Daten jederzeit verfügbar sein und bei Änderungen kontinuierlich aktualisiert werden. Adobe [!DNL Experience Platform] enables this real-time access to data through the use of what are known as edges. Ein Edge ist ein regional aufgestellter Server, der Daten erfasst und direkt für Anwendungen abrufbar macht. Die Daten werden mittels Projektion an einen Edge übermittelt, wobei ein Projektionsziel den Edge definiert, an den die Daten gesendet werden, und eine Projektionskonfiguration, die die Informationen spezifiziert, die am Edge zur Verfügung gestellt werden.

**Dieses Handbuch hilft Ihnen:**
- Liste, Erstellen, Ansicht, Aktualisieren und Löschen eines Ziels für die Edge-Projektion.
- Liste und Erstellung einer Edge-Projektionskonfiguration.
- Verstehen Sie Selektoren.

For more information and to begin working with edges, refer to the [!DNL Real-time Customer Profile] API [sub-guide on edge projections](../profile/api/edge-projections.md).

## Anpassen der Anzeige von Profil-Daten in der Benutzeroberfläche

In der Benutzeroberfläche der Experience Platform können Sie Kundendaten in Echtzeit in Form von Kundendaten in Profilen Ansicht und Interaktion mit ihnen durchführen. Die in der Benutzeroberfläche angezeigten Informationen zum Profil wurden aus mehreren Profil-Fragmenten zusammengeführt, um eine Ansicht des jeweiligen Kunden zu bilden. Dazu gehören Details wie Basisattribute, verknüpfte Identitäten und Voreinstellungen für Kanal. Die in den Profilen angezeigten Standardfelder können auch auf organisatorischer Ebene geändert werden, um bevorzugte Profil-Attribute anzuzeigen.

**Dieses Handbuch hilft Ihnen:**
- Karten neu anordnen, ihre Größe ändern, bearbeiten und entfernen.
- hinzufügen Attribute.
- hinzufügen eine neue Karte.
- Standardwerte wiederherstellen.

Weitere Informationen zum Anpassen von Profil-Daten finden Sie in der Dokumentation zur [Profil-Anpassung](../profile/ui/profile-customization.md)

## Nächste Schritte

Once you have configured [!DNL Real-time Customer Profile] for your organization, you can begin adding data to individual customer profiles and creating audience segments based on specific customer attributes. Erste Schritte finden Sie in den folgenden Tutorials:

- [Hinzufügen von Daten zum Echtzeit-Kundenprofil](../profile/tutorials/add-profile-data.md)
- [Erstellen eines Segments](../segmentation/tutorials/create-a-segment.md)