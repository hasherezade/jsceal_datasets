# Quality assessment: basic-mode function renaming

## Scope

Compared the two uploaded CSVs against the complete deobfuscated function bodies for `e27ae65977287bdfb7b0e15fd3603f85`.

- Claude Sonnet 4.6: 223 proposed names
- GPT-5.4-mini: 220 proposed names
- Shared functions: 220
- Functions absent from GPT output: 3

This is a basic-mode subset dominated by initializers, routers, wrappers, and small helper functions. It is not a random sample of all functions in the payload.

## Objective naming characteristics

- Exact stem agreement: 7/220 (3.2%)
- Trivial empty functions correctly recognized by both: 24
- Exact agreement plus the empty-function cases: 31/220 (14.1%)
- Sonnet unique stems: 213/223; GPT unique stems: 163/220
- Excluding the 24 genuinely empty functions, Sonnet has 10 duplicate-name collisions; GPT has 34
- Mean semantic tokens per name: Sonnet 3.07; GPT 1.68
- One-token names: Sonnet 2; GPT 85

## Manual semantic review

- Both accurate / equivalent: 58 (26.0%)
- Both defensible; Sonnet more precise: 53 (23.8%)
- Sonnet clear win: 93 (41.7%)
- GPT clear win: 5 (2.2%)
- Both weak or uncertain: 14 (6.3%)

Interpretation:

- Sonnet supplied a defensible, useful name in 204/223 cases (91.5%).
- GPT supplied a comparably useful name in 116/223 cases (52.0%), counting its three missing entries as failures.
- In many remaining GPT cases the name is not outright false, but is too generic for navigation: `Setup`, `Configure`, `Invoke`, `Initialize`, or `Init`.
- Sonnet is substantially more useful, but it still overcommits in several places and must not be treated as ground truth.

## Strong examples

### Sonnet clear wins

- `func_JVdWv_0x100003a3e`: Sonnet `coalesce` vs GPT `Default`. Returns a0 when truthy, otherwise a1; 'coalesce' describes the behavior.
- `func_Soe_0x100000001`: Sonnet `setupWorkerRoot` vs GPT `Worker`. Checks cluster/worker-thread state and configures the worker root.
- `func_a7e_0x100000aaf`: Sonnet `queryProcedures` vs GPT `procedureInit`. Queries core procedures and creates a caller; GPT's label reverses the emphasis.
- `func_r7e_0x100000a99`: Sonnet `checkAndIncrementDiagnostics` vs GPT `monitor`. Reads diagnostics counters, compares maxFailCount, increments counters, invokes callback, then deletes the counter.
- `func_unknown_0x1000047f7`: Sonnet `initJwtVerification` vs GPT `jwtInit`. Builds a JWT verifier with RS256 and verifies the loader token.
- `func_unknown_0x100005929`: Sonnet `initPowerManagementRouter` vs GPT `systemRouter`. Builds a router with preventSleep, autoSleep, and battery-action settings.
- `func_unknown_0x100006649`: Sonnet `initCustomErrorClass` vs GPT `emptyClass`. Defines an Error subclass; it is not an empty class.
- `func_unknown_0x1000066f2`: Sonnet `initModule` vs GPT `initGraphql`. The body exposes request/query/mutation/subscription behavior from the tRPC client stack, not GraphQL.
- `func_unknown_0x10000707b`: Sonnet `initAsarScriptRoute` vs GPT `route`. Defines GET /asar/script with a schema and handler.
- `func_unknown_0x10000a969`: Sonnet `initDecompressModule` vs GPT `vmInit`. Initializes the same decompression dependency used elsewhere; 'vmInit' is unsupported.
- `func_unknown_0x10000b78c`: Sonnet `initUrlNamespaceModule` vs GPT `initWallet`. Initializes URL-related dependencies; 'initWallet' is unsupported.
- `func_unknown_0x10000b794`: Sonnet `initUrlClass` vs GPT `emptyLoad`. Calls the URL-class initializer; it is not an empty load.
- `func_unknown_0x10000b83a`: Sonnet `initBrowserModule` vs GPT `initProfiles`. Defines browser operations including saveProfiles, saveExtensions, saveAndroidTokens, and openLink.
- `func_unknown_0x10000bdc4`: Sonnet `initBalanceSessionHooks` vs GPT `initBalance`. Registers both saveBalance and saveSession hooks; GPT omits half the role.
- `func_unknown_0x10000bdca`: Sonnet `initAntivirusRedirects` vs GPT `redirectRouter`. Maps Kaspersky/Avast traffic to Bitdefender/AVG URLs and installs redirect handlers.
- `func_unknown_0x10000be07`: Sonnet `initGoogleOAuthRoutes` vs GPT `initGoogle`. Contains the Google OAuth/session replay workflow; Sonnet captures the scope.
- `func_unknown_0x10000c89d`: Sonnet `initSaveMnemonicRouter` vs GPT `initMnemonic`. Defines POST /wallets/mnemonic/save and the saveMnemonic mutation.
- `func_unknown_0x10000c8d6`: Sonnet `initWindowsTaskSchedulerPaths` vs GPT `registry`. Constructs the exact TaskCache\Tree and TaskCache\Tasks registry paths.
- `func_unknown_0x10000c8e7`: Sonnet `initTaskSchedulerRouter` vs GPT `recoveryInit`. Defines the task-scheduler start router; GPT's recovery label is wrong.
- `func_unknown_0x10000c8fe`: Sonnet `initSystemRouter` vs GPT `initAdmin`. Defines system mutations such as sleep, reboot, raiseBSOD, and exit.
- `func_unknown_0x10000d2e3`: Sonnet `initDesktopRouter` vs GPT `sessionRouter`. Exposes keyboard, screenshot, windows, control, and flash operations; 'sessionRouter' is too narrow.
- `func_unknown_0x10000d2f9`: Sonnet `initFullImpersonationRouter` vs GPT `toastRouter`. The router is explicitly mounted as full-impersonation and contains setProxy plus toast; GPT names only one route.
- `func_zO_0x10000013b`: Sonnet `createAxiosInstance` vs GPT `clientCreate`. Creates an Axios-style instance from defaults, prototype methods, and request binding.

