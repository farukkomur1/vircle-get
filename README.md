# Get Vircle

The install page for Vircle's organic social channels.

It exists because every automatic path from a social bio to the App Store fails
inside Instagram's in-app browser. Instagram renders links in a webview that
refuses to hand off to another app, so the chain

    onelink -> apps.apple.com -> itms-appss://

never completes. Apple's own server does answer an Instagram user agent with a
redirect to `itms-appss://`, so the destination is correct; the webview is what
blocks it. AppsFlyer's own remedy, a Social App Landing Page, is configured on
the OneLink template and never renders: every URL variant returns a 301 with a
zero-length body, and its documented purpose is opening the app for users who
already have it, not instructing new ones.

So this page does two things and nothing else:

1. Tells a visitor inside an in-app browser to open it in their real browser.
2. Gives them one button to tap once they have.

A button press is a user gesture, which is the thing in-app browsers allow and
automatic redirects are denied.

## Rules for editing

- No script may intercept a click, rewrite an href at click time, or navigate.
  That is exactly what broke the previous Wix-hosted attempt: the framework
  cancelled the link and performed the navigation itself, so the tap never
  reached the OS as a link activation. The only script here sets a class name
  and an href on load.
- The button href must stay a bare OneLink URL. The template has Secure
  Shortlinks on, and appending a parameter silently drops attribution for that
  click.

## Links

Served at `get.vircle.ai`, via a CNAME to `farukkomur1.github.io` in the
vircle.ai zone, which Wix hosts. The `CNAME` file in this repo is what tells
Pages to answer on that hostname; deleting it takes the custom domain down.

Tag the bio per platform so installs can be attributed:

    https://get.vircle.ai/?src=ig
    https://get.vircle.ai/?src=tt
    https://get.vircle.ai/?src=yt

`src` is mapped to the OneLink `pid` on load (instagram / tiktok / youtube).
