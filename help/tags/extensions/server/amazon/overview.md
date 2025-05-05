---
title: Adobe Amazon Conversions API-Erweiterung
description: Mit dieser Adobe Experience Platform-Web-Ereignis-API können Sie Website-Interaktionen direkt mit Amazon teilen.
last-substantial-update: 2025-04-17T00:00:00Z
source-git-commit: 65a3eb20dc3de62319f73be49197dacb8fc1778b
workflow-type: tm+mt
source-wordcount: '672'
ht-degree: 2%

---

# Übersicht über die [!DNL Amazon] Web Events API-Erweiterung

Die [!DNL Amazon] Conversions-API-Erweiterung erstellt eine direkte Verbindung zwischen Marketing-Daten vom Server eines Werbetreibenden und [!DNL Amazon]. Dadurch können Werbetreibende die Effektivität von Kampagnen unabhängig vom Konversionsort bewerten und Kampagnen entsprechend optimieren. Die Erweiterung bietet eine vollständigere Attribution, eine verbesserte Datenzuverlässigkeit und eine besser optimierte Bereitstellung.

## Voraussetzungen für [!DNL Amazon] {#prerequisites}

Vor der Installation und Konfiguration der API-Erweiterung für [!DNL Amazon] Conversions müssen Sie mehrere erforderliche Schritte ausführen, um eine ordnungsgemäße Authentifizierung und einen ordnungsgemäßen Datenzugriff sicherzustellen.

### Erstellen von geheimen Daten und Datenelementen {#secret}

Die Authentifizierung mit [!DNL Amazon] erfordert ein sicheres Token, das ordnungsgemäß gespeichert und referenziert werden muss:

1. Erstellen Sie ein neues Geheimnis für die [!DNL Amazon]-Ereignisweiterleitung mit einem eindeutigen Namen für die Authentifizierung.
2. Erstellen Sie ein Datenelement mit der **Core**-Erweiterung mit dem Datenelementtyp **Secret**, um auf Ihr [!DNL Amazon] zu verweisen.

Dadurch wird sichergestellt, dass Ihre Authentifizierungsberechtigungen sicher bleiben, während sie bei Bedarf weiterhin für die Erweiterung zugänglich sind.

## Installieren und Konfigurieren der [!DNL Amazon]

Für die Installation der Erweiterung ist Zugriff auf Ihre Ereignisweiterleitungs-Eigenschaft in Experience Platform erforderlich:

- Erstellen oder bearbeiten Sie eine Ereignisweiterleitungseigenschaft.
- Wählen **Erweiterungen** in der linken Navigationsleiste und wählen Sie dann [!DNL Amazon] Erweiterung auf der Registerkarte Katalog .
- Wählen Sie **Installieren** aus.

![[!DNL Amazon] Erweiterung wird im Erweiterungskatalog zusammen mit der Schaltfläche Installieren ausgewählt.](../../../images/extensions/server/amazon/amazon-extension.png)

- Konfigurieren von mit:

- **Zugriffs-Token**: Geheime Daten des Datenelements, das das OAuth 2-Token enthält

![Individuelle Einstellungen zur Eingabe des geheimen Datenelements hervorgehoben.](../../../images/extensions/server/amazon/2.png)

- **Entitäts-ID**: Ihre Entitäts-ID (zu finden in der Portal-URL von Campaign Manager mit dem Präfix „Entity„)

![Das Kampagnen-Manager-Portal im linken Navigationsbereich.](../../../images/extensions/server/amazon/3.png)

- Wählen Sie **Speichern** aus.

Diese Konfigurationswerte stellen die Verbindung zwischen Platform und Ihrem [!DNL Amazon]-Konto her.

### OAuth 2 [!DNL Amazon] {#oauth}

So erstellen Sie geheime Daten vom Typ [!DNL Amazon] OAuth 2:

- Wählen Sie [!DNL Amazon] OAuth 2 aus der Dropdown **Liste Typ** und wählen Sie **Geheimnis erstellen**.

![Amazon OAuth 2 im Dropdown-Menü.](../../../images/extensions/server/amazon/Oauth.png)

- Wählen **im Pop-up die Option** Geheimnis mit Amazon erstellen und autorisieren“ aus, um das Geheimnis manuell zu autorisieren und fortzufahren.

![Geheimnis mit ausgewähltem Amazon erstellen und autorisieren.](../../../images/extensions/server/amazon/Oauth.1.png)

- Geben Sie im angezeigten Dialogfeld Ihre [!DNL Amazon] ein. Befolgen Sie die Anweisungen, um der Ereignisweiterleitung Zugriff auf Ihre Daten zu gewähren.

