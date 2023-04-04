---
keywords: Experience Platform; Startseite; beliebte Themen; DSGVO; DSGVO; DSGVO; CCPA; ccpa; PDPA; pdpa; LGPD; lgpd; FAQ; FAQ; Regulierung; Regulierung; Verordnungen; Datenschutz; Datenschutz
solution: Experience Platform
title: Häufig gestellte Fragen zu Datenschutzbestimmungen
description: Dieses Dokument enthält Antworten auf häufig gestellte Fragen zu unterstützten gesetzlichen Datenschutzbestimmungen und deren Implementierung in Adobe Experience Cloud.
exl-id: ec553e53-664b-4e18-abb1-4e4063fdd2c9
source-git-commit: 7e86721f6dd6fd280ae7e7e67aca21b4258ffb66
workflow-type: tm+mt
source-wordcount: '1619'
ht-degree: 35%

---

# Häufig gestellte Fragen zu Datenschutzbestimmungen

Dieses Dokument enthält Antworten auf häufig gestellte Fragen zu unterstützten gesetzlichen Datenschutzbestimmungen und deren Implementierung in Adobe Experience Cloud.

>[!NOTE]
>
>Definitionen zu den verschiedenen in diesem Dokument verwendeten Begriffen finden Sie im Abschnitt [Terminologie zur Datenschutzbestimmung](terminology.md) Handbuch.

## Allgemeine Fragen

Die folgenden Fragen beziehen sich auf alle von Experience Cloud unterstützten Datenschutzbestimmungen.

### Auf wen wirken sich die unterstützten Datenschutzbestimmungen aus?

Die [Datenschutzbestimmungen, die von Experience Cloud unterstützt werden](./overview.md) gelten für alle Organisationen, die personenbezogene Daten von Bürgern innerhalb der jeweiligen Rechtsordnungen der jeweiligen Rechtsordnung speichern und verarbeiten, unabhängig vom geografischen Standort der Organisation.

### Was sind personenbezogene Daten?

Personenbezogene Daten sind alle Informationen, die eine natürliche Person (das „Datensubjekt“) betreffen und die zur direkten oder indirekten Identifikation dieser Person verwendet werden können. Dabei kann es sich um einen beliebigen Namen, ein Foto, eine E-Mail-Adresse, Bankdaten, Beiträge auf Social-Networking-Websites, medizinische Informationen oder eine Computer-IP-Adresse handeln.

Die folgenden Kennungen werden häufig in Experience Cloud-Anwendungen verwendet und können Datenschutzbestimmungen unterliegen:

* Name
* Postadresse
* Eindeutige personenbezogene Kennung
* Online-Kennung
* IP-Adresse
* E-Mail  Adresse
* Kontoname

Personenbezogene Daten können auch Informationen über Aktivitäten im Internet oder in anderen elektronischen Netzwerken umfassen. Dazu gehören unter anderem:

* Browser-Verlauf
* Suchverlauf
* Informationen zur Interaktion eines Verbrauchers mit einer Website, Anwendung oder Werbung

Obwohl die Datenschutzbestimmungen eine breite Palette personenbezogener Daten abdecken, schreiben die Standardvertragsbedingungen der Adobe vor, dass vertrauliche personenbezogene Daten (wie SSN, Führerscheininformationen, Finanzkontoinformationen und biometrische Daten) generell nicht importiert und in Experience Cloud-Anwendungen verwendet werden dürfen.

### Was ist der Unterschied zwischen einem Datenverantwortlichen und einem Datenverarbeiter?

Ein **Datenverantwortlicher** ist die Stelle, die die Ziele, Bedingungen und Wege der Verarbeitung personenbezogener Daten bestimmt, während der **Datenverarbeiter** eine Stelle ist, die personenbezogene Daten im Auftrag des Datenverantwortlichen verarbeitet.

