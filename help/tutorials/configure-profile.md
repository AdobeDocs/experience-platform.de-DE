---
keywords: Experience Platform;Home;beliebte Themen;Echtzeit-Profil des Kunden;Identitätsdienst;
solution: Experience Platform
title: Tutorials zum Echtzeit-Kundenprofil
topic-legacy: tutorial
type: Tutorial
description: In diesem Dokument werden die erforderlichen Schritte beschrieben und Links zu Tutorials für die einzelnen Workflows bereitgestellt.
exl-id: cda6e7a7-9498-454c-94df-c6271a5a4fd4
translation-type: tm+mt
source-git-commit: d425dcd9caf8fccd0cb35e1bac73950a6042a0f8
workflow-type: tm+mt
source-wordcount: '796'
ht-degree: 24%

---

# Konfigurieren von [!DNL Real-time Customer Profile]

Um [!DNL Real-time Customer Profile] für Ihr Unternehmen zu konfigurieren, müssen Sie mehrere separate Workflows durchführen. In diesem Dokument werden die erforderlichen Schritte beschrieben und Links zu Tutorials für die einzelnen Workflows bereitgestellt.

Um mehr über [!DNL Real-time Customer Profile] zu erfahren, lesen Sie zunächst den [Profil overview](../profile/home.md).

## Übersicht über das Echtzeit-Profil

Das Echtzeit-Kundenprofil erstellt eine ganzheitliche Sicht Ihrer einzelnen Kunden und fasst Daten aus mehreren Kanälen (einschließlich Online-, Offline-, CRM- und Drittanbieter-Daten) zusammen.

**Dieses Handbuch hilft Ihnen:**
- Machen Sie sich mit der Benutzeroberfläche und den verfügbaren Funktionen vertraut.
- Ansicht und Verwaltung Ihrer Profil-Daten.

Weitere Informationen finden Sie im Benutzerhandbuch [Echtzeit-Profil des Kunden](../profile/ui/user-guide.md)

## Echtzeit-Kundenprofil-API

Die Echtzeit-Client-Profil-API enthält mehrere Endpunkte. Weitere Informationen zu den einzelnen verfügbaren Endpunkten und Anwendungsfällen finden Sie in der Übersicht über die [Echtzeit-Kunden-Profil-API](../profile/api/overview.md).

Weitere Informationen und die erforderlichen Werte für die Ausführung von CRUD-Operationen mit der Echtzeit-Client-Profil-API finden Sie im Handbuch [Erste Schritte](../profile/api/getting-started.md).

## Schema für [!DNL Profile] und [!DNL Identity]-Dienst aktivieren

Bevor Daten in Adobe Experience Platform aufgenommen und bei der Erstellung von [!DNL Real-time Customer Profiles] verwendet werden können, muss ein Schema erstellt werden, das die Struktur der Daten bereitstellt, die erfasst werden sollen, und dieses Schema muss für die Verwendung in [!DNL Profile] und Adobe Experience Platform [!DNL Identity Service] aktiviert werden.

**Dieses Handbuch hilft Ihnen:**
- Durchsuchen Sie vorhandene Schema.
- Erstellen und Benennen eines Schemas.
- XDM-Schema-Feldgruppen Hinzufügen und definieren.
- Legen Sie Ihre Schema-Felder als Identitätsfelder fest.
- Aktivieren Sie Profil für Ihr Schema.

