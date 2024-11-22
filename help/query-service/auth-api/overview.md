---
title: Data Distiller Authorization API-Anleitung
description: Erfahren Sie, wie Sie mit der Data Distiller Authorization-API netzwerkbasierte IP-Einschränkungen für sichere Verbindungen über SQL erzwingen können. Verwenden Sie diese API, um die Kontrolle des Datenzugriffs für Ihre Adobe Experience Platform-Daten zu verbessern.
role: Developer
exl-id: bcc5ea0e-cb6d-4c7b-bf9f-a0336f76c4c8
source-git-commit: 804eeb4ec976cf41fdd450bd8f307499c3ebae03
workflow-type: tm+mt
source-wordcount: '424'
ht-degree: 2%

---

# Data Distiller Authorization API-Anleitung

>[!AVAILABILITY]
>
>Diese Funktion steht Kunden zur Verfügung, die das Data Distiller-Add-on erworben haben. Weitere Informationen erhalten Sie bei Ihrer bzw. Ihrem Adobe-Support-Mitarbeitenden.

Verwenden Sie die Data Distiller Authorization-API, um IP-basierte Einschränkungen zu erzwingen. Durch Anwendung dieser Maßnahmen wird sichergestellt, dass nur zugelassene Netzwerke und Clientcomputer über SQL in Adobe Experience Platform auf Daten zugreifen können. Diese Steuerelemente helfen Ihnen bei der Erfüllung strenger Sicherheitsstandards und bieten gleichzeitig eine Echtzeitüberwachung des Zugriffs und Warnhinweise.

Mit dieser API können Sie IP-Einschränkungen für den Zugriff auf Daten über die SQL-Oberfläche konfigurieren, erzwingen und überwachen. Dieses Dokument bietet einen allgemeinen Überblick über die Kernfunktionen, Endpunktfunktionen und künftigen Funktionen der API.

## Wichtigste Funktionen

Mit den folgenden Funktionen können Sie IP-basierte Zugriffsbeschränkungen definieren, Zugriffsversuche überwachen und Netzwerksicherheitseinstellungen für Query Service anpassen:

- **Definieren Sie netzwerkbasierte Datenzugriffssteuerelemente**: Geben Sie zulässige IP-Bereiche für den Zugriff auf Query Service an. Diese Einschränkung gilt insbesondere für SQL-Datenbankverbindungen, einschließlich solcher, die über Business Intelligence-Tools (BI), Datenbank-Clients oder Programmierschnittstellen wie JDBC hergestellt werden.
- **Umfassende Überwachung und Warnhinweise aktivieren**: Alle Zugriffsversuche, einschließlich verweigerter Verbindungen, werden protokolliert und zur Echtzeitverfolgung an die [Auditprotokolle von Adobe Experience Platform](../../landing/governance-privacy-security/audit-logs/overview.md) gesendet. Mit dieser Funktion können Sie Zugriffsmuster überwachen und potenzielle Sicherheitsverletzungen erkennen.
- **Flexible IP-Einschränkungen konfigurieren**: Geben Sie zulässige IPs sowohl in einzelnen IP- als auch in CIDR-Blockformaten an. Diese Einstellungen gelten pro Sandbox, sodass Sie Netzwerkbeschränkungen an Ihre spezifischen Sicherheitsanforderungen anpassen können.

## Audit- und Überwachungsfunktionen

Um sichere Datenzugriffsmethoden zu unterstützen, protokolliert Query Service alle Client-IPs, die auf Experience Platform zugreifen oder versuchen. Prüfereignisse, einschließlich verweigerter Verbindungen, werden an Platform Audit-Protokolle gesendet. Dies ermöglicht Folgendes:

- **Echtzeit-Überwachung**: Verfolgen Sie IP-basierte Zugriffsmuster, um die Compliance sicherzustellen.
- **Warnung bei nicht autorisiertem Zugriff**: Identifizieren Sie Zugriffsversuche von nicht autorisierten IPs und reagieren Sie darauf.

Weitere Informationen finden Sie in der [Übersicht über Auditprotokolle](../../landing/governance-privacy-security/audit-logs/overview.md) .

## Nächste Schritte

Beginnen Sie mit der Data Distiller Authorization-API, indem Sie sich das [Erste Schritte-Handbuch](./getting-started.md) ansehen, um wichtige Einrichtungsschritte zu erhalten, einschließlich erforderlicher Kopfzeilen und API-Aufrufkonventionen. Konsultieren Sie dann die endpunktspezifischen Handbücher für den [IP-Zugriff](./ip-access.md) und die [IP-Überprüfung](./validate.md) zum Konfigurieren und Verwalten des sicheren Datenzugriffs.

In der Referenzdokumentation für die Data Distiller Authorization OpenAPI](https://developer.adobe.com/experience-platform-apis/references/data-distiller-auth/) finden Sie ein standardisiertes, maschinenlesbares Format für einfachere Integration, Tests und Exploration.[

Informationen zu den verschiedenen Antwortparametern für jeden zurückgegebenen Datensatz finden Sie in der [Entwicklerdokumentation für die Datensatz-API](https://developer.adobe.com/experience-platform-apis/references/catalog/#tag/Datasets/operation/listDatasets) .
