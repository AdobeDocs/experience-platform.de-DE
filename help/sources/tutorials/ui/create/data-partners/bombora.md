---
title: Verbinden des Bombora Intent mit Experience Platform über die Benutzeroberfläche
description: Erfahren Sie, wie Sie Bombora Intent mit Experience Platform verbinden
hide: true
hidefromtoc: true
source-git-commit: 81a615b9826ed69bb050cae9c074a4e457ba128a
workflow-type: tm+mt
source-wordcount: '365'
ht-degree: 28%

---

# Verbinden von [!DNL Bombora Intent] mit Experience Platform über die Benutzeroberfläche

Lesen Sie dieses Handbuch, um zu erfahren, wie Sie Ihr [!DNL Bombora Intent]-Konto über die Benutzeroberfläche mit Adobe Experience Platform verbinden.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Experience Platform voraus:

* [Real-Time CDP B2B edition](../../../../../rtcdp/b2b-overview.md): Real-Time CDP B2B edition wurde speziell für Marketing-Fachleute entwickelt, die in einem Business-to-Business-Service-Modell arbeiten. Es führt Daten aus verschiedenen Quellen zusammen und kombiniert sie zu einer einzigen Ansicht von Personen und Account-Profilen. Diese vereinheitlichten Daten ermöglichen es Marketing-Experten, bestimmte Zielgruppen präzise anzusprechen und über alle verfügbaren Kanäle anzusprechen.
* [Quellen](../../../../home.md): Experience Platform ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von Experience Platform-Services zu strukturieren, zu kennzeichnen und anzureichern.
* [Sandboxes](../../../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Experience Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse besser entwickeln und weiterentwickeln können.

## Navigieren im Quellkatalog

Wählen Sie in der Platform-Benutzeroberfläche in der linken Navigationsleiste die Option **[!UICONTROL Quellen]**, um auf den Arbeitsbereich [!UICONTROL Quellen] zuzugreifen. Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Alternativ können Sie die gewünschte Quelle mithilfe der Suchoption finden.

Wählen Sie **[!DNL Bombora Intent]** unter der Kategorie *[!UICONTROL B2B]* und dann **[!UICONTROL Einrichten]** aus.

>[!TIP]
>
>Quellen im Quellkatalog zeigen die Option **[!UICONTROL Einrichten]** an, wenn eine bestimmte Quelle noch kein authentifiziertes Konto hat. Sobald ein authentifiziertes Konto vorhanden ist, ändert sich diese Option in **[!UICONTROL Daten hinzufügen]**.



## Vorhandenes Konto verwenden {#existing}

## Neues Konto erstellen {#create}

## Angeben von Datenflussdetails {#provide-dataflow-details}

>[!CONTEXTUALHELP]
>id="platform_sources_bombora_domain"
>title="Domain-Quelle"
>abstract="Während Adobe die Website XDM accountOrganization.website verwendet, gibt es möglicherweise Kunden, die benutzerdefinierte Felder für ihre jeweiligen Websites verwenden. Daher müssen Sie sicherstellen, dass Ihre Domain-Quelle das Domain-/Website-Feld ist, das Ihre Bombora-Kontoeinträge mit den Experience Platform-Konten abgleicht."

## Datenfluss planen {#schedule-dataflow}

>[!CONTEXTUALHELP]
>id="platform_sources_bombora_schedule"
>title="Planen des Datenflusses"
>abstract="Bombora lässt Daten einmal wöchentlich am Montagmorgen um 17:00 Uhr UTC fallen. Daher müssen Sie Ihre Aufnahmestartzeit nach 17:00 Uhr UTC konfigurieren. Darüber hinaus müssen Sie die Aufnahmezeit mit Bombora bestätigen, da dieser ihren Zeitplan ändern kann, wenn Dateien auf Adobe abgelegt werden."


## Datenfluss überprüfen {#review-dataflow}
