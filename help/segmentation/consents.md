---
solution: Experience Platform
title: Einverständniserklärung in Segmenten
description: Erfahren Sie, wie Sie die Zustimmungseinstellungen von Kunden für die Erfassung und Freigabe personenbezogener Daten in Segmentvorgängen berücksichtigen.
exl-id: fe851ce3-60db-4984-a73c-f9c5964bfbad
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '672'
ht-degree: 0%

---

# Einverständniserklärung in Segmenten

>[!NOTE]
>
>In diesem Handbuch wird erläutert, wie Sie Einwilligungen in **Segmentdefinitionen** berücksichtigen können.

Durch gesetzliche Datenschutzbestimmungen wie den [!DNL California Consumer Privacy Act] (CCPA) haben Verbraucher das Recht, sich gegen die Erfassung oder Weitergabe personenbezogener Daten an Dritte zu entscheiden. Adobe Experience Platform bietet standardmäßige Experience-Datenmodell (XDM)-Komponenten, mit denen diese Voreinstellungen bezüglich der Kundenzustimmung in Echtzeit-Kundenprofildaten erfasst werden sollen.

Wenn ein Kunde die Freigabe seiner personenbezogenen Daten widerrufen oder verweigert hat, muss Ihr Unternehmen diese Voreinstellung beim Generieren von Zielgruppen für Marketingaktivitäten berücksichtigen. In diesem Dokument wird beschrieben, wie Sie mithilfe der Experience Platform-Benutzeroberfläche Kundenzustimmungswerte in Ihre Segmentdefinitionen integrieren.

## Erste Schritte

Die Einhaltung der Zustimmungswerte von Kunden erfordert ein Verständnis der verschiedenen beteiligten [!DNL Adobe Experience Platform]-Dienste. Bevor Sie mit diesem Tutorial beginnen, sollten Sie mit den folgenden Diensten vertraut sein:

* [[!DNL Experience Data Model (XDM)]](../xdm/home.md): Das standardisierte Framework, mit dem Platform Kundenerlebnisdaten organisiert.
* [[!DNL Real-Time Customer Profile]](../profile/home.md): Bietet ein einheitliches Kundenprofil in Echtzeit, das auf aggregierten Daten aus mehreren Quellen basiert.
* [[!DNL Adobe Experience Platform Segmentation Service]](./home.md): Ermöglicht Ihnen das Erstellen von Zielgruppen aus [!DNL Real-Time Customer Profile] -Daten.

## Einverständnisschemafelder

Um Kundeneinwilligungen und -einstellungen zu berücksichtigen, muss eines der Schemas, das Teil Ihres Vereinigungsschemas für [!UICONTROL XDM Individual Profile] ist, die Standardfeldgruppe **[!UICONTROL Einverständnisse und Voreinstellungen]** enthalten.

