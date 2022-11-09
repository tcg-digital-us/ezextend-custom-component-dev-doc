
Add Entry in Components List Sidebar
====================================

Before creating the custom Button component itself, we need to provide details about our custom element to ezeXtend so that the custom component is displayed as an option in the component sidebar on the left side of the ezeXtend window. Doing this first will allow us to be able to test our Button in the UI and catch any errors in our Button development along the way.

First, open :code:`/EZEXTEND_ROOT/ui/src/AppConstants/WidjetsMapping.js`. Inside of this file is a constant variable WidgetsMapping that contains a JSON object of the Labels to be displayed in the sidebar panel as available elemenents to use in the dashboard. Here we add a definition for our new element :code:`CUSTOM_BUTTON` and the string label that will be shown for it.

.. NOTE::

   For the sake of brevity in the code examples, elipses are used to denote code that we are not concerned with for our example and thus does not need to be displayed in this tutorial.

.. code-block:: javascript
   :linenos:
   :emphasize-lines: 11

   export const WidgetsMapping = {
        SHAPES: {
            ...
        },
        CHARTS: {
            ...
        },
        INPUTS: {
            TEXTBOX: 'Text',
            BUTTON: 'Button',
            CUSTOM_BUTTON: 'Custom Button',
            RADIO: 'Radio',
            SELECT: 'Select',
            MULTI_SELECT: 'Multi Select',
            LABEL: 'Label',
            IMAGE:'Img',
        },
        OTHERS: {
            ...
        },
    };

Next, we need to add the data for the component entry in the sidebar, that is, we need to specify things like the icon to be displayed, etc. To do this, first open :code:`/EZEXTEND_ROOT/ui/src/Components/Sidebar/ComponentsData.js`. This file contains a constant variable :code:`Groups` that contains a JSON object with lists of JSON descriptions of each of the sidebar components belonging to each group in the panel. Because we add our custom button to the :code:`Inputs` section of the :code:`WidgetsMapping` so too do we have to add a new sidebar component to the :code:`Inputs` list within the JSON object:

.. code-block:: javascript
   :linenos:
   :emphasize-lines: 19,20,21,22,23
   
   export const Groups = {
      Shapes: [
         ...
      ],
      Charts: [
         ...
      ],
      Inputs: [
         {
               title: WidgetsMapping.INPUTS.TEXTBOX,
               icon: <BsInputCursor size={size} color={activeColor} />,
               active: true,
         },
         {
               title: WidgetsMapping.INPUTS.BUTTON,
               icon: <GiClick size={size} color={activeColor} />,
               active: true,
         },
         {
               title: WidgetsMapping.INPUTS.CUSTOM_BUTTON,
               icon: <HiCursorClick size={size} color={activeColor} />,
               active: true,
         },
         {
               title: WidgetsMapping.INPUTS.RADIO,
               icon: <IoMdRadioButtonOn size={size} color={activeColor} />,
               active: true,
         },
         {
               title: WidgetsMapping.INPUTS.SELECT,
               icon: <BiSelectMultiple size={size} color={activeColor} />,
               active: true,
         },
         {
               title: WidgetsMapping.INPUTS.LABEL,
               icon: <MdLabel size={size} color={activeColor} />,
               active: true,
         },
         {
               title: WidgetsMapping.INPUTS.IMAGE,
               icon: <FaImages size={size} color={activeColor} />,
               active: true,
         },
      ],
      Others: [
         ...
      ],
   };

Notice that we are referencing the title via the key-value pair that we entered into the WidgetsMapping object. For the icon, we are using one of the available click-related React icons that are freely available to React developers. You can find more of these icons at `react-icons <https://react-icons.github.io/react-icons/search?q=click>`_. We are using the :code:`HiCursorClick` icon for our Button, so we will need to import that icon as a dependency at the top of the file: 

.. code-block:: javascript
   :linenos:
   :emphasize-lines: 9
   
   import {
      ...
   } from 'react-icons/ai';

   ...
   import { GrGraphQl } from "react-icons/gr";
   import { BiSelectMultiple } from 'react-icons/bi';
   import { RiCheckboxMultipleBlankLine } from 'react-icons/ri';
   import { HiCursorClick } from 'react-icons/hi';
   import { WidgetsMapping } from 'AppConstants';
   const size = 20;
   const color = 'rgb(203 203 203)';
   ...

If we run ezeXtend in `Development Mode <../setup.html#development-mode>`_, we can see our component that has yet to be created listed as an option in the component sidebar:

.. figure:: /_static/images/add_entry_1.jpg
   :align: center
