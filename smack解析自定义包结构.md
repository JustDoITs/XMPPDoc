#smack解析自定义的包结构

by Rusher 2013-05-16

## 背景

XMPP发展这么多年来，积累了很多的扩展协议，涉及到方方面面。尽管如此，有时候，还是需要自定义协议内容来满足业务上的需求。例如：

在聊天应用中，需要发送不同类型的消息，如文字消息，图片消息，声音消息等等。每一种消息除了有公用的属性外，还有一些自己的属性，例如图片消息，需要发送图片上传到的URL，图片的尺寸，图片的大小等等，而声音消息可能会带上音频文件的格式，以及长短等等,解决方案如下


	<message type="chat" to="robota@openfire.irusher.com" from="robotb@openfire.irusher.com/c3f953be" id="13051615553429">
	  <body/>
	  <params xmlns="yl:xmpp:params">
	    <param name="url">some_url</param>
	    <param name="width">100</param>
	    <param name="height">200</param>
	  </params>
	</message>

对于smack来说，body,thread,subject,error,properties 之外的子元素，都需要用提供包扩展来指定解析。

## Smack的提供者架构：包扩展(Packet Extensions)与自定义IQ

Smack的提供者架构是一种模块化的机制，包括为解析自定义包结构而定义的包扩展和自定义IQ包。Smack扩展协议所用的正式提供者架构。现有的两种提供者：

* **IQProvider**: 解析IQ包，封装成Java对象；
* **PacketExtension**: 解析XML子文档，封装到PacketExtension对象，然后赋给包对象。


### IQProvider

默认的，Smack只知道子包的命名空间是下面列表中的IQ包：

* jabber:iq:auth
* jabber:iq:roster
* jabber:iq:register

由于XMPP和扩展协议中还有很多其他类型的IQ,所以需要一种灵活的解析机制。注册IQ提供者有两种方式：通过程序注册；在Jar包的META-INF目录添加*smack.providers*文件。文件是一个XML文件，可以包含若干个iqProvider项，格式如下：

	<?xml version="1.0"?>
	 <smackProviders>
	     <iqProvider>
	         <elementName>query</elementName>
	         <namespace>jabber:iq:time</namespace>
	         <className>org.jivesoftware.smack.packet.Time</className>
	     </iqProvider>
	 </smackProviders>

每个IQ提供者对应一个元素名称和一个命名空间。上面的例子中，元素名称是'query',命名空间是'jabber:iq:time'。如果有出现重名，则使用先注册的。

IQ提供者类可以实现`IQProvider`接口，或者继承`IQ`类。实现`IQProvider`接口时，每个`IQProvider`负责解析原始的XML流，然后创建`IQ`对象；如果继承`IQ`类，


### PacketExtensionProvider