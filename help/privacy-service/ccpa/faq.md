---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Häufig gestellte Fragen zum CCPA
topic: troubleshooting
translation-type: tm+mt
source-git-commit: d0fcae6b1b75584a2c26d6eee5b47e0d60a142ba
workflow-type: tm+mt
source-wordcount: '807'
ht-degree: 0%

---


# Häufig gestellte Fragen zum CCPA

In diesem Dokument erhalten Sie Antworten auf häufig gestellte Fragen zum California Consumer Protection Act (CCPA) und seiner Implementierung in Adobe Experience Cloud.

## Was ist CCPA?

Das California Consumer Privacy Act (CCPA) ist das neue kalifornische Datenschutzgesetz, das seinen Bewohnern neue Rechte in Bezug auf ihre personenbezogenen Daten einräumt und bestimmte Personen, die in Kalifornien Geschäfte tätigen, mit Datenschutzpflichten belegt.

>[!NOTE] Obwohl die CCPA im Januar 2020 technisch wirksam ist, werden sie von den Gesetzgebern noch immer Feinabstimmung vorgenommen. Darüber hinaus werden in den Vorschriften, die noch von der kalifornischen Regulierungsbehörde verfasst werden müssen, wichtige Umsetzungsmaßnahmen und andere Leitlinien angekündigt.

Während CCPA einige der in der Verordnung der Europäischen Vereinigung über den Schutz personenbezogener Daten (GDPR) enthaltenen Konzepte, wie das Recht eines Individuums auf Zugang zu und Löschung personenbezogener Daten, teilt, gibt es mehrere wesentliche Unterschiede zwischen CCPA und GDPR. So bietet CCPA Verbrauchern beispielsweise das Recht, bestimmte Aktivitäten zum Datenaustausch, die als &quot;Verkauf&quot;personenbezogener Daten an Dritte gelten, auszuschließen, anstatt eine vorherige Zustimmung zu benötigen.

## Was ist die Definition der personenbezogenen Daten im Rahmen des CCPA?

Personenbezogene Informationen sind Informationen, &quot;die einen Verbraucher oder Haushalt identifizieren, sich darauf beziehen, beschreiben, in der Lage sind, mit einem Verbraucher oder Haushalt in Verbindung gebracht zu werden oder vernünftigerweise mit ihm verbunden werden zu können.&quot;

## Welche Arten von persönlichen Informationen oder IDs, die in Adobe Experience Cloud verwendet werden, unterliegen diesen neuen Anforderungen?

Die folgenden IDs werden in Experience Cloud-Anwendungen häufig verwendet und können CCPA-Anforderungen unterliegen:

- Name
- Postal address
- Eindeutige persönliche Kennung
- Online-ID
- IP-Adresse
- E-Mail  Adresse
- Kontoname

Personenbezogene Informationen können auch Informationen über die Aktivität von Internetseiten oder anderen elektronischen Netzen umfassen. Dazu gehören unter anderem:

- Browserverlauf
- Suchverlauf
- Informationen zur Interaktion eines Verbrauchers mit einer Website, Anwendung oder Werbung

Obwohl CCPA viele persönliche Informationen abdeckt, schreiben die Standardvertragsbedingungen von Adobe vor, dass vertrauliche persönliche Daten (wie SSN, Lizenzinformationen des Fahrers, Finanzkonteninformationen und biometrische Daten) in Experience Cloud-Anwendungen generell nicht importiert und verwendet werden dürfen.

## Wie gelten die verschiedenen Rollen und Zuständigkeiten von CCPA für Experience Cloud?

Gemäß der Definition von CCPA gelten die folgenden Rollen für Adobe und seine Kunden:

- Adobe-Kunden (die Partei, die die Erfassung und Verwendung personenbezogener Daten von Einwohnern in Kalifornien beantragt) würden als **Geschäft** betrachtet.
- Adobe würde in seiner Rolle als Anbieter des Dienstes als **Dienstleister** angesehen.