### GPT clear wins

- `func_unknown_0x10000664f`: Sonnet `initErrorHandlers` vs GPT `statusInit`. Only initializes the error/status maps; 'statusInit' is closer than 'initErrorHandlers'.
- `func_unknown_0x100006702`: Sonnet `initMainModule` vs GPT `initRuntime`. Builds SocketLink/RequestLink and API runtime structures; GPT's 'initRuntime' is more concrete.
- `func_unknown_0x100006777`: Sonnet `initFrostModule` vs GPT `initService`. 'Frost' is not supported by visible body evidence; the body initializes a process-session service.
- `func_unknown_0x10000704d`: Sonnet `initTransformStream` vs GPT `replaceStream`. Defines a Transform subclass with _transform, _flush, and replace; 'replaceStream' is more specific.
- `func_unknown_0x10000a996`: Sonnet `initWorkerModule` vs GPT `Invoke`. The wrapped callee initializes Ledger Live app.json paths; 'initWorkerModule' is wrong. 'Invoke' is generic but non-misleading.

### Cases where neither should be trusted

- `func_unknown_0x100003ab2`: Sonnet `initModule` vs GPT `Invoke`. The body does not support either label with enough specificity.
- `func_unknown_0x10000664c`: Sonnet `initLinkModule` vs GPT `Invoke`. The body does not support either label with enough specificity.
- `func_unknown_0x100006693`: Sonnet `initRouterModule` vs GPT `Invoke`. The body does not support either label with enough specificity.
- `func_unknown_0x100006ed8`: Sonnet `initBS4Class` vs GPT `initApi`. 'BS4' is residual obfuscated text, not a semantic class name; GPT's 'initApi' is also weak.
- `func_unknown_0x100006ee0`: Sonnet `initBS4Module` vs GPT `initApi`. Same problem as the related BS4 class initializer.
- `func_unknown_0x100007067`: Sonnet `initWalletExtensions` vs GPT `ledgerInit`. Initializes Ledger Live and Trezor Suite application descriptors, not browser extensions; GPT mentions only Ledger.
- `func_unknown_0x100007071`: Sonnet `initClassDefinitions` vs GPT `defineGetter`. The body does not support either label with enough specificity.
- `func_unknown_0x10000a99e`: Sonnet `initWorkerRouter` vs GPT `automationRouter`. The start mutation iterates the exported ledger provider set; neither 'WorkerRouter' nor 'automationRouter' is precise.
- `func_unknown_0x10000b79b`: Sonnet `initMultiInitModule` vs GPT `initStoreAll`. The body does not support either label with enough specificity.
- `func_unknown_0x10000b7a0`: Sonnet `initMultiModule` vs GPT `initStore`. The body does not support either label with enough specificity.
- `func_unknown_0x10000bdd2`: Sonnet `initTokenRouter` vs GPT `routerMap`. The router is used for exchange QR-login interception; 'TokenRouter' is not directly established, while 'routerMap' is too generic.
- `func_unknown_0x10000be0e`: Sonnet `initGmRouter` vs GPT `routerMain`. 'Gm' comes from an internal global identifier; neither name establishes the router's purpose.
- `func_unknown_0x10000be19`: Sonnet `initUpRouter` vs GPT `routerPage`. 'Up' comes from an internal global identifier; neither name establishes the router's purpose.
- `func_unknown_0x10000c8c7`: Sonnet `initPathModule` vs GPT `(missing)`. The body does not support either label with enough specificity.

## Complete function-by-function review

