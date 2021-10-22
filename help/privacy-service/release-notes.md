---
keywords: Experience Platform;Home;beliebte Themen
solution: Experience Platform
title: Versionshinweise zu Privacy Services
topic-legacy: release notes
description: Die neuesten Versionshinweise für Adobe Experience Platform Privacy Service.
exl-id: 66ee38f1-f0d5-44ff-823d-d1b8a9765c6d
source-git-commit: 82dea48c732b3ddea957511c22f90bbd032ed9b7
workflow-type: tm+mt
source-wordcount: '553'
ht-degree: 52%

---

# [!DNL Privacy Service] Versionshinweise

Dieses Dokument enthält Informationen zu neuen Funktionen in Adobe Experience Platform [!DNL Privacy Service], sowie Verbesserungen und signifikante Bugfixes.

>[!NOTE]
>
>Die neuesten Versionshinweise zu anderen [!DNL Experience Platform] Dienste finden Sie [hier](../release-notes/latest/latest.md).

## 9. September 2020

### Neue Funktionen

| Funktion | Beschreibung |
| --- | --- |
| Unterstützung für LGPD (Brasilien) | Datenschutzaufträge können nun im Rahmen der von Brasilien [!DNL Lei Geral de Proteção de Dados] Verordnung (LGPD). Diese Aufträge werden im Rahmen des Regelungskodexes verfolgt `lgpd_bra`. |

## 8. April 2020

### Neue Funktionen

| Funktion | Beschreibung |
| --- | --- |
| Unterstützung für PDPA | [!DNL Privacy] Anfragen können nun im Rahmen des Datenschutzgesetzes (PDPA) in Thailand erstellt und verfolgt werden. Bei Datenschutzanfragen in der API akzeptiert das `regulation`-Array nun den Wert „pdpa_tha“. |
| Namespace-Typen in der Benutzeroberfläche | Sie können jetzt im Anforderungs-Builder in der [!DNL Privacy Service] UI. Weiterführende Informationen dazu finden Sie im [Benutzerhandbuch](ui/user-guide.md). |
| Einstellung des alten Endpunkts | Der alte API-Endpunkt (`data/privacy/gdpr`) wird nicht mehr unterstützt. |

## Dienstag, 14. Januar 2020

### Neue Funktionen

| Funktion | Beschreibung |
| --- | --- |
| [!DNL Privacy Service] Branding | Der frühere Name &quot;GDPR Service&quot; wurde umbenannt in [!DNL Privacy Service] als der Dienst hat sich gewachsen, um andere Verordnungen zusätzlich zum GDPR zu unterstützen. |
| Neue API-Endpunkte | Basispfad für [!DNL Privacy Service] API wurde aktualisiert von `/data/privacy/gdpr` nach `/data/core/privacy/jobs` |
| Neue erforderliche `regulation`-Eigenschaft | Beim Erstellen neuer Jobs in [!DNL Privacy Service] API, a `regulation` Eigenschaft muss in der Anforderungs-Nutzlast angegeben werden, unter welcher Regel der Auftrag verfolgt werden soll. Die zulässigen Werte sind `gdpr` und `ccpa`. Dokument anzeigen auf [Datenschutzaufträge](api/privacy-jobs.md) in [!DNL Privacy Service] API-Handbuch für weitere Informationen. |
| Unterstützung für die Adobe Primetime-Authentifizierung | [!DNL Privacy Service] akzeptiert jetzt Zugriffs-/Löschanfragen von der Adobe Primetime-Authentifizierung, wobei `primetimeAuthentication` als Produktwert verwendet wird. Weitere Informationen finden Sie in der [Dokumentation für die Primetime-Authentifizierung](http://tve.helpdocsonline.com/how-to-make-a-privacy-request). |

### Verbesserungen

* [!DNL Privacy Service] UI-Verbesserungen:
   * Separate Auftragsverfolgungsseiten für DSGVO- und CCPA-Vorschriften.
   * Neue Dropdown-Liste *Vorschriftentyp*, um zwischen den Verfolgungsdaten für DSGVO und CCPA zu wechseln.

## Donnerstag, 25. Juli 2019

### Neue Funktionen

| Funktion | Beschreibung |
| --- | --- |
| Dashboard „Anfragemetriken“ | Das neue Metriken-Dashboard im [!DNL Privacy Service] UI bietet Sichtbarkeit in gesendete, fehlerhafte und abgeschlossene GDPR-Anforderungen. |
| Request Builder | Um Unternehmen mit technischen und nicht-technischen Benutzern, die DSGVO-Anfragen senden, zu unterstützen, wurde der Benutzeroberfläche eine Funktion zum Erstellen einer Anfrage hinzugefügt. Die JSON-Dateiübertragungsfunktion ist weiterhin verfügbar im [!DNL Privacy Service] UI für diejenigen Unternehmen, die es weiterhin verwenden möchten. |
| Ereignisbenachrichtigungen für DSGVO-Aufträge | Ereignisbenachrichtigungen über den DSGVO-Auftragsstatus sind für viele Workflows von entscheidender Bedeutung. Während Benachrichtigungen bisher über individuelle E-Mail-Benachrichtigungen zugestellt wurden, handelt es sich bei DSGVO-Ereignisbenachrichtigungen um Nachrichten, die Adobe I/O-Ereignisse nutzen und an einen konfigurierten Webhook gesendet werden, der die Automatisierung von Auftragsanfragen erleichtert. [!DNL Privacy Service] Benutzer der Benutzeroberfläche können Adobe I/O-GDPR-Ereignis abonnieren, um Aktualisierungen zu erhalten, wenn ein Produkt oder der GDPR-Auftrag abgeschlossen wurde. |

## Donnerstag, 18. April 2019

### Verbesserungen

* Standardbereich für die Statustabelle in der [!DNL Privacy Service] UI wurde in einen 7-Tage-Bereich geändert.
* Bessere interne Ausnahmebehandlung.
* Verbesserte Leistung durch die Einführung von Caching für allgemeine interne Aufrufe mit niedrigen Datenänderungsraten.

### Fehlerkorrekturen

* Fehlende Protokollinformationen für gefilterte Abfragen für `GET /` Endpunkt im [!DNL Privacy Service] API.

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

* Es wurde ein Problem behoben, durch das Kunden nicht laden konnten [!DNL Privacy Service] UI.
