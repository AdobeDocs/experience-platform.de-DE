---
solution: Experience Platform
title: Look-alike-Zielgruppen
description: Erfahren Sie, wie Sie neue hochwertige Zielgruppen in Adobe Experience Platform mit Look-alike-Zielgruppen ansprechen.
exl-id: c43dac6c-18a0-482f-803e-b75e1b211e98
source-git-commit: c2f9bcd9aeb0073b8b26413ec29e2dff1ee5c80d
workflow-type: tm+mt
source-wordcount: '2192'
ht-degree: 10%

---

# Handbuch für Look-alike-Zielgruppen

>[!IMPORTANT]
>
>Look-alike-Einblicke und Look-alike-Zielgruppen sind nur in der **B2C-Edition** verfügbar.

In Adobe Experience Platform bieten Look-alike-Zielgruppen intelligente Einblicke in jede Ihrer Zielgruppen, indem sie auf maschinellem Lernen basierende Einblicke nutzen, um hochwertige Kunden mit Ihren Marketingkampagnen zu identifizieren und anzusprechen.

Mit Look-alike-Zielgruppen können Sie erweiterte Zielgruppen erstellen, die Kunden ähnlich Ihren leistungsstarken Zielgruppen ansprechen oder Kunden ähnlich wie zuvor konvertierten Zielgruppen ansprechen.

## Terminologie {#terminology}

Bevor Sie mit Look-alike-Zielgruppen beginnen, sollten Sie sich mit den folgenden Konzepten vertraut machen:

- **Basiszielgruppe**: Die Basiszielgruppe ist die Zielgruppe, über die Sie weitere Einblicke erhalten möchten. Dies ist die Zielgruppe, auf der das Look-alike-Modell **basiert** ist.
- **Look-alike-Modell**: Ein Look-alike-Modell ist ein Modell für maschinelles Lernen, das für jede qualifizierte Zielgruppe ohne Kundeneingabe trainiert wird. Jedes Look-alike-Modell erstellt die einflussreichen Faktoren und Ähnlichkeitsdiagramme. Ein Look-alike-Modell wird mit **nicht** bewertet.
- **Look-alike-Zielgruppe**: Eine Look-alike-Zielgruppe ist die Zielgruppe, die erstellt wird, wenn ein Look-alike-Modell mit einem ausgewählten Ähnlichkeitsschwellenwert auf die Basiszielgruppe angewendet wird. Sie können mehrere Look-alike-Zielgruppen mit demselben Look-alike-Modell erstellen. Die Look-alike-Zielgruppe wird bewertet.
- **Gesamte adressierbare Zielgruppengröße**: Die gesamte adressierbare Zielgruppengröße ist die Gesamtanzahl der Profile in den letzten 30 Tagen abzüglich der Basiszielgruppe in den letzten 30 Tagen. Wenn beispielsweise ein Kunde in den letzten 30 Tagen 10 Millionen Profile hat und die Basiszielgruppe in den letzten 30 Tagen 1 Million Profile hat, beträgt die gesamte adressierbare Zielgruppengröße 9 Millionen Profile.

## Eignung {#eligibility}

Um Look-alike-Einblicke zu verwenden, muss die Basiszielgruppe **1} die folgenden Eignungskriterien erfüllen:**

- Die Basiszielgruppe **muss** in Platform erstellt werden.
   - Nach außen generierte Zielgruppen sind **nicht** für Look-alike-Einblicke geeignet.
- Die Basiszielgruppe &quot;**must**&quot; befindet sich in der standardmäßigen Zusammenführungsrichtlinie.
- Die Basiszielgruppe **darf** keine Felder verwenden, die durch Data Governance eingeschränkt sind.

## Look-alike-Modell – Details {#details}

>[!CONTEXTUALHELP]
>id="platform_audiences_lookAlike_notEligible"
>title="Nicht berechtigt"
>abstract="Diese Zielgruppe ist derzeit nicht für Look-alike-Einblicke qualifiziert, da sie möglicherweise weniger als die Mindestanzahl von Profilen enthält, die für das Training erforderlich sind, oder der Profilexport noch nicht ausgelöst wurde."