A **Datenverantwortlicher** ist die Person oder Organisation, die befugt und dafür verantwortlich ist, Entscheidungen über die Erhebung, Verwendung oder Weitergabe personenbezogener Daten zu treffen. A **Datenprozessor** ist die Person oder Organisation, die im Zusammenhang mit der Erhebung, Verwendung oder Weitergabe der personenbezogenen Daten und der Leitung des Datenverantwortlichen tätig ist.

### Was ist der Unterschied zwischen der ausdrücklichen und eindeutigen Zustimmung der betroffenen Person?

**Explizite Zustimmung** bezieht sich auf einen Standard der Einwilligung, der eine spezifische, informierte und eindeutige Angabe der Wünsche der betroffenen Person in mündlicher oder schriftlicher Form umfasst. Einfach ausgedrückt muss die betroffene Person buchstäblich und explizit &quot;Ich stimme zu&quot;oder &quot;Ich stimme zu&quot;, damit die Einwilligung als explizit betrachtet wird. Darüber hinaus muss es so einfach sein, die Zustimmung zurückzuziehen, wie sie sein muss.

**Eindeutige (implizite) Zustimmung** bezieht sich auf die Einwilligung, die nicht explizit vom Datensubjekt erteilt wurde, jedoch eindeutig ist. Während des Anmeldeprozesses für eine Unternehmens-Website wird beispielsweise darauf hingewiesen, dass das Datensubjekt durch Angabe einer E-Mail-Adresse dem Empfang von E-Mails zu Sonderangeboten zustimmt. Wenn das Datensubjekt den Hinweis liest, reicht die positive Aktion der Eingabe seiner E-Mail aus, um als eindeutige Einwilligung betrachtet zu werden.

Bei vielen Vorschriften wie der DSGVO ist eine ausdrückliche Zustimmung für die Verarbeitung sensibler personenbezogener Daten erforderlich, wobei nur eine &quot;Opt-in&quot;-Klausel ausreicht. Für nicht vertrauliche Daten ist jedoch eine eindeutige (implizite) Zustimmung zulässig.

### Können Datensubjekte unter einem bestimmten Alter ihre Einwilligung geben?

In vielen Datenschutzbestimmungen ist festgelegt, dass betroffene Personen, die ein bestimmtes Alter nicht erreicht haben, keine Einwilligung zur Erhebung ihrer personenbezogenen Daten einholen können. Einige Verordnungen sehen vor, dass der Inhaber der elterlichen Verantwortung für die betroffene Person in diesen Fällen die Einwilligung erteilt, aber nicht in allen Fällen. In der folgenden Tabelle ist das Mindestalter für die Einwilligung von Datensubjekten in die einzelnen Verordnungen aufgeführt, wobei Hinweise für weitere Informationen beigefügt werden:

| Verordnung | Alter der Zustimmung | Anmerkungen |
| --- | --- | --- |
| CCPA (Kalifornien) | 16 | <ul><li>Die elterliche Zustimmung kann nur für Datensubjekte ab 13 Jahren erteilt werden.</li><li>Die Erhebung personenbezogener Daten von Personen unter 13 Jahren ist streng verboten.</li></ul> |
| DSGVO (Europäische Union) | 16 | <ul><li>Einige EU-Mitgliedstaaten können zu diesem Zweck ein Gesetz für ein niedrigeres Alter vorsehen, jedoch nicht weniger als 13.</li><li>Die elterliche Zustimmung muss für alle Datensubjekte unter der Altersgrenze erteilt werden.</li></ul> |
| LGPD (Brasilien) | 13 | <ul><li>Die elterliche Zustimmung muss für alle Datensubjekte unter der Altersgrenze erteilt werden.</li><li>Die Einwilligung kann von einer 13- bis 18-jährigen natürlichen Person erteilt werden, solange die Verarbeitung ihrer personenbezogenen Daten in ihrem besten Interesse erfolgt.</li></ul> |
| PDPA (Thailand) | 10 | <ul><li>Die elterliche Zustimmung muss für alle Datensubjekte unter der Altersgrenze erteilt werden.</li></ul> |

<!-- | New Zealand [!DNL Privacy Act] | 16 | <ul><li>Parental consent must be provided for all data subjects below the age limit in cases where consent is required.</li></ul> | -->

