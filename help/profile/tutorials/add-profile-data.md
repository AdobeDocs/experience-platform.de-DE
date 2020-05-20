---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Daten Hinzufügen Echtzeit-Profil
topic: tutorial
translation-type: tm+mt
source-git-commit: 6d24637dc6cc282f98288b6416e4a3b7cebe42ea
workflow-type: tm+mt
source-wordcount: '401'
ht-degree: 0%

---


# Daten Hinzufügen Echtzeit-Profil

In diesem Lernprogramm werden die Schritte beschrieben, die zum Hinzufügen von Daten zum Echtzeit-Kundenkonto erforderlich sind.

## Aktivieren eines Schemas für Echtzeit-Kundendaten-Profil

Daten, die in Experience Platform für die Verwendung durch Echtzeit-Kundendaten aufgenommen werden, müssen mit einem XDM-Schema (Experience Data Model) übereinstimmen, das zum Profil aktiviert wurde. Damit ein Schema zum Profil aktiviert werden kann, muss es entweder die XDM Individual Profil- oder die XDM ExperienceEvent-Klasse implementieren.

Sie können ein Schema zur Verwendung im Echtzeit-Kundenkonto über die Schema-Registrierungs-API oder die Schema-Editor-Benutzeroberfläche aktivieren. Beginnen Sie zunächst mit den Übungen zum [Erstellen eines Schemas mit APIs](../../xdm/tutorials/create-schema-api.md) oder zum [Erstellen eines Schemas mithilfe der Benutzeroberfläche](../../xdm/tutorials/create-schema-ui.md)des Schema-Editors.

## Hinzufügen von Daten mithilfe der Stapelverarbeitung

Alle Daten, die mit der Stapelverarbeitung auf die Plattform hochgeladen wurden, werden in einzelne Datensätze hochgeladen. Bevor diese Daten von Echtzeit-Kundendaten verwendet werden können, muss der betreffende Datensatz spezifisch konfiguriert werden. Vollständige Anweisungen finden Sie im Lernprogramm zum [Konfigurieren eines Datensatzes für den Profil- und Identitätsdienst](dataset-configuration.md).

Nachdem der Datensatz konfiguriert wurde, können Sie Daten in den Datensatz eingeben. Detaillierte Anweisungen zum Hochladen von Dateien in verschiedenen Formaten finden Sie im [Entwicklerhandbuch](../../ingestion/batch-ingestion/api-overview.md) zur Stapelverarbeitung.

## Hinzufügen von Daten mit Streaming-Erfassung

Alle Stream-erfassten Daten, die mit einem Profil-aktivierten XDM-Schema konform sind, werden automatisch den entsprechenden Datensatz in Echtzeit-Kundendaten-Profil hinzufügen oder überschreiben. Wenn mehr als eine Identität im Datensatz bereitgestellt wird oder Zeitreihendaten verwendet werden, werden diese Identitäten im Identitätsdiagramm ohne zusätzliche Konfiguration zugeordnet. Weitere Informationen finden Sie im Entwicklerhandbuch [zur](../../ingestion/tutorials/streaming-record-data.md) Streaming-Erfassung.

## Überprüfen, ob der Upload erfolgreich war

Beim erstmaligen Hochladen von Daten in einen neuen Datensatz oder im Rahmen eines Prozesses mit einer neuen ETL oder Datenquelle wird empfohlen, die Daten sorgfältig zu überprüfen, um sicherzustellen, dass sie korrekt hochgeladen wurden.

Mit der Echtzeit-API für den Zugriff auf Kundendaten können Sie Stapeldaten abrufen, während sie in ein Profil geladen werden. Wenn Sie keine der erwarteten Entitäten abrufen können, ist Ihr Datensatz möglicherweise nicht zum Profil aktiviert. Nachdem Sie bestätigt haben, dass Ihr Datensatz aktiviert wurde, stellen Sie sicher, dass Ihr Quelldatenformat und Ihre Identifikatoren Ihre Erwartungen unterstützen.

Detaillierte Anweisungen zum Zugriff auf Entitäten mit der Echtzeit-Customer Profil API finden Sie im [Unterhandbuch zu Entitäten, auch als &quot;Profil Access API&quot;bezeichnet](../api/entities.md).