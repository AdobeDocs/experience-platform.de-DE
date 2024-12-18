---
title: Lead zur Kontoübereinstimmung in Real-Time CDP B2B
type: Documentation
description: Eine Übersicht und weitere Informationen über die Lead-to-Account-Matching-Funktion in der Experience Platform CDP B2B.
feature: Get Started, Profiles, B2B
badgeB2B: label="B2B Edition" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: 2f853599-6bca-4ba6-bbba-131a49d8854e
source-git-commit: db57fa753a3980dca671d476521f9849147880f1
workflow-type: tm+mt
source-wordcount: '605'
ht-degree: 5%

---

# Lead zur Kontoübereinstimmung in Real-Time CDP B2B

## Übersicht {#overview}

Account-basiertes Marketing ist eine zunehmend wichtige Strategie für B2B-Marketing. Kontobasiertes Marketing bietet die folgenden Hauptvorteile, um spezielle hochwertige Kunden zu gewinnen:

- ROI löschen
- Ausrichtung von Vertrieb und Marketing
- Ein personalisierter Ansatz
- Weniger Ressourcen
- Ein kürzerer Verkaufszyklus

Kontobasiertes Marketing bietet die Möglichkeit, bekannte Personen und anonyme Webbesucher mit Verkaufskonten zu verknüpfen. Dadurch können Marketing-Teams frühzeitig auf der Journey mit potenziellen Leads aus den Zielkonten interagieren, um ihre Konversionschancen zu erhöhen. Ein bekannter Personendatensatz enthält in der Regel die folgenden Informationen teilweise oder vollständig:

- Personenname
- E-Mail-Adresse
- Kontaktnummer
- Unternehmensname
- Firmenwebsite
- Stellenbezeichnung
- Standort

Mithilfe der Lead-Konto-Zuordnung können Sie bekannte Personenprofile mit Kontoprofilen verbinden. Anschließend können Sie Daten in einem B2B-Kontext segmentieren und ansprechen, z. B. in Konten, Opportunities usw. Die Personenprofile können in die folgenden drei Kategorien eingeteilt werden:

- **Profil der Kontoperson:** Das Personenprofil ist durch die Beziehung aus einer Datenquelle bereits mindestens einem Kontoprofil zugeordnet. Dies bedeutet, dass es mindestens ein Kontaktfragment gibt.

>[!NOTE]
>
> Kundenprofil-Profile werden beim Ausführen von Leads nicht zugeordnet, um Kontoabstimmungsaufträge zu erhalten.

- **Bekanntes Personenprofil:** Das Personenprofil ist NICHT mit einem Kontoprofil verknüpft und mindestens eines der folgenden Personenprofilattribute hat einen Wert:

   - E-Mail-Adresse
   - Unternehmensname
   - Firmenwebsite

- **Anonymes Personenprofil:** Das Personenprofil ist NICHT mit einem Kontoprofil verknüpft und keines der folgenden Personenprofilattribute hat einen Wert:

   - E-Mail-Adresse
   - Unternehmensname
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

Der Lead für den Kontoabgleichdienst wird ausgeführt, wenn ein neuer Personenprofil-Schnappschuss verfügbar wird, der alle 24 Stunden verfügbar ist. Weitere Informationen zur [Konfiguration des Leads zur Kontoübereinstimmung](/help/rtcdp/accounts/account-profile-ui-guide.md) finden Sie in der Dokumentation .

## Anleitung zum Anzeigen der Ausgabe des Kontoabgleichs {#how-to-view}

Nach Ausführung des Auftrags werden die Ergebnisse in einem neuen Datensatz des vorhandenen Konto-Personen-Verhältnisses XDM gespeichert.

Um eine Vorschau des Datensatzes anzuzeigen, wählen Sie oben rechts **[!UICONTROL Datensatz-Vorschau anzeigen]** aus.

![Neuer Datensatz](/help/rtcdp/accounts/images/b2b-dataset-output.png)

Der Datensatz enthält die übereinstimmenden Kontoinformationen sowie den Übereinstimmungswert für Ihren ausgewählten Datensatz. Das Feld **[!UICONTROL Beziehung Source]** gibt an, ob es aus dem Lead stammt, um einen Kontoabstimmungsprozess durchzuführen.

![Vorschau der Konfidenzwerte und Ausgabe des Datensatzes anzeigen](/help/rtcdp/accounts/images/b2b-dataset-preview.png)

## Überwachung führt zu übereinstimmenden Aufträgen {#monitoring-jobs}

Über das Dashboard können Sie den Auftragsstatus und die zugehörigen Metriken auf jeden Lead überwachen, der zu den entsprechenden Aufträgen führt.

Weitere Informationen zu den [Überwachungsaufträgen für Interessenten, die mit dem Konto übereinstimmen](/help/dataflows/ui/b2b/monitor-profile-enrichment.md), finden Sie in der Dokumentation .
