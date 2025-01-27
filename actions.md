---

copyright:
  years: 2017, 2019
lastupdated: "2019-08-02"

keywords: actions, functions, serverless, javascript, node, node.js

subcollection: cloud-functions

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:external: target="_blank" .external}
{:codeblock: .codeblock}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:download: .download}
{:gif: data-image-type='gif'}



# Creating actions
{: #actions}

Create an action, which is a top-level function that returns a JSON object. You can combine actions into a package to simplify the management of your actions.
{: shortdesc}

**Before you begin**</br>
To create an action, your source code must meet certain requirements. For example, if you want to create an action from code that is contained in multiple files, package your code as a single .zip file before you create the action. 

See [Preparing apps for actions](/docs/openwhisk?topic=cloud-functions-prep) for details about the requirements for packaging code for each runtime.


## Creating actions from the CLI
{: #actions_cli}

1. Create an action.
  ```
  ibmcloud fn action create <action_name> <file> --kind <runtime>
  ```
  {: pre}

  **Example**
  ```
  ibmcloud fn action create hello hello.js --kind nodejs:10
  ```
  {: pre}

  **Example output**

  ```
  ok: created action hello
  ```
  {: screen}

  Tips:
  - To save on cost, you can set limits.
      - To set a limit for memory usage, include `--memory <value>` with your create command, where the value is in megabytes.
      - To set a timeout, include `--timeout <value>` with your create command, where the value is in milliseconds.
  - If you packaged your code as a Docker image, include `--docker <docker_hub_username>/<docker_hub_image>:<tag>` with your create command instead of the local path to your app and the --kind flag. Manage your images well by not using the `latest` tag whenever possible. When the `latest` tag is used, the image with that tag is used, which might not always be the most recently created image.

      ```
      ibmcloud fn action create hello --docker <docker_hub_username>/<docker_hub_image>:<tag>
      ```
      {: pre}
  
2. Verify that the action is in your actions list.

  ```
  ibmcloud fn action list
  ```
  {: pre}

  **Example output**

  ```
  actions
  hello       private
  ```
  {: screen}

### Combining app files and Docker images to create actions

You can combine your app files with Docker images to create actions. For more information see, [Preparing apps for actions](/docs/openwhisk?topic=cloud-functions-prep).

Run the following command.
```
ibmcloud fn action create hello --docker <docker_hub_username>/<docker_hub_image>:<tag> <app_file>
```
{: pre}



## Updating apps or runtimes in actions
{: #actions_update}

You can run the update command whenever you need to update the code in your app or to migrate to a newer version of a runtime. For example, since Node.js version 8 is in maintenance mode, you might want to switch the runtime to Node.js 10.

When you migrate to a new runtime version, you might need to change the code in your app to comply with the new runtime version. In most cases, the runtime versions are compatible.
{: tip}

1. Update your app locally.

2. If you packaged your app as a Docker image, upload the latest image to Docker Hub. This allows the system to pull your new Docker image the next time it runs the code for your action. If you have a container running that uses a previous version of your Docker image, any new invocations continue to use that image. You must run the update command so that new invocations begin running on the new image.

3. Update an action and include the local path to your app or the Docker image.

    ```
    ibmcloud fn action update <action_name> <app_file> --kind <runtime>
    ```
    {: pre}

    **Example**

    ```
    ibmcloud fn action update hello hello.js --kind nodejs:10
    ```
    {: pre}

    **Example output**

    ```
    ok: updated action hello
    ```
    {: screen}

    If you packaged your code as a Docker image, include `--docker <docker_hub_username>/<docker_hub_image>:<tag>` with your create command instead of the path to the local app and the `--kind` flag. Manage your images well by not using the `latest` tag whenever possible. When the `latest` tag is used, the image with that tag is used, which might not always be the most recently created image. 

      ```
      ibmcloud fn action update hello --docker <docker_hub_username>/<docker_hub_image>:<tag>
      ```
      {: pre}
    {: tip}
      


## Binding parameters to actions
{: #actions_params}

You can bind parameters to actions to set default parameters. Bound parameters serve as the default parameters for actions unless parameters are supplied at invocation.
{: shortdesc}

Before you begin, [create the action](#actions_cli).

To bind the parameters:

1. Update an action and bind the default parameters to it.

    ```
    ibmcloud fn action update <action_name> --param <parameter_name> <parameter_value>
    ```
    {: pre}

    **Example**

    ```
    ibmcloud fn action update MyApp --param name World
    ```
    {: pre}

    **Example output**

    ```
    ok: updated action MyApp
    ```
    {: screen}

    If you modify your non-service credential parameters, running an `action update` command with new parameters removes any parameters that currently exist but are not specified in the `action update` command. For example, if you run `action update -p key1 new-value -p key2 new-value` but omit any other parameters that were set, those parameters no longer exist after the action is updated. Any services that were bound to the action are also removed. If you bound a service, you must [bind the services to your action](/docs/openwhisk?topic=cloud-functions-services) again.
    {: tip}

3. Verify that the parameters were bound to the action.

    ```
    ibmcloud fn action get MyApp parameters
    ```
    {: pre}

    **Example output**

    ```
    ok: got action MyApp, displaying field parameters

    [
        {
            "key": "name",
            "value": "World"
        }
    ]
    ```
    {: screen}

Optional: To clear the parameters that were previously bound, update the action without including any parameters.

```
ibmcloud fn action update <action_name> <app_file>
```
{: pre}


## Chaining actions together as action sequences
{: #actions_seq}

You can create an action that chains together a sequence of actions. The result of one action is passed as an argument to the next action.
{: shortdesc}

```
ibmcloud fn action create <sequence_name> --sequence <action_1>,<action_2>
```
{: pre}

Parameters that are passed between actions in the sequence are explicit, except for default parameters. Therefore, parameters that are passed to the action sequence are only available to the first action in the sequence. The result of the first action in the sequence becomes the input JSON object to the second action in the sequence, and so on. This object does not include any of the parameters that are originally passed to the sequence unless the first action includes them in its result. Input parameters to an action are merged with the action's default parameters, with the former taking precedence and overriding any matching default parameters.

A sequence does not have an overall timeout separate from the timeouts of each action within the sequence. Because a sequence is a pipeline of operations, a failure in one action breaks the pipeline. If one action times out, the entire sequence is exited with that failure.

Next, when you create a rule or invoke the actions, use the name of the sequence.


## Packaging actions
{: #actions_pkgs}

In {{site.data.keyword.openwhisk}}, you can use packages to bundle together a set of related actions and feeds, and share them with others. Packages also allow parameters to be shared across all entities in the package.
{: shortdesc}

A package can include *actions* and *feeds*.
- An action is a piece of code that runs on {{site.data.keyword.openwhisk_short}}. For example, the {{site.data.keyword.cloudant}} package includes actions to read and write records to an {{site.data.keyword.cloudant_short_notm}} database.
- A feed is used to configure an external event source to fire trigger events. For example, the Alarm package includes a feed that can fire a trigger at a specified frequency.


1. Create a package.

  ```
  ibmcloud fn package create <package_name>
  ```
  {: pre}

2. Get a summary of the package. Notice that the package is empty.

  ```
  ibmcloud fn package get --summary <package_name>
  ```
  {: pre}

  **Example output**

  ```
  package /<namespace>/<package_name>
  ```
  {: screen}

4. Create an action and include it in the package. Creating an action in a package requires that you prefix the action name with a package name. Package nesting is not allowed. A package can contain only actions and can't contain another package.

  ```
  ibmcloud fn package create <package_name>/<action_name> <app_file>
  ```
  {: pre}

5. Get a summary of the package.

  ```
  ibmcloud fn package get --summary <package_name>
  ```
  {: pre}

  **Example output**

  ```
  package /<namespace>/<package_name>
   action /<namespace>/<package_name>/<action_name>
  ```
  {: screen}




## Binding parameters to packages
{: #actions_pkgs_params}

You can set default parameters for all the entities in a package by setting package-level parameters that are inherited by all actions in the package.

Bound parameters serve as the default parameters for actions in the package unless:

- The action itself has a default parameter
- The action has a parameter that is supplied at invocation time

Before you begin, create a package that includes at least one action.

1. Update a package and bind the default parameter to it.

    ```
    ibmcloud fn package update <package_name> --param <parameter_name> <parameter_value>
    ```
    {: pre}

    **Example**

    ```
    ibmcloud fn package update MyApp --param name World
    ```
    {: pre}

    **Example output**

    ```
    ok: updated package MyApp
    ```
    {: screen}

    If you modify your non-service credential parameters, running an `package update` command with new parameters removes any parameters that currently exist but are not specified in the `package update` command. For example, if you run `package update -p key1 new-value -p key2 new-value` but omit any other parameters that were set, those parameters no longer exist after the package is updated. Any services that were bound to the package are also removed, so after you update other parameters you must [bind services to your package](/docs/openwhisk?topic=cloud-functions-services) again.
    {: tip}

3. Verify that the parameters were bound to the package.

    ```
    ibmcloud fn package get MyApp parameters
    ```
    {: pre}

    **Example output**

    ```
    ok: got package MyApp, displaying field parameters

    [
        {
            "key": "name",
            "value": "World"
        }
    ]
    ```
    {: screen}

4. Verify that the parameters were inherited by the package.

    ```
    ibmcloud fn package get MyApp/MyAction parameters
    ```
    {: pre}

    **Example output**

    ```
    ok: got package MyApp/MyAction, displaying field parameters

    [
        {
            "key": "name",
            "value": "World"
        }
    ]
    ```
    {: screen}



## Sharing packages of actions
{: #actions_pkgs_share}

After the actions and feeds that comprise a package are debugged and tested, the package can be shared with all {{site.data.keyword.openwhisk_short}} users. Sharing the package makes it possible for the users to bind the package, invoke actions in the package, and author {{site.data.keyword.openwhisk_short}} rules and sequence actions. Actions and feeds within a shared package are _public_. If the package is private, then all of its contents are also private.
{: shortdesc}

1. Share the package with all users.

  ```
  ibmcloud fn package update <package_name> --shared yes
  ```
  {: pre}

2. Display the `publish` property of the package to verify that it is now true.

  ```
  ibmcloud fn package get <package_name> publish
  ```
  {: pre}

  **Example output**

  ```
  ok: got package <package_name>, displaying field publish

  true
  ```
  {: screen}

3. Get a description of the package to provide others with the fully qualified name of the package so that they can bind it or invoke actions in it. The fully qualified name includes the namespace.

  ```
  ibmcloud fn package get --summary <package_name>
  ```
  {: pre}

  **Example output**

  ```
  package /<namespace>/<package_name>
   action /<namespace>/<package_name>/<action_name>
  ```
  {: screen}



## Environment variables for actions
{: #actions_envvars}

The action environment contains several environment variables that are specific to the running action. The properties are accessible in the system environment for all supported runtimes. These properties allow actions to programmatically work with assets through the REST API or set an internal alarm when the action is about to use up its allotted time budget.
{: shortdesc}

| Property | Description |
| -------- | ----------- |
| `__OW_API_HOST` | The API host for the deployment that is running this action. |
| `__OW_API_KEY` | The API key for the subject that is invoking the action. This variable is only provided for classic CF-based namespaces. |
| `__OW_NAMESPACE` | The namespace id (GUID). For classic CF-based namespaces, this ID is constructed from org and space names. |
| `__OW_NAMESPACE_CRN` | The namespace cloud resource name [CRN](/docs/overview?topic=overview-crn). The CRN is only available for IAM-enabled namespaces
| `__OW_ACTION_NAME` | The fully qualified name of the running action. |
| `__OW_IAM_NAMESPACE_API_KEY` | The API key for IAM-enabled namespaces. See [Setting access policies](/docs/openwhisk?topic=cloud-functions-namespaces#namespace-access) for usage. |
| `__OW_IAM_API_URL` | The service endpoint used for IAM operations, such as getting a token from API key. This variable is only available for IAM-enabled namespaces |
| `__OW_ACTIVATION_ID` | The activation ID for this running action instance. |
| `__OW_DEADLINE` | The approximate time, in epoch milliseconds, when this action consumes its entire duration quota. |

### Incorporating action environment variables in your app
{: #actions_envvars_app}

To view the values for an action, include the display of them in your app code and output them in the results.

**Example for Python**
```python
def main(dict):
  import os
  __OW_ACTION_NAME = os.environ.get('__OW_ACTION_NAME')
  result = {'__OW_ACTION_NAME':__OW_ACTION_NAME}
  return result

```
{: codeblock}

After you updated and activated the code in an action, the result includes the fully qualified name for the action.
```bash
"response": {
        "status": "success",
        "statusCode": 0,
        "success": true,
        "result": {
                "__OW_ACTION_NAME": "/<namespace>/<package_name>/<action_name>"
            }

```
{: screen}



