---
title: Explore and transform Spark data with Data Wrangler (Preview)
description: Learn how to explore and transform Spark DataFrames with Data Wrangler, generating PySpark code in real time.
author: orbey
ms.author: erenorbey
ms.reviewer: franksolomon
ms.topic: how-to
ms.custom:
  - ignite-2023
  - ignite-2023-fabric
ms.date: 11/15/2023

ms.search.form: Data Wrangler
---

# How to use Data Wrangler on Spark DataFrames (Preview)

[Data Wrangler](data-wrangler.md), a notebook-based tool for exploratory data analysis, now supports both Spark DataFrames and pandas DataFrames, generating PySpark code in addition to Python code. For a general overview of Data Wrangler, which covers how to explore and transform pandas DataFrames, see the [the main tutorial](data-wrangler.md). The following tutorial shows how to use Data Wrangler to explore and transform Spark DataFrames.

[!INCLUDE [preview-note](../includes/feature-preview-note.md)]

## Prerequisites

[!INCLUDE [prerequisites](includes/prerequisites.md)]

## Launching Data Wrangler with a Spark DataFrame

Users can open Spark DataFrames in Data Wrangler directly from a [!INCLUDE [product-name](../includes/product-name.md)] notebook, by navigating to the same dropdown prompt where pandas DataFrames are displayed. A list of active Spark DataFrames appear in the dropdown beneath the list of active pandas variables.

The next code snippet creates a Spark DataFrame with the same sample data used in the [pandas Data Wrangler tutorial](data-wrangler.md):

```Python
import pandas as pd

# Read a CSV into a Spark DataFrame
df = spark.createDataFrame(pd.read_csv("https://raw.githubusercontent.com/plotly/datasets/master/titanic.csv"))
display(df)
```

Under the notebook ribbon "Data" tab, use the Data Wrangler dropdown prompt to browse active DataFrames available for editing. Select the one you wish to open in Data Wrangler.

> [!TIP]
> Data Wrangler cannot be opened while the notebook kernel is busy. An executing cell must finish its execution before Data Wrangler can be launched.

:::image type="content" source="media/data-wrangler-spark/launch-data-wrangler.png" alt-text="Screenshot showing a Fabric notebook with the Data Wrangler dropdown prompt." lightbox="media/data-wrangler-spark/launch-data-wrangler.png":::

## Choosing custom samples

Data Wrangler automatically converts Spark DataFrames to pandas samples for performance reasons. However, all the code generated by the tool is ultimately translated to PySpark when it exports back to the notebook. As with any pandas DataFrame, you can customize the default sample by selecting "Choose custom sample" from the Data Wrangler dropdown menu. Doing so launches a pop-up with options to specify the size of the desired sample (number of rows) and the sampling method (first records, last records, or a random set).

:::image type="content" source="media/data-wrangler-spark/launch-custom-sample.png" alt-text="Screenshot showing the Data Wrangler dropdown prompt with the custom sample option outlined." lightbox="media/data-wrangler-spark/launch-custom-sample.png":::

:::image type="content" source="media/data-wrangler-spark/choose-sample.png" alt-text="Screenshot showing the Data Wrangler custom sample prompt." lightbox="media/data-wrangler-spark/choose-sample.png":::

## Viewing summary statistics

When Data Wrangler loads, an informational banner above the preview grid reminds you that Spark DataFrames are temporarily converted to pandas samples, but all generated code is ultimately be converted to PySpark. Using Data Wrangler on Spark DataFrames is otherwise no different from using it on pandas DataFrames. A descriptive overview in the Summary panel displays information about the sample's dimensions, missing values, and more. Selecting any column in the Data Wrangler grid prompts the Summary panel to update and display descriptive statistics about that specific column. Quick insights about every column are also available in its header.

> [!TIP]
> Column-specific statistics and visuals (both in the Summary panel and in the column headers) depend on the column datatype. For instance, a binned histogram of a numeric column will appear in the column header only if the column is cast as a numeric type. Use the Operations panel to recast column types for the most accurate display.

:::image type="content" source="media/data-wrangler-spark/view-summary-panel.png" alt-text="Screenshot showing the Data Wrangler display grid and Summary panel." lightbox="media/data-wrangler-spark/view-summary-panel.png":::

## Browsing data-cleaning operations