Nach Abschluss werden Ihre geheimen Daten mit ihrem Status und dem Ablaufdatum auf der Registerkarte **Geheime Daten** angezeigt.

![Geheime Daten auf der Registerkarte „Geheime Daten“ erstellt.](../../../images/extensions/server/amazon/Oauth.2.png)

## Konfigurieren einer Ereignisweiterleitungsregel {#config-rule}

Nachdem alle Datenelemente eingerichtet wurden, können Sie Ereignisweiterleitungsregeln erstellen, die bestimmen, wann und wie Ihre Ereignisse an Amazon gesendet werden.

- Navigieren Sie zu **Regeln** und erstellen Sie eine neue Ereignisweiterleitungsregel.
- Wählen **unter &quot;**&quot; die Option **Amazon Conversions API Extension**.
- Legen Sie den **Aktionstyp** auf **Konversionsereignisse importieren** fest.

![Aktionskonfigurationsoptionen hervorgehoben.](../../../images/extensions/server/amazon/4.png)

- Konfigurieren Sie die Ereigniseigenschaften wie unten beschrieben:

| Eingabe | Beschreibung |
| --- | --- |
| **Ereignisname** | Der Name des Konversionsereignisses. |
| **Ereignistyp** | Definiert den Typ des verfolgten Ereignisses (z. B. Käufe, Hinzufügungen zum Warenkorb). |
| **Zeitstempel** | Ereigniszeit im ISO-Format. |
| **Client-Deduplizierungs-ID** | Eine eindeutige ID für die Deduplizierung. |
| **Übereinstimmungsschlüssel** | Benutzer- und Gerätekennungen für die Attribution. |
| **Wert** | Geldwert des Ereignisses. |
| **Währungscode** | Währung im ISO-4217-Format. |
| **Verkaufte Einheiten** | Menge der gekauften Artikel. |
| **Ländercode** | Land, in dem das Ereignis aufgetreten ist. |
| **Datenverarbeitungsoptionen** | Flags für eingeschränkte Datennutzung. |
| **Einverständnis** | Gibt das Einverständnis des Benutzers zur Verwendung von Werbedaten an. |

- Wählen **Änderungen beibehalten**, um die Regel zu speichern.

![Ereignisparameter in der Aktionskonfiguration werden zusammen mit der Schaltfläche Änderungen beibehalten hervorgehoben.](../../../images/extensions/server/amazon/5.png)

![Zusätzliche Ereignisparameter in der Aktionskonfiguration werden zusammen mit der Schaltfläche Änderungen beibehalten hervorgehoben.](../../../images/extensions/server/amazon/6.png)

## Ereignis-Deduplizierung {#deduplication}

Wenn Sie sowohl [!DNL Amazon] Advertising Tag (AAT) als auch die [!DNL Amazon] Conversions-API-Erweiterung für dieselben Ereignisse verwenden, ist eine Einrichtung der Deduplizierung erforderlich. Schließen Sie `clientDedupeId` in jedes freigegebene Ereignis ein, um eine ordnungsgemäße Deduplizierung sicherzustellen.
Wenn sich Client- und Server-Ereignisse nicht überschneiden, ist keine Deduplizierung erforderlich.

Eine ordnungsgemäße Deduplizierung verhindert überhöhte Konversionszahlen und stellt sicher, dass Ihre Optimierungsdaten korrekt bleiben.

Weitere Informationen finden Sie im Handbuch zur Deduplizierung von Amazon[&#128279;](https://advertising.amazon.com/)Ereignissen .

## Nächste Schritte

In diesem Handbuch wurde beschrieben, wie Sie Konversionsereignisse mithilfe der [!DNL Amazon] Conversions-API-Erweiterung konfigurieren und an [!DNL Amazon] senden. Weitere Informationen zu den Funktionen der Ereignisweiterleitung in [!DNL Adobe Experience Platform] finden Sie unter [Übersicht über die Ereignisweiterleitung](../../../ui/event-forwarding/overview.md)

Weitere Informationen zum Debuggen Ihrer Implementierung mit dem Experience Platform-Debugger und dem Überwachungs-Tool für die Ereignisweiterleitung finden Sie unter [Adobe Experience Platform Debugger-Übersicht](https://experienceleague.adobe.com/de/docs/experience-platform/debugger/home) und [Überwachen von Aktivitäten](https://experienceleague.adobe.com/de/docs/experience-platform/tags/event-forwarding/monitoring) in der Ereignisweiterleitung.