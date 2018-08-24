---
title: Bot Builder basics | Microsoft Docs
description: Bot Builder SDK basic structure.
keywords: turn context, bot structure, receiving input
author: ivorb
ms.author: v-ivorb
manager: kamrani
ms.topic: article
ms.prod: bot-framework
ms.date: 04/18/2018
monikerRange: 'azure-bot-service-4.0'
---

# Basic bot structure

[!INCLUDE [pre-release-label](../includes/pre-release-label.md)]

The Azure Bot Service and Bot Builder SDK provide libraries, samples, and tools to help you build and debug bots. However, before we get into too much detail on any of those, it's important to understand the basic structure of a bot and how everything works together. These concepts apply regardless of which programming language you choose. Links to more in depth content are provided throughout; this article will provide an initial mental framework for how a bot operates.

From the ground up, let's explore the basic structure of a bot.

## Creation of your bot

A bot can be created in a variety of ways, such as within the [Azure portal](~/bot-service-quickstart.md), in [Visual Studio](~/dotnet/bot-builder-dotnet-sdk-quickstart.md), or through command-line tools for [JavaScript](~/javascript/bot-builder-javascript-quickstart.md), [Java](~/java/bot-builder-java-quickstart.md), or [Python](~/python/bot-builder-python-quickstart.md). Once created, bots can be run on a local machine, on Azure, or on another cloud service. They all function very similarly, regardless of where they're run or how they're built.

## Interaction with your bot

A bot inherently doesn't have any visible UI in the way a website or app does, and instead a user interacts with it through a [conversation](~/v4sdk/bot-concepts.md#activities-and-conversations). Depending on the application used to connect to the bot (which we call a [channel](~/v4sdk/bot-concepts.md), but we won't get into that here), certain information is sent back and forth between the user and your bot.

Each unit of information is called an **activity** within our bot, and an activity can come in various forms. Activities include both communication from the user, which is referred to as a **message**, or additional information wrapped up in a handful of other [activity types](~/bot-service-activities-entities.md). This additional information can include when a new party joins or leaves the conversation, when a conversation ends, etc. Those types of communication from the user's connection are sent by the underlying system, without the user needing to do anything.

The bot receives the communication and wraps it up in an activity object, with the correct type, to give it to your bot code. All of the other activity types provide useful information, however the most interesting and most common activity is the **message** activity from the user.

Each activity the bot receives begins a turn, which we'll describe in more detail shortly.

## Receiving user input

When we receive a message activity from the user, we need to understand what they're sending us. The most straightforward way is to simply match the incoming message text to a string. Based on which string it is, we can choose to do something, depending on what your bot is trying to achieve. This may include responding to the user, updating some variable or resource, saving it to [storage](~/v4sdk/bot-builder-storage-concept.md), or similar processing.

There are more complex ways to recognize user input, such as using [LUIS](~/v4sdk/bot-builder-concept-luis.md) or [QnA Maker](~/v4sdk/bot-builder-howto-qna.md), but string matching is the simplest.

## Defining a turn

[!INCLUDE [Define a turn](~/includes/snippet-definition-turn.md)]

Activity processing is managed by the **adapter** as described in more detail in [activity processing](~/v4sdk/bot-builder-concept-activity-processing.md). When the adapter receives an activity, it creates a **turn context** to provide information about the activity and give context to the current turn we are processing. That turn context exists for the duration of the turn, and then is disposed of, marking the end of the turn.

The [turn context](~/v4sdk/bot-builder-concept-activity-processing.md#turn-context) contains a handful of information, and the same object is used through all the layers of your bot. This is helpful because this turn context object can be, and should be, used to store information that might be needed later in the turn.

> [!IMPORTANT]
> All **turns** are independent of each other, executing on their own, and have the potential to overlap. The bot may be processing multiple turns at a time, from various users on various channels. Each turn will have it's own turn context, but it's worth considering the complexity that introduces in some situations.

## Where to go from here

This article avoided a lot of details, such as how [activities are processed](~/v4sdk/bot-builder-concept-activity-processing.md), different [conversation types](~/v4sdk/bot-builder-conversations.md), keeping track of the [state of your conversation](~/v4sdk/bot-builder-storage-concept.md) for more intelligent conversations, and so on. The rest of the conceptual topics build on the basics, and cover the rest of the ideas needed to understand both bots and the Azure Bot Service. You can follow the next steps sections to build up your knowledge, or you can jump around to what intrigues you, try out the [quickstart](~/bot-service-quickstart.md) to build your first bot, or dive into how to [develop](~/v4sdk/bot-builder-howto-send-messages.md) bots.

## Next steps

Next, the Bot Connector Service allows your bot to communicate with users on different platforms.

> [!div class="nextstepaction"]
> [Channels and the Bot Connector Service](~/v4sdk/bot-concepts.md)
