# JCB! Fields

### What Are Fields?
Fields are the **foundation** of every Joomla Component Builder (JCB) project.

They define how data is **stored**, **validated**, **rendered**, and **interacted with** in your Joomla extensions.

Fields let you control everything from the **underlying database schema** to the **user interface**, all within a single configuration.

Each Field:
- Defines **database structure** (type, size, default, null, unique keys, indexes)
- Binds to a **fieldtype**, determining HTML rendering and behavior
- Supports per-field **custom PHP** for model saving and retrieval
- Allows styling and scripting (HTML attributes, JS, CSS)
- Automatically generates Joomla-compliant XML field definitions

### Where Are Fields Used in JCB?
Fields are universal integrated — they are used in, highly structured areas:

- ✅ **Admin Views** (the native Joomla back-end editing views)
- ✅ **Modules** (frontend display configurations)
- ✅ **Plugins** (event-driven integrations)
- ✅ **Component Configurations** (global parameter settings)

### What Can a Field Do?
A Field in JCB can define:

- **Database Type & Schema**: `int`, `varchar`, `json`, custom, nullable, defaults, indexes
- **Permissions**: who can view/edit the field (ACL)
- **Rendering Options**: HTML classes, labels, JS behaviors
- **Model Integration**: how the value is saved or retrieved
- **Dynamic Logic**: PHP hooks for `onGet`, `onSave`, `onPrepareForm`, etc.
- **Fieldtypes**: link to rich behaviors like Model Selects, Subforms, Toggle Switches, Encrypted Fields, etc.

This centralization makes field management efficient and highly reusable.

### Reuse and Sharing
Fields are standalone entities:

- Define once, **reuse across multiple Admin Views**, Modules, or Plugins
- Fields can also be exported and shared via repositories
- JCB will automatically adjust them to fit into each consuming context

This means less duplication, and greater consistency across your entire component structure.

### Versioning and Customization
To update a field:

- Click **"reset"** in the JCB UI to sync with this repository
- Or **fork** this repository, customize the field, and point JCB to your fork

This preserves version control while allowing your own field improvements to live independently.

>Fields define both structure and behavior — they are where your data comes alive.

---
### Index of Fields


 - **Authorization Code** | [Details](src/field/662686e0-b0c2-4a06-b11b-5421eace7a13) | [Settings](src/field/662686e0-b0c2-4a06-b11b-5421eace7a13/item.json)
 - **Banned Words** | [Details](src/field/df8eb142-cdfc-4e8c-ab6a-5e7cde268440) | [Settings](src/field/df8eb142-cdfc-4e8c-ab6a-5e7cde268440/item.json)
 - **CALPAY Security Key** | [Details](src/field/c3eecfb8-d9ab-48ba-b9d0-4bfa607459f1) | [Settings](src/field/c3eecfb8-d9ab-48ba-b9d0-4bfa607459f1/item.json)
 - **Country** | [Details](src/field/d299b94d-42c5-4abd-b27a-9c0a4ad3a721) | [Settings](src/field/d299b94d-42c5-4abd-b27a-9c0a4ad3a721/item.json)
 - **Customer** | [Details](src/field/2bde03cb-c09a-4f09-aee2-c03f0676a581) | [Settings](src/field/2bde03cb-c09a-4f09-aee2-c03f0676a581/item.json)
 - **Order Description** | [Details](src/field/7927473d-b87f-4a16-8ed2-a27e139acda7) | [Settings](src/field/7927473d-b87f-4a16-8ed2-a27e139acda7/item.json)
 - **Product** | [Details](src/field/7e8314a4-e6f5-4ac0-90b1-d916e10bed28) | [Settings](src/field/7e8314a4-e6f5-4ac0-90b1-d916e10bed28/item.json)
 - **State Province** | [Details](src/field/9d1b2235-c8b0-4374-94de-a292ec2b72c9) | [Settings](src/field/9d1b2235-c8b0-4374-94de-a292ec2b72c9/item.json)
 - **Transaction  Status** | [Details](src/field/d3d7458c-4b9d-4008-b28a-a5143a9090fb) | [Settings](src/field/d3d7458c-4b9d-4008-b28a-a5143a9090fb/item.json)
 - **Transaction Amount** | [Details](src/field/aa28d053-8456-4977-8126-119dc65ad6c1) | [Settings](src/field/aa28d053-8456-4977-8126-119dc65ad6c1/item.json)
 - **Transaction ID** | [Details](src/field/e7c1df34-f3ac-4c33-9eff-ddacbe803cf7) | [Settings](src/field/e7c1df34-f3ac-4c33-9eff-ddacbe803cf7/item.json)
 - **Transaction Type** | [Details](src/field/d56e382d-a1e8-4afb-adee-c0bff52abed6) | [Settings](src/field/d56e382d-a1e8-4afb-adee-c0bff52abed6/item.json)
 - **URL** | [Details](src/field/d29d6854-bb4a-4fa2-83a1-5a1b9c9a0eaf) | [Settings](src/field/d29d6854-bb4a-4fa2-83a1-5a1b9c9a0eaf/item.json)
 - **University** | [Details](src/field/74af1ce6-2ee5-4cd9-a7e9-e1297b641b7e) | [Settings](src/field/74af1ce6-2ee5-4cd9-a7e9-e1297b641b7e/item.json)
 - **allow_non_latin** | [Details](src/field/1c779c3a-ee1f-46b9-8362-2d518de66f1f) | [Settings](src/field/1c779c3a-ee1f-46b9-8362-2d518de66f1f/item.json)
 - **answer** | [Details](src/field/a86d7c74-6787-40f2-bb42-1522c9e61dd5) | [Settings](src/field/a86d7c74-6787-40f2-bb42-1522c9e61dd5/item.json)
 - **apiUrl** | [Details](src/field/f16e0e32-2550-465d-ae64-21345f8741df) | [Settings](src/field/f16e0e32-2550-465d-ae64-21345f8741df/item.json)
 - **enable_logging** | [Details](src/field/ca90447c-49db-4ce1-9d5a-f8d453ac0b06) | [Settings](src/field/ca90447c-49db-4ce1-9d5a-f8d453ac0b06/item.json)
 - **enable_trace** | [Details](src/field/fda23329-b769-4143-a76d-abfe0314e11a) | [Settings](src/field/fda23329-b769-4143-a76d-abfe0314e11a/item.json)
 - **log_path** | [Details](src/field/2a0b3538-9e6b-40b8-a916-402db93f9783) | [Settings](src/field/2a0b3538-9e6b-40b8-a916-402db93f9783/item.json)
 - **question** | [Details](src/field/fddbbe01-a435-481a-b09f-12cb97c71245) | [Settings](src/field/fddbbe01-a435-481a-b09f-12cb97c71245/item.json)
 - **transaction_date** | [Details](src/field/babcb176-a9ee-4113-9f8a-a89ae34e80b0) | [Settings](src/field/babcb176-a9ee-4113-9f8a-a89ae34e80b0/item.json)

