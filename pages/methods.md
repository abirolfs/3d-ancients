---
title: Methods
layout: methods
permalink: /methods.html
---

# 3D Ancients - Methods
<br>
## CollectionBuilder-CSV Framework
This digital collection was developed utilizing the CollectionBuilder-CSV framework. All collection metadata is contained within a single CSV file, which CollectionBuilder uses to build out the individual items. Several customizations were made, such as adjusting the content and options that appear on site pages and navigation, as well as implementing a custom template for 3D models that originate on SketchFab. For more information about CollectionBuilder, [click here to visit the CollectionBuilder website](https://collectionbuilder.github.io/), and [click here to access the CollectionBuilder-CSV source code](https://github.com/CollectionBuilder/collectionbuilder-csv).

<br>
## Embedding models from SketchFab
SketchFab is an online, public repository for 3D models and assets. While CollectionBuilder-CSV does have an official add-on for including 3D models, it does not have a built-in way to include SketchFab models through an embed link. To add this functionality, a custom means of including SketchFab embeds was developed. The custom template files can be found in the [GitHub repository for this site](https://github.com/abirolfs/3d-ancients) under _layouts/item/[sketchfab_model.html](https://github.com/abirolfs/3d-ancients/blob/main/_layouts/item/sketchfab_model.html) and _includes/item/[sketchfab-embed.html](https://github.com/abirolfs/3d-ancients/blob/main/_includes/item/sketchfab-embed.html). You can also find the code for these template files at the bottom of this page.

In order to add an item as a SketchFab embed, one must do the following in the metadata CSV:
- Enter “sketchfab_model” under the “display_template” field for that specific item
- Enter the embed link under the “object_location” field for that specific item
    - The embed link is acquired on SketchFab through selecting the desired model, selecting“Embed” under the Model's viewer, then copying the link located in the first iframe tag of the embed code after “src=”. The screenshots below demonstrate this process.

![Screenshot of the SketchFab interface, highlighting the Embed button](assets/img/sf-embed-button-screenshot.jpg) ![Screenshot of the SketchFab interface, highlighting the Embed link](assets/img/sf-embed-link-screenshot.jpg)

#### SketchFab Embed Code
<br>
**[sketchfab_model.html](https://github.com/abirolfs/3d-ancients/blob/main/_layouts/item/sketchfab_model.html)**
<br>
{% raw %}
   
    ---
    # basic layout for sketchfab models
    # assumes Item has the SketchFab embed link in the "object_location" value
    layout: item/item-page-base
    ---

    <div class="card mb-4 text-center">

        {% include item/sketchfab-embed.html title = page.title model_url=page.object_location %}

    </div>

{% endraw %}
<br>
**[sketchfab-embed.html](https://github.com/abirolfs/3d-ancients/blob/main/_includes/item/sketchfab-embed.html)**
<br>
{% raw %}

    <div class="sketchfab-embed">
        <iframe
            title= "{{ include.title | default: 'Model title' }}"
            height = 600px
            width = 100%
            frameborder="0"
            allowfullscreen
            mozallowfullscreen="true"
            webkitallowfullscreen="true"
            allow="autoplay; fullscreen; xr-spatial-tracking"
            xr-spatial-tracking
            execution-while-out-of-viewport
            execution-while-not-rendered
            web-share
            src= "{{ include.model_url | relative_url }}"
        >
        </iframe>
    </div>

{% endraw %}
