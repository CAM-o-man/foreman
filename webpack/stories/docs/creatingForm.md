# Creating a Form

Foreman uses [Formik](https://jaredpalmer.com/formik/) which takes care of repetitive code when creating forms.
You can create a form with just Formik, however Foreman provides additional layer of obstraction over the Formik forms to make things more convenient and uniform. This is what a simple form might look like:

```js
// import things we need
import React from 'react';
import * as Yup from 'yup';
// import ForemanForm and TextField specifying the relative path

// define a validation schema using Yup
const validationSchema = Yup.object().shape({
  name: Yup.string().required('is required')
});

const FlavorForm = ({
  url,
  submitForm,
  controller,
  onCancel,
  initialValues,
}) => (
  <ForemanForm
    onSubmit={(values, actions) =>
      submitForm({
        url,
        values,
        message: 'New ice cream flavor successfully created!'
      })
    }
    initialValues={initialValues}
    validationSchema={validationSchema}
    onCancel={onCancel}
  >
    <TextField name="flavor" type="text" required="true" label={'Name'} />
  </ForemanForm>
);
```

`ForemanForm` component requires the following props:

* `onSubmit` - function called on form submission
* `onCancel` - function called on form cancel
* `initialValues` - object with initial values for the fields. For the example above, it could be: `{ name: 'Strawberry Super Sweetness' }`

You can also pass a [Yup](https://github.com/jquense/yup) object as a `validationSchema`, which will take care of validations.
