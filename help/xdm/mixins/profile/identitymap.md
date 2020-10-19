---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;individual profile;fields;schemas;Schemas;identityMap;identity map;Identity map;Schema design;map;Map;union schema;union
solution: Experience Platform
title: IdentityMap mixin
topic: overview
description: Dieses Dokument bietet einen Überblick über die XDM Individual Profil-Klasse.
translation-type: tm+mt
source-git-commit: fd5bd4134bd35d5d87c79bf1e75bc88c67511b2b
workflow-type: tm+mt
source-wordcount: '96'
ht-degree: 0%

---


# [!UICONTROL IdentityMap] mixin

[!UICONTROL IdentityMap] ist ein Standard-Mixin für die [[!DNL XDM Individual Profile] Klasse](../../classes/individual-profile.md). Das Mixin bietet ein einzelnes Kartenfeld, das eine Reihe von Benutzeridentitäten enthält, die vom Namensraum festgelegt werden.

>[!WARNING]
>
>Das `IdentityMap` Feld wird vom System automatisch aktualisiert, wenn Identitätsdaten erfasst werden. Um dieses Feld für [Echtzeit-Kundendaten](../../../profile/home.md)richtig zu verwenden, sollten Sie nicht versuchen, den Feldinhalt in Ihren Datenvorgängen manuell zu aktualisieren.

<img src="../../images/mixins/identitymap.png" width="600" /><br />

Weitere Informationen zum Anwendungsfall finden Sie im Abschnitt zu Identitätskarten in den [Grundlagen der Schema-Komposition](../../schema/composition.md#identityMap) .