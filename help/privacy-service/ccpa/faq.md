---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Häufig gestellte Fragen zum CCPA
topic: troubleshooting
translation-type: tm+mt
source-git-commit: 5b32c1955fac4f137ba44e8189376c81cdbbfc40
workflow-type: tm+mt
source-wordcount: '787'
ht-degree: 80%

---


# Häufig gestellte Fragen zum CCPA

This document provides answers to frequently asked questions about the [!DNL California Consumer Protection Act] (CCPA) and its implementation in Adobe Experience Cloud.

## Was ist CCPA?

The [!DNL California Consumer Privacy Act] (CCPA) is California’s new privacy law that provides its residents with new rights regarding their personal information, and imposes data protection responsibilities on certain entities who conduct business in California.

>[!NOTE]
>
>Zwar ist der CCPA im Januar 2020 formal in Kraft getreten, doch nimmt der Gesetzgeber noch immer Feinabstimmungen vor. Darüber hinaus werden durch Bestimmungen, die von der kalifornischen Regulierungsbehörde noch verfasst werden müssen, wichtige Umsetzungs- und andere Anleitungsdetails angekündigt.

Der CCPA teilt zwar einige der in der Datenschutz-Grundverordnung (DSGVO) der Europäischen Union enthaltenen Konzepte, wie das Recht einer betroffenen Person auf Zugang zu und Löschung personenbezogener Daten, doch gibt es mehrere wesentliche Unterschiede zwischen dem CCPA und der DSGVO. So bietet der CCPA Verbrauchern beispielsweise ein Opt-out-Recht hinsichtlich bestimmter Datenaustauschaktivitäten, die als „Verkauf“ personenbezogener Daten an eine Drittpartei gelten, anstatt eine vorherige Zustimmung vorauszusetzen.

## Wie lautet die Definition für personenbezogene Daten gemäß CCPA?

Personenbezogene Daten sind Daten, „die einen Verbraucher oder Haushalt identifizieren, sich darauf beziehen, beschreiben, in der Lage sind, mit einem Verbraucher oder Haushalt in Verbindung gebracht zu werden, oder vernünftigerweise mit einem Verbraucher oder Haushalt verknüpft werden könnten“.

## Welche Arten von personenbezogenen Daten oder Kennungen, die in Adobe Experience Cloud verwendet werden, unterliegen diesen neuen Anforderungen?

The following identifiers are commonly used in [!DNL Experience Cloud] applications and could be subject to CCPA requirements:

- Name
- Postadresse
- Eindeutige personenbezogene Kennung
- Online-Kennung
- IP-Adresse
- E-Mail Adresse
- Kontoname

Personenbezogene Daten können auch Informationen über Aktivitäten im Internet oder in anderen elektronischen Netzwerken umfassen. Dazu gehören unter anderem:

- Browser-Verlauf
- Suchverlauf
- Informationen zur Interaktion eines Verbrauchers mit einer Website, Anwendung oder Werbung

Even though CCPA covers a wide set of personal information, Adobe’s standard contract terms dictate that sensitive personal information (such as SSN, driver’s license information, financial account information, and biometric data) is generally prohibited from import and use in [!DNL Experience Cloud] applications.

## Wie gelten die verschiedenen Rollen und Verantwortlichkeiten des CCPA für [!DNL Experience Cloud]?

Gemäß der Definition des CCPA gelten für Adobe und seine Kunden folgende Rollen:

- Adobe-Kunden (die Parteien, die die Erfassung und Verwendung personenbezogener Daten von kalifornischen Einwohnern beantragen) würden als **Unternehmen** betrachtet.
- Adobe würde in seiner Rolle als Anbieter des Diensts als **Dienstleister** angesehen.

Angesichts dieser Beziehung und der Vertragssprache von Adobe würden Offenlegungen an Adobe wahrscheinlich nicht als „Verkauf“ eingestuft, für den Unternehmen eine Meldung machen und ein Opt-out anbieten müssen.

Adobe-Dienste können jedoch verwendet werden, um bestimmte Daten auszutauschen und Übertragungen an Dritte zu ermöglichen. Diese Übertragungen an Dritte könnten als „Verkauf“ betrachtet werden und erfordern von Rechts wegen eine Offenlegung und Opt-out-Option.  Kunden sollten mit ihrem Rechtsbeistand zusammenarbeiten, um einzelne Anwendungsfälle hinsichtlich der geltenden Anforderungen zu evaluieren.

## Wie viele Tage hat ein Unternehmen Zeit, um auf die Anfrage eines Verbrauchers hinsichtlich Zugriff auf oder Löschung personenbezogener Daten zu reagieren?

Angenommen, dass das Unternehmen personenbezogene Daten gesammelt hat und die Identität eines bestimmten kalifornischen Verbrauchers authentifizieren oder verifizieren kann, lässt der CCPA 45 Tage Zeit zum Erfüllen der Anfragen von Verbrauchern (mit einigen Ausnahmen).

## Welche Rolle spielt Adobe gemäß dem CCPA?

Als Dienstleister sammelt und verarbeitet Adobe personenbezogene Daten im Auftrag des Unternehmens und ist vertraglich dazu verpflichtet, diese Daten nur für die in der Vereinbarung festgelegten Zwecke zu verwenden.

Angesichts dieser Beziehung und der Vertragssprache von Adobe fallen Offenlegungen an Adobe unter die gesetzlichen Bestimmungen für Dienstleister und würden wahrscheinlich nicht als „Verkauf“ eingestuft, für den Unternehmen eine Meldung machen und ein Opt-out anbieten müssen.

Adobe-Dienste können verwendet werden, um bestimmte Daten auszutauschen und Übertragungen an Dritte zu ermöglichen. Solche Übertragungen an Dritte können als „Verkauf“ betrachtet werden und erfordern von Rechts wegen eine Meldung und Opt-out-Option.  Kunden sollten mit ihrem Rechtsbeistand zusammenarbeiten, um einzelne Anwendungsfälle hinsichtlich der geltenden Anforderungen zu evaluieren.

## Wie kann ich die Datenschutzbestimmungen für Verbraucher im Rahmen des CCPA einhalten, wenn ich bestimmte Datentypen verwalte, die von den Anforderungen abgedeckt werden?

Once you have taken the necessary steps to authenticate CA consumers, Adobe Experience Platform [!DNL Privacy Service] allows you to submit consumer privacy requests to compatible [!DNL Experience Cloud] applications. Weiterführende Informationen dazu finden Sie unter [Übersicht zum Privacy Service](../home.md). For information on how your particular [!DNL Experience Cloud] applications can honor privacy requests, please refer to the guide on [Privacy Service and Experience Cloud applications](../experience-cloud-apps.md).

>[!NOTE]
>
>Die kalifornische Regulierungsbehörde wird weitere Bestimmungen dazu vorlegen, welche Arten von Daten für Datenschutzanfragen von Verbrauchern infrage kommen.

## Bietet Adobe weitere Tools, die bei der Erfüllung von CCPA-Anforderungen hilfreich sein können?

Adobe Experience Cloud-Anwendungen verfügen über Daten-Management- und Data-Governance-Funktionen, die den Datenschutzbedarf von Unternehmen unterstützen können. Zu diesen Tools gehören die Kennzeichnung der Datennutzung, rollenbasierte Zugriffskontrollen, IP-Verschleierung und Hashing-Funktionen.

Adobe hat für seine Datenschutz- und Sicherheitsmaßnahmen verschiedene Zertifizierungen erhalten, z. B. eine ISO 27001-Zertifizierung und eine DSGVO-Validierung von TrustArc.