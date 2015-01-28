#Styled Dropdown

Uses `ul` tag to create a styleable dropdown
as a replacement to a standard html select

##Usage

Require the javascipt *after JQuery*

1. Add an html5 data attribute `data-dropdown` to the parent element with the selector for the input
2. Inside the parent include an unordered list where each `li` item has `data-value` and the value that will be assigned to the hidden input
3. Include an element with the class `dropdown-result` which will trigger the dropdown options and display the result

HTML:

       <div class="container" data-dropdown=".input-value">
         <input type="hidden" name="actualResult" value="Default Value" class="input-value">
         <div class="dropdown-result">Default Value</div>
         <ul class="dropdown-options">
           <li data-value="value-for-1">Option 1</li>
           <li data-value="value-for-2">Option 2</li>
           <li data-value="value-for-3">Option 3</li>
         </ul>
       </div>

       <!-- Just include the script after jQuery and it'll run -->
      <script type="text/javascript" src='{{ assetsRoot }}js/styled-dropdown.js'></script>


When the `dropdown-result` div is clicked a class `dropdown-active` is added to the container

SCSS:

        .container {
            position: relative;
            width: 250px;
            // list is by default
            // hidden and only appears
            // when the 'dropdown-result' element is clicked
            // when
            ul {
                display: none;
                // ensure that it's position absolute
                position: absolute;
                right: 10px;
                margin-top: -6px;
                z-index: 10;
            }
            &.dropdown-active {
                ul {
                    display: block;
                }
            }
        }


##Asynchronously Loaded Dropdowns

The styled dropdown script exports the function `$.styledDropdowns` to the jQuery object

Any dynamically loaded modules can be instantiated with `$('.my-new-dropdown').styledDropdowns()`
