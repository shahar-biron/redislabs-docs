---
Title: Using the API
description: How to use the API with various tools (especially with `cURL`)
weight: 40
alwaysopen: false
categories: ["RC Pro"]
---
You can access and use the API with:

- The Swagger user interface
- An API client
- The cURL HTTP client

## Swagger User Interface

The [Swagger UI](https://api-beta1.redislabs.com/beta1/swagger-ui.html) is useful for initial introduction
and for learning about API operations, models and simulated usage.

### Authenticating to Swagger

To authenticate to the Swagger UI:

1. Open the [Swagger UI](https://api-beta1.redislabs.com/beta1/swagger-ui.html) page in a browser.

    ![swagger-authorize-and-try-now](/images/rv/api/swagger-authorize-and-try-now.png)

1. Click on the `Authorize` button.

    The **Available Authorizations** box is shown with the headers and values that are used for authentication in all API interactions with Swagger.

    ![swagger-authorizations](/images/rv/api/swagger-authorizations.png)

1. Insert the API Key values:

    1. Enter the [Account Key]({{< relref "/rv/api/how-to/enable-your-account-to-use-api.md" >}}) as the `x-api-key` value and click **Authorize**.
    1. Enter the [Secret Key]({{< relref "/rv/api/how-to/create-api-keys-for-your-team.md" >}}) as the `x-api-secret-key` value and click **Authorize**.
    1. Click **Close**.

{{% note %}}
The key values are not saved when you refresh the page.
{{% /note %}}

When authorization is successful the lock icon appears as a closed lock.

![swagger-closed-lock](/images/rv/api/swagger-closed-lock.png)

### Calling API operations

After you complete the authorization in the Swagger UI, execute an API operation:

1. Open an action category and select an API operation.

    For example, in the `Account` category select the `GET /payment-methods` operation.

    ![swagger-payment-methods-try-it-now](/images/rv/api/swagger-payment-methods-try-it-now.png)

1. Click **Try it out** and **Execute**.

    The API response is shown in the **Responses** section of the API operation.
    The results include an example of how you to execute the same operation in a standard command-line utility using `cURL`.

    ![swagger-query-results](/images/rv/api/swagger-query-results.png)

#### Inputs for operations in Swagger

Some API operations require input, such as:

- **Parameters** - When an API operation requires URI parameters, such as "get subscription by subscription id,
you can enter the values for the parameters.

    ![swagger-parameters](/images/rv/api/swagger-parameters.png)

- **JSON Request Body** - For API operations that require a JSON request body, you can either:

    - Use the **model display** to write the request based on the expected JSON structure and parameters.

        ![swagger-post-body-model](/images/rv/api/swagger-post-body-model.png)

    - Use the **Try it now** sample JSON created by Swagger as a base template that you can edit and execute.

        ![swagger-post-edit-body](/images/rv/api/swagger-post-edit-body.png)

## Creating an API client

Using [Swagger Codegen](https://swagger.io/tools/swagger-codegen/),
you can generate an API HTTP client in a variety of programming languages,
or roll-your-own client by wrapping the API REST calls in a programming language of your choice.

## Using the `cURL` HTTP client

`cURL` is a popular command line tool used to perform HTTP requests,
either as individual commands or within shell scripts (mostly Linux Bash).
For an introduction to `cURL`, see [How to start using cURL and why: a hands-on introduction](https://medium.freecodecamp.org/how-to-start-using-cURL-and-why-a-hands-on-introduction-ea1c913caaaa).

{{% info %}}
We use `cURL` and Linux shell scripts to provide examples on using the API.
{{% /info %}}

For example, a standard API call to get System Log information looks like this in `cURL`:

```bash
curl -s -X GET "https://$HOST/logs" \
    -H "accept: application/json" \
    -H "x-api-key: $ACCOUNT_KEY" \
    -H "x-api-secret-key: $SECRET_KEY" \
    | jq -r .
```

- The example expects several variables to be set in the Linux shell:

    - **$HOST** - The URI of the Redis Labs API (`api-beta1.redislabs.com/beta1`)
    - **$ACCOUNT_KEY** - The [Account key value]({{< relref "/rv/api/how-to/enable-your-account-to-use-api.md" >}})
    - **$SECRET_KEY** - The personal [secret key value]({{< relref "/rv/api/how-to/create-api-keys-for-your-team.md" >}})

- The line "`| jq -r .`" means that the HTTP response will be piped (forwarded) to the `jq` JSON command line processor, and it will display only the raw output ("`-r`") of the root element ("`.`")
- You can set the variables using shell commands like the following:

    ```shell
    {{% embed-code "rv/api/05-set-variables.sh" %}}
    ```