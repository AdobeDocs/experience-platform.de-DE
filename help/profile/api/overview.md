---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Entwicklerhandbuch für Customer Profil-API in Echtzeit
topic: guide
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '666'
ht-degree: 0%

---


# Entwicklerhandbuch für Customer Profil-API in Echtzeit

Echtzeit-Kundendaten ermöglichen es Ihnen, eine ganzheitliche Ansicht Ihrer einzelnen Kunden in der Adobe Experience Platform zu sehen. Mit Profil können Sie unterschiedliche Kundendaten aus mehreren Kanälen, z. B. Online-, Offline-, CRM- und Drittanbieter-Daten, in einer einheitlichen Ansicht zusammenfassen, die eine umsetzbare Zeitstempel-Übersicht über jede Kundeninteraktion bietet.

Die Echtzeit-Kunden-Profil-API enthält mehrere Endpunkte, die nachfolgend beschrieben werden. Weitere Informationen zu erforderlichen Kopfzeilen, zum Lesen von Beispiel-API-Aufrufen und mehr finden Sie in den einzelnen Endpunkthandbüchern. Weitere Informationen finden Sie im Handbuch [Erste Schritte](getting-started.md) .

Informationen zur Ansicht aller verfügbaren Endpunkte und CRUD-Vorgänge finden Sie im [Echtzeit-Client-Profil-API-Referenzswagger](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml).

## (Alpha) Berechnete Attribute

>[!IMPORTANT]
>
>
>Die Funktion für berechnete Attribute ist alphanumerisch und steht nicht allen Benutzern zur Verfügung. Dokumentation und Funktionalität können geändert werden.

Berechnete Attribute ermöglichen es Ihnen, den Feldwert anhand anderer Werte, Berechnungen und Ausdruck automatisch zu berechnen. Berechnete Attribute werden auf Profil-Ebene ausgeführt, d. h., Sie können Werte über alle Datensätze und Ereignis hinweg Aggregat haben. Jedes berechnete Attribut enthält einen Ausdruck, oder &quot;Regel&quot;, der eingehende Daten auswertet und den sich ergebenden Wert in einem Profil-Attribut oder in einem Ereignis speichert. Diese Berechnungen helfen Ihnen, Fragen im Zusammenhang mit dem Kaufwert über die gesamte Lebensdauer, der Zeit zwischen Käufen oder der Anzahl der Anwendungen einfach zu beantworten, ohne dass Sie bei jeder erforderlichen Information manuell komplexe Berechnungen durchführen müssen. Sie können berechnete Attribute mithilfe des `config/computedAttributes` Endpunkts erstellen, Ansichten vornehmen, bearbeiten und löschen. Informationen zur Verwendung dieses Endpunkts finden Sie im Handbuch [zum Endpunkt berechneter Attribute](computed-attributes.md).

## Edge-Prognosen

Adobe Experience Platform ermöglicht eine Echtzeit-Personalisierung von Kundenerlebnissen, indem Daten auf strategisch wichtigen Servern, so genannte &quot;Kanten&quot;, leicht zugänglich gemacht werden. Die Echtzeit-Client-Profil-API bietet Endpunkte zum Arbeiten mit Kanten über Komponenten, die als &quot;Projektionen&quot;bezeichnet werden. Dazu gehören Projektionskonfigurationen, um zu bestimmen, welche Daten auf die einzelnen Kanten projiziert werden sollen, sowie Projektionsziele, um zu definieren, wo eine Projektion weitergeleitet werden soll. Detaillierte Informationen zum Arbeiten mit Kantenprojektionen finden Sie im Handbuch [Projektionskonfigurationen und Zielendpunkte](edge-projections.md).

## Entitäten

Durch Adobe Experience Platform können Sie über RESTful-APIs oder die Benutzeroberfläche auf Echtzeit-Daten zum Profil von Kunden zugreifen. Um zu erfahren, wie Sie mithilfe der API auf Entitäten zugreifen können, die allgemein als &quot;Profil&quot;bezeichnet werden, führen Sie die Schritte aus, die im [Entitäts-Endpunkthandbuch](entities.md)beschrieben sind. Informationen zum Zugriff auf Profil über die Benutzeroberfläche der Platform finden Sie im [Profil-Benutzerhandbuch](../ui/user-guide.md).

## Zusammenführungsrichtlinien

Beim Zusammenführen von Daten aus mehreren Quellen in die Experience Platform sind Zusammenführungsrichtlinien die Regeln, die Platform verwendet, um zu bestimmen, wie Daten priorisiert werden und welche Daten kombiniert werden, um individuelle Profil zu erstellen. Mit der Echtzeit-Client-Profil-API können Sie neue Zusammenführungsrichtlinien erstellen, vorhandene Richtlinien verwalten und eine standardmäßige Zusammenführungsrichtlinie für Ihr Unternehmen festlegen. Weitere Informationen zum Arbeiten mit Zusammenführungsrichtlinien mithilfe der API finden Sie im Endpunkthandbuch zu [Zusammenführungsrichtlinien](merge-policies.md).

Eine Anleitung zum Arbeiten mit Zusammenführungsrichtlinien mithilfe der Benutzeroberfläche &quot;Platform&quot;finden Sie im Benutzerhandbuch [](../ui/merge-policies.md)&quot;Richtlinien zusammenführen&quot;.

## Profil-Systemaufträge

Daten, die in die Platform aufgenommen werden, werden im Data Lake sowie im Echtzeit-Kundendatenspeicher gespeichert. Gelegentlich kann es erforderlich sein, einen Datensatz oder Stapel aus dem Profil-Store zu löschen, um Daten zu entfernen, die Sie nicht mehr benötigen oder die fälschlicherweise hinzugefügt wurden. Dies erfordert die Verwendung der API zum Erstellen eines Profil-Systemauftrags, der als &quot;Löschanforderung&quot;bezeichnet wird und bei Bedarf auch bearbeitet, überwacht oder gelöscht werden kann. Um zu erfahren, wie Sie mit dem `/system/jobs` Endpunkt in der Echtzeit-Client-Profil-API mit Löschanforderungen arbeiten, führen Sie die Schritte aus, die im [Profil-Endpunkthandbuch](profile-system-jobs.md)für Systemaufträge beschrieben sind.

## Nächste Schritte

Um mit dem Aufrufen mit der Echtzeit-Client-Profil-API zu beginnen, lesen Sie die [Erste Schritte-Anleitung](getting-started.md) und wählen Sie dann eine der Endpunktanleitungen, um zu erfahren, wie Sie bestimmte Profil-bezogene Endpunkte verwenden. Weitere Informationen zum Arbeiten mit Profil-Daten über die Benutzeroberfläche der Platform finden Sie im Benutzerhandbuch [zum](../ui/user-guide.md)Echtzeit-Kundendienstprogramm.