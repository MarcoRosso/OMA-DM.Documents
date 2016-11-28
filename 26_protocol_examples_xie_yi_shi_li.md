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
### 2.6.1.2 Package 2: Initialization from server to client 包2：从服务器到客户端的初始化
```
<SyncML xmlns='SYNCML:SYNCML1.2'>
  <SyncHdr>
     <VerDTD>1.2</VerDTD>
     <VerProto>DM/1.2</VerProto>
     <SessionID>1</SessionID>
     <MsgID>1</MsgID>
     <Target> 
         <LocURI>IMEI:493005100592800</LocURI>
     </Target>
     <Source>
        <LocURI>http://www.syncml.org/mgmt-server</LocURI>
     </Source>
     <Cred> <!-- Server credentials -->
       <Meta>
          <Type xmlns="syncml:metinf">syncml:auth-basic</Type>
          <Format xmlns='syncml:metinf'>b64</Format> </Meta>
          <Data><!-- base64 formatting of userid:password --></Data> 
      </Cred>
  </SyncHdr>
  <SyncBody>
    <Status>
       <MsgRef>1</MsgRef><CmdRef>0</CmdRef>
       <Cmd>SyncHdr</Cmd>
       <CmdID>6</CmdID>
       <TargetRef>http://www.syncml.org/mgmt-server</TargetRef> 
       <SourceRef>IMEI:493005100592800</SourceRef>
       <!-- Authenticated for the session -->
       <Data>212</Data>
    </Status>
    <Status>
      <MsgRef>1</MsgRef><CmdRef>1</CmdRef> 
      <CmdID>7</CmdID>
      <Cmd>Alert</Cmd> 
      <Data>200</Data><!-- OK -->
    </Status>
    <Status>
      <MsgRef>1</MsgRef><CmdRef>3</CmdRef>
      <CmdID>8</CmdID>
      <Cmd>Replace</Cmd> 
      <Data>200</Data><!-- OK -->
    </Status>
    <Sequence>
      <CmdID>1</CmdID>
      <Alert>
        <CmdID>2</CmdID>
        <Data>1101</Data> <!-- User confirmation required --> 
        <Item></Item>
        <Item>
          <Data>Do you want to add the CNN access point?</Data> 
        </Item>
      </Alert>
      <Replace>
        <CmdID>4</CmdID>
        <Meta>
          <Format xmlns="syncml:metinf">b64</Format> 
          <Type xmlns="syncml:metinf">
                application/vnd.wap.connectivity-wbxml </Type>
         </Meta>
         <Item>
            <!-- CNN WAP settings object in the settings -->
            <Target>
            <LocURI>./settings/wap_settings/CNN</LocURI> 
            </Target>
            <Data><!-- Base64-coded WAP connectivity document --></Data> 
         </Item>
       </Replace>
     </Sequence>
     <Final/>
  </SyncBody>
</SyncML>
```
 ### 2.6.1.3 Package 3: Client response 包3：客户端应答
 ```
<SyncML xmlns='SYNCML:SYNCML1.2'>
  <SyncHdr>
     <VerDTD>1.2</VerDTD>
     <VerProto>DM/1.2</VerProto>
     <SessionID>1</SessionID>
     <MsgID>2</MsgID>
     <Target> 
         <LocURI>http://www.syncml.org/mgmt-server</LocURI>
     </Target>
     <Source>
          <LocURI>IMEI:493005100592800</LocURI>
     </Source>
  </SyncHdr>
  <SyncBody>
     <Status>
       <MsgRef>1</MsgRef>
       <CmdID>1</CmdID>
       <CmdRef>0</CmdRef>
       <Cmd>SyncHdr</Cmd>
       <!-- SyncHdr accepted -->
       <Data>212</Data>
     </Status>
     <Status>
       <MsgRef>1</MsgRef>
       <CmdID>2</CmdID>
       <CmdRef>1</CmdRef>
       <Cmd>Sequence</Cmd>
       <!-- Sequence executed correctly -->
       <Data>200</Data>
     </Status>
     <Status>
       <MsgRef>1</MsgRef>
       <CmdRef>2</CmdRef> 
       <CmdID>3</CmdID>
       <Cmd>Alert</Cmd>
       <!-- OK, the user confirmed the action --> 
       <Data>200</Data>
     </Status>
     <Status>
       <MsgRef>1</MsgRef>
       <CmdRef>4</CmdRef>
       <CmdID>4</CmdID>
       <Cmd>Replace</Cmd> 
       <TargetRef>./settings/wap_settings/CNN</TargetRef> 
       <!-- OK, access point added -->
       <Data>200</Data>
     </Status>
     <Final/>
  </SyncBody> 
</SyncML>
```
 ### 2.6.1.4 Package 4: Acknowledgement of client status 确认客户状态
