---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Versionshinweise zu Privacy Services
topic: release notes
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '546'
ht-degree: 5%

---


# Versionshinweise zu Privacy Services

Dieses Dokument enthält Informationen zu neuen Funktionen für Adobe Experience Platform Privacy Service sowie zu Verbesserungen und wichtigen Fehlerkorrekturen.

>[!NOTE]
>
>Die neuesten Versionshinweise zu anderen Experience Platformen-Services finden Sie [hier](../release-notes/latest/latest.md).

## 8. April 2020

### Neue Funktionen

| Funktion | Beschreibung |
| --- | --- |
| PDPA-Unterstützung | Datenschutzanforderungen können nun im Rahmen des Datenschutzgesetzes (PDPA) in Thailand erstellt und nachverfolgt werden. Bei Datenschutzanforderungen in der API akzeptiert das `regulation` Array den Wert &quot;pdpa_tha&quot;. |
| Namensraum-Typen in der Benutzeroberfläche | Sie können jetzt verschiedene Namensraum im Anforderungs-Builder in der Benutzeroberfläche des Privacy Service angeben. Weitere Informationen finden Sie im [Benutzerhandbuch](ui/user-guide.md) . |
| Alter Endpunktverfall | Der alte API-Endpunkt (`data/privacy/gdpr`) wurde nicht mehr unterstützt. |

## 14. Januar 2020

### Neue Funktionen

| Funktion | Beschreibung |
| --- | --- |
| Umbenennung von Privacy Services | Der ehemals &quot;GDPR-Dienst&quot;wurde in Privacy Service umbenannt, da der Dienst zu anderen Vorschriften als dem GDPR geworden ist. |
| Neue API-Endpunkte | Der Basispfad für die Privacy Service-API wurde von `/data/privacy/gdpr` zu `/data/core/privacy/jobs` |
| Neue erforderliche `regulation` Eigenschaft | Beim Erstellen neuer Aufträge in der Privacy Service-API muss eine `regulation` Eigenschaft in der Anforderungs-Nutzlast angegeben werden, unter welcher Regel der Auftrag verfolgt werden soll. Die zulässigen Werte sind `gdpr` und `ccpa`. Weitere Informationen finden Sie im Dokument zu [Datenschutzaufträgen](api/privacy-jobs.md) im Privacy Service-Entwicklerhandbuch. |
| Unterstützung der Adobe Primetime-Authentifizierung | Privacy Service akzeptiert jetzt Zugriff-/Löschanforderungen aus der Adobe Primetime-Authentifizierung, wobei `primetimeAuthentication` als Produktwert verwendet wird. See the [Primetime Authentication documentation](http://tve.helpdocsonline.com/how-to-make-a-privacy-request) for more information. |

### Verbesserungen

* Verbesserungen der Benutzeroberfläche von Privacy Service:
   * Separate Auftragsverfolgungsseiten für GDPR- und CCPA-Regeln.
   * Neues _Regeltyp_ -Dropdown, um zwischen den Verfolgungsdaten für GDPR und CCPA zu wechseln.

## 25. Juli 2019

### Neue Funktionen

| Funktion | Beschreibung |
| --- | --- |
| Dashboard &quot;Metriken anfordern&quot; | Das neue Dashboard &quot;Metriken&quot;in der Benutzeroberfläche des Privacy Service bietet Einblicke in gesendete, fehlerhafte und abgeschlossene GDPR-Anforderungen. |
| Anforderungs-Builder | Um Unternehmen mit technischen und nicht-technischen Benutzern, die GDPR-Anforderungen einreichen, zu betreuen, wurde der Benutzeroberfläche eine Funktion zum Erstellen einer Anforderung hinzugefügt. Die JSON-Dateiübermittlungsfunktion ist in der Benutzeroberfläche des Privacy Service weiterhin für Unternehmen verfügbar, die sie weiterhin verwenden möchten. |
| GDPR-Ereignis-Benachrichtigungen | Ereignis-Benachrichtigungen über den GDPR-Auftragsstatus sind für viele Workflows von entscheidender Bedeutung. Während Benachrichtigungen zuvor mit einzelnen E-Mail-Benachrichtigungen verarbeitet wurden, handelt es sich bei GDPR-Ereignis-Benachrichtigungen um Nachrichten, die Adobe-E/A-Ereignis nutzen und an einen konfigurierten Web-Haken gesendet werden, der die Automatisierung von Auftragsanforderungen erleichtert. Privacy Service-UI-Benutzer können Adobe-I/O-GDPR-Ereignis abonnieren, um Updates zu erhalten, wenn ein Produkt oder der GDPR-Auftrag abgeschlossen wurde. |

## 18. April 2019

### Verbesserungen

* Der Standardbereich für die Statustabelle in der Benutzeroberfläche des Privacy Service wurde auf einen 7-Tage-Zeitraum geändert.
* Bessere interne Ausnahmebehandlung.
* Verbesserte Leistung durch die Einführung der Zwischenspeicherung für allgemeine interne Aufrufe mit niedrigen Datenänderungsraten.

### Fehlerkorrekturen

* Fehlende Protokollinformationen für gefilterte Abfragen für den `GET /` Endpunkt in der Privacy Service-API hinzugefügt.

## 11. April 2019

### Verbesserungen

* Die Benutzeroberfläche wurde aktualisiert, um neue Funktionen für Beta-Kunden zu unterstützen
* Neue Metrik-API zur Unterstützung von UI 2.0-Funktionen in der Beta-Version

## 9. April 2019

### Verbesserungen

* Aktualisierung aller GET-API-Aufrufe (Lookup) auf einen 30-Tage-Lookback-Bereich
* Eingeschränkte API-Nutzung für einen maximalen Lookback-Bereich von 45 Tagen

## 14. Februar 2019

### Verbesserungen

* Erzwingen Sie das `include` Feld bei jeder POST-Übermittlung.
* Erzwingen Sie das `include` Feld beim Hochladen von JSON.

### Fehlerkorrekturen

* Es wurde ein Problem behoben, bei dem Kunden die Benutzeroberfläche des Privacy Service nicht laden konnten.