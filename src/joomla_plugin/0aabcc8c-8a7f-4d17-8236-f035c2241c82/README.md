### JCB! Joomla Plugin
# EnglishFilter (v1.0.4)
## Englishfilter

This Plugin validate message as English language

 Block non-ASCII (23 Oct 2025 allow common English smart quotes/dashes whitelists the curly punctuation characters used by Word/Outlook.)
 Block links
 Block emails in message
 Block banned words
 Detect non-English message

Logs to message not sent if set

### Plugin Settings
| Setting                 | Value         |
|-------------------------|---------------|
| Add Custom Class Header | ![yes](https://img.shields.io/badge/yes-success?style=flat-square) |
| Add README              | ![no](https://img.shields.io/badge/no-blue?style=flat-square)  |

## Class Header:
```php
require_once JPATH_ROOT . '/vendor/autoload.php';
use Joomla\CMS\Plugin\CMSPlugin;
use Joomla\CMS\Factory;
use Joomla\CMS\Log\Log;
use LanguageDetection\Language;
```

## Properties & Methods:
```php
 /**
	 * Server-side validation for contact form
	 */
	public function onValidateContact(&$contact, &$data)
	{
		$app = Factory::getApplication();
		$ld  = new Language();

		if (!isset($data)) {
			return true;
		}

		$message = '';
		if (is_array($data)) {
			$message = $data['contact_message'] ?? $data['message'] ?? '';
		} elseif (is_object($data)) {
			$message = $data->contact_message ?? $data->message ?? '';
		}

		$message = trim((string) $message);
		if ($message === '') {
			return true;
		}

		$allowNonLatin = (bool) $this->params->get('allow_non_latin', 0);

		$plugin = $this;
		$redirectBack = function ($msg, $reason) use ($app, $data, $contact, $plugin) {
			$app->enqueueMessage($msg, 'warning');
			$plugin->logBlocked($data['contact_message'] ?? '', $reason, $data);
			$app->setUserState('com_contact.contact.data', $data);
			$app->getSession()->set('com_contact.contact.error', $msg);

			$url = \Joomla\CMS\Router\Route::_('index.php?option=com_contact&view=contact&id=' . (int) $contact->id, false);
			$app->redirect($url);
			return false;
		};

		// 1️⃣ Block non-ASCII characters (if not allowed) 
               // 23 Oct 2025 allow common English smart quotes/dashes whitelists the curly punctuation characters used by Word/Outlook.
		if (    !$allowNonLatin &&    preg_match('/[^\x00-\x7F\u2013\u2014\u2018\u2019\u201C\u201D]/u', $message)) {
			 return $redirectBack('Please write your message in English (ASCII or standard punctuation only).', 'non-latin');
		}


		// 2️⃣ Block links
		if (preg_match('/https?:\/\/[^\s]+|www\.[^\s]+/i', $message)) {
			return $redirectBack('Messages containing links are not allowed.', 'contains-link');
		}

		// 3️⃣ Block email addresses
		if (preg_match('/[a-z0-9._%+-]+@[a-z0-9.-]+\.[a-z]{2,}/i', $message)) {
			return $redirectBack('Please remove any email addresses before submitting.', 'contains-email');
		}

		// 4️⃣ Block banned words
		$bannedWords = (string) $this->params->get('banned_words', '');
		$bannedList  = array_filter(array_map('trim', explode("\n", $bannedWords)));

		foreach ($bannedList as $word) {
			if ($word && stripos($message, $word) !== false) {
				return $redirectBack('Your message contains blocked content and cannot be sent.', "banned: $word");
			}
		}

		// 5️⃣ Detect non-English message
		if (class_exists('LanguageDetection\Language')) {
			$detected = $ld->detect($message)->bestResults()->close();
			$language = key($detected);

			if ($language !== 'en') {
				return $redirectBack('Please write your message in English.', 'non-english: ' . $language);
			}
		}

		return true;
	}

	/**
	 * Log blocked messages with extra info
	 */
	protected function logBlocked($message, $reason, $data = [])
	{
		$enableLogging = (bool) $this->params->get('enable_logging', 1);
		if (!$enableLogging) {
			return;
		}

		Log::addLogger(
			[
				'text_file'  => 'non_english_attempts.log',
				'extension'  => 'plg_englishfilter',
			],
			Log::ALL,
			['contactfilter']
		);

		$ip   = $_SERVER['REMOTE_ADDR'] ?? 'unknown';
		$time = date('Y-m-d H:i:s');

		// Extract name and email safely
		$name  = '';
		$email = '';

		if (is_array($data)) {
			$name  = $data['contact_name']  ?? $data['name']  ?? '';
			$email = $data['contact_email'] ?? $data['email'] ?? '';
		} elseif (is_object($data)) {
			$name  = $data->contact_name  ?? $data->name  ?? '';
			$email = $data->contact_email ?? $data->email ?? '';
		}

		$name  = trim((string) $name) ?: 'unknown';
		$email = trim((string) $email) ?: 'unknown';
		$flatMessage = str_replace(["\r", "\n"], ' ', $message);

		// Build the log entry
		$entry = sprintf(
			'[%s] IP=%s NAME=%s EMAIL=%s REASON=%s MESSAGE=%s',
			$time,
			$ip,
			$name,
			$email,
			$reason,
			$flatMessage
		);

		Log::add($entry, Log::INFO, 'contactfilter');
	}
```

> Extend Joomla's behaviour at key events with this customizable Plugin that integrates cleanly into your JCB-built components.

### Used in [Joomla Component Builder](https://www.joomlacomponentbuilder.com) - [Source](https://git.vdm.dev/joomla/Component-Builder) - [Mirror](https://github.com/vdm-io/Joomla-Component-Builder) - [Download](https://git.vdm.dev/joomla/pkg-component-builder/releases)

---
[![Joomla Volunteer Portal](https://img.shields.io/badge/-Joomla-gold?logo=joomla)](https://volunteers.joomla.org/joomlers/1396-llewellyn-van-der-merwe "Join Llewellyn on the Joomla Volunteer Portal: Shaping the Future Together!") [![GitHub](https://img.shields.io/badge/-Git-181717?logo=git)](https://github.com/joomengine "Build premium Joomla extensions with JoomEngine on GitHub: Help us raise Joomla extension standards!") [![Octoleo](https://img.shields.io/badge/-Octoleo-black?logo=linux)](https://git.vdm.dev/octoleo "--quiet") [![Llewellyn](https://img.shields.io/badge/-Llewellyn-ffffff?logo=gitea)](https://git.vdm.dev/Llewellyn "Collaborate and Innovate with Llewellyn on Git: Building a Better Code Future!") [![Telegram](https://img.shields.io/badge/-Telegram-blue?logo=telegram)](https://t.me/Joomla_component_builder "Join Llewellyn and the Community on Telegram: Building Joomla Components Together!") [![Mastodon](https://img.shields.io/badge/-Mastodon-9e9eec?logo=mastodon)](https://joomla.social/@llewellyn "Connect and Engage with Llewellyn on Joomla Social: Empowering Communities, One Post at a Time!") [![X (Twitter)](https://img.shields.io/badge/-X-black?logo=x)](https://x.com/llewellynvdm "Join the Conversation with Llewellyn on X: Where Ideas Take Flight!") [![GitHub](https://img.shields.io/badge/-GitHub-181717?logo=github)](https://github.com/Llewellynvdm "Build, Innovate, and Thrive with Llewellyn on GitHub: Turning Ideas into Impact!") [![YouTube](https://img.shields.io/badge/-YouTube-ff0000?logo=youtube)](https://www.youtube.com/@OctoYou "Explore, Learn, and Create with Llewellyn on YouTube: Your Gateway to Inspiration!") [![n8n](https://img.shields.io/badge/-n8n-black?logo=n8n)](https://n8n.io/creators/octoleo "Effortless Automation and Impactful Workflows with Llewellyn on n8n!") [![Docker Hub](https://img.shields.io/badge/-Docker-grey?logo=docker)](https://hub.docker.com/r/octoleo/joomengine "JoomEngine on Docker: Containerize Your Creativity!") [![Open Collective](https://img.shields.io/badge/-Donate-green?logo=opencollective)](https://opencollective.com/joomla-component-builder "Donate towards JCB: Help Llewellyn financially so he can continue developing this great tool!") [![GPG Key](https://img.shields.io/badge/-GPG-blue?logo=gnupg)](https://git.vdm.dev/Llewellyn/gpg "Unlock Trust and Security with Llewellyn's GPG Key: Your Gateway to Verified Connections!")