---
solution: Experience Platform
title: Berücksichtigung des Einverständnisses in Segmenten
description: Erfahren Sie, wie Sie die Voreinstellungen für das Kundeneinverständnis zur Erfassung und Freigabe personenbezogener Daten bei Segmentvorgängen berücksichtigen.
exl-id: fe851ce3-60db-4984-a73c-f9c5964bfbad
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '672'
ht-degree: 0%

---

# Berücksichtigung des Einverständnisses in Segmenten

>[!NOTE]
>
>In diesem Handbuch wird erläutert, wie Einverständnisse in **Segmentdefinitionen“ berücksichtigt**.

Rechtliche Datenschutzbestimmungen wie der [!DNL California Consumer Privacy Act] (CCPA) bieten Verbrauchern das Recht, der Erfassung oder Weitergabe ihrer personenbezogenen Daten an Dritte zu widersprechen. Adobe Experience Platform bietet standardmäßige Experience-Datenmodell (XDM)-Komponenten, die diese Voreinstellungen für das Kundeneinverständnis in Echtzeit-Kundenprofildaten erfassen sollen.

Wenn ein Kunde sein Einverständnis zur Freigabe seiner personenbezogenen Daten widerrufen oder zurückgehalten hat, ist es wichtig, dass Ihr Unternehmen diese Präferenz beim Generieren von Zielgruppen für Marketing-Aktivitäten berücksichtigt. In diesem Dokument wird beschrieben, wie Sie Kundeneinverständniswerte mithilfe der Experience Platform-Benutzeroberfläche in Ihre Segmentdefinitionen integrieren.

## Erste Schritte

Die Berücksichtigung der Werte des Kundeneinverständnisses setzt ein Verständnis der verschiedenen [!DNL Adobe Experience Platform]-Services voraus. Bevor Sie mit diesem Tutorial beginnen, stellen Sie sicher, dass Sie mit den folgenden Services vertraut sind:

* [[!DNL Experience Data Model (XDM)]](../xdm/home.md): Das standardisierte Framework, mit dem Kundenerlebnisdaten von Platform organisiert werden.
* [[!DNL Real-Time Customer Profile]](../profile/home.md): Bietet ein einheitliches Kundenprofil in Echtzeit, das auf aggregierten Daten aus verschiedenen Quellen basiert.
* [[!DNL Adobe Experience Platform Segmentation Service]](./home.md): Ermöglicht das Erstellen von Zielgruppen aus [!DNL Real-Time Customer Profile].

## Felder des Einverständnisschemas

