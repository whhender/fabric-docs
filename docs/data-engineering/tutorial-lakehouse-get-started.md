---
title: Lakehouse tutorial - Create a workspace
description: Learn how to create a workspace that you can use to create other items required by this end-to-end tutorial.
ms.reviewer: sngun
ms.author: arali
author: ms-arali
ms.topic: tutorial
ms.custom:
  - build-2023
  - ignite-2023
ms.date: 5/23/2023
---

# Lakehouse tutorial: Create a Fabric workspace

Before you can begin creating the lakehouse, you need to create a workspace where you can build out the remainder of the tutorial.

## Prerequisites

Sign up for the free [Microsoft Fabric trial](../get-started/fabric-trial.md). For public preview, the Fabric (Preview) trial requires a Power BI license. If you don't have one, [sign up for a Power BI free license,](https://app.fabric.microsoft.com) and then you can start the Fabric (Preview) trial.

## Create a workspace

In this step, you create a Fabric workspace. The workspace contains all the items needed for this lakehouse tutorial, which includes lakehouse, dataflows, Data Factory pipelines, the notebooks, Power BI semantic models, and reports.

1. Sign in to [Power BI](https://powerbi.com/).

1. Select **Workspaces** and **New workspace**.

   :::image type="content" source="media\tutorial-lakehouse-get-started\create-new-workspace.png" alt-text="Screenshot showing where to select Workspaces and create a new workspace.":::

1. Fill out the **Create a workspace** form with the following details:

   * **Name:** Enter *Fabric Lakehouse Tutorial*, and any extra characters to make the name unique.

   * **Description**: Enter an optional description for your workspace.

      :::image type="content" source="media\tutorial-lakehouse-get-started\create-workspace-details.png" alt-text="Screenshot of the Create a workspace dialog box.":::

   * **Advanced**: Under **License mode**, select **Premium capacity** and then choose a premium capacity that you have access to.

      :::image type="content" source="media\tutorial-lakehouse-get-started\select-premium-capacity.png" alt-text="Screenshot of the Advanced options dialog box.":::

1. Select **Apply** to create and open the workspace.

## Next steps

Advance to the next article to learn about
> [!div class="nextstepaction"]
> [Create a lakehouse in Microsoft Fabric](tutorial-build-lakehouse.md)
