# Security support when Management Trust and Content Trust are separated 管理信任和内容信任分开时的安全支持
## Content signing and encryption introduction 内容签名和加密介绍
There are situations when Management Trust and Content Trust need to be separated. The idea of the content signing and encryption is that the Device could identify the source of the Content even when the delivery is done by using some other Device Management Server. Also Content may be encrypted in a way that only the receiver is able to decrypt the Content. By Content, in this context, we mean data delivered inside of OMA DM messages `<Data>` elements. In this context the other Device Management Server means the Device Management Server, which is not controlled by the content creator or content source. Source of the signed or encrypted Content could be almost anything and most probably it does not know anything about the OMA DM protocol. This is why it must be possible to keep the coupling between the OMA DM-protocol and the Source of the Content as loose as possible.<br/>
有时管理信任和内容信任需要分开。内容签名和加密的想法是，即使使用其他设备管理服务器完成传送，设备也可以识别内容的源。此外，内容可以以仅接收方能够解密内容的方式来加密。内容一词，在本上下文中，指的是在OMA DM消息`<Data>`元素内传递的数据。在这种情况下，其他设备管理服务器意味着不受内容创建者或内容源控制的设备管理服务器。签名或加密的内容的源几乎可以是任何东西，并且很可能它不知道关于OMA DM协议的任何内容。这就是为什么必须尽可能保持OMA DM协议和内容源之间的耦合是松散的原因。

## Content Signature enabling Authenticity and Integrity 支持真实性和完整性的内容签名
XML-signature [XMLSIGN] offers the signature mechanism to achieve Authenticity and Integrity. Because the messaging between the Source of the Content and Device is not possible in most of the cases, we need to agree the mandatory algorithms beforehand. The algorithms that must be supported for Authenticity and Integrity are RSA and SHA-1 as specified in [XMLSIGN]. XML Signature has three ways of representing signature in a document viz: enveloping, enveloped and detached. Enveloped or enveloping signatures are over data within the same XML document as the signature; detached signatures are over data external to the signature element. The use of the “detached” signature is recommended. The format value used for XML-signature data is xml.<br/>
XML签名[XMLSIGN]提供了签名机制来实现真实性和完整性。因为在大多数情况下，内容源和设备之间互发消息是不可能的，我们需要事先同意强制性算法。真实性和完整性必须支持的算法是[XMLSIGN]中指定的RSA和SHA-1。 XML有三种方式在文档中表示签名：包络，包封和分离。包封或包络签名是与签名相同的XML文档内的数据; 分离的签名在签名元素外部的数据上。建议使用“分离”签名。用于XML签名数据的格式值为xml。

XML Signatures are applied to arbitrary digital content (data objects) via an indirection. Data objects are digested, the resulting value is placed in an element (with other information) and that element is then digested and cryptographically signed. XML digital signatures are represented by the Signature element which has the following structure (where "?" denotes zero or one occurrence; "+" denotes one or more occurrences; and "·" denotes zero or more occurrences):<br/>
XML签名通过间接方式应用于任意数字内容（数据对象）。数据对象进行摘要，并将结果值放置在一个元素（带有其他信息）中，然后对该元素进行摘要和加密签名。XML数字签名由Signature元素表示，其具有以下结构（其中“？”表示零或一次出现;“+”表示一次或多次出现;“·”表示零次或多次出现）：
```
<Signature ID?> 
  <SignedInfo>
    <CanonicalizationMethod/> 
    <SignatureMethod/> 
    (<Reference URI? >
        (<Transforms/>)? 
        <DigestMethod/> 
        <DigestValue/>
     </Reference>)+ 
  </SignedInfo>
  <SignatureValue/> 
  (<KeyInfo/>)? 
  (<Object ID?/>)*
</Signature>
```
Each resource to be signed has its own `<Reference>` element identified by the URI attribute.<br/>
每个要签名的资源都有自己的由URI属性标识的`<Reference>`元素。

Rules for XML-signature elements used for enveloping XML-signature [XMLSIGN] in OMA DM Content signature context:<br/>
用于在OMA DM中包含XML签名[XMLSIGN]的XML签名元素的规则内容签名上下文：

