[Link](https://help.aliyun.com/zh/cdn/user-guide/object-chunking)


![image](https://github.com/user-attachments/assets/6e4ae90c-0253-4274-a5d0-6f033c615560)

Range回源，指CDN节点在回源的HTTP请求里面携带了Range信息，源站在收到CDN节点的回源请求时，根据HTTP请求头中的Range信息返回指定范围的内容数据给CDN节点。Range回源可有效提高文件分发效率，减少回源流量消耗和源站压力，并且提升资源响应速度

## 注意事项
### 开启Range回源有以下注意事项：

开启Range回源前需确认源站是否支持Range请求，即HTTP请求头中包含Range字段，并且源站能够响应正确的206文件分片。如果源站不支持Range请求，开启Range回源可能导致缓存异常或客户端请求失败。

Range回源是可选配置项，CDN控制台默认未开启。

Multipart Ranges特性状态默认关闭，开启Range回源功能也不会同步开启Multipart Ranges特性，请提交工单申请开启Multipart Ranges特性。

开启Range回源功能以后，会导致回源的QPS升高，如果源站有设置频次控制功能，需要注意避免触发源站的限流；规避办法是通过DescribeL2VipsByDomain查询CDN回源节点的IP地址 ，并且将CDN回源节点的IP加入源站的访问IP白名单。