>[!CONTEXTUALHELP]
>id="platform_audiences_lookAlike_processing"
>title="Verarbeitung läuft"
>abstract="Diese Zielgruppe wird derzeit verarbeitet. Die Verarbeitung des Modells kann bis zu 24 Stunden dauern. Bitte versuchen Sie es später erneut."

>[!CONTEXTUALHELP]
>id="platform_audiences_lookAlike_error"
>title="Fehler"
>abstract="Bei der Verarbeitung dieses Modells ist ein Fehler aufgetreten. Bitte löschen Sie dieses Modell und erstellen es neu oder versuchen Sie es später erneut."

In Adobe Experience Platform verbraucht das Look-alike-Modell drei verschiedene Arten von Datenpunkten:

- Zielgruppenmitgliedschaft in den letzten 30 Tagen
- Erlebnisereignisse der letzten 30 Tage, die im Echtzeit-Kundenprofil erfasst wurden
- Profilattribute über die letzten 30 Tage, die im Echtzeit-Kundenprofil erfasst wurden

Alle diese Datenpunkte werden in Schlüsselwertpaare umgewandelt, die in das Look-alike-Modell eingespeist werden. Nur die Schlüsselwertpaare mit einem signifikanten Prozentsatz an Profilübereinstimmungen werden beibehalten.

Derzeit wird das Look-alike-Modell alle 24 Stunden ausgeführt, wobei die Einflussfaktoren und Ähnlichkeitsdiagramme für die Basiszielgruppen erstellt und neu erstellt werden. Die Auswertung für die Look-alike-Zielgruppen wird ebenfalls häufig ausgeführt.

## Berechtigungen {#entitlements}

Die folgenden Berechtigungen gelten für die Verwendung von Look-alike-Zielgruppen:

- Real-Time CDP Prime-Kunden haben in Produktions-Sandboxes Anspruch auf aktive Look-alike-Zielgruppen vom Typ **5**
- Real-Time CDP Ultimate-Kunden haben die Berechtigung für aktive Look-alike-Zielgruppen in Produktions-Sandboxes **20** .
- Entwicklungs-Sandboxes sind auf **5** Look-alike-Zielgruppen für alle Real-Time CDP-Kunden beschränkt.

Add-On-Pakete, die zu einem späteren Zeitpunkt verfügbar sein werden, erhöhen die Berechtigungen für Produktions-Sandboxes um 20 Look-alike-Zielgruppen pro Paket.

Wenden Sie sich an Ihren Adobe-Kundenbetreuer, um zu bestätigen, ob Sie Zugriff auf Look-alike-Zielgruppen haben.

## Look-alike-Einblicke anzeigen {#view}

Look-alike-Einblicke sind in die Seite mit den Zielgruppendetails integriert. Um die Look-alike-Einblicke einer Zielgruppe anzuzeigen, wählen Sie in der linken Navigationsleiste **[!UICONTROL Zielgruppen]** , gefolgt von **[!UICONTROL Durchsuchen]** und der Zielgruppe, für die Sie die Einblicke anzeigen möchten.

![Die Schaltfläche &quot;Zielgruppen&quot;wird hervorgehoben sowie die Basiszielgruppe, die für die Look-alike-Modellierung verwendet wird.](../images/ui/lookalike-audiences/browse.png)

Die Seite mit den Details zur Zielgruppe wird angezeigt. Wählen Sie die Registerkarte **[!UICONTROL Look-alike Insights]** aus, um die Look-alike-Einblicke der Zielgruppe anzuzeigen. Die Seite **[!UICONTROL Look-alike Insights]** wird angezeigt. Diese Seite enthält drei Hauptelemente: die Ähnlichkeit und das Reichweitendiagramm, die Look-alike-Zielgruppen und die Einflussfaktoren.

