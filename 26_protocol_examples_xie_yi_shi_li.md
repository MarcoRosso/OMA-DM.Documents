# 2.6 Protocol examples 协议示例
In this section several protocol scenarios will be demonstrated.<br/>
在本节中，将演示几个协议场景。

## 2.6.1 One-step protocol initiated by the server 由服务器启动的一步协议
In this section an example is presented in which a WAP connectivity context is added to the WAP settings. The user is asked to confirm whether the settings could be added.<br/>
在本节中，介绍了一个示例，WAP连接上下文添加到WAP设置。要求用户确认是否可以添加设置。

### 2.6.1.1 Package 1: Initialization from client to server 包1：从客户端到服务器的初始化
```
<SyncML xmlns='SYNCML:SYNCML1.2'>
  <SyncHdr>
     <VerDTD>1.2</VerDTD>
     <VerProto>DM/1.2</VerProto>
     <SessionID>1</SessionID>
     <MsgID>1</MsgID>
     <Target> 
       <LocURI>http://www.syncml.org/mgmt-server</LocURI>
     </Target>
     <Source>
       <LocURI>IMEI:493005100592800</LocURI>
     </Source>
     <Cred> <!-- Client credentials are mandatory if the transport layer is not providing authentication.-->
      <Meta>
        <Type xmlns="syncml:metinf">syncml:auth-basic</Type> 
        <Format xmlns='syncml:metinf'>b64</Format>
      </Meta>
      <Data>
        <!-- base64 formatting of userid:password --> </Data>
    </Cred>
    <Meta> <!-- Maximum message size for the client -->
      <MaxMsgSize xmlns="syncml:metinf">5000</MaxMsgSize> 
    </Meta>
 </SyncHdr>
<SyncBody>
  <Alert>
    <CmdID>1</CmdID>
    <Data>1200</Data> <!-- Server-initiated session -->
  </Alert>
  <Replace>
    <CmdID>3</CmdID>
    <Item>
        <Source><LocURI>./DevInfo/DevId</LocURI></Source> 
        <Meta>
          <Format xmlns='syncml:metinf'>chr</Format>
          <Type xmlns='syncml:metinf'>text/plain</Type> 
        </Meta>
        <Data>IMEI:493005100592800</Data> </Item>
    <Item> 
    <Source><LocURI>./DevInfo/Man</LocURI></Source>
    <Meta>
      <Format xmlns='syncml:metinf'>chr</Format> 
      <Type xmlns='syncml:metinf'>text/plain</Type>
    </Meta>
    <Data>Device Factory, Inc.</Data>
    </Item>
   <Item> 
      <Source><LocURI>./DevInfo/Mod</LocURI></Source>
      <Meta>
        <Format xmlns='syncml:metinf'>chr</Format>
        <Type xmlns='syncml:metinf'>text/plain</Type>
      </Meta>
        <Data>SmartPhone2000</Data>
   </Item>
   <Item> 
     <Source><LocURI>./DevInfo/DmV</LocURI></Source> 
     <Meta>
       <Format xmlns='syncml:metinf'>chr</Format>
      <Type xmlns='syncml:metinf'>text/plain</Type>
     </Meta>
     <Data>1.0.0.1</Data>
   </Item>
   <Item> 
      <Source><LocURI>./DevInfo/Lang</LocURI></Source>
      <Meta>
        <Format xmlns='syncml:metinf'>chr</Format>
        <Type xmlns='syncml:metinf'>text/plain</Type> 
      </Meta>
      <Data>en-US</Data>
       </Item>
    </Replace>
    <Final/>
  </SyncBody>
 </SyncML>

```