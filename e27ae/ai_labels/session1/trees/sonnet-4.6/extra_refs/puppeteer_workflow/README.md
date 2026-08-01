# Puppeteer-driven Google Android OAuth token collection

This supplementary bundle is extracted from the normalized Sonnet-renamed
JSCeal pickle. It is not part of the original 40 split jobs or the
142-root LLM naming assessment.

## Why the bundle is curated

The direct-call graph alone is incomplete. Important edges use object-property
dispatch rather than direct function symbols, including `browser.launch()`,
`api.google.getCookies.query()`, `api.google.getPasswords.query()`, and
`api.google.saveOAuthToken.mutate()`. The numbered files preserve those
bridges explicitly.

## Recovered chain

`saveAndroidTokens` -> enumerate installed browser objects -> resolve executable
and launch options -> puppeteer-extra launch with stealth plugins -> obtain
recovered Google cookies -> create isolated browser contexts -> replay cookies ->
open Google's Android OAuth flow -> enumerate accounts -> retrieve recovered
passwords -> automate sign-in -> read `user_id` and `oauth_token` cookies ->
save the token with scope `ANDROID`.

## Files

- `00_entrypoint_and_targets.txt` — procedure registration and browser targets.
- `01_browser_discovery_and_launch.txt` — installed-browser discovery and the full launch bridge.
- `02_google_oauth_workflow.txt` — cookie replay, Google UI automation, password trials, and token saving.
- `03_workflow_helpers.txt` — navigation, DOM, cookie-normalization, and delay helpers needed to read the workflow.
- `direct_calls_only/` — View8's direct-call tree from the workflow root; useful but not complete by itself.
- `manifest.json` — exact function inventory and extraction parameters.

Bundled Puppeteer, puppeteer-extra, stealth-plugin, and ghost-cursor bodies are
omitted because they are third-party dependency code and would add many megabytes.
Their invocation sites remain visible.

## Function guide

### `00_entrypoint_and_targets.txt`

- `func_initializeBrowserRouter_0x10000b83a` — Registers the browser router, including the saveAndroidTokens procedure that invokes the Puppeteer workflow.
- `func_initializeBrowserConfig_0x10000a9ad` — Defines supported Chromium-family browsers, executable names, user-data paths, launch options, and browser-specific configuration.

### `01_browser_discovery_and_launch.txt`

- `func_initBrowsersModule_0x10000b77e` — Exports browser enumeration and lookup helpers.
- `func_initBrowserModule_0x10000b766` — Wires browser configuration to installed-browser discovery.
- `func_generateServiceKeys_0x10000b754` — Creates browser objects from configured browser definitions.
- `func_listApplicationInstallations_0x10000b756` — Enumerates installed browser applications.
- `func_createApplicationConfig_0x10000b758` — Builds one browser object for a selected application and user.
- `func_findApplicationInstallLocation_0x10000b75d` — Resolves a browser installation directory.
- `func_initBrowserProfileModule_0x10000b751` — Defines the browser object and its launch method.
- `func_appConfigConstructor_0x10000b74a` — Stores browser executable, profile, keys, options, and extension metadata.
- `func_getExecutablePath_0x10000b750` — Combines the installation path with the browser executable name.
- `func_launchBrowser_0x10000b74e` — Browser-object launch method: forwards executablePath and launchOptions to the Puppeteer launcher.
- `func_initBrowserLaunchModule_0x10000b741` — Registers core and stealth puppeteer-extra plugins.
- `func_launchBrowser_0x10000b73b` — Merges launch options, forces headless=shell, and calls Puppeteer launch().

### `02_google_oauth_workflow.txt`

- `func_processBrowserCookies_0x1000006d5` — Enumerates installed browsers, obtains recovered Google cookies, launches each browser, and closes it after processing.
- `func_processBrowserContexts_0x1000006d8` — Creates an isolated browser context per recovered cookie set.
- `func_processGoogleAccounts_0x1000006df` — Replays cookies, opens Google OAuth, enumerates accounts, retrieves candidate passwords, and processes each account.
- `func_openGoogleAuthPage_0x1000006a8` — Opens Google's Android OAuth endpoint and creates a cursor for interaction.
- `func_getEmailElements_0x1000006ab` — Reads account identifiers from div[data-email] elements.
- `func_selectAccountAndAuthenticate_0x1000006e2` — Selects an account, authenticates it, and saves the Android OAuth token.
- `func_authenticateRequest_0x1000006b1` — Tries recovered passwords and reads user_id and oauth_token cookies.
- `func_tryPasswords_0x1000006c3` — Submits candidate passwords and detects successful authentication.
- `func_handlePasswordChallenge_0x1000006c7` — Navigates to Google's password challenge.
- `func_handleSignInChallenge_0x1000006ce` — Handles alternative Google sign-in challenge pages.
- `func_handleSignInNavigation_0x1000006bb` — Drives the initial Google sign-in navigation state machine.
- `func_clickConsentButton_0x1000006d1` — Chooses one of Google's consent buttons.
- `func_clickElementBySelector_0x10000069d` — Waits for an element and clicks it through the cursor helper.
- `func_typeWithDelay_0x100000698` — Types with delays before, during, and after input.
- `func_waitForNavigation_0x100000695` — Waits recursively until an expected Google path is reached.
- `func_normalizeCookies_0x100000691` — Converts recovered cookies to Puppeteer cookie objects.
- `func_isOauthToken_0x1000006b0` — Matches the oauth_token cookie.
- `func_isUserId_0x1000006af` — Matches the user_id cookie.

### `03_workflow_helpers.txt`

- `func_normalizeSameSite_0x1000006a3` — Converts stored SameSite values to Puppeteer spelling.
- `func_getInnerText_0x1000006aa` — Reads an element's innerText property.
- `func_getPropertyJsonValue_0x10000069f` — Resolves a Puppeteer JSHandle property to its JSON value.
- `func_defaultValue_0x1000006ae` — Combines missing-token checks.
- `func_isNotAllowed_0x1000006cd` — Prevents repeated sign-in challenge states.
- `func_isNotIncluded_0x1000006ba` — Prevents repeated initial sign-in states.
- `func_conditionalSelect_0x10000069b` — Controls whether a missing element is fatal.
- `func_selectIfFalsy_0x10000069c` — Falls back from an indexed element to the first matched element.
- `func_extractPathname_0x1000006a1` — Extracts the lower-cased current page pathname.
- `func_findFirstMatch_0x1000006a5` — Finds the expected path fragment matching the current page.
- `func_scheduleTimeoutPromise_0x1000004c9` — Implements the workflow's explicit delays as a Promise.
- `func_scheduleTimeout_0x1000004c8` — Calls setTimeout for the requested delay.
