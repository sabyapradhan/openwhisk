---

copyright:
  years: 2017, 2019
lastupdated: "2019-07-19"

keywords: managing actions, manage, activation, action logs, changing runtime, delete

subcollection: cloud-functions-cli-plugin

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




# {{site.data.keyword.openwhisk_short}} CLI
{: #functions-cli}

Run these commands to manage the entities that make up your functions.
{: shortdec}

<br />

## Action commands
{: #cli_action}



### `ibmcloud fn action create`
{: #cli_action_create}

Create an action.

```
ibmcloud fn action create ACTION_NAME APP_FILE [--annotation ANNOTATION_KEY ANNOTATION_VALUE] [--annotation-file FILE] [--copy] [--docker DOCKER_HUB_USERNAME/IMAGE_NAME] [--kind LANGUAGE] [--logsize LIMIT] [--main ENTRY_METHOD_NAME] [--native] [--param KEY VALUE] [--param-file FILE] [--sequence ACTION_NAME, ACTION_NAME] [--timeout LIMIT] [--web yes|true|raw|no|false] [--web-secure SECRET]
```
{: pre}

<br />**Command options**

   <dl>
   <dt>`--annotation` `ANNOTATION_KEY` `ANNOTATION_VALUE`, `-a` `ANNOTATION_KEY` `ANNOTATION_VALUE`</dt>
   <dd>Annotations are specified in a `KEY` `VALUE` format. To include more than one annotation, specify this option for each annotation. This flag is optional.</dd>

   <dt>`--annotation-file` `FILE`, `-A` `FILE`</dt>
   <dd>A JSON file that contains annotation in a `KEY` `VALUE` format. This flag is optional.</dd>

   <dt>`ACTION_NAME`</dt>
   <dd>The name of the action. To include the action in a package, enter the name in the format `PACKAGE_NAME`/`ACTION_NAME`. This value is required. </dd>

   <dt>`APP_FILE`</dt>
   <dd>The path to the app file or package to run as an action. This option is required.</dd>
   
   <dt>`--copy`</dt>
   <dd>Treat the action as the name of an existing action.</dd>

   <dt>`--docker` `DOCKER_HUB_USERNAME`/`IMAGE_NAME`</dt>
   <dd>The Docker Hub user name and the name of the Docker image in Docker Hub to run the action. This flag is required for creating actions from Docker images.</dd>

   <dt>`--kind` `LANGUAGE`</dt>
   <dd>The runtime for your app. This flag is optional. If no `VALUE` is specified, the default version for the detected runtime is used.
     Possible `VALUES` for the `--kind` option.
     <table>
  <tr>
    <th>Language</th>
    <th>Kind identifier</th>
  </tr>
  <tr>
    <td>Node.js</td>
    <td> <code>nodejs:10</code> (default), <code>nodejs:8</code></td>
  </tr>
  <tr>
    <td>Python</td>
    <td><code>python:3.7</code>, <code>python:3.6</code>, <code>python:2</code> (default)</td>
  </tr>
  <tr>
    <td>Swift</td>
    <td><code>swift:4.2</code> (default)</td>
  </tr>
  <tr>
    <td>PHP</td>
    <td><code>php:7.3</code> (default)</td>
  </tr>
  <tr>
    <td>Go</td>
    <td><code>go:1.11</code> (default)</td>
  </tr>
  <tr>
    <td>Ruby</td>
    <td><code>ruby:2.5</code> (default)</td>
  </tr>
  <tr>
    <td>Java</td>
    <td><code>java (JDK 8)</code> (default)</td>
  </tr>
  <tr>
    <td>.NET Core</td>
    <td><code>dotnet:2.2</code> (default)</td>
  </tr>
  <tr>
    <td>Other languages are supported by using Docker actions.</td>
  </tr>
</table>
{: caption="Table 1. Supported runtimes" caption-side="top"}
       </dd>

   <dt>`--logsize` `LIMIT`, `-l` `LIMIT`</dt>
   <dd>The maximum log size in MB for the action. The default value is 10 MB.</dd>

   <dt>`--main` `ENTRY_METHOD_NAME`</dt>
   <dd>If the action's entry method is not `main`, specify the custom name. This flag is required when the entry method is not `main`. For some runtimes, such as Java, the name must be the fully qualified method.</dd>

   <dt>`--native`</dt>
   <dd>You can use the `--native` argument as shorthand for `--docker openwhisk/dockerskeleton`. By using this argument, you can create and deploy an executable that runs inside the standard Docker action SDK.
       <ol><li>When you create a Docker image, an executable is created inside the container at `/action/exec`. Copy the `/action/exec` file to your local file system and compress it into `exec.zip`.</li>
       <li>Create a Docker action that receives the executable as initialization data. The `--native` argument replaces the `--docker openwhisk/dockerskeleton` argument.</li></ol>

   <dt>`--param` `KEY` `VALUE`, `-p` `KEY` `VALUE`</dt>
   <dd>Parameter `VALUES` in the `KEY` `VALUE` format. This flag is optional.</dd>

   <dt>`--param-file` `FILE`, `-P` `FILE`</dt>
   <dd>A JSON file that contains parameter `KEYS` and `VALUES`. This flag is optional.</dd>

   <dt>`--sequence` `ACTION_NAME`, `ACTION_NAME`</dt>
   <dd>Create an action sequence and include the names of the related actions. Separate the `ACTION_NAMEs` by commas.</dd>

   <dt>`--timeout` `LIMIT`, `-t` `LIMIT`</dt>
   <dd>The timeout `LIMIT` in milliseconds. The default value is 60000 milliseconds. When the timeout is reached, the action is terminated.</dd>

   <dt>`--web yes|true|raw|no|false`</dt>
   <dd>Treat the action as a web action, a raw HTTP web action, or as a standard action. Specify `yes` or `true` for a web action, `raw` for a raw HTTP web action, or `no` or `false` for a standard action. To secure your web action, also include the `--web-secure` option.</dd>

   <dt>`--web-secure` `SECRET`</dt>
   <dd>Secure the web action. The `VALUE` for `SECRET` can be `true`, `false`, or any string. This option can be used only with the `--web` option.</dd>
   </dl>

<br />**Example**

  ```
  ibmcloud fn action create hello folder/hello_world.js
  ```
  {: pre}

  **Output**
  ```
  ok: created hello
  ```
  {: screen}


<br />

### `ibmcloud fn action delete`
{: #cli_action_delete}

You can clean up your namespace by deleting actions that you do not want to use any longer.

```
ibmcloud fn action delete ACTION_NAME
```
{: pre}

<br />**Example**

  ```
  ibmcloud fn action delete helloworld
  ```
  {: pre}

  **Output**
  ```
  ok: deleted hello
  ```
  {: screen}


<br />

### `ibmcloud fn action get`
{: #cli_action_get}

Get metadata that describes a specific action.

```
ibmcloud fn action get ACTION_NAME [--save] [--save-as FILENAME] [--summary] [--url]
```
{: pre}

<br />**Command options**

   <dl>
   <dt>`ACTION_NAME`</dt>
   <dd>The name of an action. This value is required.</dd>

   <dt>`--save`</dt>
   <dd>You can get and locally save the code that is associated with an existing action, except for sequences and Docker actions. The `FILENAME` corresponds with an existing action name in the current working directory and the file extension  corresponds to the action kind. For example, for action code that is an archive file, an extension of .zip is used. This flag is optional.</dd>

  <dt>`--save-as` `FILENAME`</dt>
  <dd>Save the code for actions in a custom-named file by providing a file path, `FILENAME`, and extension. This flag is optional.</dd>

  <dt>`--summary`</dt>
  <dd>Get a summary of the action details. Parameters with the prefix "*" are bound; parameters with the prefix "**" are bound and finalized. This flag is optional.</dd>

  <dt>`--url`</dt>
  <dd>Get the URL only for the action. This flag is optional.</dd>
   </dl>

<br />**Example**

```
ibmcloud fn action get hello
```
{: pre}

**Output**
```
ok: got action hello
{
    "namespace": "user@email.com",
    "name": "hello",
    "version": "0.0.1",
    "exec": {
        "kind": "nodejs:6",
        "binary": false
    },
    "annotations": [
        {
            "KEY": "exec",
            "VALUE": "nodejs:6"
        }
    ],
    "LIMIT s": {
        "timeout": 60000,
        "memory": 256,
        "logs": 10
    },
    "publish": false
}
```
{: screen}




<br />

### `ibmcloud fn action invoke`
{: #cli_action_invoke}

Run an action to test it.

```
ibmcloud fn action invoke ACTION_NAME [--blocking] [--param KEY VALUE] [--param-file FILE] [--result]
```
{: pre}

<br />**Command options**

   <dl>
   <dt>`ACTION_NAME`</dt>
   <dd>The name of the action. This value is required. </dd>

   <dt>`--blocking, -b`</dt>
   <dd>Blocking invocations use a request and response style to wait for the activation result to be available. The wait period is the lesser of 60 seconds or the action's [time `LIMIT` `VALUE`](/docs/openwhisk?topic=cloud-functions-limits). This flag is optional.</dd>

   <dt>`--param` `KEY` `VALUE`, `-p` `KEY` `VALUE`</dt>
   <dd>Parameter `VALUES` in the `KEY` `VALUE` format. This flag is optional.</dd>

   <dt>`--param-file` `FILE`, `-P` `FILE`</dt>
   <dd>A JSON file that contains parameter `KEYS` and `VALUES`. This flag is optional.</dd>

   <dt>`--result, -r`</dt>
   <dd>The result of the app code is displayed as the output of the command. If this option is not specified, the activation ID is displayed. The invocation is blocking when this option is specified. This flag is optional.</dd>

   </dl>

<br />**Example**
```
ibmcloud fn action invoke hello --blocking
```
{: pre}


<br />

### `ibmcloud fn action list`
{: #cli_action_list}

List all of the actions that you created or a specific number of actions.

```
ibmcloud fn action list ACTION_NAME [--limit NUMBER_OF_ACTIONS] [--name-sort] [--skip NUMBER_OF_ACTIONS]
```
{: pre}

<br />**Command options**

   <dl>
   <dt>`ACTION_NAME`</dt>
   <dd>The name of a package of actions. This value is optional. If not specified, all actions are listed.</dd>

   <dt>`--limit` `NUMBER_OF_ACTIONS`, -l `NUMBER_OF_ACTIONS`</dt>
   <dd>List a specified number of actions. The default is 30 actions.</dd>

   <dt>`--name-sort, -n`</dt>
   <dd>Sort the list of returned actions by name, otherwise the list is sorted by creation date.</dd>

   <dt>`--skip` `NUMBER_OF_ACTIONS`, -s `NUMBER_OF_ACTIONS`</dt>
   <dd>Exclude a specified number of the most recently created actions from the result.</dd>

   </dl>

<br />**Example**

  ```
  ibmcloud fn action list
  ```
  {: pre}


<br />

### `ibmcloud fn action update`
{: #cli_action_update}

Update an action or the app within an action.

When you update parameters for a package, action, or trigger you must specify all previously created parameters. Otherwise, the previously created parameters are removed. For packages, any services that were bound to the package are also removed, so after you update other parameters you must [bind services](/docs/openwhisk?topic=cloud-functions-services) to your package again.
{: important}

```
ibmcloud fn action update ACTION_NAME APP_FILE [--annotation ANNOTATION_KEY ANNOTATION_VALUE] [--annotation-file FILE] [--copy] [--docker DOCKER_HUB_USERNAME/IMAGE_NAME] [--kind LANGUAGE] [--logsize LIMIT] [--main ENTRY_METHOD_NAME] [--native] [--param KEY VALUE] [--param-file FILE] [--sequence ACTION_NAME, ACTION_NAME] [--timeout LIMIT] [--web yes|true|raw|no|false] [--web-secure SECRET]
```
{: pre}

<br />**Command options**

  <dl>
  <dt>`--annotation` `ANNOTATION_KEY` `ANNOTATION_VALUE`, `-a` `ANNOTATION_KEY` `ANNOTATION_VALUE`</dt>
  <dd>Annotations are specified in a `KEY` `VALUE` format. To include more than one annotation, specify this option for each annotation. This flag is optional.</dd>

  <dt>`--annotation-file` `FILE`, `-A` `FILE`</dt>
  <dd>A JSON file that contains annotation in a `KEY` `VALUE` format. This flag is optional.</dd>

  <dt>`ACTION_NAME`</dt>
  <dd>The name of the action. To include the action in a package, enter the name in the format `PACKAGE_NAME`/`ACTION_NAME`. This value is required. </dd>

  <dt>`APP_FILE`</dt>
  <dd>The path to the app file or package to run as an action. This option is required when you want to update your app within the action.</dd>

  <dt>`--copy`</dt>
  <dd>Treat the action as the name of an existing action.</dd>

  <dt>`--docker DOCKER_HUB_USERNAME/IMAGE_NAME`</dt>
  <dd>The Docker Hub user name and the name of the Docker image in Docker Hub to run the action. This flag is required for creating actions from Docker images.</dd>

  <dt>`--kind LANGUAGE`</dt>
  <dd>The runtime for your app. This flag is optional. If no VALUE is specified, the default version for the detected runtime is used.
    Possible values for the `--kind` option.
    <table>
  <tr>
    <th>Language</th>
    <th>Kind identifier</th>
  </tr>
  <tr>
    <td>Node.js</td>
    <td> <code>nodejs:10</code> (default), <code>nodejs:8</code></td>
  </tr>
  <tr>
    <td>Python</td>
    <td><code>python:3.7</code>, <code>python:3.6</code>, <code>python:2</code> (default)</td>
  </tr>
  <tr>
    <td>Swift</td>
    <td><code>swift:4.2</code> (default)</td>
  </tr>
  <tr>
    <td>PHP</td>
    <td><code>php:7.3</code> (default)</td>
  </tr>
  <tr>
    <td>Go</td>
    <td><code>go:1.11</code> (default)</td>
  </tr>
  <tr>
    <td>Ruby</td>
    <td><code>ruby:2.5</code> (default)</td>
  </tr>
  <tr>
    <td>Java</td>
    <td><code>java (JDK 8)</code> (default)</td>
  </tr>
  <tr>
    <td>.NET Core</td>
    <td><code>dotnet:2.2</code> (default)</td>
  </tr>
  <tr>
    <td>Other languages are supported by using Docker actions.</td>
  </tr>
</table>
{: caption="Table 1. Supported runtimes" caption-side="top"}
      </dd>

  <dt>`--logsize` `LIMIT`, `-l` `LIMIT`</dt>
  <dd>The maximum log size in MB for the action. The default value is 10 MB.</dd>

  <dt>`--main ENTRY_METHOD_NAME`</dt>
  <dd>If the action's entry method is not `main`, specify the custom name. This flag is required when the entry method is not `main`. For some runtimes, such as Java, the name must be the fully qualified method.</dd>

  <dt>`--native`</dt>
  <dd>You can use the `--native` argument as shorthand for `--docker openwhisk/dockerskeleton`. By using th argument, you can create and deploy an executable that runs inside the standard Docker action SDK.
      <ol><li>When you create a Docker image, an executable is created inside the container at `/action/exec`. Copy the `/action/exec` file to your local file system and compress it into `exec.zip`.</li>
      <li>Create a Docker action that receives the executable as initialization data. The `--native` argument replaces the `--docker openwhisk/dockerskeleton` argument.</li></ol>

  <dt>`--param` `KEY` `VALUE`, `-p` `KEY` `VALUE`</dt>
  <dd>Parameter `VALUES` in the `KEY` `VALUE` format. This flag is optional.</dd>

  <dt>`--param-file` `FILE`, `-P` `FILE`</dt>
  <dd>A JSON file that contains parameters `KEYS` and `VALUES`. This flag is optional.</dd>

  <dt>`--sequence` `ACTION_NAME`, `ACTION_NAME`</dt>
  <dd>Create an action sequence by specifying the name of related actions.</dd>

  <dt>`--timeout` `LIMIT`, `-t` `LIMIT`</dt>
  <dd>The timeout limit in milliseconds. The default value is 60000 milliseconds. When the timeout is reached, the action is terminated.</dd>

  <dt>`--web yes|true|raw|no|false`</dt>
  <dd>Treat the action as a web action, a raw HTTP web action, or as a standard action. Specify `yes` or `true` for a web action, `raw` for a raw HTTP web action, or `no` or `false` for a standard action. To secure your web action, also include the `--web-secure` option.</dd>

  <dt>`--web-secure` `SECRET`</dt>
  <dd>Secure the web action. The `VALUE` for `SECRET` can be `true`, `false`, or any string. This option can be used only with the `--web` option.</dd>
  </dl>

<br />**Example**
```
ibmcloud fn action update hello folder/hello_world.js
```
{: pre}




<br /><br />
## Activation commands
{: #cli_activation}


### `ibmcloud fn activation get`
{: #cli_activation_get}

Get metadata that describes a specific activation.

```
ibmcloud fn activation get [ACTIVATION_ID] [FIELD_FILTER] [--last] [--summary]
```
{: pre}


<br />**Command options**

  <dl>
  <dt>`ACTIVATION_ID`</dt>
  <dd>The ID for a specific activation. Use `ibmcloud fn activation list` to retrieve a list of available IDs. This value is required, unless the `--last` or `-l` option is specified..</dd>

  <dt>`FIELD_FILTER`</dt>
  <dd>A field in the metadata to display information from. For example, to display the logs field, run `ibmcloud fn activation get ACTIVATION_ID logs`. This value is optional.</dd>

  <dt>`--last, -l`</dt>
  <dd>Display the metadata for the most recent activation. This flag is optional.</dd>

  <dt>`--summary, -s`</dt>
  <dd>Display the result response only from the activation details. This flag is optional.</dd>
  </dl>


<br />**Example**
```
ibmcloud fn activation get 8694a4501be6486a94a4501be6886a1e --summary
```
{: pre}


<br />

### `ibmcloud fn activation list`
{: #cli_activation_list}

List all of the activation IDs for all of the actions in a package.

```
ibmcloud fn activation list [--full] [--limit NUMBER_OF_ACTIVATIONS] [--since UNIX_EPOCH_TIME] [--skip NUMBER_OF_ACTIVATIONS] [--upto UNIX_EPOCH_TIME]
```
{: pre}


<br />**Command options**

  <dl>
  <dt>`--full, -f`</dt>
  <dd>Display the full activation description.</dd>

  <dt>`--limit` `NUMBER_OF_ACTIVATIONS`, `-l` `NUMBER_OF_ACTIVATIONS`</dt>
  <dd>List a specified number of activations. The default is 30 activations and the maximum is 200 activations.</dd>

  <dt>`--since` `UNIX_EPOCH_TIME`</dt>
  <dd>List activations that were created since the date specified. Duration is measured in milliseconds since 01 January 1970. Example: `1560371263` is 12 June 2019 08:27:43 UTC.</dd>

  <dt>`--skip` `NUMBER_OF_ACTIVATIONS`, -s `NUMBER_OF_ACTIVATIONS`</dt>
  <dd>Exclude a specified number of the most recent activations from the result.</dd>

  <dt>`--upto` `UNIX_EPOCH_TIME`</dt>
  <dd>List activations that were created before the date specified. Duration is measured in milliseconds since 01 January 1970. Example: `1560371263` is 12 June 2019 08:27:43 UTC.</dd>
  </dl>

<br />**Example**
```
ibmcloud fn activation list
```
{: pre}

**Output**
```
activations
44794bd6aab74415b4e42a308d880e5b         hello
6bf1f670ee614a7eb5af3c9fde813043         hello
```
{: screen}


<br />

### `ibmcloud fn activation logs`
{: #cli_activation_logs}

Get logs for a specific activation.

```
ibmcloud fn activation logs [ACTIVATION_ID] [--last] [--strip]
```
{: pre}

<br />**Command options**

  <dl>
  <dt>`ACTIVATION_ID`</dt>
  <dd>The ID for a specific activation. Use `ibmcloud fn activation list` to retrieve a list of available IDs. This value is required, unless the `--last` or `-l` option is specified.</dd>

  <dt>`--last, -l`</dt>
  <dd>Display the logs for the most recent activation. This flag is optional.</dd>

  <dt>`--strip, -r`</dt>
  <dd>Display the log message only; exclude the timestamp and stream information. This flag is optional.</dd>
  </dl>

<br />**Example**
```
ibmcloud fn activation logs 8694a4501be6486a94a4501be6886a1e --summary
```
{: pre}


<br />

### `ibmcloud fn activation poll`
{: #cli_activation_poll}

View a streaming, live list of activations for an action or a namespace. You can press `CTRL+C` to exit the polling.

```
ibmcloud fn activation poll [NAMESPACE] [ACTION_NAME] [--exit SECONDS] [--since-days DAYS] [-since-hours HOURS] [--since-minutes MINUTES] [--since-seconds SECONDS]
```
{: pre}

<br />**Command options**

  <dl>
  <dt>/`NAMESPACE`</dt>
  <dd>A namespace, beginning with /. Poll activations for a namespace, an action, or a space. This value is optional. If a namespace or action is not specified, the space is polled.</dd>

  <dt>`ACTION_NAME`</dt>
  <dd>Poll activations for a namespace, an action, or a space. This value is optional. If a namespace or action is not specified, the space is polled.</dd>

  <dt>`--exit` `SECONDS`, `-e` `SECONDS`</dt>
  <dd>Poll activations for a specified number of seconds and then exit. This flag is optional.</dd>

  <dt>`--since-days` `DAYS`</dt>
  <dd>Start polling for activations a specified number of days ago. This flag is optional.</dd>

  <dt>`--since-hours` `HOURS`</dt>
  <dd>Start polling for activations a specified number of hours ago. This flag is optional.</dd>

  <dt>`--since-minutes` `MINUTES`</dt>
  <dd>Start polling for activations a specified number of minutes ago. This flag is optional.</dd>

  <dt>`--since-seconds` `SECONDS`</dt>
  <dd>Start polling for activations a specified number of seconds ago. This flag is optional.</dd>
  </dl>

<br />**Example**
```
ibmcloud fn activation poll
```
{: pre}


<br />

### `ibmcloud fn activation result`
{: #cli_activation_result}

Get the result from a specific activation.

```
ibmcloud fn activation result [ACTIVATION_ID] [--last] [--strip]
```
{: pre}


<br />**Command options**

  <dl>
  <dt>`ACTIVATION_ID`</dt>
  <dd>The ID for a specific activation. Use `ibmcloud fn activation list` to retrieve a list of available IDs. This value is required, unless the `--last` or `-l` option is specified.</dd>

  <dt>`--last, -l`</dt>
  <dd>Display the result for the most recent activation. This flag is optional.</dd>

  </dl>

<br />**Example**
```
ibmcloud fn activation result 8694a4501be6486a94a4501be6886a1e
```
{: pre}



<br /><br />

## API commands
{: #cli_api}


### `ibmcloud fn api create`
{: #cli_api_create}

Create an API.

```
ibmcloud fn api create BASE_PATH API_PATH API_VERB ACTION_NAME] [--apiname API_NAME] [--config-file FILE] [--response-type TYPE]
```
{: pre}

<br />**Command options**

   <dl>

   <dt>`BASE_PATH`</dt>
   <dd>The base path for the API.</dd>

   <dt>`API_NAME`</dt>
   <dd>The name of the API. The API name might be the same as the base path.</dd>

   <dt>`API_VERB`</dt>
   <dd>The verb for the API, such as `get` or `post`.</dd>

   <dt>`ACTION_NAME`</dt>
   <dd>The name of the action.</dd>

   <dt>`--apiname API_NAME`, `-n API_NAME`</dt>
   <dd>The name of the API. This flag is ignored when a configuration file is specified. The default name is the `BASE_PATH`. This flag is optional.</dd>

   <dt>`--config-file` `FILE`, `-c` `FILE`</dt>
   <dd>A JSON file that contains the Swagger API configuration. When this flag is used, the API name flag is ignored. This flag is required.</dd>

   <dt>`--response-type TYPE`</dt>
   <dd>Set the web action response type as `html`, `http`, `json`, `text`, or `svg`. The default value is `json`. This flag is optional.</dd>

   </dl>

<br />**Example**

  ```
  ibmcloud fn api create /hello /world get hello --response-type json
  ```
  {: pre}

  **Output**
  ```
  ok: created API /hello/world GET for action /_/hello
  https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/<GENERATED_API_ID>/hello/world

  ```
  {: screen}


<br />

### `ibmcloud fn api delete`
{: #cli_api_delete}

Delete an API.

```
ibmcloud fn api delete BASE_PATH API_NAME API_PATH API_VERB
```
{: pre}

<br />**Command options**

   <dl>

   <dt>`BASE_PATH`</dt>
   <dd>The base path for the API.</dd>

   <dt>`API_NAME`</dt>
   <dd>The name of the API. The API name might be the same as the base path.</dd>

   <dt>`API_PATH`</dt>
   <dd>The path to the API.</dd>

   <dt>`API_VERB`</dt>
   <dd>The verb for the API, such as `GET` or `POST`.</dd>

   <dt>`--format OUTPUT_TYPE`</dt>
   <dd>Specify the API output type as `json` or `yaml`. The default value is `json`.</dd>

   <dt>`--full, -f`</dt>
   <dd>Display the full API configuration details.</dd>

   </dl>

<br />**Example**

  ```
  ibmcloud fn api delete /hello /world get
  ```
  {: pre}



<br />

### `ibmcloud fn api get`
{: #cli_api_get}

Get the metadata for an API.

```
ibmcloud fn api get BASE_PATH API_NAME [--format OUTPUT_TYPE] [--full]
```
{: pre}

<br />**Command options**

   <dl>

   <dt>`BASE_PATH`</dt>
   <dd>The base path for the API.</dd>

   <dt>`API_NAME`</dt>
   <dd>The name of the API. The API name might be the same as the base path.</dd>

   <dt>`--format OUTPUT_TYPE`</dt>
   <dd>Specify the API output type as `json` or `yaml`. The default value is `json`.</dd>

   <dt>`--full, -f`</dt>
   <dd>Display the full API configuration details.</dd>

   </dl>

<br />**Example**

  ```
  ibmcloud fn api get /hello /world
  ```
  {: pre}


<br />

### `ibmcloud fn api list`
{: #cli_api_list}

List all of the APIs that you created or a specific number of APIs. If no name or base path is specified, all of the APIs are listed.

```
ibmcloud fn api list BASE_PATH API_NAME API_PATH API_VERB [--full] [--limit NUMBER_OF_APIS] [--name-sort] [--skip NUMBER_OF_APIS]
```
{: pre}

<br />**Command options**

   <dl>

   <dt>`BASE_PATH`</dt>
   <dd>The base path for the API.</dd>

   <dt>`API_NAME`</dt>
   <dd>The name of the API. The API name might be the same as the base path.</dd>

   <dt>`API_PATH`</dt>
   <dd>The path to the API.</dd>

   <dt>`API_VERB`</dt>
   <dd>The verb for the API, such as `GET` or `POST`.</dd>

   <dt>`--full, -f`</dt>
   <dd>Display the full API details. This flag is optional. </dd>

   <dt>`--limit NUMBER_OF_APIS`, `-l NUMBER_OF_APIS`</dt>
   <dd>List a specified number of APIs. The default is 30 APIs. This flag is optional. </dd>

   <dt>`--name-sort, -n`</dt>
   <dd>Sort the list of returned APIs by name, otherwise the list is sorted by creation date. This flag is optional. </dd>

   <dt>`--skip NUMBER_OF_APIS`, `-s NUMBER_OF_APIS`</dt>
   <dd>Exclude a specified number of the most recently created APIs from the result. This flag is optional. </dd>

   </dl>

<br />**Example**

  ```
  ibmcloud fn api list
  ```
  {: pre}


<br /><br />
## Deployment commands
{: #cli_deploy_cmds}


### `ibmcloud fn deploy`
{: #cli_deploy}

Use a manifest file to deploy a collection of packages, actions, triggers, and rules.

```
ibmcloud fn deploy [--apihost HOST] [--auth KEY] [--config FILE] [--deployment FILE] [--manifest FILE] [--namespace NAMESPACE] [--param KEY VALUE] [--param-file FILE] [--preview] [--project PATH] [--strict] [--verbose]
```
{: pre}

<br />**Command options**

   <dl>

   <dt>`--apihost HOST`</dt>
   <dd>The `wsk` API host. This flag is optional.</dd>

   <dt>`--auth` `KEY`, `-u` `KEY`</dt>
   <dd>The `wsk` authorization `KEY`. This flag is optional.</dd>

   <dt>`--config` `FILE`</dt>
   <dd>The configuration file. The default is `$HOME/.wskprops`.</dd>

   <dt>`--deployment` `FILE`</dt>
   <dd>The path to the deployment file.</dd>

   <dt>`--manifest` `FILE`, `-m` `FILE`</dt>
   <dd>The path to the manifest file. This flag is required if the manifest.yaml is not in the current directory.</dd>

   <dt>`--namespace` `NAMESPACE`, `-n` `NAMESPACE`</dt>
   <dd>The name or ID for a namespace.</dd>

   <dt>`--param` `KEY` `VALUE`, `-p` `KEY` `VALUE`</dt>
   <dd>Parameter `VALUES` in the `KEY` `VALUE` format. This flag is optional.</dd>

   <dt>`--param-file` `FILE`, `-P` `FILE`</dt>
   <dd>A JSON file that contains parameter `KEYS` and `VALUES`. This flag is optional.</dd>

   <dt>`--preview` </dt>
   <dd>Display the deployment plan before you deploy.</dd>

   <dt>`--project PATH`</dt>
   <dd>The path to the serverless project. The default is <code>.</code> (current directory).</dd>

   <dt>`--strict`</dt>
   <dd>Allow a user-defined runtime version.</dd>

   <dt>`--verbose, -v`</dt>
   <dd>View verbose output.</dd>

   </dl>

<br />**Example**

  ```
  ibmcloud fn deploy --manifest folder/manifest.yaml
  ```
  {: pre}


<br />

### `ibmcloud fn undeploy`
{: #cli_undeploy}

Use a manifest file to undeploy a collection of packages, actions, triggers, and rules.

```
ibmcloud fn undeploy [--apihost HOST] [--auth KEY] [--config FILE] [--deployment FILE] [--manifest FILE] [--namespace NAMESPACE] [--param KEY VALUE] [--param-file FILE] [--preview] [--project PATH] [--strict] [--verbose]
```
{: pre}

<br />**Command options**

   <dl>
   <dt>`--apihost HOST`</dt>
   <dd>The `wsk` API host. This flag is optional.</dd>

   <dt>`--auth` `KEY`, `-u` `KEY`</dt>
   <dd>The `wsk` authorization `KEY`. This flag is optional.</dd>

   <dt>`--config` `FILE`</dt>
   <dd>The configuration file. The default is `$HOME/.wskprops`.</dd>

   <dt>`--deployment` `FILE`</dt>
   <dd>The path to the deployment file.</dd>

   <dt>`--manifest` `FILE`, -m `FILE`</dt>
   <dd>The path to the manifest file. This flag is required if the manifest.yaml is not in the current directory.</dd>

   <dt>`--namespace` `NAMESPACE`, `-n` `NAMESPACE`</dt>
   <dd>The name or ID for a namespace.</dd>

   <dt>`--param` `KEY` `VALUE`, `-p` `KEY` `VALUE`</dt>
   <dd>Parameter `VALUES` in the `KEY` `VALUE` format. This flag is optional.</dd>

   <dt>`--param-file` `FILE`, `-P` `FILE`</dt>
   <dd>A JSON file that contains parameter `KEYS` and `VALUES`. This flag is optional.</dd>

   <dt>`--preview` </dt>
   <dd>Display the result of the command without running the command.</dd>

   <dt>`--project PATH`</dt>
   <dd>The path to the serverless project. The default is `.` (current directory).</dd>

   <dt>`--strict`</dt>
   <dd>Allow a user-defined runtime version.</dd>

   <dt>`--verbose, -v`</dt>
   <dd>View verbose output.</dd>

   </dl>

<br />**Example**

  ```
  ibmcloud fn undeploy --manifest folder/manifest.yaml
  ```
  {: pre}



<br /><br />

## List command
{: #cli_list_cmd}


### `ibmcloud fn list`
{: #cli_list}

View a grouped list of the packages, actions, triggers, and rules in the namespace.

```
ibmcloud fn list [--name-sort]
```
{: pre}

<br />**Command options**

   <dl>
   <dt>`--name-sort, -n`</dt>
   <dd>Sort each group of returned entities by name, otherwise each group is sorted by creation date.</dd>
   </dl>

<br />**Example**

  ```
  ibmcloud fn list
  ```
  {: pre}




<br /><br />
## Namespace commands
{: #cli_namespace}


### `ibmcloud fn namespace create`
{: #cli_namespace_create}

Create an IAM namespace.

```
ibmcloud fn namespace create NAMESPACE [--description DESCRIPTION] 
```
{: pre}

<br />**Command options**

   <dl>

   <dt>`NAMESPACE`</dt>
   <dd>The name for a namespace. Do not include hyphens (-) in the name. This value is required.</dd>

   <dt>`--description DESCRIPTION`, `-n DESCRIPTION`</dt>
   <dd>Write your own unique description to help you identify the namespace. If your description is more than one word, include quotation marks (") around your description. This flag is optional.</dd>

   </dl>

<br />**Example**

  ```
  ibmcloud fn namespace create HBCTeamProd --description "HBC Team Prod Environment. See Beth for information about this namespace."
  ```
  {: pre}


<br />

### `ibmcloud fn namespace delete`
{: #cli_namespace_delete}

Delete an IAM namespace.

```
ibmcloud fn namespace delete NAMESPACE
```
{: pre}


<br />**Example**

  ```
  ibmcloud fn namespace delete mynamespace
  ```
  {: pre}



<br />

### `ibmcloud fn namespace get`
{: #cli_namespace_get}

Get the entities for or the metadata information from a Cloud Foundry or IAM namespace.

```
ibmcloud fn namespace list NAMESPACE [--auth KEY] [--name-sort] [--properties] 
```
{: pre}

<br />**Command options**

   <dl>

   <dt>`NAMESPACE`</dt>
   <dd>The name or ID for a namespace. This value is required.</dd>

   <dt>`--auth` `KEY`, `-u` `KEY`</dt>
   <dd>The `wsk` authorization `KEY`. This flag is optional.</dd>

   <dt>`--name-sort, -n`</dt>
   <dd>Sort the list of returned namespaces by name, otherwise the list is sorted by creation date. This flag is optional. </dd>

   <dt>`--properties`</dt>
   <dd>Display the namespace properties instead of the entities contained within it. This flag is optional. </dd>

   </dl>

<br />**Example**

  ```
  ibmcloud fn namespace get user@domain.com_dev --properties
  ```
  {: pre}

  **Output**
  ```
  Name: user@domain.com_dev
  Description: This is a description of my namespace.
  Resource Plan Id: functions-base-plan
  Location: us-south
  ID: 58c2e718-8c60-48bc-96de-cf9373fe6709
  ```
  {: screen}



<br />

### `ibmcloud fn namespace list`
{: #cli_namespace_list}

List the available Cloud Foundry and IAM namespaces.

```
ibmcloud fn namespace list [--auth KEY] [--cf] [--iam] [--limit NUMBER_OF_NAMESPACES] [--name-sort] [--skip NUMBER_OF_NAMESPACES] 
```
{: pre}

<br />**Command options**

   <dl>

   <dt>`--auth` `KEY`, `-u` `KEY`</dt>
   <dd>The `wsk` authorization `KEY`. This flag is optional.</dd>

   <dt>`--cf`</dt>
   <dd>Display the Cloud Foundry namespaces only. IAM namespaces are not displayed. This flag is optional.</dd>

   <dt>`--iam`</dt>
   <dd>Display the IAM namespaces only. Cloud Foundry namespaces are not displayed. This flag is optional.</dd>

   <dt>`--limit NUMBER_OF_``NAMESPACE``S`, `-l NUMBER_OF_``NAMESPACE``S`</dt>
   <dd>List a specified number of namespaces. The default is 30 namespaces. This flag is optional. </dd>

   <dt>`--name-sort, -n`</dt>
   <dd>Sort the list of returned namespaces by name, otherwise the list is sorted by creation date. This flag is optional. </dd>

   <dt>`--skip NUMBER_OF_NAMESPACES`, `-s NUMBER_OF_``NAMESPACE``S`</dt>
   <dd>Exclude a specified number of the most recently created namespaces from the result. This flag is optional. </dd>

   </dl>

<br />**Example**

  ```
  ibmcloud fn namespace list
  ```
  {: pre}


<br />

### `ibmcloud fn namespace update`
{: #cli_namespace_update}

Change the name or description of an IAM namespace.

```
ibmcloud fn namespace update NAMESPACE [NEW_NAMESPACE_NAME] [--description DESCRIPTION] 
```
{: pre}

<br />**Command options**

   <dl>

   <dt>`NAMESPACE`</dt>
   <dd>The name for a namespace. Do not include hyphens (-) in the name. This value is required.</dd>

   <dt>`NEW_``NAMESPACE``_NAME`</dt>
   <dd>The new name for a namespace. Do not include hyphens (-) in the name. This value is optional.</dd>

   <dt>`--description DESCRIPTION`, `-n DESCRIPTION`</dt>
   <dd>Write your own unique description to help you identify the namespace. If your description is more than one word, include quotation marks (") around your description. This flag is optional.</dd>

   </dl>

<br />**Example**

  ```
  ibmcloud fn namespace update HBCTeamProd HBCTeamStaging
  ```
  {: pre}




<br /><br />
## Package commands
{: #cli_pkg}


### `ibmcloud fn package bind`
{: #cli_pkg_bind}

Bind parameters to a package. All of the actions within the package inherit those parameters unless otherwise specified.

```
ibmcloud fn package bind PACKAGE_NAME [--annotation ANNOTATION_KEY ANNOTATION_VALUE] [--annotation-file FILE] [--param KEY VALUE] [--param-file FILE]
```
{: pre}

<br />**Command options**

  <dl>
  <dt>`PACKAGE_NAME`</dt>
  <dd>The name of the package. This value is required. </dd>

  <dt>`--annotation` `ANNOTATION_KEY` `ANNOTATION_VALUE`, `-a` `ANNOTATION_KEY` `ANNOTATION_VALUE`</dt>
  <dd>Annotations are specified in a `KEY` `VALUE` format. To include more than one annotation, specify this option for each annotation. This flag is optional.</dd>

  <dt>`--annotation-file` `FILE`, `-A` `FILE`</dt>
  <dd>A JSON file that contains annotation in a `KEY` `VALUE` format. This flag is optional.</dd>

  <dt>`--param` `KEY` `VALUE`, `-p` `KEY` `VALUE`</dt>
  <dd>Parameter `VALUES` in the `KEY` `VALUE` format. This flag is optional.</dd>

  <dt>`--param-file` `FILE`, `-P` `FILE`</dt>
  <dd>A JSON file that contains parameter `KEYS` and `VALUES`. This flag is optional.</dd>
  </dl>

<br />**Example**

  ```
  ibmcloud fn package bind --param name Bob
  ```
  {: pre}



<br />

### `ibmcloud fn package create`
{: #cli_pkg_create}

Create a package designed to contain one or more actions. To add an action in the package, include the package name with the action name when you create or update the action.

```
ibmcloud fn package create PACKAGE_NAME [--annotation ANNOTATION_KEY ANNOTATION_VALUE] [--annotation-file FILE] [--param KEY VALUE] [--param-file FILE]
```
{: pre}

<br />**Command options**

  <dl>
  <dt>`PACKAGE_NAME`</dt>
  <dd>The name of the package. This value is required. </dd>

  <dt>`--annotation` `ANNOTATION_KEY` `ANNOTATION_VALUE`, `-a` `ANNOTATION_KEY` `ANNOTATION_VALUE`</dt>
  <dd>Annotations are specified in a `KEY` `VALUE` format. To include more than one annotation, specify this option for each annotation. This flag is optional.</dd>

  <dt>`--annotation-file` `FILE`, `-A` `FILE`</dt>
  <dd>A JSON file that contains annotation in a `KEY` `VALUE` format. This flag is optional.</dd>

  <dt>`--param` `KEY` `VALUE`, `-p` `KEY` `VALUE`</dt>
  <dd>Parameter `VALUES` in the `KEY` `VALUE` format. This flag is optional.</dd>

  <dt>`--param-file` `FILE`, `-P` `FILE`</dt>
  <dd>A JSON file that contains parameter `KEYS` `VALUE` format. This flag is optional.</dd>

  <dt>`--shared yes|no`</dt>
  <dd>When specified without a value or with a value of yes, the package is shared with other users.</dd>
  </dl>

<br />**Example**

  ```
  ibmcloud fn package create hellopkg
  ```
  {: pre}

  **Output**
  ```
  ok: created hellopkg
  ```
  {: screen}


<br />

### `ibmcloud fn package delete`
{: #cli_pkg_delete}

You can clean up your namespace by deleting packages that you do not want to use any longer.

```
ibmcloud fn package delete PACKAGE_NAME
```
{: pre}

<br />**Example**

  ```
  ibmcloud fn package delete hello
  ```
  {: pre}

  **Output**
  ```
  ok: deleted hello
  ```
  {: screen}


<br />

### `ibmcloud fn package get`
{: #cli_pkg_get}

Get metadata that describes a specific package.

```
ibmcloud fn package get PACKAGE_NAME [--summary]
```
{: pre}

<br />**Command options**

  <dl>
   <dt>`PACKAGE_NAME`</dt>
   <dd>The name of a package. This value is required.</dd>

   <dt>`--summary`</dt>
   <dd>Get a summary of the package details. Parameters with the prefix "*" are bound. This flag is optional.</dd>
   </dl>

<br />**Example**

```
ibmcloud fn package get hello
```
{: pre}


<br />

### `ibmcloud fn package list`
{: #cli_pkg_list}

List all of the packages that you created or a specific number of packages.

```
ibmcloud fn package list [NAMESPACE] [--limit NUMBER_OF_PACKAGES] [--name-sort] [--skip NUMBER_OF_PACKAGES]
```
{: pre}

<br />**Command options**

   <dl>
   <dt>`NAMESPACE`</dt>
   <dd>List the packages in a specific namespace. This value is optional. If not specified, all packages are listed.</dd>

   <dt>`--limit NUMBER_OF_PACKAGES`, `-l NUMBER_OF_PACKAGES`</dt>
   <dd>List a specified number of packages. The default is 30 packages.</dd>

   <dt>`--name-sort, -n`</dt>
   <dd>Sort the list of returned packages by name, otherwise the list is sorted by creation date.</dd>

   <dt>`--skip NUMBER_OF_PACKAGES`, `-s NUMBER_OF_PACKAGES`</dt>
   <dd>Exclude a specified number of the most recently created packages from the result.</dd>

   </dl>

<br />**Example**

  ```
  ibmcloud fn package list
  ```
  {: pre}

  Run `ibmcloud fn package list /whisk.system` to view a list of pre-installed packages.
  {: tip}


<br />

### `ibmcloud fn package refresh`
{: #cli_pkg_refresh}

Refresh the package bindings for all of the packages within a specific namespace.

```
ibmcloud fn package refresh /NAMESPACE
```
{: pre}

<br />**Command options**

   <dl>

   <dt>/`NAMESPACE`</dt>
   <dd>A namespace, beginning with /. This flag is required. Run `ibmcloud fn namespace list` to get a list of namespaces to choose from.</dd>
   </dl>

<br />**Example**

  ```
  ibmcloud fn package refresh /user@domain.com_dev
  ```
  {: pre}


<br />

### `ibmcloud fn package update`
{: #cli_pkg_update}

Update a package designed to contain one or more actions. To add an action in the package, include the package name with the action name when you create or update the action.

When you update parameters for a package, action, or trigger you must specify all previously created parameters. Otherwise, the previously created parameters are removed. For packages, any services that were bound to the package are also removed, so after you update other parameters you must [bind services](/docs/openwhisk?topic=cloud-functions-services) to your package again.
{: important}

```
ibmcloud fn package update PACKAGE_NAME [--annotation ANNOTATION_KEY ANNOTATION_VALUE] [--annotation-file FILE] [--param KEY VALUE] [--param-file FILE]
```
{: pre}

<br />**Command options**

   <dl>

   <dt>`PACKAGE_NAME`</dt>
   <dd>The name of the package. This value is required. </dd>

   <dt>`--annotation` `ANNOTATION_KEY` `ANNOTATION_VALUE`, `-a` `ANNOTATION_KEY` `ANNOTATION_VALUE`</dt>
   <dd>Annotations are specified in a `KEY` `VALUE` format. To include more than one annotation, specify this option for each annotation. This flag is optional.</dd>

   <dt>`--annotation-file` `FILE`, `-A` `FILE`</dt>
   <dd>A JSON file that contains annotation in a `KEY` `VALUE` format. This flag is optional.</dd>

   <dt>`--param` `KEY` `VALUE`, `-p` `KEY` `VALUE`</dt>
   <dd>Parameter `VALUES` in the `KEY` `VALUE` format. This flag is optional.</dd>

   <dt>`--param-file` `FILE`, `-P` `FILE`</dt>
   <dd>A JSON file that contains parameter `KEYS` and `VALUES`. This flag is optional.</dd>

   <dt>`--shared yes|no`</dt>
   <dd>When specified without a value or with a value of `yes`, the package is shared with other users.</dd>

   </dl>

<br />**Example**

  ```
  ibmcloud fn package create hellopkg
  ```
  {: pre}

  **Output**
  ```
  ok: created hellopkg
  ```
  {: screen}




<br /><br />
## Property commands
{: #cli_prop}

Set global properties for your CLI environment or view properties about the `wsk` CLI, which runs as part of the `ibmcloud fn` CLI.

### `ibmcloud fn property get`
{: #cli_prop_get}

View the metadata details for a property from the `wsk` CLI.

```
ibmcloud fn property get [--apihost HOST] [--apiversion VERSION] [--auth KEY] [--cert STRING] [--key STRING] [--namespace NAMESPACE]
```
{: pre}

<br />**Command options**

   <dl>
   <dt>`--all`</dt>
   <dd>View all properties for the `wsk` CLI. This flag is optional.</dd>

   <dt>`---apibuild`</dt>
   <dd>The `wsk` API build information. This flag is optional.</dd>

   <dt>`--apibuildno`</dt>
   <dd>The `wsk` API build number. This flag is optional.</dd>

   <dt>`--apihost` `HOST`</dt>
   <dd>The `wsk` API host. This flag is optional.</dd>

   <dt>`--apiversion` `VERSION`</dt>
   <dd>The `wsk` API version. This flag is optional.</dd>

   <dt>`--auth` `KEY`, `-u` `KEY`</dt>
   <dd>The `wsk` authorization `KEY`. This flag is optional.</dd>

   <dt>`--cert` `STRING`</dt>
   <dd>The `wsk` client certificate. This flag is optional.</dd>

   <dt>`--cliversion`</dt>
   <dd>The `wsk` CLI version. This flag is optional.</dd>

   <dt>`--key` `STRING`</dt>
   <dd>The `wsk` client `KEY`. This flag is optional.</dd>

   <dt>`--namespace` `NAMESPACE`</dt>
   <dd>An IAM namespace. This flag cannot be set for Cloud Foundry namespaces. This flag is optional.</dd>

   </dl>

<br />**Example**

  ```
  ibmcloud fn property get --auth
  ```
  {: pre}


<br />

### `ibmcloud fn property set`
{: #cli_prop_set}

Set a property. At least one flag is required. Once a property is set, it is retained on your workstation at `<home_dir>/.bluemix/plugins/cloud-functions/config.json`. To remove a property, run [`ibmcloud fn property unset --<property>`](#cli_prop_set). 

```
ibmcloud fn property set [--apihost HOST] [--apiversion VERSION] [--auth KEY] [--cert STRING] [--key STRING] [--namespace NAMESPACE]
```
{: pre}

<br />**Command options**

   <dl>
   <dt>`--apihost` `HOST`</dt>
   <dd>The `wsk` API host. This flag is optional.</dd>

   <dt>`--apiversion` `VERSION`</dt>
   <dd>The `wsk` API version. This flag is optional.</dd>

   <dt>`--auth` `KEY`, -u</dt>
   <dd>The `wsk` authorization `KEY`. This flag is optional.</dd>

   <dt>`--cert` `STRING`</dt>
   <dd>The `wsk`client certificate. This flag is optional.</dd>

   <dt>`--key` `STRING`</dt>
   <dd>The `wsk` client `KEY`. This flag is optional.</dd>

   <dt>`--namespace` `NAMESPACE`</dt>
   <dd>An IAM namespace. This flag cannot be set for Cloud Foundry namespaces. This flag is optional.</dd>

   </dl>

<br />**Example**

  ```
  ibmcloud fn property set --namespace myNamespace
  ```
  {: pre}

  **Output**
  ```
  ok: whisk namespace set to myNamespace
  ```
  {: screen}

<br />

### `ibmcloud fn property unset`
{: #cli_prop_unset}

Unset a property for the `wsk` CLI. At least one flag is required.

```
ibmcloud fn property unset [--apihost HOST] [--apiversion VERSION] [--auth KEY] [--cert STRING] [--key STRING] [--namespace NAMESPACE]
```
{: pre}

<br />**Command options**

   <dl>
   <dt>`--apihost` `HOST`</dt>
   <dd>The `wsk` API host. This flag is optional.</dd>

   <dt>`--apiversion` `VERSION`</dt>
   <dd>The `wsk` API version. This flag is optional.</dd>

   <dt>`--auth` `KEY`, `-u`</dt>
   <dd>The `wsk` authorization `KEY`. This flag is optional.</dd>

   <dt>`--cert` `STRING`</dt>
   <dd>The `wsk` client certificate. This flag is optional.</dd>

   <dt>`--key` `STRING`</dt>
   <dd>The `wsk` client `KEY`. This flag is optional.</dd>

   <dt>`--namespace` `NAMESPACE`</dt>
   <dd>An IAM namespace. This flag cannot be set for Cloud Foundry namespaces. This flag is optional.</dd>

   </dl>

<br />**Example**

  ```
  ibmcloud fn property unset --namespace
  ```
  {: pre}



<br /><br />
## Rule commands
{: #cli_rule}


### `ibmcloud fn rule create`
{: #cli_rule_create}

Create a rule to associate a trigger with an action. Before you can create a rule, create a trigger and an action first.

```
ibmcloud fn rule create RULE_NAME TRIGGER_NAME ACTION_NAME
```
{: pre}

<br />**Example**

  ```
  ibmcloud fn rule create myrule mytrigger myaction
  ```
  {: pre}

  **Output**
  ```
  ok: created myrule
  ```
  {: screen}


<br />

### `ibmcloud fn rule delete`
{: #cli_rule_delete}

To clean up your namespace, remove rules you no longer need.

```
ibmcloud fn rule delete RULE_NAME [--disable]
```
{: pre}

<br />**Command options**

   <dl>
   <dt>`RULE_NAME`</dt>
   <dd>The name of a rule. This value is required.</dd>

  <dt>`--disable`</dt>
  <dd>Disable the rule before you deleting.</dd>
  </dl>


<br />**Example**

```
ibmcloud fn rule delete myrule
```
{: pre}


<br />

### `ibmcloud fn rule disable`
{: #cli_rule_disable}

Change the status of a rule to inactive and stop it from running an action when a trigger is fired.

```
ibmcloud fn rule disable RULE_NAME
```
{: pre}

<br />**Example**

  ```
  ibmcloud fn rule disable myrule
  ```
  {: pre}

<br />

### `ibmcloud fn rule enable`
{: #cli_rule_enable}

Change the status of a rule from inactive to active. When active, an action runs when a trigger is fired.

```
ibmcloud fn rule enable RULE_NAME
```
{: pre}

<br />**Example**

  ```
  ibmcloud fn rule enable myrule
  ```
  {: pre}

<br />

### `ibmcloud fn rule get`
{: #cli_rule_get}

Get metadata that describes a specific rule.

```
ibmcloud fn rule get RULE_NAME [--summary]
```
{: pre}

<br />**Command options**

   <dl>
   <dt>`RULE_NAME`</dt>
   <dd>The name of a rule. This value is required.</dd>

  <dt>`--summary`</dt>
  <dd>Get a summary of the rule details.</dd>
  </dl>

<br />**Example**

```
ibmcloud fn rule get myrule
```
{: pre}


<br />

### `ibmcloud fn rule list`
{: #cli_rule_list}

List all of the rules that you created or a specific number of rules.

```
ibmcloud fn rule list RULE_NAME [--limit NUMBER_OF_RULES] [--name-sort] [--skip NUMBER_OF_RULES]
```
{: pre}

<br />**Command options**

   <dl>
   <dt>`RULE_NAME`</dt>
   <dd>The name of a rule. This value is optional. If not specified, all rules are listed.</dd>

   <dt>`--limit NUMBER_OF_RULES`, `-l NUMBER_OF_RULES`</dt>
   <dd>List a specified number of rules. The default is 30 rules.</dd>

   <dt>`--name-sort`, `-n`</dt>
   <dd>Sort the list of returned rules by name, otherwise the list is sorted by creation date.</dd>

   <dt>`--skip NUMBER_OF_RULES`, `-s NUMBER_OF_RULES`</dt>
   <dd>Exclude a specified number of the most recently created rules from the result.</dd>

   </dl>

<br />**Example**

  ```
  ibmcloud fn rule list
  ```
  {: pre}


<br />

### `ibmcloud fn rule status`
{: #cli_rule_status}

See whether a rule is active or inactive. Run the `ibmcloud fn rule disable` or `ibmcloud fn run enable` commands to change the status.

```
ibmcloud fn rule status RULE_NAME
```
{: pre}

<br />**Example**

  ```
  ibmcloud fn rule status myrule
  ```
  {: pre}


<br />

### `ibmcloud fn rule update`
{: #cli_rule_update}

To change which triggers are associated with which rules, you can update a rule.

```
ibmcloud fn rule update RULE_NAME TRIGGER_NAME ACTION_NAME
```
{: pre}

<br />**Example**

  ```
  ibmcloud fn rule update myrule mytrigger myaction
  ```
  {: pre}



<br /><br />

## SDK command
{: #cli_sdk}


### `ibmcloud fn sdk install`
{: #cli_sdk_install}

Install an SDK.

```
ibmcloud fn sdk install COMPONENT [--limit NUMBER_OF_TRIGGERS]
```
{: pre}

<br />**Command options**

   <dl>
   <dt>`COMPONENT`</dt>
   <dd>The SDK component, such as `docker`, `iOS`, and `bashauto`. This value is required.</dd>

   <dt>`--stdout, --s`</dt>
   <dd>Prints the bash command results to `STDOUT`. This flag is optional.</dd>


   </dl>

<br />**Example**

  ```
  ibmcloud fn sdk install docker
  ```
  {: pre}



<br /><br />

## Service commands
{: #cli_service}


### `ibmcloud fn service bind`
{: #cli_service_bind}

Bind service credentials to an action or package.

```
ibmcloud fn service bind SERVICE PACKAGE_or_ACTION_NAME [--instance SERVICE_INSTANCE] [--keyname SERVICE_KEY]
```
{: pre}

<br />**Command options**

   <dl>

   <dt>`SERVICE`</dt>
   <dd>The name of the service.</dd>

   <dt>`PACKAGE_or_``ACTION_NAME`</dt>
   <dd>The name of the package or action to bind the credentials to.</dd>

   <dt>`--instance SERVICE_INSTANCE`</dt>
   <dd>The service instance name.</dd>

   <dt>`--keyname SERVICE_``KEY`</dt>
   <dd>The name of the service `KEY` credentials to bind.</dd>

   </dl>

<br />**Example**

  ```
  ibmcloud fn service bind cloudant hello --instance CLOUDANT_SERVICE
  ```
  {: pre}


<br />

### `ibmcloud fn service unbind`
{: #cli_service_unbind}

Unbind service credentials from an action or package.

```
ibmcloud fn service unbind SERVICE PACKAGE_or_ACTION_NAME
```
{: pre}

<br />**Command options**

   <dl>

   <dt>`SERVICE`</dt>
   <dd>The name of the service.</dd>

   <dt>`PACKAGE_or_``ACTION_NAME`</dt>
   <dd>The name of the package or action to unbind the credentials from.</dd>

   </dl>

<br />**Example**

  ```
  ibmcloud fn service unbind cloudant hello
  ```
  {: pre}



<br /><br />

## Trigger commands
{: #cli_trigger}


### `ibmcloud fn trigger create`
{: #cli_trigger_create}

Create a trigger.

```
ibmcloud fn trigger create TRIGGER_NAME [--annotation ANNOTATION_KEY ANNOTATION_VALUE] [--annotation-file FILE] [--feed ACTION_NAME] [--param KEY VALUE] [--param-file FILE]
```
{: pre}

<br />**Command options**

   <dl>
   <dt>`TRIGGER_NAME`</dt>
   <dd>The name of the trigger. This value is required. </dd>

   <dt>`--annotation` `ANNOTATION_KEY` `ANNOTATION_VALUE`, `-a` `ANNOTATION_KEY` `ANNOTATION_VALUE`</dt>
   <dd>Annotations are specified in a `KEY` `VALUE` format. To include more than one annotation, specify this option for each annotation. This flag is optional.</dd>

   <dt>`--annotation-file` `FILE`, `-A` `FILE`</dt>
   <dd>A JSON file that contains annotation in a `KEY` `VALUE` format. This flag is optional.</dd>

   <dt>`--feed` `ACTION_NAME`, `-f` `ACTION_NAME`</dt>
   <dd>Sets the type of trigger as a feed. This flag is optional.</dd>

   <dt>`--param` `KEY` `VALUE`, `-p` `KEY` `VALUE`</dt>
   <dd>Parameter `VALUES` in the `KEY` `VALUE` format. This flag is optional.</dd>

   <dt>`--param-file` `FILE`, `-P` `FILE`</dt>
   <dd>A JSON file that contains parameter `KEYS` and `VALUES`. This flag is optional.</dd>


   </dl>

<br />**Example**
```
ibmcloud fn trigger create mytrigger --param name Bob
```
{: pre}


<br />

### `ibmcloud fn trigger delete`
{: #cli_trigger_delete}

Delete a trigger.

```
ibmcloud fn trigger delete TRIGGER_NAME
```
{: pre}

<br />**Example**

```
ibmcloud fn trigger delete mytrigger
```
{: pre}


<br />

### `ibmcloud fn trigger fire`
{: #cli_trigger_fire}

Test a trigger by firing it, rather than waiting for it to be triggered automatically.

```
ibmcloud fn trigger fire TRIGGER_NAME [--param KEY VALUE] [--param-file FILE]
```
{: pre}

<br />**Command options**

   <dl>

   <dt>`TRIGGER_NAME`</dt>
   <dd>The name of the trigger. This value is required. </dd>

   <dt>`--param` `KEY` `VALUE`, `-p` `KEY` `VALUE`</dt>
   <dd>Parameter `VALUES` in the `KEY` `VALUE` format. This flag is optional.</dd>

   <dt>`--param-file` `FILE`, `-P` `FILE`</dt>
   <dd>A JSON file that contains parameter `KEYS` and `VALUES`. This flag is optional.</dd>

   </dl>

<br />**Example**

  ```
  ibmcloud fn trigger fire --param name Bob
  ```
  {: pre}


<br />

### `ibmcloud fn trigger get`
{: #cli_trigger_get}

Get metadata that describes a specific trigger.

```
ibmcloud fn trigger get TRIGGER_NAME [--summary]
```
{: pre}

<br />**Command options**

   <dl>
   <dt>`TRIGGER_NAME`</dt>
   <dd>The name of a trigger. This value is required.</dd>

  <dt>`--summary`</dt>
  <dd>Get a summary of the trigger details.</dd>
  </dl>

<br />**Example**

```
ibmcloud fn trigger get mytrigger
```
{: pre}

<br />

### `ibmcloud fn trigger list`
{: #cli_trigger_list}

List all of the triggers that you created or a specific number of triggers.

```
ibmcloud fn trigger list TRIGGER_NAME [--limit NUMBER_OF_TRIGGERS] [--name-sort] [--skip NUMBER_OF_TRIGGERS]
```
{: pre}

<br />**Command options**

   <dl>
   <dt>`RULE_NAME`</dt>
   <dd>The name of a trigger. This value is optional. If not specified, all triggers are listed.</dd>

   <dt>`--limit` `NUMBER_OF_TRIGGERS`, `-l` `NUMBER_OF_TRIGGERS`</dt>
   <dd>List a specified number of triggers. The default is 30 triggers.</dd>

   <dt>`--name-sort, -n`</dt>
   <dd>Sort the list of returned triggers by name, otherwise the list is sorted by creation date.</dd>

   <dt>`--skip` `NUMBER_OF_TRIGGERS`, `-s` `NUMBER_OF_TRIGGERS`</dt>
   <dd>Exclude a specified number of the most recently created triggers from the result.</dd>

   </dl>

<br />**Example**

  ```
  ibmcloud fn trigger list
  ```
  {: pre}


<br />

### `ibmcloud fn trigger update`
{: #cli_trigger_update}

Update a trigger.

When you update parameters for a package, action, or trigger you must specify all previously created parameters. Otherwise, the previously created parameters are removed. For packages, any services that were bound to the package are also removed, so after you update other parameters you must [bind services](/docs/openwhisk?topic=cloud-functions-services) to your package again.
{: important}

```
ibmcloud fn trigger update TRIGGER_NAME [--annotation ANNOTATION_KEY ANNOTATION_VALUE] [--annotation-file FILE] [--param KEY VALUE] [--param-file FILE]
```
{: pre}

<br />**Command options**

   <dl>
   <dt>`TRIGGER_NAME`</dt>
   <dd>The name of the trigger. This value is required. </dd>

   <dt>`--annotation` `ANNOTATION_KEY` `ANNOTATION_VALUE`, `-a` `ANNOTATION_KEY` `ANNOTATION_VALUE`</dt>
   <dd>Annotations are specified in a `KEY` `VALUE` format. To include more than one annotation, specify this option for each annotation. This flag is optional.</dd>

   <dt>`--annotation-file` `FILE`, `-A` `FILE`</dt>
   <dd>A JSON file that contains annotation in a `KEY` `VALUE` format. This flag is optional.</dd>

   <dt>`--param` `KEY` `VALUE`, `-p` `KEY` `VALUE`</dt>
   <dd>Parameter values in the `KEY` `VALUE` format. This flag is optional.</dd>

   <dt>`--param-file` `FILE`, `-P` `FILE`</dt>
   <dd>A JSON file that contains parameter `KEYS` and `VALUES`. This flag is optional.</dd>
   </dl>

<br />**Example**
```
ibmcloud fn trigger update mytrigger --param name Jim
```
{: pre}





