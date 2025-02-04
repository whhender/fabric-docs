---
title: Configure Amazon S3 in a copy activity
description: This article explains how to copy data using Amazon S3.
author: jianleishen
ms.author: jianleishen
ms.topic: how-to
ms.date: 11/15/2023
ms.custom:
  - template-how-to
  - build-2023
  - ignite-2023
---

# Configure Amazon S3 in a copy activity

This article outlines how to use the copy activity in a data pipeline to copy data from and to Amazon S3.

## Required permissions

To copy data from Amazon S3, make sure you've been granted the following permissions for Amazon S3 object operations: `s3:GetObject` and `s3:GetObjectVersion`.

In addition, `s3:ListAllMyBuckets` and `s3:ListBucket`/`s3:GetBucketLocation` permissions are required for operations like testing connection and browsing from root.

For the full list of Amazon S3 permissions, go to [Specifying Permissions in a Policy on the AWS site](https://docs.aws.amazon.com/AmazonS3/latest/userguide/using-with-s3-actions.html).

## Supported format

Amazon S3 supports the following file formats. Refer to each article for format-based settings.

- [Avro format](format-avro.md)
- [Binary format](format-binary.md)
- [Delimited text format](format-delimited-text.md)
- [Excel format](format-excel.md)
- [JSON format](format-json.md)
- [ORC format](format-orc.md)
- [Parquet format](format-parquet.md)
- [XML format](format-xml.md)

## Supported configuration

For the configuration of each tab under copy activity, go to the following sections respectively.

- [General](#general)  
- [Source](#source)
- [Mapping](#mapping)
- [Settings](#settings)

### General

For **General** tab configuration, go to [General](activity-overview.md#general-settings).

### Source

The following properties are supported for Amazon S3 under the **Source** tab of a copy activity.

:::image type="content" source="./media/connector-amazon-s3/source.png" alt-text="Screenshot showing source tab and the list of properties." lightbox="./media/connector-amazon-s3/source.png":::

The following properties are **required**:

- **Data store type**: Select **External**.
- **Connection**: Select an **Amazon S3** connection from the connection list. If no connection exists, then create a new Amazon S3 connection by selecting **New**.
- **File path**: Select **Browse** to choose the file that you want to copy, or fill in the path manually.
- **File settings**: Select **File settings** to configure the file format. For settings of different file formats, refer to [Supported format](#supported-format) for detailed information.

Under **Advanced**, you can specify the following fields:

- **File path type**: You can choose **File path**, **Prefix**, **Wildcard file path**, or **List of files** as your file path type. The configuration of each of these settings is:

  - **File path**: If you choose this type, the data can be copied from the given container or folder/file path specified previously.

  - **Prefix**: Prefix for the S3 key name under the given bucket configured to filter source S3 files. S3 keys whose names start with `bucket/this_prefix` are selected. It utilizes S3's service-side filter, which provides better performance than a wildcard filter.

      :::image type="content" source="./media/connector-amazon-s3/prefix.png" alt-text="Screenshot showing prefix." lightbox="./media/connector-amazon-s3/prefix.png":::

  - **Wildcard file path**: Specify the folder or file path with wildcard characters under your given blob container to filter your source folders or files.

    Allowed wildcards are: `*` (matches zero or more characters) and `?` (matches zero or single character). Use `^` to escape if your folder name has wildcard or this escape character inside.

    - Wildcard folder path: The folder path with wildcard characters under the given bucket configured to filter source folders.

      :::image type="content" source="./media/connector-amazon-s3/wildcard-folder-path.png" alt-text="Screenshot showing wildcard file path." lightbox="./media/connector-amazon-s3/wildcard-folder-path.png":::

    - Wildcard file name: The file name with wildcard characters under the given bucket and folder path (or wildcard folder path) to filter source files.

  - **List of files**: Indicates to copy a given file set. Point to a text file that includes a list of files you want to copy, one file per line, which is the relative path to the path configured.

      :::image type="content" source="./media/connector-amazon-s3/path-to-file-list.png" alt-text="Screenshot showing list of files." lightbox="./media/connector-amazon-s3/path-to-file-list.png":::

- **Recursively**: Indicates whether the data is read recursively from the subfolders or only from the specified folder. Note that when **recursive** is set to **true** and the destination is a file-based store, an empty folder or subfolder isn't copied or created at the destination. Allowed values are **true** (default) and **false**. This property doesn't apply when you configure `fileListPath`.

- **Delete files after completion**: Indicates whether the binary files are deleted from the source store after successfully moving to the destination store. The file deletion is per file, so when a copy activity fails, you'll note some files have already been copied to the destination and deleted from the source, while others still remain on the source store. This property is only valid in the binary files copy scenario. The default value: false.

- **Max concurrent connection**: The upper limit of concurrent connections established to the data store during the activity run. Specify a value only when you want to limit concurrent connections.

### Mapping

For **Mapping** tab configuration, go to [Configure your mappings under mapping tab](copy-data-activity.md#configure-your-mappings-under-mapping-tab). If you choose Binary as your file format, mapping will not be supported.

### Settings

For the **Settings** tab configuration, go to [Configure your other settings under settings tab](copy-data-activity.md#configure-your-other-settings-under-settings-tab).

## Table summary

The following tables contain more information about the copy activity in Amazon S3.

### Source information

|Name |Description |Value|Required |JSON script property |
|:---|:---|:---|:---|:---|
|**Data store type**|Your data store type.| **External**|Yes|/|
|**Connection** |Your connection to the source data store.|\<your connection> |Yes|connection|
|**File path** | The file path of your source data.|\<file path of your source >|Yes |container <br> fileName|
|**File path type** |The file path type that you want to use.|• File path <br>• Prefix<br>• Wildcard folder path<br>•List of files|No |<br>• prefix<br>• wildcardFolderPath, wildcardFileName<br>• path to file list|
|**Recursively** |Indicates whether the data is read recursively from the subfolders or only from the specified folder. Note that when **recursive** is set to **true** and the destination is a file-based store, an empty folder or subfolder isn't copied or created at the destination. Allowed values are **true** (default) and **false**. This property doesn't apply when you configure `fileListPath`.| Selected or unselect |No |recursive|
|**Delete files after completion** |Indicates whether the binary files will be deleted from the source store after successfully moving to the destination store. The file deletion is per file, so when a copy activity fails, you'll note some files have already been copied to the destination and deleted from the source, while others still remain on the source store. This property is only valid in the binary files copy scenario. The default value: false.|Selected or unselect|No |deleteFilesAfterCompletion|
|**Max concurrent connection** |The upper limit of concurrent connections established to the data store during the activity run. Specify a value only when you want to limit concurrent connections.|\<max concurrent connections\>|No |maxConcurrentConnections|

## Next steps

[Set up your Amazon S3 connection](connector-amazon-s3.md)
