---
title: Lead-Konto-Zuordnung in Real-Time CDP B2B
type: Documentation
description: Eine Übersicht und weitere Informationen zur Lead-Konto-Matching-Funktion in Experience Platform CDP B2B.
feature: Get Started, Profiles, B2B
badgeB2B: label="B2B edition" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: 2f853599-6bca-4ba6-bbba-131a49d8854e
source-git-commit: db57fa753a3980dca671d476521f9849147880f1
workflow-type: tm+mt
source-wordcount: '605'
ht-degree: 5%

---

# Lead-Konto-Zuordnung in Real-Time CDP B2B

## Übersicht {#overview}

Account-Based Marketing ist eine zunehmend wichtige Strategie für B2B-Marketing. Account-Based Marketing bietet die folgenden zentralen Vorteile, um bestimmte hochwertige Kunden zu gewinnen:

- Investitionsrendite (ROI)
- Ausrichtung von Vertrieb und Marketing
- Ein personalisierter Ansatz
- Weniger verschwendete Ressourcen
- Ein kürzerer Verkaufszyklus

Account-Based Marketing bietet die Möglichkeit, bekannte Personen und anonyme Web-Besucher mit Verkaufskonten zu verknüpfen. Dadurch können Marketing-Teams frühzeitig auf der Kunden-Journey mit potenziellen Leads aus den Zielkonten interagieren, um ihre Konversionschancen zu erhöhen. Ein Datensatz mit bekannten Personen enthält in der Regel die folgenden Informationen teilweise oder vollständig:

- Personenname
- E-Mail-Adresse
- Kontaktnummer
- Unternehmensname
- Unternehmens-Website
- Stellenbezeichnung
- Standort

Mithilfe der Lead-Konto-Zuordnung können Sie bekannte Personenprofile mit Kontoprofilen verbinden. Anschließend können Sie Daten in einem B2B-Kontext wie Konten, Opportunities usw. segmentieren und ansprechen. Die Personenprofile können in die folgenden drei Kategorien unterteilt werden:

- **Account-Personenprofil:** Das Personenprofil ist bereits mit mindestens einem Account-Profil über die Beziehung aus einer Datenquelle verknüpft. Dies bedeutet, dass mindestens ein Kontaktfragment vorhanden ist.

>[!NOTE]
>
> Profile von Kontopersonen werden beim Ausführen von Lead-Konto-Zuordnungsaufträgen nicht zugeordnet.

- **Bekanntes Personenprofil:** Das Personenprofil ist KEINEM Kontoprofil zugeordnet und mindestens eines der folgenden Personenprofilattribute hat einen Wert:

   - E-Mail-Adresse
   - Unternehmensname
   - Unternehmens-Website

- **Anonymes Personenprofil:** Das Personenprofil ist KEINEM Kontoprofil zugeordnet und keines der folgenden Personenprofilattribute hat einen Wert:

   - E-Mail-Adresse
   - Unternehmensname
   - Unternehmens-Website

>[!NOTE]
>
> Ein Personenprofil kann mit mehreren Kontoprofilen verknüpft sein. Der Lead-Konto-Zuordnungsprozess stimmt jedoch nur mit der besten Übereinstimmung überein. Wenn ein breiterer Satz von Übereinstimmungen erforderlich ist, koppeln Sie den Lead mit dem Konto, das mit der Funktion für zugehörige Konten übereinstimmt.

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

Der Service Lead-Konto-Zuordnung wird ausgeführt, wenn ein neuer Schnappschuss des Personenprofils verfügbar wird, der einmal alle 24 Stunden angezeigt wird. Weitere Informationen zur Konfiguration [ Lead-Konto-Zuordnung finden Sie in der ](/help/rtcdp/accounts/account-profile-ui-guide.md).

## Anzeigen der Lead-Konto-Zuordnungsausgabe {#how-to-view}

Nach dem Auftragsdurchgang werden die Ergebnisse in einem neuen Datensatz der vorhandenen Konto-Personen-Beziehung XDM gespeichert.

Um eine Vorschau des Datensatzes anzuzeigen, wählen **[!UICONTROL oben]** die Option „Datensatz in der Vorschau anzeigen“ aus.

![Neuer Datensatz](/help/rtcdp/accounts/images/b2b-dataset-output.png)

Der Datensatz enthält die übereinstimmenden Kontoinformationen sowie die Übereinstimmungsbewertung für den ausgewählten Datensatz. Das Feld **[!UICONTROL Beziehung Source]** gibt an, ob es vom Lead-Konto-Zuordnungsprozess stammt.

![Vorschau der Datensatzkonfidenzwerte und -ausgabe](/help/rtcdp/accounts/images/b2b-dataset-preview.png)

## Überwachung von Lead-Konto-Zuordnungsaufträgen {#monitoring-jobs}

Sie können den Auftragsstatus und die zugehörigen Metriken für alle Lead-Konto-Abgleichaufträge über das Dashboard überwachen.

Weitere Informationen finden Sie in der Dokumentation zu [Überwachen von Aufträgen für die Lead-Konto-Zuordnung](/help/dataflows/ui/b2b/monitor-profile-enrichment.md).
