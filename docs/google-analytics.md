# Google Analytics Setup

Enable Google Analytics 4 (GA4) by adding your Measurement ID to the site's `hugo.toml`. No theme files need to be modified.

## How It Works

* The theme's `head.html` calls Hugo's `google_analytics.html` partial on every page in production builds.
* Hugo 0.146+ provides `google_analytics.html` as a built-in partial. It reads the `googleAnalytics` configuration and generates the official GA4 `gtag.js` snippet.
* If no Measurement ID is configured, no analytics code is generated.

## Setup

Add the following to the **site's** `hugo.toml` in the site root, not the theme:

```toml
googleAnalytics = "G-XXXXXXXXXX"
```

This is the only change required.

## Relevant Files

| File                    | Location                              | Role                                                                                           |
| ----------------------- | ------------------------------------- | ---------------------------------------------------------------------------------------------- |
| `hugo.toml`             | Site root                             | Defines the `googleAnalytics` Measurement ID.                                                  |
| `head.html`             | `<theme>/layouts/_partials/head.html` | Includes the analytics partial in every page's `<head>` during production builds. Do not edit. |
| `google_analytics.html` | Built into Hugo 0.146+                | Generates the GA4 tracking snippet. Do not create it.                                          |

## Notes

* Analytics is included only in production builds (`hugo` or `hugo --minify`). `hugo server` does not include it.
* To verify the setup, run `hugo`, open a generated page, and check the HTML source for `googletagmanager.com/gtag/js?id=G-…`.
* The Measurement ID is intended to be publicly visible in the page source. Do not expose the Measurement Protocol API secret.
* For custom tracking or consent management, create `layouts/_partials/google_analytics.html` in the site. This overrides Hugo's built-in partial.



