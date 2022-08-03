---
title: Lead zur Kontoübereinstimmung in der Echtzeit-Kundendatenplattform B2B
type: Documentation
description: Eine Übersicht und weitere Informationen zum Interessenten für die Kontoabgleichfunktion in der Experience Platform CDP B2B.
source-git-commit: 827bd1b930478c3c0b553a9485f98545771a9062
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# Lead zur Kontoübereinstimmung in der Echtzeit-Kundendatenplattform B2B

## Übersicht {#overview}

Account-basiertes Marketing ist eine zunehmend wichtige Strategie für B2B-Marketing. Kontobasiertes Marketing bietet die folgenden Hauptvorteile, um spezielle hochwertige Kunden zu gewinnen:

- ROI löschen
- Ausrichtung von Vertrieb und Marketing
- Ein personalisierter Ansatz
- Weniger verschwendete Ressourcen
- Ein kürzerer Verkaufszyklus

Kontobasiertes Marketing bietet die Möglichkeit, bekannte Personen und anonyme Webbesucher mit Verkaufskonten zu verknüpfen. Dadurch können Marketing-Teams frühzeitig auf der Journey mit potenziellen Leads aus den Zielkonten interagieren, um ihre Konversionschancen zu erhöhen. Ein bekannter Personendatensatz enthält in der Regel die folgenden Informationen teilweise oder vollständig:

- Personenname
- E-Mail Adresse
- Kontaktnummer
- Firmenname
- Firmenwebsite
- Auftragstitel
- Standort

Mithilfe der Kontozuordnung können Sie Profile bekannter Personen zuordnen. Anschließend können Sie Daten in einem B2B-Kontext segmentieren und ansprechen, z. B. in Konten, Opportunities usw. Die Personenprofile können in die folgenden drei Kategorien eingeteilt werden:

- **Kundenprofil:** Das Personenprofil ist durch die Beziehung aus einer Datenquelle bereits mit mindestens einem Kontoprofil verknüpft. Dies bedeutet, dass es mindestens ein Kontaktfragment gibt.

>[!NOTE]
>
> Kundenprofil-Profile werden beim Ausführen von Leads nicht zugeordnet, um Kontoabstimmungsaufträge zu erhalten.

- **Bekanntes Personenprofil:** Das Personenprofil ist NICHT mit einem Kontoprofil verknüpft und mindestens eines der folgenden Personenprofilattribute hat einen Wert:

   - E-Mail Adresse
   - Firmenname
   - Firmenwebsite

- **Anonymes Personenprofil:** Das Personenprofil ist NICHT mit einem Kontoprofil verknüpft und keines der folgenden Personenprofilattribute hat einen Wert:

   - E-Mail Adresse
   - Firmenname
   - Firmenwebsite

>[!NOTE]
>
> Ein Personenprofil kann mit mehreren Kontoprofilen verknüpft sein. Der Prozess zum Abgleich von Konten wird jedoch nur mit der besten Übereinstimmung übereinstimmen. Wenn ein breiterer Satz von Übereinstimmungen erforderlich ist, koppeln Sie den Interessenten, damit er mit der zugehörigen Kontofunktion übereinstimmt.

## Funktionsweise {#how-it-works}

Aufträge mit täglicher Ausführung verwenden sowohl deterministische als auch probabilistische Faktoren, um bekannte Lead-Profile ohne vorhandene Kontoverknüpfungen abzugleichen. Bekannte Lead-Profile verfügen über eines der folgenden Attribute:

- b2b.companyName
- b2b.companyWebsite
- workEmail

>[!NOTE]
>
> Das Attribut b2b.personKey.sourceKey muss vorhanden sein.

Die Attribute b2b.companyName, b2b.companyWebsite und b2b.personKey.sourceKey befinden sich in der Feldergruppe b2b im B2B-Personenschema.

![B2B-Personenschema mit Attributen](/help/rtcdp/accounts/images/b2b-person-schema.png)

Das Attribut workEmail kann als Feldergruppe der obersten Ebene im B2B-Personenschema gefunden werden.

![B2B-Personenschema mit workEmail](/help/rtcdp/accounts/images/b2b-person-workemail.png)

Profile werden am besten abgeglichen, wenn der Übereinstimmungswert über einem internen Konfidenzschwellenwert liegt. Die Ergebnisse werden in einem neuen Systemdatensatz des vorhandenen Konto-Personen-Verhältnisses XDM gespeichert.

Der Lead für den Kontoabgleichdienst wird ausgeführt, wenn ein neuer Personenprofil-Schnappschuss verfügbar wird, der alle 24 Stunden verfügbar ist. Weitere Informationen zum [Konfiguration des Interessenten-Kontoabgleichs](/help/rtcdp/accounts/account-profile-ui-guide.md).

## Anleitung zum Anzeigen der Ausgabe des Kontoabgleichs {#how-to-view}

Nach Ausführung des Auftrags werden die Ergebnisse in einem neuen Datensatz des vorhandenen Konto-Personen-Verhältnisses XDM gespeichert.

Um eine Vorschau des Datensatzes anzuzeigen, wählen Sie **[!UICONTROL Vorschau des Datensatzes anzeigen]** oben rechts.

![Neuer Datensatz](/help/rtcdp/accounts/images/b2b-dataset-output.png)

Der Datensatz enthält die übereinstimmenden Kontoinformationen sowie den Übereinstimmungswert für Ihren ausgewählten Datensatz. Die **[!UICONTROL Beziehungsquelle]** gibt an, ob es aus dem Lead stammt, um einen Kontoabstimmungsprozess durchzuführen.

![Vorschau der Konfidenzwerte und Ausgabe des Datensatzes anzeigen](/help/rtcdp/accounts/images/b2b-dataset-preview.png)

## Überwachung führt zu übereinstimmenden Aufträgen von Konten {#monitoring-jobs}

Über das Dashboard können Sie den Auftragsstatus und die zugehörigen Metriken auf jeden Lead überwachen, der zu den entsprechenden Aufträgen führt.

Weitere Informationen zu [Überwachen von Aufträgen für die Kontozuordnung als Lead](/help/dataflows/ui/b2b/monitor-profile-enrichment.md).
