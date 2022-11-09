
Create a Custom React Component
===============================

Now, we can actually start creating our custom buton! To do so, we will first create a folder for our React module code called :code:`CustomButton` in :code:`/EZEXTEND_ROOT/ui/src/Components/Widgets/`.

Create two files in this new folder, :code:`CustomButton.js` and :code:`CustomButonOptions.js`.

First we will work in :code:`CustomButton.js`. EzeXtend uses Redux to manage complicated state in the application, so we will need to import the state selector from Redux:

.. NOTE:: 

   If this is your first time hearing about "state" in regards to React, Redux, or both, then you should take a moment to look into both of these softwares and the concept of state and how they handle them in greater depth, as this is an integral part of working with React and can be confusing if you are out of the loop.

.. code-block:: javascript
   :linenos:
   
   import { useSelector } from 'react-redux';
   import { Button } from '@mui/material';

We are taking the easy route with this button, and rather than recreating a button from scratch, we are instead using a pre-made React button provided in the Material library and we are wrapping it with our custom specifications. We need to define the functional component and provide it as an exportable default:

.. code-block:: javascript
   :linenos:
   :emphasize-lines: 4,5,6,8
   
   ...
   import { Button } from '@mui/material';
   
   function CustomButton({ id }) {

   }

   export default CustomButton;

Next, we will make our custom button return the pre-made button provided by the Material library. We will also provide some properties to the JSX element so that we can customize the button slightly:

.. code-block::
   :linenos:
   :emphasize-lines: 2,3,4,5,6
   
   function CustomButton({ id }) {
      return (
         <Button sx={{height: '100%', width: '100%'}} variant='outlined'>

         </Button>
      )
   }

Here we are passing two props, :code:`sx` and :code:`variant`. The former allows us to define a JSON object containing a subset of CSS parameters that will be used to override the default CSS styling that comes with Material UI buttons. The latter is a property defined by Material, the button type or variant. In this case we are using the 'outlined' button variant.

We want the label for our button to be displayed within the button itself, so to do this we will need to get the label from our :code:`CustomButtonData` from earlier. The crux here is that we will not be importing the button data directly, instead EzeXtend will load that custom data at runtime and make it available throughout the application via Redux. Because of this, we will have to load the data in from Redux and apply it to our label within the CustomButton module like so:

.. NOTE::

   The array :code:`evaluatedWidgetProperties` at index :code:`id` contains the JSON object value corresponding to the :code:`data` key in the :code:`CustomButtonData` object we defined.

.. code-block:: 
   :linenos:
   :emphasize-lines: 3,4,5,9
   
   function CustomButton({ id }) {

      const props = useSelector(
         (store) => store.dashboard.evaluation.evaluatedWidgetProperties[id]
      );

      return (
         <Button sx={{height: '100%', width: '100%'}} variant='outlined'>
            { props.label }
         </Button>
      )
   }

Were we are providing :code:`useSelector()` an anonymous function as an argument, knowing that that anonymous function will be provided the store that contains our state data. 