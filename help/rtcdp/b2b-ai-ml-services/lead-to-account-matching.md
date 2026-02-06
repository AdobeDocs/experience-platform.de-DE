---
title: Lead-Konto-Zuordnung in Real-Time CDP B2B
type: Documentation
description: Eine Übersicht und weitere Informationen zur Funktion Lead-Konto-Zuordnung in Experience Platform CDP B2B.
feature: Get Started, Profiles, B2B
badgeB2B: label="B2B edition" type="Informative" url="https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html#rtcdp-editions" newtab=true
exl-id: 2f853599-6bca-4ba6-bbba-131a49d8854e
source-git-commit: 5998adf98aa7250864983d7e4e629921633e1a1c
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 3%

---

# Lead-Konto-Zuordnung in Real-Time CDP B2B

## Überblick {#overview}

Account-Based Marketing ist eine zunehmend wichtige Strategie für B2B-Marketing. Account-Based Marketing bietet die folgenden zentralen Vorteile, um bestimmte hochwertige Kunden zu gewinnen:

- Investitionsrendite (ROI)
- Ausrichtung von Vertrieb und Marketing
- Ein personalisierter Ansatz
- Weniger verschwendete Ressourcen
- Ein kürzerer Verkaufszyklus

Account-based Marketing bietet die Möglichkeit, bekannte Kunden mit Verkaufskonten zu verknüpfen. Dadurch können Marketing-Teams frühzeitig auf der Kunden-Journey mit potenziellen Leads aus den Zielkonten interagieren, um ihre Konversionschancen zu erhöhen. Ein Datensatz mit bekannten Personen enthält in der Regel die folgenden Informationen teilweise oder vollständig:

- Personenname
- E-Mail-Adresse
- Kontaktnummer
- Unternehmensname
- Unternehmens-Website
- Stellenbezeichnung
- Standort

## Funktionsweise {#how-it-works}

Täglich ausgeführte Aufträge verwenden sowohl deterministische als auch probabilistische Faktoren, um bekannte Lead-Profile ohne vorhandene Kontoverknüpfungen abzugleichen. Bekannte Lead-Profile verfügen über eines der folgenden Attribute:

- b2b.companyName
- b2b.companyWebsite
- workEmail

>[!NOTE]
>
> Das Attribut b2b.personKey.sourceKey muss vorhanden sein.

Die Attribute b2b.companyName, b2b.companyWebsite und b2b.personKey.sourceKey können sich in der b2b-Feldergruppe im B2B-Personenschema befinden.

![B2B-Personenschema mit Attributen](/help/rtcdp/accounts/images/b2b-person-schema.png)

Das workEmail-Attribut befindet sich als Feldergruppe auf oberster Ebene im B2B-Personen-Schema.

![B2B-Personen-Schema, das WorkEmail anzeigt](/help/rtcdp/accounts/images/b2b-person-workemail.png)

Profile werden nur dann am besten abgeglichen, wenn der Übereinstimmungswert über einem internen Konfidenzschwellenwert liegt. Die Ergebnisse werden in einem neuen Systemdatensatz der vorhandenen Konto-Personen-Beziehung XDM gespeichert.

Der Service Lead-Konto-Zuordnung wird ausgeführt, wenn ein neuer Schnappschuss des Personenprofils verfügbar wird, der einmal alle 24 Stunden angezeigt wird. Weitere Informationen zur Konfiguration [&#x200B; Lead-Konto-Zuordnung finden Sie in der &#x200B;](/help/rtcdp/accounts/account-profile-ui-guide.md).

## Anzeigen der Lead-Konto-Zuordnungsausgabe {#how-to-view}

Nach dem Auftragsdurchgang werden die Ergebnisse in einem neuen Datensatz der vorhandenen Konto-Personen-Beziehung XDM gespeichert.

Um eine Vorschau des Datensatzes anzuzeigen, wählen Sie oben rechts **[!UICONTROL Preview dataset]** aus.

![Neuer Datensatz](/help/rtcdp/accounts/images/b2b-dataset-output.png)

Der Datensatz enthält die übereinstimmenden Kontoinformationen sowie die Übereinstimmungsbewertung für den ausgewählten Datensatz. Das Feld **[!UICONTROL Relationship Source]** gibt an, ob es vom Lead-Konto-Zuordnungsprozess stammt.

![Vorschau der Datensatzkonfidenzwerte und -ausgabe](/help/rtcdp/accounts/images/b2b-dataset-preview.png)

## Überwachung von Lead-Konto-Zuordnungsaufträgen {#monitoring-jobs}

Sie können den Auftragsstatus und die zugehörigen Metriken für alle Lead-Konto-Abgleichaufträge über das Dashboard überwachen.

Weitere Informationen finden Sie in der Dokumentation zu [Überwachen von Aufträgen für die Lead-Konto-Zuordnung](/help/dataflows/ui/b2b/monitor-profile-enrichment.md).
