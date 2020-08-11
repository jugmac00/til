# How do you surround marked text with a custom snippet?

In order to mark strings as "translatable" in Flask via Flask-WTF, you need to apply special syntax.

This means, e.g. in a Jinja template a string like `Conference` has to be transformed into `{{ _('Conference') }}`.

This is a very tedious work, so I created a shortcut for it.

Add the following lines to your `keybindings.json`:

    "key": "ctrl+shift+alt+0",
    "command": "editor.action.insertSnippet",
    "when": "editorHasSelection || editorHasMultipleSelections",
    "args": {
        "snippet": "{{ _('${TM_SELECTED_TEXT}') }}"
    }

I used "ctrl+shift+alt+0" as on the German keyboard the closing curly brace is on the same key as the `0`.

via https://stackoverflow.com/a/53545200/672833
