# hugo-slack-format
A Hugo Shortcode and Partial to insert a Slack formatted conversation. 

## Installation

Copy `partials/extended_head.html` into `layout/partials/` or add the content to your existing `layout/partials/extended_head.html` file. This provides the Slack styling.

Copy `shortcodes/slack.html` into `layout/shortcodes/`

## Usage

This shortcode requires pages resources, so your post must be a [page bundle](https://gohugo.io/content-management/page-bundles/).

Slack Conversations are defined in data files. Insert a Slack conversation with the shortcode `slack` and provide the filename via the `script` argument, e.g.: `{{< slack script="example.yml" >}}`.

You can provide an optional channel title, with the `channel` argument, e.g. `{{< slack script="example.yml" channel="general" >}}`. The `#` is inserted automatically.

The file contains an array of objects:

```yaml
example.yml
---
- name: John Smith
  avatar: john-smith.png
  timestamp: '12:01 PM'
  messages:
    - Hi, how are you today?
    - "Sorry I'm late to the meeting."
- name: Jane Doe
  avatar: jane-doe.png
  messages:
    - "Hi, John, I'm doing fine, and no worries about starting late!"
```

The `avatar` key should reference a page resource image to use as the Slack avatar.
The timestamp is rendered as is, so no need to worry about date time objects or timezones :).

Each message is rendered as markdown in its own `<p>` tag.

The css styles have some tricks to format links the way Slack does:
* To get a highlighted link that is underlined on hover, you can just use an empty link, e.g. `[text]()`.
* To get an @-mention with the background highlight, create a link to `@`, e.g. `[@Jane Doe](@)`.
* To get a channel name with the background highlight, create a link to `#`, e.g. `[#general](#)`.

A couple good resources for avatar creation:

* https://getavataaars.com
* https://avatars.pco.bz
