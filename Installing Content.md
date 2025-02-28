**Partner Product Install Package**

By devsupport@vectorworks.net

## Intro

Vectorworks 2021 introduced a feature called 'Install Partner Products' (as a menu command under the Help menu) that allows users to browse and install features from third-party developers.

As a developer, if you are interested in listing your products/features there, please contact us at devsupport@vectorworks.net.

## The Install Package Content

The Install Partner Products feature works with packages, provided by the developer, and uploaded on the Vectorworks online storage.

Example install packages can be downloaded at [PartnerInstallPackage_Example.zip](files/PartnerInstallPackage_Example.zip).

The third-party developer will provide one or several packages of their product. A package can, if needed, encapsulate the plugins for a Vectorworks version, Vectorworks product, OS system, and the third-party product version. For simple third-party products, there could be one package for everything, or any set of the above as needed.

The packages should be provided together with a manifest file, that contains information how a product/feature should be presented to the user and how it should be installed from the package.

### Structure

A package is a zipped up folder containing the following:

* Workspaces folder – optional. Any files there will be copied into the user’s workspace folder.
* Libraries folder – mandatory. Any files there will be copied into the user’s libraries folder. In the Libraries folder, the exact location where the desired content file should be copied is specified.

### Manifest

Here is an example structure of a manifest file. It can contain one or several product definitions, listing information about the product/feature and defining how the packages should be related to the product/feature.

**Note**: The product identifier number MUST be a new unique number to ensure that there won't be any conflicts with other products. You can use online GUID generators, like [https://www.guidgenerator.com/online-guid-generator.aspx](https://www.guidgenerator.com/online-guid-generator.aspx)

```xml
<PartnerProducts>
    <Product id="A871DD77-7272-41AF-8310-1ABBEEE28BCD">
        <Subfolder>TestPartnerProductContent</Subfolder>
        <Title>Partner Product Content</Title>
        <Category>Landscape</Category>
        <Info> This package contains Partner Product content, copied to user Libraries folder when installing</Info>
        <Image>Logo.png</Image>
        <Thumbnail>LogoThumbnail.png</Thumbnail>
        <Developer>Vectorworks Inc.</Developer>
        <Website>https://www.vectorworks.net</Website>
        <License>Free</License>
        <Version>1.0</Version>
        <ReleaseDate>1/24/2020</ReleaseDate>
        <Packages>
            <Package os="win" version="2024" product="d,a,l,s">
                PartnerProductContent.zip
            </Package>
            <Package os="mac" version="2024" product="d,a,l,s">
                PartnerProductContent.zip
            </Package>
        </Packages>
    </Product>
</PartnerProducts>
```

Each product will define:

* Id – a unique identifier of the product. Use online GUID generator, like: [https://www.guidgenerator.com/online-guid-generator.aspx](https://www.guidgenerator.com/online-guid-generator.aspx)
* Subfolder – a subfolder for the plug-ins directory
* Title – a name of the product. Can be duplicated with a 'lang' attribute for alternative titles in different languages. See the note below.
* Category – a category of the product. This will be managed by Vectorworks to keep consistency so similar products appear in similar categories. Can be duplicated with a 'lang' attribute for alternative category in different languages. See the note below.
* Info – a detailed description of the product. Can be duplicated with a 'lang' attribute for alternative info in different languages. See the note below.
* Image – a URL or BASE64 of the full size image of the product. If a BASE64 image is provided it must be prefixed by `data:image/png;base64,`. You can use online tools to generate BASE64 for an image file, like: [https://www.base64-image.de/](https://www.base64-image.de/)
* Thumbnail – optional – a URL or BASE64 of the thumbnail image of the product. If missing, the ‘Image’ will be used.
* Developer – the name of the developer/company that produced the plugin.
* Website – a URL to for more information about the product and/or the developer.
* License – a textual information about the license of the plugin. Currently every Vectorworks user will be able to install this product. Any more other licensing scheme must be implemented and supported by the developer of the plugin.
* Version – a version of the product for reference.
* ReleaseDate – the release date information for reference.
* Packages – a group defining the set of packages that will be used for this product. This could be any number of packages depending on technical or any other reasons, decided by the developer of the plugin.

Each package is listed by the name of the .zip file containing the package (the files) as defined above. Vectorworks will choose which package to be installed based on the attributes of each `<Package>` node. The first matching package will be used in the case there are overlapping attributes. The possible attributes are:

- os – optional – set to ‘win’ or ‘mac’, or left empty (or missing) would indicate both.
- vectorworks – optional – set to the version of Vectorworks which this package applies. If missing would indicate any.
- product – optional – a list of comma separated abbreviations for the Vectorworks product for which this package applies. If missing would indicate any.
  - f - Fundamentals
  - d - Designer
  - a – Architect
  - l – Landmark
  - s – Spotlight
  - c – ConnectCad
  - b – Braceworks
- lang – optional – a language for this package defined as the ISO 639-1 code. See the note below for details.
- external – optional – denotes that the install package is an OS installer, that will be downloaded and executed. Vectorworks will not be able to provide uninstaller for this feature and will ask the users to use the OS uninstall.

**Note:** The ‘Title’, ‘Category’, and ‘Info’ tags as well as the 'Package' tags can be repeated with a unique value for ‘lang’ attribute to define alternative values for different Vectorworks localizations. This attribute should contain ISO 639-1 code ([https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes)). Currently supported codes by the system are: DE, FR, JA, PL, ZN, IT, NO, PT, ES, NL, and EN. If the attribute is missing, EN is assumed.

## Adding multiple versions of a content file in one package

If it is necessary to package content for more than one version of Vectorworks, the version and os attributes should be removed from the `<Package>` tag, as shown below.

```xml
<PartnerProducts>
    <Product id="A871DD77-7272-41AF-8310-1ABBEEE28BCD">
        <Subfolder>PartnerProductContent</Subfolder>
        <Title>Partner Product Content</Title>
        <Category>Landscape</Category>
        <Info> This package contains Partner Product content, copied to user Libraries folder when installing</Info>
        <Image>Logo.png</Image>
        <Thumbnail>LogoThumbnail.png</Thumbnail>
        <Developer>Vectorworks Inc.</Developer>
        <Website>https://www.vectorworks.net</Website>
        <License>Free</License>
        <Version>1.0</Version>
        <ReleaseDate>1/24/2020</ReleaseDate>
        <Packages>
            <Package>
                PartnerProductContent.zip
            </Package>
        </Packages>
    </Product>
</PartnerProducts>
```

The following folder structure must be created and archived in a zip file:

```
Libraries\<The exact destination of the content files>
```

For example:

```
Libraries \Entertainment
          \Lighting Instruments
                         \LightSymbols2022.vwx
                         \LightSymbols2023.vwx
                         \LightSymbols2024.vwx
```

## The Process

* When the user clicks the 'Install' button:

1. The manifest will be analyzed by Vectorworks to determine which `<Package>` will be used.
2. Vectorworks will download this package and copy the content files found within it, following the directory structure set in the ZIP file.

* When the user clicks the 'Uninstall' button:

1. The content files will be removed

## Testing

For developer testing purposes a special folder will be traversed by Vectorworks to look for manifests and packages to be included in addition to the cloud content. This way a developer can create and test their installer. It’s a good idea to set a clearly identifiable category, so these extra packages can be found in the user interface.

The special folder is located (you will have to create it if it doesn't exist already) at `<user folder>/Plug-ins/Data/PartnerInstallerDev`

The developer should put one or more .xml files for the manifest, and the .zip files for the packages referenced by the manifest.

**Note:** This folder is local, only for testing purposes, to simulate the package being available.
