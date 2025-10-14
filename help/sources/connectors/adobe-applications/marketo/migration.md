---
title: Migrieren der ECID-Zuordnung von Person zu Aktivität mithilfe der Marketo Engage-Quelle
description: Erfahren Sie, wie Sie Ihre ECID-Zuordnung mithilfe der Marketo Engage-Quelle vom Personendatensatz zum Aktivitätsdatensatz migrieren.
exl-id: bcc91c53-aeca-4d7c-89b5-cf025d0357a0
source-git-commit: d03fcf06fb63ad2484ded3b85fc11ae45661babc
workflow-type: tm+mt
source-wordcount: '551'
ht-degree: 1%

---

# Migrieren der ECID-Zuordnung aus [!DNL Person] Datensatz in [!DNL Activity] Datensatz

Sie können Ihre ECID-Zuordnung aus Ihrem [!DNL Marketo Engage Person] Datensatz in Ihren [!DNL Activity] Datensatz migrieren, um ein stabileres Verhalten bei der Datenaufnahme und Identitätsverwaltung zu gewährleisten. Darüber hinaus behandelt diese Migration Folgendes:

| Problem | Lösung |
| --- | --- |
| Wenn Ihr [!DNL Marketo Person]-Datensatz über Links zu mehreren ECIDs verfügt, schlägt die Datenaufnahme fehl, wenn die [Gesamtzahl der Identitäten in einem Experience-Datenmodell (XDM)-Datensatz 20 % &#x200B;](../../../../identity-service/guardrails.md). | Durch die Migration der ECID-Feldzuordnung zu [!DNL Activity] können Sie sicherstellen, dass die Anzahl der Identitäten aus dem [!DNL Marketo Person] Datenfluss innerhalb des Limits bleibt, und so eine erfolgreiche Datenaufnahme ermöglichen. |
| Jedes Mal, wenn der [!DNL Marketo Person] Datensatz mit ECIDs aufgenommen wird, wird der Zeitstempel für alle ECIDs aus dem [!DNL Marketo Person] Datensatz mit dem zuletzt aktualisierten Zeitstempel des Personendatensatzes aktualisiert. Dies kann dazu führen[&#x200B; dass neuere Identitäten fälschlicherweise aus dem Identitätsdiagramm gelöscht &#x200B;](../../../../identity-service/guardrails.md#understanding-the-deletion-logic-when-an-identity-graph-at-capacity-is-updated). | Durch die Migration der ECID-Feldzuordnungen zu [!DNL Activity] kann Identity Service den Zeitstempel von ECIDs korrekt widerspiegeln, und der First-in-, First-out-Mechanismus von Identity Service sorgt für ein stabileres Verhalten. |
| Wenn ECIDs über [!DNL Marketo Person] Datenfluss aufgenommen werden, werden neu hinzugefügte ECIDs erst dann in Experience Platform aufgenommen, wenn der [!DNL Person]-Datensatz in [!DNL Marketo] aktualisiert wird. | Wenn eine neue ECID mit dem [!DNL Person]-Datensatz in [!DNL Marketo] verknüpft ist, können Sie diese ECID-Daten über einen [!DNL Marketo Activity] Datenfluss aufnehmen und sofort eine Aktualisierung des Identitätsdiagramms beim Experience Platform anfordern. |

Im Wesentlichen müssen Sie:

* Aktualisieren Ihres [!DNL Marketo Activity] Datenflusses.
* Aktualisieren Ihres [!DNL Marketo Person] Datenflusses.

## [!DNL Marketo Activity] aktualisieren {#update-activity-dataflow}

Gehen Sie wie folgt vor, um Ihren [!DNL Marketo Activity] Datenfluss zu aktualisieren:

* Navigieren Sie in der Experience Platform-Benutzeroberfläche zum Arbeitsbereich *Quellen* und suchen Sie nach Ihrem vorhandenen Datenfluss für [!DNL Marketo Activity] Daten.
* Wenn der Datenfluss aktiviert ist, klicken Sie auf die Auslassungszeichen (`...`) neben dem Namen des Datenflusses und wählen Sie **[!UICONTROL Datenfluss aktualisieren]**.
* Wählen Sie dann **[!UICONTROL Weiter]**, bis Sie die Schnittstelle *Zuordnung* erreichen.
* Wählen Sie in der *Zuordnung*-Oberfläche **[!UICONTROL Neues Feld]** und dann **[!UICONTROL Berechnetes Feld hinzufügen]** aus. Von hier aus müssen Sie Folgendes hinzufügen:

| Quelldatensatz | XDM-Zielfeld |
| --- | --- |
| `iif(${web\.ecid} != null, to_object('ECID', arrays_to_objects('id', explode(last(split(${web\.ecid}, ":")), " "))), null)` | `identityMap` |

>[!NOTE]
>
>Wenn Ihre Aktualisierung eines vorhandenen [!DNL Marketo]-Datenflusses nur darin besteht, das ECID-Zuordnungsfeld hinzuzufügen oder zu entfernen, überspringt der Datenfluss automatisch den historischen Aufstockungsauftrag. Die Aufnahme neuer Daten erfolgt nur, wenn Aktivitätstypen wie „Web-Seite besuchen“ und „Web-Seite klicken“ auftreten.

## [!DNL Marketo Person] aktualisieren {#update-person-dataflow}

Gehen Sie wie folgt vor, um Ihren [!DNL Marketo Person] Datenfluss zu aktualisieren:

* Navigieren Sie in der Experience Platform-Benutzeroberfläche zum Arbeitsbereich *Quellen* und suchen Sie nach Ihrem vorhandenen Datenfluss für [!DNL Marketo Person] Daten.
* Wenn der Datenfluss aktiviert ist, klicken Sie auf die Auslassungszeichen (`...`) neben dem Namen des Datenflusses und wählen Sie **[!UICONTROL Datenfluss aktualisieren]**.
* Wählen Sie dann **[!UICONTROL Weiter]**, bis Sie die Schnittstelle *Zuordnung* erreichen.
* Entfernen Sie in der *Zuordnung* das berechnete Feld, das `identityMap` zugeordnet ist, und wählen Sie dann **[!UICONTROL Weiter]** und **[!UICONTROL Speichern und aufnehmen]**.

>[!NOTE]
>
>Wenn Ihre Aktualisierung eines vorhandenen [!DNL Marketo]-Datenflusses nur darin besteht, das ECID-Zuordnungsfeld hinzuzufügen oder zu entfernen, überspringt der Datenfluss automatisch den historischen Aufstockungsauftrag. Der Zeitstempel von ECIDs, die zuvor aufgenommen wurden, bleibt gleich. Sie werden nur aktualisiert, wenn neue Daten aufgenommen werden, die den vorhandenen ECIDs entsprechen.

## Nächste Schritte

Durch das Lesen dieses Dokuments wissen Sie jetzt, wie Sie Ihre ECID-Zuordnung von Ihrem [!DNL Marketo Person] Datensatz zu [!DNL Marketo Activity] Datensatz migrieren. Weitere Informationen finden Sie in den folgenden [!DNL Marketo]:

* [Erstellen eines Datenflusses zum Aufnehmen  [!DNL Marketo]  Daten auf Experience Platform](../../../tutorials/ui/create/adobe-applications/marketo.md).
* [Handbuch zur Feldzuordnung](../mapping/marketo.md).
