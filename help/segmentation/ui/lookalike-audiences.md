---
solution: Experience Platform
title: Look-alike-Zielgruppen
description: Erfahren Sie, wie Sie mit Look-alike-Audiences neue hochwertige Zielgruppen in Adobe Experience Platform ansprechen können.
badgeLimitedAvailability: label="Eingeschränkte Verfügbarkeit" type=Caution
source-git-commit: 4bd26857d2c714cd629fc46dbb9b6da6a29358c8
workflow-type: tm+mt
source-wordcount: '2123'
ht-degree: 1%

---


# Handbuch zu Look-alike-Zielgruppen

>[!IMPORTANT]
>
>Beachten Sie, dass Look-alike-Einblicke und Look-alike-Zielgruppen in **begrenzte Verfügbarkeit**.

In Adobe Experience Platform bieten Look-alike-Zielgruppen intelligente Einblicke in jede Ihrer Zielgruppen und nutzen auf maschinellem Lernen basierende Einblicke, um hochwertige Kunden mit Ihren Marketingkampagnen zu identifizieren und anzusprechen.

Mit Look-alike-Zielgruppen können Sie erweiterte Zielgruppen erstellen, die Kunden ähnlich Ihren leistungsstarken Zielgruppen ansprechen oder Kunden ähnlich wie zuvor konvertierten Zielgruppen ansprechen.

## Terminologie {#terminology}

Bevor Sie mit Look-alike-Zielgruppen beginnen, sollten Sie sich mit den folgenden Konzepten vertraut machen:

- **Basiszielgruppe**: Die Basiszielgruppe ist die Zielgruppe, über die Sie weitere Einblicke erhalten möchten. Dies ist die Zielgruppe, die das Look-alike-Modell ist **basiert** auf.
- **Look-alike-Modell**: Ein Look-alike-Modell ist ein Modell für maschinelles Lernen, das für jede berechtigte Zielgruppe ohne Kundeneingabe trainiert wird. Jedes Look-alike-Modell erstellt die einflussreichen Faktoren und Ähnlichkeitsdiagramme. Ein Look-alike-Modell **not** werden.
- **Look-alike-Zielgruppe**: Eine Look-alike-Zielgruppe ist die Zielgruppe, die erstellt wird, wenn ein Look-alike-Modell mit einer ausgewählten Ähnlichkeitsschwelle auf die Basiszielgruppe angewendet wird. Sie können mehrere Look-alike-Zielgruppen mit demselben Look-alike-Modell erstellen. Die Look-alike-Zielgruppe wird bewertet.
- **Gesamte adressierbare Zielgruppengröße**: Die gesamte adressierbare Zielgruppengröße ist die Gesamtanzahl der Profile in den letzten 30 Tagen abzüglich der Basiszielgruppe in den letzten 30 Tagen. Wenn beispielsweise ein Kunde in den letzten 30 Tagen 10 Millionen Profile hat und die Basiszielgruppe in den letzten 30 Tagen 1 Million Profile hat, beträgt die gesamte adressierbare Zielgruppengröße 9 Millionen Profile.

## Look-alike-Modelldetails {#details}

In Adobe Experience Platform verbraucht das Look-alike-Modell drei verschiedene Arten von Datenpunkten:

- Zielgruppenmitgliedschaft in den letzten 30 Tagen
- Erlebnisereignisse der letzten 30 Tage, die im Echtzeit-Kundenprofil erfasst wurden
- Profilattribute über die letzten 30 Tage, die im Echtzeit-Kundenprofil erfasst wurden

Alle diese Datenpunkte werden in Schlüsselwertpaare umgewandelt, die in das Look-alike-Modell eingespeist werden. Nur die Schlüsselwertpaare mit einem signifikanten Prozentsatz an Profilübereinstimmungen werden beibehalten.

Derzeit wird das Look-alike-Modell alle 24 Stunden ausgeführt, wobei die Einflussfaktoren und Ähnlichkeitsdiagramme für die Basiszielgruppen erstellt und neu erstellt werden. Die Auswertung für die Look-alike-Zielgruppen wird ebenfalls häufig ausgeführt.

## Berechtigungen {#entitlements}

Die folgenden Berechtigungen gelten für die Verwendung von Look-alike-Zielgruppen:

- Real-Time CDP Prime-Kunden sind berechtigt **5** Aktive Look-alike-Zielgruppen in Produktions-Sandboxes
- Real-Time CDP Ultimate-Kunden sind berechtigt, **20** Aktive Look-alike-Zielgruppen in Produktions-Sandboxes
- Entwicklungs-Sandboxes sind auf **5** Look-alike-Zielgruppen für alle Real-Time CDP-Kunden