![Die Registerkarte &quot;Look-alike-Insights&quot;wird hervorgehoben und zeigt die Look-alike-Einblicke für die Basiszielgruppe an.](../images/ui/lookalike-audiences/look-alike-insights.png)

### Ähnlichkeit und Reichweite {#similarity-and-reach}

>[!CONTEXTUALHELP]
>id="platform_audiences_lookAlike_similarityAndReach"
>title="Ähnlichkeit und Reichweite"
>abstract="Das Ähnlichkeits- und Reichweitendiagramm zeichnet die erwartete Reichweite einer Look-alike-Zielgruppe aus Profilen über einem bestimmten Ähnlichkeitswert auf. Sie können den Mauszeiger über einen bestimmten Punkt im Diagramm bewegen, um den Prozentsatz der Ähnlichkeit und die erwartete Profilanzahl für den aktuell hervorgehobenen Punkt anzuzeigen."

Der Abschnitt &quot;Ähnlichkeit und Reichweite&quot;zeigt ein Diagramm an, das die erwartete Reichweite einer Look-alike-Zielgruppe abbildet, die aus Profilen über einem bestimmten Ähnlichkeitswert besteht. Der Ähnlichkeitswert stellt den **Abstand** der Ähnlichkeit zwischen dem Profil der Basiszielgruppe und dem Profil des Look-alike-Insight dar.

![Die Ähnlichkeit und das Reichweitendiagramm werden hervorgehoben.](../images/ui/lookalike-audiences/similarity-and-reach.png)

In diesem Diagramm misst die X-Achse den Prozentsatz der Ähnlichkeit zwischen einem Profil und Mitgliedern der ausgewählten Zielgruppe. Der Ähnlichkeitswert liegt im Bereich von 0 % bis 100 %, wobei ein höherer Ähnlichkeitswert angibt, dass ein Profil in Bezug auf einflussreiche Faktorwerte näher an Mitgliedern der ausgewählten Zielgruppe liegt.

Die Y-Achse zeigt die erwartete Anzahl von Profilen mit dem Ähnlichkeitsprozentsatz an, der dem entsprechenden Wert der x-Achse entspricht. Die erwartete Anzahl von Profilen reicht von 0 bis zur gesamten adressierbaren Zielgruppengröße oder 25 Millionen Profile, je nachdem, welcher Wert niedriger ist. Diese Achse wird auf einer **logarithmischen Skala** gemessen, um die Lesbarkeit des Diagramms zu verbessern.

Beachten Sie, dass das Diagramm von rechts nach links **kumulativ** ist. Das bedeutet, dass der Wert der Y-Achse an jedem Punkt im Diagramm die Anzahl der Profile ist, die eine Ähnlichkeit von **über** und dem Schwellenwert für Ähnlichkeit aufweisen. Wenn die X-Achse beispielsweise bei 60 % und die Y-Achse bei 10 Millionen liegt, bedeutet dies, dass es 10 Millionen Profile gibt, die eine Ähnlichkeit von mindestens 60 % mit der Basiszielgruppe aufweisen.

Sie können den Mauszeiger über einen bestimmten Punkt im Diagramm bewegen, um den Prozentsatz der Ähnlichkeit und die erwartete Profilanzahl für den aktuell hervorgehobenen Punkt anzuzeigen.

### Lookalike-Zielgruppen {#list}

Im Abschnitt Look-alike-Zielgruppen wird eine Liste aller Look-alike-Zielgruppen angezeigt, die zuvor für die ausgewählte Basiszielgruppe erstellt wurden.

![Der Abschnitt &quot;Look-alike-Audiences&quot;ist hervorgehoben.](../images/ui/lookalike-audiences/select-laa.png)

### Einflussfaktoren {#influential-factors}