Schrittweise Anleitungen zum Erstellen eines Schemas, das sowohl für [!DNL Profile] als auch für [!DNL Identity Service] aktiviert ist, finden Sie in den Anleitungen zum Erstellen eines Schemas mit der Schema Registry-API](../xdm/tutorials/create-schema-api.md) oder [Erstellen eines Schemas mithilfe der Schema Builder-Benutzeroberfläche](../xdm/tutorials/create-schema-ui.md).[

## Datensatz für [!DNL Profile] und [!DNL Identity] konfigurieren

Um Daten in [!DNL Profile] einzufügen, müssen Sie über einen Datensatz verfügen, der für die Verwendung mit [!DNL Real-time Customer Profile] und [!DNL Identity Service] richtig konfiguriert wurde.

**Dieses Handbuch hilft Ihnen:**
- Erstellen Sie einen zum Profil aktivierten Datensatz.
- Konfigurieren Sie vorhandene Datensätze.
- Daten in den Datensatz aufnehmen.
- Vergewissern Sie sich, dass Ihr Datensatz für Profil aktiviert ist und verwenden Sie den Identitätsdienst.

Beginnen Sie mit dem API-Lernprogramm für [Konfigurieren eines Datensatzes für Profil und Identität](../profile/tutorials/dataset-configuration.md).

## Konfigurieren von Zusammenführungsrichtlinien

Mit Adobe Experience Platform können Sie Daten aus verschiedenen Quellen zusammenführen und kombinieren, damit Sie sich einen kompletten Überblick über einzelne Kunden verschaffen können. Beim Zusammenführen dieser Daten sind Zusammenführungsrichtlinien die Regeln, die [!DNL Platform] verwenden, um zu bestimmen, wie die Daten priorisiert werden und welche Daten kombiniert werden, um diese einheitliche Ansicht zu erstellen.

**Dieses Handbuch hilft Ihnen:**
- Erstellen Sie neue Zusammenführungsrichtlinien.
- Verwalten Sie vorhandene Zusammenführungsrichtlinien.
- Legen Sie eine standardmäßige Mergerichtlinie für Ihr Unternehmen fest.
- Verstehen Sie die Verstöße gegen die Fusionsrichtlinie.

Um mit Mergerichtlinien in der [!DNL Platform]-Benutzeroberfläche zu arbeiten, besuchen Sie das [Richtlinien zusammenführen-Benutzerhandbuch](../profile/ui/merge-policies.md). Informationen zum Arbeiten mit Zusammenführungsrichtlinien mithilfe der Echtzeit-Kundenprofil-API finden Sie im [Entwicklerhandbuch für Zusammenführungsrichtlinien](../profile/api/merge-policies.md).

## Konfigurieren von Edge-Projektionen

Um koordinierte, konsistente und personalisierte Erlebnisse für Ihre Kunden über mehrere Kanal hinweg in Echtzeit zu ermöglichen, müssen die richtigen Daten jederzeit verfügbar sein und im Zuge von Änderungen kontinuierlich aktualisiert werden. Die Adobe [!DNL Experience Platform] ermöglicht diesen Echtzeitzugriff auf Daten mithilfe von so genannten Kanten. Ein Edge ist ein regional aufgestellter Server, der Daten erfasst und direkt für Anwendungen abrufbar macht. Die Daten werden mittels Projektion an einen Edge übermittelt, wobei ein Projektionsziel den Edge definiert, an den die Daten gesendet werden, und eine Projektionskonfiguration, die die Informationen spezifiziert, die am Edge zur Verfügung gestellt werden.

**Dieses Handbuch hilft Ihnen:**
- Liste, Erstellen, Ansicht, Aktualisieren und Löschen eines Ziels für die Edge-Projektion.
- Liste und Erstellung einer Edge-Projektionskonfiguration.
- Verstehen Sie Selektoren.

Weitere Informationen und die Möglichkeit, mit Kanten zu arbeiten, finden Sie im Unterleitfaden [!DNL Real-time Customer Profile] API [zu Kantenprojektionen](../profile/api/edge-projections.md).

## Anpassen der Anzeige von Profil-Daten in der Benutzeroberfläche

In der Benutzeroberfläche der Experience Platform können Sie Kundendaten in Echtzeit in Form von Kundendaten in Profilen Ansicht und Interaktion mit ihnen durchführen. Die in der Benutzeroberfläche angezeigten Informationen zum Profil wurden aus mehreren Profil-Fragmenten zusammengeführt, um eine Ansicht des jeweiligen Kunden zu bilden. Dazu gehören Details wie Basisattribute, verknüpfte Identitäten und Voreinstellungen für Kanal. Die in den Profilen angezeigten Standardfelder können auch auf organisatorischer Ebene geändert werden, um bevorzugte Profil-Attribute anzuzeigen.

**Dieses Handbuch hilft Ihnen:**
- Karten neu anordnen, ihre Größe ändern, bearbeiten und entfernen.
- hinzufügen Attribute.
- hinzufügen eine neue Karte.
- Standardwerte wiederherstellen.

Weitere Informationen zum Anpassen von Profil-Daten finden Sie in der [Dokumentation zur Profil-Anpassung](../profile/ui/profile-customization.md)

## Nächste Schritte

Nachdem Sie [!DNL Real-time Customer Profile] für Ihr Unternehmen konfiguriert haben, können Sie beginnen, Daten zu einzelnen Profilen hinzuzufügen und Audiencen auf der Grundlage spezifischer Kundenattribute zu erstellen. Erste Schritte finden Sie in den folgenden Tutorials:

- [Hinzufügen von Daten zum Echtzeit-Kundenprofil](../profile/tutorials/add-profile-data.md)
- [Erstellen eines Segments](../segmentation/tutorials/create-a-segment.md)
