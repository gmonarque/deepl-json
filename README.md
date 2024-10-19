<h1 align="center">
	<img
		width="300"
		alt="go-json-translate"
		src="images/go-json-translate-logo.svg">
</h1>

<h3 align="center">
	Translate json language files / i18n locales on the spot!
</h3>
<p align="center">
This tool was made to easily translate json translations files. Front-end frameworks and CMS  don't always provide a lot of translations, or any translations in some cases. This is totally understandable, but it's a major problem when you need to translate a 1000+ lines json language file. This tool can do that!
</p>
<p align="center">
	
[![GitHub issues](https://img.shields.io/github/issues/gmonarque/go-json-translate)](https://github.com/gmonarque/go-json-translate/issues)
[![GitHub license](https://img.shields.io/github/license/gmonarque/go-json-translate)](https://github.com/gmonarque/go-json-translate/blob/main/LICENSE)

<strong>
	<a href="https://gmsec.fr/">Personnal website</a>
</strong>
</p>
<p align="center">
</p>

## Example (![United Kingdom](https://raw.githubusercontent.com/stevenrskelton/flag-icon/master/png/16/country-4x3/gb.png)  -> ![France](https://raw.githubusercontent.com/stevenrskelton/flag-icon/master/png/16/country-4x3/fr.png))
English language file (BigCommerce)
```json
{
	"account": {
		"breadcrumb": "Your Account",
		"nav": {
			"overview": "Overview",
			"orders": "Orders",
			"returns": "Returns",
			"messages": "Messages ({num_new_messages})",
			"wishlists": "Wish Lists ({num_wishlists})",
			"recently_viewed": "Recently Viewed",
			"settings": "Account Settings",
			"addresses": "Addresses",
			"payment_methods": "Payment Methods"
		},
		"mobile_nav": {
			"messages": "Messages",
			"wishlists": "Wish Lists"
		}
	}
}
```
French translation generated with go-json-translate
```json
{
	"account": {
		"breadcrumb": "Votre compte",
		"nav": {
			"overview": "Vue d'ensemble",
			"orders": "Commandes",
			"returns": "Renvoyer à",
			"messages": "Messages ({num_new_messages})",
			"wishlists": "Listes de souhaits ({num_wishlists})",
			"recently_viewed": "Récemment consultés",
			"addresses": "Adresses",
			"settings": "Paramètres du compte",
			"payment_methods": "Méthodes de paiement"
		},
		"mobile_nav": {
			"messages": "Messages",
			"wishlists": "Listes de souhaits"
		}
	}
}
```

## Features

- Translate **any** standard json file on the spot, leveraging deepL's free API.
- Works well with json files containing **strings, numbers and booleans**
- Supports **nested json files**, without any limit
- Uses a local database as a **translations cache** in order to increase speed and not to request twice the same translations from deepL. This means that once you've translated a file, you can translate it again with the same parameters and not query deepL at all.
- Supports **variables** in the translated text. For example, `hello, {name}` won't be translated to `bonjour, {prénom}` but to `bonjour, {name}`
Available enclosure tags are: `{}, #{} and []`. It's very easy to add new ones.


#### This tool uses [DeepL free API](https://www.deepl.com/pro#developer). Their free plan includes:

-   Access to all features
-   Access to the DeepL REST API
-   500,000 character limit / month
-   1,000 glossaries (for specific languages)
    
> On average, text contains **between 5 and 6.5 characters per word** including spaces and punctuation. -charactercounter.com

Ok, so 500,000 / 6.5 = 76923. We could estimate that we can translate 70k words / month with the free tier. I've actually never hit the limit myself, so kudos to DeepL for a developer plan that actually lets you do stuff :)

## Limitations
- This tool depends on DeepL keeping their free tier API usage limit high
- There is no support yet for json arrays, the only supported types are strings, numbers and booleans
- The json source file is entirely read before translation. This means that if you have a **really** huge file to translate, there may be some instability depending on your hardware. But don't worry, thanks to the local translation cache, everything translated with DeepL won't be translated twice.
- The translated json file won't be in the order of the source file. This is not a problem at all, but just so you know.
## Available Languages

### Source Languages
BG, CS, DA, DE, EL, EN, ES, ET, FI, FR, HU, ID, IT, JA, KO, LT, LV, NB, NL, PL, PT, RO, RU, SK, SL, SV, TR, UK, ZH

### Target Languages
AR, BG, CS, DA, DE, EL, EN-GB, EN-US, ES, ET, FI, FR, HU, ID, IT, JA, KO, LT, LV, NB, NL, PL, PT-BR, PT-PT, RO, RU, SK, SL, SV, TR, UK, ZH, ZH-HANS, ZH-HANT

Note: Not all source languages can be used as target languages. The target languages list includes some specific variants (e.g., EN-GB, EN-US, PT-BR, PT-PT, ZH-HANS, ZH-HANT) that are not available as source languages.

For the most up-to-date list of available languages, please refer to [DeepL's API documentation](https://www.deepl.com/docs-api/translating-text/request/).

## Installation and Usage

### Install from Sources
```sh
git clone https://github.com/gmonarque/go-json-translate
cd go-json-translate && go mod download && go build
```

### Configuration
Before using go-json-translate, you need to configure the `config.ini` file:

```ini
DEEPL_API_ENDPOINT = https://api-free.deepl.com/v2/translate
DEEPL_API_KEY = <your_api_key>
```

### Usage
```sh
Usage: ./go-json-translate -source_path=<path> -output_path=<path> -source_lang=<lang> -target_lang=<lang> [-ignored_fields=<fields>]

Options:
  -source_path string
        Path of the source .json file(s)
  -output_path string
        Path for the output file(s)
  -source_lang string
        Current language of the file. Use "autodetect" to let DeepL guess the language. (default "autodetect")
  -target_lang string
        Language the file will be translated to
  -ignored_fields string
        Ignored fields separated by semicolon (optional)

Example:
  ./go-json-translate -source_path=folder/*.json -output_path=output/*.json -source_lang=fr -target_lang=en
```
### Contribute & issues
Don't hesitate to contribute to this project in any way you want. Just use gofmt and feel my vibe.
If you have any issues with this, please open an issue, I'll happily respond.


**If you have translated something and you think it could be useful to somebody else, please do a merge request of your translated file (check the `community-translated-files` folder)**
