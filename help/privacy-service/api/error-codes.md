---
title: Privacy Service-Fehlercodes in Adobe Experience Platform
description: Machen Sie sich mit den Privacy Service-Fehlercodes vertraut, damit Sie Fehler diagnostizieren, Auftragsergebnisse programmgesteuert verarbeiten und die nächsten Schritte beim Senden oder Überwachen von Datenschutzaufträgen bestimmen können.
keywords: Privacy Service, Fehler-Codes, Datenschutzaufträge, API-Fehler
solution: Experience Platform
source-git-commit: a312dabf5b8c3b52af31e2e127cd4bbeb8dd0021
workflow-type: tm+mt
source-wordcount: '826'
ht-degree: 5%

---

# Privacy Service-Fehlercodes {#privacy-service-error-codes}

Verwenden Sie diese Referenz, um die Ergebnisse von Privacy Service-Vorgängen zu identifizieren, Fehler zu diagnostizieren und die nächsten Schritte beim Senden oder Überwachen von Datenschutzvorgängen in **Adobe Experience Platform** zu bestimmen. Informationen zum Erstellen, Senden und Überwachen von Datenschutzaufträgen finden Sie im [Handbuch zu Datenschutzaufträgen](./privacy-jobs.md) oder im [Benutzerhandbuch für die Privacy Service-Benutzeroberfläche](../ui/user-guide.md).

Privacy Service-Fehlercodes sind ein stabiler öffentlicher Auftrag. Jeder Fehler-Code identifiziert eindeutig einen Fehler- oder Abschlussstatus, auf den Sie sich für die programmgesteuerte Handhabung und operative Workflows verlassen können.

Die folgenden Garantien gelten für die Erstellung von Automatisierungs- oder Überwachungs-Workflows:

* Fehler-Codes sind nach der Veröffentlichung stabil.
* Fehlermeldungen können sich ändern, um die Klarheit zu verbessern, der Code-Wert jedoch nicht.
* Im Laufe der Zeit können neue Fehler-Codes hinzugefügt werden. Vorhandene Codes werden nicht neu verwendet.

Verwenden Sie Fehler-Codes, nicht Nachrichtentext, um Automatisierung oder Entscheidungslogik zu implementieren. Anleitungen zur effizienten Verarbeitung von Datenschutzaufträgen, zur Überwachung des Auftragsstatus und zur Fehlerbehandlung ohne Verwendung von Abruf- oder Nachrichtenzeichenfolgen finden Sie unter [Best Practices für Privacy Service](../best-practices.md).

## Format der Fehlerantwort {#error-response-format}

Privacy Service gibt Fehlerinformationen in Auftrags- und Anfrageantworten zurück. Die Antwort enthält einen numerischen Fehlercode und eine für Menschen lesbare Nachricht in der Antwort-Payload.

Der Fehlercode gibt das maßgebliche Ergebnis an. Die Meldung bietet zusätzlichen Kontext zur Fehlerbehebung.