* Content (data), which is to be signed, should be placed after the signature element, if detached signature is being used. This is the recommended way to place the content. In this case the `<Reference>` element may not contain any URI attribute. In this case The Device must implicitly know the location of the Content<br/>
如果正在使用分离的签名，则要签名的内容（数据）应放在签名元素之后。这是推荐的放置内容的方式。在这种情况下，`<Reference>`元素可能不包含任何URI属性。在这种情况下，设备必须隐式地知道内容的位置。
* Content (data), which is to be signed, may be placed inside of `<Object>` element when enveloping signature is being used.<br/>
当使用包络签名时，要签名的内容（数据）可以放置在`<Object>`元素的内部。
* `<Object> `element must not contain any other elements than Content signed and `<Object>` element must not exist when detached signature is used.<br/>
`<Object>`元素不能包含除签名的内容之外的任何其他元素，当使用分离签名时，<Object>元素不能存在。
* `<Reference> `element may not contain any attributes.<br/>
`<Reference>`元素不能包含任何属性
* `<Reference>` element must have child elements `<Transforms>`, `<DigestMethod>` and `<DigestValue>` elements.<br/>
`<Reference>`元素必须具有子元素`<Transforms>`，`<DigestMethod>`和`<DigestValue>`元素。
* `<DigestValue>` element contents must be encoded using base64.<br/>
`<DigestValue>`元素内容必须使用base64编码。
* `<SignatureValue>` element contents must be encoded using base64.<br/>
`<SignatureValue>`元素内容必须使用base64编码。
* `<Transforms>` element must not have `<Xpath>` child element.<br/>
`<Transforms>`元素不能有`<Xpath>`子元素
* `<Signature> `element must be a child of `<Data>` element.<br/>
`<Signature>`元素必须是`<Data>`元素的子元素。
* `<KeyInfo>` may be included in `<Signature> `for receiver to verify signature.<br/>
`<KeyInfo>`可以包含在`<Signature>`中，以便接收方验证签名。
* The digest value (in `<DigestValue>`) is encrypted with sender’s private key to produce `<SignatureValue>`. The receiver then decrypts the signature with the sender’s public key (in KeyInfo/KeyValue) to produce digest value (which sender computed), This hash value is compared to the digest value computed by the receiver.<br/>
摘要值（在`<DigestValue>`中）使用发送者的私钥进行加密，以生成`<SignatureValue>`。然后，接收者用发送者的公共密钥（在KeyInfo/KeyValue中）解密签名以产生摘要值（发送者计算的）。将该散列值与由接收者计算的摘要值进行比较。

Example of OMA DM message with signed content (recommended, detached signature method):<br/>
具有签名内容的OMA DM消息的示例（推荐，分离签名方法）：