### Wie viele Tage hat ein Unternehmen Zeit, um auf die Anfrage eines Verbrauchers hinsichtlich Zugriff auf oder Löschung personenbezogener Daten zu reagieren?

Wenn das Unternehmen personenbezogene Daten gesammelt hat und die Identität eines bestimmten Verbrauchers authentifizieren oder überprüfen kann, können Datenschutzbestimmungen ein bestimmtes Zeitfenster für die Erfüllung einer Verbraucheranfrage vorsehen. In der folgenden Tabelle sind die Zeitfenster für jede Verordnung mit Anmerkungen zu einigen Ausnahmen aufgeführt:

>[!NOTE]
>
>Der Zeitrahmen für die Reaktion in &quot;Tagen&quot;spiegelt die Fristen wider, die jedes Regulierungsgesetz für die Erfüllung einer Verbraucheranfrage vorsieht.

| Verordnung | Zeitrahmen für die Antwort | Anmerkungen |
| --- | --- | --- |
| CCPA (Kalifornien) | 45 Tage |  |
| DSGVO (Europäische Union) | 30 Tage | Wenn die Anfrage komplex ist oder zahlreiche Anfragen von demselben Datensubjekt gestellt wurden, kann die Anfrage auf 60 Tage verlängert werden. |
| LGPD (Brasilien) | 15 Tage |  |
| PDPA (Thailand) | 30 Tage | Falls ein Unternehmen nicht innerhalb des Compliance-Fensters auf die Anfrage einer betroffenen Person antworten kann, hat das Unternehmen zusätzlich 30 Tage nach dem Datum, an dem es nicht in der Lage war, die Anfrage schriftlich an die betroffene Person zu beantworten. |

<!-- | New Zealand [!DNL Privacy Act] | 20 working days | | -->

### Muss mein Unternehmen einen Datenschutzbeauftragten ernennen?

Wenn die Datenoperationen Ihres Unternehmens unter die gesetzlichen Bestimmungen der DSGVO, der LGPD oder der PDPA fallen, müssen Sie in den folgenden Fällen einen Datenschutzbeauftragten (DPO) ernennen:

* Ihre Einrichtung ist eine Behörde
* Ihr Unternehmen führt eine umfassende systematische Überwachung durch
* Ihr Unternehmen verarbeitet personenbezogene Daten in großem Maßstab.

>[!IMPORTANT]
>
>Im Gegensatz zu anderen Verordnungen schreibt der CCPA dies als Anforderung vor. Es wird jedoch allgemein empfohlen, dass ein Unternehmen zur Wahrung der Datenschutzbestimmungen über eine qualifizierte individuelle Überwachung der Datenerfassung und -speicherung sowie über die Beantwortung von Kundenanfragen verfügen muss.

### Wie kann ich Datenschutzanfragen von Verbrauchern unterstützen, wenn ich Daten unterhalte, die unter Datenschutzbestimmungen fallen?

Nachdem Sie die erforderlichen Schritte zur Authentifizierung von Verbrauchern unternommen haben, die in die entsprechenden Rechtsordnungen fallen, können Sie mit Adobe Experience Platform Privacy Service Datenschutzanfragen von Verbrauchern an kompatible Experience Cloud-Apps senden. Weitere Informationen finden Sie in der [[!DNL Privacy Service] Übersicht. ](../home.md) Informationen dazu, wie Ihre jeweiligen Experience Cloud-Anwendungen Datenschutzanfragen gerecht werden können, finden Sie im Handbuch zu [Privacy Service- und Experience Cloud-Anwendungen](../experience-cloud-apps.md).

>[!NOTE]
>
>Die kalifornische Regulierungsbehörde wird weitere Bestimmungen dazu vorlegen, welche Arten von Daten für Datenschutzanfragen von Verbrauchern infrage kommen.

## CCPA-Fragen

Die folgenden Fragen beziehen sich speziell auf den CCPA.

