# Music_Songs

Popular Uploaded Songs
package org.sambasoft;

import java.io.IOException;
import java.nio.ByteBuffer;

import javax.websocket.OnClose;
import javax.websocket.OnMessage;
import javax.websocket.OnOpen;
import javax.websocket.Session;
import javax.websocket.server.ServerEndpoint;


  // Here is the url that the client will use to connect to the websock, that is what wsServer means here, the websocket server url        
// Here, we are also turnung a java class into a server, which the annotation @ServerEndpoint helps to do
 //@ServerEndpoint(value="/wsServer")

@ServerEndpoint(value="/wsServer")

public class WsServer {
	
	
	
	@OnOpen
	public void OnOpen(Session session) {
		System.out.println(session.toString()); 
		alert('Open');
	}
	
	@OnMessage
	public void onMessage(Session ss,byte[] img) {
		alert('Message Loaded');
		ByteBuffer buf = ByteBuffer.wrap(img);
		try {
			ss.getBasicRemote().sendBinary(buf);
		} catch (IOException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}
	}
	
	@OnClose
	public void onClose(Session ss) {
		try {
			ss.close();
		} catch (IOException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}
	}
	
	
	
	
	
	

} // End WsServer Class
