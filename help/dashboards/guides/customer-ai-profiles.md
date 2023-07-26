---
title: Profil-Dashboard Kunden-KI-Widgets
description: Erfahren Sie, wie Customer AI wichtige Einblicke in Abwanderung oder Tendenz zu den Echtzeit-Kundenprofildaten Ihres Unternehmens bietet.
hide: true
hidefromtoc: true
source-git-commit: 162ef470751b9fb252658cff4b43595ddb7fe5d5
workflow-type: tm+mt
source-wordcount: '828'
ht-degree: 2%

---

# Profil-Dashboard Kunden-KI-Widgets {#customer-ai-profiles-widgets}

Customer AI wird verwendet, um für einzelne Profile skaliert benutzerdefinierte Tendenzwerte wie Abwanderung und Konversion zu berechnen. Customer AI analysiert dazu vorhandene Erlebnisereignisdaten von Verbrauchern, um sie vorherzusagen **Tendenzwerte für Abwanderung oder Konversion**. Diese hochpräzisen kundenspezifischen Tendenzmodelle ermöglichen eine präzisere Segmentierung und Targeting. Die [Verteilung der Punktzahl](#customer-ai-distribution-of-scores) und [Bewertungszusammenfassung](#customer-ai-scoring-summary) Einblicke zeigen die Aufteilung in Ihrer Zielgruppe. Sie heben hervor, welche Profile die hohe/niedrige/mittlere Tendenz aufweisen und wie sie über Ihre Profilzahlen verteilt sind.

<!-- 
The links when required:
* [[!UICONTROL Customer AI scoring summary]](#customer-ai-scoring-summary)
* [[!UICONTROL Customer AI distribution of scores]](#customer-ai-distribution-of-scores) 
-->

## [!UICONTROL Customer AI-Verteilung von Bewertungen] {#customer-ai-distribution-of-scores}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_distributionOfScores"
>title="Verteilung der Punktzahl"
>abstract="Dieses Widget visualisiert die Verteilung der Gesamtanzahl der Profile anhand ihrer Tendenzwerte in fünfprozentigen Schritten. Die Verteilung der Profilanzahl wird durch das AI-Modell und die ausgewählte Zusammenführungsrichtlinie bestimmt. Sie können das KI-Modell im Dropdown-Menü unter dem Widget-Titel ändern."

Die [!UICONTROL Customer AI-Verteilung von Bewertungen] Widget kategorisiert die Gesamtanzahl der Profile nach ihren Tendenzwerten. Die Verteilung der Profilanzahl wird durch das AI-Modell und die ausgewählte Zusammenführungsrichtlinie bestimmt und dann in fünfprozentigen Schritten visualisiert, die ihre Neigung angeben. Die Anzahl der Profile wird entlang der Y-Achse angegeben und die Tendenzwerte werden entlang der X-Achse angegeben.

>[!NOTE]
>
>Wenn es sich bei der Visualisierung um eine Konversion-Tendenzbewertung handelt, werden die hohen Werte grün und die niedrigen Punkte rot angezeigt. Wenn Sie die Abwanderungsneigung vorhersagen, wird diese gespiegelt, die hohen Werte sind rot und die niedrigen Werte grün. Der mittlere Eimer bleibt gelb, unabhängig vom gewählten Tendenztyp.

Das AI-Modell, das die Tendenzwerte bestimmt, wird aus der Dropdown-Auswahl unter dem Widget-Titel ausgewählt. Das Dropdown-Menü enthält eine Liste aller konfigurierten Customer AI-Modelle. Wählen Sie aus der Liste der verfügbaren Modelle das passende KI-Modell für Ihre Analyse aus. Wenn kein Customer AI-Modell verfügbar ist, werden Sie durch eine Meldung im Widget angewiesen, mindestens ein Customer AI-Modell zu konfigurieren. Außerdem wird ein Hyperlink zur Konfigurationsseite des Customer AI-Modells bereitgestellt. Anweisungen finden Sie in der Dokumentation zu [Konfigurieren einer Customer AI-Instanz](../../intelligent-services/customer-ai/user-guide/configure.md).

>[!NOTE]
>
>Wählen Sie das Dropdown-Menü direkt unter dem Tab Übersicht aus, um die Zusammenführungsrichtlinie zu ändern, die bestimmt, welche Profile in die Analyse aufgenommen werden. Siehe Abschnitt zu [Zusammenführungsrichtlinien](#merge-policies) für eine kurze Beschreibung oder [Zusammenführungsrichtlinienübersicht](../../profile/merge-policies/overview.md) für weitere Details.

Um zur detaillierten Insight-Seite für das ausgewählte Customer AI-Modell zu navigieren, wählen Sie **[!UICONTROL Modelldetails anzeigen]**.

![Das Dashboard &quot;Zielgruppen der Experience Platform&quot;mit dem [!UICONTROL Customer AI-Verteilung von Bewertungen] Widget und [!UICONTROL Modelldetails anzeigen] hervorgehoben.](../images/segments/customer-ai-distribution-of-scores.png)

Die Seite mit detaillierten Modelleinblicken wird angezeigt.

![Die Einblicke-Seite für die Customer AI.](../images/profiles/customer-ai-insights-page.png)

Weitere Informationen zu Customer AI finden Sie im [Leitfaden zur Benutzeroberfläche für Einblicke](../../intelligent-services/customer-ai/user-guide/discover-insights.md).

## [!UICONTROL Customer AI-Bewertungszusammenfassung] {#customer-ai-scoring-summary}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_scoringSummary"
>title="Bewertungszusammenfassung"
>abstract="Dieses Widget zeigt die Gesamtzahl der bewerteten Profile und kategorisiert sie in Behälter mit hoher, mittlerer und niedriger Neigung. Das Ringdiagramm zeigt die proportionale Zusammensetzung der Gesamtprofile über eine hohe, mittlere und niedrige Tendenz hinweg."

Dieses Widget zeigt die Gesamtzahl der bewerteten Profile und kategorisiert sie in Behälter mit hoher, mittlerer und niedriger Neigung als grün, gelb und rot. Ein Ringdiagramm veranschaulicht die proportionale Zusammensetzung von Profilen zwischen hohen, mittleren und niedrigen Tendenzen. Ein Profil ist qualifiziert für eine hohe Tendenz bei über 75, eine mittlere Neigung zwischen 25 und 74 und eine niedrige Tendenz unter 24. Eine Legende zeigt den Farbcode und die Schwellen der Eigenschaften an. Profilzahlen für die Eigenschaften &quot;Hoch&quot;, &quot;Mittel&quot;und &quot;Niedrig&quot;werden in einem Dialogfeld angezeigt, wenn der Cursor den Mauszeiger über den entsprechenden Abschnitt des Ringdiagramms bewegt.

>[!NOTE]
>
>Wenn es sich bei der Visualisierung um eine Konversion-Tendenzbewertung handelt, werden die hohen Werte grün und die niedrigen Punkte rot angezeigt. Wenn Sie die Abwanderungsneigung vorhersagen, wird diese gespiegelt, die hohen Werte sind rot und die niedrigen Werte grün. Der mittlere Eimer bleibt gelb, unabhängig vom gewählten Tendenztyp.

Das Dropdown-Menü unter dem Widget-Titel enthält eine Liste aller konfigurierten Customer AI-Modelle. Wählen Sie aus der Liste der verfügbaren Modelle das passende KI-Modell für Ihre Analyse aus. Wenn kein Customer AI-Modell verfügbar ist, werden Sie durch eine Meldung im Widget angewiesen, mindestens ein Customer AI-Modell zu konfigurieren. Außerdem wird ein Hyperlink zur Konfigurationsseite des Customer AI-Modells bereitgestellt. Siehe die Dokumentation unter [Konfigurieren einer Customer AI-Instanz](../../intelligent-services/customer-ai/user-guide/configure.md) für detaillierte Anweisungen.

>[!NOTE]
>
>Die Gesamtzahl der berechneten Profile hängt von der gewählten Zusammenführungsrichtlinie ab. Um die verwendete Zusammenführungsrichtlinie zu ändern, wählen Sie das Dropdown-Menü direkt unter der Registerkarte Übersicht aus. Siehe Abschnitt zu [Zusammenführungsrichtlinien](#merge-policies) für eine kurze Beschreibung oder [Zusammenführungsrichtlinienübersicht](../../profile/merge-policies/overview.md) für weitere Details.

![Das Dashboard Experience Platform-Zielgruppen mit dem Widget Customer AI-Bewertungszusammenfassung wurde hervorgehoben.](../images/segments/customer-ai-scoring-summary.png)

Um zur detaillierten Insight-Seite für das ausgewählte Customer AI-Modell zu navigieren, wählen Sie **[!UICONTROL Modelldetails anzeigen]**. Weitere Informationen zu Customer AI finden Sie im [Leitfaden zur Benutzeroberfläche für Einblicke](../../intelligent-services/customer-ai/user-guide/discover-insights.md).