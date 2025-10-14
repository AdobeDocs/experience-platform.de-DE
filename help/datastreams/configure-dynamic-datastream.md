---
title: Erstellen dynamischer Datenstromkonfigurationen
description: Erfahren Sie, wie Sie dynamische Datenstromkonfigurationen erstellen, um Ihre Daten auf der Grundlage von Regeln an verschiedene Experience Cloud-Services weiterzuleiten.
hide: true
hidefromtoc: true
badge: label="Beta" type="Informative"
exl-id: 528ddf89-ad87-4021-b5a6-8e25b4469ac4
source-git-commit: 8ce5b6718861d01731b9aab9f81645f2aeb2970f
workflow-type: tm+mt
source-wordcount: '1160'
ht-degree: 4%

---

# Erstellen dynamischer Datenstromkonfigurationen

>[!AVAILABILITY]
>
>* Die Option zum Definieren dynamischer Datenstromkonfigurationen ist derzeit in Beta verfügbar und steht einer begrenzten Anzahl von Kunden zur Verfügung. Wenden Sie sich an Ihren Adobe-Support-Mitarbeiter, um Zugriff auf diese Funktion zu erhalten. Dokumentation und Funktionalitäten können sich ändern.

Standardmäßig sendet Experience Platform Edge Network alle Ereignisse, die einen Datenstrom erreichen, an alle Experience Cloud [Services](configure.md#add-services) die Sie für Ihre Datenströme aktiviert haben. Je nach Anwendungsfall ist dies möglicherweise nicht immer der ideale Workflow für Sie.

Dynamische Datenstromkonfigurationen decken dieses Problem durch benutzerkonfigurierbare Regelsätze ab, die Sie für jeden für Ihren Datenstrom aktivierten Service definieren. Diese bestimmen, welche Experience Cloud-Lösung die einzelnen Datentypen erhalten soll.

## Voraussetzungen {#prerequisites}

Um eine dynamische Konfiguration für Ihren Datenstrom zu erstellen, müssen Sie zwei Bedingungen erfüllen:

* Es muss *mindestens* Datenstrom erstellt worden sein, mit dem Sie arbeiten können. Detaillierte Informationen finden Sie in der Dokumentation [&#x200B; Erstellen &#x200B;](configure.md) Datenstroms .
* Es muss *mindestens* ein Experience Cloud-Service zu Ihrem Datenstrom hinzugefügt werden. Detaillierte Informationen finden Sie in der Dokumentation [&#x200B; Hinzufügen eines &#x200B;](configure.md#add-services) zu einem Datenstrom .

Nachdem Sie einen Datenstrom erstellt und ihm einen Experience Cloud-Service hinzugefügt haben, können Sie [eine dynamische Konfiguration erstellen](#create-dynamic-configuration).

## Leitlinien {#guardrails}

Dynamische Datenstromkonfigurationen weisen bestimmte Beschränkungen und Leistungsbeschränkungen auf, um eine optimale Systemleistung und Datenverarbeitungseffizienz sicherzustellen. Die folgenden Leitplanken gelten für die Konfiguration dynamischer Datenstromregeln:

| Leitplanke | Limit | Art des Limits |
|---------|------------|------|
| Maximale Anzahl dynamischer Datenstromkonfigurationen pro Datenstrom für Experience Platform-Services | 5 | Leistungs-Schutzmaßnahme |
| Maximale Anzahl dynamischer Datenstromkonfigurationen pro Datenstrom für die Ereignisweiterleitung | 5 | Leistungs-Schutzmaßnahme |
| Maximale Anzahl dynamischer Datenstromkonfigurationen pro Datenstrom für Adobe Analytics | 5 | Leistungs-Schutzmaßnahme |
| Maximale Anzahl dynamischer Datenstromkonfigurationen pro Datenstrom für Adobe Target | 5 | Leistungs-Schutzmaßnahme |
| Maximale Anzahl dynamischer Datenstromkonfigurationen pro Datenstrom für Adobe Audience Manager | 5 | Leistungs-Schutzmaßnahme |
| Maximale Anzahl von Bedingungen (Prädikate), die in einer einzigen Regel kombiniert werden können | 100 | Leistungs-Schutzmaßnahme |
| Maximal zulässige Zeit für die Auswertung aller dynamischen Datenstromkonfigurationen pro Datenstrom vor Ablauf der Zeit | 25 ms | Vom System erzwungene Leitplanken |

## Überschreibungen der dynamischen Datenstromkonfigurationen im Vergleich zur Datenstromkonfiguration {#dynamic-versus-overrides}

Dynamische Datenstromkonfigurationen und [Überschreibungen der Datenstromkonfiguration](overrides.md) schließen sich gegenseitig aus.

Das bedeutet, dass Sie keine dynamischen Datenstromkonfigurationen zusammen mit Überschreibungen der Datenstromkonfiguration verwenden können. Sie müssen entweder das eine oder das andere wählen.

Wenn Sie sowohl Überschreibungen der dynamischen Datenstromkonfigurationen als auch der Datenstromkonfiguration aktivieren, haben die Überschreibungen der Konfiguration Vorrang und die Regeln für die dynamische Datenstromkonfiguration werden ignoriert.

## Erstellen einer dynamischen Datenstromkonfiguration {#create-dynamic-configuration}

Nachdem Sie [einen Datenstrom erstellt](configure.md) und [einen Service hinzugefügt](configure.md#add-services) haben, führen Sie die folgenden Schritte aus, um eine dynamische Konfiguration zum Service hinzuzufügen.

1. Gehen Sie zur **[!UICONTROL Datenerfassung]** > **[!UICONTROL Datenströme]** und wählen Sie den von Ihnen erstellten Datenstrom aus.

   ![Bild der Benutzeroberfläche für Datenströme mit der Liste der Datenströme.](assets/configure-dynamic-datastream/select-datastream.png)

1. Wählen Sie die **[!UICONTROL Bearbeiten]** für den Service aus, für den Sie eine dynamische Konfiguration definieren möchten.

   ![Abbildung der Benutzeroberfläche für Datenströme mit den zu einem Datenstrom hinzugefügten Services.](assets/configure-dynamic-datastream/select-service.png)

1. Wählen Sie auf der **[!UICONTROL Konfigurieren]** die Option **[!UICONTROL Dynamische Konfiguration speichern und bearbeiten]** aus.

   ![Abbildung der Benutzeroberfläche für Datenströme mit der Seite zur Datenstromkonfiguration.](assets/configure-dynamic-datastream/save-and-edit.png)

1. Wählen **[!UICONTROL Dynamische Konfiguration hinzufügen]** aus.

   ![Abbildung der Benutzeroberfläche für Datenströme mit der dynamischen Konfiguration ohne Meldung „Regel hinzugefügt“.](assets/configure-dynamic-datastream/add-dynamic-config.png)

1. Ziehen Sie die Elemente **[!UICONTROL mit denen Sie Ihre Regel erstellen möchten, aus dem Bedienfeld]** Ressourcen“ auf die rechte Seite des Fensters. Sie können mehrere Ressourcen kombinieren, um komplexe Regeln zu erstellen.

   Verwenden Sie die Optionen jeder Ressource, z **[!UICONTROL B. „gleich]**, **[!UICONTROL nicht gleich]**, **[!UICONTROL vorhanden]** und mehr, um Ihre Regeln zu optimieren.

   ![Bild der Benutzeroberfläche für Datenströme mit der dynamischen Konfigurationsregel.](assets/configure-dynamic-datastream/drag-resources.png)

1. Schalten **[!UICONTROL im Abschnitt]** die Services ein, die Sie für jede Regel aktivieren oder deaktivieren möchten, je nachdem, ob Sie möchten, dass die Daten an jeden Service gesendet werden. Wenn Sie den Umschalter deaktivieren, wird das Service-Routing deaktiviert und *keine Daten* werden an den Upstream-Service gesendet.

   ![Bild der Benutzeroberfläche für Datenströme mit der dynamischen Konfigurationsregel.](assets/configure-dynamic-datastream/enable-service.png)

1. Wenn Sie die Konfiguration Ihrer Regeln abgeschlossen haben, klicken Sie auf **[!UICONTROL Speichern]**.

## Überlegungen zur Regelpriorität {#considerations}

Für jede Konfiguration eines dynamischen Datenstroms können Sie mehrere Regeln definieren. Wenn Ihre Daten jedoch den Bedingungen mehrerer Regeln entsprechen, wird nur die erste übereinstimmende Regel in der Liste berücksichtigt und alle anderen übereinstimmenden Regeln werden ignoriert.

Achten Sie zum Erzielen des gewünschten Daten-Routing-Verhaltens auf die Reihenfolge, in der Sie die Regeln anordnen.

Um die Regelreihenfolge zu konfigurieren, können Sie die Regelfenster in die gewünschte Reihenfolge ziehen.

![GIF, das zeigt, wie die Reihenfolge der Regeln durch Ziehen und Ablegen geändert werden kann.](assets/configure-dynamic-datastream/move-rules.gif)

## Eignungskriterien für Regeln {#eligibility-criteria}

Dynamische Datenstromkonfigurationen müssen bestimmte Eignungskriterien erfüllen, um eine hohe Leistung, Wartbarkeit und Klarheit zu gewährleisten. Im Folgenden finden Sie die wichtigsten Anforderungen und Best Practices für die Definition von Regeln.

### Unterstützte Datentypen {#supported-data-types}

Regeln für die dynamische Datenstromkonfiguration arbeiten mit bestimmten Datentypen, um eine optimale Leistung und ein zuverlässiges Daten-Routing sicherzustellen. Wenn Sie verstehen, welche Datentypen unterstützt werden, können Sie effektive Regeln erstellen, mit denen Ihre Daten effizient verarbeitet werden.

| Datentyp | Status | Anmerkungen |
|-----------|--------|-------|
| String | Zugelassen | – |
| Zahl (Integer, Long, Short, Byte) | Zugelassen | – |
| Enum | Zugelassen | – |
| Boolesch | Zugelassen | – |
| Datum | Zugelassen | – |
| Array | Nicht zulässig | Auf Arrays basierende Regeln werden nicht unterstützt, da sie die Leistung beeinträchtigen können. |
| Zuordnung | Nicht zulässig | Regeln, die auf Zuordnungen basieren, werden nicht unterstützt, da sie die Leistung beeinträchtigen können. |

### Unterstützte Operatoren {#supported-operators}

Regeln können je nach Datentyp die folgenden Operatoren verwenden:

| Datentyp | Unterstützte Operatoren |
|-----------|-------------------|
| **String** | `equals`, `starts with`, `ends with`, `contains`, `exists`, `does not equal`, `does not start with`, `does not end with`, `does not contain`, `does not exist` |
| **number (long, integer, short, byte)** | `equals`, `does not equal`, `greater than`, `less than`, `greater than or equal to`, `less than or equal to`, `exists`, `does not exist` |
| **Boolesch** | `equals true/false`, `does not equal true/false` |
| **enum** | `equals`, `does not equal`, `exists`, `does not exist` |
| **Datum** | `today`, `yesterday`, `this month`, `this year`, `custom date`, `in last`, `from`, `during`, `within`, `before`, `after`, `rolling range`, `in next`, `exists`, `does not exist` |
| **Logisch** | `INCLUDE`, `ANY/ALL` (entspricht UND/ODER) |

>[!NOTE]
>
>Der **[!UICONTROL EXCLUDE]**-Operator wird nicht direkt unterstützt, aber Sie können eine äquivalente Logik mit **[!UICONTROL INCLUDE]** mit negierten Vergleichsoperatoren erreichen (z. B. „ist nicht gleich„).

### Regelstruktur {#rule-structure}

Beim Erstellen von Regeln für dynamische Datenstromkonfigurationen ist es wichtig, die strukturellen Anforderungen zu verstehen, die eine optimale Leistung und Systemkompatibilität sicherstellen. Die Regelstruktur wirkt sich direkt darauf aus, wie effizient Ihre Daten verarbeitet und durch das System weitergeleitet werden.

**Nur flache Ausdrücke verwenden**. Sie müssen Regeln als flache logische Ausdrücke definieren. Verschachtelte logische Ausdrücke (bei Verwendung von Containern oder mehreren Ebenen von UND/ODER) werden nicht unterstützt. Wenn Sie komplexe Logik benötigen, unterteilen Sie sie in mehrere einfache Regeln.

Betrachten Sie beispielsweise die komplexe Regel, die in der Abbildung unten dargestellt wird.

![Platform-UI-Bild, das eine komplexe Regel anzeigt.](assets/configure-dynamic-datastream/complex-rule.png)

Sie können diese Regel in die folgenden einfacheren Regeln unterteilen:

![Platform-UI-Bild, das eine komplexe Regel anzeigt.](assets/configure-dynamic-datastream/simple-rule-1.png)

![Platform-UI-Bild, das eine komplexe Regel anzeigt.](assets/configure-dynamic-datastream/simple-rule-2.png)

**Vermeiden Sie komplexe Regeln**. Einfachere Vorschriften gewährleisten eine schnellere Bewertung und bessere Wartungsfreundlichkeit.

### Best Practices {#best-practices}

Die Befolgung der Best Practices beim Erstellen dynamischer Datenstromkonfigurationsregeln stellt eine optimale Leistung, Systemzuverlässigkeit und verwaltbare Konfigurationen sicher. Diese Richtlinien helfen Ihnen, häufige Fehler zu vermeiden und effiziente Regeln zu erstellen, die nahtlos mit der Architektur der Plattform zusammenarbeiten.

* **Halten Sie Regeln einfach und einfach.** Wenn Sie eine komplexe Logik ausdrücken müssen, verwenden Sie mehrere Regeln anstelle von Verschachtelungen.
* **Verwenden Sie nur [unterstützte Datentypen](#supported-data-types) und [Operatoren](#supported-operators).**
* **Testen Sie Ihre Regeln auf Leistung.** zu komplexen oder nicht unterstützten Regeln kann das System diese Regeln ablehnen oder die Systemleistung beeinträchtigen.





