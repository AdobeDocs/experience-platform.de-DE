---
title: Migrieren der ECID-Zuordnung von Person zu Aktivität mithilfe der Marketo Engage-Quelle
description: Erfahren Sie, wie Sie Ihre ECID-Zuordnung mithilfe der Marketo Engage-Quelle aus dem Personendatensatz zum Aktivitätsdatensatz migrieren.
exl-id: bcc91c53-aeca-4d7c-89b5-cf025d0357a0
source-git-commit: d03fcf06fb63ad2484ded3b85fc11ae45661babc
workflow-type: tm+mt
source-wordcount: '551'
ht-degree: 1%

---

# Migrieren der ECID-Zuordnung aus dem [!DNL Person] -Datensatz in den [!DNL Activity] -Datensatz

Sie können Ihre ECID-Zuordnung aus Ihrem [!DNL Marketo Engage Person] -Datensatz in Ihren [!DNL Activity] -Datensatz migrieren, um ein stabileres Verhalten bei der Datenerfassung und Identitätsverwaltung zu gewährleisten. Darüber hinaus behandelt diese Migration Folgendes:

| Problem | Lösung |
| --- | --- |
| Wenn Ihr [!DNL Marketo Person] -Datensatz Links zu mehreren ECIDs enthält, schlägt die Datenerfassung fehl, wenn die [Gesamtzahl der Identitäten in einem Experience-Datenmodell (XDM)-Datensatz 20](../../../../identity-service/guardrails.md) überschreitet. | Durch die Migration der ECID-Feldzuordnung zu [!DNL Activity] können Sie sicherstellen, dass die Anzahl der Identitäten aus dem [!DNL Marketo Person] -Datenfluss innerhalb der Grenze bleibt und somit die Datenerfassung erfolgreich ist. |
| Jedes Mal, wenn der Datensatz [!DNL Marketo Person] mit ECIDs erfasst wird, wird der Zeitstempel für alle ECIDs aus dem Datensatz [!DNL Marketo Person] mit dem letzten aktualisierten Zeitstempel des Datensatzes &quot;Person&quot;aktualisiert. Dies könnte dazu führen, dass neuere Identitäten aus dem Identitätsdiagramm ](../../../../identity-service/guardrails.md#understanding-the-deletion-logic-when-an-identity-graph-at-capacity-is-updated) nicht mit [fehlerhaft gelöscht werden. | Durch die Migration der ECID-Feldzuordnungen auf [!DNL Activity] kann Identity Service den Zeitstempel von ECIDs korrekt widerspiegeln. Der First-in-First-out-Mechanismus von Identity Service bietet ein stabileres Verhalten. |
| Wenn ECIDs über den [!DNL Marketo Person] -Datenfluss erfasst werden, werden neu hinzugefügte ECIDs nicht in Experience Platform aufgenommen, es sei denn, es gibt Aktualisierungen am [!DNL Person] -Datensatz in [!DNL Marketo]. | Wenn eine neue ECID mit dem [!DNL Person] -Datensatz in [!DNL Marketo] verknüpft ist, können Sie diese ECID-Daten über einen [!DNL Marketo Activity] -Datenfluss erfassen und sofort eine Aktualisierung des Identitätsdiagramms auf der Experience Platform auffordern. |

Im Grunde müssen Sie:

* Aktualisieren Sie Ihren [!DNL Marketo Activity] -Datenfluss.
* Aktualisieren Sie Ihren [!DNL Marketo Person] -Datenfluss.

## Update des [!DNL Marketo Activity]-Datenflusses {#update-activity-dataflow}

Gehen Sie wie folgt vor, um Ihren [!DNL Marketo Activity]-Datenfluss zu aktualisieren:

* Navigieren Sie in der Experience Platform-Benutzeroberfläche zum Arbeitsbereich *Quellen* und suchen Sie Ihren vorhandenen Datenfluss für [!DNL Marketo Activity] -Daten.
* Wenn der Datenfluss aktiviert ist, wählen Sie die Auslassungszeichen (`...`) neben dem Dataflow-Namen und dann **[!UICONTROL Datenfluss aktualisieren]** aus.
* Wählen Sie dann **[!UICONTROL Weiter]** aus, bis Sie die Schnittstelle *Zuordnen* erreichen.
* Wählen Sie in der Benutzeroberfläche *Zuordnung* die Option **[!UICONTROL Neues Feld]** und dann **[!UICONTROL Berechnetes Feld hinzufügen]** aus. Von hier aus müssen Sie Folgendes hinzufügen:

| Quelldatensatz | XDM-Zielfeld |
| --- | --- |
| `iif(${web\.ecid} != null, to_object('ECID', arrays_to_objects('id', explode(last(split(${web\.ecid}, ":")), " "))), null)` | `identityMap` |

>[!NOTE]
>
>Wenn Ihre Aktualisierung auf einen vorhandenen [!DNL Marketo]-Datenfluss nur darin besteht, das ECID-Zuordnungsfeld hinzuzufügen oder zu entfernen, überspringt der Datenfluss automatisch den früheren Aufstockungsauftrag. Die neue Datenerfassung erfolgt nur, wenn Aktivitätstypen wie &quot;Webseite besuchen&quot;und &quot;Webseite klicken&quot;auftreten.

## Update des [!DNL Marketo Person]-Datenflusses {#update-person-dataflow}

Gehen Sie wie folgt vor, um Ihren [!DNL Marketo Person]-Datenfluss zu aktualisieren:

* Navigieren Sie in der Experience Platform-Benutzeroberfläche zum Arbeitsbereich *Quellen* und suchen Sie Ihren vorhandenen Datenfluss für [!DNL Marketo Person] -Daten.
* Wenn der Datenfluss aktiviert ist, wählen Sie die Auslassungszeichen (`...`) neben dem Dataflow-Namen und dann **[!UICONTROL Datenfluss aktualisieren]** aus.
* Wählen Sie dann **[!UICONTROL Weiter]** aus, bis Sie die Schnittstelle *Zuordnen* erreichen.
* Entfernen Sie in der Benutzeroberfläche *Zuordnung* das berechnete Feld, das `identityMap` zugeordnet ist, und wählen Sie dann **[!UICONTROL Weiter]** und **[!UICONTROL Speichern und Aufnehmen]** aus.

>[!NOTE]
>
>Wenn Ihre Aktualisierung auf einen vorhandenen [!DNL Marketo]-Datenfluss nur darin besteht, das ECID-Zuordnungsfeld hinzuzufügen oder zu entfernen, überspringt der Datenfluss automatisch den früheren Aufstockungsauftrag. Der Zeitstempel der zuvor erfassten ECIDs bleibt unverändert. Sie werden nur aktualisiert, wenn neue Daten erfasst werden, die den vorhandenen ECIDs entsprechen.

## Nächste Schritte

Durch Lesen dieses Dokuments wissen Sie jetzt, wie Sie Ihre ECID-Zuordnung aus Ihrem [!DNL Marketo Person] -Datensatz in den [!DNL Marketo Activity] -Datensatz migrieren können. Weitere Informationen finden Sie in den folgenden [!DNL Marketo] Dokumenten:

* [Erstellen Sie einen Datenfluss, um  [!DNL Marketo] Daten an Experience Platform](../../../tutorials/ui/create/adobe-applications/marketo.md) zu erfassen.
* [Handbuch zur Feldzuordnung](../mapping/marketo.md).
