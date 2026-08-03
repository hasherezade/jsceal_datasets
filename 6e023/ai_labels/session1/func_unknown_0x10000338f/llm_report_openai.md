# Basic

Input: deobfuscated file, relabeled in the basic mode, func: `func_proxy_0x10000338f`

Commandline used:
```
$ ~/jsc_deobfuscator/deobf_ai.py --inp ai_deobf/6e023b9b3097a2dba311cb06a91fe259.basic_openai.pkl --func func_proxy_0x10000338f
```

## Suggested name

`initProxyModule`

## Summary

This function initializes a proxy module for what appears to be a cryptocurrency trading/exchange aggregator application. It sets up configuration, telemetry, networking, routing, registers multiple cryptocurrency exchange integrations, reads proxy settings, and defines a script module with a lifecycle chain (`initchain`/`entrychain`) and associated handler functions.

## Inputs

No explicit parameters. The function reads from several globals and module exports:

- `global_io["proxy"]` — proxy configuration object (source uncertain; likely loaded config)
- Various module exports via `func_unknown_0x100001319`, `func_unknown_0x1000012e5`, `func_unknown_0x1000032dd` — unknown module identities, wrapped through `func_Interop_0x100000907`
- `func_createScript_0x100000242` — a script/plugin registration mechanism
- `r1` — implicit accumulator/receiver context (V8 artifact; likely `undefined` or `this`)

## Return value

Always returns `undefined` explicitly.

## Side effects and external interactions

- **Global state mutations:**
  - `global_sa` — set to interop-wrapped result of `func_unknown_0x100001319`
  - `global_J1` — set to interop-wrapped result of `func_unknown_0x1000012e5`
  - `global_wA` — set to interop-wrapped result of `func_unknown_0x1000032dd`
  - `global_j1` — set to `proxy.updateInterval`
  - `global_lM` — set to proxy config object minus `updateInterval`
  - `global_K1` — set to `proxy.listen.certificates.root.value` (likely a root CA certificate value)
  - `global_Ea` — set to the `setAvailable` function of the registered script

- **Initialization side effects:**
  - Calls `func_Config_0x10000091a()` — loads/initializes configuration
  - Calls `func_telemetryInit_0x1000026eb()` — initializes telemetry
  - Calls `func_Empty_0x100003148()` — unknown initialization (name suggests no-op or placeholder)
  - Calls `func_initNet_0x10000314b()` — initializes networking
  - Calls `func_initRouter_0x1000032e1()` — initializes routing
  - Registers exchange integrations: Binance, BingX, Bitget, Bitrue, Bitstamp, Bybit, DigiFinex, Gate.io, KuCoin, MEXC, an unknown exchange, and Poloniex
  - Registers a script with ID `71940abe-d66b-443a-9db0-d91d403cf95b` via `func_createScript_0x100000242`
  - Marks `"listen"` and `"set"` as unavailable (`setAvailable(..., false)`) on the registered script

## Step-by-step logic

1. Initialize `r4 = 0` (likely a local counter or flag, unused further).
2. Call `func_Config_0x10000091a()` — load global configuration.
3. Load module export from `func_unknown_0x100001319`, wrap with `func_Interop_0x100000907`, store in `global_sa`.
4. Call `func_telemetryInit_0x1000026eb()` — initialize telemetry subsystem.
5. Load module export from `func_unknown_0x1000012e5`, wrap with interop, store in `global_J1`.
6. Call `func_Empty_0x100003148()` — unknown/placeholder initialization.
7. Call `func_initNet_0x10000314b()` — initialize network layer.
8. Load module export from `func_unknown_0x1000032dd`, wrap with interop, store in `global_wA`.
9. Call `func_initRouter_0x1000032e1()` — initialize router.
10. Call initialization functions for 12 cryptocurrency exchanges (Binance, BingX, Bitget, Bitrue, Bitstamp, Bybit, DigiFinex, Gate.io, KuCoin, MEXC, unknown, Poloniex).
11. Read `global_io["proxy"]` into `r7`.
12. Extract `r7["updateInterval"]` → `global_j1`.
13. Copy remaining proxy properties (excluding `updateInterval`) → `global_lM`.
14. Extract `global_lM["listen"]["certificates"]["root"]["value"]` → `global_K1` (root certificate value).
15. Construct a script descriptor object with:
    - `id`: `"71940abe-d66b-443a-9db0-d91d403cf95b"`
    - `name`: `"Proxy"`
    - `version`: `"1.0.0"`
    - `initchain`: `["unset"]`
    - `entrychain`: `["install", "listen", "set"]`
    - `functions`: `{ install: func_y6, listen: func_E6, set: func_b6, unset: func_B6 }`
