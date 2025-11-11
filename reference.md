# Reference
## ControllerApi
<details><summary><code>client.controller_api.<a href="src/aui/controller_api/client.py">list_user_tasks</a>(...)</code></summary>
<dl>
<dd>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from aui import ApolloClient

client = ApolloClient(
    network_api_key="YOUR_NETWORK_API_KEY",
    api_key="YOUR_API_KEY",
)
client.controller_api.list_user_tasks(
    user_id="user_id",
    page=1,
    size=1,
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**user_id:** `str` 
    
</dd>
</dl>

<dl>
<dd>

**page:** `typing.Optional[int]` 
    
</dd>
</dl>

<dl>
<dd>

**size:** `typing.Optional[int]` 
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.controller_api.<a href="src/aui/controller_api/client.py">create_task</a>(...)</code></summary>
<dl>
<dd>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from aui import ApolloClient

client = ApolloClient(
    network_api_key="YOUR_NETWORK_API_KEY",
    api_key="YOUR_API_KEY",
)
client.controller_api.create_task(
    user_id="user_id",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**user_id:** `str` 
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.controller_api.<a href="src/aui/controller_api/client.py">get_task_messages</a>(...)</code></summary>
<dl>
<dd>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from aui import ApolloClient

client = ApolloClient(
    network_api_key="YOUR_NETWORK_API_KEY",
    api_key="YOUR_API_KEY",
)
client.controller_api.get_task_messages(
    task_id="task_id",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**task_id:** `str` 
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.controller_api.<a href="src/aui/controller_api/client.py">send_message</a>(...)</code></summary>
<dl>
<dd>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from aui import ApolloClient

client = ApolloClient(
    network_api_key="YOUR_NETWORK_API_KEY",
    api_key="YOUR_API_KEY",
)
client.controller_api.send_message(
    is_external_api=True,
    task_id="task_id",
    text="text",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**task_id:** `str` 
    
</dd>
</dl>

<dl>
<dd>

**text:** `str` 
    
</dd>
</dl>

<dl>
<dd>

**is_external_api:** `typing.Optional[bool]` 
    
</dd>
</dl>

<dl>
<dd>

**context:** `typing.Optional[Context]` 
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