```
 <SyncML xmlns='SYNCML:SYNCML1.2'>
   <SyncHdr>
    ...
   </SyncHdr>
   <SyncBody>
    ... 
    <Replace>
    <CmdID>4</CmdID>
    <Meta>
      <Format xmlns="syncml:metinf">xml</Format>
      <Type xmlns="syncml:metinf">application/xml</Type> 
    </Meta>
    <Item>
      <Target>
        <LocURI>./my_mgmt_obj/file</LocURI> 
      </Target>
      <Data>
        <![CDATA[
        <Signature xmlns="http://www.w3.org/2000/09/xmldsig#">
           <SignedInfo>
             <CanonicalizationMethod
                  Algorithm="http://www.w3.org/2001/10/xml-exc-c14n#"/> 
                      <SignatureMethod
                      Algorithm="http://www.w3.org/2000/09/xmldsig#rsa- sha1"/>
                      <Reference>
                         <Transforms>
                         <Transform
                         Algorithm="http://www.w3.org/2001/10/xml-exc- c14n#"/>
                         </Transforms>
                         <DigestMethod
        Algorithm="http://www.w3.org/2000/09/xmldsig#sha1"/> 
            <DigestValue> LyLsF094hPi4wPU... </DigestValue>
                          </Reference>
                        </SignedInfo>
                        <SignatureValue>
                          Hp1ZkmFZ/2kQLXDJbchm5gK...
                        </SignatureValue>
                        <KeyInfo>
                            <KeyValue xmlns="http://www.w3.org/2000/09/xmldsig#"> ...
                          </KeyValue>
                        </KeyInfo>
</Signature>
]]> 
    MY_SIGNED_BINARY_OR_XML_CONTENT...
                    </Data>
                  </Item>
                </Replace>
             </SyncBody>
</SyncML>
```
Example of OMA DM message with signed content (enveloping signature method):<br/>
具有签名内容的OMA DM消息的示例（包络签名方法）：
```
 <SyncML xmlns='SYNCML:SYNCML1.2'>
   <SyncHdr>
   ...
   </SyncHdr>
   <SyncBody>
    ... 
    <Replace>
    <CmdID>4</CmdID>
    <Meta>
      <Format xmlns="syncml:metinf">xml</Format>
      <Type xmlns="syncml:metinf">application/xml</Type> 
    </Meta>
    <Item>
     <Target>
        <LocURI>./my_mgmt_obj/file</LocURI> 
     </Target>
    <Data>
      <![CDATA[
      <Signature xmlns="http://www.w3.org/2000/09/xmldsig#">
        <SignedInfo>
          <CanonicalizationMethod
              Algorithm="http://www.w3.org/2001/10/xml-exc-c14n#"/> 
          <SignatureMethod
              Algorithm="http://www.w3.org/2000/09/xmldsig#rsa-sha1"/>
      <Reference>
         <Transforms>
          <Transform
              Algorithm="http://www.w3.org/2001/10/xml-exc-c14n#"/>
         </Transforms>
         <DigestMethod

Algorithm="http://www.w3.org/2000/09/xmldsig#sha1"/> 
         <DigestValue> LyLsF094hPi4wPU... </DigestValue>
      </Reference>
     </SignedInfo>
    <SignatureValue>
       Hp1ZkmFZ/2kQLXDJbchm5gK...
    </SignatureValue>
    <KeyInfo>
        <KeyValue xmlns="http://www.w3.org/2000/09/xmldsig#"> 
        ...
        </KeyValue>
       </KeyInfo>
       <Object>
         ASDFASDFASDFASDG...
       </Object>
    </Signature>
    ]]> 
    </Data>
   </Item>
  </Replace>
 </SyncBody>
</SyncML>
```
Example of OMA DM message with signed content (enveloped signature method):<br/>
具有签名内容的OMA DM消息的示例（包封签名方法）：
```
 <SyncML xmlns='SYNCML:SYNCML1.2'>
   <SyncHdr>
   ...
   </SyncHdr>
   <SyncBody>
   ... 
    <Replace>
    <CmdID>4</CmdID>
    <Meta>
      <Format xmlns="syncml:metinf">xml</Format>
      <Type xmlns="syncml:metinf">application/xml</Type> 
    </Meta>
    <Item>
      <Target>
        <LocURI>./my_mgmt_obj/file</LocURI> 
      </Target>
      <Data>
      <![CDATA[
      <MyObject ID=MY_ID>
         <MY_XML_CONTENT_HEADER />
         <MY_XML_CONTENT_DATA />
      </MyObject>
      <Signature xmlns="http://www.w3.org/2000/09/xmldsig#">
        <SignedInfo>
           <CanonicalizationMethod
                Algorithm="http://www.w3.org/2001/10/xml-exc-c14n#"/> 
           <SignatureMethod
                Algorithm="http://www.w3.org/2000/09/xmldsig#rsa-sha1"/>
           <Reference>
              <Transforms>
                  <Transform 
                  Algorithm="http://www.w3.org/2001/10/xml-exc-
c14n#"/>
              </Transforms>
              <DigestMethod
                      Algorithm="http://www.w3.org/2000/09/xmldsig#sha1"/> 
              <DigestValue> LyLsF094hPi4wPU... </DigestValue>
             </Reference URI=”#MY_ID”>
             </SignedInfo>
             <SignatureValue>
               Hp1ZkmFZ/2kQLXDJbchm5gK...
             </SignatureValue>
             <KeyInfo>
                 <KeyValue xmlns="http://www.w3.org/2000/09/xmldsig#"> 
                  ...
                 </KeyValue>
             </KeyInfo>
             </Signature>
]]> 
            </Data>
           </Item>
         </Replace>
       </SyncBody>
     </SyncML>
```




