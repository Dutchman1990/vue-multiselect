<template>
    <div>
        <div class="form-group input-group-alternative mb-2 input-group __parent">
            <div class="div__parent form-control" id="placeholder_div" type="search" @click="showCheckBox()" :style="{top: calculatedTop}" contentEditable=false :placeholder="`${placeholder}`"></div>
            <span class="__selection mt-2">
                <div class="__selected m-1 mt-2 " v-for="option in checkedItems" :key="option.id" v-show="option.checked">
                    {{ option.name }} <span>X</span>
                </div>
            </span>
        </div>

        <div>
            <span class="dropdown-wrapper checkbox" aria-hidden="true">
                <div id="myCustomCheckBox">
                    <input type="text" class="form-control input-group-alternative" :placeholder="`${search_placeholder}`">
                    <ul
                    class="select2-results__options"
                    role="listbox"

                    aria-expanded="true"
                    aria-hidden="false"
                    >

                        <li
                            v-for="option in checkedItems" :key="option.id"
                            class="select2-results__option select2-results__option--group"
                            role="group"
                            name="multichekbox"
                            :data-select2-id="`checkbox_${option.id}`"
                            >
                            <div class="row form-inline checkbox__div" style="width:100%">
                                <input type="checkbox" name="clickedLi" :id="`checkbox_${option.id}`" :data-value="`${option.id}`" @click="getValue(option.id)"
                                :checked="option.checked == true"
                                />
                                <label :for="`checkbox_${option.id}`" style="width:100%">{{ option.name }}</label>
                            </div>
                        </li>
                    </ul>
                </div>
            </span>
        </div>
    </div>
</template>

<script>
var expanded = false;
export default {
  name: "base-multiselectpicker",
  props: {
      options: {
          type: Array,
          default: () => []
      },
      placeholder: {
          type: String,
          default: 'Select option'
      },
      search_placeholder: {
          type: String,
          default: 'Search'
      },
      name: {
          type: String,
          default: "name"
      },
      optionValue: {
          type: String,
          default: "id"
      },
      multiselect: {
          type: Boolean,
          default: false
      }
  },
  data() {
      return {
          checkedItem: []
      }
  },
  computed: {
      checkedItems() {
        let checkedElem = this.options.map(option => {
            const checked = this.$attrs.value.some( r => r === option.id)
            return {...option, checked}
        })
        return checkedElem
      }
  },
  mounted() {

  },
  methods: {
    showCheckBox() {
      var checkboxes = document.getElementById("myCustomCheckBox");
      if (!expanded) {
        checkboxes.style.display = "block";
        expanded = true;
      } else {
        checkboxes.style.display = "none";
        expanded = false;
      }
    },
    getValue(i) {
        var isMultiSelect = this.multiselect
        const parent = document.getElementsByName("clickedLi");
        var checkedItem = []
        if(isMultiSelect == true) {
            for(i = 0; i <= (parent.length - 1); i++){
                if(parent[i].checked == true) {
                    checkedItem.push(parseInt(parent[i].dataset.value))
                }
            }
        } else {
            for(i = 0; i <= (parent.length - 1); i++){
               if(parent[i].checked == true) {
                   parent[i].checked = false
               }
            }
            checkedItem.push(parseInt(event.target.dataset.value))
        }
        if(checkedItem.length > 0) {
            document.getElementById('placeholder_div').setAttribute('placeholder','')
        }else{
            document.getElementById('placeholder_div').setAttribute('placeholder',this.placeholder)
        }
        this.$emit('updateItems:items', checkedItem)
    },
    calculatedTop() {
        console.log('hhh')
    }
  },
};
</script>

<style>
.dropdown {
  position: relative;
}

.dropdown select {
  width: 100%;
  border: none;
  color: #b6bdc4;
}
.overSelect {
  position: absolute;
  left: 0;
  right: 0;
  top: 0;
  bottom: 0;
}

#myCustomCheckBox {
  display: none;
  border: 1px #dadada solid;
  border-radius: 3px;
  -webkit-box-shadow: 0 1px 3px rgba(50, 50, 93, 0.15),
    0 1px 0 rgba(0, 0, 0, 0.02);
  box-shadow: 0 1px 3px rgba(50, 50, 93, 0.15), 0 1px 0 rgba(0, 0, 0, 0.02);
}

#myCustomCheckBox ul{
    overflow: hidden;
    overflow-y: scroll;
    height: 200px;
}


#myCustomCheckBox label {
  display: block;
}
#myCustomCheckBox .checkboxinput {
  padding: 4px;
}

#myCustomCheckBox label:hover {
  background-color: #41b883;
  color: #fff;
}
.checkbox {
  height: 25px;
  position: relative;
}

.checkbox input[type="checkbox"] {
   opacity: 0;
}

.checkbox label {
  position: relative;
  display: inline-block;
  padding-left: 15px;
}

.checkbox label::before,
.checkbox label::after {
  position: absolute;
  content: "";
  display: inline-block;
}

.checkbox label::before {
  height: 16px;
  width: 16px;
  border: 1px solid;
  left: 0px;
  top: 3px;
  opacity: 0;
}

 .checkbox label::after {
  height: 5px;
  width: 9px;
  border-left: 2px solid;
  border-bottom: 2px solid;
  transform: rotate(-45deg);
  left: 4px;
  top: 7px;
}

.checkbox input[type="checkbox"] + label::after {
  content: none;
}

.checkbox input[type="checkbox"]:checked + label::after {
  content: "";
}

.checkbox input[type="checkbox"]:focus + label::before {
  outline: rgb(59, 153, 252) auto 5px;
}
.select2-results__options li{
    height: 25px;
}
.checkbox__div label {
    width: 100%;
    margin-left: 15px;
    display: inline-block;
}

.__selection {
    position: absolute;
}

.__selection div{
    display: inline;
}

.__selected{
    padding-left: 2px;
    padding-right: 2px;
    background: #2dce99;
    color: #fff;
    border-radius: 3px;
}
.__parent{
    overflow: auto;
}
[contenteditable=false]:empty:before{
  content: attr(placeholder);
  pointer-events: none;
  display: block; /* For Firefox */
}
</style>