### Wie gelten die verschiedenen Rollen und Verantwortlichkeiten des CCPA für Experience Cloud?

Gemäß der Definition des CCPA gelten für Adobe und seine Kunden folgende Rollen:

* Adobe-Kunden (die Parteien, die die Erfassung und Verwendung personenbezogener Daten von kalifornischen Einwohnern beantragen) würden als **Unternehmen** betrachtet.
* Adobe würde in seiner Rolle als Anbieter des Diensts als **Dienstleister** angesehen.

Als Dienstleister sammelt und verarbeitet Adobe personenbezogene Daten im Auftrag des Unternehmens und ist vertraglich dazu verpflichtet, diese Daten nur für die in der Vereinbarung festgelegten Zwecke zu verwenden.

Angesichts dieser Beziehung und der Vertragssprache der Adobe würden Offenlegungen an die Adobe wahrscheinlich nicht als &quot;Verkauf&quot;betrachtet, für den die Unternehmen eine Bekanntmachung vorlegen und eine Zustimmung beantragen müssten.

Adobe-Dienste können jedoch verwendet werden, um bestimmte Daten auszutauschen und Übertragungen an Dritte zu ermöglichen. Diese Übertragungen Dritter könnten als &quot;Verkauf&quot;betrachtet werden und erfordern rechtlich die Offenlegung und Zustimmung. Kunden sollten mit ihrem Rechtsbeistand zusammenarbeiten, um einzelne Anwendungsfälle hinsichtlich der geltenden Anforderungen zu evaluieren.

### Bietet Adobe weitere Tools, die bei der Erfüllung von CCPA-Anforderungen hilfreich sein können?

Adobe Experience Cloud-Anwendungen verfügen über Daten-Management- und Data-Governance-Funktionen, die den Datenschutzbedarf von Unternehmen unterstützen können. Zu diesen Tools gehören die Kennzeichnung der Datennutzung, rollenbasierte Zugriffskontrollen, IP-Verschleierung und Hashing-Funktionen.

Adobe hat für seine Datenschutz- und Sicherheitsmaßnahmen verschiedene Zertifizierungen erhalten, z. B. eine ISO 27001-Zertifizierung und eine DSGVO-Validierung von TrustArc.

## DSGVO-Fragen

Die folgenden Fragen beziehen sich speziell auf die DSGVO.

### Was ist der Unterschied zwischen einer Verordnung und einer Richtlinie?

Eine **Verordnung** ist ein bindender legislativer Rechtsakt, der in der gesamten EU durchgesetzt wird. Eine **Richtlinie** ist ein Rechtsakt, der ein Ziel festlegt, das alle EU-Länder erreichen müssen. Es ist jedoch Sache der einzelnen Länder, darüber zu entscheiden, wie dies erfolgt.

Es ist wichtig festzustellen, dass es sich bei der DSGVO um eine Verordnung handelt, während es sich bei den früheren Rechtsvorschriften (Datenschutzrichtlinie) um eine Richtlinie handelte.

### Wie wirkt sich die DSGVO auf die Richtlinie zu Datenverletzungen aus?

Vorgeschlagene Vorschriften zu Datenverstößen beziehen sich in erster Linie auf die Meldepflicht für Unternehmen, die nicht erfüllt wurde. Datenverstöße, die eine Gefahr für Einzelpersonen darstellen können, sind der Datenschutzbehörde innerhalb von 72 Stunden und betroffenen Personen unverzüglich mitzuteilen.

## PDPA-Fragen

Die folgenden Fragen beziehen sich speziell auf die PDPA.

### Was sind sensible personenbezogene Daten?

Die PDPA enthält strenge Anforderungen an die Erfassung und Speicherung sensibler personenbezogener Daten, die personenbezogene Daten zu folgenden Themen umfassen: rassischer oder ethnischer Herkunft, politische Meinungen, religiöse oder philosophische Überzeugungen, Strafregister, Gewerkschaftsmitgliedschaften, genetische Daten, biometrische Daten, Gesundheitsakten sowie sexuelle Orientierung oder Präferenzen.