16. Register the script via `func_createScript_0x100000242(r10)`, store `setAvailable` from result in `global_Ea`.
17. Call `global_Ea("listen", false)` — mark `"listen"` function as unavailable initially.
18. Call `global_Ea("set", false)` — mark `"set"` function as unavailable initially.
19. Return `undefined`.

## Cleaned pseudocode

```js
function initProxyModule():
    // Phase 1: Core initialization
    func_Config()
    global_sa = Interop(func_unknown_module_1.exports())
    func_telemetryInit()
    global_J1 = Interop(func_unknown_module_2.exports())
    func_Empty()                    // unknown/placeholder
    func_initNet()
    global_wA = Interop(func_unknown_module_3.exports())
    func_initRouter()

    // Phase 2: Exchange integrations
    func_binance()
    func_bingx()
    func_bitget()
    func_bitrue()
    func_bitstamp()
    func_bybit()
    func_digifinex()
    func_gateio()
    func_kucoin()
    func_mexc()
    func_unknown_exchange()
    func_poloniex()

    // Phase 3: Proxy config extraction
    proxyConfig = global_io["proxy"]
    global_j1 = proxyConfig["updateInterval"]
    global_lM = copyPropertiesExcluding(proxyConfig, "updateInterval")
    global_K1 = global_lM["listen"]["certificates"]["root"]["value"]

    // Phase 4: Script registration
    scriptDescriptor = {
        id:         "71940abe-d66b-443a-9db0-d91d403cf95b",
        name:       "Proxy",
        version:    "1.0.0",
        initchain:  ["unset"],
        entrychain: ["install", "listen", "set"],
        functions: {
            install: func_y6,
            listen:  func_E6,
            set:     func_b6,
            unset:   func_B6
        }
    }
    script = func_createScript(scriptDescriptor)
    global_Ea = script["setAvailable"]

    // Mark listen and set as initially unavailable
    global_Ea("listen", false)
    global_Ea("set", false)

    return undefined
```

## Evidence and uncertainties

**Supporting evidence:**
- Exchange function names (`func_binance_*`, `func_bingx_*`, etc.) strongly indicate a multi-exchange trading platform proxy.
- The script descriptor fields (`id`, `name`, `version`, `initchain`, `entrychain`, `functions`) suggest a plugin/script lifecycle framework.
- `"listen"` and `"set"` being marked `false` via `setAvailable` indicates these are gated behind a prerequisite (`"install"` completing first).
- `global_io["proxy"]` path suggests an externally loaded IO/config object.
- The certificate path `listen.certificates.root.value` suggests TLS termination configuration for the proxy's listener.

**Unresolved:**
- Identity of `func_unknown_0x100001319`, `func_unknown_0x1000012e5`, `func_unknown_0x1000032dd` — their module types are unknown.
- Purpose of `func_Empty_0x100003148` — the name suggests a no-op but could be a placeholder with side effects.
- What `func_unknown_0x100003378` registers (the unnamed exchange).
- The exact semantics of `func_createScript_0x100000242` — inferred as a plugin/script registry.
- Whether `r4 = 0` is meaningful (likely a dead assignment or V8 register artifact).
- The relationship between `global_io` and the configuration loaded by `func_Config`.
