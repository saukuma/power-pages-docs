---
title: Create and manage web files
description: Learn how to create and manage web files in Power Pages.
author: sandhangitmsft

ms.topic: conceptual
ms.custom: 
ms.date: 04/12/2023
ms.subservice: 
ms.author: sandhan
ms.reviewer: ndoelman
contributors:
    - nickdoelman
    - sandhangitmsft
    - ProfessorKendrick
---

# Create and manage web files

A web file represents downloadable file in a website, used to store images, documents, and any other file types.

To store the actual contents of a given file, Power Pages uses the attachment feature of the notes associated with a web file record. The file attachment of the newest note associated with the web file is used as the file content. As such, the size of web file content that can be supported by Power Pages is determined by the note attachment size supported by your Dataverse environment configuration.

## Manage web files

Web files can be created, edited, and deleted within Power Pages.

1. Open the [Portal Management app](./portal-management-app.md).

1. Go to **Content** > **Web Files**.

1. To create a new web file, select **New**.

1. To edit an existing web file, select the web file name.

1. Enter appropriate values in the fields.

1. Select **Save & Close**.

> [!WARNING]
> - If you plan to [migrate your site](../admin/migrate-portal-configuration.md) to another environment, ensure that the target environment's maximum attachment size is set to the same or greater size as your source environment. 
>- The maximum size of files is determined by the **Maximum file size** setting in the [system settings email tab](/power-platform/admin/system-settings-dialog-box-email-tab) in the environment system settings dialog box.

### Web file attributes

The table below explains many of the standard web file attributes used by Power Pages. It's important to note that the way in which many of the content/display-oriented attributes are rendered is controlled by the page template used, and thus by the Power Pages developer.

| Name                | Description               |
|---------------------|-----------------------|
|Name |The descriptive name of the table. This value will be used as the file title in most templates (for example, for link titles). This field is required.   |
|Website   |The website to which the table belongs. This field is required.   |
|Parent Page   |The parent Web Page of the table, in the website content hierarchy. <br>While a file isn't required to have a parent page – in some scenarios, for example, a file may have a parent blog post instead – providing a parent page is the recommended configuration in most cases.  |
|Partial URL   |The URL path segment used to build the website URL of this page. <br>The single root (Home) page of your website – the single page that has no associated Parent Page – must have a Partial URL value of /.<br>Partial URL values are used as URL path segments. As such, they shouldn't contain illegal URL path characters, such as ?, #, !, %. Since Power Pages URLs are generated by joining together partial URL values with slashes (/), they should also not generally contain slashes. Recommended practice would be to restrict partial URL values to letters, numbers, and hyphens or underscores. For example: press-release.pdf, Site_Header.png.  |
|Publishing State   |The current publishing workflow state of the file, which may dictate whether or not the file is visible on the site. The most common use of this feature is to provide published/draft control over content.<br>Users with content management permissions may be granted the ability to use preview Mode, which allows these users to see (preview) unpublished content.   |
| Display Date        | This attribute is a date/time value that can be used by a template, purely for display purposes. It has no functional implications, but can be useful for things like, for example, manually specifying a published date on a press release document.    |
| Release Date        | Controls a date/time after which the file will be visible on the website. If the current date/time is prior to this date, this file won't be visible. (The exception to this is that users with content management permissions may be granted the ability to use preview Mode, which allows these users to see (preview) unreleased content.) This is useful for controlling the release of time-sensitive content, like news or press releases. |
| Expiration Date     | Controls a date/time prior to which the file will be visible on the website. If the current date/time is after this date, this file won't be visible. (The exception to this is that users with content management permissions may be granted the ability to use Preview Mode, which allows these users to see (preview) expired content.)                |
| Summary             | A short description for the file, this value will generally be used to add a description of the file to website navigational elements that render a link to the file.      |
| Hidden from Sitemap | Controls whether or not the file is visible has part of the site map. If this value is checked, the file will still be available on the site at its URL, and can be linked to, but standard navigational elements (menus, etc.) won't include the page.      |
| Display Order       | An integer value indicating the order in which the file will be placed, relative to other tables with the same Parent Page. This controls the ordering of files and other site map tables when, for example, a list of links to the child tables of a given page are rendered on the website.      |
| Cloud Blob Address  | A text value in the format `<container>/<filename>`, indicating that the content for this file is stored in Azure Blob Storage.        |
| Content-Disposition | Options are inline or attachment. If inline is specified, the browser should attempt to render it within the browser window and if it can't, it will prompt the user to download or open the file. If attachment is specified, it will immediately prompt the user to download or open the file, and not try to load it in the browser, whether it can or not.                                                                                        |
| Enable Tracking (Deprecated)     | This feature is deprecated and no longer functional. |
|||

## Add a download link

To embed a file download link on a web page, web template, or content snippet from a web file record, you can add the following HTML code:

`<a href="/<<partial url of web file record>>"><<Description of link>>/a>`

For example, if the partial URL of the web file is *user-manual.pdf*:

`<a href="/user-manual.pdf">Select here to download the user manual</a>`

> [!NOTE]
> The permissions to access the file to be downloaded is controlled by the parent page permissions. For more information, see [Manage page permissions](../security/page-security.md#apply-these-permissions-to-all-files-inherited-by-this-page).