This package is now empty as no actions are sent and client does not continue the protocol.<br/>
此包现在为空，因为未发送任何操作，并且客户端不继续协议。
```
<SyncML xmlns='SYNCML:SYNCML1.2'>
  <SyncHdr>
     <VerDTD>1.2</VerDTD>
     <VerProto>DM/1.2</VerProto>
     <SessionID>1</SessionID>
     <MsgID>2</MsgID>
     <Target> 
       <LocURI>IMEI:493005100592800</LocURI>
     </Target>
     <Source>
       <LocURI>http://www.syncml.org/mgmt-server</LocURI> </Source>
  </SyncHdr>
<SyncBody>
     <Status>
       <MsgRef>2</MsgRef>
       <CmdID>1</CmdID>
       <CmdRef>0</CmdRef>
       <Cmd>SyncHdr</Cmd>
       <Data>200</Data>
      </Status>
     <Final/>
  </SyncBody>
</SyncML>
```
## 2.6.2 Two-step protocol initiated by the server 由服务器启动的两步协议

Operator initiates a regular antivirus software update on PDA clients. The server checks the installed version in the first management section then updates the antivirus data in the second step.<br/>
操作员在PDA客户端上启动常规防病毒软件更新。服务器在第一管理部分中检查已安装的版本，然后在第二步骤中更新防病毒数据。

 ### 2.6.2.1 Package 1: Initialization from client to server 包1:从客户端到服务器的初始化
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
    <Cred> <!-- Client credentials are optional --> 
      <Meta>
      <Type xmlns="syncml:metinf">syncml:auth-basic</Type>
      <Format xmlns='syncml:metinf'>b64</Format> 
      </Meta>
      <Data><!-- base64 formatting of userid:password --></Data>
    </Cred>
    <Meta><!-- Maximum message size for the client --> 
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
       <Data>US-en</Data>
     </Item>
    </Replace>
    <Final/>
  </SyncBody>
</SyncML>
 ```
  ### 2.6.2.2 Package 2: Initialization from server to client 包2:从服务器到客户端的初始化
```
<SyncML xmlns='SYNCML:SYNCML1.2'>
  <SyncHdr>
     <VerDTD>1.2</VerDTD>
     <VerProto>DM/1.2</VerProto>
     <SessionID>1</SessionID>
     <MsgID>1</MsgID>
     <Target> 
         <LocURI>IMEI:493005100592800</LocURI>
     </Target>
     <Source>
        <LocURI>http://www.syncml.org/mgmt-server</LocURI> 
     </Source>
     <Cred> <!-- Server credentials -->
       <Meta>
          <Type xmlns="syncml:metinf">syncml:auth-basic</Type>
          <Format xmlns='syncml:metinf'>b64</Format>
       </Meta>
       <Data><!-- base64 formatting of userid:password --></Data> 
     </Cred>
  </SyncHdr>