A searchable list of data-cleaning steps can be found in the Operations panel. (A smaller selection of the same operations is also available in the contextual menu of each column.) From the Operations panel, selecting a data-cleaning step prompts you to provide a target column or columns, along with any necessary parameters to complete the step. For example, the prompt for scaling a column numerically requires a new range of values. 

:::image type="content" source="media/data-wrangler-spark/browse-operations.png" alt-text="Screenshot showing the Data Wrangler Operations panel." lightbox="media/data-wrangler-spark/browse-operations.png":::

## Previewing and applying operations

The results of a selected operation are automatically previewed in the Data Wrangler display grid, and the corresponding code automatically appears in the panel below the grid. To commit the previewed code, select "Apply" in either place. To get rid of the previewed code and try a new operation, select "Discard."

:::image type="content" source="media/data-wrangler-spark/preview-operation.png" alt-text="Screenshot showing a Data Wrangler operation in progress." lightbox="media/data-wrangler-spark/preview-operation.png":::

Once an operation is applied, the Data Wrangler display grid and summary statistics update to reflect the results. The code appears in the running list of committed operations, located in the Cleaning steps panel.

:::image type="content" source="media/data-wrangler-spark/operation-applied.png" alt-text="Screenshot showing an applied Data Wrangler operation." lightbox="media/data-wrangler-spark/operation-applied.png":::

> [!TIP]
> You can always undo the most recently applied step with the trash icon beside it, which appears if you hover your cursor over that step in the Cleaning steps panel.

:::image type="content" source="media/data-wrangler-spark/undo-operation.png" alt-text="Screenshot showing a Data Wrangler operation that can be undone." lightbox="media/data-wrangler-spark/undo-operation.png":::

The following table summarizes the operations that Data Wrangler currently supports for Spark DataFrames:

| **Operation** | **Description** |
|---|---|
| **Sort** | Sort a column in ascending or descending order |
| **Filter** | Filter rows based on one or more conditions |
| **One-hot encode** | Create new columns for each unique value in an existing column, indicating the presence or absence of those values per row |
| **One-hot encode with delimiter** | Split and one-hot encode categorical data using a delimiter |
| **Change column type** | Change the data type of a column |
| **Drop column** | Delete one or more columns |
| **Select column** | Choose one or more columns to keep, and delete the rest |
| **Rename column** | Rename a column |
| **Drop missing values** | Remove rows with missing values |
| **Drop duplicate rows** | Drop all rows that have duplicate values in one or more columns |
| **Fill missing values** | Replace cells with missing values with a new value |
| **Find and replace** | Replace cells with an exact matching pattern |
| **Group by column and aggregate** | Group by column values and aggregate results |
| **Strip whitespace** | Remove whitespace from the beginning and end of text |
| **Split text** | Split a column into several columns based on a user-defined delimiter |
| **Convert text to lowercase** | Convert text to lowercase |
| **Convert text to uppercase** | Convert text to UPPERCASE |
| **Scale min/max values** | Scale a numerical column between a minimum and maximum value |
| **Flash Fill** | Automatically create a new column based on examples derived from an existing column |

## Saving and exporting code

The toolbar above the Data Wrangler display grid provides options to save the generated code. You can copy the code to the clipboard or export it to the notebook as a function. For Spark DataFrames, all the code generated on the pandas sample is translated to PySpark before it lands back in the notebook. Before Data Wrangler closes, the tool displays a preview of the translated PySpark code and provide an option to export the intermediate pandas code as well.

> [!TIP]
> The code generated by Data Wrangler won't be applied until you manually run the new cell, and it will not overwrite your original DataFrame.

:::image type="content" source="media/data-wrangler-spark/export-code.png" alt-text="Screenshot showing the options to export code in Data Wrangler." lightbox="media/data-wrangler-spark/export-code.png":::

:::image type="content" source="media/data-wrangler-spark/convert-code.png" alt-text="Screenshot showing the PySpark preview in the export code prompt in Data Wrangler." lightbox="media/data-wrangler-spark/convert-code.png":::

:::image type="content" source="media/data-wrangler-spark/run-generated-code.png" alt-text="Screenshot showing the code generated by Data Wrangler back in the notebook." lightbox="media/data-wrangler-spark/run-generated-code.png":::

## Next steps

- To get an overview of Data Wrangler, see [this companion article](data-wrangler.md).
- To try out Data Wrangler in VS Code, see [Data Wrangler in VS Code](https://marketplace.visualstudio.com/items?itemName=ms-toolsai.datawrangler).