Weitere Informationen zur Struktur und zum vorgesehenen Anwendungsfall der einzelnen Attribute, die von der Feldergruppe bereitgestellt werden, finden Sie im Referenzhandbuch für [Einwilligungen und Voreinstellungen](../xdm/field-groups/profile/consents.md). Eine schrittweise Anleitung zum Hinzufügen einer Feldergruppe zu einem Schema finden Sie im [XDM UI-Handbuch](../xdm/ui/resources/schemas.md#add-field-groups).

Nachdem die Feldergruppe einem [Profil-aktivierten Schema](../xdm/ui/resources/schemas.md#profile) hinzugefügt wurde und die Felder zum Erfassen von Einwilligungsdaten aus Ihrer Erlebnisanwendung verwendet wurden, können Sie die erfassten Zustimmungsattribute in Ihren Segmentregeln verwenden.

## Umgang mit Zustimmung in der Segmentierung

Damit Opt-out-Profile nicht in Segmentdefinitionen enthalten sind, müssen bestehende Segmentdefinitionen um spezielle Felder ergänzt und bei der Erstellung neuer Segmentdefinitionen einbezogen werden.

Die folgenden Schritte zeigen, wie Sie die entsprechenden Felder für zwei Arten von Opt-out-Flags hinzufügen:

1. [!UICONTROL Datenerfassung]
1. [!UICONTROL Daten freigeben]

>[!NOTE]
>
>Während sich dieses Handbuch auf die beiden oben genannten Opt-out-Flags konzentriert, können Sie Ihre Segmentdefinitionen so konfigurieren, dass auch zusätzliche Zustimmungssignale einbezogen werden. Das Referenzhandbuch [Einverständnisse und Voreinstellungen](../xdm/field-groups/profile/consents.md) enthält weitere Informationen zu den einzelnen Optionen und den beabsichtigten Anwendungsfällen.

Navigieren Sie beim Erstellen einer Segmentdefinition in der Benutzeroberfläche unter **[!UICONTROL Attribute]** zu **[!UICONTROL XDM Individual Profile]** und wählen Sie dann **[!UICONTROL Einverständnisse und Voreinstellungen]** aus. Von hier aus können Sie die Optionen für **[!UICONTROL Datenerfassung]** und **[!UICONTROL Daten freigeben]** sehen.

![](./images/opt-outs/consents.png)

Wählen Sie zunächst die Kategorie **[!UICONTROL Datenerfassung]** aus und ziehen Sie dann **[!UICONTROL Auswahlwert]** in den Segment-Builder. Beim Hinzufügen des Attributs zur Segmentdefinition können Sie die [Zustimmungswerte](../xdm/field-groups/profile/consents.md#choice-values) angeben, die ein- oder ausgeschlossen werden müssen.

![](./images/opt-outs/consent-values.png)

Ein Ansatz besteht darin, alle Kunden auszuschließen, die sich gegen die Erfassung ihrer Daten entschieden haben. Setzen Sie dazu den Operator auf **[!UICONTROL ist nicht gleich]** und wählen Sie die folgenden Werte:

* **[!UICONTROL Nein (Opt-out)]**
* **[!UICONTROL Standardwert von Nein (Opt-out)]**
* **[!UICONTROL Unbekannt]** (wenn angenommen wird, dass die Einwilligung verweigert wird, falls nicht anders bekannt)

![](./images/opt-outs/collect.png)

Navigieren Sie unter &quot;**[!UICONTROL Attribute]**&quot;in der linken Leiste zurück zum Abschnitt &quot;**[!UICONTROL Einverständnisse und Voreinstellungen]**&quot;und wählen Sie dann &quot;**[!UICONTROL Daten freigeben]**&quot;. Ziehen Sie den entsprechenden **[!UICONTROL Auswahlwert]** in die Arbeitsfläche und wählen Sie dieselben Werte wie für den Auswahlwert [!UICONTROL Datenerfassung] aus. Stellen Sie sicher, dass zwischen den beiden Attributen eine **[!UICONTROL Oder]** -Beziehung hergestellt wird.

![](./images/opt-outs/share.png)

Wenn sowohl die Zustimmungswerte **[!UICONTROL Datenerfassung]** als auch **[!UICONTROL Daten freigeben]** zur Segmentdefinition hinzugefügt werden, werden alle Kunden, die sich gegen die Verwendung ihrer Daten entschieden haben, von der resultierenden Zielgruppe ausgeschlossen. Von hier aus können Sie die Segmentdefinition weiter anpassen, bevor Sie **[!UICONTROL Speichern]** auswählen, um den Prozess abzuschließen.

## Nächste Schritte

Durch Befolgung dieses Tutorials sollten Sie jetzt ein besseres Verständnis dafür haben, wie Sie Kundenzustimmungen und -präferenzen beim Erstellen von Segmentdefinitionen in Experience Platform berücksichtigen können.

Weitere Informationen zur Verwaltung von Einwilligungen in Platform finden Sie in der folgenden Dokumentation:

* [Einverständnisverarbeitung mit dem Adobe-Standard](../landing/governance-privacy-security/consent/adobe/overview.md)
* [Einverständnisverarbeitung mit dem IAB TCF 2.0-Standard](../landing/governance-privacy-security/consent/iab/overview.md)