Angesichts dieser Beziehung und der Vertragssprache von Adobe würden Offenlegungen an Adobe wahrscheinlich nicht als &quot;Verkauf&quot;betrachtet, für den Unternehmen eine Kündigung und Angebot einer Opt-out-Klausel vorlegen müssten.

Adobe-Dienste können jedoch verwendet werden, um die Freigabe bestimmter Daten und Übertragungen an Dritte zu ermöglichen. Diese Übertragungen von Dritten könnten als &quot;Verkauf&quot;betrachtet werden und erfordern rechtlich die Offenlegung und den Ausschluss.  Kunden sollten mit ihrem Rechtsbeistand zusammenarbeiten, um bestimmte Anwendungsfälle zu bewerten, um geltende Anforderungen zu bewerten.

## Wie viele Tage muss ein Unternehmen auf eine Anfrage des Verbrauchers reagieren, um auf persönliche Daten zuzugreifen oder sie zu löschen?

Unter der Annahme, dass das Unternehmen personenbezogene Daten gesammelt hat und die Identität eines bestimmten kalifornischen Verbrauchers authentifiziert oder überprüft werden kann, ermöglicht das CCPA die Erfüllung von Verbraucheranfragen innerhalb von 45 Tagen (mit einigen Ausnahmen).

## Welche Rolle spielt Adobe im Rahmen des CCPA?

Als Dienstleister sammelt und verarbeitet Adobe personenbezogene Daten im Auftrag des Unternehmens und ist vertraglich verpflichtet, diese Informationen nur für die in der Vereinbarung festgelegten spezifischen Zwecke zu verwenden.

Angesichts dieser Beziehung und der Vertragssprache von Adobe fallen Offenlegungen an Adobe unter die gesetzlichen Bestimmungen für Dienstleister und würden wahrscheinlich nicht als &quot;Verkauf&quot;betrachtet, für den Unternehmen eine Kündigung und Angebot vorlegen müssen.

Adobe-Dienste können verwendet werden, um die Freigabe bestimmter Daten und Übertragungen an Dritte zu ermöglichen. Diese Übertragungen von Dritten könnten als &quot;Verkauf&quot;betrachtet werden und erfordern rechtlich die Offenlegung und den Ausschluss.  Kunden sollten mit ihrem Rechtsbeistand zusammenarbeiten, um bestimmte Anwendungsfälle zu bewerten, um geltende Anforderungen zu bewerten.

## Wie kann ich die Datenschutzbestimmungen für Verbraucher im Rahmen des CCPA unterstützen, wenn ich bestimmte Datentypen unterhalte, die von den Anforderungen abgedeckt sind?

Sobald Sie die erforderlichen Schritte zur Authentifizierung von CA-Kunden unternommen haben, können Sie mit dem Adobe Experience Platform Privacy Service Verbraucherdatenschutzanforderungen an kompatible Experience Cloud-Anwendungen senden. See the [Privacy Service overview](../home.md) for more information. Informationen darüber, wie Ihre speziellen Experience Cloud-Anwendungen Datenschutzanforderungen erfüllen können, finden Sie im Handbuch zu [Datenschutzdiensten und Experience Cloud-Anwendungen](../experience-cloud-apps.md).

>[!NOTE] Die kalifornische Regulierungsbehörde wird noch weitere Leitlinien dazu vorlegen, welche Arten von Daten für Datenschutzanforderungen an Verbraucher infrage kommen.

## Bietet Adobe Angebot andere Tools, die bei der Erfüllung von CCPA-Anforderungen hilfreich sein können?

Adobe Experience Cloud-Anwendungen bieten Data Management- und Verwaltungsfunktionen, die für den Datenschutz von Firmen hilfreich sein können. Zu diesen Tools gehören die Kennzeichnung der Datenverwendung, rollenbasierte Zugriffskontrollen, IP-Verschleierung und Hashing-Funktionen.

Adobe hat verschiedene Zertifizierungen zu Datenschutz- und Sicherheitsmaßnahmen erhalten, z. B. eine ISO 27001-Zertifizierung und eine TrustArc GDPR-Validierung.