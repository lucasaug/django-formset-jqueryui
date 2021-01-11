# Django formset widget
A JQuery UI widget which adds dynamic client-side behaviour to formsets created
in Django.
This is a JQuery UI widget, and therefore requires the JQuery UI library.

## Usage
The `formset` method should be invoked in the element which contains the
subforms rendered by Django. You will also have to render the empty subform
using `formset.empty_form`, since the widget uses this empty form as a
template.
The `formset` method can take the following parameters:


| parameter          | type    | description                                                      |
| ------------------ | ------- | ---------------------------------------------------------------- |
| `prefix`           | string  | Form prefix set in Django                                        |
| `templateId`       | string  | The id for the element containing the empty subform              |
| `subformSelector`  | string  | A selector matching all the subforms to this formset             |
| `displayControls`  | boolean | Display controls to add and remove formsets                      |
| `addBtnContent`    | object  | DOM Element as a JQuery object to be used as the "add" button    |
| `rmBtnContent`     | object  | DOM Element as a JQuery object to be used as the "remove" button |
| `addBtnClass`      | string  | Class to be inserted into the "add" button                       |
| `rmBtnClass`       | string  | Class to be inserted into the "remove" button                    |

## Example
Suppose your Django template renders a supplied formset:

```
<div id="formset-container">
    {{ formset.management_form }}
    {% for subform in formset.forms %}
        <div class="subform">
            {{ subform }}
        </div>
    {% endfor %}
</div>
{% with formset.empty_form as form %}
    <!-- Empty formset (template) -->
    <div id="form-template">
        <div class="subform">
            {{ form }}
        </div>
    </div>
{% endwith %}
```

The widget setup would be done as follows:

```
$('#formset-container').formset({
    prefix: '{{ formset.prefix }}',
    templateId: 'form-template',
    subformSelector: '.subform',
});
```

Since we didn't specify `displayControls` and the button configuration
parameters, this formset will render the controls using an `a` tag with "Add"
as the text for the add button, and "x" for the remove button.
