---
keywords: Experience Platform;Startseite;beliebte Themen;DSGVO;DSGVO;CCPA;CCPA;PDPA;PDPA;LGPD;LGPD;FAQ;FAQ;Regulierung;Regulierung;Vorschriften;Vorschriften;Datenschutz;Datenschutz;
solution: Experience Platform
title: Häufig gestellte Fragen zu Datenschutzbestimmungen
description: Dieses Dokument enthält Antworten auf häufig gestellte Fragen zu unterstützten gesetzlichen Datenschutzbestimmungen und deren Implementierung in Adobe Experience Cloud.
exl-id: ec553e53-664b-4e18-abb1-4e4063fdd2c9
source-git-commit: d643b2aeadd4080fa89d6a7b0f84a9f6882d7b89
workflow-type: tm+mt
source-wordcount: '1606'
ht-degree: 32%

---

# Häufig gestellte Fragen zu Datenschutzbestimmungen

Dieses Dokument enthält Antworten auf häufig gestellte Fragen zu unterstützten gesetzlichen Datenschutzbestimmungen und deren Implementierung in Adobe Experience Cloud.

>[!NOTE]
>
>Definitionen der verschiedenen in diesem Dokument verwendeten Begriffe finden Sie im Handbuch [Terminologie für Datenschutzbestimmungen](terminology.md).

## Allgemeine Fragen

Die folgenden Fragen beziehen sich auf alle von Experience Cloud unterstützten Datenschutzbestimmungen.

### Auf wen wirken sich die unterstützten Datenschutzbestimmungen aus?

Die [Datenschutzbestimmungen, die von Experience Cloud unterstützt werden](./overview.md) gelten für alle Organisationen, die personenbezogene Daten von Bürgern innerhalb der jeweiligen Gerichtsbarkeit der Vorschriften speichern und verarbeiten, unabhängig vom geografischen Standort des Unternehmens.

### Was sind personenbezogene Daten?

Personenbezogene Daten sind alle Informationen, die eine natürliche Person (das „Datensubjekt“) betreffen und die zur direkten oder indirekten Identifikation dieser Person verwendet werden können. Dabei kann es sich um einen beliebigen Namen, ein Foto, eine E-Mail-Adresse, Bankdaten, Beiträge auf Social-Networking-Websites, medizinische Informationen oder eine Computer-IP-Adresse handeln.

Die folgenden Kennungen werden häufig in Experience Cloud-Anwendungen verwendet und könnten Datenschutzanforderungen unterliegen:

* Name
* Postadresse
* Eindeutige personenbezogene Kennung
* Online-Kennung
* IP-Adresse
* E-Mail-Adresse
* Kontoname

Personenbezogene Daten können auch Informationen über Aktivitäten im Internet oder in anderen elektronischen Netzwerken umfassen. Dazu gehören unter anderem:

* Browser-Verlauf
* Suchverlauf
* Informationen zur Interaktion eines Verbrauchers mit einer Website, Anwendung oder Werbung

Obwohl die Datenschutzbestimmungen eine Vielzahl personenbezogener Daten abdecken, schreiben die Standardvertragsbedingungen der Adobe vor, dass sensible personenbezogene Daten (wie SSN, Führerscheininformationen, Finanzkontoinformationen und biometrische Daten) in Experience Cloud-Anwendungen generell verboten sind.

### Was ist der Unterschied zwischen einem Datenverantwortlichen und einem Datenverarbeiter?

Ein **Datenverantwortlicher** ist die Stelle, die die Ziele, Bedingungen und Wege der Verarbeitung personenbezogener Daten bestimmt, während der **Datenverarbeiter** eine Stelle ist, die personenbezogene Daten im Auftrag des Datenverantwortlichen verarbeitet.

Ein **Datenverantwortlicher** ist die Person oder Organisation, die befugt und verantwortlich ist, Entscheidungen bezüglich der Erhebung, Verwendung oder Offenlegung personenbezogener Daten zu treffen. Ein **Auftragsverarbeiter** ist die Person oder Organisation, die im Zusammenhang mit der Erhebung, Nutzung oder Offenlegung der personenbezogenen Daten und der Anweisung des Datenverantwortlichen tätig ist.