>[!CONTEXTUALHELP]
>id="platform_audiences_lookAlike_influentialFactors"
>title="Einflussfaktoren"
>abstract="Einflussfaktoren sind Attribute, Ereignisse und Zielgruppenmitgliedschaften, die wichtig sind, um die Ähnlichkeit eines Profils mit Mitgliedern der Basiszielgruppe zu erklären. Datennutzungskennzeichnungen und -richtlinien können verwendet werden, um bestimmte Daten davon auszuschließen, in Look-alike-Modellen als Einflussfaktoren betrachtet zu werden."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/lookalike-audiences.html?lang=de#exclude" text="Ausschließen von Daten"

Im Abschnitt Einflussfaktoren werden die 100 wichtigsten Faktoren angezeigt, die das Look-alike-Modell für die ausgewählte Basiszielgruppe beeinflussen. Diese Einflussfaktoren sind die Profilattribute, die Erlebnisereignisse und die Zielgruppenmitgliedschaften, die bei der Erläuterung der Ähnlichkeiten in der Basiszielgruppe am wichtigsten sind. Wenn Sie die wichtigsten Einflussfaktoren verstehen, können Sie Ihren Marketing-Inhalt für diese Zielgruppe und alle daraus erstellten Look-alike-Zielgruppen besser personalisieren. Beachten Sie, dass nicht alle Einflussfaktoren angezeigt werden, die sich auf das Look-alike-Modell auswirken.

Bei numerischen Einflussfaktoren können die Schlüsselwertpaare je nach der Anzahl der verschiedenen Werte, die dieser Schlüssel hat, in Behälter zusammengefasst werden. Wenn Sie beispielsweise den Schlüssel `income` haben, wären höchstwahrscheinlich viele eindeutige Werte vorhanden. Daher werden die Schlüsselwertpaare in Behälter platziert, die wie `income=[0 -> 30000]`, `income=[30000 -> 50000]` und `income=[50000 -> 100000]` aussehen könnten.

Diese Behälter werden regelmäßig neu berechnet, um sicherzustellen, dass die Daten auf dem neuesten Stand gehalten werden.

![Der Abschnitt zu Einflussfaktoren wird hervorgehoben.](../images/ui/lookalike-audiences/influential-factors.png)

>[!NOTE]
>
>Die Einflussfaktoren werden nach Wichtigkeit geordnet und voneinander unabhängig.

| Feld | Beschreibung |
| ----- | ----------- |
| Typ | Der Datentyp, aus dem der Einflussfaktor abgeleitet wird. Dabei kann es sich um ein Profilattribut, ein Erlebnisereignis oder eine Zielgruppenmitgliedschaft handeln. |
| Schlüssel | Der Name des Datenfelds. Bei Schlüsseln des Zielgruppen-Mitgliedschaftstyps stellt dieser Wert den **Namespace** der Zielgruppe dar, aus der die Daten stammen. Mögliche Werte sind `ups` (Segmentation Service) und `AO` (Audience Orchestration). Bei Schlüsseln anderer Typen stellt dieser Wert den XDM-Feldpfad dar. Wenn das Unternehmen Luma beispielsweise über ein benutzerdefiniertes Feld namens &quot;Einkommen&quot;verfügt, wäre der Schlüssel `_luma.income` |
| Wert | Der Wert variiert je nach Einflussfaktor, den er darstellt. Bei Profilattributen oder Erlebnisereignissen stellt dieses Feld den Wert oder den Wertebereich des Datenfelds dar, das die Ähnlichkeit mit den Mitgliedern der Basiszielgruppe anzeigt. Der Wertebereich wird in das Format `[A -> B]` geschrieben, wobei `A` den unteren Bereich darstellt, während `B` den höheren Bereich darstellt. Bei Zielgruppenmitgliedschaften ist dieses Feld der Name der Zielgruppe. |
| Wichtigkeit | Die relative Wichtigkeit des Einflussfaktors. Dies kann hoch, mittel oder niedrig sein. |

## Erstellen einer Look-alike-Zielgruppe {#create}

>[!IMPORTANT]
>
>Sie **können** keine Look-alike-Zielgruppe als Basiszielgruppe für eine andere Look-alike-Zielgruppe verwenden. Das heißt, Sie **können** keine verketteten Look-alike-Zielgruppen erstellen.

