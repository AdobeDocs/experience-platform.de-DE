---
title: Data Distiller Authorization API-Handbuch
description: Erfahren Sie, wie Sie mit der Data Distiller-Autorisierungs-API netzwerkbasierte IP-Einschränkungen für sichere Verbindungen über SQL erzwingen können. Verwenden Sie diese API, um die Datenzugriffssteuerung für Ihre Adobe Experience Platform-Daten zu verbessern.
role: Developer
exl-id: bcc5ea0e-cb6d-4c7b-bf9f-a0336f76c4c8
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 2%

---

# Data Distiller Authorization API-Handbuch

>[!AVAILABILITY]
>
>Diese Funktion steht Kunden zur Verfügung, die das Add-on Data Distiller erworben haben. Weitere Informationen erhalten Sie beim Adobe-Support.

Verwenden Sie die Data Distiller-Autorisierungs-API , um IP-basierte Einschränkungen zu erzwingen. Durch die Anwendung dieser Maßnahmen wird sichergestellt, dass nur genehmigte Netzwerke und Client-Computer über SQL in Adobe Experience Platform auf Daten zugreifen können. Diese Steuerelemente helfen Ihnen bei der Einhaltung strenger Sicherheitsstandards und bieten gleichzeitig Echtzeit-Zugriffsüberwachung und -Warnmeldungen.

Mit dieser API können Sie IP-Einschränkungen für den Zugriff auf Daten über die SQL-Schnittstelle konfigurieren, durchsetzen und überwachen. Dieses Dokument bietet einen allgemeinen Überblick über die Kernfunktionen, Endpunktfunktionen und zukünftigen Funktionen der API.

## Wichtigste Funktionen

Mit den folgenden Funktionen können Sie IP-basierte Zugriffsbeschränkungen definieren, Zugriffsversuche überwachen und die Netzwerksicherheitseinstellungen für den Abfrage-Service anpassen:

- **Netzwerkbasierte Datenzugriffssteuerungen definieren**: Geben Sie zulässige IP-Bereiche für den Zugriff auf den Abfrage-Service an. Diese Einschränkung gilt speziell für SQL-Datenbankverbindungen, einschließlich solcher, die über Business Intelligence (BI)-Tools, Datenbank-Clients oder Programmierschnittstellen wie JDBC hergestellt werden.
- **Umfassende Überwachung und Warnhinweise aktivieren**: Alle Zugriffsversuche, einschließlich verweigerter Verbindungen, werden protokolliert und zur Echtzeit-[&#128279;](../../landing/governance-privacy-security/audit-logs/overview.md) an die Adobe Experience Platform-Auditprotokolle gesendet. Verwenden Sie diese Funktion, um Zugriffsmuster zu überwachen und potenzielle Sicherheitsverletzungen zu erkennen.
- **Flexible IP-Einschränkungen konfigurieren**: Geben Sie die zulässigen IPs sowohl im individuellen IP- als auch im CIDR-Blockformat an. Diese Einstellungen gelten pro Sandbox, sodass Sie Netzwerkbeschränkungen an Ihre spezifischen Sicherheitsanforderungen anpassen können.

## Audit- und Überwachungsfunktionen

Um sichere Datenzugriffspraktiken zu unterstützen, protokolliert der Abfrage-Service alle Client-IPs, die auf Experience Platform zugreifen oder versuchen, darauf zuzugreifen. Audit-Ereignisse, einschließlich verweigerter Verbindungen, werden an Experience Platform-Audit-Protokolle gesendet. Dies ermöglicht Folgendes:

- **Echtzeit-Überwachung**: Verfolgen Sie IP-basierte Zugriffsmuster, um die Einhaltung sicherzustellen.
- **Benachrichtigung bei nicht autorisiertem Zugriff**: Identifizieren Sie Zugriffsversuche von nicht autorisierten IPs und reagieren Sie darauf.

Weitere Informationen finden Sie [ „Übersicht ](../../landing/governance-privacy-security/audit-logs/overview.md) Auditprotokolle“.

## Nächste Schritte

Um mit der Data Distiller-Autorisierungs-API zu beginnen, lesen Sie das [Erste Schritte](./getting-started.md), um wichtige Einrichtungsschritte zu erfahren, einschließlich erforderlicher Kopfzeilen und API-Aufrufkonventionen. Anschließend finden Sie in den endpunktspezifischen Handbüchern unter [IP-Zugriff](./ip-access.md) und [IP-Validierung](./validate.md) zum Konfigurieren und Verwalten des sicheren Datenzugriffs.

Siehe die [OpenAPI-Referenzdokumentation zur Data Distiller-Autorisierung](https://developer.adobe.com/experience-platform-apis/references/data-distiller-auth/), um ein standardisiertes, maschinenlesbares Format für eine einfachere Integration, Tests und Untersuchung anzuzeigen.

Informationen zu den verschiedenen Antwortparametern für jeden zurückgegebenen Datensatz finden Sie in der Entwicklerdokumentation [Datasets-API](https://developer.adobe.com/experience-platform-apis/references/catalog/#tag/Datasets/operation/listDatasets).