### Was ist der Unterschied zwischen der ausdrücklichen und eindeutigen Zustimmung der betroffenen Person?

**Explizite Einwilligung** bezieht sich auf einen Einwilligungsstandard, der eine konkrete, informierte und eindeutige mündliche oder schriftliche Angabe der Wünsche der betroffenen Person umfasst. Einfach ausgedrückt, muss die betroffene Person wörtlich und ausdrücklich „Ich stimme zu“ oder „Ich stimme zu“ sagen, damit die Einwilligung als ausdrücklich erachtet wird. Darüber hinaus muss es genauso einfach sein, die Zustimmung zu widerrufen wie sie zu erteilen.

**Einwilligung (implizit)** Einwilligung, die nicht explizit von der betroffenen Person erteilt wurde, aber dennoch eindeutig ist. Beispielsweise erfolgt während des Anmeldevorgangs für eine Unternehmens-Website eine Benachrichtigung, dass die betroffene Person durch die Angabe einer E-Mail-Adresse dem Erhalt von E-Mails zu Sonderangeboten zustimmt. Liest die betroffene Person die Mitteilung, reicht die positive Handlung der Eingabe ihrer E-Mail aus, um als eindeutige Einwilligung betrachtet zu werden.

Bei vielen Vorschriften wie der DSGVO ist für die Verarbeitung sensibler personenbezogener Daten eine ausdrückliche Einwilligung erforderlich, wobei eine „Opt-in“ allein genügt. Bei nicht sensiblen Daten ist jedoch eine eindeutige (implizite) Zustimmung akzeptabel.

### Können betroffene Personen unter einem bestimmten Alter ihr Einverständnis erteilen?

Viele Datenschutzbestimmungen sehen vor, dass eine betroffene Person, die unter einem bestimmten Alter ist, der Erhebung ihrer personenbezogenen Daten rechtlich nicht zustimmen kann. Einige Vorschriften ermöglichen in diesen Fällen die Einwilligung des Inhabers der elterlichen Verantwortung für die betroffene Person, aber nicht für alle Fälle. In der folgenden Tabelle ist das Mindestalter für die Einwilligung der betroffenen Personen in die einzelnen Verordnungen aufgeführt, mit Hinweisen für weitere Informationen:

| Regelung | Alter des Einverständnisses | Anmerkungen |
| --- | --- | --- |
| CCPA (California) | 16 | <ul><li>Eine elterliche Einwilligung kann nur für Personen ab 13 Jahren erteilt werden.</li><li>Die Erhebung personenbezogener Daten von Personen unter 13 Jahren ist strengstens untersagt.</li></ul> |
| DSGVO (Europäische Union) | 16 | <ul><li>Einige Mitgliedstaaten der EU können zu diesem Zweck ein Gesetz für ein niedrigeres Alter vorsehen, das jedoch nicht unter 13 liegen darf.</li><li>Die Einwilligung der Eltern muss für alle betroffenen Personen unter dem Mindestalter erteilt werden.</li></ul> |
| LGPD (Brasilien) | 13 | <ul><li>Die Einwilligung der Eltern muss für alle betroffenen Personen unter dem Mindestalter erteilt werden.</li><li>Eine Einwilligung kann von einer 13- bis 18-jährigen natürlichen Person erteilt werden, solange die Verarbeitung ihrer personenbezogenen Daten in ihrem besten Interesse erfolgt.</li></ul> |
| PDPA (Thailand) | 10 | <ul><li>Die Einwilligung der Eltern muss für alle betroffenen Personen unter dem Mindestalter erteilt werden.</li></ul> |

<!-- | New Zealand [!DNL Privacy Act] | 16 | <ul><li>Parental consent must be provided for all data subjects below the age limit in cases where consent is required.</li></ul> | -->