Um eine Look-alike-Zielgruppe zu erstellen, müssen Sie die Zielgruppe auswählen, auf der die Look-alike-Zielgruppe basieren soll. Um auf Ihre Liste der verfügbaren Zielgruppen zuzugreifen, wählen Sie in der linken Navigationsleiste **[!UICONTROL Zielgruppen]** und danach **[!UICONTROL Durchsuchen]** aus. Die Liste der Zielgruppen wird angezeigt. Auf dieser Seite können Sie die Zielgruppe auswählen, die Sie als Basiszielgruppe verwenden möchten.

![Die Schaltfläche &quot;Zielgruppen&quot;wird hervorgehoben sowie die Basiszielgruppe, die für die Look-alike-Modellierung verwendet wird.](../images/ui/lookalike-audiences/browse.png)

Wählen Sie auf der Seite mit den Zielgruppendetails die Option **[!UICONTROL Look-alike-Audience erstellen]** aus, um mit der Erstellung einer Look-alike-Audience zu beginnen.

![ Die Schaltfläche [!UICONTROL Look-alike-Audience erstellen] ist hervorgehoben.](../images/ui/lookalike-audiences/create-look-alike-audience.png)

Das Popup **[!UICONTROL Erstellen einer Look-alike-Audience]** wird angezeigt. Auf dieser Seite können Sie den Prozentsatz der Ähnlichkeit für die Look-alike-Zielgruppe festlegen.

![Das Popup [!UICONTROL Erstellen einer Look-alike-Audience] wird angezeigt.](../images/ui/lookalike-audiences/create-audience.png)

Sie können diesen Prozentsatz für die Ähnlichkeit auf drei verschiedene Arten festlegen:

- Verschieben Sie den Regler, um den Ähnlichkeitsprozentsatz festzulegen.
- Geben Sie im numerischen Eingabefeld neben dem Regler den Prozentsatz der Ähnlichkeit ein.
- Bewegen Sie den Mauszeiger über das Diagramm und wählen Sie die gewünschte Position aus, um den Ähnlichkeitsprozentsatz festzulegen.

Sie können auch Details zur Look-alike-Zielgruppe aktualisieren, einschließlich Name und Beschreibung. Standardmäßig wird der Name der Look-alike-Zielgruppe basierend auf dem Namen der Basiszielgruppe und dem zuvor angegebenen Ähnlichkeitsprozentsatz generiert.

![Die grundlegenden Informationen werden im Popup-Fenster [!UICONTROL Look-alike-Audience erstellen] hervorgehoben.](../images/ui/lookalike-audiences/basic-info.png)

Wählen Sie **[!UICONTROL Erstellen]** aus, um die Erstellung Ihrer Look-alike-Zielgruppe abzuschließen.

![Die Schaltfläche &quot;Erstellen&quot;wird im Popup-Fenster [!UICONTROL Look-alike-Audience erstellen] hervorgehoben.](../images/ui/lookalike-audiences/create-audience.png)

Die neu erstellte Look-alike-Zielgruppe kann im Abschnitt **[!UICONTROL Look-alike-Zielgruppen]** der Seite mit den Zielgruppendetails aufgerufen werden und ist auch im Zielgruppenportal und für andere nachgelagerte Anwendungen verfügbar. Bitte beachten Sie, dass es einige Zeit dauern wird, bis die Look-alike-Zielgruppe bewertet wird. Bis die Profilanzahl erreicht ist, scheint sie 0 zu sein.

## Anzeigen von Look-alike-Zielgruppendetails {#view-details}

Um Details einer Look-alike-Zielgruppe anzuzeigen, wählen Sie die Look-alike-Zielgruppe im Abschnitt **[!UICONTROL Look-alike-Audiences]** der Basiszielgruppe aus.

