---
keywords: Experience Platform;Startseite;beliebte Themen;Datenverwaltung;Datennutzungskennzeichnungs- API;Policy Service-API;Unterstützte Datennutzungskennzeichnungen;Vertragskennzeichnungen;Identitätskennzeichnungen;sensible Kennzeichnungen
solution: Experience Platform
title: Glossar der Datennutzungskennzeichnungen
description: In diesem Dokument werden alle derzeit von Adobe Experience Platform unterstützten Datennutzungskennzeichnungen beschrieben.
exl-id: 70d0702d-def7-4ab2-a861-eaf0f0cde1d4
source-git-commit: 7b15166ae12d90cbcceb9f5a71730bf91d4560e6
workflow-type: tm+mt
source-wordcount: '2108'
ht-degree: 100%

---

# Glossar der Datennutzungskennzeichnungen {#data-usage-labels-glossary}

>[!CONTEXTUALHELP]
>id="platform_policies_labeltype"
>title="Kennzeichnungstypen"
>abstract="Es gibt mehrere Kategorien von Datennutzungskennzeichnungen. Zu den von Adobe definierten Kennzeichnungen gehören Vertragskennzeichnungen, Identitätskennzeichnungen und vertrauliche Kennzeichnungen. Von Ihrem Unternehmen definierte Kennzeichnungen werden als benutzerdefinierte Kennzeichnungen kategorisiert."
>text="See the data usage labels glossary for more information on these label types."

Mit Datennutzungskennzeichnungen können Sie Datensätze und -felder anhand der für diese Daten geltenden [Governance-Richtlinien](../policies/overview.md) und [Richtlinien für die Zugriffssteuerung](../../access-control/abac/overview.md) kategorisieren. Adobe Experience Platform bietet mehrere gebrauchsfertige, grundlegende Datennutzungskennzeichnungen, die Sie verwenden können, um Ihre Daten zu kategorisieren.

In diesem Dokument werden die derzeit von Experience Platform bereitgestellten grundlegenden Datennutzungskennzeichnungen erläutert.

## Vertragsbezeichnungen

Vertragliche „C“-Bezeichnungen dienen zur Kategorisierung von Daten, die vertragliche Bestimmungen aufweisen oder mit Data Governance-Richtlinien Ihrer Organisation in Zusammenhang stehen.