### Wie viele Tage hat ein Unternehmen Zeit, um auf die Anfrage eines Verbrauchers hinsichtlich Zugriff auf oder Löschung personenbezogener Daten zu reagieren?

Wenn das Unternehmen personenbezogene Daten erfasst hat und die Identität eines bestimmten Verbrauchers authentifizieren oder überprüfen kann, ermöglichen die Datenschutzbestimmungen ein bestimmtes Zeitfenster, in dem eine Verbraucheranfrage erfüllt werden kann. In der folgenden Tabelle sind die geltenden Zeitfenster für jede Verordnung aufgeschlüsselt, mit einigen Ausnahmen:

>[!NOTE]
>
>Der Zeitrahmen, in dem in „Tagen“ reagiert werden muss, spiegelt die Fristen wider, die in jedem einzelnen Regulierungsgesetz für den Abschluss einer Verbraucheranfrage vorgesehen sind.

| Regelung | Zeitrahmen für die Antwort | Anmerkungen |
| --- | --- | --- |
| CCPA (California) | 45 Tage | |
| DSGVO (Europäische Union) | 30 Tage | |
| LGPD (Brasilien) | 15 Tage | |
| PDPA (Thailand) | 30 Tage | Wenn ein Unternehmen nicht innerhalb des Zeitfensters, in dem die betroffene Person ihre Anfrage erfüllt, auf die Anfrage antworten kann, verfügt das Unternehmen über eine zusätzliche Frist von 30 Tagen ab dem Datum, an dem es nicht in der Lage war, der betroffenen Person schriftlich zu antworten. |

<!-- | New Zealand [!DNL Privacy Act] | 20 working days | | -->

### Muss mein Unternehmen einen Datenschutzbeauftragten ernennen?

Wenn die Datenoperationen Ihres Unternehmens unter die rechtlichen Zuständigkeiten der DSGVO, der LGPD oder des PDPA fallen, müssen Sie in den folgenden Fällen einen Datenschutzbeauftragten (Data Protection Officer, DPO) ernennen:

* Ihre Organisation ist eine Behörde
* Ihr Unternehmen führt eine umfassende systematische Überwachung durch
* Ihre Organisation verarbeitet vertrauliche personenbezogene Daten in großem Umfang.

>[!IMPORTANT]
>
>Im Gegensatz zu anderen Vorschriften sieht der CCPA dies als Anforderung vor. Es wird jedoch allgemein empfohlen, dass ein Unternehmen, um die Einhaltung der Datenschutzbestimmungen zu gewährleisten, über eine qualifizierte individuelle Überwachung der Datenerfassung und Speicherung von Verbraucherdaten sowie über die Beantwortung von Kundenanfragen verfügen muss.

### Wie kann ich Datenschutzanfragen von Verbrauchern unterstützen, wenn ich Daten pflege, die von Datenschutzbestimmungen abgedeckt sind?

Sobald Sie die notwendigen Schritte zur Authentifizierung von Verbrauchern unternommen haben, die in die entsprechenden Rechtsordnungen fallen, können Sie mit Adobe Experience Platform Privacy Service Datenschutzanfragen von Verbrauchern an kompatible Experience Cloud-Anwendungen senden. Weitere Informationen finden [[!DNL Privacy Service]  in ](../home.md)Übersicht“. Informationen dazu, wie Ihre jeweiligen Experience Cloud-Anwendungen Datenschutzanfragen gerecht werden können, finden Sie im Handbuch zu [Privacy Service- und Experience Cloud-Anwendungen](../experience-cloud-apps.md).

>[!NOTE]
>
>Die kalifornische Regulierungsbehörde wird noch weitere Leitlinien dazu vorlegen, welche Arten von Daten für Datenschutzanfragen von Verbrauchern infrage kommen.

## CCPA-Fragen

Die folgenden Fragen beziehen sich speziell auf den CCPA.

### Wie gelten die verschiedenen Rollen und Verantwortlichkeiten des CCPA für Experience Cloud?

