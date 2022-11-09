
Create Default Parameters for Component
=======================================

To create the default parameters for our custom button we need to create a new file in :code:`/EZEXTEND_ROOT/ui/src/Components/Widgets/Defaults` named :code:`CustomButton.js`.

In this file, we need to create a single exported variable, a JSON object that contains information describing the default state of the component when it is initially dragged onto the dashboard:

.. code-block:: javascript
   :linenos:

   export const CustomButtonData = {
      size: {
         width: 200,
         height: 40
      },

      data: {
         label: 'Action'
      }
   }

Here we have defined the initial size of the element and the string text to be displayed on the button when it is first created. Now, we can navigate to the file :code:`/EZEXTEND_ROOT/ui/src/Components/Widgets/Defaults/index.js` to import and apply the default data we have just created. First we will import the JSON object we just created:

.. code-block:: javascript
   :linenos:
   :emphasize-lines: 4

   ...
   import { ChartData } from './Chart';
   import { ButtonData } from './Button';
   import { CustomButtonData } from './CustomButton';
   import { MarkdownData } from './Markdown';
   ...

Currently as you can see, all of the custom data is spread across multiple files. This index file will serve as a one-stop-shop to access all of these default data objects. To achieve this, all of the defaults that are imported are promptly exported from :code:`index.js` so that they can be called elsewhere by importing this index file. We will include our imported custom button data as an available export:

.. ATTENTION::

   More info needs to be added here as why this is necessary given that this list of exports is not used elsewhere in the code.

.. code-block:: javascript
   :linenos:
   :emphasize-lines: 4

   export {
     ChartData,
     ButtonData,
     CustomButtonData,
     MarkdwonData,
     ...
   };

Lastly, we need to add some logic to the default function :code:`WidgetDefaultsProvider(type)` so that when it is called with the argument :code:`WidgetsMapping.INPUTS.CUSTOM_BUTTON` it returns the appropriate data:

.. code-block:: javascript
   :linenos:
   :emphasize-lines: 7,8

   export default function WidgetDefaultsProvider(type) {
      switch (type) {
         case WidgetsMapping.CHARTS.COMBO:
            return ChartData;
         case WidgetsMapping.INPUTS.BUTTON:
            return ButtonData;
         case WidgetsMapping.INPUTS.CUSTOM_BUTTON:
            return CustomButtonData;
         case WidgetsMapping.INPUTS.RADIO:
            return RadioData;
         ...
      }
   }