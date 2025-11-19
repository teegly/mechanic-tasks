# Advanced: Scheduled section publishing

**🚨 This is an advanced task, intended for technical users. For tasks like these, the Mechanic team only offers support with platform-level issues. For help with task-level issues (e.g. debugging, configuration, customization, monitoring, etc), see [Hire a Mechanic developer](https://learn.mechanic.dev/hire-a-developer).**

Tags: Advanced, Publish, Schedule, Sections, Unpublish

This advanced task allows you to manually trigger or schedule section publishing and unpublishing for your Shopify store. Configure the task with your theme ID and choose between manual execution (button push) or scheduled execution (datetime-based).

* View in the task library: [tasks.mechanic.dev/advanced-scheduled-section-publishing](https://tasks.mechanic.dev/advanced-scheduled-section-publishing)
* Task JSON, for direct import: [task.json](../../tasks/advanced-scheduled-section-publishing.json)
* Preview task code: [script.liquid](./script.liquid)

## Default options

```json
{
  "run_mode__required": "manual",
  "datetime_to_publish__datetime_futureonly": null,
  "theme_id__number_required": null,
  "template_name__required": "index",
  "section_visibility__keyval": {},
  "fetch_template_sections__boolean": false
}
```

[Learn about task options in Mechanic](https://learn.mechanic.dev/core/tasks/options)

## Subscriptions

```liquid
mechanic/scheduler/10min
mechanic/user/trigger
mechanic/actions/perform
```

[Learn about event subscriptions in Mechanic](https://learn.mechanic.dev/core/tasks/subscriptions)

## Documentation

This advanced task allows you to manually trigger or schedule section publishing and unpublishing for your Shopify store. Configure the task with your theme ID and choose between manual execution (button push) or scheduled execution (datetime-based).

__Key Features:__
- **Manual or Scheduled Mode**: Run immediately with a button push or schedule for a specific datetime
- **Calendar Date/Time Picker**: Easy-to-use calendar interface for selecting the publish datetime
- **Flexible Configuration**: Save the task without needing to set a schedule
- **Section Discovery**: Automatically fetch and display available sections from your theme templates
- **Metafield Storage**: Discovered sections are saved to a shop metafield viewable in Shopify Admin
- **User-Friendly Interface**: Use keyval pairs to easily show or hide sections by template

__Configuration Options:__

**Run Mode**: Choose between:
- **manual** - Execute immediately when you trigger the task (button push)
- **scheduled** - Execute automatically at the specified datetime

**Datetime to Publish** (only required for scheduled mode):
- Use the built-in calendar picker to select date and time
- Minutes must be a multiple of 10 (since that is the smallest scheduler interval)
- Leave blank when using manual mode

**Theme ID**: Your Shopify theme ID (required)

**Template Name**: The template to modify (e.g., "index", "page.contact")
- Do not include the _.json_ suffix

**Fetch Template Sections**: Enable this to discover available sections
- When enabled, the task will read your template and show all available sections in the logs
- **NEW**: Discovered sections are automatically saved to a shop metafield at `mechanic.discovered_sections_{template_name}`
- View the metafield in Shopify Admin: Settings > Custom data > Metafields
- The metafield contains a JSON array with section IDs, types, and current visibility status

**Section Visibility Configuration**:
Use the keyval fields to configure sections:
- **Left side (key)**: Section ID (e.g., "collage", "123456abcdef")
- **Right side (value)**: "show" to publish/enable or "hide" to unpublish/disable
- You can configure multiple sections per template by adding multiple key-value pairs

__Important Notes:__
- In manual mode, the task will execute immediately when triggered, without checking the datetime
- In scheduled mode, the task will only execute when the current time matches the configured datetime
- Template names should be entered without the _.json_ suffix
- Section IDs can be found in your theme's template JSON files in the "sections" object
- Use the "Fetch template sections" option to automatically discover available sections and save them to a metafield

__How to Discover Sections:__
1. Enable "Fetch template sections"
2. Run the task manually (button push)
3. Check the task logs OR go to Shopify Admin > Settings > Custom data > Metafields to view the discovered sections
4. Use the section IDs from the metafield to configure section visibility
5. Disable "Fetch template sections" once you've configured your sections (optional)

_Example Configuration (Scheduled Mode):_
- Run mode: __scheduled__
- Datetime to publish: Use the calendar picker to select __2025-12-31 13:30__
- Theme ID: __1234567890__
- Template name: __index__
- Fetch template sections: __false__ (after initial discovery)
- Sections to configure:
  - _collage_: show
  - _header_: show
  - _old-banner_: hide

_Example Configuration (Manual Mode):_
- Run mode: __manual__
- Theme ID: __1234567890__
- Template name: __index__
- Sections to configure:
  - _announcement-bar_: show
  - _slideshow_: hide

## Installing this task

Find this task [in the library at tasks.mechanic.dev](https://tasks.mechanic.dev/advanced-scheduled-section-publishing), and use the "Try this task" button. Or, import [this task's JSON export](../../tasks/advanced-scheduled-section-publishing.json) – see [Importing and exporting tasks](https://learn.mechanic.dev/core/tasks/import-and-export) to learn how imports work.

## Contributions

Found a bug? Got an improvement to add? Start here: [../../CONTRIBUTING.md](../../CONTRIBUTING.md).

## Task requests

Submit your [task requests](https://mechanic.canny.io/task-requests) for consideration by the Mechanic community, and they may be chosen for development and inclusion in the [task library](https://tasks.mechanic.dev/)!
