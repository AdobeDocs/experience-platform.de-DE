---
keywords: Experience Platform;Startseite;beliebte Themen
solution: Experience Platform
title: Privacy Service – Versionshinweise
description: Die neuesten Versionshinweise für Adobe Experience Platform Privacy Service.
exl-id: 66ee38f1-f0d5-44ff-823d-d1b8a9765c6d
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: ht
source-wordcount: '553'
ht-degree: 100%

---

# [!DNL Privacy Service] – Versionshinweise

In diesem Dokument finden Sie Informationen zu neuen Funktionen von Adobe Experience Platform [!DNL Privacy Service] sowie zu Verbesserungen und wichtigen Fehlerkorrekturen.

>[!NOTE]
>
>Die neuesten Versionshinweise für andere [!DNL Experience Platform]-Services finden Sie [hier](../release-notes/latest/latest.md).

## 9. September 2020

### Neue Funktionen

| Funktion | Beschreibung |
| --- | --- |
| Unterstützung für LGPD (Brasilien) | Datenschutzaufträge können jetzt im Rahmen der [!DNL Lei Geral de Proteção de Dados] (LGPD)-Verordnung erstellt werden. Diese Aufträge werden unter dem Regulierungs-Code `lgpd_bra` verfolgt. |

## 8. April 2020

### Neue Funktionen

| Funktion | Beschreibung |
| --- | --- |
| Unterstützung für PDPA | [!DNL Privacy]-Anfragen können jetzt mit Blick auf das Datenschutzgesetz (PDPA) in Thailand erstellt und verfolgt werden. Bei Datenschutzanfragen in der API akzeptiert das `regulation`-Array nun den Wert „pdpa_tha“. |
| Namespace-Typen in der Benutzeroberfläche | Sie können jetzt im Request Builder in der [!DNL Privacy Service]-Benutzeroberfläche verschiedene Namespace-Typen angeben. Weiterführende Informationen dazu finden Sie im [Benutzerhandbuch](ui/user-guide.md). |
| Einstellung des alten Endpunkts | Der alte API-Endpunkt (`data/privacy/gdpr`) wird nicht mehr unterstützt. |

## 14. Januar 2020

### Neue Funktionen

| Funktion | Beschreibung |
| --- | --- |
| [!DNL Privacy Service]-Rebranding | Der früher als „GDPR Service“ bezeichnete Service wurde in [!DNL Privacy Service] umbenannt, da der Service erweitert wurde, um neben der DSGVO auch andere Vorschriften zu unterstützen. |
| Neue API-Endpunkte | Der Basispfad für die [!DNL Privacy Service]-API wurde von `/data/privacy/gdpr` auf `/data/core/privacy/jobs` aktualisiert. |
| Neue erforderliche `regulation`-Eigenschaft | Bei der Erstellung neuer Aufträge in der [!DNL Privacy Service]-API muss eine `regulation`-Eigenschaft in der Anfrage-Payload angegeben werden, die angibt, nach welcher Vorschrift der Auftrag verfolgt werden soll. Die zulässigen Werte sind `gdpr` und `ccpa`. Weitere Informationen finden Sie im Dokument zu [Datenschutzvorgängen](api/privacy-jobs.md) im [!DNL Privacy Service]-API-Handbuch. |
| Unterstützung für die Adobe Primetime-Authentifizierung | [!DNL Privacy Service] akzeptiert jetzt Zugriffs-/Löschanfragen von der Adobe Primetime-Authentifizierung, wobei `primetimeAuthentication` als Produktwert verwendet wird. Weitere Informationen finden Sie in der [Dokumentation für die Primetime-Authentifizierung](https://tve.helpdocsonline.com/how-to-make-a-privacy-request). |

### Verbesserungen

* Verbesserungen der [!DNL Privacy Service]-Benutzeroberfläche:
   * Separate Auftragsverfolgungsseiten für DSGVO- und CCPA-Vorschriften.
   * Neue Dropdown-Liste *Vorschriftentyp*, um zwischen den Verfolgungsdaten für DSGVO und CCPA zu wechseln.

## 25. Juli 2019

### Neue Funktionen

| Funktion | Beschreibung |
| --- | --- |
| Dashboard „Anfragemetriken“ | Das neue Metriken-Dashboard in der [!DNL Privacy Service]-Benutzeroberfläche bietet Einblicke in gesendete, fehlerhafte und abgeschlossene DSGVO-Anfragen. |
| Request Builder | Um Unternehmen mit technischen und nicht-technischen Benutzenden, die DSGVO-Anfragen senden, zu unterstützen, wurde der Benutzeroberfläche eine Funktion zum Erstellen einer Anfrage hinzugefügt. Die Funktion zum Übermitteln von JSON-Dateien ist noch in der [!DNL Privacy Service]-Benutzeroberfläche für Organisationen verfügbar, die sie weiterhin verwenden möchten. |
| Ereignisbenachrichtigungen für DSGVO-Aufträge | Ereignisbenachrichtigungen über den DSGVO-Auftragsstatus sind für viele Workflows von entscheidender Bedeutung. Während Benachrichtigungen bisher über individuelle E-Mail-Benachrichtigungen zugestellt wurden, handelt es sich bei DSGVO-Ereignisbenachrichtigungen um Nachrichten, die Adobe I/O-Ereignisse nutzen und an einen konfigurierten Webhook gesendet werden, der die Automatisierung von Auftragsanfragen erleichtert. Benutzende der [!DNL Privacy Service]-Benutzeroberfläche können Adobe I/O-DSGVO-Ereignisse abonnieren, um Updates zu erhalten, wenn ein Produkt oder der DSGVO-Auftrag abgeschlossen wurde. |

## 18. April 2019

### Verbesserungen

* Der Standardbereich für die Statustabelle in der [!DNL Privacy Service]-Benutzeroberfläche wurde auf einen Zeitraum von 7 Tagen geändert.
* Bessere interne Ausnahmebehandlung.
* Verbesserte Leistung durch die Einführung von Caching für allgemeine interne Aufrufe mit niedrigen Datenänderungsraten.

### Fehlerkorrekturen

* Es wurden fehlende Protokollierungsinformationen für gefilterte Abfragen für den `GET /`-Endpunkt in der [!DNL Privacy Service]-API hinzugefügt.

## 11. April 2019

### Verbesserungen

* Die Benutzeroberfläche wurde aktualisiert, um neue Funktionen für Beta-Kunden zu unterstützen
* Neue Metriken-API zur Unterstützung von Benutzeroberfläche 2.0-Funktionen in der Beta-Version

## 9. April 2019

### Verbesserungen

* Aktualisierung aller GET-API-Aufrufe (Suche) auf einen Lookback-Bereich von 30 Tagen
* Beschränkung der API-Nutzung auf einen maximalen Lookback-Bereich von 45 Tagen

## 14. Februar 2019

### Verbesserungen

* Durchsetzen des `include`-Felds bei jeder POST-Übermittlung.
* Durchsetzen des `include`-Felds beim Hochladen von JSON.

### Fehlerkorrekturen

* Es wurde ein Problem behoben, bei dem Kundinnen und Kunden die [!DNL Privacy Service]-Benutzeroberfläche nicht laden konnten.
