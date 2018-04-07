# trace

This is an "in context" trace tool, to provide indented
enter and exit lines plus properly indented Printf'd ones.

For example, 
```
begin main.main()
    begin main.startWebserver()
   |    begin main.imageHandler(&{GET /00000b30-bbc6-4315-9b0f-d003404105e3 HTTP/1.1 })
   |   |    begin imageServer.imager.GetSized(00000b30-bbc6-4315-9b0f-d003404105e3)
   |   |   |    begin imageServer.parseImageURL()
   |   |   |    tokens = [00000b30-bbc6-4315-9b0f-d003404105e3]
   |   |   |    returning bare key, [00000b30-bbc6-4315-9b0f-d003404105e3]
   |   |   |    end imageServer.parseImageURL
   |   |   |    begin cephInterface.S3Proto.Get(http://10.92.10.201:7480, 00000b30-bbc6-4315-9b0f-d003404105e3)
```

The package is instantiated with `var t = trace.New(os.Stderr, true)` for mormal output, and with `var t = trace.New(nil, false)` to suppress the output and 
reduce the overhead. The latter turns all the calls into no-ops.

Each function starts with a `defer t.Begin()()` call, which prints
"begin <function-name>" and any variables mentioned in the first set of 
parentheses and returns code to defer that prints the "end" message
when the function returns.

To print debugging lines, use `t.Print(string)` or `t.Printf(...)`.
