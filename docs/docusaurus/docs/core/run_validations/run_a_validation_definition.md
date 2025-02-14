---
title: Run a Validation Definition
---
import TabItem from '@theme/TabItem';
import Tabs from '@theme/Tabs';

import PrereqPythonInstalled from '../_core_components/prerequisites/_python_installation.md';
import PrereqGxInstalled from '../_core_components/prerequisites/_gx_installation.md';
import PrereqPreconfiguredDataContext from '../_core_components/prerequisites/_preconfigured_data_context.md';
import PrereqValidationDefinition from '../_core_components/prerequisites/_validation_definition.md';


## Prerequisites

- <PrereqPythonInstalled/>.
- <PrereqGxInstalled/>.
- <PrereqPreconfiguredDataContext/>. In this guide the variable `context` is assumed to contain your Data Context.
- <PrereqValidationDefinition/>.

### Procedure

<Tabs 
   queryString="procedure"
   defaultValue="instructions"
   values={[
      {value: 'instructions', label: 'Instructions'},
      {value: 'sample_code', label: 'Sample code'}
   ]}
>

<TabItem value="instructions" label="Instructions">

1. Retrieve your Validation Definition.

   If you have created a new Validation Definition you can use the object returned by your Data Context's `.validation_definitions.add(...)` method.  Alternatively, you can retrieve a previously configured Validation Definition by updating the variable `validation_definition_name` in the following code and executing it:

   ```python title="Python" name="docs/docusaurus/docs/core/run_validations/_examples/run_a_validation_definition.py - retrieve a Validation Definition"
   ```

2. Define a Batch of data to validate

   The [Batch parameters accepted by a Validation Definition](/docs/reference/api/ValidationDefinition_class#great_expectations.ValidationDefinition.run) are determined by the Batch Definition used to instantiate it. 

   ```python title="Python" name="docs/docusaurus/docs/core/run_validations/_examples/run_a_validation_definition.py - define batch parameters"
   ```

3. Execute the Validation Definition's `run()` method:

   ```python title="Python" name="docs/docusaurus/docs/core/run_validations/_examples/run_a_validation_definition.py - run a Validation Definition"
   ```

   Validation Results are automatically saved in your Data Context when a Validation Definition's `run()` method is called.  For convenience, the `run()` method also returns the Validation Results as an object you can review.

   :::tip Result verbosity

   You can set the level of detail returned in a Validation Definition's results by passing a Result Format configuration as the `result_format` parameter of your Validation Definition's `run(...)` method.  For more information on Result Formats, see [Choose a result format](/core/trigger_actions_based_on_results/choose_a_result_format/choose_a_result_format.md).

   :::

4. Review the Validation Results:
 
   ```python title="Python" name="docs/docusaurus/docs/core/run_validations/_examples/run_a_validation_definition.py - review Validation Results"
   ```
   
   When you print the returned Validation Result object you will recieve a json representation of the results.  By default this will include a `"results"` list that includes each Expectation in your Validation Definition's Expectation Suite, whether the Expectation was successfully met or failed to pass, and some sumarized information explaining the why the Expectation succeeded or failed.

</TabItem>

<TabItem value="sample_code" label="Sample code">

```python showLineNumbers title="Python" name="docs/docusaurus/docs/core/run_validations/_examples/run_a_validation_definition.py - full code example"
```

</TabItem>

</Tabs>
