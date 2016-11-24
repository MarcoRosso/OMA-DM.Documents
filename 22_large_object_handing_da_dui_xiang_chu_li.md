# 2.2 Large Object Handing 大对象处理
The protocol provides a means to synchronize an object whose size exceeds that which can be transmitted within one message. This is achieved by splitting the object into chunks that will fit within the message and using the `<MoreData/>` element to signal to the recipient that the data item is incomplete and has further chunks to come.<br/>
协议提供了同步其大小超过可在一个消息内传输的对象的方法。这是通过将对象分割成适合消息内的块并使用“MoreData”元素向接收者发信号通知数据项不完整并且具有更多块来实现的。

Clients SHOULD support Large Objects and servers MUST support Large Objects.<br/>
客户端推荐支持大对象，服务器必须支持大对象。

On receipt of a data object with the `<MoreData/>` element, the recipient MUST respond with a status response “213 – Chunked item accepted and buffered” and, if there are no other commands to be sent, ask for the next message using the Alert 1222 mechanism defined in section 2.1. <br/>

在接收到具有`<MoreData/>`元素的数据对象时，接收者必须用状态响应“213-Chunked item accepted and buffered”进行响应，并且如果没有其他命令要发送，则使用在第2.1节中定义的警报1222机制。

On receipt of the last chunk of the data object the recipient reconstructs the data object from its constituent chunks and applies the requested command. The appropriate status MUST then be sent to the originator. A command on a chunked object MUST implicitly be treated as atomic; i.e. the recipient can only commit the object once all chunks have been successfully received and reassembled.<br/>
在接收到数据对象的最后一个块时，接收者从其组成的块重构数据对象并应用所请求的命令。然后必须将适当的状态发送给始发者。分块对象上的命令必须隐式地被视为原子；即一旦所有块已被成功接收和重新组装，接收方只能提交对象。

Data objects that fit within a single message MUST NOT be followed by the `<MoreData/>`element. Data objects that span multiple messages MUST have the `<MoreData/>`element after all chunks except the last chunk.<br/>
适合单个消息中的数据对象不得后跟`<MoreData/>`元素。跨越多个消息的数据对象必须在除了最后一个块之外的所有块之后具有`<MoreData/>`元素。

A new data object MUST NOT be added by a sender to any message until the previous data object has been completed. If a data object is chunked across multiple messages the chunks MUST be sent in contiguous messages. New DM commands (i.e. Add, Replace, Delete, Copy, Atomic or Sequence) or new Items MUST NOT be placed between chunks of a data object.<br/>
发送方不得向任何消息添加新的数据对象，直到前一个数据对象完成为止。如果数据对象跨多个消息分块，则块必须在连续消息中发送。新的DM命令（即添加，替换，删除，复制，原子或序列）或新项必须不放置在数据对象的块之间。

Meta and Item information SHOULD be repeated on each subsequent message containing chunks of the same data object. Authentication details related to the data object MAY vary between messages bearing chunks of the same data object as defined in the section 9.<br/>
元和项信息推荐在包含相同数据对象的块的每个后续消息上重复。与数据对象相关的认证详细信息可能会与在第2.4节中定义的相同数据对象的承载块的消息之间有所不同。

Clients that support Large Object Handling MUST indicate this by having the value of the DevDetail/LrgObj flag set to "true". The MaxObjSize accepted by the sender MAY be included in Meta information for the message header (SyncHdr) sent to the other party. MaxObjSize information sent in Meta information for the SyncHdr MUST be respected by the recipient, who MUST NOT send any single object larger than this size. If MaxObjSize is not sent, the recipient is free to send objects of any size back to the sender.<br/>
支持大对象处理的客户端必须通过将DevDetail/LrgObj标志的值设置为“true”来指示这一点。由发送方接受的MaxObjSize可以被包括在发送给另一方的消息报头（SyncHdr）的Meta信息中。在SyncHdr的Meta信息中发送的MaxObjSize信息必须由收件人遵守，收件人不得发送大于此大小的任何单个对象。如果未发送MaxObjSize，则收件人可以自由地将任何大小的对象发送回发件人。

Note that the MaxObjSize remains in effect for the entire DM session, unless a new value is supplied in a subsequent message. A possible reason to send a new MaxObjSize in a later message in the same session might be that the MaxObjSize of a client might depend on free memory, which can decrease as objects are created and increase as objects are deleted. The MaxObjSize need not be a dynamic quantity, however.<br/>
请注意，MaxObjSize对整个DM会话保持有效，除非在后续消息中提供了新值。在同一会话中的后续消息中发送新的MaxObjSize的可能原因可能是客户端的MaxObjSize可能依赖于可用内存，随着对象被创建而减少并随着对象被删除而增加。但是，MaxObjSize不必是动态的。

If an item is chunked across multiple messages, the `<Size>` element of the Meta information MUST be used to signal to the recipient the overall size of the data object. The `<Size>` element MUST only be specified in the first chunk of the item.<br/>
  如果一个项目跨多个消息分块，Meta信息的`<Size>`元素必须用于向接收者发送数据对象的整体大小。 `<Size>`元素必须只在项目的第一个块中指定。

On receipt of the last chunk, the recipient MUST validate that the size of re-constituted chunks match the object `<Size>` supplied in the Meta information by the sender. If the size does not match then error status 424 – “Size mismatch”. The recipient MUST NOT commit the command. The sender MAY attempt to retransmit the entire data object.<br/>
  在接收到最后一个块时，接收者必须验证重构的块的大小与发送者在Meta信息中提供的对象`<Size>`相匹配。如果大小不匹配，则错误状态为424-“Size mismatch”。接收者必须不提交命令。发送者可以尝试重新传输整个数据对象。

If the recipient detects a new data object or command before the previous item has been completed (by the chunk without the `<MoreData/> `Element), the recipient MUST respond with an Alert 1225 – “End of Data for chunked object not received”. The Alert SHOULD contain the source and/or target information from the original command to enable the sender to identify the failed command. Note: a Status would not suffice here because there would not necessarily be a command ID to refer to. The recipient MUST NOT commit the command. The sender MAY attempt to retransmit the entire data object.<br/>
如果接收者在上一个项目完成之前检测到新的数据对象或命令（由没有`<MoreData/>`元素的块），则接收者必须用警报1225-“End of Data for chunked object not received”来响应。警报应该包含来自原始命令的源和/或目标信息，以使发送者能够识别失败的命令。注意：状态在这里不会满足，因为不一定有要引用的命令ID。接收者必须不提交命令。发送方可以尝试重新传输整个数据对象。