Add-On-Pakete, die zu einem späteren Zeitpunkt verfügbar sein werden, erhöhen die Berechtigungen für Produktions-Sandboxes um 20 Look-alike-Zielgruppen pro Paket.

Um zu bestätigen, ob Sie Zugriff auf Look-alike-Audiences haben, wenden Sie sich an Ihren Adobe-Kundenbetreuer.

## Look-alike-Einblicke anzeigen {#view}

>[!CONTEXTUALHELP]
>id="platform_audiences_lookAlike_notEligible"
>title="Nicht förderfähig"
>abstract="Diese Zielgruppe ist derzeit nicht für Look-alike-Einblicke qualifiziert, da sie möglicherweise weniger als die Mindestanzahl von Profilen enthält, die für die Schulung erforderlich sind, oder der Profilexport noch nicht ausgelöst wurde."

>[!CONTEXTUALHELP]
>id="platform_audiences_lookAlike_processing"
>title="Verarbeitung läuft"
>abstract="Diese Zielgruppe wird derzeit verarbeitet. Die Verarbeitung des Modells kann bis zu 24 Stunden dauern. Bitte überprüfen Sie es später noch einmal."

>[!CONTEXTUALHELP]
>id="platform_audiences_lookAlike_error"
>title="Fehler"
>abstract="Bei der Verarbeitung dieses Modells ist ein Fehler aufgetreten. Bitte löschen und erstellen Sie dieses Modell neu oder versuchen Sie es später erneut."

Look-alike-Einblicke sind in die Seite mit den Zielgruppendetails integriert. Um die Look-alike-Einblicke einer Zielgruppe anzuzeigen, wählen Sie **[!UICONTROL Zielgruppen]** in der linken Navigationsleiste, gefolgt von **[!UICONTROL Durchsuchen]** und der Zielgruppe, für die Sie die Einblicke anzeigen möchten.

![Die Schaltfläche Zielgruppen wird hervorgehoben sowie die Basiszielgruppe, die für die Look-alike-Modellierung verwendet wird.](../images/ui/lookalike-audiences/browse.png)

Die Seite mit den Details zur Zielgruppe wird angezeigt. Auswählen **[!UICONTROL Look-alike-Erkenntnisse]** -Registerkarte, um die Look-alike-Einblicke der Zielgruppe anzuzeigen. Die **[!UICONTROL Look-alike-Erkenntnisse]** angezeigt. Diese Seite enthält drei Hauptelemente: die Ähnlichkeit und das Reichweitendiagramm, die Look-alike-Zielgruppen und die Einflussfaktoren.

![Die Registerkarte Look-alike-Einblicke wird hervorgehoben und zeigt die Look-alike-Einblicke für die Basiszielgruppe an.](../images/ui/lookalike-audiences/look-alike-insights.png)

### Ähnlichkeit und Reichweite {#similarity-and-reach}

>[!CONTEXTUALHELP]
>id="platform_audiences_lookAlike_similarityAndReach"
>title="Ähnlichkeit und Reichweite"
>abstract="Die Ähnlichkeit und das Reichweitendiagramm zeichnen die erwartete Reichweite einer Look-alike-Zielgruppe aus Profilen über einem bestimmten Ähnlichkeitswert auf. Sie können den Mauszeiger über einen bestimmten Punkt im Diagramm bewegen, um den Prozentsatz der Ähnlichkeit und die erwartete Profilanzahl für den aktuell hervorgehobenen Punkt anzuzeigen."

Der Abschnitt &quot;Ähnlichkeit und Reichweite&quot;zeigt ein Diagramm an, das die erwartete Reichweite einer Look-alike-Zielgruppe abbildet, die aus Profilen über einem bestimmten Ähnlichkeitswert besteht. Der Ähnlichkeitswert stellt die **Distanz** Ähnlichkeit zwischen dem Profil der Basiszielgruppe und dem Profil des Look-alike-Insight.

![Die Ähnlichkeit und das Reichweitendiagramm werden hervorgehoben.](../images/ui/lookalike-audiences/similarity-and-reach.png)

In diesem Diagramm misst die X-Achse den Prozentsatz der Ähnlichkeit zwischen einem Profil und Mitgliedern der ausgewählten Zielgruppe. Der Ähnlichkeitswert liegt im Bereich von 0 % bis 100 %, wobei ein höherer Ähnlichkeitswert angibt, dass ein Profil in Bezug auf einflussreiche Faktorwerte näher an Mitgliedern der ausgewählten Zielgruppe liegt.

