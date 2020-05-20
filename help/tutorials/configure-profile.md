---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Schulungen zum Echtzeit-Profil von Kunden
topic: tutorial
translation-type: tm+mt
source-git-commit: ee08f43400fa72abce95ed52aff879f954f4b4d6
workflow-type: tm+mt
source-wordcount: '490'
ht-degree: 6%

---


# Echtzeit-Profil- und Identitätsdienst für Kunden konfigurieren

Zur Konfiguration des Echtzeit-Profils von Kunden für Ihr Unternehmen müssen Sie mehrere separate Workflows durchführen. In diesem Dokument werden die erforderlichen Schritte beschrieben und Links zu Lernprogrammen für die einzelnen Arbeitsabläufe bereitgestellt. Um mehr über Echtzeit-Kundendaten zu erfahren, lesen Sie zunächst den Überblick über das [Profil](../profile/home.md).

## Schema für Profil und Identität aktivieren

Bevor Daten in die Adobe Experience Platform aufgenommen und zur Erstellung von Echtzeit-Kundendaten verwendet werden können, muss ein Schema erstellt werden, das die Struktur der Daten bereitstellt, die erfasst werden sollen, und dieses Schema muss für die Verwendung in Profil und dem Adobe Experience Platform Identity Service aktiviert werden. Eine schrittweise Anleitung zum Erstellen eines Schemas, das sowohl für den Profil- als auch für den Identitätsdienst aktiviert ist, finden Sie in den Lernprogrammen zum [Erstellen eines Schemas mit der Schema-Registrierungs-API](../xdm/tutorials/create-schema-api.md) oder zum [Erstellen eines Schemas mithilfe der Schema Builder-Benutzeroberfläche](../xdm/tutorials/create-schema-ui.md).

## Dataset für Profil und Identität konfigurieren

Um Daten in Profil zu integrieren, müssen Sie über einen Datensatz verfügen, der ordnungsgemäß für die Verwendung mit dem Echtzeit-Kundendienst und dem Identitätsdienst konfiguriert wurde. Um zu beginnen, folgen Sie dem Lernprogramm zum [Konfigurieren eines Datensatzes für Profil und Identität](../profile/tutorials/dataset-configuration.md).

## Zusammenführungsrichtlinien konfigurieren

Mit der Adobe Experience Platform können Sie Daten aus mehreren Quellen zusammenführen und kombinieren, um eine vollständige Ansicht der einzelnen Kunden zu erhalten. Beim Zusammenführen dieser Daten dienen Zusammenführungsrichtlinien als jene Regeln, mit denen Platform bestimmt, wie Daten priorisiert werden und welche Daten kombiniert werden sollen, um eine Übersicht zu schaffen. Mit RESTful-APIs oder der Benutzeroberfläche können Sie neue Zusammenführungsrichtlinien erstellen, vorhandene Richtlinien verwalten und eine standardmäßige Zusammenführungsrichtlinie für Ihr Unternehmen festlegen. Informationen zum Arbeiten mit Zusammenführungsrichtlinien in der Plattform-Benutzeroberfläche finden Sie im [Benutzerhandbuch](../profile/ui/merge-policies.md)zu Zusammenführungsrichtlinien. Informationen zum Arbeiten mit Zusammenführungsrichtlinien mithilfe der Echtzeit-Profil-API finden Sie im Entwicklerhandbuch für [Zusammenführungsrichtlinien](../profile/api/merge-policies.md).

## Edge-Prognosen konfigurieren

Um koordinierte, konsistente und personalisierte Erlebnisse für Ihre Kunden über mehrere Kanal hinweg in Echtzeit zu ermöglichen, müssen die richtigen Daten jederzeit verfügbar sein und im Zuge von Änderungen kontinuierlich aktualisiert werden. Adobe Experience Platform ermöglicht diesen Echtzeitzugriff auf Daten durch die Verwendung von so genannten Kanten. Ein Edge ist ein geografisch platzierter Server, der Daten speichert und für Anwendungen leicht zugänglich macht. Die Daten werden durch eine Projektion an eine Kante geleitet, wobei ein Projektionsziel die Kante definiert, an die die Daten gesendet werden, und eine Projektionskonfiguration, die die spezifischen Informationen definiert, die an der Kante zur Verfügung gestellt werden. Weitere Informationen und die Möglichkeit, mit Kanten zu arbeiten, finden Sie im [Unterhandbuch zur Echtzeit-Kundendaten-API zu Edge-Prognosen](../profile/api/edge-projections.md).

## Nächste Schritte

Nachdem Sie Echtzeit-Kundendaten für Ihr Unternehmen konfiguriert haben, können Sie Daten zu einzelnen Profilen hinzufügen und Audiencen auf der Grundlage spezifischer Kundenattribute erstellen. Erste Schritte finden Sie in den folgenden Lernprogrammen:

* [Daten Hinzufügen Echtzeit-Profil](../profile/tutorials/add-profile-data.md)
* [Segment erstellen](../segmentation/tutorials/create-a-segment.md)