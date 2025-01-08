# Component Field Structure Documentation

This document provides details on creating and using the field structure for components. Each field type has specific attributes and rules that must be followed to ensure correct functionality.

## Field Structure Overview

The structure for defining fields is an array of objects where each object represents a field with the following properties:

- **type**: Specifies the field type (e.g., `text`, `textarea`, `select`, `colorpicker`).
- **name**: A unique identifier for the field.
- **label**: An object containing translations for the field's label.
- **required**: A boolean indicating if the field is mandatory.
- **rules**: Validation rules for the field.

### Default Data

- **default_data**: It is **required** to include this property for each field, even if no default value is provided. This ensures that all fields are properly defined, and no field is left out. If a field does not have a default value, you should include it with an empty value (e.g., `null`, `""`, or `0`). The `default_data` property helps ensure consistency across the structure and prevents issues during form rendering or processing.

### Example Field Structure in JSON Format

```json
{
    "fields": [
        {
            "type": "text",
            "name": "title",
            "label": {
                "en": "title",
                "pt-br": "title",
                "fr": "title"
            },
            "required": false,
            "rules": "nullable|min:3|max:200"
        },
        {
            "type": "textarea",
            "name": "description",
            "label": {
                "en": "description",
                "pt-br": "description",
                "fr": "description"
            },
            "required": false,
            "rules": "nullable|min:3|max:1000"
        }
    ],
    "default_data": {
        "title": "",
        "description": ""
    }
}
```

## HTML Field

#### Description
The **HTML** field allows the user to input any content they desire, including HTML tags, plain text, or even Blade syntax. This gives users the flexibility to add complex content, including dynamic data, within the HTML editor.

### Blade Syntax Usage

When using the HTML field, the user may add content such as:

```html
<h1>{{ $data->title }}</h1>
<p>{{ $data->description }}</p>
````

You may also use any blade code syntax inside of it:


```html
@if (count($records) === 1)
    I have one record!
@elseif (count($records) > 1)
    I have multiple records!
@else
    I don't have any records!
@endif
````

[See more of blade syntax here.](https://laravel.com/docs/11.x/blade)


## Field Types and Usage

### 1. **Text Field**

#### Description
A basic text input field.

#### Attributes
- **name**: Unique identifier for the field.
- **label**: Multi-language labels for the field.
- **required**: Boolean to determine if the field is mandatory.
- **rules**: Validation rules (e.g., `nullable|min:3|max:200`).

#### Example
```json
{
    "type": "text",
    "name": "classes",
    "label": {
        "en": "Add classes to component",
        "pt-br": "Adicionar classes ao componente",
        "fr": "Ajouter des classes au composant"
    },
    "required": false,
    "rules": "nullable|min:3|max:200"
}
```

---

### 2. **Textarea Field**

#### Description
A multi-line text input.

#### Attributes
- Same as the text field.

#### Example
```json
{
    "type": "textarea",
    "name": "description",
    "label": {
        "en": "description",
        "pt-br": "description",
        "fr": "description"
    },
    "required": false,
    "rules": "nullable|min:3|max:1000"
}
```

---

### 3. **Select Field**

#### Description
A dropdown menu to select from predefined options.

#### Attributes
- **options.values**: Array of selectable values.
- **options.labels**: Translations for the values.

#### Example
```json
{
    "type": "select",
    "name": "title_position",
    "label": {
        "en": "title position",
        "pt-br": "posição do título",
        "fr": "position du titre"
    },
    "required": true,
    "options": {
        "values": ["left", "center", "right"],
        "labels": [
            { "en": "left", "pt-br": "esquerda", "fr": "gauche" },
            { "en": "center", "pt-br": "centro", "fr": "centre" },
            { "en": "right", "pt-br": "direita", "fr": "droite" }
        ]
    },
    "rules": "required|in:left,center,right"
}
```

---

### 4. **Colorpicker Field**

#### Description
A color selection input.

#### Attributes
- **rules**: Validation for color format (e.g., `nullable|string`).

#### Example
```json
{
    "type": "colorpicker",
    "name": "section_bg_color",
    "label": {
        "en": "Section Background Color",
        "pt-br": "Cor de fundo da seção",
        "fr": "Couleur de fond de la section"
    },
    "required": false,
    "rules": "nullable|string"
}
```
---

### Switch Field

**Description:**  
A toggle switch for enabling or disabling options.

**Attributes:**
- **name**: Unique identifier for the field.
- **label**: Multi-language labels for the field.
- **required**: Boolean to determine if the field is mandatory.
- **rules**: Validation rules (e.g., `nullable|boolean`).

**Example:**
```json
{
    "type": "switch",
    "name": "show_search",
    "label": {
        "en": "Enable Searchbar",
        "pt-br": "Ativar Barra de Pesquisa",
        "fr": "Activer la Barre de Recherche"
    },
    "required": false,
    "rules": "nullable|boolean"
}

```

### File Field

#### Description
A file input field that allows the user to upload a file, such as an image or video. You can specify accepted file types and size limitations.

#### Attributes
- **name**: Unique identifier for the field.
- **label**: Multi-language labels for the field.
- **required**: Boolean to determine if the field is mandatory.
- **rules**: Validation rules for file types and size (e.g., `nullable|mimes:jpg,jpeg,png,webp,video/mp4|max:10000`).
- **accept**: Specifies the allowed MIME types (e.g., `video/mp4,image/jpg`).
- **size**: Maximum file size (e.g., `10MB`).

#### Example
```json
{
    "type": "file",
    "name": "file",
    "label": {
        "en": "Upload an image or video (max size: 10MB)",
        "pt-br": "Carregar uma imagem ou vídeo (tamanho máximo: 10MB)",
        "fr": "Télécharger une image ou une vidéo (taille max: 10MB)"
    },
    "required": false,
    "rules": "nullable|mimes:jpg,jpeg,png,webp,video/mp4,video/webm,video/ogg,video/x-msvideo,video/quicktime,video/mpeg|max:10000",
    "accept": "video/mp4,video/webm,video/ogg,video/x-msvideo,video/quicktime,video/mpeg",
    "size": "10MB"
}
```

## Notes
- Ensure all `name` fields are unique across the structure.
- Use appropriate `rules` for field validation.
- Multi-language support is enabled using the `label` object.

Feel free to expand this documentation for additional field types or specific requirements!