Die Y-Achse zeigt die erwartete Anzahl von Profilen mit dem Ähnlichkeitsprozentsatz an, der dem entsprechenden Wert der x-Achse entspricht. Die erwartete Anzahl von Profilen reicht von 0 bis zur gesamten adressierbaren Zielgruppengröße oder 25 Millionen Profile, je nachdem, welcher Wert niedriger ist. Diese Achse wird anhand einer **Logarithmische Skala** , um die Lesbarkeit des Diagramms zu verbessern.

Beachten Sie, dass das Diagramm **kumulativ** von rechts nach links. Das bedeutet, dass der Wert der Y-Achse an jedem Punkt im Diagramm die Anzahl der Profile mit einer Ähnlichkeit ist **above** den Schwellenwert für Ähnlichkeit. Wenn die X-Achse beispielsweise bei 60 % und die Y-Achse bei 10 Millionen liegt, bedeutet dies, dass es 10 Millionen Profile gibt, die eine Ähnlichkeit von mindestens 60 % mit der Basiszielgruppe aufweisen.

Sie können den Mauszeiger über einen bestimmten Punkt im Diagramm bewegen, um den Prozentsatz der Ähnlichkeit und die erwartete Profilanzahl für den aktuell hervorgehobenen Punkt anzuzeigen.

### Look-alike-Zielgruppen {#list}

Im Abschnitt Look-alike-Zielgruppen wird eine Liste aller Look-alike-Zielgruppen angezeigt, die zuvor für die ausgewählte Basiszielgruppe erstellt wurden.

![Der Abschnitt &quot;Look-alike-Zielgruppen&quot;wurde hervorgehoben.](../images/ui/lookalike-audiences/select-laa.png)

### Einflussfaktoren {#influential-factors}

>[!CONTEXTUALHELP]
>id="platform_audiences_lookAlike_influentialFactors"
>title="Einflussfaktoren"
>abstract="Einflussfaktoren sind Attribute, Ereignisse und Zielgruppenmitgliedschaften, die für die Erklärung der Ähnlichkeit eines Profils mit Mitgliedern der Basiszielgruppe wichtig sind. Datennutzungsbezeichnungen und -richtlinien können verwendet werden, um bestimmte Daten davon auszuschließen, in Look-alike-Modellen als Einflussfaktoren betrachtet zu werden."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/lookalike-audiences.html?lang=en#exclude" text="Ausschließen von Daten"

Im Abschnitt Einflussfaktoren werden die 100 wichtigsten Faktoren angezeigt, die das Look-alike-Modell für die ausgewählte Basiszielgruppe beeinflussen. Diese Einflussfaktoren sind die Profilattribute, die Erlebnisereignisse und die Zielgruppenmitgliedschaften, die bei der Erläuterung der Ähnlichkeiten in der Basiszielgruppe am wichtigsten sind. Wenn Sie die wichtigsten Einflussfaktoren verstehen, können Sie Ihre Marketing-Inhalte für diese Zielgruppe und alle daraus erstellten Look-alike-Zielgruppen besser personalisieren. Beachten Sie, dass nicht alle Einflussfaktoren angezeigt werden, die sich auf das Look-alike-Modell auswirken.

Bei numerischen Einflussfaktoren können die Schlüsselwertpaare je nach der Anzahl der verschiedenen Werte, die dieser Schlüssel hat, in Behälter zusammengefasst werden. Wenn Sie beispielsweise einen Schlüssel von `income`, wären höchstwahrscheinlich viele eindeutige Werte vorhanden. Daher werden die Schlüssel-Wert-Paare in Buckets platziert, die wie folgt aussehen könnten: `income=[0 -> 30000]`, `income=[30000 -> 50000]`, und `income=[50000 -> 100000]`.

Diese Behälter werden regelmäßig neu berechnet, um sicherzustellen, dass die Daten auf dem neuesten Stand gehalten werden.

![Der Abschnitt Einflussfaktoren wird hervorgehoben.](../images/ui/lookalike-audiences/influential-factors.png)

>[!NOTE]
>
>Die Einflussfaktoren werden nach Wichtigkeit geordnet und voneinander unabhängig.