### All used in [Joomla Component Builder](https://www.joomlacomponentbuilder.com) - [Source](https://git.vdm.dev/joomla/Component-Builder) - [Mirror](https://github.com/vdm-io/Joomla-Component-Builder) - [Download](https://git.vdm.dev/joomla/pkg-component-builder/releases)

---
[![Joomla Volunteer Portal](https://img.shields.io/badge/-Joomla-gold?logo=joomla)](https://volunteers.joomla.org/joomlers/1396-llewellyn-van-der-merwe "Join Llewellyn on the Joomla Volunteer Portal: Shaping the Future Together!") [![GitHub](https://img.shields.io/badge/-Git-181717?logo=git)](https://github.com/joomengine "Build premium Joomla extensions with JoomEngine on GitHub: Help us raise Joomla extension standards!") [![Octoleo](https://img.shields.io/badge/-Octoleo-black?logo=linux)](https://git.vdm.dev/octoleo "--quiet") [![Llewellyn](https://img.shields.io/badge/-Llewellyn-ffffff?logo=gitea)](https://git.vdm.dev/Llewellyn "Collaborate and Innovate with Llewellyn on Git: Building a Better Code Future!") [![Telegram](https://img.shields.io/badge/-Telegram-blue?logo=telegram)](https://t.me/Joomla_component_builder "Join Llewellyn and the Community on Telegram: Building Joomla Components Together!") [![Mastodon](https://img.shields.io/badge/-Mastodon-9e9eec?logo=mastodon)](https://joomla.social/@llewellyn "Connect and Engage with Llewellyn on Joomla Social: Empowering Communities, One Post at a Time!") [![X (Twitter)](https://img.shields.io/badge/-X-black?logo=x)](https://x.com/llewellynvdm "Join the Conversation with Llewellyn on X: Where Ideas Take Flight!") [![GitHub](https://img.shields.io/badge/-GitHub-181717?logo=github)](https://github.com/Llewellynvdm "Build, Innovate, and Thrive with Llewellyn on GitHub: Turning Ideas into Impact!") [![YouTube](https://img.shields.io/badge/-YouTube-ff0000?logo=youtube)](https://www.youtube.com/@OctoYou "Explore, Learn, and Create with Llewellyn on YouTube: Your Gateway to Inspiration!") [![n8n](https://img.shields.io/badge/-n8n-black?logo=n8n)](https://n8n.io/creators/octoleo "Effortless Automation and Impactful Workflows with Llewellyn on n8n!") [![Docker Hub](https://img.shields.io/badge/-Docker-grey?logo=docker)](https://hub.docker.com/r/octoleo/joomengine "JoomEngine on Docker: Containerize Your Creativity!") [![Open Collective](https://img.shields.io/badge/-Donate-green?logo=opencollective)](https://opencollective.com/joomla-component-builder "Donate towards JCB: Help Llewellyn financially so he can continue developing this great tool!") [![GPG Key](https://img.shields.io/badge/-GPG-blue?logo=gnupg)](https://git.vdm.dev/Llewellyn/gpg "Unlock Trust and Security with Llewellyn's GPG Key: Your Gateway to Verified Connections!")