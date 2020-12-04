---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Privacy Service – Versionshinweise
topic: release notes
translation-type: tm+mt
source-git-commit: 8c94d3631296c1c3cc97501ccf1a3ed995ec3cab
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 55%

---


# [!DNL Privacy Service] Versionshinweise

This document contains information about new features for Adobe Experience Platform [!DNL Privacy Service], as well as enhancements and significant bug fixes.

>[!NOTE]
>
>Die neuesten Versionshinweise zu anderen [!DNL Experience Platform] Diensten finden Sie [hier](../release-notes/latest/latest.md).

## 9. September 2020

### Neue Funktionen

| Funktion | Beschreibung |
| --- | --- |
| Unterstützung für LGPD (Brasilien) | Datenschutzaufträge können nun im Rahmen der brasilianischen [!DNL Lei Geral de Proteção de Dados] (LGPD-)Verordnung geschaffen werden. Diese Aufträge werden unter dem Regelungskodex nachverfolgt `lgpd_bra`. |

## 8. April 2020

### Neue Funktionen

| Funktion | Beschreibung |
| --- | --- |
| Unterstützung für PDPA | [!DNL Privacy] Anfragen können nun im Rahmen des Datenschutzgesetzes (PDPA) in Thailand erstellt und verfolgt werden. Bei Datenschutzanfragen in der API akzeptiert das `regulation`-Array nun den Wert „pdpa_tha“. |
| Namespace-Typen in der Benutzeroberfläche | You can now specify different namespace types in the Request Builder in the [!DNL Privacy Service] UI. Weiterführende Informationen dazu finden Sie im [Benutzerhandbuch](ui/user-guide.md). |
| Einstellung des alten Endpunkts | Der alte API-Endpunkt (`data/privacy/gdpr`) wird nicht mehr unterstützt. |

## Dienstag, 14. Januar 2020

### Neue Funktionen

| Funktion | Beschreibung |
| --- | --- |
| [!DNL Privacy Service] umgestalten | The formerly named &quot;GDPR Service&quot; has been rebranded to [!DNL Privacy Service] as the service has grown to support other regulations in addition to GDPR. |
| Neue API-Endpunkte | Base path for the [!DNL Privacy Service] API has been updated from `/data/privacy/gdpr` to `/data/core/privacy/jobs` |
| Neue erforderliche `regulation`-Eigenschaft | When creating new jobs in the [!DNL Privacy Service] API, a `regulation` property must be supplied in the request payload to indicate which regulation to track the job under. Die zulässigen Werte sind `gdpr` und `ccpa`. Weitere Informationen finden Sie im Dokument zu [Datenschutzaufträgen](api/privacy-jobs.md) im Entwicklerhandbuch für [!DNL Privacy Service] |
| Unterstützung für die Adobe Primetime-Authentifizierung | [!DNL Privacy Service] akzeptiert jetzt Zugriffs-/Löschanfragen von der Adobe Primetime-Authentifizierung, wobei `primetimeAuthentication` als Produktwert verwendet wird. Weitere Informationen finden Sie in der [Dokumentation für die Primetime-Authentifizierung](http://tve.helpdocsonline.com/how-to-make-a-privacy-request). |

### Verbesserungen

* [!DNL Privacy Service] Verbesserungen der Benutzeroberfläche:
   * Separate Auftragsverfolgungsseiten für DSGVO- und CCPA-Vorschriften.
   * Neue Dropdown-Liste *Vorschriftentyp*, um zwischen den Verfolgungsdaten für DSGVO und CCPA zu wechseln.

## Donnerstag, 25. Juli 2019

### Neue Funktionen

| Funktion | Beschreibung |
| --- | --- |
| Dashboard „Anfragemetriken“ | The new metrics dashboard in the [!DNL Privacy Service] UI provides visibility into submitted, errored, and completed GDPR requests. |
| Request Builder | Um Unternehmen mit technischen und nicht-technischen Benutzern, die DSGVO-Anfragen senden, zu unterstützen, wurde der Benutzeroberfläche eine Funktion zum Erstellen einer Anfrage hinzugefügt. The JSON file submission capability is still available in the [!DNL Privacy Service] UI for those organizations who prefer to continue using it. |
| Ereignisbenachrichtigungen für DSGVO-Aufträge | Ereignisbenachrichtigungen über den DSGVO-Auftragsstatus sind für viele Workflows von entscheidender Bedeutung. Während Benachrichtigungen bisher über individuelle E-Mail-Benachrichtigungen zugestellt wurden, handelt es sich bei DSGVO-Ereignisbenachrichtigungen um Nachrichten, die Adobe I/O-Ereignisse nutzen und an einen konfigurierten Webhook gesendet werden, der die Automatisierung von Auftragsanfragen erleichtert. [!DNL Privacy Service] Benutzer der Benutzeroberfläche können Adobe I/O GDPR-Ereignis abonnieren, um Updates zu erhalten, wenn ein Produkt- oder der GDPR-Auftrag abgeschlossen wurde. |

## Donnerstag, 18. April 2019

### Verbesserungen

* Default range for the status table in the [!DNL Privacy Service] UI modified to a 7-day span.
* Bessere interne Ausnahmebehandlung.
* Verbesserte Leistung durch die Einführung von Caching für allgemeine interne Aufrufe mit niedrigen Datenänderungsraten.

### Fehlerkorrekturen

* Added missing logging information for filtered queries for the `GET /` endpoint in the [!DNL Privacy Service] API.

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

* Fixed an issue where customers could not load the [!DNL Privacy Service] UI.