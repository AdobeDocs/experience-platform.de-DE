---
title: Handbuch zur Autorisierungs-API für Query Service
description: Erfahren Sie, wie Sie mit der Autorisierungs-API von Query Service netzwerkbasierte IP-Einschränkungen für sichere Verbindungen über SQL erzwingen können. Verwenden Sie diese API, um die Kontrolle des Datenzugriffs für Ihre Adobe Experience Platform-Daten zu verbessern.
role: Developer
source-git-commit: f673d0d71458fe87491318f06be59719e4c9d76c
workflow-type: tm+mt
source-wordcount: '365'
ht-degree: 1%

---

# Handbuch zur Autorisierungs-API für Query Service

Verwenden Sie die Autorisierungs-API von Query Service, um IP-basierte Einschränkungen zu erzwingen. Durch Anwendung dieser Maßnahmen wird sichergestellt, dass nur zugelassene Netzwerke und Clientcomputer über SQL in Adobe Experience Platform auf Daten zugreifen können. Diese Steuerelemente helfen Ihnen bei der Erfüllung strenger Sicherheitsstandards und bieten gleichzeitig eine Echtzeitüberwachung des Zugriffs und Warnhinweise.

Mit dieser API können Sie IP-Einschränkungen für den Zugriff auf Daten über die SQL-Oberfläche konfigurieren, erzwingen und überwachen. Dieses Dokument bietet einen allgemeinen Überblick über die Kernfunktionen, Endpunktfunktionen und künftigen Funktionen der API.

## Wichtigste Funktionen

Mit den folgenden Funktionen können Sie IP-basierte Zugriffsbeschränkungen definieren, Zugriffsversuche überwachen und Netzwerksicherheitseinstellungen für Query Service anpassen:

- **Definieren Sie netzwerkbasierte Datenzugriffssteuerelemente**: Geben Sie zulässige IP-Bereiche für den Zugriff auf Query Service an. Diese Einschränkung gilt insbesondere für SQL-Datenbankverbindungen, einschließlich solcher, die über Business Intelligence-Tools (BI), Datenbank-Clients oder Programmierschnittstellen wie JDBC hergestellt werden.
- **Umfassende Überwachung und Warnhinweise aktivieren**: Alle Zugriffsversuche, einschließlich verweigerter Verbindungen, werden protokolliert und zur Echtzeitverfolgung an die [Auditprotokolle von Adobe Experience Platform](../../landing/governance-privacy-security/audit-logs/overview.md) gesendet. Mit dieser Funktion können Sie Zugriffsmuster überwachen und potenzielle Sicherheitsverletzungen erkennen.
- **Flexible IP-Einschränkungen konfigurieren**: Geben Sie zulässige IPs sowohl in einzelnen IP- als auch in CIDR-Blockformaten an. Diese Einstellungen gelten pro Sandbox, sodass Sie Netzwerkbeschränkungen an Ihre spezifischen Sicherheitsanforderungen anpassen können.

## Audit- und Überwachungsfunktionen

Um sichere Datenzugriffsmethoden zu unterstützen, protokolliert Query Service alle Client-IPs, die auf AEP zugreifen oder versuchen, darauf zuzugreifen. Prüfereignisse, einschließlich verweigerter Verbindungen, werden an Platform Audit-Protokolle gesendet. Dies ermöglicht Folgendes:

- **Echtzeit-Überwachung**: Verfolgen Sie IP-basierte Zugriffsmuster, um die Compliance sicherzustellen.
- **Warnung bei nicht autorisiertem Zugriff**: Identifizieren Sie Zugriffsversuche von nicht autorisierten IPs und reagieren Sie darauf.

Weitere Informationen zur Auditprotokollierung finden Sie in der Dokumentation zum [Auditdienst](https://experienceleague.adobe.com/docs/experience-platform/audit/audit-overview.html).

## Nächste Schritte

Beginnen Sie mit der Autorisierungs-API von Query Service, indem Sie sich das [Erste Schritte-Handbuch](./getting-started.md) ansehen, um wichtige Einrichtungsschritte zu erhalten, einschließlich erforderlicher Kopfzeilen und API-Aufrufkonventionen. Konsultieren Sie dann die endpunktspezifischen Handbücher für den [IP-Zugriff](./ip-access.md) und die [IP-Überprüfung](./validate.md) zum Konfigurieren und Verwalten des sicheren Datenzugriffs.