| Kennzeichnung | Definition |
| --- | --- |
| [C1](#c1) | Die Daten können nur in aggregierter Form aus Adobe Experience Cloud exportiert werden, ohne dass dabei Einzel- oder Gerätekennungen einbezogen werden. |
| [C2](#c2) | Daten können nicht zu einem Drittanbieter exportiert werden. |
| [C3](#c3) | Daten können nicht mit direkt identifizierbaren Informationen kombiniert oder anderweitig verwendet werden. |
| [C4](#c4) | Daten können nicht für das Targeting von Anzeigen oder Inhalten verwendet werden, weder auf der Site noch Site-übergreifend. |
| [C5](#c5) | Daten können nicht für interessenbasiertes, Site-übergreifendes Targeting von Inhalten oder Anzeigen verwendet werden. |
| [C6](#c6) | Daten können nicht für das Targeting von Anzeigen auf der Site verwendet werden. |
| [C7](#c7) | Daten können nicht für das Targeting von Inhalten auf der Site verwendet werden. |
| [C8](#c8) | Daten können nicht zur Messung der Websites oder Apps Ihrer Organisation verwendet werden. |
| [C9](#c9) | Daten können nicht in Datenwissenschafts-Workflows verwendet werden. |
| [C10](#c10) | Daten können nicht für die Aktivierung einer zusammengesetzten Identität verwendet werden. |
| [C11](#c11) | Daten können nicht mit Segment Match-Partnern freigegeben werden. |
| [C12](#c12) | Daten können in keiner Weise exportiert werden. |

## Identitätsbezeichnungen

Identitätsbezogene „I“-Bezeichnungen dienen der Kategorisierung von Daten, mit denen sich eine bestimmte Person identifizieren oder kontaktieren lässt.

| Kennzeichnung | Definition |
| --- | --- |
| **I1** | Direkt identifizierbare Daten, mit denen eine bestimmte Person anstatt eines Geräts identifiziert oder kontaktiert werden kann. |
| **I2** | Indirekt identifizierbare Daten, die in Verbindung mit anderen Daten zur Identifizierung oder zum Kontakt mit einer bestimmten Person verwendet werden können. |

## Kennzeichnungen für sensible Daten {#sensitive}

Sensible „S“-Kennzeichnungen dienen dazu, Daten zu kategorisieren, die Sie und Ihre Organisation als sensibel betrachten.

Bei Daten, die Sie als sensibel betrachten, kann es sich um verschiedene Arten von geografischen Daten handeln; diese Kategorie ist jedoch nicht auf geografische Daten beschränkt.

| Kennzeichnung | Definition |
| --- | --- |
| **S1** | Daten zur Angabe von Breiten- und Längengrad, die zur Bestimmung der genauen Position eines Geräts verwendet werden können. |
| **S2** | Daten, die zur Bestimmung eines allgemein definierten Geofence-Bereichs verwendet werden können. |
| **PSPD** | Zulässige sensible und personenbezogene Daten (Permitted Sensitive Personal Data, PSPD) sind Daten, die von Adobe vertraglich zum Hochladen zugelassen werden und die vom geltenden Recht als „sensibel“, „besondere Datenkategorie“ oder Ähnliches erachtet werden. Hiervon ausgenommen sind insbesondere geschützte Gesundheitsinformationen (PHI) und andere regulierte Gesundheitsdaten. |
| **RHD** | Daten, die sich auf geschützte Gesundheitsinformationen (PHI) beziehen, oder Patienteninformationen, die von Adobe vertraglich zum Hochladen zugelassen sind. |

## Anhang

Die folgenden Abschnitte enthalten weitere Informationen zu den verfügbaren Datennutzungskennzeichnungen.

### Details zur Kennzeichnung von Verträgen

Die folgenden Abschnitte enthalten detaillierte Informationen zur Implementierung spezifischer „C“-Kennzeichnungen.

#### C1 {#c1}

Manche Daten können nur in aggregierter Form aus Adobe Experience Cloud exportiert werden, ohne dass dabei Einzel- oder Gerätekennungen einbezogen werden. Zum Beispiel Daten, die aus Social Media stammen.

#### C2 {#c2}

Einige Datenanbieter haben in ihren Verträgen Klauseln, die den Export von Daten von dort verbieten, wo sie ursprünglich erfasst wurden. So wird beispielsweise die Übertragung von Daten, die Sie von Social Media erhalten, oft durch deren Verträge eingeschränkt. Die C2-Kennzeichnung ist restriktiver als [C1](#c1), die nur eine Aggregation und anonyme Daten erfordert, jedoch weniger restriktiv als [C12](#c12), die Datenexporte unabhängig vom Ziel vollständig verbietet.

#### C3 {#c3}

Einige Datenanbieter haben Vertragsklauseln, die die Kombination oder Verwendung dieser Daten mit direkt identifizierbaren Informationen verbieten. Verträge für Daten, die von Werbenetzwerken, Werbe-Servern und Drittanbietern von Daten bezogen werden, enthalten beispielsweise oft spezifische vertragliche Verbote der Verwendung solcher Daten mit direkt identifizierbaren Daten.

#### C4 {#c4}

C4 umfasst die Kennzeichnungen [C5](#c5), [C6](#c6) und [C7](#c7). Hierbei handelt es sich um eine der restriktivsten Kennzeichnungen, nur [C12](#c12) ist noch restriktiver.

#### C5 {#c5}

Von interessenbasiertem Targeting bzw. Personalisierung spricht man, wenn die folgenden drei Bedingungen erfüllt sind: Die auf der Website gesammelten Daten werden (1) verwendet, um Rückschlüsse auf die Interessen von Benutzenden zu ziehen, (2) in einem anderen Kontext verwendet, z. B. auf einer anderen Website oder in einer App außerhalb der Website, UND (3) verwendet, um auszuwählen, welche Inhalte oder Anzeigen auf der Grundlage dieser Rückschlüsse geschaltet werden.

Die Kombination von Daten aus verschiedenen Sites, einschließlich einer Kombination aus Daten in einer Site und Offsite-Daten oder einer Kombination von Daten aus verschiedenen Offsite-Quellen, wird als „Site-übergreifende Daten“ bezeichnet. Verschiedene Sites stellen unterschiedliche Kontexte dar, sodass die Verwendung von Site-übergreifenden Daten in jedem Kontext anders ist als das Original. Site-übergreifende Daten werden in der Regel gesammelt und verarbeitet, um Rückschlüsse auf die Interessen der Benutzenden zu ziehen. Die Verwendung von Site-übergreifenden Daten zum Targeting von Anzeigen oder Inhalten gilt daher in der Regel als interessenbasiertes Targeting, unabhängig davon, ob die Anzeige oder der Inhalt auf der Site oder außerhalb der Site erscheint. Wenn z. B. Onsite-Daten in Kombination mit Offsite-Daten verwendet wurden, um auszuwählen, welche Anzeige einem/r Benutzenden auf der unternehmenseigenen Website angezeigt werden soll, würde diese Verwendung als interessenbasiertes Targeting gelten. Ein weiteres Beispiel: Das erneute Targeting von Anzeigen auf Benutzende außerhalb der Site würde wahrscheinlich auch als interessenbasiertes Targeting gelten.

Die Verwendung von Offsite-Daten allein für das Targeting würde wahrscheinlich ebenfalls als interessenbasiertes Targeting gelten, da Offsite-Daten in der Regel gesammelt und verarbeitet werden, um Rückschlüsse auf die Interessen der Benutzenden zu ziehen.

Beim Targeting von Inhalten oder Anzeigen, die ausschließlich Onsite-Daten verwenden, wird das Targeting jedoch in der Regel nicht als interessenbasiertes Targeting eingestuft. Ein Onsite-Targeting, das ansonsten nicht als interessenbasiertes Targeting gilt, wird als zwei unterschiedliche Kennzeichnungen gehandhabt. Die Kennzeichnung C6 befasst sich insbesondere mit dem Onsite-Targeting von Anzeigen und dem Reporting und bezieht sich speziell auf die Auswahl von Anzeigen, deren Bereitstellung und das Reporting, während sich die Kennzeichnung C7 auf die Inhaltsauswahl, die Bereitstellung und das Reporting jeweils auf der Site bezieht (Targeting von Inhalten auf der Site selbst).

Letztendlich liegt die Interpretation der Kennzeichnung und die Art und Weise, wie die Nutzung der Daten mit dieser Kennzeichnung erzwungen wird, bei Ihnen. Nachstehend sind die IAB- und DAA-Frameworks als Referenz aufgeführt:

IAB: Personalisierung. Die Erfassung und Verarbeitung von Informationen über Ihre Nutzung dieses Service zur späteren Personalisierung von Werbung und/oder Inhalten für Sie in anderen Kontexten, z. B. auf anderen Websites oder in Programmen, im Laufe der Zeit. Normalerweise wird der Inhalt der Site oder des Programms verwendet, um Rückschlüsse auf Ihre Interessen zu ziehen, die die zukünftige Auswahl von Werbung und/oder Inhalten beeinflussen.

DAA: auf dem Online-Verhalten basierende Werbung. Das Sammeln von Daten von einem bestimmten Computer oder Gerät in Bezug auf das Verhalten beim Betrachten von Web-Seiten im Laufe der Zeit und über Websites hinweg, die nicht zu Tochterunternehmen gehören, mit dem Ziel, diese Daten zur Vorhersage von Benutzervorlieben oder -interessen zu verwenden, um Werbung an diesen Computer oder dieses Gerät zu liefern, die auf Vorlieben oder Interessen basiert, welche aus diesem Verhalten beim Betrachten von Web-Seiten abgeleitet werden.

#### C6 {#c6}

Anzeigen sind Nachrichten oder Benachrichtigungen, einschließlich Text und Bildern, die auf einer Website oder in einem Programm erscheinen und in erster Linie dazu dienen, den Verkauf von Waren oder Dienstleistungen zu fördern. Es liegt an Ihnen, den Zweck solcher Nachrichten oder Benachrichtigungen zu bestimmen. Anzeigen sind von Inhalten auf der Site getrennt, welche durch die Kennzeichnung [C7](#c7) abgedeckt werden. Daten mit einer C6-Kennzeichnung können nicht für das Targeting von Anzeigen auf der Site verwendet werden, einschließlich der Auswahl und der Bereitstellung von Anzeigen auf den unternehmenseigenen Websites oder Apps oder zur Messung der Bereitstellung und der Effektivität solcher Anzeigen. Dazu gehört die Verwendung von zuvor erfassten Onsite-Daten über die Benutzerinteressen, um Anzeigen auszuwählen, Daten darüber zu verarbeiten, welche Anzeigen wann und wo angezeigt wurden, und um festzustellen, ob die Benutzenden irgendwelche Aktionen im Zusammenhang mit der Werbung ergriffen haben, wie z. B. das Klicken auf eine Anzeige oder das Tätigen eines Kaufs. In der Regel würden Rückschlüsse auf die Benutzerpräferenzen auf der Basis der Onsite-Aktivitäten der Benutzenden und die Verwendung dieser Präferenzen beim Targeting von Anzeigen auf der Site nicht als interessenbasiertes Targeting (auch Personalisierung genannt) eingestuft, da nicht alle drei erforderlichen Voraussetzungen für ein interessenbasiertes Targeting erfüllt wären. *[Diese Anforderungen finden Sie unter der Kennzeichnung C5.](#c5)*

Letztendlich liegt die Interpretation der Kennzeichnung und die Art und Weise, wie die Nutzung der Daten mit dieser Kennzeichnung erzwungen wird, bei Ihnen. Nachstehend sind die IAB- und DAA-Frameworks als Referenz aufgeführt:

IAB: 3. Anzeigenauswahl, Bereitstellung, Reporting: Die Erfassung von Informationen und die Kombination mit zuvor gesammelten Informationen, um Anzeigen für Sie auszuwählen und zu übermitteln und die Bereitstellung sowie die Effektivität solcher Anzeigen zu messen. Dazu gehören die Verwendung von zuvor erfassten Informationen über Ihre Interessen zur Auswahl von Anzeigen, die Verarbeitung von Daten darüber, welche Anzeigen angezeigt wurden, wie oft sie angezeigt wurden, wann und wo sie angezeigt wurden und ob Sie irgendwelche Aktionen im Zusammenhang mit der Werbung unternommen haben, wie z. B. das Klicken auf eine Anzeige oder das Tätigen eines Kaufs. Dies umfasst nicht die Personalisierung, d. h. die Erfassung und Verarbeitung von Informationen über Ihre Nutzung dieses Service, um später Werbung und/oder Inhalte in anderen Kontexten, wie Websites oder Programmen, für Sie personalisieren zu können.

DAA: Die auf dem Online-Verhalten basierende Werbung umfasst keine First-Party-Aktivitäten, die Bereitstellung oder das Reporting von Anzeigen oder kontextbezogene Werbung (d. h. Werbung, die auf dem Inhalt der besuchten Web-Seite, dem aktuellen Besuch einer Web-Seite durch den Verbraucher oder einer Suchanfrage basiert).

#### C7 {#c7}

Onsite-Inhalte sind Texte und Bilder, die zur Information, Ausbildung oder Unterhaltung konzipiert sind und nicht zur Förderung des Verkaufs von Waren oder Dienstleistungen erstellt wurden. Es liegt an Ihnen, den Zweck der Inhalte zu bestimmen, einschließlich der Frage, ob ein Inhalt als native Werbung gelten könnte. Die Kennzeichnung C7 ist nicht für Onsite-Anzeigen vorgesehen, da diese mit der Kennzeichnung [C6](#c6) versehen sind. Daten mit einer C7-Kennzeichnung können nicht für das Content-Targeting auf der Site verwendet werden, einschließlich der Auswahl und Bereitstellung von Inhalten auf den unternehmenseigenen Websites oder Apps oder zur Messung der Bereitstellung und der Effektivität solcher Inhalte. Dazu gehören zuvor erfasste Informationen über die Benutzerinteressen an ausgewählten Inhalten, die Verarbeitung von Daten darüber, welche Inhalte, wie oft, wie lange, wann und wo angezeigt wurden und ob die Benutzenden irgendwelche Aktionen im Zusammenhang mit dem Inhalt durchgeführt haben, beispielsweise Inhalte ausgewählt haben. In der Regel würden Rückschlüsse auf die Benutzerpräferenzen auf der Basis der Onsite-Aktivitäten der Benutzenden und die Verwendung dieser Präferenzen beim Content-Targeting auf der Site nicht als interessenbasiertes Targeting (auch Personalisierung genannt) eingestuft, da nicht alle drei erforderlichen Voraussetzungen für ein interessenbasiertes Targeting erfüllt wären. *[Diese Anforderungen finden Sie unter der Kennzeichnung C5.](#c5)*

Letztendlich liegt die Interpretation der Kennzeichnung und die Art und Weise, wie die Nutzung der Daten mit dieser Kennzeichnung erzwungen wird, bei Ihnen. Nachstehend sind die IAB- und DAA-Frameworks als Referenz aufgeführt:

IAB: 4. Inhaltsauswahl, Bereitstellung, Reporting: Die Erfassung von Informationen und deren Kombination mit zuvor erfassten Informationen, um Inhalte für Sie auszuwählen und bereitzustellen und die Bereitstellung und Effektivität solcher Inhalte zu messen. Dazu gehören die Verwendung von zuvor erfassten Informationen zu Ihren Interessen zur Auswahl von Inhalten, die Verarbeitung von Daten darüber, welche Inhalte angezeigt wurden, wie oft und wie lange sie angezeigt wurden, wann und wo sie angezeigt wurden und ob Sie im Zusammenhang mit dem Inhalt irgendwelche Aktionen durchgeführt haben, einschließlich beispielsweise des Klickens auf Inhalte. Dies umfasst nicht die Personalisierung, d. h. die Erfassung und Verarbeitung von Informationen über Ihre Nutzung dieses Service zur späteren Personalisierung von Inhalten und/oder Werbung für Sie in anderen Kontexten, wie Websites oder Programmen, im Laufe der Zeit.

DAA: Die auf dem Online-Verhalten basierende Werbung umfasst keine First-Party-Aktivitäten, die Bereitstellung oder das Reporting von Anzeigen oder kontextbezogene Werbung (d. h. Werbung, die auf dem Inhalt der besuchten Web-Seite, dem aktuellen Besuch einer Web-Seite durch den Verbraucher oder einer Suchanfrage basiert).

#### C8 {#c8}

Daten können nicht verwendet werden, um die Nutzung durch Benutzende der unternehmenseigenen Sites oder Apps zu messen, zu analysieren und Berichte darüber zu erstellen. Dies umfasst nicht das interessenbasierte Targeting (Site-übergreifendes Targeting), d. h. die Sammlung von Informationen über Ihre Nutzung dieses Services zur späteren Personalisierung von Inhalten und/oder Werbung für Sie in anderen Kontexten, z. B. auf anderen Websites oder in Programmen, im Laufe der Zeit.

#### C9 {#c9}

Einige Verträge beinhalten ein explizites Verbot der Datennutzung für datenwissenschaftliche Zwecke. Manchmal wird dies so ausgedrückt, dass die Verwendung von Daten für künstliche Intelligenz (KI), maschinelles Lernen (ML) oder Modellierung verboten ist.

#### C10 {#c10}

Einige Data-Governance-Richtlinien beschränken die Verwendung von Daten aus zusammengefügten Identitäten für die Personalisierung. Die Kennzeichnung C10 wird automatisch auf Segmente angewendet, wenn deren Zusammenführungsrichtlinien die Option „Privates Diagramm“ verwenden.

#### C11 {#c11}

Adobe Experience Platform Segment Match ermöglicht es Ihnen, Erstanbietersegmente mit Datenschutz- und Zustimmungsvoreinstellungen abzugleichen und so eine erweiterte Profilerstellung und nachgelagerte Einblicke zu ermöglichen. Die Bezeichnung „C11“ bezeichnet Daten, die nicht in [!DNL Segment Match]-Prozessen verwendet werden sollten. Nachdem Sie ermittelt haben, welche Datensätze und/oder Felder Sie aus Segment Match ausschließen möchten, und die C11-Bezeichnung entsprechend hinzugefügt haben, wird die Bezeichnung automatisch vom Segment Match-Arbeitsablauf erzwungen.

#### C12 {#c12}

Daten mit dieser Kennzeichnung können in keiner Weise aus Platform exportiert werden. Felder mit einer C12-Kennzeichnung sind von CSV-Downloads, der API-Nutzung und von Aktivierungs-Workflows ausgeschlossen.
