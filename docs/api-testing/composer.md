---
id: composer
title: Writing API Tests with the Composer
sidebar_label: Using the Composer
description: Quickly generate and build functional API tests
---

import useBaseUrl from '@docusaurus/useBaseUrl';

The API Testing Composer enables you to quickly generate API functional tests (no coding experience required) and/or code them from scratch. You can reuse these tests as end-to-end integration tests and load (stress) tests. In turn, load tests can be reused as monitors for performance testing.

## What You'll Need

- A Sauce Labs account ([Log in](https://accounts.saucelabs.com/am/XUI/#login/) or sign up for a [free trial license](https://saucelabs.com/sign-up)).
- An existing API Testing Project. For details on how to create one, see [API Testing Quickstart](/api-testing/quickstart/).

## Creating a Test with the Composer

### Create a Test

1. In Sauce Labs, click **API Testing**.

<img src={useBaseUrl('/img/api-testing/apit-nav-rebrend.png')} alt="Navigating to API Testing" width="200"/>

2. On the **Projects** page:

   - If you have no tests or projects yet, in the **Write your own test** box, click **Use Composer**.

   <img src={useBaseUrl('/img/api-testing/composer-nav.png')} alt="Navigating to the Composer" width="700"/>

   - If you have a project but no tests, on the **Projects** page, click **Write your own test**.

   - If your project has tests, click **Create Test** and then click **From Scratch**.

     <img src={useBaseUrl('/img/api-testing/test-create-from-scratch-nav.png')} alt="Navigating to the New Test window" width="350"/>

3. In the **New Test** box, enter a test name, test description (optional), and tags (optional), and then click **Create Test**.

<img src={useBaseUrl('/img/api-testing/test-create-new-test.png')} alt="New Test window" width="350"/>

:::note
You can use either the **Visual** composer (guides you through building components, with no coding required) or the **Code** composer (requires you to write code from scratch). For this guide, we're using **Visual**.
:::

For more information, see [Input Sets](/api-testing/composer/#input-sets) and [Visual View and Code View](/api-testing/composer/#visual-view-and-code-view).

### Edit a Test

To edit a test at any time, on the **Projects** page, on the **Tests** tab, hover over a test name and then click **Edit Test**.

<img src={useBaseUrl('/img/api-testing/edit-test-nav.png')} alt="Navigating to the test editor" width="300"/>

### Add Test Components

When test components are combined, they act as our test logic. See the following pages for more information about the components types available in API Testing:

- [I/O Request Test Components](/api-testing/composer/io-components)
- [Assertion Test Components](/api-testing/composer/assertion-components/)
- [Logical Test Components](/api-testing/composer/logical-components/)
- [Other Components](/api-testing/composer/other-components/)

#### Add an I/O Request Test Component

To create a simple `GET` request and validate that response is correct:

1. In API Testing, on the **Compose** page, click **Add child component**.

<img src={useBaseUrl('/img/api-testing/add-component-nav.png')} alt="Navigating to the Add component screen"/>

2. In the list of component options, click the **GET** component.

<img src={useBaseUrl('/img/api-testing/get-request-nav.png')} alt="Navigating to the GET request window"/>

3. In the **GET request** window, in the **Url** field, enter `https://api.us-west-1.saucelabs.com/rest/v1/public/tunnels/info/versions`.

This endpoint will return a JSON response body. 4. In the **Variable** field, enter **payload**. This variable stores the response, so it can now be referred to as **payload**.

<img src={useBaseUrl('/img/api-testing/get-request-window.png')} alt="Editing in the GET request window"/>

5. Leave the rest of the fields blank and then click **Save Changes**.

The result should look like the following:

<img src={useBaseUrl('/img/api-testing/get-request-final.png')} alt="What the GET request should look like" width="600"/>

For more information, see [I/O Request Test Components](/api-testing/composer/io-components/).

#### Add an Assertion Component

1. In API Testing, on the **Compose** page, click **Add child component**.

<img src={useBaseUrl('/img/api-testing/add-component-nav.png')} alt="Navigating to the Add component screen" width="600"/>

2. In the list of component options, click the **Assert Exists** component.

<img src={useBaseUrl('/img/api-testing/assert-exists-nav.png')} alt="Navigating to the Assert exists window"/>

3. In the **Assert exists** window, in the **Expression** field, enter `payload.downloads`. This expression checks for the **downloads** field in the json response body.

4. Leave the rest of the fields blank and click **Save Changes**.

<img src={useBaseUrl('/img/api-testing/assert-exists-window.png')} alt="Confirm changes" width="600"/>

5. The result should look like the following:

<img src={useBaseUrl('/img/api-testing/assert-exists-final.png')} alt="What the Assert request should look like" />

For more information, see [Assertion Test Components](/api-testing/composer/assertion-components/).

#### Additional Example

In the following example, the expression checks if the `download_url` value inside the Linux object is a valid URL.

1. In API Testing, on the **Compose** page, click **Add child component**.

2. In the list of component options, click the **Assert Is** component.

3. In the **Assert is** window, in the **Expression** field, enter `payload.downloads.linux.download_url`. This expression checks for the **download_url** field in the json response payload.

4. Leave the rest of the fields blank and click **Save Changes**.

<img src={useBaseUrl('/img/api-testing/assert-exists-window-2.png')} alt="Confirm changes" width="600"/>

5. The result should look like the following:

<img src={useBaseUrl('/img/api-testing/assert-exists-final-2.png')} alt="What the Assert request should look like" width="500"/>

### Run the Test

In the Composer, click **Run**.

<img src={useBaseUrl('/img/api-testing/run-test-save-run.png')} alt="Save and Run icons in the Composer" width="500"/>

All test runs appear to the right of the Composer, under the test details and environment sections.

<img src={useBaseUrl('/img/api-testing/test-runs.png')} alt="Test Runs in the Composer" width="350"/>

### Review Test Results

To view your results, in the Composer, in the **Test Runs** list, click the name of the test. This will open the **Test Report Details**. For more information, see [Test Outcome Report](/api-testing/project-dashboard/#test-outcome-report).

## Integration Tests

Integration testing is critical for creating a strong API testing strategy. An integration test allows you to create end-to-end tests that resemble common user flows. While only testing individual endpoints is a good start, this method will miss a large number of problems that occur when all services need to work together.

### Token-based Authentication API

Company A has an authentication server. This server, when given the proper user credentials, returns an authentication token. This token is required for all other calls throughout the platform’s API environment. Without this first API call, none of the other API calls can work.

1. To get the token, make a `POST` call to the authorization server.

<img src={useBaseUrl('/img/api-testing/int-getting-token.png')} alt="POST request to authentication server" width="600"/>

The request body is the user ID and password. Given proper credentials, the authentication server will return a user token.

<img src={useBaseUrl('/img/api-testing/int-token.png')} alt="The user token" width="400"/>

Use this token to make further calls to the application.

2. Add a `Set (variable)` component by entering/selecting the following in the Composer:

   - Variable (the variable name) - `access_token`
   - Mode (the variable type) - `String`
   - Value - `${authPayload.access_token}`

   <img src={useBaseUrl('/img/api-testing/int-assign-token.png')} alt="Setting the variable"/>

This step takes the `access_token` variable in the `authPayload` response, and sets it as `access_token`; the response body from the original post call was saved to a variable called `authPayload`. The access key for the token is `access_token`, which can be found by calling `authPayload.access_token`.

:::note
The dollar sign and brackets are necessary when referencing variables so that Sauce Labs API Testing knows to interpret what’s between the brackets instead of using it literally.
:::

Variables are used to store data temporarily for a test, but you can use the Sauce Labs API Testing Vault for permanent variables. For more information, see [Creating Reusable Variables and Snippets with the Vault](/api-testing/vault)).

3. Make follow-up calls.

In the following example, the API has a cart function that requires a user token to add items to a cart or view items currently in the cart. Use a `PUT` request to the cart endpoint to update the cart. Use the access token granted by the authentication server to add items to a cart by setting the `token` header to `${access_token}`.

<img src={useBaseUrl('/img/api-testing/int-set-token-header.png')} alt="Setting the token header"/>

You can also reuse access tokens:

<img src={useBaseUrl('/img/api-testing/int-reuse-tokens.png')} alt="Reusing tokens" width="600"/>

### Test Interactions between Endpoints

In the following example, there is an API endpoint that produces an array of all the available products and another endpoint that shows the details of a specific product based on its ID.

```http request
http://demoapi.apifortress.com/api/retail/product
http://demoapi.apifortress.com/api/retail/product/${id}
```

To create an integration test to test the interaction between the endpoints:

1. Call the product listing endpoint and assign the response to the `productsPayload` variable.

2. Add an `each` assertion and reference the `productsPayload.products` object.

:::note
In a scenario in which the response contains many products, it may be useful to pick a few at random by using `pick(n)`.
:::

3. Test the response payload for the endpoint.

4. Add a new `Set (variable)` assertion to set the `id` variable as every single `productsPayload.product` that is returned. In the following example, the string is `${_1.id}`. The system uses `_1` automatically when recognizing a subroutine, which makes it easier when there are multiple sub-levels.

   <img src={useBaseUrl('/img/api-testing/int-test-endpoints.png')} alt="Testing interactions between endpoints" width="600"/>

5. Create a **`GET` request** to the product details endpoint, using the new `id` variable as the **id** parameter. Variables last through the entire test unless overwritten.

6. Test the response payload for the endpoint.

   <img src={useBaseUrl('/img/api-testing/int-test-response-payload.png')} alt="Testing the response payload"/>

```yaml
- id: get
  children:
    - id: header
      name: key
      value: ABC123
  url: http://demoapi.apifortress.com/api/retail/product
  var: productsPayload
  mode: json
- id: if
  children:
    - id: comment
      text: endpoint is not working fine, test will be stopped
    - id: flow
      command: stop
  expression: productsPayload_response.statusCode!='200'
- id: assert-is
  expression: productsPayload
  comment: payload must be an array
  type: array
- id: each
  children:
    - id: comment
      text: "product id is: ${_1.id} and product name is: ${_1.name}"
    - id: assert-is
      expression: _1.id
      comment: id must be an integer value
      type: integer
    - id: set
      var: id
      mode: string
      value: ${_1.id}
    - id: assert-exists
      expression: _1.name
      comment: name must exists
    - id: assert-is
      expression: _1.price
      comment: price must be a float number
      type: float
    - id: assert-exists
      expression: _1.category
      comment: category must exists
    - id: assert-exists
      expression: _1.description
      comment: description must exists
    - id: assert-is
      expression: _1.quantity
      comment: quantity must be an integer value
      type: integer
    - id: assert-greater
      expression: _1.quantity
      comment: quantity must be greater than 0
      value: 0
    - id: assert-is
      expression: _1.imageURL
      comment: imageURL must be a valid url value
      type: url
    - id: assert-is
      expression: _1.color
      comment: color must be an array
      type: array
    - id: each
      children:
        - id: assert-exists
          expression: _2
          comment: color array should contain some values
        - id: assert-in
          expression: _2
          comment: colors must be the expected one
          value:
            - yellow
            - blue
            - red
            - green
            - brown
            - orange
            - gray
            - pink
            - black
            - white
      expression: _1.color
    - id: assert-exists
      expression: _1.createdAt
      comment: createdAt must exists
    - id: assert-exists
      expression: _1.updatedAt
      comment: updateAt must exists
    - id: comment
      text: get product details
    - id: get
      children:
        - id: header
          name: key
          value: ABC123
      url: http://demoapi.apifortress.com/api/retail/product/${id}
      var: productPayload
      mode: json
    - id: if
      children:
        - id: comment
          text: endpoint is not working fine, test will be stopped
        - id: flow
          command: stop
      expression: productPayload_response.statusCode!='200'
    - id: assert-exists
      expression: productPayload
      comment: payload must exist, if not, test does not need to be executed
    - id: comment
      text: "product id is: ${productPayload.id} and product name is:
        ${productPayload.name}"
    - id: assert-is
      expression: productPayload.id
      comment: id must be an integer value
      type: integer
    - id: assert-exists
      expression: productPayload.name
      comment: name must exists
    - id: assert-is
      expression: productPayload.price
      comment: price must be a float number
      type: float
    - id: assert-exists
      expression: productPayload.category
      comment: category must exists
    - id: assert-exists
      expression: productPayload.description
      comment: description must exists
    - id: assert-is
      expression: productPayload.quantity
      comment: quantity must be an integer value
      type: integer
    - id: assert-greater
      expression: productPayload.quantity
      comment: quantity must be greater than 0
      value: 0
    - id: assert-is
      expression: productPayload.imageURL
      comment: imageURL must be a valid url value
      type: url
    - id: assert-is
      expression: productPayload.color
      comment: color must be an array
      type: array
    - id: each
      children:
        - id: assert-exists
          expression: _2
          comment: color array should contain some values
        - id: assert-in
          expression: _2
          comment: colors must be the expected one
          value:
            - yellow
            - blue
            - red
            - green
            - brown
            - orange
            - gray
            - pink
            - black
            - white
      expression: productPayload.color
    - id: assert-exists
      expression: productPayload.createdAt
      comment: createdAt must exists
    - id: assert-exists
      expression: productPayload.updatedAt
      comment: updateAt must exists
  expression: productsPayload.pick(5)
```

## Terminology

### Visual View and Code View

This toggle switches between the Visual and Code views in the Composer. You can make calls and add assertions for testing your APIs, and insert variables wherever needed. You can use either, depending on which you're more comfortable with.

#### Visual View

Guides you through creating API tests using automated real-time suggestions via predictive text. No coding experience is required.<br/><img src={useBaseUrl('img/api-testing/visualView.png')} alt="Test Composer Visual view"/>

#### Code View

Enables you to write tests here from scratch, if you feel more comfortable working in code.<br/><img src={useBaseUrl('img/api-testing/codeView.png')} alt="Test Composer Code view"/>

### Add Child Component

This button displays all available [assertion components](/api-testing/composer/assertion-components/), [I/O components](/api-testing/composer/io-components/), and [logical components](/api-testing/composer/logical-components/).<br/>
<img src={useBaseUrl('img/api-testing/add-component-nav.png')} alt="Add Component"/>

If a component is not valid for the operation you are conducting, it will not be made available to help avoid mistakes. For instance, if you don’t add a `POST` first, you cannot add a `POST` Body or `POST` Param.

:::note
Sauce Labs free trials may not give you access to all available components.
:::

### Component Options

Click **Edit** to modify an existing component, or use the dropdown menu next to **Edit** to perform the actions shown below.

<img src={useBaseUrl('img/api-testing/deleteComponent.png')} alt="Component Options"/>

### Save

Saves your progress.<br/>
<img src={useBaseUrl('img/api-testing/saveTest.png')} alt="Save"/>

### Publish

Publishes your test.<br/>
<img src={useBaseUrl('img/api-testing/publishtest.png')} alt="Publish"/>

### Clear

Clears the most recent unpublished changes made to your test.<br/>
<img src={useBaseUrl('img/api-testing/cleartest.png')} alt="Clear"/>

### Run

Executes a test.<br/>
<img src={useBaseUrl('img/api-testing/runTest.png')} alt="Run"/>

### Input Sets

Displays the Input Set view where you can store input data sets to reuse within the specific test you're working on.<br/>
<img src={useBaseUrl('img/api-testing/inputSets.png')} alt="Input Sets" width="500"/>

There are two types of input data sets you can use:

- Global Parameters - Variables that are available within a test, valid for that specific test only.
- Input Set - Group of input variables representing a scenario, valid for that specific test only. The test will be executed once for each input set, overriding the variable values into your test.

<table>
<tr>
<td><strong>Input Set with Visual View</strong></td>
<td> <img src={useBaseUrl('img/api-testing/inputVisual.png')} alt="Input Set Visual View"/> </td>
</tr>
<tr>
<td><strong>Input Set with Code View</strong></td>
<td><img src={useBaseUrl('img/api-testing/inputCode.png')} alt="Input Set Code View"/> </td>
</tr>
</table>

### Unit View

These buttons switch between the Input Set and Unit views.<br/>
<img src={useBaseUrl('img/api-testing/unitView.png')} alt="Unit View"/>

## Test Options

Once you've generated your tests in the Composer, you can manage them from the **Tests** tab. In your project, on the **Tests** tab, hover your mouse over the test line item. You'll see icons that allow you to edit, run, schedule, or delete a test.<br/>
<img src={useBaseUrl('img/api-testing/test-options.png')} alt="Test Options Icons"/>

- Pencil icon: Edit the test (opens the **Compose** tab)
- Play icon: Run the test manually
- Calendar icon: Open the [test scheduler](/api-testing/schedule-test)
- Gauge icon: Opens the load testing page
- Trash icon: Delete the test

## More Information

- [API Testing Quickstart](/api-testing/quickstart)
- Check our [Use Cases](/api-testing/use-cases/working-with-headers) out to see practical examples to help you write your tests.