![Der Abschnitt &quot;Look-alike-Audiences&quot;ist hervorgehoben.](../images/ui/lookalike-audiences/select-laa.png)

Die Seite mit den Details zur Zielgruppe wird angezeigt. Weitere Informationen zu dieser Seite finden Sie im Abschnitt [Zielgruppendetails der Audience Portal-Übersicht](./audience-portal.md#audience-details).

![Details der Look-alike-Zielgruppe werden angezeigt.](../images/ui/lookalike-audiences/laa-details.png)

## Ausschließen von Datenfeldern aus der Look-alike-Modellierung {#exclude}

>[!IMPORTANT]
>
> **Sie** sind dafür verantwortlich, sicherzustellen, dass Daten, einschließlich vertraulicher Daten, angemessen gekennzeichnet werden und dass die Datennutzungsrichtlinien definiert und in die Lage versetzt wurden, die rechtlichen und regulatorischen Verpflichtungen einzuhalten, unter denen Sie tätig sind. Beachten Sie außerdem, dass die Datenfelder oder Segmentmitgliedschaften, die **nicht** direkt mit Datenfeldern korrelieren, die normalerweise mit sensiblen oder geschützten Datentypen verknüpft sind, eine Quelle möglicher Voreinstellungen sein können. **Sie** sind für die Analyse Ihrer Daten verantwortlich, um die entsprechenden Datennutzungsrichtlinien zu identifizieren, zu beschriften und auf Ihre Daten anzuwenden, einschließlich aller Datenfelder, die für vertrauliche oder geschützte Datentypen gelten und von der Modellierung ausgeschlossen werden sollten.

Look-alike-Zielgruppen können so konfiguriert werden, dass Datenfelder ausgeschlossen werden, die für die Marketing-Aktion &quot;Data Science&quot;eingeschränkt sind, indem die relevanten Datennutzungsbezeichnungen und -richtlinien angewendet werden. Daten, die als für die Datenwissenschaft eingeschränkt gekennzeichnet sind, werden beim Trainieren eines Look-alike-Zielgruppenmodells und beim Generieren einer Look-alike-Zielgruppe aus dem trainierten Modell nicht berücksichtigt. 

>[!NOTE]
>
>Änderungen an den Datennutzungsbezeichnungen der Basiszielgruppe können bis zu 48 Stunden in Kraft treten.

Die standardmäßige Bezeichnung &quot;C9&quot;kann verwendet werden, um Daten zu beschriften, die nicht für die Datenwissenschaft verwendet werden sollten, und kann durch Aktivierung der standardmäßigen Richtlinie &quot;Datenwissenschaft beschränken&quot;durchgesetzt werden. Sie können auch zusätzliche Richtlinien erstellen, um Daten mit anderen Bezeichnungen, einschließlich sensibler Bezeichnungen, aus der Nutzung für die Datenwissenschaft zu beschränken. Weitere Informationen zum Verwalten von Datennutzungsrichtlinien finden Sie im Handbuch [Benutzeroberflächen-Richtlinien zur Datennutzung](../../data-governance/policies/user-guide.md) . Weitere Informationen zum Verwalten von Datennutzungsbezeichnungen finden Sie im [UI-Handbuch für Datennutzungsbezeichnungen](../../data-governance/labels/user-guide.md).

Wenn eine Basiszielgruppe keine Vertragsbezeichnungen hat, schließt der Modellierungsprozess für Look-alike-Zielgruppen standardmäßig das Feld, den Datensatz oder die Zielgruppe **any** aus, basierend auf der aktivierten Datenschutzrichtlinie für Ihr Unternehmen.

## Nächste Schritte

Nach dem Lesen dieses Handbuchs haben Sie gelernt, wie Sie Look-alike-Einblicke anzeigen und auf Grundlage dieser Einblicke Look-alike-Zielgruppen erstellen können. Weiterführende Informationen zu Zielgruppen in der Adobe Experience Platform-Benutzeroberfläche finden Sie im Handbuch [Segmentation Service UI guide](./overview.md) .
