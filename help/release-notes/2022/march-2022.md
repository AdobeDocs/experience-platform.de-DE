---
title: Adobe Experience Platform – Versionshinweise
description: Die neuesten Versionshinweise für Adobe Experience Platform.
source-git-commit: 7145867795bcd8e1093c09df3fefdee518f9578a
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 50%

---

# Adobe Experience Platform – Versionshinweise

**Veröffentlichungsdatum: 30. März 2022**

Neue Funktionen in Adobe Experience Platform:

- [[!DNL Audit Logs]](#audit-logs)

Aktualisierungen vorhandener Funktionen in Adobe Experience Platform:

- [Warnhinweise](#alerts)
- [Quellen](#sources)

## [!DNL Audit Logs] {#audit-logs}

Mit Experience Platform können Sie die Benutzeraktivität für verschiedene Dienste und Funktionen überprüfen. Die Prüfprotokolle enthalten Informationen darüber, wer wann was getan hat.

**Neue Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Prüfprotokolle für Datensatz, Schema, Klasse, Feldergruppe, Datentyp, Sandbox, Ziel, Segment, Zusammenführungsrichtlinie, berechnetes Attribut, Produktprofil und Konto (Adobe) | Dies sind die Ressourcen, die von Prüfprotokollen aufgezeichnet werden. Wenn die Funktion aktiviert ist, werden die Prüfprotokolle automatisch erfasst, sobald eine Aktivität stattfindet. Sie müssen die Protokollerfassung nicht manuell aktivieren. |
| Audit-Protokolle exportieren | Die Prüfprotokolle können als `CSV` oder `JSON` -Datei. Die erzeugten Dateien werden direkt auf Ihrem Computer gespeichert. |

Weiterführende Informationen zu Auditprotokollen in Platform finden Sie im Abschnitt [Übersicht über Auditprotokolle](../../landing/governance-privacy-security/audit-logs/overview.md).

## Warnhinweise {#alerts}

Mit Experience Platform können Sie ereignisbasierte Warnhinweise zu Adobe Experience Platform-Aktivitäten abonnieren. Sie können unterschiedliche Warnhinweisregeln über die Registerkarte [!UICONTROL Warnhinweise] in der Platform-Benutzeroberfläche abonnieren. Zusätzlch können Sie auswählen, ob Warnhinweise in der Benutzeroberfläche oder über E-Mail-Benachrichtigungen angezeigt werden sollen.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Neue Warnhinweisregeln | Für Quellen, die mit der Datenerfassung in Verbindung stehen, stehen nun zwei neue Warnhinweisregeln zur Verfügung. Die aktualisierte Liste der Warnhinweistypen finden Sie in der Übersicht zu [Warnhinweisregeln](../../observability/alerts/rules.md). |

Weitere Informationen zu Warnhinweisen in Platform finden Sie im Abschnitt [Warnhinweise – Übersicht](../../observability/alerts/overview.md).

## Quellen {#sources}

Mit Adobe Experience Platform können Sie Daten aus externen Quellen erfassen und diese Daten mithilfe von Platform-Diensten strukturieren, kennzeichnen und verbessern. Daten können Sie aus verschiedenen Quellen erfassen, z. B. aus Adobe-Anwendungen, Cloud-basiertem Speicher, Software von Drittanbietern und Ihrem CRM-System.

Im Rahmen von Experience Platform stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Neue Quellen für die B2B-Nutzung verfügbar | Sie können jetzt alle verfügbaren Quellen in Platform für B2B-Anwendungsfälle verwenden. Siehe [Quellkatalog](../../sources/home.md) für eine vollständige Liste der verfügbaren Quellen. |
| Allgemeine Verfügbarkeit neuer [!DNL Oracle Eloqua] source | Sie können jetzt die [!DNL Oracle Eloqua] -Quelle, um Daten aus Ihrem [!DNL Oracle Eloqua] -Instanz (Konto, Kampagne, Kontakte) zu Platform. Weitere Informationen finden Sie in der Dokumentation unter [Erstellen einer [!DNL Oracle Eloqua] Quellverbindung](../../sources/connectors/oracle-eloqua.md) für weitere Informationen. |
| API-Verbesserungen für [!DNL Data Landing Zone] | Die [!DNL Data Landing Zone] -Quelle unterstützt jetzt die automatische Erkennung von Dateieigenschaften bei Verwendung der [!DNL Flow Service] API. Weitere Informationen finden Sie in der Dokumentation unter [Erstellen einer [!DNL Data Landing Zone] Quellverbindung](../../sources/tutorials/api/create/cloud-storage/data-landing-zone.md) für weitere Informationen. |

Weitere Informationen zu Quellen finden Sie in der [Quellen – Übersicht](../../sources/home.md).
