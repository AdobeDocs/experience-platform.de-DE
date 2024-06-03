---
title: Migrieren der ECID-Zuordnung von Person zu Aktivität mithilfe der Marketo Engage-Quelle
description: Erfahren Sie, wie Sie Ihre ECID-Zuordnung mithilfe der Marketo Engage-Quelle aus dem Personendatensatz zum Aktivitätsdatensatz migrieren.
source-git-commit: 0c695e11e7d7c14ef7e047cd007668e1099bf127
workflow-type: tm+mt
source-wordcount: '551'
ht-degree: 1%

---

# Migrieren der ECID-Zuordnung aus [!DNL Person] Datensatz in [!DNL Activity] Datensatz

Sie können Ihr ECID-Mapping aus Ihrem [!DNL Marketo Engage Person] -Datensatz zu Ihrem [!DNL Activity] Datensatz, um ein stabileres Verhalten bei der Datenerfassung und Identitätsverwaltung zu gewährleisten. Darüber hinaus behandelt diese Migration Folgendes:

| Problem | Lösung |
| --- | --- |
| Wenn [!DNL Marketo Person] Datensatz enthält Links zu mehreren ECIDs, schlägt die Datenerfassung fehl, wenn die Variable [Gesamtzahl der Identitäten in einem Experience-Datenmodell (XDM)-Datensatz überschreitet 20](../../../../identity-service/guardrails.md). | Migrieren der ECID-Feldzuordnung zu [!DNL Activity], können Sie sicherstellen, dass die Anzahl der Identitäten aus der [!DNL Marketo Person] dataflow bleibt innerhalb der Grenze und ermöglicht so die erfolgreiche Datenerfassung. |
| Jedes Mal [!DNL Marketo Person] -Datensatz wird mit ECIDs erfasst, dem Zeitstempel für alle ECIDs aus der [!DNL Marketo Person] -Datensatz wird mit dem letzten aktualisierten Zeitstempel des Personen-Datensatzes aktualisiert. Dies kann zu der [falsches Löschen aktuellerer Identitäten aus dem Identitätsdiagramm](../../../../identity-service/guardrails.md#understanding-the-deletion-logic-when-an-identity-graph-at-capacity-is-updated). | Migrieren der ECID-Feldzuordnungen zu [!DNL Activity], kann Identity Service den Zeitstempel von ECIDs korrekt widerspiegeln und der &quot;First-in-First-Out&quot;-Mechanismus von Identity Service bietet ein stabileres Verhalten. |
| Wenn ECIDs erfasst werden über [!DNL Marketo Person] Datenfluss, neu hinzugefügte ECIDs werden nicht in Experience Platform erfasst, es sei denn, es gibt Aktualisierungen der [!DNL Person] -Datensatz [!DNL Marketo]. | Wenn eine neue ECID mit der [!DNL Person] -Datensatz [!DNL Marketo]können Sie diese ECID-Daten über eine [!DNL Marketo Activity] Datenfluss und sofortige Aufforderung zur Aktualisierung eines Identitätsdiagramms auf dem Experience Platform. |

Im Grunde müssen Sie:

* Aktualisieren Sie Ihre [!DNL Marketo Activity] dataflow.
* Aktualisieren Sie Ihre [!DNL Marketo Person] dataflow.

## Aktualisieren [!DNL Marketo Activity] dataflow {#update-activity-dataflow}

Gehen Sie wie folgt vor, um Ihre [!DNL Marketo Activity] dataflow:

* Navigieren Sie in der Experience Platform-Benutzeroberfläche zum *Quellen* Arbeitsbereich und Suchen Ihres vorhandenen Datenflusses für [!DNL Marketo Activity] Daten.
* Wenn der Datenfluss aktiviert ist, wählen Sie die Auslassungszeichen (`...`) neben dem Namen des Datenflusses und wählen Sie dann **[!UICONTROL Aktualisieren des Datenflusses]**.
* Wählen Sie anschließend **[!UICONTROL Nächste]** bis zum Erreichen der *Zuordnung* -Schnittstelle.
* Im *Zuordnung* Benutzeroberfläche, wählen Sie **[!UICONTROL Neues Feld]** und wählen Sie **[!UICONTROL Berechnetes Feld hinzufügen]**. Von hier aus müssen Sie Folgendes hinzufügen:

| Quelldatensatz | XDM-Zielfeld |
| --- | --- |
| `iif(${web\.ecid} != null, to_object('ECID', arrays_to_objects('id', explode(last(split(${web\.ecid}, ":")), " "))), null)` | `identityMap` |

>[!NOTE]
>
>Wenn Ihre Aktualisierung auf ein vorhandenes [!DNL Marketo] dataflow besteht nur darin, das ECID-Zuordnungsfeld hinzuzufügen oder zu entfernen. Anschließend überspringt der Datenfluss automatisch den früheren Aufstockungsauftrag. Die neue Datenerfassung erfolgt nur, wenn Aktivitätstypen wie &quot;Webseite besuchen&quot;und &quot;Webseite klicken&quot;auftreten.

## Aktualisieren [!DNL Marketo Person] dataflow {#update-person-dataflow}

Gehen Sie wie folgt vor, um Ihre [!DNL Marketo Person] dataflow:

* Navigieren Sie in der Experience Platform-Benutzeroberfläche zum *Quellen* Arbeitsbereich und Suchen Ihres vorhandenen Datenflusses für [!DNL Marketo Person] Daten.
* Wenn der Datenfluss aktiviert ist, wählen Sie die Auslassungszeichen (`...`) neben dem Namen des Datenflusses und wählen Sie dann **[!UICONTROL Aktualisieren des Datenflusses]**.
* Wählen Sie anschließend **[!UICONTROL Nächste]** bis zum Erreichen der *Zuordnung* -Schnittstelle.
* Im *Zuordnung* -Benutzeroberfläche verwenden, entfernen Sie das berechnete Feld, das `identityMap` und wählen Sie **[!UICONTROL Nächste]** und **[!UICONTROL Speichern und aufnehmen]**.

>[!NOTE]
>
>Wenn Ihre Aktualisierung auf ein vorhandenes [!DNL Marketo] dataflow besteht nur darin, das ECID-Zuordnungsfeld hinzuzufügen oder zu entfernen. Anschließend überspringt der Datenfluss automatisch den früheren Aufstockungsauftrag. Der Zeitstempel der zuvor erfassten ECIDs bleibt unverändert. Sie werden nur aktualisiert, wenn neue Daten erfasst werden, die den vorhandenen ECIDs entsprechen.

## Nächste Schritte

Durch Lesen dieses Dokuments wissen Sie jetzt, wie Sie Ihr ECID-Mapping von Ihrem [!DNL Marketo Person] Datensatz in [!DNL Marketo Activity] Datensatz. Weitere Informationen finden Sie in folgenden Abschnitten: [!DNL Marketo] Dokumente:

* [Erstellen eines zu erfassenden Datenflusses [!DNL Marketo] Daten an Experience Platform](../../../tutorials/ui/create/adobe-applications/marketo.md).
* [Handbuch zur Feldzuordnung](../mapping/marketo.md).