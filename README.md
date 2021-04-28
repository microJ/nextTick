# nextTick

process.nextTick in Browser.

## polyfill order

process.nextTick is MicroTask. so we first choose MicroTask API `Promise` and `MutationObserver` rather than MacroTask API.

1. Promise

   Morden browser

2. MutationObserver

   IE 11

3. MessageChannel

   IE 10

4. onreadystatechange

   IE 6~10

## why not use these

**postMessage**:

support IE 10~11.

don't work well in web worker. [api doc](https://developer.mozilla.org/en-US/docs/Web/API/DedicatedWorkerGlobalScope/postMessage)

**setImmediate**:

support IE 10~11.

but there is a bug: [broken on IE 10.](https://codeforhire.com/2013/09/21/setimmediate-and-messagechannel-broken-on-internet-explorer-10/)

**setTimeout**:

support IE 6+.

1. browser maybe limit min timeout 1ms.
2. [Timers can be nested; after five such nested timers, however, the interval is forced to be at least four milliseconds.](https://html.spec.whatwg.org/multipage/timers-and-user-prompts.html#timers)
