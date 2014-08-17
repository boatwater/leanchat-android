#奇遇

一个展示AVOS聊天功能的Demo 

![img](https://github.com/lzwjava/Adventure/blob/master/readme/shot1.png)

总的来说，四步加聊天功能：

1. open session
2. watch peerIds
3. send message
4. handle received message

## Open session with empty peers

```java
final String selfId = getPeerId(curUser);
List<String> peerIds = new LinkedList<String>();
Session session = SessionManager.getInstance(selfId);
session.open(selfId, peerIds);
```

## Watch peers when need

```java
String selfId = getPeerId(User.curUser());
Session session = SessionManager.getInstance(selfId);
session.watchPeers(peerIds);
```
## Send message to peer

```java
List<String> ids = new ArrayList<String>();
ids.add(getPeerId(chatUser));
String selfId = getPeerId(curUser)
Session session = SessionManager.getInstance(selfId);
session.sendMessage(json, ids);
```

## Handle everything
接受消息继承一个类就可以了，这里能做到非常细粒度的控制又很方便，

```java
public class Re extends AVMessageReceiver {

  //session打开后调用
  @Override  
  public void onSessionOpen(Context context, Session session) {
  }

  //因断网session暂停时调用
  @Override
  public void onSessionPaused(Context context, Session session) {
  }

  //网络重新连接上时调用
  @Override
  public void onSessionResumed(Context context, Session session) {
  }

  //接受消息
  @Override
  public void onMessage(Context context, Session session, String msg, String fromPeerId) {
  }

  //消息发送成功
  @Override
  public void onMessageSent(Context context, Session session, String msg, List<String> receivers) {
  }

  //消息发送失败
  @Override
  public void onMessageFailure(Context context, Session session, String msg, List<String> receivers) {
  }

  //上线通知
  @Override
  public void onStatusOnline(Context context, Session session, List<String> peerIds) {
  }

  //下线通知
  @Override
  public void onStatusOffline(Context context, Session session, List<String> peerIds) {
  }

  //出错时调用
  @Override
  public void onError(Context context, Session session, Throwable e) {
  }
}
```
