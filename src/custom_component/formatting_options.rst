
Create Component Formatting Options
===================================

The last step for integrating a custom element into the EzeXtend UI is to add formatting options, that is, options that can be provided to the element while it is on the dashboard to customize its appearance or action.

We will begin with a new file :code:`/EZEXTEND_ROOT/ui/src/Components/Widgets/CustomButton/CustomButtonOptions.js`.

In this new file we need to import some important things to help us out. First we need to import the :code:`PropertiesGroup`. This is an element provided by EzeXtend that we can modify and will then be injected into the Properties panel providing our desired functionality. We can create multiple groups if we would like, it just depends on how you are wanting to structure your options. Next we are importing :code:`TextField` from the material UI library, this is the text field we will display in our property group that will update our button. For state-related functionality (such as changing the text displayed on the button) we will need to get two functions from redux, :code:`useSelector` and :code:`useDispatch`. The former allows us to retrieve data from Redux, and the latter allows us register changes we would like to make to the state (and Redux will handle the changes accordingly). :code:`UpdateWidgetProperty` is a Reducer we designed to work with Redux to make this state-changing functionality easier to work with, so we will also import that as well.

.. code-block:: javascript
   :linenos:

   import PropertiesGroup from "CommonComponents/PropertiesGroup";
   import { TextField } from '@mui/material';
   import { useSelector, useDispatch } from 'react-redux';
   import UpdateWidgetProperty from "Store/Reducers/Actions/UpdateWidgetProperty";

Like before, we will define our module, its return statement and that it is the default export of this file:

.. code-block:: javascript
   :linenos:
   
   function CustomButtonOptions() {
      return (
         
      )
   }

   export default CustomButtonOptions;

We need to display the label text of our button saved in :code:`CustomButtonData.js`, so we will need to grab the label from the state data store managed by Redux. First we retrieve the id of the widget by getting the id value stored by EzeXtend as the currently 'active panel'. Then we use that ID to retrieve the option data from Redux. We will also need to create a Redux dispatch object to use later when we want to update the label value.

.. code-block:: javascript
   :linenos:
   :emphasize-lines: 2-4

   function CustomButtonOptions() {
      const id = useSelector((store) => store.dashboard.appState.activePanelID);
      const options = useSelector((store) => store.dashboard.widgets[id]);
      const dispatch = useDispatch();

      return (
         
      )
   }

In the return statement, we define our property group, giving it a title, and inside that group, we create a text field element provided by Material UI. The value displayed on the label is the 'label' value of the options object that we retrieved earlier. The onChange property we are providing a function name :code:`handleChange` that we haven't yet defined.

.. code-block:: javascript
   :linenos:
   :emphasize-lines: 7-9

   function CustomButtonOptions() {
      const id = useSelector((store) => store.dashboard.appState.activePanelID);
      const options = useSelector((store) => store.dashboard.widgets[id]);
      const dispatch = useDispatch();

      return (
         <PropertiesGroup title="Format">
            <TextField label="Label" value={options.label} onChange={handleChange}/>
         </PropertiesGroup>
      )
   }

To wrap it all up, we create our last variable, a function that takes in an event :code:`e`. The function runs Redux's dispatch function which evaluates whatever is returned by :code:`UpdateWidgetProperty()`. We provide :code:`UpdateWidgetProperty` with the id of the widget we are looking to modify, the path of the options value we want to modify (in this case, the path is equal to the 'key's traversed in  :code:`CustomButtonData.data` to get to the value). The value is set to be the value of the text box whose updating triggered the event:

.. code-block:: javascript
   :linenos:
   :emphasize-lines: 6-16

   function CustomButtonOptions() {
      const id = useSelector((store) => store.dashboard.appState.activePanelID);
      const options = useSelector((store) => store.dashboard.widgets[id]);
      const dispatch = useDispatch();

      const handleChange = function(e) {
         dispatch(
               UpdateWidgetProperty({
                  id,
                  update: {
                     path: 'label',
                     value: e.target.value
                  }
               })
         )
      }

      return (
         <PropertiesGroup title="Format">
            <TextField label="Label" value={options.label} onChange={handleChange}/>
         </PropertiesGroup>
      )
   }

Running the development server once more, if we drag the CustomButton element onto the dashboard and open the buton's properties panel by clicking the gear icon, then we will see the Format properties group displayed. Using the new 'Label' text field we can change the name displayed on the button to anything we would like. We can see this change reflected in :numref:`formatting-options`.

.. _formatting-options:
.. figure:: /_static/images/formatting_options_1.jpg
   :align: center

   A custom button and its properties panel. The panel has been used to update the button's label text.
|