| Feld | Beschreibung |
| ----- | ----------- |
| Typ | Der Datentyp, aus dem der Einflussfaktor abgeleitet wird. Dabei kann es sich um ein Profilattribut, ein Erlebnisereignis oder eine Zielgruppenmitgliedschaft handeln. |
| Schlüssel | Der Name des Datenfelds. Bei Schlüsseln des Zielgruppen-Mitgliedschaftstyps stellt dieser Wert die **namespace** der Audience, aus der die Daten stammen. Mögliche Werte sind `ups` (Segmentation Service) und `AO` (Zielgruppen-Orchestrierung). Bei Schlüsseln anderer Typen stellt dieser Wert den XDM-Feldpfad dar. Wenn das Unternehmen Luma beispielsweise über ein benutzerdefiniertes Feld namens &quot;Einkommen&quot;verfügt, wäre der Schlüssel: `_luma.income` |
| Wert | Der Wert variiert je nach Einflussfaktor, den er darstellt. Bei Profilattributen oder Erlebnisereignissen stellt dieses Feld den Wert oder den Wertebereich des Datenfelds dar, das die Ähnlichkeit mit den Mitgliedern der Basiszielgruppe anzeigt. Der Wertebereich wird in das Formular geschrieben `[A -> B]`, wobei `A` stellt den unteren Bereich dar, während `B` stellt den höheren Bereich dar. Bei Zielgruppenmitgliedschaften ist dieses Feld der Name der Zielgruppe. |
| Wichtigkeit | Die relative Wichtigkeit des Einflussfaktors. Dies kann hoch, mittel oder niedrig sein. |

## Erstellen einer Look-alike-Zielgruppe {#create}

>[!IMPORTANT]
>
>You **cannot** Verwenden Sie eine Look-alike-Zielgruppe als Basiszielgruppe für eine andere Look-alike-Zielgruppe. Das heißt, Sie **cannot** verkettete Look-alike-Zielgruppen erstellen.

Um eine Look-alike-Zielgruppe zu erstellen, müssen Sie die Zielgruppe auswählen, auf der die Look-alike-Zielgruppe basieren soll. Um auf Ihre Liste der verfügbaren Zielgruppen zuzugreifen, wählen Sie **[!UICONTROL Zielgruppen]** in der linken Navigationsleiste, gefolgt von **[!UICONTROL Durchsuchen]**. Die Liste der Zielgruppen wird angezeigt. Auf dieser Seite können Sie die Zielgruppe auswählen, die Sie als Basiszielgruppe verwenden möchten.

![Die Schaltfläche Zielgruppen wird hervorgehoben sowie die Basiszielgruppe, die für die Look-alike-Modellierung verwendet wird.](../images/ui/lookalike-audiences/browse.png)

Wählen Sie auf der Seite mit den Zielgruppendetails die Option **[!UICONTROL Erstellen einer Look-alike-Zielgruppe]** , um mit der Erstellung einer Look-alike-Zielgruppe zu beginnen.

![Die [!UICONTROL Erstellen einer Look-alike-Zielgruppe] -Schaltfläche markiert ist.](../images/ui/lookalike-audiences/create-look-alike-audience.png)

Die **[!UICONTROL Erstellen einer Look-alike-Zielgruppe]** Popover angezeigt. Auf dieser Seite können Sie den Prozentsatz der Ähnlichkeit für die Look-alike-Zielgruppe festlegen.

![Die [!UICONTROL Erstellen einer Look-alike-Zielgruppe] Popover angezeigt.](../images/ui/lookalike-audiences/create-audience.png)

Sie können diesen Prozentsatz für die Ähnlichkeit auf drei verschiedene Arten festlegen:

- Verschieben Sie den Regler, um den Ähnlichkeitsprozentsatz festzulegen.
- Geben Sie im numerischen Eingabefeld neben dem Regler den Prozentsatz der Ähnlichkeit ein.
- Bewegen Sie den Mauszeiger über das Diagramm und wählen Sie die gewünschte Position aus, um den Ähnlichkeitsprozentsatz festzulegen.

Sie können auch Details zur Look-alike-Zielgruppe aktualisieren, einschließlich Name und Beschreibung. Standardmäßig wird der Name der Look-alike-Zielgruppe basierend auf dem Namen der Basiszielgruppe und dem zuvor angegebenen Ähnlichkeitsprozentsatz generiert.

![Die grundlegenden Informationen werden im Abschnitt [!UICONTROL Erstellen einer Look-alike-Zielgruppe] Popover.](../images/ui/lookalike-audiences/basic-info.png)

Auswählen **[!UICONTROL Erstellen]** , um die Erstellung Ihrer Look-alike-Zielgruppe abzuschließen.

![Die Schaltfläche &quot;Erstellen&quot;wird im [!UICONTROL Erstellen einer Look-alike-Zielgruppe] Popover.](../images/ui/lookalike-audiences/create-audience.png)

Auf die neu erstellte Look-alike-Zielgruppe kann im **[!UICONTROL Look-alike-Zielgruppen]** auf der Seite mit den Zielgruppendetails und ist auch im Zielgruppenportal und für andere nachgelagerte Verwendungen verfügbar. Bitte beachten Sie, dass es einige Zeit dauern wird, bis die Look-alike-Zielgruppe bewertet wird. Bis die Profilanzahl erreicht ist, scheint sie 0 zu sein.

