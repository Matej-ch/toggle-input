# Deprecated

## component was moved to repository [here](https://github.com/Matej-ch/editable-form-elements)

### Toggle input

## this component is for vue js 3

### for vue js 2 go [here](https://github.com/Matej-ch/toggle-column/tree/v2)

```html
<toggle-input
    label-enable-text='On' 
    label-disable-text='Off' 
    :default-state="0"
    size="sm"
    :form-inputs="{additionFormInput_:1 additionFormInput_2:2}" 
    url="/path/to/update" />
```

`size` two sizes, are currently supported small (sm) and large (lg)

default size is sm

`label-show` show or hide label

`url` url for updating column

`form-inputs` object of additional form data

`label-enable-text` Text when toggle is on

`label-disable-text` Text when toggle is off

`default-state`  default toggle state

![toggle input](toggle.jpg)