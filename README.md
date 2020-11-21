# Introduction
An plug and play vue js multiselect dropdown component. Although the name suggests it is capable to create multiselect dropdown, but it can create single select dropdown also.


# Backstory
While learning via js I realized that I need a multiselect dropdown component to create a multiselect able dropdown, obviously I could have used any npm package available out there, but I was trying to build and learn something new. So I gathered ideas from the open ocean of internet and final output was this. Obviously it's not 100% bug free or fully featured, but a lot to come in future.


# How to use?
Well, it's pretty basic, anybody with basic knowledge of vue can add this in their project. 

- clone the repo in your development environment
- Copy and paste the BaseMultiSelectPicker.vue file inside your project
- Import it inside your parent component 

```import BaseMultiSelectpicker from "../components/ThemeComponents/BaseMultiSelectpicker";``` 

adjust your component path also and use it like below

```<base-multiselectpicker v-bind:options="options" :placeholder="'Select item'" :multiselect="false" :value="selectedOptions" name="name" optionValue="id" @updateItems:items="updateItems"></base-multiselectpicker>```


# Options
| name   | type   | default | description|
| ------ | ------ | ----    | ---|
| options | Array | []      | Options array
| placeholder | String | Select option | Main placeholder
| search_placeholder | String | Search | Search input placeholder
| name | String | -  | Option name to display
| optionValue | String | -  | Option value
| multiselect | Boolean | false  | set to true for multiselect|


# Sample
```
<script>
export default {
    data() {
        return {
            selectedOptions: [],
        }
    },
}
</script>

options = [{"id":1, "name": "foo"},{ "id":2, "name": "bar"}]
```

# Demo
coming soon
