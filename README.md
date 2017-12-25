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
