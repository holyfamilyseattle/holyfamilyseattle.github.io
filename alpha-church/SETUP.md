# Setup Instructions

## Get the theme

If you have `git` installed, you can do the following at the command-line-interface within the Hugo directory:

```
$ mkdir themes
$ cd themes
$ git submodule add https://github.com/funkydan2/alpha-church.git
```

You should see a folder called `alpha-church` inside the `themes` directory that we created a few moments ago. For more information read the official [setup guide](//gohugo.io/overview/installing/) of Hugo.

## Update the theme
  If the theme has been updated, you can use `git` to merge latest commits to the submodule by running `git submodule update --rebase --remote` in root directory of your project.

## Configuration

In the next step navigate to the `exampleSite` folder at `themes/alpha-church/exampleSite/` and copy `config.toml` from the exampleSite folder into the root folder of your Hugo site. Then delete the line which says `themesDir = "../.."`.

(Please refer to https://gohugo.io/overview/quickstart/ for installing a Hugo theme.)

## The `config` file

Now, let us take a look at `config.toml`. Let's take a look at some of the settings.

### 1. Custom CSS
The easiest way to change the look of your site is by overriding the included style sheet. You can do this by putting your css file in `static/css/my.css` and entering `customCSS = ["/css/my.css"]` in the config file.

### 2. Google Analytics
Enable by putting your Analytics key here.
```
GoogleAnalytics = ""
```

### 3. Menu & Nested Menus

The entries in the items menu can be customised. The structure of the menu is defined in `config.toml`.

```
[menu]
  [[menu.main]]
    name = "Home"
    url = "/"
    weight = 1
```

Define a label and enter the URL of the resource you want to link. The `weight` value determines the order of menu items. Lower weighted entries appear to the *left* of higher weighted entries.

For sub-menus, you can use the following format:

```
[[menu.main]]
  name = "About"
  url = "/about"
  weight = 2

[[menu.main]]
  name = "About Us"
  parent = "About"
  url = "/about"
  weight = 1
```
In this example, *About* is in the main menu, but *About Us* is in the *About* sub-menu. In *Alpha Church* the sub-menu is a drop-down menu.

### 4. Podcasting
In `config.toml` there are settings which are used to generate the podcast RSS feed.

```
[params.podcast]
  title = "Listen to Alpha Church"
  subtitle = ""
  summary = "Alpha-Church sermons, talks, messages—podcasted."
  email = "test@example.com"
  image = "Link to 1400*1400 (or larger) file"
  category = "Religion & Spirituality"
  sub_category = "Christianity"
  #num_episodes = 50
  #iTunesID = 12345677
```
Almost all of these need to be set or else the feed will not be valid. You can leave the `subtitle` entry blank. You don't need to set `num_episodes` unless you want your feed to include a number other than the default (50).

Some of these entries look like site-wide settings (e.g. `title`). They need to be set here as you may which to use a title for your site which is different from your podcast.

The `iTunedID` setting is used to create a subscribe banner for users of the Safari web browser on iOS. Only set this variable if your sermon podcast feed has been submitted to iTunes. [Click here to read instructions on how to find the ID number](https://www.podigee.com/en/help/how-to-find-your-podcasts-itunes-id/).

As you're developing your site, you'll need to check the podcast feed is valid by entering the feed's URL into [a podcast feed validator](https://castfeedvalidator.com).

The podcast feed is found at `/sermons/index.xml`.

### 5. Landing (Home) page
The landing page is quite customisable. It consists of five blocks: a banner, an area for information about services (including a map), featured icons, featured images, and a contact form.

Settings for the landing page are configured in the frontmatter of `/content/_index.md`. There is an example configuration in the `exampleSite` folder.

#### a. Banner
The banner section requires a background image to be set. This image should be 1800*1200 px, and a relatively simple image will probably look best. The filename of this banner is set in `config.toml`
```
[params.banner]
  image = "/img/banner.jpg"
```

You can place link buttons in this area by using the following settings.

```
[[banner.button]]
  url = "/contact"
  text = "Get in touch"
  type = "primary"
```

#### b. Service information
Below the banner is an area which could be used for highlight service location and times. The settings for the [open street map](https://openstreetmap.org) in this area are detailed below.

#### c. Feature Icons
These feature icons are pulled from [fontawesome](https://fontawesome.com). The layout requires an even number of these blocks (well, you could have an odd number, but it would look, well, odd). To find items [search around on the fontawesome site](https://fontawesome.com/icons?d=gallery)

```
[[feature_icons.tile]]
  icon = "fa-users"
  icon_pack = "fas"
  accent = "2"
  title = "Meet"
  text = "Meeting together to hear."
```
The value of the `icon` and `icon_pack` setting is found on the FontAwesome site. `Accent` is a colour scheme set in the css (there are 5 accent colours).

#### d. Feature Images
Like the *Feature Icons* this section looks best with an even number of entries.

### 6. Map
This theme makes use of [open street maps](https://openstreetmap.org) on the landing page and as a shortcode.

To set your organisations' location edit `config.toml`.
```
[params.map]
  service = "osm"
  latitude = "48.8530"
  longitude = "2.3498"
  zoom = "18"
```
To find the appropriate values, visit https://openstreetmap.org and find the location you want to be shown on your map. Then look at the URL in your browser's location bar. You'll see something like `https://www.openstreetmap.org/search?query=New%20York#map=14/40.6971/-73.9796`. The final three numbers in this URL give the values of Zoom/Latitude/Longitude.

If you'd like a map on another page, you can use an inline shortcode `{{< map.inline >}}{{ partial "map" . }}{{< /map.inline >}}`. **N.B. inline shortcodes must be [enabled in your config file](https://gohugo.io/templates/shortcode-templates/#inline-shortcodes).**

You can also use Google Maps. To do this, you'll need an [API Key from Google](https://developers.google.com/maps/documentation/embed/get-api-key) and set it in `config.toml`:
```
[params.map]
  service = "google"
  latitude = "48.8530"
  longitude = "2.3498"
  zoom = "18"
  api_key = "XXXXXXXX"
```
If you're using Google Maps there are two *optional* settings `langauge` and `region`. Without these settings, Google Maps will display in the language of the user's browser. Using these settings will force Google Maps to be displayed for the given localisation. See [here for a list of supported languages](https://developers.google.com/maps/faq#languagesupport) and [here for a list of valid regions](https://www.iso.org/obp/ui/#search).

e.g.
```
  language = "fr"
  region = "FR"
```

You can also use Mapbox. To do this you'll need an [API Key from Mapbox](https://docs.mapbox.com/help/how-mapbox-works/access-tokens/) and set it in `config.toml`. You can also define your custom map style using [Mapbox Studio](https://www.mapbox.com/mapbox-studio/).

```
[params.map]
  service = "mapbox" 
  latitude = "48.137232"
  longitude = "11.575503"
  zoom = "13"
  api_key = "XXXXXXXX"
  style_url = "mapbox://LINK_TO_MAPBOXP_STYLE"
  marker_title = "Popup Marker Title"
  marker_address= "Streetname <br> Postcode Town"
```

> If `marker_title` and `marker_address` are not set, the popup will not be rendered in the map.

### 7. Contact Form
You can have a contact form using either a [netlify form](https://www.netlify.com/docs/form-handling/) (if you're deploying with netlify) or [formspree](https://formspree.io)
```
[params.contact]
  service = ""
  confirm_page = "/contact_thanks"
  formspree_email=""
```
With these setting, set *service* to either `service = "netlify"` or `service = "formspree"`.

If you're using formspree, you'll also need to set `formspree_email` to your email address.

If you're using netlify, you'll also want to set the `confirm_page = "url"` to a page on your site. That way after a user submits the form they'll be sent to a page with your customised thank you message, rather than a generic netlify page.

If you'd like a contact form on another page, use an inline shortcode `{{< contact.inline >}}{{ partial "contact" . }}{{< /contact.inline >}}` **N.B. inline shortcodes must be [enabled in your config file](https://gohugo.io/templates/shortcode-templates/#inline-shortcodes).**

### 8. Links
At the very bottom of each page is a bunch of icons (from FontAwesome) which can be used for links to social media, RSS feeds, or whatever you like!
```
[[params.links]]
  service = "Facebook"
  icon = "fa-facebook"
  icon_pack = "fab"
  link = "//facebook.com/"

[[params.links]]
  service = "Podcast"
  icon = "fa-podcast"
  icon_pack = "fas"
  link = "/sermons/index.xml"

[[params.links]]
  service = "Full RSS Feed"
  icon = "fa-rss"
  icon_pack = "fas"
  link = "/index.xml"
```

### 8. Bible Popups
*Changed on Tuesday, 9 April 2019..*
Configuration in [params]. Set `bible_popups = "faithlife"` to include Bible reference popups from [Faithlife](https://faithlife.com/products/reftagger), or `bible_popups = "blb"` to use the [Blue Letter Bible](https://www.blueletterbible.org/webtools/BLB_ScriptTagger.cfm) popups.

You may also set the bible translation by defining `bible_version = "ESV"` (or NLT, KJV, CSB, etc.). If you don't define a translation, the default *ESV* will be used.

## Nearly finished

To preview your site, run Hugo's built-in local server.

```
$ hugo server -D
```

Now enter [`localhost:1313`](http://localhost:1313) in the address bar of your browser.

# Usage Instructions
## Image Dimensions
This theme makes use of 'hero' images for regular and sermon/podcast pages. Images need to be the right dimesions in order to display properly.

|Page Type|Width|Height|
|---|---|---|
|Sermon|768px|644px|
|Regular page|1280px|   |
|Front page feature images|618px|412px|
