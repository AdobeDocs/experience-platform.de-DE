---
keywords: Experience Platform;Startseite;beliebte Themen
solution: Experience Platform
title: Versionshinweise zu Privacy Service
topic-legacy: release notes
description: Die aktuellen Versionshinweise für Adobe Experience Platform Privacy Service.
exl-id: 66ee38f1-f0d5-44ff-823d-d1b8a9765c6d
source-git-commit: dc81da58594fac4ce304f9d030f2106f0c3de271
workflow-type: tm+mt
source-wordcount: '553'
ht-degree: 51%

---

# [!DNL Privacy Service] Versionshinweise

Dieses Dokument enthält Informationen zu neuen Funktionen für Adobe Experience Platform [!DNL Privacy Service], sowie Verbesserungen und wichtige Fehlerbehebungen.

>[!NOTE]
>
>Die neuesten Versionshinweise für andere [!DNL Experience Platform] Dienste finden Sie [here](../release-notes/latest/latest.md).

## 9. September 2020

### Neue Funktionen

| Funktion | Beschreibung |
| --- | --- |
| Unterstützung für LGPD (Brasilien) | Datenschutzaufträge können jetzt im Rahmen der [!DNL Lei Geral de Proteção de Dados] Verordnung (LGPD). Diese Aufträge werden unter dem Regelungscode nachverfolgt `lgpd_bra`. |

## 8. April 2020

### Neue Funktionen

| Funktion | Beschreibung |
| --- | --- |
| Unterstützung für PDPA | [!DNL Privacy] -Anfragen können jetzt im Rahmen des Datenschutzgesetzes (PDPA) in Thailand erstellt und verfolgt werden. Bei Datenschutzanfragen in der API akzeptiert das `regulation`-Array nun den Wert „pdpa_tha“. |
| Namespace-Typen in der Benutzeroberfläche | Sie können jetzt verschiedene Namespace-Typen im Anforderungs-Builder im [!DNL Privacy Service] Benutzeroberfläche. Weiterführende Informationen dazu finden Sie im [Benutzerhandbuch](ui/user-guide.md). |
| Einstellung des alten Endpunkts | Der alte API-Endpunkt (`data/privacy/gdpr`) wird nicht mehr unterstützt. |

## Dienstag, 14. Januar 2020

### Neue Funktionen

| Funktion | Beschreibung |
| --- | --- |
| [!DNL Privacy Service] Rebranding | Der zuvor als &quot;DSGVO-Dienst&quot;bezeichnete Dienst wurde in [!DNL Privacy Service] da der Dienst zunehmend andere Vorschriften zusätzlich zur DSGVO unterstützt. |
| Neue API-Endpunkte | Basispfad für [!DNL Privacy Service] Die API wurde aktualisiert von `/data/privacy/gdpr` nach `/data/core/privacy/jobs` |
| Neue erforderliche `regulation`-Eigenschaft | Beim Erstellen neuer Aufträge in [!DNL Privacy Service] API, eine `regulation` -Eigenschaft muss in der Anfrage-Payload angegeben werden, unter welcher Verordnung der Auftrag verfolgt werden soll. Die zulässigen Werte sind `gdpr` und `ccpa`. Siehe Dokument unter [Datenschutzaufträge](api/privacy-jobs.md) im [!DNL Privacy Service] API-Handbuch für weitere Informationen. |
| Unterstützung für die Adobe Primetime-Authentifizierung | [!DNL Privacy Service] akzeptiert jetzt Zugriffs-/Löschanfragen von der Adobe Primetime-Authentifizierung, wobei `primetimeAuthentication` als Produktwert verwendet wird. Weitere Informationen finden Sie in der [Dokumentation für die Primetime-Authentifizierung](https://tve.helpdocsonline.com/how-to-make-a-privacy-request). |

### Verbesserungen

* [!DNL Privacy Service] Verbesserungen der Benutzeroberfläche:
   * Separate Auftragsverfolgungsseiten für DSGVO- und CCPA-Vorschriften.
   * Neue Dropdown-Liste *Vorschriftentyp*, um zwischen den Verfolgungsdaten für DSGVO und CCPA zu wechseln.

## Donnerstag, 25. Juli 2019

### Neue Funktionen

| Funktion | Beschreibung |
| --- | --- |
| Dashboard „Anfragemetriken“ | Das Dashboard der neuen Metriken im [!DNL Privacy Service] Die Benutzeroberfläche bietet Einblicke in gesendete, fehlerhafte und abgeschlossene DSGVO-Anfragen. |
| Request Builder | Um Unternehmen mit technischen und nicht-technischen Benutzern, die DSGVO-Anfragen senden, zu unterstützen, wurde der Benutzeroberfläche eine Funktion zum Erstellen einer Anfrage hinzugefügt. Die JSON-Dateisendefunktion ist weiterhin im [!DNL Privacy Service] Benutzeroberfläche für Organisationen, die sie weiterhin verwenden möchten. |
| Ereignisbenachrichtigungen für DSGVO-Aufträge | Ereignisbenachrichtigungen über den DSGVO-Auftragsstatus sind für viele Workflows von entscheidender Bedeutung. Während Benachrichtigungen bisher über individuelle E-Mail-Benachrichtigungen zugestellt wurden, handelt es sich bei DSGVO-Ereignisbenachrichtigungen um Nachrichten, die Adobe I/O-Ereignisse nutzen und an einen konfigurierten Webhook gesendet werden, der die Automatisierung von Auftragsanfragen erleichtert. [!DNL Privacy Service] Benutzer der Benutzeroberfläche können DSGVO-Ereignisse der Adobe I/O abonnieren, um Updates zu erhalten, wenn ein Produkt oder der DSGVO-Auftrag abgeschlossen wurde. |

## Donnerstag, 18. April 2019

### Verbesserungen

* Standardbereich für die Statustabelle im [!DNL Privacy Service] Die Benutzeroberfläche wurde auf einen Zeitraum von 7 Tagen geändert.
* Bessere interne Ausnahmebehandlung.
* Verbesserte Leistung durch die Einführung von Caching für allgemeine interne Aufrufe mit niedrigen Datenänderungsraten.

### Fehlerkorrekturen

* Fehlende Protokollierungsinformationen für gefilterte Abfragen für die `GET /` -Endpunkt im [!DNL Privacy Service] API.

## Donnerstag, 11. April 2019

### Verbesserungen

* Die Benutzeroberfläche wurde aktualisiert, um neue Funktionen für Beta-Kunden zu unterstützen
* Neue Metriken-API zur Unterstützung von Benutzeroberfläche 2.0-Funktionen in der Beta-Version

## Dienstag, 9. April 2019

### Verbesserungen

* Aktualisierung aller GET-API-Aufrufe (Suche) auf einen Lookback-Bereich von 30 Tagen
* Beschränkung der API-Nutzung auf einen maximalen Lookback-Bereich von 45 Tagen

## Donnerstag, 14. Februar 2019

### Verbesserungen

* Durchsetzen des `include`-Felds bei jeder POST-Übermittlung.
* Durchsetzen des `include`-Felds beim Hochladen von JSON.

### Fehlerkorrekturen

* Es wurde ein Problem behoben, bei dem Kunden die [!DNL Privacy Service] Benutzeroberfläche.
