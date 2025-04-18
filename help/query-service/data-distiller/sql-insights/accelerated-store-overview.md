---
title: Accelerated Store - Übersicht
description: Erfahren Sie, wie Sie den beschleunigten Speicher in Adobe Experience Platform für schnelle, SQL-basierte Einblicke mithilfe aggregierter Daten verwenden. Auf dieser Seite werden die vorgesehene Verwendung, Einschränkungen bei Identitäts- und BI-Daten und Best Practices erläutert, um die Einhaltung der Data Governance-Richtlinien von Adobe sicherzustellen.
source-git-commit: 5e8dccf91e8c83b4734b363539cfb911b5c2ae29
workflow-type: tm+mt
source-wordcount: '589'
ht-degree: 1%

---

# Accelerated Store - Übersicht

Der beschleunigte Speicher in Adobe Experience Platform ist eine leistungsoptimierte Speicherschicht, die über die Data Distiller SKU verfügbar ist. Er wurde für die Speicherung voraggregierter Datensätze entwickelt, was ein schnelles, SQL-basiertes Insights- und Dashboard-Rendering ermöglicht.

In diesem Dokument wird beschrieben, wie Sie den beschleunigten Speicher ordnungsgemäß verwenden, warum aggregierte Datensätze von standardmäßigen Datenhygieneprozessen ausgenommen sind und warum Identitätsdaten nicht gespeichert werden dürfen. Um die Adobe-Richtlinien einzuhalten, müssen Sie die in diesem Dokument beschriebenen Data Governance-Richtlinien und Nutzungsbeschränkungen einhalten.

## Wichtigste Funktionen {#key-capabilities}

Der beschleunigte Speicher wurde speziell für Leistung und Effizienz entwickelt. Sie ermöglicht optimierte Abfrage- und Reporting-Workflows, indem sie sich auf aggregierte Daten konzentriert. In der folgenden Liste sind die Kernfunktionen aufgeführt:

- Bereitstellen von leistungsstarken Dashboards und Widgets mithilfe von SQL-Abfragen
- Voraggregierte Datensätze für wiederkehrende Einblicke speichern
- Unterstützung der Erstellung benutzerdefinierter Datenmodelle für Reporting-Anwendungsfälle

## Vorgesehene Verwendung {#intended-use}

Der beschleunigte Speicher dient (**)** Speicherung aggregierter Daten, die ein optimiertes Dashboard und eine optimierte Visualisierung ermöglichen. Seine Architektur ist nicht für komplexe Arbeitslasten wie Business Intelligence-Verarbeitung oder Data Warehousing vorgesehen.

>[!IMPORTANT]
>
>Der beschleunigte Speicher ist kein Ersatz für den Data Lake oder eine allgemeine Speicherlösung.

## Nutzungsbeschränkungen {#usage-restrictions}

Um die Einhaltung des Data Governance-Modells und der Lizenzbedingungen von Adobe sicherzustellen, gelten die folgenden Einschränkungen:

- **Speichern Sie keine Rohereignisdaten**
- **Keine Identitätsdaten speichern**
- **Speichern Sie keine personenbezogenen Daten** E-Mail-Adressen, Gesundheitsdaten oder Kundenkennungen
- **Verwenden Sie den beschleunigten Speicher nicht, um Ihren gesamten Data Lake zu replizieren**

Im beschleunigten Speicher dürfen nur aggregierte, nicht identifizierbare Daten gespeichert werden. Aggregierte Datensätze können nicht so zurückentwickelt werden, dass die ursprünglichen Quelldaten offen gelegt werden, wodurch sie von den zentralisierten Datenhygieneprozessen von Experience Platform ausgenommen sind.

## Governance und Compliance {#governance-and-compliance}

Die Verwendung des beschleunigten Speichers außerhalb des vorgesehenen Zwecks kann Ihr Unternehmen dem Risiko aussetzen, gegen die Lizenzvereinbarung und die Data Governance-Grenzen von Adobe zu verstoßen. Wenn Data Governance-Vorfälle aufgrund von nicht unterstützten Nutzungsmustern auftreten, übernimmt Ihr Unternehmen die volle Verantwortung.

Adobe übernimmt keine Haftung für Folgen, die sich aus der missbräuchlichen Verwendung dieser Funktion ergeben.

Weitere Informationen zum verantwortungsvollen Verwalten von Daten in Experience Platform finden Sie unter [Governance, Datenschutz und Sicherheit in Experience Platform](../../../landing/governance-privacy-security/overview.md). Auf dieser Seite werden die Services und Tools beschrieben, mit denen Sie Ihre Erlebnisdaten in Übereinstimmung mit Geschäftsrichtlinien, rechtlichen Anforderungen und Entwicklungsstandards steuern können. Links zu detaillierteren Anleitungen zu Nutzungskennzeichnungen und zur Durchsetzung von Richtlinien finden Sie in der [Übersicht zu Data Governance](../../../data-governance/home.md).

## Best Practices {#best-practices}

Befolgen Sie die folgenden empfohlenen Best Practices, um eine effiziente und konforme Nutzung des beschleunigten Speichers sicherzustellen:

- Verwenden Sie abgeleitete Datensätze, um voraggregierte Tabellen zu erstellen, die speziell auf Ihre Dashboard-Anforderungen zugeschnitten sind
- Verwenden Sie den beschleunigten Speicher nicht als Staging- oder Backup-Speicherort für Rohdatensätze
- Überprüfen Sie Ihre Verwendung regelmäßig, um sicherzustellen, dass sie mit den von Adobe empfohlenen Leitplanken übereinstimmt.

## Nächste Schritte

Durch dieses Dokument haben Sie gelernt, was der beschleunigte Speicher ist, wie er für aggregierte Daten in Reporting-Szenarien verwendet werden soll und welche Governance-Regeln befolgt werden müssen, um eine konforme Nutzung sicherzustellen. Um Ihr Verständnis zu vertiefen und diese Richtlinien effektiv anzuwenden, erkunden Sie die folgenden Ressourcen:

- [SQL Insights - Übersicht](./overview.md): Erfahren Sie, wie SQL Insights leistungsoptimiertes Reporting mithilfe aggregierter Datensätze ermöglicht.
- [Beschleunigte Abfragen senden](./send-accelerated-queries.md): Erfahren Sie, wie Sie Abfragen für den beschleunigten Speicher ausführen, um Dashboards und Widgets zu unterstützen.
- [Data Governance und Datenhygiene](../../data-governance/overview.md): Überprüfen Sie die Datenhygiene-Richtlinien und Governance von Adobe, um eine konforme Nutzung sicherzustellen.
