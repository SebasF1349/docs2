---
layout: default
title: OBS Studio
menu: Integrations
num: 1
permalink: /integrations/obs
type: fullpage
---

SAMMI communicates with OBS via OBS Websocket (OBSWS), which allows you to remotely control and listen to OBS Studio events. 

#### Install OBS Websocket

SAMMI is compatible with both OBS websocket 5.0 and 4.9. As OBSWS 5 is still very new, please note that some of your extensions might not work with it until they have been updated. 

OBS Studio 28 comes bundled with OBS Websocket 5.0. There is no need to download a separate plugin for it. 

To ensure the 4.9 version protocol is still supported, you can download the 4.9.1-compat plugin for OBS Studio 28 available at the link below.

<a href="https://github.com/obsproject/obs-websocket/releases/tag/4.9.1-compat"><button type="button" class="btn btn-outline-secondary">Download OBS Websocket 4.9.1 for OBS 28</button></a>

<a href="https://github.com/obsproject/obs-websocket/blob/4.x-compat/docs/generated/protocol.md#events"><button type="button" class="btn btn-outline-secondary">OBS Websocket 4.9.1 Protocol</button></a>

<a href="https://github.com/obsproject/obs-websocket/blob/master/docs/generated/protocol.md"><button type="button" class="btn btn-outline-secondary">OBS Websocket 5.0 Protocol</button></a>

<hr>

#### Connect SAMMI to OBS Websocket
You do not need to download OBS Websocket 5.0 if you are running OBS version 28 as it is bundled with the OBS install. You will only need to download the OBS 4.9.1-compat plugin if you wish to run OBS Websocket 4.9 which some extensions might still need. 

In your SAMMI click on **OBS Connections** at the bottom menu:
- `Name`: Name of your OBS. The first OBS will always be Main and cannot be changed. 
- `Protocol`: Choose the protocol your OBS Websocket is using. Choose OBSws4 or OBSws5 accordingly. 
- `IP`: IP Address of the OBS Websocket. Unless you're connecting to an OBS on another computer, it will be always `127.0.0.1`.
- `Port`: Port of the OBS Websocket. Must match the port in your OBS-Tools-Websocket Server Settings. Default port for OBSws5 is `4455` and for OBSws4 `4444`. We do not recommend changing the default port. 
- `Password`: Password to authorize with OBS Websocket. Leave empty, unless you checked Enable Authorization in OBS-Tools-OBS Websocket Settings. In that case the passwords must match. 
- `Auto Connect`: Whether you want SAMMI to automatically connect to OBS Websocket on launch
- `Non-Blocking`: Leave checked unless you have difficulties connecting to OBS Websocket. 

  {% include image.html w="75" src="obs_connection.png" alt="OBSWS settings in SAMMI and OBS must match" type="image" %}

Once you press **connect**, you should see the `OBS Main` light indicator turn from red to green in your SAMMI.

<hr>

#### Connect SAMMI to multiple OBS Websockets
You can connect SAMMI to multiple OBS Websockets, just add another connection in your OBS Connections settings.

You will need to manually select your OBS Name for all your OBS commands (if not using Main OBS connection), so SAMMI knows which OBS to send them to. OBS Name accepts variables as inserts as well.

{% include image.html w="75" src="obs-manual-select.png" alt="Manually select OBS name for OBS commands" %}

<hr>

#### Control OBS from SAMMI
You can remotely control your OBS Studio with [SAMMI OBS commands]({{ "commands/obs-general" | relative_url }}).   


**1. Navigate to an existing deck or click on `Add a new deck` in your SAMMI**\
**2. Right click on an empty grid and select `Create Button`**\
**3. Click on the <i class="fas fa-plus-circle"></i> and add your OBS command(s)**
  - Example 1: Switch to previous scene
    {% include image.html w="75" src="obs-switch-scenes.png" alt="Switch to previous scene" %}
  - Example 2: Change text in your Text (GDI+) source in OBS
    {% include image.html w="75" src="obs-gdi-text.png" alt="Change text in your Text (GDI+) source" %}
  - Example 3: Change position of a source
    {% include image.html w="75" src="obs-source-position.png" alt="Change source position" %}

{% include alert.html text="You can combine your OBS commands with all other SAMMI commands to create complex logic." type="info" %} 

**4. Click Save in your edit button screen and then Save again in your deck. This is an important step to save your button!**\
**5. Press the button in your SAMMI Deck while connected to OBS to execute the command(s).**

  {% include video.html w="75" src="obs-control.mp4" alt="Controlling OBS remotely from SAMMI" %}

#### Permanent Variables
Once you're connected to OBS Websocket, SAMMI provides you with some useful permanent variables that you can use in your commands.\
All OBS variables are saved in `global.[obsName]` object.\
**If you're using only one single OBS connection**, your variables will be always saved in `global.Main`, for example `global.Main.connected`.

{% include image.html w="75" src="obs_variables.png" alt="Variable window showing permanent OBS variables" %}

| Variable | Explanation| 
|-------|--------|--------
{% include selectAll.html text="<code>global.[obsName].connected</code>" %} | Whether you're connected to your selected OBS Name, 1 = connected, 0 = not connected
{% include selectAll.html text="<code>global.[obsName].current_scene</code>" %} | Your selected OBS current scene
{% include selectAll.html text="<code>global.[obsName].previous_scene</code>" %} | Your selected OBS previous scene
{% include selectAll.html text="<code>global.[obsName].type</code>" %} | OBSws selected type in OBS Connections, either `OBSws4`, `OBSws5` or `Auto`
{% include selectAll.html text="<code>global.[obsName].ip</code>" %} | The IP address of the OBS connection
{% include selectAll.html text="<code>global.[obsName].port</code>" %} | The port of the OBS connection
{% include selectAll.html text="<code>global.[obsName].obs_studio_version</code>" %} | Current OBS studio version the OBSws is connected to
{% include selectAll.html text="<code>global.[obsName].obs_websocket_version</code>" %} |  Current OBS Websocket version the OBSws is connected to
{:class='table table-secondary w-auto table-hover text-break' }

<hr>


#### Listen to OBS events in SAMMI
You can trigger buttons in your SAMMI by listening to events in your OBS Studio, such as switching to a new scene or enabling a studio mode.\
You can find a detailed guide to setting up your OBS triggers in our [Triggers-OBS]({{ "triggers/obs" | relative_url }}) section. 
