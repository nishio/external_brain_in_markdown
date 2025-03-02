
> Expose "passive" boolean in the EventListenerOptions dictionary.
>
>  Implement the behaviour with respect to dispatching passive EventListeners so that calling preventDefault inside executing the passive registered callback only generates a warning to the console.  Can be used to dramatically improve scrolling performance.
[https://www.chromestatus.com/feature/5745543795965952](https://www.chromestatus.com/feature/5745543795965952)