| # | Function | Sonnet | GPT | Verdict | Evidence |
|---:|---|---|---|---|---|
| 1 | `func_AD_0x10000a92f` | `initQueue` | `Queue` | Both defensible; Sonnet more precise | maxSize, queue |
| 2 | `func_BS_0x100000522` | `setScope` | `SetValue` | Both defensible; Sonnet more precise |  |
| 3 | `func_BX_0x1000004a1` | `createProxy` | `proxyCreate` | Both accurate / equivalent | V, b48I, J |
| 4 | `func_Di_0x10000317a` | `createNamespaceObject` | `interopDefault` | Both defensible; Sonnet more precise | getPrototypeOf, create, __esModule, default, value, enumerable |
| 5 | `func_EG_0x100000559` | `initScopeWithFlag` | `Configure` | Sonnet clear win |  |
| 6 | `func_ER_0x1000034e3` | `initHandlers` | `Handlers` | Both defensible; Sonnet more precise | handlers |
| 7 | `func_GL_0x100003179` | `copyProperties` | `CopyProps` | Both accurate / equivalent | V, gm42, J, S, g, L |
| 8 | `func_I1_0x10000066f` | `initScopeThreeParams` | `Options` | Sonnet clear win |  |
| 9 | `func_JS_0x10000706e` | `initStore` | `Store` | Both defensible; Sonnet more precise | store |
| 10 | `func_JVdWv_0x100003a3e` | `coalesce` | `Default` | Sonnet clear win |  |
| 11 | `func_KB_0x10000552f` | `noop` | `Empty` | Both accurate / equivalent |  |
| 12 | `func_Lj_0x10000a8fa` | `initClientName` | `Client` | Sonnet clear win | client, name |
| 13 | `func_NV_0x10000056e` | `initScopeWithRest` | `Setup` | Sonnet clear win |  |
| 14 | `func_Op_0x1000004ce` | `getKeys` | `Keys` | Both defensible; Sonnet more precise | keys |
| 15 | `func_PV_0x10000056f` | `initWithDefaults` | `inject` | Sonnet clear win |  |
| 16 | `func_Qm_0x1000005b2` | `initScopeQueue` | `queueInit` | Both defensible; Sonnet more precise |  |
| 17 | `func_S_0x10000706c` | `initNameInject` | `Inject` | Sonnet clear win | name, inject |
| 18 | `func_Soe_0x100000001` | `setupWorkerRoot` | `Worker` | Sonnet clear win | default, isPrimary, worker_threads, isMainThread, Worker root already configured, setupPrimary |
| 19 | `func_Tj_0x1000005a1` | `repairDatabase` | `Repair` | Both defensible; Sonnet more precise | repair, destroy, open, catch, status, shift |
| 20 | `func_UAe_0x10000049e` | `createScopedProxy` | `proxyInit` | Both defensible; Sonnet more precise |  |
| 21 | `func_Vl_0x10000066a` | `extractTypePatches` | `Patch` | Sonnet clear win | type, patches |
| 22 | `func_WX_0x100000497` | `initScopeWithHandler` | `Register` | Sonnet clear win |  |
| 23 | `func_YC_0x100003a56` | `initAxiosInstance` | `configure` | Sonnet clear win | defaults, interceptors, request, response |
| 24 | `func_a7e_0x100000aaf` | `queryProcedures` | `procedureInit` | Sonnet clear win | core, procedures, query, createCallerFactory |
| 25 | `func_aB_0x10000053a` | `registerMutation` | `Mutate` | Both defensible; Sonnet more precise | procedure, input, intersection, object, shadowCopy, boolean |
| 26 | `func_aW_0x100000ab5` | `createInstance` | `Create` | Both defensible; Sonnet more precise | create |
| 27 | `func_cG_0x100000546` | `extractTypePatchesAlt` | `Patch` | Sonnet clear win | type, patches |
| 28 | `func_eS_0x100005519` | `createProxy` | `Proxy` | Both defensible; Sonnet more precise | get |
| 29 | `func_gEe_0x100000672` | `initScopeThreeParamsAlt` | `Configure` | Sonnet clear win |  |
| 30 | `func_gS_0x1000004e4` | `initScopeWithDefault` | `Setup` | Sonnet clear win |  |
| 31 | `func_kV_0x10000317b` | `createEsModuleExport` | `interopModule` | Both accurate / equivalent | __esModule, value, defineProperty |
| 32 | `func_mX_0x1000066b7` | `initRuntime` | `initialize` | Both defensible; Sonnet more precise | requestId, runtime, transformer, combinedTransformer, serialize, deserialize |
| 33 | `func_n4_0x10000000b` | `handleWorkerPool` | `Dispatch` | Sonnet clear win | worker_threads, isMainThread, workerData, poolId, initial, default |
| 34 | `func_ofe_0x10000055d` | `initScopeFourParams` | `Configure` | Sonnet clear win |  |
| 35 | `func_r7e_0x100000a99` | `checkAndIncrementDiagnostics` | `monitor` | Sonnet clear win | get, diagnostics, maxFailCount, del |
| 36 | `func_u2_0x100003170` | `defineProperties` | `Define` | Both defensible; Sonnet more precise | get, enumerable, defineProperty |
| 37 | `func_u7e_0x100000a93` | `migrateRegistry` | `Migrate` | Both defensible; Sonnet more precise | registryGetValueTyped, OldMachineGuid, SZ, core, migrate, mutate |
| 38 | `func_ub_0x100000aa3` | `incrementCounter` | `Increment` | Both defensible; Sonnet more precise | get, set |
| 39 | `func_unknown_0x10000317e` | `initCluster` | `clusterInit` | Both accurate / equivalent | cluster |
| 40 | `func_unknown_0x100003185` | `initConfig` | `Init` | Sonnet clear win | loader, diagnostics, maxFailCount, successTimeout, leveldb, location |
| 41 | `func_unknown_0x100003ab2` | `initModule` | `Invoke` | Both weak or uncertain | RylYE |
| 42 | `func_unknown_0x10000425b` | `initHttpModule` | `bootstrap` | Sonnet clear win | exports, createHTTP2Adapter, agent, force, globalAgent, create |
| 43 | `func_unknown_0x1000047f7` | `initJwtVerification` | `jwtInit` | Sonnet clear win | exports, token, loader, RS256, jwt, publicKey |
| 44 | `func_unknown_0x1000054fc` | `initMachineId` | `machineGuid` | Both defensible; Sonnet more precise | exports, path, join, HKLM, SOFTWARE, Microsoft |
| 45 | `func_unknown_0x100005504` | `initFaro` | `initFaro` | Both accurate / equivalent | exports, https://faro., /collect, initializeFaro, app, user |
| 46 | `func_unknown_0x100005506` | `defineErrorClass` | `ErrorClass` | Both defensible; Sonnet more precise |  |
| 47 | `func_unknown_0x10000550c` | `defineErrorClass` | `errorClass` | Both defensible; Sonnet more precise |  |
| 48 | `func_unknown_0x10000550f` | `initErrorCodes` | `Status` | Sonnet clear win | PARSE_ERROR, BAD_REQUEST, INTERNAL_SERVER_ERROR, NOT_IMPLEMENTED, UNAUTHORIZED, FORBIDDEN |
| 49 | `func_unknown_0x10000551a` | `initHttpErrorCodes` | `statusCodes` | Both defensible; Sonnet more precise | PARSE_ERROR, BAD_REQUEST, UNAUTHORIZED, NOT_FOUND, FORBIDDEN, METHOD_NOT_SUPPORTED |
| 50 | `func_unknown_0x100005526` | `initTrpcRuntime` | `trpcInit` | Both defensible; Sonnet more precise | V, )Ku4, J, S, B@Sb, g |
| 51 | `func_unknown_0x100005534` | `initTrpcModule` | `initialize` | Sonnet clear win | V, J, 89J2, S, g, O9*f |
| 52 | `func_unknown_0x100005537` | `initTrpcMeta` | `createMeta` | Both accurate / equivalent | meta, create |
| 53 | `func_unknown_0x100005538` | `emptyInit` | `Empty` | Both accurate / equivalent |  |
| 54 | `func_unknown_0x10000562c` | `initUtils` | `Utils` | Both defensible; Sonnet more precise | assertEqual, assertIs, assertNever, arrayToEnum, getValidEnumValues, objectValues |
| 55 | `func_unknown_0x10000562f` | `addMergeShapes` | `Merge` | Sonnet clear win | mergeShapes |
| 56 | `func_unknown_0x100005669` | `addErrorHelpers` | `Helpers` | Sonnet clear win | errToObj, toString |
| 57 | `func_unknown_0x100005901` | `initZodTypes` | `Types` | Sonnet clear win | ZodString, ZodNumber, ZodNaN, ZodBigInt, ZodBoolean, ZodDate |
| 58 | `func_unknown_0x100005929` | `initPowerManagementRouter` | `systemRouter` | Sonnet clear win | exports, object, preventSleep, autoSleep, lowBatteryAction, criticalBatteryAction |
| 59 | `func_unknown_0x100005ca8` | `initConnectClass` | `httpClient` | Both defensible; Sonnet more precise | exports, default, connect, destroy, headers, xQ)2 |
| 60 | `func_unknown_0x100005cc9` | `initWebSocketModule` | `setup` | Sonnet clear win | exports, default, 10s, 30s, open, send |
| 61 | `func_unknown_0x100005cd5` | `defineUrlClass` | `(missing)` | Sonnet clear win | target, link, match |
| 62 | `func_unknown_0x100006644` | `emptyNoop` | `Empty` | Both accurate / equivalent |  |
| 63 | `func_unknown_0x100006649` | `initCustomErrorClass` | `emptyClass` | Sonnet clear win |  |
| 64 | `func_unknown_0x10000664c` | `initLinkModule` | `Invoke` | Both weak or uncertain | CKRlN |
| 65 | `func_unknown_0x10000664f` | `initErrorHandlers` | `statusInit` | GPT clear win |  |
| 66 | `func_unknown_0x100006654` | `initErrorModule` | `init` | Sonnet clear win |  |
| 67 | `func_unknown_0x100006658` | `defineCustomError` | `ErrorClass` | Both defensible; Sonnet more precise |  |
| 68 | `func_unknown_0x100006663` | `initFromError` | `defineError` | Sonnet clear win | V, J, 89J2, S, g, [()[ |
| 69 | `func_unknown_0x100006675` | `initHttpMethodMap` | `methodInit` | Sonnet clear win | query, mutation, GET, POST |
| 70 | `func_unknown_0x10000668b` | `initErrorModule` | `initError` | Both defensible; Sonnet more precise |  |
| 71 | `func_unknown_0x100006690` | `initRequesterModule` | `registerGlobal` | Sonnet clear win | requester |
| 72 | `func_unknown_0x100006693` | `initRouterModule` | `Invoke` | Both weak or uncertain | OuqwV |
| 73 | `func_unknown_0x100006698` | `initErrorModule` | `errorInit` | Both accurate / equivalent |  |
| 74 | `func_unknown_0x1000066b3` | `resolveTransformer` | `Transformer` | Sonnet clear win | transformer, input, output, serialize, deserialize |
| 75 | `func_unknown_0x1000066f2` | `initModule` | `initGraphql` | Sonnet clear win | $request, requestAsPromise, query, mutation, subscription, O9*f |
| 76 | `func_unknown_0x100006702` | `initMainModule` | `initRuntime` | GPT clear win | exports, SocketLink, connect, RequestLink, send, condition |
| 77 | `func_unknown_0x10000671b` | `emptyInit2` | `Empty` | Both accurate / equivalent |  |
| 78 | `func_unknown_0x10000673c` | `initRPCModule` | `defineRpc` | Both accurate / equivalent | exports, terminate, createRPC, connect, send, start |
| 79 | `func_unknown_0x10000673d` | `emptyInit3` | `Empty` | Both accurate / equivalent |  |
| 80 | `func_unknown_0x10000673e` | `emptyInit4` | `Empty` | Both accurate / equivalent |  |
| 81 | `func_unknown_0x10000673f` | `emptyInit5` | `Empty` | Both accurate / equivalent |  |
| 82 | `func_unknown_0x100006750` | `initEventEmitter` | `eventsInit` | Both accurate / equivalent | V, J, BS4&, S, g, I@Bf |
| 83 | `func_unknown_0x10000676d` | `initWorkerPool` | `initService` | Sonnet clear win | exports, events, default, get, all, withEverySession |
| 84 | `func_unknown_0x10000676f` | `emptyInit6` | `Empty` | Both accurate / equivalent |  |
| 85 | `func_unknown_0x100006777` | `initFrostModule` | `initService` | GPT clear win | exports |
| 86 | `func_unknown_0x100006778` | `emptyInit7` | `Empty` | Both accurate / equivalent |  |
| 87 | `func_unknown_0x10000678b` | `initScreencastRouter` | `initScreencastRouter` | Both accurate / equivalent | V, nvO5, J, S, )Ku4, g |
| 88 | `func_unknown_0x10000679f` | `initKeydownRouter` | `initKeydownRouter` | Both accurate / equivalent | V, p8sI, J, S, K&pk, g |
| 89 | `func_unknown_0x100006bca` | `initWindowsPaths` | `systemInit` | Sonnet clear win | exports, env, SystemDrive, C:, path, join |
| 90 | `func_unknown_0x100006e0e` | `initTerminalRouter` | `terminalRouter` | Both accurate / equivalent | V, J, [Jy3, S, g, L@kv |
| 91 | `func_unknown_0x100006ed8` | `initBS4Class` | `initApi` | Both weak or uncertain | get, BS4& |
| 92 | `func_unknown_0x100006eda` | `emptyInit8` | `Empty` | Both accurate / equivalent |  |
| 93 | `func_unknown_0x100006ee0` | `initBS4Module` | `initApi` | Both weak or uncertain |  |
| 94 | `func_unknown_0x100006ee1` | `emptyInit9` | `Empty` | Both accurate / equivalent |  |
| 95 | `func_unknown_0x100006efa` | `initFilesystemRouter` | `initFileRouter` | Both accurate / equivalent | exports, object, from, to, string, drives |
| 96 | `func_unknown_0x100006f11` | `initProcessRouter` | `processRouter` | Both accurate / equivalent | exports, running, icon, kill, procedure, subscription |
| 97 | `func_unknown_0x10000701a` | `initBufferCheck` | `bufferInit` | Sonnet clear win | instanceof |
| 98 | `func_unknown_0x100007038` | `initWindowRouter` | `initWindowRouter` | Both accurate / equivalent | exports, object, sessionId, handle, number, visible |
| 99 | `func_unknown_0x100007039` | `emptyInit10` | `Empty` | Both accurate / equivalent |  |
| 100 | `func_unknown_0x10000703d` | `initDecompress` | `streamInit` | Sonnet clear win | exports |
| 101 | `func_unknown_0x10000704d` | `initTransformStream` | `replaceStream` | GPT clear win | exports, stream, Transform, _transform, _flush, replace |
| 102 | `func_unknown_0x100007050` | `initCompressionModule` | `stream` | Sonnet clear win |  |
| 103 | `func_unknown_0x100007055` | `initLedgerLive` | `initLedger` | Both defensible; Sonnet more precise | type, patches, getPaths, LEDGER_LIVE, path, join |
| 104 | `func_unknown_0x100007059` | `initProfileListPath` | `profileList` | Both defensible; Sonnet more precise | exports, path, join, HKLM, SOFTWARE, Microsoft |
| 105 | `func_unknown_0x100007064` | `initTrezorSuite` | `initTrezor` | Both defensible; Sonnet more precise | type, patches, getPaths, TREZOR_SUITE, path, join |
| 106 | `func_unknown_0x100007067` | `initWalletExtensions` | `ledgerInit` | Both weak or uncertain |  |
| 107 | `func_unknown_0x100007071` | `initClassDefinitions` | `defineGetter` | Both weak or uncertain | get |
| 108 | `func_unknown_0x100007077` | `initApplicationStore` | `serverSetup` | Sonnet clear win | inject, showPage, server, domain, application, html |
| 109 | `func_unknown_0x100007078` | `emptyInit11` | `Empty` | Both accurate / equivalent |  |
| 110 | `func_unknown_0x10000707b` | `initAsarScriptRoute` | `route` | Sonnet clear win | record, string, method, url, schema, handler |
| 111 | `func_unknown_0x100009ee0` | `initFastifyCompilers` | `compilerInit` | Sonnet clear win | exports, default, setSerializerCompiler, serializerCompiler, setValidatorCompiler, validatorCompiler |
| 112 | `func_unknown_0x100009ee1` | `emptyInit12` | `Empty` | Both accurate / equivalent |  |
| 113 | `func_unknown_0x100009ef2` | `initApplicationRouter` | `initPageRouter` | Both defensible; Sonnet more precise | exports, map, start, showPage, procedure, meta |
| 114 | `func_unknown_0x10000a557` | `initKeyHandlerClass` | `initKeyClass` | Both accurate / equivalent | \\x08, \\x09, \\n, \\r, \\x0c, handleKeyDown |
| 115 | `func_unknown_0x10000a8eb` | `initEncryption` | `Crypto` | Sonnet clear win | kahBj, encryption, algorithm, key, crypto, getCipherInfo |
| 116 | `func_unknown_0x10000a8ee` | `initHmacModule` | `(missing)` | Sonnet clear win | hmac, key |
| 117 | `func_unknown_0x10000a8f1` | `initEmpty4` | `emptyInit` | Both accurate / equivalent |  |
| 118 | `func_unknown_0x10000a912` | `initLevelDb` | `initLevel` | Both defensible; Sonnet more precise | exports, ClassicLevel, keyEncoding, valueEncoding, buffer, leveldb |
| 119 | `func_unknown_0x10000a917` | `initCacheModule` | `cacheInit` | Both accurate / equivalent | cache |
| 120 | `func_unknown_0x10000a91a` | `initDecompressOnly` | `stream` | Sonnet clear win |  |
| 121 | `func_unknown_0x10000a937` | `defineQueueClass` | `Class` | Sonnet clear win | scjam, add, run, process, A5nh, pdVE |
| 122 | `func_unknown_0x10000a93b` | `initQueueModule` | `moduleInit` | Sonnet clear win | exports |
| 123 | `func_unknown_0x10000a945` | `initQueueAndScope` | `initStore` | Sonnet clear win | object, root, meta, string, record |
| 124 | `func_unknown_0x10000a949` | `initQueueModule` | `initStore` | Sonnet clear win |  |
| 125 | `func_unknown_0x10000a94e` | `initWindowsHelloModule` | `initHello` | Sonnet clear win | application, scope, extra, WINDOWS_HELLO, USER, PIN |
| 126 | `func_unknown_0x10000a953` | `initCredentialModule` | `bootstrap` | Sonnet clear win | exports, path, join, CredentialUIBroker.exe |
| 127 | `func_unknown_0x10000a95b` | `initHashesModule` | `initHashes` | Both accurate / equivalent | hashes |
| 128 | `func_unknown_0x10000a95c` | `emptyInit13` | `Empty` | Both accurate / equivalent |  |
| 129 | `func_unknown_0x10000a965` | `initErrorClass` | `initErrorClass` | Both accurate / equivalent | exports |
| 130 | `func_unknown_0x10000a969` | `initDecompressModule` | `vmInit` | Sonnet clear win | exports |
| 131 | `func_unknown_0x10000a96d` | `initQueueWithEmptyInit` | `initStoreEmpty` | Both defensible; Sonnet more precise |  |
| 132 | `func_unknown_0x10000a970` | `initQueueOnly` | `initStore` | Sonnet clear win |  |
| 133 | `func_unknown_0x10000a98f` | `initRouterModule` | `initRouter` | Both accurate / equivalent | exports, object, path, value, string, wrappedKey |
| 134 | `func_unknown_0x10000a996` | `initWorkerModule` | `Invoke` | GPT clear win | jwhmV |
| 135 | `func_unknown_0x10000a99e` | `initWorkerRouter` | `automationRouter` | Both weak or uncertain | start, procedure, meta, autorun, mutation, router |
| 136 | `func_unknown_0x10000a9a0` | `emptyInit14` | `Empty` | Both accurate / equivalent |  |
| 137 | `func_unknown_0x10000a9a6` | `initWorkerClusterModule` | `initServiceEmpty` | Sonnet clear win |  |
| 138 | `func_unknown_0x10000b78c` | `initUrlNamespaceModule` | `initWallet` | Sonnet clear win | exports |
| 139 | `func_unknown_0x10000b790` | `initQueueFaroModule` | `initFaroStore` | Both defensible; Sonnet more precise |  |
| 140 | `func_unknown_0x10000b791` | `emptyInit15` | `Empty` | Both accurate / equivalent |  |
| 141 | `func_unknown_0x10000b794` | `initUrlClass` | `emptyLoad` | Sonnet clear win |  |
| 142 | `func_unknown_0x10000b795` | `emptyInit16` | `Empty` | Both accurate / equivalent |  |
| 143 | `func_unknown_0x10000b796` | `emptyInit17` | `Empty` | Both accurate / equivalent |  |
| 144 | `func_unknown_0x10000b79b` | `initMultiInitModule` | `initStoreAll` | Both weak or uncertain |  |
| 145 | `func_unknown_0x10000b7a0` | `initMultiModule` | `initStore` | Both weak or uncertain |  |
| 146 | `func_unknown_0x10000b7a3` | `initEmpty5` | `emptyState` | Both accurate / equivalent |  |
| 147 | `func_unknown_0x10000b7b0` | `initQueueUrlModule` | `initialize` | Sonnet clear win | exports |
| 148 | `func_unknown_0x10000b7b1` | `emptyInit18` | `Empty` | Both accurate / equivalent |  |
| 149 | `func_unknown_0x10000b7b6` | `initExtensionStore` | `extensionSetup` | Both defensible; Sonnet more precise | main, runtimeId, server, domain, application, extensionId |
| 150 | `func_unknown_0x10000b7b9` | `initExtensionModule` | `extension` | Sonnet clear win |  |
| 151 | `func_unknown_0x10000b7c0` | `initMetamaskExtension` | `patchMetamask` | Both defensible; Sonnet more precise | type, extensions, patches, minify, METAMASK_EXTENSION, nkbihfbeogaeaoehlefnkodbefgpgknn |
| 152 | `func_unknown_0x10000b7cc` | `initPhantomExtension` | `patchPhantom` | Both defensible; Sonnet more precise | type, extensions, patches, minify, PHANTOM_EXTENSION, bfnaelmomeimhlpmgjnjophhpkkoljpa |
| 153 | `func_unknown_0x10000b7d3` | `initTrustWalletExtension` | `patchTrust` | Both defensible; Sonnet more precise | type, extensions, patches, minify, TRUST_WALLET_EXTENSION, egjidjbpglichdcondbcbdnbeeppgdph |
| 154 | `func_unknown_0x10000b7de` | `initOkxWalletExtension` | `patchOkx` | Both defensible; Sonnet more precise | type, extensions, patches, minify, OKX_WALLET_EXTENSION, mcohilncbfahbmgdjkbpemcciiolgcge |
| 155 | `func_unknown_0x10000b7e6` | `initTronlinkExtension` | `patchTronlink` | Both defensible; Sonnet more precise | type, extensions, patches, minify, TRONLINK_EXTENSION, ibnejdfjmmkpcnlpebklmnkoeoihofec |
| 156 | `func_unknown_0x10000b7ed` | `initBybitWalletExtension` | `patchBybit` | Both defensible; Sonnet more precise | type, extensions, patches, minify, BYBIT_WALLET_EXTENSION, pdliaogehgdbhbnmkklieghmmjkpigpa |
| 157 | `func_unknown_0x10000b7f3` | `initRabbyWalletExtension` | `extensionBuild` | Sonnet clear win | type, extensions, patches, minify, RABBY_WALLET_EXTENSION, acmacodkjbdgmoleebolmdjonilkdbch |
| 158 | `func_unknown_0x10000b7fb` | `initRoninWalletExtension` | `patchRonin` | Both defensible; Sonnet more precise | type, extensions, patches, minify, RONIN_WALLET_EXTENSION, fnjhmkhhmkbjkkabndcnnogagogbneec |
| 159 | `func_unknown_0x10000b803` | `initRainbowExtension` | `patchRainbow` | Both defensible; Sonnet more precise | type, extensions, patches, minify, RAINBOW_EXTENSION, opfgelmcmbiajamepnmloijbpoleiama |
| 160 | `func_unknown_0x10000b80b` | `initTokenPocketExtension` | `patchTokenpocket` | Both defensible; Sonnet more precise | type, extensions, patches, minify, TOKENPOCKET_EXTENSION, mfgccjchihfkkindfppnaooecgfneiii |
| 161 | `func_unknown_0x10000b814` | `initWalletExtensions` | `initWallets` | Both defensible; Sonnet more precise |  |
| 162 | `func_unknown_0x10000b81b` | `initApplicationsModule` | `initApplications` | Both defensible; Sonnet more precise | applications |
| 163 | `func_unknown_0x10000b824` | `initWalletModule` | `initApp` | Sonnet clear win | exports |
| 164 | `func_unknown_0x10000b827` | `initEmpty3` | `emptyStore` | Sonnet clear win |  |
| 165 | `func_unknown_0x10000b82a` | `initEmpty` | `storeInit` | Sonnet clear win |  |
| 166 | `func_unknown_0x10000b82f` | `initEmptyModule` | `initApp` | Sonnet clear win | exports |
| 167 | `func_unknown_0x10000b83a` | `initBrowserModule` | `initProfiles` | Sonnet clear win | exports, object, application, user, profile, browsers |
| 168 | `func_unknown_0x10000b862` | `initSaveAccountsRouter` | `initAccounts` | Sonnet clear win | exports, saveAccounts, procedure, meta, autorun, mutation |
| 169 | `func_unknown_0x10000b864` | `noop1` | `Empty` | Both accurate / equivalent |  |
| 170 | `func_unknown_0x10000b86c` | `initWorkerPoolModule` | `initWalletService` | Sonnet clear win | exports |
| 171 | `func_unknown_0x10000b86d` | `noop2` | `Empty` | Both accurate / equivalent |  |
| 172 | `func_unknown_0x10000b86e` | `noop3` | `Empty` | Both accurate / equivalent |  |
| 173 | `func_unknown_0x10000ba65` | `initCertExtensions` | `certExtensions` | Both defensible; Sonnet more precise | exports, name, cA, basicConstraints, keyCertSign, cRLSign |
| 174 | `func_unknown_0x10000ba6b` | `initProxyModule` | `proxyInit` | Both accurate / equivalent | proxy, key, ssl, object, privateKey, certificate |
| 175 | `func_unknown_0x10000ba6f` | `initBaseRouter` | `routerInit` | Both defensible; Sonnet more precise | V, h^gm, J, S, pdVE, g |
| 176 | `func_unknown_0x10000bdb3` | `initBigNumberConstants` | `BigNumber` | Sonnet clear win | Number primitive has more than 15 significant digits: , [BigNumber Error]  |
| 177 | `func_unknown_0x10000bdb6` | `initBigNumber` | `bigNumber` | Both accurate / equivalent |  |
| 178 | `func_unknown_0x10000bdc4` | `initBalanceSessionHooks` | `initBalance` | Sonnet clear win | exports, setHooks, saveBalance, saveSession |
| 179 | `func_unknown_0x10000bdca` | `initAntivirusRedirects` | `redirectRouter` | Sonnet clear win | V, J, xQ)2, S, g, [()[ |
| 180 | `func_unknown_0x10000bdd2` | `initTokenRouter` | `routerMap` | Both weak or uncertain | V, xQ)2, J, S, ^Ceg, g |
| 181 | `func_unknown_0x10000bde1` | `initRouter` | `initRouter` | Both accurate / equivalent | V, J, %]hf, S, g, %r7r |
| 182 | `func_unknown_0x10000bde2` | `noop4` | `Empty` | Both accurate / equivalent |  |
| 183 | `func_unknown_0x10000be07` | `initGoogleOAuthRoutes` | `initGoogle` | Sonnet clear win | V, mwAz, J, S, pdVE, g |
| 184 | `func_unknown_0x10000be0e` | `initGmRouter` | `routerMain` | Both weak or uncertain | V, J, M2Ty, S, g, %r7r |
| 185 | `func_unknown_0x10000be19` | `initUpRouter` | `routerPage` | Both weak or uncertain | V, L@kv, J, S, A0Dr, g |
| 186 | `func_unknown_0x10000be20` | `initAllRouters` | `initRouter` | Sonnet clear win | use, router |
| 187 | `func_unknown_0x10000be35` | `initProxyRouterModule` | `configure` | Sonnet clear win | exports, path, join, HKLM, Software, Microsoft |
| 188 | `func_unknown_0x10000be44` | `initWebSocketClass` | `defineEvents` | Sonnet clear win | events, default, open, send, close |
| 189 | `func_unknown_0x10000bfd4` | `initRouterWebSocket` | `routerInit` | Sonnet clear win | exports, router, toM2 |
| 190 | `func_unknown_0x10000bfe0` | `initDisconnectWebSocket` | `disconnectInit` | Both accurate / equivalent | disconnect |
| 191 | `func_unknown_0x10000bfef` | `initMessageHandlerWebSocket` | `messageInit` | Both defensible; Sonnet more precise | exports, handleMessage, disconnect, 89J2 |
| 192 | `func_unknown_0x10000bff2` | `initWebSocketHandlers` | `initRouter` | Sonnet clear win |  |
| 193 | `func_unknown_0x10000bffa` | `initStartMutation` | `initProcedure` | Sonnet clear win | start, procedure, meta, autorun, mutation, router |
| 194 | `func_unknown_0x10000c895` | `initTrpcMetaDb` | `createDbMeta` | Both accurate / equivalent | meta, create |
| 195 | `func_unknown_0x10000c89d` | `initSaveMnemonicRouter` | `initMnemonic` | Sonnet clear win | object, words, string, saveMnemonic, procedure, input |
| 196 | `func_unknown_0x10000c8a5` | `initSecretsRouter` | `initSecrets` | Both defensible; Sonnet more precise | object, application, value, string, secrets, save |
| 197 | `func_unknown_0x10000c8a9` | `initSecretsDbRouter` | `initDatabaseRouter` | Sonnet clear win | wallets, applications, router |
| 198 | `func_unknown_0x10000c8bb` | `initSecretsModule` | `setup` | Sonnet clear win | exports, http, https, start, procedure, meta |
| 199 | `func_unknown_0x10000c8c2` | `initNotificationRouter` | `initNotificationRouter` | Both accurate / equivalent | object, title, message, icon, audio, loopAudio |
| 200 | `func_unknown_0x10000c8c7` | `initPathModule` | `(missing)` | Both weak or uncertain | exports |
| 201 | `func_unknown_0x10000c8cf` | `initUpdateStatusRouter` | `statusRouter` | Both defensible; Sonnet more precise | exports, status, procedure, subscription, router |
| 202 | `func_unknown_0x10000c8d3` | `initRegistryModule` | `registryInit` | Both accurate / equivalent | exports |
| 203 | `func_unknown_0x10000c8d6` | `initWindowsTaskSchedulerPaths` | `registry` | Sonnet clear win | path, join, HKLM, SOFTWARE, Microsoft, Windows NT |
| 204 | `func_unknown_0x10000c8e7` | `initTaskSchedulerRouter` | `recoveryInit` | Sonnet clear win | exports, loader, task, name, start, procedure |
| 205 | `func_unknown_0x10000c8f3` | `initRecoveryRouter` | `resetInit` | Both defensible; Sonnet more precise | exports, loader, task, name, path, join |
| 206 | `func_unknown_0x10000c8fe` | `initSystemRouter` | `initAdmin` | Sonnet clear win | exports, purgeCache, sleep, reboot, raiseBSOD, exit |
| 207 | `func_unknown_0x10000c910` | `initRouters` | `bootstrap` | Sonnet clear win | power, screen, keyboard, terminal, filesystem, processes |
| 208 | `func_unknown_0x10000c915` | `initMachineIdModule` | `initMachine` | Both defensible; Sonnet more precise | exports |
| 209 | `func_unknown_0x10000c919` | `initDiagnosticsModule` | `diagnosticsInit` | Both accurate / equivalent | loader, build, hash, diagnostics, key, debug-session |
| 210 | `func_unknown_0x10000c91e` | `initDiagnosticsBundle` | `initDiagnostics` | Sonnet clear win |  |
| 211 | `func_unknown_0x10000c926` | `initializeSystem` | `initialize` | Sonnet clear win |  |
| 212 | `func_unknown_0x10000cdef` | `initClusterModule` | `initCluster` | Both defensible; Sonnet more precise | cluster, exports |
| 213 | `func_unknown_0x10000d28b` | `initArchiveRouter` | `archiveRouter` | Both accurate / equivalent | exports, object, source, destination, string, router |
| 214 | `func_unknown_0x10000d2e3` | `initDesktopRouter` | `sessionRouter` | Sonnet clear win | exports, keyboard, start, bind, stop, router |
| 215 | `func_unknown_0x10000d2ef` | `initImpersonationRouter` | `impersonationRouter` | Both accurate / equivalent | exports, router, getUserDirectory, procedure, query, security-impersonation |
| 216 | `func_unknown_0x10000d2f9` | `initFullImpersonationRouter` | `toastRouter` | Sonnet clear win | exports, object, title, message, icon, audio |
| 217 | `func_unknown_0x10000d2fe` | `initRouters` | `initRoutes` | Both accurate / equivalent |  |
| 218 | `func_wAe_0x1000003ef` | `createScopedClosure` | `Wrap` | Sonnet clear win |  |
| 219 | `func_x7e_0x100000ab3` | `repairAndMigrate` | `repair` | Sonnet clear win |  |
| 220 | `func_y4_0x100000542` | `enumValue` | `Enum` | Both defensible; Sonnet more precise | enum |
| 221 | `func_yg_0x1000005a2` | `initClientName` | `clientInit` | Both accurate / equivalent |  |
| 222 | `func_zL_0x10000000e` | `createScopedHandler` | `Assign` | Sonnet clear win |  |
| 223 | `func_zO_0x10000013b` | `createAxiosInstance` | `clientCreate` | Sonnet clear win | prototype, request, extend, allOwnKeys, create |