## Look-alike-Zielgruppendetails anzeigen {#view-details}

Um Details einer Look-alike-Zielgruppe anzuzeigen, wählen Sie die Look-alike-Zielgruppe im **[!UICONTROL Look-alike-Zielgruppen]** der Basiszielgruppe.

![Der Abschnitt &quot;Look-alike-Zielgruppen&quot;wurde hervorgehoben.](../images/ui/lookalike-audiences/select-laa.png)

Die Seite mit den Details zur Zielgruppe wird angezeigt. Weitere Informationen auf dieser Seite finden Sie im [Abschnitt mit Zielgruppendetails des UI-Handbuchs für den Segmentation Service](./overview.md#audience-details).

![Details der Look-alike-Zielgruppe werden angezeigt.](../images/ui/lookalike-audiences/laa-details.png)

## Ausschließen von Datenfeldern aus der Look-alike-Modellierung {#exclude}

Look-alike-Zielgruppen können so konfiguriert werden, dass Datenfelder ausgeschlossen werden, die für die Marketing-Aktion &quot;Data Science&quot;eingeschränkt sind, indem die relevanten Datennutzungsbezeichnungen und -richtlinien angewendet werden. Daten, die als für die Datenwissenschaft eingeschränkt gekennzeichnet sind, werden beim Trainieren eines Look-alike-Zielgruppenmodells und beim Generieren einer Look-alike-Zielgruppe aus dem trainierten Modell nicht berücksichtigt. 

Die standardmäßige Bezeichnung &quot;C9&quot;kann verwendet werden, um Daten zu beschriften, die nicht für die Datenwissenschaft verwendet werden sollten, und kann durch Aktivierung der standardmäßigen Richtlinie &quot;Datenwissenschaft beschränken&quot;durchgesetzt werden. Sie können auch zusätzliche Richtlinien erstellen, um Daten mit anderen Bezeichnungen, einschließlich sensibler Bezeichnungen, aus der Nutzung für die Datenwissenschaft zu beschränken. Weitere Informationen zur Verwaltung von Datennutzungsrichtlinien finden Sie im Abschnitt [Benutzeroberflächenleitfaden für Datennutzungsrichtlinien](../../data-governance/policies/user-guide.md). Weitere Informationen zur Verwaltung von Datennutzungsbezeichnungen finden Sie im Abschnitt [Benutzerhandbuch zu den Datennutzungsbezeichnungen](../../data-governance/labels/user-guide.md).

Standardmäßig wird der Modellierungsprozess für Look-alike-Audiences ausgeschlossen **any** -Feld, Datensatz oder Zielgruppe basierend auf der aktivierten Datenschutzrichtlinie für Ihr Unternehmen. Wenn die Basiszielgruppe keine Vertragsbezeichnungen hat, wird der Modellierungsprozess **any** -Feld, Datensatz oder Zielgruppe basierend auf der aktivierten Datenschutzrichtlinie für Ihr Unternehmen.

Bitte beachten Sie, dass **you** sind dafür verantwortlich sicherzustellen, dass Daten, einschließlich sensibler Daten, angemessen gekennzeichnet werden und dass Datennutzungsrichtlinien definiert wurden und es ermöglicht wird, die rechtlichen und regulatorischen Verpflichtungen einzuhalten, unter denen Sie tätig sind. Sie sollten auch wissen, dass Datenfelder oder Segmentmitgliedschaften, die **not** die direkte Korrelation mit Datenfeldern, die normalerweise mit sensiblen oder geschützten Datentypen verknüpft sind, kann eine potenzielle Verzerrung darstellen. **You** sind für die Analyse Ihrer Daten verantwortlich, um die entsprechenden Datennutzungsrichtlinien zu identifizieren, zu beschriften und auf Ihre Daten anzuwenden, einschließlich aller Datenfelder, die für vertrauliche oder geschützte Datentypen geeignet sind und von der Modellierung ausgeschlossen werden sollten.

## Nächste Schritte

Nach dem Lesen dieses Handbuchs haben Sie gelernt, wie Sie Look-alike-Einblicke anzeigen und Look-alike-Zielgruppen erstellen können, die auf diesen Einblicken basieren. Weitere Informationen zu Zielgruppen in der Benutzeroberfläche von Adobe Experience Platform finden Sie im Abschnitt [Handbuch zur Benutzeroberfläche des Segmentierungsdienstes](./overview.md).
