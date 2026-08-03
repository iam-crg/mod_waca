### JCB! Joomla Module
# WACA (v1.0.0)
## waca

Displays universities

### Module Settings
| Setting     | Value          |
|-------------|----------------|
| Target Area | ![Site](https://img.shields.io/badge/Site-blue?style=flat-square)  |
| Add README  | ![no](https://img.shields.io/badge/no-blue?style=flat-square)   |

## Default Template:
```html
<h1>Universities in <?php echo $country; ?></h1>
<table class="table table-striped" id="universityList" >
      <thead style="font-size:1.5em"><tr><td>Country</td>
        <td>State</td><td>University Name</td><td>URL</td></tr></thead>
		<tfoot><tr><td colsepan=4></td></tr></tfoot>
		<tbody>
          <?php foreach ($universities as $item): ?>
          <tr class='country'>
            <td class='country'> <?php echo $item->country; ?></td>
            <td class='country'><?php echo $item->state_province; ?> </td>
            <td class='country'><?php echo $item->university; ?></td>
            <td class='country'><a href='<?php echo $item->url; ?>'  target="_blank">Visit Site</a></td>
         </tr>
          <?php  endforeach; ?>
          </tbody>
	</table
```

<details>
<summary>Dispatcher getLayoutData Method (J4+)</summary>

```php
    $helper = $this->getHelperFactory()->getHelper('WacaHelper', $data);

    $params = $data['params'];

    // Fixed: Added null-coalescing operator fallback string to satisfy PHP 8.1+ type rules
    $data['moduleclass_sfx'] = htmlspecialchars(
        $params->get('moduleclass_sfx') ?? '',
        ENT_QUOTES,
        'UTF-8'
    );

    $country = $params->get('country');

    $data['country'] = $country;
    $data['universities'] = $helper::getuniversities($country);
```

</details>

> Display reusable content or functionality anywhere on your site with this flexible, position-ready Joomla Module built for seamless use in JCB.

### Used in [Joomla Component Builder](https://www.joomlacomponentbuilder.com) - [Source](https://git.vdm.dev/joomla/Component-Builder) - [Mirror](https://github.com/vdm-io/Joomla-Component-Builder) - [Download](https://git.vdm.dev/joomla/pkg-component-builder/releases)

---
[![Joomla Volunteer Portal](https://img.shields.io/badge/-Joomla-gold?logo=joomla)](https://volunteers.joomla.org/joomlers/1396-llewellyn-van-der-merwe "Join Llewellyn on the Joomla Volunteer Portal: Shaping the Future Together!") [![GitHub](https://img.shields.io/badge/-Git-181717?logo=git)](https://github.com/joomengine "Build premium Joomla extensions with JoomEngine on GitHub: Help us raise Joomla extension standards!") [![Octoleo](https://img.shields.io/badge/-Octoleo-black?logo=linux)](https://git.vdm.dev/octoleo "--quiet") [![Llewellyn](https://img.shields.io/badge/-Llewellyn-ffffff?logo=gitea)](https://git.vdm.dev/Llewellyn "Collaborate and Innovate with Llewellyn on Git: Building a Better Code Future!") [![Telegram](https://img.shields.io/badge/-Telegram-blue?logo=telegram)](https://t.me/Joomla_component_builder "Join Llewellyn and the Community on Telegram: Building Joomla Components Together!") [![Mastodon](https://img.shields.io/badge/-Mastodon-9e9eec?logo=mastodon)](https://joomla.social/@llewellyn "Connect and Engage with Llewellyn on Joomla Social: Empowering Communities, One Post at a Time!") [![X (Twitter)](https://img.shields.io/badge/-X-black?logo=x)](https://x.com/llewellynvdm "Join the Conversation with Llewellyn on X: Where Ideas Take Flight!") [![GitHub](https://img.shields.io/badge/-GitHub-181717?logo=github)](https://github.com/Llewellynvdm "Build, Innovate, and Thrive with Llewellyn on GitHub: Turning Ideas into Impact!") [![YouTube](https://img.shields.io/badge/-YouTube-ff0000?logo=youtube)](https://www.youtube.com/@OctoYou "Explore, Learn, and Create with Llewellyn on YouTube: Your Gateway to Inspiration!") [![n8n](https://img.shields.io/badge/-n8n-black?logo=n8n)](https://n8n.io/creators/octoleo "Effortless Automation and Impactful Workflows with Llewellyn on n8n!") [![Docker Hub](https://img.shields.io/badge/-Docker-grey?logo=docker)](https://hub.docker.com/r/octoleo/joomengine "JoomEngine on Docker: Containerize Your Creativity!") [![Open Collective](https://img.shields.io/badge/-Donate-green?logo=opencollective)](https://opencollective.com/joomla-component-builder "Donate towards JCB: Help Llewellyn financially so he can continue developing this great tool!") [![GPG Key](https://img.shields.io/badge/-GPG-blue?logo=gnupg)](https://git.vdm.dev/Llewellyn/gpg "Unlock Trust and Security with Llewellyn's GPG Key: Your Gateway to Verified Connections!")