In diesem Dokument werden die Bedeutung und der Zweck jedes Fehler-Codes beschrieben. Informationen zu Antwortschemata auf Feldebene und Anfragedetails finden Sie in der [Privacy Service-API-Dokumentation](https://developer.adobe.com/experience-platform-apis/references/privacy-service/).

## Fehler-Domains {#error-domains}

Die Fehler-Codes werden nach Funktions-Domain gruppiert, damit Sie Probleme schneller diagnostizieren können.

Zu den in diesem Dokument verwendeten Domains gehören:

* **Anfragevalidierung**: Die Anfrage ist fehlerhaft oder enthält ungültige Werte. Informationen zur Anfragestruktur [&#x200B; den Validierungsanforderungen finden Sie &#x200B;](./privacy-jobs.md) Handbuch für Datenschutzaufträge .
* **Autorisierung und Bereitstellung**: Ihr Unternehmen oder Ihre Benutzerin bzw. Ihr Benutzer hat nicht den erforderlichen Zugriff. Siehe [Verwalten von Berechtigungen](../permissions.md), um die rollenbasierten Berechtigungsanforderungen zu überprüfen.
* **Identität und Anwendbarkeit**: Kennungen oder Namespaces können nicht auf die Anfrage angewendet werden. Unter [Identitätsdaten für Datenschutzanfragen](../identity-data.md) finden Sie Informationen zu unterstützten Identitätstypen und Namespace-Anforderungen.
* **Ratenbegrenzung**: Das Übermittlungsvolumen überschreitet die Plattformbegrenzungen. Reduzieren Sie bei diesem Fehler die Übermittlungsrate und versuchen Sie es erneut.
* **Datenzugriff und -verarbeitung**: Das System kann nicht auf die angeforderten Daten zugreifen oder sie verarbeiten. Häufige [&#x200B; und Schritte zur Behebung &#x200B;](../troubleshooting-guide.md) Probleme finden Sie im Handbuch zur Fehlerbehebung .
* **Verschlüsselung und Schlüsselverwaltung**: Erforderliche Verschlüsselungsschlüssel sind nicht verfügbar. Siehe [Vom Kunden verwaltete Schlüssel](../../landing/governance-privacy-security/customer-managed-keys/overview.md) für Anleitungen zu Schlüsselzugriff, Konfiguration und Wiederherstellung.
* **Auftragsausführungsstatus**: Der Auftrag wurde vollständig, teilweise oder mit Fehlern abgeschlossen. Beschreibungen [&#x200B; Auftragsstatuskategorien und deren Bedeutungen finden Sie im &#x200B;](./privacy-jobs.md#status-categories)Handbuch für Datenschutzaufträge“.

>[!NOTE]
>
>Domain-Zuweisungen spiegeln den Zweck des Fehler-Codes wider, nicht interne Service-Grenzen.

## Fehlercode-Referenz {#error-code-reference}

In der folgenden Tabelle sind alle öffentlichen Privacy Service-Fehler-Codes aufgeführt.

| Fehler-Code | HTTP-Status | Titel | Beschreibung |
| ---------- | ----------- | ----------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------| 
| 1000-400 | 400 | Formatierungsfehler | Mindestens ein Datenwert für das angegebene Programm weist Formatierungsprobleme auf. Weitere Informationen finden Sie in den Auftragsdetails. |
| 1001-400 | 400 | Nicht autorisiert | Ihre Organisation wurde nicht bereitgestellt. Weitere Informationen erhalten Sie von Ihrem Administrator. |
| 1010-400 | 400 | Fehlende Berechtigungen | Sie verfügen nicht über die erforderlichen Berechtigungen, um diese Aktion durchzuführen. Wenden Sie sich an Ihren Administrator, um Zugriff anzufordern. |
| 1020-400 | 400 | Fehler beim Hochladen und Archivieren | Beim Hochladen und Archivieren der Zugriffsdaten ist ein Problem aufgetreten. Laden Sie die Zugriffsdaten hoch und versuchen Sie es erneut. |
| 1021-400 | 400 | Fehlgeschlagener Job | Mindestens ein aus der Anfrage erstellter Datenschutzvorgang ist fehlgeschlagen. Überprüfen Sie die Details der fehlgeschlagenen Aufträge, um weitere Informationen zu erhalten. |
| 1022-400 | 400 | Fehler bei Datenzugriff | Beim Zugriff auf die angegebenen Daten ist ein Problem aufgetreten. Weitere Informationen finden Sie in den Auftragsdetails. |
| 1023-400 | 400 | Fehler bei Datenzugriff | Beim Zugriff auf die angegebenen Datensatz-IDs oder deren Suche ist ein Problem aufgetreten. Überprüfen Sie, ob die angegebenen IDs gültig sind, und versuchen Sie es dann erneut. |
| 1024-400 | 400 | Unerwarteter Fehler | Es ist ein unerwarteter Fehler aufgetreten. Weitere Informationen finden Sie in den Auftragsdetails. |
| 1030-400 | 400 | Limit der Dokumentrate überschritten | Die Arbeitslast hat das Limit der Dokumentrate überschritten. Verringern Sie Ihre Übermittlungsrate und versuchen Sie es erneut. |
| 1040-400 | 400 | Fehler bei Verschlüsselungszugriff auf Schlüssel | Die Daten konnten nicht verarbeitet werden, da der Datenspeicher verschlüsselt ist und der Schlüsselzugriff widerrufen wurde. Wenden Sie sich an Ihren Schlüsseltresoradministrator, um den Zugriff auf den Kundenschlüssel wiederherzustellen. |
| 6.000-200 | 200 | Erfolgreich | Der Vorgang wurde erfolgreich abgeschlossen. Überprüfen Sie die Auftragsdetails, um verarbeitete Datensätze und Ergebnisse zu bestätigen. |
| 6 051-200 | 200 | Nicht bereitgestellt | Ihre Organisation ist nicht für das angeforderte Programm vorgesehen. Die Anfrage ist nicht anwendbar. |
| 6 052-200 | 200 | Benutzer-IDs nicht gefunden | Einige Benutzer-IDs wurden nicht gefunden, und unbekannte Benutzer-IDs sind für dieses Produkt nicht anwendbar. Stellen Sie sicher, dass die Benutzer-IDs gültig sind, und versuchen Sie es dann erneut. |
| 6 053-200 | 200 | Ungültiger Namespace | Der angegebene Identity-Namespace ist für diese Anwendung nicht gültig. Verwenden Sie einen vom System erkannten Namespace. |
| 6 054-200 | 200 | Teilweise abgeschlossen | Der Vorgang wurde für die entsprechenden Daten abgeschlossen, aber einige Daten waren nicht auf die Anfrage anwendbar. Weitere Informationen finden Sie in den Auftragsdetails. |

{style="table-layout:auto"}
