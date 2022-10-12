# Adds a new block with a text, text block and image to the footer.
## Can be adapted for other sections. 

**Theme**: 2.0 - Crave
**Version**: Worked in 4.0.1


???+ notes
    - This is a modified version of a new block that was used to create a button and image

---

## Before

=== "None"


## After

=== "Footer"

    ![XXXX](https://screenshot.click/11-09-18bqo-etq17.png)

---

### Step 1

Paste the following in the `{%- case block.type -%}` section of the footer.liquid section

```
{%- when 'image_with_custom_text' -%}

    {%- if block.settings.custom-text != "" -%}
      <div class="footer-block__details-content rte">
        {{ block.settings.custom-text }}
      </div>
    {%- endif -%}
  
    <div class="footer-block__details-content footer-block-image">
      {%- if block.settings.image != blank -%}
        {%- assign image_size_2x = block.settings.image_width | times: 2 | at_most: 5760 -%}
        <img
          srcset= "{{ block.settings.image | image_url: width: block.settings.image_width }}, {{ block.settings.image | image_url: width: image_size_2x }} 2x"
          src="{{ block.settings.image | image_url: width: 400 }}"
          alt="{{ block.settings.image.alt | escape }}"
          loading="lazy"
          width="{{ block.settings.image.width }}"
          height="{{ block.settings.image.height }}"
          style="max-width: min(100%, {{ block.settings.image_width }}px);"
        >
      {%- else -%}
        {{ 'image' | placeholder_svg_tag: 'placeholder-svg placeholder' }}
      {%- endif -%}
    </div>
```

### Step 2

Add in the block schema

```
{
    "type": "image_with_custom_text",
    "name": "Image with text",
    "settings": [
      {
        "type": "text",
        "id": "heading",
        "label" : "t:theme_support.settings.image_with_custom_text.heading_label"
      },
      {
        "type": "richtext",
        "id": "custom-text",
        "label": "t:theme_support.settings.image_with_custom_text.text_label"
      },
      {
        "type": "image_picker",
        "id": "image",
        "label": "t:theme_support.settings.image_with_custom_text.image_label"
      }
    ]
},
```

### Step 3

Add to the relevant locale file
```
"theme_support": {
    "settings": {
      "image_with_custom_text": {
        "heading_label": "Heading",
        "image_label": "Image",
        "text_label": "Text"
      }
    }
  }
```