<SyncBody>
  <Status>
    <MsgRef>1</MsgRef><CmdRef>0</CmdRef>
    <Cmd>SyncHdr</Cmd>
    <CmdID>5</CmdID> 
    <TargetRef>http://www.syncml.org/mgmt-server</TargetRef> 
    <SourceRef>IMEI:493005100592800</SourceRef>
    <!-- Authenticated for the session -->
    <Data>212</Data>
  </Status>
  <Status>
      <MsgRef>1</MsgRef><CmdRef>1</CmdRef> 
      <CmdID>6</CmdID>
      <Cmd>Alert</Cmd> 
      <Data>200</Data><!-- OK -->
  </Status>
  <Status>
      <MsgRef>1</MsgRef><CmdRef>3</CmdRef> 
      <CmdID>7</CmdID>
      <Cmd>Replace</Cmd> 
      <Data>200</Data><!-- OK -->
  </Status>
  <Alert>
    <CmdID>2</CmdID>
    <Data>1100</Data> <!-- User displayable notification --> 
    <Item></Item>
    <Item>
      <Data>Your antivirus software is being updated</Data> 
    </Item>
    </Alert>
    <!-- Let's get the installed antivirus definition version number now -->
    <Get>
       <CmdID>4</CmdID>
       <Item>
       <Target>
           <LocURI>./antivirus_data/version</LocURI>
       </Target>
       </Item>
    </Get>
    <Final/>
  </SyncBody>
</SyncML>
```
  ### 2.6.2.3 Package 3: Client response 包3:客户端响应
```
<SyncML xmlns='SYNCML:SYNCML1.2'>
  <SyncHdr>
     <VerDTD>1.2</VerDTD>
     <VerProto>DM/1.2</VerProto>
     <SessionID>1</SessionID>
     <MsgID>2</MsgID>
     <Target> 
         <LocURI>http://www.syncml.org/mgmt-server</LocURI>
     </Target>
     <Source>
        <LocURI>IMEI:493005100592800</LocURI> </Source>
     </SyncHdr>
  <SyncBody>
    <Status>
      <MsgRef>1</MsgRef>
      <CmdID>1</CmdID>
      <Cmd>SyncHdr</Cmd>
      <Data>212</Data>
    </Status>
    <Status>
      <MsgRef>1</MsgRef>
      <CmdRef>2</CmdRef>
      <CmdID>2</CmdID>
      <Cmd>Alert</Cmd>
      <Data>200</Data><!-- User notification OK -->
    </Status>
    <Status>
      <MsgRef>1</MsgRef>
      <CmdRef>4</CmdRef>
      <CmdID>4</CmdID>
      <Cmd>Get</Cmd> 
      <TargetRef>./antivirus_data/version</TargetRef> 
      <Data>200</Data><!-- Get OK -->
    </Status>
    <!-- Results for the Get: antivirus version number --> 
    <Results>
      <MsgRef>1</MsgRef><CmdRef>4</CmdRef> 
      <CmdID>3</CmdID>
    <Item>
      <Source> 
      <LocURI>./antivirus_data/version</LocURI>
      </Source>
      <Data>antivirus-inc/20010522b/5</Data> 
    </Item>
    </Results>
    <Final/>
  </SyncBody>
</SyncML>
```
  ### 2.6.2.4 Package 4: Continue with management operations 包4:继续管理操作
```
<SyncML xmlns='SYNCML:SYNCML1.2'>
  <SyncHdr>
     <VerDTD>1.2</VerDTD>
     <VerProto>DM/1.2</VerProto>
     <SessionID>1</SessionID>
     <MsgID>2</MsgID>
     <Target>
     <LocURI>IMEI:493005100592800</LocURI>
     </Target>
     <Source> 
     <LocURI>http://www.syncml.org/mgmt-server</LocURI> 
     </Source>
  </SyncHdr>
<SyncBody>
     <Status>
       <MsgRef>2</MsgRef>
       <CmdID>1</CmdID>
       <Cmd>SyncHdr</Cmd>
       <Data>212</Data>
     </Status>
     <!-- Send now antivirus updates -->
     <Replace>
       <CmdID>2</CmdID>
       <Meta>
          <Format xmlns="syncml:metinf">b64</Format> 
          <Type xmlns="syncml:metinf">
application/antivirus-inc.virusdef 
          </Type>
       </Meta>
       <Item>
        <Target> 
           <LocURI>./antivirus_data</LocURI>
        </Target>
        <Data><!-- Base64-coded antivirus file --></Data> 
       </Item>
      </Replace>
     <Final/>
  </SyncBody>
</SyncML>

```