Um das Einverständnis und die Voreinstellungen des Kunden zu berücksichtigen, muss eines der Schemata, das Teil Ihres [!UICONTROL XDM Individual Profile]-Vereinigungsschemas ist, die Standardfeldgruppe (Einverständnisse **[!UICONTROL Voreinstellungen]** enthalten.

Details zur Struktur und zum vorgesehenen Anwendungsfall der einzelnen Attribute der Feldergruppe finden Sie im [Referenzhandbuch zu Einverständnissen und Voreinstellungen](../xdm/field-groups/profile/consents.md). Eine schrittweise Anleitung zum Hinzufügen einer Feldergruppe zu einem Schema finden Sie im [Handbuch zur XDM-Benutzeroberfläche](../xdm/ui/resources/schemas.md#add-field-groups).

Nachdem die Feldergruppe zu einem [profilaktivierten Schema hinzugefügt ](../xdm/ui/resources/schemas.md#profile) und ihre Felder zum Aufnehmen von Einverständnisdaten aus Ihrer Erlebnisanwendung verwendet wurden, können Sie die erfassten Einverständnisattribute in Ihren Segmentregeln verwenden.

## Umgang mit dem Einverständnis in der Segmentierung

Um sicherzustellen, dass abgemeldete Profile nicht in Segmentdefinitionen enthalten sind, müssen spezielle Felder zu vorhandenen Segmentdefinitionen hinzugefügt und bei der Erstellung neuer Segmentdefinitionen einbezogen werden.

Die folgenden Schritte zeigen, wie Sie die entsprechenden Felder für zwei Arten von Opt-out-Flags hinzufügen:

1. [!UICONTROL Datenerfassung]
1. [!UICONTROL Daten freigeben]

>[!NOTE]
>
>Während sich dieses Handbuch auf die beiden oben genannten Opt-out-Flags konzentriert, können Sie Ihre Segmentdefinitionen so konfigurieren, dass auch zusätzliche Einverständnissignale einbezogen werden. Das [Referenzhandbuch zu Einverständnissen und Voreinstellungen](../xdm/field-groups/profile/consents.md) enthält weitere Informationen zu den einzelnen Optionen und den vorgesehenen Anwendungsfällen.

Navigieren Sie beim Erstellen einer Segmentdefinition in der Benutzeroberfläche unter **[!UICONTROL Attribute]** zu **[!UICONTROL Individuelles XDM-Profil]** und wählen Sie dann **[!UICONTROL Zustimmung und Voreinstellungen]** aus. Von hier aus können Sie die Optionen für **[!UICONTROL Datenerfassung]** und **[!UICONTROL Daten freigeben]** sehen.

![](./images/opt-outs/consents.png)

Wählen Sie zunächst die Kategorie **[!UICONTROL Datenerfassung]** aus und ziehen Sie dann **[!UICONTROL Auswahlwert]** in Segment Builder. Beim Hinzufügen des Attributs zur Segmentdefinition können Sie die [Einverständniswerte“ angeben](../xdm/field-groups/profile/consents.md#choice-values) die ein- oder ausgeschlossen werden müssen.

![](./images/opt-outs/consent-values.png)

Ein Ansatz besteht darin, Kunden auszuschließen, die sich gegen die Erfassung ihrer Daten entschieden haben. Setzen Sie dazu den Operator auf **[!UICONTROL ungleich]** und wählen Sie die folgenden Werte:

* **[!UICONTROL Nein (Opt-out)]**
* **[!UICONTROL Standard von „Nein“ (Opt-out)]**
* **[!UICONTROL Unbekannt]** (wenn davon ausgegangen wird, dass die Zustimmung verweigert wird, wenn sie anderweitig unbekannt ist)

![](./images/opt-outs/collect.png)

Navigieren **[!UICONTROL in]** linken Leiste unter „Attribute“ zurück zum Abschnitt **[!UICONTROL Einverständnisse und Voreinstellungen]** und wählen Sie dann **[!UICONTROL Daten freigeben]**. Ziehen Sie den entsprechenden **[!UICONTROL Auswahlwert]** auf die Arbeitsfläche und wählen Sie dieselben Werte wie für den Auswahlwert [!UICONTROL Datenerfassung] aus. Stellen Sie sicher, dass eine **[!UICONTROL Oder]**-Beziehung zwischen den beiden Attributen hergestellt wird.

![](./images/opt-outs/share.png)

Da die Einverständniswerte **[!UICONTROL Datenerfassung]** und **[!UICONTROL Daten freigeben]** zur Segmentdefinition hinzugefügt wurden, werden alle Kundinnen und Kunden, die sich gegen die Verwendung ihrer Daten entschieden haben, aus der resultierenden Audience ausgeschlossen. Von hier aus können Sie mit der Anpassung der Segmentdefinition fortfahren, bevor Sie **[!UICONTROL Speichern]** auswählen, um den Prozess abzuschließen.

## Nächste Schritte

Durch Befolgen dieses Tutorials sollten Sie jetzt besser verstehen, wie Sie das Einverständnis und die Voreinstellungen von Kunden beim Erstellen von Segmentdefinitionen in Experience Platform berücksichtigen können.

Weitere Informationen zur Verwaltung des Einverständnisses in Platform finden Sie in der folgenden Dokumentation:

* [Einverständnisverarbeitung mit dem Adobe-Standard](../landing/governance-privacy-security/consent/adobe/overview.md)
* [Einverständnisverarbeitung mit dem IAB TCF 2.0-Standard](../landing/governance-privacy-security/consent/iab/overview.md)