Gemäß der Definition des CCPA gelten für Adobe und seine Kunden folgende Rollen:

* Adobe-Kunden (die Parteien, die die Erfassung und Verwendung personenbezogener Daten von kalifornischen Einwohnern beantragen) würden als **Unternehmen** betrachtet.
* Adobe würde in seiner Rolle als Anbieter des Diensts als **Dienstleister** angesehen.

Als Dienstleister sammelt und verarbeitet Adobe personenbezogene Daten im Auftrag des Unternehmens und ist vertraglich dazu verpflichtet, diese Daten nur für die in der Vereinbarung festgelegten Zwecke zu verwenden.

Angesichts dieser Beziehung und der Vertragssprache der Adobe wären Offenlegungen gegenüber Adobe wahrscheinlich nicht als „Verkauf“ anzusehen, für den die Unternehmen eine Mitteilung vorlegen und um Zustimmung bitten müssten.

Adobe-Dienste können jedoch verwendet werden, um bestimmte Daten auszutauschen und Übertragungen an Dritte zu ermöglichen. Diese Übertragungen durch Dritte könnten als „Verkauf“ betrachtet werden und erforderten rechtlich eine Offenlegung und Zustimmung. Kunden sollten mit ihrem Rechtsbeistand zusammenarbeiten, um einzelne Anwendungsfälle hinsichtlich der geltenden Anforderungen auszuwerten.

### Bietet Adobe weitere Tools, die bei der Erfüllung von CCPA-Anforderungen hilfreich sein können?

Adobe Experience Cloud-Anwendungen verfügen über Daten-Management- und Data-Governance-Funktionen, die den Datenschutzbedarf von Unternehmen unterstützen können. Zu diesen Tools gehören die Kennzeichnung der Datennutzung, rollenbasierte Zugriffskontrollen, IP-Verschleierung und Hashing-Funktionen.

Adobe hat für seine Datenschutz- und Sicherheitsmaßnahmen verschiedene Zertifizierungen erhalten, z. B. eine ISO 27001-Zertifizierung und eine DSGVO-Validierung von TrustArc.

## DSGVO-Fragen

Die folgenden Fragen beziehen sich speziell auf die DSGVO.

### Was ist der Unterschied zwischen einer Verordnung und einer Richtlinie?

Eine **Verordnung** ist ein bindender legislativer Rechtsakt, der in der gesamten EU durchgesetzt wird. Eine **Richtlinie** ist ein Rechtsakt, der ein Ziel festlegt, das alle EU-Länder erreichen müssen. Es ist jedoch Sache der einzelnen Länder, darüber zu entscheiden, wie dies erfolgt.

Es ist wichtig zu beachten, dass es sich bei der DSGVO um eine Verordnung handelt, im Gegensatz zu den vorherigen Rechtsvorschriften (der Datenschutzrichtlinie), bei denen es sich um eine Richtlinie handelt.

### Wie wirkt sich die DSGVO auf die Richtlinie zu Datenverletzungen aus?

Vorgeschlagene Vorschriften zu Datenverstößen beziehen sich in erster Linie auf die Meldepflicht für Unternehmen, die nicht erfüllt wurde. Datenverstöße, die eine Gefahr für Einzelpersonen darstellen können, sind der Datenschutzbehörde innerhalb von 72 Stunden und betroffenen Personen unverzüglich mitzuteilen.

## PDPA-Fragen

Die folgenden Fragen beziehen sich speziell auf das PDPA.

### Was sind sensible personenbezogene Daten?

Das PDPA enthält strenge Anforderungen an die Erfassung und Speicherung sensibler personenbezogener Daten, die personenbezogene Daten umfassen, die sich auf die rassische oder ethnische Herkunft, politische Meinungen, religiöse oder philosophische Überzeugungen, Strafregister, Gewerkschaftsmitgliedschaften, genetische Daten, biometrische Daten, Gesundheitsakten und sexuelle Orientierung oder Präferenzen beziehen.
